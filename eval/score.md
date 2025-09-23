# Score Last Slash Command

<input>
Parse score value (0-10) from $ARGUMENTS
Get current session ID from environment or project
</input>

<workflow>
1. Find the current session ID from Claude environment
2. Execute eval_score.py with score and session_id arguments
3. Script finds the session file and extracts conversation
4. Saves file snapshots for reproducibility
5. Stores everything in .evals/ directory
</workflow>

<output>
Show evaluation summary with location
</output>

<clarification>
- No score: "What score (0-10)?"
- Invalid: "Please provide 0-10"
- No session: "Could not find current session"
</clarification>

Get current session and run the backend:
```bash
# Try to get session ID from current Claude context
# First, try from the most recent session file in the project directory
SESSION_ID=$(ls -t ~/.claude/projects/*/[a-f0-9]*.jsonl 2>/dev/null | head -1 | xargs basename 2>/dev/null | sed 's/.jsonl//')

# If not found, try to get from current working directory name (often contains session)
if [ -z "$SESSION_ID" ]; then
    SESSION_ID=$(basename "$PWD" | grep -E '^[a-f0-9-]{36}$' || echo "")
fi

# If still not found, look for most recent in sessions directory
if [ -z "$SESSION_ID" ]; then
    SESSION_ID=$(find ~/.claude/sessions -name "*.jsonl" -type f -mtime -1 2>/dev/null | head -1 | xargs basename 2>/dev/null | sed 's/.jsonl//')
fi

if [ -z "$SESSION_ID" ]; then
    echo "❌ Could not find current session ID"
    echo "   Please make sure you're in an active Claude session"
    exit 1
fi

echo "📍 Using session: $SESSION_ID"
cd ~/Desktop/zPersonalProjects/ClaudeEval && python eval_score.py "$ARGUMENTS" --session_id "$SESSION_ID"
```