-...
Título: LeetCode 3286. Encontrar un seguro caminar a través de una rejilla -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 3286 – “Encontrar una caminata segura a través de una cuadrilla”
*Java / Python / C++ Soluciones + In‐Depth Blog Post*

-...

## TL;DR
- ** Objetivo: * Comenzar en `(0,0)`, terminar en `(m-1,n‐1) ` manteniendo la salud 0 después de pisar cada celda.
- Pérdida de salud: " 1 " punto para cada célula insegura (grid[i][j]=1 " ).
- **Retorno:** 'verdad' si existe un camino seguro, de lo contrario `falso'.

** Estrategia óptima**
1. **BFS con estado (row, col, remainingHealth). #
2. **Mantenga la mejor salud que hemos visto en cada célula** – sólo re-queue cuando llegamos con *más* salud.
3. **Tiempo:** `O(m × n × salud)` (≤ 50 × 50 × 100 ♥ 250 000).
4. **Espacio:** `O(m × n)` para la mejor tabla de salud.

También mostraremos una alternativa *DP* (0‐1 BFS) que funciona en `O(m × n)`.

-...

## 1. Aspectos Algorítmicos

Silencio Silencio Silencio Silencio
Silencio...
Silencio **BFS** garantiza que exploremos primero la trayectoria de pérdida de salud *cortada*. Silencio ** Explosión estatal** si mantenemos ingenuamente todo valor de salud → soplamiento de memoria. ← **Recursivo DFS + memo** puede causar desbordamiento de la pila en las redes 50×50. Silencio
Silencio **Visitar con salud máxima** evita revisitar una célula con salud inferior o igual. Silencio **Edge caso:** La célula inicial puede ser insegura – debemos restar que la pérdida antes de BFS. Falta de comprobación de `saludRemanente √≥ 0` después de cada movimiento conduce a falsos positivos. Silencio
tención **0‐1 BFS DP** convierte el problema en “mínimo número de células inseguras a lo largo de cualquier camino”. TEN **DP sólo funciona cuando conoce el coste óptimo** (aquí 0/1 cuesta). ← **Large la memoria para 3-D dp** (`m×n×salud`) es innecesaria y lenta. Silencio

-...

## 2. Soluciones de referencia

A continuación encontrará implementaciones limpias y idiomáticas en **Java, Python, y C++**.

■ **Todas las soluciones asumen que la cuadrícula de entrada es no vacía y rectangular. #
" La salud " está garantizada a ser " 1`.**

-...

### 2.1 Java – BFS con poda “mejor salud”

``java
importar java.util*;

Solución de la clase pública {}
// direcciones: arriba, abajo, izquierda, derecha
int final estático privado[][] DIRS = {-1,0},{0},{0,-1},{0,1}};

encontrar booleano públicoSafeWalk(ListectoListectoList madeInteger confianza grid, int health) {}
int m = grid.size();
int n = grid.get(0).size();

// Salud inicial después del paso a la célula de inicio
int startLoss = grid.get(0).get(0);
si (salud 0= startLoss) devuelve falso;
int start Salud = salud - empezar Pérdida;

// bestHealth[i][j] = máxima salud cuando llegamos a la celda (i,j)
int[][] bestHealth = nuevo int[m][n];
for (int[] row : bestHealth) Arrays.fill(row, -1);

Queue hizo [] confiar q = nuevo ArrayDeque correspondió();
q.offer(nueva int[]{0, 0, startHealth});
bestHealth[0] [0] = startHealth;

(!q.isEmpty()) {
int[] cur = q.poll();
int r = cur[0], c = cur[1], h = cur[2];

si (r == m - 1 ' p == n - 1) retorno verdadero; // alcanzado meta

para (int[] d : DIRS
int nr = r + d[0];
int nc = c + d[1];
si (nr < 0 Новыный nr не= m удующенный nc неныеные n) continúan;

int loss = grid.get(nr).get(nc);
int nh = h - la pérdida;
si (nh <= 0) continuar; // moriría
si (nh י= bestHealth[nr][nc]) continúan; // no mejora

bestHealth[nr] [nc] = nh;
q.offer(new int[]{nr, nc, nh});
}
}
volver falso; // no camino
}
}
`` `

**Por qué funciona* *

* La cola garantiza que exploramos células en orden creciente del *número de pasos tomados*, no salud.
* Las ciruelas de la tabla "bestHealth" revisitan a menos que lleguemos con *más* salud que antes.
* Debido a que cada célula está enqueued en la mayoría de los tiempos `salud', el algoritmo funciona lo suficientemente rápido para las restricciones.

