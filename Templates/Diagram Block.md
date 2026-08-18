<%*
// Prompts for a title, creates a new drawing in Diagrams/ from the generic
// Meeting Diagram template, and embeds it at the cursor.
const defaultTitle = tp.date.now("YYYY-MM-DD HHmm");
const title = await tp.system.prompt("Diagram title?", defaultTitle);
const ea = ExcalidrawAutomate;
ea.reset();
await ea.create({
	filename: title,
	foldername: "Diagrams",
	templatePath: "Templates/Meeting Diagram.excalidraw.md",
	onNewPane: true
});
tR = "**Diagram:** ![[Diagrams/" + title + ".md]]";
%>
