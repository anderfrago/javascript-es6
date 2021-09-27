# solution

1. Utilice una función wrapper \(envoltura\), de tipo arrow \(flecha\) para ser conciso:

   ```javascript
    askPassword(() => user.login(true), () => user.login(false));
   ```

```text
Ahora obtiene `user` de variables externas y lo ejecuta de la manera normal.
```

1. O cree una función parcial desde `user.login` que use `user` como contexto y tenga el primer argumento correcto:

```javascript
    askPassword(user.login.bind(user, true), user.login.bind(user, false));
```