-...

### 2.2 Python – BFS + mejor tabla de salud

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def find SafeWalk (self, grid: List[List[int]], health: int) Bool:
m, n = len(grid), len(grid[0])
start_loss = grid[0][0]
si la salud se realiza= start_loss:
Retorno Falso
start_health = salud - start_loss

mejor = [1] * n para _ en rango(m)]
best[0][0] = start_health
q = deque([(0, 0, start_health)]

dirs = [(-1, 0), (1, 0), (0, -1), (0, 1)]

mientras q:
r, c, h = q.popleft()
si r == m - 1 y c == n - 1:
Retorno
para dr, dc en dirs:
nr, nc = r + dr, c + dc
si 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
pérdida = rejilla[nr][nc]
nh = h - pérdida
si no
continuar
[nc]:
continuar
mejor[nr][nc] = nh
q.append(nr, nc, nh))
Retorno Falso
`` `

-...

### 2.3 C++ – BFS con prioridad sobre la salud restante

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
bool findSafeWalk(vector seleccionadovector seleccionado) {}
int m = grid.size(), n = grid[0].size();
int start Pérdida = rejilla [0][0];
si (salud 0= startLoss) devuelve falso;
int start Salud = salud - empezar Pérdida;

vector se llevó a cabo el título de propiedad intelectual mejor(m, vector seleccionado(n, -1));
queue obedeció,int,int,int
q.emplace(0,0,startHealth);
mejor[0][0] = startHealth;

const int dr[4] = {-1,0,0};
const int dc[4] = {0,0,-1,1};

(!q.empty()) {
auto [r,c,h] = q.front(); q.pop();
si (r===m-1 ' p=n-1) regresan verdaderos;
para (int k=0;k obtenidos4;+k) {}
int nr=r+dr[k], nc=c+dc[k];
si (nr identificado0 vidas eternanr confianza=m permanecen intencionadamente) continuar;
int loss = grid[nr][nc];
int nh = h - la pérdida;
si (nh won=0) continúan;
si (nh י= best[nr][nc]) continúan;
mejor[nr][nc] = nh;
q.emplace(nr,nc,nh);
}
}
devolver falso;
}
};
`` `

-...

## 3. A DP (0‐1 BFS) Alternative

El BFS anterior ya es óptimo, pero a muchos entrevistadores les gusta ver un *disnamic-programming* eliminado:
“Encontrar el número mínimo de células inseguras (`grid[i][j]==1`) a lo largo de cualquier camino. ”

Si ese mínimo es " k " , sólo necesitamos " salud " (porque cada célula insegura deduce un punto de salud).

## 3.1 ¿Por qué 0‐1 BFS?
* Cada movimiento cuesta `0` (célula segura) o `1` (célula insegura).
* Standard Dijkstra sería exagerado; 0‐1 BFS utiliza una cola de doble duración para procesar los bordes cuesta-0 antes de los bordes costo-1, dando tiempo lineal.

#### 3.2 Java implementation

``java
importar java.util*;

clase pública SolutionDP {}
int final estático privado[][] DIRS = {-1,0},{0},{0,-1},{0,1}};

encontrar booleano públicoSafeWalk(ListectoListectoList madeInteger confianza grid, int health) {}
int m = grid.size(), n = grid.get(0).size();
int[][] dist = new int[m][n];
para (int[] fila : dist) Arrays.fill(row, Integer. MAX_VALUE);

Deque cumplimentint[] confianza dq = nuevo ArrayDeque correspondió();
int startLoss = grid.get(0).get(0);
si (salud 0= startLoss) devuelve falso; // no puede incluso pisar el comienzo

dist[0][0] = startLoss; // costo incluye la célula de inicio
dq.offerFirst(new int[]{0,0});

