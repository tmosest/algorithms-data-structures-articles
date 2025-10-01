-...
Título: LeetCode 864. Sendero más corto para conseguir todas las llaves -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## Sendero más corto para conseguir todas las llaves – 864 (LeetCode)

Silencio Idioma Silencio Nombre del archivo Silencio Key Idea Silencio
Silencio----------------------------
Silencio **Java** Silencioso `Solution.java` Silencioso BFS + mordaz – estado = `(row, col, keys)` Silencio
Silencio **Python** Silencio `solution.py` Silencio `deque` BFS - la misma representación del estado
Silencio **C+** Silencio `solution.cpp` Silencio `queue` + `unordered_set` para los estados visitados

A continuación se encuentran soluciones completas, listas para pasar por cada idioma, seguidas por un blog **SEO-optimizado** que explica el problema, el algoritmo y las sugerencias de estilo de entrevista.

-...

## 1. Java – `Solution.java `

``java
importar java.util*;

Solución de la clase pública {}

Estado de clase estática privada {
teclas int; // mascarilla de llaves recolectadas
int r, c; // posición actual

Estado(int keys, int r, int c) {
esto. claves = llaves;
this.r = r;
this.c = c;
}
}

público más corto PathAllKeys(String[] grid) {
int m = grid.length, n = grid[0].length();
total Keys = 0;
int sr = -1, sc = -1;

// 1 / ⃣ Encontrar las teclas de inicio y cuenta
para (int i = 0; i)
para (int j = 0; j) {}
char ch = grid[i].charAt(j);
si (ch ==@) { sr = i; sc = j; }
si ('a') totalKeys++;
}
}

int allKeysMask = (1  Se hizo totalKeys) - 1;
Queue Utilizar el Estado titular q = nuevo ArrayDeque corresponde();
Establecer:String titulada visitado = nuevo HashSet correctamente();

q.offer(new State(0, sr, sc));
visitado.add(0 + " + sr + " + sc);

int[] dirs = {1,0},{-1,0},{0,1},{0,-1}};
int steps = 0;

// 2down B BFS
(!q.isEmpty()) {
int sz = q.size();
para (int s = 0; s) {}
State cur = q.poll();

si (cur.keys == allKeysMask) los pasos de retorno;

para (int[] d : dirs) {
int nr = cur.r + d[0];
int nc = cur.c + d[1];
si (nr < 0 Новыный nr не= m удующенный nc неныеные n) continúan;

char ch = grid[nr].charAt(nc);
si (ch == '#') continúan; //

int newKeys = cur.keys;
si
newKeys TENIDO= 1 ANTERITO (ch - 'a'); // elegir clave

si ('A') se entiende= ch " sensible " ) == 0)
continuar; // puerta cerrada

llave de cuerda = newKeys + " + nr + " + nc;
si (visited.add(key)) { // nuevo estado
q.offer(new State(newKeys, nr, nc));
}
}
}
pasos++;
}
retorno -1; // imposible
}
}
`` `

### Complexity

TENIDO ANTERIOR TERRITORIO TERRITORIO
Silencio...
Silencio **O(m · n · 2n)** donde `n` ≤ 6 (keys) Silencio **O(m · n · 2n)** para el conjunto visitado

-...

## 2. Python – `solution.py `

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def más corto PathAllKeys(self, grid: List[str]) - int:
m, n = len(grid), len(grid[0])
total_keys = 0
sr = sc = 1

# 1 Encontrar el comienzo, contar las teclas
para r en rango(m):
para c en el rango(n):
ch = grid[r][c]
si ch == '@':
sr, sc = r, c
elif 'a' = ch = 'f'
total_keys += 1

all_keys_mask = (1  se indicaron total_keys) - 1
q = deque([(0, sr, sc)]) # (keys, r, c)
visitados = {(0, sr, sc)}
dirs = [(1,0),(-1,0),(0,1),(0,-1)]
pasos = 0

# 2️ BFS
mientras q:
para _ en rango(len(q)):
claves, r, c = q.popleft()
si las teclas == all_keys_mask:
Pasos de retorno

para dr, dc en dirs:
nr, nc = r + dr, c + dc
si no (0 <= nr < m y 0 = nc = nc)
ch = grid[nr][nc]
si ch == '#': continuar

new_keys = teclas
si 'a'
new_keys TENIDO= 1 ANTESITO (ord(ch) - ord('a'))
si 'A' se hizo= ch  ch= 'F' y no (new_keys √Ī (ord(ch) - ord('A')) > 1):
continuar

estado = (new_keys, nr, nc)
si el estado no es visitado:
visitado.add(state)
q.append(state)
pasos += 1
retorno -1
`` `

