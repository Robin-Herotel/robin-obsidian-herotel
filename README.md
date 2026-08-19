# Robin — Herotel Work Vault

Daily-note-driven vault for meeting capture + inline diagramming. Each daily
note starts **blank except the date** — content comes from pulling in
**blocks**, on demand, as a session unfolds. Multiple meetings, ideas, and
follow-ups all live inside one day's note, each contained in its own
**callout**, rather than spinning off into separate files.

## Folder structure

```
Daily/            One note per calendar day, created bare from the date template.
Meetings/         Index notes — one per recurring meeting (e.g. "Praelexis Standup").
                  Not raw content: they link OUT to the daily notes that discussed them.
Diagrams/         All Excalidraw drawings live here, one file per diagram.
Projects/
  NorthStar/
  HeroVision/
  Footprint/
Ideas/            Full write-ups for ideas that earned their own note
                  (promoted from an Idea Block via Idea Template.md).
Templates/        Templater + Excalidraw templates — see "Blocks" and
                  "Templates" below. Naming convention: files ending in
                  "Template" spawn a whole new note; files ending in
                  "Block" insert inline into a note you're already in.
Attachments/      Images, PDFs, anything dragged or pasted into a note.
```

## The organizing rule: folders / tags / links each do one job

- **Folders** — broad separation (this list above). Rarely change.
- **Tags** — mark **type** or **state**, never topic or person. `#meeting/1-1`
  says *what kind* of meeting; `#followup/open` says *what state* a task is
  in. "Who owns this" is a field (`**Owner:**`), not a tag. "What project is
  this about" is a `[[link]]` to that project's note, not a tag. This keeps
  the tag list from growing into one tag per person or per project as the
  team grows.
- **Links** — connection and context. The `[[Meetings/...]]` backlink from a
  meeting callout to its recurring-meeting index note is this vault's one
  deliberate link pattern — keep using it rather than replacing it with tags.

## Callouts

Meeting, Followup, and Idea blocks render as **callouts** (`> [!type]`) —
a foldable box that visually contains everything about that item while
staying inside the daily note. Diagram and Photo don't use a callout; an
embed or a captioned image doesn't need a box around it.

| Callout | Syntax | Contains | Default state |
|---|---|---|---|
| `meeting` | `> [!meeting]+ Name #meeting/<type>` | Time, Attendees, linked meeting index, Notes | Expanded — you're actively in it |
| `followup` | `> [!followup]+ #followup/open` | Owner, Due, one checkbox task | Expanded while open; collapse once closed |
| `idea` | `> [!idea]+ #idea/raw` | Free-text bullet(s) | Expanded |

## Tag taxonomy

**Meeting type** (parent `#meeting` catches all; narrow with a subtype):
```
#meeting/team                    — internal team / Praelexis catchups
#meeting/Herotel-stakeholder      — cross-department / internal stakeholder engagement
#meeting/sprint-planning
#meeting/standup
#meeting/1-1                     — one-on-ones
#meeting/external                — vendor / partner / customer-facing
```
Add new types by editing the `types` list at the top of `Meeting Block.md` —
the Templater prompt reads from that list, so new meeting types show up in
the picker without hunting for exact tag spelling later.

**Followup state:**
```
#followup/open        — default on creation
#followup/delegated    — handed to someone else; who goes in **Owner:**
#followup/done
```

**Idea state:**
```
#idea/raw          — default on creation
#idea/exploring
#idea/promoted     — has a full note in Ideas/; link it back
#idea/parked
```

## Blocks (insert into the note you're already in)

Cursor where you want it → Command Palette → **"Templater: Open insert
template modal"** (not "Create new note from template" — that one spawns a
separate file/tab instead of inserting inline):

| Block | Use for |
|---|---|
| `Meeting Block.md` | Prompts for meeting type + name, inserts a `[!meeting]` callout |
| `Notes Block.md` | Lightweight timestamped bullet, no callout, no meeting header needed |
| `Idea Block.md` | Inserts a `[!idea]` callout; promote to `Ideas/` later if it develops |
| `Followup Block.md` | Inserts a `[!followup]` callout with owner/due/checkbox |
| `Diagram Block.md` | Prompts for a title, creates a new Excalidraw drawing in `Diagrams/`, embeds it at the cursor |
| `Photo Block.md` | Caption placeholder — use the mobile toolbar's camera/gallery icon to insert the image below it |

