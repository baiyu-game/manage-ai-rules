# manage-ai-rules

[English](README.md) | 简体中文

> 一个通用的 Skill，用于跨多个平台管理 AI IDE 规则文件。

统一管理各类 AI IDE 的规则文件，支持多平台规则创建、修改、删除、项目初始化和跨 IDE 同步。

## 功能特性

- **项目初始化** - 创建项目骨架和核心规则文件
- **创建规则** - 生成正确格式和 front matter 的规则文件
- **修改规则** - 更新现有规则
- **删除规则** - 删除规则并更新索引
- **跨 IDE 同步** - 在不同 AI IDE 之间同步规则，自动转换格式

## 支持的 AI IDE

| IDE | 核心文件 | 规则目录 | Front Matter |
|-----|---------|---------|-------------|
| Claude Code | `CLAUDE.md` | - | 无 |
| Cursor | `.cursorrules` | `.cursor/rules/` | 支持 |
| Windsurf | `.windsurfrules` | `.windsurf/rules/` | 支持 |
| Trae | - | `.trae/rules/` | 支持 |
| GitHub Copilot | `.github/copilot-instructions.md` | - | 无 |
| 通用 | `AGENTS.md` | - | 无 |

## 安装

### Claude Code

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/baiyu-game/manage-ai-rules ~/.claude/skills/manage-ai-rules
```

### Trae

```bash
mkdir -p ~/.trae/skills
git clone https://github.com/baiyu-game/manage-ai-rules ~/.trae/skills/manage-ai-rules
```

### Cursor

```bash
mkdir -p ~/.cursor/skills
git clone https://github.com/baiyu-game/manage-ai-rules ~/.cursor/skills/manage-ai-rules
```

### Windsurf

```bash
mkdir -p ~/.windsurf/skills
git clone https://github.com/baiyu-game/manage-ai-rules ~/.windsurf/skills/manage-ai-rules
```

## 使用方法

### 初始化项目

开始新项目时，让 AI 创建规则文件骨架：

```
为 Claude Code 和 Cursor 初始化项目
```

这将创建：
```
your-project/
├── CLAUDE.md                    # Claude Code 核心文件
├── .cursorrules                 # Cursor 核心文件
└── .cursor/rules/
    ├── README.md                # 规则索引
    └── update-rules.md          # 更新机制
```

### 创建规则

```
创建一个文档检索规则
```

AI 将：
1. 询问规则详情
2. 生成正确的 front matter
3. 创建规则文件
4. 更新规则索引

### 修改规则

```
修改检索规则
```

### 删除规则

```
删除检索规则
```

### 跨 IDE 同步

```
把规则从 Claude Code 同步到 Cursor
```

AI 将：
1. 读取源 IDE 规则
2. 转换格式（添加/移除 front matter）
3. 写入目标 IDE

## 规则文件格式

### 带 Front Matter（Cursor/Windsurf/Trae）

```markdown
---
alwaysApply: false
description: search-rule - 高效搜索项目文档
---
# 检索规则

[规则内容...]
```

### 不带 Front Matter（Claude Code/GitHub Copilot）

```markdown
# 检索规则

[规则内容...]
```

## 常用命令

| 命令 | 功能 |
|-----|------|
| `初始化项目` | 创建项目骨架 |
| `创建 [名称] 规则` | 创建新规则 |
| `修改 [名称] 规则` | 修改现有规则 |
| `删除 [名称] 规则` | 删除规则 |
| `同步规则到 [IDE]` | 跨 IDE 同步 |

## 项目结构示例

一个组织良好的规则项目：

```
your-project/
├── CLAUDE.md                    # 核心文件（自动加载）
├── .cursorrules                 # Cursor 核心文件
├── .cursor/
│   └── rules/
│       ├── README.md            # 规则索引
│       ├── search.md            # 文档检索规则
│       ├── coding.md            # 编码规范规则
│       └── git.md               # Git 提交规则
└── src/
    └── ...
```

## 许可证

MIT License
