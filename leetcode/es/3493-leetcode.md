-...
Título: LeetCode 3493. Propiedades Gráfico -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Soluciones de tres idiomas

A continuación se muestran las soluciones **ready‐to-copy** para LeetCode 3493 – “Propiedades Gráfico”.
Todos usan la misma idea:

1. **Construir un bit-set (o hash-set) para cada fila** para que podamos contar elementos comunes en *O(1)* (o *(m)*).
2. **Union‐Find (Disjoint‐Set Union, DSU)** mantiene un seguimiento de los componentes conectados.
3. Por cada par `(i , j)` fusionamos los dos nodos si su intersección ≥ `k`.
4. Finalmente cuenta cuántas raíces únicas existen – esa es la respuesta.

Las implementaciones a continuación siguen las restricciones (`n , m ≤ 100`, valores ≤ 100) y están fuertemente comentadas para que pueda pegarlos directamente en LeetCode.

-...

#### 1.1 Java – “BitSet + DSU”

``java
importa java.util. BitSet;

Clase DSU {}
int[] parent, rank;

DSU(int n) {
padre = nuevo int[n];
rango = nuevo int[n];
para (int i = 0; i)
}

int find(int x) {
si (parent[x] != x) parent[x] = encontrar(parent[x]); // path compresión
devolver padre[x];
}

unión de vacío(int a, int b) {}
int ra = find(a), rb = find(b);
si (ra == rb) regresa;
si (rank[ra]) [rb]) padre [ra] = rb;
[rb] = ra;
{ parent[rb] = ra; rank[ra]++; }
}
}

Solución de la clase pública {}
int numberOfComponents(int[][] prop, int k) {
int n = prop.length;
// 101 es suficiente: los valores están en [1, 100]
BitSet[] filas = nuevo BitSet[n];

// Paso 1 – convertir cada fila en un BitSet
para (int i = 0; i)
filas[i] = nuevo BitSet(101);
for (int val : prop[i]) rows[i].set(val);
}

DSU dsu = nuevo DSU(n);

// Paso 2 - examinar cada par sin orden
para (int i = 0; i)
para (int j = i + 1; j)
// Cuenta rápidamente los intereses comunes:
BitSet tmp = (BitSet) rows[i].clone();
tmp.and(rows[j]); // intersection
si (tmp.cardinality()
dsu.union(i, j);
}
}
}

// Paso 3 - contar raíces distintas
int comps = 0;
para (int i = 0; i)
si (dsu.find(i) == i) comps++;
comps de retorno;
}
}
`` `

■ ¿Por qué BitSet?
Todos los valores son ≤ 100 → 101 bits → un Java `BitSet` encaja en una palabra de máquina.
√≥ - `cardinality()` es una cuenta pop nativa; la intersección es `O(1)`.

-...

### 1.2 Python – “Set Intersection + DSU”

``python
clase DSU:
def __init__(self, n):
self.parent = list(range(n))
self.rank = [0] * n

def find(self, x):
si yo. parent[x]!= x:
self.parent[x] = self.find(self.parent[x]) # path compresión
Vuélvete. parent[x]

def union(self, a, b):
ra, rb = self.find(a), self.find(b)
si ra == rb: retorno
si auto.rank[ra] se auto.rank[rb]:
self.parent[ra] = rb
elif self.rank[ra] œ self.rank[rb]:
self.parent[rb] = ra
más:
self.parent[rb] = ra
self.rank[ra] += 1

Solución de clase:
def numberOfComponents(self, prop: List[List[int], k: int) - título int:
n = len(prop)
# Convertir every row to a *set* – set‐intersection is O(min( vivida sometida, sometidab sometida)
filas = [set(row) for row in prop]

dsu = DSU(n)

para i en rango(n):
para j en rango(i + 1, n):
common = len(rows[i] & rows[j]) # set intersection
si es común
dsu.union(i, j)

# Cuenta raíces distintas
raíces = {dsu.find(i) for i in range(n)}
len(roots)
`` `

■ ¿Por qué un `set'?
■ Los valores son diminutos, por lo que la parte superior de un `BitSet` es innecesaria en Python.
■ La intersección 'set' es limpia, fácil de leer, y lo suficientemente rápida para 'n ≤ 100'.

-...

### 1.3 C++ – “`std::bitset` + DSU”

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase DSU {}
public:
vector:
DSU(int n) : parent(n), rank(n,0) {
iota(parent.begin(), parent.end(), 0);
}
int find(int x) {
si (parent[x] != x) parent[x] = encontrar(parent[x]); // path compresión
devolver padre[x];
}
vacío unite (incluido a, int b) {}
int ra = find(a), rb = find(b);
si (ra == rb) regresa;
si (rank[ra]) [rb]) padre [ra] = rb;
[rb] = ra;
{ parent[rb] = ra; ++rank[ra]; }
}
};

Clase Solución {
public:
número de intOfComponents(vector seleccionadovector seleccionado) {
int n = prop.size();
// 101 bits son suficientes – los valores son 1..100
vector obtenidos bitset realizado128 hilos(n);
para (int i = 0; i)
for (int v : prop[i]) rows[i].set(v);

DSU dsu(n);

para (int i = 0; i)
para (int j = i + 1; j)
int common = (rows[i] & rows[j]).count(); // popcount
dsu.unite(i, j);
}

// Cuentan raíces distintas
int comps = 0;
para (int i = 0; i)
si (dsu.find(i) == i) ++comps;
comps de retorno;
}
};
`` `

