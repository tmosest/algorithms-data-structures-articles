-...
Título: LeetCode 295. Encontrar Median de Data Stream -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 295. Encontrar Median de Data Stream
## Full‐stack Solution (Java fort Python tención C++) + SEO‐Optimised Blog Post

-...

#### TL;DR
*Problema*: Construya una clase `MedianFinder' que apoye:
- `void addNum(int num)` – insertar un número de un flujo de datos
- `Doble hallazgoMedian()` - devolver la mediana actual
- ** Complejidad** - `addNum` : **O(log n)**, `findMedian`: **O(1)**
- **Aprobación** – Dos montones (un max-heap para la mitad inferior, un min-heap para la mitad superior)
¿Por qué importa? Este es un problema de entrevista clásica que te muestra conocer *las colas de prioridad*, *los árboles balanceados* y *análisis enamorado*.

-...

## 1. Código - Una aplicación por idioma

■ La misma lógica se aplica en los tres idiomas:
■ *Mantengan dos montones: `bajo ` (máximo) y `alto' (min-heap). *
■ *Mantenga la diferencia de tamaño ≤ 1 y `low.peek() ≤ high.peek()`.
■ Mediano es el elemento superior único (tamaño dd) o el promedio de ambos superior (igual tamaño). *

### 1.1 Java (LeetCode-style)

``java
importa java.util. Prioridad Queue;
importa java.util. Comparador;

clase pública MedianFinder {}
// Max-heap para la mitad inferior
final privado Búsquedas realizadasInteger bajos = nueva PrioridadQueue correspondió(Comparator.reverseOrder());
// Min-heap para la mitad superior
Prioridad final privadaQueue (3)Integer título alto = nueva PrioridadQueue relacionarse();

public MedianFinder() {}

public void addNum(int num) {
// 1 Cambios en el montón apropiado
si (low.isEmpty() {}
low.offer(num);
. ♫ ... {
High.offer(num);
}

// 2 comentarios⃣ Re-balance so that tenciónsize(low) – size(high) duración ≤ 1
si (low.size() + 1) {
high.offer(low.poll());
} si (alto.size() 1) {
baja.oferta (alto.poll());
}
}

public double findMedian() {}
// 3VIEW⃣ Compute median in O(1)
int total = low.size() + high.size();
(total % 2 == 1) {
// Número extraño de elementos – mayor montón sostiene la mediana
retorno low.size() ⇩ high.size() ? low.peek() : high.peek();
. ♫ ... {
// Incluso – promedio de ambos tops
(low.peek() + high.peek()) / 2.0;
}
}
}
`` `

### 1.2 Python

``python
importación heapq

Clase MedianFinder:
def __init__(self):
# max‐heap (invert sign) and min‐heap
auto.low = [] # Max‐heap for lower half
self.high = [] # min‐heap for upper half

def addNum(self, num: int) - Ninguno.
# 1 Empuje en el salto correcto
si no yo. bajo o num <= -self.low[0]:
heapq.heappush(self.low, -num) # invert sign → max‐heap
más:
heapq.heappush(self.high, num)

# 2⃣ Re-balance
si len(self.low)
heapq.heappush(self.high, -heapq.heappop(self.low))
elif len(self.high)
heapq.heappush(self.low, -heapq.heappop(self.high))

def findMedian(self) - Propiedad flotante:
O(1) median
si len(self.low) == len(self.high):
(-self.low[0] + self.high[0]) / 2.0
retorno flotante(-self.low[0]) si len(self.low) ю len(self.high) otro flotador(self.high[0])
`` `

#### 1.3 C++

``cpp
#include >
Incluido el título

class MedianFinder {}
privado:
// max‐heap (media baja)
std::priority_queue Utilizaint bajos;
// min‐heap (upper half)
std:::priority_queue obtenidosint, std::vector fielint, std:::greater interpretadoint

public:
MedianFinder() = default;

vacío addNum(int num) {}
// 1 / ⃣ Insertar en el montón adecuado
si (bajo.entonces() TENIDO EN SUPERVISIÓN num 0 = bajo.top()) bajo.push(num);
más alto.push(num);

// 2 pesquisas Reequilibrio para mantener la vidalow.size() - high.size()
si (low.size() + 1) {
alto.push(low.top()); low.pop();
} si (alto.size() 1) {
bajo.push (alto.top()); alto.pop();
}
}

