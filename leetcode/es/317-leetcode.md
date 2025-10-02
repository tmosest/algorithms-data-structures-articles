-...
Título: LeetCode 317. Distancia más corta de todos los edificios -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 317. Distancia más corta de todos los edificios
**Hard – BFS + estrategia multifunción* *

■ **TL;DR** – Para cada edificio ejecuta un BFS para acumular la distancia a cada célula vacía, mantenga un contador de “reach” para saber cuándo una célula puede ver todos los edificios, y finalmente tomar la distancia mínima acumulada.

-...

### Code

A continuación se muestran **ready‐to‐paste** soluciones en **Java, Python y C++** que compilan con los compiladores estándar (Java 17, Python 3.10+, C++17).
Los tres utilizan el mismo algoritmo: para cada edificio ejecutar un BFS, añadir la distancia a cada tierra vacía alcanzable, contar cuántos edificios cada tierra vacía puede llegar, y finalmente elegir la célula vacía que puede alcanzar * todos* edificios con la suma más pequeña.

-...

#### Java 17

``java
importar java.util*;

Solución de la clase pública {}
privada estática final int[] DX = {0, 1, 0, -1};
privada static final int[] DY = {1, 0, -1, 0};

público más corto Distancia (int[][] grid) {
si (grid == null ¦ 0) retorno -1;
int m = grid.length, n = grid[0].length;

int[][] dist = nuevo int[m][n]; // distancia acumulada
int[][] alcance = nuevo int[m][n]; // cuántos edificios pueden llegar a esta celda
edificio int Cuenta = 0;

para (int i = 0; i)
para (int j = 0; j) {}
si (grid[i] [j] == 1) { /// un edificio
construcción Conteo++;
bfs(grid, i, j, dist, reach, m, n);
}
}
}

respuesta int = Integer. MAX_VALUE;
para (int i = 0; i)
para (int j = 0; j)
si (grid[i] [j] == [j] == buildingCount)
respuesta = Math.min(respuesta, dist[i][j]);

respuesta de retorno == entero. ¿MaX_VALUE? -1 : respuesta;
}

bfs vacío privado(int[][] grid, int sx, int sy,
int[][] dist, int[][]
int m, int n) {
booleano[][] visitado = nuevo booleano[m][n];
Queue hizo [] confiar q = nuevo ArrayDeque correspondió();
q.offer(nueva int[]{sx, sy});
visitado[sx][sy] = verdadero;
nivel int = 0; // distancia del edificio

(!q.isEmpty()) {
int size = q.size();
para (int i = 0; i) {}
int[] cur = q.poll();
para (int d = 0; d)
int nx = cur[0] + DX[d];
int ny = cur[1] + DY[d];
si (nx ; 0 Новыные ные ные ные ные ные ные ные нных ненные ные ные неные ныеные неных неные ныеный ный continuar ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный
si (grid[nx][ny] != 0 Silenciosos visitados[nx][ny]) continúan;
visitado[nx][ny] = verdadero;
dist[nx][ny] += nivel + 1;
[nx][ny]++;
q.offer(nueva int[]{nx, ny});
}
}
nivel++;
}
}

// Arnés de prueba rápido
public static void main(String[] args) {
int[][] grid1 = {
{1, 0, 2, 0, 1},
{0, 0, 0, 0, 0},
0, 1, 0, 0
};
System.out.println(new Solution().shortestDistance(grid1)); // 7

int[][] grid2 = {{1,0};
System.out.println(new Solution().shortestDistance(grid2)); // 1

int[][] grid3 = {{1};
System.out.println(new Solution().shortestDistance(grid3)); // -1
}
}
`` `

-...

##### Python 3.10+

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def más corto Distancia (yo mismo, rejilla: Lista [Lista [int]]] int:
si no cuadrícula o no cuadrícula[0]:
retorno -1

m, n = len(grid), len(grid[0])
dist = [[0] * n para _ en rango(m)] # distancia acumulada
alcance = [[0] * n para _ en rango(m)] # Cuantas construcciones pueden llegar
edificios = sum(row.count(1) for row in grid)

# Directions: right, down, left, up
dirs = [(0, 1), (1, 0), (0, -1), (-1, 0)]

para i en rango(m):
para j en rango(n):
[i] [j] == 1:
visitados = [[False] * n para _ en rango(m)]
q = deque([i, j, 0)]) # (x, y, distance)
visitado[i][j] = Verdadero

mientras q:
x, y, d = q.popleft()
para dx, Dy en dirs:
nx, ny = x + dx, y + dy
si 0 0 0 0 0 0 0 0 0 0
and grid[nx][ny] == 0 and not visited[nx][ny]:
visitado[nx][ny] = Verdadero
dist[nx][ny] += d + 1
[nx][ny] += 1
q.append(nx, ny, d + 1))

mejor = flotante('inf')
para i en rango(m):
para j en rango(n):
[i] [j] == 0 y alcance[i][j] == edificios:
mejor = min(best, dist[i][j])

retorno -1 si mejor == flotante('inf') mejor


# Demo
si __name_ == "__main__":
sol = Solución()
print(sol.shortestDistance([1, 0, 2, 0, 1], [0, 0, 0, 0, 0], [0, 0, 1, 0, 0]])
print(sol.shortestDistance([1, 0])) # 1
print(sol.shortestDistance([[1]]) # -1
`` `

-...

##### C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
más corto Distancia (vector seleccionador) {
si (grid.empty() TENIDO LA REDUCCIÓN [0].empty()) regresa -1;
int m = grid.size(), n = grid[0].size();

vector seleccionado(n, 0));
vector seleccionado(n, 0));
edificio int Cnt = 0;

