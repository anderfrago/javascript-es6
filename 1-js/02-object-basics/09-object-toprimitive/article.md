# Conversión de objeto a valor primitivo

¿Qué sucede cuando los objetos se suman `obj1 + obj2`, se restan `obj1 - obj2` o se imprimen utilizando `alert(obj)`?

JavaScript no permite exactamente personalizar cómo los operadores trabajan con los objetos. Al contrario de otros lenguajes de programación como Ruby o C++, no podemos implementer un método de objeto especial para manejar una suma \(u otros operadores\).

En ese caso, los objetos se convierten automáticamente en valores primitivos, y luego se lleva a cabo la operación sobre esos primitivos, y resultan en un valor primitivo.

Esto es una limitación importante, porque el resultado de `obj1 + obj2` ¡no puede ser otro objeto!

Por ejemplo no podemos hacer objetos que representen vectores o matrices \(o conquistas o lo que sea\), sumarlas y esperar un objeto "sumado" como resultado. Tal objetivo arquitectural cae automáticamente "fuera del tablero".

Como no podemos hacer mucho aquí, no se hace matemáticas con objetos en proyectos reales. Cuando ocurre, usualmente es por un error de código.

En este capítulo cubriremos cómo un objeto se convierte a primitivo y cómo podemos personalizarlo.

Tenemos dos propósitos:

1. Nos permitirá entender qué ocurre en caso de errores de código, cuando tal operación ocurre accidentalmente.
2. Hay excepciones, donde tales operaciones son posibles y se ven bien. Por ejemplo al restar o comparar fechas \(objetos `Date`\). Las discutiremos más adelante.

## Reglas de conversión

En el capítulo , hemos visto las reglas para las conversiones de valores primitivos numéricos, strings y booleanos. Pero dejamos un hueco en los objetos. Ahora, como sabemos sobre métodos y símbolos, es posible completarlo.

1. Todos los objetos son `true` en un contexto booleano. Solo hay conversiones numéricas y de strings.
2. La conversión numérica ocurre cuando restamos objetos o aplicamos funciones matemáticas. Por ejemplo, los objetos de tipo `Date` \(que se cubrirán en el capítulo \) se pueden restar, y el resultado de `date1 - date2` es la diferencia horaria entre dos fechas.
3. En cuanto a la conversión de strings : generalmente ocurre cuando imprimimos un objeto como en `alert(obj)` y en contextos similares.

Podemos ajustar la conversión de tipo string y numérica, utilizando métodos especiales del objeto.

Hay tres variantes de conversión de tipos que ocurren en varias situaciones.