doble encuentroMedian() {
O(1) median computation
si (low.size() == high.size())
(low.top() + high.top()) / 2.0;
retorno low.size() √≥ high.size() ? low.top() : high.top();
}
};
`` `

Los tres snippets están listos para pasar por una presentación **LeetCode 295** o para una entrevista técnica.
Siéntete libre de añadir pruebas de unidad o integrarlas en tu propio andamio coding-platform.

-...

## 2. Por qué este blog es Job‐Interview‐ Listo

El objetivo no es sólo resolver LeetCode 295; es demostrar *design* y *optimization* habilidades que los gerentes de contratación anhelan.
A continuación se rompe la solución en tres secciones – *El Bien* **The Bad**, **The Ugly** – para que pueda articular los intercambios cuando explique el código en una entrevista.

-...

## 2.1 The Good – Why Esta Solución Rocks

TENIDO VALORAR LA FACCIÓN ANTERIOR Por qué Es Grande
Silencio...
Silencio **O(log n) inserción** Silencio Usa un montón binario → *logarítmico* costo, incluso para 5 × 104 operaciones. Silencio
Silencio **O(1) median query** Silencio Simplemente mire en las cimas de los dos montones – sin traversal, sin copia. Silencio
tención **Espacio-optimal** Silencio Almacena cada elemento una vez: **O(n)** total. Silencio
Silencioso **Simplicity & Clarity** Silencio Dos saltos + rebalancing logic es fácil de código, prueba y explicar. Silencio
tención **Scalable** Silencioso Trabaja para *cualquier * rango entero – no suposiciones sobre la distribución de datos. Silencio
Silencio **Interview‐ready** ¦ Shows mastery of **priority queues** and **amortised analysis** – a must‐know for senior data‐structure roles. Silencio

-...

## 2.2 The Bad – Common Pitfalls & Edge Cases

Н нели вали Pitfall ны fijar / Insight
Silencio----------------------------
Silencio **Escoge el tipo equivocado de montón** Silencio En Java: use `Comparator.reverseOrder()` para el máximo salto; en Python: invert sign; en C++: `std::greater interpretadoint titulada` para el min‐heap. Silencio
Silencio **Off‐por-uno en la diferencia de tamaño** Silencio Siempre comprobar ` duraciónlow.size() – high.size() sometida ≤ 1`. Olvidar esto rompe la lógica mediana para los conteos uniformes. Silencio
Silencio **Failing to balance after insertion** Silencio Incluso si usted empuja hacia el montón equivocado, debe volver a equilibrar. Un único `heap.pop()` / `push()` mueve el elemento ofensivo. Silencio
Silencio **Desbordamiento entero sobre el cálculo mediano** Silencio En Java, elenco a `long` antes de añadir: `(long)low.peek() + high.peek()) / 2.0`.
Silencio **Usar un solo montón (cerrar, hacer encuestas)** Silencio Cerrar un montón para cada `findMedian()` conduce a **O(n)** tiempo – *nunca* hacer esto en una entrevista. Silencio

-...

## 2.3 The Ugly - When Things Go Wrong

TENIDO 👹 Escenario Ugly ANTERIOR POR QUÉ Ocurre
Silencio...
Silencio **Heaps Unbalanced on Insert** Silencio Si empujas ingenuamente cada número en un montón, el otro se queda vacío → medianamente equivocado. Silencio
Silencio **Neglecting Order Constraint** Silencio `low.peek()` debe ser ≤ `high.peek()`; de lo contrario el medio será de la mitad equivocada. Silencio
Silencio **Wrong Median Calculation on Even Size** Silencio Devolviendo `low.peek()` o `high.peek()` solo para un número uniforme de elementos es incorrecto. Silencio
TEN **Using Recursion or Merge Sort** TENED Algunas soluciones (por ejemplo, merge‐sort después de cada inserción) son *(n log n)* o *O(n)* para la consulta mediana – inaceptable para grandes corrientes. Silencio
Silencio **Assuming Sorted Input** Silencio Si el flujo de datos ya está clasificado, un único array puede dar mediana en O(1), pero usted *debe* manejar el caso general. Silencio

-...

## 3. Bono: Pequeña optimización para pequeños rangos enteros

Si usted sabe que los valores de la corriente están garantizados para mentir en `[0, 100]`, usted puede dejar las colas de prioridad completamente:

Silencio Idioma Silencio Concepto
Silencio--------------------------
TEN Java TENIDO `int[] freq = nuevo int[101];` Silencio `addNum ' : **O(1)**, `findMedian`: **O(100)** (continuado)
Silencio Python Silencioso `colecciones. Counter` + suma de prefijo confidencialidad Igual que Java tención
TENIDO C++ TENIDO `estd::array madeint,101 ` TENIDO M igual que Java TENIDO

Esta variante es *nice para la micro-optimización*, pero la mayoría de los entrevistadores todavía esperan la solución de dos pasos. Mencione sólo si la entrevista pide explícitamente una solución restringida.

-...

## 4. SEO‐Optimised Blog Post: “El Bien, el Mal y el Ugly de LeetCode 295 – MedianFinder”

■ **Etiquetas clave:** *LeetCode 295*, *MedianFinder*, *find median from data stream*, *two heaps*, *Entrevista de Java*, *Entrevista de Python*, *Entrevista de C++*, *O(log n) prioridad queue*, *entrevista de estructuras de datos*, *preguntas técnicas de entrevista*.

