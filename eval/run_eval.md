# Re-run Saved Evaluations

<input>
Parse optional sample size N from $ARGUMENTS
</input>

<workflow>
1. Execute eval_run.py with optional sample size
2. Script finds all saved evals in .evals/
3. Samples N random evals (or all if not specified)
4. For each eval:
   - Restores file state from snapshots
   - Uses Claude SDK resume to continue session
   - Re-runs command with same arguments
   - Captures new output
5. Generates HTML comparison with side-by-side outputs
</workflow>

<output>
Progress updates and HTML file location
</output>

<clarification>
- Invalid number: "Invalid sample size"
- No evals: "No saved evaluations found"
- SDK missing: "Claude SDK not installed"
</clarification>

Run the Python backend:
```bash
cd ~/Desktop/zPersonalProjects/ClaudeEval && python eval_run.py "$ARGUMENTS"
```