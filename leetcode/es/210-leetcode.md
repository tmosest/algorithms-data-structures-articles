-...
Título: LeetCode 210. Calendario del curso II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 210. Programación del curso II – Solución de nivel superior (Java / Python / C++)
#### ⏱י 3 minutes read ← | 3 languages Silencio 🚀 100 % test-coverage

-...

### ##  Settlement Problem Summary

■ **Given** cursos de `numCourses ' (0 ... numCourses‐1) y un array `prerequisites ' donde `prerequisites[i] = [a, b] ` significa curso de toma `b ' antes del curso `a`*,
■ **Retorno** *cualquier orden válido de cursos que satisfaga todos los requisitos.
■ **Si no existe ningún pedido (el gráfico contiene un ciclo), devuelve un array vacío.

■ **Constraints**
≤ 2000
* `0 ≤ requisitos. longitud ≤ numCourses · (numCourses - 1)`
* todos los pares son distintos, `a ل b`.

-...

## 🔬 Why it's a Graph Problem

Cada curso es un **vertex**.
Cada requisito " [a, b] " es un borde **directo** `b → a`.
Necesitamos una orden **topológica** del DAG (Grafo Acíclico Directado).
Si el gráfico contiene un ciclo, un orden topológico es imposible.

-...

## Dos enfoques clásicos

TEN TERRITORIO ANTERIOR Idea ANTERI
Silencio----------------------------
Silencio **El Algoritmo de Karen (BFS)** Silencio Mantener vértices con cero indegrejo en una cola, pop them, decrement indegree of neighbours.
TEN **DFS (Recursivo)** Silencio DFS-visit, empuje vertices sobre la pila cuando todos los niños visitados. Ciclo de detección a través de la pila de recursión. Tiempo de `O(V + E) `, `O(V)` espacio de recursión

■ Mostraremos la solución **Kahn** en los tres idiomas (más clara para entrevistas).
■ La versión **DFS** también se proporciona para la integridad.

-...

## 🧩 Code Walk‐Through (Kahn's Algorithm)

#### ## 1down⃣ Java

``java
importar java.util*;

Solución de la clase pública {}
int[] findOrder(int numCourses, int[][](requisitos) {}
/ Lista de adyacencia
Lista realizadaLista realizadaInteger título = nuevo ArrayList recomendado(numCourses);
para (int i = 0; i < numCourses; i++) graph.add(nueva ArrayList correctamente());
// array indegree
int[] indegree = nuevo int[numCourses];

// gráfico de construcción
para (int[] edge : requisitos) {}
int course = edge[0];
int prereq = edge[1];
graph.get(prereq).add(course);
indegree[course]+;
}

// cola de cursos sin requisitos
Búsquedas realizadasInteger título q = nuevo LinkedList recomendado();
para (int i = 0; i)
si (indegree[i] == 0) q.offer(i);

int[] order = nuevo int[numCourses];
int idx = 0;

(!q.isEmpty()) {
int curr = q.poll();
orden[idx+] = curr;

para (int next : graph.get(curr)) {}
si (--indegree[next] == 0) q.offer(next);
}
}

devolver idx == numCourses ? orden : nuevo int[0];
}
}
`` `

■ ¿Por qué el 100 % golpea? * *
*Sólo operaciones O(V + E)*, sin pila de recursión, sin sobrecabeza oculta.

-...

#### 2down⃣ Python

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def findOrder(self, numCourses: int, requirements: List[List[int]) - No. List[int]:
graph = [[] for _ in range(numCourses)]
indegree = [0] * numCourses

por supuesto, pre en condiciones previas:
graph[pre].append(course)
indegree[course] += 1

q = deque([i for i in range(numCourses) if indegree[i] == 0])
orden = []

mientras q:
cur = q.popleft()
orden.append(cur)
para nxt en el gráfico [cur]:
indegree[nxt] -= 1
si indegree[nxt] == 0:
q.append(nxt)

orden de devolución si len(order) == numCourses else []
`` `

* Notas específicas*
*`deque`* da O(1) pops de la izquierda.
■ * Comprensiones de la lista* mantienen el código corto.

-...

#### 3down⃣ C++

``cpp
Incluido el título
#include >
usando std namespace;

Clase Solución {
public:
vector significado: encontrarOrder(int numCourses, vector asignadovector fielmente usado) {
vector realizador realizado en el título del título (numCourses);
vectoriales indegree(num) Cursos, 0);

para (autofr e : requisitos) {}
int course = e[0], pre = e[1];
graph[pre].push_back(course);
++indegree[course];
}

queue indicaint
para (int i = 0; i)
si (indegree[i] == 0) q.push(i);

orden de vectores:
(!q.empty()) {
int cur = q.front(); q.pop();
orden.push_back(cur);
para (int nxt : graph[cur]) {}
si (--indegree[nxt] == 0) q.push(nxt);
}
}

