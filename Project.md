<%*
const name = await tp.system.prompt("Project name");
const status = await tp.system.suggester(["🟢 Active", "🟡 Planning", "⏸️ On hold", "✅ Done"], ["active", "planning", "on-hold", "done"]);
const due = await tp.system.prompt("Target date (YYYY-MM-DD, or blank)", "");
await tp.file.move("Projects/" + name);
-%>
---
type: project
status: <% status %>
started: <% tp.date.now("YYYY-MM-DD") %>
due: <% due %>
board: 
tags: [project]
---
# 🚀 <% name %>

**Goal:** 
**Done looks like:** 

## ✅ Next actions
- [ ] 

> [!warning]- 📋 All open tasks
> ```tasks
> not done
> (path includes <% name %>) OR (description includes [[<% name %>]])
> sort by due
> short mode
> hide edit button
> ```

## 📓 Log
- <% tp.date.now("MMM D") %>: Created

## 🔗 Resources
- 

> [!info]- 🧭 Mentioned in
> ```dataview
> LIST
> FROM [[]]
> SORT file.mtime DESC
> ```
