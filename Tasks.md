---
tags: [dashboard]
---

# Tasks

Auto-populated from every note in the vault. Nothing is copied here by
hand — write a to-do anywhere and it appears below. Tick the checkbox
(here or in the original note) and it moves to Done.

**Capture format**, in any note:
```
- [ ] the thing that needs doing #todo
```

---

## Open

```dataview
TASK
WHERE !completed
  AND contains(text, "#todo")
  AND !contains(file.path, "Templates/")
SORT file.name DESC
```

## Done

```dataview
TASK
WHERE completed
  AND contains(text, "#todo")
  AND !contains(file.path, "Templates/")
SORT file.name DESC
LIMIT 50
```

---

## Safety net — every unchecked box, tagged or not

Catches anything you forgot to tag, so a stray checkbox can't go missing.

```dataview
TASK
WHERE !completed
  AND !contains(file.path, "Templates/")
  AND file.name != "Tasks"
SORT file.name DESC
```

<!--
Note on the queries: they filter with WHERE contains(text, "#todo") rather
than FROM #todo on purpose. FROM #todo would match every task in any note
that mentions #todo anywhere - including untagged tasks in the same daily
note. Filtering on the task's own text keeps it accurate.

Tasks written inside a To-do Block callout do not carry #todo on the
checkbox line itself, so they surface in the safety net section rather than
Open. The To-do Block has been updated to include #todo on its checkbox
line so both capture styles land in Open.
-->
