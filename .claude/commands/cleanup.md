You are running the /cleanup command. Your job is to audit the current codebase structure, report problems, and fix them with the user's approval.

## Phase 1: Scan

Analyze the project root and all subdirectories. Collect the following:

1. **File inventory**: Count total files, directories, and maximum nesting depth. Flag any nesting deeper than 4 levels.
2. **Large files**: Identify files over 500 lines (warning) and over 1000 lines (critical, "god files").
3. **Root junk**: Look for these in the project root: .bak files, scratch/temp files, old PRDs, multiple TODO/NOTES/CHANGELOG files that aren't actively used, random one-off scripts.
4. **Orphaned AI config**: Check for .cursorrules, .windsurfrules, .aider.conf.yml, .github/copilot.md, or other AI tool configs that aren't actively used alongside CLAUDE.md.
5. **CLAUDE.md check**: Does it exist? How many lines? Is it over 200 lines (bloated)?
6. **Organization style**: Is the codebase organized by type (controllers/, models/, views/) or by feature (auth/, billing/, dashboard/)? Type-based is an anti-pattern for AI navigation.
7. **Documentation duplication**: Are there multiple files covering the same topic? Is critical context scattered across README, CLAUDE.md, CONTRIBUTING, and random docs?
8. **Circular dependencies**: Look for obvious circular import patterns between modules.
9. **Convention files**: Check for .editorconfig, .prettierrc, tsconfig.json, eslint config. Note which are missing.

## Phase 2: Report

Present findings in this format:

```
# Codebase Cleanup Report

## 🔴 Critical
- [list critical issues: god files, junk drawer root, no CLAUDE.md, deep nesting]

## 🟡 Warning
- [list warnings: files 500-1000 lines, type-based org, bloated CLAUDE.md, missing convention files]

## 🟢 Good
- [list things already done well]

## Recommended Actions
1. [numbered list of specific actions you can take, ordered by impact]
```

## Phase 3: Fix

After presenting the report, ask the user: "Which of these would you like me to fix? I can handle all of them, or pick specific numbers."

Based on their response, execute the relevant fixes:

### Creating structure
- Create feature directories based on what the code actually does (e.g., auth/, billing/, api/, shared/)
- Create docs/ if it doesn't exist
- Create scripts/ and move loose scripts there

### Moving files
- Move files to their proper feature directories
- Move root junk to a scratch/ directory (or delete with explicit confirmation)
- Consolidate orphaned AI configs into CLAUDE.md where relevant, then remove the originals

### Splitting god files
- For files over 1000 lines, analyze the file and suggest logical split points based on class/function boundaries
- Propose the new file names and what goes in each
- Execute the split after user confirms

### CLAUDE.md management
If CLAUDE.md doesn't exist, generate one with this structure:

```markdown
# Project Name

## Overview
[one paragraph: what this project does, primary language/framework]

## Architecture
[key directories and what lives in each]

## Key Files
[map of the most important files and their purpose]

## Development
[how to run, test, and deploy]

## Conventions
[coding style, naming patterns, important rules]
```

If CLAUDE.md is bloated (over 200 lines), slim it down:
- Move detailed API docs, architecture deep-dives, and reference material to docs/
- Keep CLAUDE.md focused on what Claude needs to know to work in this codebase
- Add navigation comments pointing to the detailed docs

### Navigation comments
After reorganizing, update CLAUDE.md with a file map showing where key files moved:

```markdown
## File Map
- Authentication: src/features/auth/
- Database models: src/features/*/models/
- Shared utilities: src/shared/
- Scripts: scripts/
- Documentation: docs/
```

## Rules

- Always show what you plan to do before doing it
- Never delete files without explicit user confirmation. Default to moving to scratch/
- Preserve git history awareness: mention that the user should review `git diff` after cleanup
- If the project uses a framework with strong conventions (Rails, Next.js, Django), respect those conventions instead of imposing generic structure
- Be specific in your report. Don't say "some files are large." Say "src/api/handler.ts is 1,247 lines"
- Reference docs/patterns.md and docs/anti-patterns.md when explaining why something is a problem (if those files exist in the project)
