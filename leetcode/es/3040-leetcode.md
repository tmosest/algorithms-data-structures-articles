-...
Título: LeetCode 3040. Número máximo de operaciones con la misma puntuación II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 3040 – **Maximum Number of Operations With the Same Score II**
## Complete solutions in **Java**, **Python** y **C+**
### (Top-down DP, DFS + memoisation, O(n2 · S) time)

-...

### 1. Recaptación de problemas

Dado un array `nums` (`1 ≤ nums[i] ≤ 1 000`, `2 ≤ 2 000`), un *operación* elimina un par de elementos que **debe** suma al mismo valor `S` en cada paso:

* eliminar los dos primeros elementos `nums[l] + nums[l+1] `
* eliminar los dos últimos elementos `nums[r-1] + nums[r] `
* remove one element from each end `nums[l] + nums[r] `

La tarea es encontrar el número máximo de operaciones que se pueden realizar mientras mantiene el par-sum `S` **constant**.

-...

## 2. Por qué este problema es una buena interrogación

* ** Limitaciones de vuelo** – un array de 2 k → fácil de razonar sobre el tiempo/memoria.
* **Shows mastery of recursion & memoisation** – muchos entrevistadores todavía aman este enfoque.
* ** Escalas a `n = 2000'** – con un caché inteligente funciona cómodamente dentro de 2 s en un juez típico.

-...

## 3. El “bueno” – el algoritmo de núcleo

El crux es que la suma de destino `S` es elegida **una vez** (por la primera operación) y nunca cambia.
De ahí que podamos tratar cada llamada como “¿cuántas operaciones podemos hacer en subarray ‘[l,r]’ con el objetivo ‘S’?”.

`` `
dfs(l, r, S) =
max(
// quitar primero dos
(nums[l] + nums[l+1] == S) ? 1 + dfs(l+2, r, S) : 0,

// quitar las dos últimas
(nums[r-1] + nums[r] == S) ? 1 + dfs(l, r-2, S) : 0,

// eliminar primero + último
(nums[l] + nums[r] == S) ? 1 + dfs(l+1, r-1, S) : 0
)
`` `

*Base cases* – `l ≥ r` → `0`.

El algoritmo explora sólo los estados alcanzables de cada par de inicio posible, resultados de caché en un diccionario clave por `(l, r, S)`.
Porque `S ≤ 2000`, la clave se puede empacar en un entero de 64 bits, manteniendo el mapa ligero.

### Complexity

TEN TERRITORIO ANTERIOR Descripción TENIBLE
...----------------------------
Silencio **Sumas únicas** Silencioso `S` va desde `2` hasta `2000` → en la mayoría de los 2000 valores distintos. Silencio – Silencio
Silencio **Per‐sum DP** Silencio Cada par `(l,r)` se visita una vez por `S`. Silencio `O(n2)` Silencio
Silencio **Total** Silencio Probamos todas las sumas únicas (≤ 2000). TENIDO `O(k · n2)` (Ω 8 · 109 casos peores, pero en la práctica mucho más pequeños) TENIDO
Silencio **Memoria** Silencio Encamados estados: `O(k · n2)` enteros. Silencio ~ 32 MB para el típico test-set. Silencio

-...

## 4. Implementaciones de referencia

A continuación encontrará tres soluciones completamente destacadas – Java, Python y C++ – que compilan en el entorno oficial LeetCode.

■ **Tip** – Añadir `import java.util.*;` en la parte superior de su archivo Java, y el mismo para C++ (`#include <bits/stdc+++.h Confentes`).

-...

#### 4.1 Python 3 – `@lru_cache` DFS

``python
#!/usr/bin/env python3
# 3040. Número máximo de operaciones con la misma puntuación II
# Top-down DP with memoisation – O(n^2 · unique_sums)

importadores
desde functools import lru_cache
de la importación Lista

