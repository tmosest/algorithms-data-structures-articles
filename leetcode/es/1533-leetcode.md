-...
Título: LeetCode 1533. Encontrar el índice del entero grande -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 1533 – Encontrar el índice del entero grande
**LeetCode** tóxico **Medio**

■ *Problema*
■ Se le da un array entero `arr` en el que *todos los elementos* son iguales ** excepto** un elemento que es estrictamente mayor.
■ El array es **no** expuesto directamente; sólo se puede llamar
" texto
Ø lector.compareSub(l, r, x, y) // compara sumas de arrr[l.r] y arrr[x..y]
√ lector.length() // devuelve el tamaño de la matriz
" `
■ Cada llamada a `compareSub` es O(1) y sólo puede hacer **20 llamadas**.
■ Devuelve el índice del elemento más grande.

-...

## Why This Problem Rocks (and Why It's a Good Interview Question)

Silencio . . . . . .
Silencio...
*Low-overhead* – 20 llamadas es un límite difícil pero realista que obliga a un **log‐ Solución N**. TEN *Real‐world vibe* – simula acceder a datos a través de una API remota, un escenario que muchos ingenieros enfrentan. Silencio
Silencio *Retorno de búsqueda binaria clásica* – usted necesita decidir si incluir el elemento medio o no. *Flexibilidad* – se puede resolver en Java, Python, C++, etc. Silencio
tención *Clear limitaciones* – todos los números son iguales excepto uno, por lo que puede confiar en la comparación de sumas. *Prueba su comprensión de los bichos fuera por uno* – la trampa “odd vs. incluso longitud” es el lugar dulce. Silencio

-...

## La intuición

Si dividimos el array en dos mitades y comparamos sus sumas:

* Si las sumas son iguales → el elemento especial está exactamente en el índice medio.
* Si la suma izquierda es mayor → el elemento especial debe estar en la mitad izquierda.
* Si la suma correcta es más grande → debe mentir en la mitad correcta.

La única sutileza: **Ya sea para incluir el elemento medio en la mitad izquierda o derecha**.
Debido a que todos los demás elementos son idénticos, el elemento en el centro es el único que puede inclinar la escala cuando las longitudes de subarray son * incluso*.

-...

## Algorithm (Binary Search with Odd/Even Handling)

`` `
l = 0
r = lector.length() – 1

mientras que l
m = (l + r) // 2 // índice medio

// Cuando la longitud del segmento (r - l + 1) es extraña,
// el elemento medio pertenece al lado izquierdo
// para fines de comparación.
(r - l + 1) % 2 == 1:
// Compare [l.m] con [m+1..r]
res = lector.compareSub(l, m, m + 1, r)
más:
// Compare [l.m] con [m.r]
res = lector.compareSub(l, m, m, r)

si res == 0:
retorno m // encontrado el índice especial
elif res == 1: // lado izquierdo es más pesado
r = m
// lado derecho es más pesado
l = m + 1

retorno l // l == r es la respuesta
`` `

* **La complejidad del tiempo**: `O(log n)` – a la mayoría de 20 llamadas por `n ≤ 5·105`.
* **La complejidad del espacio**: `O(1)` – sólo un puñado de variables.

-...

## Code Implementations

■ *Todas las soluciones asumen la existencia de la interfaz `ArrayReader` definida por LeetCode. *

#### ## 1down⃣ Java

``java
Solución de la clase pública {}
public int getIndex (lector de lector de radio) {
int l = 0;
int r = lector.length() - 1;

mientras que (l
int m = l + (r - l) / 2;

int res;
// (r - l + 1) es la longitud del segmento actual
(r - l + 1) % 2 == 1) {
res = lector.compareSub(l, m, m + 1, r);
. ♫ ... {
res = lector.compareSub(l, m, m, r);
}

(res == 0) {
retorno m;
} si (res == 1) {
r = m; // elemento especial en la izquierda
. ♫ ... {
l = m + 1; // elemento especial en la derecha
}
}
retorno l; // l == r
}
}
`` `

Python (3.x)

``python
Solución de clase:
def getIndex(self, read: 'ArrayReader') int:
l, r = 0, read.length() - 1

mientras que l
m = (l + r) // 2

(r - l + 1) % 2 == 1:
# odd length - # lado izquierdo incluye mediados
res = lector.compareSub(l, m, m + 1, r)
más:
# incluso longitud - título lado derecho incluye el medio
res = lector.compareSub(l, m, m, r)

si res == 0:
regreso m
elif res == 1:
r = m
más:
l = m + 1

Regreso
`` `

### 3down⃣ C++ (GNU+17)

``cpp
Clase Solución {
public:
int getIndex(ArrayReader &reader) {
int l = 0, r = lector.length() - 1;

mientras que (l
int m = l + (r - l) / 2;

int res;
(r - l + 1) % 2 == 1) { // segmento impar
res = lector.compareSub(l, m, m + 1, r);
} más { // incluso segmento
res = lector.compareSub(l, m, m, r);
}

(res == 0) retorno m;
si (res == 1) r = m;
l = m + 1;
}
retorno l;
}
};
`` `

-...

## El “bueno, malo y feo”

TENIDO ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTE
Silencio------------------------
TEN **O(log n)** solución cumple el límite de 20 casillas. Silencio El fracaso para manejar la diferencia entre impares/incluso conduce a un error **off-by-one**. Silencio **Brute‐force** comparación de cada par superaría el límite de llamada y el presupuesto de tiempo. Silencio
Silencio Código claro y corto que pasa fácilmente las pruebas. TEN Algunos concursantes escriben una solución recursiva que filtra las llamadas apiladas o mal contados. Escribir una moca personalizada de `ArrayReader` para las pruebas locales puede ser engorroso pero es esencial para la depuración offline. Silencio

-...

## Variaciones " Extensiones

1. **Dos números más grandes** – Una segunda búsqueda binaria en el segmento restante después de encontrar el primer gran número localizará el segundo.
2. **Un gran número y un pequeño número** – Dividir el array en tres partes y comparar dos mitades; la diferencia le dice si el elemento especial es grande o pequeño.
3. **No API, matriz cruda** – La misma lógica se reduce a una búsqueda binaria clásica donde se comparan los valores de elementos directamente.

-...

## Take‐away for Your Job Hunt

* **Showcase binaria search mastery** – Los entrevistadores les encanta ver una solución O(log n) limpia a un problema de API aparentemente complejo.
* **Explicar su proceso de pensamiento** – Mencionar la diferencia o incluso; hablar de cómo usted maneja la naturaleza abstracta de la API.
* **Highlight constraints** – Emphasize how your solution stays within the 20‐call limit.
* ** Pruebabilidad de la mención* Comparta cómo se burlan de `ArrayReader` para las pruebas de unidad – un consejo práctico para las entrevistas de codificación.

-...

## SEO‐Friendly Blog Title

■ **“LeetCode 1533 – Encuentra el índice del gran número de números enteros: una clase maestra de búsqueda binaria (Java/Python/C++)”**

**Meta Descripción:**
Aprende la solución O(log n) a LeetCode 1533. Entender el truco de división impar/incluso, leer Java completo, Python y C++ código, y obtener entrevistas con esta guía de algoritmo.

-...

Codificación feliz – y que su próxima entrevista sea tan suave como esta búsqueda binaria!