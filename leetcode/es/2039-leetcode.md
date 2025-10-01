-...
Título: LeetCode 2039. El tiempo cuando la red se convierte en ocio -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2039. El tiempo cuando la red se convierte en ocio
■ **Medium – LeetCode** Silencio **Java / Python / C++** Silencio **BFS + Matemáticas**

El problema es un problema clásico de gráficos de estilo entrevista que prueba su capacidad de:

* Construir un gráfico no dirigido de listas de bordes
* Computa distancias más cortas con un solo BFS
* Motivo de simulación de eventos basados en el tiempo sin simular cada segundo

A continuación encontrará implementaciones limpias y listas de producción en **Java, Python y C+**.
Después del código nos sumergimos en un blog **SEO-friendly** que explica el algoritmo, los casos de borde que debe cuidar, y por qué esta solución es lo suficientemente rápida para los límites del problema (hasta 105 nodos/edges).

-...

## 🚀 1. Solution Overview

Silencio Lo que hacemos _ Por qué funciona
...------------------------
Silencio 1 Silencio **Construir una lista de adyacencia** para el gráfico no dirigido. tención Permite a O(1) traversal vecino. Silencio
Silencio 2 Silencio **BFS desde el nodo 0** para encontrar el recuento de hop más corto (distancia) a cada otro servidor. El gráfico no tiene peso; BFS da longitudes de ruta más cortas exactas en O(N+E). Silencio
Silencio 3 ← Para cada servidor de datos *i* (i √≥ 0) compute: √≥br confianza• *roundTrip* = 2 × dist[i] √°Send* = ⌊(roundTrip – 1) / paciencia[i] × paciencia[i] > > > idleTime* = last Enviar + roundTrip Silencio *lastSend* es el timetamp del último mensaje que el servidor reenvia *antes* llega la respuesta del maestro. Silencio
Silencio 4 Silencio Respuesta = **max(idleTime) + 1**. Silencio Red es ocioso cuando la respuesta **última** ha llegado; añadimos 1 porque el tiempo comienza a 0. Silencio

El algoritmo funciona en **O(N + E)** tiempo y utiliza **O(N + E)** memoria.

-...

## 🖥 2. Código

## Java

``java
importar java.util*;

