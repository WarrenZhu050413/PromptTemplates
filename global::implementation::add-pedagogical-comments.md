Create detailed pedagogical comments for a file in a separate comments file: $ARGUMENTS

This command creates comprehensive educational comments for code files to help with learning and understanding. Instead of modifying the original file, it creates a separate file with the same name but with "_comments" added before the file extension (e.g., "myfile.py" becomes "myfile_comments.py").

The comments explain:
- What each section of code does
- Why certain approaches were chosen
- How different parts work together
- Common patterns and best practices
- Potential gotchas or edge cases

The user may provide custom requests for what specific aspects they want explained in the comments, beyond just the file path. These requests should be incorporated into the commenting process.

Steps:
1. Read the specified file to understand its current structure and functionality
2. Check if the user has provided any specific focus areas or custom requests for the comments (e.g., "explain how X relates to Y", "focus on performance implications", etc.)
3. Analyze the code to identify key concepts, patterns, and learning opportunities, with special attention to any user-specified areas
4. Create a new file with "_comments" suffix containing the original code plus detailed comments that explain:
   - Function/method purposes and parameters
   - Complex logic or algorithms
   - Design patterns being used
   - Error handling approaches
   - Performance considerations
   - Security implications where relevant
   - Any specific aspects requested by the user
5. Ensure comments are:
   - Clear and beginner-friendly
   - Accurate and up-to-date with the code
   - Well-formatted and consistent
   - Not overly verbose but sufficiently detailed
   - Addressing the user's specific learning goals if provided
6. Add a header comment in the new file explaining that this is an educational version with pedagogical comments
7. Verify the commented file has correct syntax (though it's for educational purposes, not execution)

File naming convention:
- Original: "filename.ext" → Comments: "filename_comments.ext"
- Original: "BUILD.bazel" → Comments: "BUILD_comments.bazel"
- Original: "script.py" → Comments: "script_comments.py"

IMPORTANT: Only add comments that genuinely help with understanding. Avoid stating the obvious or cluttering the code with unnecessary explanations. Pay special attention to any custom requests from the user about what they want to learn. The original file remains unchanged - only the new comments file is created.
