---
description: Update an existing expansion
---

Update an expansion's configuration.

Usage:
```bash
python ~/.claude/expansions-dev/expansions_cli.py update EXPANSION_ID [OPTIONS]
```

Available options:
- `--name NAME`: Update the name
- `--pattern PATTERN`: Update the trigger pattern
- `--priority N`: Update priority (0-100)
- `--enabled true|false`: Enable or disable
- `--output-mode MODE`: Change output mode (context/replacement/both)
- `--description DESC`: Update description

Example:
```bash
python ~/.claude/expansions-dev/expansions_cli.py update my-expansion \
  --priority 75 \
  --enabled true \
  --output json
```

**Which expansion would you like to update? Provide the ID and options.**
