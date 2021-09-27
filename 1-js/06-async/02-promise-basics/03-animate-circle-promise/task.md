# Círculo animado con promesa

Vuelva a escribir la función `showCircle` en la solución de la tarea &lt;info:task/animate-circle-callback&gt; para que devuelva una promesa en lugar de aceptar un callback.

Nueva forma de uso:

```javascript
showCircle(150, 150, 100).then(div => {
  div.classList.add('message-ball');
  div.append("Hola, mundo!");
});
```

Tome la solución de la tarea &lt;info:task/animate-circle-callback&gt; como base.

