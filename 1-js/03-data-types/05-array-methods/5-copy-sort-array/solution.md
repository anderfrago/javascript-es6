# solution

Podemos usar `slice()` para crear una copia y realizar el ordenamiento en ella:

\`\`\`js run function copySorted\(arr\) { return arr.slice\(\).sort\(\); }

let arr = \["HTML", "JavaScript", "CSS"\];

_!_ let sorted = copySorted\(arr\); _/!_

alert\( sorted \); alert\( arr \);

\`\`\`

