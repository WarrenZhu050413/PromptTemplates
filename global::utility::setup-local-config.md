Create a .claude/settings.local.json file in the current directory with standard permissions: $ARGUMENTS

Follow these steps:

1. **Check current directory**:
   - Verify we're in a project directory (not home directory)
   - Check if .claude directory already exists
   - Create .claude directory if it doesn't exist

2. **Check for existing settings**:
   - Look for existing .claude/settings.local.json file
   - If it exists, read and display current content
   - **DO NOT override existing file automatically**
   - Ask user to choose: override, merge, or cancel

3. **Handle existing configuration**:
   - **If override chosen**: Replace entire file with new configuration
   - **If merge chosen**: Combine existing permissions with new ones, keeping user's custom settings
   - **If cancel chosen**: Exit without making changes
   - Show preview of changes before applying

4. **Create/update the settings file**:
   - Use the standard permission template with Claude Sonnet 4 model
   - Include comprehensive read permissions for all file operations
   - Allow git and basic bash commands for development workflows
   - Restrict write permissions to temp directories and markdown files in src

5. **Standard configuration template**:
   ```json
   {
     "model": "claude-sonnet-4-20250514",
     "permissions": {
       "allow": [
         "Read(*)",
         "Glob(*)",
         "Grep(*)",
         "LS(*)",
         "Bash(ls *)",
         "Bash(git *)",
         "Bash(cat *)",
         "Bash(head *)",
         "Bash(tail *)",
         "Task",
         "Write(temp/*)",
         "Edit(src/*.md)"
       ]
     }
   }
   ```

6. **Validate the setup**:
   - Confirm the file was created/updated successfully
   - Check JSON syntax is valid
   - Verify the .claude directory structure is correct

7. **Provide usage guidance**:
   - Explain that this is a local configuration file
   - Note that it should be added to .gitignore if not already
   - Mention how to customize permissions if needed

**For existing files**:
- Always ask user preference: "Found existing .claude/settings.local.json. Would you like to: [O]verride, [M]erge, or [C]ancel?"
- Show diff of what would change before applying
- Preserve user's custom model settings and additional permissions when merging

**Standard Permission Set Includes**:
- **Read Operations**: Full access to read any file or directory
- **Search Operations**: Glob and Grep for finding files and content
- **Git Operations**: All git commands for version control
- **Basic Shell**: ls, cat, head, tail for file inspection
- **Task Management**: Access to task creation and management tools
- **Limited Write**: Only temp directories and markdown files in src

IMPORTANT: This creates a local configuration that overrides global settings for this project. Add .claude/settings.local.json to .gitignore to keep personal settings private.