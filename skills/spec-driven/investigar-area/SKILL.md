---
name: investigar-area
description: Investigates a specific repository area using the general project map and one scoped investigation task, producing an evidence-backed report for that area. Use when the user asks to deepen understanding of a subsystem, execute a project investigation task, or analyze one part of the codebase without implementing changes. Do not use for project-wide mapping, feature implementation, or bug fixing.
---

# Area Investigation

## Procedures

**Step 1: Validate Inputs**
1. Confirm the project map path and the investigation task path.
2. Read both files completely before exploring code.
3. If paths are not provided, infer them from the same `./tasks/project-map-[project-slug]/` directory when possible.
4. Derive the output path: `./tasks/project-map-[project-slug]/results/[task-id]-[area-slug]-result.md`.
5. If the result file already exists, confirm before overwriting.

**Step 2: Rebuild Investigation Context (Mandatory)**
1. Extract scope, key questions, hypotheses, and starting points from the task.
2. Re-read `AGENTS.md` and any local instructions that apply to the relevant directories.
3. Read the files, configs, tests, docs, and symbols named in the map and task before expanding further.
4. Keep the investigation within the declared scope unless adjacent code is required to answer the task.

**Step 3: Investigate the Area Deeply (Mandatory)**
1. Trace the main runtime paths, data flow, boundaries, and integrations for the scoped area.
2. Identify the relevant modules, ownership boundaries, extension points, failure paths, and test coverage.
3. Separate confirmed facts from informed inference.
4. Capture file references and concrete evidence for important claims.
5. Record unknowns and contradictions instead of smoothing them over.

**Step 4: Generate the Area Report (Mandatory)**
1. Read the template at `assets/investigation-result-template.md`.
2. Create the directory `./tasks/project-map-[project-slug]/results/` if it does not exist.
3. Write the final report to `./tasks/project-map-[project-slug]/results/[task-id]-[area-slug]-result.md`.
4. Include answered questions, architecture notes, evidence, risks, open questions, and recommended next steps.
5. Keep the report focused on the task scope. Do not rewrite the entire project map.

**Step 5: Report Results**
1. Provide the output path for the investigation result.
2. Summarize the most important findings and unresolved questions.
3. Recommend whether another investigation task should be run next.

## Guidelines

- Treat `project-map.md` as shared context, not as ground truth.
- Use the task file as the boundary of the investigation.
- Prefer direct code evidence over assumptions or style guidance.
- Cite the files or symbols that justify each important finding.
- Do not implement fixes or refactors unless the user explicitly changes the request.

## Quality Checklist

- [ ] General project map read completely.
- [ ] Investigation task read completely.
- [ ] Relevant repository instructions re-checked for the scoped area.
- [ ] Report generated with the template.
- [ ] Findings backed by concrete evidence.
- [ ] Result saved under `./tasks/project-map-[project-slug]/results/`.
- [ ] Final path and summary reported to the user.

## Error Handling

- If `project-map.md` or the task file is missing, halt and direct the user to `mapear-projeto`.
- If the task scope is too broad, narrow it before proceeding and state the change clearly.
- If the evidence in code conflicts with the map or task, trust the code and record the mismatch in the report.
- If the output file already exists, confirm before overwriting.
