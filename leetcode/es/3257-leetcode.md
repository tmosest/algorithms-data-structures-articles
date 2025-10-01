-...
Título: LeetCode 3257. Máximo Suma de valor al colocar tres ganchos II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 3257 – Maximum Suma de valor al colocar tres ganchos II
**Idiomas** Java Silencio Python Silencio C++
*Dificultad* Duro
**LeetCode URL** : ▪ https://leetcode.com/problems/maximum-value-sum-by-placing-three-rooks-ii/ título

-...

## 1. Recaptación de problemas

Se le da una tabla de 'm × n` donde `board[i][j]` es el valor de la celda `(i, j)`
( `3 ≤ m, n ≤ 500`, `-109 ≤ tabla [i] [j] ≤ 109`).

Lugar **Exactamente tres** vagabundos en el tablero para que no dos ladrones compartan la misma fila o la misma columna.
Devuelve la suma máxima posible de las tres células elegidas.

-...

## 2. The Brute‐Force Trap

La solución obvia es probar cada combinación de tres células (`O(m3n3)`) y comprobar el
restricciones de fila/columna – que es astronómicamente costoso para '500 × 500'.

Incluso un DFS de 3 niveles (`O(m3)`) todavía produce **125 000 000 000** operaciones en el peor caso.

■ **Bad** – O(n6) = *imposible* para los límites dados.

-...

## 3. La "buena" visión

Sólo necesitamos **tres** giros, por lo que el número de posiciones *conflicto* que pueden ser
bloqueado por un ladrón es pequeño.
La idea clave es:

1. **Reducir el espacio de búsqueda** manteniendo solamente las celdas * más valiosas*.
2. Después de la reducción, el conjunto restante es lo suficientemente pequeño como para ser forzada por bruto.

-...

## 4. Los Casos de bordes “Ugly”

* Valores negativos – la respuesta podría ser el triple * más grande* (es decir, menos negativo).
* Valores duplicados en la misma fila / columna – todavía debemos evitar compartir filas / columnas.
* Ties – necesitamos mantener suficientes candidatos para cubrir todas las combinaciones óptimas.

Un ingenuo “top-K” (por ejemplo, K = 250) puede perder un triple óptimo si el óptimo
implica una célula que está * justo debajo* del corte.
Por lo tanto necesitamos un vínculo determinista que garantice que capturamos todo óptimo posible.

-...

## 5. La solución óptima (O(m·n) + O(K3) donde K ≤ 15)

1. #Per-row top‐3**
Para cada fila, mantenga las 3 células con los mayores valores.
(Si una fila tiene menos de 3 células, mantenga todas ellas).

2. **Recojan a los candidatos* *
Reúne todas estas células → en la mayoría de las células `3·m`.

3. **Per-column filter**
Clasificar las células recolectadas por valor (descendiente).
Escanee la lista ordenada y mantenga hasta **3** celdas por columna (las mejores).
Después de este paso, la lista contiene **en la mayoría de las células `3·m + 3·n`**, pero en la práctica ella
se encoge dramáticamente.

4. **Bound the final list to 15 cells**
Para cualquier célula elegida, en la mayoría de otras 2 células comparten su fila y en la mayoría 2 comparten su
columna → un total de 5 células conflictivas.
Puesto que sólo necesitamos 3 rooks, el número máximo de células que *podríamos* necesita
La inspección es de 3 a 5 = 15.
Por lo tanto, podemos tomar con seguridad las primeras **15** células de la lista clasificada
(o todos ellos si menos).

5. **Brute‐force all triplets* *
Con la mayoría de 15 celdas, sólo hay tres triples C(15, 3) = 455` – trivial para probar.

6. **Regresar la mejor suma** (utilizar `long` para evitar el desbordamiento).

Corrección

- El per-row top‐3 garantiza que cualquier colocación óptima de rook debe utilizar una célula
que está entre los 3 mejores en su fila.
- El filtro per-column garantiza que para cada columna mantengamos sus 3 mejores
células que sobrevivieron al filtro de fila.
- El límite de “15 celdas” sigue el principio del agujero de paloma descrito anteriormente.
- Por lo tanto, cada triple óptimo aparece en la lista final y se examina.

### Complexity

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
tención Row top‐3 (heap per row) Silencio `O(m·n·log 3)` → `O(m·n)` Silencio `O(m)` Silencio
Filtro de columna ( surtido + conteo) Silencio `O( (3m)·log (3m) ) → `O(m·n·log m)` Silencio `O(m·n)` Silencio
tención Lista final (≤ 15 celdas) Silencio
Silencio Triplet brute‐force Silencio `O(153) = 455` Silencio `O(1)` Silencio
Silencio **Total** Silencioso `O(m·n)` Silencioso `O(m·n)` (característica de todas las células)

