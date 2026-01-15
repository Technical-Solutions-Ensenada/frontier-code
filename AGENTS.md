# Repository Guidelines

## How to Use This Guide

- Start here for cross-project norms.
- Each component has an `AGENTS.md` file with specific guidelines (e.g., `api/AGENTS.md`, `ui/AGENTS.md`).
- Component docs override this file when guidance conflicts.

## Available Skills

Use these skills for detailed patterns on-demand:

### Generic Skills (Any Project)

| Skill | Description | URL |
|-------|-------------|-----|
| `typescript` | Const types, flat interfaces, utility types | [SKILL.md](skills/typescript/SKILL.md) |
| `tailwind-4` | cn() utility, no var() in className | [SKILL.md](skills/tailwind-4/SKILL.md) |

### Project-Specific Skills

| Skill | Description | URL |
|-------|-------------|-----|
| `skill-creator` | Create new AI agent skills | [SKILL.md](skills/skill-creator/SKILL.md) |

### Auto-invoke Skills

When performing these actions, ALWAYS invoke the corresponding skill FIRST:

| Action | Skill |
|--------|-------|
| After creating/modifying a skill|`skill-sync`|

---

## Project Overview
