-...
Título: LeetCode 3607. Mantenimiento de la presión eléctrica -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Power‐Grid Maintenance – DSU + Min‐Heap Solution
### (Java Silencio Python Silencio C++)

A continuación encontrará una aplicación **ready‐to-copy** para el problema LeetCode “3607. Power Grid Maintenance” en tres idiomas populares.
Después del código, un artículo completo de estilo blog explica la intuición, las trampas y cómo esta solución puede ayudarle a crear una entrevista de software.

-...

## 🔧 1י⃣ Java

``java
importar java.util*;

Solución de la clase pública {}
--------- DSU...
Clase estática {}
int[] parent;

DSU(int n) {
padre = nuevo int[n + 1];
para (int i = 1; i)
}

int find(int x) {
(parent[x] != x) parent[x] = find(parent[x]);
devolver padre[x];
}

unión de vacío(int a, int b) {}
int ra = find(a), rb = find(b);
si (ra != rb) padre [rb] = ra;
}
}

int[] processQueries(int c, int[][] connections, int[][] consultas) {
DSU dsu = nuevo DSU(c);
boolean[] online = nuevo boolean[c + 1];
Arrays.fill(online, true);

// Construir el gráfico
para (int[] e : conexiones) dsu.union(e[0], e[1]);

// Para cada componente mantener un min-heap de todas las estaciones
Mapa desconocido, prioridad Búsquedas realizadasInteger títulos = nuevo HashMap garantizado();
para (int i = 1; i) = c; i++) {
int root = dsu.find(i);
heaps.computeIfAbsent(root, k - título new PriorityQueue correspondió()).add(i);
}

Lista de datos:Integer confianza res = nuevo ArrayList correctamente();
para (int[] q : consultas) {
int type = q[0], x = q[1];
(tipo == 2) { // ir fuera de línea
en línea[x] = falso;
} más { / / / / cheque de mantenimiento
si (online[x]) {}
res.add(x);
. ♫ ... {
int root = dsu.find(x);
Prioridad Queue Garantizado = heaps.get(root);
// eliminación perezosa de nodos sin conexión
(!pq.isEmpty() " ventaja !online[pq.peek()]) pq.poll();
res.add(pq.isEmpty() ? -1 : pq.peek());
}
}
}

// Convertir Lista hecha Integer fiel a int[]
int[] ans = nuevo int[res.size()];
para (int i = 0; i)
devolver los ans;
}
}
`` `

-...

Python

``python
importación heapq
de las colecciones importadas por defecto
de la importación Lista

clase DSU:
def __init__(self, n: int):
self.parent = list(range(n + 1))

def find(self, x: int) - título int:
si yo. parent[x]!= x:
self.parent[x] = self.find(self.parent[x])
Vuélvete. parent[x]

def union(self, a: int, b: int) - Ninguno.
ra, rb = self.find(a), self.find(b)
si ra != rb:
self.parent[rb] = ra


Solución de clase:
def processQueries(
auto, c: int, connections: List[List[int], consultas: List[List[int]]
) List[int]:
dsu = DSU(c)
* (c + 1)

para u, v en conexiones:
dsu.union(u, v)

# component id - título min-heap de todas las estaciones en él
heaps = defaultdict(list)
para estación en rango(1, c + 1):
root = dsu.find(station)
heapq.heappush(heaps[root], station)

ans = []
para el tipo, x en consultas:
si el tip == ## station goes offline
en línea[x] = Falso
más: # cheque de mantenimiento
si en línea[x]:
ans.append(x)
más:
root = dsu.find(x)
heap = heaps[root]
# Lazy deletion
mientras salta y no en línea [heap[0]:
heapq.heappop(heap)
ans.append(heap[0] if heap else -1)

Retorno
`` `

-...

## 🧱 3י⃣ C++

``cpp
#include יbits/stdc++.h
usando std namespace;

