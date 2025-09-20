Analyze a specific file to understand its purpose, usage, and code patterns: $ARGUMENTS

Follow these steps:
1. **Read the target file**: Use Read tool to examine the complete file content
2. **Identify main purpose**: Determine the primary function and responsibility of this file
3. **Find usage patterns**: Use Grep and Task tools to find how other components import, call, or reference this file
4. **Analyze dependencies**: Examine what this file imports/requires and how it uses external components
5. **Document code patterns**: Identify architectural patterns, design principles, and coding conventions used

**Analysis Structure**:

## 1. Main Purpose
- **Primary responsibility**: What this file is designed to do
- **Component type**: Model, view, controller, utility, config, etc.
- **Business domain**: Which area of the application this serves
- **Key functionality**: Main methods, classes, or exports provided

## 2. How This File Is Used by Other Components
- **Direct imports/references**: Show exact import statements and file paths
- **Method calls**: Display actual code that calls functions from this file
- **Configuration usage**: How config files or settings reference this file
- **API endpoints**: If applicable, show URL routing that uses this file
- **Frontend integration**: React components or services that consume this file's functionality

## 3. Code Patterns
- **Architecture patterns**: MVC, repository, factory, singleton, etc.
- **Error handling**: How exceptions and errors are managed
- **Data validation**: Input validation and sanitization approaches
- **Performance patterns**: Caching, optimization, lazy loading
- **Configuration patterns**: How settings and environment variables are used
- **Testing patterns**: How this file is tested or should be tested
- **Documentation patterns**: Code comments, docstrings, type hints

**Implementation Guidelines**:
- Use exact code snippets with file paths and line numbers
- Search broadly for usage patterns across the entire codebase
- Include both direct and indirect usage (e.g., inheritance, composition)
- Note any deprecated or legacy patterns that should be avoided
- Identify missing patterns that should be implemented

**Special Focus Areas**:
- **Django files**: Models, views, serializers, URL patterns, middleware
- **React files**: Components, hooks, state management, routing
- **Configuration files**: Settings, environment configs, build configs
- **Utility files**: Helper functions, constants, shared logic
- **Test files**: Test patterns, mocking strategies, coverage

IMPORTANT: Provide specific file paths and line numbers for all code examples. Focus on actual implementation rather than theoretical usage.