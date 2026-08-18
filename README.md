# Robin — Herotel Work Vault

Daily-note-driven vault for meeting capture + inline diagramming. One note per **day**, one repeatable block per **meeting**, diagrams embedded inline via Excalidraw.

## Folder structure

```
Daily/            One note per calendar day. This is where live capture happens.
Meetings/         Index notes — one per recurring meeting (e.g. "Praelexis Standup").
                  Not raw content: they link OUT to the daily notes that discussed them.
Diagrams/         All Excalidraw drawings live here, one file per diagram.
Projects/
  NorthStar/
  HeroVision/
  Footprint/
Ideas/            One note per idea, created from Templates/Idea.md. Loose capture,
                  promote to Projects/ when it has legs.
Templates/        Templater + Excalidraw templates.
Attachments/      Images, PDFs, anything dragged into a note.
```

## One-time setup (do this in Obsidian, in order)

1. **Open this folder as a vault** in Obsidian (Open folder as vault).
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
   - Trigger Templater on new file creation: **on** (so the Daily note fills itself in automatically when core Daily Notes creates it)
5. **Configure Excalidraw** (Settings → Excalidraw):
   - Excalidraw folder: `Diagrams`
   - Default template for new drawings: `Templates/Meeting Diagram.excalidraw.md`

## Daily workflow

1. Open today's daily note (Ctrl/Cmd+O or the ribbon calendar icon) — Templater fills in the date heading and one meeting block.
2. Per meeting: duplicate the `### Meeting block` (see comment in the template) and fill in time / attendees / notes.
3. Need a diagram mid-meeting: Command Palette → **Excalidraw: Create new drawing** → save into `Diagrams/` named `YYYY-MM-DD Meeting Name` → embed it under that meeting's notes with `![[Diagrams/2026-08-18 Praelexis Standup.md]]`.
4. If the meeting recurs, add a line to (or create) its index note in `Meetings/` linking back to today's daily note.
5. Any idea that comes up: quick-add a line under "Ideas captured today" in the daily note; if it's worth developing, create a proper note from `Templates/Idea.md` in `Ideas/` and link it.

## Notes

- `Meetings/Praelexis Standup.md` is included as a worked example of the index pattern — copy it for other recurring meetings, then delete it once you've got a few real ones.
- The Excalidraw template is intentionally generic (3 boxes + connectors) — it's a starting layout, not a fixed diagram type.
