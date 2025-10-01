-...
Título: LeetCode 3422. Operaciones mínimas para hacer que los elementos subarray sean iguales -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Mastering LeetCode 3422
## Operaciones mínimas para hacer iguales los elementos de subarray
**El Bien, el Mal, y el Ugly** – Una guía completa (Java / Python / C++)

-...

Problema Recap

■ **Given** un array entero `nums` y un entero `k`.
■ Usted puede aumentar o decrementar cualquier elemento de `nums` por `1` cualquier número de veces.
■ ** Objetivo:** Encontrar el número mínimo de operaciones requeridas para que *al menos una* sub-array del tamaño `k` contenga **todos los elementos iguales**.

`` `
Entrada: nums = [4,-3,2,1,-4,6], k = 3
Producto: 5
`` `

-...

### 🧠 Why This Problem Rocks

* **La estrella de entrevista real** – aparece en muchas listas de reproducción “medianamente activas”.
* ** Profundidad conceptual** – combina *ventanas deslizantes*, *mediana*, *con balanceo de salto*, y * sumas de prefijo*.
* **Hard‐to-spot pitfalls** – manipulación de duplicados, números negativos, y mantener la mediana eficientemente.

-...

## 1. El enfoque ingenuo - Qué NO hacer

``text
Por cada ventana de tamaño k
Por cada valor x de -10^6 a 10^6
Cuenta operaciones para hacer ventana todo x
`` `

* **Tiempo:** O(n * (range)) → imposible.
* **Espacio:** O(1).

**Lesson:** Necesitas una mediana *dinámica*, no un escáner de fuerza bruta.

-...

## 2. The Winning Strategy – Sliding‐Window Median

1. **Elige el valor objetivo** – la mediana de la ventana actual da la suma mínima de diferencias absolutas.
2. **Mantengan dos montones**
* `low` (max‐heap) – la mitad inferior de la ventana
* `alto' (min-heap) - la mitad superior
3. **Mantenga las sumas de funcionamiento**
* `sumLow` – sum of elements in `low`
* `sumHigh` – sum of elements in `high `
4. *Sliding*
* Insertar el nuevo elemento en uno de los montones.
* Eliminar el elemento saliente (supresión perezosa o multiset).
* Reequilibrio de modo que `responder a la vida eterna'.
* Compute current cost:
``cost = mediana * low.size() - sumLow + sumHigh - median * high.size()` `
5. **Track the minimum cost** across all windows.

**Las complejidades* *

Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio Cada operación Silencio O(log k) Silencio O(k) (heaps + lazy‐del sets)
Silencio Entire pass Silencio O(n log k) Silencio O(k)

-...

## 3. Aplicación del Código

A continuación se encuentran soluciones limpias y de producción en **Java**, **Python**, y **C+**.
Todos comparten la misma lógica pero usan estructuras de datos específicas para cada idioma.

■ **Tip:** Si estás en LeetCode, simplemente pega la clase 'Solution' al editor.
■ Si usted está preparando para un trabajo, copiar el archivo completo, añadir un `main()` para las pruebas locales, y empujar a su GitHub.

-...

### 3.1 Java – `TreeSet` + Two Heaps

``java
importar java.util*;

Solución de la clase pública {}
public long minOperations(int[] nums, int k) {
// Dos colas prioritarias: max‐heap (low), min‐heap (high)
Prioridad Búsquedas realizadasInteger bajos = nueva PrioridadQueue escogida(Collections.reverseOrder());
PriorityQueue se cumplióInteger confianza high = new PriorityQueue especificado();

// Para la eliminación perezosa: contar ocurrencias
Mapa seleccionadoInteger, Integer confianza toDelete = nuevo HashMap贸 conveniente();

long sumLow = 0, sumHigh = 0;
Ans largos = largo. MAX_VALUE;

// Lambdas ayudantes
java.util.function.IntConsumer add = (x) - { {
si (low.isEmpty() tención eterna x י= low.peek() {}
bajo.add(x); sumLow += x;
. ♫ ... {
alta.add(x); sumHigh += x;
}
balance();
};

java.util.function.IntConsumer remove = (x) - { {
// Marca para la eliminación
toDelete.put(x, toDelete.getOrDefault(x, 0) + 1);
// Quitar del montón apropiado lógicamente
si (x= bajo.peek()) sumLow -= x;
suma Alto -= x;
// Elementos superiores limpios si es necesario
cleanTop(low, toDelete);
cleanTop(high, toDelete);
balance();
};

java.util.function.VoidFunction balance = () - título {
// Tamaños de equilibrio: bajo.size()
mientras (bajo.size() + 1) {
int val = low.poll(); sumLow -= val;
alta.add(val); sumHigh += val;
cleanTop(low, toDelete);
cleanTop(high, toDelete);
}
mientras (alta.tamaño()
int val = high.poll(); sumHigh -= val;
bajo.add(val); sumLow += val;
cleanTop(low, toDelete);
cleanTop(high, toDelete);
}
};

java.util.function.LongSupplier getMedian = () - propiedades low.peek();

java.util.function.LongSupplier currentCost = () - {
long median = getMedian.getAsLong();
mediana de retorno * bajo.size() - sumLow + sumHigh - median * high.size();
};

// Construye la ventana inicial
para (int i = 0; i < k; i++) add.accept(nums[i]);
as = Math.min(ans, currentCost.getAsLong());

// ventana de diapositivas
para (int i = k; i)
add.accept(nums[i]);
remove.accept(nums[i - k]);
as = Math.min(ans, currentCost.getAsLong());
}

devolver los ans;
}

// Elementos superiores limpios que están marcados para la eliminación
vacío privado limpio Top(Prioridad Queue hacía Integer confianza heap, Map hacíaInteger, Integer confianza toDelete
mientras (!heap.isEmpty() " hastaDelete.getOrDefault(heap.peek(), 0)
int val = heap.poll();
toDelete.put(val, toDelete.get(val) - 1);
}
}
}
`` `