### Complexity

- **Tiempo**: `O(m · n · 2n)` - en la mayoría `O(400 · 64)` para red 20×20 con 6 llaves.
- **Espacio**: `O(m · n · 2n)` – estados visitados.

-...

## 3. C++ – `solution.cpp `

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
struct State {}
claves int; // bitmask
int r, c;
Estado(int k, int rr, int cc) : keys(k), r(rr), c(cc) {}
};
public:
int shortestPathAllKeys(vector seleccionadostring ventaja) {
int m = grid.size(), n = grid[0].size();
total Keys = 0, sr = -1, sc = -1;

// 1 / ⃣ Localizar las teclas de inicio y cuenta
para (int i = 0; i)
para (int j = 0; j)
char ch = grid[i][j];
si (ch ==@) { sr = i; sc = j; }
si ('a' <= ch ' t Keys;
}

int allMask = (1  won total) - 1;
q);
unordered_set buscadostring confianza vis; // visitado estado hash

q.emplace(0, sr, sc);
vis.insert("0 " + to_string(sr) + " + to_string(sc));

const int dr[4] = {1,-1,0,0};
const int dc[4] = {0,0,1,-1};
int steps = 0;

// 2down B BFS
(!q.empty()) {
int sz = q.size();
para (int i = 0; i) {}
State cur = q.front(); q.pop();

si (cur.keys == allMask) los pasos de retorno;

para (int d = 0; d)
int nr = cur.r + dr;
int nc = cur.c + dc;
si (nr < 0 Новыный nr не= m удующенный nc неныеные n) continúan;

char ch = grid[nr][nc];
si (ch == '#') continúan; //

int newKeys = cur.keys;
si
newKeys TENIDO= 1 ANTERITO (ch - 'a'); // recoger clave

si ('A') se entiende= ch " sensible " ) == 0)
continuar; // puerta cerrada

llave de cadena = to_string(newKeys) + " + to_string(nr) + " + to_string(nc);
si (vis.insert(key).second) { // nuevo estado
q.emplace(new Keys, nr, nc);
}
}
}
++ pasos;
}
retorno -1; //
}
};
`` `

-...

## 4. Blog Post – “Mastering LeetCode 864: Sendero más corto para conseguir todas las claves”

■ **Keywords**: Camino más corto para conseguir todas las claves, LeetCode 864, BFS, bitmask, solución Java, solución Python, solución C++, entrevista de codificación, entrevista de ingeniería de software, prep

-...

#### Introduction

**LeetCode 864 – *Shortest Path to Get All Keys*** es un clásico rompecabezas de investigación de la cuadrícula que prueba dos habilidades básicas que cada entrevista del programa requiere:

1. **Breadth‐First Search (BFS)** – para la exploración más corta.
2. **Bit-mask DP** – para comprimir conjuntos de llaves en un solo entero.

Con hasta **6 llaves** (`a-f`) y un tamaño de cuadrícula moderado (`≤ 20 × 20`), el algoritmo es rápido * y* fácil de entender – el problema de entrevista perfecta.

-...

### El problema (en una frase)

■ *Given a 2-D grid where `@` is your start, `#` block movement, lowercase letters (`a–f`) are keys and uppercase letters (`A–F`) are locked doors that require the matching key, find the minimal number of moves to collect every key. *

Si no puedes conseguir todas las llaves, devuelve `-1`.

-...

### Why BFS + Bit‐Masking Works

Ø Concepto Silencioso
Silencio...
Silencio **Estado** Silencioso `(row, col, keys)` – debes recordar *donde* estás *y* *qué teclas* tienes. Silencio
Silencio **Bit-mask** Silencio Cada clave es un poco (`1 Identificado índice`). Para ≤6 llaves necesitamos en la mayoría de 64 bitmasks distintos (`26`). Silencio
Silencio **Transición** Silencio Mover a una célula adyacente si no es una pared. Si contiene una llave, coloque el bit; si es una puerta, compruebe el bit antes de moverse. Silencio
Silencio **Visitado** Silencio Hash `(row, col, keys)` para evitar volver a visitar los estados. Sin la dimensión de las llaves nos hundimos para siempre. Silencio

Debido a que BFS explora *nivel por nivel*, la primera vez que vemos `allKeysMask` hemos encontrado el camino más corto.

-...

### «Bien» – Lo que hace ganar esta solución

