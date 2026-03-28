---
name: consolidar-investigacoes
description: Consolidates the outputs of `mapear-projeto` and multiple `investigar-area` runs into a single synthesized repository document. Use when the user asks to unify `project-map.md`, `investigation-backlog.md`, task files, and investigation result files into one report for onboarding, architectural review, or handoff. Do not use for creating the initial map, executing one investigation task, or implementing code changes.
---

# Investigation Consolidation

## Procedures

**Step 1: Validate Inputs**
1. Confirm the path to `project-map.md`.
2. Confirm the path to `investigation-backlog.md`.
3. If paths are not provided, infer them from the same `./tasks/project-map-[project-slug]/` directory when possible.
4. Derive the task directory as `./tasks/project-map-[project-slug]/tasks/`.
5. Derive the results directory as `./tasks/project-map-[project-slug]/results/`.
6. Derive the output path as `./tasks/project-map-[project-slug]/project-map-consolidated.md`.
7. If the output file already exists, confirm before overwriting.

**Step 2: Verify Consolidation Coverage (Mandatory)**
1. Read `investigation-backlog.md` completely before inspecting the results.
2. Read every task file referenced by the backlog.
3. Inventory the expected result files for each task.
4. Compare expected tasks against the files present in `results/`.
5. Mark the consolidation status as:
   - `Complete` when every scoped task has a corresponding result file.
   - `Partial` when some result files are missing but the user explicitly wants an interim consolidation.
6. If result coverage is incomplete, list the missing tasks clearly before writing the final document.

**Step 3: Rebuild the Full Investigation Corpus (Mandatory)**
1. Read `project-map.md`, `investigation-backlog.md`, every task file, and every result file completely.
2. Treat investigation result files as the deepest source among the generated artifacts.
3. Preserve traceability by keeping task IDs, area names, and file paths attached to important findings.
4. Separate confirmed facts, informed inference, contradictions, and unresolved gaps.
5. Identify cross-cutting themes that only become visible when the individual investigations are combined.

**Step 4: Generate the Consolidated Document (Mandatory)**
1. Read the template at `assets/project-map-consolidated-template.md`.
2. Write the final document to `./tasks/project-map-[project-slug]/project-map-consolidated.md`.
3. Synthesize the shared architecture, boundaries, flows, dependencies, risks, and open questions across all investigations.
4. Include a coverage matrix showing which tasks were consolidated and which are still missing.
5. Merge overlapping findings instead of concatenating every source document verbatim.
6. If a result file contradicts the original map, keep the contradiction explicit and prefer the deeper investigation evidence.
7. Keep the final document concise enough to be used as the primary onboarding artifact for the mapped repository.

**Step 5: Report Results**
1. Provide the output path for the consolidated document.
2. Summarize the main cross-cutting findings and the highest-risk unresolved gaps.
3. State whether the consolidation is `Complete` or `Partial`.
4. If any investigations are still missing, recommend the next task IDs to execute before treating the dossier as final.

## Guidelines

- Synthesize, do not concatenate.
- Use the map, backlog, tasks, and result files as source artifacts, not as unquestioned truth.
- Preserve task IDs and file references so the user can drill back into the original evidence.
- Highlight cross-area dependencies, recurring hotspots, and duplicated risks.
- Keep the consolidated document readable by someone who has not read the individual task outputs.
- Do not implement fixes or refactors during consolidation.

## Quality Checklist

- [ ] `project-map.md` read completely.
- [ ] `investigation-backlog.md` read completely.
- [ ] Every scoped task file read completely.
- [ ] Every available result file read completely.
- [ ] Coverage matrix built before synthesis.
- [ ] Consolidated document generated with the template.
- [ ] Missing investigations, if any, called out explicitly.
- [ ] Output saved under `./tasks/project-map-[project-slug]/project-map-consolidated.md`.
- [ ] Final path and consolidation status reported to the user.

## Error Handling

- If `project-map.md` or `investigation-backlog.md` is missing, halt and direct the user to `mapear-projeto`.
- If the task files are missing, halt and direct the user to regenerate the investigation backlog from `mapear-projeto`.
- If no result files exist yet, halt and direct the user to `investigar-area`.
- If only some result files exist, ask whether a partial consolidation is acceptable before generating the document.
- If the generated artifacts disagree with each other, preserve the disagreement explicitly and explain which artifact appears stronger.
- If the output file already exists, confirm before overwriting.
