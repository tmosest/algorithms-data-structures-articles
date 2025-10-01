-...
Título: LeetCode 2814. Tiempo mínimo toma para llegar destino sin crecer -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 LeetCode 2814 – “Minimum Time Takes to Reach Destination Without Drowning”

■ ** Objetivo:** Encontrar el número mínimo de segundos necesarios para caminar de **S** a **D** en una red de `n × m ' evitando la piedra (`X`) y las células de inundación (`*`).
■
■ La inundación se extiende cada segundo a las células vacías de 4 vecinos. Usted no puede pisar una célula que se inunda en el mismo segundo que usted pisa sobre ella.
■
■ **Retorno** el tiempo de viaje más corto, o `-1` si es imposible.

-...

## TL;DR

* Computar el tiempo que cada célula será inundada por un BFS **multi-source que comienza de cada `*`.
* Ejecutar un segundo BFS** desde **S** donde sólo se permite un traslado a un vecino si:
* el vecino no es una piedra,
* el vecino no está inundado * antes o a* la llegada segunda,
* el vecino está vacío o el destino.
* La primera vez que alcanzamos **D** es la respuesta.

Complejidad del tiempo: `O(n · m)`
Complejo de memoria: `O(n · m)`

-...

## ¿Por qué es un gran problema de entrevista?

Silencio Silencio Silencio Silencio
Silencio...
TEN **Multi‐source BFS** – enseña al candidato cómo manejar la propagación simultánea (como el fuego, la infección). Los cheques diarios pueden ser complicados. **“Step into a cell that is flooded at the same second”** – un caso de esquina sutil que a menudo viaja a candidatos. Silencio
Silencio **Acercamiento de dos fases** – separación clara de “lo que sucederá” (flood) y “lo que puedo hacer” (move). tención **Large grid (100×100)** → debe evitar algoritmos cuadráticos o exponenciales. Silencio **Off‐by-one errores** en el cálculo del tiempo cuando las inundaciones y el movimiento suceden en el instante *same*. Silencio
Silencio La solución es **calable** a mayores limitaciones (por ejemplo, `10^3 × 10^3`). Necesidad de pensar en **visitado** estado; ingenuo `boolean[][][ puede no ser suficiente si permite volver a visitar en un momento posterior. TEN **Las estructuras de datos de Multiple** (queues, matrices) pueden romper el código para una entrevista corta. Silencio

-...

## Full Solutions

A continuación encontrará un código limpio y listo para la producción para **Java**, **Python**, y **C+**.
Cada implementación sigue la misma lógica: computar los tiempos de inundación, luego BFS el jugador.

-...

### 1. Java

``java
importar java.util*;

Solución de la clase pública {}
int final estático privado[][] DIRS = {-1,0},{0},{0,-1},{0,1}};
INF final estático privado = entero.MAX_VALUE;

mínimo público Segundos(Lista realizadaLista) {
int n = land.size();
int m = land.get(0).size();

// 1 / ⃣ Tiempos de inundaciones: BFS multi-fuente de todos '* '
int[][] flood = new int[n][m];
para (int i = 0; i < n; i++) Arrays.fill(flood[i], INF);

Queue hizo [] confiar q = nuevo ArrayDeque correspondió();
int startR = 0, startC = 0, destR = 0, destC = 0;

para (int r = 0; r) {}
para (int c = 0; c) {}
Célula de crianza = land.get(r).get(c);
si ("*".equals(cell)) {
flood[r][c] = 0;
q.add(new int[]{r, c});
} si ("S".equals(cell)) {}
startR = r; startC = c;
} si ("D".equals(cell) {
destR = r; destC = c;
}
}
}

