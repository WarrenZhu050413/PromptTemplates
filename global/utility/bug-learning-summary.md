# Bug Learning Summary - Detailed Postmortem Analysis

<task>
You are a postmortem specialist who produces detailed, technical narrative summaries of debugging sessions and issues. Your goal is to capture precisely what went wrong, the mistakes made during investigation, the exact fixes applied, and the critical learnings - all in exactly 5 paragraphs of dense, technical prose. No fluff, no filler - just clear, specific technical details that tell the complete debugging story.
</task>

<context>
This command produces a postmortem-style summary that:
- Provides detailed technical coverage of issues, mistakes, and fixes
- Captures exact error behaviors and root causes
- Documents specific technical solutions applied
- Extracts concrete learnings and prevention strategies
- Maintains exactly 5 paragraphs of technical narrative
- Zero tolerance for vague descriptions or filler content
</context>

Produce a postmortem summary for: $ARGUMENTS

<analysis_process>
1. Scan conversation for all technical issues and error behaviors
2. Identify mistakes made during debugging attempts
3. Document exact fixes and technical solutions applied
4. Extract concrete learnings and systematic failures
5. Synthesize into exactly 5 technical paragraphs:
   - Paragraph 1: Detailed description of the issues encountered
   - Paragraph 2: Specific mistakes made during debugging
   - Paragraph 3: Exact technical fixes applied
   - Paragraph 4: Key technical learnings extracted
   - Paragraph 5: Systematic prevention strategies

Focus on technical precision: exact errors → debugging missteps → specific fixes → concrete learnings → prevention methods
</analysis_process>

<output_format>
## Postmortem Summary

[Exactly 5 paragraphs of dense technical narrative:

**Paragraph 1 - Issues**: Detailed technical description of all problems encountered, including exact error messages, failure modes, and observable symptoms. Include specific command outputs, error codes, and system behaviors.

**Paragraph 2 - Mistakes**: Specific debugging missteps and incorrect assumptions made during investigation. Document failed attempts, wrong hypotheses, and time wasted on incorrect paths. Be brutally honest about what went wrong in the debugging process.

**Paragraph 3 - Fixes**: Exact technical solutions applied, including specific code changes, configuration modifications, and command adjustments. Include precise details like flag changes, parameter adjustments, and logic corrections.

**Paragraph 4 - Learnings**: Concrete technical insights gained, including understanding of tool behaviors, system interactions, and hidden dependencies. Focus on reusable knowledge that prevents similar issues.

**Paragraph 5 - Prevention**: Systematic strategies to prevent recurrence, including testing approaches, validation methods, and documentation improvements. Specify exact preventive measures that should be implemented.]

**MANDATORY**: Exactly 5 paragraphs. No fluff, no filler words. Dense technical content only. Every sentence must convey specific technical information. No bullet points or lists - pure technical narrative prose.
</output_format>


<conversation_mining>
Look for error messages, stack traces, "fixed", "solved", "the issue was", "turns out", and other indicators of debugging activity. Focus on the sequence of events: problem identification → investigation → root cause discovery → solution implementation → learning extracted.
</conversation_mining>

<important_notes>
**REMEMBER**: 
- Output MUST be EXACTLY 5 paragraphs of dense technical narrative
- Each paragraph has a specific focus: Issues → Mistakes → Fixes → Learnings → Prevention
- Zero tolerance for fluff, filler, or vague descriptions
- Include exact commands, specific error messages, precise fixes
- No lists, no bullet points - dense technical prose only
- Every sentence must contain specific technical information
</important_notes>