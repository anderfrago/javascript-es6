# solution

El error se produce porque `ask` obtiene las funciones `loginOk/loginFail` sin el objeto.

Cuando los llama, asumen naturalmente `this = undefined`.

Vamos a usar `bind` para enlazar el contexto:

\`\`\`js run function askPassword\(ok, fail\) { let password = prompt\("Password?", ''\); if \(password == "rockstar"\) ok\(\); else fail\(\); }

let user = { name: 'John',

loginOk\(\) { alert\(`${this.name} logged in`\); },

loginFail\(\) { alert\(`${this.name} failed to log in`\); },

};

_!_ askPassword\(user.loginOk.bind\(user\), user.loginFail.bind\(user\)\); _/!_

```text
Ahora funciona.

Una solución alternativa podría ser:
```js
//...
askPassword(() => user.loginOk(), () => user.loginFail());
```

Por lo general, eso también funciona y se ve bien.

Aunque es un poco menos confiable en situaciones más complejas donde la variable `user` podría cambiar _después_ de que se llama a `askPassword`, _antes_ de que el visitante responde y llame a `() => user.loginOk ()`.

It's a bit less reliable though in more complex situations where `user` variable might change _after_ `askPassword` is called, but _before_ the visitor answers and calls `() => user.loginOk()`.

