<%*
// Meeting type — add new types here as they come up. Keep names matching
// the README's tag taxonomy exactly (case matters in Obsidian tags).
const types = ["team", "Herotel-stakeholder", "sprint-planning", "standup", "1-1", "external"];
const type = await tp.system.suggester(types, types, false, "Meeting type?");

// Meeting series — add recurring series here as they come up. "One-off"
// skips the series tag entirely and just asks for a free-text name.
// The series tag is derived automatically from the name (lowercased,
// spaces -> hyphens) so you never have to remember exact tag spelling.
const series = ["Praelexis Standup", "One-off / no series"];
const chosenSeries = await tp.system.suggester(series, series, false, "Meeting series?");

let title, seriesTag;
if (chosenSeries === "One-off / no series") {
	title = await tp.system.prompt("Meeting name?", "");
	seriesTag = "";
} else {
	title = chosenSeries;
	seriesTag = " #meeting/" + chosenSeries.toLowerCase().replace(/\s+/g, "-");
}

tR = `> [!meeting]+ ${title} #meeting/${type}${seriesTag}
> **Time:** ${tp.date.now("HH:mm")}
> **Attendees:**
>
> **Notes:**
> -
`;
%>
