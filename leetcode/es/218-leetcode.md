-...
Título: LeetCode 218. El problema Skyline -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📐 The Skyline Problem – Java, Python & C++ Soluciones + Blog de profundidad

A continuación encontrará tres implementaciones de trabajo completo (Java, Python, C++) para LeetCode 218 – *The Skyline Problem*.
Después del código encontrarás un poste de blog amigable de SEO que explica el algoritmo, los trade-offs, y por qué dominar este problema puede aterrizar un trabajo técnico.

-...

#### ## 1down⃣ Java 17 Solución

``java
importar java.util*;

Solución de la clase pública {}
public List made(int[][] buildings) {}
// 1. Construir una lista de todos los eventos (izquierda & derecha bordes)
Lista obtenida[] eventos relativos = nuevo ArrayList correctamente();
para (int i = 0; i) edificios.length; i++) {
int[] b = buildings[i];
sucesos.add(new int[]{b[0], -b[2]}); // left edge: negative height
sucesos.add(new int[]{b[1], b[2]}); // right edge: positive height
}
// 2. Ordenar por x, luego altura (negativa antes positiva para los lazos)
events.sort(a, b) - Propiedad {
(a[0]!= b[0]) devolver Integer.compare(a[0], b[0]);
integer.compare(a[1], b[1]);
});

Lista realizadaLista realizadaInteger confianza result = nuevo ArrayList recomendado();
// Max‐heap para mantener las alturas activas actuales
Prioridad Queue won(Collections.reverseOrder());
maxHeap.offer(0); // nivel de tierra
int prevMax = 0;

para (int[] e : eventos) {
int x = e[0], h = e[1];
si (h 0) { // borde izquierdo
maxHeap.offer(-h);
} más { // borde derecho
// Eliminación perezosa – el montón puede contener alturas que ya han terminado
(!maxHeap.isEmpty() " maxHeap.peek() == h) {
maxHeap.poll();
ruptura;
}
}

int curMax = maxHeap.peek();
si (curMax != prevMax) {
result.add (Arrays.asList(x, curMax));
prevMax = curMax;
}
}
Resultado de retorno;
}
}
`` `

-...

## ## 2down⃣ Python 3 Solution

``python
de la importación Lista
importación heapq

Solución de clase:
def getSkyline(self, buildings: List[List[int]) - No. List[List[int]]:
# sucesos: (x, altura) donde la altura 0 hacia el borde izquierdo
sucesos = []
para l, r, h en edificios:
events.append(l, -h)) # start
events.append(r, h)) # end

# ordenar por x; para el mismo x, comienza antes de los extremos (negativo antes positivo)
events.sort(key=lambda x: (x[0], x[1]))

Resultado = []
# max‐heap of active heights (store as negative for min‐heap)
Max_heap = [0]
prev = 0

para x, h en eventos:
si h 0: # inicio de un edificio
heapq.heappush(max_heap, h)
# Fin de un edificio
# Quita la altura del edificio del montón
# Python heap no soporta la eliminación, así que perezoso pop
mientras max_heap y max_heap [0] == -h:
heapq.heappop(max_heap)
descanso

cur = -max_heap[0] # actual altura máxima
si se cura!= Prev:
result.append([x, cur])
prev = curro
Resultado de retorno
`` `

-...

### 3down⃣ C++ (GNU C+17) Solución

``cpp
Incluido el título
#include >
#include >
#include ■utility
usando std namespace;

Clase Solución {
public:
vectores seleccionados: {}
// 1. Crear eventos: (x, altura) – altura negativa para el borde izquierdo
vectores realizadospair hechosint,int títulos.
para (auto &b : edificios) {}
sucesos.emplace_back(b[0], -b[2]); // left
sucesos.emplace_back(b[1], b[2]); // right
}
sort(events.begin(), events.end(), [](auto &a, auto &b){
si (a.first != b.first) devuelve a.first
de vuelta a.second
});

vector de vectores resultado;
priority_queue obtenidosint confianza maxHeap; // max‐heap of active heights
maxHeap.push(0); // nivel de tierra
int prev = 0;

