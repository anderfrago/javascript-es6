# task

importance: 5

## Destructuring assignment

We have an object:

```javascript
let user = {
  name: "John",
  years: 30
};
```

Write the destructuring assignment that reads:

* `name` property into the variable `name`.
* `years` property into the variable `age`.
* `isAdmin` property into the variable `isAdmin` \(false, if no such property\)

Here's an example of the values after your assignment:

```javascript
let user = { name: "John", years: 30 };

// tu código al lado izquierdo:
// ... = user

alert( name ); // John
alert( age ); // 30
alert( isAdmin ); // false
```

