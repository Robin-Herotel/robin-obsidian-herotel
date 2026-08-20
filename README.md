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
  says *who it's with*; `#todo` marks an action item (done = the checkbox,
  not a tag). "Who
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
| `todo` | `> [!todo]+ #todo` | Owner, Due, one checkbox task | Expanded; checking the box marks it done — no tag to flip |
| `idea` | `> [!idea]+ #idea` | Free-text bullet(s) | Expanded |
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
#meeting/d-a               — Data & Analytics
#meeting/sdi
#meeting/bs-support         — maps to the real HR "Support" function
#meeting/bs-dev             — maps to the real HR "Systems Development" function
#meeting/business-systems   — the core Business Systems function itself
#meeting/digital-innovation
#meeting/it                 — Information Technology
#meeting/infrastructure
#meeting/praelexis
#meeting/commercial         — real HR department: Sales, Product, Customer Experience
#meeting/networks           — real HR department: field ops, NOC
#meeting/finance            — the broader division Information Systems sits inside
#meeting/customer-support    — real HR department: Helpdesk, Accounts
#meeting/hr
#meeting/external
```
Both lists live in the `types` and `counterparties` arrays at the top of
`Meeting Block.md` — add new entries there, the tag is generated
automatically (lowercased, spaces/`&` become hyphens).

There is no `series` tag — "which recurring meeting" is fully
covered by the combination of ceremony type + counterparty, with no third
tag to keep in sync.

**To-do** — a single flat tag, no lifecycle. "Done" is the checkbox itself
(`- [x]`), not a tag transition:
```
#todo
```

**Idea** — a single flat tag, no lifecycle. Ideation is just ideation;
promoting one to a full note in `Ideas/` is signaled by the link existing,
not by a tag change:
```
#idea
```

**Value** — what business outcome a delivered piece of work serves. Not a
meeting attribute — lives on the Outcome Block, logged when something
actually ships or a decision lands. Multi-select: one outcome can carry
several. Two framings sit side by side in one flat list — commercial
(revenue-facing) and QCDSM (operational):
```
#value/revenue-protect
#value/revenue-growth
#value/revenue-expand
#value/customer-experience
#value/cost-reduction        — QCDSM: Cost
#value/quality                — QCDSM: Quality
#value/delivery                — QCDSM: Delivery
#value/safety                  — QCDSM: Safety
#value/morale                  — QCDSM: Morale
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
| `Idea Block.md` | Inserts a `[!idea]` callout — pure ideation capture, no state |
| `To-do Block.md` | Inserts a `[!todo]` callout with owner/due/checkbox — an action item for you to track, done = checking the box |
| `Outcome Block.md` | Prompts for one or more value tags (loop, pick "Done" to finish), then a description; inserts a `[!outcome]` callout — use when something ships or a decision lands, for demonstrating team value later |
| `Diagram Block.md` | Prompts for a title, creates a new Excalidraw drawing in `Diagrams/`, embeds it at the cursor |
| `Photo Block.md` | Caption placeholder — use the mobile toolbar's camera/gallery icon to insert the image below it |

## Templates (spawn a whole new note — use "Create new note from template")

| Template | Use for |
|---|---|
| `Daily Note Template.md` | Used automatically by core Daily Notes — you shouldn't need to invoke this one manually |
| `Idea Template.md` | Full write-up once an idea (captured via Idea Block) earns its own note in `Ideas/` |
| `Meeting Diagram Template.excalidraw.md` | The generic canvas Diagram Block starts new drawings from — not usually invoked directly |

## Per-device setup (repeat on EVERY device, and after any vault reset)

**This is not one-time — it's per-device.** Because `.obsidian/*.json` is
deliberately untracked (see Sync process), no plugin setting syncs between
devices. Every device needs these entered by hand once, and again after any
full reset. Skipping this is what produces symptoms like daily notes
landing at `Daily/Untitled` instead of `Daily/2026-08-20`.

1. **Open this folder as a vault** in Obsidian.
2. **Install community plugins**: Settings → Community plugins → Browse →
   - `Templater`
   - `Excalidraw`
   - `Obsidian Git`
3. **Core plugins** (Settings → Core plugins):
   - **Daily notes** → **ON**
   - **Templates** → **OFF**. ⚠️ This is Obsidian's built-in feature, not
     Templater. It has a near-identical command name but *cannot* run
     Templater scripts — if enabled, it silently inserts `<%* ... %>` as
     literal text instead of executing it. Keep it off to remove the
     ambiguity entirely. See the trap note below.