para (auto &e : eventos) {}
int x = e.first, h = e.second;
si (h 0) { // inicio de la construcción
maxHeap.push(-h);
} otro { // final de la construcción
// Eliminación perezosa: pop sólo cuando la parte superior coincide con la altura final
mientras (!maxHeap.empty() " maxHeap.top() == h) {
maxHeap.pop();
ruptura;
}
}
int cur = maxHeap.top();
si (cur != prev) {
result.push_back({x, cur});
prev = cur;
}
}
Resultado de retorno;
}
};
`` `

-...

## 📢 Blog Artículo: “El problema de la línea de cielo – bueno, malo”

■ *Título*
■ **The Skyline Problem: Good, Bad, " Ugly – A Complete Guide for Job Interviews**
■
■ **Meta Descripción:**
■ Master LeetCode 218 – El problema Skyline. Aprenda el algoritmo de barrido, compare soluciones ingenuas, prioritarias-queue & segment‐tree y entienda por qué este problema es un conocimiento imprescindible para cualquier entrevista de ingeniería de software.
■
■ **Keywords:** problema de skyline, LeetCode 218, algoritmo de línea de barrido, cola prioritaria, algoritmo de entrevista, entrevista de trabajo, estructuras de datos, C++, Java, Python, entrevista de codificación, algoritmo de diseño

-...

#### ## 1down⃣ ¿Cuál es el problema de Skyline?

En la planificación urbana, el *skyline* es el esbozo que ves al mirar una ciudad desde lejos.
Formalmente:

- ** Entrada:** 'construcción[i] = [left_i, right_i, height_i]` - cada edificio es un rectángulo en una base plana.
- **Output:** Una lista de *puntos clave*[x1, y1], [x2, y2], que traza el contorno exterior.
El último punto siempre tiene `y = 0`.

El reto es producir este contorno de manera eficiente para hasta 104 edificios, cada uno con coordenadas hasta 231-1.

-...

#### 2down⃣ Los tres enfoques “Flavor”

¦ Flavor Silencio Complejidad Silencio Código Complejidad
Silencio----------------------------...
Silencio **Good – Sweep Line + Max‐Heap** TEN **O(n log n)** TENIDO 1‐2 páginas TENIDO *Respuesta de entrevista a grado de producción*. Silencio
Silencio **Bad – Brute Force** Silencio **O(n2)** Silencio 1 página Silencio Trabaja para pequeños insumos pero no en limitaciones. Silencio
Silencio **Ugly – Segment Tree** Silencio **O(n log N)** (N = tamaño de compresión de coordenadas) TEN 4+ páginas ANTERI Muestra conocimiento profundo de la estructura de datos pero sobrematar. Silencio

-...

##### 2.1 The *Good* Solution: Sweep Line + Max‐Heap

1. *Eventos*
Para cada edificio creamos dos eventos:
- `(izquierda, -altura)' - inicio de la construcción (altura negativa para diferenciar).
- '(derecha, +derecha)' - final de construcción.

2. **Acontecimientos inteligentes**
Ordenar por `x`. Cuando los " vínculos " , comienzan (negativos) llegan antes de fines (positivos).

3. - ¿Qué?
Mantenga un máximo de alturas de edificio *activo*.
*Push* cuando un edificio comienza, *lazy‐pop* cuando un edificio termina.

4. **Skyline Update**
Después de cada evento, la parte superior del montón es la altura máxima actual.
Si difiere de la altura anterior, emita un nuevo punto clave.

*Por qué funciona esto: *
El montón siempre contiene las alturas de los edificios que cubren la posición de barrido actual. El más grande es exactamente la altura del skyline visible.

**Hora**: `O(n log n)` para clasificar + operaciones de salto.
**Espacio**: `O(n)` para eventos + montón.

-...

#### 2.2 The *Bad* Approach: Brute Force

``text
Por cada x de min(izquierda) a max(derecha):
Cura = 0
para cada edificio:
si la izquierda se indica= x  se indica a la derecha: cur = max(cur, height)
si se curan los cambios - punto de registro
`` `

