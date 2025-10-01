-...
Título: LeetCode 2242. Máxima puntuación de una secuencia de nodos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recapitulación del problema – LeetCode 2242
**Maximum Score of a Node Sequence**

■ *Se le da un gráfico no dirigido con nodos (0-basados).
■ Cada nodo `i` tiene una puntuación `scores[i]`.
■ Una * secuencia de nodos válida* de longitud 4 satisfies: *
■ 1. cada par de nodos consecutivos está conectado por un borde
■ 2. ningún nodo aparece dos veces
■
■ Devuelve la suma máxima posible de los cuatro puntajes.
■ Si no existe una secuencia válida, vuelva `‐1`. *

`4 ≤ n ≤ 5·104`, `edges.length ≤ 5·104`, `1 ≤ puntuaciones[i] ≤ 108`.

-...

## 2. El “bueno, el malo y el ugly” de una fuerza bruta

Silencio **Method** Silencio**
Silencio----------------------------------------------------
Silencio Enumerate cada 4-nodo caminar Silencio fácil de implementar Silencio `O(n4)` – imposible para `n=5·104` Silencio Tiempo-out en los datos reales
TEN DFS with pruning TENED Reduce ramificación TEN aún exponencial en el peor de los casos Ø Código complejo, difícil de depurar
Silencio Programación dinámica en subconjuntos ← Precisse ← Requiere `2n` la memoria Silencio No es factible

Los tres enfoques son demasiado lentos o demasiado de memoria. La clave para una solución aceptada es **evitar explorar todo el espacio de búsqueda**.

-...

## 3. Insight – “Mantenga sólo los 3 mejores vecinos”

Considere un borde `(u, v)`.
Si estamos buscando una secuencia de 4-nodos `a – u – v – b`, entonces:

* `a` must be a neighbour of `u` (different from `v`).
* `b` must be a neighbour of `v` (different from `u`).

Para maximizar la puntuación total sólo necesitamos emparejar `u` con sus **tres vecinos más destacados**, y de manera similar para `v`.
¿Por qué?
Porque los otros dos nodos de la secuencia son `a` y `b`.
Si guardamos a los tres mejores vecinos por cada nodo, garantizamos que al menos uno de ellos será distinto del vecino del otro lado y del propio `u` o `v`.
(Si un nodo tiene menos de tres vecinos, los guardamos a todos).

Así el algoritmo se convierte en:

1. Construir listas de adyacencia.
2. Para cada nodo, mantenga los índices de sus 3 mejores vecinos (por puntuación).
3. Por cada borde `(u, v)` iterate over the top 3 neighbours of `u` and `v`.
* Skip duplicate indices or when a neighbour equals the other endpoint.
* Computar la puntuación `scores[u] + puntuaciones[v] + puntuaciones[a] + puntuaciones[b].
* Mantenga el máximo.

La obra es `O(n + m + 9m)` ♥ `O(n + m)` (la constante 9 viene de 3 × 3 cheques por borde), fácilmente ajustando las limitaciones.

-...

## 4. Análisis de la complejidad

Silencio ** Métrico** Silencioso **Java** Silencio**
Silencio----------------------------------------------------------
TENIDO Tiempo TENIDO `O(n + m)` Silencio `O(n + m)` Silencio
TENIDO Espacio TENIDO `O(n + m)` Silencio `O(n + m)` Silencio

Tanto el tiempo como el espacio son lineales en el tamaño de entrada – la complejidad asintotica óptima para este problema.

-...

## 5. Aplicación del Código

A continuación encontrará un código limpio y listo para la producción en **Java, Python, y C++** que sigue la estrategia superior a 3.

## 5.1 Java (Java 17)

``java
importar java.util*;

Solución de la clase pública {}
máximo Score(int[] scores, int[] edges) {
int n = scores.length;
// Construir listas de adyacency y mantener a los 3 vecinos por nodo
Lista hecha[]]] propiedad[] top = nuevo ArrayList[n];
para (int i = 0; i) no; i++) top[i] = nuevo ArrayList recomendado();

// minutos temporales para mantener las 3 puntuaciones principales
Lista de preciosPrioridadQueue cumplió[] título pq = nuevo ArrayList fiel(n);
para (int i = 0; i)
pq.add(new PriorityQueue incorrecta(Comparator.comparingInt(a - título a[1]))); // min‐heap on score
}

// Poblar montones
para (int[] e : bordes) {
int u = e[0], v = e[1];
pq.get(u)offer(new int[]{v, scores[v]});
pq.get(v).offer(new int[]{u, scores[u]});
si (pq.get(u).size()
si (pq.get(v).size() √° 3) pq.get(v).poll();
}

// Extraer los 3 vecinos principales
para (int i = 0; i)
(!pq.get(i).isEmpty() {)
top[i].add(pq.get(i).poll());
}
// reverso para tener la puntuación más alta primero (opcional)
Collections.reverse(top[i]);
}

int best = -1;
para (int[] e : bordes) {
int u = e[0], v = e[1];
para (int[] a : top[u]) {}
int aIdx = a[0];
si (aIdx == v) continúan;
para (int[] b : top[v]) {}
int bIdx = b[0];
si (bIdx == u Новывые bIdx == aIdx) continúan;
int score = scores[u] + puntuaciones[v] + puntuaciones[aIdx] + puntuaciones[bIdx];
mejor = Math.max(mejor, puntuación);
}
}
}
devolver mejor;
}
}
`` `

