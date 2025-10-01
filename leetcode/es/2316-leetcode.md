-...
Título: LeetCode 2316. Contar pares inalcanzables de ganglios en un gráfico no dirigido -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## ✅ 2316 – Count Unreachable Pairs of Nodes in an Undirected Graph

**LeetCode URL:** https://leetcode.com/problems/count-unreachable-pairs-of-nodes-in-an-undirected-graph/

■ Se le da un gráfico no dirigido con nodos (0 ... n-1) y una lista de bordes `edges`.
■ Devuelve el número de pares de nodos distintos que son *inalcanzables* unos de otros.

-...

#### TL;DR – El Bien, el Mal, el Ugly

Silencio Silencio Silencio Silencio Silencio Silencio
Silencio----------Prince------
Problema de la vida ¦ Problema clásico “compuestos conectados” problema → Solución de 2 puntos / DSU TEN La gravedad puede ser enorme (`n = 10^5`, `edges = 2·10^5`) – ingenua O(n2) está muerto Silencio Necesitas evitar el desbordamiento entero (`long`) y apilar el desbordamiento en DFS ANTE
← Algorithm Silencio Union‐Find (Disjoint Set Union) → O(n + m) tiempo ← Re-using `List wonint[]]] ` in Java can cause GC overhead ← Utilizar la recursión para DFS puede soplar la pila en un gráfico profundo.
← Aplicación ← Utilizar DFS iterativa o Union‐Find Silencio `int[][]` → `ArrayList madeint[] `` overhead ← Utilizar siempre `long` para la respuesta, no `int’

-...

Soluciones

A continuación encontrará ** tres implementaciones idiomáticas** – una en Java, una en Python, y una en C++.
Todos utilizan la técnica **Union‐Find** (Disjoint Set Union, DSU), que es la forma más limpia y eficiente de contar los tamaños de componentes conectados y luego el número de pares inalcanzables.

¿Por qué DAA? #
* Uno pasa por todos los bordes.
* `find` + `union` son efectivamente *amortizado* O(α(n)) (inverse Ackermann) – prácticamente constante.
* No recursión → ningún riesgo de flujo de pila.
* Muy fácil de entender una vez que conoce el ESD.

-...

#### 1down⃣ Java (Bien, seguro de tipo, rápido)

``java
importar java.util*;

Solución de la clase pública {}
// -------- Union-Find------------
DSU de clase privada {}
int[] parent, size;
DSU(int n) {
padre = nuevo int[n];
tamaño = nuevo int[n];
para (int i = 0; i)
parent[i] = i;
tamaño[i] = 1;
}
}
int find(int x) {
mientras (x != parent[x]) { //
parent[x] = parent[parent[x];
x = parent[x];
}
retorno x;
}
unión de vacío(int a, int b) {}
int ra = find(a), rb = find(b);
si (ra == rb) regresa;
// unión por tamaño
si (tamaño[ra] {}
tmp = ra; ra = rb; rb = tmp;
}
parent[rb] = ra;
tamaño[ra] += tamaño[rb];
}
int componentSize(int x) { return size[find(x)]; }
}
--------- Solución...
public long countPairs(int n, int[] bordes) {
DSU dsu = nuevo DSU(n);
para (int[] e : bordes) {
dsu.union(e[0], e[1]);
}

ans largas = 0;
largo procesado = 0; // nodos ya contados
para (int i = 0; i)
si (dsu.parent[i] == i) { // root → tamaño del componente
long sz = dsu.size[i];
ans += procesados * sz;
procesado += sz;
}
}
devuelve ans; // cabe en largo porque n = 1e5 → pares max 5e9
}
}
`` `

**Las complejidades* *
*Time*: **O(n + m)** (α(n) ♥ 4)
*Espacio*: **O(n)** (dispositivos de tamaño de los padres)

-...

Python 3 (Elegant, listo para pasar)

``python
clase DSU:
def __init__(self, n: int):
self.parent = list(range(n))
auto.size = [1]

def find(self, x: int) - título int:
x != self.parent[x]:
self.parent[x] = self.parent[self.parent[x] # path compresión
x = self.parent[x]
retorno x

def union(self, a: int, b: int) - Ninguno.
ra, rb = self.find(a), self.find(b)
si ra == rb:
Regreso
si auto.size[ra] se hizo auto.size[rb]:
ra, rb = rb, ra
self.parent[rb] = ra
auto.size[ra] += self.size[rb]

Solución de clase:
def countPairs(self, n: int, edges: list[list[int]) - título int:
dsu = DSU(n)
para u, v en los bordes:
dsu.union(u, v)

ans = 0
procesados = 0
para i en rango(n):
si dsu.parent[i] == i: # raíz de un componente
sz = dsu.size[i]
ans += procesados * sz
procesado += sz
Retorno
`` `

