<%*
// Work out the week from the file name (e.g. 2026-W47); fall back to the current week.
let base = moment(tp.file.title, "gggg-[W]ww", true);
if (!base.isValid()) base = moment();
const start = base.clone().startOf("week");
const end = start.clone().endOf("week");
const wk = start.format("gggg-[W]ww");
const prev = start.clone().subtract(1, "week").format("gggg-[W]ww");
const next = start.clone().add(1, "week").format("gggg-[W]ww");
const s = start.format("YYYY-MM-DD");
const e = end.format("YYYY-MM-DD");
const after = start.clone().add(7, "days").format("YYYY-MM-DD");
-%>
---
type: weekly
week: <% wk %>
start: <% s %>
end: <% e %>
rating: 
tags: [weekly]
---
# 🗓️ <% start.format("MMM D") %> – <% end.format("MMM D") %>

[[<% prev %>|◀ Prev]] · [[<% next %>|Next ▶]]

## 🏆 Wins
- 

> [!example]- ✅ Done this week
> ```tasks
> done in <% s %> <% e %>
> short mode
> hide backlink
> hide edit button
> ```

> [!warning]- 🔁 Still open
> ```tasks
> not done
> due before <% after %>
> sort by due
> short mode
> hide edit button
> ```

> [!info]- 📆 Days
> ```dataview
> LIST "😊 " + default(mood, "–") + " · ⚡ " + default(energy, "–")
> FROM #daily
> WHERE date >= date(<% s %>) AND date <= date(<% e %>)
> SORT date ASC
> ```

> [!note]- 🚀 Projects
> ```dataview
> LIST status + choice(due, " · due " + dateformat(due, "MMM d"), "")
> FROM "Projects"
> WHERE status = "active" OR status = "planning"
> SORT due ASC
> ```

## 🔍 Reflection
- **Worked:** 
- **Didn't:** 
- **Learned:** 

## 🎯 Next week's Top 3
1. 
2. 
3. 
