---
description: "Create a structured execution plan based on an existing markdown file"
---

# from-file

Create a structured execution plan based on an existing markdown file.

## Arguments

- `file_path` (required): Path to the markdown file containing the task/feature description
- `--type` (optional): Work type template to use (feature, bugfix, refactor, migration, performance)

## Instructions

You are a planning assistant. Create a structured plan based on the content of a file.

### Step 1: Read the File

Read the file at the specified path: `$ARGUMENTS`

Extract the file path and optional `--type` parameter:
- If arguments contain `--type <type>`, use that template
- If no type specified, analyze the content to determine the best template

### Step 2: Analyze Content

Read and understand the file content. Look for:
- What is being requested/described?
- What is the scope and complexity?
- Are there acceptance criteria or requirements listed?
- What type of work is this? (feature, bugfix, refactor, migration, performance)

### Step 3: Select Template

If `--type` was specified, use that template. Otherwise, auto-detect:

| Content indicators | Template |
|-------------------|----------|
| "add", "implement", "create", "new feature" | feature |
| "fix", "bug", "issue", "broken", "error" | bugfix |
| "refactor", "restructure", "clean up", "improve code" | refactor |
| "migrate", "move", "upgrade", "convert" | migration |
| "performance", "optimize", "slow", "speed", "latency" | performance |

### Step 4: Generate Plan

Using the selected template, generate a structured plan that:
1. Uses the **phases** from the template
2. Creates **specific tasks** based on the file content
3. Includes **verifiable promises** from the template
4. Incorporates any requirements/criteria from the file

Output format:
```
## Plan: [Title derived from file content]

**Source:** [file path]
**Template:** [selected template type]

### Phase 1: [Phase Name from template]
**Tasks:**
- [ ] [Task derived from file content]
- [ ] ...

**Completion Criteria:** [From template + file specifics]

[Continue for all phases...]

---

**Total Tasks:** [count]
**Estimated Iterations:** [count × 3]

🏷️ **Promise Tag:** [Verifiable promises from template]
```

### Step 5: Generate Loop Command

```
Ready to execute? Run:
/ralph-wiggum:ralph-loop [estimated iterations] "[brief summary]"
```

## Examples

```
/ralph-planner:from-file "./docs/auth-feature.md"
/ralph-planner:from-file "./issues/bug-123.md" --type bugfix
/ralph-planner:from-file "./specs/api-migration.md" --type migration
```

## Guidelines

- Preserve important details from the source file
- Map file requirements to specific tasks
- If file has acceptance criteria, incorporate into completion criteria
- Auto-detection is best-effort; use `--type` when certain
