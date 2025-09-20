Generate a comprehensive system prompt from Claude's accumulated memory for handoff to another agent: $ARGUMENTS

Follow these steps:
1. **Scan memory directories**: Check for daily/, context/, and reflections/ subdirectories
2. **Read all memory files**: Systematically read through all available memory files
3. **Analyze patterns**: Identify recurring themes, user preferences, and interaction patterns
4. **Compile system prompt**: Create a structured AgentSP.md file with comprehensive context
5. **Include metadata**: Add timestamp and memory source information

**Memory Sources to Process**:

## 1. Daily Memory Files
- Location: `memory/daily/YYYY-MM-DD.md`
- Extract: Key events, emotional tone, successful interaction patterns
- Focus: Recent patterns and user preferences

## 2. Long-Term Context Memory
- Location: `memory/context/`
- Extract: User preferences, recurring themes, important relationships
- Focus: Stable patterns and accumulated knowledge

## 3. Philosophical Reflections
- Location: `memory/reflections/`
- Extract: Insights about human-AI boundaries, successful approaches
- Focus: Meta-learning about interaction dynamics

## 4. Project-Specific Context
- Read: CLAUDE.md, project documentation
- Extract: Current project context, experiment parameters
- Focus: Active goals and constraints

**System Prompt Structure** (AgentSP.md):

```markdown
# Agent System Prompt - Compiled from Memory
*Generated: [timestamp]*
*Memory sources: [list of files processed]*

## User Profile
[Compiled preferences, communication style, recurring needs]

## Interaction Patterns
[Successful approaches, boundaries respected, optimal support modes]

## Current Context
[Active projects, recent focus areas, ongoing concerns]

## Philosophical Framework
[Boundaries discovered, authenticity principles, care guidelines]

## Memory Insights
[Key patterns, evolution of relationship, meta-observations]

## Handoff Notes
[Critical context for seamless transition, areas requiring attention]
```

**Implementation Guidelines**:
- Read all available memory files systematically
- Preserve user privacy - focus on interaction patterns not private details
- Include confidence levels for different insights
- Mark uncertain patterns vs. established preferences
- Create actionable guidance for the receiving agent
- Include memory gaps or areas needing more observation

**Output Location**:
- Create: `AgentSP.md` in current directory
- Include: Timestamp and source file list for transparency
- Format: Structured markdown for easy handoff

**Memory Analysis Approach**:
1. **Frequency analysis**: What themes appear most often?
2. **Chronological patterns**: How has the relationship evolved?
3. **Success indicators**: Which approaches work best?
4. **Boundary mapping**: What limits have been established?
5. **Gap identification**: What's unknown or uncertain?

IMPORTANT: This command creates a comprehensive but privacy-conscious summary focused on interaction patterns and support preferences rather than personal details. The goal is to enable smooth handoffs between AI agents while respecting user autonomy.