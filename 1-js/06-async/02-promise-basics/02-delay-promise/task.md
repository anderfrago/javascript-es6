# Demora con una promesa

La función incorporada `setTimeout` utiliza callbacks. Crea una alternativa basada en promesas.

La función `delay(ms)` debería devolver una promesa. Esa promesa debería resolverse después de `ms` milisegundos, para que podamos agregarle `.then`, así:

```javascript
function delay(ms) {
  // tu código
}

delay(3000).then(() => alert('se ejecuta después de 3 segundos'));
```

