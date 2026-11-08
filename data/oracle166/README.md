# Oracle task documents

This directory contains the **166 current `.task.md` execution guides** for MS-Eval.
The [first 2026-11-09 errata](ERRATA-2026-11-09.md) correct 26 orchestration plans without
changing their original task descriptions. A [subsequent four-task cleanup](ERRATA-2026-11-09-TASK-PROMPTS.md)
removes answer disclosures from ordinary tasks and Oracle prefixes, including
repeated market-result hints in one plan. The [published golden delegation tags](../../eval/delegation_appropriateness/delegate_gt_tag/README.md)
retain their original reviewed contexts through [historical source snapshots](../oracle166_history/README.md);
they have not been regenerated for the corrected guides.

Each filename defines a task ID by removing `.task.md`. The ID connects the task document, its golden-tag JSON, task-category lists, and execution summaries. Golden-tag records store the exact reviewed source path and SHA-256 in `source`; use those pinned paths when reproducing historical labels and scores. Corrected-guide evaluations require a separately reviewed annotation version.

Browse tasks by [domain](../task_categories/cluster_by_domain/README.md) or by [delegation category](../task_categories/cluster_by_delegation/README.md). The category READMEs link here. Task documents are not duplicated inside the category directories.
