-...
Título: LeetCode 1192. Conexiones críticas en una red -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Conexiones críticas en una red – LeetCode 1192
**Una profunda inmersión en puentes, el algoritmo de Tarjan, y cómo llegar a esta pregunta de entrevista* *

■ **Keywords:** *Conexiones verticales en una red, LeetCode 1192, hallazgo de puentes, algoritmo de Tarjan, fiabilidad de red, solución Java, solución Python, solución C++, entrevista de ingeniero de software, preparación de entrevistas de trabajo*

-...

## 1. Panorama general de los problemas

■ **LeetCode 1192 – Conexiones críticas en una red**
■ Dificultad:

Se le da un gráfico no dirigido y conectado con **`n`** nodos (servidores) numerados de **0** a ** n-1** y una lista de **`conexiones`** donde cada conexión es un array de 2 elementos `[a, b]`.
Una conexión **crítica** (o **puente**) es un borde que, si se elimina, aumenta el número de componentes conectados.
Devuelve todas las conexiones críticas en cualquier orden.

■ **Constraints**
≤ 105
* n - 1 ≤ conexiones. longitud ≤ 105
* 0 ≤ ai, bi
* ai ل bi
* No hay bordes duplicados

-...

## 2. ¿Por qué es difícil este problema?

Silencio Silencio Silencio Silencio
Silencio...
Silencio **Requiere comprensión de la teoría del gráfico** – no un simple DFS o BFS Silencio **La complejidad del tiempo** debe ser **O(V + E)** – la eliminación de la fuerza bruta de cada borde es O(V·E) Silencioso** riesgo de recidiva profunda sobre los gráficos esquejados
Silencio ** La elegancia algorítmica** – El algoritmo de Tarjan es un clásico Silencio **Large tamaños de entrada** – la profundidad de la recursión puede llegar a 105 Silencio ** Casos de emergencia** – nodos aislados, múltiples componentes, auto-ops (no se permite aquí pero vale la pena la pena la custodia)
Silencio **Entrevistas le encanta** – escaparate problemas–solving, estructuras de datos TEN ** Necesidad para la lista de adyacencia** – mal uso puede llevar a la memoria soplo TEN **Testing** – muchos casos sutiles; debe validarse contra la suite de pruebas LeetCode ¦

-...

## 3. Core Idea – Algorithm de búsqueda de puente de Tarjan

1. **Traversal de las Fuerzas de Defensa** con sellos (`tin`) cuando se visita por primera vez un nodo.
2. ** Valor de enlace inferior** ( " bajo[u] " ) = menor número de veces que se puede alcanzar de `u ' utilizando ** en la mayoría de un borde trasero**.
3. Al explorar un borde `u → v ' (del borde del árbol), después de regresar de `v ' , si `low[v] ¢ tin[u]`, el borde `(u, v)` es un puente.
4. Para los bordes traseros, actualice `low[u]` con `tin[v]`.

Esto se ejecuta en **O(V + E)** tiempo y **O(V + E)** memoria (lista de adyacencia + pila de recursión).

-...

## 4. Aplicación del Código

A continuación encontrará soluciones limpias y listas de producción en **Java, Python y C+**.
Los tres utilizan la misma lógica de Tarjan, son comentados para la claridad, y manejan las máximas restricciones con seguridad.

-...

#### 4.1 Java 17

``java
importar java.util*;

*
* LeetCode 1192 – Conexiones críticas en una red
*
* Hora : O(V + E)
* Espacio : O(V + E) (lista de adyacencia + pila de recursión)
*/
Clase Solución {
Lista privada realizadaLista realizada Resultado de Integer confianza; // lista de puentes
lista privada hecha Integer confianza[] gráfico; // lista de adjacency
int privado[] estaño; // tiempo de entrada
int privado[] bajo; // valores de bajo enlace
temporizador privado int;

public List armonizado(int n, Lista seleccionadaList madeInteger títulos) {}
// Construir la lista de adjacency
gráfico = nuevo ArrayList[n];
para (int i = 0; i) no; i++) grafo[i] = nuevo ArrayList fiel();
para (Lista realizadaInteger conn : conexiones) {}
int u = conn.get(0), v = conn.get(1);
graph[u].add(v);
graph[v].add(u);
}

estaño = nuevo int[n];
bajo = nuevo int[n];
Arrays.fill(tin, -1); // -1 = no previsto
timer = 0;
resultado = nuevo ArrayList garantizado();

// El gráfico está garantizado para estar conectado, pero corremos DFS desde 0
dfs(0, -1);

Resultado de retorno;
}

