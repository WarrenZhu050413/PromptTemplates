# Show Eval Statistics

<input>
No arguments needed
</input>

<workflow>
1. Scan .evals/ directory for all saved evaluations
2. Group by command type
3. Calculate average scores and counts
4. Show distribution of scores
</workflow>

<output>
📊 Eval Statistics
━━━━━━━━━━━━━━━
Total Evals: [N]
Commands: [M] unique

By Command:
• [command]: [count] evals, avg score: [X.X]/10
• [command]: [count] evals, avg score: [X.X]/10

Score Distribution:
10: ████████ (N)
9:  ██████ (N)
8:  ████ (N)
...
</output>

<clarification>
- No evals: "No evaluations found. Use /score to start tracking."
</clarification>