Clase Solución {
red de entrada públicaBecomesIdle(int[] bordes, int[] paciencia {
int n = paciencia. longitud;

// 1. Construir la lista de adyacencia
Lista realizadaInteger() g = nuevo ArrayList[n];
para (int i = 0; i) no; i++) g[i] = nuevo ArrayList recomendado();
para (int[] e : bordes) {
g[e[0].add(e[1]);
g[e[1]].add(e[0]);
}

// 2. BFS del maestro (nodo 0)
int[] dist = nuevo int[n];
Arrays.fill(dist, -1);
Búsquedas realizadasInteger título q = nuevo ArrayDeque corresponde();
q.add(0);
[0] = 0;
(!q.isEmpty()) {
int u = q.poll();
(int v: g[u]) si (dist[v] == -1) {
dist[v] = dist[u] + 1;
q.add(v);
}
}

// 3. Computar el último tiempo de ocio
respuesta int = 0;
para (int i = 1; i) {}
int roundTrip = 2 * dist[i];
el último Enviar = (roundTrip) 1) / paciencia[i]) * paciencia[i];
int idle = último Enviar + ronda Trip;
respuesta = Math.max(respuesta, ocio);
}
respuesta de retorno + 1; // +1 porque idle comienza después de la última respuesta
}
}
`` `

## Python

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def network Se convierte en Idle(self, edges: List[List[int]], paciencia: List[int]) int:
n = len(patiencia)

# 1. lista de adjacency
g = [[] for _ in range(n)]
para u, v en los bordes:
g[u].append(v)
g[v].append(u)

# 2. Distancias BFS
[-1]
dist[0] = 0
q = deque([0])
mientras q:
u = q.popleft()
for v in g[u]:
si se dist[v] == -1:
dist[v] = dist[u] + 1
q.append(v)

# 3. Compute idle times
ans = 0
para i en rango(1, n):
round_trip = 2 * dist[i]
last_send = (round_trip - 1) // paciencia[i] * paciencia[i]
idle_time = last_send + round_trip
as = max(ans, idle_time)

de retorno + 1
`` `

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
red int Se convierte en Idle(vector identificadovector fielint estrecho bordes, vector implicaint compartir paciencia) {
int n = paciencia.size();
vector realizador:
para (auto &e : bordes) {}
g[e[0].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

vector asignadoint -1);
queue indicaint
dist[0] = 0; q.push(0);
(!q.empty()) {
int u = q.front(); q.pop();
(int v: g[u]) si (dist[v] == -1) {
dist[v] = dist[u] + 1;
q.push(v);
}
}

int ans = 0;
para (int i = 1; i) {}
int roundTrip = 2 * dist[i];
el último Enviar = (roundTrip) 1) / paciencia[i]) * paciencia[i];
int idle = último Enviar + ronda Trip;
ans = max(ans, idle);
}
devolver los ans + 1;
}
};
`` `

-...

## 📄 3. SEO‐Optimized Blog Post

### Title
**LeetCode 2039 – “El tiempo cuando la red se vuelve ociosa”**
*Solución rápida de BFS (Java, Python, C++) – Algoritmos de entrevista maestra*

-...

## Meta Descripción
Solve LeetCode 2039 “El tiempo cuando la red se convierte en ocio” con un algoritmo BFS + matemáticas óptimo. Lea nuestra explicación paso a paso, código Java/Python/C++ y consejos de entrevista. ¡Perfecto para desarrolladores de backend e ingenieros de red!

-...

#### Introduction

LeetCode 2039 le pide que encuentre el segundo más temprano cuando una red de servidores se hace ocioso después de una serie de intercambios de mensajes. Aunque la descripción del problema parece un rompecabezas de simulación, un enfoque matemático limpio con BFS da una solución O(N+E). Este post camina a través de ese enfoque, la intuición detrás de la fórmula clave, y por qué el código funciona lo suficientemente rápido para los límites superiores (105 nodos y bordes).

-...

Problema Recap

* **Graph** – Sin dirección, sin peso.
* **Master server** – node 0.
* ** Servidores de datos** – nodos 1...n‐1.
* ** Mensajes** – cada servidor de datos envía su primer mensaje a la vez 0.
* **Resend rule** – every *patience[i]* seconds after the last send, if no reply has arrived.
* ** Objetivo** – el segundo más temprano cuando no hay mensajes en tránsito.

-...

## 📌 Core Insight

1. **Cuenta la distancia más corta** – porque cada mensaje sigue el camino * más corto*.
2. **Tiempo de viaje** = `2 * dist[i]`.
3. **Resén último antes de la respuesta**: el mayor número de `paciencia[i]` que es *strictamente* antes de que llegue la respuesta.
`` `
lastSend = ⌊ (roundTrip – 1) / paciencia[i] * paciencia[i]
`` `
4. **Tiempo de servidor i** = 'últimoSend + roundTrip`.
5. ** Cierre de red** = `max(idleTimes) + 1`.

¿Por qué la fórmula del piso?
Si una respuesta llegara a tiempo `roundTrip ' , cualquier reenvío a `roundTrip` o posterior es inútil.
Por lo tanto, encontramos el mayor tiempo de envío que es `traducido roundTrip`.
The `(roundTrip – 1)` truco garantiza que si `roundTrip` es exactamente un múltiple de `patience[i]` no contamos el último envío.

-...

## 🛠ف Algorithm Walk‐through

### 1. Construir el Gráfico
Las listas de Adjacency son la forma más simple de representar gráficos poco redirigidos.
``cpp
para (auto &e : bordes) {}
g[e[0].push_back(e[1]);
g[e[1]].push_back(e[0]);
}
`` `