■ **¿Por qué `bitset efectuado128 ``? #
√ - 128 bits mantienen cómodamente los 100 valores posibles.
" operador " y " cuenta() " se implementan en hardware (peso adelgazado), dando *O(1)* por par.

-...

## 2. El Bien, el Mal, y el Ugly

**Aspecto** Silencio**
Silencio----------------------------------------------------
Silencio ** Claridad Conceptual** Silencio Union‐Find es una entrevista clásica. Las intersecciones contables ingenuamente pueden ser difíciles de razonar. Silencio Olvidar la *unidad* de elementos (duplicados) conduce a respuestas erróneas. Silencio
tención **Implementation Simplicity** ← DSU + BitSet/Set es lógica de 5 líneas. TEN Python set intersection es una sola línea de código. TEN Utilizar arrays crudos y cuentapa manual puede ser error‐prone. Silencio
Silencio **Performance** Silencio Las operaciones Bit dan *(n2)* con una pequeña constante. La `set.intersección ' de tención Python es `O(m)`, pero aún así se realizaron 106 operaciones para restricciones. tención Los bucles manuales de más de 100 números por par son perfectamente finos pero más difíciles de leer. Silencio
Silencio **Readability** Silencio Java `BitSet` + DSU es autordocumentante. Los conjuntos de Python son casi autoexplicativos. tención C++ `bitset obtenidos128 `` puede sentir un poco de “bajo nivel” para los recién llegados. Silencio
Silencio **Edge Cases** tención Valores externos 1–100 rompería la lógica bit-set – guardia con cheques. Silencio Duplicados en una fila son inofensivos porque usamos 'set`. peru DSU rango/size heuristics son esenciales para evitar árboles degenerados. Silencio

■ **Bottom line:**
■ El *bueno* es un algoritmo rápido y limpio.
■ El *bad* es la tentación de escribir una rutina de intersección pesada.
■ La *superior* falta optimizaciones del ESD (comprensión por vía, unión por rango), que pueden convertir una solución *O(n2 α(n)* en una lenta en entradas más grandes.

-...

## 3. SEO‐Optimized Blog Post

■ *Título*
■ **Propiedades Gráfico: Contando componentes conectados con ESD - El bueno, el malo, el ugly**

■ ** Descripción de los datos* *
■ Master LeetCode’s “Properties Graph” con una solución Union‐Find para entrevistas. Aprenda a optimizar los recuentos de intersección con bitsets, solucionar problemas comunes, y as a su próxima entrevista de codificación.

■ ** Palabras clave principales* *
" LeetCode 3493 " , `properties graph ' , `union find`, `DSU algoritmo`, `interview question`, `job interview coding`, `algorithm interview prep`, `data structure ', `graph theory`, `C++ bitset`, `Java BitSet`, `Python set intersection `

■ **Secondary Keywords* *
" entrevista de codificación " , " entrevista de ingeniería de software " , " contratación de tecnología " , " solución de problemas algoritmicos " , " conectividad gráfica `

-...

#### Introduction

■ En entrevistas tecnológicas modernas, los problemas de LeetCode que mezclan *graphs* y *data structures* son minas de oro para mostrar pensamiento algorítmico.
> LeetCode 3493 – *Properties Graph* – te pide modelar los perfiles de usuario como nodos, vincularlos cuando comparten suficientes intereses, y cuenta cuántos “círculos de amistad” independientes existen.
■ A continuación diseccionamos el problema, mostrar una solución óptima, y darle una hoja de trampa rápida para el día de la entrevista.

-...

## Problema Recap

- ** Entrada*
`prop` - una matriz de enteros `n × m ' (`1 ≤ n, m ≤ 100 ' , valores ≤ 100).
`k` - el número mínimo de atributos *common* requeridos para conectar dos filas.
- **Construcción de gráficos**
Nodos: `0 ... n‐1`.
Edge `(i, j)` existe sif `presentprop[i] ∩ prop[j] sometida ≥ k`.
- ¿Qué?
Devuelve el número de componentes conectados en este gráfico no dirigido.

-...

### ¿Por qué Union‐Find?

1. **Natural fit for “merge if connected”** – una vez que vemos un borde, nos unimos a dos componentes.
2. **Amortised `α(n)` (inverse Ackermann) time** – virtualmente constante para tamaños de entrada prácticos.
3. **La habilidad de entrevista clásica** – los reclutadores a menudo le piden que explique el ESD; tener una solución de trabajo demuestra profundidad.

-...

## Optimizando la Conteo de Intersección

El enfoque ingenuo escanearía ambas filas por cada par, costando `O(n2 m)`.
Dada la pequeña gama de valores, podemos hacerlo mejor:

Silencio **Idioma**
Silencio--------------------------------------------- La vida eterna...
Silencio **C++ / Java** Silencio `estd::bitset` / `BitSet` Silencio Representar cada fila como un bitmask de 101 bits. La intersección es un poco insensato Y, la cardenalidad es una cuenta pop. Silencio
Silencio **Python** Silencio `set` Silencio `row ' other` es una intersección de conjunto; los conjuntos de hash incorporados de Python dan un excelente comportamiento constante para juegos pequeños. Silencio

■ **Tip**: En Python, si quieres velocidad máxima y sabes que `m` es grande, todavía puedes usar `array('I')` y empaquetar los valores.

-...

### Full Solution Walkthrough (C++)

``cpp
vector obtenidos bitset realizado128 hilos(n);
para (int i=0;i obtenidos;i++)
for (int v: prop[i]) rows[i].set(v); // set bit v

DSU dsu(n);
para (int i=0;i obtenidos;i++)
para (int j=i+1;j obtenidos;j++) {}
if ((rows[i] & rows[j]).count() k)
dsu.unite(i,j);
}
`` `

- **`rows[i] & rows[j]** - Intersección acelerada por hardware.
- **`.count()`** - cuentapágina; O(1).
- **DSU** – la compresión del camino + unión por rango garantiza un comportamiento casi lineal.

