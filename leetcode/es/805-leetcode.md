-...
Título: LeetCode 805. Array de división con el mismo promedio -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Resumen del problema – Dividir la raya con el mismo promedio
**LeetCode #805** – *Hard*

■ Dado un array `nums`, dividirlo en dos sub-arrays no vacíos **A** y **B** (se pueden formar re-ordenando los elementos originales).
■ If `average(A) == average(B)` return `true`, otherwise return `false`.
■
■ Constraints:
≤ 30
≤ 104

Debido a que la longitud de la matriz es pequeña (≤ 30) podemos permitirnos soluciones de tiempo exponencial que son lo suficientemente inteligentes para podar ramas imposibles.

-...

## 2. Intuición

Vamos.

`` `
total Sum = sum(nums)
n = nums.length
`` `

Si el promedio de un subconjunto elegido de tamaño `k` equivale al promedio de toda la matriz, entonces la suma del subconjunto debe ser

`` `
objetivo Sum = total Sum * k / n
`` `

Para que eso sea un entero necesitamos `(totalSum * k) % n == 0`.
Así que sólo necesitamos probar *posibles* subset tamaños `k` (1 ... n/2) que satisfagan la condición de divisibilidad y comprobar si existe un subconjunto de ese tamaño cuya suma equivale a `target Sum`.

Encontrar un subconjunto con un tamaño específico y suma es un problema clásico *subset‐sum*, pero con una dimensión adicional (el tamaño).
Dos enfoques que encajan perfectamente:

1. **Recursive DP + Memoization** – explore el árbol de búsqueda mientras cachea estados ya vistos.
2. **Meet-in-the‐Middle** – dividir el array en dos mitades, enumerar todas las sumas subset en cada mitad, luego combinarlas.

Ambos tienen la misma complejidad teórica peor de los casos `O(2^(n/2)', pero el DP recursivo es a menudo más fácil de leer e implementar en los ajustes de entrevista.

-...

## 3. Por qué el DP Recursivo es “bueno”

* **Readability** – Una única función recursiva (`dfs`) captura la idea de “pick o saltar un elemento”.
* Early Pruning* Si los elementos restantes no pueden llenar el tamaño requerido ( " k + i " ) o el objetivo se vuelve negativo, retrocedemos inmediatamente.
* **Memoización** – Nunca recomputamos el mismo triple `(i, k, target)`, por lo que el número de estados distintos está obligado por `n * (n/2) * target` (todavía pequeño porque `n ≤ 30`).
* **Deterministic** – No pasa ninguna aleatorización o paso múltiple sobre los datos – el algoritmo se comporta previsiblemente.

-...

## 4. ¿Por qué “Bad” o “Ugly” (y cómo evitarlo)

Silencio ¿Por qué?
Silencio...
Silencio **Using a string key** like `"target,k,i"` in Java Silencio ineficiente, memoria extra, riesgo de colisiones clave ANTE Utilizar un `long` que empaqueta los tres enteros (`(target Геленноватенннная 20) Silencio (k ванетелите 10) ны i ') o un objeto personalizado con el `hashCode adecuado. Silencio
Silencio **Profundidad de recursión sin límites** en idiomas que no optimizan las llamadas a la cola Silencio Rebosa de Stack para entradas más grandes (aunque `n ≤ 30` es seguro) ← Utilizar un DP iterativo o limitar la profundidad de recursión mediante la conversión a bucles. Silencio
* Comprobando todo ‘k’ ciegamente* incluso cuando ‘total Sum * k) % n!= 0` ← Trabajo extra desperdiciado Silencioso Skip those `k` values early. Silencio
Silencio **Re-alizar la memoria** en cada llamada de DFS ¦ Garbage‐collection overhead Silencio Usa un caché de LRU o `Mapa` que reutiliza objetos clave. Silencio
Silencio **No hay casos de borde de manipulación** como arrays de elementos únicos ← Respuesta incorrecta ← Regresar `falso` cuando `n == 1` porque no podemos dividir un solo elemento en dos conjuntos no vacíos. Silencio

-...

## 5. Solución – DP Recursivo (Memoización)

A continuación se presentan implementaciones limpias y de producción en **Java**, **Python**, y **C+**. Los tres resuelven el problema en *O(2^(n/2))* tiempo y *O(n * objetivo)* memoria, y están garantizados para correr rápido para el tamaño máximo de entrada (`n = 30`).

■ **Tip for interviews**: Cuando se le pide que resuelva este problema, primero mencione el cheque de divisibilidad, luego diga que usará recursión + memoización. Eso muestra que conoces la información básica antes de bucear en código.

### 5.1 Java

``java
importa java.util. HashMap;
importa java.util. Mapa;

Solución de la clase pública {}
pública booleana splitArraySameAverage(int[] nums) {
int n = nums.length;
si (n 0 = 1) devolver falso; // no puede dividirse en dos arrays no vacíos

total Sum = 0;
para (int x : nums) total Sum += x;

// probar cada posible tamaño del subconjunto k (1 ... n/2)
para (int k = 1; k)
(long) total Sum * k % n!= 0) continuar; // objetivo no sería entero
int target = (int) ((long) total Sum * k / n);
si (dfs(nums, 0, k, target, new HashMap correctamente()))
retorno verdadero;
}
devolver falso;
}

// clave de memoria: (i, k, target) - título Boolean
dfs booleanos privados (int[] nums, int i, int k, int target,
Mapa identificado Estado, Boolean título memo) {
(k == 0) objetivo de retorno == 0;
si (objetivo) 0 Silencioso k + i не nums.length) volver falso;
State key = new State(i, k, target);
si (memo.containsKey(key)) devuelve memo.get(key);

// recoger nums[i] o saltarlo
boolean res = dfs(nums, i + 1, k - 1, target - nums[i], memo)
i + 1, k, target, memo);
memo.put(key, res);
restitución;
}

// Llave inmutable para la memoización
Estado de clase final estática privada {
idx final, tamaño, objetivo;
Estado(int idx, int size, int target) {
este.idx = idx; este.size = tamaño; esto. objetivo = objetivo;
}
@Override public boolean equals(Object o) {
si (esto == o) regresan verdaderos;
si (!(o instancia de Estado)) devuelve falso;
Estado distinto = (Estado) o;
retorno idx == other.idx ' dimensiones == other.size " punto destinatario == other.target;
}
@Override public int hashCode() {}
int h = 17;
h = 31 * h + idx;
h = 31 * h + tamaño;
h = 31 * h + objetivo;
retorno h;
}
}
}
`` `

