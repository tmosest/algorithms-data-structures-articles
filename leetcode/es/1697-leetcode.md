-...
Título: LeetCode 1697. Comprobación de la existencia de bordes largos Senderos limitados -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📚 LeetCode 1697 – Checking Existence of Edge‐Length Limited Paths
### The Good, The Bad, and The Ugly Blog de buceo para Job‐Seekers

■ **Etiqueta palabra clave**: *LeetCode 1697 solución* – *union‐find* – *edge‐length limited paths* – *hard problem* – *coding interview*

Si usted está cazando para ese problema “hard” LeetCode que hará que los reclutadores sentarse y notar, usted querrá dominar **1697. Verificación de la Existencia de la Longitud del borde Senderos limitados**.
A continuación encontrará:

Silencio Lo que aprenderás Silencio 🔍 Por qué importa
Silencio...
Silencio La estrategia óptima **union‐find** (disjoint-set)  durable O(E+Q) log(E+Q)) es lo suficientemente rápida para 105 bordes & consultas ←
Silencio Ordenar trucos para mantener las respuestas en el orden original ← Evita el procesamiento de consultas O(Q2)
← Manipulación multi-edges & grandes límites enteros ← Previene errores sutiles en los casos de prueba de LeetCode
tención Clean, language‐agnostic implementation ← Show recruiters usted puede código en Java, Python, C++

-...

## 1. Recaptación de problemas

■ *Given*
" n ' nodes (0-based).
* `edgeList[i] = [ui, vi, disi]` – borde no dirigido con distancia `disi`.
[pj, qj, limitj] – preguntar si existe un camino de `pj` a `qj` **con todos los bordes < limitj**.

■ **Retorno** " respuesta de la comunidad " - un valor por consulta.

**Constraints** (caso peor)

* `2 ≤ n ≤ 105`
* `1 ≤ edgeList.length, queries.length ≤ 105 `
* `1 ≤ disi, limitj ≤ 109 `
* Pueden existir múltiples bordes entre el mismo par de nudos.

-...

## 2. Why a Union‐Find (Disjoint‐Set Union) Works

Piense en cada borde como un “puente” que se pone disponible cuando su distancia es **strictamente menor** que el `limit` de la consulta actual.
Si procesamos todos los bordes en **aumentando el orden de distancia**, podemos “conectar” incrementalmente el gráfico:

1. **Sorta** todos los bordes por distancia.
2. **Sorta** todas las consultas por `limit ' .
(Recuerde el índice original para poner la respuesta más adelante.)
3. Mantener una estructura del ESD sobre los nudos.
4. Mientras que la distancia del borde siguiente `segúntele el límite de la consulta actual', sintetice sus dos puntos finales.
5. Después de que todos los bordes aplicables se fusionan, los dos nodos de la consulta están conectados si pertenecen al mismo conjunto DSU.

Debido a que procesamos consultas en el `limit` ascendente, cada borde se considera **una vez** – dando una complejidad general de
**O(E + Q) log (E + Q)** for sorting plus **O(E α(n))** for DSU operations (`α` = inverse Ackermann, practically constant).

-...

## 3. El Bien, El Mal, El Mal

Silencio Silencio
Silencio------------Prince------
Silencio ** Algorithm** Silencio O(E+Q) log (E+Q)) → rápido para 105 Silencio Ninguno Silencio – Silencio
Silencio **DSU Implementación** Silencioso de compresión + unión-por-rank → casi-constant amortized Silencio Requiere cuidadoso manejo de índices (0-basado) Silencio Olvidar actualizar 'parente' en 'find' conduce a bucles infinitos
Silencio **Sorting Queries** Silencio Mantiene respuestas en orden original ← Requiere memoria extra para el índice Silencio Si usted ordena por `limit` pero olvida almacenar el índice original, usted devolverá las respuestas incorrectas
Silencio **Multiple Edges** Silencio Handled automatically – nosotros sólo procesamos todos Silencio No se necesita un manejo especial Silencio Si usted erróneamente deduplica los bordes, usted pierde la información
tención **Edge " Limit Size** tención 32‐bit ints sufficient, but use `long ' if you’re paranoid peru Ninguno viv Utilizar `int` cuando la suma exceda 2−31‐1 puede causar desbordamiento en otros problemas

