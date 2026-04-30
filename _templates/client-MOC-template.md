---
type: MOC
client: <% tp.file.folder() %>
created: <% tp.date.now("YYYY-MM-DD") %>
status: active
tags: [client, MOC]
---

# <% tp.file.folder() %> — Map of Content

> Home page for this client. Links to everything that matters.

---

## Quick context
- **What they do:**
- **Primary contact:** [[<% tp.file.folder() %>-primary]]
- **Started:** <% tp.date.now("YYYY-MM-DD") %>
- **Status:** active

See full context → [[context]]

---

## Active priorities
- [ ]
- [ ]
- [ ]

---

## Recent sessions
```dataview
TABLE date as "Date", topic as "Topic"
FROM "wiki/clients/<% tp.file.folder() %>/sessions"
SORT date DESC
LIMIT 10
```

---

## Open tasks
```dataview
TASK
FROM "wiki/clients/<% tp.file.folder() %>"
WHERE !completed
GROUP BY file.link
```

---

## Lessons & patterns
```dataview
LIST
FROM "wiki/clients/<% tp.file.folder() %>/lessons"
SORT file.ctime DESC
```

---

## Key people
- [[<% tp.file.folder() %>-primary]]
-

## Related projects
-