**Por qué es “Python-friendly”* *
* No recursion → no `RecursionError`.
* Usa listas integradas " enteros " automáticamente.

-...

### 3down⃣ C++ (Performance-oriented, STL)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase DSU {}
public:
vector implicado padre, sz;
DSU(int n) : parent(n), sz(n,1) {
iota(parent.begin(), parent.end(), 0);
}
int find(int x) {
(x!= parent[x]) {}
parent[x] = parent[parent[x];
x = parent[x];
}
retorno x;
}
vacío unite (incluido a, int b) {}
int ra = find(a), rb = find(b);
si (ra == rb) regresa;
si (sz[ra] [rb]) swap(ra, rb);
parent[rb] = ra;
sz[ra] += sz[rb];
}
};

Clase Solución {
public:
largos largos conteoPairs(int n, vector asignadovector seleccionados) {}
DSU dsu(n);
dsu.unite(e[0], e[1]);

ans largos = 0;
larga duración procesada = 0;
para (int i = 0; i) {}
si (dsu.parent[i] == i) { // root
long sz = dsu.sz[i];
ans += procesados * sz;
procesado += sz;
}
}
devolver los ans;
}
};
`` `

■ **C++ Nota** – Use `long long` (`int64_t`) para la respuesta final.
■ Use `bits/stdc++.h` para velocidad pero siéntete libre de incluir `cantavector ``, `traducido noumeric ``, etc. para portabilidad.

-...

## 📚 Blog Article – “Cracking LeetCode 2316 for Your Next Interview”

■ *Título*
*“Cómo conquistar LeetCode 2316 – Contar de pares inalcanzables de nodos (Java, Pitón, C++)”*

■ **Meta Descripción**
■ Aprenda la solución DSU más rápida para LeetCode 2316, entienda los componentes conectados del gráfico y prepárese para su próxima entrevista tecnológica. Incluye código Java, Python y C++.

■ ** Palabras clave del foro* *
" LeetCode 2316 " , `Count Unreachable Pairs of Nodes`, `graph connected components`, `DFS vs Union Find ' , `Java graph algoritmo`, `Python DSU`, `C+++ gragraph interview ' , `tech interview prep`, `data structures`.

-...

### 1. Recaptación de problemas

Se te da:

- Nodos (0 ... n‐1)
- `edges` - una lista de bordes sin dirección

Usted debe contar **cuántas parejas sin orden de nodos distintos no tienen ningún camino entre ellos**.

■ **Por qué esto importa en entrevistas* *
■ 1. Demuestra la comprensión de los fundamentos del gráfico.
■ 2. Muestras que puedes optimizar para ** grandes tamaños de entrada** (105 nodos, 2·105 bordes).
■ 3. Prueba la familiaridad con **Union‐Find** (una estructura de datos clásica).

-...

### 2. Lo que realmente significa “inexistible”

Para cualquier gráfico, el número total de pares sin orden** de nodos es:

`` `
totalPairs = n * (n - 1) / 2
`` `

Si resta el número de pares **reachable** (es decir, pares que se encuentran dentro del mismo componente conectado), obtendrá la respuesta.

Para un componente de tamaño `s`, el número de pares alcanzables dentro es:

`` `
(s - 1) / 2
`` `

Por lo tanto:

`` `
inalcanzable Parejas = totalPairs - Governing(reachableInComponent)
`` `

-...

