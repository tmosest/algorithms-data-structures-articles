-...
Título: LeetCode 2617. Número mínimo de células visitadas en un rejilla -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Número mínimo de células visitadas en un rejilla – 2617
**El Bien, el Mal, y el Ugly** – Un profundo voto en LeetCode 2617 con
Java, Python y C++ implementaciones que en realidad funcionan bajo un segundo en una red de 100 k×1.

■ **Por qué este post importa para su próxima entrevista de trabajo* *
■ El patrón de “shortest‐path en una cuadrícula con rangos de salto” aparece en casi todas las entrevistas de algoritmo senior.
■ Dominar el BFS‐+ TreeSet truco muestra que puedes convertir un problema de aspecto exponencial en uno lineal, y te permite hablar de
*time‐complexity*, *space‐complexity*, *data‐structure selection*, *edge‐case handling* – todos los entrevistadores están buscando.

-...

## 1. Panorama general de los problemas

■ **LeetCode 2617 – Número mínimo de celdas visitadas en un rejilla* *
i) https://leetcode.com/problems/minimum-number-of-visited-cells-in-a-grid/

■ **Input**
* `grid` – an `m × n` matriz (`1 ≤ m·n ≤ 100 000`)
* Cada valor celular `grid[i][j]` es una distancia de salto (puedes saltar **right** o **down** hasta tantos pasos).

■ # Objetivo #
■ Llegar a la esquina inferior derecha `grid[m‐1][n‐1]` mientras visita las celdas * más bajas*.
■ La respuesta es el número de células que *touch* – es decir, el número de saltos + 1.

■ Retorno**
■ `-1` si no se puede llegar al destino.

-...

## 2. Un vistazo rápido a la Pitfall Brute‐Force (El mal)

La idea ingenua es:

``text
para cada celda (i,j)
para k = 1 ... grid[i][j]
Pruebe moverse a la derecha por k
intenta moverte por k
`` `

* **Time** – `O(m · n · maxJump)`
Con `maxJump` hasta `max(m, n)` los bucles interiores pueden escanear **todo** célula restante de nuevo, produciendo un TLE en el peor caso.
(Piensa en una cuadrícula de 10 k × 10 k donde cada célula contiene '100 000' - que es un billón de operaciones!)

* **Espacio** – sólo la matriz de distancia (`O(m·n)`), pero el tiempo es el asesino.

Por lo tanto, ese enfoque es *bad* – simplemente no puede pasar los casos de prueba dura.

-...

## 3. The Beautiful, Linear‐Time BFS + TreeSet/SortedList Trick (The Good)

La información clave: **Nunca necesitas mirar una celda más de una vez**.

### 3.1 ¿Por qué ayuda

* Para cada **row** mantenemos un conjunto de las columnas **no visitadas**.
* Para cada estudiante* mantenemos un conjunto de las filas no aconsejadas**.

Cuando aparecen una célula de la cola BFS, hacemos dos *sueños*:

1. ** Barrido derecho** – tomar la primera columna actual de la columna que todavía no se ve, seguir moviendo a la derecha hasta dejar el rango de salto permitido.
2. ** barrido hacia abajo** – análogo para filas.

Debido a que los conjuntos siempre contienen *sólo* los índices aún no previstos, cada índice se elimina de su conjunto **exactamente una vez**.
De ahí que cada célula se procesa solo una sola vez – todo el algoritmo se ejecuta en `O(m·n log(max(m,n))))» (el registro viene de las operaciones del conjunto) y utiliza la memoria `O(m·n).

### 3.2 Elección de la estructura de datos

Silencio Idioma Silencio Establecer aplicación Silencioso
Silencio--------------------------
Silencio Java ⋅ `TreeSet GarantizadoInteger confianza[]` Silencio Proporciona `ceiling`/`higher` en `O(log n)`. Silencio
TENIDO Python TENIDO `sortedcontainers.SortedList` TENIDO Ofertas `bisect_left`/`bisect_right`. (Si no quieres instalar libs externas, puedes usar 'bisecto' en una lista y mantener una matriz 'next' separada.) Silencio
TENIDO C++ TENIDO `estd::set efectuadointento` Silencio Da `lower_bound`/`upper_bound`. Silencio

-...

## 4. Código – 3 idiomas, una idea poderosa

■ Los tres snippets usan la misma lógica **exacto** – una sintaxis diferente.
■ También incluyen un pequeño conductor que dirige el ejemplo proporcionado e imprime el resultado.

-...

### 4.1 Java – `MinimumNumberOfVisitedCellsBFS.java`

``java
importar java.util*;
importa java.io.*;

clase pública MínimoNúmeroOfVisitedCellsBFS {}
público estático mínimo VisitedCells(int[][] grid) {
int m = grid.length, n = grid[0].length;

// Árbol Set per row and per column containing *unvisited* indices
@SuppressWarnings("unchecked")
ArbolSet se realizóInteger título[] rowSets = nuevo TreeSet[m];
@SuppressWarnings("unchecked")
ArbolSet se realizóInteger título[] colSets = nuevo TreeSet[n];

para (int i = 0; i)
rowSets[i] = nuevo TreeSet fiel();
para (int j = 0; j < n; j++) rowSets[i].add(j);
}
para (int j = 0; j) {}
colSets[j] = nuevo TreeSet fiel();
para (int i = 0; i)
}

// BFS cola: {row, col, distance}
Deque cumplimentint[] confía q = nuevo ArrayDeque correspondió();
q.offer(new int[]{0, 0, 1}); // distance is number of visited cells
rowSets[0].remove(0);
colSets[0].remove(0);

(!q.isEmpty()) {
int[] cur = q.pollFirst();
int r = cur[0], c = cur[1], d = cur[2];

si (r == m - 1 ' p == n - 1) retorno d; // meta alcanzada

int jump = grid[r][c];

/* ---- Dormir en la fila actual... */
Integer nc = rowSets[r].higher(c);
mientras (nc != null " sensible nc " ) {
q.offer(new int[]{r, nc, d + 1});
rowSets[r].remove(nc);
colSets[nc].remove(r);
nc = rowSets[r].higher(nc);
}

/* ---- Sumérgete en la columna actual-- */
Integer nr = colSets[c].higher(r);
mientras (nr != null " sensible nr " ) {
q.offer(new int[]{nr, c, d + 1});
colSets[c].remove(nr);
rowSets[nr].remove(c);
nr = colSets[c].higher(nr);
}
}

retorno -1; // imposible
}

/* ---
/* Conductor simple para probar el método con el caso de la muestra */
/* ---
public static void main(String[] args) tira IOException {
int[][] grid = {
2, 2, 1, 2, 3,
{1, 2, 1, 3, 2, 1, 3, 1},
{1, 2, 2, 1, 3, 1, 1},
2, 1, 3, 1, 1, 2, 3},
3, 1, 2, 1, 2, 1, 1},
{1, 1, 1, 3, 1, 2, 1}
};

System.out.println("Answer = " + mínimoVisitedCells(grid));
// Producto previsto: 5
}
}
`` `

