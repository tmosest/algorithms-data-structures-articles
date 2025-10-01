-...
Título: LeetCode 1834. -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1834 – “CPU Panteada”
**Java Silencio Python ← C+** – Soluciones completas y de producción + un *completo blog* que habla de lo bueno, lo malo y lo feo**.
Utilice esto para crear su próxima entrevista de codificación, aumentar su currículum e impresionar a los reclutadores.

-...

### ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## #

Se le da una serie de tareas:

`` `
tareas[i] = [enqueueTimei, procesamiento Timei]
`` `

* `enqueueTimei` – cuando la tarea está disponible.
* `procesandoTimei` - cuánto tiempo se tarda en terminar.

La CPU está sola:
1. Si es ocioso y ninguna tarea está lista → permanecer ocioso.
2. Si está ocioso y hay tareas listas → elegir el uno con el tiempo de procesamiento ** más corto**.
- Tie → elegir el índice más pequeño ****.
3. Una vez que una tarea comienza se termina.

Devuelve el orden de índices que la CPU procesará.

-...

### 🎯 Optimal Solution Outline

1. **Sort** tareas por `enqueue Hora.
2. Use un **min-heap** (`PriorityQueue` en Java, `priority_queue` en C++, `heapq` en Python) keyed by `(processingTime, index)`.
3. Camina por la lista clasificada mientras:
* Add all tasks whose `enqueue Tiempo 0 = Tiempo actual` al montón.
* Si salta vacío → saltar `currentTime` a la siguiente tarea 'encuue Hora.
* Pop from heap → tarea de proceso → actualización `current Tiempo += ProcesamientoTiempo.
4. Almacene índices en el array de respuesta.

El algoritmo es `O(n log n)` debido a la clasificación + operaciones de salto, con `O(n)` memoria.

-...

##  Settlements Code Implementations

## Java

``java
importar java.util*;

Solución de la clase pública {}
Clase estática privada {
int idx, enqueue, process;
Task(int idx, int enqueue, int process) {
esto.idx = idx;
esto. enqueue = enqueue;
esto. proceso = proceso;
}
}

int[] getOrder(int[][][] tareas) {
int n = tasks.length;
Task[] arr = new Task[n];
para (int i = 0; i)
arr[i] = nuevo Task(i, tasks[i][0], tasks[i][1]);

// 1 / Clasificar por tiempo de encuado
Arrays.sort(arr, Comparator.comparingInt(t - título t.enqueue));

// 2Ω⃣ Min‐heap: primero por proceso, luego por idx
PriorityQueue se realizóTask confidencial pq = nueva PrioridadQueue se obtuvo(
Comparador.
.thenComparingInt(t - título t.idx));

int[] ans = nuevo int[n];
int ptr = 0; // puntero en arrr ordenados
tiempo largo = 0; // tiempo actual, utilizar largo para evitar el desbordamiento
int ansIdx = 0;

mientras (ptr יnt n TENIDO TENIDO!pq.isEmpty()) {}
// Empuja todas las tareas que han llegado
mientras que (ptr ecto n " prórr[ptr]. enqueue <= curTime) {
pq.offer(arr[ptr++]);
}

si (pq.isEmpty()) {
Task cur = pq.poll();
ans[ansIdx++] = cur.idx;
curTime += cur.process;
. ♫ ... {
// No hay tarea lista → saltar a la siguiente llegada
curTime = arrr[ptr].enqueue;
}
}
devolver los ans;
}
}
`` `

## Python

``python
importación heapq
de la importación Lista

Solución de clase:
def getOrder(self, tasks: List[List[int]) - No. List[int]:
# Attach index
tareas = [(e, p, i) para i, (e, p) en enumerado(tasks)]
tasks.sort() # sort by enqueue time

res = []
pq = [] # montón de (proceso, índice)
tiempo = 0
I = 0
n = len(tasks)

mientras yo no o pq:
# Add all ready tasks
mientras que yo hice n y tareas [i] [0]
e, p, idx = tasks[i]
heapq.heappush(pq, (p, idx))
i += 1

si pq:
p, idx = heapq.heappop(pq)
tiempo += p
re.append(idx)
más:
# Idle - saltar al siguiente tiempo de encuar
tiempo = tareas[i][0]

retorno
`` `

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vectorial: conseguirOrder(vector seleccionador) tareas) {
struct Task { long long e, p; int idx; };
vector asignadoTask confidencial v;
para (int i = 0; i) ++i)
v.push_back({tasks[i][0], tasks[i][1], i});

(v.begin(), v.end(),
[](contTarea limitada a, const Task limitada b){ devuelva a.e; });

priority_queue hicistepair realizado largo,int
vector asignadopair llevado largo largo,int.
mayor significación hecha larga, un título de propiedad intelectual largo pq; // (proceso, idx)

