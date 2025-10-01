-...
Título: LeetCode 3575. Maximum Good Subtree Score -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Maximum Good Subtree Score – A Tree‐DP with Bitmasks* *
*Java fort Python ← C++ implementaciones + SEO-friendly blog post*

-...

## 1. Recaptación de problemas

Nos dan un árbol no dirigido arraigado en el nodo **0**.
Cada nodo `i` tiene un valor `vals[i]` (1 ≤ `vals[i]` ≤ 109).
Un subconjunto de nodos dentro de un subárbol se llama **bueno** si, cuando escribes todos los valores seleccionados en decimal, ** cada dígito 0-9 aparece al máximo una vez**.
(Si un valor contiene un dígito repetido – por ejemplo 121 – nunca puede pertenecer a un subconjunto bueno.)

Para cada nodo `u` necesitamos la suma máxima de un buen subconjunto que se encuentra enteramente en el subárbol de `u`.
Finalmente regresamos

`` `
(sumo sobre todos los nodos de ese máximo) mod 1 000 000 007
`` `

`par[i]` describe el árbol:
`par[0] = -1` y por cada `i título0` hay un borde `(par[i], i)`.

`n = par.length ≤ 500`.

La tarea es calcular la respuesta de manera eficiente.



-...

## 2. Idea de alto nivel

1. **Máscara de dígitos** – Para un valor `x` construimos una máscara de 10 bits.
* bit `d` is 1 α dígito `d` occur in `x`.
* Si aparece un dígito dos veces, la máscara es *inválida* (retorno `-1`).

2. **DP over masks** –
Para un subárbol guardamos un array `dp[1024]` Donde

`` `
dp[mask] = suma máxima que utiliza sólo los dígitos establecidos en 'mask '
`` `

(Si `mask` es un subconjunto de los dígitos ya utilizados, la suma correspondiente se puede lograr.)

