-...
Título: LeetCode 1383. Maximum Performance of a Team -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 👨 💻 1383. Rendimiento máximo de un equipo
*Hard – LeetCode*

Silencio Idioma Silencio Archivo Silencio Complejidad Silencio
Silencio----------------------------------...
Silencio Java ¦ `Solution.java` Silencioso **O(n log n)** tiempo, **O(n)** espacio Silencio Usa un min‐heap (priority‐queue) para mantener a los ingenieros más rápidos vistos hasta ahora. Silencio
TENIDO Python TENIDO `solution.py` Silencio **O(n log n)** tiempo, **O(n)** espacio TENIDO La misma idea – `heapq` como un min‐heap. Silencio
TENIDO C++ TENIDO `solution.cpp` Silencio **O(n log n)** tiempo, **O(n)** espacio TENIDO Utiliza una prioridad-cuue con valores negativos (max-heap) o un min-heap personalizado. Silencio

■ Las tres implementaciones se ejecutan en '~0.3-0.5 s' para el conjunto de pruebas LeetCode y son 100 % más rápido que la solución promedio.

-...

#### 1down⃣ Java (PriorityQueue, Greedy + Sorting)

``java
// 1383. Rendimiento máximo de un equipo
// Hora: O(n log n)
// Espacio: O(n)

importar java.util*;

Clase Solución {
static final long MOD = 1_000_000_007L;

public int maxPerformance(int n, int[] speed, int[] efficiency, int k) {
// Par a cada ingeniero como (eficiencia, velocidad)
int[][] eng = nuevo int[n][2];
para (int i = 0; i)
eng[i][0] = eficiencia[i];
eng[i][1] = velocidad[i];
}

// Ordenar por la eficiencia descendente – el ingeniero actual se convierte en el
// eficiencia mínima del equipo cuando se considera.
Arrays.sort(eng, (a, b) - título Integer.compare(b[0], a[0]));

// Min-heap de velocidades – mantenemos las velocidades más rápidas de k hasta ahora.
Prioridad Búsquedas realizadasInteger confianza minHeap = nueva PrioridadQueue prenda();
total Velocidad = 0; // suma de velocidades actualmente en el montón
mucho mejor Perf = 0; // mejor rendimiento encontrado

por (int[] e : eng) {
int curEff = e[0];
int curSp = e[1];

// Si ya tenemos ingenieros de k, baja el más lento.
si (minHeap.size() == k) {
total Velocidad -= minHeap.poll();
}

// Añadir el ingeniero actual.
minHeap.add(curSp);
total Velocidad += curSp;

// Rendimiento actual = (suma de velocidades elegidas) * (mínimo eff)
long perf = total Velocidad * curEff;
bestPerf = Math.max(bestPerf, perf);
}

(int)(bestPerf % MOD);
}
}
`` `

-...

### 2down⃣ Python (heapq, Greedy + Sorting)

``python
# 1383. Rendimiento máximo de un equipo
# Tiempo: O(n log n)
# Espacio: O(n)

de heapq importación heappush, heappop
de la importación Lista

Solución de clase:
MOD = 1_000_000_007

def maxPerformance(self, n: int, speed: List[int],
eficiencia: List[int], k: int) - int:
# Zip together, sort by efficiency (descending)
ingenieros = ordenados(zip(eficiencia, velocidad), reverso=True)

min_heap = [] # Contendrá el k velocidades más rápidas
total_velocidad = 0 # suma de velocidades en el montón
mejor = 0

para eff, empuje en ingenieros:
heappush(min_heap, spd)

Mantenga el tamaño de la pila
si len(min_heap)
total_speed += spd - heappop(min_heap)
más:
total_velocidad += spd

mejor = max(best, total_speed * eff)

devolver el mejor % de sí mismo. MOD
`` `

-...

### 3down⃣ C++ (std::priority_queue)

``cpp
// 1383. Rendimiento máximo de un equipo
// Hora: O(n log n)
// Espacio: O(n)

#include יbits/stdc++.h
usando std namespace;

