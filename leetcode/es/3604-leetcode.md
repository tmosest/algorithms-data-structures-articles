-...
Título: LeetCode 3604. Tiempo mínimo para llegar Destino en Gráfico Directo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Resumen de la solución

*Problema*
Dado un gráfico dirigido con nodos (0 ... n‐1).
Un borde se define por `[u, v, start, end]`. y sólo puede ser atravesado en un tiempo entero 't ' tal que 'comienza ≤ t ≤ final'.
Empiezas en el nodo `0` a la vez `0`.
En una unidad de tiempo puede esperar en el nodo actual o atravesar un borde saliente válido.
Encuentre el tiempo posible que pueda alcanzar el nodo `n‐1`.
Regrese `-1' si es imposible.

-...

#### 1.1 Why Dijkstra Obras Aquí.

La observación clave es que el “costo” de pasar de un nodo `u’ en el momento `t` a un nodo `v` es ** siempre exactamente 1 unidad de tiempo** (el acto de atravesar el borde).
El único giro extra es que podría tener que esperar* hasta que el borde esté disponible, es decir, hasta `max(start, t)`.

Por un nodo que lleguemos a la hora:

`` `
si t ≤ final:
part_time = max(start, t) // wait if necessary
arriba_time = part_time + 1 // edge traversal toma 1 unidad
`` `

El tiempo de llegada es una función monotónica del tiempo de salida, por lo tanto el tiempo de llegada más temprano a cualquier nodo es siempre mejor que cualquier llegada posterior.
Por lo tanto, podemos tratar el gráfico como un gráfico ponderado donde el peso de `u` a `v` depende del tiempo actual, pero la optimización todavía sostiene – sólo necesitamos un **prioridad‐cuue** (min-heap) que siempre expande el nodo que se puede alcanzar lo antes posible.

Ese es exactamente el algoritmo de Dijkstra con un paso de relajación dependiente del tiempo.

-...

### 1.2 Pasos de Algoritmo

← Paso Silencioso Descripción Silencio
Silencio...
Silencio 1 ← Construir una lista de adyacencia `G[u]` que contenga tuples `(v, start, end)` para cada borde saliente de `u`. Silencio
Silencio 2 Silencio `dist[i]` – el tiempo de llegada más antiguo conocido en el nodo `i`. Inicializar a todos a `móvil' excepto `dist[0] = 0`. tención
Silencio 3 TENIDO Utilizar un pequeño salto almacenando `(tiempo, nodo)`. Empuje `(0, 0)` inicialmente. Silencio
Silencio 4 Silencio Mientras el montón no está vacío: Silencio
* Pop `(t, u)` – el nodo que se puede alcanzar lo antes posible. Silencio
* Si ya tenemos un tiempo más conocido para `u` (`t ⇩ con con personas [u]`), skip. Silencio
TENIDO ANTERIOR * Si `u == n-1`, hemos terminado - devolver `t`. Silencio
* Por cada filo `(v, s, e)` de `u`: Silencio
TENIDO TERRITORIO * Si `t > e` → el borde ya está cerrado, ignorar. Silencio
Silencio Silencioso * `part = max(s, t)` (espera si es necesario). Silencio
Silencio Silencio * `arrival = salida + 1`. Silencio
* Si `arrival ' no[v]`, actualice `dist[v]` y empuje `(arrival, v)` hacia el montón. Silencio
Silencio 5 Silencio Si el bucle termina sin alcanzar el nodo `n-1`, regrese `-1`. Silencio

-...

#### 1.3 Correctness Proof Sketch

Demostramos que el algoritmo devuelve el tiempo mínimo posible de llegada al nodo `n-1`.

**Lema 1 (Monotonicidad)* *
Si se puede llegar a un nodo " u " a la vez " y " t1 " , entonces cualquier camino que parta de " u " a la vez " no puede llegar más tarde a un destino que un camino que comienza a la vez " t2 " .

*Proof.* La única operación que puede retrasar el progreso está esperando. Esperar más sólo puede empujar el tiempo de salida del próximo borde hacia adelante, nunca antes. Por lo tanto la llegada más temprana de un tiempo de inicio posterior es ≥ la llegada más temprana de un tiempo de inicio anterior. ∎

**Lemma 2 (Subestructura Optimal)* *
Seamos un camino óptimo desde el nodo `0` hasta el nodo `n-1`. El prefijo de `π` hasta cualquier nodo intermedio `u` es también un camino óptimo de `0` a `u`.

*Proof.* Asume lo contrario – que existe un mejor camino hacia 'u'. Concatenando que un mejor prefijo con el sufijo de `π` de `u` a `n-1` daría un mejor camino general, contradiciendo la óptimaidad de `π`. ∎

**Teorema (corrección algorítmica)* *
Cuando el algoritmo extrae un nodo `u` de la cola prioritaria con el tiempo `t`, `t` equivale al tiempo mínimo posible de llegada a `u`.

*Proof by induction on the number of extracted nodes. *

