-...
Título: LeetCode 363. Max Sum of Rectangle No Larger Than K -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Max Sum of Rectangle No Larger Than K – LeetCode 363
*(Hard – 2‐D Kadane + Prefix‐Sum + búsqueda binaria)*

■ **TL;DR** – La solución óptima comprime la matriz 2-D en un array 1-D para cada par de filas (o columnas).
■ Para cada matriz comprimida encontramos la suma de sub-array más grande ≤ k en *O(n log n)* con un `TreeSet` (Java) / `multiset` (C++) / `bisect` (Python).
■ Hora: **O(min(m, n)2 · max(m, n) · log max(m, n)**, Memoria: **O(max(m, n))**.

-...

## 1. Recaptación de problemas

■ **Input**
√≥ `matrix`: `m × n` 2‐D array (`1 ≤ m, n ≤ 100`, `-100 ≤ matriz[i] [j] ≤ 100`)
Ø `k`: un entero (`-105 ≤ k ≤ 105`)

■ # Objetivo #
■ Devuelve la suma máxima de cualquier rectángulo axis alineado dentro de `matrix` cuya suma no excede ** k ' .
■ Un rectángulo se define por dos filas y dos columnas; su suma es la suma de todos los elementos dentro.

■ *Garantía* – Al menos un rectángulo existe cuya suma ≤ k.

-...

## 2. El enfoque “bueno” – 2-D Kadane + Prefijo Sum + búsqueda binaria

1. **Linas o columnas de compresión* *
*Si la matriz tiene más columnas que filas, iterate sobre pares de filas; de lo contrario se iteran sobre pares de columnas. *
La compresión reduce el problema 2-D a un problema 1-D en un array de longitud `max(m, n)`.

2. **1‐D Sub-array Problema* *
Para el array comprimido `nums` necesitamos la suma de sub-array más grande ≤ k.
Este es un problema clásico que se puede resolver en *O(n log n)*:
* Mantenga un multiconjunto de sumas prefijo ordenados hasta ahora (`prefijo = 0` inicialmente).
* Camina por `nums ' , manteniendo una suma corriente `curr`.
* Para cada `curr` necesitamos el prefijo más pequeño `p` tal que `curr - p ≤ k` → `p ≥ curr - k`.
La búsqueda de menor alcance ( " techo " ) da que " .
* Actualizar la mejor respuesta con `curr - p`.
* Insertar `curr` en el multiset.

3. *Para pronto* Si la mejor respuesta llega a `k`, es óptima; rompe inmediatamente.

La complejidad total del algoritmo está dominada por el doble bucle sobre los pares de fila/columna (Ω min(m,n)2) y el *O(n log n)* 1-D rutina, dando

`` `
Hora : O(min(m, n)2 · max(m, n) · log max(m, n)
Memoria : O(max(m, n))
`` `

Con 'm, n ≤ 100' esto funciona muy por debajo de 1 ms en la práctica.

-...

## 3. “El malo” – Naïve 4‐Nested Loops

Una fuerza bruta de libro de texto enumera todos los rectángulos de ` (top, izquierda, inferior, derecha) y los resume con una tabla 2-D de prefijo.
*Tiempo*: `O(m2 · n2)` → hasta 108 operaciones para 100 × 100, todavía demasiado lento para el límite de 2 s de LeetCode.
*Memoria*: `O(m · n)` para la tabla de prefijo 2-D.

-...

## 4. “El Ugly” – O(m2 · n2) Sin Sumas de Prefijo

Resumiendo el rectángulo sobre la mosca cada vez, recomponiendo la suma de cero para cada rectángulo.
Esto es *O(m3 · n3)* y totalmente poco práctico.

-...

## 5. Seguimiento – Filas mucho más grandes Than Columns

Si `m нелинилинининининит, la matriz delgada), el algoritmo todavía funciona – sólo se iteran sobre pares de columna en lugar de pares de fila, intercambiando los roles de `m` y `n`.
En la práctica esto mantiene el array 1‐D interior lo más corto posible, dando el mejor rendimiento.

-...

## 6. Aplicación del Código

A continuación se encuentran soluciones limpias y autocontenidas en **Java, Python y C++**.
Los tres utilizan la misma idea central: filas comprimidas, búsqueda binaria sobre sumas prefijo, y una salida temprana cuando golpeamos 'k'.

■ **Consejo para entrevistas** – Mención de que la observación clave es “compresar una dimensión y resolver el problema 1-D con un BST. ”
■ Hable a través de la subrutina *O(n log n)* y por qué el `TreeSet` / `multiset` es esencial.

-...

### 6.1 Java

``java
importar java.util*;

Clase Solución {
int public int maxSumSubmatrix(int[][] matriz, int k) {
filas int = matriz. longitud, cols = matriz[0].longth;
fila booleanaMajor = filas = = cols = =; // iterate sobre la dimensión más pequeña
int result = Integer.MIN_VALUE;

si (rowMajor) { // comprime filas
int[] temp = new int[cols];
para (incluido superior = 0; superior de las filas seleccionadas; superior++) {}
Arrays.fill(temp, 0);
para (incluido inferior = superior; inferior) {}
para (int c = 0; c) {}
temp[c] += matriz[bottom][c];
}
resultado = Math.max(resultar, maxSubarrayNoMoreThanK(temp, k));
if (result == k) return k; // best possible
}
}
} más { / / / compres columnas
int[] temp = nuevo int[rows];
para (inc. izquierda = 0; izquierda) {}
Arrays.fill(temp, 0);
para (a la derecha = izquierda; derecha) {}
para (int r = 0; r  se realizaron filas; r++) {
temp[r] += matriz[r][right];
}
resultado = Math.max(resultar, maxSubarrayNoMoreThanK(temp, k));
si (resultado == k) retorno k;
}
}
}
Resultado de retorno;
}

/** 1‐D rutina – mayor suma de sub-arrayo 0= k en O(n log n) */
int privada maxSubarrayNoMoreThanK(int[] nums, int k) {
int best = Integer.MIN_VALUE;
int curr = 0;
TreeSet se realizóInteger confianza prefix = nuevo TreeSet fiel();
prefix.add(0);

para (int x : nums) {
curr += x;
// necesitamos el prefijo más pequeño
Objetivo entero = prefijo.ceiling (curr - k);
si (target != null) {
mejor = Math.max(mejor, curr - target);
si (mejor == k) regresa mejor; // parada temprana
}
prefix.add(curr);
}
devolver mejor;
}
}
`` `

**Complejidad** – *(min(m,n)2 · max(m,n) · log max(m,n))* tiempo, *O(max(m,n))* memoria.
El `TreeSet` nos da búsqueda binaria en *log n*.

-...

### 6.2 Python

``python
importador bisect
de la importación Lista

Solución de clase:
def maxSumSubmatrix(self, matriz: List[List[int], k: int) - título int:
filas, cols = len(matrix), len(matrix[0])
row_major = hileras = cols
ans = 10**9

si la fila_major:
temp = [0] * cols
para arriba en rango(rows):
temp = [0] * cols
para abajo en rango(top, filas):
para c en rango(cols):
temp[c] += matriz[bottom][c]
ans = max(ans, self._best_no_more_than_k(temp, k))
si ans == k:
de vuelta k
más: # comprime columnas
temp = [0] * filas
para izquierda en rango(cols):
temp = [0] * filas
para derecho en rango(izquierda, cols):
para r en rango(rows):
temp[r] += matriz[r][right]
ans = max(ans, self._best_no_more_than_k(temp, k))
si ans == k:
de vuelta k
Retorno

def _best_no_more_than_k(self, nums: List[int], k: int) - título int:
prefijo = [0]
mejor = 10**9
curr = 0
para x en nums:
curr += x
# need smallest p œ= curr - k
idx = bisect.bisect_left(prefix, curr - k)
si idx se hizo len(prefix):
mejor = max(best, curr - prefix[idx])
bisect.insort(prefix, curr)
mejor
`` `

La versión Python utiliza `bisect.insort` para mantener la lista de prefijos ordenados – equivalente a un árbol de búsqueda binaria.

-...

### 6.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxSumSubmatrix(vector seleccionadovector identificadoint implicancia reducida matriz, int k) {
int m = matriz.size(), n = matriz[0].size();
bool rowMajor = m <= n; // iterate over smaller dimension
int best = INT_MIN;

si (rowMajor) { // comprime filas
vector:
para (incluido superior = 0; superior)
fill(temp.begin(), temp.end(), 0);
para (incluido inferior = superior; inferior) {}
para (int c = 0; c < n; ++c) temp[c] += matriz[bottom][c];
mejor = max(best, subarrayNoMoreThanK(temp, k));
si (mejor == k) retorno k;
}
}
} más { / / / compres columnas
vector:
para (inc. izquierda = 0; izquierda)
fill(temp.begin(), temp.end(), 0);
para (a la derecha = izquierda; derecha)
para (int r = 0; r < m; ++r) temp[r] += matriz[r] [right];
mejor = max(best, subarrayNoMoreThanK(temp, k));
si (mejor == k) retorno k;
}
}
}
devolver mejor;
}

privado:
int subarrayNoMoreThanK(const vector identificadoint círculo nums, int k) {
int curr = 0, best = INT_MIN;
multiset didint titulada pref{0};

para (int x : nums) {
curr += x;
auto = pref.lower_bound(curr - k); // prefijo más pequeño
si (lo != pref.end())
mejor = max(best, curr - *it);
pref.insert(curr);
}
devolver mejor;
}
};
`` `

"multiset " da el mismo comportamiento de investigación binaria que " TreeSet " .
El regreso temprano ( `mejor == k`) mantiene la solución de relámpago rápido.

-...

## 7. Entrevista " Consejos de búsqueda de empleo

Silencioso Pregunta Silencio Qué hacer
Silencio...
Silencio *¿Por qué comprime una dimensión?* Silencio Reduce un problema de 2-D a un problema de 1-D – una visión clave que reduce la complejidad de los bucles de 4 a 3-nested. Silencio
Silencio *¿Cómo funciona la rutina de 1‐D?* ← Utilizar sumas prefijas + BST. Explique `curr - p ≤ k` → `p ≥ curr - k`. Mostrar búsqueda de menor alcance. Silencio
* Complejidad en el tiempo* Silencioso `O(min(m,n)2 · max(m,n) · log max(m,n)). Para 100 × 100 esto es ~106 operaciones, fácilmente dentro de los límites. Silencio
Silencio *Espacio* Silencioso `O(max(m,n))` para el array comprimido + BST. Silencio
Silencio * Casos de edge* Silencio Negativo `k`, todos los valores de matriz negativos, matrices de un solo cuervo / un solo culumn, `k` igual al máximo global. Silencio
TENIDO *Siguiente* ANTERIOR Si hileras columnas, swap loops. Silencio
Silencio *Por qué esto importa para trabajos* Silencio Demuestra el dominio de las estructuras de datos avanzadas (BST, multiset), 2-D DP, y los intercambios espacio-tiempo. Excelente para entrevistas técnicas de alto nivel. Silencio

-...

## 8. SEO‐Friendly Blog Summary

- **Keywords**: LeetCode 363, Max Sum of Rectangle No Larger Than K, Hard LeetCode Problem, 2-D Kadane, Prefix Sums, TreeSet, multiset, búsqueda binaria, pregunta de entrevista, entrevista de codificación, algoritmo, entrevista de trabajo, entrevista de alta definición, C+++, Java, soluciones Python.
- **Meta Descripción**: “Solve LeetCode 363 – Max Sum of Rectangle No Larger Than K (Hard). Aprender el 2-D Kadane + Prefix Solución Sum + BST en Java, Python y C++. Guía de entrevista. ”

-...

## 9. Preguntas frecuentes

Silencio
Silencio...
Silencio **¿Puedo usar un mapa de hash en lugar de TreeSet?** Silencio Un mapa de hash da *O(n)* tiempo promedio, pero no puede realizar la búsqueda de menor alcance requerida para `curr - p ≤ k`. Necesitas una estructura ordenada. Silencio
Silencio **¿Qué pasa si todos los números son positivos?** Silencio La rutina 1‐D todavía funciona; simplemente devuelve el sub-array más grande ≤ k (o toda la matriz si su suma ≤ k). Silencio
Silencio **¿La solución es óptima?** Silencio Sí – la mejor suma posible ≤ k no puede exceder `k`, y nos detenemos tan pronto como golpeamos `k`. Silencio
Silencio **¿Podemos usar la ventana de deslizamiento en su lugar? ** Silencioso ventana funciona sólo cuando todos los números son no negativo. Aquí tenemos negativos, así que debemos utilizar el enfoque BST. Silencio

-...

## 10. Final Takeaway

El problema 2-D Hard LeetCode 363 te enseña uno de los patrones más valiosos para las entrevistas de codificación: **Consigue una dimensión, reduzca a 1-D, y luego solucione con un árbol equilibrado**.
Muestra:

- Comprensión profunda del algoritmo de Kadane y su extensión 2-D.
- Mastería de sumas prefix y búsqueda binaria en un contenedor clasificado.
- Capacidad para razonar acerca del tiempo – intercambio espacial y terminación temprana.

Implementar esto en Java, Python y C++ muestra la habilidad lingüística-agnóstica – un escaparate perfecto para una entrevista técnica de alto nivel.

■ **Pro-Tip** – En una entrevista, bosquejar la idea de alto nivel primero, luego bucear en la rutina 1‐D; el entrevistador verá inmediatamente entender el truco que da el tiempo óptimo.

¡Feliz codificación, y que su búsqueda de trabajo sea tan exitosa como esta solución!