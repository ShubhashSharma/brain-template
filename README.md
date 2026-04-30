---
type: vault-readme
created: today
---

# Welcome to your brain

This is your **second brain** — a structured place to capture, link, and revisit everything you work on. It runs on [Obsidian](https://obsidian.md) and syncs to a private GitHub repo via the **obsidian-git** plugin.

---

## What goes where

| Folder | What it holds |
|---|---|
| `wiki/clients/` | One folder per client. Context, sessions, tasks, lessons. |
| `wiki/projects/` | Internal projects, products, ventures. |
| `wiki/internal/` | Operations areas — your business itself, not a client. |
| `wiki/personal/` | Personal notes, life admin, anything non-work. |
| `wiki/concepts/` | Patterns, frameworks, mental models. Reusable thinking. |
| `wiki/entities/` | People and companies. Linked from everywhere. |
| `wiki/daily/` | Daily roll-ups (`YYYY-MM-DD.md`). One per day, optional. |
| `wiki/queries/` | Saved Dataview queries — "what's open across all clients", etc. |
| `raw/` | Unfiltered inputs. Email exports, Slack dumps, transcripts, anything raw before you curate it. |
| `_templates/` | Templater templates. Used to create new clients, sessions, MOCs in one click. |

---

## How to actually use it

1. **Capture in `raw/`** — anything you're not sure where to put goes here first.
2. **Curate into `wiki/`** — once a piece of raw has value, move it (or distil it) into the right wiki folder.
3. **Link aggressively** — use `[[double brackets]]` to link people, companies, concepts. The graph is the value.
4. **Run `/wrap` (Claude Code users)** — at the end of any work session, this auto-mirrors progress into the right `sessions/` folder.

---

## Daily flow (5 minutes)

- Open Obsidian. obsidian-git auto-pulls the latest version.
- Write what you need to write.
- Close Obsidian (or just leave it). Auto-commits every 30 seconds, auto-pushes too.
- That's it.

---

## First things to set up

1. Create your first client folder: `wiki/clients/<ClientName>/` and add a `MOC.md` (use the template in `_templates/MOC-template.md`).
2. Create your daily note: `wiki/daily/YYYY-MM-DD.md` (use `_templates/daily-template.md`).
3. Open the **graph view** (left sidebar icon) and watch your brain take shape as you link things.

---

## Read next

- `_templates/` — copy these to start any new client, project, session, or daily note.
- The setup guide that came with this template (one-time install steps for sync + Claude Code).
