-...
Título: LeetCode 2322. Puntuación mínima después de la eliminación en un árbol -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 2322 – Puntuación mínima después de las desinversiones en un árbol
**El Bien, el Mal El Infiel - Un Profundo Buceo con Java / Python / C++ Soluciones**

■ **SEO Palabras clave**: *LeetCode 2322*, *Minimum Score After Removals on a Tree*, *Tree DP*, *XOR*, *Hard*, *Interview Prep*, *Java*, *Python*, *C+*,* * Diseño de Algorithm*, *Partición de Tree*

-...

## 1. Recaptación de problemas

Se le da un árbol arraigado con nodos (`3 ≤ n ≤ 1000`).
- `nums[i]` - valor del nodo `i.
- `edges` - lista de los bordes no dirigidos.

Usted debe eliminar **dos bordes distintos**, dividiendo el árbol en **tres componentes conectados**.
Para cada componente computa el XOR de todos los valores de nodos dentro de él.
El **score** de ese par de eliminación es

`` `
puntuación = max(XOR1, XOR2, XOR3) – min(XOR1, XOR2, XOR3)
`` `

Devuelve la puntuación más mínima posible** sobre todos los pares de eliminaciones del borde.

-...

## 2. Por qué este problema es grande para las entrevistas

La buena vida es la mala vida
Silencio--------------------------
Silencio ** Limitaciones moderadas** (`n ≤ 1000`) → le permite pensar en la fuerza bruta + poda inteligente. **Dos eliminaciones** te obligan a razonar sobre componentes *permitidos* – casos fáciles de perder. TEN **XOR truco**: la resta no está disponible; necesitas pensar en la diferencia de configuración en el espacio XOR. Silencio
Silencio **Vista clásica DFS + Euler** para el subárbol XORs – un patrón visto en muchos sitios. Silencio **Primera búsqueda** profundidad de recursión (≤1000) es seguro en la mayoría de los idiomas, pero el flujo de pila es un riesgo en Java. Silencio **Los bucles de ácaro** (`O(n2)`) pueden parecer caros; debe justificar por qué está bien para las limitaciones. Silencio
Silencio **El subproblema plano**: compute subtree XOR una vez, reutilizar. Silencio **Los controles del antepasado** con los tiempos de entrada/salida – una fuente común de errores fuera-por-uno. ← **El alcance pasa** sobre los bordes puede conducir fácilmente a O(n3) si no tienes cuidado. Silencio

-...

## 3. Estrategia de alto nivel

1. **Arranque el árbol** (cualquier nodo, elegimos `0`).
2. Ejecute un solo DFS para calcular:
* `subXor[u]` – XOR de todos los valores en el subárbol de U.
* `tin[u]`, `tout[u]` – tiempos de entrada / salida para probar relaciones con el ancestro en O(1).
* `parent[u]` - padre de cada nodo.
3. Por cada par sin orden de *niños nodos* `(i, j)` (el borde es `parent[i]-i`), evaluar el componente resultante XORs:
* **Aristas descomunales** – tres subárboles independientes:
c1 = subXor[i]`, `c2 = subXor[j]`, `c3 = total Xor ^ subXor[i] ^ subXor[j]`.
* **Nested edges** (uno dentro del otro):
Si `j` está dentro `i` →
c1 = subXor[j] " ,
c2 = subXor[i] ^ subXor[j] (XOR of subtree `i` **without** `j`),
c3 = total Xor ^ subXor[i]`.
(Simétrico si `i` está dentro `j`.)
4. Computar `score = max(c1, c2, c3) – min(c1, c2, c3)` y mantener el mínimo.

Porque `n ≤ 1000`, el bucle par (`~5·105` iteraciones) es trivial.
El algoritmo funciona en **O(n2)** tiempo y **O(n)** espacio.

-...

## 4. Casos de borde " Pitfalls

Silencio Pitfall Silencio Cómo evitar
Silencio...
Silencio ** Errores de prueba del antepasado** – mezclando `trabaja=` y `haciendo `` incorrectamente uso de la vida **Euler tour** (`tin[u] ≤ tin[v] ' ≤ tout[u]`) para un control robusto del antepasado. Silencio
tención **XOR diferencia** – olvidando que `a \ b` en XOR es `a ^ b` si `b ⊆ a` ¦ Para los bordes anidados, componente XOR es `subXor[ancestor] ^ subXor[descendente]`. Silencio
tención **Exclusión de bordes de raíz** – root no tiene padre tención Sólo considerar nodos `u != root` como niños. Silencio
Silencio **Iniciar la profundidad de la recursión** en Java ← Utilizar DFS iterativa o aumentar el tamaño de la pila. Silencio

