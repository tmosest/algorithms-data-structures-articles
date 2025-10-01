-...
Título: LeetCode 1210. Movimientos mínimos para alcanzar el objetivo con rotaciones -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1210 – **Minimum se mueve a alcanzar el objetivo con las rotaciones* *
*El bueno, el malo y el feo - cómo romperlo en Java, Python & C++ *

-...

## 1. Recaptación de problemas

`` `
Entrada: int[][] grid // 0 = vacío, 1 = bloqueado
Producto: número mínimo de movimientos, o -1 si imposible
`` `

El “snake” es siempre dos células largas:

← Orientación Silencioso Las células ocupadas
Silencio...
TENIDO Horizontal TENIDO (r, c) y (r, c+1)
TENIDO Vertical TENIDO (r, c) y (r+1, c)

* Estado de inicio: **Horizontal** en la esquina superior izquierda → celdas (0,0) y (0,1).
* Estado de destino: **Horizontal** en la esquina inferior derecha → células (n-1, n-2) y (n-1, n-1).
* Un movimiento puede ser:

Silencio Silencio Silencio Silencio Silencio Silencio
Silencio--------------------
← Derecho Silencio Ambas células pueden cambiar a la derecha
Las células pueden cambiar la misma orientación
Silencio Clockwise tención Horizontal & las dos celdas debajo de él están vacías
Las dos celdas a su derecha están vacías.

" n " es en la mayoría de los 100, por lo que es factible un BFS exhaustivo en todos los estados.



-...

## 2. Why Breadth‐First Search (BFS)

* Cada estado (posición + orientación) tiene un costo fijo de 1 para llegar al siguiente estado.
* BFS garantiza que la primera vez que aparece el estado objetivo de la cola hemos utilizado el número mínimo de movimientos.
* El espacio estatal está vinculado: 'n × n × 2 ≤ 20 000` – trivial para el hardware moderno.



-...

## 3. Core BFS Idea (in plain English)

1. **Representar a un estado** como `(row, col, orientation)` donde `row, col` son las coordenadas de la célula *head* (la célula más alta o más izquierda).
2. Mantenga una matriz booleana 3-D `visited[n][n][2]` para evitar revisiting estados.
3. Comience con `(0, 0, 0)` – horizontal.
4. Mientras que la cola no está vacía:
* Pop a state, increase `steps`.
* Si es el objetivo, devuelve los pasos.
* Generar hasta cuatro nuevos estados mediante la aplicación de las cuatro reglas de movimiento; añadir las que son legales e invisitas a la cola.
5. Si la cola se vacía sin golpear el objetivo → devolver `-1`.



-...

## 4. Lista de verificación Edge‐Case

Silencio Chequeo confidencialidad Por qué importa
Silencio...
viv Moving right while **horizontal** – must verify cell `(r, c+2)` está dentro de la cuadrícula y vacía. Silencio
TENIDO Moving right while **vertical** – must verify both `(r, c+1)` and `(r+1, c+1)` are empty. Silencio
Silencio Rotación en sentido de reloj – necesidad ** ambas células debajo de la serpiente para estar vacías: `(r+1, c)` y `(r+1, c+1)`. Silencio
← Rotating contra-a la derecha de la serpiente: `(r, c+1)` y `(r+1, c+1)`. Silencio
Silencio Nunca se mueva fuera de la cuadrícula ( " r " 0 " , " 0 " , " , " c+1 " = n " ). Silencio
Silencio El objetivo en sí debe estar en celdas vacías – el problema lo garantiza, pero los controles defensivos ayudan a evitar errores ocultos. Silencio

-...

## 5. Aplicación

A continuación se presentan implementaciones idiomáticas limpias en **Java, Python y C+**.
Los tres siguen el mismo patrón BFS descrito anteriormente.

### 5.1 Java 17

``java
importar java.util*;

*
* LeetCode 1210 – Movimientos Mínimos para alcanzar Meta con Rotaciones
*/
Solución de la clase pública {}
HORIZ = 0, VERT = 1;
int[] DR = {0, 0}; // right, down for horizontal
int final estático privado [] DC = {1, 1};

mínimo público Moves(int[][] grid) {
int n = grid.length;
booleano[][][] visitado = nuevo booleano[n][n][2];
Queue Utilizar el Estado titular q = nuevo ArrayDeque corresponde();

// inicio: horizontal en (0,0)
[0][0] [HORIZ] = verdadero;
q.offer(new State(0, 0, HORIZ));

int steps = 0;
int targetR = n - 1, targetC = n - 2;

(!q.isEmpty()) {
int sz = q.size();
mientras (sz... 0) {
State cur = q.poll();
int r = cur.r, c = cur.c, ori = cur.ori;

si R " C = " Pasos de retorno C " oi == HORIZ);

--- 1. Muévete a la derecha
si (puedeMoveRight(grid, r, c, ori)) {}
Estado nxt = siguienteRight(r, c, ori);
[nxt.c] [nxt.ori] {}
[nxt.r][nxt.c][nxt.ori] = true;
q.offer(nxt);
}
}

--- 2. Muévete
si (puedeMoveDown(grid, r, c, ori)) {}
Estado nxt = siguienteDown(r, c, ori);
[nxt.c] [nxt.ori] {}
[nxt.r][nxt.c][nxt.ori] = true;
q.offer(nxt);
}
}

