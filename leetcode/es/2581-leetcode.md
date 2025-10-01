-...
Título: LeetCode 2581. Número de cuentas de posibles nodos de raíz -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 2581 – Número de cuentas de posibles nodos de raíz
**Hard vivir Graph / Tree  durable DFS / Hashing**

■ **TL;DR** –
■ Construya una búsqueda rápida para los bordes entre padres e hijos adivinados, haga un DFS para contar cuántas adivinaciones son correctas si el árbol está arraigado en el nodo 0, luego haga un segundo DFS que "reroots" el árbol. Cada vez que movemos la raíz a través de un borde actualizamos el número de adivinaciones correctas en *O(1)*. La respuesta es el número de nodos cuyo recuento ≥ *k*.
■ Complejidad: **O(n + m)** tiempo, **O(n + m)** memoria.

A continuación encontrará tres implementaciones de producción (Java, Python, C++) y un blog de bloque completo que es SEO-optimizada para las palabras clave **létcode 2581**, **Adivina de raíz de árbol**, **DFS**, ** programación competitiva**, etc.

-...

#### 🔍 Problema de Restatement

Se les da:

TENIDO ANTERIOR ANTERIOR Descripción
Silencio...
TENIENDO `edges` TENIDO `n‐1` bordes no redirigidos de un árbol (`0 ≤ nodo < n`). Silencio
TENIENDO `asesina' Silencio Cada conjetura es un *ordenado* borde `[u, v]` significado "**u es el padre de v**". Cada conjetura está garantizada a ser un borde real del árbol y todas las conjeturas son únicas. Silencio
Bob sostiene que al menos 'k' de sus conjeturas son correctas para la raíz (no conocida) del árbol. Silencio

**Retorna el número de nodos que podrían ser la raíz de un árbol que satisface la afirmación de Bob. #

-...

### 📦 Observaciones clave

1. **Root Choice es sólo una reorientación del árbol* *
Si escogemos cualquier nodo como una raíz temporal (por ejemplo 0) podemos calcular cuántas conjeturas son correctas. Cuando “movemos” la raíz a través de un borde `(p, c)` sólo necesitamos actualizar el conteo localmente:
* Si la suposición `[p, c]` está en el conjunto, se convierte en **wrong** para la nueva raíz.
* Si la suposición `[c, p]` está en el conjunto, se convierte en **correcto para la nueva raíz.

2. ** Hash Set for Quick Lookup* *
Almacene cada conjetura como una clave de 64 bits `u * n + v ' (o una cadena `'u#v'` en Java/Python) para que podamos consultar `O(1)` si un borde dirigido es una suposición.

3. **Dos Traversales DFS* *
* **DFS1** – Root at 0, compute initial `correct` count.
* **DFS2** – Propagar los conteos a todos los nodos re-arraigando a lo largo de los bordes, utilizando la regla anterior.
El número de nodos con "correcto " es la respuesta.

-...

### 📘 Code Walk‐through (Java)

``java
importar java.util*;

Clase Solución {
// codificar un borde dirigido (u, v) en una llave larga
llave larga privada (int u, int v, int n) {
(long) u) * n + v;
}

int public int rootCount(int[] edges, int[][]dives, int k) {
int n = edges.length + 1; // número de nodos
Lista realizadaInteger() g = nuevo ArrayList[n];
para (int i = 0; i) no; i++) g[i] = nuevo ArrayList recomendado();

// construir lista de adjacency
para (int[] e : bordes) {
g[e[0].add(e[1]);
g[e[1]].add(e[0]);
}

// conjunto de bordes dirigidos adivinados
HashSet Garantizado();
para (int[] gk : suposiciones) {}
(key(gk[0], gk[1], n));
}

--------- DFS1 : contar correctamente suposiciones cuando se enraiza en 0 ----------
int[] correct = nuevo int[1];
boolean[] vis = new boolean[n];
dfsCount(0, -1, g, guessSet, correct, n);
int base = correcto[0]; // correctas suposiciones para root 0

--------- DFS2 : propagar la cuenta correcta a cada nodo --------
int[] response = new int[1];
dfsReRoot(0, -1, g, guessSet, base, k, response, n);
respuesta de retorno[0];
}

// helper DFS para calcular la base correcto
vacío privado dfs Conde(int u, int parent,
Lista de datos g,
HashSet significaba:
int[] correct, int n) {
para (int v : g [u]) si (v != padre) {
si (guessSet.contains(key(u, v, n))) correcto[0]++; // u es padre de v
dfsCount(v, u, g, guessSet, correct, n);
}
}

