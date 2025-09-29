# Codex: Advanced AI Debugger and Analyzer

Use Codex CLI with GPT-5 high reasoning for complex debugging and analysis: $ARGUMENTS

## Core Concept
Think of Codex as an intelligent debugger that can understand entire codebases, trace bugs across files, and provide deep architectural insights. It excels at complex reasoning tasks that require understanding multiple interconnected systems.

## Essential Workflow

### 1. Basic Invocation (Background Process)
```bash
# Setup output files
OUTPUT_FILE="/tmp/codex_output_$(date +%Y%m%d_%H%M%S).txt"
FINAL_FILE="/tmp/codex_final_$(date +%Y%m%d_%H%M%S).txt"

# Use Claude's Bash tool with run_in_background=true and 10+ minute timeout
# This runs codex in background natively without blocking
codex exec --model gpt-5 -c reasoning_effort=high \
  --skip-git-repo-check --sandbox read-only << 'EOF' > "$OUTPUT_FILE" 2>&1
$ARGUMENTS
EOF
# Set timeout=600000 (10 minutes in milliseconds) and run_in_background=true

echo "Codex running in background"
echo "Output: $OUTPUT_FILE"
echo "Final: $FINAL_FILE"

# Monitor output file for activity using BashOutput tool
# Check every 10 seconds for file size changes
# If no change for 30 seconds, assume completion
LAST_SIZE=0
NO_CHANGE_COUNT=0
while [ true ]; do
    if [ -f "$OUTPUT_FILE" ]; then
        CURRENT_SIZE=$(wc -c < "$OUTPUT_FILE" 2>/dev/null || echo 0)
        
        if [ "$CURRENT_SIZE" -eq "$LAST_SIZE" ]; then
            NO_CHANGE_COUNT=$((NO_CHANGE_COUNT + 1))
            if [ $NO_CHANGE_COUNT -ge 3 ]; then  # 30 seconds of no output
                echo "No output for 30 seconds, analysis likely complete"
                break
            fi
        else
            NO_CHANGE_COUNT=0
            echo "Processing... ($(du -h "$OUTPUT_FILE" | cut -f1))"
        fi
        
        LAST_SIZE=$CURRENT_SIZE
    fi
    sleep 10
done

# Extract final output
tail -n 1000 "$OUTPUT_FILE" > "$FINAL_FILE"
echo "Final output saved to: $FINAL_FILE"
tail -n 100 "$FINAL_FILE"
```

### 2. Structured Analysis Template
```bash
cat > /tmp/codex_request.txt << 'EOF'
PROBLEM: [specific issue]

FILES TO ANALYZE:
[list relevant files]

CURRENT BEHAVIOR:
[what's happening]

EXPECTED BEHAVIOR:
[what should happen]

ANALYZE:
1. Root cause identification
2. Impact assessment  
3. Solution with code changes
4. Test recommendations

OUTPUT FORMAT: Structured JSON or clear sections
EOF

# Execute with request file using Claude's background execution
# Use Bash tool with timeout=600000 and run_in_background=true
codex exec --model gpt-5 -c reasoning_effort=high \
  --skip-git-repo-check --sandbox read-only < /tmp/codex_request.txt > "$OUTPUT_FILE" 2>&1
```

## Key Usage Patterns

### Debug Complex Issues
```bash
codex exec --model gpt-5 -c reasoning_effort=high --skip-git-repo-check --sandbox read-only << 'EOF'
TRACE BUG: User action doesn't trigger expected UI update

Files: frontend/js/app.js, frontend/js/services/*.js
Symptoms: Click handler fires but DOM doesn't update

Find where the data flow breaks.
EOF
```

### Architecture Analysis  
```bash
codex exec --model gpt-5 -c reasoning_effort=high --skip-git-repo-check --sandbox read-only << 'EOF'
REVIEW ARCHITECTURE: Event-driven state management

Analyze for:
- Race conditions
- Memory leaks
- Performance bottlenecks
- Security vulnerabilities

Prioritize findings by impact.
EOF
```

### Generate Tests
```bash
codex exec --model gpt-5 -c reasoning_effort=high --skip-git-repo-check --sandbox read-only << 'EOF'
CREATE TEST SUITE:

Component: [name]
Framework: [Jest/Mocha/etc]
Coverage: unit + integration

Generate comprehensive tests.
EOF
```

## Critical Rules

1. **Use Claude's background execution** - Set `run_in_background=true` and `timeout=600000` (10 minutes)
2. **ALWAYS redirect to file** - Never use tee or inline output  
3. **Monitor with BashOutput tool** - Check the background shell's output periodically
4. **Watch file size changes** - Stop when no output for 30 seconds
5. **Extract final output** - Use tail after completion

## Output Monitoring Script

```bash
# Complete monitoring solution
monitor_codex() {
    local OUTPUT_FILE="$1"
    local FINAL_FILE="${OUTPUT_FILE%.txt}_final.txt"
    
    # Wait for initial output
    while [ ! -f "$OUTPUT_FILE" ]; do
        sleep 1
    done
    
    # Monitor for changes
    LAST_SIZE=0
    NO_CHANGE_COUNT=0
    MAX_NO_CHANGE=3  # 30 seconds
    
    while true; do
        CURRENT_SIZE=$(wc -c < "$OUTPUT_FILE" 2>/dev/null || echo 0)
        
        if [ "$CURRENT_SIZE" -eq "$LAST_SIZE" ]; then
            NO_CHANGE_COUNT=$((NO_CHANGE_COUNT + 1))
            if [ $NO_CHANGE_COUNT -ge $MAX_NO_CHANGE ]; then
                echo "Analysis appears complete (no output for 30s)"
                break
            fi
        else
            NO_CHANGE_COUNT=0
            echo "Active... ($(du -h "$OUTPUT_FILE" | cut -f1))"
        fi
        
        LAST_SIZE=$CURRENT_SIZE
        sleep 10
    done
    
    # Extract final results
    tail -n 1000 "$OUTPUT_FILE" > "$FINAL_FILE"
    echo "Final output saved to: $FINAL_FILE"
    tail -n 50 "$FINAL_FILE"
}
```

## Example Use Cases

1. **Debug why feature X stopped working after commit Y**
2. **Trace data flow from user input to database**
3. **Find all security vulnerabilities in auth system**
4. **Generate comprehensive test coverage for module**
5. **Analyze performance bottlenecks in rendering**
6. **Review architecture for technical debt**

## Tips for Best Results

- **Be specific** - "Debug login failure" vs "app broken"
- **Include context** - Recent changes, error messages, logs
- **Request structure** - Ask for JSON or sections in output
- **Limit scope** - Focus on specific modules when possible
- **Use stages** - Break complex analysis into phases

Remember: Codex is your intelligent debugging partner - treat it like a senior engineer who can see your entire codebase at once.