--- 3. Gire el reloj (H - título V)
si (ori == HORIZ " próteseClockwise(grid, r, c)) {
State nxt = new State(r, c, VERT);
si (!visited[nxt.r][nxt.c] [VERT]) {}
visitado[nxt.r][nxt.c] [VERT] = verdadero;
q.offer(nxt);
}
}

--- 4. Girar en sentido contrario (V - título) H)
si (ori == VERT " sensible canRotateCounter Clockwise (grid, r, c) {
Estado nxt = nuevo Estado(r, c, HORIZ);
si (!visited[nxt.r][nxt.c] [HORIZ]) {}
visitado[nxt.r][nxt.c] [HORIZ] = verdadero;
q.offer(nxt);
}
}
}
pasos++;
}
retorno -1; // imposible
}

--------- Métodos de ayuda para los cuatro tipos de movimiento-------- */

cantina booleana privadaMoveRight(int[] g, int r, int c, int ori) {}
int n = g.length;
si (ori == HORIZ) {
int nc = c + 2;
retorno nc 0;
} más { // vertical
(c + 1) == 0) "
(c + 1 ) == 0);
}
}

Estado privado siguienteRight(int r, int c, int ori) {}
si (ori == HORIZ) devuelve nuevo Estado(r, c + 1, HORIZ);
c + 1, VERT);
}

booleano privadoMoveDown(int[] g, int r, int c, int ori) {}
int n = g.length;
si (ori == VERT) {
int nr = r + 2;
devolver nr. 0;
} más { // horizontal
retorno (r + 1 י n ' t ' g[r + 1][c] == 0) "
(r + 1) == 0);
}
}

Estado privado siguienteDown(int r, int c, int ori) {}
si (ori == VERT) devuelve nuevo Estado(r + 1, c, VERT);
devolver nuevo Estado(r + 1, c, HORIZ);
}

booleano privadoRotateClockwise(int[] g, int r, int c) {
int n = g.length;
retorno (r + 1 < n) "
(g[r + 1][c] == 0 " , g[r + 1] [c + 1] == 0);
}

booleano privado canRotateCounterClockwise(int[] g, int r, int c) {
int n = g.length;
retorno (c + 1 < n) "
(g[r][c + 1] == 0 " , g [r + 1] [c + 1] == 0);
}

--------- Clase estatal...
Estado(int r, int c, int ori) {}
}
`` `

# El arnés de los mejores #

``java
Clase principal {}
public static void main(String[] args) {
int[][] grid = {
[0,0,0,0,1},
{1,1,0,0,1,0},
[0,0,0,1,1},
{0,0,1,0,0},
{0,1,0,0,0},
{0,1,0,0,0}
};
System.out.println(new Solution().minimumMoves(grid)); // → 11
}
}
`` `

-...

### 5.2 Python 3.10

``python
de las colecciones importa
de la importación Lista

Solución de clase:
HORIZ, VERT = 0, 1

mínimo Moves(self, grid: List[List[int]]) - int:
n = len(grid)
visitados = [[False]*2 para _ en rango(n)] para _ en rango(n)]
q = deque([(0, 0, self.HORIZ)]) # (row, col, orientation)

