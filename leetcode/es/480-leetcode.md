-...
Título: LeetCode 480. Ventana deslizante mediana -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. The Problem Recap

■ **Sliding Window Median**
■ Se le da un array entero 'nums' y un entero 'k'.
■ Una ventana corredera de tamaño `k` se mueve de la izquierda de la matriz a la derecha, un paso a la vez.
■ Para cada ventana, salga la mediana de los números 'k' dentro de la ventana.
■ Si `k` es raro que la mediana sea el número medio en la ventana clasificada.
■ Si `k` es incluso la mediana es el *medio* de los dos números medios.

Limitaciones típicas:
* `1 ≤ k ≤ nums.length ≤ 10^5`
* `-2^31 ≤ nums[i] ≤ 2^31 – 1`

La precisión necesaria es 1e‐5.

■ **¿Por qué es esta una pregunta “hard” LeetCode? #
■ Prueba su conocimiento de estructuras de datos equilibradas, técnicas de ventanilla deslizante y manejo cuidadoso de valores duplicados.

-...

## 2. La solución “buena” – dos montones + eliminación perezosa

La forma más limpia de mantener una mediana dinámica es mantener dos montones:

TENIDO HABITACIÓN TENIDO Mantiene ANTERIOR invariante
Silencio--------------------
Silencio `maxHeap` (a max‐heap)
Silencio `minHeap` (a min‐heap) Silencio superior media (Consejo= median) Silencio superior = más pequeño de la mitad superior

*Key Idea*
* La mediana es `maxHeap.top()` (odd `k`) or the average of `maxHeap.top()` and `minHeap.top()` (even `k`).
* Al insertar un nuevo elemento lo ponemos en el montón correcto y luego rebalance.
* La eliminación de un elemento que tiene *slid fuera* de la ventana es la parte difícil porque los montones Java / Python no tienen `remove(element)` en O(log n).
Lo resolvemos con un mapa *lazy‐deletion* (`delayed`) que registra cuántos casos de un valor deben ser ignorados cuando aparece en una parte superior.

#### 2.1 Java Implementation

``java
importar java.util*;

clase pública SlidingWindowMedian {}
public double[] medianSlidingWindow(int[] nums, int k) {
// Max-heap para la mitad inferior
Prioridad Búsquedas realizadasInteger bajos = nueva PrioridadQueue escogida(Collections.reverseOrder());
// Jabón pequeño para la mitad superior
PriorityQueue se cumplióInteger confianza high = new PriorityQueue especificado();

// Mapa para recordar recuentos de borraciones retrasadas
Mapa seleccionadoInteger, Integer confianza retardado = nuevo HashMap fiel();

int lowSize = 0, highSize = 0; // tamaños lógicos (ignore delay)
doble[] ans = nuevo doble[nums.length - k + 1];
int ansIdx = 0;

// Ayudante: prune top de un montón si está programado para la eliminación
BiConsumer realizadasPrioridadQueue RealizarSeguido: Integer confianza prune = (heap, sign) - Propiedad {
mientras (!heap.isEmpty()) {}
int num = heap.peek();
Integer d = delay.get(num);
(d!= null " d " 0) {
// eliminar esta ocurrencia
retardado.put(num, d - 1);
si (delayed.get(num) == 0) retardado.remove(num);
heap.poll();
(sign == 1) bajo Talla... Talla...
} más romper;
}
};

para (int i = 0; i)
int num = nums[i];

// 1. Insertar nuevo elemento
si (low.isEmpty() {}
low.offer(num);
bajo Tamaño++;
. ♫ ... {
High.offer(num);
alto Tamaño++;
}

// 2. Saldo de saltos de modo que tenciónlowSize - highSize habit י= 1
si (lowSize > highSize + 1) {
high.offer(low.poll());
bajo Talla... Tamaño++;
} si (highSize > lowSize) {
baja.oferta (alto.poll());
alto Tamaño--; bajo Tamaño++;
}

// 3. Ventana de diapositivas si ya tenemos elementos k
si
int out = nums[i - k];
// Marca para la eliminación retardada
retardado.merge(out, 1, Integer::sum);
si (sin out= bajo.peek()) lowSize... Talla...

// Tops de Prune si es necesario
prune.accept(low, 1);
prune.accept (alto, -1);

// Rebalance after deletion
si (lowSize > highSize + 1) {
high.offer(low.poll());
bajo Talla... Tamaño++;
} si (highSize > lowSize) {
baja.oferta (alto.poll());
alto Tamaño--; bajo Tamaño++;
}
}

