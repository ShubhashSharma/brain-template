---
type: person
created: <% tp.date.now("YYYY-MM-DD") %>
tags: [person]
company: 
role: 
---

# <% tp.file.title %>

**Role:**
**Company:** [[]]
**Email:**
**Last contact:** <% tp.date.now("YYYY-MM-DD") %>

---

## Context
> Who they are, how you met, why they matter.

## Recent interactions
```dataview
TABLE date, topic
FROM "wiki/clients" or "wiki/projects"
WHERE contains(file.outlinks, [[<% tp.file.title %>]]) AND type = "session"
SORT date DESC
LIMIT 10
```

## Notes
-
