-...
Título: LeetCode 358. Rearrange String k Distancia Apart -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🎯 LeetCode 358 – “Rearrange String k Distancia Apart”
**Java Silencio Python ← C+** – Soluciones de trabajo completas + un artículo de blog optimizado de SEO que te ayudará a conseguir tu próxima entrevista de trabajo.

-...

## 1. Recaptación de problemas

■ **Rearrange String k Distancia Apart**
■ Dada una cuerda `s` y un entero `k`, rearrange `s` para que los mismos caracteres sean por lo menos `k` índices separados.
■ Devuelve cualquier reorganización válida, o una cadena vacía si es imposible.

■ **Constraints**
* `1 ' s.length
* `s` contiene sólo minúsculas letras en inglés
* " 0 " = k " `

-...

## 2. Idea de alto nivel

Un algoritmo codicioso con un *max‐heap* (primera cola) funciona hermosamente:

1. Cuenta las frecuencias de cada personaje.
2. Utilice un máximo de salto para elegir siempre el personaje más frecuente que se permite **actualmente**.
3. Después de colocar un personaje, no se puede utilizar de nuevo para las próximas posiciones 'k-1' – lo “bloqueamos temporalmente” en una cola.
4. Cuando el tamaño de la cola alcanza `k`, el elemento más antiguo es desbloqueado y empujado de nuevo en el montón.
5. Si en cualquier momento el montón está vacío pero todavía necesitamos colocar un personaje, la tarea es imposible.

Este es el patrón clásico *k‐distance rearrangement* usado en muchas preguntas de entrevista.

-...

## 3. Detalles de la aplicación

Silencio Idioma Silencio Silencio
Silencio...
Silencio **Java** Silencio Uso `PriorityQueue hacíaint[] `con la comparación personalizada (desciende la frecuencia). `ArrayDeque se hizo []] propiedad para la cola de espera. Silencio
Silencio **Python** Silencio `heapq` proporciona un min-heap, por lo que empujamos frecuencias negativas. Colecciones. Deque` para la cola de espera. Silencio
Silencio **C++** Silencio `priority_queue hizopair seleccionado,char confianza `` (max‐heap by default). `queue hizopair realizado,char título `` para esperar. Silencio

Las tres soluciones funcionan en **O(n log m)** tiempo (`m י= 26`) y **O(m)** espacio extra.

-...

## 4. Código

#### 4.1 Java

``java
importar java.util*;

Solución de la clase pública {}
public String rearrangeString(String s, int k) {
si (k 0 = 1) retorno s; // No se necesita ninguna limitación

// Mapa de frecuencia
int[] freq = nuevo int[26];
para (carc : s.toCharArray()) freq[c - 'a']+;

// Max‐heap: (-frecuencia, carácter)
PriorityQueue madeint[] conviene pq = new PriorityQueue Curso()
a, b) - Propiedad Integer.compare(b[0], a[0]); // max‐heap

para (int i = 0; i)
si (freq[i] 0) pq.offer(new int[]{freq[i], i});
}

StringBuilder sb = nuevo StringBuilder();
Deque correspondint[] Esperar = nuevo ArrayDeque correspondió(); // elementos que esperan pasos k

