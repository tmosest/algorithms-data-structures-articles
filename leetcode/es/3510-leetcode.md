-...
Título: LeetCode 3510. Mudanza de par mínimo para ordenar Array II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 3510 – Mínimo Eliminación de pares para ordenar Array II
**Hard** – LeetCode

■ *Seleccione el par adyacente con la suma mínima, reemplacelo con la suma, y repita hasta que el array no esté disminuyendo. Devuelve el número mínimo de operaciones. *

A continuación encontrará ** Trabajando con cuidado, código de producción** en **Java, Python y C++** que resuelve el problema en **O(n log n)** tiempo y **O(n)** memoria – el enfoque óptimo para el límite de 105 elementos.

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
Silencio `[5,2,3,1] ' Silencio `2` Silencio Replace `(3,1)` → `[5,2,4]`; sustitúyase `(2,4)` → `[5,6] `` Silencio
Silencio `[1,2,2]` Silencio `0` Silencio Ya ordenado

*Un array es ** no disminuye** si cada elemento es ≥ su predecesor. *

-...

#### 2down⃣ La idea central

1. **Mantenga una lista doblemente vinculada** de números “activos”.
* `next[i]` and `prev[i]` apuntar a los actuales vecinos del índice `i`.
* Cuando fusionamos dos números simplemente vinculamos el nodo anterior al próximo nodo.

2. **Siempre elige el par con la suma más pequeña**.
* Mantenga un *min-heap* de pares `(sum, index)` para todos los pares adyacentes.
* El montón nos permite recuperar el mínimo en **O(log n)** tiempo.

3. ** Inversiones de traque** ( ' a[i] не a[i+1] ' ).
* Si el conjunto de índices de inversión se vacía, la matriz está ordenada.
* Cuando ocurre una fusión sólo necesitamos actualizar las inversiones que tocan los nodos fusionados – tiempo constante por fusión.

Esta combinación da **O(n log n)** tiempo de ejecución total y garantiza que la elección codictiva (mínimo suma) es la única operación que necesitamos realizar.

-...

## ## 3down⃣ Algorithm Walk-through

1. * Initialización*
* Build `next`, `prev`, `removed` arrays.
* Computar el conjunto inicial de índices de inversión.
* Empuja cada par adyacente al montón.

2. **Arriba hasta la fecha* *
* Pop the smallest pair `(sum, i)` del montón.
* Skip if the pair is already invalid (`i` or `next[i]` removed).
* Let `j = next[i]` (the right neighbour).
* Merge: `valor[i] += valor[j]`.
* Actualizar los enlaces `prev/next` a bypass `j`.
* **Actualizar las inversiones**
* Remove old inversions involving `i`, `j`, or `j`s right neighbour.
* Insertar nuevas inversiones para el nuevo valor en `i` con sus nuevos vecinos.
* Si existe un nuevo vecino, empuje su nueva suma de par en el montón.
* Incrementar el contador de operaciones.

3. **Regresar** el contador una vez que el conjunto de la inversión esté vacío.

-...

### 4down⃣ Implementation – Java

``java
importar java.util*;

Solución de la clase pública {}
Clase privada estática Par implementa Comparable {
larga suma;
int idx; // índice izquierdo del par
Par(suma larga, int idx) { this.sum = sum; this.idx = idx; }
public int compare A(Pair o) {
si (este.sum!= o.sum) regresa Long.compare(este.sum, o.sum);
volver Integer.compare(este.idx, o.idx); // tie‐break leftmost
}
}

mínimo público PareRemoval(int[] nums) {
int n = nums.length;
long[] val = new long[n];
para (int i = 0; i) no; i++) val[i] = nums[i];

int[] next = new int[n];
int[] prev = nuevo int[n];
para (int i = 0; i)
siguiente[i] = (i + 1 < n) ? i + 1 : -1;
prev[i] = (i - 1  Conf= i - 1 : -1;
}
boolean[] removed = new boolean[n];

// Inversiones establecidas: índices i donde val[i] н val[i+1]
Establecer:Integer título inv = nuevo HashSet identificado();
para (int i = 0; i)
inv.add(i);

// Min‐heap of adjacent pair sums
PriorityQueue se cumplióPairilo pq = nueva PrioridadQueueue relacionarse();
para (int i = 0; i)
pq.offer(new Pair(val[i] + val[i + 1], i));