4. **Configure Daily notes** (Settings → Daily notes):
   - Date format: `YYYY-MM-DD`
   - New file location: `Daily`
   - Template file location: `Templates/Daily Note Template.md`
5. **Configure Templater** (Settings → Templater):
   - Template folder location: `Templates`
   - Trigger Templater on new file creation: **on**
6. **Configure Excalidraw** (Settings → Excalidraw):
   - Use Excalidraw folder: **on** → `Diagrams`
   - Template for new drawings: `Templates/Meeting Diagram Template.excalidraw.md`
7. **Set commit identity** — same name/email on every device, matching your
   GitHub account, so history stays attributable:
   ```
   git config --global user.name "Robin Lawrence"
   git config --global user.email "<your GitHub email>"
   ```

### Trap: "Templates" vs "Templater"

Three commands look interchangeable and are not. Only the first is correct
for inserting a block:

| Command | What it does |
|---|---|
| **Templater: Open insert template modal** | ✅ Runs the script, inserts at cursor — **always use this** |
| Templater: Create new note from template | Spawns a separate new file/tab instead of inserting inline |
| Templates: Insert template | Core plugin — pastes raw text, does **not** run scripts |

Also: typing `[[` and picking a template from link autocomplete just
creates a *link to the template file*. It doesn't insert or run anything.

If a block ever inserts visible `<%*` code, spawns an unexpected new note,
or does nothing at all — it's almost always the command, not the file.
Consider setting a hotkey for "Templater: Open insert template modal"
(Settings → Hotkeys) so there's nothing to mis-tap.

## Sync process — the rules that prevent downtime

Git is doing a job it wasn't designed for: syncing a live-edited folder
across two devices, one of them mobile and sometimes offline. That works,
but only with discipline. These rules exist because each one maps to a real
failure that has already happened in this vault.

### What git tracks (and why nothing else)

`.gitignore` excludes everything device-specific, so git only ever touches
files you deliberately changed:
- `.obsidian/workspace*.json` — pane/tab layout, always differs per device
- `.obsidian/plugins/` — plugin *code*; reinstall per device via Community
  Plugins → Browse
- `.obsidian/app.json`, `appearance.json`, `community-plugins.json`,
  `core-plugins.json`, `daily-notes.json` — per-device settings. **These
  caused a hard sync loop**: Obsidian rewrites them whenever you toggle a
  plugin, which collided with git's tracked copy on every single clone.
- `.trash/` — local deleted-notes cache

**Never re-add anything under `.obsidian/` to git.** If a future change
seems to need it, the answer is a documented setup step in this README
instead.

### The four rules

1. **Pull before you type. Every session. Both devices.** This is the
   single highest-value habit — nearly every conflict comes from editing a
   file that the other device already changed.
2. **Push before you walk away.** Especially before the tablet goes
   offline. An unsynced tablet edit is the one scenario that creates a real
   conflict rather than a clean merge.
3. **One device per diagram.** Excalidraw files are JSON. Text notes merge
   cleanly or show readable conflict markers; a half-merged canvas can just
   fail to render. Finish a drawing and push before touching it elsewhere.
4. **Daily content goes straight to `main`. Structural changes go through a
   branch + PR.** See below — the review step has already caught real
   errors (stale templates, missing files) before they went live.

### Going offline with the tablet

Before losing connection:
1. Pull (get whatever desktop has)
2. Work offline freely — commits queue up locally, this is fine
3. On reconnect: **pull first, then push** — in that order

If step 3 reports a conflict, go to the runbook below. Do not force-push.

### Structural changes (templates, README, tag taxonomy) — desktop only

```
git checkout main
git pull
git checkout -b <short-branch-name>
# make the change
git add .
git commit -m "..."
git push -u origin <short-branch-name>
```
Then open the PR on GitHub, **read the diff**, merge, delete the branch.
Back on desktop: `git checkout main && git pull`.

Two traps that have bitten this repo already:
- **`git checkout -b` fails silently if the branch name already exists**,
  leaving you on `main` — so your "branch" commit lands on `main` instead.
  Always confirm with `git status` that you're on the branch you expect
  before committing.
- **PowerShell only.** `Expand-Archive` and friends don't exist in Command
  Prompt; a whole round of "the file didn't change" was cmd.exe silently
  failing. If the prompt doesn't start with `PS`, you're in the wrong shell.

### Tablet stays on `main`

The tablet never creates branches or opens PRs. It pulls, edits daily
content, commits, pushes. Mobile git is the least reliable link in this
chain — give it the simplest possible job.

## Runbook — when sync breaks

Work through these in order. Stop at the first one that resolves it.

