# ¿Volver a resolver una promesa?

¿Cuál es el resultado del código a continuación?

```javascript
let promise = new Promise(function(resolve, reject) {
  resolve(1);

  setTimeout(() => resolve(2), 1000);
});

promise.then(alert);
```