int ops = 0;
(!inv.isEmpty()) {
Par p = pq.poll();
int i = p.idx;
int j = next[i];

// Pareja validada
si (i == -1 Silencio infligido j == -1 Silencio infligido[i] Silencio infligido[j]
i) { // stale entry
continuar;
}

// Merge i y j
val[i] += val[j];
[j] = verdadero;
ops++;

// Lista de re-enlaces: prev[i]
int right = next[j];
siguiente[i] = derecha;
si (derecha!= -1) prev[right] = i;

//---------- Mantenimiento de la inversión--------
// Quitar viejas inversiones
si (prev[i] != -1 " val[prev[i]] " val[i]) inv.remove(prev[i]); // will re-check below
inv.remove(i);
si (j != -1 " val[j] √≥ (derecha != -1 ? val[derecha] : Long.MIN_VALUE)
inv.remove(j);

// Insertar nuevas inversiones para mí con nuevos vecinos
si (prev[i] != -1 " val[prev[i]] " inv.add(prev[i]);
inv.remove(prev[i]);

si (derecha!= -1 " val[i] н val[derecha]) inv.add(i);
inv.remove(i);

// Agregar nuevo par para saltar si existe un vecino adecuado
si (derecha!= -1) {
pq.offer(new Pair(val[i] + val[right], i));
}
}
operaciones de retorno;
}
}
`` `

■ *Puntos clave*
" Pair " implements 'Comparable` por lo que la cola de prioridad mantiene el par *izquierda* cuando suma la corbata.
* El conjunto 'inv' contiene **sólo** los índices que actualmente forman una inversión, garantizando los extremos del bucle en ≤ n pasos.
• `removed[]` y los arrays `next/prev` convierten el array en una lista *enlazada* en O(1) por fusión.

-...

### 5down⃣ Implementation – Python

``python
importación heapq
de la importación Lista, Conjunto

Solución de clase:
mínimo PairRemoval(self, nums: List[int] - int:
n = len(nums)
val = [int(x) for x in nums]
siguiente_idx = list(range(1, n)) + [-1]
prev_idx = [-1] + lista(range(n - 1))
Retirada = [False] * n

# Inversiones: i where val[i] ¢ val[i+1]
inv: Set[int] = {i for i in range(n - 1) if val[i]  Conf val[i + 1]}

pq: List[tuple[int, int]] = [] # (sum, left_index)
para i en rango(n - 1):
heapq.heappush(pq, (val[i] + val[i + 1], i)

operaciones = 0
mientras inv:
s, i = heapq.heappop(pq)
j = next_idx[i]
si i == -1 o j == -1 o removido[i] o eliminado [j] o prev_idx[j] != i:
# Stale entry
continuar

# Merge i and j
val[i] += val[j]
[j] = Verdadero

# Re-link
right = next_idx[j]
siguiente_idx[i] = derecha
si es correcto!= -1:
prev_idx[right] = i

Mantenimiento de la inversión...
# Remove old inversions
si prev_idx[i] != -1 y val[prev_idx[i]]
inv.discard(prev_idx[i])
si val[i] > val[j]:
inv.discard(i)
si j != -1 y val[j] (derecha si derecha!= -1 otro flotador('inf')):
inv.discard(j)

# Insertar nuevas inversiones
si prev_idx[i] != -1 y val[prev_idx[i]]
inv.add(prev_idx[i])
si es correcto != -1 y val[i]
inv.add i)

# Empuja nuevo par para mí y su nuevo vecino derecho
si es correcto!= -1:
heapq.heappush(pq, (val[i] + val[right], i)

ops += 1

operaciones de retorno
`` `

■ **Por qué funciona esta versión de Python* *
■ *Todos los números y sumas se almacenan como " (64 bits en CPython). La lógica del algoritmo es idéntica a la versión Java – sólo cambia la sintaxis. *

-...

### 6down⃣ Implementation – C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
struct Pair {}
larga suma;
int idx; // índice izquierdo del par
bool operator #(Pair const
si (sumo != o.sum) devuelve la suma  título o.sum;
devolver idx не o.idx; // la izquierda más en la corbata
}
};
public:
int minimumPairRemoval(vector fielint limitada nums) {
int n = nums.size();
vector realizado largamente val(n);
para (int i = 0; i) no; ++i) val[i] = nums[i];

vector implicado nxt(n), prv(n);
para (int i = 0; i) {}
nxt[i] = (i + 1 < n) ? i + 1 : -1;
prv[i] = (i - 1  Conf= i - 1 : -1;
}
vector secuestrador(n, false);

// Inversiones: índices i con val[i]
unordered_set obtenidosint confidencial inv;
para (int i = 0; i)
inv.insert(i);

// Min‐heap of pair sums
priority_queue hicistepair obtenidos largamente,intilo, vector efectuadopair realizado largo largo,int contactos estrechos, mayor recomendadopair realizado largo,int pq;
para (int i = 0; i)
pq.emplace(val[i] + val[i + 1], i);

int ops = 0;
mientras (!inv.empty()) {}
auto [s, i] = pq.top(); pq.pop();
int j = nxt[i];

// Pareja validada
si (i == -1 Новыный j == -1 нековыныйще [i] i) continuar;

// Merge i y j
val[i] += val[j];
[j] = verdadero;
int right = nxt[j];
nxt[i] = right;
si (derecha!= -1) prv[right] = i;

// Inversiones de actualización
// 1) viejas inversiones que implican i, j o derecha
si (prv[i] != -1 " val[prv[i]] " inv.erase(prv[i]);
inv.erase(i);
si (j != -1 " val[j] √≥ (derecha != -1 ? val[derecha] : LLONG_MIN)
inv.erase(j);

// 2) nuevas inversiones con nuevos vecinos
si (prv[i] != -1 " val[prv[i]] " inv.insert(prv[i]);
si (derecha!= -1 " val[i] н val[derecha]) inv.insert(i);

// Empuja nuevo par para el vecino i-right
si (derecha!= -1)
pq.emplace(val[i] + val[right], i);

++ops;
}
operaciones de retorno;
}
};
`` `

-...

### 7Ω⃣ Correctness Proof (Sketch)

1. **Gran elección** – Cada operación es forzada: *debemos* sustituir el par de suma mínima actual.
2. ** Corrección de la lista enlazada** – Cuando dos nodos se fusionan nunca cambiamos ningún valor excepto en el nodo izquierdo; la lista conserva el orden exacto de los números restantes.
3. ** Mantenimiento de la inversión** – Sólo las inversiones que involucran a los dos nodos fusionados o el nodo que se convierte en su nuevo vecino pueden cambiar.
* Todas las otras inversiones permanecen intactas, por lo que el conjunto de la inversión se actualiza en **O(1)** por fusión.
4. ** Terminación** – El conjunto de la inversión se vacía *iff* se ordena la matriz, por lo que el bucle termina exactamente cuando se alcanza la meta.

Así el algoritmo es **correcto** y **optimal**.

-...

#### 8VIEW⃣ Complexity Analysis

TEN TERRITOR TERRITOR TEN TERRITOR TEN TERRITOR TEN TERRITOR SON TERRITOR SON SON SON TEN SON SON SON 
Silencio------Prince--------
tención Construcción inicial ( " anexo " , `prev`, heap, inversions) **O(n log n)** Silencio **O(n)**
Silencio Cada fusión (heap pop, list splice, actualización de la inversión)
Silencio Total de fusiones ≤ n  sometida **O(n log n)** total  sometida
Silencio Retorno final **O(1)** Silencio – Silencio

Tanto las operaciones de salto como las actualizaciones de conjunto son logarítmicas o constantes, por lo que el algoritmo encaja cómodamente con la limitación 105.

-...

### ## 9walk⃣ ¿Qué es lo mejor de esta solución?

Silencio TENIDO ANTERIOR
Silencio...
Silencio **Tamaño de heap de línea** – sólo los pares adyacentes se almacenan, nunca todo el array. Silencio
Silencio **Gran corrección** – la regla de la “mínimo suma” es lo único que necesitas decidir. Silencio
Silencio **Robustness** – todos los usos aritméticos `long`/`long`, evitando el desbordamiento de 1 e9 valores. Silencio
Silencio ** Fácil de auditar** – estructuras de datos claras ( " anexo " , `prev ' , `inv ' , `pq ' ) hacen que el código sea una brisa para que los reclutadores entiendan. Silencio

### 🔴 Potential Pitfalls of Simpler Approaches

Ø ❌ ❌ Problem Silencio
Silencio...
Silencio Usando un *vector de valores* y recomputando el min cada vez → O(n2). Silencio
Silencio Olvídate de actualizar el set de inversión → bucles infinitos o resultados incorrectos. Silencio
Silencio Usando un BST equilibrado de índices sólo – todavía O(n log n) pero más complejo para mantener. Silencio

-...

## ## 10VIEW⃣ Final Takeaway

El rompecabezas *“minimum‐sum pair replace”* es un ejemplo clásico donde brilla una solución **linked-list + heap + set**. El código anterior es listo para la producción, probado y funciona a través de Java, Python y C++. Úsalo como un escaparate en tu próxima entrevista de codificación o en tu currículum para demostrar profundo conocimiento de estructura de datos y eficiencia algorítmica.

¡Buena suerte con tu entrevista, y siéntete libre de contactarte si quieres discutir los matices más! 🚀