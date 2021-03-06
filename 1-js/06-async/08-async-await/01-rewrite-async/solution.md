# solution

Las notas están bajo el código:

\`\`\`js run async function loadJson\(url\) { // \(1\) let response = await fetch\(url\); // \(2\)

if \(response.status == 200\) { let json = await response.json\(\); // \(3\) return json; }

throw new Error\(response.status\); }

loadJson\('no-such-user.json'\) .catch\(alert\); // Error: 404 \(4\)

```text
Notas:

1. La función `loadJson` se vuelve `async`.
2. Todo lo que está dentro de `.then` es reemplazado por `await`.
3. Podemos devolver `return response.json()` en lugar de esperar por él, como esto:

    ```js
    if (response.status == 200) {
      return response.json(); // (3)
    }
```

```text
Entonces el código externo tendría que esperar que la promesa se resuelva. En nuestro caso eso no importa.
```

1. El error arrojado por `loadJson` es manejado por `.catch`. No podemos usar `await loadJson(…)` allí, porque no estamos en una función `async`.

