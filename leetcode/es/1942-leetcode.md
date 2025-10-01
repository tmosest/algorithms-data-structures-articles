-...
Título: LeetCode 1942. El número de la silla más pequeña ocupada -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Llámame 1942. El número de la silla más pequeña ocupada – Solución en **Java, Python & C++* *

A continuación encontrará una implementación limpia y lista para la producción del clásico problema LeetCode “Smallest Unoccupied Chair” en tres idiomas.
Todas las soluciones utilizan **dos colas prioritarias (saltos)** – una para sillas disponibles y una para sillas ocupadas ordenados por el tiempo de salida – dando un **O(n log n)** tiempo y **O(n)** complejidad espacial.

-...

## Problema Recap

■ Estás en una fiesta con **n** amigos (índices basados en 0).
■ Hay infinitamente muchas sillas numeradas 0...∞.
■ Cuando llega un amigo, toman la silla inocupada.
■ Cuando un amigo sale de la silla se libera inmediatamente y puede ser tomado por alguien que llega al mismo tiempo.
[arrival_i, departure_i]` (Los tiempos de llegada son distintos).
■ Devuelve el número de silla que **targetFriend** ocupará.

-...

## 1. Python 3 – 9 líneas (dos montones)

``python
importación heapq
de la importación Lista

Solución de clase:
def más pequeño Chair(self, times: List[List[int]], targetFriend: int) - título int:
# 1 Ordenar amigos por hora de llegada
orden = orden(range(len(times)), key=lambda i: times[i][0])

# 2⃣ Montaje de sillas libres (inicialmente 0...n-1), montón de sillas ocupadas (departamento, asiento)
libre, ocupado = lista(range(len(times))), []

para idx en orden:
llegar, salir = tiempos[idx]

# 3️ Libere todas las sillas cuyo propietario ha dejado por el tiempo de llegada
mientras que ocupado y ocupado [0] [0]
heapq.heappush(gratis, heapq.heappop(ocupado)[1])

# 4️ Coge la silla libre más pequeña
silla = heapq.heappop(gratuito)

si idx == objetivo Amigo: # 🎯 Found the answer
silla de retorno

# 5️ Silla de la marca como ocupada hasta 'leave '
heapq.heappush(ocupado, (leave, chair))
`` `

**Por qué funciona* *
- El montón " libre " siempre contiene todas las sillas que actualmente están vacías.
- El montón 'ocupado' se ordena por el tiempo de salida; el elemento superior es la silla que liberará lo más pronto.
- Al aparecer repetidamente de 'ocupado' cuando su tiempo de salida ≤ la llegada actual, mantenemos `libre' actualizado.
- La silla libre más pequeña está siempre en la parte superior de `libre`, por lo que podemos asignarlo en O(log n).

-...

## 2. Java – `PriorityQueue` versión

``java
importar java.util*;

Clase Solución {
público más pequeño Presidente(int[][] times, int targetFriend) {}
int n = times.length;

// 1 / ⃣ Ordenar índices de amigos por hora de llegada
Integer[] order = nuevo Integer[n];
para (int i = 0; i)
Arrays.sort(order, Comparator.comparingInt(i - título times[i][0]));

// 2Get⃣ Min‐heap of free chairs
Prioridad Búsquedas realizadasInteger libremente = nueva prioridadQueue correspondió();
para (int i = 0; i)

// 3Ω⃣ Min‐heap of occupied chairs: pair(departure, seat)
PriorityQueue madeint[] ocupado = nuevo PriorityQueue asignado(Comparator.comparingInt(a - título a[0]));

para (int idx : order) {
int arrive = times[idx][0];
int leave = times[idx][1];

// 4down Sillas de liberación cuyo propietario dejó
mientras (!occupied.isEmpty() " ocupado.peek()[0] " )
free.offer(occupied.poll()[1]);
}

// 5down Tome la silla libre más pequeña
silla int = libre.poll();

si (idx == targetFriend) silla de retorno;

// 6 millas ⃣ Silla de marca como ocupada hasta 'salir '
ocupado.offer(nueva int[]{leave, chair});
}
retorno -1; // no alcanzable - objetivo de garantía de entrada El amigo existe
}
}
`` `

