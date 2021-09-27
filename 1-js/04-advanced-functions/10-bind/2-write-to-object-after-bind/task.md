# task

importance: 5

## Función enlazada como método

¿Cuál será el resultado?

```javascript
function f() {
  alert( this ); // ?
}

let user = {
  g: f.bind(null)
};

user.g();
```

