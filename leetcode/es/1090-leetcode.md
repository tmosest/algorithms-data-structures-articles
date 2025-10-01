-...
Título: LeetCode 1090. Valores más grandes de etiquetas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
*Respuesta absoluta*

Puede portar la solución JavaScript a Java casi line‐by-line.
Las únicas cosas que necesitas cambiar son:

Silencio en la comunicación en Java por qué
Silencio...
Silencio `const` Silencio `final` (o ninguna palabra clave) Silencio Java no tiene `const`. Silencio
Silencio `deberemos vivir una declaración variable normal (`int`, `String ' , ...)
← `` función Silencio `() - título` en lambda, o un método normal
Silencioso `Array.prototype.sort` Silencioso `Collections.sort` o `Arrays.sort`
Silencio `map.hasKey()` ¦
Silencioso `map.getOrDefault(key, 0)` Silencio `map.getOrDefault(key, 0)` (same)
Silencioso `retorno`
Silencio

A continuación se muestra una aplicación Java **minimal e idiomática** que sigue la misma lógica que su solución JavaScript.

``java
importar java.util*;

*
* Valores más grandes de etiquetas
* (LeetCode 2291)
*
* La implementación Java refleja la lógica del JavaScript
* solución que publicó:
*
* 1. Construir una lista de pares (marca, valor).
* 2. Ordenar esa lista por valor (descendente).
* 3. Escoge cuidadosamente los artículos más valorados, respetando:
* – un límite global (numWanted)
* – un límite por etiqueta (useLimit)
*
* Todas las estructuras y operaciones de datos son Java estándar:
* Lista/ArrayList
* - Colecciones.sort con un Comparador
* - Mapa seleccionadoString,Integer título para contadores de etiquetas
*/
Solución de la clase pública {}

*
* Ayudante graciosa que elige los elementos principales para una sola etiqueta.
*
* valores @param ordenados en orden descendente
* Uso de @param Limite cuántas veces se puede usar una etiqueta
* @param num Número de artículos que todavía necesitamos elegir
* @return [sum of picked values, remaining numWanted]
*/
privado largo[] valores codiciosos(int[], uso intLimit, int numWanted) {
larga suma = 0;
int limit = Math.min(useLimit, numWanted);

para (int i = 0; i) {}
sum +=valores[i];
}

numWanted -= limit;
devolver nuevo largo[]{sum, numWanted};
}

grandes valores públicos, etiquetas String[],
int numWanted, int useLimit) {
int n = values.length;

// Construir una lista de pares (etiqueta, valor)
Lista de los pares de padres = nuevo ArrayList correctamente(n);
para (int i = 0; i)
pares.add(nuevo par(labels[i], valores[i]));
}

// Ordenar pares por valor descendente
pares.sort(a, b) - título Integer.compare(b.value, a.value));

// Cuenta cuántas veces se ha utilizado cada etiqueta
Mapa seleccionadoString, Integer inteligente utilizado = nuevo HashMap Quería();
total largo = 0;
int remaining = num Deseado;

para (Pair p : pares) {
si (se mantiene == 0) romper;

int usado Cnt = used.getOrDefault(p.label, 0);

si (utilizadoCnt < UsoLimit) { // todavía podemos utilizar esta etiqueta
total += p.value;
us.put(p.label, usedCnt + 1);
restante...
}
}

Total de retorno;
}

* Soporte de datos simple para un par de etiqueta/valor */
Clase privada estática
final etiqueta de cuerda;
valor int final;
Par(Etiqueta de fijación, valor int) {
esto. etiqueta = etiqueta;
esto. valor = valor;
}
}
}
`` `

### Cómo coincide con la versión JS

Silencio en la comunicación conjunta Java Silencioso
La vida... la vida...
Silencio `valores.map(v, i) = confianza [labels[i], v])` Silencio Construir `Lista seleccionadaPair confianza` Silencio Java no tiene ninguna matriz de-arrays; utilizar una clase pequeña. Silencio
Silencio `arr.sort(a,b)= usuario b[1] - a[1])` Silencio `pairs.sort(a,b) - título Integer.compare(b.value,a.value)] tención Comparador clasifica por el valor numérico. Silencio
TENIDO `const cnt = nuevo mapa();` TENIDO `Mapa realizadaString,Integer confianza used = new HashMap entendido();` ANTE Java `Map` replaces JavaScript `Map`.
Silencio `cnt.get(...)` / `cnt.set(...)` ¦ La misma idea. Silencio
Silencio `for (const [label, val] of arr)` Silencio `for (Pair p : pairs)` Iterate sobre la lista ordenada. Silencio
Silencio `cnt.has(label)` / `cnt.get(label) > UsoLimit` Silencio `usedCnt > UtilizarLimit` Silencio Mismo lógico. Silencio
Silencio `retorno total ' Silencio `retorno total ' Silencio El tipo de retorno es `long ' porque la suma puede exceder `int`.

### Performance

* **Tiempo**: `O(n log n)` debido a la clasificación; el escaneo codicioso es lineal.
* **Pace**: `O(n)` para la lista `Pair` y la `Map`.

Ambas versiones tienen el mismo comportamiento asintotico; la implementación de Java es más segura y más fácil de leer una vez que estés acostumbrado a la sintaxis de Java.