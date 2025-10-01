-...
Título: LeetCode 1293. Sendero más corto en una plancha con eliminación de obstáculos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Sendero más corto en una rejilla con eliminación de obstáculos
**(LeetCode 1293 – Hard)**
*Python ← Java ← C++ – Solución de 3 idiomas + un blog listo para el trabajo*

-...

## Tabla de contenidos
1. [Norma general](#problema vista previa)
2. [Key Insights " Greedy " No-Go "](#key-insights)
3. [Algorithm Design](#algorithm-design)
4. [Análisis de complejidad](#complexidad-análisis)
5. [Aplicación en 3 idiomas](#implementaciones)
* Java – 3‐D visitados + BFS
* Python – `collections.deque` + 3-D visitado
* C++ – `struct` + `queue` + 3-D visitado
6. [El Bien, el Mal, y el Ugly] (#bueno-bad-ugly)
7. [SEO‐Ready Summary " Takeaway for Interviewers](#seo-summary)
8. [Más lectura > Recursos](#recursos)

-...

## יa name="problem-overview"

Se le da una cuadrícula 2D (`m × n`) que consiste de 0s (células libres) y 1s (obstacles).
Puedes moverte **up, down, left, right** en un paso.
Usted comienza en `(0,0)` y quiere alcanzar `(m‐1,n‐1) ` lo más rápido posible.

Se le permite destruir ** en la mayoría de los obstáculos 'k'** (convierte un 1 en un 0).
Si es imposible alcanzar la meta, vuelva `-1`.

■ *Examples*
■ 1. `grid = [[0,0,0],[1,0],[0,0],[0,1,1],[0,0]] ' `k = 1` → `6`
■ 2. `grid = [[0,1,1],[1,1],[1,0,0]] ' `k = 1` → `- 1

Constraints (`1 ≤ m,n ≤ 40`, `1 ≤ k ≤ m × n`).

-...

## יa name="key-insights" Login/a confianzaKey Insights – Estrategia No-Go

Silencio insight _ Por qué importa
Silencio...
Silencio **BFS garantiza el camino más corto** Silencio Porque cada movimiento tiene igual costo (1). Silencio
tención **El Estado debe incluir las eliminaciones restantes** Silencio La misma célula puede ser alcanzada por un camino que utilizó menos eliminaciones, dando más flexibilidad más adelante. Silencio
Silencio **Prune estados imposibilitados** Silencio Visitar una celda con *más* eliminaciones restantes siempre es mejor. Silencio
Silencio **3-D visitado array** Silencio Mantiene seguimiento de '(x, y, remaining_k)` combos, evitando el soplo exponencial. Silencio

-...

## יa name="algorithm-design"

1. ** Entrada pendiente** – `Estado(x, y, remaining_k, steps)`.
2. ** Visitado** – `visited[x][y][remaning_k]` (boolean).
3. **Initializar** – empujar `(0,0,k,0)`; marca visitada.
4. **Mientras que la cola no está vacía* *
* Pop front.
* If `(x,y)` is target → return `steps`.
* Para cada una de las 4 direcciones:
* Si fuera de los límites → saltar.
* Si la próxima célula es un obstáculo (`grid[nx][ny]=1`) y `remaining_k Conf0` → decrement and enqueue.
* Si la siguiente célula es libre (`grid[nx][ny]=0`) → encuue with same `remaining_k`.
* Encuue únicamente si ese estado no ha sido visitado todavía.
5. **Retorno `-1'** si BFS agota todas las posibilidades.

■ **Por qué 3-D visitó obras* *
■ Para una celda fija `(x,y)`, sólo importan las eliminaciones * más altas* restantes.
■ Si llegamos a la misma celda con menos eliminaciones restantes, no puede conducir a un mejor resultado.
■ Así almacenamos el recuento exacto que queda; la primera visita para cada `(x,y,remaining_k)` es óptima.

-...

## יa name="complexity-analysis"

Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio **BFS (3‐D visitado)** Silencio `O(m × n × (k+1))` caso peor (cada estado procesado una vez) Silencio `O(m × n × (k+1))` para visitar + cola  sometida

Con `m,n ≤ 40` y `k ≤ m × n`, esto es cómodamente dentro de los límites (vedad 40 × 40 × 1600 ♥ 2.5 M estados).

-...

## יa name="implementations" Login/a Confeccionado en 3 idiomas

#### ## 1down⃣ Java

``java
importar java.util*;

Solución de la clase pública {}
int final estático privado[][] DIRS
{1, 0}, {-1, 0}, {0, 1}, {0,1}
};

public int shortestPath(int[][] grid, int k) {
int m = grid.length, n = grid[0].length;
si 1) retorno 0;

booleano[][][] visitado = nuevo booleano[m][n][k + 1];
Queue Utilizar el Estado titular q = nuevo ArrayDeque corresponde();
q.offer(new State(0, 0, k, 0));
[0][k] = verdadero;

(!q.isEmpty()) {
State cur = q.poll();
int x = cur.x, y = cur.y, remaining = cur.rem, steps = cur.steps;

para (int[] d : DIRS
int nx = x + d[0], ny = y + d[1];
si (nx ; 0 Новыные ные ные ные ные ные ные ные нных ненные ные ные неные ныеные неных неные ныеный ный continuar ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный

siguiente Rem = restante;
si (grid[nx] [ny] == 1) {
si (se mantiene == 0) continuar;
siguiente Rem...
}

si (nx == m - 1 " ny == n - 1) pasos de retorno + 1;
si (!visited[nx][ny][nextRem]) {}
visitado[nx][ny][nextRem] = verdadero;
q.offer(Nuevo Estado(nx, ny, siguiente Rem, pasos + 1));
}
}
}
retorno -1;
}

Estado de clase estática privada {
int x, y, rem, steps;
Estado(int x, int y, int rem, int steps) {}
this.x = x; this.y = y; this.rem = rem; this.steps = steps;
}
}
}
`` `

■ **Por qué está limpio** – "visitado" es un "boolean" 3-D, la cola almacena un `Estado ligero.
■ La matriz 'DIRS' mantiene la lógica del movimiento separada.

-...

#### 2down⃣ Python

``python
de las colecciones importa
de la importación Lista

Solución de clase:
DIRS = [(1,0), (-1,0), (0,1), (0,-1)]

def shortestPath(self, grid: List[List[int], k: int) - confianza int:
m, n = len(grid), len(grid[0])
si m == 1 y n == 1:
retorno 0

visitados = [[False] * (k+1) para _ en rango(n)] para _ en rango(m)]
q = deque([(0, 0, k, 0)]) # (x, y, remaining_k, steps)
[0][k] = True

mientras q:
x, y, rem, steps = q.popleft()
para dx, tio en ti mismo. DIRS:
nx, ny = x + dx, y + dy
si 0 0 0 0 0 0 0 0 0 0 0 0 0
siguiente_rem = rem
si la cuadrícula[nx] [ny] == 1:
si rem == 0:
continuar
next_rem -= 1
si nx == m-1 y ny == n-1:
pasos de retorno + 1
si no es visitado[nx][ny][next_rem]:
[nx][ny][next_rem] = True
q.append(nx, ny, next_rem, steps + 1))
retorno -1
`` `

■ **Tocados pitónicos** – `deque` para O(1) pops/pushes, comprensión de lista para 3-D visitados.

-...

#### 3down⃣ C++

``cpp
#include יbits/stdc++.h
usando std namespace;

struct State {}
int x, y, rem, steps;
Estado(int _x, int _y, int _rem, int _steps)
: x(_x), y(_y), rem(_rem), steps(_steps) {}
};

Clase Solución {
const int DIRS[4][2] = {1,0},{-1,0},{0,1},{0,-1}};
public:
int shortestPath(vector seleccionadovector seleccionador)
int m = grid.size(), n = grid[0].size();
si 1) retorno 0;

vector de vectores seleccionados visitado(
m, vector asignadovector seleccionadobool confianza(n, vector asignadobool confianza(k+1, false)
);
q);
q.emplace(0, 0, k, 0);
[0][k] = verdadero;

(!q.empty()) {
State cur = q.front(); q.pop();
int x = cur.x, y = cur.y, rem = cur.rem, steps = cur.steps;

para (auto &d : DIRS) {
int nx = x + d[0], ny = y + d[1];
si (nx ; 0 Новыные ные ные ные ные ные ные ные нных ненные ные ные неные ныеные неных неные ныеный ный continuar ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный

int next_rem = rem;
si (grid[nx] [ny] == 1) {
si (rem == 0) continuar;
Next_rem...
}

si (nx == m-1 " ny == n-1) pasos de retorno + 1;
si (!visited[nx][ny][next_rem]) {}
[nx][ny][next_rem] = true;
q.emplace(nx, ny, next_rem, steps + 1);
}
}
}
retorno -1;
}
};
`` `

■ **C+++-style** – una `estructura' que contiene sólo tipos primitivos, `vector` para 3-D visitado, `cuue` para BFS.

-...

## יa name="buen-bad-ugly"] Dijo/a ConfíaThe Good, The Bad, and The Ugly

← Stage ← Lo que es bueno para la vida Qué evitar (Bad)
Silencio----------------------------------------
← **Data‐Structure Choice** Silencio 3‐D visitado → O(1) look‐ups Silencio Usando un *set de tuples* (`(x,y,rem)`) en Python añade un factor de registro y retrasa la memoria. Silencio Declarando `int[][][]` en Java y olvidando multiplicarse por `(k+1)` conduce a `ArrayIndexOutOfBoundsException`. Silencio
Silencio ** State Pruning** Silencio Check `if !visited[nx][ny][next_rem] antes de encuuear Silencio Neglecting this results in *duplicate work* (exponential time). Silencio Destruyendo un obstáculo pero aún encendiendo el *same* `(x,y,rem)` estado → interminables lazos. Silencio
Silencio **Early Exit** Silencio Regresar inmediatamente una vez que usted pop el objetivo Silencio Regresar sólo después de los acabados del bucle puede perder la solución más corta. tención Olvídate de manejar el caso de borde de rejilla `1×1` → respuesta incorrecta en pequeña prueba. Silencio
Silencio **Estilo de codificación** Silencio Mantener direcciones en una constante separada, utilizar `estructura / clase de datos' para el estado Silencio de mezcla con I / O caldera hace que la depuración sea difícil. tención Usando recursión + memoización (DFS) en lugar de BFS → difícil de demostrar la optimización. Silencio

■ **Bottom line** – A *correct* BFS + 3-D visitado es elegante y rápido.
■ Los enfoques “muy” (DFS + memo, cola prioritaria con “k” como prioridad) pueden pasar pequeñas pruebas pero no en el peor de los casos, y son más difíciles de explicar en una entrevista.

-...

## יa name="seo-summary" Login/a Confeso-Ready Summary for Interviewers

- **Keyword‐dense headline**: “Shortest Path in Grid with Obstacles Elimination – LeetCode 1293 – BFS / Java / Python / C+”
- **Descripción de los datos**:
■ “Aprenda la solución LeetCode 1293 más dura en tres idiomas. Entiende por qué BFS + 3-D visitado es óptimo, y descubre trampas comunes que pueden hacer o romper su entrevista de codificación. ”
- **Los puntos de contacto para los gerentes de contratación**:
* Uso correcto de BFS para caminos más cortos
* Rastreo estatal adecuado (células + eliminaciones restantes)
* matriz visitada de memoria 3-D eficiente
* Manejo por caso de borde (1×1 cuadrícula, sin obstáculos, `k=0`)

■ Presentando una solución multilingüe *polished* y discutiendo los aspectos “buenos, malos, feos”, demuestras no sólo habilidad algorítmica sino también la mentalidad de ingeniería de software** —exactamente lo que buscan los entrevistadores.

-...

## יa name="resources" Leer más " Recursos "

Silencioso recursos
Silencio...
[LeetCode 1293 – Discussion](https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/discuss/) soluciones de la comunidad, trucos de persianas
Silencio [Graph BFS Basics – Big O](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) tención BFS fundamentals tención
[Tree‐Dimensional Visited Array Pattern](https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/discuss/520876/3-D-visited)
(https://leetcode.com/tag/graph/) ← Más preguntas difíciles basadas en la red

-...

#### TL;DR for Your Resume / Portfolio

*“Resolví LeetCode 1293 (Shortest Path in a Grid with Obstacles Elimination) utilizando un BFS óptimo que rastrea las obstaliminations restantes en un array visitado en 3-D. La solución funciona en el tiempo y la memoria de `O(m·n·k), trabaja en Java, Python y C++, y es una entrevista probada.*

Añadir esto a tu **GitHub Gist**, **LeetCode Profile**, o **coding‐interview blog** para mostrar a los reclutadores que estás listo para los desafíos de la investigación gráfica.

Buena suerte – y recuerde: *BFS + estado* es la receta para todos los problemas de cuadrícula más cortos! 🚀