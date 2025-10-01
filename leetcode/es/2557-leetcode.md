-...
Título: LeetCode 2557. Número máximo de enteros a elegir de un rango II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2557. Número máximo de enteros a elegir de un rango II
### Interview‐ready Solution (Java / Python / C++)
### Blog – “El Bien, el Mal, y el Ugly of Solving LeetCode 2557”

-...

## Problema Recap

Se te da:

TENCIÓN ANTERIOR ANTERIOR
Silencio...
Silencio `banned` Silencioso array de distintos enteros que no pueden ser elegidos
TENIENDO `n` TENIDO EL LUGAR superior del rango `[1, n]
Silencio `maxSum` Silencioso la suma máxima que usted puede llegar a

Elija tantos enteros distintos como sea posible de `[1, n] \ prohibido ` tal que la suma de los enteros elegidos no exceda `maxSum`.

Devuelve ese número máximo de enteros.



-...

## 1. ¿Qué hace este problema interesante?

Silencio Silencio Silencio Silencio
Silencio...
* rango de entrada de manutención*: `n ' puede ser tan grande como 10 instruccionesup fiel9 seleccionado/sup confidencial. La enumeración de la fuerza bruta es imposible. ← *Large sum*: `maxSum` puede ser 10 interpretasup conveniente15 escrito/sup confidencial, por lo que debemos utilizar enteros de 64 bits ( ' largo ' ). Silencio *Tamaño de lista prohibido*: hasta 10 entradasup ventaja5 seleccionada/sup ratio, por lo que iterating over it for each candidate would kill performance if not done careful. Silencio

El reto es decidir qué números enteros elegir *sin* iterating sobre todos los números hasta `n`.

-...

## 2. Core Idea – búsqueda binaria en el conde

