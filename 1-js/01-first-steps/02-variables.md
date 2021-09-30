# 02-variables

La mayoría del tiempo, una aplicación de JavaScript necesita trabajar con información. Aquí hay 2 ejemplos: 

1. Una tienda en línea -- La información puede incluir los bienes a la venta y un "carrito de compras". 

2. Una aplicación de chat -- La información puede incluir los usuarios, mensajes, y mucho más.

Utilizamos las variables para almacenar esta información.

## Una variable

Una \[variable\]\([https://es.wikipedia.org/wiki/Variable\_\(programaci%C3%B3n](https://es.wikipedia.org/wiki/Variable_%28programaci%C3%B3n)\)\) es un "almacén con un nombre" para guardar datos. Podemos usar variables para almacenar golosinas, visitantes, y otros datos.

Para generar una variable en JavaScript, se usa la palabra clave `let`.

La siguiente declaración genera \(en otras palabras: _declara_ o _define_\) una variable con el nombre "message":

```javascript
let message;
```

Ahora podemos introducir datos en ella al utilizar el operador de asignación `=`:

```javascript
let message;

*!*
message = 'Hola'; // almacenar la cadena 'Hola' en la variable llamada message
*/!*
```

La cadena ahora está almacenada en el área de la memoria asociada con la variable. La podemos acceder utilizando el nombre de la variable:

```javascript
let message;
message = 'Hola!';
alert(message); // muestra el contenido de la variable 
```

Para ser concisos, podemos combinar la declaración de la variable y su asignación en una sola línea:

```text
let message = 'Hola!'; // define la variable y asigna un valor

alert(message); // Hola!
```

También podemos declarar variables múltiples en una sola línea:

```javascript
let user = 'John', age = 25, message = 'Hola';
```

Esto puede parecer más corto, pero no lo recomendamos. Por el bien de la legibilidad, por favor utiliza una línea por variable.

La versión de líneas múltiples es un poco más larga, pero se lee más fácil:

```text
let user = 'John';
let age = 25;
let message = 'Hola';
```

Algunas personas también definen variables múltiples en estilo multilínea:

```javascript
let user = 'John', age = 25, message = 'Hola';
```

...Incluso en este estilo "coma primero":

```text
let user = 'John'
  , age = 25
  , message = 'Hola';
```

Técnicamente, todas estas variantes hacen lo mismo. Así que, es cuestión de gusto personal y preferencia estética.

En scripts más viejos, a veces se encuentra otra palabra clave:varen lugar delet\`:

```javascript
var mensaje = 'Hola';
```

La palabra clave `var` es _casi_ lo mismo que `let`. También hace la declaración de una variable, aunque de un modo ligeramente distinto, y más antiguo.

Existen sutiles diferencias entre `let` y `var`, pero no nos interesan en este momento. Cubriremos el tema a detalle en el capítulo .

{% hint style="info" %}
Una analogía de la vida real

Podemos comprender fácilmente el concepto de una "variable" si nos la imaginamos como una "caja" con una etiqueta de nombre único pegada en ella.

Por ejemplo, podemos imaginar la variable \`message\` como una caja etiquetada \`"message"\` con el valor \`"Hola!"\` adentro:

!\[\]\(variable.svg\)

Podemos introducir cualquier valor a la caja.

También la podemos cambiar cuantas veces queramos:
{% endhint %}

```javascript
let message;
message = 'Hola!';
message = 'Mundo!'; // valor alterado
alert(message);
```

{% hint style="info" %}
Cuando el valor ha sido alterado, los datos antiguos serán removidos de la variable:

!\[\]\(variable-change.svg\)

También podemos declarar dos variables y copiar datos de una a la otra.
{% endhint %}

```javascript
let hello = 'Hola mundo!';
let message;
*!*
// copia 'Hola mundo' de hello a message
message = hello;
*/!*
// Ahora, ambas variables contienen los mismos datos
alert(hello); // Hola mundo!
alert(message); // Hola mundo!
```

## Resumen

Podemos declarar variables para almacenar datos al utilizar las palabra clave `var`, `let`, o `const`.

* `let` -- es la forma moderna de declaración de una variable.
* `var` -- es la declaración de variable de vieja escuela. Normalmente no lo utilizamos en absoluto. Cubriremos sus sutiles diferencias con `let` en el capítulo , por si lo necesitaras.
* `const` -- es como `let`, pero el valor de la variable no puede ser alterado.

Las variables deben ser nombradas de tal manera que entendamos fácilmente lo que está en su interior.