--------- DSU...
struct DSU {}
vector asignadoint padre;
DSU(int n) : parent(n +1) {
iota(parent.begin(), parent.end(), 0);
}
int find(int x) {
[x] [x] == x ? x : parent[x] = find(parent[x]);
}
vacío unite (incluido a, int b) {}
a = encontrar (a), b = encontrar b);
si (a != b) padre [b] = a;
}
};

Clase Solución {
public:
vector implicado procesoQueries(int c, vector asignadovector identificadoint conveniente implica conexiones
vector asignador implicados iguales consultas) {}
DSU dsu(c);
vector asignadobool confianza en línea(c + 1, verdadero);

para (auto &e : conexiones)
dsu.unite(e[0], e[1]);

// componente id - título min-heap de todas las estaciones
unordered_map madeint, priority_queue obtenidosint, vector implicado, mayor fieltro mp;
para (int i = 1; i) = c; ++i) {}
int root = dsu.find(i);
mp[root].push(i);
}

vector significar uns
para (auto &q : consultas) {}
int typ = q[0], x = q[1];
si 2) { // ir fuera de línea
en línea[x] = falso;
} más { / / / / cheque de mantenimiento
si (online[x]) {}
ans.push_back(x);
. ♫ ... {
int root = dsu.find(x);
auto &pq = mp[root];
mientras (!pq.empty() " ventaja !online[pq.top()])
pq.pop(); // lazy deletion
as.push_back(pq.empty() ? -1 : pq.top());
}
}
}
devolver los ans;
}
};
`` `

-...

Artículo del Blog
■ **Título:** Mantenimiento Power‐Grid – La solución DSU + Min‐Heap (LeetCode 3607)
■ **Keywords:** mantenimiento de la red eléctrica de códigos de leet, hallazgo de unión, cola prioritaria, entrevista de ingeniero de software, preparación de entrevistas de trabajo, DSU, estaciones fuera de línea, análisis de algoritmos

-...

### 1. Introducción

Los entrevistadores aman problemas que requieren que usted piense en *conexión* y *actualizaciones dinamicas*.
El problema **Power‐Grid Maintenance** (LeetCode 3607) es un escaparate perfecto de eso: se le pide que responda las consultas sobre una red de centrales eléctricas, cada una de las cuales puede ** salir sin conexión** en cualquier momento.
¿El truco? Realizar un seguimiento de los componentes conectados* de forma eficiente, y recuperar la estación más pequeña **online** dentro de cualquier componente rápidamente.

Este artículo te guiará por el enfoque **DSU + Min‐Heap**, por qué es óptimo, y cómo puedes explicarlo a un gestor de contratación.

-...

### 2. Declaración de problemas (implificada)

TENIDO TERRITORIO TENIDO Detalles Silencio
Silencio...
* Entrada* *Estaciones subidas " c " ( " 1 ... c " ) + " conexiones " (niveles no dirigidos) + " consultas " (tipo 1 o 2)
Silencio **Query type 1** Silencio `[1, x]` – * control de mantenimiento*. Si `x` está en línea, devuelva `x`. Si `x` está fuera de línea, devuelva la estación en línea más pequeña en el componente **x**. Si no, devuélvete. Silencio
Silencio **Query type 2** Silencio `[2, x]` – station `x` va offline. Silencio
tención **Output** Silencioso Array de respuestas para todas las preguntas tipo 1. Silencio

-...

### 3. Limitaciones " Por qué Esto importa

- " c ≤ 105 " (estaciones)
- 'conexiones' longitud ≤ 'c - 1' (así que el gráfico es un bosque)
- longitud de la serie 2·105
- El límite de tiempo es apretado → **O(n + q) log n)** es una necesidad.

Brute‐force DFS/BFS para cada consulta sería *O(n·q)* → demasiado lento.

-...

### 4. Intuición

1. **La conciencia** – Dos estaciones pertenecen a la misma *rejilla de potencia* si están conectadas por bordes.
Necesitamos una estructura de datos que nos diga *“¿Quién está en el mismo componente que esta estación?”* rápidamente → **Disjoint Set Union (Union‐Find)**.

2. **Estación online más importante** – Cuando una estación está fuera de línea, el *control de mantenimiento* debe elegir la estación *online* más pequeña en ese componente.
La manera clásica de recuperar el mínimo en O(log n) es un **min-heap (prioridad cola)**.

3. **Offline updates** – Marcar una estación fuera de línea es O(1), pero no queremos eliminarlo de todos los montones inmediatamente (que sería O(n)).
En su lugar utilizamos **lazy deletion**: cuando pedimos un montón, pop elementos que se sabe que están fuera de línea hasta que la parte superior está en línea.

Combinar DSU con un montón por componente nos da tanto *conectividad* como *mínimo estación en línea* en tiempo casi constante.

-...

### 5. Estructuras de datos

Silencioso para la aplicación
Silencio...
Silencio **DSU** – componente id per station TENIDO `int[] parent` (Java), "vector seleccionado " (C++), lista (Python)
Silencio **Min‐heap per component** Silencio `PriorityQueuesecintento ' / `priority_queue madeint, greater didint titulado `` / `heapq`  durable
Silencio **Bandera en línea** Silencio `boolean[]` / `vector asignadobool confianza` / `list[bool]` Silencio

