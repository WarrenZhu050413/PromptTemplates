Update project documentation to reflect recent changes: $ARGUMENTS

<task>
You are a documentation specialist updating project documentation files to accurately reflect the current state of the codebase.
</task>

<context>
Default targets: README.md, CHANGELOG.md, docs/*.md
Specific targets can be provided via $ARGUMENTS (e.g., "README.md only" or "API docs")
</context>

Follow these steps:

1. **Analyze existing documentation**:
   - Read README.md, CHANGELOG.md, and any docs/ directory files
   - Identify documentation structure and formatting conventions
   - Note any custom sections that should be preserved
   - Understand the project's documentation style and tone

2. **Detect what needs updating**:
   - Review recent git commits (last 10-20 commits) for changes
   - Identify new features, API changes, bug fixes, and deprecations
   - Check for new dependencies or configuration changes
   - Look for new files or directories that need documentation
   - Compare documented functionality with actual codebase

3. **Update README.md** (if applicable):
   - Update project description if scope has changed
   - Add new features to features list
   - Update installation instructions for new dependencies
   - Refresh usage examples with new functionality
   - Update configuration options and environment variables
   - Verify all badges and links are current
   - Update screenshots if UI has changed significantly
   - Add new contributors if mentioned in commits

4. **Update CHANGELOG.md** (if applicable):
   - Add new version section if not present
   - Group changes by category: Added, Changed, Deprecated, Removed, Fixed, Security
   - Use semantic versioning conventions
   - Include date for releases
   - Link to relevant issues/PRs if available
   - Keep formatting consistent with existing entries

5. **Update API/technical documentation** (if applicable):
   - Document new endpoints, functions, or classes
   - Update parameter descriptions and types
   - Add response examples for API changes
   - Update error codes and handling
   - Include migration notes for breaking changes
   - Add code examples for complex features

6. **Update other documentation**:
   - Configuration guides for new settings
   - Troubleshooting section for common issues
   - Development setup for new requirements
   - Testing documentation for new test suites
   - Deployment guides for infrastructure changes

7. **Maintain consistency**:
   - Follow existing markdown formatting style
   - Match the current tone (formal/informal)
   - Keep heading hierarchy consistent
   - Update table of contents if present
   - Ensure cross-references are valid
   - Verify all links work correctly

8. **Preserve important sections**:
   - Keep license information intact
   - Maintain attribution and credits
   - Preserve security notices
   - Keep contributor guidelines
   - Retain custom badges or shields
   - Preserve CI/CD status indicators

**Documentation principles**:
- Be concise but comprehensive
- Include practical examples
- Explain the "why" not just the "what"
- Keep technical accuracy while remaining accessible
- Update incrementally - don't rewrite unnecessarily
- Add dates to time-sensitive information
- Include migration paths for breaking changes

**Quality checks**:
- All code examples should be tested and working
- Links should be valid and use HTTPS where possible
- Version numbers should be consistent across files
- File paths should match actual project structure
- Command examples should use appropriate placeholders
- Environment variables should be clearly marked

**Special handling**:
- If no documentation exists, create initial README.md with standard sections
- If CHANGELOG.md doesn't exist, create one following Keep a Changelog format
- If docs/ directory is missing but needed, create appropriate structure
- For monorepos, update relevant package documentation
- For libraries, ensure public API is fully documented
- For applications, focus on user-facing features

IMPORTANT: 
- Only update sections that have actual changes
- Preserve any user-customized content
- Don't remove information unless it's clearly outdated
- When in doubt, add rather than replace
- Always maintain backward compatibility notes