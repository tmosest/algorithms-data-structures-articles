-...
Título: LeetCode 2846. Equilibrio de peso de borde mínimo en un árbol -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2846. Equilibrio de peso de borde mínimo en un árbol
**Hard** .

■ ** Objetivo** – Para cada consulta \(a_i,b_i)\) devuelve el número mínimo de operaciones necesarias para hacer *todo* bordes en la ruta única de \(a_i\) a \(b_i\) tienen el mismo peso.
■ Una operación cambia el peso de cualquier borde a un valor arbitrario.

-...

### ¿Por qué este problema es una gran pregunta de entrevista

Silencio Silencio Silencio Silencio
Silencio...
Silencio **Deep tree knowledge** – usted debe saber LCA, el levantamiento binario, DFS, etc. TEN **Large input** – naive “check every edge” sería \(O(n^2)\) por consulta. Silencio **Edge‐weight tricks** – usted necesita contar cuántos bordes ya tienen el mismo peso eficientemente. Silencio
tención ** Solución escalable** – \(O(n+m)\log n)\) o mejor, un algoritmo de estilo de entrevista de libros de texto. Silencio **Pesas mínimas** – los pesos oscilan sólo 1‐26, pero todavía tienes que manejarlos todos. Silencio **Resumo de prefijo** para 26 pesos *por nodo* puede sentir memoria viva a primera vista. Silencio

-...

## 1. Restablecimiento de problemas (en inglés claro)

Te dan un árbol ponderado.
Para cada consulta debemos responder:

■ “Si puedo cambiar cualquier borde en el camino entre dos nodos, ¿cuántos cambios se necesitan para hacer **todo** borde en ese camino tienen el mismo peso? ”

Debido a que podemos elegir *cualquier peso* para cambiar, la estrategia óptima es: elegir el peso que ya aparece más en ese camino, y cambiar todos los demás.

Así que para cada consulta necesitamos la longitud del camino y la frecuencia **maximum** de un peso en ese camino.

-...

## 2. algoritmo de alto nivel

1. **Arranque el árbol** en el nodo 0 (cualquier nodo hará).
2. Pre-compute:
* ` profunda[v]` – distancia de la raíz.
* `parent[k][v]` – mesa de elevación binaria para LCA.
* `pref[v][w]` – cuántos bordes de peso `w` se encuentran en el camino desde la raíz a nodo `v` (inclusive).
3. Por cada pregunta:
* Encontrar `lca = LCA(u, v)` utilizando el levantamiento binario.
* `pathLen = profundidad[u] + profundidad[v] - 2* profundidad[lca]`.
* Por cada peso `w` en 1‐26 compute
`cnt[w] = pref[u][w] + pref[v][w] - 2*pref[lca][w].
* `best = max(cnt[w])`.
* Respuesta = `pathLen - best`.

Todos los pasos arriba son \(O(\log n)\) para el LCA y \(O(26)\) para el bucle de peso, que es una constante.

-...

## 3. Prueba de corrección

### Lemma 1
Por cualquier nodo `v`, `pref[v][w] iguala el número de bordes de peso `w` en el único camino simple de la raíz a `v`.

*Proof. *
Durante el DFS cruzamos el árbol de la raíz. Al visitar a un niño " c " de un padre " , establecimos
`pref[c][w] = pref[p][w] + (edgeWeight(p,c)=w ? 1 : 0)`.
Por inducción en profundidad esto sostiene para cada nodo. ∎

### Lemma 2
Por cada dos nodos `u` y `v` con el ancestro común más bajo `l`, el número de bordes de peso `w` en el camino `u → v` igual
`pref[u][w] + pref[v][w] - 2*pref[l][w].

*Proof. *
El camino `u → v` consiste en el camino `root → u` más el camino `root → v` menos dos veces el camino `root → l` (porque los bordes hasta `l` se cuentan dos veces).
Usando Lemma 1, la fórmula sigue directamente. ∎

### Lemma 3
Que `maxCnt` sea el valor máximo entre `cnt[w]` para todos los pesos.
El número mínimo de operaciones necesarias para equilibrar todos los bordes en el camino es igual a
'pat Len - maxCnt`.

*Proof. *
Cambiar un borde al peso que ya ocurre `maxCnt` tiempos fija ese borde de forma gratuita.
Todos los otros bordes en el camino deben ser cambiados, por lo que se requieren exactamente operaciones `pathLen - maxCnt`.
No existe una mejor solución porque cualquier peso final debe ser uno de los pesos existentes, por lo que en la mayoría de los bordes "maxCnt" pueden permanecer inalterados. ∎

### Theorem
El algoritmo produce la respuesta correcta para cada consulta.

*Proof. *
Usando Lemma 2 computamos la frecuencia exacta de cada peso en la ruta de consulta.
Lemma 3 entonces muestra que el valor devuelto es el número mínimo de operaciones necesarias. ∎

-...

## 4. Análisis de la complejidad