mientras (!dq.isEmpty()) {
int[] cur = dq.pollFirst();
int r = cur[0], c = cur[1];

para (int[] d : DIRS
int nr = r + d[0], nc = c + d[1];
si (nr < 0 Новыный nr не= m удующенный nc неныеные n) continúan;
int add = grid.get(nr).get(nc);
int nd = dist[r][c] + add;
si (nc) {}
[nr][nc] = nd;
(add == 0) dq.offerFirst(new int[]{nr,nc});
dq.offerLast(new int[]{nr,nc});
}
}
}
// dist[m-1][n-1] = mínimo # de células inseguras en cualquier camino
salud de retorno > dist[m-1][n-1];
}
}
`` `

### 3.2 Versión de pitón

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def find SafeWalk (self, grid: List[List[int]], health: int) Bool:
m, n = len(grid), len(grid[0])
INF = 10**9
dist = [[INF]*n for _ in range(m)]
dist[0][0] = grid[0][0]
dq = deque([(0,0)])

dirs = [(-1,0),(1,0),(0,-1),(0,1)]

mientras dq:
r,c = dq.popleft()
para dr, dc en dirs:
nr, nc = r+dr, c+dc
si 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
cost = grid[nr][nc]
nd = dist[r][c] + costo
si nd  se hizo dist[nr][nc]:
[nr][nc] = nd
si cuesta == 0:
dq.appendleft(nr,nc))
más:
dq.append(nr,nc))

salud de retorno
`` `

**La complejidad* *

* **Tiempo:** `O(m × n)` - cada célula procesada al máximo dos veces (una vez por un '0' borde, una vez por un '1' borde).
* **Espacio:** `O(m × n)` – una simple serie 2-D de números mínimos de células no seguras.

-...

## 4. Lista de verificación Edge‐Case

Silencio Caso confidencialidad Cómo manejar la vida ¿Por qué importa
Silencio...
Silencio **Iniciar la célula insegura** ¦ Subtract its loss *before* BFS. Silencio Incapacidad para hacerlo volverá `verdad` incluso si muere inmediatamente. Silencio
Silencio ** La salud es exactamente igual a la pérdida** Silencio Regresar `false`. El problema explícitamente dice que la salud debe permanecer ** 0**.
Silencio ** Celular de Objetivo inseguro** Silencio Garantizar `mantener la salud - grid[goal]  Si ignoramos la pérdida en la celda final, podemos pensar que existe un camino cuando es fatal. Silencio
Silencio **Large health** Silencio No hay manejo especial – la mesa de poda se encarga de ella. Sólo las células que mejoran la salud se vuelven a clasificar, por lo que la memoria permanece `O(m × n)`. Silencio

-...

## 5. Consejos para entrevistas

Silencioso Code Snippet Silencio Por qué es útil
Silencio----------------------------
Silencio **Explicar el estado** – `(r, c, remainingHealth)` – **antes de que el buceo en el código. Silencio `int[] state = {r, c, healthLeft};`  Shows you understand the problem constraints. Silencio
Silencio **Mostrar la idea de podar** – “Mantendremos la mejor salud para cada célula”. Silencio `si (nh י= bestHealth[nr]) continúan;` Silencio Recorta la reexploración innecesaria. Silencio
Silencio **Mandle the starting cell explicitly**. Silencio `int startHealth = health - grid[0][0];` Silencio Muchos candidatos olvidan esto, llevando a errores sutiles. Silencio
Silencio **Mención 0-1 BFS** como alternativa. Silencio `deque significaint[] confianza dq;` Silencio Demuestra la amplitud del conocimiento (DP + BFS). Silencio

-...

## 6. Pensamientos finales

* El enfoque BFS es **simple, rápido y garantizado correcto** bajo las limitaciones.
* La alternativa DP/0‐1 BFS es ideal para demostrar una visión de “memorización de costos”.
* Evite el DP 3-D o la repetición ingenua del DFS – son innecesarios y pueden engañar a los entrevistadores.

¡Buena suerte! 🚀

-...

### 7. Search‐Engine‐ Palabras clave listas

- LeetCode 3286
- Busca un paseo seguro a través de una cuadrilla
- Correción de salud BFS
- Programación dinámica BFS 0‐1
- Solución Java BFS LeetCode
- Python BFS
- C++ BFS con salud restante

-..