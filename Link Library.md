---
type: link-index
tags: [links]
---
# 📚 Link Library

```dataviewjs
const pages = dv.pages('"Links"')
  .where(p => p.type === "link-library")
  .sort(p => p.file.name, "asc");

const rows = [];
for (const p of pages) {
  const text = (await dv.io.load(p.file.path)) || "";
  const count = (text.match(/^```cardlink/gm) || []).length;
  rows.push([p.file.link, count, p.description || ""]);
}

if (rows.length === 0) {
  dv.paragraph("No subjects yet. Create one with the **Link Subject** template.");
} else {
  dv.table(["Subject", "🔗", "About"], rows);
}
```

> [!info]- 🕒 Recently updated
> ```dataview
> LIST
> FROM "Links"
> WHERE type = "link-library"
> SORT file.mtime DESC
> LIMIT 5
> ```