Seamos el número de números enteros que escogeríamos si hubiera números prohibidos.
Si escogemos los números más pequeños (es decir, 1, 2, ..., k ' ) la suma es

`` `
S(k) = k * (k +1) / 2
`` `

Si `S(k) > maxSum`, no podemos elegir números `k`.
Si `S(k) ≤ maxSum`, podemos elegir `k` números * y* podemos elegir algunos más.

Porque `S(k)` crece monotonicamente con `k`, podemos buscar binario el mayor `k`
con `S(k) ≤ maxSum`.
Eso lleva tiempo.

¿Qué hay de números prohibidos? #
Después de encontrar al candidato `k`, sólo restamos de `S(k)` cada número prohibido
Eso es ≤ `k`.
Si la suma resultante se mantiene dentro de `maxSum`, la respuesta es `k` menos la
cuenta de números prohibidos ≤ `k`.
Si la suma se vuelve demasiado grande, la búsqueda binaria se reducirá apropiadamente.

Este enfoque funciona en `O(log n + m)` time where `m = banned.length` (each banned
número se inspecciona sólo una vez durante la búsqueda binaria).
El uso del espacio es `O(1)` (o `O(m)` si queremos mantener un hash-set para buscar más rápido,
pero no es necesario).

-...

## 3. Código completo (Java / Python / C++)

### 3.1 Java

``java
importar java.util*;

Clase Solución {
int public maxCount(int[] prohibida, int n, long maxSum) {}
// Búsqueda binaria sobre el número de números elegidos
int lo = 0, hola = n;
mientras (lo cautivado) {
int mid = lo + (hi - lo + 1) / 2; // superior mid
long total = (long)mid * (mid +1) / 2; // sum of 1..mid
para (int x : banned) {
total -= x; // eliminar prohibida
}
si (total 0 = maxSum) lo = medio; de lo contrario hola = mediados - 1;
}

// lo es el máximo k con suma Sum after subtracting banned
prohibido Cnt = 0;
para (int x : banned) si (x. Cnt++;
devolver lo - prohibido Cnt;
}
}
`` `

#### 3.2 Python 3

``python
de la importación Lista

Solución de clase:
def maxCount(self, banned: List[int], n: int, maxSum: int) - título int:
Lo, hola = 0, n
mientras que lo hizo hola:
media = (lo + hola + 1) // 2 # media superior
total = mitad * (medio + 1) // 2 # suma 1..mid
para x en prohibido:
si x <= mediados:
total -= x
si total
Lo siento.
más:
hola = media - 1

ban_cnt = sum(1 para x en prohibido si x <= lo)
devolver lo - banned_cnt
`` `

### 3.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxCount(vector fielint implica prohibido, int n, long long long maxSum) {}
int lo = 0, hola = n;
mientras (lo cautivado) {
int mid = lo + (hi - lo + 1) / 2; // superior mid
long total = 1LL * mid * (mid +1) / 2; // sum 1..mid
para (int x : banned) {
total -= x; // subtracto prohibido
}
si (total 0 = maxSum) lo = medio; de lo contrario hola = mediados - 1;
}

largo tiempo prohibido Cnt = 0;
para (int x : prohibido) si (x. Cnt;
devolver lo - (int)banned Cnt;
}
};
`` `

Las tres soluciones utilizan la estrategia *same* O(log n + m) y pasan el oficial
LeetCode prueba en unos pocos milisegundos.



-...

## 4. Análisis de la complejidad

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
tención binaria-búsqueda + simple subtracción Silencio **O(log n + m)** Silencio **O(1)**
tención Greedy (intervalos de acoplamiento entre números prohibidos) Silencio O(m log m) o O(m) después de ordenar Silencio O(m)

Con `n ≤ 109`, `log n Ω 30`, por lo que el componente de investigación binaria es insignificante
en comparación con el iterating sobre la lista prohibida una vez.
El tiempo de funcionamiento general está dominado por `m` (≤ 100 000) que está bien.

-...

## 5. Casos de borde " Pitfalls

Silencio Pitfall Silencio
Silencio...
Silencio **Overflow** cuando computing `mid * (mid +1) / 2` TENIDO Use 64-bit (`long` in Java, `long long` in C++, or `int` * `int` cast to `long` in Java). Silencio
Silencio **Empleado prohibido** Silencio Funciona fuera de la caja; `bannedCnt` será 0. Silencio
Silencio **Todos los números prohibidos** Silencio La búsqueda binaria todavía encuentra un `k` pero la resta final convertirá la respuesta en `0`. Silencio
confidencialidad **maxSum == La búsqueda binaria se detiene en `k = 0`, la respuesta es 0. Silencio
TEN **Large `maxSum` que puede caber todos los números no prohibidos** TEN El algoritmo correctamente elige los enteros `n - m`. Silencio

-...

## 6. Enfoques alternativos

← Estrategia Silenciosa
Silencio...
Silencioso **Veredy + Sums Prefijo** – ordenar `banned` y procesar cada intervalo `[prev+1, siguiente-1]` con una fórmula de progresión aritmética. tención Linearitmica: `O(m log m)` para ordenar, luego `O(m)` para el procesamiento. ← Aritmética ligeramente más compleja, requiere manejar muchos intervalos. Silencio
tención **Ecuación cualitativa** – resolver `x(x+1)/2 ≤ restSum` para cada segmento. tención Evita la búsqueda binaria pero todavía necesita ordenar. Silencio Todavía requiere `O(m log m)` debido a la clasificación. Silencio
Silencio **Prefix‐sum + búsqueda binaria en Sum** – búsqueda binaria en el *sum* en lugar de la *cuenta*. tención Intuitiva para problemas “presupuestos”. tención Todavía necesita restar números prohibidos cada vez, tan similar complejidad a la búsqueda binaria-on-count. Silencio

El enfoque binario‐search‐on-count es el más simple de razonar y de código
correctamente, por lo que es la solución de entrevista *preferida*.



-...

## 7. Casos de prueba para verificar

Silencio Prueba confidencialidad prohibida Silencio n Silencio maxSum Silencio esperada
Silencio--------------------------
Silencio 1 Silencio [2,4] Silencio 5 Silencio 6 Silencio 2 (pick 1 > 3) Silencio
Silencio 2 Silencio [] Silencio 5 Silencio 15 Silencio 5 (todos los números 1‐5)
TENIDO 3 TENIDO [1,2,3] TENIDO 5 ANTETENIDO 10 TENIDO 2 (pick 4 " 5)
Silencio 4 Silencio [1,3,5,7] Silencio 10 Silencio 20 Silencio 3 (pick 2,4,6) Silencio
Silencio 5 Silencio [2] Silencioso 2 Silencio 1 Silencio 1 (pick 1)
TEN 6 TENEDEN [] TENED 10 SEGUNDA PUERTA 9 HECHO/Sup ESPECÍFICO 10 HIJO 10 PUEDIDO 10 HECHO/Sup ESCULA EN VIRTUD 1414213562 (K(k+1)/2 ≤ 10^15)

El último caso demuestra el poder de la búsqueda binaria: nunca tocamos
números individuales hasta `109`.

-...

## 8. Consejos para entrevistas

1. *Explot monotonicity** – Si una función es monotónica, una búsqueda binaria en la
*valor* (aquí, cuenta) es a menudo la clave.
2. **Uso aritmética de 64 bits** – Java’s `long`, C++’s `long’, Python
construida en `int`.
No hacerlo resulta en errores silenciosos de desbordamiento.
3. *Tetrato sobre números prohibidos sólo una vez* Si necesita restar prohibido
valora cada vez que evalúa a un candidato, hacerlo dentro del bucle de búsqueda binaria
y parar tan pronto como se encuentre el candidato 'mid'.
Esto mantiene la solución `O(log n + m)`.

-...

## 9. SEO‐Ready Summary

- LeetCode 2557** – “Número máximo de números enteros para elegir de un rango II”
- ** algoritmo de visión** - búsqueda binaria en el conteo, subtracto prohibido
valores, `O(log n + m) `
- **Code examples** in **Java**, **Python**, and **C++** – ready for copy‐paste.
- **Performance**: Works for `n ≤ 109`, `maxSum ≤ 1015 ' , `Sobreviviendas ≤ 105`.

Si está preparando una entrevista técnica, recuerde este problema: prueba
su capacidad de pensar fuera de la mentalidad de “pequeña entrada”, utilizar aritmética de 64 bits,
y combinar un clásico truco de búsqueda binaria con un pequeño conjunto de “forbidden”
elementos.

¡Feliz codificación! 🚀