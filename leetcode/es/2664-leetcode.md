-...
Título: LeetCode 2664. El Tour del Caballero -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## The Knight's Tour on LeetCode #2664
*Bueno, malo y feo – Una guía de búsqueda de empleo*

-...

#### TL;DR

Silencio Idioma Silencio Complejidad Silencio
Silencio--------------------------
Silencio **Java** Silencio O(m·n) retroceso (caso inferior ♥ 120 000 caminos) Silencio Usos Tabla basada en 0, profundidad de recursión ≤ 25 Silencio
Silencio **Python** Usa tuples para posiciones, `itertools` no necesita  sometida
TENIDO **C+** TENIDO Mismo TENIDO Usos `vector asignadovector fielint and a global `moves` array ←

El tablero es en la mayoría de 5 × 5, por lo que una búsqueda exhaustiva de profundidad (DFS) es lo suficientemente rápida.
La clave es almacenar el orden de visitación en `board[r][c] y backtrack cuando se golpea un extremo muerto.

-...

## 1. Recaptación de problemas

Se le da una tabla de tamaño `m × n` (1 ≤ m, n ≤ 5) y una posición de inicio `(r, c)`.
Un caballero se mueve como en ajedrez: `(dr, dc)` es un par donde un componente es 2 y el otro es 1.
Su tarea es devolver una matriz donde cada célula contiene el número de paso en el que el caballero visitó esa plaza, comenzando en `0` para la célula inicial.
Se garantiza que exista un recorrido completo para los casos de prueba suministrados.

-...

## 2. Por qué Backtracking funciona aquí

- **Espacio Estado: ** `m · n` celdas, cada una visita exactamente una vez → a la mayoría de 25! caminos posibles (tiny para m,n ≤ 5).
- *La viabilidad* El problema garantiza una solución, para que podamos parar cuando encontremos el primer tour.
- *Determinismo* La salida es determinista una vez que decidimos el orden en el que intentamos movimientos.

Debido a que el tablero es pequeño, podemos ignorar heurísticas más avanzadas (regla de Warnsdorff) y aún terminar bien bajo 1 ms.
Sin embargo, añadir una simple orden de movimiento (Warnsdorff) acelera la búsqueda y demuestra buenas prácticas de entrevista de codificación.

-...

## 3. Resumen del algoritmo

1. **Definir** el 8 caballero se mueve.
2. **Crear** un array 2-D " inicializado con "-1 " para marcar células no visibles.
3. **DFS(posición, paso):**
- Marca la celda actual con "paso".
- Si `paso == m*n - 1`, terminamos → devolver `true`.
- Generar candidatos a las próximas celdas.
- *Opcional:* clasificar candidatos por el número de movimientos en marcha (Warnsdorff).
- Recupere a cada candidato.
- Si la recursión falla, retroceso: set `board[next]` volver a `-1`.
4. **Call** DFS comenzando desde `(r, c, 0)`.

-...

## 4. Análisis de la complejidad

- Hora:
En el peor de los casos visitamos cada nodo del árbol de recursión:
\(O(8^{m·n})\).
Para m,n ≤ 5 esto es trivial (≤ 8^25 Ω 3·10^22, pero la búsqueda es muy frecuente).
Prácticamente 1 ms en hardware moderno.

- ¿Qué?
- `board`: O(m·n).
- Recursión: O(m·n).
- No hay estructuras de datos extra grandes.

-...

## 5. Casos de borde

Silencio Caso confidencialidad ¿Por qué importa?
Silencio...
TENIDO 1 × 1 tablero TENIDO No se pueden hacer movimientos ANTE DFS inmediatamente devuelve el éxito
Silencio Plazas inalcanzables ( tablas redondas) Silencio Problema garantiza entrada solvable Silencio No es necesario realizar controles
tención Posición de inicio en la esquina Silencio Moves reducir Silencio Funciona fuera de la caja ←

-...

## 6. Aplicación del Código

A continuación se encuentran soluciones limpias, listas para entrevistas en **Java, Python, y C++**.
Los tres usan el mismo núcleo de retroceso.

### 6.1 Java

``java
importar java.util*;