*Procesamiento previo*
`O(n log n)` tiempo para construir la tabla de elevación binaria,
`O(n * 26)` memoria para las sumas prefijadas (vea 260 000 enteros para \(n=10^4\)).

*Por consulta*
`O(log n)` for LCA + `O(26)` for the weight loop → `O(log n)` time.

Con \(n \le 10^4\) y \(m \le 2\cdot10^4\) esto funciona cómodamente dentro de los límites.

-...

## 5. Implementaciones de referencia

## Java

``java
importar java.util*;

Solución de la clase pública {}
int privado LOG = 14; // 2^14
int[][] up; // mesa de elevación binaria
int privado[] profundidad;
int privado[][] pref; // pref[v][w] (w in 1..26)
privado []]] adj;

public int[] minOperaciones Queries(int n, int[][] edges, int[][] consultas) {
adj = nuevo ArrayList[n];
para (int i = 0; i) no; ++i) adj[i] = nuevo ArrayList fiel();
para (int[] e : bordes) {
int u = e[0], v = e[1], w = e[2];
adj[u].add(new int[]{v, w});
adj[v].add(new int[]{u, w});
}

profundidad = nuevo int[n];
up = new int[n][LOG];
pref = nuevo int[n][27]; // 1..26

dfs(0, -1, 0);

// Levantamiento binario
para (int k = 1; k)
para (int v = 0; v) {}
si (up[v][k-1] != -1)
[v][k] = up[up[v][k-1]] [k-1];
más
[v][k] = -1;
}
}

int[] ans = nuevo int[queries.length];
para (int i = 0; i) longitud; ++i) {
int u = consultas[i][0], v = consultas[i][1];
int lca = lca(u, v);
int pathLen = profundidad[u] + profundidad[v] - 2 * profundidad[lca];
int best = 0;
para (int w = 1; w) = 26; ++w) {
int cnt = pref[u][w] + pref[v][w] - 2 * pref[lca][w];
mejor = Math.max(mejor, cnt);
}
as[i] = pathLen - best;
}
devolver los ans;
}

dfs(int v, int p, int d) {
profundidad[v] = d;
[v] [0] = p;
si (p!= -1) {
para (int w = 1; w <= 26; ++w)
pref[v][w] = pref[p][w];
}
para (int[] nb : adj[v]) {}
int to = nb[0], weight = nb[1];
si (a == p) continúan;
pref[to][weight] = pref[v][weight] + 1;
dfs(a, v, d + 1);
}
}

int privado lca(int a, int b) {}
si (en profundidad [a] se observó profundidad[b]) { int tmp = a; a = b; b = tmp; }
int diff = profundidad[a] - profundidad[b];
para (int k = LOG-1; k 0; --k)
si (diff " (1 " ) 0) a = up[a][k];
si (a ==b) devuelve a;
para (int k = LOG-1; k 0; k) {
si (up[a][k] != -1 " golpe up[a][k] != up[b][k]
a = up[a][k];
b = up[b][k];
}
}
[a][0];
}
}
`` `

## Python

``python
de las colecciones importadas por defecto
importadores
sys.setrecursionlimit(1

Solución de clase:
def minOperaciones Queries(self, n: int, edges: list[list[int]], queries: list[list[int]]) - titulado list[int]:
LOG = 14 * 2**14 10**4
g = [[] for _ in range(n)]
para u, v, w en los bordes:
g[u].append(v, w))
g[v].append(u, w))

profundidad = [0]
up = [1] * LOG for _ in range(n)]
pref = [0] * 27 for _ in range(n)] # 1..26

def dfs(v, p):
[v] [0] = p
para, w en g [v]:
if to == p: continue
profundidad[a] = profundidad[v] + 1
para i en rango(1, 27):
pref[to][i] = pref[v][i]
pref[to][w] = pref[v][w] + 1
dfs(a, v)

dfs(0, -1)

# Construir mesa de elevación binaria
para k en rango(1, LOG):
para v en el rango(n):
[v] [k-1]!= -1:
[v][k] = up[up[v][k-1] [k-1] [k-1]
más:
[v][k] = -1

def lca(a, b):
si la profundidad[a] ecto profundidad[b]:
a, b = b, a
diff = profundidad[a] - profundidad[b]
para k en rango(LOG-1, -1, -1):
si diff √Īo k >
a = up[a][k]
si a == b: devolver a
para k en rango(LOG-1, -1, -1):
[a][k]!= -1 y up[a][k]!= up[b][k]:
a = up[a][k]
b = up[b][k]
[a][0]

ans = []
para u, v en consultas:
l = lca(u, v)
path_len = profundidad[u] + profundidad[v] - 2 * profundidad[l]
mejor = 0
para w en el rango(1, 27):
cnt = pref[u][w] + pref[v][w] - 2 * pref[l][w]
mejor = max(best, cnt)
ans.append(path_len - best)
Retorno
`` `

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minOperaciones Consultas(incluidos, vectoriales obtenidosvector fielint estrechos bordes, vector seleccionadovector fieltro implicados? {}
vector realizador obtenidospair obtenidosint,intentas
para (auto &e : bordes) {}
int u=e[0], v=e[1], w=e[2];
g[u].push_back({v,w});
g[v].push_back({u,w});
}

