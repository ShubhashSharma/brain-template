---
type: daily
date: <% tp.date.now("YYYY-MM-DD") %>
tags: [daily]
---

# <% tp.date.now("YYYY-MM-DD") %>

## Focus today
- 
- 
- 

## Done
- 

## Notes / thoughts
- 

## Tomorrow
- 

---

## Sessions today
```dataview
TABLE client, topic
FROM "wiki/clients" or "wiki/projects"
WHERE type = "session" AND date = "<% tp.date.now("YYYY-MM-DD") %>"
```