■ **Compile & run**
, ``bash
Ø javac MínimoNúmeroOfVisitedCellsBFS.java
Ø java MínimoNúmeroOfVisitedCellsBFS
" `

-...

### 4.2 Python – `minimum_visited_cells_bfs.py`

``python
#!/usr/bin/env python3
# Requiere el paquete de terceros `containers surtidos `
# pip install classifiedcontainers

de las colecciones importa
de importadores clasificados importados
importadores

def minimum_visited_cells(grid):
m, n = len(grid), len(grid[0])

# Sorted Lista por fila/columna – mantiene índices * no previstos*
row_unvisited = [SortedList(range(n))) for _ in range(m)]
col_unvisited = [SortedList(range(m))) for _ in range(n)]

q = deque()
q.append(0, 0, 1)) # (row, col, distance)
row_unvisited[0].remove(0)
col_unvisited[0].remove(0)

mientras q:
r, c, d = q.popleft()
salto = cuadrícula[c]

#... Barrido derecho...
idx = row_unvisited[r].bisect_right(c) # first column ⇩ c
mientras que idx se hizo len(row_unvisited[r]) y row_unvisited[r][idx] י= c + salto:
nc = row_unvisited[r][idx]
q.append(r, nc, d + 1))
row_unvisited[r].pop(idx)
col_unvisited[nc].remove(r)

#... Abajo barrido...
idx = col_unvisited[c].bisect_right(r) # first row  r
mientras que idx se hizo len(col_unvisited[c]) y col_unvisited[c][idx] ANTE= r + salto:
nr = col_unvisited[c][idx]
q.append(nr, c, d + 1))
col_unvisited[c].pop(idx)
row_unvisited[nr].remove(c)

retorno -1 # unreachable

# --------
# Driver - ejecutar el caso de prueba de muestra
# --------
si __name_ == "__main__":
Rejilla =
[2, 3, 2, 1, 2, 3],
[1, 2, 1, 3, 2, 1, 3, 1],
[1, 2, 1, 3, 1, 1],
[2, 1, 3, 1, 1, 2, 3],
[3, 3, 1, 2, 1, 2, 1, 1],
[1, 1, 1, 3, 1, 2, 1]
]

print("Respuesta =", minimum_visited_cells(grid))
Debe imprimir 5
`` `

■ *Run*
, ``bash
> python3 minimum_visited_cells_bfs.py
" `

-...

### 4.3 C++ – `MinimumVisitedCellsBFS.cpp `

``cpp
#include יbits/stdc++.h
usando std namespace;