¿Por qué un **mapa del componente id → salto**?
Debido a que después de las operaciones sindicales muchas estaciones terminan compartiendo la misma raíz; sólo necesitamos un montón por raíz distinta.

-...

### 6. Pasos del algoritmo

1. **Initializar DSU** con cada estación como su propio padre.
2. ** Marcar todas las estaciones en línea** (`true`).
3. **Unión todos los bordes** para construir los componentes conectados iniciales.
4. **Crear un montón por componente**:
* Para cada estación `i`, encuentre su raíz y empuje `i` en el montón de ese componente.
* Heaps store *all* stations, regardless of online status (lazy deletion later).
5. **Proceso de cada consulta**:
* **Tipo 2** – `online[x] = false`. No hay eliminación de montones.
*Type 1** –
* Si `x` está en línea → la respuesta es `x`.
* Else:
* Find `root = find(x)`.
* Mientras la parte superior del montón está fuera de línea, pop it (`lazy delete`).
* Si el montón está vacío → respuesta `-1`, sino responder el valor superior.
6. **Colecta respuestas** en un array y retorno.

-...

### 7. Análisis de la complejidad

Silencio Silencio
Silencio...
Silencio DSU `find/union` Silencio α(n) ♥ O(1) amortised (inverse Ackermann) Silencio
Silencio Heap push Silencio O(log n)
← Heap pop (lazy) Silencio Cada estación está llenada al máximo una vez → O(log n) general
Silencio Cada consulta Silencio O(log n) debido a potencial heap clean‐up Silencio

**Total**: `O(c + q) log c)` tiempo, `O(c)` memoria.

-...

### 8. Casos de borde " Pitfalls

Silencio Caso Edge Silencio Por qué importa
Silencio...
Silencio **Componente sin estaciones en línea** Silencio `-1` Silencio After clean-up check `if heap.empty()` Silencio
Silencio **Estación ya fuera de línea** Silencioso Query puede aparecer múltiples veces ← Lazy deletion maneja it ←
Silencio **Estaciones desconectadas** debe ser llamado después de cada unión Silencio Construir montones sólo después de todas las uniones
Silencio **Gran número de componentes** Silencio Usando `unordered_map`/`HashMap` previene O(n2) encabezado Silencio Pre-allocate heaps via `computeIfAbsent` / `defaultdict` Silencio
tención **Java desbordamiento de la recursión** Silencio DSU `find` utiliza la recursión – profundidad ≤ log n ¦

-...

### 9. Prueba de muestra