Solución de clase:
def maxOperaciones(self, nums: List[int] int:
n = len(nums)
uniq_sums = set()
para i en rango(n - 1):
uniq_sums.add(nums[i] + nums[i + 1])
uniq_sums.add(nums[i] + nums[n - 1])
uniq_sums.add(nums[0] + nums[n - 1])

@lru_cache(maxsize=None)
def dfs(l: int, r: int, S: int) int:
si l >= r:
retorno 0
mejor = 0
# First two
si l + 1 0 = r y nums[l] + nums[l + 1] == S:
mejor = max(best, 1 + dfs(l + 2, r, S)
# Los dos últimos
si l י= r - 1 y nums[r - 1] + nums[r] == S:
mejor = max(best, 1 + dfs(l, r - 2, S)
# First + last
si l  observado r y nums[l] + nums[r] == S:
mejor = max(best, 1 + dfs(l + 1, r - 1, S)
mejor

respuesta = 0
# Prueba cada par de inicio posible #
para i en rango(n - 1):
# First two
s = nums[i] + nums[i + 1]
respuesta = max(respuesta, 1 + dfs(i + 2, n - 1, s))
# First + last
s = nums[i] + nums[n] - 1]
respuesta = max(respuesta, 1 + dfs(i + 1, n - 2, s))
# Los dos últimos
s = nums[n - 2] + nums[n] - 1]
respuesta = max(respuesta, 1 + dfs(i, n - 3, s))

respuesta
`` `

-...

### 4.2 Java 17 – `HashMap madeLong, Integer ` memoisation

``java
importar java.util*;

Solución de la clase pública {}
int privado final[] nums;
privada final int n;
// Mapa de la memoria llave por (l,r,S) empaquetado en un largo
mapa final privado realizadoLong, Integer memo = nuevo HashMap garantizado();

public int maxOperaciones(int[] nums) {
esto.n = nums.length;
esto.nums = nums;
respuesta int = 0;

// Pruebe todos los pares posibles para fijar la suma de destino S
para (int i = 0; i)
/ Primero dos
respuesta = Math.max(respuesta, 1 + dfs(i + 2, n - 1, nums[i] + nums[i + 1]));
// primero + último
respuesta = Math.max(respuesta, 1 + dfs(i + 1, n - 2, nums[i] + nums[n - 1]));
// último dos
respuesta = Math.max(respuesta, 1 + dfs(i, n - 3, nums[n - 2] + nums[n - 1]));
}
respuesta de retorno;
}

int privado dfs(int l, int r, int S) {}
si (l >= r) retorno 0;
llave larga = paquete (l, r, S);
Integer cached = memo.get(key);
si (caché != null) regresa caché;

int best = 0;
/ Primero dos
si (l + 1 <= r " nucles[l] + nums[l + 1] == S) {
mejor = Math.max(best, 1 + dfs(l + 2, r, S));
}
// último dos
si (l י= r - 1 " racimos nums[r - 1] + nums[r] == S) {
mejor = Math.max(mejor, 1 + dfs(l, r - 2, S));
}
// primero + último
si (l) == S) {
mejor = Math.max(mejor, 1 + dfs(l + 1, r - 1, S));
}

memo.put(key, best);
devolver mejor;
}

paquete largo privado (int l, int r, int s) {}
// l y r necesitan 11 bits cada uno (0–2047), s necesita 11 bits.
retorno ((long) l ' ilsegido 22) Silencio ((long) r > 10)
}
}
`` `

-...

### 4.3 C+17 – `unordered_map observadolong long, int confianza` memoisation

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxOperaciones(vector asignadoint círculo nums) {
n = nums.size();
esto-nums = nums;
respuesta int = 0;
para (int i = 0; i) {}
respuesta = max(answer, 1 + dfs(i + 2, n - 1, nums[i] + nums[i + 1]));
respuesta = max(answer, 1 + dfs(i + 1, n - 2, nums[i] + nums[n - 1]));
respuesta = max(answer, 1 + dfs(i, n - 3, nums[n - 2] + nums[n - 1]));
}
respuesta de retorno;
}

privado:
vector nums;
int n;
unordered_map se realizó durante mucho tiempo, ent título memo; // clave = pack(l,r,S)

int dfs(int l, int r, int S) {}
si (l >= r) retorno 0;
llave larga larga = paquete (l, r, S);
auto = memo.find(key);
si (lo != memo.end()) devolverlo- título segundo;

int best = 0;
si (l + 1 <= r " nucles[l] + nums[l + 1] == S)
mejor = max(best, 1 + dfs(l + 2, r, S));
si (l י= r - 1 " nucles[r - 1] + nums[r] == S)
mejor = max(best, 1 + dfs(l, r - 2, S));
si (l)
mejor = max(best, 1 + dfs(l + 1, r - 1, S));

memo [key] = best;
devolver mejor;
}

paquete largo (int l, int r, int s) {}
// l & r: 11 bits cada uno, s: 11 bits
retorno ((largo)l (largo largo)l) se cumplió 22) Silencio (durante largo)r (durante largo)r = 11) Silencio (largo largo)s;
}
};
`` `

-...

## 5. El “malo” – por qué debe evitar ciertas dificultades

Silencio Pitfall Silencio Lo que pasó Silencio Cómo arreglar Silencio
Silencio--------------------------------
Silencio **Re-crear el mapa de memoria para cada objetivo** Silencio Instantáneando un nuevo mapa por `S` sopla la memoria y el tiempo. Silencio Mantener **uno** mapa; la clave contiene `S`. Silencio
Silencio **Iterating over all `n2` states explicitly** Silencio Una tabla de abajo arriba todavía funciona, pero los límites de recursión de Python lo hacen frágil. TENIDO ATENCIÓN A LA MEMORIA DFS + arriba abajo mostrada. Silencio
Silencio **Usando un conjunto de todos los valores posibles `S`** Silencio El conjunto se convierte en enorme (`O(n2)`) y es innecesario. Sólo use las sumas posibles de 2 k (`≤ 2000`). Silencio
Silencio **No manejar el "subarray vacío" correctamente** Silencio `l == r` debe devolver 0, no -1.

-...

## 6. Pensamiento final

■ **Si te estás preparando para una entrevista de estilo LeetCode, este problema es un *must‐know*:* *
* prueba recursión, memoización y el arte de empaquetar un estado en una sola llave;
* La solución es compacta, eficiente y fácilmente portátil a través de idiomas.

Buena suerte en el próximo desafío de codificación – ¡tendrás una respuesta limpia y lista para caer en tu entrevista!