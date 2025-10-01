-...
Título: LeetCode 2050. Cursos paralelos III -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Cursos paralelos III – LeetCode 2050
### From Concept to Code – Java, Python & C++

A continuación encontrará una solución **ready‐to-copy** en tres de los lenguajes de entrevista más populares, un artículo de blog profundo que explica el algoritmo, destaca el “bueno, el malo, el feo”, y está totalmente optimizado SEO para cualquiera que busque ence este problema de LeetCode o una entrevista de teoría gráfica.

-...

## Tabla de contenidos

TEN TERRITORIO TENIDO Enlace ANTE
Silencio...
tención 1️ Problema Reseña confidencialidad #problem-overview Silencio
Solución Idea Silencioso Silencio
Silencio 3️ Código Silencioso
Silencio 4️ Complejidad
Silencio 5️ Casos de bordes " Pitfalls "
Silencio 6️ Blog Artículo Silencioso #blog-article
TENIDO RESPUESTO ANTERIOR ANTERIOR

-...

Sinopsis del problema
** Cursos paralelos III (LeetCode 2050)**
*Hard – Gráfico Acíclico Dirigido (DAG) + Programación Dinámica*

■ *Se le dan cursos " n " , una lista de pares prerrequisitos " , y un array `tiempo ' donde `tiempo[i]` es la duración (en meses) por supuesto `i+1`.
■ Busque los meses mínimos requeridos para terminar todos los cursos si puede tomar cualquier número de cursos en paralelo mientras sus requisitos estén satisfechos. *

### Constraints
- 1 ≤ 5·104
- `0 ≤ relaciones. longitud ≤ 5·104 `
- `1 ≤ tiempo [i] ≤ 104
- El gráfico es un DAG – cada curso puede terminarse.

-...

## 2down I Solution Idea
El problema es esencialmente un ** "tiempo de finalización más temprano"** computación en un DAG.

1. ** Orden técnico** – Cursos de proceso sólo después de que todos sus requisitos estén terminados.
2. ** Programación dinámica en el DAG** –
* `start[i]` – el mes anterior se puede comenzar el curso *i*.
* `finish[i]` – el mes anterior se puede terminar el curso *i* (`start[i] + tiempo[i]`).

Durante un estilo de Kahn BFS:
- Por cada curso `u` saltó de la cola, propagar su tiempo de llegada a cada vecino `v`.
- Actualizar `start[v] = max(start[v], end[u]).
- Disminuir el grado de `v`; cuando llegue a cero, computar `finish[v] = start[v] + time[v]` y enqueue `v`.

La respuesta es el máximo 'finish[i]` sobre todos los cursos.

-...

## 3down Código

## Java 17

``java
importar java.util*;

Solución de la clase pública {}
int public int minNumberOfMonths(int n, int[][] relations, int[] time {)
// Construir la lista de adjacency y array indegree
Lista realizadaLista realizadaInteger confianza adj = nuevo ArrayList recomendado(n);
para (int i = 0; i < n; i++) adj.add(new ArrayList correctamente());
int[] indeg = nuevo int[n];
(int[] r : relations) {}
int u = r[0] - 1, v = r[1] - 1;
adj.get(u).add(v);
indeg[v]+;
}

// DP arrays
int[] start = new int[n];
int[] end = new int[n];
Deque cumplióInteger título dq = nuevo ArrayDeque correspondió();

// Inicia los cursos sin requisitos
para (int i = 0; i)
si (indeg[i] == 0) {
start[i] = 0;
[i] = tiempo[i];
dq.offer(i);
}
}

respuesta int = 0;
mientras (!dq.isEmpty()) {
int u = dq.poll();
respuesta = Math.max(respuesta, final[u]);

para (int v : adj.get(u)) {}
start[v] = Math.max(start[v], end[u]); // early start for v
indeg[v]--;
si (indeg[v] == 0) { // Todos los requisitos establecidos
[v] = start[v] + time[v];
dq.offer(v);
}
}
}
respuesta de retorno;
}
}
`` `

## Python 3.10

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def minNumberOfMonths(self, n: int, relations: List[List[int],
tiempo: List[int]) - Propiedad int:
adj = [[] for _ in range(n)]
indeg = [0] * n
por a, b en las relaciones:
adj[a-1].append(b-1)
indeg[b-1] += 1

inicio = [0]
* n
q = deque([i for i, d in enumerate(indeg) if d == 0])

para mí en q:
terminar[i] = tiempo[i]

respuesta = 0
mientras q:
u = q.popleft()
respuesta = max(respuesta, acabado[u])
for v in adj[u]:
start[v] = max(start[v], end[u])
indeg[v] -= 1
si indeg[v] == 0:
terminar[v] = start[v] + time[v]
q.append(v)

respuesta
`` `

