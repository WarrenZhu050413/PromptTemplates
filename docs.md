# Claude Code Documentation Browser

Access Claude Code documentation instantly without leaving your terminal.

## Usage
`/docs [topic] [-t|--test]`

## Examples
- `/docs` - View main documentation
- `/docs hooks` - View hooks documentation
- `/docs mcp` - View MCP documentation
- `/docs memory` - View memory documentation
- `/docs -t` - Test freshness and update if needed

## Topics
hooks, mcp, memory, agents, prompts, settings, slash-commands, github-actions, and more

## Options
- `-t`, `--test`: Check freshness and force update if needed

## Handler
```bash
~/.claude-code-docs/claude-docs-helper.sh "$@"
```

This command provides instant access to local Claude Code documentation.