Solución de la clase pública {}
dd = 2, 1, -1, -2, -2, -1, 1, 2};
privada static final int[] DC = {1, 2, 1, -1, -2, -2, -1};

int[][] tourOfKnight(int m, int n, int r, int c) {
int[][] board = new int[m][n];
for (int[] row : board) Arrays.fill(row, -1);
dfs(board, r, c, 0);
de retorno;
}

dfs booleanos privados(int[][] board, int r, int c, int step) {}
[r][c] = paso;
si (paso == tabla.length * tabla [0].length - 1) volver verdadero;

Lista hecha [] Movidas de contacto = nuevo ArrayList correctamente();
para (int k = 0; k)
int nr = r + DR[k], nc = c + DC[k];
si (nr не= 0 " sensible nr)
nc 0 < nc > > longitud "
board[nr][nc] == -1) {
moves.add(new int[]{nr, nc});
}
}

// Ordenación opcional de Warnsdorff
moves.sort(Comparator.comparingInt(a - título onwardCount(board, a[0], a[1]));

para (int[] mv : moves) {
si (dfs(board, mv[0], mv[1], paso + 1)) retornan verdadero;
}

board[r][c] = -1; // backtrack
devolver falso;
}

int privado int onwardCount(int[][] board, int r, int c) {
int cnt = 0;
para (int k = 0; k)
int nr = r + DR[k], nc = c + DC[k];
si (nr не= 0 " sensible nr)
nc 0 < nc > > longitud "
board[nr][nc] == -1) cnt++;
}
cnt de retorno;
}
}
`` `

### 6.2 Python

``python
Solución de clase:
movimientos = [(2, 1), (1, 2), (-1, 2), (-2, 1),
(-2, -1), (-1, -2), (1, -2), (2, -1)]

def tourOfKnight(self, m: int, n: int, r: int, c: int) - lista de contactos[list]:
tabla = [1] * n para _ en rango(m)]
autodfs(board, r, c, 0)
tabla de retorno

def dfs(self, board, r, c, step):
[r][c] = paso
si paso == len(board) * len(board[0]) - 1:
Retorno

candidatos =
para Dr, Dr. en sí mismo. movimientos:
nr, nc = r + dr, c + dc
[nc] == -1:
(nr, nc))

# Warnsdorff: ordenar por el número de movimientos en marcha
candidatos.sort(key=lambda pos: self.onward(board, *pos))

para nr, nc en candidatos:
si auto.dfs(board, nr, nc, step + 1):
Retorno

board[r][c] = -1 # backtrack
Retorno Falso

def hacia adelante(self, board, r, c):
Conteo = 0
para Dr, Dr. en sí mismo. movimientos:
nr, nc = r + dr, c + dc
[nc] == -1:
Cuenta += 1
cuenta de retorno
`` `

### 6.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
const int dr[8] = {2,1,-1,-2,-2,-1,1,2};
const int dc[8] = {1,2,2,1,-1,-2,-2,-1};

vector seleccionado, int r, int c)
vector seleccionado(n, -1));
dfs(board, r, c, 0);
de retorno;
}

privado:
bool dfs(vector realizador identificadovector fielmente limitado junta, int r, int c, int step) {}
[r][c] = paso;
si (step == board.size() * board[0].size() - 1) retornar verdadero;

vector realizado, se mueven intrínsecos, intrínsecos.
para (int k=0;k obtenidos8;k+){
int nr=r+dr[k], nc=c+dc[k];
si (nr título=0 " sensiblen(int)board.size() "
nc]=0 " sensible(int)board[0].size() "
board[nr][nc]==-1)
moves.push_back({nr,nc});
}

// Heurística Warnsdorff
(moves.begin(), moves.end(),
[Contiguo](contiguo par observadoint,int estrecho contacto a, const pair observadoint,intющ b) {}
volver a bordo (a., primero, segundo)
a bordo (b.first,b.second);
});

(auto [nr,nc]: moves) {
si (dfs(board,nr,nc,step+1)) retornan verdadero;
}
board[r][c] = -1; // backtrack
devolver falso;
}

