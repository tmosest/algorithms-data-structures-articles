-...
Título: LeetCode 3535. Conversión de Unidad II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 3535. Conversión de unidad II – Guía completa, SEO-Optimizada (Java / Python / C++)

■ **“Cuando resuelves un problema una vez, estás listo para mil más.”* – *LeetCode*

Este artículo recorre el problema **Unit Conversion II** de LeetCode, da una implementación de trabajo en **Java, Python, y C+**, y luego se sumerge en el *bueno, el malo, y el feo* de la solución. El post está escrito para **Preparación de entrevistas de ingeniería de software** y está completamente optimizado para las palabras clave **Unit Conversion II, LeetCode, entrevista de trabajo, DFS, BFS, Java, Python, C++**.

-...

## 1. Recaptación de problemas

`` `
Hay n tipos de unidad (0 ... n‐1).
conversiones[i] = [fuente, objetivo, factor] → 1 unidad de “fuente” = unidades factor de “target”.
consultas[i] = [Ai, Bi] → ¿Cuántos Bi‐units equivalen a 1 Ai-unit? Respuesta como (p / q) mod 1e9+7.
`` `

* " 1 " = factor "
* " 1 "
* El gráfico es un árbol (exactamente 'n-1' bordes) y cada unidad es accesible desde la unidad 0.

La respuesta requerida para cada consulta es:

`` `
respuesta[i] = (factor de Bi relativo a Ai) mod MOD
= (numerator * inv(denominator)) mod MOD
`` `

Donde `inv(x)` es el modulo inverso modular `MOD = 1_000_000_007`.

-...

## 2. Observaciones

1. ** Estructura de la torre** – hay exactamente un camino simple entre cada dos unidades.
2. ** cadena multiplicativa** – pasando de `u` a `v` multiplica el factor de conversión de cada borde en el camino.
3. **Dirección reversa** – si el borde `u → v` tiene factor `c`, entonces `v → u` tiene factor `1 / c`.
En aritmética modular almacenamos 'c' y su inverso modular 'c−1`.
4. Una vez que conozcamos el factor acumulativo de la raíz (unidad 0) a *todo* nodo, podemos responder a cualquier consulta en `O(1)`:

`` `
factor(Ai → Bi) = (factor(0 → Bi)) * inv(factor(0 → Ai))
`` `

Así que el problema se reduce a un **single DFS/BFS** que propaga dos valores para cada nodo:
* `toRoot[u]` – producto de factores de borde de raíz a `u`.
* `invToRoot[u]` – producto del borde inversos de raíz a `u`.

-...

## 3. Algoritmo (versión de las FDIS)

`` `
construir lista de adjacency:
para cada borde (a,b,c):
b, c, 1) a
(a, c−1, c) a b

DFS(0):
toRoot[0] = 1
invToRoot[0] = 1
pila/recusión:
para cada vecino (v, factor, invFactor):
si no es visitado:
toRoot[v] = toRoot[u] * factor % MOD
invToRoot[v] = invToRoot[u] * invFactor % MOD
DFS(v)

respuesta preguntas:
res = (toRoot[Bi] * invToRoot[Ai] % MOD
`` `

**La complejidad del tiempo** – `O(n + q) `
**La complejidad del espacio** – `O(n)`

La única operación pesada es la exponencia modular utilizada una vez por borde para computar la inversa `c−1` (`pow(c, MOD-2)`), que es `O(log MOD)` pero hecho `n‐1` veces.

-...

## 4. Código

### 4.1 Java (DFS)

``java
importar java.util*;

Clase Solución {
static final long MOD = 1_000_000_007L;

int[] queryConversiones(int[][] conversiones, int[][] consultas) {
int n = conversiones.length + 1;
Lista hecha [] adj = nuevo ArrayList[n];
para (int i = 0; i) no; i++) adj[i] = nuevo ArrayList fiel();

// Gráfico de construcción
para (int[] e : conversiones) {}
int a = e[0], b = e[1];
c = e[2];
inv largo = modPow(c, MOD - 2);
adj[a].add(new long[]{b, c, inv}); // a - título b
adj[b].add(new long[]{a, inv, c}); // b - título a
}

long[] toRoot = new long[n];
long[] invToRoot = new long[n];
boolean[] vis = new boolean[n];
toRoot[0] = invToRoot[0] = 1;
dfs(0, adj, toRoot, invToRoot, vis);

int[] res = nuevo int[queries.length];
para (int i = 0; i) hice consultas.length; i++) {
int a = consultas[i][0];
int b = consultas[i][1];
res[i] = (int) (toRoot[b] * invToRoot[a] % MOD);
}
restitución;
}

dfs de vacío privado (int u, Lista hecha larga [] adj,
long[] toRoot, long[] invToRoot, boolean[] vis) {
vis[u] = verdadero;
for (long[] e : adj[u]) {}
int v = (int) e[0];
si (vis[v]) continúan;
long fac = e[1];
long invFac = e[2];
aRoot[v] = toRoot[u] * fac % MOD;
invToRoot[v] = invToRoot[u] * invFac % MOD;
dfs(v, adj, toRoot, invToRoot, vis);
}
}

