---
type: MOC
project: <% tp.file.folder() %>
created: <% tp.date.now("YYYY-MM-DD") %>
status: active
tags: [project, MOC]
---

# <% tp.file.folder() %> — Map of Content

> Internal project home page.

---

## What this is
- **One-line description:**
- **Why it exists:**
- **Owner:**
- **Started:** <% tp.date.now("YYYY-MM-DD") %>
- **Status:** active

---

## Current focus
- [ ]
- [ ]

---

## Recent sessions
```dataview
TABLE date as "Date", topic as "Topic"
FROM "wiki/projects/<% tp.file.folder() %>/sessions"
SORT date DESC
LIMIT 10
```

---

## Open tasks
```dataview
TASK
FROM "wiki/projects/<% tp.file.folder() %>"
WHERE !completed
```

---

## Linked concepts
-

## Linked clients
-
