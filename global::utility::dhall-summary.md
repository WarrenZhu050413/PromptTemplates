---
task: Summarize today's dining hall food from Harvard Hillel and Harvard dining houses
category: global::utility
status: active
context: Provides a quick summary of today's dining options at Harvard dining facilities
---

# Dhall Food Summary

I'll fetch and summarize today's dining hall food options from Harvard dining services using the Codex MCP tool for comprehensive and accurate menu information.

## Step 1: Get today's date

```bash
date +"%A, %B %d, %Y"
```

## Step 2: Fetch dining information using Codex

I'll use the Codex MCP tool to fetch and analyze today's menu from Harvard dining services.

<function_calls>
<invoke name="Task">
<parameter name="subagent_type">general-purpose</parameter>
<parameter name="description">Fetch Harvard dining menu using Codex</parameter>
<parameter name="prompt">Use the Codex MCP tool to fetch and analyze today's Harvard dining hall menu. Search for current menu information from Harvard dining services (HUDS) and Harvard Hillel. Provide specific menu items for breakfast, lunch, and dinner, including vegetarian, vegan, and halal options. Include dining hall hours if available.</parameter>
</invoke>
</function_calls>

## Step 3: Summarize the findings

Based on the information gathered, I'll provide:
- Today's menu highlights from Harvard Hillel
- Today's menu highlights from Harvard dining houses
- Special dietary options available
- Dining hall hours for today

The summary will be concise and focus on the actual food being served today.