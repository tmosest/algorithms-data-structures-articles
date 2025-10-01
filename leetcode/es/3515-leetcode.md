-...
Título: LeetCode 3515. Sendero más corto en un Árbol Peso -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📌 Leetcode 3515 – Sendero más corto en un Árbol Peso
■ **Java Silencio Python ← C++ – Código completo + entrevista Blog de estilo**

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

Te dan un árbol ponderado arraigado en el nodo 1.
Dos tipos de consultas llegan en línea:

Silencio, sufrimiento
Silencio...
Silencio `[1, u, v, w]` Silencio ** Actualizar** el peso del borde `(u, v)` a `w`. El par está garantizado para ser un borde existente. Silencio
Silencio `[2, x]` Silencio Regresar la distancia más corta** de la raíz (nodo 1) a nodo `x`. Silencio

n, q ≤ 105`, pesos de borde `≤ 104`.
La tarea es responder a todas las preguntas `[2, x]` de manera eficiente mientras se apoyan las actualizaciones de bordes.

-...

#### 2down⃣ Solución ingenua (Por qué no pasará)

* Por cada `[1, ...]` cambiar reconstruir todas las distancias con DFS/BFS – **O(n)** por actualización.
* Por cada `[2, ...]` leer la distancia pre-computada - **O(1)**.

Con hasta 105 actualizaciones esto se convierte en `O(n·q)` ♥ `1010`, mucho más allá del límite de tiempo.

-...

#### 3down⃣ The Elegant Idea – Euler Tour + Fenwick Tree

1. **SAS de la raíz* *
* Compute the initial distance `dist[v]` del nodo 1 a cada nodo `v`.
* Entrada récord ( "tin[v] " ) y salida ( " tout[v] " ) veces – el clásico **Euler tour**.
* Para un árbol arraigado todo el subárbol de `v` ocupa el segmento continuo `[tin[v], tout[v].

2. **Mapa cada borde al niño* *
* For an edge `(u, v)` the node with larger `tin` is the child.
* Mantener el peso actual en un mapa `edgeWeight[(parent, child)]`.

3. **Fenwick (Binary Indexed) Tree**
* Necesitamos *range add* (actualizar el subárbol entero) y *point query* (distance to a node).
* Un árbol de Fenwick que soporta actualizaciones de rango con dos actualizaciones de puntos funciona en `O(log n)`.

4. *Procesamiento de una consulta*

*Update `[1, u, v, w]**
* Identificar al niño (`c`).
* `delta = w - oldWeight`.
* Aplicar `delta` al segmento `[tin[c], tout[c] ' via `rangeAdd`.
* Almacenar `nuevo Peso' en el mapa.

* Distance `[2, x]***
* Respuesta = `dist[x] + fenwick.pointQuery(tin[x])`.
* `dist[x]` es la distancia de referencia, `fenwick` contiene todos los deltas acumulados.

**Las complejidades* *

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio DFS (pre-process) Silencio
TENIDO Cada consulta TENIDO `O(log n)` Silencio

Eso es lo suficientemente rápido para nodos y consultas.

-...

## 🧑 💻 Code Walkthrough

A continuación se presentan implementaciones limpias y listas para pasar en **Java**, **Python**, y **C+** siguiendo el estilo Leetcode.

-...

### 🟨 Java Solution

``java
importar java.util*;
importa java.io.*;

Solución de la clase pública {}
/* ------------ Fenwick Tree (1-basado)--------
clase privada estática Fenwick {
final privado [] bit;
privada final int n;
Fenwick(int n) { this.n = n; bit = new long[n + 2]; }
vacío add(int idx, long val) {
para (int i = idx; i i " i) bit[i] += val;
}
larga suma (int idx) {}
larga res = 0;
para (int i = idx; i 0; i -= i ' i) res += bit[i];
restitución;
}
/* añadir rango: añadir val a [l, r] */
rango de vacío Add(int l, int r, long val) {
add(l, val);
add(r + 1, -val);
}
}

--------- Asistente de llaves...
llave larga estática privada(int a, int b) {}
(largo) a (seguido) se cumplió 32)
}

--------- Solución principal...-------- */
public List Nombramiento:Integer ratio árbolQueries(int n, List madeList madeInteger bordes,
Lista seleccionadaLista realizadaInteger confianza consultas) {
* Lista de adyacencia*
Lista seleccionadaLista realizada[]] título g = nuevo ArrayList recomendado();
para (int i = 0; i <= n; i++) g.add (new ArrayList fiel());
para (Lista realizadaInteger título e : bordes) {
int u = e.get(0), v = e.get(1), w = e.get(2);
g.get(u).add(new int[]{v, w});
g.get(v).add(new int[]{u, w});
}