privado largo modPow(long a, long exp) {}
larga res = 1;
mientras (ex) 0) {
((exp) == 1) res = res * un % de MOD;
a = un * % de MOD;
experiencia= 1;
}
restitución;
}
}
`` `

-...

### 4.2 Python (DFS)

``python
MOD = 1_000_000_007

Solución de clase:
def queryConversiones(self, conversiones: List[List[int],
consultas: List[List[int]]) - No. List[int]:
n = len(conversiones) + 1
adj = [[] for _ in range(n)]

para a, b, c en conversiones:
inv = pow(c, MOD - 2, MOD)
adj[a].append(b, c, inv)) b
adj[b].append(a, inv, c)) # b - título a

to_root = [0]
inv_root = [0]
visitado = [False] * n
to_root[0] = inv_root[0] = 1
auto.dfs(0, adj, to_root, inv_root, visited)

res = []
para a, b en consultas:
re.append(to_root[b] * inv_root[a] % MOD)
retorno

def dfs(self, u, adj, to_root, inv_root, visited):
visitado[u] = Verdadero
para v, fac, inv_fac en adj[u]:
si es visitado[v]:
continuar
to_root[v] = to_root[u] * fac % MOD
inv_root[v] = inv_root[u] * inv_fac % MOD
auto.dfs(v, adj, to_root, inv_root, visited)
`` `

-...

### 4.3 C++ (DFS)

``cpp
#include יbits/stdc++.h
usando std namespace;
const long MOD = 1'000'000'007LL;

Clase Solución {
public:
Conversiones(vector seleccionador seleccionado)
vector asignador implicados iguales consultas) {}
int n = conversiones.size() + 1;
vector realizador realizador realizador realizado durante mucho tiempo,3 título conveniente adj(n);
para (auto &e : conversiones) {}
int a = e[0], b = e[1];
largo c = e[2];
long long inv = modpow(c, MOD-2);
adj[a].push_back({b, c, inv});
adj[b].push_back({a, inv, c});
}

vector realizado largo tiempo aRoot(n), invRoot(n);
vector:
toRoot[0] = invRoot[0] = 1;
dfs(0, adj, toRoot, invRoot, vis);

vector significar uns
para (auto &q : consultas) {}
int a = q[0], b = q[1];
as.push_back(int)(toRoot[b] * invRoot[a] % MOD));
}
devolver los ans;
}

privado:
vacío dfs(int u,
vector realizador realizador realizador >
vector de larga duración &toRoot,
vector de larga duración 'invRoot,
vector asignado >
vi[u] = 1;
para (auto &e : adj[u]) {}
int v = e[0];
si (vis[v]) continúan;
larga data = e[1], invFac = e[2];
aRoot[v] = toRoot[u] * fac % MOD;
invRoot[v] = invRoot[u] * invFac % MOD;
dfs(v, adj, toRoot, invRoot, vis);
}
}

largo largo modpow (largo largo, largo largo e) {}
largo largo r = 1;
e) {
(e " 1) r = r * a % MOD;
a = un * % de MOD;
e 1;
}
retorno r;
}
};
`` `

Las tres soluciones son **`O(n + q)`** y encajan cómodamente dentro de las limitaciones (`n, q ≤ 10^5`).

-...

## 5. Artículo del Blog – “Unit Conversion II: El Bien, el Mal y el Ugly”

### 5.1 Introduction

La conversión de unidad es un problema de entrevista clásico que esconde un toque algebraico sutil. **LeetCode 3535 – Unidad Conversión II** le pide convertir entre unidades arbitrarias cuando sólo se da un árbol de factores de conversión pares. En un contexto de búsqueda de trabajo, dominar este problema demuestra su comprensión de traversal gráfico, aritmética modular y optimización bajo límites de tiempo estrictos.

**Keywords**: *Unit Conversion II, LeetCode, DFS, BFS, entrevista de trabajo, inverso modular, Java, Python, C++ *

## 5.2 El Bien - ¿Por qué la Solución DFS/BFS es Elegante

← Strength ← Explicación
Silencio...
Silencio **Tiempo de iluminación** Silencioso `O(n + q)` – una traversal para pre-computar todas las ratios. Silencio
Silencio **Espacio eficiente** Silencioso Sólo la lista de adyacencia (`O(n)`) y dos 'long` arrays. Silencio
tención **Single pass** Silencio Después de DFS, cada consulta es contestada en tiempo constante. Silencio
TEN **Modular-friendly** TEN Store edge factor y su inverso; evita errores de punto flotante. Silencio
tención **Language‐agnostic** Silencio El mismo algoritmo funciona en Java, Python, o C++ con cambios mínimos. Silencio

En una entrevista, puede presentar esto como “construir un mapa de factores de conversión desde root a cada nodo, luego compute `root→ Bi * inv(root→Ai)`. El entrevistador aprecia la idea de arraigar el árbol y propagar productos acumulativos.