const int dx[4] = {0, 1, 0, -1};
const int dy[4] = {1, 0, -1, 0};

para (int i = 0; i)
para (int j = 0; j)
si (grid[i] [j] == 1) {
++construcción Cnt;
bfs(grid, i, j, dist, reach, dx, dy, m, n);
}

int ans = INT_MAX;
para (int i = 0; i)
para (int j = 0; j)
si (grid[i] [j] == [j] == buildingCnt)
as = min(ans, dist[i][j]);

volver ans == INT_MAX ? -1 : ans;
}

privado:
vacío bfs(vector identificadovector fielint círculo, int sx, int sy,
vector asignador se llevó a cabo, vector se llevó a cabo,
const int* dx, const int* dy, int m, int n) {
vector asignadovector asignadobool confianza visitado(m, vector asignadobool confianza(n, false));
queue efectuastetuple observadoint,int,int
q.emplace(sx, sy, 0);
visitado[sx][sy] = verdadero;

(!q.empty()) {
auto [x, y, d] = q.front(); q.pop();
para (int dir = 0; dir 0);
int nx = x + dx[dir];
int ny = y + dy[dir];
si (nx ; 0 Новыные ные ные ные ные ные ные ные нных ненные ные ные неные ныеные неных неные ныеный ный continuar ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный
si (grid[nx][ny] != 0 Silenciosos visitados[nx][ny]) continúan;
visitado[nx][ny] = verdadero;
dist[nx][ny] += d + 1;
[nx][ny] += 1;
q.emplace(nx, ny, d + 1);
}
}
}
};

/ Demo
int main() {}
Sol de solución;
vector de vectores g1 = {1,0,2,0,1},
{0,0,0,0},
{0,0,0,0}};
cout se realizó el sol.shortestDistance(g1)

vector de vectores g2 = {{1,0};
cout se realizó el sol.shortestDistance(g2)

vector asignador implicado g3 = {1};
cout se realizó el sol.shortestDistance(g3)
}
`` `

-...

### Algoritmic Insight

##### 1. ¿Por qué BFS de cada edificio?

- BFS garantiza la distancia *cortada* a cada célula vacía accesible porque se expande uniformemente capa por capa.
- Para un edificio en `(sx, sy)`, la primera capa (distancia 1) es sus vecinos inmediatos, la segunda capa (distancia 2) es el siguiente anillo, etc.
- Añadiendo `(nivel + 1)` al array `dist` da la distancia correcta de Manhattan.

##### 2. Distancia acumulada + contador de alcance

- `dist[x] [y] almacena el **sum** de distancias de * todos* edificios que pueden alcanzar `(x, y)`.
- `reach[x] [y]` cuenta cuántos edificios alcanzaron `(x, y)`.
Sólo las celdas con `reach == totalBuildings` son candidatos válidos para la respuesta final.

##### 3. Complejidad

- Sea el número de edificios, `M × N` el tamaño de la cuadrícula.
Cada BFS visita cada celda vacía al máximo una vez: `O(M·N)` por edificio.
**Hora total**: `O(B · M · N)`.
En el peor de los casos (cada célula es un edificio excepto una célula vacía), `B ≤ M·N`, por lo que `O((M·N)^2) ` – todavía bien para las limitaciones (`M, N ≤ 50`).

- **Memoria**: tres matrices integer/boolean " M × N " .

##### 4. Casos de borde

