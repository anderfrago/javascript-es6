# task

importance: 5

## Claves iterables

Nos gustaría obtener un array de `map.keys()` en una variable y luego aplicarle métodos específicos de array, ej. `.push`.

Pero eso no funciona:

\`\`\`js run let map = new Map\(\);

map.set\("name", "John"\);

let keys = map.keys\(\);

_!_ // Error: keys.push no es una función keys.push\("more"\); _/!_

\`\`\`

¿Por qué? ¿Cómo podemos arreglar el código para que funcione `keys.push`?