// helper DFS para re-root y contar raíces válidas
dfsReRoot(int u, int parent,
Lista de datos g,
HashSet significaba:
int curvoCorrecto, int k,
int[] respuesta, int n) {
[0]++;

para (int v : g [u]) si (v != padre) {
int nextCorrect = curCorrect;

// El borde (u,v) se convierte en niño- padre, por lo que:
// - si adivina [u- títulov] era correcto, perdemos uno
si el siguiente Correct...

// - si adivina [v- títulou] es correcto, ganamos uno
(guessSet.contains(key(v, u, n)))) siguienteCorrect++;

dfsReRoot(v, u, g, guessSet, nextCorrect, k, answer, n);
}
}
}
`` `

■ *Por qué es rápido*
■ Cada borde se visita dos veces (una vez en cada DFS). Todas las miradas son constantes porque usamos un `HashSet`.
■ Memory: adjacency list `O(n)`, guess set `O(m)`.

-...

### 🐍 Python Implementation

``python
de las colecciones importadas por defecto
de la importación Lista

Solución de clase:
def rootCount(self, edges: List[List[int],
conjeturas: List[List[int],
k: int) - título int:
n = len(edges) + 1
g = defaultdict(list)
para a, b en los bordes:
g[a].append(b)
g[b].append(a)

# encode directed edge (u,v) - collar "u#v"
guess_set = {"#".join(map(str, gk)) for gk in guesses}

# DFS1: Contar correctamente adivinaciones cuando root = 0
def dfs_count(u, p):
cnt = 0
for v in g[u]:
si v == p: continuar
si...
cnt += 1
cnt += dfs_count(v, u)
retorno cnt

base = dfs_count(0, -1) # correctas suposiciones para el nodo 0

# DFS2: reroot and count valid nodes
ans = 0
def dfs_reroot(u, p, cur):
no local
si cur >= k:
ans += 1
for v in g[u]:
si v == p: continuar
nxt = curtido
si...
nxt -= 1
si f"{v} "indiv_set:
nxt += 1
dfs_reroot(v, u, nxt)

dfs_reroot(0, -1, base)
Retorno
`` `

■ La misma lógica DFS de dos pasos se aplica. La clave de codificación utiliza una cuerda simple; para 1 e5 nodos una tecla de cuerda sigue siendo cómodamente rápida en CPython.

-...

### 🧱 C++ Implementation

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
// codificar borde dirigido (u,v) como un entero de 64 bits
static inline long key(int u, int v, int n) {
retorno 1LL * u * n + v;
}

int rootCount(vector seleccionadovector identificadoint
vector asignador implicados iguales adivinaciones,
int k) {
int n = edges.size() + 1;
vector realizador:
para (auto &e : bordes) {}
g[e[0].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

unordered_set obtenidos largo Supongo. Set;
para (auto &gk : suposiciones)
suposiciónSet.insert(key(gk[0], gk[1], n));

// -------- DFS1: base correcta adivinanzas para root -------
vector:
int base = dfsCount(0, -1, g, guessSet, n);

------- DFS2: propagar cuentas --------
int ans = 0;
dfsReRoot(0, -1, g, guessSet, base, k, ans, n);
devolver los ans;
}

privado:
int dfs Conde(int u, int p,
const vector identificador g,
const unordered_set Set,
int n) {
int cnt = 0;
para (int v : g[u]) si (v != p) {}
cnt++;
cnt += dfsCount(v, u, g, guessSet, n);
}
cnt de retorno;
}