## 5.2 Python (Python 3.10)

``python
importación heapq
de las colecciones importadas por defecto
de la importación Lista

Solución de clase:
def máximo Score(self, scores: List[int], edges: List[List[int]) - título int:
n = len(scores)

# Min‐heaps for each node to keep top 3 scores
heap = [] for _ in range(n) ]

para u, v en los bordes:
heapq.heappush(heap[u], (scores[v], v)
heapq.heappush(heap[v], (scores[u], u)
si len(heap[u])
si len(heap[v])

# Convertir en listas clasificadas por puntuación decreciente
top = [ surtido(h, reverso=True) para h en montones]

mejor = 1
para u, v en los bordes:
para s_a, un arriba[u]:
si a == v: continuar
para s_b, b en top[v]:
si b == u o b == a: continuar
mejor = max(best, scores[u] + puntuaciones[v] + puntuaciones[a] + puntuaciones[b]

mejor
`` `

## 5.3 C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
máximo Puntaje(vector seleccionado), puntuaciones vectoriales obtenidos mediante: {}
int n = scores.size();
vectores obtenidosarrayos realizados, 3 títulos principales(n); // índices de los 3 vecinos principales
vector asignador implicado(n, {}) // tamaño real por nodo

// Min-heaps (score, neighbour)
vector asignadopriority_queue hizopair identificado,intilo, vector asignadopair realizadoint,intilos estrechos, mayor fieltro(n);
para (auto golpe e : bordes) {
int u = e[0], v = e[1];
minHeap[u].push({scores[v], v});
minHeap[v].push({scores[u], u});
si (minHeap[u].size()
si (minHeap[v].size()
}

// Extract top 3 neighbours for every node
para (int i = 0; i) {}
vector significado:
(!minHeap[i].empty() {
tmp.push_back(minHeap[i].top());
minHeap[i].pop();
}
// tmp ahora tiene vecinos en * orden de puntuación*
inverso(tmp.begin(), tmp.end()); // descending
para (auto golpe p : tmp) {
topSize[i].push_back(p.second);
}
}

int best = -1;
para (auto golpe e : bordes) {
int u = e[0], v = e[1];
para (int a : topSize[u]) {}
si (a == v) continúan;
para (int b : topSize[v]) {}
si (b == u Новывывывыеных b == a) continúan;
mejor = max(best, scores[u] + puntuaciones[v] + puntuaciones[a] + puntuaciones[b]);
}
}
}
devolver mejor;
}
};
`` `

■ **¿Por qué el código C+ es seguro para grandes entradas? #
< > > > > mantiene exactamente tres vecinos por nodo – ninguna asignación dinámica durante el bucle principal.
"priority_queue" es un montón de operaciones "O(log 3), es decir, tiempo constante.

-...

## 6. Artículo del Blog – “Cracking LeetCode 2242: 3-Neighbour Graph Algorithm”

### 6.1 Title (SEO‐first)

■ **LeetCode 2242 – “Maximum Score Node Sequence” – Java, Python & C++ Graph Solution for Interview Success**

### 6.2 Meta‐Descripción

■ Aprende a resolver LeetCode 2242 en tiempo O(n+m).
■ Limpie Java, Python, y C++ código, además de una profunda inmersión en el truco del vecino top‐3.
■ Perfecto para cualquier persona que se prepare para entrevistas de ingeniería de software o una publicación de trabajo grafico-algoritmo.

Artículo 6.3

`` `
# LeetCode 2242: Maximum Score of a Node Sequence – A Job‐Ready Graph Trick

Cuando miras un problema de LeetCode que parece *graph‐heavy*, es tentador pensar que la fuerza bruta es la única manera.
Pero para **Maximum Puntuación de un Node Sequence** (problema 2242) el truco óptimo es *pequeño* – **Mantenga a los 3 mejores vecinos**.

¿Por qué necesitamos los 3 mejores?
Porque cualquier camino de cuatro nodos `a‐u‐v‐b` sólo se preocupa por dos vecinos: `a ` (por `u') y `b` (por `v`).
Si guardamos a los tres mejores vecinos por cada nodo estamos garantizados para capturar lo mejor posible `a` y `b` sin mirar el gráfico entero.

A continuación se presenta la estrategia de 3 líneas:

1. Construir listas de adyacencia.
2. Por cada nodo, mantenga índices de sus **tres vecinos más destacados**.
3. Para cada borde `(u,v)` comprobar todos los pares 3×3 de estos vecinos, saltar duplicados, computar la puntuación y recordar el máximo.

El algoritmo es `O(n+m)` – tiempo lineal y memoria, que es perfecto para los límites (`5·104` nodos, `5·104` bordes).

## 1. Código - Java

``java
// Java 17 solución (ver código completo en la sección de respuesta)
máximo Score(int[] scores, int[] edges) { ... }
`` `

## 2. Código - Python

``python
# Solución Python 3.10 (ver código completo en la sección de respuesta)
Solución de clase:
def máximo Score(self, scores: List[int], edges: List[List[int]) - título int: ...
`` `

## 3. Código: C++

``cpp
// solución C+17 (ver código completo en la sección de respuesta)
clase Solución { public: int maximumScore(vector seleccionadoint círculo puntuados, vector identificadovector fieltradoncias) { ... } };
`` `

## 4. Por qué esto gana entrevistas

* **Simplicidad** – El algoritmo se reduce a dos lazos: uno a los vecinos de pre-proceso, uno a los bordes de verificación.
* **Scalability** – La complejidad lineal garantiza que incluso los casos de prueba más grandes terminen en milisegundos.
* Porteabilidad* La misma lógica funciona en Java, Python y C++ – ideal para una cartera de coding-interview.

Añada los fragmentos de código anteriores a su GitHub repo, etiquetarlos con `leetcode-2242`, `graph-algorithm`, `top-3-neighbours`, y tendrá una solución lista para aprobar la próxima entrevista.

-...

## 7. Pensamientos finales – La parte “Ugly”

Mientras que el truco top‐3 es elegante, todavía debe tener cuidado con:

* Nodos con **más de tres vecinos** – simplemente mantenerlos a todos.
* ** Índices Duplicados** – `a` podría ser igual `b`, o un vecino podría ser el otro punto final del borde.
* Integer overflow in Java or C++ (use `long`/`long` al summing four 108 scores).

Si saltas estos detalles obtendrás respuestas incorrectas en pruebas ocultas.

-...

#### TL;DR

*Problema 2242 se resuelve en tiempo lineal manteniendo sólo a los tres primeros vecinos de cada nodo.
La solución está disponible en Java, Python y C++ – copy‐paste en tu perfil de LeetCode o tu cuaderno de entrevista. *

-...

## Quick Links

Silencio Idioma Silencio Código Silencio
Silencio...
TEN Java ANTERIOR ANTERIEDEN DEtalles Haga clic para ampliar(a) (Código de Java) Silencio
TENIDO Python ANTERITO ANTERIDOS DE INFORMACIÓN Haga clic para ampliar(a) (Python code) Silencio
TENIDO C++ TENIDO ANTERIDOS DEtalles Haga clic para ampliar seleccionados/summary confidencial... (C++) Silencio

*(Reemplazar el “...” con la fuente completa mostrada arriba.) *

¡Feliz codificación, y que este top‐3 vecino te engañe ese próximo papel de ingeniería de software!