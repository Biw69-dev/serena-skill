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
```

## Explore Code

Use the narrowest useful Serena operation:

- `get_symbols_overview(<file>)` to inspect a file's top-level structure.
- `find_symbol(<name>)` to locate a class, method, function, property, or field.
- `find_declaration(<symbol>)` to jump to the actual definition.
- `find_referencing_symbols(<symbol>)` to find callers and usages.
- `find_implementations(<interface_or_base>)` to inspect implementations.
- `search_for_pattern(<pattern>)` only for text that is not a code symbol, such as config keys, log messages, UI labels, or literal strings.

## Edit Code

Before changing code, inspect references when the symbol is shared or public.

Prefer:

- `replace_symbol_body` for replacing a function, method, or class body.
- `insert_before_symbol` or `insert_after_symbol` for precise additions.
- `rename_symbol` for real refactors.
- `safe_delete_symbol` when removing code.
- `replace_content` only for contained text edits where symbol tools do not apply.

After edits, run diagnostics on the changed files:

```text
get_diagnostics_for_file(<changed-file>)
```

## Review Or Debug

For reviews and bug fixes:

1. Reproduce or identify the exact failing path when possible.
2. Use `find_symbol` and `find_referencing_symbols` to trace the real call path.
3. Use diagnostics before and after edits.
4. Record useful project-specific findings with `write_memory` when they will help future sessions.

## Avoid

- Do not read large files end to end just to find one symbol.
- Do not do text-only rename for classes, methods, properties, or variables.
- Do not skip onboarding in a new project unless Serena confirms it was already done.
- Do not try to guess the architecture when Serena can show definitions, references, and diagnostics.
