-...
Título: LeetCode 2467. Most Profitable Camino en un árbol -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 2805 – “Most Profitable Path in a Tree”
** Solución completa en Java, Python y C+++ + un blog amigable con SEO**

-...

### 1. El problema (LeetCode 2805)

■ **Función de la firma**
" texto
másProfitablePath(edges: List[List[int]], bob: int, amount: List[int]) - título int
" `

Alice comienza en el nodo raíz de un árbol arraigado.
Bob comienza en un nodo dado `bob` y camina ** Hacia la raíz** (nodo `0`) – cada paso toma un segundo.
Mientras caminan, abren cada nodo que llegan y abren la puerta allí.
El *beneficio* de un nodo depende de quién llegue primero:

Silencio Orden de llegada ← El beneficio de Alice ¦
Silencio----------------------------
Silencio Alice first ⋅ `amount[i]` ¦
Silencio, Bob, primeramente, Silencio
TENIDA MUNDIAL tiempo TENIDO `amount[i]/2` TENIDO `amount[i]/2 `

Ambos agentes se detienen tan pronto como llegan a un nodo de hoja.
Regresar el beneficio máximo ** Alice puede recoger** eligiendo el mejor camino de hoja a hoja.

*Constraints*
- `1 ≤ ≤ 2·104` (n = número de nodos)
- `amount[i]` encaja en un entero firmado de 32 bits
- `edges` es un árbol válido

-...

## 2. Core Idea

1. **Construir una lista de adyacencia** para el árbol.
2. **Encontrar el camino único de Bob** desde su nodo de inicio hasta la raíz.
- Almacene para cada nodo el *paso* (timestamp) al que llega Bob (`bobDepth[node]`).
3. **SAS de la raíz** para Alice.
- En cada nodo determinar cuánto puede ganar Alice usando el "bobDepth" almacenado y su propia profundidad actual.
- Para los nodos de hoja, devuelve la puntuación acumulada.
- Para los nodos internos, explore recursivamente cada niño y mantenga la puntuación máxima.

El algoritmo funciona en **O(n)** tiempo y **O(n)** espacio auxiliar.

-...

## 3. Implementaciones de referencia

### 3.1 Java

``java
importar java.util*;

clase pública MostProfitable Camino
public static int mostProfitablePath(Listecto)List madeInteger confianza bordes, int bob, List woningInteger título) {
int n = amount.size();
Lista realizadaLista realizadaInteger título = nuevo ArrayList recomendado(n);
para (int i = 0; i < n; i++) graph.add(new ArrayList correctamente());

para (Lista realizadaInteger título e : bordes) {
graph.get(e.get(0)).add(e.get(1));
graph.get(e.get(1)).add(e.get(0));
}

// Encuentra el camino de Bob a la raíz (nodo 0)
int[] bobDepth = nuevo int[n];
Arrays.fill(bobDepth, -1);
Lista realizadaInteger título = nuevo ArrayList implicado();
encontrarPathToRoot(bob, -1, camino, gráfico);
para (int d = 0; d )

// DFS para Alice
dfsAlice(0, -1, 0, 0, graph, bobDepth, amount);
}

// backtracking DFS to collect Bob's path
encontrar booleano privadoPathToRoot(un nodo, padre int,
Lista de registro de entrada, Lista de registro de entrada, Lista de datos
si (nodo == 0) Retorno verdadero; // alcanzado raíz
para (int nb : graph.get(node) {
si (nb == parent) continúan;
path.add(node);
si (findPathToRoot(nb, node, path, graph))) regresan verdadero;
path.remove(path.size() - 1);
}
devolver falso;
}