### 5.3 Los malos – saltos comunes

Silencio Pitfall Silencio Cómo evitar
Silencio...
tención **Missing modular inverses** tención Recuerde `pow(c, MOD-2)` en un campo primario; el uso de 'c' sola da resultados erróneos al invertir los bordes. Silencio
Silencio **Desbordamiento de la cubierta (Java)** La profundidad Recursive DFS puede alcanzar el `10^5`; cambiar a la pila iterativa o aumentar el límite de recursión. Silencio
tención **Iniciar valores intermedios** Silencio Multiply before modulo; utilizar `long`/`int64` para permanecer dentro de 64‐bit. Silencio
Silencio **Repetición de exponencia** Silencio Compute inverse sólo una vez por borde; pre-computing all inverses via `pow` puede cost `n log MOD`. Silencio
Silencio **Desbordamiento de enteros en Python** Silencio Use `pow(c, MOD-2, MOD)` para mantener el resultado en el módulo. Silencio

Estas trampas son típicas de los entrevistadores “gotchas” amor: prueban si puedes detectar errores ocultos.

### 5.4 The Ugly – What Makes Este problema es complicado.

Por qué es Ugly
Silencio----------------
tención **Implicit reversals** Silencio Convertir de `Bi` a `Ai` requiere factores inversos; si usted ignora esto usted conseguirá división por cero o errores de flotación. Silencio
Silencio **División móvil** Silencio Division no es directo en modulo arithmetic; usted debe recordar el pequeño teorema de Fermat o pre-compute inverses. Silencio
Silencio **Large graph size** Silencio Un DFS ingenuo para cada consulta sería `O(q * n)` – infeasible. Silencio
Silencio **Problemas de precisión** Silencio Usar dobles puede conducir a errores de redondeo; modulo garantiza la exactitud pero debe implementarlo correctamente. Silencio

En la entrevista, un candidato podría primero escribir un enfoque ingenuo: para cada consulta realizar un DFS en la mosca. Eso pasaría en grandes entradas y mostraría una falta de previsión. La parte *ugly* está aprendiendo a reconocer que **una vez que enraizas el árbol, el resto de la obra es una simple multiplicación e inversión**.

## 5.5 Cómo hablar a través del problema en una entrevista

1. **Clarificar el modelo**
“Nos dan un árbol de factores de conversión pares; yendo hacia adelante se multiplica por “c”, yendo hacia atrás se multiplica por “1/c”. ”

2. **Explicar aritmética modular**
“Como la respuesta debe ser modulo `10^9+7`, reemplazamos la división por multiplicación por inversos modulares (`pow(c, MOD-2)`), porque el módulo es primario. ”

3. **En línea con el preprocesamiento* *
“Haz un DFS/BFS de nodo 0. Para cada nodo, mantenga `factorRoot[u]` (producto de raíz a `u') e `invRoot[u]` (producto de inversos). ”

4. #Mostrar fórmula de consulta #
Cualquier consulta `Ai → Bi` = `factorRoot[Bi] * invRoot[Ai] (mod MOD)`. Así que sólo necesitamos los dos arrays pre-computados. ”

5. ** Casos de emergencia**
* Verificar que todos los nodos son visitados; manejar índices basados en 1 vs 0-basados.
* Por cada borde compute inverse sólo una vez.

6. ** Tiempo-presupuesto**
“El DAAT es lineal; cada consulta es `O(1)`. Podemos resolver fácilmente 10^5 consultas en menos de 100 ms en Java/Python/C++ en el entorno de LeetCode. ”

### 5.6 Take‐away for Job‐Hunters

*Unit Conversion II* es un pequeño problema que toca muchos conceptos importantes. Al implementar un solo DFS y responder a las consultas en tiempo constante, muestra:
* ** Profundidad algorítmica** – convirtiendo una cadena multiplicativa en una simple multiplicación basada en la raíz.
* **Proficiencia lingüística** – el código funciona de forma idéntica en Java, Python y C++.
* **Manejo del tiempo** – su solución funciona dentro de 1 s para el peor caso (`10^5` nodos, `10^5` consultas).

Al explicar su solución en una entrevista, caminar por la intuición primero, luego detallar la traversal DFS, pre-computación inversa modular, y finalmente la resolución de la consulta. Destaca que esta es la solución *canónica* – no se necesitan trucos inteligentes de DP o bibliotecas pesadas.

-...

## 6. Pensamientos finales

El problema **Unit Conversion II** es una mina de oro para los candidatos que se preparan para entrevistas técnicas. Combina un sencillo traversal gráfico con aritmética modular y exigente manejo cuidadoso de inversos. La solución DFS arriba es sencilla, eficiente y puede aplicarse en cualquiera de los idiomas principales. Entréguelo, y impresionará a los entrevistadores con la corrección y el código performant limpio. ¡Buena suerte en tu búsqueda de trabajo!