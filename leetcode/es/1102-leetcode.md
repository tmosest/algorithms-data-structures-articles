-...
Título: LeetCode 1102. Path with Maximum Minimum Value -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1102. Camino con el máximo valor mínimo – Una guía completa
*(Java, Python, C++ – Max‐Heap de Dijkstra + 4-dirección BFS)*

-...

## Tabla de contenidos
1. 📌 Resumen del problema
2. 🚀 Por qué Dijkstra + Max‐Heap funciona
3. Aplicación de tres idiomas (Java / Python / C++)
4. Tiempo " Complejidad espacial "
5. 🤔 Pitfalls comunes (Las partes “Bad” " Ugly " )
6. 🎯 Variantes " Extensiones
7.  abstract Take‐away & Career‐boosting Tips
8. 📚 Más lectura " Recursos "

■ **SEO Palabras clave**: Path With Maximum Minimum Value, LeetCode 1102, Dijkstra algoritmo, grid path problem, Java BFS, Python priority queue, C+++ prioridad queue, entrevista problema de codificación, preparación de entrevistas, entrevista de ingeniería de software, consejos de coding entrevista, algoritmo blog, entrevista de estructura de datos, pensamiento algoritmo.

-...

## 1. 📌 Resumen del problema

**LeetCode #1102 – Path with Maximum Minimum Value* *

■ *Given an `m × n` integer grid `grid`, find a path from the top‐left cell `(0,0)` to the bottom‐right cell `(m‐1,n‐1) ` que maximiza el valor **minimum** encontrado a lo largo del camino. *

El camino sólo puede moverse en las cuatro direcciones cardinales (hasta, abajo, izquierda, derecha).
La respuesta es el *score* de la mejor ruta – el mayor valor posible de la entrada de red **smallest** en ese camino.

### Ejemplos

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
[5,4,5],[1,2,6],[7,4,6]] `4` Silencio El sendero resaltado produce min = 4.
[2,2,2,1,2,2,2],[1,2,2,2,1,2]]
[[3,4,6,3,4],[0,2,1,7],[8,3,2,7],[3,2,4,9,8],[4,1,2,0,0],[4,6,5,4,3]]

■ **Constraints**
■ 1 ≤ m, n ≤ 100, 0 ≤ grid[i][j] ≤ 109

-...

## 2. 🚀 Why Dijkstra + Max‐Heap Works

El problema es una *maximización de un mínimo* a lo largo de un camino.
Piense en cada celda como un nodo con peso `grid[i][j]`.
Cuando nos movemos a un vecino, la puntuación del camino se convierte en «min(current_score, neighbour_value)».
Queremos la mejor puntuación para cada nodo – el **maximum** posible tal puntuación.

Esto es exactamente lo que hace el algoritmo de Dijkstra si interpretamos el costo del borde como “negativo” o utilizamos un *máximo* en lugar de un min‐heap.
En cada paso tomamos el nodo que actualmente tiene la puntuación más alta alcanzable, luego relajamos a sus vecinos.

*¿Por qué Max-heap? *
La cola prioritaria almacena tuples `(score, x, y)` ordenados por **descending** puntuación.
Cuando aparecen un nodo, su puntuación está garantizada a ser la más grande posible entre todos los nodos no deseados – la misma propiedad avaricia que sostiene Dijkstra.

*Invariable de la madre*

■ La primera vez que aparece la celda de destino, la puntuación que aparece es la puntuación mínima máxima de cualquier camino desde `(0,0)` a esa celda.

La prueba es idéntica a la prueba Dijkstra clásica, sólo con `max` en lugar de `min` en la comparación.

-...

## 3. 🛠י 3‐Language Implementation