// 4. Grabación mediana una vez que tengamos una ventana completa
si
(k) == 1) { //
ans[ansIdx++] = low.peek();
♪ otra vez { // incluso
ans[ansIdx+] = (low.peek() + high.peek()) / 2.0;
}
}
}

devolver los ans;
}
}
`` `

**¿Por qué es esto “bueno”? * *

* **O(n log k)** tiempo – cada inserción, eliminación o equilibrio es O(log k).
* **O(k)** espacio extra – dos montones + mapa retardado.
* Manijas duplica correctamente gracias a la eliminación retardada.
* No es necesario un árbol de búsqueda binaria equilibrado (por ejemplo, `TreeSet`) – más fácil de entender para la mayoría de los entrevistadores.

### 2.2 Python Implementation

``python
importación heapq
de las colecciones importadas por defecto

Solución de clase:
def medianSlidingWindow(self, nums, k):
bajo, alto = [], [] # max-heap (como negativos), min-heap
retardado = defaultdict(int) # lazy deletion map
ans = []
lowSize = highSize = 0

def prune(heap, sign):
# sign = 1 for low, -1 for high
Mientras salta:
num = -heap[0] si el montón es bajo más montón[0]
si se retrasa[num]:
heapq.heappop(heap)
retardado[num] -= 1
si el signo == 1: bajo tamaño -= 1
más: HighSize -= 1
más:
descanso

para i, num in enumerate(nums):
# Introducir
si no baja o num <= -low[0]:
heapq.heappush(low, -num)
bajo Tamaño += 1
más:
heapq.heappush (alto, num)
HighSize += 1

# Balance
si lowSize > highSize + 1:
heapq.heappush (alto, -heapq.heappop(low))
lowSize -= 1
HighSize += 1
elif highSize > low Tamaño:
heapq.heappush(low, -heapq.heappop(high))
highSize -= 1
bajo Tamaño += 1

# diapositivas
si me iere= k:
fuera = nums[i - k]
retardado[out] += 1
si fuera hacia fuera= -low[0]:
lowSize -= 1
más:
highSize -= 1
prune(low, 1)
(alto, -1)
si lowSize > highSize + 1:
heapq.heappush (alto, -heapq.heappop(low))
lowSize -= 1
HighSize += 1
elif highSize > low Tamaño:
heapq.heappush(low, -heapq.heappop(high))
highSize -= 1
bajo Tamaño += 1

# Median
si me ignoro= k - 1:
si k % 2:
ans.append(-low[0])
más:
ans.append(-low[0] + high[0]) / 2.0

Retorno
`` `

### 2.3 C++ Aplicación

