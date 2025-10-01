-...
Título: LeetCode 1135. Ciudades de conexión con coste mínimo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Connecting Cities With Minimum Cost – A Job‐Ready Guide
*(LeetCode 1135 – Árbol de recambio mínimo – Java, Python, C++)*

-...

## Por qué este problema importa

- Una estrella de entrevistas clásicas Prueba los fundamentos gráficos, algoritmos codiciosos y conocimiento de estructura de datos.
- **Real-world relevance** – Diseño de red, planificación de carreteras y minimización de costes de infraestructura en la nube son todos los problemas de “conexión de todas las ciudades”.
- Tres ángulos para mostrar - Puedes resolverlo con **Prim**, **Kruskal**, o incluso un híbrido **Union‐Find + Min‐Heap**.
- **SEO-ready** – “mínimo árbol de azotes”, “ciudades de conexión”, “Java MST”, “Python MST”, “C++ MST”, “LeetCode 1135” son palabras clave de alto tráfico que buscan los reclutadores.

-...

## The Good

Por qué es bueno
Silencio----------
Silencio ** Declaración de problemas claros** Silencio `n` ciudades, `m` carreteras bidireccionales con un costo → encontrar el costo mínimo para conectar todos. Silencio
Silencio **Restricciones limitadas** Silencio `n, m ≤ 10^4` → una solución `O(m log m)` es cómodamente rápida. Silencio
*“Construir el árbol más barato que abarca todos los nodos.”* Silencio
Silencio **Discusión de la entrevista de Rich** Silencio Puedes hablar de elección codictiva, detección de ciclos y pruebas de optimización. Silencio

-...

## El malo

Silencio Lo que puede morderte Silencio
Silencio...
Silencio ** Gráficos desconectados** Silencio Usted debe detectar que ningún árbol de azotes existe y regresar `-1`. Silencio
Silencio ** Pesos de bordes elevados** TENIDO Use `long` o `int` cuidadosamente para evitar el desbordamiento. Silencio
Silencio **Memory limits** Silencio Robar todos los bordes como una lista de arrays de 3 pulgadas está bien para 10^4, pero ten cuidado si te ajustas a las limitaciones. Silencio

-...

## El Ugly

Silencioso punto de dolor
Silencio...
Silencio **Off‐by-one indices** Silencio Las ciudades están basadas en 1-basados – mantener `parent[0]` no utilizado. Silencio
Silencio **Unión‐Encuentra error de compresión de ruta** ← Recursive `find()` con compresión de ruta o circuito iterativo; prueba siempre en un ciclo simple. Silencio
Silencio **PriorityQueue comparator pitfalls (Java)** Silencio Una lambda `(a, b) - título a[1] puede desbordarse; use `Integer.compare(a[1], b[1])`. Silencio
tención **C++ STL pitfalls** Silencio `std::sort` on vector of tuples; use `std::priority_queue` with `greater il título ``. Silencio
Silencio **Python list sorting overhead** Silencio Use `key=lambda e: e[2]` and `heapq` for Prim. Silencio

-...

## Solution Overview

Dos algoritmos de MST canónicos funcionan perfectamente aquí:

1. **Kruskal** – Ordenar todos los bordes por costo, añadir el borde más barato que no crea un ciclo (Union‐Find).
2. **Prim** – Empezar desde una ciudad arbitraria, tomar siempre el borde más barato dejando el conjunto visitado (min-heap).

Ambos dan el mismo costo total mínimo.
A continuación ofrecemos implementaciones limpias y listas de producción en **Java, Python, y C++**.

-...

## Java Implementation – Kruskal with Union‐Find

``java
importar java.util*;

Solución de la clase pública {}
// -------- Union-Find------------
clase privada UnionFind {
int privado final[] parent;
int final privado[] tamaño;
componentes privados de int; // número de conjuntos de disjoint

public UnionFind(int n) {}
padre = nuevo int[n + 1]; //
tamaño = nuevo int[n + 1];
componentes = n;
para (int i = 1; i) = n; i++) {
parent[i] = i;
tamaño[i] = 1;
}
}

int find(int x) {
si (parent[x] != x) {
parent[x] = find(parent[x]); // path compresión
}
devolver padre[x];
}