visitado[0][0][self. HORIZ] = Verdadero
pasos = 0
objetivo = (n-1, n-2, auto. HORIZ)

mientras q:
para _ en rango(len(q)):
r, c, o = q.popleft()
(r, c, o) == objetivo:
Pasos de retorno

# 1. Move right
si auto.can_move_right(grid, r, c, o):
nr, nc, no = self.next_right(r, c, o)
si no es visitado[nr][nc][no]:
visitado[nr][nc] [no] = Verdadero
q.append(nr, nc, no))

# 2. Muévete
si auto.can_move_down(grid, r, c, o):
nr, nc, no = self.next_down(r, c, o)
si no es visitado[nr][nc][no]:
visitado[nr][nc] [no] = Verdadero
q.append(nr, nc, no))

# 3. Girar el sentido del reloj (H → V)
si es uno mismo. HORIZ and self.can_rotate_cw(grid, r, c):
si no es visitado[r][c][self. VERT:
visitado[r][c][self. VERT = True
q.append(r, c, self.VERT))

# 4. Girar en sentido contrario (V → H)
o == uno mismo.VERT y uno mismo.can_rotate_ccw(grid, r, c):
si no es visitado[r][c][self. HORIZ:
visitado[r][c][self. HORIZ] = Verdadero
q.append(r, c, self. HORIZ)

pasos += 1
retorno -1

# ---------- helper methods --------
def can_move_right(self, g, r, c, o):
n = len(g)
si es uno mismo. HORIZ:
de vuelta c + 2 0
# vertical
(c + 1) == 0 y
c + 1  observado n y g[r + 1][c + 1] == 0)

def next_right(self, r, c, o):
si es uno mismo. HORIZ:
retorno r, c + 1, o
retorno r, c + 1, o

def can_move_down(self, g, r, c, o):
n = len(g)
si es uno mismo. VERT:
retorno r + 2  obtenidos n y g [r + 2] [c] == 0
# horizontal
retorno (r + 1  detectado n y g [r + 1] [c] == 0 y
r + 1  obtenidos n y g[r + 1][c + 1] == 0)

def next_down(self, r, c, o):
si es uno mismo. VERT:
retorno r + 1, c, o
retorno r + 1, c, o

def can_rotate_cw(self, g, r, c):
n = len(g)
volver r + 1 < n y c + 1
g[r + 1][c] == 0 y g[r + 1][c + 1] == 0

def can_rotate_ccw(self, g, r, c):
n = len(g)
volver r + 1 < n y c + 1
g[r][c + 1] == 0 y g[r + 1][c + 1] == 0
`` `

** Complejidad** – `O(n2) ` tiempo, `O(n2) espacio.



-...

### 5.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
mínimo Moves(vector identificadovector fielint círculo) {
const int n = grid.size();
const int H = 0, V = 1;
vector realizador realizador realizador seleccionadobool, 2 hilo conductor vis(n, vector seleccionadoarray madebool, 2 título(n, {false, false}));

queue efectuastetuple obtenidosint,int,int,int
q.emplace(0, 0, H);
[0][H] = verdadero;
int steps = 0;
const int tr = n - 1, tc = n - 2; // target bottom‐right of the block

(!q.empty()) {
int sz = q.size();
mientras (sz--) {
auto [r, c, o] = q.front(); q.pop();
si (r == tr ' pc == tc H) las medidas de retorno;

/* 1. Mover a la derecha */
si (puedeMoveRight(grid, r, c, o)) {
[nr, nc, no] = nextRight(r, c, o);
si (!vis[nr][nc] [no]
vis[nr][nc] [no] = true;
q.emplace(nr, nc, no);
}
}

/* 2. Muévete */
si (puedeMoveDown(grid, r, c, o)) {
[nr, nc, no] = nextDown(r, c, o);
si (!vis[nr][nc] [no]
vis[nr][nc] [no] = true;
q.emplace(nr, nc, no);
}
}

/* 3. Gire el reloj (H - título V) */
(o == H " puedeRotateCW(grid, r, c) {
si (!vis[r][c] [V]) {
vis[r][c] [V] = verdadero;
q.emplace(r, c, V);
}
}

/* 4. Girar en sentido contrario (V - título) H) */
si (o == V " próteseCCW(grid, r, c) {
si (!vis[r][c] [H]) {
vis[r][c] [H] = verdadero;
q.emplace(r, c, H);
}
}
}
++ pasos;
}
retorno -1;
}

privado:
const int H = 0, V = 1;

Los métodos de ayuda...
bool canMoveRight(cont vector identificadovector seleccionado) {}
int n = g.size();
si (o == H) { // horizontal
c + 2 == 0;
} // vertical
(c + 1 ) == 0 >
c + 1 י n ' t ' g[r + 1][c + 1] == 0);
}