3. *Añadiendo un nodo*
Supongamos que el nodo actual tiene máscara `S` (válido).
Podemos extender todos los conjuntos anteriormente alcanzables `M` que es **disjoint** con `S`.
Es decir, por cada submasco `m` de ``s` que hacemos

`` `
dp[m TEN S] = max(dp[m ANTE S], dp[m] + vals[nodo]
`` `

4. **Small‐to-Large merging** –
La fusión ingenua de dos tablas de DP infantiles requeriría una convolución sobre máscaras *disjoint* (conjunto 310 Ω 59 000 ops por fusión).
Con **pequeño a grande** mantenemos el DP del niño más grande y "add" el resto de los niños un nodo a la vez.
Cada nodo se procesa nuevamente en la mayoría de las veces `O(log n)`, dando un costo total `O(n log n n · 210)` que es trivial para 'n ≤ 500`.

-...

## 2. The DP In‐Depth

Símbolo vocacional Significado
Silencio...
Silencio `mask` Silencio integer de 10 bits – bits de conjunto representan dígitos usados
Silencio `dp[mask]` Silencioso mejor suma que utiliza exactamente los dígitos de `mask` Silencio
Silencioso `S` Silencioso máscara del valor del nodo actual (o `-1' si contiene un dígito repetido)
tención `ALL = 1023` (binary 1111111111) unión permanente de los 10 dígitos

### Adding a node with mask `S`

``text
para cada submask 'm' de (ALL ^ S) // máscaras que NO utilizan dígitos de S
dp[m TENIDO S] = max( dp[m ANTE S] , dp[m] + val )
`` `

La enumeración de las submascaras utiliza el clásico truco “`for (int m = sub; m; m = (m-1) ' sub), que cuesta a la mayoría de 1024 iteraciones por nodo.

### Resultado para un subárbol

Después de que todos los niños se hayan fusionado y el nodo actual añadido, la respuesta para el subárbol es simplemente "dp[ALL]" – la mejor suma que puede utilizar **cualquier** conjunto de dígitos.

-...

## 3. Técnica pequeña a alta

1. **DFS** – Traverse las listas de adyacencia del edificio del árbol de `par`.
2. Por cada nodo:
* Computar Recursivamente las tablas DP de todos los niños.
* Escoge al niño con el subárbol más grande (`bigChild`) y *reutiliza* su matriz DP como la base (`dp`).
* Add node `u` to `dp`.
* Por cada *otro* niño `v` (los pequeños) dirigen un ayudante `addSubtree(v, dp)` que recorre todo el pequeño subárbol y añade cada nodo al mismo `dp`.
Esto es seguro porque sólo somos **appendiendo** nodos, nunca fusionando dos arrays DP completos.

El número de veces que cualquier nodo es reincidido equivale al número de antepasados que lo escogieron como un niño *pequeño*, que está obligado por `O(log n)`.

-...

## 4. Corrección

* **Máscara de dígitos** garantiza que ningún valor con dígitos repetidos contribuya a un buen subconjunto.
* La regla de actualización DP sólo combina conjuntos de dígitos que son *disjoint*, por lo que el subconjunto resultante sigue siendo bueno.
* El subconjunto vacío está representado implícitamente por los ceros iniciales en el array DP.
* La respuesta para cada nodo es `dp[ALL]`, que es el máximo sobre todas las máscaras, es decir, la suma máxima de cualquier subconjunto bueno dentro de ese subárbol.

-...

## 5. Análisis de la complejidad

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio Building adjacency list Silencio `O(n)` Silencio `O(n)` Silencio
TENIDA DFS + pequeña a grande TENIDO `O(n log n · 210)` Ω **4.6 M operations** for `n = 500` ANTE `O(n)` extra arrays, plus the fixed 1024‐long DP per recursion level TEN

Tanto Java como C+ necesitan 64 bits ( " largo " / `long " ) para sumas intermedias; la respuesta final se toma modulo 1 000 000 000 007.

-...

## 6. Notas de Edge‐Cases

Silencioso en el caso
Silencio...
TENIDO Valor = 0 TENIDO No permitido por restricciones, pero `getMask` lo trata como un dígito único 0. Silencio
Silencio Todos los nodos inválidos ← Todas las entradas DP se quedan 0 → respuesta 0. Silencio
Silencio Árbol en forma de estrella ← Procesamientos pequeños a grandes cada hoja sólo una vez → todavía rápido. Silencio

-...

## 7. Aplicación del Código

A continuación se muestran soluciones listas para **Java 17**, **Python 3.10**, y **C++17**.
Los tres siguen la misma lógica que se describe.

-...

### 7.1 Java

``java
importar java.util*;

Solución de la clase pública {}
int final estático privado MOD = 1_000_000_007;
privada estática final int FULL_MASK = (1  se realizó 10) - 1; // 1023

public int goodSubtreeSum(int[] vals, int[] par) {
int n = par.length;
Lista realizadaInteger() g = nuevo ArrayList[n];
para (int i = 0; i) no; ++i) g[i] = nuevo ArrayList fiel();

para (int i = 1; i)

long[] ans = new long[n];
int[] sz = nuevo int[n];
dfs(0, vals, g, ans, sz);

larga suma = 0;
para (long v : ans) suma += v;
(int) (sum % MOD);
}

/** búsqueda de profundidad – devuelve la matriz dp para el subárbol arraigado en u */
privado largo[] dfs(int u, int[] vals, List madeInteger confianza[] g,
long[] ans, int[] sz) {
sz[u] = 1;
long[] dp = null; // mantendrá el DP del niño más pesado
int heavy = -1;

para (int v : g[u]) {}
long[] child = dfs(v, vals, g, ans, sz);
sz[u] += sz[v];
si (heavy == -1 Silencioso sz[v]  Quieresz [heavy]) {}
pesado = v;
dp = niño; // reutilizar el DP del niño pesado
}
}

si (dp == null) dp = nuevo largo [FULL_MASK + 1];

addNode(u, vals, dp);

// fusionar a los niños pequeños añadiéndolos node-by-node
para (int v : g[u]) {}
si (v != heavy) añadirSubtree(v, vals, g, dp);
}

ans[u] = dp[FULL_MASK]; // mejor sobre todas las máscaras
retorno dp;
}

/** añadir todos los nodos del subárbol arraigados en u en un matriz dp existente */
vacío privado añadirSubtree(int u, int[] vals, List Garantizado[] g, long[] dp) {
addNode(u, vals, dp);
para (int v : g[u]) añadirSubtree(v, vals, g, dp);
}

/** añadir un solo nodo a la matriz dp */
vacío privado addNode(int u, int[] vals, long[] dp) {
int mask = digitMask(vals[u]);
si (mask 0) retorno; // valor ha repetido dígito → no se puede utilizar

int free = FULL_MASK ^ máscara; // máscaras que NO utilizan dígitos de este nodo
// iterate sobre todas las submasks de 'libre' en orden descendente
para (incluido sub = libre; sub ≤ 0; sub = (sub - 1) " libre) {
int newMask = sub ¦ máscara;
dp[newMask] = Math.max(dp[newMask], dp[sub] + vals[u]);
}
dp[mask] = Math.max(dp[mask], vals[u]); // caso donde tomamos solamente este nodo
}

