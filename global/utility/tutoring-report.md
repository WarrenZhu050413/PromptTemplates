# Tutoring Report Generator (Chinese)

<input>
## Parse Arguments
Process $ARGUMENTS to extract:
- Student name (e.g., "Student A", "Student B")
- Week number or date range
- Class information (can be in English or Chinese)
- Any specific details to include

## Example Inputs
- `/global::utility::tutoring-report "Student A" week3`
- `/global::utility::tutoring-report "Student B" "Monday 1hr EPQ discussion, Wed 45min thesis review"`
- `/global::utility::tutoring-report "Student A" week3 "两堂课，周一1小时，周三45分钟"`

## Read Context
Look for and read:
- Previous reports for this student (week1, week2, etc.)
- Previous reports for other students to maintain style consistency
- Any notes or class documents mentioned

## Build Context
Gather information for:
- Student's previous report style and phrases
- Standard report structure
- Consistent Chinese phrasing patterns
- Time tracking details
</input>

<workflow>
## Phase 1: Gather Report Information
- Search for previous reports (pattern: `*week*_*.txt`, `*report*.txt`)
- Read the most recent reports to understand style
- Parse the input for class details
- If input is in English, prepare for translation

## Phase 2: Structure Report Content
Required elements:
1. Greeting line ([Recipient]您好：)
2. Introduction (我跟您讲一下这周与[Student]的情况:)
3. Class summary (dates and durations)
4. Total hours calculation
5. Detailed class descriptions with Google Drive links
6. Current progress section (关于现在[Student]的进度：)
7. Future goals and timeline

## Phase 3: Style Matching and Translation
- If input is English, translate to Chinese
- Match phrasing from previous reports:
  - "我们这周总共上了X堂课"
  - "总共课时为：X小时X分钟"
  - "第一堂课..." / "第二堂课..."
- Maintain formal yet friendly tone
- Use consistent time expressions

## Phase 4: Generate Final Report
- Format with proper Chinese punctuation (：、。)
- Include Google Drive links where applicable
- Add progress assessment
- Include forward-looking goals

## Tools to Use:
- Glob: Find previous reports
- Read: Get previous report styles
- Write: Create new report file
- Edit: Update existing reports if needed
</workflow>

<output>
## Format
Generate a complete Chinese report following this structure:

```
[Recipient]您好：

我跟您讲一下这周与[Student]的情况:

我们这周总共上了X堂课：[dates]。

[Day]上了X小时/分钟
[Day]上了X小时/分钟

总共课时为：X小时X分钟。

第一堂课（[date]）[detailed description]。[Google Drive link if available]

第二堂课（[date]）[detailed description]。

关于现在[Student]的进度：

[Progress description]

[Future goals and timeline]
```

## Style Guidelines
- Use formal Chinese with consistent punctuation
- Keep sentences clear and professional
- Include specific details about class content
- Maintain the same phrasing patterns as previous reports

## Example Output:
"I've created the week 3 report for Student A at week3_studentA_report.txt. The report includes:
- 2 classes totaling 1 hour 45 minutes
- Detailed descriptions of thesis discussion and outline review
- Links to Google Drive documents
- Progress update and goals for next week"
</output>

<clarification>
## When to Ask Questions
Clarify when:
- Class dates or durations are unclear
- Multiple students have similar names
- Google Drive links are missing but expected
- Report week/number is ambiguous

## What to Clarify
- "Which week is this report for?"
- "What was the duration of the second class?"
- "Do you have the Google Drive link for Monday's class materials?"
- "Should I include the discussion about EPQ in the report?"

## How to Ask
Present options clearly:
- "I found reports for Student A and Student B. Which student is this for?"
- "You mentioned two classes but only provided one duration. How long was the Wednesday class?"
- "Should I create this as week3_studentA_report.txt or use a different filename?"
</clarification>

## Usage Notes
1. **Input Language**: Can accept English or Chinese input
2. **Translation**: Automatically translates English to appropriate Chinese
3. **Style Consistency**: Analyzes previous reports to maintain consistent phrasing
4. **File Naming**: Creates files as `week[N]_[student]_report.txt`
5. **Google Drive Links**: Include when provided, format inline with descriptions

## Common Phrases Reference
- 我跟您讲一下这周与...的情况 (Let me tell you about this week with...)
- 我们这周总共上了X堂课 (We had X classes this week)
- 总共课时为 (Total class time was)
- 第一堂课/第二堂课 (First class/Second class)
- 关于现在...的进度 (Regarding ...'s current progress)
- 我们的目标是 (Our goal is)
- 计划在...完成 (Plan to complete by...)
- 她的进度很不错 (Her progress is quite good)
- 能够按时完成布置的任务 (Able to complete assigned tasks on time)