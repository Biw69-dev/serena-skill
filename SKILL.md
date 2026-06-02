---
name: serena
description: Use Serena MCP for IDE-grade, symbol-level code intelligence over real codebases. Use when exploring an unfamiliar repository, finding definitions or references, understanding call sites, renaming or deleting symbols, making precise cross-file edits, checking diagnostics, or when the user asks where a function/class is used or defined.
---

# Serena

## Core Rule

Use Serena before broad file reading when the task depends on code structure. Prefer symbol tools for definitions, references, renames, body replacement, and diagnostics. Small files can still be read directly when that is simpler.

## Start a Session

1. Activate the project path the user named.
2. Check whether onboarding has already been performed.
3. Run onboarding only when needed.
4. List memories if prior project context may affect the task.

Typical flow:

```text
activate_project(<path>)
check_onboarding_performed()
onboarding()  # only if needed
list_memories()
