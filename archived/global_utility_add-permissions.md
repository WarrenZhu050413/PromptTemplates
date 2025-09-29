Add global bash permissions for Claude Code: $ARGUMENTS

Follow this process:

1. **Identify the bash commands to allow**:
   - Parse the provided command or pattern from $ARGUMENTS
   - Determine if wildcards or specific parameters are needed
   - Consider security implications of the permission

2. **Locate settings file**:
   - Check for ~/.claude/settings.json (global settings)
   - Create the file if it doesn't exist
   - Ensure proper JSON structure is maintained

3. **Add permissions**:
   - Read current settings to understand existing permissions
   - Add new bash command patterns to the allowed_tools array
   - Use format: "Bash(command:pattern)" for specific commands
   - Use format: "Bash(command:*)" for wildcard permissions
   - Validate JSON syntax is correct

4. **Update settings**:
   - Use Edit tool to modify the permissions section
   - Ensure the allowed_tools array includes the new bash permissions
   - Maintain existing permissions while adding new ones

5. **Verify the change**:
   - Test that the new permissions work as expected
   - Confirm Claude can now run the specified bash commands
   - Document the change for future reference

Example permission formats:
- "Bash(git commit:*)" - Allow all git commit commands
- "Bash(npm install:*)" - Allow all npm install commands  
- "Bash(docker:*)" - Allow all docker commands
- "Bash(pytest:*)" - Allow all pytest commands

IMPORTANT: Only add permissions for commands that are safe and necessary for development work.