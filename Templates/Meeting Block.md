<%*
// Ceremony type — the FORMAT of the meeting, nothing about who's in it.
// Add new types here as needed.
const types = ["standup", "sprint-planning", "retro", "1-1", "workshop", "problem-solving", "review", "planning", "training", "steering", "general"];
const type = await tp.system.suggester(types, types, false, "Ceremony type?");

// Counterparty — WHO the meeting is with, nothing about format.
// Explicit lookup (display name -> tag) instead of a regex-generated slug,
// so new counterparties are one line to add and the tag is always exact.
const counterpartyTags = {
	"general": "general",
	"D&A": "d-a",
	"SDI": "sdi",
	"BS-Support": "bs-support",
	"BS-Dev": "bs-dev",
	"Business-Systems": "business-systems",
	"Digital-Innovation": "digital-innovation",
	"IT": "it",
	"Infrastructure": "infrastructure",
	"Praelexis": "praelexis",
	"Commercial": "commercial",
	"Networks": "networks",
	"Finance": "finance",
	"Customer-Support": "customer-support",
	"HR": "hr",
	"external": "external"
};
const counterpartyNames = Object.keys(counterpartyTags);
const counterparty = await tp.system.suggester(counterpartyNames, counterpartyNames, false, "Counterparty?");
const counterpartyTag = counterpartyTags[counterparty];

const title = await tp.system.prompt("Meeting name?", "");

tR = "> [!meeting]+ " + title + " #meeting/" + type + " #meeting/" + counterpartyTag + "\n" +
	"> **Time:** " + tp.date.now("HH:mm") + "\n" +
	"> **Attendees:**\n" +
	">\n" +
	"> **Notes:**\n" +
	"> -\n";
%>
