# Score Last Slash Command (Advanced)

<input>
Parse score value (0-10) from $ARGUMENTS
Find current session using multiple strategies
</input>

<workflow>
1. Try multiple methods to find current session ID:
   - Check CLAUDE_SESSION_ID environment variable
   - Look in current project directory
   - Find most recent session file
   - Use codex to analyze session
2. Execute eval_score.py with discovered session ID
3. Save evaluation data with full context
</workflow>

<output>
Session discovery details and evaluation summary
</output>

<clarification>
- No score: "What score (0-10)?"
- No session: "Could not determine current session"
- Multiple sessions: "Found multiple sessions, using most recent"
</clarification>

Advanced session discovery and scoring:
```bash
SCORE="${ARGUMENTS:-}"

# Validate score
if [ -z "$SCORE" ]; then
    echo "❓ What score (0-10) would you like to give?"
    exit 1
fi

if ! [[ "$SCORE" =~ ^[0-9]$|^10$ ]]; then
    echo "❌ Invalid score. Please provide a number between 0 and 10"
    exit 1
fi

echo "🔍 Finding current session ID..."

# Strategy 1: Check environment variable
if [ -n "$CLAUDE_SESSION_ID" ]; then
    SESSION_ID="$CLAUDE_SESSION_ID"
    echo "  ✓ Found from environment: $SESSION_ID"

# Strategy 2: Check current project directory
elif [ -d ~/.claude/projects ]; then
    CURRENT_PROJECT=$(pwd | xargs basename)
    if [ -f ~/.claude/projects/"$CURRENT_PROJECT"/*.jsonl ]; then
        SESSION_ID=$(ls -t ~/.claude/projects/"$CURRENT_PROJECT"/*.jsonl 2>/dev/null | head -1 | xargs basename | sed 's/.jsonl//')
        echo "  ✓ Found in project directory: $SESSION_ID"
    fi
fi

# Strategy 3: Find most recent session in sessions directory  
if [ -z "$SESSION_ID" ]; then
    RECENT_SESSION=$(find ~/.claude/sessions -name "*.jsonl" -type f -mmin -60 2>/dev/null | head -1)
    if [ -n "$RECENT_SESSION" ]; then
        SESSION_ID=$(basename "$RECENT_SESSION" .jsonl)
        echo "  ✓ Found recent session: $SESSION_ID"
    fi
fi

# Strategy 4: Use codex to help find session
if [ -z "$SESSION_ID" ]; then
    echo "  🤖 Using codex to analyze sessions..."
    
    # Create a temporary script for codex to run
    cat > /tmp/find_session.sh << 'EOF'
#!/bin/bash
# Find the most recent Claude session that contains slash commands
find ~/.claude/sessions -name "*.jsonl" -type f -mtime -1 2>/dev/null | while read file; do
    if grep -q '^{"role":"user","content":"/' "$file" 2>/dev/null; then
        echo "$(stat -f %m "$file") $(basename "$file" .jsonl)"
    fi
done | sort -rn | head -1 | cut -d' ' -f2
EOF
    
    chmod +x /tmp/find_session.sh
    SESSION_ID=$(/tmp/find_session.sh)
    
    if [ -n "$SESSION_ID" ]; then
        echo "  ✓ Codex found session: $SESSION_ID"
    fi
    
    rm -f /tmp/find_session.sh
fi

# Final check
if [ -z "$SESSION_ID" ]; then
    echo "❌ Could not find current session ID"
    echo ""
    echo "💡 Suggestions:"
    echo "  1. Make sure you're in an active Claude session"
    echo "  2. Try running a slash command first"
    echo "  3. Set CLAUDE_SESSION_ID environment variable"
    echo ""
    echo "Available recent sessions:"
    find ~/.claude/sessions -name "*.jsonl" -type f -mtime -1 2>/dev/null | tail -5 | while read f; do
        echo "  - $(basename "$f" .jsonl)"
    done
    exit 1
fi

echo "📍 Using session: $SESSION_ID"
echo ""

# Run the evaluation
cd ~/Desktop/zPersonalProjects/ClaudeEval && python eval_score.py "$SCORE" --session_id "$SESSION_ID"
```