- **Base**: El primer nodo extraído es `(0,0)`. Claramente `0` es mínimo para el nodo `0`.
* Paso de inducción* Asume the statement holds for all nodes extracted before `u`.
Supongamos que, para la contradicción, existe un camino hacia 'u' que llega a la hora 't'' ".
Seamos el predecesor de 'u' en ese camino óptimo, llegando a la hora 't_p'.
Por hipótesis de inducción, `t_p` es mínimo, por lo tanto cuando se extrajo 'p`, el algoritmo consideró el borde 'p → u`.
Habría calculado `arrival = max(start, t_p) + 1 ≤ t'` e insertado `(arrival, u)` en el montón.
Ya que `arrival ≤ t' se hizo t`, el montón habría aparecido `(arrival, u)` antes `(t, u)`, contradiciendo la suposición de que `(t,u)` fue extraída siguiente. ∎

Finalmente, la primera vez que el algoritmo extrae nodo `n-1`, el tiempo es el tiempo de llegada óptimo. Si el montón se vacía antes de eso, no existe camino. ∎

-...

#### 1.4 Complexity Analysis

Silencio Silencio Silencio Silencio
Silencio------------------------
← Construir la lista de adyacencia Silencio **O(E)** Silencio `E` = número de bordes Silencio
Silencio Operaciones de salto Silencio Cada nodo puede ser insertado varias veces, pero a lo sumo una vez por relajación que mejora `dist`. Cada inserción/extracción cuesta **O(log V)**. En el peor de los casos procesamos cada borde una vez → **(V+E) log V)** Silencio
Silencio Tiempo total Silencio **O((V + E) log V)** Silencio
← Espacio Silencioso **O(V + E)** para la lista de adyacency, array de distancia, montón, y las banderas visitadas. Silencio

Con limitaciones `n ≤ 10^5` y `edges.length ≤ 10^5`, esto encaja cómodamente en los límites de tiempo y memoria.

-...

## 2. Aplicación del Código

A continuación se presentan soluciones concisas y de producción en **Java**, **Python**, y **C+**.

■ **Tip** – Para la práctica de entrevistas, implemente el algoritmo desde cero (sin biblioteca “shortcuts”) para demostrar comprensión.

#### 2.1 Java

``java
importar java.util*;

Solución de la clase pública {}
int public int minTime(int n, int[] edges) {
// lista de adjacency: nodo - título lista de {to, start, end}
Lista realizada[] gráfico = nuevo ArrayList recomendado(n);
para (int i = 0; i) no; ++i) graph.add(new ArrayList fiel());

para (int[] e : bordes) {
graph.get(e[0]).add(new int[]{e[1], e[2], e[3]});
}

// los primeros tiempos de llegada conocidos
long[] dist = new long[n];
Arrays.fill(dist, Long.MAX_VALUE);
[0] = 0;

// min-heap of (time, node)
PriorityQueue hacía lo largo[] confía pq = nueva PrioridadQueue decir correctamente(Comparador.comparingLong(a - título a[0]));
pq.offer(new long[]{0, 0});

mientras (pq.isEmpty()) {
long[] cur = pq.poll();
t largo = cur[0];
int u = (int) cur[1];

si (t != dist[u]) continúan; //
si (u == n - 1) retorno (int) t; //

para (int[] e : graph.get(u) {
int v = e[0], s = e[1], eEnd = e[2];
si (t > eEnd) continuar; // borde ya cerrado
larga salida = Math.max(s, t);
larga llegada = salida + 1;
si (arrigen) {}
dist[v] = llegar;
pq.offer(new long[]{arrive, v});
}
}
}
retorno -1; //
}
}
`` `

-...

### 2.2 Python

``python
importación heapq
de la importación Lista

Solución de clase:
def minTime(self, n: int, edges: List[List[int]) - título int:
graph = [[] for _ in range(n)]
para u, v, s, e en los bordes:
graph[u].append(v, s, e))

INF = 10**20
[INF]
dist[0] = 0

pq = [(0, 0)] # (time, node)
mientras pq:
t, u = heapq.heappop(pq)
si t != dist[u]:
continuar
si es que...
t

for v, s, e_end in graph[u]:
si t > e_end:
continuar
salida = max(s, t)
llegada = salida + 1
si llegas a la salida [v]:
dist[v] = llegar
heapq.heappush(pq, (arrive, v))

retorno -1
`` `

-...

