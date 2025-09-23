Modify an existing slash command with intelligent name matching: $ARGUMENTS

Follow this process:

## Phase 1: Parse Request
1. **Extract components from $ARGUMENTS**:
   - Identify the command name to modify (may be partial or slightly incorrect)
   - Extract the requested changes/modifications
   - Note any specific instructions about the modification

## Phase 2: Find Target Command
2. **Search for the command**:
   ```bash
   # First check both global and project commands directories
   ls ~/.claude/commands/ 2>/dev/null | grep -i "{partial_name}"
   ls ./.claude/commands/ 2>/dev/null | grep -i "{partial_name}"
   ```
   
3. **Fuzzy matching logic**:
   - If exact match found → proceed directly
   - If single close match → confirm with user: "Did you mean `/command-name`?"
   - If multiple potential matches → show list: "Which command did you mean?"
     - List all candidates with their full names
     - Ask user to confirm selection
   - If no matches → try broader search:
     - Remove prefixes (global::, project::, local::)
     - Search by command name only
     - Check for similar category/name combinations
   
4. **Handle ambiguity**:
   ```
   Found multiple potential matches:
   1. /global::utility::feature-request
   2. /global::workflow::add-feature
   3. /project::feature-check
   
   Which command did you want to modify? (Enter number or full name)
   ```

## Phase 3: Read Current Command
5. **Load the command file**:
   - Use Read tool to get current command contents
   - Identify the structure and key sections
   - Note any special patterns or references

## Phase 4: Apply Modifications
6. **Determine modification type**:
   - **Content changes**: Modify specific sections or behaviors
   - **Structural changes**: Add/remove phases or sections
   - **Parameter changes**: Update how $ARGUMENTS is handled
   - **Reference updates**: Change documentation or tool references
   - **Workflow adjustments**: Modify step sequences or logic

7. **Apply changes intelligently**:
   - Preserve the overall command structure
   - Maintain consistent formatting and style
   - Keep critical sections intact (task, context)
   - Update documentation references if needed
   - Ensure $ARGUMENTS placeholder remains functional

## Phase 5: Validation and Confirmation
8. **Show proposed changes**:
   ```markdown
   I'll modify `/global::utility::command-name` with these changes:
   
   **Changes to apply:**
   - [Description of each change]
   
   **Key sections affected:**
   - [List of sections being modified]
   
   Proceed with these modifications? (yes/no/show-diff)
   ```

9. **If user requests diff view**:
   - Show before/after comparison of key changes
   - Highlight specific modifications
   - Allow further refinements

## Phase 5.5: Test & Compare with Headless Mode
10. **Create test environment**:
    ```bash
    # Create temporary files for both versions
    cp {command_path} /tmp/original_command.md
    # Apply modifications to create new version (but don't save yet)
    cat {modified_content} > /tmp/modified_command.md
    ```

11. **Select or request test prompt**:
    - For most commands, suggest a simple test case
    - Ask user: "What test prompt should we use to compare outputs?"
    - Default: Use the command's primary function with simple arguments
    ```bash
    # Example test prompt
    echo "/command-name test arguments" > /tmp/test_prompt.txt
    ```

12. **Run both versions through Claude headless mode**:
    ```bash
    # Test original command
    cat /tmp/original_command.md | claude -p "$(cat /tmp/test_prompt.txt)" > /tmp/original_output.txt 2>&1
    
    # Test modified command
    cat /tmp/modified_command.md | claude -p "$(cat /tmp/test_prompt.txt)" > /tmp/modified_output.txt 2>&1
    
    # Generate unified diff for the HTML display
    diff -u /tmp/original_command.md /tmp/modified_command.md > /tmp/command_diff.txt 2>&1 || true
    ```

