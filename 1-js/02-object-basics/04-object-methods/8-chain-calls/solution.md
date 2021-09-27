# solution

La solución es devolver el objeto mismo desde cada llamado.

\`\`\`js run demo let ladder = { step: 0, up\(\) { this.step++; _!_ return this; _/!_ }, down\(\) { this.step--; _!_ return this; _/!_ }, showStep\(\) { alert\( this.step \); _!_ return this; _/!_ } };

ladder.up\(\).up\(\).down\(\).up\(\).down\(\).showStep\(\); // 1

```text
También podemos escribir una simple llamada por línea. Para cadenas largas es más legible:

```js
ladder
  .up()
  .up()
  .down()
  .up()
  .down()
  .showStep(); // 1
```

