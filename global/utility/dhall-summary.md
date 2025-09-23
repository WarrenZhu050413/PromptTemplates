---
task: Summarize today's dining hall food from Harvard Hillel and Harvard dining houses
category: global::utility
status: active
context: Provides a quick summary of today's dining options at Harvard dining facilities
---

# Dhall Food Summary

I'll fetch and summarize today's dining hall food options directly from the Harvard HUDS FoodPro system for the most up-to-date menu information.

## Step 1: Get today's date

```bash
date +"%A, %B %d, %Y"
```

## Step 2: Fetch dining information from HUDS FoodPro

I'll fetch today's menu directly from the HUDS FoodPro system.

```bash
# Get current date in format needed for URL (M/D/YYYY)
DATE=$(date +"%-m%%2f%-d%%2f%Y")
echo "Fetching menu for date: $DATE"
```

<function_calls>
<invoke name="WebFetch">
<parameter name="url">https://www.foodpro.huds.harvard.edu/foodpro/shtmenu.aspx?sName=HARVARD+UNIVERSITY+DINING+SERVICES&locationNum=16&locationName=Dining+Hall&naFlag=1&WeeksMenus=This+Week%27s+Menus&myaction=read&dtdate=${DATE}</parameter>
<parameter name="prompt">Extract and organize today's dining hall menu from this HUDS FoodPro page. For each meal period (breakfast/brunch, lunch, dinner), list:
1. Main entrees and proteins
2. Vegetarian/vegan options (marked with icons or labels)
3. Sides and accompaniments  
4. Desserts
5. Any special dietary markers (halal, kosher, gluten-free)

Format the output as a clean, organized summary grouped by meal period. Include any dining hours shown.</parameter>
</invoke>
</function_calls>

## Step 2b: Fetch Harvard Hillel menu (if available)

<function_calls>
<invoke name="WebSearch">
<parameter name="query">Harvard Hillel kosher dining menu today</parameter>
<parameter name="allowed_domains">["hillel.harvard.edu", "harvard.edu"]</parameter>
</invoke>
</function_calls>

## Step 3: Summarize the findings

Based on the information gathered, I'll provide:
- Complete menu from HUDS dining halls (breakfast/lunch/dinner)
- Dessert options for each meal
- Special dietary options (vegetarian, vegan, halal, kosher)
- Harvard Hillel kosher dining options (if available)
- Dining hall hours for today

The summary will be concise and focus on the actual food being served today, with special attention to desserts since these are often requested.