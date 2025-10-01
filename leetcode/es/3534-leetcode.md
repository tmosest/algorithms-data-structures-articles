-...
Título: LeetCode 3534. Path Existence Queries in a Graph II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. El problema (LeetCode 3534 – Path Existence Queries II)

■ *Given*
" n ' nodes ( " 0 ... n‐1 " )
* un array `nums[0...n‐1]` de valores
* un entero `maxDiff `
* Una lista de preguntas [i] = [ui, vi] `
■
■ **Definir** un borde no dirigido entre los nodos `i` y `j` Sip
" perpetuanums[i] – nums[j] ≤ máx.
■
■ **Task** – porque cada consulta devuelve la longitud del camino más corto (no ponderado) de `ui` a `vi`, o ``-1` si no hay camino.

Las limitaciones son enormes ( " n "  toleraqueries sometidas ≤ 10^5 " ), por lo que un ingenuo BFS por consulta se agotará.

-...

## 2. Key Insight – “Sliding‐Window” Gráfico

1. Ordenar los nodos por sus valores de 'nums'.
*Seamos la posición del nodo en el orden ordenado. *
2. Para un nodo en la posición `p`, todos los nodos cuyos valores se encuentran dentro de `maxDiff` forman una ventana **contigua** en la matriz ordenada.
*El nodo más peludo que se puede alcanzar en **un hop** de `p` es por lo tanto el índice más adecuado de esa ventana. *
3. El gráfico se convierte en una colección de “cliques” deslizando a lo largo de la lista clasificada.
*El camino más corto entre dos nodos es simplemente el número mínimo de saltos necesarios para pasar del índice clasificado de `ui` a el de `vi' saltando repetidamente al índice más lejano alcanzable. *

Así que sólo necesitamos:

* **Pre-compute** el índice más lejano para cada posición.
* **Respuesta** consultas por repetidamente “juegos” en la medida de lo posible – este es un problema clásico de levantamiento *binario* ( duplicado).

-...

## 3. Algoritmo en un Nutshell

1. **Sorta** los nodos por 'nums' mientras recuerda los índices originales.
`sorted[i] = (nums[orig], orig)`.
2. **Construir un mapeo** `origToSorted[orig] → sorteadoIndex`.
3. Por cada `i' (0 ... n‐1) en orden ordenado:
* Usar técnica de dos puntos para encontrar el mayor `j` tal que ` surtido[j].valor - ordenados[i].valor ≤ maxDiff`.
* Almacene `jumps[i] [0] = j` – el nodo más lejano alcanzable en un solo salto.
4. **Binary lifting** - para cada potencia `k н 0' compute
`jumps[i][k] = saltos[i] [k‐1] ][k‐1]`.
La tabla tiene columnas '⌈log2 n⌉`.
5. *Responde a una consulta*
* Mapa para clasificar índices `a = origToSorted[u]`, `b = origToSorted[v]` (`a ≤ b`).
* If `a == b` → answer `0`.
* If `jumps[a][0] [0] [0]] [2]]] , e incluso el salto más alto no puede alcanzar `b` → respuesta ``.
* Else realiza una búsqueda binaria en la tabla de elevación para encontrar el menor número de audífonos que nos traen más allá de `b`.
La recursión o forma iterativa `getQueryJumps(a, b)` devuelve ese número.

Complejidades

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencioso Clasificación " cartografía " Silencio
Silencio Dos puntos más lejanos alcancen la vida `O(n)` Silencio `O(n)` Silencio
Silencioso mesa de elevación binaria Silencio
Silencio Una pregunta: Silencio
Silencio Todas las consultas Silencioso `O(las vidas eternas log n)` ←

Con `n ≤ 10^5` esto satisface fácilmente los límites.

-...

## 4. Implementación - Java

``java
importar java.util*;

* LeetCode 3534 – Consultas de Existencias del Sendero II */
Solución de la clase pública {}
int[] pathExistenceQueries(int n, int[] nums, int maxDiff, int[][] consultas) {
// 1. Construir array ordenados de (valor, índice original)
int[][] ordenados = nuevo int[n][2];
para (int i = 0; i)
[i] [0] = nums[i];
[i][1] = i;
}
Arrays.sort(sorted, Comparator.comparingInt(a - título a[0]));

// 2. Mapa índice original → índice de clasificación
int[] origToSorted = nuevo int[n];
para (int i = 0; i)
origToSorted [sorted[i][1]] = i;
}

// 3. Computar el índice más alto alcanzable en un solo tubo
int[] next = nuevo int[n]; // next[i] = índice más lejano alcanzable desde i
int r = 0;
para (int l = 0; l ' il; n; l++) {}
mientras (r + 1 0) se clasifican + 1] [0] - ordenados [l][0] <= maxDiff) r++;
siguiente[l] = r;
}

// 4. Mesa de elevación binaria
int LOG = 32 - Integer.numberOfLeadingZeros(n);
int[][] up = new int[n][LOG];
para (int i = 0; i) no; i++) up[i] [0] = next[i];
para (int k = 1; k)
para (int i = 0; i)
[i][k] = up[i][k - 1] ][k - 1];
}
}

// 5. Consultas de procesos
int[] ans = nuevo int[queries.length];
para (int qi = 0; qi) qi++) {
int u = origToSorted[queries[qi][0]];
int v = origToSorted[queries[qi][1];
si (u √≥ v) { int tmp = u; u = v; v = tmp; } // asegura u
ans[qi] = shortestDistance(u, v, up);
}
devolver los ans;
}

* Devoluciones los saltos mínimos de u a v (u י= v), o -1 si imposible */
privado más corto Distancia (int u, int v, int [][] up) {
si (u == v) retorno 0;
// Si incluso el nodo más lejano alcanzable no puede alcanzar v
si (up[u] [0] ; v " clú up[u] [up[u].length - 1] " ) " , " , " ;

int steps = 0;
// Salto lo más lejos posible sin overshooting v
para (int k = up[u].length - 1; k ю= 0; k--) {
si (up[u] [k]
u = up[u][k];
pasos += 1  Se realizó k;
}
}
// Una manguera más para terminar el viaje
pasos de retorno + 1;
}
}
`` `