-...

## 3. C++ – `priority_queue` + `vector `

``cpp
Incluido el título
#include >
#include >

Clase Solución {
public:
más pequeño Chair(std:::vector obtenidosstd:::vector seleccionadoint implicados iguales veces, int targetFriend) {}
int n = times.size();

// 1 / ⃣ Ordenar índices por hora de llegada
std::vector seleccionado(n)
std::iota(order.begin(), order.end(), 0);
std::sort(order.begin(), order.end(),
[](int a, int b){ return times[a][0] [b] [0]; }

// 2Get⃣ Min‐heap of free chairs
std:::priority_queue obtenidosint, std::vector fielint, std::greater interpretadoint título libre;
para (int i = 0; i)

// 3Ω⃣ Min‐heap of occupied chairs: pair(departure, seat)
std::priority_queue corresponding
std::pair obtenidos,int
std::vector seleccionados::pair seleccionado,int
std::greater obtenidosstd::pair obtenidosint,int
- Ocupado;

para (int idx : order) {
int arrive = times[idx][0];
int leave = times[idx][1];

// 4down Gratis todas las sillas cuyo propietario se fue ahora
mientras (!occupied.empty() " ocupado.top().
free.push (ocupied.top().second);
ocupados.pop();
}

// 5 Cambios  Grab Tome la silla libre más pequeña
silla int = libre.top(); libre.pop();

si (idx == targetFriend) silla de retorno;

// 6 Cambios  chair Silla de marca ocupada hasta la salida '
ocupado.emplace(leave, chair);
}
retorno -1; // nunca debe suceder
}
};
`` `

-...

## 🎯 Por qué estas soluciones ganan entrevistas

Silenciosos en el futuro Python Silencio en Java
Silencio--------------------------
Silencio **Readability** Silencio 9 líneas + comentarios Silencio Compacto, tipo seguro Silencio Conciso, estructuras de datos explícitas
Silencio ** Complejidad en el tiempo** Silencio O(n log n) Silencio O(n log n)
Silencio ** Complejidad del espacio** Silencio O(n) Silencio O(n) Silencio
Silencio **Key Insight** Silencio Dos colas prioritarias: libre " ocupado Silencio Dos `PrioridadQueue`s vivir Dos `prioridad_queue`s con la comparación personalizada
Silencio **Edge Cases Handled** tención Releases at same timestamp, target friend at first or last

-...

Artículo del blog optimizado

■ **Título**: "LeetCode 1942 – La más pequeña silla ocupada: Una profunda inmersión en soluciones de dos saltos (Java, Python & C++)”

-...

Introducción
- Gancho: “Imagina una fiesta donde cada nuevo invitado debe sentarse en la silla vacía *smallest*. ¿Cómo haces un seguimiento de la siempre cambiante alineación de sillas? ”
- Establece el problema, enlace con LeetCode, mencionar las limitaciones (n ≤ 104).
- SEO palabras clave: *LeetCode 1942*, *Smallest Unoccupied Chair*, *Interview Question*, *Two Heaps*, *Priority Queue*, *Java*, *Python*, *C+*.

### #2# Problema de desintegración
- Diagrama visual de llegadas & salidas.
- Clarify “presidencia se vuelve libre al instante” y “los tiempos de llegada son distintos”.
- ¿Por qué una simulación ingenua (arriba de sillas) es O(n2) e impráctica.

#### 3down⃣ Naïve vs. Optimal Approaches
TENCIÓN TENIDO Complejidad ANTERIEDARES ANTERIOR Cuando se utiliza
Silencio--------------------------------------------------------------
← Brute Force Array Silencioso O(n2) ← Memoria pesada, tiempo fuera TENIDO PEQUEÑO
Silencio Eventos clasificados + TreeSet ← O(n log n) Silencio Ligeramente más código Silencio Cuando usted está cómodo con las operaciones establecidas ¦
Silencio Dos saltos (recomendados) Silencio O(n log n) Silencio más simple  **

#### 4down⃣ The Two‐Heap Strategy (The Good)
- **Salta de silla gratuita**: siempre tiene la silla más pequeña disponible.
- **Ocupado Presidente Heap**: ordenados por tiempo de salida.
- Lógica de liberación: pop de ocupado mientras la salida ≤ actual llegada → silla de empuje de nuevo en libre.
- Asignación: abrir la parte superior de la libre, empujar hacia ocupado con su partida.
- Deténgase temprano cuando el amigo objetivo esté sentado.

#### Code Walk‐through (Python)
- Explicación paso a paso con comentarios en línea (la solución de 9 líneas).
- Destaca el bucle que libera sillas.
- Mostrar cómo la salida temprana ahorra trabajo.

#### 5down⃣ Traducción a Java & C++ (El Ugly)
- Discuss language-specific quirks:
- Java `PriorityQueue` es un min‐heap por default? (No, es un min-heap pero necesita la comparación).
- C++ `priority_queue` es max‐by-default → uso `greater seleccionado... `` comparador.
- Mostrar cómo guardar parejas (partida, silla) de forma segura.
- Dificultades comunes: olvidando el pop después de los errores de los índices.