La memoria está dominada por la propia tabla (entrada).
El algoritmo es totalmente lineal en el tamaño de la tabla y sólo utiliza un puñado de extra
arrays.

-...

## 6. Aplicación

A continuación se presentan implementaciones limpias y de producción en **Java**, **Python**, y **C+**.

-...

### 6.1 Java

``java
importar java.util*;
importa java.io.*;

Solución de la clase pública {}
Clase privada estática
int r, c, val;
Cell(int r, int c, int val) { this.r = r; this.c = c; this.val = val; }
}

máximo público largo ValueSum(int[][] board) {
int m = board.length, n = board[0]. longitud;
Lista de candidatos Cell] = nuevo ArrayList recomendado();

// 1 ride⃣ Per‐row top‐3 (min‐heap of size 3)
para (int i = 0; i)
PriorityQueue se llevó a caboCell confiar min = nueva PrioridadQueue quiso decir (Comparador.comparadorInt(a - título a.val));
para (int j = 0; j) {}
Cell cur = new Cell(i, j, board[i][j]);
min.offer(cur);
si (min.size() 3) min.poll();
}
candidatos.addAll(min);
}

// 2Get⃣ Per‐column filter – mantener hasta 3 mejores por columna
(a, b) - título Integer.compare(b.val, a.val)); // descending
Mapa seleccionadoInteger, Integer confianza colCnt = nuevo HashMap garantizado();
Lista seleccionadaCell] filtrado = nuevo ArrayList recomendado();
para (Célula Celular : candidatos) {}
int c = cell.c;
si (colCnt.getOrDefault(c, 0)
filtrado.add(cell);
colCnt.put(c, colCnt.getOrDefault(c, 0) + 1);
}
}

// 3down Mantenga sólo las primeras 15 células (o todas menos)
int limit = Math.min(filtered.size(), 15);
mucho mejor = Long.MIN_VALUE;

// 4Get Bru Brute‐force todos los triples
para (int i = 0; i) {}
para (int j = i + 1; j) {}
para (int k = j + 1; k) {}
Celda a = filtrado.get(i);
Cell b = filtered.get(j);
Cell c = filtered.get(k);
si (a.r == b.r
a.c == b.c Silencioso a.c == c.c Silencioso b.c == c.c {}
continuar; // misma fila o columna
}
long sum = (long) a.val + b.val + c.val;
si (sumo mejor) = suma;
}
}
}
devolver mejor;
}
}
`` `

-...

### 6.2 Python

``python
Solución de clase:
def máximo ValueSum(self, board: List[List[int]) - int:
m, n = len(board), len(board[0])

# --- Paso 1: mantener la parte superior 3 por fila --------------------
row_candidates = [] # lista de (r, c, val)
para r en rango(m):
* # min‐heap of length #
para c en el rango(n):
val = board[r][c]
si salta(salto)
heap.append(val, c))
más:
[0] [0]:
heap[0] = (val, c)
# Mantén el montón ordenados después de cada inserción
heap.sort()
para Val, c en montones:
row_candidates.append(r, c, val))

# --- Paso 2: mantener la parte superior 3 por columna - Sí.
row_candidates.sort(key=lambda x: -x[2]) # ordenar por val descendiendo
col_cnt = {}
col_candidates = []
para r, c, val in row_candidates:
si col_cnt.get(c, 0)
col_candidates.append(r, c, val))
col_cnt[c] = col_cnt.get(c, 0) + 1

# --- Paso 3: tomar primero 15 (o todos) - Sí.
limit = min(15, len(col_candidates))
mejor = -10**18 # lo suficientemente largo para los negativos

# --- Paso 4: brute‐force todos los triples .
para i en rango(limit):
r1, c1, v1 = col_candidates[i]
para j en rango(i+1, límite):
r2, c2, v2 = col_candidates[j]
si r1 == r2 o c1 == c2: continuar
para k en rango(j+1, límite):
r3, c3, v3 = co_candidatos[k]
si r1 == r3 o r2 == r3 o c1 == c3 o c2 == c3
mejor = max(best, v1 + v2 + v3)
mejor
`` `

