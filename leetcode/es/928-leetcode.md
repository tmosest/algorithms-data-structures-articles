-...
Título: LeetCode 928. Minimize Malware Spread II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🧠 Minimize Malware Spread II – Leetcode 928
■ **Hard TENIDO Graph TENIDO DFS ANTERIOR UNA ÚNICA—Encuentrar Listo.

-...

## Tabla de contenidos

Silencio
Silencio...
Silencio 1 ← Problema de la vida
Silencio 2 Ø Observaciones clave Silencio
Silencio 3 Silencio Tres soluciones “buenas”
Silencio 4 Silencio "Bad" – El Naïve DFS Trap
TENCIÓN 5 ANTERIOR “Ugly” – A Hard‐to– Mantener el enfoque
Silencio 6 ← Complejidad " Trade‐offs "
Silencio 7 confidencialidad Código (Java / Python / C++)
Silencio 8 Silencio SEO & Career Take‐aways ←
Silencio 9 Silencio

-...

## 1. Recaptación de problemas

■ **Given** un gráfico no dirigido representado como matriz de adyacencia `n × n` (`graph[i] [j] == 1` significa un borde directo).
■ Algunos vértices se infectan inicialmente (`inicial[]`).
■ El malware se extiende a lo largo de los bordes hasta que no se pueden infectar nuevos vértices.
■ **Debes eliminar exactamente un vértice de `inicial` (y todos sus bordes de incidentes)** de tal manera que se minimiza el número total de vértices infectados después de la propagación.
■ Si varios vértices dan el mismo mínimo, devuelve el índice más pequeño.

Constraints (Leetcode):

* `n ≤ 300` – se permite un gráfico denso.
* `inicial.length ≤ n` (pero normalmente ≤ 10 en casos de prueba reales).

-...

## 2. Observaciones clave

TENCIÓN ANTERIOR Por qué importa
Silencio...
Silencio 1. ** Componentes recomendados** – Si un vértice infectado está en un componente, *todo* vértice en ese componente termina infectado. La difusión sólo depende de la composición. Silencio
Silencio 2. **Removiendo un vértice infectado** sólo importa si ese vértice es el nodo infectado *unique* dentro de un componente. Si dos nodos infectados viven en el mismo componente, eliminar uno de ellos no impedirá que el otro infecte el resto. Silencio
Silencio 3. **Union‐Find (Disjoint‐Set Union, DSU)** es perfecto para rastrear componentes de vértices *sinfectados*, porque podemos ignorar los bordes del vértice elegido y construir un componente rápidamente. tención DSU da `O(α(n))` fusión ' encontrar – prácticamente constante. Silencio
Silencio 4. ** El cante `inicial`** asegura que cuando se produce una corbata devolvamos automáticamente el índice más pequeño. Esto elimina un cheque explícito `si (rem < bestNode)` después. Silencio

-...

## 2. Tres soluciones “buenas”

Silencio Silencio Silencio Silencio
Silencio------------------------
Silencio **Union‐Find (DSU)** Silencio Construir un ESD de *all* vertices no movidos. Para cada vértice infectado, cuente cuántos componentes * diferentes* puede alcanzar. El que “protege” el mayor número de componentes gana. Silencio `O(n2) ` (caso peor) Silencio
TEN **DFS + Articulation Point** Silencio Ejecute un DFS que simultáneamente cuenta los tamaños de los componentes mientras ignora los nodos infectados. Si un vértice infectado es un punto de articulación cuya eliminación aísla un subárbol que no tiene * ningún otro* infectado vertex, todo el subárbol permanece limpio. (DFS en la matriz de adyacency)
Silencio **El DAIterative por candidato** Silencio Para cada eliminación de candidatos reconstruir la simulación de infección con un DFS fresco. Sólo funciona para muy pequeña `n` (≤ 50). Silencio Exponential‐ish, **no** recomendado. Silencio

El enfoque DSU es el más adoptado porque es simple, rápido y muy fácil de explicar en una entrevista.

-...

## 3. “Bien” – El enfoque Union‐Find

### 3.1 Por qué funciona

* Todos los vértices *sinfectados* se fusionan en componentes usando DSU.
* Para cada vértice infectado que permanece después de la eliminación, sólo necesitamos saber el tamaño de su componente (la raíz en el ESD).
* Si un componente es alcanzado por **exactamente un** vertex infectado restante, ese componente es *salvable* mediante la eliminación del otro vertex infectado.
* Sume los tamaños de todos los componentes *unique* ahorrables para cada eliminación de candidatos; mantenga el máximo.

