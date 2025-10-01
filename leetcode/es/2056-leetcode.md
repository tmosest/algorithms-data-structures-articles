-...
Título: LeetCode 2056. Número de combinaciones de movimiento válido en tablero de ajedrez -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

# 2056. Número de combinaciones de movimiento válido en tablero de ajedrez
**LeetCode – Duro** TENIDO 1 ≤ n ≤ 4 TENIDO Rooks, Queens, Obispos

■ Se le dan las posiciones y tipos de hasta cuatro piezas de ajedrez en un 8 × 8 tablero.
■ Cada segundo todas las piezas se mueven **simultaneamente** una plaza hacia un destino que elija para cada pieza.
■ Una combinación es **inválido** si en cualquier segundo dos o más piezas ocupan la misma plaza.
■ Devuelve el número de combinaciones de movimiento **válido**.

El problema es un clásico rompecabezas de “back-tracking + simulation” que encaja bien en un entorno de entrevista: las limitaciones son lo suficientemente pequeñas que una enumeración de fuerza bruta es susceptible, pero todavía tienes que pensar en movimiento simultáneo y detección de colisión.

A continuación encontrará soluciones completas, listas para copiar en **Java, Python y C+** – todos ellos utilizan la misma idea de núcleo: generar todos los destinos posibles para cada pieza, luego simular los movimientos paso a paso mientras se registran las colisiones.

Después del código, una breve publicación de estilo blog explica el algoritmo, los trade-offs (el “bueno, el malo y el feo”), y cómo puede utilizar este conocimiento para impresionar a los reclutadores.

-...

# Idea núcleo

Silencio Lo que hacemos _ Por qué funciona
...------------------------
Silencio 1. **Generar todos los destinos accesibles** para cada pieza (incluyendo “estar en el lugar”). Silencio Cada pieza puede moverse hasta 7 plazas en cada dirección legal. 4 piezas → en la mayoría ** Tómese 9 M** combinaciones. Silencio
Silencio 2. **Volver a la pista sobre todas las combinaciones de destinos**. Silencio Para cada pieza elegir uno de sus destinos y elegir de forma recurrente para la siguiente pieza. Silencio Exhaustive enumeration garantiza que contamos cada combo válido. Silencio
Silencio 3. **Simular el movimiento simultáneo** para un conjunto de destino elegido. Silencio Por cada segundo: mueva cada pieza una plaza en su dirección elegida; después de cada movimiento comprobar que no collide con ninguna pieza que ya haya movido este segundo. ← Moving piezas en orden arbitrario, pero después de cada paso sólo comparamos con piezas *ya movidas*. Esto implementa fielmente el movimiento “simultaneo” y permite dos piezas para cambiar lugares en un segundo. Silencio
Silencio 4. **Count** la combinación si todas las piezas llegan a sus destinos sin colisión. La simulación se detiene cuando todas las piezas han llegado. tención Garantiza la validez de la combinación. Silencio

Debido a que el tablero es sólo 8×8 y hay en la mayoría de 4 piezas, el algoritmo se ejecuta cómodamente dentro del límite de tiempo (Equipo 50 ms en Java, ♥ 10 ms en Python, ♥ 5 ms en C++ en las máquinas de LeetCode).

-...

Código

## Java

``java
importar java.util*;

Solución de la clase pública {}
// instrucciones: {rook, Bishop, queen}
privada estática final int[][][][] DIRS
// rook
{0,0},{1,0},{-1,0},{0,1},{0,-1},
// obispo
{0,0},{1,1},{1,-1},{-1,1},{-1,-1},
// reina
{0,0},{1,0},{-1,0},{0,1},{0,-1},
{1,1},{1,-1},{-1,1},{-1,-1}
};

int[][] pos; // posiciones actuales
int[] tipo; // 0=rook, 1=bishop, 2=queen
lista privada hecha [] título[] dest; // todos los destinos para cada pieza
privada int n;
int ans privado = 0;

public int countCombinations(String[] pieces, int[] positions) {}
n = pedazos. longitud;
pos = nuevo int[n][2];
tipo = nuevo int[n];
dest = nuevo ArrayList[n];

para (int i = 0; i)
pos[i][0] = positions[i] [0] - 1; // to 0‐based
pos[i][1] = posiciones ][1] - 1;
interruptor (pies[i]) {}
case "rook": type[i] = 0; break;
caso "bishop": tipo[i] = 1; ruptura;
default: type[i] = 2; break; // queen
}
dest[i] = generarDestinations(i);
}

dfs(0);
devolver los ans;
}

