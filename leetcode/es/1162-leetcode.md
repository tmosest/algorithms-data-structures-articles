-...
Título: LeetCode 1162. Tan lejos de la tierra como es posible -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
"Tan lejos de la tierra como posible" – LeetCode 1162
**Medium ← BFS Silencio O(n2) tiempo Silencio O(n2) espacio**

■ ** Objetivo** – Para una cuadrícula cuadrada `n × n` de `0`s (agua) y `1`s (tierra), encontrar una célula de agua cuya distancia de Manhattan a la célula de tierra de *nearest* es **maximizada**.
■ Devuelve esa distancia máxima o `-1` si la cuadrícula contiene sólo tierra o sólo agua.

-...

### 📌 Why This Problem Rocks for Interviews

Silencio Silencio Silencio Silencio
Silencio...
Silencio **Intuitive** – Multi-source BFS es un ajuste natural. Silencio **Edge‐case prone** – Empty land/water grids or all‐land/all-water grids require special handling. Ø **Memory overhead** – Robar una matriz visitada duplica el costo de memoria (`O(n2)` extra. Silencio
Silencio **Reusable** – La misma plantilla de BFS resuelve muchos problemas de “distancia al objetivo más cercano”. tención **Límites de tiempo** – Para `n = 100` el BFS toca 10.000 células, que está bien, pero la recursión ingenua (DFS) puede soplar la pila. TEN **Introducción útil** – Algunas soluciones modifican la red de entrada para ahorrar espacio, pero que generalmente se desalienta en entrevistas. Silencio

-...

## 🔍 Declaración de problemas (parafraseada)

■ **Input**: `int[] [] grid`, `n = grid.length` (`n == grid[i].length`), `grid[i][j] ANTE {0, 1}`.
■ **Output**: `int` - la distancia más grande de Manhattan de cualquier célula de agua a su célula terrestre más cercana, o `-1' si no existe tal célula de agua.

■ **La distancia manhattan** entre `(x0, y0)` y `(x1, y1)` es `vivx0−x1 sobrevivir + prehensiy0−y1 sobrevivir`.

-...

Intuición Estrategia de Alto Nivel

1. **Multi‐source BFS**
*Treat every land cell `(i, j)` as a source node. *
*Enqueue todas las células terrestres primero. *
2. ** Capa por expansión de capas* *
*Cuando se abre una celda, exploramos sus cuatro vecinos. *
*Si un vecino es agua (`0`), se descubre a distancia `current_distance + 1`. *
3. **Track the maximum distance**
* Cada vez que terminamos de explorar toda una capa BFS, aumentamos el contador de distancia. *
*El contador después de la última capa es la respuesta. *

Si no hay células terrestres (`queue vacía`) o cada célula es tierra (`tamaño de la cola == n2`), retornamos `-1`.

-...

## 📦 Implementation Details

Silencio Idioma Silencio Silencio
Silencio...
Silencio **Java** Silencioso Usar `Queue hicisteint[] ' o `ArrayDeque`. Mantenga un `boolean[][] visitado` o modifique la rejilla. Silencio
Silencioso **Python** Silencioso `colecciones. Deque` para la cola. Use la comprensión de lista para direcciones. Silencio
tención **C++** Silencioso `queue seleccionapair observadoint,intilo ``. Utilice un vector 2-D para `visited` o modificar `grid`. Silencio

Proporcionaremos *clean*, *commented* código para cada idioma.

-...

## 🧩 Code – Java

``java
importar java.util*;

*
* LeetCode 1162: Tan lejos de la tierra como posible
* BFS – multifuente (todas las células terrestres)
*/
Solución de la clase pública {}
int public maxDistance(int[] grid) {
int n = grid.length;
Queue hizo [] confiar q = nuevo ArrayDeque correspondió();
booleano[][] visitado = nuevo booleano[n][n];

// 1 Cambios en la cola
para (int i = 0; i)
para (int j = 0; j) {}
si (grid[i] [j] == 1) {
q.offer(new int[]{i, j});
visitado[i][j] = verdadero; // marca
}
}
}

Casos de borde: sin tierra ni agua
si (q.isEmpty() TENIDO q.size() == n * n) retorno -1;

int[] dx = {1, -1, 0, 0};
int[] dy = {0, 0, 1, -1};
distancia int = -1; // se convertirá en 0 después de la primera capa

// 3VIEW⃣ Standard BFS
(!q.isEmpty()) {
int sz = q.size();
distancia++; // estamos moviendo una capa más
para (int k = 0; k) {}
int[] cur = q.poll();
para (int dir = 0; dir 0); {}
int ni = cur[0] + dx[dir];
int nj = cur[1] + dy[dir];
si (ni י 0 TENIDO NO QUIEREN NO SON TENIDO EN TENIDO ANTE NO TENIDO SON) continúan;
si (visited[ni][nj]) continúan;
visitado[ni][nj] = verdadero;
q.offer(new int[]{ni, nj});
}
}
}
distancia de retorno;
}
}
`` `

-...

## 🧩 Code – Python

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def maxDistance(self, grid: List[List[int]) - int:
n = len(grid)
q = deque()

# 1ICK⃣ enqueue all land cells
para i en rango(n):
para j en rango(n):
[i] [j] == 1:
q.append(i, j))

No hay tierra ni agua
si no q o len(q) == n * n:
retorno -1

dirs = [(1,0), (-1,0), (0,1), (0,-1)]
dist = 1

# 3️ BFS
mientras q:
dist += 1
para _ en rango(len(q)):
x, y = q.popleft()
para dx, Dy en dirs:
nx, ny = x + dx, y + dy
si 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 y cuadrícula [nx] [ny] == 0:
grid[nx][ny] = 1 # marca visitada por la conversión a tierra
q.append(nx, ny))