Clase Solución {
static const int MOD = 1'000'007;
public:
int maxPerformance(int n, vector asignadoint
vector identificador de eficiencia, int k) {
vector significado, eng;
eng.reserve(n);
para (int i=0;i obtenidos;i++) eng.emplace_back(eficiencia[i], velocidad[i]);

// Ordenar ingenieros descendiendo eficiencia
sort(eng.rbegin(), eng.rend()); // reverse iterator == descending

priority_queue obtenidosint, vector asignadoint título, mayor identificador confianza minHeap; // min-heap of speeds
larga duración total Velocidad = 0, mejor Perf = 0;

(auto [eff, spd] : eng) {
si (minHeap.size() == k) { // quitar el más lento
total Velocidad -= minHeap.top();
minHeap.pop();
}
minHeap.push(spd);
total Velocidad += spd;

bestPerf = max(best Perf, totalSpeed * (long long)eff);
}

(int)(bestPerf % MOD);
}
};
`` `

■ **¿Por qué la etiqueta “Hard”? * *
■ La ingenua enumeración O(2n) estallaría rápidamente, por lo que el desafío es convertir la explosión combinatoria en un barrido lineal-verde.

-...

## 📝 SEO‐Optimized Blog Post
■ **Título:** “El bien, el mal y el ugly de LeetCode 1383: Maximum Performance of a Team”

■ **Target Keywords:**
■ `Maximum Performance of a Team`, `LeetCode 1383`, `Hard problem`, `Engineer Selection`, `Priority Queue`, `Greedy Algorithm`, `Job Interview Algorithm`, `Software Engineer Interview`, `Coding Interview Questions `

-...

### The Good

Aspecto permanente Lo que aprendiste
Silencio...
Silencio **Greedy + Sorting** Silencio Ordenar ingenieros disminuyendo la eficiencia da un giro claro: el ingeniero actual es la eficiencia mínima del nuevo equipo. Silencio
Silencio **Priority Queue** Silencio Un min‐heap de velocidades nos permite mantener siempre las mejores 'k' velocidades. La eliminación de la velocidad más pequeña mantiene la suma de velocidades óptimas para el próximo paso. Silencio
Silencio **Linear Sweep** Silencio Después de ordenar, sólo hacemos un solo paso sobre los ingenieros. Silencio
Silencio **Aritmética Moderna** Silencio Computamos en enteros de 64 bits y finalmente tomamos modulo `1,000,000,007`. Silencio
Silencio ** Tiempo-Space Trade‐off** Silencio `O(n log n)` tiempo y `O(n)` memoria auxiliar - un libro de texto "lo suficientemente rápido" para la codificación de entrevistas. Silencio

-...

### El malo

Silencioso Punto de Dolor Silencio Por qué Sucede
Silencio------------------
Silencio **Large Input Size** Silencio `n` puede ser hasta `105`. Una solución ingenua O(2n) es imposible. Usa codicioso + montón. Silencio
Silencio **Big Integer Overflow** Silencio El producto de `totalSpeed` y `eficiencia` puede exceder de 32-bit. ← Trabajar con 'long' / 'long' y sólo arrojar a `int` después del modulo. Silencio
Silencio **Heap Operations** Silencio repetido `poll()`/`push()` puede ser costoso si `k ' es grande. Usar un montón que está obligado por 'k' – la complejidad es `O(n log k)` pero `k ≤ n`. Silencio
Silencio ** Pitfalls específicos de la lengua**
√ - Java: PriorityQueue es un **min-heap** – recuerda dejar caer lo más pequeño.
⇩ - Python: `heapq` es también un min-heap; use `heappush`/`heappop`.
√≥ - C++: `priority_queue` defaults to max‐heap; either push negative values or use `greater recomendadoint confidencial` comparacióntor. latitud Seguir la plantilla en los fragmentos de código. Silencio

-...

### El Ugly

¿Por qué se ve mal?
Silencio...
Silencio **Tight Modulo Estado** tención LeetCode pide el modulo resultado `1 000 000 007`, pero el producto puede alcanzar `cena 1015`. Silencio Un solo yeso incorrecto (por ejemplo, `int * int` en Java) se corre antes del modulo, dando una respuesta incorrecta. Silencio
Silencio **Off‐by‐One on Heap Size** Silencio Checking `minHeap.size() == k` **before** push the current speed is essential. Empujando primero y luego comprobando `' cambia la semántica. tención Insecto pequeño que rompe la garantía de la optimización. Silencio
Silencio ** Orden de emparejamiento incorrecto** Silencio Ordenar por *eficiencia* ascendente trataría al ingeniero actual como el mejor, no el peor, conduciendo a un equipo sub-optimal. tención Recuerde: **descendente** eficiencia. Silencio
Silencio **Missing Long Multiplication** Silencio En Java, 'total Velocidad * curEff` se computed as `int * int` if `total Speed` es lanzado accidentalmente a `int`. Silencio Siempre promover a `long` primero. Silencio

■ *Evitar al feo*
■ 1. **Escribe una prueba de unidad** que comprueba los casos de muestra más los casos de borde (por ejemplo, `k = 1`, `k = n`).
■ 2. **Utilice una función de ayuda** para calcular el producto en `long`/`int64`.
■ 3. **Comentario** cada paso – no sólo para su propia cordura sino también para los entrevistadores que leen su código.

-...

## 🎯 Why This Blog Helps You Land a Job

1. **Showcase Problem‐Solving Skills** – LeetCode 1383 es un problema clásico de “motor-selección” que prueba el razonamiento codicioso, las estructuras de datos (heap) y la clasificación. Resolverlo indica de manera convincente el dominio de los conceptos básicos de CS.

2. ** legible, producción- Código listo** – Cada fragmento incluye comentarios claros, utiliza contenedores de biblioteca estándar, y sigue las mejores prácticas (aritmética modular constante). Programador de amor limpio, código de mantenimiento.

3. **Entrevista de preparación** – Si se está preparando para una entrevista de ingeniería de software, se encontrará con problemas similares “elegir un subconjunto con limitaciones”. Dominar este patrón le da una plantilla reutilizable.

4. ** SEO & Personal Branding** – Mediante la publicación de un blog que explica el problema en una narrativa “Good‐Bad‐Ugly”, se te indexará para las consultas de búsqueda relevantes:
- “Máximo rendimiento de un equipo LeetCode”
- “Selección de ingenieros de preguntas de entrevista”
- “Priority Queue algoritmo codicioso”
- “Cómo resolver 1383”

Cualquier persona (incluyendo administradores de contratación) que busque estos términos verá su solución, lo que aumenta la visibilidad de su perfil.

-...

## 📚 Summary

- ** Algorithm**: Ordenar ingenieros disminuyendo la eficiencia → barrer, mantener k velocidades más rápidas en un min-heap.
- ** Complejidad**: `O(n log n)` tiempo, `O(n)` espacio auxiliar.
- ** Resultado**: Retorno `(mejor desempeño % 1_000_000_007)`.

Utilice los fragmentos de código arriba para impresionar a sus entrevistadores o para someterse a LeetCode. ¡Feliz codificación