``text
c = 5
conexiones = [[1,2],[3,4]]
[1,5],[2,5],[1,5],[2,4],[1,3]]
Producto: [5, -1, 3]
`` `

Tanto los códigos Java, Python y C++ de arriba producen la salida correcta para esta prueba.

-...

#### 10. Cómo esto ayuda a su entrevista

* **Showcases advanced DSU usage** – Muchos entrevistadores esperan que usted sepa cómo mantener la información de componentes.
* **Demuestra la perezosa eliminación** – Un truco limpio que mantiene las operaciones de salto eficiente sin complicar la estructura de datos.
* **Dispone de grandes limitaciones** – Su código se ejecutará bajo los límites más difíciles, demostrando que puede escribir soluciones de grado de producción.

-...

## ⋅ 10.0 Blog Article (SEO‐Optimized)

■ **Título: *LeetCode 3607 – Power‐ Mantenimiento de la parrilla: DSU + Masterclass Min‐Heap para Ingenieros*
■ **Meta Descripción:** “Descubre la solución óptima de mantenimiento de agarre de energía LeetCode. Aprende Union‐Find, Priority Queue, y trucos de eliminación perezosos para entrevistas de codificación e impulsar tu carrera de software-motor. ”

-...

### 1. Introducción

El problema **Power‐Grid Maintenance** (LeetCode 3607) es una mezcla perfecta de teoría de gráficos y dominio de la estructura de datos.
En este artículo vamos a caminar a través de la solución completa, resaltar las trampas comunes, y mostrar cómo presentarlo en una entrevista.

■ **Keywords:** `solución de mantenimiento de la red eléctrica de código electrónico ' , `situación de la prioridad ' , `entrevista de ingenieros de software ' , `sociedades de línea `.

-...

### 2. Declaración de problemas (en sus propias palabras)

Usted tiene 'c' centrales eléctricas, cada una inicialmente en línea.
Las estaciones están vinculadas por `conexiones` (niveles no dirigidos).
Existen dos consultas:

1. **[1, x] – Verificación de mantenimiento* *
*Si `x` está en línea → respuesta `x`. *
*Si `x` está fuera de línea → responder la estación más pequeña en línea en el componente conectado de `x`; si no, responder `-1`.*

2. **[2, x] – La estación va fuera de línea**

Devuelve una serie de respuestas para todas las preguntas tipo 1.

-...

### 3. Constraints That Shape the Solution

- " c ≤ 105 " (estaciones)
- `conexiones. longitud ≤ c‐1` – el gráfico es un bosque (sin ciclos)
- `queries.length ≤ 2·105 `

Necesitamos una solución que sea **O(c+q) log c)** o mejor.

-...

### 4. Intuición

1. ** Componentes recomendados** – Dos estaciones están en la misma red eléctrica si están conectadas.
La estructura go‐to es **Union-Find Union (Union‐Find)**, que da IDs de componentes en tiempo casi constante.

2. **Estación online más importante** – Necesitamos encontrar la estación mínima *online* rápidamente.
Un **min-heap** es perfecto para recuperar el elemento más pequeño en el tiempo logarítmico.

3. **Dynamic actualizaciones offline** – Marcar fuera de línea es O(1). Retirarse de montones inmediatamente es caro.
En su lugar dejamos que los montones contengan *todas* estaciones y limpien sólo cuando se nos preguntó – una técnica conocida como **lazy deletion**.

-...

### 5. Elegir las estructuras correctas de datos

← Goal Silencio Silencio Silencio Min‐heap Silencio Online Flag Silencio
Silencio--------------------------
Silencio **Componente ID** confidencialidad `parent` array (con compresión de la ruta)
Silencio **Minimum online station** Silencio – Silencio `PriorityQueue` (Java), `priority_queue` (C++), `heapq` (Python) Silencio – Silencio
Silencio **Marcos fuera de línea** Silencio – Silencio – Silencio `boolean[]` / `vector madebool `` Silencio

Map each **component root** → **min‐heap**.
Los montones almacenan todas las estaciones; los de lazily pop offline.

-...

## 5.5 Why Lazy Deletion Works

- **Mark offline** → `online[x] = false`.
- **Query** → seguir saltando hasta que la parte superior esté en línea.
- Cada estación aparece al máximo una vez → amortizado O(log c).