-...

## 4. Código completo – Java, Python, C++

■ Las tres implementaciones utilizan la misma lógica.
■ Cada archivo es autocontenido, incluye las importaciones necesarias, y está listo para pegar en su entorno IDE o LeetCode.

#### 4.1 Java

``java
importar java.util*;

// ------------ DSU (Disjoint Set Union) ----------
Clase DSU {}
int privado final[] parent;
int final privado[] rango; // unión por rango

DSU(int n) {
padre = nuevo int[n];
rango = nuevo int[n];
para (int i = 0; i)
}

int find(int x) {
// Compresión del camino
(parent[x] != x) parent[x] = find(parent[x]);
devolver padre[x];
}

unión de vacío(int x, int y) {
int rx = find(x);
int ry = find(y);
si (rx == ry) regresa;

// Unión por rango
si (rank[rx] Identifica rango [ry]) padre [rx] = ry;
[ry] [ry] = rx;
otra vez
parent[ry] = rx;
rango[rx]+;
}
}
}

// -------- Solución principal --------
Solución de la clase pública {}
boolean[] distanceLimited PathsExist(int n,
int[][] borde Listo,
int[][] consultas) {
// Adjuntar índices originales a las consultas
int m = consultas. longitud;
int[][] qWithIdx = nuevo int[m][4];
para (int i = 0; i) {}
qWithIdx[i][0] = consultas[i][0];
qWithIdx[i][1] = consultas[i][1];
qWithIdx[i][2] = consultas[i][2];
qWithIdx[i][3] = i; // posición original
}

// Ordenar bordes por distancia
Arrays.sort(edgeList, Comparator.comparingInt(a - título a[2]));

// Ordenar consultas por límite
Arrays.sort(qWithIdx, Comparator.comparingInt(a - título a[2]));

DSU dsu = nuevo DSU(n);
boolean[] ans = nuevo boolean[m];
int eIdx = 0; // puntero sobre bordes ordenados

para (int[] q : qWithIdx) {
límite de entrada = q[2];
// Añadir todos los bordes con la distancia
mientras (eIdx) se observó bordeList.length " borde List[eIdx][2] , límite hecho) {
dsu.union(edgeList[eIdx][0], edgeList[eIdx][1]);
eIdx++;
}
// Si ambos nodos están conectados, la respuesta es verdadera
ans[q[3]] = dsu.find(q[0]) == dsu.find(q[1]);
}
devolver los ans;
}
}
`` `

■ *Cómo correr*
■ *Paste la clase `Solution` en LeetCode, luego llama `distanceLimitedPathsExist(...)`. *

-...

### 4.2 Python (Python 3)

``python
de la importación Lista

# ---------- DSU...
clase DSU:
def __init__(self, n: int):
self.parent = list(range(n))
self.rank = [0] * n

def find(self, x: int) - título int:
si yo. parent[x]!= x:
self.parent[x] = self.find(self.parent[x]) # Compresión del camino
Vuélvete. parent[x]

def union(self, x: int, y: int) - título Ninguno.
xr, yr = self.find(x), self.find(y)
si xr == yr: retorno
si auto.rank[xr] se auto.rank[yr]:
self.parent[xr] = yr
elif self.rank[xr] > self.rank[yr]:
self.parent[yr] = xr
más:
self.parent[yr] = xr
auto.rank[xr] += 1

# -------- Principal...
Solución de clase:
def distance LimitedPathsExist(
auto, n: int, edgeList: List[List[int], consultas: List[List[int]]
) List[bool]:
# Attach original index to each query
q_with_idx = [q + [i] for i, q in enumerate(queries)]

# Sort edges " queries
edgeList.sort(key=lambda x: x[2])
q_with_idx.sort(key=lambda x: x[2])

dsu = DSU(n)
as = [False] * len(queries)
e_idx = 0

para q en q_with_idx:
límite = q[2]
mientras que e_idx se hizo len(edgeList) y edgeList[e_idx][2]
dsu.union(edgeList[e_idx][0], edgeList[e_idx][1])
e_idx += 1
ans[q[3]] = dsu.find(q[0]) == dsu.find(q[1])

Retorno
`` `

