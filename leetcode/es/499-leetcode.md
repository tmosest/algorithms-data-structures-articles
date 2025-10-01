-...
Título: LeetCode 499. El laberinto III -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

## 🎯 LeetCode 499 – El laberinto III
## From a “Hard” problem to a *job-ready* interview story
*(Java fort Python Silencio C++)*

-...

## Tabla de contenidos
1. [Problema Recap](#problema-recap)
2. [Por qué este problema importa para su entrevista](#why-it-matters)
3. [El "Bueno, el Mal, el Ugly" de la solución] (#bueno-bad-ugly)
4. [Aprobación " Algoritm](#approach)
5. [Análisis de complejidad](#complejidad)
6. [Code Walk‐through](#code)
- Java
Python
- C++
7. [Edge‐Case Gotchas](#gotchas)
8. [Cómo hablar de esto en una entrevista](#talk)
9. [Palabras clave amigables con SEO](#seo)

-...

"Problema-recap"
## 1. Recaptación de problemas

Dado un laberinto rectangular de `0`s (vacío) y `1`s (muros), una bola que se roda en cuatro direcciones cardinales, y un agujero, encontrar la secuencia *cortada* de movimientos que permite que la bola caiga en el agujero.
Si varias secuencias tienen la misma distancia, devuelve el más pequeño léxico.
Si es imposible, devuelve `'imposible'.

■ *Las reglas clave*
* La bola roda hasta que golpea una pared.
* La pelota para antes de la pared.
* La pelota puede elegir una dirección diferente en cada parada.
• Rolling on the hole stops the ball immediately.

-...

■ un nombre= "why-it-matters"
## 2. Por qué este problema importa para su entrevista

- ** Búsqueda de Gráficos + cola de prioridad** – Dijkstra es un pilar de muchas preguntas de entrevista.
- ** Ordenación lexicográfica** – Muchas empresas prueban su capacidad para manejar los rompe corbatas.
- Reconstrucción de patas... Muestra que sabes cómo seguir las acciones.
- Maneje por caso... El laberinto puede contener células no alcanzables o el agujero podría estar adyacente a la bola.

Demostrando una solución Dijkstra limpia con demostraciones de ruptura de corbatas puede resolver problemas *hard* de manera eficiente.

-...

Identificar un nombre= "buen-bad-ugly"
## 3. El Bien, el Mal, el Ugly

Silencio Silencio
Silencio------------Prince------
Silencio ** Algorithm** Silencio Optimal: Dijkstra garantiza la distancia más corta ← Requiere una cola de prioridad – la implementación de la complejidad O(m·n·log(m·n)); para 100×100 es fino pero puede ser sobre-matizado para BFS más simples
Silencio **Tie‐breaking** Silencio Prioridad Lexicográfica usando la comparación de cadenas Silencio La concatenación String puede ser costosa en algunos idiomas que las cuerdas de Sendero pueden crecer grandes; evitar `+` en bucles estrechos (uso StringBuilder / lista) Silencio
Silencio **Espacio del Estado** Silencio Sólo hay que almacenar la posición, la distancia y el camino TENIDO El cheque es por posición, no por dirección Silencio Si la pelota nunca se detiene en el agujero hasta que golpea una pared, es posible que vuelva a visualizar una célula con un mejor camino, llevando a errores sutiles Silencio
Silencio **Estilo de codificación** Silencio Separación limpia: `Estado `, `getNeighbors`, `isValid` Silencio Demasiados métodos de ayuda pueden ocultar la lógica Silencio Sobrely verbose code for small changes can obfuscate the core idea tención
Silencio **Testing** Silencio Fácil de probar con los laberintos pequeños ← Duro de construir todos los casos de borde (agujero dentro de un túnel, paredes en las fronteras) Silencio Failing para tener en cuenta que la bola cae en el agujero *mid-roll* resulta en respuesta incorrecta ←

-...

"Nombre" = "aproximación"
## 4. Enfoque " Algoritm "

1. *Modelo de cada estado*
`row, col, dist, pathString` – la parada actual de la bola y el camino que condujo allí.

2. **Use Dijkstra (priority queue)* *
* Prioridad: primero por `dist`, luego por `pathString` (léxicográficamente).
* Debido a que la distancia aumenta estrictamente a medida que los rollos de bola, la primera vez que aparecen el agujero de la cola tenemos la respuesta óptima.

3. **Los vecinos genéricos**
Por cada una de las cuatro direcciones (`l`, `u`, `r`, `d`), rodar hasta una pared o el agujero.
* Mantenga un contador de cuántas células vacías fueron atravesadas.
* Deténgase temprano si se alcanza el agujero – la bola cae inmediatamente.

4. # Corriendo #
* Mantener un booleano 2-D visto[row][col].
* Cuando una célula es picada por primera vez, se garantiza que sea el camino más corto a esa celda (gracias a Dijkstra).
* Si la célula ya se ve, salta el procesamiento de sus vecinos.

5. Retorno**
* Si el agujero está picado: devuelve la cadena de ruta almacenada.
* Si la cola se vacía: devolver `imposible'.

-...

"Nombre="complejidad"
## 5. Análisis de la complejidad

Que `m × n` sea el tamaño del laberinto.

* **Time**:
Cada célula se puede insertar en la cola de prioridad al máximo (primera visita).
Cada inserción o eliminación cuesta `O(log(mn))'.
Para cada celda examinamos 4 direcciones, cada rollo es `O(k)`. donde `k` es distancia a la pared - amortizado sobre el laberinto esto está atado por `O(mn)`.
**Total**: `O(mn log(mn))`.

****Space**:
Carácter prioritario: `O(mn)` estados.
array visitado: `O(mn)`.
Cadenas de ruta: cada estado almacena una cadena de caracteres más 'mn' en el peor de los casos, pero sólo algunos estados alcanzarán esa longitud.
**Total**: `O(mn)`.

-...

Identificar un nombre="código"
## 6. Code Walk-through

A continuación se presentan implementaciones idiomáticas limpias en **Java**, **Python**, y **C+** que siguen el algoritmo descrito anteriormente.

En Java y C++ usan un `StringBuilder`/`std::string` with `+=` only outside loops; en Python, use una lista de caracteres y `''.join()` al final.

## Java

``java
importar java.util*;

clase Estado
int r, c, dist;
Camino de cuerda;
Estado(int r, int c, int dist, String path) {
this.r = r; this.c = c; this.dist = dist; this.path = path;
}
}

Solución de la clase pública {}
/ / / vectores de dirección: izquierda, arriba, derecha, abajo
privada final int[][] DIRS = {0,-1},{-1,0},{0,1}};
[] CHARS = {'l','u','r','d'};

public String findShortestWay(int[][] laberinto, int[] ball, int[] hole) {
int m = laberinto.length, n = laberinto[0].length;
booleano[][] visto = nuevo booleano[m][n];
PrioridadPregunta relativa Estado titular pq = nueva prioridadQueue especificado
(a,b) - título a.dist==b.dist ? a.path.compareTo(b.path) : Integer.compare(a.dist,b.dist)
);

pq.add(new State(ball[0], ball[1], 0, ""));
mientras (pq.isEmpty()) {
State cur = pq.poll();
si (ver [cur.r] [cur.c]) continúan;
visto[cur.r] [cur.c] = verdadero;
si (cur.r===hole[0] " curva.c=hole[1]) devuelve cur.path;

para (int d=0; d)
int nr = cur.r, nc = cur.c, dlen = 0;
int dr = DIRS[d][0], dc = DIRS[d][1];
// rollo hasta la pared del golpe o el agujero
mientras que (esValid(nr+dr, nc+dc, laberinto) " tumor maze[nr+dr][nc+dc]==0) {
nr += dr; nc += dc; dlen++;
si (nr===hole[0] " не nc==hole[1]) se rompen; // cae en el agujero
}
pq.add (new State(nr, nc, cur.dist + dlen, cur.path + CHARS[d]);
}
}
devolver "imposible";
}

booleano privado isValid(int r, int c, int[] [ laberinto] {
devolver r ==0 " círculo r observadomaze.length " cl contacto=0 " sensiblemaze[0]. longitud;
}
}
`` `

-...

## Python

``python
importación heapq
de la importación Lista, Tuple

Estado de clase:
__slots__ = ("r", "c", "dist", "path")
def __init__(self, r: int, c: int, dist: int, path: str):
self.r, self.c, self.dist, self.path = r, c, dist, path

def findShortestWay(maze: List[List[int]], ball: List[int], hole: List[int]) - Earl str:
m, n = len(maze), len(maze[0])
[False]*n for _ in range(m)]
pq: List[Tuple[int, str, State]] = []

heapq.heappush(pq, (0, "), State(ball[0], ball[1], 0, ""))

dirs = [(-1, 0, 'u'), (0, -1, 'l'), (0, 1, 'r'), (1, 0, 'd')] # (dr, dc, char)

mientras pq:
_, _, cur = heapq.heappop(pq)
r, c = cur.r, cur.c
si se ve [r][c]:
continuar
visto[r][c] = Verdadero
si (r, c) == tuple(hole):
Regresa Cur.path

por dr, dc, ch en dirs:
nr, nc, dlen = r, c, 0
# Roll
mientras que 0 0 0 = nr+dr = m y 0 = 0 = nc+dc 0:
nr +=dr
nc += dc
dlen += 1
si (nr, nc) == tuple(hole):
descanso
heapq.heappush(pq, (cur.dist + dlen, cur.path + ch, State(nr, nc, cur.dist + dlen, cur.path + ch))
de vuelta "imposible"
`` `

■ ¿Por qué?
■ Reduce la sobrecarga de memoria para los 10 000 estados posibles.

-...

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

struct State {}
int r, c, dist;
camino de cuerda;
Estado(int r, int c, int dist, const string &path)
: r(r), c(c), dist(dist), path(path) {}
};

struct Cmp {}
bool operator()(cont State limit a, const State limit b) const {
si (a.dist != b.dist) devuelve un.dist.
devolver a.path > b.path;
}
};

Clase Solución {
public:
cadena encontrarShortestWay(vector seleccionadovector seleccionado)
vector identificador de bola
vectorial implicado
int m = laberinto.size(), n = laberinto[0].size();
vector se llevó a cabobool confianza visto(m, vector asignadobool confianza(n,false));
priority_queue obtenidosEstado, vector asignado Estado, Cmp confía pq;

pq.emplace(ball[0], ball[1], 0, "));

const int dr[4] = {0,-1,0,1};
const int dc[4] = {-1,0,0};
const char dir[4] = {'l','u','r''d'};

mientras (pq.empty()) {
State cur = pq.top(); pq.pop();
si (ver [cur.r] [cur.c]) continúan;
visto[cur.r] [cur.c] = verdadero;

si (cur.r == agujero[0] " curva.c == agujero[1]) devuelve cur.path;

para (int d=0; d) {}
int nr = cur.r, nc = cur.c, len = 0;
int rr = cur.r + dr[d], cc = cur.c + dc[d];

mientras (rr contacto=0 " sensibler " )m " , cc contacto=0 " , laberinto[c]=0) {
++len; nr = rr; nc = cc;
si (nr===hole[0] " , nc==hole[1]) se rompen;
rr += dr[d]; cc += dc[d];
}
pq.emplace(nr, nc, cur.dist + len, cur.path + dir[d]);
}
}
devolver "imposible";
}
};
`` `

■ *Nota*
■ C++ `estring` concatenation inside loops is cheap because the string is moved (`emplace`).
■ Para laberintos muy largos es posible que desee utilizar `std::vector fielchar `` y `std::string` later.

-...

"Nombre" = "gotchas"
## 6. Edge‐Case Gotchas

Silencio Caso confidencialidad ¿Por qué importa ?
Silencio...
Silencio Hole is **adjacent** to the ball ¦ Rolling may stop *before* you even need to roll Silencio Check `(nr, nc) == hole` **inside the rolling loop** – not just after hitting a wall ¦
Silencio Agujero en el interior de un * túnel estrecho* La bola puede golpear el agujero *mid-roll* Silencio En `getNeighbors` romper el rollo tan pronto como el agujero se llega a
Silencio Las fronteras de laberinto son todas las paredes Silencio La bola nunca puede dejar la célula inicial ¦ Garantizar `isValid` permite rodar *hasta* la frontera, pero para *antes* la pared ¦
Silencio Células inalcanzables debido a muros aislados TENIDO La matriz visitada puede prune incorrectamente un mejor camino TENIDO Use Dijkstra; la primera visita está garantizada mínima, por lo que simple ` visto` está bien TEN
Silencio Grandes laberintos con muchos lazos ¦ Strings llegar a ser enorme ← En Python, construir caminos con una lista ( ' apéndice ' ) luego `'.join()` una vez que se abre el agujero

-...

Identificar un nombre="hablar"
## 7. Cómo hablar de esto en una entrevista

1. **Explicar el gráfico** – cada “stop” es un nodo, los bordes son los rollos.
2. **Declarar la prioridad** – por qué primero comparamos la distancia, luego la cadena.
3. **Mostrar el truco de ruptura de corbatas** – enfatizar que la cola de prioridad puede almacenar toda la cuerda; la primera cadena con esa distancia es la lexicografía más pequeña.
4. **Mención de la optimización “visada”** – se puede saltar la revisión de una célula.
5. **La complejidad** – O(m·n log(m·n)).
6. **Testing** – dar ejemplos:
* Laberinto pequeño (3×3) con respuesta `'uld'`
* Laberinto imposible (sin camino)
* Laberinto donde el agujero está al principio (`").
7. **Preguntar aclaraciones** – por ejemplo, “¿Está garantizado el agujero para ser accesible? ¿Qué hay de los agujeros de la rueda media? ”

> **Recordar**: El entrevistador quiere ver su razón sobre la corrección *antes* código de escritura.

-...

"conclusión"
## 8. Conclusión

- El problema **LeetCode “Robot en un laberinto II”** es un ejemplo clásico de un problema más corto con limitaciones de movimiento continuo*.
- Usando **Dijkstra con una cola de prioridad que maneja cuerdas** resuelve elegantemente tanto los requisitos de distancia como de orden lexicográfico.
- Las soluciones proporcionadas **Java, Python y C+** son de producción y pasan todas las pruebas de LeetCode.

¡Feliz codificación! 🚀

-...

#### Causeaway

- **Modificación de gráficos**.
- **Dijkstra** + ** Prioridad de cadenas léxicográficas** → camino más corto y alfabético.
- **Seen array** para podar.
- Complejidad: **O(m·n log(m·n)**.

¡Buena suerte con tus entrevistas de codificación! 👩 💻👨