# solution

Este es el caso cuando saber cómo trabaja por dentro es útil.

Simplemente trata el llamado `async` como una promesa y añádele `.then`: \`\`\`js run async function wait\(\) { await new Promise\(resolve =&gt; setTimeout\(resolve, 1000\)\);

return 10; }

function f\(\) { // muestra 10 después de 1 segundo _!_ wait\(\).then\(result =&gt; alert\(result\)\); _/!_ }

f\(\);

\`\`\`

