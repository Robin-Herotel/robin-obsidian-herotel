<%*
// Meeting type list — add new types here as they come up; keep names
// matching the Tags sheet/README exactly (case matters in Obsidian tags).
const types = ["team", "Herotel-stakeholder", "sprint-planning", "standup", "1-1", "external"];
const type = await tp.system.suggester(types, types, false, "Meeting type?");
const title = await tp.system.prompt("Meeting name?", "");
tR = `> [!meeting]+ ${title} #meeting/${type}
> **Time:** ${tp.date.now("HH:mm")}
> **Attendees:**
> **Linked meeting index:** [[Meetings/]]
>
> **Notes:**
> -
`;
%>
