<%*
// Value tags — commercial framing (revenue-*, customer-experience) plus
// QCDSM (Quality, Cost, Delivery, Safety, Morale) operational framing.
// Add new ones here as needed, keep "Done" last in the list.
const values = ["revenue-protect", "revenue-growth", "revenue-expand", "customer-experience", "cost-reduction", "quality", "delivery", "safety", "morale", "Done - no more tags"];
let chosen = [];
while (true) {
	const pick = await tp.system.suggester(values, values, false, "Add a value tag (pick Done to finish)");
	if (pick === "Done - no more tags") break;
	if (!chosen.includes(pick)) chosen.push(pick);
}
const tagLine = chosen.map(v => "#value/" + v).join(" ");
const title = await tp.system.prompt("Outcome — short description?", "");

tR = `> [!outcome]+ ${title} ${tagLine}
> **Linked project:**
>
> **Details:**
> -
`;
%>