-...

## 5. Aplicación del Código

A continuación se encuentran soluciones limpias, listas para pasar en **Java**, **Python**, y **C+**.

## 5.1 Java (Java 17)

``java
importar java.util*;

Solución de la clase pública {}
Registro privado:Integer() g;
int privado [] padre, estaño, tout, subXor;
temporizador privado int;
total privado Xor;

mínimo público Score(int[] nums, int[][] edges) {
int n = nums.length;
g = nuevo ArrayList[n];
para (int i = 0; i) no; ++i) g[i] = nuevo ArrayList fiel();
para (int[] e : bordes) {
g[e[0].add(e[1]);
g[e[1]].add(e[0]);
}

padre = nuevo int[n];
estaño = nuevo int[n];
tout = nuevo int[n];
subXor = nuevo int[n];
timer = 0;

dfs(0, -1, nums);

totalXor = subXor[0];
int best = Integer.MAX_VALUE;

// Recopilar todos los ganglios infantiles (edges que podemos eliminar)
Lista Nombramiento de niños enteros = nuevo ArrayList implicado();
para (int i = 1; i)

// Tetrato sobre pares sin orden
int m = children.size();
para (int a = 0; a) {}
int i = children.get(a);
para (int b = a + 1; b)
int j = children.get(b);
int[] comps = compsXor(i, j);
int score = Math.max(Math.max(comps[0], comps[1]), comps[2]
- Math.min(Math.min(comps[0], comps[1]), comps[2]);
si (score ) mejor = puntuación;
}
}
devolver mejor;
}

dfs(int u, int p, int[] nums) {
parent[u] = p;
tin[u] = ++timer;
int xr = nums[u];
para (int v : g[u]) si (v != p) {}
dfs(v, u, nums);
xr ^= subXor[v];
}
subXor[u] = xr;
tout[u] = ++timer;
}

// Devoluciones {c1, c2, c3} para borrar los bordes (parent[i]-i) y (parente[j]-j)
int privado[] compsXor(int i, int j) {
// Verificar la relación del antepastor
boolean iInsideJ = tin[j] не= tin[i] " sensible tout[i];
boolean jInsideI = tin[i] не= tin[j] " sensible tout[i] "

c1, c2, c3;
si (iInsideJ) { // j interior i
c1 = subXor[j];
c2 = subXor[i] ^ subXor[j]; // i \ j
c3 = total Xor ^ subXor[i];
} si (jInsideI) { // I inside j
c1 = subXor[i];
c2 = subXor[j] ^ subXor[i]; // j \ i
c3 = total Xor ^ subXor[j];
} más { // disjoint
c1 = subXor[i];
c2 = subXor[j];
c3 = total Xor ^ subXor[i] ^ subXor[j];
}
devolver nuevo int[]{c1, c2, c3};
}
}
`` `

*Puntos clave*
- Un DFS llena los tiempos de la gira de Euler.
- " Timer " garantiza los controles del antepasado " O(1) " .
- Todo aritmético está en `int`; LeetCode garantiza `nums[i]` se ajusta en `int`.

-...

### 5.2 Python 3

``python
de la importación Lista

Solución de clase:
mínimo Score(self, nums: List[int], edges: List[List[int]) - título int:
n = len(nums)
g = [[] for _ in range(n)]
para a, b en los bordes:
g[a].append(b)
g[b].append(a)

padre = [-1]
estaño, tout = [0] * n, [0]
sub = [0]
timer = 0

def dfs(u, p):
temporizador no local
padre [u] = p
timer += 1
tin[u] = timer
xr = nums[u]
for v in g[u]:
si v == p:
continuar
dfs(v, u)
xr ^= sub[v]
sub[u] = xr
timer += 1
tout[u] = timer

dfs(0, -1)
total = sub[0]
mejor = flotante('inf')

# Nodos infantiles (edge we may cut)
niños = [i for i in range(1, n)]

para un rango (len(niños)):
i = niños[a]
para b en rango(a + 1, len(children)):
j = niños[b]
# Ancestor checks
si la estaño[i] 0 = lata [j] 0 0 = tout[j]
c1 = sub[j]
c2 = sub[i] ^ sub[j]
c3 = total ^ sub[i]
elif tin[j] Identifica= tin[i] Identificado= tout[i]
c1 = sub[i]
c2 = sub[j] ^ sub[i]
c3 = total ^ sub[j]
# Disjoint
c1, c2, c3 = sub[i], sub[j], total ^ sub[i] ^ sub[j]

puntuación = max(c1, c2, c3) - min(c1, c2, c3)
mejor = min(mejor, puntuación)

mejor
`` `