El "multiset" de C+ ya nos da un BST equilibrado con la iteración ordenada, por lo que podemos mantener un multiset *single* y mantener un iterador al medio. Este enfoque es conciso y perfectamente O(n log k).

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vectoriales Ventana(vectora) realizada empuje nums, int k) {
vectoriales res;
multisección indicativa ventana(nums.begin(), nums.begin() + k);
auto mid = next(window.begin(), k/2); // iterator to median

para (int i = k; i) = nums.size(); ++i) {
// añadir el nuevo elemento (cuando yo == k ya tenemos uno)
si (i == k) {
// nada que hacer – estamos en primera ventana llena
. ♫ ... {
ventana.erase(ventana.find(nums[i - k])); // elemento hojas
ventana.insert(nums[i]); // nuevo elemento

// pasar a mitad para mantenerlo apuntando a la mediana
si (nums[i]
(k % 2 == 0) ++mid; // nuevo elemento está en la izquierda
. ♫ ... {
(k % 2 == 1) --mid; // nuevo elemento en la derecha
}

si (nums[i - k]
(k % 2 == 0) --mid; // elemento eliminado estaba en la izquierda
. ♫ ... {
(k % 2 == 1) ++mid; // elemento eliminado estaba en la derecha
}
}

// compute median
(k % 2) { // odd
res.push_back(*mid);
♪ otra vez { // incluso
auto nextMid = siguiente(mid);
res.push_back(static_cast seleccionadodouble(*mid) + *nextMid) / 2.0);
}
}
restitución;
}
};
`` `

**¿Por qué es esto “bueno”? * *

* Usa el árbol equilibrado del STL; no hay balanceo de saltos tirados a mano.
* Mantiene el iterador a la mediana para que podamos consultar en O(1).
* Aún **O(n log k)** – cada erase/insert en el multiset es O(log k).

-...

## 3. El enfoque “Bad” (Simpler) – Clasificación de cada ventana

``python
def bad(nums, k):
res = []
para i en rango(len(nums) - k + 1):
ganar = ordenados (nums[i:i+k])
media = len(win)//2
si k % 2: res.append(win[mid])
más: res.append(win[mid-1]+win[mid])/2)
retorno
`` `

* **O(n k log k)** – demasiado lento para `k = 10^5`.
* Funciona sólo en entradas de juguete; los entrevistadores marcarán inmediatamente la ineficiencia.

Esta es la base *bad* que demuestra el “por qué no puedes simplemente volver a surtir”.

-...

## 4. Los Casos de esquina “Ugly”

Silencio ¿Qué puede pasar mal? Cómo evitarlo
Silencio...
Silencio **Números duplicados** Silencio Un ingenuo `TreeSet` colapsará duplicados en un elemento, perdiendo recuentos. TENIENDO `multiset` (C++), o `TreeMap Haga clic enInteger, Integer `` + iterator (Java), o mapas de eliminación retardada (aproximación de salto). Silencio
tención **Sliding window deletion** Silencioso Removing an arbitrary element from a heap is O(n). ← Lazy‐deletion, o utilizar un BST que soporta eliminar en O(log n). Silencio
Silencio **Incluso `k` precision** Silencio División entero en algunos idiomas truncates. tención Explicitamente lanzado a `doble` o `float` antes de la división. Silencio
Silencio **Iterator invalidation** Silencio In C++ `multiset::erase(it)` invalidates only `it`. Silencio Mantener el iterador y actualizarlo manualmente con `++` / `--`.
Silencio **Gran número negativo** Silencio En Java max‐heap con `PriorityQueue obtenidosInteger ` funciona bien; en Python usted necesita números negativos para un máximo-heap. TENIDO A LOS idiomas específicos del lenguaje. Silencio
Silencio **Overflow when averaging** Silencio `maxHeap.top() + minHeap.top()` podría rebosar 32-bit int. Silencio Convertir a `long' o `double` antes de summing. Silencio

-...

## 5. Resumen de la complejidad

TEN TERRITORIO TENIDO Tiempo ANTERIOR
Silencio--------------------------
Silencio 2-heap + lazy deletion ← **O(n log k)** Silencio **O(k)** Silencio
Silencio `multiset` + median iterator (C++) Silencio **O(n log k)** Silencio **O(k)** Silencio
Silencio Ordenando cada ventana (bad) Silencio **O(n k log k)** Silencio **O(k)**

Todas las soluciones son aceptables para la solución oficial LeetCode, pero el enfoque de dos pasos es *el* más fácil de entrevista.

-...

## 6. Escribir el artículo del blog – SEO‐Ready, Job‐Ready

■ *Título*
■ *“Sliding‐Window Median – El problema duro favorito del entrevistador (Java, Python, C++)*

### 6.1 Meta Descripción (Equipo 155 caracteres)

■ Master the *Sliding Window Median* LeetCode hard problem. Lea nuestra guía detallada con Java, Python y código C++, trucos de rendimiento y consejos de entrevista.

### 6.2 Esquema

1. **Problema Declaración " Importancia**
* Recap rápido + por qué importa en la analítica del mundo real.
2. **Naïve vs. Optimal**
* Mostrar el truco O(n k log k) de la ventana, luego explicar por qué falla.
3. *Estrategia de dos caballos*
* Explicar las instrucciones de datos, los invariantes y cómo mantener la mediana.
* Mostrar pseudo-código y resaltar la perezosa eliminación.
4. **Multiset + Iterator** (C++ < Java alternative)
* Cuando un BST equilibrado es más simple.
5. **Edge‐Case Checklist* *
* Valores duplicados, números negativos, incluso / tamaño de la ventana.
6. **Performance & Memory**
* Big‐O, cache amabilidad, por qué la perezosa eliminación es todavía rápida.
7. ** Consejos de opinión**
* Cómo hablar del algoritmo en entrevistas de 5 minutos.
* Lo que los entrevistadores suelen buscar: * árboles balanceados, trucos de montón, tiempo de O(n log k), claridad*.
8. **Takeaway & Further Reading**
* Enlace a temas avanzados: *Order Statistic Trees, Fenwick/BIT con dos punteros, RMQ*.

### 6.3 El artículo completo del Blog

-...

### Sliding‐Window Median: Masterclass for Interviews

■ **TL;DR** – Mantenga dos montones (máximo salto para la mitad inferior, min-heap para la mitad superior). Utilice la eliminación perezosa para eliminar elementos de venta libre en *O(log k)*. Complejidad: **O(n log k)** tiempo, **O(k)** espacio.

-...

Problema profundo Dive

En el mundo real a menudo necesitarás computar una estadística sobre una ventana deslizante – pensar *rolling average*, *moving median*, o *online outlier detection*. La mediana es el *centro* de los datos y es robusta a los valores extremos, por eso se utiliza en finanzas, fusión de sensores y detección de anomalías.

Habida cuenta de las limitaciones (`n = 10^5`), cualquier solución que vuelva a surtir cada ventana (`O(n k log k)`) se agotará. Necesitas una estructura de datos que soporta **inserción, eliminación y recuperación del elemento k/2-th** todo en tiempo logarítmico.

-...

##### 2down⃣ ¿Por qué los saltos ganan

* A **max‐heap** le permite conocer siempre el elemento más grande de la mitad * más baja*.
* Un **min-heap** te da el elemento más pequeño de la mitad *upper*.
* La mediana es ya sea la parte superior del max-heap (ventanaodd) o el promedio de las dos tapas (incluso la ventana).

Cuando la ventana se desliza, se elimina un elemento que puede estar en cualquier lugar en los montones. Eliminar un elemento arbitrario directamente de un montón es caro, pero podemos **delay** la eliminación:

`` `
perezoso[num]+ // marca que una instancia de 'num' debe ser ignorada
`` `

Cuando un elemento sale en la parte superior de un montón, comprobaremos si está marcado para la eliminación; si es así, lo hacemos y decrementamos el mostrador perezoso. Esto mantiene cada pila superior limpia y mantiene operaciones O(log k).

-...

##### 3down⃣ Code Walk-through

■ #Java #

``java
public double[] medianSlidingWindow(int[] nums, int k) {
// dos montones + mapa de eliminación retardada
Prioridad Búsquedas realizadasInteger bajos = nueva PrioridadQueue habilitado(Collections.reverseOrder()); // max‐heap
PrioridadSea realizadaInteger confianza alta = nueva PrioridadQueue relacionarse(); // min‐heap
Mapa seleccionadoInteger, Integer confianza retardado = nuevo HashMap fiel();
int lowSize = 0, highSize = 0;

doble[] ans = nuevo doble[nums.length - k + 1];
int idx = 0;

// ... funciones de ayuda prune(), balance(), diapositiva() ...
}
`` `

■ Python

``python
Solución de clase:
def medianSlidingWindow(self, nums: List[int], k: int) - título List[float]:
# dos montones + Contrato para la eliminación perezosa
bajo, alto = [], [] # max‐heap (negatives)
retardado = defaultdict(int)
El resto del código...
`` `

■ **C++**

``cpp
Clase Solución {
public:
vectoriales Ventana(vectora) realizada empuje nums, int k) {
multiset significante ventana(nums.begin(), nums.begin()+k);
auto mid = next(window.begin(), k/2);
// ... diapositiva, prune, balance ...
}
};
`` `

Los tres francotiradores comparten las mismas complejidades **invariantes** y **tiempo/espacio**.

-...

#### ## 4down⃣ Complexity Analysis

Silencioso Operación Java/Python (Heap) Silencio C++ (multiset)
Silencio...
Silencioso Silencioso `O(log k)` Silencio `O(log k)` Silencio
Silencioso para la eliminación Silencio
TENIDA Median TENIDA `O(1)` ANTE `O(1)` Silencio
Silencio **Total** Silencio**
Silencioso de la memoria **O(k)**

La eliminación perezosa** asegura que nunca pagues más que `O(log k)` para eliminar un elemento, aunque el elemento real podría ser profundo dentro de un montón.

-...

#### 5down⃣ Handling Edge Cases

Silencio tóxico tómese el error común
Silencio...
← Valores Duplicados Silenciosos `TreeSet` los desploma bajo `multiset` (C++), `TreeMap` + conteos (Java)
Silencio Incluso tamaño de la ventana ¦ Integer division truncates fort Convertir a `doble` antes de dividir Silencio
Silencio Números negativos Silencio Max‐heap necesita negativos en Python fort Uso `-valor ' para el montón de vida
Silencio El desbordamiento de la suma Silencioso `max + min` puede rebosar 32‐bit  durable Convertir to `long long` or `double` first ←