13. **Generate HTML comparison**:
    Create `claude-output.html` with side-by-side comparison using this template:
    
    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Command Modification Test Results</title>
        <style>
            :root {
                --chinese-red: #8B0000;
                --chinese-gold: #FFD700;
                --jade-green: #00A86B;
                --ink-black: #2B2B2B;
                --paper-beige: #F5F5DC;
                --light-cream: #FAFAF0;
                --level-1: #000;
                --level-2: #333;
                --level-3: #666;
                --level-4: #999;
            }
            
            * {
                margin: 0;
                padding: 0;
                box-sizing: border-box;
            }
            
            body {
                font-family: -apple-system, BlinkMacSystemFont, "SF Pro", "Segoe UI", Roboto, Arial, sans-serif;
                background: linear-gradient(135deg, var(--paper-beige) 0%, var(--light-cream) 100%);
                color: var(--ink-black);
                margin: 0;
                padding: 0;
                width: 100vw;
                max-width: 100%;
                line-height: 1.2;
                font-size: 14px;
            }
            
            .container {
                width: 100%;
                padding: 2px;
                margin: 0;
            }
            
            h1 {
                font-size: 24px;
                font-weight: 900;
                margin: 4px 0;
                padding: 6px 4px;
                background: linear-gradient(135deg, var(--chinese-red), #CD5C5C);
                -webkit-background-clip: text;
                -webkit-text-fill-color: transparent;
                letter-spacing: -0.5px;
            }
            
            h2 {
                font-size: 18px;
                font-weight: 700;
                margin: 8px 0 4px 0;
                padding: 4px;
                border-left: 4px solid var(--chinese-red);
                background: rgba(139, 0, 0, 0.03);
                color: var(--level-1);
            }
            
            .important-always-visible {
                background: linear-gradient(135deg, rgba(255, 215, 0, 0.1), white);
                border: 2px solid var(--chinese-gold);
                padding: 8px;
                margin: 8px 0;
                border-radius: 3px;
            }
            
            .important-always-visible h2 {
                color: var(--chinese-red);
                margin-top: 0;
            }
            
            .collapsible {
                margin: 4px 0;
            }
            
            .collapsible-header {
                cursor: pointer;
                padding: 6px 8px;
                background: linear-gradient(135deg, rgba(139, 0, 0, 0.05), rgba(255, 215, 0, 0.02));
                border-left: 3px solid var(--chinese-gold);
                display: flex;
                align-items: center;
                justify-content: space-between;
                user-select: none;
                transition: all 0.2s ease;
            }
            
            .collapsible-header:hover {
                background: linear-gradient(135deg, rgba(139, 0, 0, 0.1), rgba(255, 215, 0, 0.05));
            }
            
            .collapsible-header .arrow {
                display: inline-block;
                transition: transform 0.3s ease;
                color: var(--chinese-red);
                font-size: 10px;
            }
            
            .collapsible.open .arrow {
                transform: rotate(90deg);
            }
            
            .collapsible-content {
                max-height: 0;
                overflow: hidden;
                transition: max-height 0.3s ease;
                padding: 0 8px;
                margin-left: 12px;
            }
            
            .collapsible.open .collapsible-content {
                max-height: 5000px;
                padding: 8px;
            }
            
            .comparison-grid {
                display: grid;
                grid-template-columns: 1fr 1fr;
                gap: 4px;
                margin: 4px 0;
            }
            
            .output-column {
                background: white;
                border: 1px solid rgba(139, 0, 0, 0.2);
                border-radius: 2px;
                padding: 6px;
                box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
            }
            
            .original {
                border-top: 3px solid var(--level-3);
            }
            
            .modified {
                border-top: 3px solid var(--jade-green);
            }
            
            .output-header {
                font-weight: 700;
                font-size: 14px;
                margin-bottom: 4px;
                padding-bottom: 2px;
                border-bottom: 1px solid var(--light-cream);
                color: var(--level-1);
            }
            
            .output-content {
                background: linear-gradient(135deg, rgba(245, 245, 220, 0.3), rgba(255, 255, 255, 0.5));
                border: 1px solid rgba(139, 0, 0, 0.1);
                padding: 4px 6px;
                border-radius: 2px;
                overflow-x: auto;
                white-space: pre-wrap;
                font-family: 'SF Mono', Consolas, 'Courier New', monospace;
                font-size: 12px;
                line-height: 1.3;
                max-height: 400px;
                overflow-y: auto;
            }
            
            .dense-list {
                list-style: none;
                padding: 0;
                margin-left: 8px;
            }
            
            .dense-list li {
                padding: 2px 0 2px 12px;
                border-left: 2px solid transparent;
                position: relative;
                font-size: 13px;
            }
            
            .dense-list li:before {
                content: "▸";
                position: absolute;
                left: 0;
                color: var(--chinese-red);
                font-size: 10px;
            }
            
            .code-diff {
                background: white;
                border: 1px solid rgba(139, 0, 0, 0.2);
                border-radius: 2px;
                padding: 6px;
                margin: 4px 0;
                box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
            }
            
            .code-diff h2 {
                font-size: 16px;
                margin: 4px 0;
            }
            
            .diff-content {
                background: #f8f8f8;
                border: 1px solid #ddd;
                border-radius: 2px;
                padding: 6px;
                overflow-x: auto;
                font-family: 'SF Mono', Consolas, 'Courier New', monospace;
                font-size: 11px;
                line-height: 1.2;
                max-height: 400px;
                overflow-y: auto;
            }
            
            .diff-line {
                margin: 0;
                padding: 1px 3px;
                white-space: pre;
            }
            
            .diff-added {
                background-color: rgba(0, 168, 107, 0.15);
                color: #00694d;
            }
            
            .diff-removed {
                background-color: rgba(139, 0, 0, 0.15);
                color: #8B0000;
            }
            
            .diff-header {
                color: #666;
                font-weight: bold;
                background-color: #f0f0f0;
            }
            
            pre, code {
                background: linear-gradient(135deg, rgba(245, 245, 220, 0.3), rgba(255, 255, 255, 0.5));
                border: 1px solid rgba(139, 0, 0, 0.1);
                padding: 2px 4px;
                margin: 1px 0;
                font-size: 12px;
                line-height: 1.1;
            }
            
            @media (max-width: 768px) {
                .comparison-grid {
                    grid-template-columns: 1fr;
                }
            }
        </style>
    </head>
    <body>
        <div class="container">
            <h1>Command Modification Test Results</h1>
            
            <div class="important-always-visible">
                <h2>🎯 Test Prompt</h2>
                <code>[INSERT TEST PROMPT]</code>
            </div>
            
            <div class="collapsible" data-collapsible="closed">
                <div class="collapsible-header">
                    <span>📋 Changes Applied</span>
                    <span class="arrow">▶</span>
                </div>
                <div class="collapsible-content">
                    <ul class="dense-list">
                        [INSERT CHANGE SUMMARY]
                    </ul>
                </div>
            </div>
            
            <div class="code-diff">
                <h2>🔍 Command Code Differences</h2>
                <div class="diff-content">
                    [INSERT COMMAND DIFF]
                </div>
            </div>
            
            <h2>⚡ Output Comparison</h2>
            <div class="comparison-grid">
                <div class="output-column original">
                    <div class="output-header">Original Command Output</div>
                    <div class="output-content">[INSERT ORIGINAL OUTPUT]</div>
                </div>
                <div class="output-column modified">
                    <div class="output-header">Modified Command Output</div>
                    <div class="output-content">[INSERT MODIFIED OUTPUT]</div>
                </div>
            </div>
        </div>
        
        <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Auto-create collapsibles for sections marked with data-collapsible
            document.querySelectorAll('[data-collapsible]').forEach(function(section) {
                const isOpen = section.getAttribute('data-collapsible') === 'open';
                section.classList.add('collapsible');
                if (isOpen) section.classList.add('open');
            });
            
            // Handle collapsible clicks
            document.querySelectorAll('.collapsible-header').forEach(function(header) {
                header.addEventListener('click', function() {
                    const collapsible = this.closest('.collapsible');
                    collapsible.classList.toggle('open');
                });
            });
        });
        </script>
    </body>
    </html>
    ```
    
    - Fill in placeholders with actual test data:
      - [INSERT TEST PROMPT]: The actual test command used
      - [INSERT CHANGE SUMMARY]: Format as list items: `<li>Change description</li>`
      - [INSERT COMMAND DIFF]: Process the diff file:
        * Read /tmp/command_diff.txt
        * Convert each line to HTML with proper escaping
        * Apply CSS classes: diff-added for lines starting with '+'
        * Apply CSS classes: diff-removed for lines starting with '-'
        * Apply CSS classes: diff-header for lines starting with '@@'
        * Escape < > & characters to &lt; &gt; &amp;
      - [INSERT ORIGINAL OUTPUT]: The test output from original command
      - [INSERT MODIFIED OUTPUT]: The test output from modified command
    - Ensure all HTML special characters are properly escaped

14. **Display and get approval**:
    ```bash
    # Open the comparison in browser
    open claude-output.html
    ```
    
    Ask user:
    ```markdown
    ## Command Test Results
    
    I've tested both versions of the command. Please review the comparison:
    - Original output (left)
    - Modified output (right)
    
    Do you prefer the modified version? 
    Options:
    - **approve** - Apply the modifications
    - **reject** - Keep the original
    - **refine** - Make additional changes
    - **retest** - Try with a different test prompt
    ```

15. **Handle user decision**:
    - **approve**: Proceed to Phase 6 (Write Updates)
    - **reject**: Cancel modifications, clean up temp files
    - **refine**: Return to Phase 4 with user feedback
    - **retest**: Return to step 11 with new test prompt

## Phase 6: Write Updates
16. **Update the command file** (only if approved in Phase 5.5):
    - Use Edit or MultiEdit tool for modifications
    - Preserve file permissions and structure
    - Maintain proper markdown formatting

17. **Verify the update**:
    - Re-read the file to confirm changes
    - Check that command still follows conventions
    - Ensure no syntax errors introduced

## Phase 7: Document and Test
18. **Create update record** (if significant changes):
    ```bash
    # Optional: Create backup before major changes
    cp {command_path} {command_path}.backup.$(date +%Y%m%d)
    ```

19. **Test recommendation**:
    - Note that command was already tested in Phase 5.5
    - Provide example usage if behavior changed
    - Note any breaking changes
    - Clean up temporary test files:
    ```bash
    rm -f /tmp/original_command.md /tmp/modified_command.md
    rm -f /tmp/test_prompt.txt /tmp/original_output.txt /tmp/modified_output.txt
    ```

## Phase 8: Sync Codex Prompts
20. **Publish the updated commands repository**:
    - From `~/.claude/commands`, stage and commit the modified command (include a descriptive message).
    - Run `git -C ~/.claude/commands push` to ensure the shared commands repo has the change.
21. **Refresh Codex's prompts clone**:
    - Run `git -C ~/.codex/prompts pull --ff-only` to bring the latest command into Codex's prompts directory.
    - Resolve any merge conflicts before continuing.
22. **Spot-check**:
    - Verify the updated command file now appears under `~/.codex/prompts` and matches the expected content.

## Examples of Modifications

### Example 1: Simple content update
User: "modify feature-request to include a priority field"
Action: Add priority selection to the feature request template

### Example 2: Fuzzy name matching
User: "modify the bug report command to be more concise"
Search: Find "bug", "report", "bug-report" in command names
Confirm: "Did you mean `/global::utility::bug-report`?"

### Example 3: Workflow change
User: "modify add-command to include a validation step"
Action: Insert validation phase into the workflow

### Example 4: Multiple matches
User: "modify the planning command"
Response: Show all commands with "planning" and ask for selection

## Error Handling

- **Command not found**: Suggest similar commands or offer to create new one
- **Ambiguous request**: Ask for clarification with specific options
- **Invalid modifications**: Explain why change cannot be applied
- **Permission issues**: Note if command is read-only or system command

## Best Practices

1. **Always confirm** ambiguous command names before modifying
2. **Preserve command structure** - don't break existing functionality
3. **Maintain naming conventions** - keep consistent with category
4. **Update documentation** - if command has associated docs
5. **Test after modification** - ensure command still works

IMPORTANT: 
- Never modify system commands (/init, /memory, /clear) without explicit confirmation
- Always show what will be changed before applying modifications
- Create backups for major structural changes
- Maintain backwards compatibility when possible