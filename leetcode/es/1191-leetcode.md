-...
Título: LeetCode 1191. K-Concatenation Maximum Sum -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 K‐Concatenation Maximum Sum – Full Solution in **Java, Python & C+**
■ **LeetCode 1470** – *Suma Máximo de un Array After K Reversals* (realmente K‐concatenation)

-...

## TL;DR

Silencio Idioma Silencio Tiempo Complejidad Silencio Complejidad Espacial Silencio Final Code Silencio
Silencio--------------------------
Silencio **Java** TENIDO O(n) TENIDO O(1) ANTERIEDENTES Ver código Java seleccionado/summary título... Silencio
Silencio **Python** Silencio O(n) TENIDO O(1) TENIDO DEtalles recomendados Ver Código de Python realizado/summary título... Silencio
Silencio **C++** Silencio O(n) Silencio O(1) TENIDO DEtalles Ver C+++ Código seleccionado/summary título... Silencio

■ **Respuesta** – `maxSubarraySum(duplicadoArray)` cuando `k==1`.
■ Cuando la suma total de `arr` es negativa, la respuesta viene de las dos primeras concatenaciones.
■ Cuando la suma total es positiva, agregamos `(k-2) * suma(arr)` a ese valor.
■ Finalmente, aplicar `max(0, respuesta) % 1_000_000_007`.

-...

## Por qué esto importa

Para cualquier entrevista de codificación o desafío de programación competitiva, conseguir el algoritmo *right* que funciona en tiempo lineal mientras mantiene el código legible es el lugar dulce.
A continuación encontrará:

1. Una solución ** limpia y lista para cada idioma.
2. Una publicación **blog** que se sumerge en los aspectos *bueno*, *bad* y *muy* de las soluciones típicas.
3. Títulos, encabezados y uso de palabras clave para que el artículo se clasifica en motores de búsqueda para “k-concatenation suma máxima” y consultas relacionadas.

-...

## 1. El problema (LeetCode 1470)

■ **K‐Concatenation Maximum Sum**
■ Dada una matriz de enteros de 1-D `arr` y un entero `k`, forman una matriz concatenando `arr` a sí mismo `k` veces.
■ Devuelve la suma máxima de sub-array posible en esta nueva matriz.
■ La respuesta debe tomarse modulo 109 + 7. Si la suma máxima es negativa, devuelve `0`.

Las limitaciones son grandes (resistentes ≤ 105, k ≤ 105) – necesitamos un algoritmo O(n), no O(k·n).

-...

## 2. The Core Idea (Good)

- **El algoritmo de Kadane** da la suma máxima de sub-array de cualquier matriz en O(n).
- Cuando concatenamos dos copias de `arr` (`k==2`), el sub-array máximo puede cruzar el límite; necesitamos a Kadane en un array de longitud-`2·n`.
- Let `total = sum(arr)`.
* Si `total ≤ 0`, la mejor suma no se puede mejorar añadiendo más copias, por lo que la respuesta es sólo el Kadane en las dos primeras copias.
* Si `total ≤ 0`, la mejor suma utiliza una parte que comienza en la copia *primera* y termina en la copia *última*. Todas las copias en el medio contribuyen al total total `total` cada una.
Por lo tanto, por " k confía2 " y " total confianza0 " :

``text
respuesta = Kadane(arr duplicado) + (k-2) * total
`` `

- Por último, tome `max(0, respuesta) % MOD`.

Esta es la solución **canónica O(n)** que funciona en espacio extra constante.

-...

## 3. Código completo

### 3.1 Java

``java
importar java.util*;

Clase Solución {
static final long MOD = 1_000_000_007L;

int kConcatenationMaxSum(int[] arr, int k) {
int n = arr.length;
total largo = 0;
total += v;

// Kadane para una sola copia
long bestSingle = kadane(arr);

(k == 1) retorno (int)Math.max(bestSingle, 0);

// Kadane en dos copias (tamaño 2*n)
mucho mejor Dos = kadaneDos Copies (arr);

si (total) 0) {
(int)Math.max(best Dos, 0) % (int)MOD;
}

ans largas = mejor Dos + (k - 2) * total;
as %= MOD;
(int)Math.max(ans, 0);
}

// estándar Kadane, trabaja en cualquier longitud de la matriz
kadane (int[] a) {
cur = a[0], mejor = a[0];
para (int i = 1; i)
cur = Math.max(a[i], cur + a[i]);
mejor = Math.max(mejor, cur);
}
devolver mejor;
}

// Kadane on arrr concatenated twice (length 2*n)
kadane privado TwoCopies(int[] arr) {
int n = arr.length;
long cur = arr[0], best = arr[0];
para (int i = 1; i)
int val = arr[i % n];
cur = Math.max(val, cur + val);
mejor = Math.max(mejor, cur);
}
devolver mejor;
}
}
`` `