/* arrays */
long[] dist = new long[n + 1];
int[] tin = nuevo int[n + 1];
int[] tout = nuevo int[n + 1];
long[] timer = nuevo largo[1]; // para emular el entero mutable
Mapa seleccionadoLong, Integer confianza weightMap = new HashMap garantizado();

/* DAAT para calcular el destilamiento, lata/tout y los pesos del niño */
dfs(1, 0, 0, g, dist, tin, tout, timer, weightMap);

Fenwick fenwick = nuevo Fenwick(n);
Lista realizadaInteger confía ans = nuevo ArrayList correctamente();

para (Lista seleccionadaInteger título q : consultas) {}
si (q.get(0) == 1) {///
int u = q.get(1), v = q.get(2), w = q.get(3);
int parent, child;
si (tin[u] , lata [v]) { padre = u; niño = v; }
{ parent = v; child = u; }

long old = weightMap.get(key(parent, child));
long delta = (long) w - old;
fenwick.rangeAdd(tin[child], tout[child], delta);
weightMap.put(key(parent, child), w);
} más { //
int x = q.get(1);
largo cur = dist[x] + fenwick.sum(tin[x]);
ans.add(int) cur); // cabe en int bajo restricciones
}
}
devolver los ans;
}

--------- Aplicación del DAAT ---------- */
dfs de vacío privado(int u, int parent, int deep, List madeList madeint[] g,
long[] dist, int[] tin, int[] tout, long[] timer,
Mapa seleccionadoLong, Integer confianza weightMap) {
dist[u] = profundidad;
tin[u] = (int) timer[0] + 1; // 1-based index
timer[0]+;

para (int[] nb : g.get(u) {
int v = nb[0], w = nb[1];
si (v == padre) continúan;
weightMap.put(key(u, v), w); // store parent→child weight
dfs(v, u, profundidad + w, g, dist, tin, tout, timer, weightMap);
}
tout[u] = (int) timer[0];
}
}
`` `

*Puntos clave*

* `long` en todas partes – evita el desbordamiento si decides relajar las restricciones.
* La llave del borde empaca dos `int`s en un `long` para un rápido `HashMap`.
* `Fenwick.range Add` es un clásico *difference array* truco.

-...

### 🟪 Python Solution

``python
importadores
de las colecciones importadas por defecto
de la importación Lista

# ---------- Árbol de Fenwick para añadir rango + búsqueda de puntos...----------
clase Fenwick:
def __init__(self, n: int):
self.n = n
self.bit = [0] * (n + 2)

def _add(self, i: int, delta: int) Ninguno.
mientras que yo...
auto.bit[i] += delta
i += i

def range_add(self, l: int, r: int, delta: int) Ninguno.
auto._add(l, delta)
auto._add(r + 1, -delta)

def point_query(self, i: int) - título int:
S = 0
mientras que yo 0:
s += self.bit[i]
I -= i
retorno s


Solución de clase:
def treeQueries(self, n: int,
bordes: List[List[int],
consultas: List[List[int]]) - No. List[int]:
# Lista de adjacency
g = [[] para _ en rango(n +1)]
para u, v, w en los bordes:
g[u].append(v, w))
g[v].append(u, w))

(n +1)
(n +1)
(n +1)
temporizador = 1

# map: (parente, child) - titulado peso
¿Qué?

def dfs(u: int, p: int, d: int):
temporizador no local
dist[u] = d
tin[u] = timer
timer += 1
for v, w in g[u]:
si v == p: continuar
edge_w[(u, v)] = w # store parent→child weight
dfs(v, u, d + w)
tout[u] = timer - 1

dfs(1, 0, 0)

bit = Fenwick(n)
ans = []

para q en consultas:
si q[0] == 1: Actualización
_, u, v, new_w = q
niño = v si estaño [u]
padre = u si niño == v v v
viejo = edge_w [(parente, niño)]
delta = new_w - old
bit.range_add(tin[child], tout[child], delta)
edge_w[(parente, child)] = new_w
# distancia
_, x = q
cur = dist[x] + bit.point_query(tin[x])
ans.append(cur)

Retorno
`` `

*Por qué es rápido*

* `timer` es 1-basado así que los índices Fenwick se alinean con los tiempos de entrada de Euler.
* `edge_w` mantiene el mapeo de niños *exacto* – no repetido DFS.

-...

#### 🟪 C++ Solución

``cpp
#include יbits/stdc++.h
usando std namespace;