-...

##### 5down⃣ Presentación

* **Empieza con un diagrama** – dibuja dos montones y muestra cómo se sienta la mediana en el medio.
* **Declarar los invariantes**:
* `low.size() == high.size()` or `low.size() == high.size() + 1` (dependiendo de la paridad de `k ').
* Todos los elementos en `bajo' ≤ todos los elementos en 'alto'.
* **Explicar la perezosa eliminación** en una frase: “Mantendremos un contador de elementos que necesitan ser eliminados, y limpiarlos cuando lleguen a la parte superior. ”
* **Mostrar pseudo código**: O(n log k) es el titular.
* **Agregar “por qué es robusto”**: la mediana se ve menos afectada por los superávidos que la mediana, un buen punto de discusión para las funciones financieras y analíticas.

Los entrevistadores aprecian el código que es *clear* y *testable*, así que incluyen pruebas unitarias para ventanas extrañas/incluso, duplicados y números negativos.

-...

##### 6down⃣ Take‐away

1. **Two‐heap + lazy deletion** es el oro estándar para la mediana de la ventana deslizante.
2. Para los usuarios de C++, un 'multiset' con un iterador de mediana puede ser incluso más simple.
3. Verificar siempre los casos de borde: duplicados, números negativos e incluso «k».
4. En una entrevista, articular el *por qué* detrás de cada operación, no sólo el *cómo*.
5. Práctica de codificación en los tres idiomas – cada empresa puede probar en su pila preferida.

-...

Otros recursos

* **Order Statistic Tree** – mantener el elemento k/2-th en O(log n).
* **Binary Indexed Tree (Fenwick)** con dos punteros: una solución sin conexión limpia para los arrays estáticos.
* ** Árboles de segmento con propagación perezosa** – para actualizaciones de rango y consultas.

-...

##### 8down⃣ Wrap-up

Sliding-window median es más que un ejercicio de codificación; es una herramienta *real‐world data‐análisis*. Dominarlo demuestra su capacidad para:

* Elija la estructura correcta de datos (heaps, BST).
* Optimize for time/space under large inputs.
* Piense en las eliminaciones y los datos de establo.

Con las implementaciones Java, Python y C++, estás listo para clavar el problema duro de LeetCode * y* as de la entrevista.

-...

¡Done!

Este artículo no sólo muestra el código, sino que da a los entrevistadores * pista de hablar* les encantará. Al enfocarse en el rendimiento, la claridad y la robustez del borde, usted está listo para brillar en cualquier entrevista de codificación.

-...

## 7. Palabra final

Ahora tienes:

* Tres soluciones *production-ready* en los tres idiomas principales.
* Una explicación clara de por qué el enfoque de dos pasos es óptimo.
* Una hoja concisa de trampas.
* Un poste de blog listo para publicar, SEO optimizado para aumentar su visibilidad como ingeniero de software.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀

-..