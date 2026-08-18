# Robin — Herotel Work Vault

Daily-note-driven vault for meeting capture + inline diagramming. Each daily
note starts **blank except for the date** — you pull in whatever blocks you
need, as you need them, rather than filling out a fixed form.

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
Ideas/            One note per idea, created from Templates/Idea.md when an
                  idea earns its own write-up (promoted from an Idea Block).
Templates/        Templater + Excalidraw templates — see "Blocks" below.
Attachments/      Images, PDFs, anything dragged or pasted into a note.
```

## Blocks

The daily note is just frontmatter + a date heading. Content comes from
inserting one of these, cursor wherever you want it, via Command Palette →
**Templater: Insert Template**:

| Block | Use for |
|---|---|
| `Meeting Block.md` | Header, time, attendees, notes for one meeting |
| `Notes Block.md` | Lightweight timestamped bullet, no meeting header needed |
| `Idea Block.md` | Quick inline idea capture; promote to `Ideas/` later if it has legs |
| `Followup Block.md` | A single open-thread checkbox item |
| `Diagram Block.md` | Prompts for a title, creates a new Excalidraw drawing in `Diagrams/` from the generic template, embeds it at the cursor |
| `Photo Block.md` | Caption placeholder — use the mobile toolbar's camera/gallery icon to insert the actual image below it |

Bring in as many of each as the session needs — a meeting with three
diagrams and two follow-ups is six inserts, not six different note files.

## One-time setup (do this in Obsidian, in order)

1. **Open this folder as a vault** in Obsidian.
2. **Install community plugins**: Settings → Community plugins → Browse →
   - `Templater`
   - `Excalidraw`
   - (core, not community) **Daily notes** — enable under Settings → Core plugins.
3. **Configure Daily notes** (Settings → Daily notes):
   - Date format: `YYYY-MM-DD`
   - New file location: `Daily`
   - Template file location: `Templates/Daily Note.md`
4. **Configure Templater** (Settings → Templater):
   - Template folder location: `Templates`
   - Trigger Templater on new file creation: **on**
5. **Configure Excalidraw** (Settings → Excalidraw):
   - Use Excalidraw folder: **on** → `Diagrams`
   - Template for new drawings: `Templates/Meeting Diagram.excalidraw.md`

## Git hygiene — read before syncing across devices

`.gitignore` in this repo excludes:
- `.obsidian/workspace*.json` — local pane/tab layout, always differs per
  device; tracking it just causes conflicts with no benefit.
- `.obsidian/plugins/` — plugin *code*. Reinstall plugins per device via
  Community Plugins → Browse, don't sync the code through git. Tracking it
  bloats the repo and creates diff noise on every plugin auto-update.

If you're re-cloning on a device that already has an untracked `.obsidian`
folder with these files committed from an earlier backup, run once:
```
git rm -r --cached .obsidian/plugins
git rm --cached .obsidian/workspace-mobile.json .obsidian/workspace.json 2>/dev/null
git add .gitignore
git commit -m "Stop tracking plugin binaries and device-specific workspace state"
git push
```

## Daily workflow

1. Open today's daily note — it starts blank except the date heading.
2. Insert whatever blocks the moment calls for (see table above).
3. If a meeting recurs, add a line to its index note in `Meetings/` linking
   back to today's daily note.
4. Any idea worth developing further: promote it from an Idea Block into a
   full note via `Templates/Idea.md` in `Ideas/`, and link it back.

## Notes

- `Meetings/Praelexis Standup.md` is a worked example of the index pattern —
  copy it for other recurring meetings, then delete it once you've got a few
  real ones.
- The Excalidraw template is intentionally generic (3 boxes + connectors) —
  a starting layout, not a fixed diagram type.