-...

### 5.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
vector realizador realizador:
vector significado padre, estaño, tout, subXor;
int timer, total Xor;

vacio dfs(int u, int p, const vector identificadoint
parent[u] = p;
tin[u] = ++timer;
int xr = nums[u];
para (int v : g[u]) si (v != p) {}
dfs(v, u, nums);
xr ^= subXor[v];
}
subXor[u] = xr;
tout[u] = ++timer;
}

public:
mínimo Puntaje(vector seleccionado) {}
int n = nums.size();
g.assign(n, {});
para (auto &e : bordes) {}
g[e[0].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

parent.resize(n);
tin.resize(n);
tout.resize(n);
subXor.resize(n);
timer = 0;

dfs(0, -1, nums);
totalXor = subXor[0];

int best = INT_MAX;
vector niños;
para (int i = 1; i)

para (size_t a = 0; a) ++a) {
int i = niños[a];
para (size_t b = a + 1; b) ++b) {
int j = children[b];
c1, c2, c3;
si (tin[i] <= tin[j] " sensible tout[j] "
c1 = subXor[j];
c2 = subXor[i] ^ subXor[j];
c3 = total Xor ^ subXor[i];
} si (tin [j] <= tin[i] ' ющ tout[i] I inside j
c1 = subXor[i];
c2 = subXor[j] ^ subXor[i];
c3 = total Xor ^ subXor[j];
} más { // disjoint
c1 = subXor[i];
c2 = subXor[j];
c3 = total Xor ^ subXor[i] ^ subXor[j];
}
int mx = max({c1, c2, c3});
int mn = min({c1, c2, c3});
mejor = min (mejor, mx - mn);
}
}
devolver mejor;
}
};
`` `

Los tres códigos comparten la misma lógica del núcleo – sólo diferentes expresiones.

-...

## 6. Why the `O(n2)` Brute‐ Fuerza de trabajo

- ** Iteraciones máximas**: `C(n-1, 2) = (n-1)(n-2)/2 ♥ 5·105` for `n = 1000`.
- Cada iteración hace sólo un puñado de operaciones enteros → Identificar 1 ms en C++ / Python, se realizaron 5 ms en Java.
- El uso de la memoria es lineal: `O(n)` para la lista de adyacency, metadatos DFS y algunos arrays enteros.

**Si te preocupa el rendimiento**, puedes probar lo siguiente:
`5·105` bucles × ~10 operaciones primitivas ♥ 5 M operaciones – bien por debajo del límite de 1 segundo en LeetCode.
No hay necesidad de trucos bit-parallel o estructuras de datos avanzadas.

-...

## 7. Pensamientos finales – Lo que hace este problema *Entrevista-Ley*

1. **Clear Sub-Problema** – Compute subtree XOR *once*.
2. **Euler Tour Ancestor Test** – un patrón reutilizable para cualquier lógica “subtree vs subtree”.
3. **Diferencia de conjuntos en el espacio XOR** – una sutileza que viaja a muchos candidatos; dominarlo demuestra un fuerte razonamiento poco acertado.
4. ** Análisis de complejidad** – mostrar que puede razonar sobre `O(n2)` vs. `O(n3)` y justificar sus opciones de diseño.

Si usted puede explicar esta solución, caminar a través del bucle de pares, y mostrar por qué el código es correcto, usted demostrará la maestría de las traversales de árboles, la manipulación de bits y el pensamiento algorítmico – exactamente los gerentes de contratación de habilidades buscan en un problema *Hard* LeetCode.

-...

## 8. Meta Descripción

■ *Aprenda a resolver LeetCode 2322 – Puntuación mínima Después de las depuraciones en un árbol – con paso a paso Java, Python, y código C++. Entender el truco de la diferenciación del antepasado, las comprobaciones de intervalo de tiempo, y por qué este problema de entrevista “Hard” es un escaparate perfecto de habilidades de árbol DP y XOR. *

-...

¡Feliz codificación y buena suerte matando esa entrevista! 🚀