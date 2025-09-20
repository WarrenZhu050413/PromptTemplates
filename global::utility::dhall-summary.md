---
task: Summarize today's dining hall food from Harvard Hillel and Harvard dining houses
category: global::utility
status: active
context: Provides a quick summary of today's dining options at Harvard dining facilities
---

# Dhall Food Summary

I'll fetch and summarize today's dining hall food options from Harvard Hillel and Harvard dining houses.

## Step 1: Get today's date

```bash
date +"%A, %B %d, %Y"
```

## Step 2: Fetch dining information from both sources

I'll fetch the current menus from:
1. Harvard Hillel dining hall
2. Harvard undergraduate dining houses

<function_calls>
<invoke name="WebFetch">
<parameter name="url">https://www.hillel.harvard.edu/week-harvard-hillel-dining</parameter>
<parameter name="prompt">Extract today's menu items for breakfast, lunch, and dinner. List the specific food items being served today. Focus on the actual menu items, not general information.</parameter>
</invoke>
</function_calls>

<function_calls>
<invoke name="WebFetch">
<parameter name="url">https://www.dining.harvard.edu/undergraduate-dining/dining-houses</parameter>
<parameter name="prompt">Find and extract today's specific menu items for Harvard dining halls. Look for links to daily menus or weekly menus and extract what's being served today for breakfast, lunch, and dinner.</parameter>
</invoke>
</function_calls>

## Step 3: Summarize the findings

Based on the information gathered, I'll provide:
- Today's menu highlights from Harvard Hillel
- Today's menu highlights from Harvard dining houses
- Special dietary options available
- Dining hall hours for today

The summary will be concise and focus on the actual food being served today.