-...

##### 📌 Title
**Master LeetCode 295: MedianFinder – Un profundo buceo en la solución de dos saltos (Java / Python / C++)**

-...

### 📝 Meta Descripción
Aprende cómo implementar 'MedianFinder' para LeetCode 295 – Encuentra Mediano desde Data Stream – en Java, Python y C++.
Explore lo bueno, lo malo, y lo feo de los enfoques comunes, y consiga entrevistas listos con O(log n) inserción y O(1) consulta.

-...

#### 🔥 Body

##### 1. Introducción
El problema ** "Find Median from Data Stream"** (LeetCode 295) es un elemento básico para entrevistas de estructura de datos.
Te obliga a diseñar una estructura de datos *dinámica* que mantiene un seguimiento del elemento medio de un conjunto siempre creciente.
En este artículo, caminaremos a través del algoritmo óptimo **2-heap**, ilustraremos cómo codificarlo en **Java, Python, y C+**, y resaltaremos los intercambios que puedes discutir durante las entrevistas.

##### 2. Why MedianFinder Matters
- **Real-world relevance:** Streaming analytics, motores de recomendación en línea, y dashboards de precios de stock todos necesitan calcular mediana en la mosca.
- **Dirección de interés:** Demuestra el control sobre las colas de prioridad**, el equilibrio de salto**, y ** el análisis amortizado**.

##### 3. El Bien – Un Provenido O(log n) Estrategia
- **Heaps binarios** proporcionan una inserción *logarítmica*, esencial para flujos de 105+ números.
- **Rebalancing** mantiene cerca los tamaños de las pilas, asegurando que la lógica mediana se mantenga a la vez extraña e incluso cuenta.
- **O(1) median query** - sólo mire en las cimas del montón.

##### 4. El mal – errores comunes para evitar
- Usar un solo montón o una clasificación ingenua conduce a los tiempos de consulta.
- Olvídate de mantener la restricción de orden (`low.peek() ≤ high.peek()`).
- Integer desborda en Java al añadir dos tapas de salto.

##### 5. The Ugly – What Interviewers No quiero
- Cierre o votación de montones dentro de `findMedian()`.
- Saltos desequilibrados que rompen la mediana por longitudes extrañas o uniformes.
- Re-implementing merge-sort en cada inserción – un desastre *O(n log n)*.

##### 6. Detalles de la aplicación
- Java: `PrioridadQueue se realizóInteger `` con `Comparator.reverseOrder()` para el max‐heap.
- Python: `heapq` con inversión de signos para simular un max-heap.
- C++: `std::priority_queue` para max‐heap y un min‐heap con `std::greater interpretadoint titulado ``.

Cada snippet está acompañado por comentarios claros para que pueda copiar-paste en LeetCode o su IDE.

##### 7. Bono: Cuando la entrada está restringida a 0–100
Si el problema garantiza pequeños rangos de enteros, un array de frecuencia da *O(1) insert* y *O(1)* median en la práctica.
Pero los entrevistadores generalmente esperarán la solución general de dos pasos – mencionar la optimización sólo si se le pregunta.

##### 8. Takeaway - ¿Por qué usted debe navegar esta pregunta
- **Design skill:** Mostrar que puede construir una estructura de datos *dinámica*.
- ** Profundidad algorítmica**: insertar " O " , " O(1) " consulta – un referente de eficiencia clásico.
- * Confianza en la codificación* Código listo para funcionar en Java, Python y C++ – perfecto para pruebas de codificación remotas.

-...

### ⋅ Call‐to‐Action
■ *“¿Quieres romper más problemas de LeetCode? Suscríbete para inmersiones más profundas en soluciones de estructura de datos de estilo entrevista.”*

-...

#### 🚀 Endnote

Mastering LeetCode 295 te equipa con un poderoso modelo mental: *dos montones + rebalancing*.
Usted puede discutir los **trade-offs** (bueno/bad/ugly) en cualquier entrevista de estructura de datos, impresionar a los gerentes de contratación con su pensamiento de diseño, y alejarse con una solución **robust, lista para producción** en tres idiomas principales.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀

-...

## 5. Pensamientos de clausura

Ya sea que estés preparando una **Google**, **Amazon**, o **Microsoft** entrevista, este blog y los fragmentos de código te dan:

1. Una solución *ready‐to-run* en el idioma de su elección.
2. Un marco claro para explicar *por qué* el algoritmo funciona (bien).
3. Una lista de errores comunes para evitar (Bad).
4. Una mirada rápida en las trampas de la periferia (Ugly).

Utilice la narrativa “Good‐Bad‐Ugly” para guiar su historia de entrevista, y dejará a los reclutadores convencidos de que usted es un verdadero ingeniero **data‐structure**.

¡Feliz entrevista!

-..