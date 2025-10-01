-...
Título: LeetCode 1926. Salida más cercana de la entrada en laberinto -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. LeetCode 1926 – “La salida más cercana de la entrada en laberinto”

** Resumen del programa**

TENIDO ANTERIOR ANTERIOR Descripción
Silencio...
Silencio ** Objetivo** Silencio Encuentra el número mínimo de pasos de una celda de entrada dada a la salida más cercana (una célula fronteriza vacía) en un laberinto `m × n`. Silencio
Silencio **Movimiento** Silencio 4-directional (up, down, left, right). No puede entrar en las paredes (`'+'`) o fuera del laberinto. Silencio
Silencio ** Entrada** Silencioso `car[] [] laberinto`, `int[] entrada ` (la entrada está garantizada a ser `'. Silencio
Silencio ** Salida** Silencio Pasos mínimos a la salida más cercana, o `-1` si no existen. Silencio
Silencioso **Constraints** Silencioso `1 ≤ m, n ≤ 100`


La solución clásica es **Breadth‐First Search (BFS)** – el árbol más corto en un gráfico no ponderado.
A continuación se presentan implementaciones limpias y de producción en **Java**, **Python**, y **C+**.

-...

## 2. Código - Tres idiomas

### 2.1 Java – Clean, Fast BFS

``java
importar java.util*;

Solución de la clase pública {}
int más cercanoExit(char[][] laberinto, int[] entrada) {
int rows = laberinto.length;
int cols = laberinto[0]. longitud;

// Instrucciones: derecha, izquierda, abajo, arriba
int[] dirs = {0, 1}, {0, -1}, {1}, {-1, 0}};
Queue hizo [] confiar q = nuevo ArrayDeque correspondió();
q.offer(entrance);
laberinto[entrance[0][entrance[1]] = '+'; // marca visitada

int steps = 0;
(!q.isEmpty()) {
pasos+; // una capa = un paso
int size = q.size();
para (int i = 0; i) {}
int[] cur = q.poll();
para (int[] d : dirs) {
int r = cur[0] + d[0];
int c = cur[1] + d[1];
si continúan (r s 0 TENIDO SONIDO SONIDO= hileras ANTETENIDO c = 0 TENIDO= cols)
si (maze[r][c] == '+') continúan; // muro o ya visitado

// Salida encontrada (en la frontera, pero no en la entrada)
si (r == 0 Silencioso r == filas-1 Silencioso c == 0 Silencioso c == cols-1)
medidas de retorno;

laberinto[r][c] = '+'; // marca visitada
q.offer(new int[]{r, c});
}
}
}
retorno -1; // ninguna salida accesible
}
}
`` `

### 2.2 Python – Simple BFS con `deque `

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def más cercanoExit(self, laberinto: List[List[str]], entrada: List[int]) int:
R, C = len(maze), len(maze[0])
dirs = [(0, 1), (0, -1), (1, 0), (-1, 0)]
q = deque([tuple(entrance)])
laberinto[entrance[0][entrance[1]] = '+'

pasos = 0
mientras q:
pasos += 1
para _ en rango(len(q)):
r, c = q.popleft()
para dr, dc en dirs:
nr, nc = r + dr, c + dc
si no (0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
continuar
si laberinto[nr] == '+': # wall / visited
continuar
# Border exit (not entrance)
si nr == 0 o nr == R-1 o nc == 0 o nc == C-1:
Pasos de retorno
[nr] [nc] = '+ '
q.append(nr, nc))
retorno -1
`` `

### 2.3 C++ – BFS with `queue` (C+17)

``cpp
Incluido el título
#include >

Clase Solución {
public:
int nextExit(std::vector efectuadostd:::vector correspondía caracteres bajos ganando maze, std::vector correspondint limitada entrance) {
int R = laberinto.size(), C = laberinto[0].size();
const std::vector seleccionado::pair obtenidosint,int
{0,1}, {0,-1}, {-1,0}
};
std::queue obtenidosstd::pair obtenidosint,int Confeder q;
q.push({entrance[0], entrance[1]});
laberinto[entrance[0][entrance[1]] = '+'; // bandera visitada

int steps = 0;
(!q.empty()) {
++ pasos; // capa = paso
int sz = q.size();
para (int i=0; i interpretasz; ++i) {}
auto [r, c] = q.front(); q.pop();
para (auto [dr, dc] : dirs) {
int nr = r + dr, nc = c + dc;
si (nr < 0 Новыный nr ненные ныенный noc неный неный ненный неный неный неный C) continuar;
si (maze[nr] [nc] == '+') continúan;

// Salida en la frontera (pero no la entrada en sí)
si (nr==0 Silenciosos inmortales nr==R-1
medidas de retorno;

[nr][nc] = '+';
q.push({nr, nc});
}
}
}
retorno -1;
}
};
`` `

Las tres soluciones se ejecutan en el tiempo **O(m × n)**, utilizando una bandera visitada en el lugar (convirtiendo células a '+').
Manejan cada caso de borde – entrada en la frontera, celdas aisladas, grandes áreas abiertas – con seguridad.

-...

## 3. Blog Artículo – “El Bien, el Mal, el Ugly de LeetCode 1926”

-...

# 🚀 Salida más cercana de la entrada en Maze – LeetCode 1926
### El enfoque BFS explicado en Java, Python y C++
■ *Listo para su próxima entrevista técnica? Maestro este problema de laberinto-shortest-path y brilla en su próxima búsqueda de trabajo. *

-...

## 3.1 Meta‐Descripción
*¿Quieres ace LeetCode 1926?* Aprenda la solución BFS, vea código Java/Python/C++ y descubra el *bueno, malo y feo* de este problema de entrevista clásica. Ideal para la preparación de la entrevista de software prep.

-...

## 3.2 Problema Recap

■ **Salida más cercana de la entrada en Maze* *
■ Encontrar los pocos pasos de la entrada dada a una célula fronteriza vacía en una cuadrícula de 2D donde `'+'` son paredes y `'.` son células caminables.

- *Tamaño bruto* `1 ≤ m, n ≤ 100`
- **Movimiento:** 4-directional (sin diagonales)
* Objetivo: * Pasos mínimos → `-1` si no hay salida

-...

## 3.3 ¿Por qué BFS? La visión del núcleo

*Todos los bordes tienen peso 1* – el laberinto es un gráfico ** sin peso**.
BFS amplía los nodos de nivel por nivel; la primera vez que llegamos a una célula fronteriza (excepto la entrada) sabemos que tenemos la distancia más corta.
No es necesario para Dijkstra, no DP, no heuristic – BFS simple es óptimo.

-...

## 3.4 Algorithm Walkthrough

1. ** Entrada de Marcas** – Poner `maze[entrance]` a una pared (`‘+’) por lo que nunca lo revisitamos.
2. **Initializar la cola** – Empuje la coordenadas de entrada.
3. **Directional Offsets** – `[(0,1),(0,-1),(1,0),(-1,0)].
4. *Exasión de nivel por curso*
- " pasos+ " antes de procesar la capa actual.
- Para cada nodo en la capa, explore las 4 direcciones.
- Saltear las celdas o las paredes.
- Si la nueva célula se encuentra en la frontera → ** Retorno** actual `pasos`.
- Marca de Else como visitada (`+’’) y encuue.
5. **No hay salida** – La cola vacía → retorno `-1`.

-...

## 3.5 Corner‐ Lista de verificación de casos

← Caso Edge tóxico Por qué Es importante
Silencio...
La entrada en la frontera podría considerarse una salida → ** **No debe contarse**. Silencio entrada Mark como se visita inmediatamente. Silencio
Silencio Todas las celdas son paredes Silencio No hay camino → `-1`. Silencio BFS terminará después de 1 × n operaciones de cola. Silencio
Silencio Gran área abierta ← La cola puede crecer grande → use `ArrayDeque`/`deque` (no hay lista enlazada). Silencio Uso `ArrayDeque` en Java / `deque` en Python. Silencio
tención Tamaño de entrada 100 × 100 tención Max 10,000 celdas → fino para la memoria. ← El marcado en el lugar mantiene el array visitado fuera de la imagen. Silencio

-...

## 3.6 Good, Bad & Ugly – In‐Depth Analysis

Lo que es bueno para la vida Lo que es malo para la vida
Silencio------------------------------------------------------
Silencio ** Fuerza Algorítmica** Silencio BFS garantiza la optimización, tiempo O(mn), memoria O(mn). ← Requiere una cola – sobrecarga de la asignación de objetos en Java, lista en Python. Ninguno si te olvidas de marcar visitada → bucle infinito. Silencio
Silencioso **Coding Simplicidad** Silencio Conjunto de cuatro direcciones, recuento de capas, bucle único. Muy legible, sin recidiva. La marcación en el lugar TEN modifica la entrada; si el callador reutiliza el laberinto esto es destructivo. Silencio
Silencio **Performance** Silencio Comprobaciones vecinas de tiempo constante, salida temprana se detiene temprano. Silencio Visitas más peligrosas cada celda → 10,000 operaciones (trivial). Silencio Usar `'+' para marcar visitado puede causar cache‐miss si el laberinto es grande; una matriz separada 'bool' podría ser más clara. Silencio
Silencio **Robustness** Silencio Maneja cualquier entrada válida, incluyendo la frontera. Debe ignorar explícitamente la entrada como salida. TENIDO Olvidar comprobar `si (r == 0 TENIDO ...)` puede dar la distancia incorrecta cuando la entrada ya está en la frontera. Silencio
Silencio **Espacio** Silencioso O(mn) con bandera visitada en el lugar; cola máx tamaño ~ perímetro. Si utilizas una matriz separada 'visitada', duplicarás la memoria. Si el laberinto es enorme (no en limitaciones), la profundidad de recursión/apilación podría soplar en alternativas DFS. Silencio

-...

## 3.7 Performance & Space Molinos

← Técnica Silenciosa Silencio Cuándo usar
Silencio------------------------------
Silencio **In‐place visited flag** (`maze[i][j] = '+'') Silencio Cuando se le permite mutar la entrada (la mayoría de los problemas de LeetCode). Silencio Guarda `O(mn)` matriz booleana. Silencio
Silencio **Pre-allocate directions array** Silencio Previene la creación de 4 nuevos 'int[]` por nodo. Silencio Menor speedup en Java/C++. Silencio
Silencio **`ArrayDeque` en lugar de `LinkedList`** TEN Java 8+ Silencio Operaciones de cola más rápida, menos GC churn. Silencio
Silencio **Use `deque` en Python** Silencio Python 3 Silencio `popleft()` es O(1) – más rápido que la lista pop(0). Silencio
Silencio **Layer-counting** (`steps++` outside internal loop) Silencio Necesitaba devolver la distancia exacta. tención Evita el seguimiento de una distancia por nodo. Silencio
Silencio **Early exit check** (`if on border return steps`) tención Para cuando se encuentra la primera salida. Silencio Ahorra tiempo en laberintos escasos. Silencio

-...

## 3.8 Consejos de entrevista – Cómo hacer realidad esta pregunta

1. **Clarificar la definición de una salida**
*Una salida es una célula fronteriza vacía que no es ** la entrada misma. *

2. **Declara tus asunciones**
*La entrada es transitable.
*No puedes entrar en las paredes (`'+'`). *

3. # Toma el Gráfico #
*Trata cada célula como nodo; los bordes conectan las células adyacentes transitables. *

4. *Elige BFS*
*Explicar por qué BFS es la opción óptima: gráfico sin ponderar, camino más corto.
*Mostrar que el DFS sería incorrecto (noche encontrar un camino más largo). *

5. *La complejidad*
*Tiempo: O(m × n).
*Espacio: O(m × n) para cola + bandera visitada. *

6. ** Casos de emergencia**
*Continúe por el caso “entrada en la frontera”.
*Explica cómo evitas contarlo como una salida. *

6. *Código limpio de la palabra*
*Utilizar bucles concisos, evitar estructuras de datos redundantes.
*En Java, utilice `ArrayDeque`. *

7. **Test on Your Phone**
*Si es posible, ejecute manualmente un ejemplo 3×3 para ilustrar la conteo de nivel. *

-...

## 3.9 Conclusión – El Takeaway

LeetCode 1926 puede parecer un rompecabezas de laberinto simple, pero prueba *graph traversal intuition* y *maneamiento obligatorio*.
Al dominar la solución BFS – y conocer los detalles buenos, malos y feos – no solo resolverás este problema de manera eficiente sino también demostrarás:

- Una comprensión sólida de los fundamentos algorítmicos**.
- La capacidad de escribir **clean, código listo para la producción**.
- Conocimiento práctico de optimizaciones de rendimiento**.

¡Buena suerte en tu próxima entrevista! ▪

-...

## 3.10 Share " Discuss

■ ¿Encontró este artículo útil? Deja un comentario a continuación con tus propios hacks de periferia o pide ayuda en otros problemas de LeetCode.
■ ¡Feliz codificación!

-...

*(End of article)*

-...

## 4. Agitación

Ahora tienes:

- ** Tres implementaciones comprobadas por batalla** listas para cualquier lenguaje de entrevista.
- Una profunda inmersión en *por qué BFS funciona*, cómo evitar las trampas, y cómo manejar cada caso de borde.
- Una guía de estilo blog que enmarca el problema de una manera que los entrevistadores aman: supuestos claros, razonamiento paso a paso, discusión de complejidad, y consejos del mundo real.

Utilice este conocimiento para fortalecer su cartera, impresionar a los reclutadores, y asegurar ese papel de ingeniería de software de sueño. ¡Feliz piratería!

-...

¡Buena suerte, codificador! *