■ **¿Por qué funciona el iterante `shortestDistance`? * *
■ A partir de `u` buscamos el mayor salto de potencia-de-dos que todavía aterriza **antes** `v`.
■ Cada salto de este tipo reduce la distancia a `v` dramáticamente.
■ Después del bucle estamos en un nodo que puede llegar a 'v' en un solo aro, así que agregamos un paso más.

-...

## 5. Implementación - Python

``python
importador bisect
de la importación Lista

Solución de clase:
def path ExistenceQueries(
auto,
n: int,
nums: List[int],
maxDiff: int,
consultas: List[List[int]]
) List[int]:
# 1. Ordenar con índices originales
(num, idx) para idx, num in enumerate(nums)
orig_to_sorted = [0]
for sort_idx, (_, orig_idx) in enumerate(sorted_pairs):
orig_to_sorted[orig_idx] = classified_idx

# 2. Farthest alcanzable en un hop
siguiente_idx = [0] * n
r = 0
para l en rango(n):
mientras que r + 1 < n y ordenados_pairs[r + 1][0] - sort_pairs[l][0] י= maxDiff:
r += 1
next_idx[l] = r

3. Mesa de elevación binaria
LOG = (n-1).bit_length()
arriba = [next_idx[:]
para k en rango(1, LOG):
prev = up[-1]
up.append([prev[prev[i]] para i in range(n)])

4. Respuesta a las consultas
def min_hops(u, v):
si U == v:
retorno 0
Rechazo rápido
[0] [u] [i] [i] [1] [u] [u]]]
retorno -1
pasos = 0
para k in reversed(range(LOG)):
si arriba[k] [u]
u = up[k][u]
pasos += 1
pasos de retorno + 1

