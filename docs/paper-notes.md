# Notes on the study

These notes summarize the paper behind this skill, and show how each rule in [SKILL.md](../SKILL.md) follows from it.

> Thomas Hikaru Clark (New York University), Matias B. Martin, and Kyle Mahowald (The University of Texas at Austin). 2026. *Why is AI-generated language so hard to understand?* arXiv:2610.29162 [cs.CL], version 1, 21 October 2026. Licensed CC BY 4.0. https://arxiv.org/abs/2610.29162

## The question

Many readers feel that text from recent AI models has become harder to understand. The authors test two hypotheses:

- **H1.** The output of frontier and near-frontier models overuses linguistic features that are linked to comprehension difficulty in people.
- **H2.** Pressure toward information density during post-training makes the output of models less humanlike.

They find support for both.

## The features they measured

Psycholinguistic research links each of these features to slower or harder reading. For each one, the authors also explain why a push to pack information into fewer tokens might favor it.

| Feature | Example | Why it is hard for people | Why compression might favor it |
| --- | --- | --- | --- |
| Rare word pairs and high n-gram perplexity | "verified red", "reader-patience budget" | Unpredictable words take longer to read (Hale 2001; Levy 2008; Smith and Levy 2013). | Common, predictable words carry little information, so a dense writer skips them. |
| Long dependencies | "The guitar sitting in the corner because you're still 'deciding' teaches you zero chords." | Related words that sit far apart strain working memory (Gibson 1998, 2000), and people tend to avoid them (Futrell et al. 2015). | Not argued separately. |
| Object relatives, with and without "that" | "the behaviour (that) the old code never reached" | They are harder than subject relatives, partly because of word order and longer dependencies (Staub 2010). | They are shorter than the passive alternative, and leaving out "that" saves another word. |
| Stacked nouns (three or more) | "class-time shutdown requirement" | The grouping is ambiguous ("Squad Helps Dog Bite Victim"), and new compounds slow reading (Staub et al. 2007). | A stack packs a specific meaning into few words. |
| Nouns used as verbs | "calendar it" | The change of word class makes readers reanalyze the sentence (Thierry et al. 2008). | "Calendar it" is shorter than "put it on your calendar". |
| Inanimate subjects with verbs that need a person | "`is_file()` swallows that" | Readers use animacy to parse, and a mismatch triggers reanalysis (Trueswell et al. 1994; Kim and Osterhout 2005). | "Bites" can stand in for "causes an issue". |

The authors find all of these by parsing the text with spaCy. For nouns used as verbs and for inanimate subjects, an automated classifier then judges each candidate.

## The data

- **Models.** Fourteen in total. The nine frontier or near-frontier models were Claude Sonnet 5, Claude Opus 5, Claude Opus 5.5, Claude Fable 5, GPT-5.6 Luna, Terra, and Sol, GLM-5, and Kimi K2.5. The five smaller open models were Llama 3.1 8B (base and Instruct) and Olmo 3 7B (base, Instruct, and Think). All models ran under the same agent harness and the same prompts.
- **Chat.** Ten conversation topics, 12 turns each, with a simulated user, for 120 conversations and 1,428 replies.
- **Coding.** Each frontier model was asked to find and fix bugs in five real GitHub repositories, for 45 sessions in total. Only the last message of each turn was analyzed, which is usually a summary of the work.
- **Essays.** Seven assignments from the PERSUADE 2.0 corpus, ten essays per model per assignment, for 980 essays. The human comparison was 2,934 student essays with high scores on the same assignments.
- **Human baselines.** OpenSubtitles for chat, StackExchange for coding, the student essays for essays, and Wikipedia.

The whole collection cost $251.19 in API fees.

## The method: paraphrase by round-trip translation

To separate a model's choice of wording from what it means, the authors translated every sentence into Japanese and back into English with NLLB-200. Translation keeps the meaning and replaces the wording with more common forms. If a feature becomes rarer after the round trip, the model chose it over an available alternative. They repeated the check with a Russian pivot and with a second translator.

## What they found (H1)

- **Compared with paraphrases of the same content,** frontier models overused rare word pairs, nouns used as verbs, inanimate subjects, and object relatives without "that". They underused object relatives with "that", which suggests a preference for skipping optional words. In chat and coding, the same held for stacked nouns and dependency length, but not in the essays.
- **Compared with human writing,** all nine frontier models used more inanimate subjects with verbs that need a person, and more rare word sequences. In conversation, most also used longer dependencies, more stacked nouns, and more object relatives without "that".
- **The setting matters.** The effects were smaller in single essays than in multi-turn chat and coding. The authors suggest that long back-and-forth exchanges may push models toward compression.
- **The model matters.** The Llama models changed least under the round trip, and so did the base and instruction-tuned Olmo models. Olmo Think, a reasoning model, looked like the frontier models: within the Olmo family, the effects grew from the base model to the instruction-tuned model to the reasoning model. Claude Opus 5.5 scored lower than Claude Opus 5 on 19 of 21 comparisons of the difficulty measures.

## The mechanism (H2)

The authors fine-tuned a small open model (Qwen2.5-1.5B-Instruct) with reinforcement learning (GRPO). Its task was to turn a structured event description into one English sentence. The reward was correctness minus a penalty for each token. Every event could be expressed with either form of a short-or-long choice, for example "He sent us a photo" or "He sent a photo to us".

- The more the training penalized length, the more often the model chose the shorter form.
- Without a constraint that kept it close to the original model, any length penalty drove every run to choose the short form almost always. For the two trained "that" constructions, the short form appeared more than 98 percent of the time.
- The preference spread to "that" constructions that the model never saw in training, "sure (that)" and "so (that)". Among four unrelated constructions, only the genitive shifted, and only without the constraint.
- People use both forms and choose by context. For example, they include an optional "that" more often when what follows is harder to predict (Levy and Jaeger 2007; Jaeger 2010).

The authors' interpretation: training with verifiable rewards scores whether an answer is correct, not whether a person can follow it. Training on human feedback tends to reward longer outputs (Singhal et al. 2024), so the pressure toward compression is more plausibly tied to verifiable rewards. Models may drift toward a dialect that is good for packing information densely but hard for people to read. The authors add that models can also be rewarded for communicating well, and that Claude Opus 5.5 shows a measurable improvement over Claude Opus 5.

## Limitations

The authors list these:

- They studied a subset of models, only in English, with a limited number of chat topics and code repositories.
- Proving the cause in frontier models would require studying them during post-training, which is not feasible at scale, so they rely on proxies.
- Limited compute constrained the post-training experiment.

Two more points matter when you turn the findings into writing advice:

- The study measured features that earlier research links to difficulty. It did not test how quickly or how well people understood the AI-generated text itself.
- The findings are statistical. A single object relative without "that" is not a mistake. The pattern becomes a problem when a writer chooses the dense form every time.

## From the study to the skill

| Study feature or finding | Rule in SKILL.md |
| --- | --- |
| Long dependencies | 1. Keep each subject close to its verb |
| Stacked nouns | 2. Don't stack nouns |
| Object relatives without "that" | 3. Mark relative clauses |
| Optional words dropped under a length penalty | 4. Keep the small words that show structure |
| Nouns used as verbs | 5. Use ordinary verbs |
| Inanimate subjects with verbs that need a person | 6. Give human actions to people |
| Rare word pairs | 7. Use common words in their usual combinations |
| Information density in the background research | 8. Give each sentence one main idea |
| Stronger effects in long chats and coding sessions | "When to take extra care" |
| People choose between forms by context | "Don't overcorrect" |
