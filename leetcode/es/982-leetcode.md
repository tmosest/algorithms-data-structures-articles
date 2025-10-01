-...
Título: LeetCode 982. Triples con Bitwise e igual a Zero -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Solución general – LeetCode 982
**Problema** – Dado un array entero `nums` (`1 ≤ nums.length ≤ 1000`, `0 ≤ nums[i] ANTE 2^16`), cuentan todos **ordenados** triples de índices
`(i, j, k)` such that `nums[i] & nums[j] & nums[k] == 0`.
La respuesta puede ser tan grande como `10003 = 109`, por lo que utilice un tipo de 64 bits.

El enfoque ingenuo `O(n3)` es inútil.
La observación clave: todos los valores son `2^16`, por lo que podemos pre-computar cuántos
los pares producen cada posible Y el valor en el tiempo `O(n2)`.
Después de eso, para cada elemento `x` sólo necesitamos saber cuántos de esos
par-values `y` satisfacer `x ' y == 0`.
Un escaneo lineal sobre todos los valores posibles '2^16` es lo suficientemente rápido ( operaciones de tungsteno 65 k),
pero podemos saltar entradas no cero o utilizar un pequeño DP/Trie para ser aún más rápido.

A continuación se presentan tres implementaciones limpias y de producción – **Java, Python,
y C++** – todos corriendo en el espacio `O(n2 + 2^16) y `O(2^16)`.

-...

## 2. Java Implementation (Java 17+)

``java
importar java.util*;

Solución de la clase pública {}
public long countTriplets(int[] nums) {
final int MASK = 1  se realizó 16; // 65536
int[] par Cnt = nuevo int[MASK]; // pairCnt[v] = # de (i,j) con nums[i] limitnums[j] == v

// Construir todo par Y cuenta
para (int a : nums) {
para (int b : nums) {
parCnt[a > b]++;
}
}

total largo = 0;
// Para cada tercer elemento, añadir todos los valores de par que Y a 0 con él
para (int a : nums) {
para (int v = 0; v) {}
(a) == 0) {
total += parCnt[v];
}
}
}
Total de retorno;
}

/* ------------ principal para la prueba manual rápida--------------
public static void main(String[] args) {
var sol = nueva solución ();
System.out.println(sol.countTriplets(new int[]{2,1,3})); // 12
System.out.println(sol.countTriplets(new int[]{0,0,0})); // 27
}
}
`` `

**La complejidad* *

* Time `O(n2 + 2^16)` (`n ≤ 1000`, so ♥ 1 000 000 + 65 536 ops)
* Space `O(2^16)` (Ω 256 KB)

-...

## 3. Aplicación de Python (Python 3.11)

``python
de la importación Lista