*Por qué esto es bueno*
* ``Estado es inmutable y utiliza un `hashCode() / igual()` par, por lo que el `HashMap` se comporta previsiblemente.
* La función recursiva es concisa y utiliza los tres parámetros exactos que necesitamos para la memoización.

### 5.2 Python

``python
desde functools import lru_cache
de la importación Lista

Solución de clase:
def splitArraySameAverage(self, nums: List[int]) - ratio bool:
n = len(nums)
si no
Retorno Falso

total_sum = sum(nums)

# comprobar todos los tamaños de subconjunto válidos
para k en rango(1, n // 2 + 1):
si (total_sum * k) % n != 0:
continuar
objetivo = (total_sum * k) // n

@lru_cache(maxsize=None)
def dfs(i: int, remaining_k: int, remaining_target: int) Bool:
si rest_k == 0:
retorno restante_target == 0
si rest_target se realizó 0 o rest_k + i
Retorno Falso
# Elige o salta el elemento actual
(dfs(i + 1, remaining_k - 1, remaining_target - nums[i]) o
dfs(i + 1, remaining_k, remaining_target)

si dfs(0, k, target):
Retorno
Retorno Falso
`` `

*Por qué esto es bueno*
* El decorador `@lru_cache` maneja la memoización automáticamente.
* La profundidad de recursión es segura (`n ≤ 30`).
* El código es sólo unas pocas líneas, lo que lo hace ideal para entrevistar sesiones de escritura rápida.

### 5.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
bool splitArraySameAverage(vector identificadoint ánimo nums) {
int n = nums.size();
si (n 0 = 1) devolver falso;

total Sum = 0;
para (int x : nums) total Sum += x;

// clave de memoización: (idx, k, target)
unordered_map significa largo, bool memo;

llave automática = [](int idx, int k, int target) - largo
retorno (static_cast seleccionado largo largo(idx)
(static_cast seleccionado largo largo(k)
static_cast realizado largo largo(target);
};

función recomendadabool(int,int,int) título dfs = [ cl](int idx, int k, int target) - título bool
(k == 0) objetivo de retorno == 0;
si (target Identificado 0 Silencioso k + idx √ n) devuelve falso;
largo tiempo id = clave(idx, k, target);
auto = memo.find(id);
si (lo != memo.end()) devolverlo- título segundo;

bool res = dfs(idx + 1, k - 1, target - nums[idx])
dfs(idx + 1, k, target);
memo[id] = res;
restitución;
};

para (int k = 1; k)
si ((1LL * totalSum * k) % n != 0) continuar;
int target = (int)(1LL * totalSum * k) / n);
si (dfs(0, k, target)) regresan verdaderos;
}
devolver falso;
}
};
`` `

*Por qué esto es bueno*
* La función 'key` empaca los tres enteros en un solo entero de 64 bits, dando O(1) look-ups en el mapa sin orden.
* La lambda recursiva mantiene la lógica compacta.

-...

## 6. Análisis de la complejidad

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
TENED Recursive DP (Memoization) ANTE `O(2^(n/2)' (caso peor) (inscripciones de memoria)
Silencio Meet‐in‐the‐Middle Silencio `O(2^(n/2)'' Silencio `O(2^(n/2)' para almacenar todas las sumas subconjuntas

Con `n = 30`, `2^(n/2) = 2^15 ♥ 32,768`, que encaja cómodamente en la memoria y se ejecuta en unos pocos milisegundos en las CPU modernas.

-...

## 7. Despacho para entrevistadores

1. ** Mención la regla de divisibilidad** primero.
2. **Explicar el problema de la búsqueda**: " subconjunto de tamaño " k " con la suma `target ' .
3. **Elija la recursión + memoización** – mostrar que puede escribir DFS limpio, memoizado.
4. **Opcional**: Si se pide una solución de factor constante aún más rápida, sugiera Meet‐in-the-Middle.

Este problema demuestra la maestría sobre *programación dinamica*, *subset‐sum*, y *bit-mask tricks*, lo que lo convierte en un elemento básico de la entrevista técnica.

-...

## 7. Pensamiento final

Recursive DP + Memoization no es sólo un hack rápido; es una estrategia probada y amigable para entrevistas que equilibra ** elegancia conceptual** y ** rendimiento práctico**.
Siéntete confiado en escribirlo en cualquier idioma, y prepárate para explicar las primeras opciones de poda y memoización: acabas de convertir un problema aparentemente complejo en una solución concisa y eficiente!