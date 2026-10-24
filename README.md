# understandable

A Claude Code skill that makes Claude's writing easier to read. It applies the findings of *Why is AI-generated language so hard to understand?* (Clark, Martin, and Mahowald, 2026) while Claude writes. Nothing is retrained.

**Before:**

> Swept the repo and fixed the three bugs I could verify. The `parse_args()` fallback was silently swallowing malformed flags; it now surfaces a proper error. Config reload path handling regressions are fixed too, and every behavioral test was verified red against the original source.

**After:**

> I went through the repository and fixed the three bugs that I could confirm. `parse_args()` used to accept malformed flags without an error, and it now reports one. Reloading the config no longer breaks how file paths are handled. I ran each new test against the original code and confirmed that it failed there.

## Why this exists

The study compared text from 14 language models with human writing, and with paraphrases of the same content. Frontier models overused six features that psycholinguistics links to slower reading:

| Feature | Example from the study | Plainer version |
| --- | --- | --- |
| Subject far from its verb | "The guitar sitting in the corner because you're still 'deciding' teaches you zero chords." | "You won't learn any chords while the guitar sits in the corner and you keep 'deciding'." |
| Stacked nouns | "Policy 1's class-time shutdown requirement" | "Policy 1's rule that phones stay off during class" |
| Object relatives without "that" | "the others check behaviour the old code never reached" | "the other tests check behavior that the old code never reached" |
| Nouns used as verbs | "So yes, calendar it." | "So yes, put it on your calendar." |
| Things that act like people | "The docstring promises they're skipped." | "The docstring says that they are skipped." |
| Rare word pairs | "Every behavioral test was verified red against the original source." | "I ran every behavior test against the original code and confirmed that each one failed there." |

The authors' explanation is post-training that rewards correct answers in few tokens, with no check that a person can follow the text. They support it with an experiment. In that experiment, a small model trained with a length penalty learned to choose the shorter of two equal phrasings almost every time. For example, it dropped the optional "that", even in constructions that it was never trained on. People choose between such forms by context. The effects were strongest in long chats and coding sessions.

These habits are not fixed. Claude Opus 5.5 scored lower than Claude Opus 5 on 19 of 21 comparisons. Because each feature is specific and has a name, a model can be told to avoid it. That is what this skill does.

For a fuller summary of the study, see [docs/paper-notes.md](docs/paper-notes.md).

## What the skill does

When you run `/understandable`, Claude follows eight rules for the rest of the session:

1. Keep each subject close to its verb.
2. Don't stack nouns.
3. Mark relative clauses with "that", "which", or "who".
4. Keep the small words that show structure.
5. Use ordinary verbs, not nouns turned into verbs.
6. Give human actions to people, not to things.
7. Use common words in their usual combinations.
8. Give each sentence one main idea.

Rules 1 to 3 and 5 to 7 match the six features that the study measured. Rule 4 comes from the study's experiment with a length penalty, and rule 8 comes from the research on information density that the study builds on.

The skill also tells Claude not to overcorrect. People use both forms of each choice, so Claude should not add "that" everywhere, pad its replies, or simplify the ideas. Replies may come out slightly longer, but they should not say more.

## Install

**For all your projects** (recommended):

```bash
git clone https://github.com/hsheimbuch/understandable ~/.claude/skills/understandable
```

To update it later, run `git -C ~/.claude/skills/understandable pull`.

**For one project**, so that everyone on the project gets it:

```bash
git submodule add https://github.com/hsheimbuch/understandable .claude/skills/understandable
```

**As a plugin**:

```bash
claude plugin marketplace add hsheimbuch/understandable
claude plugin install understandable@understandable
```

Plugin skills carry the plugin's name as a prefix, so with this method the command is `/understandable:understandable`.

## Use

| Command | What happens |
| --- | --- |
| `/understandable` | Claude follows the rules for the rest of the session. If its last reply was dense, it rewrites that reply first. |
| `/understandable off` | Claude stops following the rules. |
| `/understandable check docs/guide.md` | Claude lists the hard-to-read spots in the file, with a rewrite for each, and changes nothing. |
| `/understandable docs/guide.md` | Claude rewrites the prose in the file. Code, links, and identifiers stay as they are. |
| `/understandable <text>` | Claude rewrites the text and returns the new version. |

Claude can also load the skill on its own when you ask for plainer wording, or when it writes documentation, READMEs, or pull request descriptions.

## How it works

- The skill is plain instructions. Claude Code loads `SKILL.md` into the conversation when you invoke it.
- `SKILL.md` is short, because its text stays in context for the whole session. The longer catalog in `references/constructions.md` loads only for `check` and for file rewrites.
- After `/compact`, Claude Code re-attaches the start of each skill that you invoked, and the rules sit at the start. In a very long session, run `/understandable` again if the old habits return.

## Limitations

- It covers English only.
- The study measured features that earlier research links to reading difficulty. It did not test how well people understood the AI text itself.
- The skill changes how Claude writes. It does not change what Claude knows, or the code that Claude writes.

## Repository layout

- `SKILL.md`: the skill, with its modes and the eight rules
- `references/constructions.md`: the full catalog, with examples from the study
- `docs/paper-notes.md`: a summary of the study, and how each rule follows from it
- `.claude-plugin/`: the plugin and marketplace manifests

## Author

Heinrich Heimbuch, [github.com/hsheimbuch](https://github.com/hsheimbuch)

## Credits

The rules and the examples come from this study. This project is not affiliated with its authors.

```bibtex
@misc{clark2026understand,
  title         = {Why is {AI}-generated language so hard to understand?},
  author        = {Clark, Thomas Hikaru and Martin, Matias B. and Mahowald, Kyle},
  year          = {2026},
  eprint        = {2610.29162},
  archivePrefix = {arXiv},
  primaryClass  = {cs.CL},
  url           = {https://arxiv.org/abs/2610.29162}
}
```

## License

The skill and the documentation are under the [MIT License](LICENSE). The examples quoted from the study are under the paper's license, [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
