-...
Título: LeetCode 2146. K artículos más altos Rankeado dentro de un rango de precio -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Algoritmos – Aplicación de 3 idiomas

A continuación encontrará una implementación limpia y lista para la producción del problema ** "Most Valuable Path"** (LeetCode 2143) en **Java, Python y C+**.
Las tres soluciones siguen la misma estrategia de alto nivel:

1. **Breadth‐first search (BFS)** desde la celda de inicio – garantiza que visitemos las celdas para aumentar la distancia de Manhattan.
2. **Min‐heap / prioridad cola** que mantiene la siguiente celda para examinar de acuerdo con las cuatro reglas de clasificación
(distancia, precio, fila, columna).
3. Cuando el precio de una celda se encuentra en `[bajo, alto]` lo agregamos a la lista de respuestas hasta que tengamos resultados 'k'.

La aplicación utiliza una estructura " visitada " para evitar la revisitación de células (un "boolean[] " en Java/C++ y un " conjunto " en Python).
La complejidad es **O(N log N)** tiempo y **O(N)** espacio auxiliar, donde `N = R × C` (el número de células traversables).

-...

#### 1.1 Java

``java
importar java.util*;

Solución de la clase pública {}

dIR = {1, 0, -1, 0, 1};

public List made más altoRankedKItems(es)
int[][] grid, int[] pricing, int[] start, int k) {

int R = grid.length, C = grid[0].length;
int low = pricing[0], high = pricing[1];
int sx = start[0], sy = start[1];

// celdas visitadas
booleano[][] visitado = nuevo booleano[R][C];
visitado[sx][sy] = verdadero;

// Min-heap: {dist, price, row, col}
PriorityQueue madeint[]] jeap = new PriorityQueue贸 conveniente()
(a, b) - título a [0] != b[0] ? a[0] - b[0] :
a[1] ?= b[1] ? a[1] - b[1]
a[2] != b[2] ? a[2] - b[2] :
a[3] - b[3]);

// cola BFS
Queue hizo [] confiar q = nuevo ArrayDeque correspondió();
q.offer(new int[]{0, grid[sx][sy], sx, sy});

Lista realizadaLista realizadaInteger título ans = nuevo ArrayList recomendado();

mientras (!q.isEmpty() " vence uns.size()
int[] cur = q.poll();
int dist = cur[0], precio = cur[1], r = cur[2], c = cur[3];

si (bajo) = precio " precio " = alto) {
ans.add (Arrays.asList(r, c));
}

para (int d = 0; d)
int nr = r + DIR[d];
int nc = c + DIR[d + 1];
si (nr < 0 Новыный nr ненные ныенный noc неный неный ненный неный неный неный C) continuar;
si (grid[nr][nc] == 0 Silenciosos visitados[nr][nc]) continúan;
visitado[nr][nc] = verdadero;
q.offer(new int[]{dist + 1, grid[nr][nc], nr, nc});
}
}

devolver los ans;
}
}
`` `

*¿Por qué `PriorityQueue` + BFS? *
La cola de prioridad garantiza que las celdas estén en el orden correcto de las reglas de clasificación, mientras que BFS garantiza que visitemos las células en mayor distancia.
No se requiere ninguna clasificación de todas las células, por lo que el algoritmo se mantiene rápido incluso para el límite de 100 k-cell.

-...

### 1.2 Python

``python
importación heapq
de la lista de importación de escritura, Tuple, Set

Solución de clase:
def más alto RankedKItems(
auto,
grid: List[List[int],
precios: List[int],
start: List[int],
k: int
) - Lista de títulos [List [int]:
R, C = len(grid), len(grid[0])
bajo, alto = precio
Sx, sy = empezar

# Min‐heap: (distancia, precio, fila, col)
heap: List[Tuple[int, int, int, int] = [(0, grid[sx][sy], sx, sy)]
visitado: Set[Tuple[int, int] = {(sx, sy)}

ans: List[List[int] = []

mientras saltaba y se apoyaba
dist, price, r, c = heapq.heappop(heap)

si bajo / precio 0 = alto =
ans.append([r, c])

para dr, dc en ((1, 0), (-1, 0), (0, 1), (0, -1)):
nr, nc = r + dr, c + dc
si 0 0 0 0 0 0 0 0 0 0 0 0
y cuadrícula[nr] [nc] 0 y (nr, nc) no se visitan:
visitado.add(nr, nc))
heapq.heappush(heap, (dist + 1, grid[nr][nc], nr, nc)

Retorno
`` `

