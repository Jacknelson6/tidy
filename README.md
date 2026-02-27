<p align="center">
  <img src="assets/logo.jpg" alt="Tidy" width="400"/>
</p>

<h1 align="center">Tidy</h1>
<p align="center"><strong>Stop burning tokens on disorganized code.</strong></p>

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-skill-blueviolet)](https://docs.anthropic.com/en/docs/claude-code)

A Claude Code skill that audits your codebase structure, reports problems, and fixes them. One command to go from messy to maintainable.

## Why This Matters

Disorganized codebases burn Claude's context window on noise. Every god file, junk drawer root, and duplicated doc eats tokens that should be spent on your actual task.

The costs are real:
- **God files** (1000+ lines) force Claude to ingest thousands of irrelevant lines to find one function
- **Type-based organization** makes Claude jump across directories to understand a single feature
- **Bloated CLAUDE.md** files eat context before Claude even looks at your code
- **Deep nesting** produces wrong import paths and confused file references
- **Barrel export mazes** hide where code actually lives, wasting reads on re-export files

A clean codebase means faster responses, better output, and fewer wasted tokens.

## Installation

Copy the `.claude/` directory into your project:

```bash
# Clone the repo
git clone https://github.com/Jacknelson6/tidy.git

# Copy the command into your project
cp -r tidy/.claude your-project/.claude
```

Or just grab the command file directly:

```bash
mkdir -p your-project/.claude/commands
curl -o your-project/.claude/commands/tidy.md \
  https://raw.githubusercontent.com/Jacknelson6/tidy/main/.claude/commands/tidy.md
```

Optionally, copy the reference docs:

```bash
cp -r tidy/docs your-project/docs
```

## Usage

Open Claude Code in your project and run:

```
/tidy
```

Claude will:

1. **Detect** your framework (Next.js, Rails, Django, etc.) and respect its conventions
2. **Scan** your codebase for structural problems
3. **Report** findings as Critical (🔴), Warning (🟡), and Good (🟢)
4. **Dry run** showing exactly what it plans to change
5. **Execute** the fixes after you confirm

### What It Checks

| Check | What It Finds |
|-------|--------------|
| God files | Files over 1000 lines that should be split |
| Junk drawer root | .bak files, scratch files, old PRDs cluttering the root |
| Orphaned AI configs | .cursorrules, .windsurfrules, .aider.conf.yml sitting unused |
| CLAUDE.md health | Missing, bloated, or poorly structured |
| Organization style | Type-based vs feature-based directory structure |
| Deep nesting | Directories nested more than 4 levels deep |
| Doc duplication | Same information repeated across multiple files |
| Convention files | Missing .editorconfig, .prettierrc, tsconfig.json |
| Barrel export maze | index.ts files that re-export everything, hiding source locations |
| Circular imports | Modules that import each other, confusing the dependency graph |

### Example Output

```
# Tidy Report

**Framework detected:** Next.js
**Files:** 847 | **Directories:** 94 | **Max depth:** 5

## 🔴 Critical
- src/api/handlers.ts is 1,847 lines (god file)
- No CLAUDE.md found
- 12 non-config files in project root
- src/modules/features/auth/handlers/middleware/ nested 6 levels deep

## 🟡 Warning
- src/utils/helpers.ts is 623 lines
- Type-based organization detected in src/services/, src/models/
- Missing .editorconfig and .prettierrc
- src/components/index.ts re-exports 34 modules (barrel export maze)

## 🟢 Good
- Tests are co-located with features
- No circular import patterns detected
- tsconfig.json and eslint config present

## Recommended Actions
1. Split src/api/handlers.ts into per-resource handler files
2. Generate CLAUDE.md with project overview and file map
3. Move 12 root junk files to scratch/
4. Flatten deep nesting in src/modules/features/
5. Add .editorconfig and .prettierrc
```

## Before and After

**Before /tidy:**
```
project/
  src/
  TODO.md
  TODO-old.md
  scratch.py
  old-prd-v2.md
  backup.sql.bak
  .cursorrules
  .windsurfrules
  package.json
```

**After /tidy:**
```
project/
  src/
  docs/
    architecture.md
  scratch/
    TODO-old.md
    scratch.py
    old-prd-v2.md
    backup.sql.bak
  scripts/
  CLAUDE.md
  README.md
  package.json
  .editorconfig
  .prettierrc
```

## Reference Docs

- [Organization Patterns](docs/patterns.md): Feature-based layout, progressive docs, CLAUDE.md best practices
- [Anti-Patterns](docs/anti-patterns.md): Junk drawer roots, god files, deep nesting, barrel export mazes, and how to fix them

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed and configured
- That's it

## Author

Jack Nelson ([@JackHnels](https://x.com/JackHnels))

## License

[MIT](LICENSE)
