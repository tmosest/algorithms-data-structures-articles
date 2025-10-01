-...
Título: LeetCode 3128. Triángulos derecho -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Soluciones de tres idiomas para LeetCode 3128 – * Triángulos rectos*

A continuación se presentan implementaciones limpias y de producción en **Java**, **Python** y **C++** que resuelven el problema en *O(m × n)* tiempo y *(m + n)* memoria adicional, donde *m* es el número de filas y *n* el número de columnas.

■ *Problema recap*
■ Un triángulo derecho** está formado por tres células que contienen `1`.
■ Un vértice debe compartir un **row** con el segundo vértice, y el primer vértice debe compartir un **column** con el tercer vértice.
■ Contar todos estos triángulos en una matriz binaria.

-...

#### 1.1 Java

``java
importar java.util*;

Clase Solución {
public long numberOfRightTriangles(int[][] grid) {
filas int = grid.length;
int cols = grid[0]. longitud;

// Cuenta previa en cada fila y columna
int[] rowCnt = nuevo int[rows];
int[] colCnt = nuevo int[col];

para (int r = 0; r  se realizaron filas; r++) {
para (int c = 0; c) {}
si (grid[r][c] == 1) {
fila Cnt[r]+;
colCnt[c]+;
}
}
}

triángulos largos = 0;
para (int r = 0; r  se realizaron filas; r++) {
para (int c = 0; c) {}
si (grid[r][c] == 1) {
// (rowCnt[r] - 1) opciones para la pierna horizontal
// (colCnt[c] - 1) opciones para la pierna vertical
triángulos += 1L * (rowCnt[r] - 1) * (colCnt[c] - 1);
}
}
}
triángulos de retorno;
}
}
`` `

¿Por qué 'long'? *
El número máximo de triángulos puede alcanzar `1012` (1 000 × 1 000 rejilla llena de uno). "int" se desbordaría.

-...

### 1.2 Python

``python
Solución de clase:
def number OfRightTriangles(self, grid: List[List[int]]) int:
filas, cols = len(grid), len(grid[0])

# Rema y mostradores de columna
row_cnt = [0] * rows
col_cnt = [0] * cols

para r en rango(rows):
para c en rango(cols):
si la rejilla [r][c]:
row_cnt[r] += 1
col_cnt[c] += 1

triángulos = 0
para r en rango(rows):
para c en rango(cols):
si la rejilla [r][c]:
triángulos += (row_cnt[r] - 1) * (col_cnt[c] - 1)

triángulos de retorno
`` `

Los enteros arbitrarios de precisión de Python significan que no necesitamos preocuparnos por el desbordamiento.

-...

#### 1.3 C++

``cpp
Incluido el título

Clase Solución {
public:
Número de largosOfRightTriangles(std::vector seleccionado:::vector fieltro unidad grid) {
int rows = grid.size();
int cols = grid[0].size();

std::vector seleccionado injerto(rows, 0), colCnt(cols, 0);

// Cuenta 1 en cada fila y columna
para (int r = 0; r)
para (int c = 0; c)
si (grid[r][c]) {}
++rowCnt[r];
++colCnt[c];
}

triángulos largos = 0;
para (int r = 0; r)
para (int c = 0; c)
si (grid[r][c]) {}
triángulos += 1LL * (rowCnt[r] - 1) * (colCnt[c] - 1);
}

triángulos de retorno;
}
};
`` `

" larga duración " garantiza una aritmética segura de 64 bits.

-...

## 2. Blog Artículo: “El Bien, el Mal, y el Ugly of Counting Right Triangles”

### 2.1 Por qué este problema importa en las entrevistas

- **Traversal de Matrix** - un pilar de preguntas de entrevista.
**Conteo de la combinación** – prueba si puede detectar soluciones *O(m × n)* en lugar de brute‐force O(m × n)3).
- ** Pensamiento por caso edge** – manejo de salidas muy grandes y limitaciones de memoria.
- **Cross‐language fluency** – entrevistadores a menudo piden soluciones Java/Python/C++ sobre la marcha.

### 2.2 El Bien – Intuición & Simplicidad

La visión clave:
■ *Si una célula (r, c) es un vertex de ángulo derecho, cualquier otro `1` en su fila puede ser la pierna horizontal, y cualquier otro `1` en su columna puede ser la pierna vertical. *

Así, para cada uno de `1` sólo necesitamos los recuentos de `1`s en su fila y columna.
El número de triángulos con esa célula como ángulo recto es simplemente
`(rowCount[r] – 1) × (colCount[c] – 1).

Esto reduce una explosión aparentemente combinatoria a un paso lineal.

### 2.3 The Bad – Naïve Approaches that TLE

Un sencillo O(m × n)3) algoritmo:
1. Enumerar todos los trillizos de células.
2. Revisa la condición geométrica.