*¿Por qué un `set' para visitar? *
La cuadrícula puede ser tan grande como las células `1e5`; un `boolean[][]` consumiría una cantidad comparable de memoria. Un `set` de tuples mantiene el uso de la memoria apretado mientras proporciona O(1) mira-ups.

-...

#### 1.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

struct Node {}
int dist;
precio int;
int r, c;
Nodo(int d, int p, int rr, int cc) : dist(d), price(p), r(rr), c(cc) {}
};

struct cmp {}
bool operator()(const Node cosecha a, const Node cosecha b) const {
si (a.dist != b.dist) devuelve a.dist.
si (a.price != b.price) devuelve a.price b.Precio;
si (a.r != b.r) devuelve a.r.
devolver a.c.
}
};

Clase Solución {
public:
vector de vectores más altoRankedKItems(es)
vector identificador:
vector significado
vector asignadoint
int k) {

int R = grid.size(), C = grid[0].size();
int low = pricing[0], high = pricing[1];
int sx = start[0], sy = start[1];

vector secuestrador(C, false));
vis[sx][sy] = verdadero;

priority_queue obtenidosNodo, vector efectuadoNode confianza, cmp Conf.
queue hacíapair seleccionadaint,int titulada bfs; // tiendas coordenadas solamente
bfs.push({sx, sy});
int dist = 0;

// BFS para calcular la distancia a cada célula accesible
vector iniciado, intrínseco en relación con los principios = {1,0},{-1,0},{0,1},{0,-1};
vector se llevó a cabo injerto de confianza distMat(R, vector asignadoint confianza(C, -1));
distMat[sx][sy] = 0;

mientras (!bfs.empty()) {}
auto [x, y] = bfs.front(); bfs.pop();
int d = distMat[x][y];
int p = grid[x][y];
si (bajo) = p " p " = alto)
pq.emplace(d, p, x, y);

para (auto [dx, dy] : dirs) {
int nx = x + dx, ny = y + dy;
si (nx < 0 Наныенных не ные ный не ный не не ные ные ные ные ные ные ные ных не нене ные не не не ны ны не ный не ный ный не не ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный не не ный ный ный ный ный ный ный ный ный ный ный ный не ный ны C) continuar;
si (grid[nx][ny] == 0 Silencioso vis[nx][ny]) continúan;
vis[nx][ny] = verdadero;
distMat[nx][ny] = d + 1;
bfs.push({nx, ny});
}
}

vector realizador:
mientras (!pq.empty() " k--) {}
Nodo cur = pq.top(); pq.pop();
ans.push_back({cur.r, cur.c});
}
devolver los ans;
}
};
`` `

■ **Tip** – Si quieres evitar la matriz 'distMat', simplemente empuja la distancia junto con el nodo en la cola prioritaria como lo hacemos en las soluciones Java/Python. El recuento de capas BFS (`dist`) se puede aumentar en la mosca.

-...

## 2. Blog Post – “Cracking LeetCode 2143: Why BFS + Min‐Heap is the Secret Weapon”

### Title
**“BFS + Min‐Heap: Mastering LeetCode 2143 (Most Valuable Path) – 3-Language Deep Dive”**

## Meta‐Descripción
*“Solve el difícil problema LeetCode 2143 en Java, Python y C++ con un algoritmo probado. Aprenda las reglas de clasificación, por qué un min-heap importa, y cómo evitar trampas comunes. ¿Listo para impresionar a los reclutadores?”*

-...

#### 2.1 Introduction

Cuando golpeas el problema “Most Valuable Path” (LeetCode 2143), el primer instinto es a menudo “simplemente ordenar todas las células” o “utiliza el algoritmo de Dijkstra”. Ambos enfoques funcionan, pero son o bien *slow* para el límite de 100 k‐cell o *memory‐hungry*.

¿Y si hubiera un truco que garantice el tiempo **O(N log N)** y una pequeña huella de memoria? El truco es **Breadth‐First Search (BFS) + un Min‐Heap (priority queue)** – un patrón que reaparece en cada gran entrevista sistema-diseño y algoritmo.

-...

### 2.2 Problema Recap

■ *Se le da una cuadrícula rectangular, un rango `[bajo, alto]`, una posición inicial, y un número `k`.
■ Usted debe devolver las coordenadas de las primeras células 'k' que tienen un precio dentro del rango, ordenados por:*

1. * Distancia Manhattan desde el principio*
2. *Precio (primer trimestre)*
3. * Número real*
4. * Número de colon*

■ *Si hay menos de las células k ' son alcanzables, devuelve todas ellas. *

-...

### 2.3 ¿Por qué las reglas del ranking son cruciales

