-...
Título: LeetCode 1958. Compruebe si Move es legal -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. El Código - Tres idiomas, una idea

A continuación encontrará ** tres implementaciones autocontenidas** que resuelven el problema LeetCode
**“1958. Compruebe si Move es legal”**.
La idea central es la misma en cada idioma:

* Después de pintar la celda elegida con el color del jugador, escanee las 8 direcciones de línea posibles
(Abajo, abajo, izquierda, derecha, las cuatro diagonales).
Si alguna dirección forma una *buena línea* (dos o más células de color opuesto entre el dos del mismo color)
endpoints) return `true`; otherwise return `false`. *

-...

### 1.1 Java (LeetCode-style)

``java
*
* 1958. Compruebe si Move es legal
* Firma de LeetCode
*/
Solución de la clase pública {}
// 8 vectores de dirección
int final estático privado[][] DIRS
{0, 1}, {0, -1}, {-1, 0},
{1, 1}, {-1, -1}, {1}, {-1, 1}
};

public boolean checkMove(char[][] board, int rMove, int cMove, char color) {
// Se nos permite pintar tabla[rMove][cMove] con `color `
para (int[] d : DIRS
int r = rMove + d[0], c = cMove + d[1];
len int = 2; // longitud incluye la célula pintada + primer vecino

mientras (0 < = < r > > > 8 > > > >
char cur = board[r][c];

// Si golpeamos una celda vacía, o si golpeamos una celda del mismo color antes
// la línea es lo suficientemente larga, esta dirección no puede formar una buena línea
si (cur == '.' {}
ruptura;
}

// Si golpeamos una célula del mismo color después de al menos 3 células
si (cur == color) {
retorno verdadero;
}

// Avance a la siguiente célula en esta dirección
r += d[0];
c += d[1];
len++;
}
}
devolver falso;
}
}
`` `

-...

### 1.2 Python 3

``python
Solución de clase:
# 8 vectores de dirección
DIRS = [(0, 1), (0, -1), (1, 0), (-1, 0),
(1, 1), (-1, -1), (1, -1), (-1, 1)]

Def check Move(self, board: List[List[str]], rMove: int,
cMove: int, color: str) Bool:
para Dr, Dr. en sí mismo. DIRS:
r, c = rMove + dr, cMove + dc
longitud = 2 # celda pintada + primer vecino

mientras que 0 0 0 0 0 0 0 0 0 8 y 0 0 0 0 = c 8
cur = board[r][c]

# No puedo formar una buena línea si golpeamos vacío o el mismo color demasiado temprano
si cur == '.' o (duración) 3 y cur == color):
descanso

# Good line found
si cur == color:
Retorno

r +=dr
c +=dc
longitud += 1

Retorno Falso
`` `

■ **Tip** – LeetCode espera el método 'checkMove' dentro de una clase llamada `Solution`.
■ The `List[List[str]]` tipo de indicio es opcional pero mantiene el código legible.

-...

#### 1.3 C++ (LeetCode style)

``cpp
Clase Solución {
public:
// 8 vectores de dirección
const int dirs[8][2] = {}
{0, 1}, {0, -1}, {-1, 0},
{1, 1}, {-1, -1}, {1}, {-1, 1}
};