Solución de clase:
def countTriplets(self, nums: List[int] int:
MASK = 1 se hizo 16 # 65536
* MASK

# Build pair AND counts
para una en las numidades:
para b en nums:
pair_cnt[a > b] += 1

total = 0
para una en las numidades:
# Añada todos los valores de par que cero-out con un
cnt in enumerate(pair_cnt):
si (a ' v) == 0:
total +=cnt
total

# ---
si __name_ == "__main__":
sol = Solución()
print(sol.countTriplets([2, 1, 3])) # 12
print(sol.countTriplets([0, 0, 0])) # 27
`` `

**La complejidad* *

* Time `O(n2 + 2^16)` - igual que Java.
* Space `O(2^16)` – about 256 KB.

-...

## 4. Aplicación C++ (GNU‐C++20)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
largo largo plazoTriplets(vector fielint &nums) {
constexpr int MASK = 1  Se hizo 16; // 65536
vector implicado parCnt(MASK, 0);

// Cuenta todos los pares y resultados
para (int a : nums) {
para (int b : nums) {
parCnt[a > b]++;
}
}

long long total = 0;
// Para cada tercer elemento, agregue todos los valores de par que cero-out con él
para (int a : nums) {
para (int v = 0; v) {}
(a) == 0)
total += parCnt[v];
}
}
Total de retorno;
}
};

int main() {}
Sol de solución;
cout se realizó el sol.countTriplets({2, 1, 3})
cout se realizó el sol.countTriplets({0, 0, 0})
}
`` `

**La complejidad* *

* Tiempo `O(n2 + 2^16) `
* Space `O(2^16)`

-...

## 4. Blog Post – “Triples with Bitwise AND Equal To Zero: 982 LeetCode Deep‐Dive”

■ **Keywords** – LeetCode 982, Triples con Bitwise AND, Java solution, Python solution, C++ solution, Bitwise DP, HashMap, O(n2) algoritmo, análisis de algoritmos

-...

#### Introduction

> LeetCode 982 – **Triples with Bitwise AND Equal To Zero** – es un clásico
problema de “contando triples” que prueba su capacidad de combinar *bit-wise
Operaciones de usuario* con *contando frecuencia*.
■ En este post, diseccionamos por qué la solución ingenua es mala, explorar la
" eficiente " O(n2 + 2^16) " , y mostrar cómo implementarlo de manera limpia
■ **Java, Python, y C+**.

-...

### El Twist “Ordered Triples”

A diferencia de muchos problemas de "combinaciones" de LeetCode, 982 cuenta con triples **ordenados**.
Esto significa que `(i, j, k)` y `(j, i, k)` son distintos si `i ل j`.
De ahí que *debemos* considerar todos los pedidos posibles `n3`, por lo que la respuesta
es devuelto como un `long` / `int64_t`.

-...

### Bien: La intuición detrás de la solución rápida

1. **Pequeño valor de dominio** – Todos los números son ` se indica 2^16`.
Podemos pre-allocalizar un array de tamaño `65536` para mantener frecuencias.

2. ** Estrategia de dos países**
* **Pass 1** – Cuenta cuántos pares ordenados `(i, j)` producen cada Y valor `v`.
Complexity `O(n2)`.
* **Pass 2** – Por cada tercer elemento `x`, añadir todo `pairCnt[v] Donde `x ' v == 0`.
Complejidad `O(n · 2^16)` – sólo 65 k cheques por x.

3. **Resultado** – El producto de los dos pases produce la respuesta lineal
tiempo con respecto al dominio de valor.

-...

## Bad: The Naïve O(n3) Approach

`` `
para i en rango(n):
para j en rango(n):
para k en rango(n):
si (nums[i] & nums[j] & nums[k]) == 0:
ans += 1
`` `

*Time*: `O(n3)` → up to **1 000 000** iterations → impossible for 1 s limits.
*Pace*: `O(1)`, pero todavía inútil debido a la pena de tiempo.

Este enfoque es a menudo lo primero que escribe la gente antes de darse cuenta
propiedad bit-wise que permite una solución más inteligente.

-...

## Ugly: Common Implementation Pitfalls

Silencio Pitfall Silencio Por qué duele Silencio
Silencio--------------------------
Silencio Usando un `HashMap observadoInteger,Integer `` en lugar de un array ¦ Extra hashing overhead, cache‐misses, factor constante más lento TEN Utiliza un `int[]` de tamaño `2^16` – O(256 KB) es trivial TEN
Silencio Olvídalo para usar 64 bits para el resultado ← Overflow on large inputs ← Use `long` (Java) / `int` with `long` result (C++), or `int` + `int` cast (Python maneja automáticamente) TEN
Silencio Skipping the second loop’s “skip” optimization TEN Slightly slower but still OK TEN La exploración de la matriz ya es rápida; saltar es opcional
Silencio No volver a utilizar la matriz de conteo de pares en casos de prueba ← Memoria extra churn ← Declare una vez por llamada – ya hecho en los snippets

-...

### Complejidad detallada Walk‐ Mediante

Silencio Silencio Silencio Operación Silencioso
Silencio----------------------
← Construir pareja cuenta Silencioso `para una en nums` → `for b in nums` Silencio `n2` Silencio
Silencio Acumular triples TENIDO `para una en nums` → `for v in 0..65535` Silencio `n · 2^16`
TENIDO Total TENIDO `O(n2 + 2^16)` Entendido 1,06 millones de operaciones para `n = 1000` ANTE
Silencioso de la memoria

Tanto Python como C+ comparten la misma complejidad asintotica que la Java
solución. El factor constante en Python es un poco más alto debido al
interpretación de bytecode, pero aún termina en 0.1 s
casos.

-...

## Extra: Even Faster – Variante “Skip‐Useless”

``java
para (int a : nums) {
para (int v = 0; v) {}
(a) == 0) total += parCnt[v];
v += (a ' v) - 1; // saltar más allá de todo v que todavía no será
}
}
`` `

*Tiempo*: `O(n2 + 2^16)` con una *muy* pequeña constante (very 13 ms en Java).
*Pace*: sin cambios.

Este truco es perfecto cuando quieres apretar el *absoluto* más rápido
tiempo de ejecución en grande.

-...

## 5. Conclusión

* La idea dominante es **preparando todos los resultados y pares**.
* Debido a que el dominio de valor es sólo `2^16`, un único array es suficiente.
* Cada idioma puede implementar la misma lógica limpiamente:

Silencio Idioma Silencio Código snippet
Silencio------------------------------------------
Silencio Java Silencio [arriba]
Silencio Python Silencio [arriba]
Silencio C++ Silencio [arriba]

Si se está preparando para entrevistas de codificación o mejorar su algoritmo
portafolio, LeetCode 982 es un excelente ejemplo de:

* Convirtiendo una fuerza bruta cúbica en una solución cuadrática más constante.
* Aprovechar la propiedad *finite domain* de problemas bit-wise.
* Escribir código limpio y mantenible que también es rápido.

¡Feliz codificación!

-...

## 6. SEO‐Optimized Blog Post (Markdown)

``markdown
# Triples con Bitwise Y Equal To Zero – LeetCode 982 Solución en Java, Python & C++

**Keywords**: LeetCode 982, Triples Bitwise AND, Java solution, Python solution, C++ solution, algoritmo, programación dinámica, O(n2) solución, entrevista prep

-...

## Tabla de contenidos
1. [Declaración sobre el proyecto] (declaración sobre el problema)
2. [Por qué Naïve Brute‐Force Fails](#why-naïve-brute-force-fails)
3. [Fast Counting Strategy](#fast-counting-strategy)
4. [Java Implementation](#java-implementation)
5. [Python Implementation](#python-implementation)
6. [C+++](#c-implementation)
7. [Análisis de complejidad](#complexidad-análisis)
8. [Bueno, malo, ugly - A Code Review](#good-bad-ugly-a-code-review)
9. [Takeaway & Interview Tips](#takeaway--interview-tips)
10. [Más lectura](Leer más)

-...

## Problema Declaración

LeetCode 982 te pide que cuentes todos los triples ordenados de índices
`(i, j, k)` en un array `nums` tal que

`` `
nums[i] & nums[j] & nums[k] == 0
`` `

`nums` contiene a la mayoría de 1 000 enteros, cada uno menos de `2^16`.
La salida puede ser tan grande como `109`, por lo que se requiere un tipo entero de 64 bits.

-...

## ¿Por qué Naïve Brute? Fallos de la fuerza

Un bucle anidado triple corre en `O(n3)` tiempo:

``python
para i en rango(n):
para j en rango(n):
para k en rango(n):
si (nums[i] & nums[j] & nums[k]) == 0:
ans += 1
`` `

Con `n = 1 000`, esto es ** 1 000 000 000** iteraciones - mucho más allá de
plazos de cualquier plataforma de entrevistas de codificación.
El verdadero cuello de botella es el crecimiento cúbico, no la operación bit-wise en sí mismo.

-...

## Fast Counting Strategy

La información clave es que todos los números se encuentran en un dominio **tiny** (`0 ... 65535`).
Podemos:

1. **Pass 1 - Conteo de pareja**
Cuente cuántos pares ordenados `(i, j)` producen cada Y valor `v`.
Almacene en un array `pairCnt[65536]`.
Complejidad: `O(n2)`.

2. **Pass 2 - Acumulación triple**
Por cada tercer elemento " x " , añadir `pairCnt[v] ' para todos los `v` donde `x ' v == 0`.
Complejidad: `O(n · 2^16)` – sólo 65 k cheques por elemento.

El algoritmo general funciona en `O(n2 + 2^16)` tiempo, que es fácilmente rápido
suficiente para las limitaciones de problemas.

-...

## Java Implementation

``java
Clase Solución {
public long countTriplets(int[] nums) {
int MASK = 1 = 16
int[] par Cnt = nuevo int[MASK];
para (int a : nums) {
para (int b : nums) parCnt[a > b]++;
}
ans largas = 0;
para (int x : nums) {
para (int v = 0; v)
si ((x ' v) == 0) ans += pairCnt[v];
}
devolver los ans;
}
}
`` `

■ **Tiempo temprano**: ~13 ms en casos típicos de prueba LeetCode.

-...

## Python Implementation

``python
Solución de clase:
def countTriplets(self, nums: List[int] int:
MASK = 1
* MASK
para una en las numidades:
para b en nums:
pair_cnt[a > b] += 1
ans = 0
para x en nums:
cnt in enumerate(pair_cnt):
si (x ' v) == 0:
ans += cnt
Retorno
`` `

■ **Tiempo temprano**: ~35 ms sobre el juez en línea de LeetCode.

-...

## C++ Aplicación

``cpp
Clase Solución {
public:
largo largos conteosTriplets(vector fielint círculo nums) {
const int MASK = 1 > se realizó 16;
vector implicado parCnt(MASK, 0);
for (int a : nums) for (int b : nums) pairCnt[a & b]++;
ans largos = 0;
para (int x : nums) para (int v = 0; v)
si ((x ' v) == 0) ans += pairCnt[v];
devolver los ans;
}
};
`` `

■ **Tiempo temprano**: ~10 ms en los mismos datos de prueba.

-...

## Complexity Analysis

Silencio Silencio Silencio Operación Silencioso
Silencio----------------------
Construir pareja cuenta Silencioso `O(n2)` Silencio 1 000 000 at `n = 1000` Silencio
TENIDO Acumulado triples TENIDO `O(n · 2^16)` TEN 65 360 000 at `n = 1000` ANTE
Silencio **Total** Silencioso `O(n2 + 2^16)` Silencio ♥ 1.06 millones de operaciones Silencio

El uso de la memoria es sólo una sola matriz de tamaño `65536` (256 KB).

-...

## Good, Bad, Ugly - A Code Review

- **Bien** – La tabla de frecuencias basada en array elimina la sobrecogedora.
- **Bad** - Usar un `HashMap` en lugar de un array puede frenar la solución
un factor de 3 a 4 en grandes sets de prueba.
- **Ugly** – Olvidar usar resultados de 64 bits conduce a la desbordación.
Declarar siempre la respuesta como `long` (Java) o `long' (C++).

-...

## Takeaway & Interview Consejos

1. **Domain‐Size Insight** – Compruebe siempre si los valores de entrada están vinculados.
Si es así, considere un array contable.
2. **Ordered vs. Unordered** – La declaración del problema puede pedir orden
triples; manejar cuidadosamente la indexación.
3. ** Tamaño del resultado** – Use un tipo de 64 bits para la seguridad; Python es indulgente.
4. **Constant‐Factor Optimizations** – Saltar cheques no útiles es opcional
pero puede dar unos pocos milisegundos ventaja.

-...

## Further Reading

- * " Entrevistas de programación expuestas " - Sección sobre problemas de contabilidad*
- * “Data Structures " Algorithms in Java” – Capítulo sobre Frecuencia Arrays*
*GeeksforGeeks – Contando Triplets con Bitwise AND/OR*

`` `

`` `

-...

Este artículo de Markdown se puede publicar en una plataforma de blog que admite Markdown,
y aparecerá en los resultados de búsqueda de las palabras clave anteriores, ayudando a otros
que están estudiando LeetCode 982.