unión booleana pública(int a, int b) {}
int ra = find(a), rb = find(b);
si (ra == rb) devolver falso; // ya conectado
si (tamaño[ra]  se observó tamaño[rb]) { // unión por tamaño
tmp = ra; ra = rb; rb = tmp;
}
parent[rb] = ra;
tamaño[ra] += tamaño[rb];
componentes...
retorno verdadero;
}

public boolean allConnected() {}
componentes de retorno == 1;
}
}

--------- Función principal...
mínimo público Cost(int n, int[][] connections) {
// Ordenar los bordes por costo (k[2] = peso)
Arrays.sort(connections, (a, b) - título Integer.compare(a[2], b[2]));

UnionFind uf = new UnionFind(n);
long total = 0; // use long to avoid overflow

para (int[] e : conexiones) {}
int u = e[0], v = e[1], w = e[2];
(uf.union(u, v)) {
total += w;
}
}

uf.allConnected() ? (int) total : -1;
}

// -------- Arnés de prueba simple...
public static void main(String[] args) {
Solución s = nueva solución ();
int[][] conn1 = {1,2,5},{1,3,6},{2,3,1}};
System.out.println(s.minimumCost(3, conn1)); // → 6

int[][] conn2 = {1,2,3},{3,4};
System.out.println(s.minimumCost(4, conn2)); // → -1
}
}
`` `

*Puntos clave*

- `UnionFind` implementa la compresión *path* y *union por tamaño* para `α(n)` tiempo amortizado.
- La clasificación de bordes da `O(m log m)`.
- Complejidad: `O(m log m + m α(n)) ♥ O(m log m)`; Espacio: `O(n + m)`.

-...

## Python Implementation – Prim with Min‐Heap

``python
importación heapq
de las colecciones importadas por defecto
de la importación Lista

Solución de clase:
mínimo Cost(self, n: int, connections: List[List[int]]) - título int:
# Build adjacency list
gráfico = defaultdict(list)
para u, v, w en conexiones:
graph[u].append(w, v))
(w, u)

[False] * (n + 1)
min_heap = [(0, 1)] # (cost, vertex) – empezar desde la ciudad 1
total_cost = 0
edges_used = 0

mientras que min_heap y bordes_utilizados
w, u = heapq.heappop(min_heap)
si es visitado[u]:
continuar

visitado[u] = Verdadero
total_cost += w
edges_used += 1

por costo, v in graph[u]:
si no es visitado[v]:
heapq.heappush(min_heap, (cost, v)

devolver total_cost si edges_used == n otra -1

# ------------ Ejemplo------------
si __name_ == "__main__":
s = Solución()
[1, 2, 5], [1, 3, 6], [2, 3, 1]]
print(s.minimumCost(3, conn1)) # 6

[1, 2, 3], [3, 4, 4]]
print(s.minimumCost(4, conn2)) # -1
`` `

¿Por qué Prim? #

- No hay necesidad de ordenar toda la lista de bordes – usted consigue el siguiente borde más barato en `O(log m)` como usted atraviesa.
- Manijas gráficas desconectadas automáticamente: si el montón se vacía antes de que todos los vértices sean visitados, devuelve `-1`.
- Complejidad: `O(m log m)` (heap operations) - el mismo costo asintotico que Kruskal.
- Usa sólo bibliotecas integradas, por lo que es fácil de enviar a una plataforma.

-...

## C++ Implementación – Kruskal con `std::vector`

``cpp
#include יbits/stdc++.h
usando std namespace;

// -------- Disjoint Set Union...--------
Clase DSU {}
public:
vector implicado padre, sz;
int comps; // número de componentes

DSU(int n) : parent(n + 1), sz(n + 1, 1), comps(n) {}
iota(parent.begin(), parent.end(), 0); // 1-based, 0 unused
}

int find(int x) {
si (parent[x] != x)
parent[x] = find(parent[x]); // path compresión
devolver padre[x];
}

bool unite(int a, int b) {}
int ra = find(a), rb = find(b);
si (ra == rb) vuelve falso;
si (sz[ra] ) swap(ra, rb); // unión por tamaño
parent[rb] = ra;
sz[ra] += sz[rb];
-comps;
retorno verdadero;
}

bool connected() const { return comps == 1; }
};

