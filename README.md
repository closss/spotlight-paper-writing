# Spotlight: Write Papers the Way Reviewers Read Them

A Claude skill for writing and revising papers for top AI venues: **NeurIPS, ICLR, ICML, CVPR, ICCV, ECCV, ACL, EMNLP, AAAI, ICASSP** and similar.

Most paper-writing skills start by producing a full draft. Spotlight starts one step earlier. It first works out a closed-loop narrative with you, turns it into a one-line-per-subsection skeleton, and checks that every claim has evidence behind it. Only then does it write. The prose it produces states results plainly, keeps hedging to a minimum, and avoids the vocabulary that makes reviewers suspect a paper was written by an LLM.

## Before / After

A typical LLM-polished paragraph:

> Notably, our method achieves a significant improvement across a comprehensive set of benchmarks, highlighting its effectiveness. It is worth noting that while these results are promising, this does not imply that our approach generalizes to all settings. Furthermore, we emphasize that our method seamlessly integrates with existing pipelines.

The same paragraph after Spotlight:

> On four long-context benchmarks, our method improves accuracy by 4.2 points over the strongest baseline while using 38% less KV memory (Table 2). It needs no retraining and runs as a single step before decoding.

*(Numbers are illustrative.)* The second version carries more information in fewer words. The caveat did not disappear; the claim was narrowed to what the experiments show, and any real limitation goes into one Limitations paragraph.

<!-- TODO: add a screenshot of a results table rendered with references/latex-snippets.md, e.g. assets/table-example.png -->

## What it enforces

**Narrative before prose.** Spotlight discusses the story with you first: the one-sentence contribution, the specific failure of prior work, the insight, and which results support it. It then builds a skeleton (4–7 sections, 2–4 subsections each, one sentence per subsection) and a claim–evidence table. Claims without evidence get cut or narrowed; experiments that answer no question from the introduction move to the appendix.

**Title.** `MethodName: subtitle`. The method name should be short and memorable, not an acronym forced out of filler words. The subtitle states the mechanism or the finding.

**Abstract.** Problem : method : results ≈ 1 : 1 : 1, opening on the concrete problem, with one or two key numbers.

**Introduction.** Specific failure conditions of existing work ("under X, Y happens because Z"), then the insight and method, then about three verifiable contributions. Emphasis is expressed through facts and numbers, never through "we emphasize" or "importantly".

**Tables.** Best results get one light, non-green color block (or bold); second best is underlined; the same scheme is used across all tables and figures. A LaTeX template is included.

**Statistics.** Bootstrap intervals and significance tests appear in the one or two core tables only. Everything else goes to the appendix. No pre-registration or "locked protocol" language in the main text.

**Hedging.** At most one or two defensive sentences ("…, but this does not imply…") in the whole paper. The skill rewrites the rest by narrowing the claim itself.

**AI flavor.** A blacklist of words and patterns (*delve*, *crucial*, *seamlessly*, *notably*, chains of *Moreover*, trailing *", highlighting…"* clauses, and so on) is checked section by section.

**Consistency.** One term per concept, identical numbers everywhere they appear, notation defined before use.

## Workflow

| Stage | Output | You confirm? |
|---|---|---|
| 0. Constraints | Venue, page limit, anonymity rules, required checklists (checked against this year's CFP) | Yes |
| 1. Narrative | One-sentence contribution and the problem → gap → insight → method → evidence chain | Yes |
| 2. Skeleton | Section skeleton and claim–evidence table | Yes |
| 3. Topic sentences | One lead sentence per paragraph; reading only these tells the whole story | Optional |
| 4. Drafting | Section-by-section LaTeX | Per section |
| 5. Self-review | Checklist pass, including a reviewer's-eye read | — |

In **revision mode**, Spotlight first reverse-engineers the skeleton and claim–evidence table from your draft, marks the breaks, and agrees with you on what to fix before editing any sentences.

When turning reviews into a revision plan, it splits tasks into two lists: edits that can be made from the paper and reviews alone, and items that need the codebase or new experiments. The second list is meant for whoever (or whichever agent) has access to the code, so the writing side never invents numbers.

## Installation

**Claude Code**

```bash
git clone https://github.com/closss/spotlight-paper-writing.git ~/.claude/skills/spotlight-paper-writing
```

The destination folder has to be named `spotlight-paper-writing`. Claude requires that name to match the `name` field in `SKILL.md`.

**Claude.ai**

Download [`spotlight-paper-writing.zip`](https://github.com/closss/spotlight-paper-writing/releases/latest/download/spotlight-paper-writing.zip) from the [Releases](https://github.com/closss/spotlight-paper-writing/releases) page and upload that zip in the Skills section of your settings. Upload the archive as-is. The "Code → Download ZIP" button on this repository produces a different archive, and Claude rejects it because the folder name inside does not match the skill name.

## Usage

The skill triggers on its own when you ask for paper-writing help. Some prompts to start with:

```
I have results for a KV-cache compression method. Help me write an ICLR paper.
```
```
Here is my intro. Revise it with the Spotlight rules.
```
```
Turn these three reviews into a revision plan.
```
```
Give me five name candidates for this method.
```

## Repository structure

```
spotlight-paper-writing/
├── SKILL.md                         # workflow and rules
└── references/
    ├── latex-snippets.md            # table highlighting template
    ├── ai-flavor-blacklist.md       # words, patterns, and rewrites
    └── final-checklist.md           # self-review checklist
```

## Scope

- Covers writing from scratch and revising existing drafts.
- Does not write rebuttals; they follow a different logic and deserve their own skill.
- Does not hard-code venue rules. Page limits and checklists change every year, so the skill checks the current CFP instead.

## Language

The skill instructions are currently written in Chinese; the papers it produces are in English. Claude reads both without issue. An English version of `SKILL.md` is planned.

## Contributing

Issues and pull requests are welcome, especially additions to the AI-flavor blacklist and venue-specific notes.

## License

MIT