-...

### 6.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
struct Cell {
int r, c, val;
Cell(int _r, int _c, int _v) : r(_r), c(_c), val(_v) {}
};

Long long maximumValueSum(vector seleccionadovector realizador seleccionado) { {
int m = board.size(), n = board[0].size();
vector asignadoCell confianza rowTop; // en la mayoría de 3 por fila

--------- Paso 1: superior a 3 por fila...
para (int r = 0; r) {}
priority_queue obtenidosCell, vector efectuadoCell confianza, función efectuadabool(cont Celular reducida, const Cell cerrada) minHeap(
[](cont Celular reducida a, const Celular reducida b){ devolver a.val se realizó b.val; }); // max-heap
para (int c = 0; c) {}
minHeap.emplace(r, c, board[r][c]);
si (minHeap.size() 3) minHeap.pop();
}
(!minHeap.empty()) {}
rowTop.push_back(minHeap.top());
minHeap.pop();
}
}

--------- Paso 2: filtro por columna...
(rowTop.begin(), rowTop.end(),
[](cont Celular reducida a, const Celular reducida b){ devolver a.val не b.val; });

vector asignadoCell] colTop
unordered_map madeint,int confianza colCnt;
para (contigo Celular reducida x : rowTop) {
si (colCnt[x.c]
colTop.push_back(x);
++colCnt[x.c];
}
}

--------- Paso 3: Mantener a la mayoría de 15 células...------
int lim = min(int)colTop.size(), 15);
largo tiempo mejor = LLONG_MIN;

// -------- Paso 4: triples de fuerza bruta --------
para (int i = 0; i) {}
para (int j = i+1; j)
si (colTop[i].r == colTop[j].r
para (int k = j+1; k)
si (colTop[i].r == colTop[k].r
colTop[i].c == colTop[k].c Silencioso colTop[j].c == colTop[k].c) continue;
long sum = (long long)colTop[i].val + colTop[j].val + colTop[k]. val;
mejor = max(best, sum);
}
}
}
devolver mejor;
}
};
`` `

-...

## 6. Prueba tu solución

``text
Input: board = [[1, 2, 3], [3, 4, 5], [7, 6, 8]
Producto: 23 (3 + 8 + 12? en realidad mejor 5 + 7 + 11 = 23)
`` `

Maletas de borde:

← Consejo Permanente
Silencio...
Silencio Todos los negativos TENIDOS, por ejemplo: `[-5,-10,-3,-2,-8]` → `-3 + -5 + -8 = -16` TEN
Silencio Valores idénticos en la misma fila
Silencio Las columnas muy escasas / cuervos ¦ algoritmo todavía elige top‐3 por fila/column TEN

-...

## 7. Por qué este blog te ayudará a aterrizar un trabajo

Cómo el artículo lo demuestra
Silencio...
Silencio **Problema decomposición** Silencio Naïve → reducir el espacio de búsqueda → final brute‐force
Silencio ** Diseño de algorithm** TENIDO Utilizar filtros per-row / per-column, 15-cell bound TEN
tención **Análisis de la complejidad** tención Tiempo lineal, ciclo triple de tamaño constante
Silencio **Codificación limpia** Silencio Java, Python, C+++ snippets
Silencio **Edge-case thinking** ← Extensiva mesa de prueba

Los entrevistadores aman a los ingenieros que pueden **ver patrones**, **optimizar** y **escribir código de mantenimiento**. Este artículo muestra exactamente eso.

-...

## 8. TL;DR

1. Mantener **top 3 celdas por fila** (min-heap, tamaño ≤ 3).
2. Mantenga **top 3 celdas por columna** de aquellas (tipo descendente).
3. **Toma sólo las primeras 15** células (o todas menos).
4. Brute-force todos los triples, saltando las combinaciones de la misma hoja / mismo-column.
5. Complejidad: **O(m × n)** tiempo, **O(m × n)** memoria.

-...

Siéntete libre de copiar el código, ejecutelo en LeetCode y añádelo a tu cartera de GitHub. ¡Feliz codificación!

-...

*Keywords: `máximo valor suma`, `board`, `linear time`, `3x3 board`, `algorithm design`, `LeetCode`, `Java`, `Python`, `C++`, `O(m*n)`. *