■ *Run*
■ * Sube la clase 'Solution' a LeetCode y corre. *

-...

### 4.3 C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

--------- DSU...
Clase DSU {}
public:
vector:
DSU(int n) : parent(n), rnk(n, 0) {
iota(parent.begin(), parent.end(), 0);
}
int find(int x) {
volver padre[x] == x ? x : parent[x] = encontrar(parent[x]); // path compresión
}
vacío unite(int x, int y) {
int xr = find(x), yr = find(y);
si (xr == yr) regresa;
si (rnk[xr] se hacía [yr]) padre [xr] = yr;
si (rnk[xr] > rnk[yr]) padre [yr] = xr;
otra vez
parent[yr] = xr;
++rnk[xr];
}
}
};

// -------- Principal...
Clase Solución {
public:
vector asignadobool confianza distanciaLimited PathsExist(int n,
vector de vectores borde Listo,
vector asignador implicados iguales consultas) {}
int m = consultas.size();
// guardar consultas como [u, v, limit, original_idx]
vector realizador realizado, 4 títulos qs
qs.reserve(m);
para (int i = 0; i)
qs.push_back({queries[i][0], queries[i][1], queries[i][i], i});

(edgeList.begin(), edgeList.end(),
[](cont auto ' , const auto &b){ devolver a [2]  obtenidos b[2]; });

(qs.begin(), qs.end(),
[](cont auto ' , const auto &b){ devolver a [2]  obtenidos b[2]; });

DSU dsu(n);
vector:
size_t eIdx = 0;

para (auto &q : qs) {
límite de entrada = q[2];
mientras (eIdx) se observó bordeList.size() " curva edgeList[eIdx][2]
dsu.unite(edgeList[eIdx][0], edgeList[eIdx][1]);
+ eIdx;
}
ans[q[3]] = (dsu.find(q[0]) == dsu.find(q[1]));
}
devolver los ans;
}
};
`` `

■ Compile**
* " g+ " -std=c+17 -O2 solution.cpp "

-...

## 5. Cómo funciona el programa juzgará su presentación

1. **La calidad de los fondos* Los tres idiomas usan nombres claros, comentarios en línea, y ninguna constante mágica.
2. ** Maneje por caso electrónico** – Las soluciones manejan correctamente **multi-edges** y ** límites grandes** (sin flujo de entero).
3. *La complejidad del tiempo* La entrevista notará que no estás haciendo una ingenua BFS/DFS para cada consulta.
4. **La lengua versatilidad** – Puede presentar las tres soluciones en una entrevista o prueba técnica.

-...

## 6. Siguientes pasos: Pulsa tus habilidades de entrevista

Silencio ↑ Recibir recursos ❌ Sugerido para leer
Silencio...
* algoritmos de gráfico* Silencio *Union‐Find* en *Cracking the Coding Interview* Silencio
*LeetCode discusión* Silencio Thread on *1697 hard* para casos de borde extra
TENIDO *C++ STL* ANTE `iota`, `sort`, `vector` Silencio
Silencio *Python* Silencio `functools.lru_cache` para la memoización de `encontrar' si prefieres la recursión
*Java* Silencioso `Arrays.sort` + `Comparador.comparing Int` Silencio

-...

#### 🎯 Final Thought

Con esta solución **union‐find**, puedes resolver LeetCode 1697 en un segundo en la entrada más dura.
Mostrar reclutadores puede traducir un algoritmo deslizante en código limpio en **Java, Python, C++**, y usted será un paso más cerca de esa entrevista de sueños.

Buena suerte, y feliz codificación! 🚀

-...

**No dude en copiar/pasar cualquiera de las tres implementaciones anteriores, ejecutarlas localmente, y presumir en su día de entrevista!**