-...

#### 3.2 Python

``python
MOD = 1_000_000_007

Solución de clase:
def kConcatenation MaxSum(self, arr, k: int) - int:
n = len(arr)
total = suma (arri)

def kadane(a):
cur = mejor = a[0]
para x en a[1:]:
cur = max(x, cur + x)
mejor = max(best, cur)
mejor

si k == 1:
as = kadane(arr)
volver max(ans, 0) % MOD

Kadane sobre dos copias
doble = arrr
best_two = kadane(double)

si total 0 0
volver max(best_two, 0) % MOD

as = (best_two + (k - 2) * total) % MOD
volver max(ans, 0)
`` `

-...

### 3.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
static constexpr long MOD = 1'000'007LL;

int kConcatenationMaxSum(vector identificadoint tendrían una relación, int k) {
int n = arr.size();
long long total = 0;
total += v;

si (k == 1) retorno estática_cast fielint(max(0LL, kadane(arr)))) % MOD;

largo tiempo mejor Dos = kadaneDos Copies (arr);
si (total LL= 0) devolver static_cast(max(0LL, bestTwo)) % MOD;

ans largos = (mejores + (k - 2) * total) % MOD;
volver estática_cast seleccionado(max(0LL, ans));
}

privado:
largo largo largo kadane(cont vector identificadoint estrecho a) {
largo largo cur = a[0], mejor = a[0];
para (size_t i = 1; i) ++i) {
r = max(long long)a[i], cur + a[i]);
mejor = max(best, cur);
}
devolver mejor;
}

largo largo largo kadane TwoCopies(cont vector identificadoint círculo arr) {
vector: dobleArr(arr)
doubleArr.insert(doubleArr.end(), arr.begin(), arrr.end());
kadane (doubleArr);
}
};
`` `

-...

## 4. The Blog Post

■ **Título**: *K‐Concatenation Maximum Sum – A Deep Dive into Good, Bad, and Ugly Solutions*
■ **Meta Descripción**: “Aprenda a resolver LeetCode 1470 en Java, Python y C++. Entender el algoritmo de Kadane, manejar el k grande, y evitar errores comunes. ¡Lee el guía completo ahora! ”

#### 4.1 Introducción

Cuando te sientas para resolver **LeetCode 1470 – K‐Concatenation Maximum Sum**, una ola de errores comunes a menudo se lava sobre su cabeza:

- "Concatenate copias y ejecuten Kadane. ”
- “Utilice programación dinámica sobre los estados “k”. ”
- “No olvides el modulo 1 000 000 007. ”

Cada uno de estos enfoques puede llevar a *TLE*, *MLE*, o incluso a errores sutiles de flujo entero. En este artículo, vamos a diseccionar las formas *buena*, *bad* y *muy* para abordar el problema, proporcionar código de copiado listo para tres idiomas populares, y mostrarle por qué la solución de tiempo lineal gana cada vez.

-...

### 4.2 Lo que el problema realmente pide

■ **K‐Concatenation** – crear un nuevo array por appending `arr` a itself `k` times.
■ ** Objetivo** – la suma máxima de un sub-array contiguo en esa nueva matriz, modulo `109 + 7`.
■ **Edge case** – si la suma máxima es negativa, devuelve `0`.

Las limitaciones son enormes (larga hasta 105, k hasta 105). Una solución ingenua O(k · n) nunca pasará.

-...

### 4.3 Good: The Optimal Kadane‐Based Strategy

Silencio ¿Por qué funciona?
...------------------------------
Silencio **Kadane en una sola copia** Silencio Da el mejor sub-array que permanece dentro de una copia. TEN Classic linear‐time max‐sub-array. Silencio
Silencio **Kadane en dos copias** Silencio Captura el mejor sub-array que *cruza* el límite entre dos copias. El único lugar que un sub-array puede abarcar más de una copia está en el cruce. Silencio
Silencio **Utilice la suma total** Silencio Si `sum(arr) ≤ 0`, cada copia intermedia aporta su suma completa a cualquier sub-array transfronterizo. Silencio Todas las copias interiores agregan `total` cada una; las dos copias restantes manejan la parte de cruce. Silencio
Silencio **Formula** Silencioso Dos + (k-2) * total " (cuando `k título2 ' y `total confianza0 ' ). Silencio Linear, espacio constante. Silencio
Silencio **Modulo " final clip** tención `max(0, respuesta) % MOD`. ← Maneja respuestas negativas y mantiene el resultado en límites. Silencio

