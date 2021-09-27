# solution

Es porque `i` nunca sería igual a `10`.

Ejecuta esto para ver los valores _reales_ de `i`:

\`\`\`js run let i = 0; while \(i &lt; 11\) { i += 0.2; if \(i &gt; 9.8 && i &lt; 10.2\) alert\( i \); }

\`\`\`

Ninguno de ellos es exactamente `10`.

Tales cosas suceden por las pérdidas de precisión cuando sumamos decimales como `0.2`.

Conclusión: evita chequeos de igualdad al trabajar con números decimales.

