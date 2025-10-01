-...
Título: LeetCode 773. Puzzle deslizante -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 773. Puzzle deslizante – El bueno, el malo, y el
*(Cómo dominar un problema duro de LeetCode, escribir código limpio en **Java**, **Python**, y **C+**, y convertirlo en una pieza de portafolio de arranque de trabajo.) *

-...

## Tabla de contenidos
1. [Problema Recap](#problema-recap)
2. [Por qué este problema importa] (por qué este problema-matters)
3. [The Classic Approach – Breadth‐First Search (BFS)](#the-classic-approach---breadth-first-search-bfs)
4. [ Representación Estatal " Codificación " )(#representación del Estado - codificación)
5. [Pre-check: Solvability](#pre-check-solvability)
6. [Putting It All Together – Code Snippets](#puting-it-all-all-code-snippets)
- Java
Python
- C++
7. [El Bien, el Mal, el Ugly] (El bueno-el-el-bad-el-ugly)
8. [SEO Tips " How to Market Esta Habilidad](#seo-tips--cómo-al-mercado-esta-skill)
9. [Pensamientos Finales](Pensamientos finales)

-...

## Problema Recap
**773. Puzzle deslizante* *

■ *En un tablero de 2 × 3, hay cinco fichas etiquetadas 1–5 y un cuadrado vacío `0`.
■ En un movimiento se puede cambiar `0` con cualquiera de sus números de cuatro direcciones adyacentes. *
■ The goal state is `[1,2,3],[4,5,0].
■ Devuelve el número mínimo de movimientos para resolver el rompecabezas, o `-1' si imposible.

-...

## Por qué este problema importa
* ** Profundidad algorítmica** – Le exige razonar sobre permutaciones, espacios estatales y paridad.
* ** habilidad práctica** – Sliding-puzzle es una ilustración clásica de *Breadth‐First Search* (BFS) en gráficos.
* **Interview flag** – Muchas empresas lo utilizan (o variantes) para probar técnicas de traversal, escaneo y optimización de gráficos.
* Portafolio showcase** – Una solución limpia y multilingüe demuestra *la fluidez algorítmica* y *la artesanía de código*.

-...

## The Classic Approach – Breadth‐First Search (BFS)
1. **Prueba cada configuración de la tabla como nodo. #
2. **Neighbors** – Todas las configuraciones alcanzables por un solo movimiento (swap `0` con una baldosa adyacente).
3. **BFS** – Porque cada borde tiene igual peso (1 movimiento), BFS garantiza la primera vez que alcanzamos el objetivo usamos el número mínimo de movimientos.
4. ** Conjunto visitado** – Para evitar reprocesar la misma configuración.

■ ** Complejidad del tiempo**: `O(6!)` en el peor de los casos (720 estados) – constante para este problema.
■ ** Complejidad del espacio**: `O(6!)` – cola + conjunto visitado.

-...

## State Representation " Encoding
Guardar el tablero como un array 2-D es conveniente para la legibilidad, pero para la piratería y rápidas comprobaciones de igualdad que *codificamos* el estado en una cadena (o un entero de 64 bits).

### Encoding to String
* Aplanar la matriz 2×3 hilera a mano → `"123450"` para el estado de gol.
* Sencillo, legible por humanos, y trabaja con `Setring fiel`.

### Encoding to Integer (Bit Manipulation)
* Pack 3 bits por ficha (valores 0–5).
* Todo el estado encaja en un entero de 18 bits → `int`.
* Más rápido hash y menos memoria arriba.

Ambas codificacións se muestran en los fragmentos de código a continuación.

-...

## Pre-check: Solvability
El punzón deslizante es solvable **iff** la paridad de permutación (número de inversiones) es incluso.
`` `
inversiones de entrada = 0;
j) Si el estado[i] y el estado[j] y el estado[i] != 0 y estado[j] != 0
inversiones++;
si inversiones % 2 == 1 → imposible → regreso -1
`` `
Este cheque rápido nos salva de ejecutar BFS en tablas insolvables.

-...

## Put it all Together – Code Snippets

■ *Las tres implementaciones utilizan la misma lógica: BFS + asignación de conjuntos visitados + cartografía vecina. *
■ *Están listos para pegar en LeetCode, su IDE, o un simulador de entrevista de codificación. *

### 1. Java

``java
importar java.util*;

Solución de la clase pública {}
// Lista de adyacencia para las posiciones 0..5 (2x3 tablero)
privada estática final int[][] NEIGHBORS = {
{1,3}, // 0
{0,2,4}, // 1
{1,5}, // 2
{0,4}, // 3
{1,3,5}, // 4
{2,4} // 5
};
estática privada final String TARGET = "123450";

public int slidingPuzzle(int[][] board) {
Inicio de la cuerda = serialize (board);
si (!isSolvable(start)) retorno -1;
si (start.equals(TARGET)) devuelve 0;

Queue wonString confía q = nuevo ArrayDeque corresponde();
Establecer:String titulada visitado = nuevo HashSet correctamente();
q.offer(start);
visitado.add(start);
int moves = 0;

(!q.isEmpty()) {
int sz = q.size();
para (int i = 0; i) {}
Cura de cuerda = q.poll();
si (cur.equals (TARGET)) movimientos de retorno;
int ceroIdx = cur.indexOf('0');
para (int nb : NEIGHBORS[zeroIdx]) {}
Cierre siguiente = swap(cur, ceroIdx, nb);
q.offer(next);
}
}
moves+;
}
retorno -1; // Nunca debería pasar si ser solvable
}

private String serialize(int[][] board) {
StringBuilder sb = nuevo StringBuilder();
para (int[] fila : tabla)
para (int v : fila)
sb.append(v);
devolver sb.toString();
}

booleano privado esSolvable(Estado de cuerda) {
int[] nums = state.chars().map(c - confianza c - '0').toArray();
int inv = 0;
para (int i = 0; i)
para (int j = i + 1; j)
si (nums[i] != [j]!= [j]
inv++;
inv % 2 == 0;
}

swap (String s, int i, int j) {
char[] arr = s.toCharArray();
char tmp = arr[i];
arr[i] = arrr[j];
arrr[j] = tmp;
volver nuevo String(arr);
}
}
`` `

### 2. Pitón

``python
de las colecciones importa
de la importación Lista

Solución de clase:
NEIGHBORS =
[1, 3], 0
[0, 2, 4]
[1, 5],
[0, 4]
[1, 3, 5], # 4
[2, 4]
]
TARGET = "123450"

def slidingPuzzle(self, board: List[List[int]) - int:
inicio = ''.join(str(v) para fila en tabla para v en fila)
si no uno mismo._is_solvable(start):
retorno -1
si empiezas == yo. TARGET:
retorno 0

q = deque([start])
visitados = {start}
movimientos = 0

mientras q:
para _ en rango(len(q)):
cur = q.popleft()
si se curan. TARGET:
Cambios de retorno
cero = cur.index('0')
para Nb en uno mismo. NEIGHBORS[zero]:
nxt = self._swap(cur, cero, nb)
si no está en visita:
visitado.add(nxt)
q.append(nxt)
movimientos += 1
retorno -1

@staticmethod
def _is_solvable(state: str) - Propiedad Bool:
nums = [int(c) for c in state]
inv = sum(1 para i en rango(len(nums))
para j en rango(i + 1, len(nums))
si nums[i] != 0 y nums[j] != 0 y nums[i] ⇩ nums[j]
inv % 2 == 0

@staticmethod
def _swap(s: str, i: int, j: int) - confía str:
lst = list(s)
lst[i], lst[j] = lst[j], lst[i]
volver ''.join(lst)
`` `

### 3. C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
const vector identificador NEIGHBORS = {}
{1,3}, // 0
{0,2,4}, // 1
{1,5}, // 2
{0,4}, // 3
{1,3,5}, // 4
{2,4} // 5
};
const string TARGET = "123450";

cadena serialize(cont vectorial identificadovector fielint estrecho contacto junta) {
cuerda s;
para (auto &row : bordo)
(int v : row) s.push_back('0' + v);
retorno s;
}

bool isSolvable(const string borde state) {
vector implicado nums(state.size());
para (int i = 0; i < state.size(); ++i) nums[i] = state[i] - '0';
int inv = 0;
para (int i = 0; i) ++i)
para (int j = i + 1; j) nums.size(); ++j)
si (nums[i] " nums[j] " nums[i]
++inv;
inv % 2 == 0;
}

swap de cadena(cont string limitado s, int i, int j) {
hilo t = s;
swap(t[i], t[j]);
t;
}

public:
int slidingPuzzle(vector identificadovector fielint sentido pizarra) {
string start = serialize (board);
si (!isSolvable(start)) retorno -1;
si (start == TARGET) devuelve 0;

queue hacía referencia q;
unordered_set obtenidosstring confianza vis;
q.push(start);
vis.insert(start);
int moves = 0;

(!q.empty()) {
int sz = q.size();
para (int k = 0; k)
string cur = q.front(); q.pop();
si (cur == TARGET) movimientos de retorno;
int 0 = cur.find('0');
para (int nb : NEIGHBORS[zero]) {}
string nxt = swap(cur, cero, nb);
q.push(nxt);
}
}
++moves;
}
retorno -1; // Inalcanzable si solvable
}
};
`` `

■ *Los tres códigos están listos para funcionar, con comentarios en línea y una separación clara entre la lógica BFS, la codificación del estado y el control de la soledad. *

-...

## The Good, The Bad, The Ugly

♦ Subtítulos Lo que funcionó 
Silencio--------------------------------------------------...
Silencio **Bueno – Concepto** Silencio *BFS garantiza la optimización en un gráfico sin ponderar.* Silencio — Silencio Mantenga BFS en el núcleo de cualquier problema de estilo de puntillas deslizantes. Silencio
Silencio **Bien - Codificación** Silencio El estado de String es legible, simple y trabaja con `Set`. El bit-mask entero es más rápido y eficiente en memoria. La elección de la representación correcta puede ser difícil. tención Para entrevista: mostrar ambos y explicar los cambios. Silencio
Silencio **Bien – Pre-check** tención La paridad de la Solvabilidad evita la búsqueda innecesaria. tención Recuerde que 0 está excluido del recuento de inversión. Siempre agregue un cheque de solvabilidad cuando el tamaño del rompecabezas 3. Silencio
Silencio **Bad – Verbose Implementation** tención Lista de vecinos manuales, la lógica swap puede convertirse en caldera. Silencio, difícil de leer. Usar funciones de ayuda, mantenerlas pequeñas. Silencio
Silencio **Bad – Edge Cases** Silencio Cuando el consejo ya está resuelto. Necesita manejar 0 movimientos. Añadir un cheque rápido de igualdad antes de BFS. Silencio
Silencio **Ugly – Recursion / DFS** Silencio Algunas soluciones utilizan erróneamente DFS o recursión. ← DFS no puede garantizar pasos mínimos; el desbordamiento de la pila de riesgo. Silencio pegado a la BFS iterativa para la óptimaidad garantizada. Silencio
Silencio **Ugly – Over-Optimization** ← Utilizar estructuras de datos complejas (por ejemplo, hash personalizado) cuando el conjunto de cuerdas simples es suficiente. Silencio Añade carga cognitiva, riesgo de errores. La Simplicidad tórax supera la micro-optimización para la configuración de entrevistas. Silencio

-...

## SEO Tips & How to Market Esta habilidad

1. **Keyword‐Rich Title* *
*“Solving LeetCode 773 – Sliding Puzzle en Java, Python, C++ (BFS + Máscara de Bit) – Job‐Ready Interview Guide”*

2. **Meta Descripción**
*“Master LeetCode Sliding Puzzle con soluciones limpias de lenguaje múltiple. Aprende BFS, codificación estatal, solvabilidad y optimización para entrevistas. Obsérvese por los reclutadores.”*

3. ** Enlace interno**
- Enlace a los blogs relacionados: *“Breadth‐First Search Explained”, “State Space Search in Interview”, “C++ Bit Manipulation Tricks”*.

4. **Visuales* *
- Incluir una animación paso a paso de capas de expansión BFS.
- Mostrar una tabla de recuento de inversión para la solvabilidad.

5. ** Call‐to-Action**
- “Descargue el PDF de todas las soluciones”, “Suscríbete para problemas semanales de entrevista”, “Contácteme para un papel de instrucciones de datos”.

5. *Proofo Social*
- Agregue una sección con * “Cómo aterricé un papel de Ingeniero de Software aplastando los rompecabezas de LeetCode”* con una breve anécdota.

6. **Use Schema.org**
Agregue el esquema del artículo con autoría, fecha de publicación, y el marcado del código para que los motores de búsqueda puedan resaltar su contenido.

7. ** Participación comunitaria* *
- Poner las soluciones en GitHub con un README que explica el enfoque.
- Comentarios sobre preguntas de flujo de pila utilizando lógica similar.

-...

## Final Takeaway

*LeetCode 773* es un ejemplo de libro de texto de cómo una mentalidad algorítmica sólida, junto con código limpio y explicaciones agnósticas de lenguaje, puede convertir un rompecabezas en un punto de conversación listo para el trabajo.
Siéntase libre de utilizar los fragmentos proporcionados en su cartera, presentarlos en una entrevista, o adaptarlos a su curso de instrucciones de datos favoritos.

¡Feliz codificación y feliz entrevista! 🚀

-...

*Si desea inmersiones más profundas en cualquiera de las técnicas (por ejemplo, hash personalizado para mascarillas de bits, poda avanzada BFS), suelte un comentario a continuación o suscríbete para recibir notificado sobre nuevas entradas. *

-...

*Feliz resolución! *