-...

### Common Pitfalls > Cómo evitarlos

Silencio **Pitfall** Silencio**
Silencio----------------------------...
Silencio **Atributos duplicados en una fila** Silencio Sobre-cuenta intersección Silencio Convertir cada fila en un *set* (Python) o utilizar `BitSet` (duplicados no importan). Silencio
Silencio **Zero-indexed vs one‐indexed values** ← Posición de bits Wrong TEN siempre compensada por 1 cuando se utiliza `BitSet` / `bitset`. Silencio
Silencio **Missing DSU rank** Silencio O(n2) peor-case on bad inputs tención Siempre implementa unión por rango o tamaño. Silencio
tención **Using slow loops** tención Timeouts on larger tests TEN Replace `for` loops over 100 values with bitset intersection or set intersection. Silencio

-...

### Quick Interview Cheat‐ Sheet

- Estructuras de datos para mencionar
- `UnionFind (DSU)`
- `BitSet` (Java/C++) o `set ' (Python)
*La complejidad del tiempo*
`O(n2)` edges *popcount* → ~104 operations for `n=100`.
- *La complejidad del espacio*
`O(n)` para DSU + `O(n * bitset)` ♥ `O(n)` bits → insignificante.
- **Edge‐Case Note**
- ¿Matricia vacía? Regresa.
- `k == 0` → cada nodo conectado → 1 componente.

-...

## Final Thought

■ Mastering *Properties Graph* significa dominar la sinergia entre *graph connectivity* y *efficient merging*.
■ Si puedes explicar esta solución en menos de 5 minutos y codificarla de forma impecable, impresionarás a los entrevistadores en todo el espectro tecnológico – de startups a Fortune 500.

-...

### FAQ

**Q1. Uso recursiva en el ESD `find`?* *
- En entrevistas, un enfoque iterativo es más seguro – evita el desbordamiento de la apilación en la recursión profunda.

**Q2. ¿Por qué no utilizar BFS/DFS? #
- BFS/DFS funcionaría, pero tendría que construir todos los bordes primero.
- El DAA se fusiona en la mosca y utiliza la memoria *(n)*, mientras que el DFS utilizaría `O(n + bordes)`.

**Q3. ¿Y si 'k' es grande, dicen 50? #
- El algoritmo todavía funciona; la intersección cuenta naturalmente reducir el número de sindicatos.

-...

#### Takeaway

■ El problema Propiedades Gráfico es un excelente escaparate del poder del ESD en un contexto gráfico.
■ Mediante el uso de intersecciones basadas en bitset, garantiza una solución rápida que se escala cómodamente.
■ La próxima vez que se le haga una pregunta de “conexión de perfiles”, recuerde: **merge si está conectado → DSU**.

-...

**Feliz codificación, y puede que su entrevista esté llena de algoritmos limpios y cero errores!* *

-...

*End of post*

-...

■ **Sin ánimo de copiar los fragmentos de código arriba** – están listos para pegar en LeetCode, Codeforces o su IDE local. ¡Buena suerte en tu próxima entrevista!