vacío dfsReRoot(int u, int p,
const vector identificador g,
const unordered_set Set,
int curvoCorrecto, int k,
int
si (correcta >= k) ++ans;
para (int v : g[u]) si (v != p) {}
int nextCorrect = curCorrect;
(guessSet.count(key(u, v, n)))) --nextCorrect; // lost
(guessSet.count(key(v, u, n)))) ++nextCorrect; // won
dfsReRoot(v, u, g, guessSet, nextCorrect, k, ans, n);
}
}
};
`` `

-...

#### 📈 Complexity > Por qué importa

TENIDO MEDIO TENIDO Fórmula TENIDO Ejemplo TENIDO Por qué importa
Silencio------------------------------------- La vida eterna
Silencio **Tiempo** Silencio `O(n + m)` Silencio ~200 k operaciones para 1e5 nodos Silencio Confortablemente bajo 1 s en LeetCode Silencio
Silencio **Memoria** Silencio `O(n + m)` Silencio ~1.5 MB para la adyacencia + ~2 MB para las conjeturas Silencio Dentro de 256 MB límite Silencio

■ **Edge‐Case** – Si `k == 0` la respuesta es `n` (todo nodo satisfies "al menos 0 adivinaciones correctas").
■ **Edge‐Case** – Si las preguntas están vacías, la respuesta es `n` también.

-...

### 📚 Blog Post (SEO‐Ready)

■ *Título* 2581 – Número del número de posibles nodos de raíz DFS Solution
■ **Descripción de datos**: Solve LeetCode 2581 (hard) con una solución O(N) DFS limpia en Java, Python y C++. Aprenda a desarraigar un árbol, usar el arañazo para adivinar, y contar raíces válidas en tiempo lineal.

-...

##### 1. Introducción

LeetCode’s 2581 “Count Number of Possible Root Nodes” es un clásico árbol-problema que a menudo viaja hacia los principiantes porque mezcla ** bordes no dirigidos** con ** adivinaciones ordenadas**. La clave para una solución rápida es un DFS de dos pasos que *reroots* el árbol. En este artículo verá:

* Problema re-frasado para la claridad
* Una implementación completa y lista para la producción en **Java**, **Python**, y **C+**
* Una prueba paso a paso de la corrección
* Análisis de complejidad
* trampas comunes y “gotchas”
* Casos de prueba de muestras

Si usted es un programador competitivo, un reclutador, o sólo un fan LeetCode, las ideas aquí aumentarán tanto su velocidad de codificación como su rendimiento de entrevista.

-...

##### 2. Sinopsis de problemas

Dado un árbol de nodos, `m` ordenadas suposiciones ``[u, v]` ( ' es padre de v ' ), y un entero `k`, debemos contar cuántos nodos podrían ser la raíz de tal manera que al menos 'k' suposiciones son correctas.

Principales limitaciones:

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio...
TENIDO `1 ≤ n ≤ 10^5` TENIDO hasta 100k nodes TENIDO
TENIDO `0 ≤ m ≤ 10^5`
Silencioso `0 ≤ k ≤ m`

Todos los bordes son únicos, el árbol está conectado, y cada conjetura es un verdadero borde dirigido del árbol.

-...

##### 3. Intuición

1. **Root es un Mirador** – Arreglar cualquier nodo como raíz temporal (nodo 0). El árbol se convierte en un árbol dirigido arraigado.
2. **El conde de Correcta es local** – Cuando movemos la raíz de padre " p " a niño " a lo largo del borde " (p,c) " sólo dos bordes dirigidos cambian de estado:
*[p,c]` pérdida de corrección
*[c,p]` puede ganar corrección
3. **Hash Set for Constant‐Time Query** – Guarda todas las conjeturas en un conjunto de bordes dirigidos.
4. **Dos DFS** –
* **DFS‐Base**: Contar correctamente suposiciones para la raíz arbitraria.
* **DFS‐Reroot**: Camine el árbol de nuevo, actualice el conteo localmente, y cuente nodos cuyo conteo ≥ `k`.

-...

##### 4. Algoritm

`` `
1. Construir la lista de adyacencia del árbol.
2. Almacene todas las adivinanzas dirigidas en un set de hash (u * n + v) // 64‐bit key
3. DFS1: root at node 0
- Por cada niño v de u, si adivina [u- títulov] en el set - ratio ++correct
- Acumular con precisión las adivinanzas correctas
- correcta[0] = base correcta cuenta para root 0
4. DFS2: re-root el árbol
- Comience en el nodo 0 con curCorrecto = base
- Por cada borde (u,v) (u padre, v hijo)
siguienteCorrecto = curvaCorrecto
si adivina [u- confíav] siguienteCorrecto...
si adivina[v-]u - No. siguienteCorrecto++
- Recusarse en niño v con siguienteCorrecto
- Cada vez que se corrige ≥ k, respuesta de aumento
5. Respuesta de retorno
`` `

**Proof of Correctness* *

*Lemma 1* – En un árbol enraizado, una suposición `[u,v]` es correcto **iff** `u` es el padre de `v`.
*Proof*: La consecuencia directa de la definición. ∎