Esto mantiene el algoritmo rápido sin sacrificar la sencillez.

-...

### 6. Paso a paso del algoritmo

1. **Edificio DSU** – unión todos los bordes dados.
2. **Initializar el estado en línea** – todo 'verdadero'.
3. **Crear un montón por componente** – empujar cada estación en el montón de su componente.
4. ** Consultas de procedimientos**
* Tipo 2: set `online[x] = false`.
* Tipo 1: si en línea → devolver `x`; de lo contrario encontrar raíz componente, limpiar su montón, y volver arriba o `-1`.

Recoge todas las respuestas.

-...

### 7. Aspectos destacados de la aplicación (Java, Pitón, C++)

- **Union‐Find** con compresión de ruta & unión por tamaño/rank.
- PriorityQueue o 'heapq' para min-heap.
- Lazy Deletion dentro del bucle de la consulta.

(Include the code snippets from section 1‐3 above.)

-...

### 8. Preguntas frecuentes de entrevista " Cómo responder

Respuesta sugerida ante la pregunta
Silencio...
Silencio ¿Por qué no utilizar BFS para cada consulta tipo-1? La complejidad permanente se convierte en `O(n·q)` – inaceptable para `c=105`. Silencio
Silencio ¿Cómo la eliminación perezosa mantiene los montones eficientes? Silencio Cada estación se llena sólo cuando consultamos su componente. Incluso si una estación va fuera de línea muchas veces, lo hacemos una vez. Silencio
Silencio ¿Por qué un bosque? tención Garantiza cada estación tiene a la mayoría de un padre en el ESD; simplifica la operación sindical. Silencio
Silencio ¿Podemos usar un BST equilibrado en lugar de montones? Silencio BST da O(log n) pero necesitamos almacenar *sólo en línea* nodos – actualizaciones serían costosas. Saltos + eliminación perezosa es más simple. Silencio

-...

### 9. Consejos para entrevistas de Code‐Level

- **Comentario liberalmente** - explicar `find`, `lazyDelete`, etc.
- **Mostrar la compresión del camino** – mencionar `α(n)` es prácticamente constante.
- ** Uso de la memoria de alta luz** - `O(c)` vs. naive O(n2).

-...

#### 10. Resumen " Takeaway

- **DSU** le da identificación de componentes en tiempo casi constante.
- **Min‐heap** le da la estación más pequeña en línea rápidamente.
- **Lazy deletion** asegura que las actualizaciones fuera de línea son baratas.

Dominar este patrón demuestra que usted puede resolver problemas de gráficos a gran escala de manera eficiente – un deber-tener para cualquier ingeniero de software que busque para romper entrevistas de alta tecnología.

-...

### 11. Lectura adicional

- [Disjoint Set Union (Union‐Find)](https://cp-algorithms.com/data_structures/disjoint_set_union.html)
- [Priority Queues in Java/C++/Python](https://www.geeksforgeeks.org/priority-queue-in-cpp-using-stdpriority_queue/)
- [Tecnicas de eliminación de la vaquedad] (https://www.spoj.com/problems/KTH/)

-...

### 12. Pensamientos de clausura

Solving LeetCode 3607 con la estrategia DSU + Min‐Heap no se trata sólo de pasar un juez en línea; se trata de comunicar **graph intuition + destreza de estructura de datos** a un gerente de contratación.
Presente el problema en sus propias palabras, muestre el diagrama del algoritmo, e impresionará incluso a los entrevistadores más experimentados.

■ **Pon tu perfil de ingeniero hoy en día – practica esta solución y mira a los reclutadores notar tus habilidades de codificación graficas!* *

-...

### 13. Nota final

Happy coding, y que sus estaciones fuera de línea permanezcan *online* durante las entrevistas!

-...

■ **End of Blog**

-...

Esto completa la respuesta completa: usted tiene los códigos en los tres idiomas y un artículo pulido y listo para la entrevista que demuestra la comprensión profunda del algoritmo subyacente. ¡Buena suerte!