## Templates (spawn a whole new note — use "Create new note from template")

| Template | Use for |
|---|---|
| `Daily Note Template.md` | Used automatically by core Daily Notes — you shouldn't need to invoke this one manually |
| `Idea Template.md` | Full write-up once an idea (captured via Idea Block) earns its own note in `Ideas/` |
| `Meeting Diagram Template.excalidraw.md` | The generic canvas Diagram Block starts new drawings from — not usually invoked directly |

## One-time setup (do this in Obsidian, in order)

1. **Open this folder as a vault** in Obsidian.
2. **Install community plugins**: Settings → Community plugins → Browse →
   - `Templater`
   - `Excalidraw`
   - (core, not community) **Daily notes** — enable under Settings → Core plugins.
3. **Configure Daily notes** (Settings → Daily notes):
   - Date format: `YYYY-MM-DD`
   - New file location: `Daily`
   - Template file location: `Templates/Daily Note Template.md`
4. **Configure Templater** (Settings → Templater):
   - Template folder location: `Templates`
   - Trigger Templater on new file creation: **on**
5. **Configure Excalidraw** (Settings → Excalidraw):
   - Use Excalidraw folder: **on** → `Diagrams`
   - Template for new drawings: `Templates/Meeting Diagram Template.excalidraw.md`

## Git hygiene — read before syncing across devices

`.gitignore` in this repo excludes:
- `.obsidian/workspace*.json` — local pane/tab layout, always differs per
  device; tracking it just causes conflicts with no benefit.
- `.obsidian/plugins/` — plugin *code*. Reinstall plugins per device via
  Community Plugins → Browse, don't sync the code through git.

If a device already has these committed from an earlier backup, run once:
```
git rm -r --cached .obsidian/plugins
git rm --cached .obsidian/workspace-mobile.json .obsidian/workspace.json 2>/dev/null
git add .gitignore
git commit -m "Stop tracking plugin binaries and device-specific workspace state"
git push
```

## Daily workflow

1. Open today's daily note — blank except the date heading.
2. Insert whatever blocks the moment calls for — a meeting, a followup, an
   idea, a diagram, a photo — in any order, as many times as needed.
3. If a meeting recurs, add a line to its index note in `Meetings/` linking
   back to today's daily note.
4. Promote an idea that has legs into a full note via `Idea Template.md`.

## Worked example — one day, three meetings, a followup, an idea

```markdown
# 2026-08-18, Tuesday

> [!meeting]+ Sprint Planning #meeting/sprint-planning
> **Time:** 09:00
> **Attendees:**
> **Linked meeting index:** [[Meetings/]]
>
> **Notes:**
> -

> [!followup]+ #followup/open
> **Owner:** Thabo
> **Due:** 2026-08-22
> - [ ] Confirm churn model retraining cadence

> [!meeting]+ Praelexis Standup #meeting/team
> **Time:** 11:00
> **Attendees:**
> **Linked meeting index:** [[Meetings/Praelexis Standup]]
>
> **Notes:**
> -

> [!idea]+ #idea/raw
> - NorthStar could auto-flag stale dashboards

> [!meeting]+ Vendor Check-in — QContact #meeting/external
> **Time:** 15:00
> **Attendees:**
> **Linked meeting index:** [[Meetings/]]
>
> **Notes:**
> -
```

**What searching this later gets you:**

| Search | Returns |
|---|---|
| `#meeting` | Every meeting, any type, across every day |
| `#meeting/1-1` | Just your one-on-ones |
| `#followup/open` | Every open action item, across every day |
| `#followup/open "Owner: Thabo"` | Everything open that Thabo owes you |
| `#idea/raw` | Every idea not yet triaged |

## Notes

- `Meetings/Praelexis Standup.md` is a worked example of the index pattern —
  copy it for other recurring meetings, then delete it once you've got a few
  real ones.
- `Meeting Diagram Template.excalidraw.md` is intentionally generic (3 boxes
  + connectors) — a starting layout, not a fixed diagram type.