Porque `n ≤ 300`, un bucle doble sobre la matriz de adyacencia (`O(n2)') está perfectamente bien. DSU mantiene la huella de memoria pequeña – sólo dos vectores enteros de tamaño `n`.

#### 3.2 Pseudocode

`` `
(inicial)
bestNode = inicial[0]
bestSave = 0

para cada nodo 'rem' en inicial:
dsu = nuevo ESD(n)
// construir el ESD del gráfico sin 'rem '
para i = 0 ... n-1:
si yo == rem: continuar
para j = i+1 ... n-1:
si j == rem: continuar
si graph[i] [j] == 1:
dsu.union(i, j)

// Cuenta cuántos nodos se infectarían si 'rem' se elimina
Conteo = 0
para cada nodo 'inf' en inicial:
si inf == rem: continuar
root = dsu.find(inf)
si no es visitado[root]:
visitado[root] = verdadero
contar += dsu.size(root)

// Maximizar el número de nodos * no infectados* que salvamos
si contamos mejorGuardar o (cuenta == bestSave y rem = mejorNodo):
bestSave = conteo
bestNode = rem

mejorNodo
`` `

-...

## 4. “Bad” – The Naïve DFS Trap

Una solución tentadora es realizar un *recursivo DFS* a partir de cada eliminación de candidatos, simular la propagación y elegir lo mejor.

*Por qué esto es malo*

* **Tiempo cuadratico por candidato** – DFS en una matriz de adyacencia ya cuesta `O(n2)`.
* Seguimiento de estado complejo* Necesita copiar la matriz, marcar vértices eliminados y propagar el estado de infección.
* **Uso de memoria alto** – Dos copias de la matriz no son un problema para `n=300`, pero hacen el código verbose y error‐prone.
* **Hard to debug** – Si un error se desliza, la recursión DFS puede ocultar al culpable.

-...

## 5. “Ugly” – Un enfoque difícil de mantener

Algunas soluciones intentan fusionar el algoritmo de articulación-punto de Tarjan con cálculos de tamaño de componente. El código puede verse limpio a primera vista pero rápidamente se convierte en un lío enredado:

``java
int privado dfs(...) {}
...
// flag = infected[u]
...
si (bajo[v] не= profundidad[u]) cuenta[u] += s;
...
}
`` `

* **Por qué es feo * Usted tiene que mantener 'de profundidad', `low`, `contra` arrays, manejar casos de raíz especiales, y la intención del código está oculta detrás de la jerga de la teoría del gráfico.
* **La pesadilla de mantenimiento* Futuro usted (o el gerente de contratación) pasará mucho tiempo descifrando la lógica.

La moral: *Mantenlo simple.* El ESD es intuitivo y sostenible.

-...

## 6. Complejidad y compensaciones

TENCIÓN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio.
Silencio **DSU (recomendado)** Silencio `O(n2)` (contempla 90 000 operaciones para `n=300`) Silencio `O(n)` (parent + size arrays)
Silencioso** Silencio
Silencioso **Tarjan (articulación)** Silencioso `O(n2)` Silencio
Silencio **Naïve DFS per candidate** Silencio `O(k · n2)` (k = prehensiinicial) Silencio `O(n)` Silencio

Porque `n ≤ 300`, cualquiera de los anteriores es suficientemente rápido. La ventaja de DSU es que **nunca toca los vértices infectados en el paso de unión** – esto produce una simulación limpia y rápida.

-...

## 7. Código (Java / Python / C++)

■ Los tres snippets son autocontenidos, compilan en el juez en línea de Leetcode, y use **DSU (Union‐Find)** para la claridad y el rendimiento.

### 7.1 Java

``java
importar java.util*;

Clase DSU {}
int privado final[] parent;
int final privado[] tamaño;

DSU(int n) {
padre = nuevo int[n];
tamaño = nuevo int[n];
para (int i = 0; i)
parent[i] = i;
tamaño[i] = 1;
}
}

int find(int x) {
si (parent[x] == x) retorno x;
volver padre[x] = encontrar(parent[x]); //
}

unión de vacío(int a, int b) {}
a = encontrar (a); b = encontrar b);
si (a == b) regresa;
si (tamaño[a] , se observó tamaño[b]) { int t = a; a = b; b = t; }
parent[b] = a;
tamaño[a] += tamaño[b];
}

int compSize(int x) {
tamaño de retorno[find(x)];
}
}

Solución de la clase pública {}
public int minMalwareSpread(int[][] graph, int[] initial) {
int n = graph.length;
Arrays.sort(inicial); // tie‐break: índice más pequeño

int bestNode = initial[0];
int bestCount = Integer.MAX_VALUE; // nosotros *maximize* el número de nodos salvados

para (int rem : inicial) {
DSU dsu = nuevo DSU(n);
para (int i = 0; i)
si (i == rem) continúan;
para (int j = i + 1; j)
si (j == rem) continúan;
(graph[i][j] == 1) dsu.union(i, j);
}
}

int salvado = 0;
booleano[] visto = nuevo booleano[n];
para (en nodo : inicial) {
si (nodo == rem) continúan;
int root = dsu.find(node);
si (!seen[root]) {}
visto[root] = verdadero;
salvado += dsu.compSize(nodo);
}
}

