# solution

\`\`\`js run demo function filterRange\(arr, a, b\) { // agregamos paréntesis en torno a la expresión para mayor legibilidad return arr.filter\(item =&gt; \(a &lt;= item && item &lt;= b\)\); }

let arr = \[5, 3, 8, 1\];

let filtered = filterRange\(arr, 1, 4\);

alert\( filtered \); // 3,1 \(valores dentro del rango\)

alert\( arr \); // 5,3,8,1 \(array original no modificado\)

\`\`\`