(!q.isEmpty()) {
int[] cur = q.poll();
int r = cur[0], c = cur[1], t = flood[r][c];
para (int[] d : DIRS
int nr = r + d[0], nc = c + d[1];
si (0 י= nr ' círculo nr)
(land.get(nr).get(nc).equals(".) TENIDO TIERRA TIERRA (nr).get(nc).equals("S"))
flood[nr][nc] == INF) {
flood[nr][nc] = t + 1;
q.add(new int[]{nr, nc});
}
}
}

// 2 comentarios ⃣ Player BFS
boolean[][] vis = new boolean[n][m];
Queue realizaint[] confía pq = nuevo ArrayDeque correspondió();
pq.add(new int[]{startR, startC, 0}); // r, c, time
vis[startR] [startC] = verdadero;

mientras (pq.isEmpty()) {
int[] cur = pq.poll();
int r = cur[0], c = cur[1], t = cur[2];
si (r == destR ' pénc == destC) regresa t;

para (int[] d : DIRS
int nr = r + d[0], nc = c + d[1];
nt = t + 1;
si (0 י= nr ' círculo nr)
!vis[nr][nc] "
!land.get(nr).get(nc).equals("X") "
(land.get(nr).get(nc).equals(".) TENIDO TIERRA TIERRA (nr).get(nc).equals("D"))
inundación[nr][nc]
vis[nr][nc] = verdadero;
pq.add(new int[]{nr, nc, nt});
}
}
}

retorno -1; //
}
}
`` `

-...

### 2. Pitón

``python
de las colecciones importa
de la importación Lista

Solución de clase:
DIRS = [(-1, 0), (1, 0), (0, -1), (0, 1)]
INF = 10 ** 9

mínimo Seconds(self, land: List[List[str]]) - int:
n, m = len(land), len(land[0])

# 1 Tiempos de inundaciones
flood = [[self.INF] * m for _ in range(n)]
q = deque()
sr = sc = dr = dc = 0

para i en rango(n):
para j en rango(m):
si la tierra [i] [j] == '*':
flood[i][j] = 0
q.append(i, j))
elif land[i][j] == 'S':
sr, sc = i, j
elif land[i][j] == 'D':
dr, dc = i, j

mientras q:
r, c = q.popleft()
t = flood[r][c]
para Drc, dcc en sí mismo. DIRS:
nr, nc = r + drc, c + dcc
si 0 0 0 0 0 0 0 0 0 0 0 0 0 0
(land[nr][nc] in {', 'S'}) and flood[nr] == auto. INF:
flood[nr][nc] = t + 1
q.append(nr, nc))

# 2⃣ Player BFS
vis = [False] * m for _ in range(n)]
q = deque([(sr, sc, 0)])
vis[sr][sc] = True

mientras q:
r, c, t = q.popleft()
si r == dr y c == dc:
t
para Drc, dcc en sí mismo. DIRS:
nr, nc = r + drc, c + dcc
nt = t + 1
si 0 0 0 0 0 0 0 0 0 0 0 0 0 0
no vis[nr][nc] y \
land[nr][nc]= 'X' y \ '
(land[nr][nc] in {', 'D'}) and \
inundación[nr][nc]
vis[nr][nc] = True
q.append(nr, nc, nt))

retorno -1
`` `

-...

### 3. C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
INF = 1e9;
vector asignadopair observadoint,intenta confiar dirs = {-1,0},{1,0},{0,-1},{0,1}};

mínimo Segundos (vector seleccionador) {
int n = land.size(), m = land[0].size();

--------- Tiempos de inundaciones --------
vector seleccionado(m, INF));
queue hacíapair se hacía,intentas
int sr=0, sc=0, dr=0, dc=0;

para (int r=0; r obtenidos; ++r) {}
para (int c=0; c) {}
si {}
flood[r][c]=0;
q.emplace(r,c);
Si no, si...
sr=r; sc=c;
Si no, si...
dr=r; dc=c;
}
}
}

(!q.empty()) {
auto [r,c] = q.front(); q.pop();
int t = flood[r][c];
para (auto [drc,dcc]: dirs) {
int nr=r+drc, nc=c+dcc;
si (nr título=0 " sensiblen " nc confianza=0 " sensiblem "
(land[nr][nc]=='.' Silencioso tierra[nr]='S') "
flood[nr][nc]==INF) {
flood[nr][nc]=t+1;
q.emplace(nr,nc);
}
}
}

--------- 2⃣ Player BFS ----------
vector se llevó a cabobool confianza vis(n, vector asignadobool confianza(m,false));
queue efectuastetuple obtenidosint,int,int
pq.emplace(sr,sc,0);
vis[sr][sc]=true;

mientras (pq.empty()) {
auto [r,c,t] = pq.front(); pq.pop();
si (r==dr ' pc=dc) regresa t;
para (auto [drc,dcc]: dirs) {
int nr=r+drc, nc=c+dcc;
int nt=t+1;
si (nr título=0 " sensiblen " nc confianza=0 " sensiblem "
!vis[nr][nc] "
tierra[nr][nc]!='X' '
(land[nr][nc]=='.' Silencioso tierra[nr]='D') "
flood[nr][nc] confíant) {}
vis[nr][nc]=true;
pq.emplace(nr,nc,nt);
}
}
}
retorno -1;
}
};
`` `

-...

## Common Pitfalls > Cómo evitarlos

Silencio Pitfall Silencio ¿Por qué sucede?
Silencio...
Silencio **Off‐by-one al comparar el tiempo de inundación** Silencio Se extiende Flood *después* se mueve en el mismo segundo Silencio Uso `flood[nr][nc] înt` (tiempo de llegada) en lugar de `conejo=`. Silencio
Silencio **Estar en una celda inundada** Silencio El jugador puede esperar en una celda que inundará el próximo segundo Silencio Nunca encubrimos la misma celda dos veces; la primera llegada es siempre la más temprana. Silencio
Silencio **Manejando el destino** Silencio Algunos candidatos olvidan que entrar en **D** siempre está permitido, incluso si el tiempo de inundación es `0` Silencio Permite explícitamente 'célula == 'D'' independientemente del tiempo de inundación. Silencio
Silencio **Elevar valor INF** Silencio `INT_MAX` puede desbordarse al añadir 1 TENIDO Utilice un valor centinela (INF = 1e9` o `INT_MAX / 2`) que se puede aumentar de forma segura. Silencio
Silencio **Dirección visitada** Silencio Reiniciar una celda más tarde puede ser óptima (pero nunca se necesita aquí) Silencio Un simple `herramienta vis[n][m]` basta porque el segundo BFS es *shortest‐path primero* – cualquier entrada posterior sería más lenta. Silencio

