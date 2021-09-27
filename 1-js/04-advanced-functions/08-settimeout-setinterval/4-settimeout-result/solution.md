# solution

Cualquier `setTimeout` se ejecutará solo después de que el código actual haya finalizado.

La `i` será la última:`100000000`.

\`\`\`js run let i = 0;

setTimeout\(\(\) =&gt; alert\(i\), 100\); // 100000000

// supongamos que el tiempo para ejecutar esta función es&gt; 100 ms for\(let j = 0; j &lt; 100000000; j++\) { i++; }

\`\`\`