*La clave se da cuenta de que después de las dos primeras copias, nunca necesitamos materializar todo el array de 'k`‐length. *

-...

### 4.4 Malo: La aproximación “Vamos a Duplicar”

Una solución tentadora pero *bad* es:

``python
doble_arr = arrr
full_arr = arr * k # O(k·n) memoria!
ans = max_subarray(full_arr)
`` `

Problemas:

1. ** Explosión de memoria** – `k` puede ser 105, por lo que `arr * k` puede ser elementos de 1010.
2. **Soplar el tiempo** – Kadane correría O(k·n).
3. **Overflow** – Las ints de Python están bien, pero C++/Java puede rebosar ints de 32 bits antes del modulo.

Debido a estas razones, este enfoque falla las pruebas de “Límite de Tiempo Excedido” o “Límite de Memoria Excedido”.

-...

### 4.5 Ugly: Mixing Prefix/Surfix Sums with Kadane, Wrong Modulo, Negative Handling

El patrón **ugly** parece:

``java
ans largos = kadaneTwoCopies(arr) + (k-2) * total;
as = un porcentaje de MOD; / / / / incorrecta! Debe hacer modulo *después* clipping negativo
int result = (int)Math.max(0, ans);
`` `

¿Por qué esto es feo?

- ** Orden Modulo** - La declaración de LeetCode exige que apliques `max(0, respuesta)`. *antes* modulo. Modding a negative number keep the negative sign, which violates the “return 0 if negative” rule.
- **Overflow** – `total` puede ser tan grande como `105 * 109` → necesita enteros de 64 bits.
- **Readability** – Mixing 3 diferentes variantes de “Kadane” en el mismo archivo hace que la lógica sea difícil de auditar.

-...

### 4.6 Consejos para la producción

Silencioso ¿Por qué?
Silencio...
Silencio Use **long / 64‐bit** para sumas intermedias. tención Previene el desbordamiento antes de aplicar el modulo. Silencio
Silencio **Reuse Kadane** – escriba un único ayudante que pueda aceptar cualquier matriz. tención mantiene el código DRY y fácil de probar. Silencio
Silencio **Modulo sólo una vez** – después de todo el cálculo. Silencio Evita llamadas innecesarias que pierden tiempo. Silencio
Silencio **Clamp a cero temprano** – `max(0, respuesta)` antes del modulo final. tención simplifica la lógica para casos negativos. Silencio
← Escribir comentarios claros que explican “cross-boundary” vs “full‐sum middle copies”. tención Future-prueba el código y hace que las revisiones de par más rápido. Silencio

-...

## 5. Por qué este artículo le ayuda a Rank

- ** Densidad de la palabra clave**: “K‐concatenation maximum sum”, “Kadane algoritmo”, “LeetCode 1470 solution”, “Java Kadane”, “Python Kadane”, “C++ LeetCode solution”.
Encabezamientos (H2, H3)** para los rastreadores de SEO.
- **Meta tags** con una descripción concisa y un título rico en palabras clave.
- **Code snippets** envuelto en `` etiquetas para satisfacer tanto humanos como bots.

Con estas optimizaciones, el artículo aparecerá cerca de la parte superior de los resultados de búsqueda de Google para cualquier candidato que busque una solución limpia LeetCode o consejos de preparación de entrevistas.

-...

## 5. Resumen

1. La manera **optimal** de resolver K‐Concatenation Maximum Sum es un solo paso Kadane más un manejo cuidadoso de las copias intermedias cuando la suma total es positiva.
2. Las tres implementaciones de idiomas anteriores se ejecutan en **O(n)** tiempo y **O(1)** espacio extra.
3. Evite las trampas **ugly**: nunca materialice todas las copias 'k', siempre maneje el modulo después de cortar respuestas negativas, y utilice enteros de 64 bits para mantener las sumas seguras.

¡Feliz codificación, y que sus sumas de sub-array siempre permanezcan en el lado alto! ▪