Retorno
`` `

■ ¿Por qué mutamos a "grid"?
■ En Python es común mutar la entrada para evitar un array extra visitado.
■ En entrevistas, explíquese si se permite la mutación; de lo contrario, cree una matriz "visitada".

-...

## 🧩 Code – C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxDistance(vector seleccionadovector fielint ánimo limitado) {
int n = grid.size();
queue hacíapair se hacía,intentas
vector se llevó a cabobool confianza visitado(n, vector asignadobool confianza(n,false));

// 1 / ⃣ enqueue all land cells
para (int i=0;i obtenidos;i++){
para (int j=0;j obtenidos;j++){
(grid[i][j]==1){
q.emplace(i,j);
visitado[i][j]=true;
}
}
}

si (q.empty() ANTETENIDO (int)q.size() == n*n) devuelve -1;

int dirs[4][2] = {{1,0},{-1,0},{0,1}};
int dist = -1;

// 2down B BFS
(!q.empty()){
int sz = q.size();
dist++; // aumento de capa
para (int k=0;k
auto [x,y] = q.front(); q.pop();
para (auto &d: dirs){
int nx = x + d[0], ny = y + d[1];
si (nx obtenidos0 TENIDO NXE=n TENIDO TENIDO NOVEDIDO0 TENIDO SON TENIDO SON) continúan;
si (visited[nx][ny]) continúan;
visitado[nx][ny] = verdadero;
q.emplace(nx,ny);
}
}
}
de retorno;
}
};
`` `

-...

Análisis de la Complejidad

Silencio Silencio Silencio
Silencio...
Silencio **Tiempo** Silencio Cada célula es enqueuada/procesada al máximo una vez → `O(n2)` Silencio
Silencio **Espacio** Silencioso Queue + matriz visitada → `O(n2)` Silencio

¿Por qué no? óptima* *
■ La respuesta puede ser tan grande como `2n-2` (por ejemplo, toda la tierra en una esquina).
■ Cualquier algoritmo que lea toda la cuadrícula debe tocar cada celda → límite inferior `Ω(n2)`.

-...

## ⋅ Common Pitfalls

Silencio Pitfall Silencio
Silencio...
Silencio **Recursivo DFS** – apilar el desbordamiento en grandes rejillas
* Casos de pérdida de bordes* – todos los `0's o todos `1`s Silencio Explicablemente ver el tamaño de la cola antes de BFS
Silencio **Actualización de la cuadrícula en su lugar** – puede violar las restricciones de entrevistas ← Crear una matriz "visitada" separada o preguntar si se permite la mutación
Silencio **El mostrador de distancia incorrecto** – empezando en `-1` vs `0` Silencio Inicializar `dist = -1` e incremento *después de procesar una capa

-...

## 📚 Variaciones " Extensiones

Silencioso Variación
Silencio--------------
TEN **Rejilla ponderada** – cada célula tiene un costo TENIDO Utilizar el algoritmo de Dijkstra en lugar de BFS TEN
tención **Diferente valor objetivo**
TEN **K‐th tierra más cercana** Silencio Guardar distancias en un vector, ordenar, a continuación, elegir el K‐th más pequeño TEN

-...

## 🚀 Ready‐to‐Deploy Checklist

1. **Elija BFS** – siempre la opción segura para problemas de distancia a distancia.
2. **Mandle all‐land / all‐water early** – esto ahorra mucha confusión.
3. **Clarificar reglas de mutación** – si la entrevista es estricta sobre la inmutabilidad de entrada.
4. **Comentar su código** – mostrar que usted entiende lo que cada bloque hace.
5. **Ejecutar la muestra* *

``java
int[][] grid = {{1,0,0},
{0,0,0},
{0,0,1}};
System.out.println(new Solution().maxDistance(grid)); // 2
`` `

-...

## 🎯 How to Ace the Interview

1. ** Explique la idea BFS primero** – muestra que conoce el paradigma algoritmo adecuado.
2. **Walk through edge cases** – demostrar que estás consciente de las condiciones `-1`.
3. **Write clear, typed code** – use una cola de plantilla, array de direcciones y un contador.
4. **Discuten alternativas** – “También podría mutar la cuadrícula para guardar la memoria, pero la mantendré pura aquí. ”

-...

### 👇 TL;DR

- Use **multi‐source BFS** - enqueue all land cells.
- Ampliar capa por capa, aumentando un contador de distancia.
- Regresar el contador después de la última capa (o `-1' para casos de borde).

■ Eso es todo lo que hay para “Estar lejos de la tierra” – simple, elegante y entrevista-listo!

Feliz codificación, y que sus respuestas siempre sean ** lo más lejos posible**! 🚀