Se denominan "hints", "sugerencias", que se describen en la [especificación](https://tc39.github.io/ecma262/#sec-toprimitive):

`"string"` : Para una conversión de objeto a string, cuando hacemos una operación que espera un string en un objeto, como `alert`:

```javascript
    // salida
    alert(obj);

    // utilizando un objeto como clave
    anotherObj[obj] = 123;
```

`"number"` : Para una conversión de objeto a número, como cuando hacemos operaciones matemáticas:

```javascript
    // conversión explícita
    let num = Number(obj);

    // matemáticas (excepto + binario)
    let n = +obj; // + unario
    let delta = date1 - date2;

    // comparación menor que / mayor que
    let greater = user1 > user2;
```

`"default"` : Ocurre en casos raros cuando el operador "no está seguro" de qué tipo esperar.

```text
Por ejemplo, el operador binario `+` puede funcionar con strings (los concatena) y números (los suma), por lo que tanto los strings como los números servirían. Entonces, si el + binario obtiene un objeto como argumento, utiliza la sugerencia `"default"` para convertirlo.

También, si un objeto es comparado utilizando `==` con un string, un número o un símbolo, tampoco está claro qué conversión se debe realizar, por lo que se utiliza la sugerencia `"default"`.

```js
// + binario utiliza la sugerencia "default"
let total = obj1 + obj2;

// obj == número utiliza la sugerencia "default"
if (user == 1) { ... };
```

Los operadores de comparación mayor que y menor que, como `<` `>`, también pueden funcionar con strings y números. Aún así, utilizan la sugerencia `"number"`, y no `"default"`. Eso es por razones históricas.

Sin embargo, en la práctica, no necesitamos recordar estos detalles peculiares, porque todos los objetos incorporados excepto un caso (el objeto `Date`, lo aprenderemos más adelante) implementan la conversión `"default"` de la misma manera que `"number"`. Y podemos hacer lo mismo.
```

`````smart header="No hay sugerencia```\"boolean\"\`" Tenga en cuenta : Solo hay tres sugerencias. Es así de simple.

No hay ninguna sugerencia "boolean" \(todos los objetos son `true` en el contexto booleano\) ni nada más. Y si tratamos `"default"` y `"number"` de la misma manera, como lo hacen la mayoría de las funciones incorporadas, entonces solo hay dos conversiones.

```text
**Para realizar la conversión, JavaScript intenta buscar y llamar a tres métodos del objeto:**

1. Llamar a `obj[Symbol.toPrimitive](hint)` : el método con la clave simbólica `Symbol.toPrimitive` (símbolo del sistema), si tal método existe,
2. En caso contrario, si la sugerencia es `"string"`
    - intentar `obj.toString()` y `obj.valueOf()`, lo que exista.
3. En caso contrario, si la sugerencia es `"number"` o `"default"`
    - intentar `obj.valueOf()` y `obj.toString()`, lo que exista.

## Symbol.toPrimitive

Empecemos por el primer método. Hay un símbolo incorporado llamado `Symbol.toPrimitive` que debe utilizarse para nombrar el método de conversión, así:

```js
obj[Symbol.toPrimitive] = function(hint) {
  // aquí va el código para convertir este objeto a un primitivo
  // debe devolver un valor primitivo
  // hint = "sugerencia", uno de: "string", "number", "default"
};
```

Si el método `Symbol.toPrimitive` existe, es usado para todos los hints y no serán necesarios más métodos.

Por ejemplo, aquí el objeto `user` lo implementa:

\`\`\`js run let user = { name: "John", money: 1000,

[Symbol.toPrimitive](https://github.com/anderfrago/javascript-es6/tree/a40cdf1844f1b053fe92cfe167a2b2a527b7ff38/1-js/02-object-basics/09-object-toprimitive/hint/README.md) { alert\(`sugerencia: ${hint}`\); return hint == "string" ? `{name: "${this.name}"}` : this.money; } };

// demostración de conversiones: alert\(user\); // sugerencia: string -&gt; {name: "John"} alert\(+user\); // sugerencia: number -&gt; 1000 alert\(user + 500\); // sugerencia: default -&gt; 1500

```text
Como podemos ver en el código, `user` se convierte en un string autodescriptivo o en una cantidad de dinero dependiendo de la conversión. Un único método `user[Symbol.toPrimitive]` maneja todos los casos de conversión.


## toString/valueOf

Si no existe `Symbol.toPrimitive` entonces JavaScript trata de encontrar los métodos `toString` y `valueOf`:

- Para una sugerencia "string": `toString`, y si no existe, entonces `valueOf` (así `toString` tiene prioridad en conversiones string.
- Para otras sugerencias: `valueOf`, y si no existe, entonces `toString` (así `valueOf` tiene prioridad para matemáticas).

Los métodos `toString` y `valueOf` provienen de la antigüedad. No son símbolos (los símbolos no existían en aquel tiempo), sino métodos "regulares" nombrados con strings. Proporcionan una forma alternativa "al viejo estilo" de implementar la conversión.

Estos métodos deben devolver un valor primitivo. Si `toString` o `valueOf` devuelve un objeto, entonces se ignora (lo mismo que si no hubiera un método).

De forma predeterminada, un objeto simple tiene los siguientes métodos `toString` y `valueOf`:

- El método `toString` devuelve un string `"[object Object]"`.
- El método `valueOf` devuelve el objeto en sí.

Aquí está la demostración:

```js run
let user = {name: "John"};

alert(user); // [object Object]
alert(user.valueOf() === user); // true
```

Por lo tanto, si intentamos utilizar un objeto como un string, como en un `alert` o algo así, entonces por defecto vemos `[object Object]`.

El `valueOf` predeterminado se menciona aquí solo en favor de la integridad, para evitar confusiones. Como puede ver, devuelve el objeto en sí, por lo que se ignora. No me pregunte por qué, es por razones históricas. Entonces podemos asumir que no existe.

Implementemos estos métodos para personalizar la conversión.

Por ejemplo, aquí `user` hace lo mismo que el ejemplo anterior utilizando una combinación de `toString` y `valueOf` en lugar de `Symbol.toPrimitive`:

\`\`\`js run let user = { name: "John", money: 1000,

// para sugerencia="string" toString\(\) { return `{name: "${this.name}"}`; },

// para sugerencia="number" o "default" valueOf\(\) { return this.money; }

};

alert\(user\); // toString -&gt; {name: "John"} alert\(+user\); // valueOf -&gt; 1000 alert\(user + 500\); // valueOf -&gt; 1500

```text
Como podemos ver, el comportamiento es el mismo que en el ejemplo anterior con `Symbol.toPrimitive`.

A menudo queremos un único lugar "general" para manejar todas las conversiones primitivas. En este caso, podemos implementar solo `toString`, así:

```js run
let user = {
  name: "John",

  toString() {
    return this.name;
  }
};

alert(user); // toString -> John
alert(user + 500); // toString -> John500
```

En ausencia de `Symbol.toPrimitive` y `valueOf`, `toString` manejará todas las conversiones primitivas.

### Una conversión puede devolver cualquier tipo primitivo

Lo importante que debe saber acerca de todos los métodos de conversión primitiva es que no necesariamente devuelven la primitiva "sugerida".

No hay control sobre si `toString` devuelve exactamente un string, o si el método `Symbol.toPrimitive` devuelve un número para una sugerencia `"number"`.

Lo único obligatorio: estos métodos deben devolver un valor primitivo, no un objeto.

`````smart header="Notas históricas" Por razones históricas, si```toString`o`valueOf\` devuelve un objeto, no hay ningún error, pero dicho valor se ignora \(como si el método no existiera\). Esto se debe a que en la antigüedad no existía un buen concepto de "error" en JavaScript.

Por el contrario, `Symbol.toPrimitive` _debe_ devolver un valor primitivo, en caso contrario habrá un error.

```text
## Más conversiones

Como ya sabemos, muchos operadores y funciones realizan conversiones de tipo, por ejemplo la multiplicación `*` convierte operandos en números.

Si pasamos un objeto como argumento, entonces hay dos etapas:
1. El objeto se convierte en un valor primitivo (utilizando las reglas descritas anteriormente).
2. Si el valor primitivo resultante no es del tipo correcto, se convierte.

Por ejemplo:

```js run
let obj = {
  // toString maneja todas las conversiones en ausencia de otros métodos
  toString() {
    return "2";
  }
};

alert(obj * 2); // 4, objeto convertido a valor primitivo "2", luego la multiplicación lo convirtió en un número
```

1. La multiplicación `obj * 2` primero convierte el objeto en valor primitivo \(que es un string `"2"`\).
2. Luego `"2" * 2` se convierte en `2 * 2` \(el string se convierte en número\).

El `+` binario concatenará los strings en la misma situación, ya que acepta con gusto un string:

\`\`\`js run let obj = { toString\(\) { return "2"; } };

alert\(obj + 2\); // 22 \("2" + 2\), la conversión a valor primitivo devolvió un string =&gt; concatenación

\`\`\`

## Resumen

La conversión de objeto a valor primitivo es llamada automáticamente por muchas funciones y operadores incorporados que esperan un valor primitivo.

Hay 3 tipos \(hints o sugerencias\) de estas:

* `"string"` \(para `alert` y otras operaciones que necesitan un string\)
* `"number"` \(para matemáticas\)
* `"default"` \(pocos operadores\)

La especificación describe explícitamente qué operador utiliza qué sugerencia. Hay muy pocos operadores que "no saben qué esperar" y utilizan la sugerencia `"default"`. Por lo general, para los objetos incorporados, la sugerencia `"default"` se maneja de la misma manera que `"number"`, por lo que en la práctica los dos últimos a menudo se combinan.

El algoritmo de conversión es:

1. Llamar a `obj[Symbol.toPrimitive](hint)` si el método existe,
2. En caso contrario, si la sugerencia es `"string"`
   * intentar `obj.toString()` y `obj.valueOf()`, lo que exista.
3. En caso contrario, si la sugerencia es `"number"` o `"default"`
   * intentar `obj.valueOf()` y `obj.toString()`, lo que exista.

En la práctica, a menudo es suficiente implementar solo `obj.toString()` como un método "general" para todas las conversiones que devuelven una representación "legible por humanos" de un objeto, con fines de registro o depuración.

Como en las operaciones matemáticas, JavaScript no brinda una forma de "sobrescribir" operadores usando métodos. Así que en proyectos de la vida real raramente se los usa en objetos.

