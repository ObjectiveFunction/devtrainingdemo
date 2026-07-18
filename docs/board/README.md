# Build Board

The Build Board is Signal42's files-in-repo work record. Each stream file in `docs/board/` tells an append-only, evidence-backed story of what landed and who owned the lane, while the canonical Build Board repository aggregates those streams into a portfolio view.

## Entry formats

Narrative entries record landed work:

```text
## YYYY-MM-DD HH:MM — <headline>
- What: <what happened or was decided>
- Why: <reason>
- Benefit: <who gains what>
- Next: <next concrete step and owner>
- Author: operator=<person> session=<session-or-run-id> model=<model-id>
- Evidence: <verifiable PR, commit, or file link>
```

CLAIM entries record ownership handoffs and contain no work content:

```text
## YYYY-MM-DD HH:MM — CLAIM <lane-slug>
- Author: operator=<person> session=<session-or-run-id> model=<model-id>
- Takes over from: session=<previous-id or none> (reason: <takeover reason>)
```

The `operator=` field is required on every new entry. Current work uses `operator=tim`. Evidence must be verifiable; a completion claim without a PR, commit, or file link is not a landed-work narrative.

## Rules

- Stream files are append-only. Never edit, reorder, or delete an existing entry; corrections are new narrative entries.
- A lane is a unit of ownership with one pen-holder at a time, not a build-plan decomposition. One sequential session is one lane; split only where sessions can genuinely write concurrently, along the human division of work.
- Before taking over a lane, read its latest CLAIM and append a new CLAIM with the prior session and a reason. A narrative Author should match the current CLAIM holder; correct mismatches with a new entry.

## Write paths

1. By default, the board entry rides the same branch and PR as the work it describes; that PR is the Evidence.
2. Where repository rules allow, use a docs-only direct commit to main for post-hoc entries, corrections, and CLAIMs.
3. Use a standalone docs-only PR only when the work already merged and main is protected. Frequent standalone board PRs mean the default path is not being followed.

See the private [`ObjectiveFunction/build-board`](https://github.com/ObjectiveFunction/build-board) repository for the [full convention](https://github.com/ObjectiveFunction/build-board/blob/main/build-board-pilot-stage0.md), user guide, renderer, and rendered board.