int onward(cont vectorial identificadovector identificadoint
int cnt=0;
para (int k=0;k obtenidos8;k+){
int nr=r+dr[k], nc=c+dc[k];
si (nr título=0 " sensiblen(int)board.size() "
nc]=0 " sensible(int)board[0].size() "
board[nr][nc]=-1) cnt++;
}
cnt de retorno;
}
};
`` `

-...

## 7. Blog‐Style Exposition: “El viaje del caballero – bueno, malo y feo”

### 7.1 Good – Why Este problema es un Gold‐Mine para los entrevistadores

1. **Shows Mastery of DFS " Backtracking**
El Tour del Caballero es un problema DFS clásico que comprueba si el candidato puede manejar la profundidad de recursión, poda y restauración estatal.
2. **Encoura el pensamiento algorítmico* *
Los candidatos necesitan razonar sobre un espacio de búsqueda combinatorial, decidir sobre el orden de movimiento y gestionar los estados visitados.
3. **Constraints Espaciales Fit LeetCode’s “Medium” Category* *
Con `m, n ≤ 5`, fuerza bruta es aceptable, pero sigue siendo un rompecabezas sutil, bueno para distinguir los pensadores rápidos.

## 7.2 Malo – Los candidatos a saltos comunes

Silencio Pitfall Silencio Por qué Es malo vivir Cómo arreglar
Silencio----------------------------
Silencio **Storing visited in a 1‐D array** Silencio Hard to map coordinates → off‐by-one errors tención Use a 2‐D matriz o bitmask with `(r * n + c)` Silencio
Silencio **No backtracking** Silencio Leaves the board in a half-filled state → respuesta incorrecta Silencio Después de la recursión, reset cell to `-1` Silencio
Silencio **Missing base case** ← Recursion nunca termina → apilar el desbordamiento  Check `step == m*n - 1`
Silencio **Utilizar el estado mutable global sin reiniciar** Silencio Llamadas subsiguientes reutilizar la misma tabla ← Reinicializar la tabla en cada método público

## 7.3 Ugly – Why It Can Spiral Out of Control

1. * Generación de movimiento sin orden*
Sin Warnsdorff o cualquier poda, la búsqueda explora muchos extremos muertos, especialmente en 5 × 5 tableros.
2. **Profundidad de recuperación en otros idiomas* *
En lenguajes como Python, la profundidad de recursión predetermina a 1000, pero para una junta de 25 celdas está bien; todavía, siempre establecer un guardia si planea extender.
3. **Ignorando la garantía de una solución**
Algunos candidatos escriben solucionadores genéricos de Hamiltonian-Path que manejan cualquier tamaño de la junta — sobrematar para este problema.

## 7.4 Consejos para Nail‐Down Your Solution

- **Iniciar siempre la junta a `-1`** (sin consultar).
- Usa los 8 movimientos proporcionados no hay números mágicos.
- **Apply Warnsdorff** (opcional) - se mueve hacia adelante-move cuenta para reducir la ramificación.
- **Test edge cases**: 1 × 1, empezando en el centro, comenzando en una esquina.

-...

## 8. Palabras finales para el Contratista

Si usted está contratando un ingeniero de software, presentar el Tour del Caballero en una sesión de entrevista es una señal fuerte de la madurez algorítmica de un candidato**.
Las soluciones anteriores demuestran el enfoque limpio y de producción que la mayoría de los reclutadores aprecian.
Y para los buscadores de empleo: una implementación sólida aquí te gana un “sí” y un impulso rápido de confianza para tu próxima ronda de codificación.

-...

### 9. Referencias " Lectura ulterior "

- [LeetCode 1231. Knights Tour (hard)](https://leetcode.com/problems/knights-tour/)
- [Warnsdorff's Rule – Wikipedia](https://en.wikipedia.org/wiki/Warnsdorff%27s_rule)
- [Backtracking Primer - Cracking the Coding Interview](https://www.crackingthecodinginterview.com/)

-...

*Este post combina el rigor algoritmo con las ideas de estrategia de entrevistas—perfecto para ambos candidatos agudizar sus habilidades y reclutadores refinando sus criterios de evaluación. *