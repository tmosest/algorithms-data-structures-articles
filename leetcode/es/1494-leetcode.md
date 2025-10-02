-...
Título: LeetCode 1494. Cursos paralelos II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Cursos paralelos II (Leetcode 1494) – De la entrevista al trabajo

■ **TL;DR**
■ *Parallel Courses II* es un problema difícil de DP-bitmask que prueba su capacidad de pensar en estados, generar subconjuntos eficientemente, y prune el espacio de búsqueda.
■ La clave para clavar la entrevista es entender **representación del estado**, ** lógica de transición**, y ** trucos de ejecución**.
■ El siguiente artículo explica el problema, muestra soluciones de trabajo en **Java**, **Python**, y **C+**, y discute el *bueno, el malo, y el feo* del enfoque DP‐bitmask.
■ Bono: SEO copia optimizada que hará que su blog o portafolio se clasifican en Google para las palabras clave de entrevista exacta!

-...

### 1. Declaración de problemas (tema 1494)

`` `
Hay n cursos etiquetados de 1 a n.
relaciones[i] = [a, b] significa curso que debe tomarse antes del curso b.

Cada semestre se puede tomar en la mayoría de k cursos,
pero sólo si todos sus requisitos ya han sido tomados.

Devuelve el número mínimo de semestres requeridos para terminar todos los cursos.
Los casos de prueba están garantizados para ser solvables (el gráfico es un DAG).
`` `

TENIDO 1 ≤ 15 TENIDO 1 ≤ k ≤ n TENIDO 0 ≤ relaciones.length ≤ n n n‐1)/2 ANTE

-...

### 2. Intuición – ¿Por qué Bitmask DP?

- **Estado** = " conjunto de cursos ya completados " .
Con *n* ≤ 15, un entero de 16 bits puede codificar todos los subconjuntos → **2n estados**.
- En cada semestre elegimos un subconjunto de cursos *disponibles* (indegree = 0) con tamaño ≤ k.
- Computar la respuesta para el nuevo estado.
- Memoizar para evitar recomputar el mismo subconjunto.

Este es el patrón clásico *DP sobre subsets* que aparece en problemas como “Course Schedule III”, “Minimum Number of Taps”, etc.

-...

### 3. Resumen del algoritmo

1. **Registro de adyacency** y array indegree.
2. **DFS + memoización** en el estado de bitmask:
* Si todos los cursos tomados → retorno 0.
* Identifique cursos *disponibles*: indegree = 0 y no en máscara.
* Enumerar todos los subconjuntos de cursos disponibles cuyo tamaño ≤ k.
Para cada subconjunto:
* Cursos de marca como tomado → nuevoMask.
* Actualizar los ingresos para niños → newIndegree.
* Recurse: `1 + dfs(newMask, newIndegree)`.
* Tome el mínimo sobre todos los subconjuntos.
3. Devuelve el resultado de la llamada inicial.

#### Optimizaciones

Problema de la vida
Silencio...
Silencio Enumerating **k**-subsets ingenuamente (O(2^m)) Silencio Pre-generar todas las combinaciones de tamaño 1...k para cada `m` (≤ n) o utilizar trucos de bits (`_construido_popcount` en C++). Silencio
TEN Re-allocating indegree array each recursion ANTE Pass it by reference and revert changes after recursion. (Para la claridad copiamos – todavía rápido para n ≤ 15.) Silencio
← Duplicar trabajo cuando muchos cursos están disponibles ← Si `m <= k` sólo tomar todos los cursos disponibles en una sola vez (sin ramificación). Silencio

-...

### 4. Prueba de corrección

Demostramos por inducción sobre el número de cursos restantes que el algoritmo devuelve el número óptimo de semestres.

*Base*: Cuando la máscara es igual a " (1 obtenidos)-1 " , se toman todos los cursos. El algoritmo devuelve 0, que es óptimo.

*Paso de inducción*: Asume para cualquier máscara con *t* cursos restantes el algoritmo devuelve el óptimo. Considere un estado con *t+1* cursos restantes.
Seamos el conjunto de cursos disponibles en este estado. Cualquier horario óptimo debe elegir algún subconjunto `X ⊆ S` con ØX para tomar en el próximo semestre, porque no podemos tomar un curso cuyos requisitos son incompletos.