*Lemma 2* – Cuando trasladamos la raíz de " p " a su hijo " , el número de conjeturas correctas sólo cambia a la mayoría de 1 por cada uno de los dos bordes dirigidos " (p,c) " y " c, p) " .
*Proof*:
- La conjetura `[p,c]` (si está presente) era correcta cuando `p` era padre; después de rerooting `c` se convierte en padre, por lo que se equivoca → disminución en 1.
- La suposición: (si está presente) se vuelve correcto → aumento por 1.
No hay cambios de estado de otros bordes. ∎

*Teorema* – Después de DFS2, por cada nodo `x` la variable `curCorrect` equivale al número de conjeturas que serían correctas si `x` fuera la raíz.
*Proof*: Por inducción sobre el traversal DFS2. Funda base: root 0 ya satisfies theorem. Paso inductivo: asumir teorema sostiene para el padre 'p'. Para el niño `c` computamos `nextCorrect` exactamente como describe Lemma 2, por lo que el teorema sostiene por `c`. ∎

Debido a que el algoritmo cuenta todos los nodos con `curecto ≥ k`, la respuesta final es correcta.

-...

##### 5. Análisis de la complejidad

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio Construir la lista de adyacencia Silencio
← Construir conjetura establecido Silencio `O(m)` Silencio
Silencio DFS1 Silencioso `O(n)` Silencioso `O(n)`
Silencio DFS2 Silencioso `O(n)` Silencioso `O(n)`
Silencio **Total** Silencioso `O(n + m)`

Ambos pases son lineales, por lo que la solución funciona cómodamente bajo los límites típicos del tiempo LeetCode.

-...

##### 6. Aspectos destacados de la aplicación

*Java*
- Usa la tecla " larga " ( " 1L * u * n + v " ) para evitar colisiones.
- `ArrayList madeint[] confía` for adjacency; `HashSet madeLong confianza` for guesses.
- Dos métodos de ayuda.

*Python*
- Usa las teclas de cadena como "u#v" o integer de 64 bits; ambas son lo suficientemente rápidas.
- Recursive DFS con `sys.setrecursionlimit`.

*C++*
- Usos " noordened_set obtenidoslong " para preguntas O(1).
- función clave (u,v,n) para computar la clave de 64 bits.

-...

##### 6. Pitfalls comunes

1. **Codificación de llave inglesa** – Utilizar `u*10^5 + v` puede rebosar de 32 bits. Use 64-bit (`long').
2. **Desbordamiento de la tensión** – Profundidad de recidiva de Python 1000; aumento con `sys.setrecursionlimit(200000)`.
3. **Empty Guess Set** – Si `m == 0`, la respuesta es `n`. Maneja temprano si desea.
4. **k == 0** – Todos los nodos satisfacen el umbral; no hay necesidad de ejecutar DFS2 (optimizar si quieres).

-...

##### 6. Pruebas de muestra

``python
# Prueba 1: k=0 (trivial)
aseverar cuentaPosibleRootNodes(n=4, m=0, k=0) == 4

# Prueba 2: Cadena simple
# Tree: 1-2-3
# Adivina: [1,2], [2,3]
# k=1 - titulado sólo root 1 obras
asever countPossibleRootNodes(3, 2, 1, [(1,2),(2,3)] == 1

Test 3: Árbol estrella
# 1 conectado a todos los demás
# Adivina: (1,2),(1,3),(1,4),(2,1),(3,1),(4,1)
# k=3 - titulado todos los nodos satisfacen
aseverar cuentaPosibleRootNodes(5, 6, 3, ...) == 5
`` `

-...

##### 7. Takeaway

El truco de rearraigación DFS de dos pasos es un patrón poderoso para los problemas que implican contar propiedades direccionales en los árboles (por ejemplo, “tamaños de subárbol”, “profundidad máxima”, “sumo de profundidades”, etc.). Parlo con un hash set para consultas de tiempo constante, y tendrá una solución O(N) que pase incluso las restricciones más estrictas.

¡Feliz codificación y buena suerte en LeetCode 2581!

-...

##### 8. Referencias " Lectura ulterior "

* [Tree Rerooting Technique](https://cp-algorithms.com/graph/tree_dfs.html#rerooting)
* [Discusiones de LeetCode – 2581](https://leetcode.com/problems/count-number-of-possible-root-nodes/discuss/)
* [Competitive Programming 3 – Trees Section](https://cpbook.readthedocs.io/en/latest/trees.html)

-...

■ **Author**: *Tu nombre*, programador competitivo experimentado y entusiasta de LeetCode. Sígueme en Twitter @YourHandle para gemas más algoritmos.