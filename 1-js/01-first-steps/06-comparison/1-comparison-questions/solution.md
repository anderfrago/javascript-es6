# solution

\`\`\`js no-beautify 5 &gt; 4 → true "apple" &gt; "pineapple" → false "2" &gt; "12" → true undefined == null → true undefined === null → false null == "\n0\n" → false null === +"\n0\n" → false

\`\`\`

Algunas de las razones:

1. Obviamente, true.
2. Comparación lexicográfica, por lo tanto false. `"a"` es menor que `"p"`.
3. Una vez más, la comparación lexicográfica, el primer carácter de `"2"` es mayor que el primer carácter de `"1"`.
4. Los valores `null` y `undefined` son iguales entre sí solamente.
5. La igualdad estricta es estricta. Diferentes tipos de ambos lados conducen a false.
6. Similar a \(4\), `null` solamente es igual a `undefined`.
7. Igualdad estricta de diferentes tipos.