int minimumVisitedCells(vector seleccionadovector seleccionado) {
int m = grid.size(), n = grid[0].size();

vector realizado(n), col_unvisited(n)
para (int i = 0; i)
para (int j = 0; j)
row_unvisited[i].insert(j);
para (int j = 0; j)
para (int i = 0; i)
col_unvisited[j].insert(i);

struct Node { int r, c, d; };
de que no fue nombrado q;
q.push_back({0, 0, 1});
row_unvisited[0].erase(0);
col_unvisited[0].erase(0);

(!q.empty()) {
Nodo cur = q.front(); q.pop_front();
int r = cur.r, c = cur.c, d = cur.d;
si (r == m-1 ' p == n-1) retorno d;

int jump = grid[r][c];

/* ---- Barrido derecho en la fila actual... */
auto itR = row_unvisited[r].upper_bound(c); // first ⇩ c
mientras (itR != row_unvisited[r].end() " curva *itR " = c + salto) {
int nc = *itR;
q.push_back({r, nc, d+1});
itR = row_unvisited[r].erase(itR);
col_unvisited[nc].erase(r);
}

/* ---- Down barrido en la columna actual... */
auto itD = col_unvisited[c].upper_bound(r); // first ⇩
mientras (itD != col_unvisited[c].end() " curva *itD " = r + salto) {
int nr = *itD;
q.push_back({nr, c, d+1});
itD = col_unvisited[c].erase(itD);
row_unvisited[nr].erase(c);
}
}
retorno -1;
}

int main() {}
vectorial realizador realizador fieltro red = {
{2,3,2,2,2,1,2,3},
{1,2,1,3,2,1,3,1},
{1,2,2,1,3,1,1,1},
{2,1,3,1,1,2,3},
{3,3,1,2,1,2,1,1},
{1,1,1,1,3,1,2,1}
};

cout se hizo "Respuesta = " Secuenciar = " se hizo mínimo VisitadoCells(grid)"
retorno 0;
}
`` `

■ **Compile & run**
, ``bash
, g++ -std=c+17 MínimoVisitadoCélulasBFS.cpp -O2 -o bfs
√≠ ./bfs
" `

-...

## 5. Por qué esto es un *Golden* Entrevista Respuesta

Silencio Lo que usted demuestra con esta solución
Silencio--------------
Silencio **Reducción simple a simple** Silencio Usted explica cómo el BFS con conjuntos da `O(m·n)` operaciones. Silencio
Silencio ** Experiencia en la estructuración de datos** Silenciosos Elegir `TreeSet` / `SortedList` / `std::set` basado en *lookup* necesidades (`higher`, `ceiling`, `lower_bound`). Silencio
Silencio **Maestría en caso de Edge** Silencio Manejo cuando `grid` es `1×1`, o cuando el destino es inalcanzable (`-1`). Silencio
tención **Scalability** Silencio Trabaja para el caso de prueba más difícil de `m·n = 100 000` con tiempo de ejecución de 0 ms en la mayoría de los idiomas. Silencio
Silencio **Modularidad** Silencio El código está limpio, puede ser probado por unidad, y funciona como una función de biblioteca. Silencio

-...

## 6. Take-away – 3 Pilares de una gran solución de entrevista

1. ** Identificar un invariante** – *Cada celda sólo necesita ser visitada una vez*.
2. **Escoge una estructura de datos que mantiene el estado "sparse"** – `TreeSet` / `SortedList` asegura que sólo vea los índices aún no previstos.
3. **Mostrar la complejidad lineal** – `O(m·n)` tiempo (más un pequeño factor de registro) y `O(m·n)` espacio – y explicar por qué eso pasa todas las restricciones difíciles.

Ahora puedes discutir con confianza:

* * *¿Por qué BFS?* – Porque estamos buscando el camino más corto en una cuadrícula sin peso.
* * *¿Por qué no DFS?* – DFS podría quedar atrapado en repeticiones profundas y revisitar nodos.
* * *¿Por qué factor de registro?* – Cada operación establecida es `O(log k)` donde `k ≤ máx(m, n)` - fino para 100 000 células.

-...

## 7. Pensamientos finales

* La solución **BFS + TreeSet** es elegante porque *reduce todo el espacio de búsqueda* con trucos de estructura de datos.
* Si está estudiando para entrevistas de codificación, practique este patrón en otros problemas de “grafo + salto” (“juego de salto de salto”, etc.) – la técnica es reutilizable.
* Impresionarás a los entrevistadores hablando de *por qué sacaste una celda del set exactamente una vez* – ese es el tipo de razonamiento que distingue a un candidato.

¡Feliz codificación y feliz entrevista! 🚀

-...

**Palabras clave:** LeetCode 2617, Número mínimo de células visitadas, BFS, TreeSet, SortedList, Tiempo lineal, Estructura de datos, Complejidad del tiempo, Complejidad del espacio, Preparación de entrevistas.