#### 6down⃣ Edge‐ Lista de verificación de casos (El Mal)
Silencio Caso Edge Silencioso Qué ver para Silencio
Silencio...
Silencio amigo Target llega el último Silencio Asegurar los procesos de bucle todas las llegadas. Silencio
Silencio Múltiples salidas al mismo tiempo tención Liberar todo antes de asignar. Silencio
El tiempo de llegada es igual a la salida anterior tención Release primero (según la llegada) para que la silla pueda ser reutilizada. Silencio
Silencio Muy grande n (104) Silencio Dos montones guardan memoria O(n). Silencio

### 7 carreras Performance Tuning Tips
- Use `heapq`s `heappush`/`heappop ' (Python) - no hace falta manual `push/pop`.
- En Java, pre-poblar el montón libre con 'IntStream.range(0, n).porCada(gratuito::offer)` para legibilidad.
- En C+++, utilice el `std::vector asignadoint ' para el montón libre si desea evitar el `push/pop` overhead para los primeros elementos n.

### 8️ Variaciones " Extensiones
- ¿Y si los tiempos de llegada no eran distintos? Agregue una regla de ruptura de corbata (por ejemplo, ID de amigo).
- ¿Cómo manejarías un número finito de sillas? Utilice un contador para el caso “sin silla disponible”.
- Use un árbol de segmentos o un árbol indexado binario para las consultas mínimas de rango si desea practicar diferentes estructuras de datos.

#### 9Ω⃣ Conclusion > Final Takeaway
- Summarize por qué la solución de dos saltos es el *sweet spot* para LeetCode 1942.
- Alentar a los lectores a practicar mediante la implementación de las tres versiones, probar contra los insumos aleatorios ( " Unidosttest " / JUnit / Google Test).
- Invitar comentarios: “¿Con qué otros problemas de entrevista estás luchando? ”

Recursos adicionales
- Enlace a los hilos de discusión de solución LeetCode.
- GitHub repo con las tres implementaciones.
- Video walkthrough en YouTube para estudiantes visuales.

-...

## 🚀 Final Thought

Con estos **tres implementaciones concisas y eficientes** y la explicación **estructurada de entrevistas**, podrás abordar con confianza a LeetCode 1942 e impresionar a los entrevistadores con velocidad y claridad. ¡Feliz codificación!

-...

■ *No dude en dejar las preguntas en los comentarios – ¡hagamos que cada nuevo invitado se sienta como en casa! *