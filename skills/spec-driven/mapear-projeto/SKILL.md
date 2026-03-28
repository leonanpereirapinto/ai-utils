---
name: mapear-projeto
description: Maps an unfamiliar repository using a spec-driven workflow, producing a general project map plus a backlog of scoped investigation tasks for deeper analysis. Use when the user asks to map a codebase, understand repository structure, plan onboarding, or break repository research into focused investigation tasks. Do not use for feature implementation, bug fixing, or single-feature technical specs.
---

# Project Mapping

## Procedures

**Step 1: Validate Prerequisites**
1. Confirm the repository root or working directory to analyze.
2. Capture any explicit scope limits from the user, such as directories to prioritize or ignore.
3. Derive the project slug from the repository directory name.
4. Define the output directory: `./tasks/project-map-[project-slug]/`.
5. If `project-map.md`, `investigation-backlog.md`, or existing task files already exist, confirm before overwriting.

**Step 2: Build a Breadth-First Repository Map (Mandatory)**
1. Read `AGENTS.md` and any nearby instructions before drawing conclusions.
2. Inspect top-level directories, representative modules, entrypoints, manifests, configs, docs, and test structure.
3. Identify the main languages, frameworks, execution surfaces, storage layers, integrations, and validation strategy.
4. Capture evidence from concrete files instead of guessing behavior.
5. Mark unknowns explicitly when the repository does not provide enough evidence.

**Step 3: Define Investigation Areas (Mandatory)**
1. Cluster the repository into 4 to 10 investigation areas based on architecture, workflows, or business domains.
2. For each area, define:
   - Why the area matters.
   - Which directories, files, or symbols are likely starting points.
   - What questions still need deeper analysis.
   - What a good investigation result should clarify.
3. Present the proposed investigation areas to the user for alignment before writing files.

**Step 4: Generate the General Map (Mandatory)**
1. Read the template at `assets/project-map-template.md`.
2. Generate `project-map.md` using evidence gathered in Steps 1 to 3.
3. Keep the document concise and scannable.
4. Include repository structure, major subsystems, execution model, testing posture, conventions, risks, and open questions.
5. Do not turn the general map into a deep dive for one area. Reserve depth for the investigation tasks.

**Step 5: Generate the Investigation Backlog and Tasks (Mandatory)**
1. Read the template at `assets/investigation-backlog-template.md`.
2. Read the template at `assets/investigation-task-template.md`.
3. Create the directory `./tasks/project-map-[project-slug]/tasks/`.
4. Create `./tasks/project-map-[project-slug]/project-map.md`.
5. Create `./tasks/project-map-[project-slug]/investigation-backlog.md`.
6. Create one task file per approved area at `./tasks/project-map-[project-slug]/tasks/[nn]-[area-slug].md`.
7. Make every task self-contained so `investigar-area` can execute it without hidden context.
8. Each task must define scope, key questions, starting points, expected deliverable, and success criteria.

**Step 6: Report Results**
1. Provide the output directory and all generated file paths.
2. Recommend a sensible execution order for the first investigation tasks.
3. Highlight the highest-risk unknowns surfaced during mapping.

## Guidelines

- Prefer breadth first, then depth.
- Use evidence from the repository, not assumptions from similar stacks.
- Keep the general map short enough to be useful as shared context.
- Split investigation tasks by coherent area, not by arbitrary file count.
- Keep task scope narrow enough to finish in one focused investigation pass.
- Do not implement changes while mapping.

## Quality Checklist

- [ ] Repository instructions read before analysis.
- [ ] General map created with the template.
- [ ] Investigation backlog created with the template.
- [ ] Individual task files created for each approved area.
- [ ] Each task includes scope, questions, starting points, deliverable, and success criteria.
- [ ] Output saved under `./tasks/project-map-[project-slug]/`.
- [ ] Final file paths reported to the user.

## Error Handling

- If the repository root or scope is unclear, ask the user before generating files.
- If the codebase is too large for one pass, map the highest-value areas first and mark the rest as deferred.
- If the proposed investigation areas are not approved by the user, revise them before generating files.
- If any target output file already exists, confirm before overwriting.
