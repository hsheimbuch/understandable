# Constructions that slow readers down

This file expands the eight rules in SKILL.md. Read it before a `check` or a file rewrite.

Each section says what to look for, why it slows readers down, what the study found, how to fix it, and when to leave it alone. Examples marked "study" are quoted from Clark, Martin, and Mahowald (2026), mostly from Table 2 and Figure 1, with the model and setting in brackets. The paper is licensed CC BY 4.0. The rewrites are ours, and they keep to what each sentence says, because the surrounding conversation is not in the paper.

## Contents

1. [Subject far from its verb](#1-subject-far-from-its-verb)
2. [Stacked nouns](#2-stacked-nouns)
3. [Object relatives without "that"](#3-object-relatives-without-that)
4. [Dropped structure words](#4-dropped-structure-words)
5. [Nouns used as verbs](#5-nouns-used-as-verbs)
6. [Things that act like people](#6-things-that-act-like-people)
7. [Rare word pairs and coinages](#7-rare-word-pairs-and-coinages)
8. [Too much in one sentence](#8-too-much-in-one-sentence)
9. [Short and long forms: how people choose](#short-and-long-forms-how-people-choose)
10. [Where the problem is worst](#where-the-problem-is-worst)
11. [A worked example](#a-worked-example)
12. [Sources](#sources)

## 1. Subject far from its verb

**What to look for.** Many words between a subject and its verb, or between a verb and its object. Common causes:

- a long modifier after the subject,
- a list or a dash-enclosed aside after the subject,
- a relative clause inside the subject,
- a long run of modifiers before a noun.

**Why it slows readers down.** Readers keep the subject in working memory until its verb arrives, and that memory fades with distance (Gibson 1998, 2000). Across 37 languages, people order words so that related words sit close together (Futrell, Mahowald, and Gibson 2015).

**What the study found.** In conversation, most frontier models produced longer dependencies than human writing. In chat and coding, they also produced longer ones than paraphrases of their own text. The essays did not show this effect.

**How to fix it.**

- Move a long modifier after the verb, or give it its own sentence.
- Put a list at the end of the sentence, after a colon.
- Start with a short subject. If the condition is long, make it an opening clause: "When X happens, Y..."
- Put the heaviest phrase last.

**Examples.**

- Hard: "The guitar sitting in the corner because you're still 'deciding' teaches you zero chords." (study: Claude Sonnet 5, chat)
- Clear: "You won't learn any chords while the guitar sits in the corner and you keep 'deciding'."

- Hard: "All five expression shapes — attribute access, subscript, calls, nested calls, string literals — leave `current` on `NAME('b')`, and the full template renders correctly." (study: Claude Fable 5, coding)
- Clear: "All five kinds of expression leave `current` on `NAME('b')`: attribute access, subscripts, calls, nested calls, and string literals. The full template renders correctly."

- Hard: "A lattice constructed with duplicate points, or a `SymbolSet` with colliding labels/names, can overwrite internal dictionary or attribute mappings." (study: GPT-5.6 Terra, coding)
- Clear: "Two kinds of input can overwrite internal mappings in dictionaries or attributes: a lattice that was built with duplicate points, and a `SymbolSet` whose labels or names collide."

- Hard: "Projects completed on weekends, during school events, or over the summer could all count." (study: GPT-5.6 Sol, essay)
- Clear: "Projects could all count, even if students completed them on weekends, during school events, or over the summer."

- Hard: "Class time, where a total blackout policy would apply under Policy 1, remains protected and focused." (study: Claude Sonnet 5, essay)
- Clear: "Under Policy 1, phones would be banned completely during class, so class time stays protected and focused."

- Hard: "Has the building had water, mold, structural, or insurance claims?" (study: GPT-5.6 Luna, chat)
- Clear: "Has the building had any claims for water, mold, or structural damage, or any other insurance claims?"

- Hard: "A cat who can always get up and away is a much calmer cat." (study: Claude Opus 5, chat)
- Clear: "A cat is much calmer when it can always climb up and get away."

**Leave it alone when** the words in between are few and short, as in "The tests in this folder pass". An opening clause that sets the scene is also fine: "When the cache is empty, the loader reads from disk."

## 2. Stacked nouns

**What to look for.** Three or more nouns in a row, each one modifying the next: "class-time shutdown requirement", "absolute dotfile backup path handling". Hyphens do not help: "reader-patience budget" is still three nouns.

**Why it slows readers down.** A stack does not say how its parts relate, so the reader has to infer the grouping. Some stacks are ambiguous, like the headline "Squad Helps Dog Bite Victim" (Cooper 1980). Eye-tracking studies show that new compounds slow reading (Staub et al. 2007; Cohen and Staub 2014).

**What the study found.** In conversation, most frontier models stacked more nouns than human writers did. In chat and coding, they also stacked more than paraphrases of their own text.

**How to fix it.**

- Name the relation with a preposition: "money market funds at a brokerage".
- Turn one noun into a clause: "the rule that phones stay off during class".
- Keep established two-word terms together and unpack the rest. "The pull request description" is fine. "The pull request description template update" is not.

**Examples.**

- Hard: "I acknowledge concerns about distraction, but Policy 1's class-time shutdown requirement directly addresses this." (study: Kimi K2.5, essay)
- Clear: "I acknowledge the concerns about distraction, but Policy 1 addresses them directly: it requires phones to be off during class."

- Hard: "Fixed absolute dotfile backup path handling while preserving the `:` marker used during reinstall." (study: GPT-5.6 Luna, coding)
- Clear: "Backups now handle absolute paths to dotfiles correctly. The `:` marker that reinstall uses still works."

- Hard: "Online banks (Ally, Marcus, Capital One 360, Discover, SoFi) or brokerage money market funds (Fidelity's SPAXX, Vanguard's VMFXX) are the standard options." (study: Claude Opus 5, chat)
- Clear: "There are two standard options. One is an online bank, such as Ally, Marcus, Capital One 360, Discover, or SoFi. The other is a money market fund at a brokerage, such as Fidelity's SPAXX or Vanguard's VMFXX."

- Hard: "Summer park district classes are a whole thing in Chicago and people actually do them." (study: GLM-5, chat)
- Clear: "In Chicago, the park district runs summer classes, and lots of people take them."

- Hard: "Every long line in that list is pre-existing (long error-message string literals, which black leaves alone since it doesn't split strings without `--preview`)." (study: Claude Opus 5, coding)
- Clear: "Every long line in that list was already there. They are long string literals that hold error messages, and black leaves them alone because it splits strings only with `--preview`."

- Hard: "You've basically installed a horror movie soundtrack generator in your skull." (study: Claude Sonnet 5, chat)
- Clear: "Basically, your brain now plays scary music, like in a horror movie."

**Leave it alone when** the stack is a fixed term in the reader's field, such as "pull request", "unit test", "cell phone policy", or "error message". Two nouns in a row are usually fine.

## 3. Object relatives without "that"

**What to look for.** A noun followed directly by a clause that has its own subject, with no "that", "which", or "who" between them: "the behaviour the old code never reached". Look hardest when the clause has a full noun phrase as its subject, such as "the old code", rather than a pronoun such as "I" or "you". Long clauses and clauses inside other clauses need the same care.

**Why it slows readers down.** In an object relative, the described noun is the object of the verb inside the clause. These clauses are harder to process than subject relatives, partly because of their unusual word order and their longer dependencies (Staub 2010). The difference shrinks when the two nouns differ in animacy and when the pattern is frequent (Mak et al. 2006; Reali and Christiansen 2007). Without "that", two noun phrases meet with nothing to mark the boundary between them.

**What the study found.** Models used object relatives without "that" more often than paraphrases of the same content did, and used them with "that" less often. The authors read this as a preference for skipping optional words. In conversation, most frontier models also used more of the reduced form than human writers did.

**How to fix it.**

- Add "that" or "which".
- If two noun phrases still crowd together, give the clause its own sentence.
- Or recast the clause so that the described noun is its subject.

**Examples.**

- Hard: "Three fail on the old code; the others check behaviour the old code never reached." (study: Claude Opus 5.5, coding)
- Clear: "Three of the tests fail on the old code. The other tests check behavior that the old code never reached."

- Hard: "These are the exact skills the worksheet hoped to teach, but she has learned them because she wanted an answer." (study: Claude Opus 5.5, essay)
- Clear: "These are exactly the skills that the worksheet was meant to teach, but she has learned them because she wanted an answer."

- Hard: "The case/when fix is technically more impressive, but the unclosed-tag errors are the papercut people feel day-to-day." (study: GLM-5, coding)
- Clear: "The case/when fix is more impressive technically. But the errors from unclosed tags are the small annoyance that people run into every day."

**Leave it alone when** the clause is short and its subject is a pronoun. These read easily, and the study's own examples include many of them:

- "That's 'leave the job you hate' money." (study: Kimi K2.5, chat)
- "That's great for a beginner, honestly one of the best genres you could pick." (study: Claude Opus 5.5, chat)
- "I am writing to share my thoughts on the cell phone policy you are considering." (study: Claude Opus 5, essay)

## 4. Dropped structure words

**What to look for.**

- A clause after "know", "find", "show", "confirm", "notice", "see", "report", or "check" that starts with a noun phrase and has no "that": "I found the config file was missing".
- An optional word dropped from any of the short-or-long choices in the [table below](#short-and-long-forms-how-people-choose).
- Prose without subjects, verbs, or articles: "New tests for X, Y, and Z." or "Swept the codebase."
- Arrows, symbols, or emoji in place of words, as in "parse -> validate".

**Why it slows readers down.** Words such as "that" carry little meaning of their own, but they tell the reader how the sentence is built. People include an optional "that" more often when the clause after it is harder to predict. This spreads information evenly through the sentence (Levy and Jaeger 2007; Jaeger 2010). Without "that", a reader may first take the noun as the verb's object and then have to go back, as in a garden-path sentence (Christianson et al. 2001).

**What the study found.** The authors fine-tuned a small model with a penalty on the length of its output. With that penalty, it learned to choose the shorter form of each trained choice almost every time, while people choose by context. Without a constraint that kept it close to the original model, it left out the optional "that" more than 98 percent of the time in the two trained "that" constructions. The habit spread to two "that" constructions that it was never trained on, "sure (that)" and "so (that)".

**How to fix it.**

- Put "that" back after the verbs above when a full noun phrase follows.
- Write complete sentences in prose. A list of changes can use short items, but keep the articles and prepositions in them.
- Write "leads to", "becomes", or "then" instead of an arrow.

**Examples.**

- Hard: "I found the config file was missing."
- Clear: "I found that the config file was missing."

- Hard: "New tests for paths with spaces, dry-run write prevention, and idempotent config reinstalls." (study: GPT-5.6 Terra, coding)
- Clear: "I added tests for three cases: paths with spaces, dry runs that must not write anything, and reinstalling the config twice."

- Hard: "Swept the codebase and fixed the bugs I could verify." (study, Figure 1, coding)
- Clear: "I went through the codebase and fixed the bugs that I could confirm."

**Leave it alone when** the clause is short and easy to predict. "I think it works" and "She said she'd come" need no "that".

## 5. Nouns used as verbs

**What to look for.** A word that is normally a noun, used as a verb in a way that readers rarely see: "calendar it", "footnote it", "bucket these", "timebox it", "caveat that".

**Why it slows readers down.** Readers can work out new verbs like these (Clark and Clark 1979), but the change of word class makes them reanalyze the sentence (Thierry et al. 2008). People also process a word that can be either a noun or a verb differently from a word that can be only one of them (Frazier and Rayner 1987; Federmeier et al. 2000).

**What the study found.** Almost all frontier models used more nouns as verbs than paraphrases of the same content did.

**How to fix it.** Use the ordinary verb phrase, even when it is a word or two longer: "put it on your calendar", "put it in a footnote", "sort these into groups".

**Examples.**

- Hard: "So yes — calendar it." (study: Claude Fable 5, chat)
- Clear: "So yes, put it on your calendar."

- Hard: "And Austin has unusually high inventory, which cushions price spikes better than supply-constrained markets." (study: Claude Opus 5, chat)
- Clear: "Austin also has an unusually large supply of homes for sale, so prices there jump less than in markets where supply is tight."

- Hard: "In each case, the logic is the same: pooling independent judgments filters out individual errors." (study: Claude Fable 5, essay)
- Clear: "In each case, the logic is the same: when you combine independent judgments, individual errors cancel out."

**Leave it alone when** the verb is established for the reader, such as "email", "text", and "google", or "cache", "stub", "commit", "stage", and "merge" for developers. In a summary of Git work, "staging changes" is the normal term.

## 6. Things that act like people

**What to look for.** A thing, an idea, or a piece of code as the subject of a verb that normally needs a person. Typical verbs are swallows, eats, bites, promises, hopes, forgets, wants, asks, misunderstands, complains, chokes, and knows.

**Why it slows readers down.** Readers use animacy as a cue while they parse a sentence (Trueswell et al. 1994). When an inanimate subject meets one of these verbs, brain responses show signs of reanalysis (Kim and Osterhout 2005; Kuperberg 2007). Readers can decode the metaphor, but it costs them time.

**What the study found.** All nine frontier models used inanimate subjects with these verbs more often than human writing did. Most also used them more often than paraphrases of the same content did.

**How to fix it.** Say what literally happens, or make a person the subject.

**Examples.**

- Hard: "`is_file()` swallows that and returns False." (study, Section 3.1)
- Clear: "`is_file()` catches that error and returns False."

- Hard: "Puzzle patterns where this asymmetry bites" (study, Section 3.1)
- Clear: "Puzzle patterns where this asymmetry causes problems"

- Hard: "The docstring promises they're skipped when they 'appear anywhere in the `source_dir` path'; e.g. backing up a dotfolder like `~/.cache/foo` was not skipped." (study: Claude Fable 5, coding)
- Clear: "The docstring says that such files are skipped when they 'appear anywhere in the `source_dir` path'. But a hidden folder such as `~/.cache/foo` was still included in the backup."

- Hard: "No new branch, no change in control flow — just closing the gap in an existing check that covered `str` but forgot its sibling scalar-like type `bytes`." (study: Claude Sonnet 5, coding)
- Clear: "This change adds no new branch and does not change the control flow. It only fixes an existing check that handled `str` but not the similar type `bytes`."

- Hard: "Second, the time objection misunderstands how service actually functions." (study: Kimi K2.5, essay)
- Clear: "Second, people who object that service takes too much time misunderstand how it works."

- Hard: "The whole conversation is eating its own tail." (study: Claude Opus 5, chat)
- Clear: "The conversation keeps going in circles."

- Hard: "Sometimes chaos has a 1099; sometimes chaos expects you to remember it independently." (study: GPT-5.6 Sol, chat)
- Clear: "Sometimes the income comes with a 1099 form. Sometimes you have to remember to report it yourself."

**Leave it alone when** the usage is standard in the field. A function returns a value or takes arguments, a server accepts or refuses a connection, a test expects a value, the documentation says something, and a study shows a result.

## 7. Rare word pairs and coinages

**What to look for.** Words that people rarely put together, invented compounds, and private metaphors: "reader-patience budget", "verified red", "a gear trap", "later enrichments". Watch for one coinage repeated across a conversation.

**Why it slows readers down.** How fast people read a word depends on how predictable it is (Hale 2001; Levy 2008; Smith and Levy 2013). A surprising pair makes the reader stop and work out what is meant.

**What the study found.** In all three settings, almost all frontier models used more word pairs that never occur in human reference text than paraphrases of their own text did. Their text was also harder to predict for a simple model trained on human text. Compared with human writing, all nine frontier models used more rare word sequences. In the Olmo family, the effect grew from the base model to the instruction-tuned model to the reasoning model. One coinage, "verified red", appeared four times in a single coding conversation.

**How to fix it.**

- Say it the way most people would, even if that takes a few more words.
- In technical writing, prefer literal words to metaphor.
- Introduce a term once, define it, and then use it consistently.
- Avoid jargon that the reader does not share.

**Examples.**

- Hard: "Every behavioral test was verified red against the original source." (study: Claude Opus 5, coding)
- Clear: "I ran every behavior test against the original code and confirmed that each one failed there."

- Hard: "That's a really legitimate concern, and honestly it's the part most internet advice glosses over." (study: Claude Fable 5, chat)
- Clear: "That's a really legitimate concern, and honestly, it's the part that most online advice leaves out."

- Hard: "`as_documents: true` previously mutated the tag instance permanently, causing later enrichments to return `DocumentsList` unexpectedly." (study: GPT-5.6 Luna, coding)
- Clear: "Before this fix, `as_documents: true` changed the tag instance permanently. As a result, later enrichment steps returned a `DocumentsList` when they should not have."

- Hard: "It's not necessary, but it's surprisingly useful—and not really a gear trap." (study: GPT-5.6 Sol, chat)
- Clear: "You don't need it, but it's surprisingly useful, and it won't lead you into buying more and more gear."

- Hard: "Your instinct is right; the convoluted sentence you are currently reading is quietly eating its own reader-patience budget — footnote it." (the study's opening sentence, written to show several features at once)
- Clear: "You're right. This sentence is hard to read, and it wastes the reader's patience. Put it in a footnote."

**Leave it alone when** the phrase is a standard term or idiom for the reader, such as "race condition" or "happy path" for developers. Such terms are fine even when they look odd out of context.

## 8. Too much in one sentence

**What to look for.** A sentence with two or more main points, several new terms, a chain of semicolons or dashes, or more than about 25 words.

**Why it slows readers down.** People tend to spread information evenly across what they say, so that no stretch of it overloads the listener (Levy and Jaeger 2007; Meister et al. 2021). Dense stretches strain the same limited working memory that long dependencies do.

**What the study found.** The study did not measure sentence length as a feature. It adjusted dependency length for sentence length, and it left sentences over 30 words out of that measure. This rule follows from the research on information density that the study builds on, and from its finding that a length penalty pushes a model to compress.

**How to fix it.**

- Give each sentence one main idea. Split at "and", "but", semicolons, and dashes.
- Put the main point first and the details after it.
- Introduce one new term at a time.

**Example.**

- Hard: "The most substantive unfixed item is the existing xfailed lazy-intermediate Lookup behavior; the others are primarily compatibility, validation, or API-policy decisions." (study: GPT-5.6 Terra, coding)
- Clear: "The most important problem that is still unfixed is a known bug in `Lookup` with lazy intermediate values, which is already marked as an expected failure. The other open items are mostly decisions about compatibility, validation, or API policy."

## Short and long forms: how people choose

English often offers a short and a long way to say the same thing. The study's experiment with a length penalty used the pairs below. People use both forms and choose by context. A model trained under a length penalty came to pick the short form almost every time. When in doubt, and especially in a long or complex sentence, choose the form that makes the structure clearer.

| Choice | Short form | Long form | Prefer the long form when |
| --- | --- | --- | --- |
| Object relative | the book the professor wrote | the book that the professor wrote | the clause has a full noun as its subject, or is long |
| Complement clause | knew the answer was wrong | knew that the answer was wrong | the noun after the verb could be read as its object |
| Adjective and clause | was sure the door was locked | was sure that the door was locked | the clause is long |
| Purpose with "so" | spoke slowly so we could follow along | spoke slowly so that we could follow along | the clause is long |
| Purpose with "to" | left early to catch the train | left early in order to catch the train | the purpose comes far from its verb |
| Dative | gave his wife a gift | gave a gift to his wife | the recipient is long or new to the reader |
| Genitive | noticed the old house's roof | noticed the roof of the old house | the owner is long, or is a thing rather than a person |
| Quantifier | ate all the cookies | ate all of the cookies | either form is fine |
| Passive | a falling branch hit it | it was hit by a falling branch | the thing affected is the topic of the passage |

## Where the problem is worst

- Long, multi-turn chats and coding sessions showed larger effects than single essays. The authors suggest that long exchanges may push models toward compression.
- In coding sessions, the study analyzed the last message of each turn, which is usually a summary of the work. All of its coding examples come from these messages.
- In the Olmo family, the effects grew from the base model to the instruction-tuned model to the reasoning model.
- Newer models are not always worse. Claude Opus 5.5 scored lower than Claude Opus 5 in 19 of 21 comparisons of the difficulty measures.

## A worked example

Here is an end-of-task summary in the compressed style. It was written for this file and is not quoted from the study:

> Swept the repo and fixed the three bugs I could verify. The `parse_args()` fallback was silently swallowing malformed flags; it now surfaces a proper error. Config reload path handling regressions are fixed too, and every behavioral test was verified red against the original source. One thing worth calendaring: the lazy-intermediate `Lookup` xfail still bites on Python 3.13.

What goes wrong:

- "Swept the repo" has no subject.
- "Swallowing" and "bites" give human actions to code.
- "Config reload path handling regressions" stacks five nouns.
- "Verified red" and "lazy-intermediate `Lookup` xfail" are private coinages.
- "Calendaring" turns a noun into a verb.

The same content, rewritten:

> I went through the repository and fixed the three bugs that I could confirm.
>
> - `parse_args()` used to accept malformed flags without an error. It now reports one.
> - Reloading the config no longer breaks how file paths are handled.
> - I ran each new test against the original code and confirmed that it failed there.
>
> One problem is still open. A test for `Lookup` with lazy intermediate values is marked as an expected failure, and it still fails on Python 3.13. It is worth scheduling a fix.

The rewrite is about 25 words longer. Most of the added words make the structure visible: subjects, "that", and verbs that name what happened.

## Sources

The study:

- Clark, T. H., Martin, M. B., and Mahowald, K. (2026). Why is AI-generated language so hard to understand? arXiv:2610.29162. https://arxiv.org/abs/2610.29162

Work that the study cites and that this file refers to:

- Christianson, K., Hollingworth, A., Halliwell, J. F., and Ferreira, F. (2001). Thematic roles assigned along the garden path linger. Cognitive Psychology, 42(4).
- Clark, E. V., and Clark, H. H. (1979). When nouns surface as verbs. Language, 55(4).
- Cohen, A. L., and Staub, A. (2014). Online processing of novel noun-noun compounds. Quarterly Journal of Experimental Psychology, 67(1).
- Cooper, G., editor (1980). Squad Helps Dog Bite Victim, and Other Flubs from the Nation's Press.
- Federmeier, K. D., Segal, J. B., Lombrozo, T., and Kutas, M. (2000). Brain responses to nouns, verbs and class-ambiguous words in context. Brain, 123(12).
- Frazier, L., and Rayner, K. (1987). Resolution of syntactic category ambiguities. Journal of Memory and Language, 26(5).
- Futrell, R., Mahowald, K., and Gibson, E. (2015). Large-scale evidence of dependency length minimization in 37 languages. PNAS, 112(33).
- Gibson, E. (1998). Linguistic complexity: Locality of syntactic dependencies. Cognition, 68(1).
- Gibson, E. (2000). The dependency locality theory. In Image, Language, Brain. MIT Press.
- Hale, J. (2001). A probabilistic Earley parser as a psycholinguistic model. NAACL.
- Jaeger, T. F. (2010). Redundancy and reduction: Speakers manage syntactic information density. Cognitive Psychology, 61(1).
- Kim, A., and Osterhout, L. (2005). The independence of combinatory semantic processing. Journal of Memory and Language, 52(2).
- Kuperberg, G. R. (2007). Neural mechanisms of language comprehension: Challenges to syntax. Brain Research, 1146.
- Levy, R. (2008). Expectation-based syntactic comprehension. Cognition, 106(3).
- Levy, R., and Jaeger, T. F. (2007). Speakers optimize information density through syntactic reduction. NeurIPS 19.
- Mak, W. M., Vonk, W., and Schriefers, H. (2006). Animacy in processing relative clauses. Journal of Memory and Language, 54(4).
- Martínez, E., Mollica, F., and Gibson, E. (2022). Poor writing, not specialized concepts, drives processing difficulty in legal language. Cognition, 224.
- Meister, C., Pimentel, T., Haller, P., Jäger, L., Cotterell, R., and Levy, R. (2021). Revisiting the uniform information density hypothesis. EMNLP.
- Reali, F., and Christiansen, M. H. (2007). Processing of relative clauses is made easier by frequency of occurrence. Journal of Memory and Language, 57(1).
- Smith, N. J., and Levy, R. (2013). The effect of word predictability on reading time is logarithmic. Cognition, 128(3).
- Staub, A. (2010). Eye movements and processing difficulty in object relative clauses. Cognition, 116(1).
- Staub, A., Rayner, K., Pollatsek, A., Hyönä, J., and Majewski, H. (2007). The time course of plausibility effects on eye movements in reading. Journal of Experimental Psychology: Learning, Memory, and Cognition, 33(6).
- Thierry, G., et al. (2008). Event-related potential characterisation of the Shakespearean functional shift in narrative sentence structure. NeuroImage, 40(2).
- Trueswell, J. C., Tanenhaus, M. K., and Garnsey, S. M. (1994). Semantic influences on parsing. Journal of Memory and Language, 33(3).