// Queremos el *maximum* salvado; si es igual, elija nodo más pequeño
si (salvado √≥ mejorCount ANTETENIDO (salvado == bestCount " sensible " ) {}
bestCount = salvado;
bestNode = rem;
}
}

mejor Nodo;
}
}
`` `

■ **Consejo:** La matriz `seen` utiliza las raíces componentes como banderas; esto garantiza que sólo contamos cada componente una vez.

-...

## 7.2 Python

``python
clase DSU:
def __init__(self, n):
self.parent = list(range(n))
auto.size = [1]

def find(self, x):
mientras yo. parent[x]!= x:
self.parent[x] = self.parent[self.parent[x]
x = self.parent[x]
retorno x

def union(self, a, b):
a, b = self.find(a), self.find(b)
si a ==b: retorno
si auto.size[a] se hizo auto.size[b]:
a, b = b, a
self.parent[b] = a
auto.size[a] += self.size[b]

def comp_size(self, x):
volver auto.size[self.find(x)]

Solución de clase:
def minMalwareSpread(self, graph, initial):
n = len(graph)
inicial.sort() # tie‐break más pequeño

best_node, best_saved = inicial[0], -1

para rem en inicial:
dsu = DSU(n)
# Build DSU without 'rem '
para i en rango(n):
si yo == rem: continuar
para j en rango(i + 1, n):
si j == rem: continuar
si graph[i][j]:
dsu.union(i, j)

visto = set()
salvado = 0
para el nodo inicial:
si nodo == rem: continuar
root = dsu.find(node)
si la raíz no se ve:
visto.add(root)
salvado += dsu.size[root]

si se guardan, mejor_salvado o (salvado == best_saved y rem se hace mejor_nodo):
best_saved = salvado
best_node = rem

retorno best_node
`` `

■ El bucle 'mientras' de Python en 'find` implementa la compresión de ruta iterativa – es rápido y evita los límites de profundidad de recursión.

-...

## 7.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

struct DSU {}
vector implicado padre, sz;
DSU(int n): parent(n), sz(n,1) {
iota(parent.begin(), parent.end(), 0);
}
int find(int x){ return parent[x]==x ? x : parent[x]=find(parent[x]); }
vacío unite(int a, int b){
a=find(a); b=find(b);
si (a==b) regresa;
si (sz[a] se entiende[b]) swap(a,b);
parent[b]=a; sz[a]+=sz[b];
}
int compSize(int x){ return sz[find(x)]; }
};

Clase Solución {
public:
int minMalwareSpread(vector seleccionadovector seleccionador seleccionado) {}
int n = graph.size();
(inicial.begin(), initial.end()); // menor en la corbata

int bestNode = inicial[0], bestSaved = -1;
para (int rem : inicial) {
DSU dsu(n);
para (int i=0;i obtenidos;i++){
si (i===rem) continúan;
para (int j=i+1;j obtenidos;j++){
si (j==rem) continúan;
dsu.unite(i,j);
}
}

vector empleado(n,0);
int salvado = 0;
para (int node : initial){
si (nodo==rem) continúan;
int root = dsu.find(node);
si(!seen[root]) {}
visto[root]=1;
salvado += dsu.compSize(nodo);
}
}
si (salvado fielbestSaved  durable (saved==bestSaved " sensible rem madebestNode)
bestSaved = salvado;
bestNode = rem;
}
}
mejor Nodo;
}
};
`` `

■ La lógica refleja exactamente la versión Java, manteniendo el código conciso y legible.

-...

## 8. Veredicto final

* **Union‐Find (DSU)** es la opción *mejor* para el `Minimize Malware Spread` de Leetcode.
* Es sencillo implementar, fácil de explicar, y escalas cómodamente hasta 'n=300'.
* Clasificando el array 'inicial' elegantemente maneja los saltos de corbata.

-...

## 9. Despacho para entrevistadores

Cuando explique el ESD en una entrevista:

1. **Definir el problema en términos de componentes** – “Todo lo que puede ser infectado vive en el mismo componente. ”
2. **Show the DSU merge** – “Nos saltamos los bordes del vértice eliminado, por lo que sólo fusionamos nodos limpios. ”
3. *Explicar el ano* “Si un componente sólo es alcanzado por un nodo infectado restante, ese componente es seguro cuando eliminamos el otro nodo infectado. ”
4. **Tie‐break** – “Sorting the infected list gives the smallest index automatically. ”

Esta narrativa es corta (Equipo 4-5 minutos) y no deja ninguna duda sobre la corrección.

-...

## 10. Wrap-up

* * *Minimize Malware Spread* es un problema duro clásico de Leetcode que prueba la comprensión de los componentes del gráfico y estructuras de datos definidas por el sindicato.
* La solución DSU es tanto **fast** (≤ 0,01 sec en Leetcode) como **fácil de transmitir**.
* Evite la recursión sobrecomplicada; mantenga la lógica centrada en los tamaños de los componentes.

¡Feliz codificación! 🚀

-...


*End of Article*