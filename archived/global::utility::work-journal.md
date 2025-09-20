Create or update a work journal entry for today: $ARGUMENTS

Follow these steps:
1. Get today's date in YYYY-MM-DD format
2. Create the directory structure:
   - Directory: `yyyy-mm-dd/` (e.g., `2025-01-13/`)
   - Journal file: `yyyy-mm-dd/yyyy-mm-dd.md` (e.g., `2025-01-13/2025-01-13.md`)
3. Check if the directory and journal file already exist
4. Parse the input format and determine the action:
   - If input contains semicolon: "<one line summary>; <numbered tasks>" (complete daily summary)
   - If no semicolon: just a task/achievement to add to existing entry
5. Handle the appropriate action:
   - **New file or complete summary**: Create directory (if needed) and full journal structure with summary and tasks
   - **Intermediate logging**: Add the new task to existing "Other notables" section with next number
6. Verify the file was updated correctly

**Input formats**:
- Complete daily summary: "Summary of the day; 1. First task, 2. Second task, 3. Third task"
- Intermediate logging: "Completed database migration testing"

**Journal structure**:
- Header with date (# YYYY-MM-DD)
- One Line Summary section (updated if provided)
- Other notables section with numbered list (tasks appended)

**Behavior**:
- If directory doesn't exist: Create directory structure
- If file doesn't exist: Create new journal with provided content
- If file exists and input has semicolon: Update summary and replace tasks
- If file exists and no semicolon: Add task to existing list with next sequential number

**Directory structure**:
- Each day gets its own directory named `yyyy-mm-dd`
- Inside the directory: `yyyy-mm-dd.md` (journal file) and any other resources produced that day

IMPORTANT: For intermediate logging, the command automatically numbers tasks sequentially. For complete summaries, tasks should be pre-numbered in the input.