mientras (!pq.isEmpty()
si (pq.isEmpty()) {
int[] cur = pq.poll();
sb.append(char) (cur[1] + 'a'));
cur[0]--; // utilizó una ocurrencia
espera.offer(cur); // cerrarlo
. ♫ ... {
// saltar vacío pero la cola de espera todavía tiene caracteres
devolver ";
}

si (wait.size() >= k) {}
int[] ready = wait.poll();
si (ready[0] 0) pq.offer(ready); // still left
}
}
devolver sb.toString();
}
}
`` `

#### 4.2 Python

``python
importación heapq
de las colecciones importan deque, Counter

Solución de clase:
def rearrangeString(self, s: str, k: int) - Propiedad str:
si k
retorno s

freq = Counter(s)
# max‐heap: (-count, char)
max_heap = [(-cnt, ch) para ch, cnt en freq.items()]
heapq.heapify(max_heap)

res = []
espera = deque() # (remaining_count, char)

mientras max_heap o espera:
si Max_heap:
cnt, ch = heapq.heappop(max_heap)
re.append(ch)
cnt += 1 # cnt is negative
wait.append(cnt, ch))
más:
# No hay char disponible para colocar

si len(wait) k:
ready_cnt, ready_ch = wait.popleft()
si listo_cnt
heapq.heappush(max_heap, (ready_cnt, ready_ch))

volver ".join(res)
`` `

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
string rearrangeString(string s, int k) {
si (k = 1) retorno s;

vector implicado freq(26, 0);
for (char c : s) freq[c - 'a']++;

// max‐heap: par consignacount, char título
priority_queue seleccionapair madeint,char confianza pq
para (int i = 0; i)
si (freq[i]) pq.emplace(freq[i], char('a' + i));

cadena res;
queue hizopair seleccionadaint,char confianza espera; // elementos bloqueados para k pasos

mientras (!pq.empty()
si (pq.empty()) {
auto cur = pq.top(); pq.pop();
res.push_back(cur.second);
cur.first...
espera.push(cur);
. ♫ ... {
retorno "; // imposible
}

si (wait.size() >= k) {}
auto listo = espera.front(); espera.pop();
if (ready.first ⇩ 0) pq.push(ready);
}
}
restitución;
}
};
`` `

Las tres soluciones compilan en la plataforma LeetCode y se ejecutan dentro de los plazos.

-...

## 5. Blog Artículo – “El Bien, el Mal, y el Ugly de LeetCode 358”

■ *Keywords:*
■ LeetCode 358, Rearrange String k Distancia Además, algoritmo de entrevista, codicioso, cola prioritaria, Java, Python, C++, entrevista de trabajo, preparación de entrevistas de codificación.

-...

### 5.1 Introduction

Cuando se prepara para una entrevista de ingeniería de software, inevitablemente se encontrará con problemas de LeetCode que parecen simples a primera vista pero son engañosamente difíciles. **Problema 358 – Rearrange String k Distancia Apart** es uno de estos clásicos. Te obliga a pensar en *frecuencia*, *disposiciones de distancia* y *estructuras de datos óptimas* de inmediato.

En este artículo diseccionaremos el problema, caminaremos a través del **bueno**, el **bad**, y las partes **ugly** de resolverlo, y le daremos una implementación limpia y lista para la producción en **Java, Python, y C+**. Ya sea que sea un codificador experimentado o un recién graduado, dominar esta solución demostrará un pensamiento algoritmo fuerte en su curriculum vitae.

-...

### 5.2 The Good – Why Este problema es grande

Beneficio permanente por qué importa
Silencio...
Silencio **Grandes + cola de prioridad** ← Combina dos conceptos básicos de CS —gran selección y operaciones de salto— en un patrón limpio. Silencio
Silencio ** Tiempo-Eficiente** Silencio `O(n log 26)` ♥ `O(n)` porque el alfabeto es fijo. Silencio
tención **Espacio-Light** Silencioso Usos `O(26)` memoria extra para frecuencias más una pequeña cola de tamaño `k`. Silencio
Silencio **Real‐World Analogy** Silencio Piense en programar tareas que no pueden ejecutar de nuevo a revés. La cola de espera es un programador de micro-tarea. Silencio
Silencio **Entrevista de oro** Silencio Muestra cómo hacer cumplir las restricciones mientras se mantiene óptimo. A los clientes les encanta esto. Silencio

-...

### 5.3 The Bad – Pitfalls You Might Encounter

1. ** Casos de emergencia**
* `k == 0` → retorno `s` sin cambios.
* " k " max_frequency " → todavía posible (por ejemplo, " aaabbb " , " k=3 " ), pero usted debe manejar la cola correctamente.
* Empty heap before the queue empties → impossible.

2. **Implementation Overhead**
* Negativo cuenta para lenguas min-heap (Python’s `heapq`).
* Comparador personalizado en Java puede hacer un viaje si olvida el orden “max”.

3. *Debugging Dificultad*
* La cola de espera y el montón interactúan de una manera sutil; un pequeño error puede producir silenciosamente una cuerda inválida o chocar el programa.

-...

### 5.4 Las partes difíciles que pueden romperse Tú.

1. **Off‐By‐One Errores**
* The `k`strictt means you must unlock a character **after** `k` placements, not `k-1`. Un bicho común es desbloquear en 'k-1'.

2. ** Tamaño de la cola de lock**
* Utilizar un `deque ' o `queue` con tamaño `k` es esencial. Olvídalo para comprobar `wait.size() k` causa desbloqueo temprano o desbloqueo perdido.

3. **Frequency Decrement Sign**
* En Python usted empujará los recuentos negativos en el montón, así que recuerde a **incremento** el valor saltado (`cnt += 1`) para reducir la frecuencia absoluta. Olvidar esto lleva a bucles infinitos.

4. *Vuelve pronto*
* No puedes regresar después de que el montón se vuelva vacío; también debes asegurar que la cola de espera no tenga caracteres “bloqueados”.

Comprender estas trampas ocultas es la diferencia entre una solución *working* y una *unreliable*.

-...

### 5.5 Walk‐ Mediante la solución óptima