// -------- Solución...
mínimo Costo(int n, vector asignadovector fielmente conectados) {}
(conexiones.begin(), connections.end(),
[](cont auto cho a, const auto golpe b){ devolver a[2]  obtenidos b[2]; });

DSU dsu(n);
long long total = 0;

para (auto pulsa e : conexiones) {}
int u = e[0], v = e[1], w = e[2];
si (dsu.unite(u, v) total += w;
}

dsu.connected() ? static_cast identificadoint(total) : -1;
}

// -------- Principal para pruebas rápidas----------
int main() {}
vector se llevó a cabo nombrando confianza conn1 = {1,2,5},{1,3,6},{2,3,1};
cout se realizó mínimoCost(3, conn1) se realizó el endl // 6

vector se llevó a cabo nombrando confianza conn2 = {1,2,3},{3,4,4};
cout se realizó mínimoCost(4, conn2) se realizó finall; // -1
retorno 0;
}
`` `

**Highlights* *

- Usa `std::vector` de vectores para mantener los bordes → `O(m)` memoria.
- `std::sort` da el `O(m log m)` requerido.
- La implementación del ESD es idiomática: iterativa `find()` + unión por tamaño.
- Funciona en índices urbanos basados en 1 sin ajustes adicionales.

-...

## Testing > Edge‐ Lista de verificación de casos

Silencio Test Silencio Resultado esperado Silencio Por qué importa
Silencio...
Silencio **Todas las ciudades ya conectadas** (p. ej., una sola carretera entre cada par) Silencio El costo mínimo equivale a la suma de los bordes más baratos `n-1`. Muestra que no estás exagerando. Silencio
Silencio ** Gráfico desconectado** – por ejemplo, dos racimos sin vínculo TEN Vuelta `-1`. ANTE Garantías que usted maneja el caso de “no azotes”. Silencio
Silencioso **Ciudad individual (`n = 1`)** Silencio Costo = `0`. Silencio Límite simple para evitar el arreglo fuera de lugar. Silencio
tención **Pesas altas** (hasta 10^6`) Silencio No hay desbordamiento al resumir (utilizar `long`/`int64`). tención Mantiene la solución correcta bajo todas las entradas. Silencio
Silencio **Los bordes Duplicados** Silencio Elige la más barata; los duplicados no afectan Union‐Find. Silencio Evita el uso innecesario de la memoria. Silencio
Silencio **Creación de ciclos** Silencio Union‐Find rechazará el borde. Silencio Garantiza la aciclicidad del árbol final. Silencio

-...

## Cómo vender este problema en una entrevista

1. *Explicar la idea principal*
■ “Necesitamos el árbol más barato que toca cada ciudad – eso es exactamente un árbol mínimo de spanning. ”

2. **Elija un algoritmo**
- Si prefieres * clasificación global* → hablar de Kruskal.
- Si te gusta * opciones codictivas locales* → hablar de Prim.

3. **Mostrar la prueba de corrección del ESD* *
- “Añadiendo bordes en orden creciente y rechazando cualquier que cerrara un ciclo, mantenemos la propiedad de la optimización probada por el teorema de corte. ”

4. **Manejo de la maleta de alta luz**
- “Si el número de componentes conectados es más de uno después de que todos los bordes sean considerados, el gráfico está desconectado; volvemos `-1`.”

5. **Discusión del tiempo y el comercio espacial**
- `O(m log m)` es el límite inferior teórico para clasificar los bordes, bien dentro de los límites 10^4.
- La huella de memoria es lineal: `O(n + m)`.

6. **Dar un código limpio snippet** – pegar el código Java (o su idioma preferido), caminar a través del DSU, y dejar que el reclutador vea que puede escribir código de grado de producción.

-...

## Final Thought

Mastering *Connecting Cities With Minimum Costo* demuestra que usted:

- Comprender la teoría del gráfico** y los algoritmos de inteligencia**.
- Puede implementar estructuras de datos ** eficientes** (Union‐Find, Min‐Heap).
- Puede anticipar las trampas (grafos desconectados, indexación de 1 base, desbordamiento).

Traiga este problema a su próxima entrevista técnica, y usted estará hablando de un algoritmo probado que resuelve desafíos de optimización de red en el mundo real – todo mientras utiliza las palabras clave que los reclutadores buscan. Buena suerte, y feliz codificación! 🚀

-..