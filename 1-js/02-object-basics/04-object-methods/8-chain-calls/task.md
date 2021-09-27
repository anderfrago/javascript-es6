# task

importance: 2

## Encadenamiento

Hay un objeto `ladder` que permite subir y bajar:

```javascript
let ladder = {
  step: 0,
  up() { 
    this.step++;
  },
  down() { 
    this.step--;
  },
  showStep: function() { // muestra el peldaño actual
    alert( this.step );
  }
};
```

Ahora, si necesitamos hacer varios llamados en secuencia podemos hacer algo como esto:

```javascript
ladder.up();
ladder.up();
ladder.down();
ladder.showStep(); // 1
```

Modifica el código de "arriba" `up`, "abajo" `down` y "mostrar peldaño" `showStep` para hacer los llamados encadenables como esto:

```javascript
ladder.up().up().down().showStep(); // 1
```

Tal enfoque es ampliamente usado entre las librerías JavaScript.