- **Time‐efficient**: `O(m·n·2^k)` donde `k` ≤ 6, perfectamente bien para los límites de LeetCode.
- **Espacio-eficiente**: `O(m·n·2^k)` estados visitados – menos de 400 × 64 Ω 25k elementos.
- Por favor. Un bucle BFS claro, una operación de masajista por movimiento.
- Language-agnostic**: La misma lógica funciona en Java, Python, C++ e incluso Go o Rust.

-...

### "Bad" – Cosas que hacer

Silencio Pitfall Silencio Lo que sucede Silencioso
Silencio--------------------------
Silencio **Macama llave inglesa** Silencioso Usando `1 > Se hizo (ch - 'a') ' con el carácter base equivocado conduce a pedacitos equivocados para 'd`-`f`. Silencio
Silencio **Over-visited states** latitud Storing just `(row, col)` ignora las diferencias clave, causando ciclos. ← Incluir las teclas en la llave visitada. Silencio
Silencio **Large grid & muchas teclas** ← El caso más malo puede volar; si las claves > 10 la solución disminuye dramáticamente. El problema de la vida garantiza ≤6 llaves, por lo que es seguro. Silencio

-...

### "Ugly" – La complejidad sutil

** Hash-based visited**: Las cuerdas de construcción `"mask r c"` o tuples pueden ser * hambriento de memoria* si la cuadrícula es grande.
- *Solución*: En C++ se puede utilizar un vector 3-D `vector seleccionadovector asignadovector asignadovector interpretadobool visitado;` o una `estructura ' personalizada Hash.
- ¿Por qué? Si eliges una llave *después* pasando una puerta, debes retroceder – el BFS maneja automáticamente esto, pero depurar puede ser confuso.
**Puntos de partida obligatorios**: LeetCode garantiza un comienzo, pero un solucionador genérico necesitaría colar todas las células `@`.

-...

### Interview‐style Tips

Silencio tóxico Qué decir
Silencio...
Silencio **Cuando se le pide que explique BFS** Silencio "Voy a pedir el comienzo, entonces por cada nivel voy a expandir a todos los vecinos. Debido a que la cuadrícula no tiene peso, la primera vez que llego a la meta está garantizada a ser la más corta.” Silencio
Silencio **Cuando el entrevistador hace hincapié en la memoria** Silencioso “Desde que tenemos en la mayoría de 6 teclas, podemos codificar conjuntos clave en un entero de 6 bits, reduciendo drásticamente el espacio del estado”. Silencio
Silencio **Si el entrevistador quiere una solución en C+** Silencioso "Usaré un hash personalizado para la struct `(r, c, máscara)` y un `queue`. Eso evita construir cuerdas”. Silencio
Silencio **Si preguntan sobre los casos de bordes** Silencioso “Voy a tratar una puerta como una pared si no tengo la llave, de lo contrario pasaré a través. La máscara asegura que nunca revisito un estado con el mismo conjunto de llaves.” Silencio
Silencio **Cuando la complejidad del tiempo es preguntada** Silencioso “Es O(m·n·2^k) donde k ≤ 6, así que al más 400 × 64 operaciones, que es trivial para las rejillas 20×20.” Silencio

-...

## Final Verdict

**LeetCode 864** es *el rompecabezas de la red* que muestra el dominio de BFS + bitmask. Su capacidad para implementarlo en cualquiera de los idiomas que ha practicado (Java, Python, C++) demuestra que usted entiende *búsqueda*, *comprsión del estado*, y *time-space trade‐offs*.

Cuando presente la solución en una entrevista:

1. **Mostrar el pseudocódigo** (estado, transición, visitado).
2. ** Explique por qué BFS da el camino más corto**.
3. **Descubre el truco de bitmask** – “Cada clave es un poco, así que necesitamos sólo 6 bits. ”
4. ** Limitaciones de mención** – “En la mayoría de las 6 llaves, el espacio del estado permanece pequeño. ”

No sólo resolverá el problema, sino que también convencerá al entrevistador que está listo para los desafíos de traversal de gráficos del mundo real.

-...

### Wrap‐Up

Mastering LeetCode 864 significa que has practicado un patrón algoritmo *core* que aparecerá en muchas entrevistas de codificación: **bús + compresión del estado**.

Prueba el **Java**, **Python**, y **C++** implementaciones arriba, casos de borde de prueba, y estarás seguro de entrar en cualquier sala de entrevistas.

¡Buena suerte! 🚀

-...


■ *No dude en adaptar el texto del blog a su propia voz o añadir fragmentos de código para su idioma favorito. ¡Feliz codificación! *