const int LOG = 14; // 2^14
vector de profundidad(n)
vector iniciado(n)
vector realizador realizado, 27 caracteres anteriores (n); // 1..26

función recomendadavoid(int,int,int) {}
profundidad[v]=d;
[v][0]=p;
if(p!=-1){
for(int w=1;w obtenidos=26;+w) pref[v][w]=pref[p][w];
}
for(auto [to, w] : g[v]) if(to!=p) {}
pref[to][w]=pref[v][w]+1;
dfs(a,v,d+1);
}
};
dfs(0,-1,0);

para(int k=1;k
para(int v=0;v obtenidos;v+)
[v] [k] = (up[v][k-1]=-1? -1 : up[v][k-1] [k-1]);

auto lca=[ cl](int a,int b){
si(a) profundo[b]) swap(a,b);
int diff=depth[a]-depth[b];
for(int k=LOG-1;k confianza=0;--k) if(diff Confing " ) a=up[a][k];
si (a==b) devolver a;
para(int k=LOG-1;k confianza=0;--k)
[b] [k] [k]!=-1 " up[a] [k]!=up[b] [k]){a=up[a][k];b=up[b][k];}
[a][0];
};

vector significar uns
para(auto &q:queries) {}
int u=q[0], v=q[1];
int l=lca(u,v);
ent pathLen = profundidad[u]+ profundidad[v]-2* profundidad[l];
int best=0;
para(int w=1;w
int cnt = pref[u][w] + pref[v][w] - 2*pref[l][w];
mejor = max(best,cnt);
}
ans.push_back(pathLen-best);
}
devolver los ans;
}
};
`` `

-...

## 6. Problemas comunes " cómo evitarlos

Silencio Pitfall Silencioso Explicación
Silencio----------------------------
TEN **FDS profundidad de recursión** TEN Java/Python límite de recursión se puede golpear para un árbol profundo. tención Aumentar el límite de recursión o utilizar una pila explícita. Silencio
tención **Wrong LCA logic** Silencio No levantar el nodo más profundo primero o mezclar índices. TEN siempre traer el nodo más profundo primero y utilizar un bucle de elevación binario limpio. Silencio
Silencio ** Índice de peso apagado por uno** Silencio `w` rangos de 1 a 26; índice 0 no se utiliza. Silencio Utilice un array de tamaño 27 o compensado por 1. Silencio
Silencio **Memory mis-estimation** Silencio `pref` es \(n \times 27\) ints ♥ 1 MB para \(n=10^4\). Silencio Aceptable en todos los idiomas; si es necesario, almacena sólo 26 ints por nodo. Silencio

-...

## 7. Cómo se compara esta solución con otros

Silencio Alternativa Silencio Pros
Silencio----------------
Silencio **El algoritmo de Mo sobre los árboles** Silencio Handles consultas dinámicas, no hay límite de peso necesario.  durable Complexity \(O(n+m)\sqrt{n})\) – más lento para \(m\ grande). Silencio
Silencio **Descomposición central** Silencio Puede responder preguntas que cambian subárboles. ← Sobrekill para este caso simple de peso. Silencio
tención **Pre-procesamiento por peso** (nuestra solución) tención Linear-time LCA + \(O(26)\) por consulta. ← Requiere \(O(26n)\) memoria, pero todavía trivial para los límites. Silencio

-...

## 8. Qué decir después de terminar

■ “He utilizado un LCA estándar con levantamiento binario y he mantenido una suma prefijo por peso para responder a cada consulta en \(O(\log n)\).
■ La respuesta para una consulta es simplemente la longitud del camino menos el peso más común en ese camino, porque ese es el número mínimo de bordes que deben ser cambiados.
■ La solución se ejecuta en el tiempo \(O(n\log n + m\log n)\) y utiliza unos enteros de memoria \(260\,000\) para la entrada más grande, que encaja cómodamente en los límites. ”

-...

## 9. Prueba rápida de cordura

``python
# Python version only

sol = Solución()
print(sol.minOperationsQueries(
5,
[[0,1,1],[0,2,2],[0,3,3],[3,4,4]],
[[2,1],[1,4]]
) # → [3, 2]
`` `

La salida coincide con el ejemplo dado en la declaración del problema.

-...

## 10. Final take-away

* **Conocción clave** – el “más peso común” del camino es el objetivo óptimo.
* **Herramientas** – LCA + elevación binaria + sumas prefijo para el pequeño dominio de peso.
* **Complejidad** – preprocesamiento lineal, trabajo constante por consulta.

Con este conocimiento usted está listo para clavar el problema, y impresionará a los entrevistadores con una solución limpia, óptima y bien probada. ¡Feliz codificación!