- No hay tierra vacía accesible → respuesta `-1`.
- Todas las celdas son edificios o obstáculos → `-1`.
- Rejilla con `0`-células que pueden alcanzar *algunos* pero no *todos* edificios son automáticamente descartados por el mostrador de acceso.

-...

## El “bueno, malo, ugly” de la solución

Silencio, cariño.
Silencio...
tención ** Algorithm** tención Simplicidad: un BFS por edificio, no complicadas estructuras de datos. tención Potentially high constant factor: one queue per building. Silencio Ninguno – el BFS es limpio y determinista. Silencio
TEN **Readability** TEN Java: utiliza clases explícitas; Python: estilo funcional conciso; C++: amigable con plantillas.
tención **Performance** Silencioso rápido para la red 50×50 (caso inferior) se realizó 0.01 s en la práctica. Igual que Java. Silencio
tención **Memoria** tención 3 × M × N int + 1 × M × N bool ♥ 4 × 502 ♥ 10 kB.
tención **Scalability** tención Funciona hasta 200 × 200 (pero LeetCode max es 50). La vida misma.

-...

### Cómo utilizar en entrevistas

1. ** Explique la idea** primero: “Para cada edificio, ejecute un BFS y acumule distancias. ”
2. **Mostrar un idioma** (a menudo Java o Python) y *hand-write* la lógica básica.
3. **Discuten la complejidad** y por qué el algoritmo es óptimo para las limitaciones.
4. **Responde una pregunta de truco**: "¿Y si la cuadrícula no tiene 0-celular alcanzable por todos los edificios?" → respuesta `-1`.

-...

### Common Interview Questions Around This Problem

Silencio
Silencio...
*¿Qué pasa si `M` y `N` son 1000?* Silencio Necesita reducir el número de traversales de BFS; quizás un BFS multifuente de todos los edificios a la vez. Silencio
Silencio *¿Puedes encontrar la respuesta en el tiempo O(M·N)?* tención Imposible en el peor de los casos porque necesita saber distancias a cada edificio. Silencio
¿Qué pasa si los obstáculos son dinámicos?* Silencio Re-run BFS de células modificadas o mantener actualizaciones incrementales. Silencio
Silencio 4 Silencio *Parallelize the BFSes?* Silencio El BFS de cada edificio es independiente – puede usar hilos, pero tenga cuidado de las actualizaciones compartidas de `dist`/`reach`. Silencio
¿Por qué BFS y no DFS?* Silencio DFS no garantiza caminos más cortos en una cuadrícula no ponderada. Silencio

-...

## Qué hacer para alejarse

- Acumular** y contar** en un solo pase por edificio.
- **Reutilizar** la misma distancia y alcanzar matrices a través de todos los BFSes.
- **Compruebe** la condición *todas las construcciones* antes de tomar el min.
- **Hora/Espacio** son ambos O(M·N) por edificio - fino para el límite de 50×50 de LeetCode.

-...

## Next Steps

1. Practica este patrón en problemas similares de LeetCode:
* 317 – *La distancia más corta de todos los edificios* (el mismo problema).
* 1472 – *Optimal Train Timetable* (BFS con base en red).
* 317 – *Shortest Distancia de todos los edificios* (versión Java).
2. Trate de *optimizar* para rejillas más grandes utilizando **multi‐source BFS** o **prefix sums**.

-...

### El “bueno, malo, ugly” de la solución

Silencio, cariño.
Silencio...
Silencio **Readability** Silencio Straightforward BFS, claros nombres de variables. TENIDO Gran caldera (por ejemplo, matriz visitada por BFS). Silencio.
tención **Performance** tención Excelente para las limitaciones; cada BFS toca cada célula vacía sólo una vez. ← Iluminar el techo por edificio: crear una nueva matriz "visitada".
Silencio ** Memoria** Silencioso `O(M·N)` arrays; insignificante para los límites de LeetCode. La vida misma.
Silencio **Portabilidad** Silencio Trabaja en Java 17+ sin cambios. Silencio Funciona en Python 3.10+; no hay libs externas. Silencio

-...

## Final Thought

**La distancia más corta de todos los edificios de LeetCode** es un ejemplo de **multi‐source BFS** en una cuadrícula.
Un solo paso sobre la cuadrícula (contando edificios) + un BFS por edificio (acumulación de distancias y conteos de alcance) da la respuesta óptima.
Maestro este patrón, y usted va a romper muchas preguntas de entrevista basadas en la cuadrícula - y usted estará listo para impresionar con código limpio, multi-idioma durante su próxima entrevista. 🚀

¡Feliz codificación!