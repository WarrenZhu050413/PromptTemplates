# HTML Style Configuration Editor

<input>
## Parse Arguments
Process $ARGUMENTS to extract:
- What aspect to change (colors, layout, fonts, mermaid, file-handling, etc.)
- Specific change requested (e.g., "make buttons blue", "change directory to outputs/")
- Which config file (html.md, HTML.md snippet, PLANHTML.md snippet)

## Example Inputs
- `/global::utility::change-html-style change primary color to navy`
- `/global::utility::change-html-style update directory to outputs_html`
- `/global::utility::change-html-style add new collapsible style`
- `/global::utility::change-html-style enable dark mode theme`

## Read Context
Read all HTML style configuration files:
- `~/.claude/output-styles/html.md` - Main output style
- `~/.claude/snippets/snippets/HTML.md` - HTML snippet (with verification hash)
- `~/.claude/snippets/snippets/PLANHTML.md` - Plan HTML snippet (with verification hash)

## Build Context
- Current style configurations
- Requested changes
- Which files need updates
- Whether verification hashes need updating
</input>

<workflow>
## Phase 1: Analysis
- Read all three HTML configuration files
- Identify what needs to change based on user request
- Determine if change affects one or all config files

## Phase 2: Make Changes
- Edit the relevant configuration file(s)
- Update CSS, colors, layouts, or file handling as requested
- Keep changes consistent across files if needed
- Update verification hashes for snippet files:
  - HTML.md: Generate new hash for VERIFICATION_HASH
  - PLANHTML.md: Generate new hash for VERIFICATION_HASH

## Phase 3: Validation
- Verify edits were applied correctly
- Confirm syntax is valid
- Show summary of changes made

## Tools to Use:
- Read: Load configuration files
- Edit: Apply changes
- Generate random verification hashes when updating snippets
</workflow>

<output>
## Format
Clear summary of changes:
- What was changed
- Which files were updated
- New verification hashes if applicable

## Style
Direct and helpful, showing before/after snippets

## Example Output:
Updated HTML style configurations:

**Changed:** Primary color from `#8B0000` to `#000080` (Navy)

**Files modified:**
- `~/.claude/output-styles/html.md`
- `~/.claude/snippets/snippets/HTML.md` (hash: `a1b2c3d4e5f6g7h8`)

The new color will apply to all future HTML outputs.
</output>

<clarification>
## When to Ask Questions
Clarify when:
- Change affects visual design significantly
- Multiple interpretation exists (e.g., "primary color" could mean red or gold)
- Change impacts multiple config files
- Destructive changes requested (removing entire sections)

## What to Clarify
- "Did you want to change the Chinese Red (#8B0000) or Chinese Gold (#FFD700)?"
- "Should I update all three config files or just the main output style?"
- "This will change the default layout. Proceed?"

## How to Ask
Be specific about impact:
- List what will change
- Show affected files
- Suggest safest option
</clarification>

---

## Quick Reference

**HTML Configuration Files:**
1. `~/.claude/output-styles/html.md` - Main output style (no hash)
2. `~/.claude/snippets/snippets/HTML.md` - HTML snippet (has VERIFICATION_HASH)
3. `~/.claude/snippets/snippets/PLANHTML.md` - Plan HTML snippet (has VERIFICATION_HASH)

**Common Modifications:**
- **Colors**: Chinese Red, Chinese Gold, Jade Green, Ink Black, Paper Beige
- **Layout**: Two-column grid, collapsibles, spacing, margins
- **Typography**: Font sizes, weights, line heights
- **File Handling**: Directory paths, naming conventions
- **Mermaid**: Diagram theming and configuration
- **Components**: Buttons, cards, tables, code blocks

**Verification Hashes:**
When editing snippet files (HTML.md, PLANHTML.md), always update the VERIFICATION_HASH to a new random 16-character hex string to force Claude Code to reload the snippet.