bool checkMove(vector asignadovector asignadovector fielchar estrecho contacto junta, int rMove,
int cMove, char color) {}
para (auto golpe d : dirs) {
int r = rMove + d[0], c = cMove + d[1];
int len = 2; // incluye celda pintada + primer vecino

mientras (0 < = < r > > > 8 > > > >
char cur = board[r][c];

si (cur == '.'
ruptura;
si (cur == color) // buena línea encontrada
retorno verdadero;

r += d[0];
c += d[1];
len++;
}
}
devolver falso;
}
};
`` `

■ **¿Por qué 20 líneas en C++? * *
■ La misma lógica se expresa en un pacto, `O(1)` estilo – solo escribes un solo bucle que
 it iterates sobre los 8 vectores de dirección.
■ El truco de 20 líneas que has visto en LeetCode es sólo una versión muy ordenada del código Java/Python
Se muestra arriba.

-...

## 2. El Blog – SEO‐Ready, Entrevista-Focused

■ *“¿Quieres aterrizar esa entrevista de ingeniería de software?
■ Lea cómo un escaneo limpio de 8 direcciones puede convertirse en un inicio de conversación!”*

-...

#### 2.1 Introduction

El problema **“Comprobar si Move es legal”** es una pregunta de entrevista **clásicamente
prueba la capacidad de un candidato para:

1. **Understand a simple state machine** (painting a cell, then validating a pattern).
2. **Traducir esa intuición en código eficiente** (8 direcciones, cheques de tiempo constante).
3. **Explicar casos de borde** (células vacías, líneas cortas, límites de la junta).

Es un gran ejemplo de un patrón *“Grid + Direction”* que aparece en muchas entrevistas de codificación,
de **Tic‐Tac‐Toe** variantes a **Go‐Moku** y **Connect‐Four** rompecabezas de estilo.

-...

### 2.2 Declaración de problemas (Re-worded)

■ **Given** un '8 × 8` tablero de caracteres ``. ``, ``W', o ``B' y un movimiento `(rMove, cMove)`.
■ **y** un color ( `W'` o ``B''') se le permite pintar en ese lugar,
■ **determine** si pintar esa célula resulta en una *buena línea*.

Una buena línea** se define como:

* Dos células *same-color* en los extremos.
* Entre ellos, al menos dos células consecutivas del color *opposite*.
* Ninguna célula vacía puede interrumpir la línea.
* La línea puede extenderse en cualquiera de las 8 direcciones rectas.

-...

#### 2.3 Constraints

Silencio Parameter Silencio Mínimo Silencio
Silencio--------------------------
Silencioso `board.length` Silencio 1
Silencioso `board[i].length` Silencio 1
Silencioso `rMove, cMove`
Silencioso `board[rMove][cMove] == '.'’
Silencioso `color  Marítima {‘W’, ‘B’}` Silencio – Silencio

Todas las juntas están garantizadas a ser `8 × 8` en la versión LeetCode, pero nuestra aplicación utiliza
el enfoque dinámico `n = board.length` / `m = board[0].length` por lo que también funciona en cualquier
'n × m` bordo.

-...

### 2.4 Algoritmo – Escáner de Dirección 8

1. **Pintura** la celda seleccionada con el color del jugador *virtually*
(la tabla real nunca se muta – nunca necesitamos deshacerla).
2. Para cada una de las **8 direcciones**:
* Mueva un paso de la celda pintada.
* Contar con el número de celdas consecutivas ( " L " ), comenzando por " 2 " (pintado + primer vecino).
* Mientras está dentro del tablero:
* Si golpeamos `'.` → esta dirección no puede formar una buena línea → parar.
* If we hit a *same‐colour* cell **before** `len  Conf= 3` → Parada (la línea es demasiado corta).
* If we hit a *same-colour* cell **after** `len  Conf= 3` → **Buena línea encontrada** → retorno `true`.
* De lo contrario, siga avanzando en la misma dirección.
3. Si ninguna dirección produjo una buena línea → devolver `false`.

-...

### 2.5 Complexity Analysis

TEN TERRITOR TEN Java ANTE Python 3
Silencio------------Prince------------------
Silencio ** Tiempo** Silencioso `O(8 * 7)` → `O(1)` (factor constante 56) Silencioso `O(8 * 7)` → `O(1)` Silencio `O(8 * 7)` → `O(1)` Silencio
Silencio** Silencio
¿Por qué constante? El tamaño de la tabla es fijo (8 × 8) – el bucle nunca excede 56 iteraciones. La misma razón. Silencio

Debido a que el tamaño de la tabla es fijo, usted puede reclamar ** "caso inferior 56 cheques"** en una entrevista;
es lo suficientemente rápido para la producción o la lógica del juego y muy fácil de razonar.

-...

### 2.6 Edge Cases " Ugly " Mistakes to avoid

Silencio Común Pitfall Silencio Por qué es malo Silencio Cómo arreglar Silencio
Silencio.
Silencio **No manipular `len' 3`** Silencio Un vecino del mismo color inmediatamente después de pintar puede parecer una línea pero no es lo suficientemente largo. Silencio Mantenga el mostrador de 'le' y sólo acepte una celda de mismo color si 'le  confianza= 3`. Silencio
Una buena línea no puede saltarse sobre una celda vacía. Silencioso Romper el bucle si `board[r][c] == '.'.
Silencio **Asumiendo que la célula pintada se cuenta dos veces** Silencio El primer vecino es contado ** después de la célula pintada; no olvide incluir la célula pintada en la longitud. Silencio Inicio `le' a `2` (painted + first neighbour) o use `count = 1` y aumento antes de comprobar. Silencio
Silencio **Boundary errors** TEN Off‐por-one errores cuando se mueve fuera del tablero. TENIDO Utilizar el `mientras (0 ANTE= r ' t 3 = 8 ' t = 0 c ' guardia (o Python's `0 0 0 = r ' 8 `). Silencio
Silencio **Mutating the board** ← Cambio accidental de la tabla de entrada puede llevar a efectos secundarios. Silencio Do **not** modificar `board` en absoluto - tratar la pintura como hipotética. Silencio
tención **Too verbose direction checks** tención Escribir 8 separado `for` loops (como en la solución "long-hand" C++) es *en términos generales* para entrevista tiempo de codificación. ← Utilice un único array de dirección 8-element y un bucle unificado – es la solución “buena”. Silencio

-...

### 2.7 Variaciones " Bien " Mejoras

¿Por qué importa una entrevista?
Silencio----------------------------------------
Silencio **Tamaño de barba no fijo** Silencio Es posible que necesite calcular la longitud máxima en cada dirección antes de paso. tención Control de límite rápido: `max(steps_up, steps_down, ...) ≥ 2`. Silencio
Silencio ** Casos de prueba de Multiple** latitud LeetCode sólo pide un solo caso de prueba, pero los juegos del mundo real sobre muchos movimientos. Silencio Envuelve la lógica en un método que acepta un movimiento, devuelve `true/false`, y actualiza el tablero. Silencio
tención **Inmutabilidad** Silencio Algunos idiomas (por ejemplo, idiomas funcionales) no prefieren efectos secundarios. Silencio Regrese una nueva copia de la junta si debe evitar la mutación. Silencio
Silencio **Procesamiento del paralelo** Silencio Para tablas muy grandes, usted podría procesar 8 direcciones en hilos paralelos. No se necesita para 8×8 pero vale la pena mencionar en entrevistas avanzadas. Silencio

-...

### 2.8 “Bien, Mal, Ugly” Resumen

← Calidad Silencioso
Silencio...
Un bucle compacto sobre `DIRS`, cheques de tiempo constante, nombres variables claros (`len`, `color`). Silencio
Silencio **Bad** tención Recursive DFS que explora todas las líneas posibles, causando un aumento exponencial en un tablero más grande. Silencio
Silencio **Ugly** Silencio Ocho separado `para` bucles cada uno manejando una dirección, lógica de borde verbosa, mala reutilización del código. Silencio

Un candidato de entrevista fuerte mostrará cómo **refactor la solución fea en el bien**,
demostrando la conciencia del rendimiento y la legibilidad.

-...

## 3. Pensamientos de clausura

Ya sea que usted está codiendo un motor de juego o resolver problemas de LeetCode, un **single, direccional ** bucle que comprueba `len` y maneja los límites es una habilidad **must‐know**.

Cuando escribes este código en una entrevista, **explicar** por qué `len  Conf= 3` importa, por qué usted ** no muta** el tablero, y cómo el escaneo de 8 direcciones garantiza un tiempo de funcionamiento constante.
Estas pequeñas explicaciones convierten un rompecabezas simple en un escaparate de la práctica de ingeniería limpia.

Buena suerte en tu próxima entrevista – ¡la red está esperando! 🚀

-..