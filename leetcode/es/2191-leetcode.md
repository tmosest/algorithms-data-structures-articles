-...
Título: LeetCode 2191. Ordenar los números jumbled -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Lo que la solución hace – en palabras sencillas* *

1. **Entra cada número en su versión “mapped”. #
- Cada dígito del número original es reemplazado por el dígito que el array *mapping* nos dice que usemos.
- Ejemplo: si `mapping[3] = 8` y el número es `123`, el `3` se convierte en `8`.
- Después de que todos los dígitos sean reemplazados obtenemos un nuevo entero (por ejemplo, `148`).

2. **Mantenga el número original y recuerde su posición. #
- Por cada elemento en 'nums' almacenamos un tuple:
`(Nota original titularidad, .mapped number monedas, Identificador original ratio)`.
- El índice original se utiliza sólo para mantener el tipo **stable** (elementos con el mismo valor mapeado mantienen su orden relativo).

3. **Sorta por los números mapeados. #
- La lista de tuples se clasifica primero en el número *mapped* y, si dos números mapeados son iguales, en el índice *original*.
- Esto garantiza que dos números que mapean al mismo valor aparecen en el mismo orden que en la entrada.

4. *Construir la matriz final*
- Después de ordenar, leemos sólo los números originales de los tuples ordenados y devolvemos ese array.

-...

### ¿Por qué funciona esto?

- **Mapping es una bijeción en dígitos** – cada dígito 0-9 es reemplazado por otro dígito único, por lo que la asignación está bien definida para cualquier entero.
- **Estabilidad** – Añadiendo el índice original como clave secundaria conservamos el orden de los lazos.
En la mayoría de los idiomas ( " sur " en C++/Java, " surtido " en Python) el algoritmo de clasificación es estable, pero añadir el índice lo garantiza incluso si la implementación del lenguaje cambia.
- *La complejidad*
- Convertir un número de *d* dígitos cuesta O(d).
- Lo hacemos por todos los números *n*: O(n·d).
- Ordenar la lista de *n* tuples cuesta O(n log n).
Así que el tiempo global es O(n log n + n·d), y el espacio es O(n) para la lista de tuples.

-...

## Quick pseudo-code

``text
para cada uno en 0 .. nums.length-1
s = representación de cadena de nums[i]
mappedString = ""
para cada personaje c en s
mappedString += mapping[ int(c) ]
mappedVal = int(mappedString) // los ceros principales son descartados
añadir tuple (nums[i], mappedVal, i) a la lista

lista por (MappedVal, originalIndex)

Resultado = []
para cada tuple en lista clasificada
apéndice número original al resultado

Resultado de retorno
`` `

Eso es – el algoritmo es simplemente “transform → par con índice → estable tipo → salida originales”.