El algoritmo enumera **todo** tal `X`.
Para cada `X`, compute `1 + óptimo(S', X)` donde `S' es la nueva máscara.
Por la hipótesis de inducción, `optimal(S', X)` es el número óptimo de semestres para los cursos restantes después de tomar 'X'.
Por lo tanto el algoritmo considera todos los posibles primeros pasos óptimos y devuelve el mínimo, que equivale al valor óptimo para el estado actual. ∎

-...

### 5. Análisis de la complejidad

- ** Estados**: 2n ' (≤ 32 768 para n = 15).
- **Por estado**: enumerar subconjuntos de cursos disponibles (`C(m,1)+...+C(m,k)`), el peor caso `C(15,7) ♥ 6435`.
- **Hora**: `O(2n * C(n, k))' → ♥ 106 operaciones, fácilmente bajo 1 s.
- **Espacio**: `O(2n)` para la memoización + `O(n)` para los arrays de adyacency + indegree.
100 kB.

-...

### 6. Código

■ **Las tres implementaciones utilizan la misma lógica pero difieren solamente en sintaxis. #
■ Cada archivo es autocontenido y se puede copiar en el correspondiente editor Leetcode.

#### 6.1 Java (estilo de código)

``java
importar java.util*;

Clase Solución {
lista privada indicada[] Gráfico;
int[] indegree privado;
int[] memo;
int privada n, k;
int privado FULL_MASK;

int public int minNumberOfSemesters(int n, int[][] relations, int k) {
this.n = n; this.k = k;
esto. FULL_MASK = (1 " 0 " ) - 1;
gráfico = nueva lista[n];
para (int i = 0; i) no; ++i) grafito[i] = nuevo ArrayList fiel();
indegree = nuevo int[n];
for (int[] rel : relations) {}
int u = rel[0] - 1, v = rel[1] - 1;
graph[u].add(v);
indegree[v]+;
}
memo = nuevo int[1]
Arrays.fill(memo, -1);
dfs(0, indegree);
}

int privado dfs(mascara, int[] curIndegree) {
si (mask == FULL_MASK) devuelve 0;
si (memo[mask] != -1) memo de retorno;

// Buscar cursos disponibles
Lista realizadaInteger ventaja = nuevo ArrayList implicado();
para (int i = 0; i)
si ((mask нелили i) == [i] == 0)
valed(i);

int m = avail.size();
si (m <= k) { /// tomar todo a la vez
int newMask = máscara;
int[] nextInd = curIndegree.clone();
(int v : avail) {
nuevoMask TENIDO= 1 Se realizó v;
para (int child : graph[v]) siguiente Ind[child]--;
}
devolver memo[mask] = 1 + dfs(newMask, nextInd);
}

// Enumerar todos los subconjuntos de tamaño 1..k
int best = Integer.MAX_VALUE;
para (incluido sub = 1; subs)
si (Integer.bitCount(sub) continuar;
int newMask = máscara;
int[] nextInd = curIndegree.clone();
para (int idx = 0; idx = m; + idx)
si ((sub , título idx)
int v = avail.get(idx);
nuevoMask TENIDO= 1 Se realizó v;
para (int child : graph[v]) siguiente Ind[child]--;
}
mejor = Math.min(best, 1 + dfs(newMask, nextInd));
}
devolver memo[mask] = mejor;
}
}
`` `

■ *Por qué esta es una solución Java “buena”*
√≥ - Clear state‐to‐state memoization (`int[] memo`).
(n ≤ 15 → costo insignificante).
- Maneja el atajo `m <= k` que elimina un gran número de ramas.

-...

#### 6.2 Python (estilo funcional, `functools.lru_cache`)

``python
desde functools import lru_cache
de las colecciones importan defaultdict, deque
de la importación Lista

Solución de clase:
def minNumberOfSemesters(self, n: int, relations: List[List[int], k: int) - título int:
graph = [[] for _ in range(n)]
indeg = [0]*n
por a, b en las relaciones:
graph[a-1].append(b-1)
indeg[b-1] += 1

FULL = (1 < > n) - 1

@lru_cache(None)
def dfs(mask, indeg_tuple):
si máscara == FULL:
retorno 0
indeg = list(indeg_tuple)

# Cursos disponibles
use = [i for i in range(n)
si no (mask > i) > 1 e indeg[i] == 0]
m = len(avail)

si m
new_mask = máscara
for v in avail:
new_mask TENIDO= 1
para niños en el gráfico [v]:
indeg[child] -= 1
volver 1 + dfs(new_mask, tuple(indeg))

mejor = flotante('inf')
# enumerar subsets of size 1..k
para sub en el rango(1, 1  se hizo referencia m):
si sub.bit_count() > k:
continuar
new_mask = máscara
new_indeg = indeg[:]
para i en rango(m):
si sub- i
v = disponibilidad[i]
new_mask TENIDO= 1
para niños en el gráfico [v]:
new_indeg[child] -= 1
mejor = min(best, 1 + dfs(new_mask, tuple(new_indeg)))
mejor

dfs(0, tuple(indeg))
`` `

■ *¿Por qué esta es una solución de pitón “mala”? *
■ Python's `clone()` y la copia de la lista son *slower* pero todavía está bien para *n* = 15.
■ Para el código de producción, usted revertirá indegrejos en lugar de copiar.

-...

#### 6.3 C++ (Estilo de código postal)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minNumberOfSemesters(int n, vector identificadovector fielmente implicado relaciones reducidas, int k) {
vector realizador:
vector implicado(n, 0);
para (autor : relaciones) {}
int u = r[0]-1, v = r[1]-1;
g[u].push_back(v);
indeg[v]+;
}

const int FULL = (1 obtenidos)-1;
vector implicado dp(1 seleccionado, -1);

función realizada(int, vector identificadoint estrecho) = dfs = [ curva](int mask, vector seleccionadoint frecuentemente curIndeg) {}
si (mask == FULL) devuelve 0;
si (dp[mask] != -1) retorno dp[mask];

vector a);
para (int i=0;i obtenidos;+i)
si (!(mask confíai paciente1) " curIndeg[i]==0) vale.push_back(i);

int m = avail.size();
si (m <= k) { // tomar todo
int newMask = máscara;
(int v: avail) {
newMask tención= 1 obtenidav;
para (int child: g[v]) curIndeg[child]--;
}
dp[mask] = 1 + dfs(newMask, curIndeg);
}

int best = INT_MAX;
// Enumerar todos los subconjuntos de utilidad cuyo tamaño se indica= k
para (incluido sub = 1; subs)
si (__construido_popcount(sub) > k) continúan;
int newMask = máscara;
// Modificación temporal indegree
vector implicado siguienteIndeg = curIndeg;
para (int i=0;i obtenidosm;+i)
si (sub título) {
int v = avail[i];
newMask tención= 1 obtenidav;
para (int child: g[v]) siguienteIndeg[child]--;
}
mejor = min(mejor, 1 + dfs(newMask, nextIndeg));
}
dp[mask] = mejor;
};

dfs(0, indeg);
}
};
`` `

■ *¿Por qué esta es una implementación “buena” C+++? *
> - Usa `__construido_popcount` para cheques de tamaño de subconjunto rápido.
⇩ - Copias endegree sólo para la llamada recursiva; copiar es barato para `n ≤ 15`.
- Separación clara de *estado*, *transición* y *memoización*.

-...

### 7. Bien, Mal & Ugly – DP‐Bitmask in Interviews

Silencio Silencio
Silencio------------Prince------
Silencio ** Tamaño del Estado** (2n) Silencio** (`n ≤ 15`). Silencio **Exponencial** – cuidado de no exagerar a `n = 30`. Silencio **Inpredecible** para mayor n.o.
Silencio ** factor de corte** (enumeración de subconjunto) Silencio Puede ser podado por `m <= k` atajo. Silencio **O(2^m)** si usted ingenuamente prueba cada subconjunto → golpe exponencial. Silencio **Volver sin podar** conduce a TLE. Silencio
Silencio **Memoización** Silencio Clean `int[] memo` → O(2n). ← Olvidar los resultados → trabajo repetido. ← Usar un *map* en lugar de un array conduce a *memory overhead*. Silencio
Silencio **Indegree updates** tención Clone array o revertir cambios → O(n) por recursión. ← Actualizar globalmente en su lugar puede producir * estados inconsistentes*. Demasiados ejemplares pueden convertirse en un factor constante* desaceleración. Silencio
Silencio **Complejidad** ← Clear O(2n C(n,k))) análisis → entrevista-friendly. ↑ Mis‐stating the complex can make the interviewer suspicious. ← Sobre-optimizar (por ejemplo, trucos de bitset) puede distraerse de la idea central. Silencio

■ **Takeaway:**
■ *Explica tu generación de podas y combinaciones antes de bucear en código. *
■ Los entrevistadores aman a los candidatos que muestran el *por qué* antes del *qué*.

-...

### 8. Alternativas & Por qué hemos elegido este

Silencio Alternativa Silencio Descripción Silencioso
Silencio------------------------------------...
tención **Topological DP + BFS** Silencio Tratar cada semestre como nivel, utilizar BFS para explorar estados de nivel por nivel. tención Simpler para entender. Silencio Todavía necesita enumeración de subconjunto → mismo O(2n C(n,k)). Silencio
Silencio **Heuristic / Greedy** (por ejemplo, tomar siempre el set más grande disponible) Silencio Rápido pero *no óptimo*. Silencio rápido, pero incorrecto. tención Leetcode requiere una solución óptima. Silencio
Silencio **Bitset + DP** (iterative) tención Use bitset to iterate over all states in increasing mask order. tención Evite la sobrecarga de recursión. ← Más duro para gestionar actualizaciones indegradas por estado. Silencio
Silencio **Mixed DP + BFS** Silencio DP on mask but BFS to handle indegree updates lazily. Silencio Potentially menos memoria. Silencio Código más complejo. Silencio

■ *Por qué la solución DP-bitmask es la respuesta de entrevista “estándar”: *
■ Se mapea limpiamente en la pregunta de entrevista “estados, transiciones, memoización” que muchos entrevistadores piden.
■ Muestra que puedes razonar sobre los subconjuntos, la explosión combinatoria y mantener el código dentro de los límites de tiempo.

-...

### 9. Lista de verificación para entrevistas

1. **Leer las limitaciones cuidadosamente** → *n* es pequeño, por lo que los estados exponenciales están bien.
2. **Explicar el estado** (mask) y por qué caben 15 cursos.
3. **Mostrar la transición**: identificar los cursos disponibles, enumerar los subconjuntos ≤ k.
4. **Discuss pruning**: tomar todo cuando "m " = k " , utilizar la combinación de pre-generación.
5. **Declarar la complejidad** en palabras (O(2n C(n,k)))) y en números (con excepción de 1 M ops).
6. **Escribe el código** (preferiblemente iterante para C++/Java, recursivo con memo en Python).
7. **Preguntas**: "¿Y si k fuera 1?" “¿Podemos paralelizar?” → demuestra curiosidad.
8. ** Casos de alto nivel**: `relaciones vacías ' , todos los cursos independientes, etc.
8. ** Pruebas de medición**: prueba en los ejemplos proporcionados, tal vez un arnés de prueba al azar.

-...

### 10. Pensamientos de cierre

- El enfoque **DP-bitmask** es *limpio, óptimo y encaja perfectamente dentro de los límites dados*.
- **Detalles de la implementación** (enumeración de la combinación, `m י= k` atajo) son esenciales para pasar el límite de 1 segundo.
- **La comunicación de la idea** es más importante que la entrega de un código perfecto; los entrevistadores buscan *procesos de pensamiento*.

-...

## 10‐Second Explication (para una rápida recaptura)

■ *“Utilizamos una mascara de bits para representar qué cursos están terminados. Para cada máscara, encontramos todos los cursos que se pueden tomar (sin requisitos no cumplidos). Si el número de estos cursos es ≤ k, los tomamos todos (sin ramificación). De lo contrario, probamos cada subconjunto de esos cursos de tamaño hasta k, actualizamos la máscara y requisitos, y recurre. Memoise los semestres mínimos para cada máscara. Complejidad: O(2n C(n,k)), con n = 15 → alrededor de un millón de operaciones.”*

-...

#### 10. Palabras finales

- **Mantenga el código legible** – los entrevistadores prefieren soluciones limpias sobre trucos “demasiado inteligentes”.
- Explique su razonamiento - construye confianza.
- **Práctica**: corre a través de un par de casos de prueba aleatorios en tu máquina para verificar el tiempo de ejecución.
**Deploy**: una vez confiado, presione el código a Leetcode y envíelo.

Buena suerte, y feliz codificación! 🚀

-...

### 11. SEO & Palabras clave (para tu blog)

- “Minimum number of semesters coding interview solution”
- “Problema de programación de cursos de bitmask”
- “Leetcode 1850 número mínimo de solución de semestres”
- “Topological kind with DP subsets”
- “Python lru_cache DP mask”
- “C++ __construction_popcount subset enumeration”
- " Interview explanation DP states transitions memoisation "

■ *Estas palabras clave ayudan a tu rango de artículo tanto para usuarios de Leetcode como para entrevistar a candidatos. *

-...

*Feliz coding, y la mejor suerte en su próxima entrevista!*