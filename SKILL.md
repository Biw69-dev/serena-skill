---
name: serena
description: "Use Serena MCP for IDE-grade, symbol-level code intelligence when a coding task depends on repository structure: exploring an unfamiliar codebase, finding definitions or references, tracing call paths, making symbol-aware edits, checking diagnostics, or answering where a function/class is used or defined."
---

# Serena

## Core Rule

Use Serena before broad file reading when the task depends on code structure. Prefer symbol tools for definitions, references, call paths, precise edits, and diagnostics. For small files, config, logs, literal strings, or when Serena is unavailable, use direct reads or `rg`.

## Start a Session

1. Call Serena `initial_instructions` if available.
2. Activate the project path the user named. If no path is named, use the current workspace or repo root.
3. Check whether onboarding has already been performed.
4. Run onboarding only when needed.
5. List or read Serena project memories only when prior project context may affect the task.

Typical flow:

```text
initial_instructions()
activate_project(<path>)
check_onboarding_performed()
onboarding()  # only if needed
list_memories()  # only when relevant
```

## Explore Code

Use the narrowest available Serena operation:

- `get_symbols_overview(<file>)` to inspect a file's top-level structure.
- `find_symbol(<name>)` to locate a class, method, function, property, or field.
- `find_referencing_symbols(<symbol>)` to find callers and usages.
- `search_for_pattern(<pattern>)` only for text that is not a code symbol, such as config keys, log messages, UI labels, or literal strings.

If the needed Serena tool is not available in the current session, fall back to `rg` and targeted file reads.

## Edit Code

Before changing code, inspect references when the symbol is shared or public.

Prefer available Serena symbol-edit tools:

- `replace_symbol_body` for replacing a function, method, or class body.
- `insert_before_symbol` or `insert_after_symbol` for precise additions.

For rename, delete, implementation lookup, content replacement, or diagnostics, use the Serena operation only if it is exposed in the current session. Otherwise use the repo's normal tooling and report the fallback.

## Review Or Debug

For reviews and bug fixes:

1. Reproduce or identify the exact failing path when possible.
2. Use `find_symbol` and `find_referencing_symbols` to trace the real call path.
3. Check diagnostics or run project tests/builds after edits when available.
4. Record reusable project findings only when memory writes are allowed and appropriate.

## Avoid

- Do not read large files end to end just to find one symbol.
- Do not do text-only rename for classes, methods, properties, or variables.
- Do not skip onboarding in a new project unless Serena confirms it was already done.
- Do not trust guessed architecture when Serena can show definitions, references, and diagnostics.
