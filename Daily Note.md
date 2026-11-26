---
type: daily
date: <% tp.date.now("YYYY-MM-DD", 0, tp.file.title, "YYYY-MM-DD") %>
week: "[[<% tp.date.now("gggg-[W]ww", 0, tp.file.title, "YYYY-MM-DD") %>]]"
mood: 
energy: 
tags: [daily]
---
# 📅 <% tp.date.now("ddd, MMM D", 0, tp.file.title, "YYYY-MM-DD") %>

[[<% tp.date.now("YYYY-MM-DD", -1, tp.file.title, "YYYY-MM-DD") %>|◀ Prev]] · [[<% tp.date.now("gggg-[W]ww", 0, tp.file.title, "YYYY-MM-DD") %>|Week]] · [[<% tp.date.now("YYYY-MM-DD", 1, tp.file.title, "YYYY-MM-DD") %>|Next ▶]]

## 🎯 Top 3
1. 
2. 
3. 

> [!todo]- ✅ Today's tasks
> ```tasks
> not done
> (due before <% tp.date.now("YYYY-MM-DD", 1, tp.file.title, "YYYY-MM-DD") %>) OR (scheduled before <% tp.date.now("YYYY-MM-DD", 1, tp.file.title, "YYYY-MM-DD") %>)
> sort by due
> short mode
> hide edit button
> hide backlink
> ```

## 📝 Log
- 

## 🌙 End of day
- **Went well:** 
- **Got in the way:** 
- **First thing tomorrow:** 

> [!abstract]- 🗂️ Created today
> ```dataview
> LIST
> WHERE file.cday = date(<% tp.date.now("YYYY-MM-DD", 0, tp.file.title, "YYYY-MM-DD") %>) AND file.name != this.file.name
> SORT file.ctime ASC
> ```