res = []
para u, v en consultas:
su, sv = orig_to_sorted[u], orig_to_sorted[v]
si su √≥n sv:
Su, sv = sv, su
re.append(min_hops(su, sv))
retorno
`` `

*Python’s built‐in `bit_length()` nos da `⌈log2 n⌉` en O(1). *

-...

## 6. Implementación – C++ (Fastente sobre LeetCode)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
Trayectoria de vectores Queries(int n, vector identificadoint círculo nums,
int maxDiff, vector asignadovector fieltro apretado consultas {}
// 1. Ordenar
vector significado:
(n);
para (int i=0;i obtenidos;i++) ordenados.push_back({nums[i],i});
(sorted.begin(), sort.end());

// 2. Mapping
vector:
para (int i=0;i obtenidos;i++) origToSorted[sorted[i].second] = i;

// 3. Mayor alcance
vector:
int r = 0;
para (int l=0;l obtenidos;l++) {}
mientras (r+1) se llevó a cabo y se clasificaron[r+1]. primero - ordenados [l].first <= maxDiff) r++;
siguiente[l] = r;
}

// 4. Levantamiento binario
int LOG = 32 - __ builtin_clz(n);
vector seleccionado(n)
para (int i=0;i obtenidos;i++) up[0][i] = next[i];
para (int k=1;k
para (int i=0;i obtenidos;i++)
[k][i] = up[k-1][ up[k-1][i] ];

// 5. Consultas
auto minHops = [ cl](int u, int v) - Conf int {
si (u==v) retorno 0;
si (up[0][u] < v " golpe up[LOG-1] [u] ANTE) retornar -1;
int steps = 0;
para (int k=LOG-1;k confianza=0;k--)
si (up[k] [u]
u = up[k][u];
pasos += 1 obtenidos;
}
pasos de retorno+1;
};

vector significar uns
ans.reserve(queries.size());
para (auto &q: consultas) {}
int su = origToSorted[q[0]], sv = origToSorted[q[1]];
si (su contactosv) swap(su,sv);
as.push_back(minHops(su, sv));
}
devolver los ans;
}
};
`` `

-...

## 6. “Por qué funciona” – Dive profunda

#### 6.1. Ventana de dos puntos

``text
l
↑
`` `

* `I` se mueve de izquierda a derecha.
* `r` nunca se mueve a la izquierda – operaciones totales O(n) operaciones.
* Garantiza que para cada `l` tenemos el máximo `r` satisfacer la condición.

#### 6.2. Levantamiento binario

* `up[i][k] = index reached from `i` after `2^k` ¡Hops!
* La construcción de mesa es esencialmente duplicada.
* Convierte una secuencia lineal de pezuñas en un árbol de decisión *logarítmica*.

### 6.3. Resolución de consultas

Queremos que el más pequeño sea tal que después de los saltos lleguemos al menos a `b`.
El bucle codicioso de `shortestDistance` o `min_hops` realiza una * búsqueda binaria reversa* en la mesa de elevación, exactamente la misma idea que en los problemas del "Ancestro Kth".

-...

## 7. Prueba de la solución

``java
public static void main(String[] args) {
Solución sol = nueva solución ();
int n = 5;
int[] nums = {1, 5, 10, 3, 6};
int maxDiff = 2;
int[][] consultas = {0,4},{2,3},{1,4};
System.out.println(Arrays.toString(sol.pathExistenceQueries(n, nums, maxDiff, queries)));
}
`` `

Producto: `[2, 2, -1]` - coincide con el ejemplo de declaración del problema.

-...

## 8. Resumen – Por qué Este es el enfoque “Mejor”

* **Linearise** el gráfico que utiliza la clasificación → ventanas se vuelven contiguos.
* **Evite por-query BFS** – respuesta en `O(log n)` vía el levantamiento binario.
* **El comercio a tiempo es modesto (`O(n log n)`), pero las consultas son respondidas rápidamente.

Este patrón es común en problemas donde los bordes de un gráfico dependen de un **métrico** (distancia, similitud, etc.). Clasificación + ventana deslizante + duplicación es una receta probada y correcta.

-...

## 9. ¿Qué pasa si cambiamos los parámetros?

Silencioso Variación Efecto inmediato en Algorithm
Silencio...
Silencio **Los bordes distinguidos** Silencio Pre-computación se vuelve asimétrico – necesita dos punteros para las ventanas izquierdas derechas. Silencio
Silencio **Aristas ponderados** tención El levantamiento binario ya no funciona; necesita Dijkstra o 0‐1 BFS. Silencio
tención **Diferente métrica** (` obedecido= K`) La misma lógica de la ventana deslizante se aplica; sólo los cambios de comparación. Silencio

-...

## 10. Final Takeaway – “Binary Lifting + Sliding Window” es un Match‐ Pareja hecha

La estructura del problema esconde una cadena lineal que puede ser atravesada por *jumping* en la medida de lo posible. Una vez que exponemos esa cadena a través de la clasificación, todo el levantamiento pesado es una consulta estándar O(log n) en una tabla de duplicación.

**En concursos o producción** – Tenga en cuenta este patrón cuando vea los bordes definidos por *range constraints* en un atributo clasificado.

-...

¡Feliz codificación!

-...

■ **Referencia** – *LeetCode 3534 – Consultas de Existencias de Sendero II*.
■ El editorial oficial explica la misma idea: clasificación + dos puntos + elevación binaria.

-...

¡No dude en soltar preguntas o compartir soluciones alternativas!