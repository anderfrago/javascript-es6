# task

importance: 5

## Error al crear una instancia

Aquí está el código de la clase `Rabbit` que extiende a `Animal`.

Desafortunadamente, los objetos `Rabbit` no se pueden crear. ¿Que pasa? Arréglalo. \`\`\`js run class Animal {

constructor\(name\) { this.name = name; }

}

class Rabbit extends Animal { constructor\(name\) {  
this.name = name; this.created = Date.now\(\); } }

_!_ let rabbit = new Rabbit\("Conejo Blanco"\); // Error: this no está definido _/!_ alert\(rabbit.name\);

\`\`\`