### 2.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minTime(int n, vector identificadovector identificadoint {}
vector realizador realizador seleccionado, 3 títulos
para (auto golpe e : bordes) { // {to, start, end}
g[e[0].push_back({e[1], e[2], e[3]});
}

const long INF = 4e18;
vector llevado a cabo largo tiempo dist(n, INF);
[0] = 0;

usando P = par realizado largo, int confidencial; // (tiempo, nodo)
priority_queue obtenidosP, vector asignadoP título, mayor especificadoP título
pq.push({0, 0});

mientras (pq.empty()) {
auto [t, u] = pq.top(); pq.pop();
si (t != dist[u]) continúan; //
si (u == n - 1) retorno (int)t;

para (auto golpe e : g[u]) {}
int v = e[0], s = e[1], eEnd = e[2];
si (t √≥ eEnd) continúan;
larga salida = max consignalong long(s, t);
larga llegada = salida + 1;
si (arrigen) {}
dist[v] = llegar;
pq.push({arrive, v});
}
}
}
retorno -1;
}
};
`` `

-...

## 3. ¿Y si? – Casos de borde " Pitfalls comunes

← Situación Silencio Cómo el algoritmo lo maneja _ Por qué es seguro
Silencio------------------------------------------------------------
Silencio **Los bordes de Multiple entre el mismo par** Silencio Todos se almacenan en la lista de adyacencia. El algoritmo elige la *más cercana* posible llegada. Las distancias están actualizadas sólo si son estrictamente mejores. Silencio
Silencio **Edge start œ end** tención Tal borde nunca se puede utilizar (el paso de relajación simplemente lo ignora). Sin coste adicional. Silencio
Silencio ** Ventanas de tiempo muy grande** Silencioso `dist` utiliza `long` / `int64` por lo que el desbordamiento no puede suceder. Incluso una ventana de '10^9` está bien. Silencio
Silencio **Stale heap entries** Silencio El cheque `si t != dist[u]` los descarta. ANTE Garantiza la corrección y mantiene el salto pequeño. Silencio
Silencio **Esperar por un largo período** Silencio `depart = max(start, t)` empujará la entrada de montones hacia fuera lejos en el futuro - eso es exactamente lo que "esperar" significa. El algoritmo sigue siendo lineal en el número de relajacións. Silencio

-...

## 4. “Good‐to‐Know” – Por qué algunos enfoques ingenuos fallan

1. **BFS sólo** – BFS asume que cada borde está siempre disponible.
La restricción dependiente del tiempo significa que puede llegar a un nodo *más tarde* a través de un camino diferente que espera un mejor borde.
BFS nunca “conoce” esperar, por lo que puede devolver una respuesta *sobre-optimista* o perder un camino factible por completo.

2. **DP by time (DP[t][u])** –
Si intentas pre-computar todos los tiempos posibles hasta el máximo `end`, necesitarás una tabla de tamaño `O(max_time * n)` que es astronómicamente grande (`max_time` puede ser `10^9`).
Por lo tanto, el enfoque de estilo Dijkstra es la única manera práctica.

-...

## 5. “Good‐to‐Know” – Por qué Este problema es una pregunta de entrevista clásica

Por qué importa
Silencio...
TEN **Aristas dependientes del tiempo** Silencio Muestras que puedes extender algoritmos clásicos para manejar limitaciones dinámicas. Silencio
Silencio **Large input (10^5)** Silencioso Te obliga a utilizar estructuras de datos eficientes (`heap`, lista de adjacency) en lugar de la recursión ingenua o las matrizs. Silencio
Silencio **Exact integer traversal** Silencio Mantiene el problema discreto – útil para enseñar cómo tratar con “esperar” en problemas gráficos. Silencio
Retorno -1** Silencioso Las fuerzas que usted piensa en *reachability* y las entradas de estancamiento. Silencio

Un candidato fuerte:

* Explicar el argumento monotónico.
* Reaplicar el paso de relajación.
* Discuss edge‐case handle (cerrados bordes, entradas de heap stale).
* Sea capaz de demostrar corrección en unas pocas oraciones.

-...

## 6. Pruebas rápidas

Puede copiar-pasar cualquiera de las tres implementaciones en el editor “Java”, “Python 3”, o “C++ (GCC 17)” de LeetCode y realizar las siguientes pruebas:

``java
int n = 4;
int[][] bordes = {
1, 0, 5},
{1, 3, 4, 6},
2, 2, 4},
{2, 3, 5, 7}
};
afirmar nueva solución().minTime(n, edges) == 5; // Respuesta esperada
`` `

``python
sol = Solución()
afirmar sol.minTime(4, [[0,1,0,5],[1,3,4,6],[0,2,2,4],[2,3,5,7]]) == 5
`` `

``cpp
Solución s;
int ans = s.minTime(4, {0,0,5},{1,3,4,6},{0,2,2,4},{2,3,5,7});
afirma(ans == 5);
`` `

-...

## 7. Pensamientos finales

¿Por qué Dijkstra todavía funciona? El paso de espera es monotónico, así que antes siempre es mejor.
¿Por qué es una buena pregunta de entrevista? Mezcla la lógica más corta clásica con un giro sutil dependiente del tiempo, que requiere una explicación clara de la monotónica y la subestructura óptima.
- Errores comunes** - Olvídate de usar `Long.MAX_VALUE` / `10**20` para los valores iniciales `dist`, o empujando entradas de heap estancas (que pueden aumentar drásticamente el tiempo de ejecución).

¡Feliz codificación y buena suerte en tu próxima entrevista!