Incluso para una red de 100×100, esto implica miles de millones de operaciones, mucho más allá de los límites de las entrevistas.
Las limitaciones del problema (1000×1000) descartan cualquier solución cúbica o cuadrática de celdas.

### 2.4 El Ugly – Corner Cases & Overflow

- Todas las células son `1`**:
El número de triángulos puede ser tan alto como
`eva (rowCount [r] – 1) × (colCount[c] – 1) ♥ `1012`.
Utilizando una sobrefluencia de enteros de 32 bits, utilice 64 bits ( " largo " ).
- ¿Qué?
Muchas filas/columnas contienen cero `1`s. Nuestro algoritmo maneja esto con gracia porque `(rowCount [r] – 1) 'se vuelve negativo sólo si `rowCount[r] == 0`, pero vigilamos comprobando `grid[r][c] == 1` antes de calcular el producto.
- **No-rectangular inputs**:
LeetCode garantiza que `grid[i].length` es constante, pero el código defensivo puede afirmar o manejar arrays jagged.

### 2.5 Step‐by‐Step Walkthrough (Java)

``text
1. Cuenta 1s en cada fila → rowCnt[]
2. Cuenta 1s en cada columna → colCnt[]
3. Por cada celda que es 1:
triángulos += (rowCnt[r] - 1) * (colCnt[c] - 1)
`` `

Los dos primeros pasos son O(m × n).
El tercer paso es también O(m × n).
Tiempo total: **O(m × n)**.
Memoria extra: **O(m + n)** para los contadores.

### 2.6 Complexity Analysis

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio Contando filas Silencio O(m × n) Silencio O(m)
Silencio Contando columnas Silencio O(m × n) Silencio O(n)
TENIDO Triángulos de computación TENIDO O(m × n) ANTE O(1) (además de los contadores)
Silencio **Total** Silencio**

Esto satisface las limitaciones cómodamente:
- Para una red de 1000 × 1000: ~ 1 000 000 operaciones, ~8 KB de almacenamiento auxiliar.

### 2.7 Testing & Edge‐ Lista de verificación de casos

Silencio Test Silenciosos Silenciosos esperados
Silencio--------Prince------
Todos los ceros Silencio 3×3 todos `0` Silencio 0 Silencio No triángulos tención
Silencio Todos los que vivieron 4×4 todos `1` Silencio 4 * (3 * 3) = 36 Silencio Max cuenta Silencio
Silencio Espesor de la vida 3×3 con aislamiento `1` Silencio 0 Silencio Necesidad al menos dos 1s en la misma fila/col
Silencio No Cuadrante Silencio 2×5 rejilla Silencio Cuenta en consecuencia
Silencio Gran entrada Ø 1000×1000 con 50% de los que están bajo control Ejecutar en י0.1 s  durable Rendimiento punto de referencia

### 2.8 Escapadas para tu próxima entrevista

- Empieza con contar ayudantes. Cuando un problema implica restricciones de la misma fila / misma columna , frecuencias de fila pre-compute / columna.
Cuidado con el flujo entero Si sospecha que los resultados pueden exceder de 231 – 1, utilizar tipos de 64 bits.
*Explica tu lógica*: Incluso si su código es perfecto, articulando la intuición (como la vista “derecho-ángulo de vertex”) impresiona a los entrevistadores.
- *La complejidad del tiempo* Muéstrale considerado O(m × n)3) y por qué falla antes de presentar la solución O(m × n).

### 2.9 Final Verdict

- **Bueno** – Un hermoso algoritmo *(m × n)* que es tanto **eficiente** como ** legible**.
- **Bad** – Cualquier enfoque de fuerza bruta *time-out* en casos de prueba grandes.
- **Ugly** – Cuidado con el desbordamiento y la sparsidad, pero un cuidadoso producto de 64 bits lo arregla.

Este problema es un ejemplo *clásico* de cómo una simple observación combinatoria puede transformar un desafío aparentemente intrínseco en una solución limpia y amigable con las entrevistas. Dominarla le dará una sólida base para cualquier pregunta de entrevista basada en matriz.

-...

### 2.9 ¿Quieres impresionar aún más?

- **Agrega una línea única para Python**:
``python
triángulos = suma(row_cnt[r]-1)*(col_cnt[c]-1)
para r en rango(rows) para c en rango(cols) si grid[r][c]
`` `
- **Discuss parallelization**: Dos escaneos separados pueden ser ejecutados paralelamente; hablar de la posibilidad si el entrevistador pregunta sobre *computación distribuida*.

### 2.10 Palabras finales

Contar triángulos derecho es un microcosmos de la *“matrix + combinatoria + conteo cuidadoso”* tema de entrevista. Al aprender el patrón de “derecho triángulo vértice” contando, estará listo para una amplia variedad de preguntas de entrevista que le piden a *contar* estructuras dentro de cuadrículas 2-D.

¡Feliz codificación y buena suerte en tu próxima entrevista!