- **Complejidad**: `O(n * ancho)` → impráctico para coordenadas anchas (hasta 231).
- **Cuando falla**: la anchura puede ser miles de millones → memoria/tiempo soplado.
- **Por qué los reclutadores lo odian**: Muestra la falta de conciencia de la estructura de datos.

-...

##### 2.3 The *Ugly* Approach: Segment Tree (Coordinate Compression)

1. Compresa todas las coordenadas únicas " izquierda " derecha " .
2. Construye un árbol de segmento sobre índices comprimidos.
3. Edificios de procesos ordenados por altura, rangos de actualización.
4. Traverse el árbol para extraer puntos clave.

- **Pros**: Demostrar conocimiento avanzado del DS.
- **Cons**: Aplicación excesiva, larga y difícil de depurar.
Cuando los reclutadores lo valoran... En papeles fuertemente centrados en geometría o programación competitiva.

-...

#### 3down⃣ Por qué dominar este problema te ayuda a aterrizar un trabajo

Cómo el problema de las líneas aéreas lo demuestra
Silencio.
Silencio ** Pensamiento Algorítmico** Silencio Elegir la línea de barrido + saltar sobre la fuerza bruta muestra que puede razonar sobre la complejidad óptima. Silencio
TEN **Data Structures** TENER Mastery of priority queues, multisets, or segment trees. Silencio
Silencio **Edge‐Case Handling** Silencio Fusionando intervalos superpuestos, manejando eventos simultáneos. Silencio
Silencio **Code Readability** ← Escribir soluciones limpias y bien adaptadas que se pueden explicar en una entrevista. Silencio
Silencio **Conciencia de desempeño** Silencio Comprensión de tiempo / cambio de espacio y por qué algunas soluciones son aceptables sólo para pequeños insumos. Silencio

Los entrevistadores aman los problemas que requieren un ** camino de solución clara** y una implementación **clara**. El Problema de Skyline marca ambas cajas.

-...

#### 4down⃣ Código de muestra Snippets (para referencia rápida)

Silencio Idioma Silencio Líneas Clave Silencio
Silencio...
Silencio **Java** Silencioso `events.sort(...)`; " PrioridadSeguido " Integer confianza maxHeap = nueva PrioridadPregunta relativa(Collections.reverseOrder()); " Silencio
Silencioso **Python** Silencioso `events.sort(key=lambda x: (x[0], x[1])) ' `heapq.heappush(max_heap, h)`
Silencio **C++** Silencioso `sort(events.begin(), events.end(), ...)`; `priority_queue didint

-...

#### 5down⃣ Lista final de verificación Antes de la entrevista

- [ ] Entender completamente el formato de entrada/salida.
- [ ] Explicar el concepto de *sweep line* antes de codificación.
- [ ] Use un **max‐heap** (o multiset) para realizar un seguimiento de alturas activas.
- [ ] Emitir un punto clave sólo cuando la altura cambia**.
- [ ] Discuta el manejo de eventos simultáneos (por ejemplo, varios edificios que comienzan en el mismo `x`).
La mención coordina la compresión si se pide soluciones alternativas.

-...

#### 5down⃣ Call‐to‐Action

■ ¿Quieres ace LeetCode 218? #
■ Copia las soluciones proporcionadas en su editor, corre a través de los casos de prueba, y la práctica explicando cada paso en voz alta.
■ Luego, deja caer el enlace del blog en tu lista de preguntas y muestra a los reclutadores que *conocen tus algoritmos*.

-...

■ ** Nota del autor:**
■ Las tres soluciones de código anteriores implementan la estrategia de barrido *Good*, que difiere sólo en sintaxis. Pruébalos localmente, comentarios tweak, y estarás listo para cualquier entrevista donde aparezca el Problema Skyline.

-...

Feliz codificación, y que su *skyline* sea tan clara y eficiente como las soluciones anteriores! 🚀

-...

*End of article. *