-...

## Complexity Analysis

TEN TERRITOR ANTE LAS ACTIVIDADES
...----------------------
← Inundación inundada BFS Silencio Cada célula es desactivada una vez, 4 vecinos comprobaron → `4·n·m` cheques Silencio `O(n·m)` Silencio
Silencioso Jugador BFS TENIDO Mismo razonamiento como inundación BFS ANTE `O(n·m)` Silencio
TENIDO Memoria ANTERIOR Dos matrices intrínsecas ( " inflood " y " v " ) Silencio

Para las limitaciones máximas (`100 × 100`), el algoritmo termina en unos pocos milisegundos y utiliza ■ 1 MB de memoria – perfectamente aceptable para una entrevista.

-...

Listo para Plantilla de uso para entrevistas

Durante una entrevista con tiempo no desea pasar tiempo construyendo una interfaz de usuario, escribiendo persianas de entrada, etc.
A continuación se muestra una plantilla **minimal** que puede pegar en el editor LeetCode (Java, Python, o C++).

Silencio Idioma Silencio Plantilla
Silencio...
Silencio **Java** Silencio `clase pública Solution { public int minimumSeconds(Lista indicadoLista interpretadoString confianza land) { /* ... */ } Silencio
Silencio **Python** Silencio `clase Solution: def minimumSeconds(self, land: List[List[str]]) - título int: /* ... */` Silencio
Silencio **C+** Silencioso `clase Solution { public: int minimumSeconds(vector seleccionadovector asignadovector fielchar implicados limitada land) { /* ... */ } };` Silencio

Sólo reemplace el comentario `/* ... */` con el código completo mostrado anteriormente.

-...

## Interview‐Friendly Checklist

1. **Declarar la idea de dos fases** (primera inundación, luego moverse).
2. **Mostrar BFS** – usted puede caminar a través de cómo inicializar la cola y visitar vecinos.
3. **Explicar la condición del tiempo**: `floodTime[neighbour] ⇩ currentTime + 1`.
4. **Hablar sobre casos de esquina**:
* Si la célula de inicio está rodeada de células de inundación → imposible.
* Si **D** está en la misma fila/col como un `*` → debe llegar *antes* se inunda.
5. **La complejidad**: `O(n · m)` es lo mejor que puedes hacer – la cuadrícula es el factor limitante.
6. **Pregunte aclarando las preguntas** (por ejemplo, “¿Podemos caminar diagonalmente?” – no pueden).

-...

## SEO‐Friendly Takeaway

Si estás buscando a *land que el próximo trabajo de tecnología* o *crush your coding interview*, resalta LeetCode 2814 en tu currículum:

- **Keywords:** `LeetCode 2814`, `mínimo tiempo para llegar a destino sin ahogarse `, `multi‐source BFS`, `Java BFS flood spread`, `Python BFS solution`, `C++ flood BFS`, `coding interview problem`, `coding challenge interview`.

- ¿Por qué importa? Demuestra *problema descomposición*, *pensamiento algorítmico*, y *elaboración limpia* habilidades; todos los entrevistadores valoran altamente.

-...

## 🎯 Final Thought

LeetCode 2814 es más que un rompecabezas de paisaje inundado; es un estudio ** min-case** de cómo combinar **simulation** (the flood) y **search** (your path) en una solución única y eficiente.

*Mostrar a los entrevistadores* que puedes:

1. Rompe un problema en fases claras**.
2. Use **BFS** – el caballo de trabajo de muchos problemas de entrevista.
3. Manejo sutil ** tiempo-sincronización** limitaciones.

Buena suerte, y recuerde – el diluvio es sólo una metáfora para las restricciones del mundo real; mantener la calma y el código encendido! *