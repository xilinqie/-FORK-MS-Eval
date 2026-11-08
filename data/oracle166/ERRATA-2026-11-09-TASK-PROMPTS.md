# Task-prompt answer disclosures — 2026-11-09

Four task descriptions contained computed results in examples or explanatory
parentheses. This revision replaces those values with placeholders or instructions
to use the queried data. Both the ordinary task in the pinned gym submodule and
its prefix in `data/oracle166/` are updated, so SA, Spec, Gen, Plan-1st and Oracle
receive the same cleaned task description.

| Task | Change |
| --- | --- |
| [canvas-semester-summary-ppt](canvas-semester-summary-ppt.task.md) | Replace the actual largest course and student count with format placeholders. |
| [terminal-sf-wc-order-audit-excel-word](terminal-sf-wc-order-audit-excel-word.task.md) | Remove the prefilled product count; retain complete pagination and all report fields. |
| [terminal-wc-yf-ppt-notion-email](terminal-wc-yf-ppt-notion-email.task.md) | Remove expected stock returns and named category winners/underperformers from analysis and email instructions; derive them from source data. Remove repeated result hints from the Oracle plan as well. |
| [terminal-yf-canvas-excel-gcal-email](terminal-yf-canvas-excel-gcal-email.task.md) | Replace the two answer-matching event descriptions with a neutral placeholder example. |

The full-history return definition, market-event window/ranking/rounding rules,
pagination, filenames, output schemas and recipients are retained. The market
task's five explicitly requested Notion initiatives remain fixed task inputs.
Ground-truth deliverables, data fixtures and task evaluators are unchanged; this
is a cleanup of these specific prompt disclosures, not an exhaustive certification
of the entire benchmark or every task-visible input.

## Sources and runtime

The gym dependency is now pinned to the corresponding commit in
[`xilinqie/-FORK-toolathlon_gym`](https://github.com/xilinqie/-FORK-toolathlon_gym/tree/fix/task-answer-disclosure-20261109).
The submodule gitlink and `docker/locks/reference.json` identify the same revision.
The [machine-readable manifest](../oracle166_history/2026-11-09-task-prompts.json)
records the original and corrected hashes for all four ordinary tasks and Oracle
documents. Initialize the new pinned source after checking out this revision:

```bash
git submodule sync -- toolathlon_gym
git submodule update --init --recursive
```

Rebuild the Docker or Enroot runtime before new benchmark runs: an older image
still contains its original ordinary task files. Results must identify the source
and runtime revision used.

## Historical labels and results

The original published contexts remain archived under
[`oracle166_history/4c1bbd3/`](../oracle166_history/README.md). Three additional
golden records now point to those snapshots; their source hashes, cache keys,
reviewed labels and counts are unchanged. The finance-workshop record already
pointed to its original context after the earlier 26-plan correction.

For that overlapping task, the intermediate corrected plan at commit `5a0753a`
is additionally preserved under `oracle166_history/5a0753a/`. The earlier
[26-plan manifest](../oracle166_history/2026-11-09.json) points its corrected-source
entry to this intermediate snapshot, retaining its original hash and the fact
that the first correction did not change task text. The new manifest records the
subsequent prompt cleanup separately.

Existing human annotations, released scores and model traces have not been
recomputed. The current guides require a separately reviewed annotation version
and new executions before reporting new `F1_hit`/MSQ or performance values.

## Validation

```bash
python3 -m unittest discover -s eval/tests -v
```

The offline checks cover archived provenance, stale-label rejection, ordinary
task/Oracle prefix parity, removal of the identified answer hints, and runtime
source-lock consistency. They do not run the four MCP workflows or estimate an
effect on model performance.
