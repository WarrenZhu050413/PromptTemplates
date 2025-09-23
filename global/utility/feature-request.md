Submit a feature request to the Claude Code repository with duplicate checking: $ARGUMENTS

Follow these steps:

## Phase 1: Duplicate Detection
1. Use `gh search issues --repo anthropics/claude-code "{search terms}" --limit 10` to search for similar feature requests using key terms from the user's description
2. If potential duplicates found:
   - Display them to the user with issue numbers, titles, and URLs
   - For each duplicate issue:
     - Use `gh issue view --repo anthropics/claude-code [issue-number] --comments` to list all comments
     - Check if the user (wz) has already commented or engaged with the issue
   - Show the user: "I found these potentially similar requests. Here are the details and comments:"
   - Display for each duplicate:
     - Issue title and number
     - Comment summary (number of comments, key points discussed)
     - Whether you have already engaged with this issue
   - Ask user: "Do any of these match your idea?"
   - If user confirms a duplicate exists:
     - If you haven't engaged yet: Ask "Would you like me to add a +1 reaction or comment to show support?"
     - If you have engaged: Note "You've already engaged with this issue"
     - If yes to new engagement, use `gh issue comment --repo anthropics/claude-code [issue-number] --body "+1 - I would also like this feature"`
     - End the command with confirmation
   - If no duplicates match, continue to Phase 2

## Phase 2: Interactive Feature Request Development
3. Start with the user's initial description: $ARGUMENTS
4. Keep it concise by default - this is about sharing ideas, not writing specs:
   - Ask ONE clarifying question if the request is unclear: "Could you briefly clarify [specific unclear aspect]?"
   - Otherwise, proceed directly to drafting
5. Build a concise feature request with:
   - Brief problem statement (1-2 sentences)
   - Simple proposed solution (what you'd like to see)
   - One concrete example of usage
   - Skip implementation details unless user wants to elaborate

## Phase 3: Final Review and Submission
6. Present a concise feature request template to user:
```markdown
# [FEATURE REQUEST] <!-- Short, clear title -->

## What I'd like
<!-- 1-2 sentences on what you want -->

## Why
<!-- Brief problem or use case -->

## Example
<!-- One quick example of how you'd use it -->
```

7. Ask user: "Does this capture your idea? Should I submit it, or would you like to expand on any part?"
8. If user wants to expand:
   - Add requested details only
   - Keep other sections concise
9. If approved:
   - Use `gh issue create --repo anthropics/claude-code --title "[FEATURE REQUEST] {title}" --body "{template}"`
   - Confirm successful submission with issue URL
10. If changes needed:
   - Make minimal edits and reconfirm

**Search Strategy for Duplicates**:
- Extract 2-3 key terms from user's description
- Search for issues: `gh search issues --repo anthropics/claude-code "{terms}" --limit 10`
- Try different term combinations if initial search has few results
- Note: --state and --match flags are not used together in the correct syntax
- Focus on feature requests and enhancements (exclude bugs)

**Interactive Guidelines**:
- Default to concise - this is about sharing ideas, not architecture specs
- Only ask clarifying questions if truly needed for understanding
- Let the user drive any expansion of detail
- Focus on capturing the core idea quickly

**Template Requirements**:
- Title should be clear and searchable (e.g., "Add support for custom prompt templates")
- Keep sections brief - a paragraph at most
- Focus on the "what" and "why", not the "how" 
- Professional but informal tone is fine

IMPORTANT: 
- Always check for duplicates first - this saves maintainer time
- Keep it lightweight by default - the user can expand if they want to provide more detail
- Think of this as "sharing what would be nice to have" rather than "comprehensive feature specification"
- Only submit when user explicitly approves the final version
- Use GitHub CLI (gh) for all GitHub operations