■ **Por qué funciona* *
* `low` mantiene la mitad * más baja*, por lo que su máx (top) es el medio.
" Lazy deletion evita costosas operaciones de `remove ' en `PriorityQueue`.
* Cada paso cuesta `O(log k)`.

-...

#### 3.2 Python – `heapq` + `Counter `

``python
importación heapq
de las importaciones de colecciones Contrato
de la importación Lista

Solución de clase:
def minOperaciones(self, nums: List[int], k: int) - confiar int:
bajo = [] # max‐heap (valores de inversión)
alto = [] # min‐heap
to_delete = Counter()
sum_low = sum_high = 0
as = flotante('inf')

def clean(heap):
and to_delete [heap[0]] 0:
val = heapq.heappop(heap)
to_delete[val] -= 1

def balance():
# Ensure len(low) ю= len(high)
len(low) не len(high) + 1:
val = -heapq.heappop(low)
limpio(bajo)
heapq.heappush (alto, val)
limpio(alto)
mientras len(alto)
val = heapq.heappop(high)
limpio(alto)

def add(x):
no local sum_low, sum_high
si no es bajo o x <= -low[0]:
heapq.heappush(low, -x)
sum_low += x
más:
heapq.heappush(high, x)
sum_high += x
Saldo()

def remove(x):
no local sum_low, sum_high
to_delete[x] += 1
si x <= -low[0]:
sum_low -= x
más:
sum_high -= x
limpio(bajo)
limpio(alto)
Saldo()

def median():
retorno -low[0]

def cost():
m = mediana()
volver m * len(low) - sum_low + sum_high - m * len(high)

Primera ventana
para i en rango(k):
add(nums[i])
as = min(ans, cost())

# Slide
para i en rango(k, len(nums)):
add(nums[i])
remove(nums[i - k])
as = min(ans, cost())

Retorno
`` `

■ **Highlights**
* `low` es un *max-heap* al almacenar negativos.
* " Counter " tracks which values should be ignored (`to_delete`).
* Todas las operaciones permanecen `O(log k)`.

-...

### 3.3 C++ – `multiset` + Alfabetizadores

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
largas minOperaciones largas(vector fieltro nums, int k) {
// multiset mantiene todo arreglado
ventana multiset significante;
larga suma = 0;
long long best = LLONG_MAX;

auto añadir = [fr](int x) {
ventana.insert(x);
suma += x;
};
autoextracción = [fr](int x) {
auto = ventana.find(x);
(it != window.end()) {
sum -= *it;
ventana.erase(it);
}
};

auto median = [ cl]() - título long {
auto = ventana.begin();
por adelantado(it, window.size() / 2); // Índice 0 basado en mediana
Regresar *it;
};

auto curCost = [ cl]() - Conf largo
long med = median();
long long leftSum = 0, rightSum = 0;
para (auto it = ventana.begin(); it != ventana.end(); ++it) {
si (*it ■= med) izquierda Sum += *it;
- Sí. Sum += *it;
}
larga izquierda Cnt = distance(window.begin(), window.find(med));
larga derecha Cnt = ventana.size() - leftCnt - 1;
// Costo = suma Silencioso - med habit
Regresar med * izquierda Cnt - izquierda Sum + derecha Sum - med * right Cnt;
};

// Construye primera ventana
para (int i = 0; i)
mejor = min(best, curCost());

/ Diapositiva
para (int i = k; i) ++i) {
add(nums[i]);
remove(nums[i - k]);
mejor = min(best, curCost());
}

devolver mejor;
}
};
`` `

■ **Por qué el multiset es el más limpio en C++**
* `multiset` da O(log k) inserción, eliminación y acceso iterador al medio.
* No es necesario que la leción perezosa – `erase(iterator)` elimina el elemento exacto.

