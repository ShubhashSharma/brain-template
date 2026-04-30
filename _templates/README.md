# Templates

Files in this folder are used by the **Templater** plugin to spin up new notes in one click.

## Available templates

| File | What it creates |
|---|---|
| `client-MOC-template.md` | A new client home page with Dataview blocks for sessions, tasks, lessons |
| `project-MOC-template.md` | Same for an internal project |
| `context-template.md` | The `context.md` that lives inside each client folder |
| `session-template.md` | A single work-session note (auto-fills date + parent folder) |
| `daily-template.md` | A daily roll-up note |
| `person-template.md` | A person entity in `wiki/entities/people/` |
| `concept-template.md` | A reusable concept/framework note |

## How to use

1. Settings → Community plugins → enable **Templater**
2. Settings → Templater → set **Template folder location** to `_templates`
3. Settings → Templater → assign a hotkey (e.g. `Cmd+Shift+T`) to **Create new note from template**
4. In any folder, hit the hotkey, pick a template — done.

## Customise

These are starting points. Edit them to match how you actually work. The `<% ... %>` syntax is Templater — it auto-fills date, folder name, etc. Leave that alone unless you know what you're doing.