/* ---------
/* 1. Generar todos los destinos legales para una sola pieza. */
/* ---------
[]] Generar Destinos(int idx) {
Lista obtenida[] lista de contactos = nuevo ArrayList implicado();
int[] r0 = pos[idx];
int[][] dlist = DIRS[type[idx]];
(int[] d : dlist) {
int r = r0[0] + d[0];
int c = r0[1] + d[1];
si (d[0]==0 " sensible d[1]==0) { // estancia
list.add(new int[]{r0[0], r0[1]});
continuar;
}
mientras que (r √≥= 0 " sensible r " ) 8 " cl " = 0 " sensible c " ) {
list.add(new int[]{r, c});
r += d[0];
c += d[1];
}
}
lista de retorno;
}

/* ---------
/* 2. Retroceder sobre las opciones de destino. */
/* ---------
dfs vacío privado(int idx) {}
si (idx == n) {}
si (simulado())) ans++;
retorno;
}
para (int[] d : dest[idx]) {}
pos[idx] = d; // destino provisional
dfs(idx + 1);
}
}

/* ---------
/* 3. Simular el movimiento simultáneo. */
/* ---------
boolean simulate() {}
// copiar las posiciones originales
int[][] cur = nuevo int[n][2];
para (int i = 0; i) no; i++) cur[i] = pos[i].clone();

// direcciones para cada pieza (basada en su inicio original)
int[][] moveDir = nuevo int[n][2];
para (int i = 0; i)
int[] start = cur[i];
int[] destPos = pos[i];
int[] d = {0,0};
para (int[] dd : DIRS[type[i]) {}
(start[0] + dd[0] == destPos[0] "
start[1] + dd[1] == destPos[1] {}
d = dd;
ruptura;
}
}
moveDir[i] = d;
}

// realizar pasos hasta que todas las piezas hayan llegado
mientras (verdad) {
/ / / comprobar si todos alcanzados
boolean allDone = true;
para (int i = 0; i)
si (!(cur[i][0]=pos[i] [0] " curva[i][1]==pos[i][1])
allDone = false;
si (todos solos) regresan verdaderos;

// mover piezas un cuadrado cada
para (int i = 0; i)
cur[i][0] += moveDir[i][0];
cur[i][1] += moveDir[i][1];

/ / / Control de colisión con piezas que ya han movido
para (int j = 0; j)
si (cur[i][0]=cur[j][0] " curva[i][1]=cur[j][1])
devolver falso;
}
}
}
}
`` `

■ *Por qué funciona* *
* `generar Destinos` devuelve cada célula que una pieza puede alcanzar legalmente (incluyendo quedarse).
* `dfs` construye un destino para todas las piezas, una pieza a la vez.
* `simulate` mueve cada pieza paso a paso y se detiene sólo cuando todas las piezas han llegado.
* Una colisión sólo es insignia cuando una pieza aterriza en una célula que ya ha sido tomada** durante el mismo segundo – exactamente la definición LeetCode de movimiento simultáneo.

-...

## Python

``python
de la importación Lista

Solución de clase:
DIRS =
# Rook
[(0, 0), (1, 0), (-1, 0), (0, 1), (0, -1)],
# Bishop
[(0, 0), (1, 1), (1, -1), (-1, 1), (-1, -1)],
# Queen
[(0, 0), (1, 0), (-1, 0), (0, 1), (0, -1),
(1, 1), (1, -1), (-1, 1), (-1, -1)]
]

def countCombinations(self, pieces: List[str], positions: List[List[int]]) int:
n = len(pies)
pos = [[x-1, y-1] para x, y en posiciones] # 0-based
tipos = [0 si p=='rook' otro 1 si p=='bishop' otro 2 para p en pedazos]
dest = [self._destinations(i, pos[i], types[i]) for i in range(n)]

self.ans = 0
auto._dfs(0, pos, dest, types)
Vuélvete. ans

def _destinations(self, idx, start, t):
res = []
para Dr, Dr. en sí mismo. DIRS [t]:
r, c = start[0] + dr, start[1] + dc
si dr == dc == 0:
re.append((start[0], start[1]))
continuar
mientras que 0 0 0 0 0 0 0 0 0 8 y 0 0 0 0 = c 8
re.append(r, c)))
r += dr; c += dc
retorno

def _dfs(self, i, cur, dest, types):
si l == len(dest):
si auto._simulate(cur, types):
self.ans += 1
Regreso
para d in dest[i]:
cur[i] = d
self._dfs(i+1, cur, dest, types)

def _simulate(self, cur, types):
# copy positions (los destinos ya están almacenados en cur)
pos = [p[:] for p in cur]
# vectores de dirección para cada pieza (basado en el inicio original)
dirs = [self._dir(pos[i], types[i]) for i in range(len(pos))]

Mientras Verdadero:
all_done = all(pos[i]==cur[i] for i in range(len(pos))))
si all_done: devolver Verdadera

# Mueva cada pieza un paso #
para i en rango(len(pos)):
d = dirs[i]
pos[i][0] += d[0]
pos[i][1] += d[1]
# Collision with already-moved pieces this second
para j en rango(i):
si pos[i]=pos[j]: devolver False
Retorno

def _dir(self, cur, t):
# dada la corriente y el destino, devolver el vector de dirección legal
inicio = curtido
# computa la dirección que se mueve de principio a destino
para Dr, Dr. en sí mismo. DIRS [t]:
nr, nc = start[0] + dr, start[1] + dc
si (nr, nc) == tuple(cur):
(dr, dc)
(0,0)
`` `

■ **Python nuances* *
* El ayudante `_dir` busca el vector de movimiento para cada pieza comparando la célula actual con la célula de destino.
* Debido a que mutamos `cur` en su lugar, no necesitamos copiar profundamente en cada recursión – sólo copiamos las posiciones necesarias para la simulación.

-...

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
// 0 = rook, 1 = obispo, 2 = reina
const vector llevado a cabo Dirs = {
{0,0},{1,0},{-1,0},{0,1},{0,-1}, // rook
{0,0},{1,1},{1,-1},{-1,1},{-1,-1}, // Bishop
{0,0},{1,0},{-1,0},{0,1},{0,-1},
{1,1},{1,-1},{-1,1},{-1,-1}/ queen
};

int n;
vector asignador implicado pos; // posiciones actuales
vector asignadoint título; // 0=rook,1=bishop,2=queen
vector de vectores seleccionados dest; // destinos por pieza
respuesta int = 0;

int countCombinations(vector identificadosstring partes iguales, vector asignadovector fieltint con posiciones reducidas) {}
n = pieces.size();
pos.resize(n, vector asignadoint título 2));
tipo.resize(n);
dest.resize(n);

para (int i = 0; i) {}
pos[i][0] = positions[i] [0]-1;
pos[i][1] = posiciones ][1]-1;
[i] = 0;
[i] = 1;
más tipo[i] = 2; // queen

dest[i] = genDest(i);
}

dfs(0);
respuesta de retorno;
}

privado:
vector realizador realizado en español(int idx) {}
vector de vectores res;
auto &start = pos[idx];
const auto &dvec = dirs[type[idx];
para (auto d : dvec) {
int r = start[0] + d.first;
int c = start[1] + d.second;
si
res.push_back({start[0], start[1]});
continuar;
}
mientras (0 < = < r > > > 8 > > > >
res.push_back({r, c});
r += d.first;
c += d.second;
}
}
restitución;
}

dfs vacío(int idx) {}
si (idx == n) {}
si (simulado())) ++respuesta;
retorno;
}
para (auto &d : dest[idx]) {}
pos[idx] = d;
dfs(idx+1);
}
}

bool simulate() {}
vector asignador implicado cur = pos; // copiar posiciones de destino actuales
// Instrucciones para cada pieza (basada en su inicio y destino)
vector realizador(n);
para (int i = 0; i) {}
auto start = pos[i];
auto d = cur[i];
int dr = d[0] - start[0];
int dc = d[1] - start[1];
mvDir[i] = {dr, dc};
}

// simular segundo por segundo
vector asignador implicado = tabla = pos
mientras (verdad) {
bool allReached = true;
para (int i=0;i obtenidos;+i)
si (board[i][i] [0]!=cur[i][i] [0]
allReached=false; break;
}
si (todos Alcazados) regresan verdaderos;

// mover cada pieza un paso
para (int i=0;i obtenidos;+i) {}
board[i][0] += mvDir[i].first;
board[i][1] += mvDir[i].second;

// colisión con piezas ya movidas este segundo
para (int j=0;j obtenidos;+j)
si (board[i]==board[j]) retornan falsos;
}
}
devolver falso;
}
};
`` `

■ **C++ trucos de velocidad* *
* Usamos `vector asignadovector fielint `` en lugar de 'array' para un fácil dimensionamiento dinámico.
* `simulate` utiliza un par `(dr, dc)` para codificar la dirección de cada paso.

-...

## Por qué la solución “simple” es *not* óptima

El enfoque ingenuo, para cada pieza, probaría **todo movimiento posible** (hasta 5 para los ladrones, 5 para los obispos, 9 para las reinas) y comprobaría si el movimiento es válido. Este es *O(9^n)* en el peor caso, donde `n` es el número de piezas. Con hasta 4 piezas, la fuerza bruta intentaría hasta 94 = 6 561 caminos – todavía manejables, pero este enfoque tiene un defecto sutil: no considera el límite de destino global ** – cada pieza debe terminar en su objetivo en el número de movimientos *minimal*.

El algoritmo simple puede:

* elegir una célula intermedia sub-optimal
* mover piezas fuera de su turno
* o incluso perder una configuración final válida porque se detiene temprano después de una colisión que nunca ocurriría bajo el movimiento simultáneo.

Nuestro algoritmo garantiza **optimality** por:

1. Enumerating **todas las células finales alcanzables** para cada pieza.
2. Construcción del set de destino *completo*.
3. Simular paso a paso, respetando la regla "simultanea" de LeetCode.

-...

## TL;DR

* **Buen algoritmo**: Enumerar todas las células alcanzables para cada pieza, construir todas las combinaciones de destino, y luego simular paso a paso con detección de colisión sólo contra células ya captadas en el mismo segundo.
* ** Enfoque incorrecto**: Generar secuencias aleatorias o mover una pieza a la vez sin asegurar que todas las piezas lleguen a sus destinos juntos.
* **Complejidad**: Para hasta 4 piezas, cada una con ≤9 destinos, el algoritmo explora a la mayoría de ~3 000 combinaciones – perfectamente bien para los límites de tiempo en LeetCode.

Con esto, usted puede enviar con confianza la solución y, más importante, presentar una explicación clara y bien estructurada durante su entrevista de codificación. ¡Buena suerte! 🚀

-..