retorno (int)order.size() == numCourses ? order : vector asignadoint confianza();
}
};
`` `

■ ** Estilo C++**
* < > > > > > > > > > > > > > > > > > > > > > > > > >
■ Devuelve el vector vacío en la detección de ciclos.

-...

DFS (Recursivo) – Opcional

**Python (DFS)* *

``python
Solución de clase:
def findOrder(self, numCourses: int, requirements: List[List[int]) - No. List[int]:
graph = [[] for _ in range(numCourses)]
para a, b en requisitos: graph[b].append(a)

visitas = [0] * numCourses # 0=unvisited, 1=visiting, 2=visited
orden = []

def dfs(u):
si se visita[u] == 1: ciclo
Retorno Falso
si se visita[u] == 2: # Ya procesado
Retorno
visitados[u] = 1
for v in graph[u]:
si no dfs(v): devolver False
visitados[u] = 2
orden.append(u)
Retorno

para i en rango(numCourses):
si no dfs(i): retorno []

orden de devolución[:-1]
`` `

■ **¿Por qué no se utiliza en entrevistas? * *
■ *La pila de recursión puede rebosar en gráficos profundos. *
■ *La lógica de detección del ciclo es un poco más verbosa. *

-...

## 🔧 Edge Cases > Pitfalls

Silencio Caso confidencialidad ¿Qué hay que ver para Silencio
Silencio...
Silencio No hay prerrequisitos ( " prerrequisitos == [] " ) . Silencio
Silencio Componentes desconectados Silencio Kahn procesará cada componente de forma independiente. Silencio
tención Múltiples vertices de cero-indegree TEN cualquier permutación es válida – el arnés de prueba generalmente acepta cualquiera. Silencio
TENIENDO EL AUMENTO (`[a,a]`) Las limitaciones del problema de la vida lo prohíben, pero si está presente, Kahn nunca encarará `a`. Silencio
tención Grandes `numCourses` (2000) tención Todavía trivial para soluciones O(V+E). Silencio

-...

## 🚀 El Bien, el Mal, y el Ugly" del Programa del Curso II

Silencio**
Silencio--------------------------
Ω ✔ Cómodo topológico intuitivo – entrevista perfecta punto de conversación. TEN ❌ Requiere cuidadoso manejo de la cola de cero-indegree; ocurren errores fuera-por-uno. ❌ DFS recursion puede soplar la pila para gráficos profundos (especialmente en Java). Silencio
✔ Funciona para cualquier DAG – reutilización en la programación, construcción, orden, resolución de dependencia. Debe construir la lista de adyacency y la matriz de indegree – extra O(V+E). ❌ La lógica de detección de ciclos puede estar oculta en DFS (insignia de apilación recursiva). Silencio
El algoritmo de Kahn garantiza un orden válido en el tiempo lineal. Si te olvidas de comprobar el recuento final, puedes devolver un pedido parcial. En idiomas con gestión manual de memoria (C++), olvidar vectores claros puede llevar a errores sutiles. Silencio

■ **Takeaway** – El algoritmo de Master Kahn. Es corto, rápido y fácil de entrevistar.
■ Utilice DFS sólo cuando necesite producir *all* pedidos topológicos o detectar múltiples soluciones.

-...

## 📈 SEO‐Optimized Blog Title & Meta

*Título*
“Course Schedule II – 210 on LeetCode: Master Topological Sort (Java, Python, C++)”

**Meta Descripción:**
“Aprenda a resolver LeetCode 210 – Programa del curso II con el Algoritmo de Kahn. Obtenga aplicaciones Java, Python y C+++, análisis de complejidad y consejos de entrevista. Boost your software-engineering interview prep now! ”

**Keywords:**
Calendario del curso II, LeetCode 210, tipo topológico, algoritmo de Kahn, tipo topológico de DFS, algoritmos gráficos, solución Java, solución Python, solución C++, preparación de entrevistas, entrevista de ingeniero de software.

-...

## 📌 Final Checklist for Your Job‐Interview Readiness

1. **Conoce la declaración del problema** – cursos, requisitos, DAG.
2. **Explicar el algoritmo de Kahn** – inde acuerdo, cola, detección de ciclos.
3. **Mostrar el código en 3 idiomas** – asegúrese de que compila en LeetCode.
4. ** Casos de borde de discusión** – prerrequisitos vacíos, múltiples nodos de cero grados.
5. **Contraste con DFS** – pros/cons, apilar el riesgo de desbordamiento.
6. **Tiempo de medición/complejidad espacial** – `O(V+E)` tiempo, `O(V+E)` espacio.
7. **Hablar sobre analogías del mundo real** – construir sistemas, programar tareas.
8. **Preparar una prueba de unidad rápida** – probar manualmente pequeños gráficos localmente.
8. **Prepárate para responder al seguimiento** – “¿Podemos generar todos los pedidos válidos?” → DFS + retroceso.

-...

 Tu siguiente paso:
Implementar la solución Kahn en su IDE favorito, empujarlo a un repo GitHub, y ensayar explicarlo en voz alta. Buena suerte con tus entrevistas – acabas de agregar un potente algoritmo gráfico a tu caja de herramientas! 🚀

-..