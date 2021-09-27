# solution

\`\`\`js run let room = { number: 23 };

let meetup = { title: "Conference", occupiedBy: \[{name: "John"}, {name: "Alice"}\], place: room };

room.occupiedBy = meetup; meetup.self = meetup;

alert\( JSON.stringify\(meetup, function replacer\(key, value\) { return \(key != "" && value == meetup\) ? undefined : value; }\)\);

/ _{ "title":"Conference", "occupiedBy":\[{"name":"John"},{"name":"Alice"}\], "place":{"number":23} }_ /

\`\`\`

Aquí también necesitamos verificar `propiedad==""` para excluir el primer llamado donde es normal que `valor` sea `meetup`.

