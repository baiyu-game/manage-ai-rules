---
name: manage-ai-rules
description: "Manage AI IDE rule files across Claude Code, Cursor, Windsurf, Trae, GitHub Copilot. Support create/modify/delete rules, project initialization, cross-IDE sync."
source: local
risk: safe
---

# AI IDE Rules Manager

Unified management of rule files across AI IDEs. Support multi-platform rule creation, modification, deletion, and synchronization.

## Trigger Scenarios

- User says "create rule", "new rule", "add rule"
- User says "modify rule", "update rule"
- User says "delete rule"
- User says "initialize project", "create project skeleton"
- User says "sync rules" (cross-IDE)
- Project has no core rule file

---

## Supported AI IDEs

| IDE | Core File | Rules Directory | Front Matter |
|-----|-----------|-----------------|--------------|
| Claude Code | `CLAUDE.md` | - | No |
| Cursor | `.cursorrules` | `.cursor/rules/` | Yes |
| Windsurf | `.windsurfrules` | `.windsurf/rules/` | Yes |
| Trae | - | `.trae/rules/` | Yes |
| GitHub Copilot | `.github/copilot-instructions.md` | - | No |
| Universal | `AGENTS.md` | - | No |

---

## Module 1: Project Initialization

### Detection Condition

Project root directory has no core rule file.

### Execution Flow

1. **Ask Target IDE**
   - Display supported IDE list
   - Support multi-select (e.g., Claude Code + Cursor)

2. **Create Project Skeleton**

   Based on selected IDEs, create corresponding structure:

   ```
   [project-root]/
   ├── CLAUDE.md                    # Claude Code (if selected)
   ├── .cursorrules                 # Cursor (if selected)
   ├── .windsurfrules               # Windsurf (if selected)
   ├── AGENTS.md                    # Universal (if selected)
   └── .[ide]/
       └── rules/
           ├── README.md            # Rules index
           └── update-rules.md      # Update mechanism
   ```

3. **Generate Core File Template**

### Core File Template

```markdown
# [Project Name]

[Brief description]

## Directory Structure

```
[Generated based on actual project structure]
```

## Core Principles

1. [Principle 1]
2. [Principle 2]

## Intent Recognition & Rule Loading

| User Intent | Action | Load Rule |
|-------------|--------|-----------|
| [intent] | [action] | [rule-file] |

## Rules Index

`.[ide]/rules/README.md`
```

### Completion Checklist

- [ ] Core rule file created (CLAUDE.md/.cursorrules etc.)
- [ ] Rules directory created (if applicable)
- [ ] README.md created
- [ ] update-rules.md created

---

## Module 2: Create Rule

### Execution Flow

1. **Collect Information**
   - Rule name (for file naming)
   - Rule purpose description
   - Trigger scenarios
   - Whether front matter is needed

2. **Auto Determine**
   - `alwaysApply`: `true` for core files, `false` for others
   - `description`: Formatted generation

3. **Generate File**
   - Choose correct path and format based on target IDE
   - Include front matter (if supported)

4. **Update Index**
   - Update README.md
   - Update core file (if needed)

### Front Matter Format

For IDEs that support front matter (Cursor, Windsurf, Trae):

```yaml
---
alwaysApply: false
description: [rule-name] - [core-function]
---
```

### alwaysApply Criteria

| Condition | Value |
|-----------|-------|
| Core rule file (CLAUDE.md/.cursorrules etc.) | `true` or no field |
| Specific task rules (default) | `false` |

### Description Guidelines

- Format: `[rule-name] - [core-function]`
- Limit: No more than 50 characters
- Example: `search-rule - Search project docs, distinguish official docs and drafts`

### File Naming Convention

- Use lowercase English
- Connect multiple words with hyphens
- Examples: `search.md`, `update-rules.md`

### Rule Content Format by IDE

