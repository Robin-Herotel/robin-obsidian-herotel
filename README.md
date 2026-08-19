# Robin — Herotel Work Vault

Daily-note-driven vault for meeting capture + inline diagramming. Each daily
note starts **blank except the date** — content comes from pulling in
**blocks**, on demand, as a session unfolds. Multiple meetings, ideas, and
follow-ups all live inside one day's note, each contained in its own
**callout**, rather than spinning off into separate files. Everything is
found later through **tags**, not folders — see the rule below before
adding any new folder to this vault.

## Folder structure

```
Daily/            One note per calendar day, created bare from the date template.
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

## The rule for adding a new folder

A folder is only justified for one of two reasons:

1. **The content isn't a record of a particular day** — it's a persistent
   artifact, read and edited across many days regardless of when it was
   created (a project's accumulated knowledge, an idea promoted into its
   own note).
2. **A plugin technically requires a separate file** — Excalidraw canvases
   and pasted images can't live inline as markdown text; Obsidian has to
   store them separately no matter how you'd prefer to organize.

Anything that is fundamentally "what happened on this day" — a meeting, an
idea as it's first captured, a follow-up — stays **inside** the daily note
and gets found later purely through **tags**. It never gets its own folder
or its own index note, even if it repeats every week. (This vault used to
have a `Meetings/` folder with one index note per recurring meeting — that
broke this rule, since a recurring meeting is an event, not a persistent
artifact. It's been replaced by ceremony-type and counterparty tags below.)

| Folder | Why it survives the rule |
|---|---|
| `Daily/` | It IS the day — the spine everything else hangs off |
| `Diagrams/` | Rule 2 — Excalidraw can't inline a canvas |
| `Attachments/` | Rule 2 — Obsidian can't inline a binary file |
| `Projects/` | Rule 1 — accumulated knowledge, not tied to one day |
| `Ideas/` | Rule 1 — same logic as Projects, once an idea is promoted |

## The organizing rule: folders / tags / links each do one job

- **Folders** — broad separation, governed by the rule above. Rarely change.
- **Tags** — mark **type**, **state**, or **who a meeting's with** — never
  topic or person. `#meeting/1-1` says *what kind*; `#meeting/bs-dev`
  says *who it's with*; `#followup/open` says *what state*. "Who
  owns this" is a field (`**Owner:**`), not a tag. "What project is this
  about" is a `[[link]]` to that project's note, not a tag.
- **Links** — connection and context, used sparingly (e.g. linking a
  promoted Idea Block to its full note in `Ideas/`).

## Callouts

Meeting, Followup, and Idea blocks render as **callouts** (`> [!type]`) —
a foldable box that visually contains everything about that item while
staying inside the daily note. Diagram and Photo don't use a callout; an
embed or a captioned image doesn't need a box around it.

| Callout | Syntax | Contains | Default state |
|---|---|---|---|
| `meeting` | `> [!meeting]+ Name #meeting/<type> #meeting/<counterparty>` | Time, Attendees, Notes | Expanded — you're actively in it |
| `followup` | `> [!followup]+ #followup/open` | Owner, Due, one checkbox task | Expanded while open; collapse once closed |
| `idea` | `> [!idea]+ #idea/raw` | Free-text bullet(s) | Expanded |
| `outcome` | `> [!outcome]+ Name #value/<tag> [#value/<tag> ...]` | Linked project, Details | Expanded — for reviewing what shipped |

## Tag taxonomy

**Meeting: ceremony type** (the FORMAT of the meeting — nothing about who's
in it). Parent `#meeting` catches all; narrow with a subtype:
```
#meeting/standup
#meeting/sprint-planning
#meeting/retro
#meeting/1-1
#meeting/workshop
#meeting/problem-solving
#meeting/review
#meeting/planning
#meeting/training
#meeting/steering
#meeting/general
```