clase Fenwick {}
vector alcanzado largo tiempo bit;
int n;
public:
Fenwick(int n=0){ init(n); }
vacio init(int n_) { n = n_; bit.assign(n+2, 0); }
vacío add(int idx, long long val){
para (int i=idx;i observado=n;i+=i sensible-i) bit[i] += val;
}
larga suma (int idx){
largo res=0;
para(int i=idx;i confianza0;i-=i sensible-i) res+=bit[i];
restitución;
}
// rango añadir [l,r] += val
rango de vacío Add(int l,int r,long long val){
add(l,val); add(r+1,-val);
}
};

static inline long key(int a,int b){
retorno (static_cast realizado largo largo(a) realizado32)
}

Clase Solución {
public:
vector significado árbolQueries(int n, vector asignadovector identificadoint círculo bordes,
vector asignador implicados iguales consultas) {}
/* adjacency */
vector realizador designadopair realizado,int hilo conductor g(n+1);
para(auto &e: edges) {}
int u=e[0],v=e[1],w=e[2];
g[u].push_back({v,w});
g[v].push_back({u,w});
}

vector realizado largo tiempo cont(n+1,0);
vector implicado(n+1), tout(n+1);
int timer=0;

unordered_map se realizó larga,int contactos bordeW; // parent-consejochild weight

función recomendadavoid(int,int,long long) {}
dist[u]=d;
tin[u]=+timer;
for(auto [v,w]: g[u]) {}
si (v==p) continúan;
edgeW[key(u,v)] = w;
dfs(v,u,d+w);
}
tout[u]=timer;
};
dfs(1,0,0);

Fenwick fw(n);
vector significar uns
para(auto &q: consultas) {}
if(q[0]==1){ // update
int _,u,v,newW; tie(_,u,v,newW)=make_tuple(q[0],q[2],q[3]);
int child = (tin[u]
int parent = (child==v)? u : v;
long long longW = edgeW[key(parent,child)];
largo largo delta = nuevoW - viejoW;
fw.rangeAdd(tin[child], tout[child], delta);
edgeW[key(parent,child)] = newW;
}else{ // distance
int _,x; tie(_,x)=make_tuple(q[0],q[1]);
largo largo cur = dist[x] + fw.sum(tin[x]);
as.push_back(int)cur);
}
}
devolver los ans;
}
};
`` `

■ **Nota:**
* La solución utiliza "largo largo" para las sumas internas para evitar el desbordamiento cuando el entorno de perspectiva laboral cambia las limitaciones.
* `key()` empaca un par de 32 bits en una llave de 64 bits, perfecto para un `unordered_map`.

-...

## 🚀 Cómo presentar esta solución en una entrevista

1. **Mostrar el árbol es *estático* en la estructura** – se puede preprocesar una vez.
2. **Explicar el recorrido Euler** – todos los subárboles se convierten en segmentos contiguos.
3. **Explicar el truco Fenwick** – rango añadir a través de dos actualizaciones de puntos; la consulta es sólo una suma de prefijo.
4. **Stress the `O(log n)` per query** – meets the constraints.
5. **Las trampas de la mención** – por ejemplo, olvidando actualizar el mapa, o utilizando índices basados en 0 con un árbol Fenwick de 1 base.

-...

## 🔍 Common Pitfalls " Ugly " Quirks

Problema de la vida ¦
Silencio...
Silencio **Edge direction** Silencio Treat `(u, v)` y `(v, u)` como el mismo niño → padre. Silencio Determinar siempre al niño comparando `tin[u]` y `tin[v]`. Silencio
Silencio ** Índices de Fenwick** Silencios fuera por uno errores (utilizando 0 en lugar de 1). TENIDO Use `+timer` para el tiempo de entrada; `fw.sum(tin[x])`. Silencio
Silencio **Overflow** Silencio Usando `int` para sumas → resultados negativos en gráficos enormes. Silencio Use 'long' o 'long' en todas partes. Silencio
tención **Map key collisions** ← Utilizando `unordered_map seleccionadaint, intilo` on pair → hash collision. ← Pareja de paquete en 'long' o utilizar `map determinadapair madeint,intilo,int contacto `. Silencio
Silencio **Profundidad de la recusión** Silencio Rebosa de arrastre para árboles profundos. Silencio

-...

## 📌 Takeaway

* **Preprocesamiento + array de diferencia + Tour Euler = elegante y eficiente. #
* El método es **language‐agnostic** – se puede adaptar a Java, Go, Rust, etc.
* En un trabajo-interview, siempre *justifique* cada elección de diseño y **anticipe las preguntas del entrevistador** sobre la complejidad, la memoria y los casos de borde.

¡Buena suerte! 🎯