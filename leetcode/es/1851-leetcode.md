-...
Título: LeetCode 1851. Intervalo mínimo para incluir cada consulta -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1851 – Intervalo mínimo para incluir cada consulta
## Full‐stack solutions (Java Silencio Python Silencio C++)

A continuación encontrará tres implementaciones completas, preparadas para la producción de la solución barrido + prior-queue más eficiente.
Los tres comparten la misma idea central:

1. **Ordenar** intervalos por hora de inicio.
2. **Ordenar** consultas por valor (conservar sus índices originales).
3. Por cada consulta
* empuje cada intervalo cuyo inicio ≤ `q` en un **min-heap** ordenado por longitud de intervalo.
* pop cada intervalo cuyo fin se hizo `q` (no puede cubrir la consulta).
* la parte superior del montón es el intervalo más mínimo válido – su longitud es la respuesta para esa consulta.
4. Restaurar las respuestas en el orden original de la consulta.

La solución funciona
**O(n + m) log(n + m))** tiempo y **O(n + m)** espacio – lo suficientemente rápido para los límites (≤ 105 intervalos " consultas).

-...

#### ## 1down⃣ Java

``java
importar java.util*;

*
* Leetcode 1851 – Intervalo mínimo para incluir cada consulta
*
* El algoritmo utiliza una línea de barrido + min-heap.
* • Los intervalos se procesan en orden de tiempo de inicio.
* • Las consultas se procesan en orden ascendente.
* • Una cola prioritaria mantiene sólo intervalos que podrían contener la consulta actual.
* La parte superior de la cola siempre da el intervalo más pequeño que cubre la consulta.
*/
Solución de la clase pública {}
int[] minInterval(int[] [] intervalos, preguntas int[] {}
// Ordenar intervalos por hora de inicio
Arrays.sort(intervalos, Comparator.comparingInt(a - título a[0]));

// Pare cada consulta con su índice original
int[][] qWithIdx = nuevo int[queries.length][2];
para (int i = 0; i) hice consultas.length; i++) {
qWithIdx[i][0] = consultas[i]; // valor
qWithIdx[i][1] = i; // posición original
}
// Ordenar consultas por valor
Arrays.sort(qWithIdx, Comparator.comparingInt(a - título a[0]));

// Min‐heap ordenados por intervalo de longitud (end - start + 1)
PriorityQueue madeint[] Heap =
nuevo PriorityQueue quiso decir(Comparador.comparingInt(a - título a[0] - a[1] + 1));

int[] result = nuevo int[queries.length];
int intervaloIdx = 0; // puntero en intervalos

para (int[] q : qWithIdx) {
int value = q[0];
original Idx = q[1];

// Añadir todos los intervalos que comienzan <= consulta actual
mientras (intervalIdx) se realizaban intervalos.length " curvas [intervalIdx][0] 0 = valor) {
heap.offer(intervalos[intervalIdx++]); // almacenar todo el intervalo
}

// Eliminar intervalos que terminaron antes de la consulta
mientras (!heap.isEmpty() " heap.peek()[1] 0 valor nominal) {
heap.poll();
}

// La parte superior del montón es el intervalo más corto que cubre la consulta
resultado[originalIdx] = heap.is
? -1
: heap.peek()[1] - heap.peek()[0] + 1;
}

Resultado de retorno;
}
}
`` `

-...

#### 2down⃣ Python

``python
importación heapq
de la importación Lista

Solución de clase:
def minInterval(self, intervalos: List[List[int]], consultas: List[int] List[int]:
"
Línea de sudor + cola de prioridad.

Hora : O(n + m) log(n + m)
Espacio : O(n + m)
"
# 1. Ordenar intervalos por hora de inicio
intervalos.sort(key=lambda x: x[0])

# 2. Adjuntar índices originales a las consultas
qs = ordenados([(q, i) para i, q en enumerate(queries)])

# 3. Min-heap hold (length, end)
*

as = [0] * len(queries)
i = 0 # puntero en intervalos

para q, idx en qs:
# añadir todos los intervalos que comienzan #
mientras que yo hice len(intervalos) y intervalos [i][0] ANTE:
inicio, final = intervalos[i]
heapq.heappush(heap, (end - start + 1, end)
i += 1

# eliminar intervalos que terminaron antes de q
mientras saltaba y saltaba[0][1] q:
heapq.heappop(heap)

# Respuesta para esta consulta
ans[idx] = heap[0][0] si salta más -1

Retorno
`` `

