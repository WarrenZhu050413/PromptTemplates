Perform rapid codebase onboarding with structured exploration: $ARGUMENTS

Follow these steps:
1. **Initial Architecture Analysis**: Use Task tool to analyze main entry points, package structure, and core abstractions
2. **Create onboarding folder**: Set up ./onboarding directory with structured documentation
3. **Generate architecture overview**: Document key abstractions, patterns, and architectural decisions
4. **Interactive exploration**: Ask user which components to deep-dive into
5. **Spawn specialized agents**: Use Task tool to create detailed analysis for each selected component
6. **Generate documentation**: Write findings to organized files in ./onboarding/

**Phase 1: Initial Analysis**
```
Use Task tool with description: "Analyze codebase architecture"
Prompt: 
- Find and read main entry points (main.py, index.js, app.py, etc.)
- Identify package/module structure
- Find configuration files (package.json, pyproject.toml, etc.) 
- Read README and documentation files
- Identify framework usage (Django, React, FastAPI, etc.)
- Find test structure and patterns
- Return a structured summary of:
  * Core abstractions and their purposes
  * Key architectural patterns (MVC, microservices, etc.)
  * Technology stack and frameworks
  * Project structure and organization
  * Testing and deployment approach
```

**Phase 2: Setup Onboarding Structure**
```bash
mkdir -p ./onboarding
mkdir -p ./onboarding/architecture
mkdir -p ./onboarding/components
mkdir -p ./onboarding/patterns
mkdir -p ./onboarding/workflows
```

**Phase 3: Generate Initial Documentation**
Write to `./onboarding/README.md`:
```markdown
# Codebase Onboarding Guide

## Overview
[Project description and purpose]

## Key Abstractions
1. **[Abstraction Name]**: [Purpose and responsibility]
2. **[Abstraction Name]**: [Purpose and responsibility]
...

## Architectural Decisions
1. **[Decision]**: [Rationale and implications]
2. **[Decision]**: [Rationale and implications]
...

## Technology Stack
- **Language**: [Primary language and version]
- **Framework**: [Main framework]
- **Database**: [Database system]
- **Testing**: [Test framework]
...

## Quick Start Commands
\`\`\`bash
# Development setup
[setup commands]

# Run tests
[test commands]

# Start application
[run commands]
\`\`\`

## Deep Dive Topics
Select components for detailed exploration:
- [ ] [Component 1]: [Brief description]
- [ ] [Component 2]: [Brief description]
- [ ] [Pattern 1]: [Brief description]
- [ ] [Workflow 1]: [Brief description]
...
```

**Phase 4: Interactive Component Selection**
Present the architecture overview and ask:
"I've analyzed the codebase and identified the key abstractions and architecture. Which of these areas would you like to explore in detail?

Available deep-dives:
1. **Core Components**:
   - [List main components with brief descriptions]
   
2. **Design Patterns**:
   - [List architectural patterns used]
   
3. **Workflows**:
   - [List key workflows or processes]
   
4. **Technical Areas**:
   - Database schema and models
   - API structure and endpoints
   - Authentication and authorization
   - Testing strategies
   - Build and deployment
   
5. **Custom Questions**:
   - Any specific questions about the codebase?

Please select the numbers/areas you'd like to explore, or ask specific questions."

**Phase 5: Spawn Specialized Analysis Agents**
For each selected topic, use Task tool to spawn dedicated analysis:

```
Use Task tool with description: "Deep dive [component name]"
Prompt:
- Perform detailed analysis of [component/pattern/workflow]
- Read all relevant files using Read tool
- Trace usage patterns using Grep tool
- Identify dependencies and interactions
- Document findings in structured format
- Write results to ./onboarding/components/[component_name].md
Include:
  * Purpose and responsibility
  * Key files and locations
  * Main functions/classes
  * Usage examples with code snippets
  * Integration points
  * Testing approach
  * Common patterns
  * Potential improvements
```

**Phase 6: Generate Component Documentation**
Each spawned agent writes to appropriate files:
- `./onboarding/components/[name].md` - Component deep dives
- `./onboarding/patterns/[pattern].md` - Pattern explanations
- `./onboarding/workflows/[workflow].md` - Process documentation
- `./onboarding/architecture/[topic].md` - Architecture details

**Output Structure for Component Files**:
```markdown
# [Component Name]

## Overview
[Detailed purpose and responsibility]

## Key Files
- `path/to/file.py`: [Purpose]
- `path/to/another.js`: [Purpose]

## Core Abstractions
### [Class/Function Name]
Location: `file:line`
Purpose: [What it does]
Usage: [How it's used]
\`\`\`python
# Example code
\`\`\`

## Dependencies
- Imports: [What this component depends on]
- Used by: [What depends on this component]

## Usage Patterns
[Common usage patterns with examples]

## Testing
[How this component is tested]

## Integration Points
[How this connects to other components]

## Potential Improvements
[Suggestions for enhancement]
```

**Phase 7: Generate Summary and Next Steps**
Create `./onboarding/next-steps.md`:
```markdown
# Next Steps for Development

Based on the codebase analysis, here are recommended next steps:

## Immediate Actions
1. [First thing to try/modify]
2. [Simple task to understand workflow]

## Learning Path
1. Start with: [Component/file]
2. Then explore: [Related component]
3. Practice by: [Suggested modification]

## Key Commands
\`\`\`bash
# Most important commands for development
[commands with explanations]
\`\`\`

## Resources
- [Link to main documentation]
- [Link to style guide]
- [Link to contribution guide]
```

**Implementation Guidelines**:
- Use Task tool for complex multi-file analysis
- Use Grep for finding usage patterns
- Use Read for examining specific files
- Always provide file paths and line numbers
- Focus on actual code, not theoretical design
- Create clear, actionable documentation
- Make the onboarding progressive and interactive

**Special Considerations**:
- **Large codebases**: Focus on core abstractions first
- **Microservices**: Map service boundaries and communication
- **Monoliths**: Identify module boundaries and layers
- **Frontend apps**: Component hierarchy and state management
- **Backend services**: API structure and data flow
- **Libraries**: Public API and usage examples

IMPORTANT: Generate documentation that enables rapid productive contribution. Focus on "what you need to know to make changes" rather than exhaustive documentation. Each spawned agent should work independently to avoid context pollution.