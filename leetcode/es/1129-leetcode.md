-...
Título: LeetCode 1129. Sendero más corto con colores alternativos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Solución de 3 idiomas a **LeetCode 1129 – Sendero más corto con colores alternativos* *

El objetivo: desde el nodo 0 encontrar la distancia más corta a cada nodo `x` cuando **no hay dos bordes consecutivos tienen el mismo color** (rojo ↔ azul).
Si un nodo no puede ser alcanzado bajo esa regla, la respuesta es `-1`.

La forma clásica es **Breadth‐First Search (BFS)** que mantiene la pista del *último color de borde usado*.

A continuación se presentan implementaciones limpias, listas para copiar en **Java, Python, y C++**.

-...

### 1.1 Java (Java 17)

``java
importar java.util*;

*
* LeetCode 1129 – Sendero más corto con colores alternativos
*/
Solución de la clase pública {}

/** enum para los dos colores del borde y un estado especial “inicial” */
privado enum Color { INIT, RED, BLUE }

int[] shortestAlternatingPaths(int n, int[][] redEdges, int[][] blueEdges) {
// lista de adjacency: nodo - lista de títulos (neighbor, edgeColor)
Lista realizada[] gráfico = nuevo ArrayList recomendado();
para (int i = 0; i < n; i++) graph.add(new ArrayList correctamente());

for (int[] e : redEdges) graph.get(e[0]).add(new int[]{e[1], Color.RED.ordinal()});
for (int[] e : blueEdges) graph.get(e[0]).add(new int[]{e[1], Color.BLUE.ordinal()});

int[] dist = nuevo int[n];
Arrays.fill(dist, -1); // -1 = not visited yet
[0] = 0;

// mantiene la cola (nodo, último color)
Deque cumplimentint[] confía q = nuevo ArrayDeque correspondió();
q.offer(nueva int[]{0, Color.INIT.ordinal()});

// visitado[nodo] [color] = verdadero si ya hemos procesado este estado
booleano[][] visitado = nuevo booleano[n][3];
[0] [Color.INIT.ordinal()] = verdadero;

(!q.isEmpty()) {
int[] cur = q.poll();
int u = cur[0];
int col = cur[1];
int step = dist[u] + 1;

para (int[] edge : graph.get(u) {
int v = edge[0];
int ec = edge[1];
// sólo podemos atravesar si el color del borde difiere del último usado
si (ec == col) continúan;
si (visited[v][ec]) continúan;

visitado[v][ec] = verdadero;
si (dist[v] == -1) dist[v] = step;
q.offer(new int[]{v, ec});
}
}

de retorno;
}

/* --- arnés de prueba rápida...
public static void main(String[] args) {
Solución s = nueva solución ();
int n = 3;
int[][] red = {0,1},{1,2}};
int[][] blue = {};
System.out.println(Arrays.toString(s.shortestAlternatingPaths(n, red, blue)));
// Se espera: [0, 1, -1]
}
}
`` `

**Las complejidades* *

Silencioso Complejidad
Silencio--------------------------
Silencio **O(n + E)** Silencio Cada nodo + borde se procesa una vez por color. Silencio
Silencio **O(n + E)** Silencio Extra arrays for adjacency, distance, visited. Silencio

-...

### 1.2 Python 3 (≥ 3.8)

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def más corto AlternatingPaths(
auto,
n: int,
redEdges: List[List[int],
blueEdges: List[List[int]
) List[int]:
# lista de adjacency: nodo - lista de títulos (neighbor, color)
graph = [[] for _ in range(n)]
para a, b en redEdges: graph[a].append((b, 0)) # 0 = rojo
para a, b en azulEdges: graph[a].append((b, 1)) # 1 = azul

[-1]
dist[0] = 0

# queue holds (node, last_color) last_color = -1 means “none”
q = deque([(0, -1)])
[False] * 3 for _ in range(n)] # 0: red, 1: azul, 2: init
visitado[0][2] = Verdadero

mientras q:
u, último = q.popleft()
paso = dist[u] + 1

para v, c en el gráfico [u]:
si c == último: # mismo color – saltar
continuar
if visited[v][c]:
continuar
visitado[v][c] = Verdadero
si se dist[v] == -1:
dist[v] = paso
q.append(v, c))

Retorno


# --- simple demo - Sí.
si __name_ == "__main__":
sol = Solución()
print(sol.shortestAlternatingPaths(3, [[0, 1], [1, 2]], [])
[0, 1, -1]
`` `

**Las complejidades* *

- Tiempo: `O(n + E)`
- Espacio: `O(n + E)`

-...

### 1.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector más corto Suplente Senderos(int n,
vector de vectores RedEdges,
vector realizador realizador implicado limitado azulEdges
// lista de adjacency: nodo - lista de títulos (neighbor, color)
vector realizador designadopair realizado,int hilo conductor g(n); // color: 0 = rojo, 1 = azul
for (auto &e : redEdges) g[e[0]].push_back({e[1], 0});
para (auto &e : blueEdges) g[e[0]].push_back({e[1], 1});

vector asignadoint -1);
[0] = 0;

// cola: (nodo, últimoColor) últimoColor = -1 ninguno
queue hacíapair se hacía,intentas
q.push({0, -1});

// visitado[nodo][color] – utilizamos 3 ranuras: 0,1,2 (2 = init)
vector realizadoarray obtenidosbool,3 confianza vis(n);
vis[0][2] = verdadero;

(!q.empty()) {
auto [u, last] = q.front(); q.pop();
int step = dist[u] + 1;

para (auto [v, col] : g[u]) {}
si (col == último) continuar; // mismo color – prohibido
si (vis[v][col]) continúan;
vis[v] [col] = verdadero;
si (dist[v] == -1) dist[v] = step;
q.push({v, col});
}
}
de retorno;
}
};

/* -------- Demo...
int main() {}
Solución s;
vector asignador implicado rojo = {0,1},{1,2};
vector realizador:
auto ans = s.shortestAlternatingPaths(3, rojo, azul);
para (int x : ans) cerrador
retorno 0;
}
*/
`` `

**Las complejidades* *

- Tiempo: `O(n + E)`
- Espacio: `O(n + E)`

-...

## 2. Blog Artículo – “Master LeetCode 1129: Sendero más corto con colores alternativos”

■ **Keywords**: LeetCode 1129, Sendero más corto con colores alternativos, BFS, gráfico, Java, Python, C++, entrevista de trabajo, desafío de codificación, algoritmo, búsqueda de empleo, entrevista técnica, impulso de carrera

-...

#### 2.1 Introduction

El problema “Shortest Path with Alternating Colors” es un favorito en la sección de entrevistas de LeetCode. Prueba dos habilidades básicas que los reclutadores se preocupan por:

1. **Traversal Gráfico** – especialmente BFS con estado.
2. ** Gestión estatal** – recordando el último color del borde para que usted no atraviesa dos bordes rojos o dos azules consecutivamente.

Si usted clavó este problema, usted tendrá un fuerte punto de conversación en su próxima entrevista. A continuación, caminamos por el *bueno*, el *bad*, y los aspectos *muy* de la solución, y proporcionamos códigos listos para copiar en **Java, Python y C+**.

-...

### 2.2 Problema Recap

■ **Input**
" n ": number of nodes (0‐based).
> `redEdges`: lista de bordes rojos dirigidos `[u, v]`.
" Azulejos " : lista de bordes azules dirigidos " [u, v] " .

■ **La salida*
■ Un array `respuesta` de longitud `n` donde `respuesta[x]` es la longitud del camino más corto de nodo 0 a nodo x, ** colores alternativos**, o `-1` si imposible.

■ **Constraints**
1 ≤ 100, bordes ≤ 400 cada uno.

-...

### 2.3 El Bien - ¿Por qué BFS es la herramienta correcta

1. **Exploción de capas**
BFS descubre naturalmente el camino más corto en un gráfico no ponderado porque explora todos los nodos a distancia `k` antes de moverse a `k+1`.

2. **Codificación del Estado**
Al adjuntar el “último color del borde” a cada estado apagado, mantenemos la búsqueda *color‐aware* sin volar el tamaño del gráfico.

3. **Simplicity " Readability* *
El algoritmo es unas líneas largas, y la complejidad es lineal en el número de bordes. Programador de amor limpio código que muestra que puede resolver un problema de manera eficiente.

4. **Idioma Agnostic**
La misma estrategia BFS-with‐color-state funciona sin cambios en Java, Python o C++ – una gran ilustración del pensamiento agnóstico del lenguaje.

-...

### 2.4 El malo – Pitfalls comunes

Silencio Pitfall Silencio Lo que sucede Silencioso
Silencio--------------------------
Silencio **Retirar “no color anterior” como 0 o 1** Silencio El nodo inicial puede tomar cualquier color; si usted trata el init como 0, usted bloquea por error el primer borde rojo. Use un tercer estado de “INIT” o use “-1” para “no color”. Silencio
Silencio **Procesamiento Duplicado de Edge** Silencio Sin una matriz visitada por color, el mismo nodo se puede encubrir infinitamente. Mantener `visitado[nodo][color]`. Silencio
Silencio **Actualización incorrecta de distancia** Silencio Actualizar `dist[v]` en cada visita puede establecer una distancia más larga más tarde. Sólo se establece `dist[v] ` cuando la primera vez que visita ese nodo (sin importar el color). Silencio

-...

### 2.5 The Ugly – Edge Cases that Obscure the Logic

Silencioso ¿Por qué es confuso?
Silencio------------------------------------
Silencio **Dos colores que se reúnen en el mismo nodo** – debes empezar con rojo, luego azul, luego rojo de nuevo. ← Revise explícitamente `ec != last` antes del traversal. Silencio
TEN **Gran número de bordes paralelos** TEN los bordes rojos pueden ser duplicados, o rojo y azul puede apuntar a la misma pareja. Utilice una matriz visitada para evitar volver a procesar el mismo par `(nodo, color). Silencio
Silencio ** Auto-loops** Silencio Un borde `[u,u]` de cualquier color puede ser atravesado, pero si es el primer borde, no se puede tomar un segundo loop de color. La misma regla de diferenciación de color se aplica; los auto-ops no romperán BFS. Silencio

-...

### 2.6 Step‐by‐Step Algorithm

1. **Construir la lista de adjacency**
`adj[u] = lista de (v, color)`. Color: 0 = rojo, 1 = azul.

2. ** Initializar**
`dist[0] = 0`, todos los demás `-1`.
La cola comienza con "(0, INIT)".

3. **BFS Loop**
`` `
mientras que la cola no está vacía:
u, últimoColor = cola.pop()
siguienteDist = dist[u] + 1
para (v, edgeColor) en adj[u]:
si el bordeColor == últimoColor: continuar
si es visitado[v][edgeColor]: continuar
visitado[v][edgeColor] = verdadero
si se dist[v] == -1: dist[v] = siguiente Dist
queue.push(v, edgeColor))
`` `

4. Retorno**.

La clave es que cada nodo puede ser alcanzado dos veces (una vez por rojo, una vez por azul). Es por eso que guardamos una matriz «visitada» de 3 columnas (también IINIT).

-...

### 2.7 Ready‐to‐ Código de copia – Tres idiomas

■ #Java #
■ [Véase la aplicación anterior](#1.1)

■ Python
■ [Véase la aplicación anterior](#1.2)

■ **C++**
■ [Ver más arriba la implementación](#1.3)

Copie la clase, déjela caer en su IDE, y ejecute los demos "mantenimiento". Estarás listo para discutir esto en una entrevista.

-...

### 2.8 Consejos para tu entrevista

1. **Hablar de la complejidad* *
“El BFS funciona en el tiempo de `O(n+E) y `O(n+E)` espacio. Con 'n ≤ 100', eso es trivial para los entrevistadores. ”

2. **Justificación del Estado* *
“Arreglamos el último color al estado para hacer cumplir la alternancia. Esto es similar a resolver el problema *“Viaje en carretera con tipos de combustible”*. ”

3. ** Casos de emergencia**
Mención: *Si `redEdges` o `blueEdges` está vacío, todavía encontramos un camino que utiliza el otro color o el retorno `-1`. *

4. # Explique Why `-1`**
“Si nunca pusimos `dist[v]`, el nodo es inalcanzable bajo la limitación de la alternancia. ”

-...

### 2.9 ¿Por qué esto aumenta tu búsqueda de empleo

- **Resolver el proyecto**: Mostrar reclutadores puede diseñar una solución eficiente para un problema de grafito no tripartito.
- ** Estilo de codificación**: código BFS limpio demuestra legibilidad, que es un gran plus en entrevistas de programación de pares.
- ** Flexibilidad en idioma**: Tener soluciones en Java, Python y C++ demuestra que no eres sólo un codificador de “un idioma”.
- **Confianza**: Saber discutir sobre el estado de BFS le ayudará a abordar preguntas similares de entrevista (por ejemplo, *“Paso más corto con los cambios K-color”*, *“Número mínimo de pasos para alcanzar el objetivo”*).

-...

### 2.10 Conclusión

El problema **Shortest Path with Alternating Colors** es más que un ejercicio de codificación; es un escaparate de madurez algorítmica.
Al dominar el patrón BFS-with-state y ser capaz de explicar las opciones de diseño *bueno*, te destacarás en entrevistas técnicas y ganarás una ventaja real en tu búsqueda de trabajo.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀

-...

*Si encontró útil este artículo, comparta en LinkedIn o Twitter usando las etiquetas anteriores. ¡Buena suerte en tu viaje de entrevista! *

-...

*End of article. *

-...

■ ¡Feliz codificación!
■ *No dude en adaptar los arnés demo a su propio marco de prueba. *

-...

## 3. Observaciones finales

Ahora tienes:

- **Tres soluciones de producción que pasarán todas las pruebas de LeetCode en minutos.
- Una inmersión profunda en la lógica algorítmica que los reclutadores aman.
- Un artículo **blog** para alimentar su marca personal en Linked En o un sitio web personal, completo con palabras clave relevantes para entrevistas.

Happy interview prep!

-...

*Todo el código y el artículo son código abierto; no dude en modificar y compartir. *