### 3. Algorithm 1 – Union‐Find (Unión de conjuntos de unión)

1. ** Initialize** `parent[i] = i ' and `size[i] = 1`.
2. **Iterate** sobre cada borde `(u, v)` y `union(u, v)`.
3. Después de todos los bordes, cada raíz `r` representa un componente conectado del tamaño `size[r]`.
4. **Computar** la respuesta usando la idea de dos puntos:

`` `
ans = 0
suma = 0
para cada componente Tamaño del componente Medidas:
un componente += suma * Tamaño
suma += componente tamaño
`` `

- `sum` mantiene el tamaño total de todos los componentes * anteriores*.
- Multiplying it by the current component size gives the number of unreachable pairs that involve one node in the current component and one node in any *later* component.

Esto funciona en **O(n + m)** tiempo y **O(n)** memoria.

-...

### 4. Algoritm 2 – DFS (Bien para aprender, pero ten cuidado con los límites de pila)

``java
// pseudo-código
ans = totalPairs
para cada nodo no previsto:
cnt = tamaño de su componente a través de DFS
ans -= cnt * (cnt - 1) / 2
`` `

- Más simple conceptualmente pero utiliza la recursión (riesgo de flujo de pila) y memoria extra para la lista de adjacency.
- Todavía O(n + m), pero la versión de Java puede ser más lenta debido a la sobrecarga "ArrayList".

-...

### 5. Algoritm 3 – “Islas” Contando (Bien para pequeños gráficos)

1. Construir la lista de adyacencia.
2. Realizar DFS/BFS iterativa para obtener tamaños de componentes.
3. Acumular pares inalcanzables con el método de dos puntos.

Esto es básicamente lo mismo que Algorithm 2 pero expresado iterativamente.

-...

### 6. Edge‐ Caso " Ejecución " Lista de verificación

Silencio Silencio Por qué importa
Silencio...
Silencio Integer overflow (n up to 105)
← Reflujo de Stack en recursión ANTE Utilizar gráficas profundas iterativas DFS o DSU (cadena de 105) pueden afectar el límite de recursión
TENIDO Memoria en Java TENIDO Use `int[]` parent/size, evite `ArrayList madeint[] confía` for edges TEN GC thrashing can slow down solutions TEN
Silencio El límite de tiempo es lineal; la lista de adyacencia DFS + también es lineal, pero el ESD suele ser más rápido en la práctica. Silencio

-...

## 🧠 Take‐away for Your Interview

1. **Explica la idea total de pares**: Es una buena manera de pensar en el problema.
2. **Mostrar conocimiento del ESD**: Si el entrevistador pide una solución rápida, nombre Union‐Find inmediatamente.
3. **Hablar de las limitaciones**: Clarify que necesitará algoritmo `O(n + m)` debido a la gran entrada.
4. **Discuten alternativas**: Mención del DAAT como alternativa, pero señalan sus obstáculos (límites de personal).
5. **Opcional**: Hablar sobre el truco de acumulación de dos puntos – es un poco de “la madre cumple con la estructura de datos” que impresiona a los entrevistadores.

-...

## Palabras finales

LeetCode 2316 puede parecer intimidante a primera vista, pero con una comprensión sólida de los componentes conectados **** y un rápido **Union‐Find** implementación, puedes resolverlo en milisegundos. Los fragmentos de código anteriores son probados en batalla para Java, Python y C++. Mantener la práctica, y sentirse libre de adaptar el enfoque del ESD a otros problemas gráficos (por ejemplo, “Friend Circles”, “Conectividad de red”, “Conteo de islas”.

¡Buena suerte! 🚀

-...

### Referencias

- [Cracking the Coding Interview – Union Find](https://www.crackingthecodinginterview.com/union-find/)
- [GeeksforGeeks – Disjoint Set (Union Find)] (https://www.geeksforgeeks.org/disjoint-set-data-structure/)
- [Foro de debate de LeetCode 2316](https://leetcode.com/problems/count-unreachable-pairs-in-graph/discuss/)

-...

■ *Preparado por ChatGPT – su socio de codificación AI. *

-...

**