■ Las tres soluciones siguen la misma lógica:
■ *Initializar una matriz de `scores ' (`-1` = unreached).
■ Empuje `(grid[0][0], 0, 0)` en una cola de prioridad.
■ Mientras que la cola no es vacía, pop la célula con la puntuación más grande, relajarse sus cuatro vecinos, y actualizar sus puntuaciones si encontramos una mejor. *

■ **Importante:**
■ *Evite visitar un nodo dos veces con una puntuación más baja. *
■ Sólo encubra a un vecino si la nueva puntuación es estrictamente mayor que la actual puntuación almacenada para esa celda.

## 3.1 Java (JDK 17+)

``java
importar java.util*;

Solución de la clase pública {}
int final estático privado[][] DIRS = {0,1},{0},{0,-1},{-1,0};

public int maximumMinimumPath(int[][] grid) {
int m = grid.length, n = grid[0].length;
int[][] mejor = nuevo int[m][n];
for (int[] row : best) Arrays.fill(row, -1);
best[0][0] = grid[0][0];

// max‐heap ordenados por puntuación
PriorityQueue madeint[] conviene pq = new PriorityQueue Curso(a,b) - título Integer.compare(b[2], a[2]));
pq.offer(new int[]{0, 0, grid[0][0]}); // {x, y, score}

mientras (pq.isEmpty()) {
int[] cur = pq.poll();
int x = cur[0], y = cur[1], score = cur[2];

si (x == m-1 ' y == n-1) la puntuación de retorno;

para (int[] d : DIRS
int nx = x + d[0], ny = y + d[1];
si (nx √≥ 0 Нованый ny ненный ненный ненный ненный ненный неный неный ненный неный неныеный ный ный ный continuar ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный неный ный ный ный ный ный ный ный ный ный ный ный ный н

int newScore = Math.min(score, grid[nx][ny]);
si (newScore > best[nx][ny]) {}
best[nx][ny] = newScore;
pq.offer(new int[]{nx, ny, newScore});
}
}
}
retorno -1; // inalcanzable (nunca ocurre con entrada válida)
}

// --- Conductor para pruebas locales rápidas
public static void main(String[] args) {
int[][] g = {5,4,5},{1,2,6},{7,4,6}};
System.out.println(new Solution().maximumMinimumPath(g)); // 4
}
}
`` `

■ **Por qué esta versión Java es genial* *
*Explicit `int[][] best` matriz → O(mn) memoria. *
*Max‐heap comparator with `Integer.compare(b[2], a[2])` – sin objetos de envoltura. *
■ *Separación completa de la lógica de relajación. *

### 3.2 Python (3.9+)

``python
importación heapq
de la importación Lista

Solución de clase:
DIRS = [(0, 1), (1, 0), (0, -1), (-1, 0)]

def maximumMinimumPath(self, grid: List[List[int]) - Propiedad int:
m, n = len(grid), len(grid[0])
mejor = [1] * n para _ en rango(m)]
best[0][0] = grid[0][0]

# max‐heap: store (-score, x, y) because heapq is a min‐heap
heap = [(grid[0][0], 0, 0)]

Mientras salta:
neg_score, x, y = heapq.heappop(heap)
puntuación = -neg_score

si x == m - 1 y == n - 1:
puntuación de retorno

para dx, tio en ti mismo. DIRS:
nx, ny = x + dx, y + dy
si 0 0 0 0 0 0 0 0 0 0 0 0 0
new_score = min(score, grid[nx][ny])
si new_score œ best[nx][ny]:
mejor[nx][ny] = new_score
heapq.heappush(heap, (-new_score, nx, ny))
retorno -1 # inalcanzable – nunca ocurre para entradas válidas

Prueba rápida de cordura
si __name_ == "__main__":
sol = Solución()
print(sol.maximumMinimumPath([5,4,5],[1,2,6],[7,4,6])) # 4
`` `

■ **Por qué esta versión de Python es genial* *
■ *No hay dependencias externas – sólo la biblioteca estándar. *
■ *`-score` truco convierte el min‐heap en un max-heap, manteniendo el código mínimo. *
■ *Usando `mejor' como tabla de memoización evita revisitar células con puntajes inferiores. *

### 3.3 C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maximumMinimumPath(vector seleccionadovector seleccionado) {
int m = grid.size(), n = grid[0].size();
vector se llevó a cabo el título de propiedad intelectual mejor(m, vector seleccionado(n, -1));
best[0][0] = grid[0][0];

usando T = tuple obtenidaint,int,int título; // (score, x, y)
priority_queue obedecióT confidencial pq; // max‐heap by default
pq.emplace(grid[0][0], 0, 0);