### 2. BFS para distancias
Debido a que los bordes no tienen peso, un solo BFS del nodo 0 da `dist[v]` para cada servidor `v`.
``python
mientras q:
u = q.popleft()
for v in g[u]:
si se dist[v] == -1:
dist[v] = dist[u] + 1
q.append(v)
`` `

### 3. Compute Idle Times
Para cada servidor `i` √ 0:
``text
roundTrip = 2 * dist[i]
lastSend = suelo(redondedo) Viaje - 1) / paciencia[i]) * paciencia[i]
Idle Time = lastSend + roundTrip
`` `
Tome el máximo sobre todos los servidores y agregue 1.

-...

Análisis de la Complejidad

← Complejidad Silencio Java Silencio Python Silencio C++
Silencio------------------------------
TENIDO Tiempo ANTERIOR O(N+E) Silencio O(N+E)
TENIDO EL ESPACIO TENIDO O(N+E) TENIDO O(N+E) TENIDO

Las tres implementaciones utilizan una sola cola, una lista de adyacency y un array de distancia. Incluso en el peor caso (`N = E = 105`), el BFS visita cada borde dos veces – muy por debajo del límite de 1 segundos de duración de LeetCode.

-...

Casos de borde “bueno, malo, feo”

¦ Situación Silencioso Qué ver para Silencio / Mitigación Silencio
Silencio...
TEN **patience[i] = 0** TEN División por cero – no permitida por limitaciones ( " patience[i] 1 " . Agregue un guardia o confíe en la garantía de problemas. Silencio
tención **roundTrip = 1** Silencioso `roundTrip-1` se convierte en 0; la fórmula todavía funciona. La división del piso maneja cero correctamente. Silencio
Silencio **Muy buena paciencia** ← `patience[i] ⇩ roundTrip` → server never resends. La fórmula produce `últimoSend = 0`. Silencio
Silencio ** Gráficos desconectados** Silencioso Problema garantiza conectividad al nodo 0. Silencio Todavía cheque `dist[i]!= - Para estar a salvo. Silencio
tención **Huge N/E** tención La recidiva de Stack (DFS) se desbordaría. Use BFS iterativa – sin recidiva. Silencio

-...

## 🎯 Why This Passes LeetCode’s Limits

* **BFS** es lineal en bordes, no en segundos.
* Todo aritmético es tiempo constante por nodo.
* Ninguna simulación de cada segundo significa que el algoritmo funciona en microsegundos incluso por 105 nodos.

-...

## 📚 Takeaway Checklist

[ ] Construir la lista de adyacencia (O(N+E))
- BFS del maestro para conseguir los más cortos
Compute `roundTrip`, `lastSend`, `idleTime `
- [ ] Regreso `max(tiempo del pasillo) + 1`
- [ ] No recursivo DFS → evitar el desbordamiento de pila
- [ ] Prueba con:
* Todos los servidores tienen `paciencia = 1` (reenviamientos de caso inferior)
* Algunos servidores con enorme paciencia (sin reenviamientos)
* Árbol grande vs denso gráfico

-...

### 🔗 Palabras finales

LeetCode 2039 es una pregunta de entrevista *network‐theory* disfrazada de simulación. Centrándose en ** senderos más cortos** y un truco aritmético limpio, se puede resolver en un solo paso. Las implementaciones Java, Python y C++ arriba están listas para una presentación de code-interview y pasarán los estrictos plazos/memoria del problema.

¡Feliz codificación! 🚀

-...

### 📌 Palabras clave para SEO

- LeetCode 2039
- El tiempo cuando la red se convierte en ocio
- Solución BFS
- Java LeetCode 2039
Python LeetCode 2039
- C++ LeetCode 2039
- Algoritmo de idle de red
- Algoritmo de gráfico de entrevistas
- El camino más corto BFS
- Preguntas de entrevista de backend

Siéntase libre de copiar los fragmentos de código, tweak ellos para su estilo de codificación personal, o utilizarlos como referencia de estudio. ¡Buena suerte en tu próxima entrevista!