// Alice's DFS – devuelve el máximo beneficio de este nodo hacia abajo
dfs estáticos privadosAlice(nodo, padre int, profundidad int,
int curScore, Lista seleccionadaLista Gráfico,
int[] bobDepth, List GarantizadoInteger título
// Puntuación actualizada basada en los tiempos de llegada
si (bobDepth[node] == -1 Silencioso bobDepth[node] √≥ profundidad) {
curScore += amount.get(node);
} si (bobDepth [node] == profundidad) {
curScore += amount.get(node) / 2;
}

// Si hoja, devuelve la puntuación actual
si (nodo != 0 " ritmo graph.get(nodo).size() == 1) volver cursillo;

int best = Integer.MIN_VALUE;
para (int nb : graph.get(node) {
si (nb == parent) continúan;
mejor = Math.max(mejor,
dfsAlice(nb, node, deep + 1, curScore, graph, bobDepth, amount));
}
devolver mejor;
}

// Envoltura simple para probar
public static void main(String[] args) {
Lista de datos bordes = Lista de (
Lista de(0,1), Lista de(1,2), Lista de(1,3)
);
Lista de(1,2,3,4);
System.out.println(mostProfitablePath(edges, 2, amount)); // Se prevé: 4
}
}
`` `

■ *Por qué funciona* *
" BobDepth [node] " tiendas en las que *time* Bob llega a `node`.
√≥ - Mientras nos cruzamos con profundidad 'a profundidad', podemos decidir si Alice llega primero, segundo o al mismo tiempo.
√ - La recursión explora todos los caminos root‐to‐leaf, manteniendo la mejor puntuación.

-...

#### 3.2 Python 3

``python
de la importación Lista
importadores
sys.setrecursionlimit(1

Solución de clase:
def mostProfitablePath(
self, edges: List[List[int], bob: int, amount: List[int]
) int:
n = len(amount)
graph = [[] for _ in range(n)]
para u, v en los bordes:
graph[u].append(v)
graph[v].append(u)

# La profundidad de llegada de Bob en cada nodo
bob_fund = [-1]
ruta = []

def dfs_bob(nodo: int, parent: int) Bool:
si nodo == 0:
Retorno
para nb en el gráfico [nodo]:
si nb == padre:
continuar
path.append(node)
si dfs_bob(nb, node):
Retorno
path.pop()
Retorno Falso

dfs_bob(bob, -1)
para d, nodo en enumerado(path):
bob_fund[nodo] = d

def dfs_alice(nodo: int, parent: int, deep: int, acc: int) - título int:
# Ajuste el beneficio basado en los tiempos de llegada
si bob_fund[nodo] == -1 o bob_fund[nodo]  profundidad:
acc += cantidad[nodo]
elif bob_fund[nodo] == profundidad:
acc += cantidad[nodo] // 2

# hoja
si nodo != 0 y len(graph[node]) == 1:
retorno acc

mejor = 10**18
para nb en el gráfico [nodo]:
si nb == padre:
continuar
mejor = máximo (mejor, dfs_alice(nb, nodo, profundidad + 1, acc))
mejor

devolver dfs_alice(0, -1, 0, 0)

Prueba rápida
si __name_ == "__main__":
bordes = [[0,1],[1,2],[1,3]]
cantidad = [1,2,3,4]
print(Solution().mostProfitablePath(edges, 2, amount)) # 4
`` `

-...

### 3.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int mostProfitablePath(vector seleccionadovector seleccionado) {
int n = amount.size();
vector realizador:
para (auto &e : bordes) {}
g[e[0].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

// La profundidad de Bob en cada nodo (tiempo de llegada)
vector asignadoint espíritu bobDepth(n, -1);
vector llamado camino de confianza;
función recomendadabool(int,int) título dfsBob = [ cl](int node, int parent) - título bool
si (nodo == 0) Retorno verdadero; // alcanzado raíz
para (int nb : g[nodo]) {}
si (nb == parent) continúan;
path.push_back(nodo);
si (dfsBob(nb, node)) regresan verdaderos;
path.pop_back();
}
devolver falso;
};

dfsBob(bob, -1);
para (int d = 0; d );

función realizada(int,int,int,long long) dfsAlice = [ю](int node, int parent, int deep,
long long acc) - título int {
si (bobDepth[node] == -1 Silencioso bobDepth[node] √≥ profundidad) {
acc += amount[node];
} si (bobDepth [node] == profundidad) {
acc += amount[node] / 2;
}

// hoja
si (nodo != 0 " п g[node].size() == 1) retorno (int)acc;

int best = INT_MIN;
para (int nb : g[nodo]) {}
si (nb == parent) continúan;
mejor = máximo (mejor, dfsAlice(nb, nodo, profundidad + 1, acc));
}
devolver mejor;
};

dfsAlice(0, -1, 0, 0);
}
};

/ Demo
int main() {}
vector realizador obtenidosint títulos = {0,1},{1,2},{1,3};
vector cantidad = {1,2,3,4};
cout se realizó Solución().másProfitable Path(edges, 2, amount)
}
`` `

-...

## 4. SEO‐Friendly Blog Post

■ **Meta Descripción**
■ Solve LeetCode 2805 “Most Profitable Path in a Tree” con una solución O(n) DFS.
■ Obtenga el código de referencia Java, Python y C++, además de consejos de entrevista y análisis de complejidad.

-...

# Sendero Profitable en un Árbol – El LeetCode Definitivo 2805 Caminen

■ **Key tags:** *LeetCode, Most Profitable Path, tree traversal, DFS, interrogante, entrevista de codificación, Python, Java, C++ *

-...

## 🎯 Why This Problem Rocks

- **Real interview staple:** aparece en entrevistas tecnológicas de alto nivel (Google, Amazon, Microsoft).
- **Tree + DP + codicioso** – prueba su comprensión de la búsqueda profunda y el estado basado en el tiempo.
- **Multi‐language** – muestra que puede implementar la misma lógica en Java, Python y C++.

-...

Problema Recap

Alice comienza en el nodo `0`.
Bob comienza en el nodo 'bob' y camina ** Hacia la raíz**.
Cada agente obtiene ganancias de un nodo dependiendo de quién llega primero.
Ambos paran en una hoja.
Devuelve el máximo beneficio que Alice puede lograr.

-...

Estrategia de solución

1. ** Lista de adyacencia** – construir una vez, O(n).
2. ** El camino de Bob a la raíz** – el árbol garantiza un camino único.
- Camina con recorsión de `bob` a `0`, registrando la profundidad en la que Bob llega a cada nodo (`bobDepth[node]`).
3. ** El DFS de Alice** – desde la raíz, siga su profundidad actual.
- Compare ` profunda' con `bobDepth[node]` para decidir el beneficio en ese nodo.
- En los nodos de hoja, devolver la puntuación acumulada; en los nodos internos, explorar todos los niños y mantener el máximo.

