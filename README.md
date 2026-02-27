# Claude Codebase Cleanup

**Stop burning tokens on disorganized code. Let Claude clean it up.**

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

A clean codebase means faster responses, better output, and fewer wasted tokens.

## Installation

Copy the `.claude/` directory into your project:

```bash
# Clone the repo
git clone https://github.com/Jacknelson6/claude-codebase-cleanup.git

# Copy the command into your project
cp -r claude-codebase-cleanup/.claude your-project/.claude
```

Or just grab the command file directly:

```bash
mkdir -p your-project/.claude/commands
curl -o your-project/.claude/commands/cleanup.md \
  https://raw.githubusercontent.com/Jacknelson6/claude-codebase-cleanup/main/.claude/commands/cleanup.md
```

Optionally, copy the reference docs:

```bash
cp -r claude-codebase-cleanup/docs your-project/docs
```

## Usage

Open Claude Code in your project and run:

```
/cleanup
```

Claude will:

1. **Scan** your codebase for structural problems
2. **Report** findings as Critical (🔴), Warning (🟡), and Good (🟢)
3. **Ask** what you want to fix
4. **Execute** the fixes: move files, split god files, create directories, generate or slim down CLAUDE.md

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

### Example Output

```
# Codebase Cleanup Report

## 🔴 Critical
- src/api/handlers.ts is 1,847 lines (god file)
- No CLAUDE.md found
- 12 non-config files in project root

## 🟡 Warning
- src/utils/helpers.ts is 623 lines
- Type-based organization detected (controllers/, models/, services/)
- Missing .editorconfig and .prettierrc

## 🟢 Good
- Maximum nesting depth is 3 levels
- Tests are co-located with features
- No circular import patterns detected
```

## Reference Docs

- [Organization Patterns](docs/patterns.md): Feature-based layout, progressive docs, CLAUDE.md best practices
- [Anti-Patterns](docs/anti-patterns.md): Junk drawer roots, god files, deep nesting, and how to fix them

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed and configured
- That's it

## Author

Jack Nelson ([@JackHnels](https://x.com/JackHnels))

## License

[MIT](LICENSE)
