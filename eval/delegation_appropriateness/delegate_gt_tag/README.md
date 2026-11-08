# Golden Delegation Tags

English | [简体中文](README.zh-CN.md)

Reviewed golden labels used by the [DA evaluator](../README.md): one JSON file per task plus `_index.json`. Of the 166 tasks, 89 require delegation and 77 do not; together they define 265 golden sub-agent units.

These are the **published-version labels**. The [2026-11-09 execution-guide corrections](../../../data/oracle166/ERRATA-2026-11-09.md)
and [four-task prompt cleanup](../../../data/oracle166/ERRATA-2026-11-09-TASK-PROMPTS.md)
do not constitute a new LLM review: the affected records point to exact historical
source snapshots, preserving their source hashes, cache keys, labels and counts.
Do not treat these labels or existing scores as a re-evaluation of the corrected guides.

## Format

| Field | Contents |
| --- | --- |
| `task`, `need_delegation` | Task ID and whether delegation is required |
| `waves`, `nodes` | Golden sub-agent assignments with function labels |
| `units`, `bag`, `counts` | Matching units and their counts |
| `roles`, `write_labels`, `domains`, `matchable_roles` | Label vocabulary; `other-write` is not matchable ([details](../README.md#matching)) |
| `source` | Source task document in [`data/oracle166`](../../../data/oracle166/README.md) and its SHA-256 |
| `reviewer`, `prompt_version`, `system_sha256`, `label_cache_keys` | Labeling provenance |

Schema `delegate-gt-tag-v4`, vocabulary `expanded-20260912-v2`, prompt `expanded-20260912-llm-v2`, reviewer `deepseek-v4-flash`.

## Regenerate

```bash
python3 -m eval.delegation_appropriateness.export_delegate_gt_tags --out results/regenerated_gt
```

Rebuilds labels and derived fields offline from the existing nodes, their pinned source contexts and the [label cache](../delegate_llm_tag_cache/README.md); identical inputs give identical files. To update this directory in place, pass `--out eval/delegation_appropriateness/delegate_gt_tag`. An explicit `--oracle` overrides the source directory only when its hashes match the reviewed records; corrected sources require a separate labeling version.
