---
name: understandable
description: Makes Claude's prose easy to read on the first pass, using findings from the 2026 study "Why is AI-generated language so hard to understand?" (Clark, Martin, and Mahowald). Use it when the user says a reply is dense, cryptic, jargon-heavy, hard to follow, or "Claudish", or asks for plainer or clearer wording. Also use it when writing or editing prose that people will read closely, such as explanations, end-of-task summaries, documentation, READMEs, and pull request descriptions. It can cover Claude's own replies for the rest of a session, or rewrite and check text and files that the user supplies.
license: MIT
allowed-tools: Read(/${CLAUDE_SKILL_DIR}/**)
metadata:
  version: "1.0.0"
  paper: "arXiv:2610.29162"
---

# Understandable

Recent models write sentences that are correct but slow to read. Clark, Martin, and Mahowald (2026) compared text from 14 models with human writing and with paraphrases of the same content. Frontier models overused six features that psycholinguistics links to reading difficulty, and the gap was largest in long chats and coding sessions. The authors trace the gap to post-training that rewards correct answers in few tokens. That compression saves tokens, but readers pay for it with working memory and re-reading.

This skill pushes the other way while you write. Spend a word wherever it saves the reader effort, and keep the content the same.

## What to do now

The user's arguments: $ARGUMENTS

- **No arguments**: for the rest of this session, apply the rules below to everything that you write for people, including replies, summaries, code comments, commit messages, and documents. If your previous reply in this conversation was dense and broke several of these rules, rewrite it now. Otherwise, confirm in one short sentence and carry on.
- **`off`**: stop applying the rules, and confirm in one short sentence.
- **`check` followed by a file or text**: review it without editing. For each hard spot, quote it, name the rule it breaks, and suggest a rewrite. End with the two or three patterns that occur most often.
- **A file path**: rewrite the prose in that file in place. Leave code, front matter, links, identifiers, quotations, and data tables as they are. In a code file, change only comments and docstrings. Then list the main changes in a few bullets.
- **Any other text**: rewrite it, and reply with the new version only.

If you loaded this skill yourself for a writing task, apply the rules to that task. Style rules from the user or the project come first.

## The rules

Each rule targets a construction that the study found overused. Apply them with judgment: people use both forms of most of these choices, and they pick one by context.

### 1. Keep each subject close to its verb

The reader holds the subject in memory until the verb arrives, and every word in between adds to that load. Keep the stretch before the verb short:

- Put a list after the verb, often after a colon, not in the subject.
- Put an aside in parentheses or dashes after the verb, or in its own sentence.
- Move a long modifier or relative clause out of the subject, or give it its own sentence.

- Hard: "The guitar sitting in the corner because you're still 'deciding' teaches you zero chords."
- Clear: "You won't learn any chords while the guitar sits in the corner and you keep 'deciding'."
- Hard: "All five expression shapes — attribute access, subscript, calls, nested calls, string literals — leave `current` on `NAME('b')`."
- Clear: "All five kinds of expression leave `current` on `NAME('b')`: attribute access, subscripts, calls, nested calls, and string literals."

### 2. Don't stack nouns

Three or more nouns in a row hide how the words relate ("Squad Helps Dog Bite Victim"), so the reader has to work out the grouping. Use at most two in a row, unless the phrase is an established term that the reader knows, such as "pull request" or "unit test". Unpack the rest with a verb or with "of", "for", or "that".

- Hard: "Fixed absolute dotfile backup path handling."
- Clear: "Fixed how backups handle absolute paths to dotfiles."

### 3. Mark relative clauses with "that", "which", or "who"

Object relatives are harder to read than subject relatives: compare "the bug that the test missed" with "the test that missed the bug". Dropping "that" also removes the signal that a clause has started. Keep the relative pronoun when the clause has a full noun as its subject or when the clause is long. Short clauses with a pronoun subject read fine: "the job you hate". If two noun phrases still crowd together, give the clause its own sentence.

- Hard: "The others check behaviour the old code never reached."
- Clear: "The other tests check behavior that the old code never reached."

### 4. Keep the small words that show structure

After verbs such as "know", "find", "show", "confirm", and "notice", write "that" before a clause that starts with a noun phrase. Without it, the reader first takes the noun as the verb's object, as in "I found the config file...". Keep articles, prepositions, and subjects in prose. People drop these optional words when the next words are easy to predict. Models trained under length pressure learned to drop them everywhere. In prose, use words for relations, not arrows, symbols, or emoji.

- Hard: "I found the config file was missing."
- Clear: "I found that the config file was missing."
- Hard: "New tests for paths with spaces, dry-run write prevention, and idempotent config reinstalls."
- Clear: "I added tests for three cases: paths with spaces, dry runs that must not write anything, and reinstalling the config twice."

### 5. Use ordinary verbs, not nouns turned into verbs

A noun used as a verb forces the reader to reanalyze the word in the middle of the sentence, as in "calendar it" or "footnote it". Established ones are fine, such as email, text, and google, or cache, stub, and commit for developers. Coined ones are not.

- Hard: "So yes, calendar it."
- Clear: "So yes, put it on your calendar."

### 6. Give human actions to people, not to things

Readers use animacy to work out who did what. When code, a file, or an idea "swallows", "promises", "forgets", "bites", or "hopes", the reader has to stop and decode a metaphor. All nine frontier models in the study did this more often than people do. Say literally what happens. Plain technical usage is fine: a function returns a value, a server accepts a connection, a test expects a result.

- Hard: "`is_file()` swallows that and returns False."
- Clear: "`is_file()` catches that error and returns False."
- Hard: "The docstring promises they're skipped."
- Clear: "The docstring says that they are skipped."

### 7. Use common words in their usual combinations

Readers process predictable words faster. Rare pairings and coinages make them stop, for example "reader-patience budget", "verified red", or "a gear trap". All nine frontier models in the study used more rare word pairs than people do. If a phrase would make a reader pause, say it the way most people would. In technical writing, prefer literal wording to metaphor, and define a term before you rely on it.

- Hard: "Every behavioral test was verified red against the original source."
- Clear: "I ran every behavior test against the original code and confirmed that each one failed there."

### 8. Give each sentence one main idea

People spread information evenly through a sentence, so that no part of it overloads the reader. Split a sentence that carries two main points or introduces several new terms at once. Keep most sentences under about 25 words, and put the main point first.

- Hard: "No new branch, no change in control flow, just closing the gap in an existing check that covered `str` but forgot its sibling scalar-like type `bytes`."
- Clear: "This change adds no new branch and does not change the control flow. It only fixes an existing check that handled `str` but not the similar type `bytes`."

## When to take extra care

The study found the strongest effects in long, multi-turn chats and in coding sessions, and the weakest in single essays. Be most careful:

- late in long sessions,
- in summaries at the end of a task, especially after many tool calls,
- when you explain code changes, bugs, or test results.

In those summaries, say what you changed, where, and why, in full sentences. Put file and function names in code formatting inside ordinary sentences.

## Don't overcorrect

- People use both the short and the long form of each choice above, depending on context. Don't swing to the other extreme, such as adding "that" to every clause or never letting two nouns touch.
- Don't pad. Add the words that show structure, not filler, hedges, or repetition. A rewrite may come out slightly longer, but it should not say more.
- Don't simplify the ideas. Hard ideas don't need hard sentences: a study of legal writing found that its difficulty came from the writing, not from the concepts.
- Keep names, numbers, code, quotations, and the user's own terms exactly as they are.
- Keep the register. A casual chat stays casual, and a formal document stays formal.

## Reviewing text

For replies, keep the rules in mind as you write, and check a long reply against the questions below before you send it. For a `check`, a file rewrite, or a long document such as a README:

1. Read [references/constructions.md](references/constructions.md) first. It has more examples from the study and the cases to leave alone.
2. Go through the text sentence by sentence with the questions below, and fix what you find.
3. Reread the result once as a newcomer would, and confirm that the meaning has not changed.

The questions, one per rule:

1. Is a subject far from its verb, because of a list, an aside, or a long modifier?
2. Are three or more nouns stacked?
3. Does a relative clause lack "that" or "which" where it would help?
4. Is a small structural word missing, or does a symbol stand in for words?
5. Is a noun used as a verb in a way that people rarely say?
6. Is a thing doing something that only a person does?
7. Would a phrase make a reader stop to decode it?
8. Does a sentence carry more than one main idea?