### C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minNumberOfMonths(int n, vector asignadovector fieltro implicado relaciones, vector interpretadoint compartir tiempo) {
vector realizador realizado en el título adj(n);
vector implicado(n, 0);
para (auto &p : relaciones) {}
int u = p[0] - 1, v = p[1] - 1;
adj[u].push_back(v);
++indeg[v];
}

vector implicado(n, 0), final(n, 0);
queue indicaint
para (int i = 0; i)
si (indeg[i] == 0) {
[i] = tiempo[i];
q.push(i);
}

respuesta int = 0;
(!q.empty()) {
int u = q.front(); q.pop();
respuesta = max(answer, end[u]);

para (int v : adj[u]) {}
start[v] = max(start[v], end[u]); // early start
si 0) { // todos los prereqs terminados
[v] = start[v] + time[v];
q.push(v);
}
}
}
respuesta de retorno;
}
};
`` `

Los tres fragmentos se ejecutan en **O(n + m)** tiempo y **O(n + m)** memoria, ajustando fácilmente las limitaciones del problema.

-...

Complejidad

← Operación Silencioso
Silencio...
Silencio para construir gráfico Silencioso **O(n + m)**
Silencio Topological BFS > DP Silencio **O(n + m)** Silencio
Silencio total **O(n + m)**
← Memoria Silencioso **O(n + m)** (lista de asistencia + arrays DP)

`m = relations.length`, `n ≤ 5·104`, por lo que la solución es cómodamente rápida.

-...

## 5down Ed Edge Cases " Pitfalls

Escenario Silencioso Qué ver
Silencio--------------------------
Silencio **No hay requisitos** (`relations` vacio) Silencio Cada curso puede comenzar en el mes 0. Nuestra cola inicial maneja esto. Silencio
TEN **Multiple independent chains** TEN La respuesta es el tiempo máximo de acabado entre todas las cadenas. Silencio
Silencio **Large `time` values** (`≤ 104`) Silencioso Use `int` or `long` si prefiere seguridad; Java, Python, C++ asas de entrada hasta ~2·109. Silencio
tención **Tamaño gráfico cerca de los límites** Silencio Evitar la recursión (DFS) para evitar el desbordamiento de la pila. Nuestra solución BFS es iterativa. Silencio
TEN **Zero‐based vs one-based indices** ANTE Convert all course labels (`1...n`) to `0...n‐1` when building adjacency lists. Silencio

-...

Artículo del Blog
■ **Título**: “Parallel Courses III – Mastering DAG DP for Your Next Software‐Engineer Interview”

-...

#### 📌 Introducción
En entrevistas de ingeniería de software, los problemas que implican **graphs**, ** orderingtopological**, y **programación dinamica** son comunes. Uno de los desafíos más queridos de LeetCode es **Parallel Courses III (Problema 2050)** – un problema *hard* que te obliga a combinar el algoritmo de Kahn con DP en un DAG.

En este artículo, caminamos a través de la declaración del problema, ilustramos la idea algorítmica, comparamos las implementaciones “buenas” vs “malas”, y entregamos soluciones de producción en **Java, Python y C++**. También proporcionaremos palabras clave amigables con SEO para que los reclutadores que buscan la solución “Parallel Courses III” o “entrevista topológica de DAG” encuentren este post al instante.

-...

### 🔍 Resumen del problema (SEO-keywords: Cursos paralelos III, LeetCode 2050, DAG)

■ ** Objetivo**: Determinar los meses mínimos requeridos para terminar los cursos " n " donde cada curso toma un número determinado de meses y puede tener cursos previos.
■ **Constraints**:
* `1 ≤ n ≤ 5·104`
* `relations` es una lista de bordes dirigidos, tamaño `≤ 5·104`.
* El Gráfico es un DAG – cada curso puede terminarse eventualmente.

-...

### ♥ Solution Idea (SEO-keywords: topológica, programación dinámica, algoritmo de Kahn)

El corazón de la solución es ** "tiempo de acabado más temprano en un DAG"**:

1. **El orden técnico** asegura que los requisitos sean procesados antes de los cursos dependientes.
2. **DP on DAG** – propagar los tiempos de acabado de los requisitos a los dependientes, siguiendo el primer mes de inicio para cada curso.
3. **Respuesta** – el tiempo máximo de acabado en todos los cursos.

*Por qué esto es bueno*:
- **Tiempo de luz** - sin retroceso ni soplamiento exponencial.
- **Iterante** – seguro para entradas enormes, sin riesgo de desbordamiento de la pila de recursión.
- **Memory‐efficient** – lista de adjacency + dos arrays enteros.

*Por qué el DFS ingenuo con recursión es malo*:
- La profundidad de la recuperación puede alcanzar 50 000 → el flujo de la pila en Java o C++.
- Más difícil razonar sobre la superposición de subproblemas – tendría que fundir manualmente.

-...

### 🧠 Good vs. Bad Implementations

TENCIÓN TERRITORIO TENIENTES ANTE LAS CUENTAS
Silencio.
Silencio **Kahn + DP (nuestro BFS)** Silencio O(n + m), iterativa, separación clara de los tiempos “iniciados” y “acabados”. Silencio
TEN **DFS + Memoisation** ANTERITO Directo al código, utiliza la recursión. Riesgo de desbordamiento de pila; más difícil justificar la complejidad de los entrevistadores. Silencio
← **Brute‐Force DP** (lazos inclinados sobre todos los pares) ← Conceptualmente simple, pero O(n2). tención No aceptable para `n = 5·104`. Silencio

-...

### 📦 Code in Three Languages

*Los tres fragmentos de código arriba están completamente comentados y listos para una entrevista de pizarra blanca o una prueba de codificación. Puedes pegarlos a tu IDE favorito o al editor LeetCode. *

-...

### ⏱ Complexity (SEO-keywords: complejidad del tiempo, complejidad del espacio, O(n+m))

- **Hora**: `O(n + m)` – lineal en el número de cursos y pares prerrequisitos.
- **Espacio**: `O(n + m)` – lista de adjacency + arrays DP.

Debido a que el problema limita `n` y `m` a 50 000, la solución encaja cómodamente dentro de los límites de 1 s/512 MB de LeetCode.

-...

###  gradualmente Casos de Edge " Ugly " Pitfalls (SEO-keywords: casos de borde, corrección de errores, trampas de entrevista)

Silencioso caso Edge
Silencio...
Silencio No hay requisitos para vivir Semillas de cola inicial todos los cursos con `start = 0`. Silencio
tención etiquetas basadas en 1-basada tención Convertir a índices 0-basados inmediatamente. Silencio
Silencio Muy grande `tiempo` Silencio Mantenga los tipos de datos lo suficientemente grandes; en Java use `long` si lo desea. Silencio
Profundidad de Recursión ← Evite el DFS; utilice BFS (Kahn) para permanecer dentro de los límites de la pila. Silencio

-...

### 📄 Conclusión (SEO-keywords: preguntas de entrevista de gráficos, DAG DP, soluciones LeetCode, entrevista Java‐Python‐C++)

Cursos paralelos III es un gráfico *icónico* DP problem that showcases two essential interview skills:

1. **Ordenamiento técnico (Kahn)** – garantizando que respete los requisitos.
2. ** Programación Dinámica en DAGs** – computar los primeros tiempos de inicio / final.

Dominar este problema demuestra que puedes manejar DAGs de alto nivel** en un entorno de producción, una habilidad muy apreciada por los reclutadores en Google, Amazon, Microsoft y fintechs por igual.

Agregue el snippet a su GitHub repo, practique en DAGs aleatorio, y se sentirá confiado en cualquier “cursos paralelos” o “programación de cursos” pregunta de entrevista.

-...

#### 📈 Takeaway

- ** Iterative BFS + DP** → **O(n + m)**, seguro para 50 nudos k.
- Evitar la recursión → sin apilar desbordamiento.
- Convertir índices en 0-basado para la claridad.
- Destacar esta solución en su currículum o cartera como “Graph DP Expert”.

¡Feliz codificación! ▪

-...

## 7Ω⃣ Takeaway (SEO-keywords: preparación de entrevistas, problemas gráficos, entrevista de codificación)

*Cursos paralelos III es un ejemplo de libro de texto de **DAG + DP** en acción. Al presentar soluciones iterativas en Java, Python y C++, usted demuestra tanto el dominio del lenguaje como la profunda visión algoritmo —exactamente lo que buscan los reclutadores. *

Siéntete libre de copiar, retocar y ejecutar estas soluciones en LeetCode o durante las entrevistas simuladas. Y recuerde: ** algoritmos gráficos son el pan-y-butter de los roles de ingeniería de software senior**. ¡Buena suerte!