<%*
// Ceremony type — the FORMAT of the meeting, nothing about who's in it.
// Add new types here as needed.
const types = ["standup", "sprint-planning", "retro", "1-1", "workshop", "problem-solving", "review", "planning", "training", "steering", "general"];
const type = await tp.system.suggester(types, types, false, "Ceremony type?");

// Counterparty — WHO the meeting is with, nothing about format.
// BS-Support / BS-Dev / Business-Systems / Digital-Innovation / IT /
// Infrastructure map to real HR functions under Information Systems.
// Add new ones here as needed.
const counterparties = ["general", "D&A", "SDI", "BS-Support", "BS-Dev", "Business-Systems", "Digital-Innovation", "IT", "Infrastructure", "Praelexis", "Commercial", "Networks", "Finance", "Customer-Support", "HR", "external"];
const counterparty = await tp.system.suggester(counterparties, counterparties, false, "Counterparty?");

const title = await tp.system.prompt("Meeting name?", "");

tR = `> [!meeting]+ ${title} #meeting/${type} #meeting/${counterparty.toLowerCase().replace(/[&\s]+/g, "-")}
> **Time:** ${tp.date.now("HH:mm")}
> **Attendees:**
>
> **Notes:**
> -
`;
%>
