# solution

Eso es porque el constructor hijo debe llamar a `super()`.

Aquí el código corregido:

\`\`\`js run class Animal {

constructor\(name\) { this.name = name; }

}

class Rabbit extends Animal { constructor\(name\) {  
_!_ super\(name\); _/!_ this.created = Date.now\(\); } }

_!_ let rabbit = new Rabbit\("Conejo Blanco"\); // ahora funciona _/!_ alert\(rabbit.name\); // Conejo Blanco

\`\`\`

