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

**Narrative before prose.** Spotlight discusses the story with you first: the one-sentence contribution, the specific failure of prior work, the insight, and which results support it. It then helps you pick one of four narrative archetypes that recur in oral papers: removing a component everyone assumed was necessary, redesigning natively around a real constraint, opening a new problem category, or dissecting why a widely used design works. Each archetype comes with the evidence it needs. Next comes a skeleton (4–7 sections, 2–4 subsections each, one sentence per subsection) and a claim–evidence table. Claims without evidence get cut or narrowed; experiments that answer no question from the introduction move to the appendix. The challenges named in the introduction, the design components, and the experiment groups must line up one to one.

**Title.** `MethodName: subtitle`. The method name should be short and memorable, not an acronym forced out of filler words. The subtitle carries a counterintuitive insight, a new category, the properties that answer the stated challenges, or the list of findings.

**Abstract.** A balanced problem : method : results split, with the problem part capped at about a third; in the reference papers it is usually closer to a fifth. One sentence carries the core contribution or finding. Results name what is compared and under which conditions, with at most one or two numbers.

**Introduction.** Specific failure conditions of existing work ("under X, Y happens because Z"), pinned down by a measurement, a concrete example, or evidence that prior gains came from somewhere else. Then the insight and method, then about three verifiable contributions. The Figure 1 type follows the archetype. Emphasis is expressed through facts and numbers, never through "we emphasize" or "importantly".

**Experiments.** Every main comparison states what was held fixed, and baselines get strengthened where needed. Trade-off claims get a frontier plot instead of a single operating point. Every "this works because X" claim gets a knockout experiment that removes only X.

**Tables.** Best results get one light, non-green color block (or bold); second best is underlined; the same scheme is used across all tables and figures. A LaTeX template is included.

**Statistics.** Bootstrap intervals and significance tests appear in at most one or two results, and reporting none is normal: five of the six reference papers have none in the main text. Everything else goes to the appendix. No pre-registration or "locked protocol" language in the main text.

**Hedging.** At most one or two defensive sentences ("…, but this does not imply…") in the whole paper. The skill rewrites the rest by narrowing the claim itself.

**AI flavor.** A blacklist of words and patterns (*delve*, *crucial*, *seamlessly*, *notably*, chains of *Moreover*, trailing *", highlighting…"* clauses, and so on) is checked section by section. Words that strong papers do use get a per-paper budget set from counts in the six reference papers, instead of an outright ban.

**Consistency.** One term per concept, identical numbers everywhere they appear, notation defined before use.

## Where the patterns come from

`references/oral-patterns.md` distills recurring moves from a hand-picked set of oral papers: DPO, Genie, NSA, VGGT, Gated Attention, and D4RT. It covers title and abstract patterns, Figure 1 types, method framing, fair-comparison controls, knockout experiments, and how these papers write their limitations. The skill uses it as a menu of proven structures, not as text to copy. The same file records where these papers disagree with the skill's original rules, such as how much of the abstract goes to background, where limitations are disclosed, and how often significance tests appear, and how each rule was adjusted.

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
    ├── oral-patterns.md             # patterns distilled from oral papers
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