**IDEs with Front Matter support (Cursor/Windsurf/Trae)**:
```markdown
---
alwaysApply: false
description: [description]
---
# [Rule Title]

[Rule content]
```

**IDEs without Front Matter support (Claude Code/GitHub Copilot)**:
```markdown
# [Rule Title]

[Rule content]
```

### Completion Checklist

- [ ] Rule file created at correct location
- [ ] Front Matter correct (if applicable)
- [ ] File name follows convention
- [ ] README.md updated
- [ ] Core file updated (if needed)

---

## Module 3: Modify Rule

### Execution Flow

1. **Read Existing Rule**
2. **Ask Modification Content**
3. **Execute Modification**
4. **Sync Check**

### Completion Checklist

- [ ] Rule content updated
- [ ] Front Matter updated (if needed)
- [ ] Index file synced

---

## Module 4: Delete Rule

### Execution Flow

1. **Confirm Deletion**
2. **Execute Deletion**
3. **Update Index**

### Completion Checklist

- [ ] Rule file deleted
- [ ] README.md updated
- [ ] Core file updated (if needed)

---

## Module 5: Cross-IDE Rule Sync

### Trigger Scenarios

- User says "sync rules to other IDE"
- User says "sync rules to Cursor/Windsurf/..."
- Project has multiple IDE configurations

### Execution Flow

1. **Detect Existing IDE Configurations**
   - Scan core files in project root
   - List configured IDEs

2. **Choose Sync Direction**
   - From which IDE to which IDE
   - Or sync all

3. **Execute Sync**
   - Read source IDE rules
   - Convert format (if needed)
   - Write to target IDE rule files

### Sync Rules

| Source IDE | Target IDE | Conversion Method |
|------------|------------|-------------------|
| Has Front Matter | No Front Matter | Remove front matter |
| No Front Matter | Has Front Matter | Add default front matter |
| Has Front Matter | Has Front Matter | Keep or adjust format |

---

## Index Update Rules

### README.md Update

Add/remove entries in rules table:

```markdown
| File | Purpose | Trigger Scenario |
|------|---------|------------------|
| `xxx.md` | [purpose] | [trigger] |
```

### Core File Update Conditions

Update core file when any of these conditions are met:

1. Added/deleted rule involves **core directory** management
2. Added/deleted rule involves **core responsibilities** (needs to be added to intent recognition table)
3. User explicitly requests update

---

## Output Format

### Create Success

```
✅ Rule file created

📄 File: [path]
📋 Description: [description]
🔄 Loading: alwaysApply: [true/false]
🎯 IDE: [IDE-name]

Synced updates:
- README.md
- [core-file] (if applicable)
```

### Initialization Success

```
✅ Project skeleton created

🎯 Target IDE: [IDE-list]

📄 File list:
- [core-file]
- [rules-dir]/README.md
- [rules-dir]/update-rules.md

Next step: Edit core file to fill in project info and directory structure
```

### Sync Success

```
✅ Rules synced

📤 Source IDE: [source-IDE]
📥 Target IDE: [target-IDE]
📄 Synced files: [count]

Sync details:
- [file1]: Converted and written
- [file2]: Converted and written
```

---

## Quick Reference

### Rule File Locations by IDE

| IDE | Core File | Rules Directory |
|-----|-----------|-----------------|
| Claude Code | `CLAUDE.md` | - |
| Cursor | `.cursorrules` | `.cursor/rules/` |
| Windsurf | `.windsurfrules` | `.windsurf/rules/` |
| Trae | - | `.trae/rules/` |
| GitHub Copilot | `.github/copilot-instructions.md` | - |
| Universal | `AGENTS.md` | - |

### Common Commands

| Command | Function |
|---------|----------|
| "initialize project" | Create project skeleton |
| "create [name] rule" | Create new rule |
| "modify [name] rule" | Modify existing rule |
| "delete [name] rule" | Delete rule |
| "sync rules to [IDE]" | Cross-IDE sync |