dfs(int u, int parent) {
tin[u] = bajo[u] = timer++; // set timestamps
para (int v : graph[u]) {}
si (v == padre) continuar; // no regresar a padre
(tin[v] == -1) { // borde del árbol
dfs(v, u);
baja[u] = Math.min(low[u], baja[v]);
si (low[v] {}
result.add (Arrays.asList(u, v)); // (u, v) es un puente
}
# Si no #
bajo[u] = Math.min(low[u], tin[v]);
}
}
}
}
`` `

-...

### 4.2 Python 3.10+

``python
de la importación Lista

Solución de clase:
"
LeetCode 1192 – Conexiones críticas en una red
Hora : O(V + E)
Espacio : O(V + E)
"
def criticalConnections(self, n: int, connections: List[List[int]]) - No. List[List[int]]:
# Build adjacency list
graph = [[] for _ in range(n)]
para u, v en conexiones:
graph[u].append(v)
graph[v].append(u)

estaño = [-1]
bajo = [0]
timer = 0
puentes = []

def dfs(u: int, parent: int) - titulado Ninguno.
temporizador no local
tin[u] = bajo [u] = temporizador
timer += 1
for v in graph[u]:
si v == padre:
continuar
si lata [v] == -1:
dfs(v, u)
bajo[u] = min(low[u], bajo[v]
si bajo[v] √≥ tin[u]:
puentes.append([u, v])
otra cosa:
bajo[u] = min(low[u], tin[v]

dfs(0, -1)
puentes de retorno
`` `

■ **Consejo:** En LeetCode, establecer un límite de recursión superior (`sys.setrecursionlimit(200000)`) si usted golpeó un error de profundidad de recursión.

-...

#### 4.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

*
* LeetCode 1192 – Conexiones críticas en una red
* Hora : O(V + E)
* Espacio: O(V + E)
*/
Clase Solución {
public:
vector realizador identificadoint títulos claveConnections(int n, vector seleccionado, vector seleccionadovector fieltint conexiones) {}
// Construir la lista de adjacency
vector seleccionado(n)
para (auto &e : conexiones) {}
int u = e[0], v = e[1];
graph[u].push_back(v);
graph[v].push_back(u);
}

vector implicado(n, -1), bajo(n, 0);
int timer = 0;
vectores obtenidos mediante puentes >

función recomendadavoid(int,int) ratio dfs = [ cl](int u, int parent) {
tin[u] = bajo [u] = temporizador++;
para (int v : graph[u]) {}
si (v == padre) continúan;
(tin[v] == -1) { // borde del árbol
dfs(v, u);
bajo[u] = min(low[u], bajo[v]);
si (low[v]
puentes.push_back({u, v});
# Si no #
bajo[u] = min(low[u], tin[v]);
}
}
};

dfs(0, -1); // grafito está conectado
puentes de retorno;
}
};
`` `

-...

## 5. Ejecutando las Soluciones en las Pruebas de Muestra

Silencio Lengua tóxica examen Silencioso
Silencio--------------
[0,1],[2,0], [1,3], [[1,3]] Silencio
TENIDO Python TENIDO Mismo TENIDO `[1,3] Silencio
TENIDO C++ TENIDO Mismo TENIDO `[1,3] Silencio

Los tres producen el puente(s) esperado, independientemente del orden.

-...

## 6. Lista de verificación Edge‐Case

1. ** Perdida individual** (`n = 2`, `[0,1]] → siempre un puente.
2. ** Gráfico totalmente conectado** (grafo completo) → sin puentes.
3. **Graph con múltiples componentes** (aunque el problema garantiza conectividad).
4. **Recidiva profunda** (gráfico de cadena) → límite de recursión / tamaño de pila.
5. **Large `n`** (105) → no se requiere BFS iterativa; la profundidad de recursión equivale a `n` en el peor de los casos; el tamaño típico de la pila (~1 MB) es suficiente para 105 en la mayoría de las plataformas.

-...

## 7. Why This Algorithm Rocks in Interviews

- ** patrón algorítmico clásico** (DFS + bajo enlace) que muestra el conocimiento profundo del gráfico.
- **Clear explanation**: puede caminar un reclutador a través de `tin`, `low`, y la condición del puente.
- **Scalable**: se ajusta a las limitaciones de LeetCode y a los sistemas de producción.
- **Reutilizable**: el mismo núcleo funciona para *puntos de articulación*, *hermanos fuertemente conectados*, etc.

-...

## 8. SEO‐Optimized Takeaway Paragraph

Si se está preparando para una entrevista de ingeniería de software, masterización **Conexiones Críticas en una Red (LeetCode 1192)** es una necesidad. Este problema duro prueba su comprensión del algoritmo de determinación de puentes **, **FDS traversal**, y ** valores de enlace lento**. Mediante la implementación de soluciones limpias en **Java, Python, y C++**, usted demuestra versatilidad y profundidad: los traidores clave buscan. Asegúrese de destacar su capacidad para manejar grandes entradas, evitar los desbordamientos de pila, y explicar la intuición del algoritmo. Estos puntos te separarán y ayudarán a aterrizar ese trabajo.

-...

#### TL;DR

- Use ** algoritmo de Tarjan** para encontrar puentes en O(V + E).
- Aplicar en **Java, Python, o C+** con listas de adyacency.
- Profundidad de recursión manual y grandes entradas cuidadosamente.
- Muestra la solución en tu entrevista para impresionar a los gerentes de contratación.

¡Feliz codificación y buena suerte en tu próxima entrevista!