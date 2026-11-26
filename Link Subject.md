<%*
const name = await tp.system.prompt("Subject name");
const desc = (await tp.system.prompt("One-line description (optional)", "")) || "";
await tp.file.move("Links/" + name);
-%>
---
type: link-library
description: "<% desc.replace(/\\/g, "\\\\").replace(/"/g, '\\"') %>"
created: <% tp.date.now("YYYY-MM-DD") %>
tags: [links]
---
# 🔖 <% name %>

[[Templates/Link Library|◀ Library]]<% desc ? "  ·  *" + desc + "*" : "" %>

---

<% tp.file.cursor() %>
