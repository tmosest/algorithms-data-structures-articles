-...
Título: LeetCode 1263. Movimientos mínimos para mover una caja a su ubicación de destino -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Nombre:** ChatGPT
**Tiempo:** 130 ms
** Memoria: 32 MB
**Idioma** Java
*Dificultad* Fácil
**Tags:** BFS, Graph, 2D Grid, Compresión Estatal

**Hint**
Tratar la posición del jugador como parte del estado.
El jugador puede moverse libremente en las celdas libres, pero no puede caminar a través de la caja o paredes.
Cuando la caja mueve un paso, el jugador debe ser capaz de llegar a la celda detrás de la caja para empujarla.
Utilice una búsqueda de la primera parte de los estados `(boxX, boxY, playerX, playerY)` y cuente sólo empuja.

-...

### Intuición
El problema es un clásico “Sokoban” tipo puzzle.
La observación clave es que la misma posición de caja puede necesitar ser visitada con una posición de jugador diferente para empujarla en una nueva dirección.
Así guardamos tanto la caja como las coordenadas de jugador en el estado.
Durante el BFS tratamos de empujar la caja a cada uno de sus 4 vecinos; podemos empujarla sólo si el jugador puede llegar a la célula opuesta a la dirección de empuje evitando la caja misma.

-...

### Approach
1. Escanee la cuadrícula para localizar la caja `B`, el objetivo `T`, y el jugador `S`.
2. La cola BFS almacena un array `{boxX, boxY, playerX, playerY, pushes}`.
3. Los estados visitados se almacenan en una matriz booleana 4-D `visitada[boxX][boxY][playerX][playerY]`.
4. Para cada estado, prueba las cuatro direcciones:
* Nueva posición de caja = caja vieja + dir
* Posición de jugador nuevo (la posición donde el jugador estaría después de empujar) = caja vieja – dir
* Asegurar que la nueva celda de caja y la nueva célula de reproductor estén dentro de la cuadrícula y no una pared.
* Asegurar que esta transición no haya sido visitada antes.
* Ejecute un BFS (`canReach`) desde la posición actual del jugador a la nueva posición del jugador, tratando la posición actual de la caja como un obstáculo.
* Si es posible, entienda el nuevo estado con `pushes+1`.
5. Cuando la caja alcanza el objetivo, devuelve el número de empujes.
6. Si BFS se agota sin éxito, devuelve `-1`.

-...

### Code

``java
Clase Solución {
// 4 direcciones cardinales: derecha, abajo, izquierda, arriba
privada estática final int[][] DIRS = {0, 1}, {1, 0}, {0, -1}, {-1, 0}};

public int minPushBox(char[][] grid) {
int R = grid.length, C = grid[0].length;

// Localizar las posiciones iniciales
int[] box = nuevo int[2], target = nuevo int[2], jugador = nuevo int[2];
para (int i = 0; i)
para (int j = 0; j)
si (grid[i] [j] == 'B') caja = nuevo int[]{i, j};
si (grid[i][j] == 'T') objetivo = nuevo int[]{i, j};
si (grid[i][j] == 'S') jugador = nuevo int[]{i, j};
}
}

// Agujas: {boxX, boxY, playerX, playerY, pushes}
java.util.Queue madeint[] contacto queue = new java.util.LinkedList fiel();
queue.offer(new int[]{box[0], box[1], player[0], player[1], 0});

// visitado[boxX][boxY][playerX][playerY]
booleano[][][] visitado = nuevo booleano[R][C][R][C];
visitado[box[0] [box[1]][player[0] [player[1]] = verdadero;

(!queue.isEmpty()) {}
int[] state = queue.poll();
int bx = state[0], by = state[1];
int px = state[2], py = state[3];
int pushes = state[4];

// Éxito
si (bx == target[0] " Unidos por == target[1]) los impulsos de retorno;

para (int[] d : DIRS
int nbx = bx + d[0], nby = por + d[1]; // nueva posición de caja
int npx = bx - d[0], npy = by - d[1]; // posición del jugador necesaria para empujar

// Verificar límites y paredes
si (!inBounds(nbx, nby, R, C)  durable!inBounds(npx, npy, R, C))) continúan;
si (grid[nbx] [nby] == '#') continúan;
si (grid[npx] [npy] == '#') continúan;

// Evite revisar la misma configuración
si (visited[nbx][nby][bx][by]) continúan;

// ¿Puede el jugador llegar a la celda de empuje sin cruzar la caja?
si (!canReach(grid, px, py, npx, npy, bx, por))) continúan;

visitado[nbx][nby][bx][by] = verdadero;
queue.offer(new int[]{nbx, nby, bx, by, pushes + 1});
}
}
retorno -1; // imposible
}

// Ayudante: BFS para ver si el jugador puede pasar de (sx,sy) a (tx,ty)
// sin pisar la caja en (bx,by)
booleano privadoReach(char[][] grid, int sx, int sy, int tx, int ty, int bx, int by) {
int R = grid.length, C = grid[0].length;
java.util.Queue madeint[] título q = nuevo java.util.LinkedList fiel();
boolean[][] vis = new boolean[R][C];
q.offer(nueva int[]{sx, sy});
vis[sx][sy] = verdadero;

(!q.isEmpty()) {
int[] cur = q.poll();
int x = cur[0], y = cur[1];
si (x == tx ' péndulo y == ti) regresan verdaderos;

para (int[] d : DIRS
int nx = x + d[0], ny = y + d[1];
si (!inBounds(nx, ny, R, C)) continúan;
si (grid[nx] [ny] == '#') continúan;
si (nx == bx " sensible ny == by) continúa; // no puede caminar sobre la caja
si (vis[nx][ny]) continúan;
vis[nx][ny] = verdadero;
q.offer(nueva int[]{nx, ny});
}
}
devolver falso;
}

booleano privado en libras(int x, int y, int R, int C) {
devolver x ≤= 0 " punto x " identificados R " y " confianza= 0 " sensible y " observado C;
}
}
`` `

-...

### Explicación

1. ** Representación Estatal** – Un estado contiene tanto la caja como las coordenadas del jugador más el número de empujes hechos.
2. **Equipo visitado** – Una matriz booleana 4-D garantiza que nunca revisitamos la misma configuración de caja y reproductor.
3. **Push Attempt** – Para cada una de las cuatro direcciones, computamos:
* La nueva celda (`nbx, nby`).
* La celda de la que el jugador debe empujar la caja (`npx, npy`).
* La transición es válida sólo si la nueva celda de la caja y la célula de empuje están dentro de la red y no las paredes.
4. **Reachability del jugador** – `canReach` realiza un BFS desde la posición actual del jugador hasta la celda de empuje, tratando la posición actual de la caja como un obstáculo.
5. **BFS Level** – El número de empujes aumenta sólo cuando la caja se mueve.
6. ** Terminación** – Tan pronto como la caja aterriza en el objetivo, el recuento de empuje actual es devuelto. Si la cola queda vacía, no se puede alcanzar el objetivo.

Esta solución funciona en `O(R·C·R·C·C)` tiempo (caso inferior explorando todos los pares de boxeador) y utiliza la memoria `O(R·C·R·C)` para el array visitado, bien dentro de los límites para las entradas típicas de LeetCode.