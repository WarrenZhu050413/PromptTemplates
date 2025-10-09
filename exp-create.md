---
description: Create a new expansion (snippet or macro)
---

Create a new expansion using the expansions CLI.

Usage:
- Implicit (regex-based): Creates context snippets that inject when regex pattern matches
- Explicit ($keyword-based): Creates macros that expand when $keyword is used

Run this command with the following parameters:
- `--id`: Unique ID (required)
- `--name`: Human-readable name (required)
- `--type`: `implicit` or `explicit` (required)
- `--pattern`: Regex pattern (implicit) or $keyword (explicit) (required)
- `--files`: Content files (required, can be multiple)
- `--template`: Enable Jinja2 templating (optional)
- `--output-mode`: `context`, `replacement`, or `both` (optional, default: context for implicit, replacement for explicit)
- `--priority`: 0-100 (optional, default: 50)

Example commands:

**Create implicit expansion (snippet):**
```bash
python ~/.claude/expansions-dev/expansions_cli.py create \
  --id my-snippet \
  --name "My Snippet" \
  --type implicit \
  --pattern "\\bkeyword\\b" \
  --files content/snippet.md
```

**Create explicit expansion (macro) with template:**
```bash
python ~/.claude/expansions-dev/expansions_cli.py create \
  --id my-macro \
  --name "My Macro" \
  --type explicit \
  --pattern "$mymacro" \
  --files content/template.j2 \
  --template \
  --output-mode replacement
```

**What would you like to create?**