vector significar uns
Cura larga larga = 0;
int i = 0, n = v.size();

mientras (i י n ¦ {}
mientras (i י n ' t ' v[i].e = cur) {
pq.emplace(v[i].p, v[i].idx);
++i;
}

si (pq.empty()) {
auto [proc, idx] = pq.top(); pq.pop();
ans.push_back(idx);
cur += proc;
. ♫ ... {
cur = v[i].e;
}
}
devolver los ans;
}
};
`` `

-...

## 📝 Blog Article – “The Good, The Bad, and the Ugly of LeetCode 1834”

■ **SEO Palabras clave**: *Single‐Threaded CPU LeetCode 1834*, *Java solution*, *Python solution*, *C++ solution*, *fastest task scheduler*, *interview coding interview*, *job interview preparation*, *algorithm explanation*, *min-heap*, *priority queue*.

-...

#### ## 1down⃣ El Bien

TENIDO VALORAR Característica ANTERIOR Por qué es genial
Silencio...
Silencio **Escaneo de línea + montón** Silencio Maneja hasta 105 tareas en `O(n log n)`. Silencio
Silencio **Determinación de la corbata determinista** Silencio Ordenar por índice garantiza la regla del “índice más sólido”. Silencio
Silencioso **La lógica del vacío de cabeza** Silencio Skips inútil tiempo ocioso, haciendo que el tiempo de ejecución sea óptimo. Silencio
TEN **Código legible** TEN Java, Python y C++ versiones son concisas pero claras. Silencio

- **La complejidad del tiempo**: `O(n log n) `
- **La complejidad del espacio**: `O(n)` (para el montón + lista clasificada)

-...

#### 2down⃣ El malo

Н нели вали Edición ный Corrección / Mitigación Silencio
Silencio...
Silencio **Overflow risk** tención Use `long long`/`long` for current time because enqueue/processing times can be up to 109. Silencio
tención **Sorting stability** Silencio Garantizar que las tareas se ordenen estrictamente por tiempo encuado; la corbata de índice no importa después de las clases de heap por tiempo de procesamiento. Silencio
Silencio ** Casos de emergencia** Silencio - Todas las tareas llegan al mismo tiempo. ¿CPU va para siempre al final? (nunca sucede porque las tareas son finitas). Silencio

-...

#### 3down⃣ El Ugly

¿Qué puede pasar mal? Silencio
Silencio...
tención **Mis-ordered heap comparator** ← Mixing `processingTime` y `index` en el orden incorrecto da resultados incorrectos. Silencio
Silencio **O(n2) bucle ingenuo** Silencio Algunas soluciones empujan todas las tareas en un montón y luego las abren todas, incluso cuando la CPU va ocioso, esto todavía funciona pero es sub-optimal. Silencio
Silencio **Usando `queue` en lugar de `priority_queue`** Silencio Una cola de FIFO ignora la regla de “tiempo de procesamiento más corto”. Silencio
Silencio **No avanzar el tiempo cuando idle** Silencio conduce a un bucle infinito porque el tiempo actual nunca aumenta. Silencio

-...

#### 4down⃣ Consejos para entrevistas

1. **Explicar la intuición primero** – hablar de “soberbio por llegada, utilizar un min-heap para tareas listas”.
2. **Discuss time/space** – A los reclutadores les encanta ver el argumento `O(n log n)`.
3. ** Casos de borde de fusión** – mostrar que usted pensó en todas las tareas que llegan a la vez o CPU idling.
4. **Mostrar las características del lenguaje actualizado** – por ejemplo, el 'Comparador' de Java.comparador Int`, Python's `heapq`.
5. **Probar casos de prueba** – los dos ejemplos dados + algunos personalizados (por ejemplo, todos los mismos encuue, tarea única).

-...

#### 5down⃣ Pensamientos finales

LeetCode 1834 es un problema clásico *priority‐queue*.
El truco no es sobre-pensar la estructura de datos; una vez que veas “siempre elige el trabajo más corto” estás haciendo esencialmente *Shortest‐Job‐First (SJF)* programación.
Con los fragmentos de código arriba, usted está listo para dejar la solución correcta en su próxima entrevista de codificación y alejarse con un impulso de confianza.

-...

### 🔗 Quick Links

- [LeetCode 1834 – Single-Threaded CPU](https://leetcode.com/problems/single-threaded-cpu/)
- [Java Solution (GitHub Gist)] (https://gist.github.com/yourusername/1234567)
- [Python Solution (Pastebin)](https://pastebin.com/yourcode)
- [C++ Solution (GitHub)](https://github.com/yourusername/leetcode-1834)

Buena suerte, ¡y que la CPU esté a su favor! 🚀