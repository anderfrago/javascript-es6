# solution

El resultado es `4`:

\`\`\`js run let fruits = \["Apples", "Pear", "Orange"\];

let shoppingCart = fruits;

shoppingCart.push\("Banana"\);

_!_ alert\( fruits.length \); // 4 _/!_

\`\`\`

Esto es porque los arrays son objetos. Entonces ambos, `shoppingCart` y `fruits` son referencias al mismo array.