El truco: *ambos* agentes se mueven a la misma velocidad, por lo que el *de profundidad* del nodo en un DFS corresponde exactamente al tiempo transcurrido.

-...

## 📈 Complexity Analysis

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio Construir la lista de adyacencia Silencio **O(n)** Silencio **O(n)**
Silencio El camino de Bob DFS Silencio **O(n)** Silencio **O(n)** (paquete)
TENIDO EL DFS de Alice **O(n)** Silencio **O(n)** (Apilación de recusión)

En general: **O(n)** tiempo, **O(n)** espacio.
Con `n ≤ 20.000`, profundidad de recursión ≤ 20.000 – seguro en la mayoría de las plataformas modernas (Python: `sys.setrecursionlimit`, C++: `-Wl,--stack` si es necesario).

-...

## Pitfalls comunes

Silencio Pitfall Silencio Cómo evitar
Silencio...
Silencio **Uso de una variedad de booleanos para visitar** Silencio Dado que el árbol tiene una relación padre-hijo única, simplemente puede pasar el nodo padre en lugar de un conjunto visitado. Silencio
Silencio **El redondeo de la división entero** Silencio `amount[i]` está garantizado a ser incluso cuando se divide por 2 en el caso del mismo tiempo, pero el uso de la división entero (`// 2` en Python, `/ 2` en Java/C++) es seguro. Silencio
← Profundidad de Bob vs. Profundidad de Bob** Silencio Recordar que ` profunda` es la distancia actual de Alice desde la raíz, mientras que `bobDepth` almacena la llegada de Bob *time*. Silencio
* Detección de hoja para nodos 0** Silencio Nodo `0` puede tener sólo un vecino pero es **no** una hoja; la condición `nodo != 0 " graph[node].size() == 1` arregla esto. Silencio

-...

## 🏁 Código completo (Todos los idiomas)

Silencio Idioma Silencio Nombre del archivo Silencio Highlights Silencio
Silencio----------------------------
Silencio **Java** Silencio `MostProfitablePath.java` TENIDO Usos `Lista realizadoLista realizadoInteger confianza `` para adjacency, `Arrays.fill`, and `Math.max`. Silencio
Silencio **Python** Silencio `solución.py`  durable Recursive DFS with `sys.setrecursionlimit`. Silencio
tención **C++** Silencioso `Solution.cpp` Silencio Usos `vector seleccionadovector fieltro' y lambda recursion. Silencio

-...

## 5. Consejos de entrevista

1. **Clarificar la regla de “parar en la hoja”** – tanto Alice como Bob terminan en la hoja *primera* que golpean.
2. **Declarar la suposición** de que el árbol está arraigado en `0` (por convención).
3. **Explicar el array de profundidad de Bob** en su respuesta – es la clave para la solución O(n).
4. **La complejidad de la mención**; los entrevistadores aman la concisa Big‐O.
5. ** Casos de borde de discusión**: nodo único, Bob ya en la raíz, los valores negativos de 'montaje' (se permiten si su código los maneja).

-...

## 6. Resumen

Silencio Silencio Silencio Silencio Silencio Silencio Silencio
Silencio----------------------------
TEN Java TENIDO O(n) TENIDO O(n) TENIDO Profundidad de recuperación ≤ 20,000 – seguro si `setRecursionLimit` no es un problema. Silencio
Silencio Python Silencio O(n) Silencio O(n) Silencio Uso `sys.setrecursionlimit` para árboles grandes. Silencio
TENIDO C++ TENIDO O(n) TENIDO O(n) TENIDO Apilación iterativa opcional, pero la recursión es más clara. Silencio

■ **Bottom line:** El truco es ** pre-computar los tiempos de llegada de Bob** y luego realizar un *single* DFS para Alice que propaga la mejor puntuación.
■ Esto convierte un problema aparentemente complejo “dos agentes que se mueven simultáneamente” en un problema clásico *root‐to‐leaf máximo de ruta*.

¡Feliz codificación y buena suerte rompiendo ese problema de LeetCode! 🚀