tuplecto,int,intios siguienteRight(int r, int c, int o) {
c + 1, o};
}

bool canMoveDown(cont vector identificadovector seleccionado) {}
int n = g.size();
(o == V) { // vertical
retorno r + 2 0;
} // horizontal
retorno (r + 1 ■ n " sensible g[r + 1][c] == 0 "
r + 1 > > > > > 0);
}

tuple dedicada, int, int o) {
retorno {r + 1, c, o};
}

bool canRotateCW(cont vector asignadovector identificador seleccionado) {
int n = g.size();
retorno r + 1 י n ' t ' c + 1
g[r + 1][c] == 0 " , g[r + 1] [c + 1] == 0;
}

bool canRotateCCW(cont vector asignadovector identificador seleccionado) {
int n = g.size();
retorno r + 1 י n ' t ' c + 1
g[r][c + 1] == 0 " , g[r + 1] [c + 1] == 0;
}
};
`` `

**Usuario**

``cpp
int main() {}
vectorial realizador realizador fieltro red = {
[0,0,0,0,1},
{1,1,0,0,1,0},
[0,0,0,1,1},
{0,0,1,0,0},
{0,1,0,0,0},
{0,1,0,0,0}
};
cout se realizó Solution().minimumMoves(grid) se realizó '\n' // 11
}
`` `

-...

-...

## 6. Discusión – Partes “buenas / malas”

Aspecto permanente (Lo que hicimos bien)
Silencio----------------------------
Silencio **Explicit state** ¦ Represented by `(row, col, orientation)` – easy to hash ' visit. TENIDO Olvidar comprobar * ambas células después de una rotación. Silencio
Silencio **Move legality checks** Silencio Cada movimiento tiene un pequeño ayudante independiente – no hay lógica duplicada. ← Mezcla índices para movimientos horizontales vs. verticales. Silencio
Silencio **Procesamiento de capas BFS** ¦ Incremento `pasos` después de procesar una capa – garantiza la distancia correcta. Silencio Usando una sola cola y olvidando el bucle sobre el tamaño ()`. Silencio
Silencio ** Condiciones monetarias** Silencio Comprobaciones claras ( < r+1 > no > , < > > ) para evitar las salidas. ← Errores desactivados por uno en 'c+2' realizados n` o `r+2  interpretado n`.
tención **Espacio** Silencioso 2‐D visitado array *per* orientación → O(n2). Silencio Usar 'unordered_set' de tuples añadiría sobrecarga. Silencio

-...

## 7. Tomado para entrevistadores y candidatos

* El problema se reduce a la navegación **grid con una pieza deslizante/rotante**.
* Un BFS sobre un espacio estatal 3-D (`row × col × orientación`) lo resuelve en `O(n2)` tiempo.
* Preste atención a las condiciones de movimiento **four** – son la única sutileza.
* Evite errores índice: Compruebe siempre el índice **maximum** antes de acceder a la red.

-...

### 8. Veredicto final

Este es un clásico rompecabezas de entrevista que prueba:

1. ** Representación estatal** – modelando la orientación del bloque.
2. ** Manejo monetario** – evitando errores fuera por uno.
3. ** Pensamiento algorítmico** – BFS sobre un pequeño espacio estatal.

Una vez que escriba los cuatro cheques de ayudante, el resto es mecánico. Las tres implementaciones anteriores deben ser perfectas **5/5** en una típica entrevista de codificación.

¡Feliz codificación! 🚀

-...

**Keywords:** `grid navigation`, `sliding block`, `BFS`, `orientation`, `rotation`, `LeetCode`, `Dynamic Programming`, `C++`, `Python`, `Java`.