-...

■ **Despegar el idioma del idioma* *
■ *Las tres soluciones* mantienen la ventana ordenada, conservan sumas y recomputan el coste mínimo en `O(log k)` por paso.

-...

## 4. Debugging & Edge‐Cases

Silencio Edge‐Case Silencio ¿Por qué importa?
Silencio...
Silencio **Números duplicados** Silencio Heaps/sets debe almacenar *exacto* ocurrencias. TENIDO Use `Counter`/`Counter` o `multiset` con iterators. Silencio
Silencio ** Valores negativos** Silencio La lógica mediana sostiene para cualquier entero, pero ten cuidado con el desbordamiento en C++. Silencio Use 64‐bit (`long') para todas las sumas. Silencio
Silencio. (1)** Silencio Cualquier ventana del tamaño 1 ya es igual. Regreso `0` temprano. Silencio
Silencio **Large `k` (≥ n)** Silencio Sólo una ventana. Silencio Construir una vez, saltar el bucle. Silencio

-...

## 5. Prueba de su solución

``python
def test():
sol = Solución()
afirmar sol.minOperaciones([4, -3, 2, 1, -4, 6], 3) == 5
afirmar sol.minOperaciones([1, 2, 3, 4, 5], 2) == 0
afirmar sol.minOperations(5,5,5,5], 4) == 0
print("Todas las pruebas pasadas!")
`` `

Ejecute el snippet localmente. En LeetCode, el arnés de prueba de LeetCode hará esto por ti.

-...

## 6. What Interviewers Care About

TENIDO Aspecto ANTERIOR Lo que buscan ANTERIOR Cómo nuestro Código lo muestra
Silencio------------operfecto----
Silencio ** Claridad algorítmica** tención Comprende mediana y fórmula de coste. tención Explicación arriba + comentarios en línea. Silencio
Silencio ** Manejo de maletas** Silencio Duplicados, negativos. tención Lazy deletion, uso `Counter`. Silencio
Silencio **La complejidad del tiempo** Silencioso `O(n log k)`. Silencio Cada operación es `log k`. Silencio
Silencio **Estilo de codificación** Silencio limpio, idiomático. Las mejores prácticas específicas del lenguaje (por ejemplo, 'Collections.reverseOrder()` en Java). Silencio

-...

## 7. SEO‐Optimized Blog – Cómo ayuda a su resumen

* Tito " Tags "
* `LeetCode 3422`, `Minimum Operations Subarray`, `Java solution`, `Python solution`, `C++ solution`, `sliding window median`, `algorithm interview`, `coding interview`, `software engineer`.

* **Meta Descripción (Ω160 chars)* *
“Solve LeetCode 3422 en Java, Python y C++. Aprenda la estrategia de mediana de ventana deslizante, obtenga análisis de espacio de tiempo y consejos de carrera para su próxima entrevista de ingeniería de software. ”

*Rich Snippets* Agregue un bloque JSON-LD para contenido *How‐to*.

``html
"Aplicación/ld+json"
{}
"@context": "https://schema.org",
"@type": "HowTo",
"Nombre": "Mastering LeetCode 3422: Operaciones mínimas para hacer iguales los elementos submarinos",
"descripción": "Una guía completa con soluciones Java, Python y C++ y conocimientos de entrevista".
"Paso":
{"@type":"HowToStep","text":"Understand the problem and why median is excellent."},
{"@type":"HowToStep","text":"Implement a sliding-window median usando dos montones."},
{"@type":"HowToStep","text":"Optimice para duplicados con deleción perezosa o multiset."},
{"@type":"HowToStep","text":"Validar contra las persianas y el análisis del tiempo/espacio."}
]
}
■/script título
`` `

* ** Enlace interno** – enlace a otras publicaciones del blog como “Two‐Pointer Tricks for Interviews” o “Heap Balancing Basics”.

* **Backlinks** – mencione el repob GitHub e invite a los lectores a estrellar el proyecto.

-...

## 🎯 Final Thoughts – Turning Code Into a Job

1. **Portfolio-ready code** – comprometer cada archivo, añadir pruebas unitarias, empujar a GitHub.
2. **Explicar el algoritmo** en un vídeo de 1 minuto o cubierta de diapositivas.
3. ** Periferias de práctica** – números negativos, duplicados, `k == 1`.
4. **Tiempo la solución** – una nota rápida de `tiempo de complejidad` en comentarios muestra que te preocupa el rendimiento.
5. **Mostrar toda la pila** – estar listo para explicar tanto *algorithm* como *implementation* a través de Java, Python y C++.

■ **Resultado:** Impresionará a los gerentes de contratación con una solución *full‐stack, lista para entrevistas* y un blog pulido que es amigable con SEO, demostrando que usted es un codificador y un comunicador.

¡Feliz codificación y buena suerte aterrizando ese papel de ingeniero de software! 