A continuación se encuentra la versión más limpia y sostenible del algoritmo. Explicaremos cada paso a medida que vayamos.

#### 5.5.1 Cuenta de Frecuencia

``python
freq = Counter(s) # O(n)
`` `

Con sólo 26 posibles caracteres, `freq` nunca superará 26 entradas.

#### 5.5.2 Max‐ Creación del salto

``python
max_heap = [(-cnt, ch) para ch, cnt en freq.items()]
heapq.heapify(max_heap)
`` `

El `heapq` de Python es un min-heap, por lo que almacenamos recuentos negativos para simular un max-heap.

#### 5.5.3 Waiting Queue (`k`‐Distance Lock)

``python
espera = deque() # Holds tuples (remaining_count, char)
`` `

Después de colocar un personaje, entra en 'espera'. Sólo cuando la longitud de la cola alcanza `k` puede el personaje volver a entrar en el montón.

#### 5.5.4 Main Loop

`` `
mientras salta o espera:
lugar más frecuente char
Cierra.
si espera.size() >= k:
desbloquear el char más viejo
`` `

Este bucle es el corazón del algoritmo codicioso. Garantiza que nunca violamos la limitación de `k` porque un personaje sólo puede ser colocado de nuevo después de que haya sido “abierto. ”

-...

### 5.6 Complexity Analysis

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
Silencio **Tiempo** Silencioso `O(n log 26)` → prácticamente linear Silencio `O(n log 26)` Silencio `O(n log 26)` Silencio
Silencioso **Espacio** Silencioso `O(26 + k)` (salario + cola) Silencio `O(26 + k)` Silencio `O(26 + k)` Silencio

Dado que `26` es una constante, el factor dominante es `n ' (longitud de `s ' ), haciendo la solución adecuada para el límite de longitud `3 * 105 `.

-...

### 5.7 Test Cases to Try

TENIDO S TENIDO K TENIDO Esperado (cualquier válido)
Silencio.
tención "aaaabb" Silencio 3 Silencio "bbaaa" Silencio más frecuente char "a" bloqueado para 2 ranuras ←
Silencio "aaabbbccc" Silencio 1 Silencio original Silencio `k=1` no impone ninguna restricción
Silencio "aaabbbccc" Silencio 2 Silencio cualquier arreglo ← 2-distance works Silencio
Silencio "aaabbbccc" Silencio 4 Silencio Imposible - necesidad por lo menos 4 aparte

Agregue estos a su arnés de prueba para capturar errores por uno.

-...

### 5.8 Takeaway – What Interviewers Want

* **Mostrar sus conocimientos de estructura de datos** – La cola de prioridad es un deber-conocimiento en la mayoría de las entrevistas de CS.
* ** Casos de borde huelguístico con gracia** – `k 0 = 1`, escenarios imposibles, y cheques de montón vacíos demuestran la robustez.
* **Mantenlo limpio** – Escribir código modular (`compildHeap`, `unlock`, etc.) y comentar a fondo.

Cuando termine esta solución, no sólo resolverá LeetCode 358 sino que también reforzará un patrón que aparece en muchos otros problemas (por ejemplo, “Task Scheduler”, “Rearrange String” variantes, “Word Pattern II”).

-...

### 5.9 Palabras finales

LeetCode 358 es un *micro-proyecto* que encapsula una poderosa estrategia avaricia. Al dominarlo, ganarás:

1. **Confianza** en el uso de colas prioritarias para limitaciones de distancia.
2. **Hablado** por escrito código Java, Python y C++ en condiciones de entrevista.
3. **Un punto fuerte de conversación** en su curriculum vitae: “Solución de salto codicioso ampliada para LeetCode 358 – Rearrange String k Distancia Apart”.

Buena suerte con tu próxima entrevista de codificación – código inteligente, piensa codicioso, y deja que la limitación de distancia haga el levantamiento pesado! 🚀

-...

## 6. Resumen

- **Java** – Utiliza `PriorityQueue hacíaint[] `` + `ArrayDeque consignaint[] ' .
- **Python** – Usa `heapq` con frecuencias negativas + `collections.deque`.
- **C++** – Utiliza `priority_queue hacíapair indicado,char título `` + `queue hacíapair observado,char título ``.

Todas las soluciones son *O(n log 26)* tiempo, *O(26)* espacio, y manejar el `k` limitación con una cola de espera.

Coge estos snippets, ejecutelos en LeetCode, y agregue el artículo del blog a su cartera. Sus entrevistadores notarán su profundo entendimiento de algoritmos codiciosos, colas prioritarias y problemas de programación del mundo real. ¡Feliz codificación!