**"Nothing happens" / plugin commands missing from the palette**
→ Settings → Community plugins. Check plugins are toggled **on** (deleting
`community-plugins.json` switches them all off). Then check Settings → Core
plugins → Daily notes is on.

**Daily note lands at `Daily/Untitled`, or template doesn't fill in**
→ Per-device settings aren't configured on this device. These never sync
(by design). Go to **Per-device setup** above and work through steps 3–6.
Most likely Daily notes has no date format / template path set. Delete the
stray `Untitled` note afterwards.

**Templater inserts raw `<%* %>` code instead of running it**
→ You used the wrong command. It must be **"Templater: Open insert template
modal"**. Obsidian's built-in *Templates* core plugin has a near-identical
command that doesn't run scripts — check Settings → Core plugins and make
sure **Templates** is **off** (see the trap table in Per-device setup).

**A block creates a new note/tab instead of inserting inline**
→ Also the wrong command: "Create new note from template" spawns a file.
Use "Open insert template modal". Also check you didn't type `[[` and pick
the template from link autocomplete — that just links to the template file.

**"Your local changes would be overwritten by checkout/merge"**
→ Something local differs from a tracked file. Check *what*:
`git status`. If it's a file you don't care about, `git checkout -- <file>`
to discard. If it's under `.obsidian/`, it shouldn't be tracked at all —
that's a bug in `.gitignore`, fix it rather than deleting the file again.

**Merge conflict in a note**
→ Open the file. Git leaves `<<<<<<<`, `=======`, `>>>>>>>` markers around
both versions. Keep what you want, delete the markers, save, commit. For
daily notes this is usually trivial — keep both halves.

**Merge conflict in an `.excalidraw.md` file**
→ Don't hand-merge JSON. Pick one side wholesale:
`git checkout --theirs "<path>"` (remote wins) or `--ours` (local wins),
then `git add` and commit. Redraw anything lost.

**Tablet is badly stuck and nothing above works — full reset**
This is safe *only* if the tablet has no unpushed work you care about.
1. Delete everything in the vault folder **except `.obsidian/`**
2. Command palette → **Git: Clone an existing remote repo**
3. URL: `https://github.com/Robin-Herotel/robin-obsidian-herotel.git`
4. **Vault Root** → **NO** to the `.obsidian` question → leave depth blank

Because nothing under `.obsidian/` is tracked anymore, you no longer need
to delete config files first, and plugins stay installed and enabled.

**Before any full reset, ask: is there unpushed work here?** If yes and
you can't push it, copy those specific files out to another folder first.
A reset discards anything git hasn't seen.

## Daily workflow

1. Open today's daily note — blank except the date heading.
2. Insert whatever blocks the moment calls for — a meeting, a to-do, an
   idea, an outcome, a diagram, a photo — in any order, as many times as needed.
3. Promote an idea that has legs into a full note via `Idea Template.md`.

There's no manual linking step for recurring meetings anymore — the
ceremony type + counterparty tag combination does that automatically.
Nothing to remember to update after a meeting ends.

## Worked example — one day, three meetings, a to-do, an idea, an outcome

```markdown
# 2026-08-18, Tuesday

> [!meeting]+ Sprint Planning #meeting/sprint-planning #meeting/bs-dev
> **Time:** 09:00
> **Attendees:**
>
> **Notes:**
> -

> [!todo]+ #todo
> **Owner:** Thabo
> **Due:** 2026-08-22
> - [ ] Confirm churn model retraining cadence

> [!meeting]+ Praelexis Standup #meeting/standup #meeting/praelexis
> **Time:** 11:00
> **Attendees:**
>
> **Notes:**
> -

> [!idea]+ #idea
> - NorthStar could auto-flag stale dashboards

> [!outcome]+ Churn model retrain shipped #value/cost-reduction #value/revenue-protect #value/quality
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
| `#todo` | Every action item, open or done, across every day |
| `#todo "Owner: Thabo"` | Everything Thabo owes you, open or done |
| `#todo "Owner: Thabo" "- [ ]"` | Just what Thabo still has open — add the literal checkbox text to exclude done items |
| `#idea` | Every idea you've ever captured |
| `#value/cost-reduction` | Every outcome that reduced cost, across every day — this quarter's whole cost-reduction case built from search alone |
| `#value/quality` or `#value/safety` or `#value/morale` | QCDSM-framed operational value, independent of the revenue framing |

## Notes

- `Meeting Diagram Template.excalidraw.md` is intentionally generic (3 boxes
  + connectors) — a starting layout, not a fixed diagram type.