**Meeting: counterparty** (WHO the meeting is with — nothing about
format). Independent of ceremony type — a meeting carries both:
```
#meeting/general
#meeting/d-a            — Data & Analytics
#meeting/sdi
#meeting/bs-support      — maps to the real HR "Support" function
#meeting/bs-dev          — maps to the real HR "Systems Development" function
#meeting/praelexis
#meeting/external
```
Both lists live in the `types` and `counterparties` arrays at the top of
`Meeting Block.md` — add new entries there, the tag is generated
automatically (lowercased, spaces/`&` become hyphens).

There is no `series` tag — "which recurring meeting" is fully
covered by the combination of ceremony type + counterparty, with no third
tag to keep in sync.

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

**Value** — what business outcome a delivered piece of work serves. Not a
meeting attribute — lives on the Outcome Block, logged when something
actually ships or a decision lands, not on every meeting. Multi-select: one
outcome can carry several:
```
#value/revenue-protect
#value/revenue-growth
#value/revenue-expand
#value/customer-experience
#value/cost-reduction
```
Add new ones by editing the `values` array at the top of `Outcome Block.md`
(keep "Done - no more tags" last in the list — that's what ends the
multi-select loop).

## Blocks (insert into the note you're already in)

Cursor where you want it → Command Palette → **"Templater: Open insert
template modal"** (not "Create new note from template" — that one spawns a
separate file/tab instead of inserting inline). This is the command
confirmed working end-to-end — including the multi-step prompts in Meeting
and Diagram blocks, which fire as a sequence of pop-ups from this same
command, one after another.

| Block | Use for |
|---|---|
| `Meeting Block.md` | Prompts for ceremony type, then counterparty; inserts a `[!meeting]` callout with both tags |
| `Notes Block.md` | Lightweight timestamped bullet, no callout, no meeting header needed |
| `Idea Block.md` | Inserts a `[!idea]` callout; promote to `Ideas/` later if it develops |
| `Followup Block.md` | Inserts a `[!followup]` callout with owner/due/checkbox |
| `Outcome Block.md` | Prompts for one or more value tags (loop, pick "Done" to finish), then a description; inserts a `[!outcome]` callout — use when something ships or a decision lands, for demonstrating team value later |
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
3. Promote an idea that has legs into a full note via `Idea Template.md`.

There's no manual linking step for recurring meetings anymore — the
ceremony type + counterparty tag combination does that automatically.
Nothing to remember to update after a meeting ends.

## Worked example — one day, three meetings, a followup, an idea

```markdown
# 2026-08-18, Tuesday

> [!meeting]+ Sprint Planning #meeting/sprint-planning #meeting/bs-dev
> **Time:** 09:00
> **Attendees:**
>
> **Notes:**
> -

> [!followup]+ #followup/open
> **Owner:** Thabo
> **Due:** 2026-08-22
> - [ ] Confirm churn model retraining cadence

> [!meeting]+ Praelexis Standup #meeting/standup #meeting/praelexis
> **Time:** 11:00
> **Attendees:**
>
> **Notes:**
> -

> [!idea]+ #idea/raw
> - NorthStar could auto-flag stale dashboards

> [!outcome]+ Churn model retrain shipped #value/cost-reduction #value/revenue-protect
> **Linked project:** [[Projects/Churn Model]]
>
> **Details:**
> - Reduced false-positive churn flags by 18%, cut manual review time

> [!meeting]+ Vendor Check-in — QContact #meeting/general #meeting/external
> **Time:** 15:00
> **Attendees:**
>
> **Notes:**
> -
```

**What searching this later gets you:**

| Search | Returns |
|---|---|
| `#meeting` | Every meeting, any type, across every day |
| `#meeting/1-1` | Just your one-on-ones |
| `#meeting/standup #meeting/bs-dev` | Every BS-Dev standup — type + counterparty combined |
| `#followup/open` | Every open action item, across every day |
| `#followup/open "Owner: Thabo"` | Everything open that Thabo owes you |
| `#idea/raw` | Every idea not yet triaged |
| `#value/cost-reduction` | Every outcome that reduced cost, across every day — this quarter's whole cost-reduction case built from search alone |

## Notes

- `Meeting Diagram Template.excalidraw.md` is intentionally generic (3 boxes
  + connectors) — a starting layout, not a fixed diagram type.