Las cuatro reglas significan que no puedes simplemente “tomar las células más baratas” – debes respetar la distancia primero.
Si lo clasificas todo por precio solo, romperás la regla #1.
Si usas BFS solo, romperás la regla #2–#4 porque tendrías que hacer un tipo adicional después de la traversal.

-...

### 2.4 El “bien” – Por qué Este enfoque funciona

TENIDO VALORAR Característica ANTERIOR Por qué es una victoria
Silencio...
Silencio **La distancia está garantizada** Silencio BFS visita las células capa por capa, por lo que la primera vez que llegamos a una celda ya sabemos que tiene la mínima distancia posible. Silencio
Silencio **Orden por precio / fila / col** Silencio Un min‐heap mantiene el *next* mejor celda en O(log N) tiempo. Nunca necesitamos clasificar toda la lista. Silencio
Silencio **Recuerdo luminoso** Silencio Sólo se almacena el conjunto de células visitadas (≤ 100 k). No denso `distMat` array necesario en Java/Python. Silencio
Silencio **Three language‐ready code** Silencio El patrón es el mismo en Java, Python y C++; los reclutadores les encanta ver que puede traducir algoritmos. Silencio

-...

### 2.5 El "Bad" – Errores comunes que rompen su solución

❌ Pitfall Silencio ¿Qué puede pasar mal? Silencio
Silencio...
Silencio **Usando un vector de tamaño R×C para distancia** Silencio En C++ o Java un array de 2-D de 100 k células todavía puede estar bien, pero si agrega otro `distMat` multiplica el uso de la memoria. Silencio
Silencio **No señalización visitada antes de empujar a la cola** Silencio Los empujes Duplicados pueden llevar a la explosión exponencial y apilar el desbordamiento. Silencio
Silencio **Comparando sólo la distancia en el montón** Silencio Si te olvidas de incorporar precio, fila o columna en la comparación, la respuesta será incorrecta. Silencio
Silencio **Using `pop()` en lugar de `top()`** Silencio En C++ debe aparecer sólo después de buscar el elemento; de lo contrario, el montón puede reducirse prematuramente. Silencio

-...

## ## 2.6 Los "Ugly" – Casos de borde que se hunden

Н вели нени ненный caso de Edge ный Cómo protegerse contra ella ные
Silencio------------------------
Silencio **El comienzo ya está fuera de alcance** Silencio El algoritmo todavía funciona: revisamos el precio *antes* ampliamos los vecinos. Silencio
Silencio **Todas las células son cero (inalcanzable)** Silencio La cola BFS terminará inmediatamente, y devolvemos una respuesta vacía. Silencio
Silencio es más grande que el número de células alcanzables** Silencio Simplemente devolvemos todas las celdas válidas – la condición de tiempo libre (`ans.size() ' ) se ocupa de esto. Silencio
Silencio **Large `R × C` pero pocas células alcanzables** Silencio Nuestro conjunto visitado mantiene la memoria baja; sólo las células alcanzables se insertan en el montón. Silencio

-...

### 2.7 Aplicación en 3 idiomas – Una referencia rápida

Silencio Idioma Silencio Key Data Structure Silencio Complejidad
Silencio--------------------------
Silencio Java ¦ `ArrayDeque` + `PriorityQueue madeint[] TENIDO O(N log N) ANTE
Silencio Python Silencio `heapq` + `set` Silencio O(N log N)
TENIDO C++ TENIDO `queue` + `priority_queue wonNode confianza` Silencio O(N log N) ANTE

■ **Pro tip:** Al escribir los elementos del montón, almacenar la distancia junto con el nodo. De esa manera evitas una matriz separada `distMat` y mantienes el limpiador de códigos.

-...

### 2.8 Pensamientos Finales – Consejos de Entrevista

1. ** Explique primero las reglas del ranking.** Los entrevistadores aman un modelo verbal claro.
2. **A través de las capas BFS** – mostrar que estás recogiendo la distancia *antes* empujas un nodo en el montón.
3. ** Destacar la comparación de min-heap** – es la * “salsa secreta”* que garantiza el orden de salida correcto.
4. **Mostrar las tres versiones del idioma** – esto demuestra tanto su capacidad de solución de problemas como su versatilidad como desarrollador.

-...

### 2.9 Call to Action

■ “¿Quieres aprender a resolver *cualquier problema de LeetCode duro con un código elegante y listo para la producción?
■ Suscríbete a mi newsletter para inmersiones semanales profundas, entrevistar vídeos de preparación y desafíos de codificación del mundo real. ”

Codificación feliz – y que sus huellas de pila siempre sean libres de errores! 🚀