-...

#### 3down⃣ C++

``cpp
#include יbits/stdc++.h
usando std namespace;

/*
* Leetcode 1851 – Intervalo mínimo para incluir cada consulta
* Línea de sudor con priority_queue (min‐heap).
*/
Clase Solución {
public:
vector implicado minInterval(vector identificadovector seleccionador seleccionados)
vectoriales: {}
// 1. Ordenar intervalos por inicio
(intervalos.begin(), intervalos.end(),
[](cont auto cho a, const auto golpe b) { return a[0] ANTE b[0]; });

// 2. Mantener índices originales de consultas
vector asignadopair observadoint,intenta título q(queries.size());
para (size_t i = 0; i) ++i) {
q[i] = {queries[i], static_cast fielint(i)};
}
(q.begin(), q.end(),
[](cont auto cho a, const auto golpe b) { devolver a.first Identificado b.first; });

// 3. Min-heap ordenados por intervalo de longitud
usando pii = par hecho,intenta; // {longitud, extremo}
priority_queue hacíapii, vector asignadopii confianza, mayor pq;

vector:
tamaño_t i = 0; // puntero en intervalos

para (auto [val, idx] : q) {
/ // intervalos de empuje que comienzan
mientras (i) se realizaron intervalos.size() " intervalos [i] [0]  made= val) {
int len = intervalos[i][1] - intervalos[i][0] + 1;
pq.emplace(len, intervalos[i][1]);
++i;
}
// intervalos de pop que terminan antes de la consulta
mientras (!pq.empty() " curva pq.top().
pq.pop();

ans[idx] = pq.empty() ? -1 : pq.top().first;
}
devolver los ans;
}
};
`` `

Las tres implementaciones utilizan la misma estrategia de barrido + prior-queue y se ejecutan cómodamente bajo las limitaciones del problema.

-...

# SEO‐Optimized Blog Post
**Título:** 1851 – Intervalo mínimo para incluir cada consulta: Sweep‐Line + Heap en Java, Python, C++*

**Meta Descripción:**
Solve Leetcode 1851 en milisegundos. Aprenda la estrategia de búsqueda de prioridad + línea barrido, Java completo, Python, C++ códigos, y por qué supera la fuerza bruta. Perfecto para entrevistas de codificación, práctica de algoritmos y preparación de entrevistas.

-...

## 1down Por qué este problema importa
Cuando estás preparando una entrevista de codificación, *las consultas de la intervaloración* aparecen todo el tiempo: “Encuentra el segmento más pequeño que contiene este punto. ”
Leetcode 1851 (Intervalo mínimo para incluir cada consulta) es un ejemplo canónico que prueba:

- **Sorting skills** – usted debe ordenar intervalos y consultas eficientemente.
- **Greedy + Sinergía de estructura de datos** – el intervalo de cobertura más corto no es obvio sin un montón.
- ** Cambios en el espacio-tiempo** – fuerza bruta TLE; solución óptima debe ser sub-cuadratica.

Si clavas esto, tendrás problemas similares en entrevistas reales y aumentarás tu confianza algorítmica.

-...

## 2down Good Good – The Elegant Sweep‐Line + Heap Approach
**Por qué es bueno:**

TENIDO Aspecto TENIDO Lo que te da ANTERIOR Por qué importa
Silencio...
TEN **O(n+m) log(n+m))** TENIDO Rápido para 105 intervalos/preguntas ANTERI Entrevista-ready performance ANTE
Silencio **Sólo un paso** Silencio No anidados bucles TENIDO Memoria > CPU amigable TEN
tención **Lógica azul** Silenciosa "Agregar cuando comienza ≤ q, pop cuando termina י q" Silencio fácil de explicar " debug ¦
Silencio ** Patrón reutilizable** Silencio Trabaja para otros problemas de frecuencias Silencio Construye un kit de herramientas de codificación

### Key Insight

En un punto de consulta `q` sólo necesita intervalos que:

- empezar ** q** (otros no pueden cubrirlo)
- final **≥ q** (otros han expirado)

El *smallest* tal intervalo es lo que el min‐heap le da al instante.

-...

## 3down Bad – Brute‐Force, Hash Maps o Two‐Pointer Missteps
**Pocaciones comunes** que conducen a soluciones “malas”:

- ** Hash mapa de inicios → longitudes** – O(n+m) para construir pero todavía requiere escanear *todos* intervalos para cada consulta → **O(n · m)**.
- **Dos puntos con un vector** – sin un montón no se puede garantizar el intervalo más corto.
- **Binary search on a classified list of lengths** – you’d need to know whether each length can still cover `q`; that’s the same as the heap, but re-implementing it manually is error‐prone.

■ **Bottom line:**
■ Brute‐force (`for q en consultas: para intervalos en intervalos`) toma ~109 operaciones → TLE.
■ Cualquier solución que haga **más que trabajo lineal** suele ser sospechosa de este problema.

-...

## 4Getly - Why Brute‐ Fallos de la fuerza
Si eres nuevo en el problema puedes probar un bucle anidado o un simple mapa de longitudes de intervalo.
¿Qué pasa? #

1. **Hora cuadrada** – 105 × 105 = 1010.
2. **Cache misses** – Acceso a la memoria aleatoria en un gran vector.
3. **Hard to trace** – Incluso un pequeño error (off-by-one en longitud) puede hacer que toda la solución sea errónea.

Los entrevistadores les encanta explicar *por qué* una solución ingenua es inaceptable. Muéstrales que sabes las trampas y por qué gana el montón.

-...

## 5down The Implementation (Pseudo‐Code)

`` `
intervalos de tipo por inicio
par consultas con índices originales
clasificar las consultas por valor