/** devuelve bitmask de dígitos o -1 si un dígito repite en x */
dígito privado Máscara(int x) {
int seen = 0;
(x 0) {
int d = x % 10;
si (ver " (1 " ) 0) retorno -1;
vistos TEN= (1 ,2)
x /= 10;
}
retorno visto;
}
}
`` `

-...

## 7.2 Python

``python
de la importación Lista

MOD = 1_000_000_007
FULL = (1 0) 10) - 1 # 1023

Solución de clase:
def good SubtreeSum(self, vals: List[int], par: List[int]) int:
n = len(par)
g = [[] for _ in range(n)]
para i en rango(1, n):
g[par[i]].append(i)

a)
Sz = [0]
auto.dfs(0, vals, g, ans, sz)

total = suma(ans) % MOD
total

def dfs(self, u: int, vals: List[int], g: List[List[int],
ans: List[int], sz: List[int] List[int]:
sz[u] = 1
Dp = Ninguno
pesado = 1

for v in g[u]:
niño = autodfs(v, vals, g, ans, sz)
sz[u] += sz[v]
si es pesado == -1 o sz[v]
pesado = v
dp = niño

si dp es Ninguno:
dp = [0] * (FULL + 1)

auto.add_node(u, vals, dp)

for v in g[u]:
si v!= pesado:
auto.add_subtree(v, vals, g, dp)

as[u] = dp [FULL] # mejor sobre todas las máscaras
Regrese.

def add_subtree(self, u: int, vals: List[int], g: List[List[int]], dp: List[int]):
auto.add_node(u, vals, dp)
for v in g[u]:
auto.add_subtree(v, vals, g, dp)

def add_node(self, u: int, vals: List[int], dp: List[int]):
máscara = auto.digit_mask(vals[u])
si máscara 0: # dígito repetido – no puede ser parte de un buen subconjunto
Regreso
libre = FULL ^ máscara
sub = libre
mientras sub:
nuevo = sub- máscara
dp[new] = max(dp[new], dp[sub] + vals[u]
sub = (sub - 1) " libre
dp[mask] = max(dp[mask], vals[u]

def digit_mask(self, x: int) - título int:
vistos = 0
mientras x:
d = x % 10
si se ve " (1 "
retorno -1
visto Ø= 1
x //= 10
Retorno visto
`` `

-...

## 7.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
bien SubtreeSum(vector identificadoint sectores vals, vector implicadoncia reducida par) {
const int MOD = 1'000'007;
int n = par.size();
vector realizador:
para (int i = 1; i)

vector realizado largo tiempo mejor(n);
vector:
dfs(0, vals, g, best, sz);

larga suma = 0;
(auto v : mejor) suma += v;
int (sum % MOD);
}

privado:
static constexpr int FULL = (1 se hizo 10) - 1; // 1023

vector realizado largo tiempo dfs(int u, vector identificadoint
vector de vectores g,
vector de largo alcance máximo, vectorial implicado estrecho contacto sz) {
sz[u] = 1;
vector llevado a cabo larga duración dp; // se establecerá en el DP del niño pesado
int heavy = -1;

para (int v : g[u]) {}
niño auto = dfs(v, vals, g, best, sz);
sz[u] += sz[v];
si (heavy == -1 Silencioso sz[v]  Quieresz [heavy]) {}
pesado = v;
dp = std::move(child);
}
}

(dp.empty()) dp.assign(FULL + 1, 0);

addNode(u, vals, dp);

para (int v : g[u]) si (v != pesado) añadirSubtree(v, vals, g, dp);

mejor[u] = dp[FULL];
retorno dp;
}

vacío añadirSubtree(int u, vector asignadoint
vector de vectores g,
vector de largo alcance dp) {
addNode(u, vals, dp);
para (int v : g[u]) añadirSubtree(v, vals, g, dp);
}

vacio addNode(int u, vector identificadoint círculo vals, vector alcanzadolong ventaja dp) {
int mask = digitMask(vals[u]);
si (mask 0) regresa; // dígito repetido – saltar

int free = FULL ^ máscara;
para (int sub = libre; sub; sub = (sub - 1) " libre) {
int newMask = sub ¦ máscara;
dp[newMask] = max(dp[newMask], dp[sub] + vals[u]);
}
dp[mask] = max(dp[mask], (long long)vals[u]);
}

int digitMask(int x) {
int seen = 0;
x) {
int d = x % 10;
si (ver " (1 " ) " d) devuelve -1;
vistos TENIDO = 1
x /= 10;
}
retorno visto;
}
};
`` `

-...

## 8. Resumen " Takeaway

* **Máscaras de dígitos + Máscaras DP** da una manera elegante de hacer cumplir la regla del “ dígito único”.
* **Pequeño a grande** mantiene la solución rápida incluso en árboles densos.
* El algoritmo se ejecuta cómodamente dentro de los límites para 'n ≤ 500' mientras que ser fácil de entender e implementar.

Siéntase libre de copiar el snippet en su presentación de LeetCode o utilizarlo como ejemplo de enseñanza para “DP en árboles + bitmask + patrones pequeños a grandes”.



-...



-...

¡Feliz codificación