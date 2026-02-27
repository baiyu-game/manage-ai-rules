# manage-ai-rules

> A universal skill to manage AI IDE rule files across multiple platforms.

Unified management of rule files across AI IDEs. Support multi-platform rule creation, modification, deletion, project initialization, and cross-IDE synchronization.

## Features

- **Project Initialization** - Create project skeleton with core rule files
- **Create Rules** - Generate rule files with proper format and front matter
- **Modify Rules** - Update existing rules
- **Delete Rules** - Remove rules and update indexes
- **Cross-IDE Sync** - Synchronize rules between different AI IDEs with format conversion

## Supported AI IDEs

| IDE | Core File | Rules Directory | Front Matter |
|-----|-----------|-----------------|--------------|
| Claude Code | `CLAUDE.md` | - | No |
| Cursor | `.cursorrules` | `.cursor/rules/` | Yes |
| Windsurf | `.windsurfrules` | `.windsurf/rules/` | Yes |
| Trae | - | `.trae/rules/` | Yes |
| GitHub Copilot | `.github/copilot-instructions.md` | - | No |
| Universal | `AGENTS.md` | - | No |

## Installation

### Claude Code

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/[username]/manage-ai-rules ~/.claude/skills/manage-ai-rules
```

### Trae

```bash
mkdir -p ~/.trae/skills
git clone https://github.com/[username]/manage-ai-rules ~/.trae/skills/manage-ai-rules
```

### Cursor

```bash
mkdir -p ~/.cursor/skills
git clone https://github.com/[username]/manage-ai-rules ~/.cursor/skills/manage-ai-rules
```

### Windsurf

```bash
mkdir -p ~/.windsurf/skills
git clone https://github.com/[username]/manage-ai-rules ~/.windsurf/skills/manage-ai-rules
```

## Usage

### Initialize Project

When starting a new project, ask AI to create the rule file skeleton:

```
initialize project for Claude Code and Cursor
```

This will create:
```
your-project/
├── CLAUDE.md                    # Claude Code core file
├── .cursorrules                 # Cursor core file
└── .cursor/rules/
    ├── README.md                # Rules index
    └── update-rules.md          # Update mechanism
```

### Create Rule

```
create a search rule for document retrieval
```

AI will:
1. Ask for rule details
2. Generate proper front matter
3. Create the rule file
4. Update the rules index

### Modify Rule

```
modify the search rule
```

### Delete Rule

```
delete the search rule
```

### Cross-IDE Sync

```
sync rules from Claude Code to Cursor
```

AI will:
1. Read source IDE rules
2. Convert format (add/remove front matter)
3. Write to target IDE

## Rule File Format

### With Front Matter (Cursor/Windsurf/Trae)

```markdown
---
alwaysApply: false
description: search-rule - Search project docs efficiently
---
# Search Rule

[Rule content...]
```

### Without Front Matter (Claude Code/GitHub Copilot)

```markdown
# Search Rule

[Rule content...]
```

## Common Commands

| Command | Function |
|---------|----------|
| `initialize project` | Create project skeleton |
| `create [name] rule` | Create new rule |
| `modify [name] rule` | Modify existing rule |
| `delete [name] rule` | Delete rule |
| `sync rules to [IDE]` | Cross-IDE sync |

## Project Structure Example

A well-organized project with rules:

```
your-project/
├── CLAUDE.md                    # Core file (auto-loaded)
├── .cursorrules                 # Cursor core file
├── .cursor/
│   └── rules/
│       ├── README.md            # Rules index
│       ├── search.md            # Document search rule
│       ├── coding.md            # Coding standards rule
│       └── git.md               # Git commit rule
└── src/
    └── ...
```

## License

MIT License