heap = min‐heap ordenados por longitud de intervalo

intervaloPtr = 0
para valor, origIdx en consultas clasificadas:
mientras intervalo Ptr  detectado intervalos. tamaño y intervalos[intervalPtr].start 0 = valor:
intervalos de presión[intervalo Ptr en el montón
intervalo Ptr++

Mientras no salta vacío y salta. top.end
pop heap

respuesta[origIdx] = salto vacío? -1 : heap.top.length
`` `

■ Este pseudocódigo es lingüístico-agnóstico; los tres fragmentos de código arriba son sólo un reemplazo de goteo para el idioma con el que estás cómodo.

-...

Desglose de la complejidad
Silencioso Operación Silencioso Complejidad
Silencio----------------------------...
TENCIÓN intervalos de clasificación TENIDO **O(n log n)** TENIDO Paso simple clasificación TENIDO
Silencio Ordenando consultas Silencio **O(m log m)** Silencio Necesitado para procesar en orden
Silencio Operaciones de Heap (push/pop) Silencio **O(n+m) log n)** Silencio Cada intervalo y las causas de la consulta a la mayoría de un empujón o pop Silencio

Total: **O(n+m) log(n+m))** tiempo, **O(n + m)** memoria.

-...

## 7VIEW⃣ Common Interview Questions Around This Problem

1. **“¿Puede explicar la elección avaricia?”* *
*Respuesta:* En cualquier consulta `q` consideramos sólo intervalos que podrían cubrirlo. El min‐heap garantiza que elijamos el uno con la longitud más pequeña inmediatamente. ”

2. ** ¿Y si dos intervalos tienen la misma longitud?* *
*Respuesta:* “El montón es estable para longitudes iguales porque también almacenamos el punto final – no afecta la corrección, sólo el orden de ruptura de la corbata. ”

3. **“¿Cómo adaptarías esto si las consultas llegaran en orden arbitrario (no ordenados)?”* *
*Respuesta:* “Aún las clasificas internamente, pero recuerda almacenar el índice original para que puedas volver a montar la salida al final. ”

-...

Pensamientos Finales > Consejos de Entrevista

- **Mostrar el patrón** – barrido + montón es un potente combo.
- ** Casos de emergencia** – prueba con consultas fuera de todos los intervalos y intervalos de longitud 1.
¿Por qué un montón? – decir “Porque necesitamos la longitud * mínima* en todo momento. ”
- **Practice** - resolver problemas similares: *Meeting Rooms II*, *Car Fleet*, *Interval Cover*, *Maximum Overlap*, etc.

Mastering Leetcode 1851 le da un bloque de construcción algorítmico reutilizable que usted puede traer con confianza en cualquier entrevista de estructura de datos. ¡Buena suerte! 🚀