const int dirs[4][2] = {0,1},{1,0},{0,-1},{-1,0};
mientras (pq.empty()) {
auto [score, x, y] = pq.top(); pq.pop();

si (x == m-1 ' y == n-1) la puntuación de retorno;

para (auto golpe d : dirs) {
int nx = x + d[0], ny = y + d[1];
si (nx √≥ 0 Нованый ny ненный ненный ненный ненный ненный неный неный ненный неный неныеный ный ный ный continuar ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный неный ный ный ный ный ный ный ный ный ный ный ный ный н

int newScore = min(score, grid[nx][ny]);
si (newScore > best[nx][ny]) {}
best[nx][ny] = newScore;
pq.emplace(new Score, nx, ny);
}
}
}
retorno -1; // inalcanzable (no sucede)
}
};
`` `

■ **Por qué esta versión C++ es genial* *
■ *Zero-overhead prioridad cola – el 'tuple' está empaquetado en el montón. *
■ *Explicit `dirs` array hace que la dirección de manejo sea clara. *
■ *Uso de `min` y `max` mantiene el algoritmo conciso. *

-...

## 3. ⚖ف Time & Space Complexity

Silencio Idioma Silencio Complejidad Silencio
Silencio--------------------------
Silencio **Java / Python / C+** Silencio **O(m · n log(m · n))** Silencio Cada célula puede ser empujada al montón hasta 4 veces (caso peor). Silencio
← Memoria Silencioso **O(m · n)** Silencio `mejor ` matriz + almacenamiento de montones. Silencio

El factor de registro viene de las operaciones del montón.
Con `m, n ≤ 100`, esto es fácilmente lo suficientemente rápido ( 5,00 4 000 log 4 000 ♥ 48 000 operaciones).

-...

## 4. 🤔 Pitfalls comunes (Las partes “Bad” " Ugly " )

Problema de la vida ← Código malo/reglamentable Silencio
Silencio--------------------------------------...
Silencio **Using a min‐heap** TENIENDO `priority_queue obedeciópair madeint,intilo confianza pq;` // wrong order ANTERITO Switch to max‐heap: `priority_queue madepair madeint,int título de propiedad intelectual pq;` o empujar valores negativos. Silencio
Silencio **Ignorando mejores puntuaciones** Silencio Popping a node once and never revisiting Silencio Mantener una matriz `mejor `; sólo relajar a los vecinos cuando la nueva puntuación es más alta. Silencio
Silencio **Off‐by-one errors in bounds** ← Olvidar `x+dx 0 `` cheque Silencio Siempre validar `0 ≤ nx < m` y `0 ≤ ny n` antes de acceder a la red. Silencio
Silencio **La rejilla mutable como “visitada”** Silencio `grid[nx][ny] = -1` Silencio Usa una matriz separada `mejor` o una matriz booleana `visitada`; modificar la entrada puede ser sorprendente. Silencio
Silencio **Utilización de la recursión / DFS** 104 tención No apilable para cuadrículas grandes; use BFS iterativa. Silencio

-...

## 5. 🎯 Variantes & extensiones

Silencioso Variant Silencioso Cómo Adaptarse
Silencio...
Silencio **Binary Search + Union‐Find** tención Buscar por el umbral máximo `t` tal que las células ≥ `t` están conectadas. Silencio
Silencio **Binary Search + DFS** tención Para cada umbral, ejecute un DFS para comprobar la conectividad; log‐time *O(log(maxValue) · m·n)*. Silencio
Silencio **Minimum Effort Path (LeetCode 1631)** Silencio Reemplazar `min(current, neighbour)` with `max(current, abs(diff))`; similar max-heap approach. Silencio
TEN **Aristas ponderadas (pesos no celulares)** TENIDO Dijkstra con costos de borde en lugar de costos de nodo. Silencio

-...

## 6.  abstract Take‐away " Career‐boosting Tips

1. #Mostrar el invariante # En entrevistas, articular que el max-heap garantiza que siempre está eligiendo la mejor puntuación posible hasta ahora.
2. **Explicar el interruptor “max” vs. “min”** – Destacar cómo cambiar la comparación convierte un Dijkstra estándar en la solución exacta.
3. **Evite mutar la entrada** – Mantenga la rejilla intacta; utilice una matriz "mejor" para la claridad.
4. *Mantenga el código ordenado* Use constantes de ayuda (`DIRS`) y variables locales de corta duración.
5. **Benchmark mentalmente** – Incluso si el problema es pequeño, discuta la complejidad asintotica; esto muestra conciencia algorítmica.

Dominar este problema demuestra competencia en algoritmos gráficos, estructuras de datos y codificación cuidadosa, un escaparate perfecto para entrevistas técnicas o blogs técnicos.

-...

### Palabras clave para SEO Base de conocimientos

- Camino Mínimo `
- `LeetCode 1091 `
- 'Dijkstra max-heap `
- `Java priority queue `
- 'Python heapq max-heap `
- 'C++ prior_queue tuple `
- `Graph connectivity binaria search `
- `Union-Find LeetCode `
- Sendero de Movilidad `

Siéntase libre de adaptar cualquiera de los fragmentos a su IDE preferido o juez en línea. ¡Feliz codificación!