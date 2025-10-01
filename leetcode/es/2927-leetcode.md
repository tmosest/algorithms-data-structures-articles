-...
Título: LeetCode 2927. Distribuir caramelos entre niños III -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2927 – Distribuir Candies Entre Niños III
**Hard Silencio LeetCode Silencio O(1) combinatoria**

■ *Problema*
■ Habida cuenta de dos números enteros positivos " n " y " límites " , devuelven el número de formas de distribuir " no " caramelos entre los niños ** tres** para que ningún niño reciba más que " caramelos límites " .
■
■ *Examples*
" texto
Ø n = 5, limit = 2 → 3 ( (1,2,2), (2,1,2), (2,2,1)
√ n = 3, limite = 3 → 10 (todos 10 triples no negativos summing to 3)
" `
■
■ **Constraints**
≤ 1 ≤ n, límite ≤ 108

-...

### Why This Problem is a “Good” Interview Question

* **Pure math + programación** – No hay estructuras de datos, sólo combinatoria.
* ** Escalas a grandes entradas** – Requiere una solución de tiempo constante.
* **Elegant use of inclusion‐exclusion** – Una técnica clásica con la que cada ingeniero senior debe estar cómodo.

-...

### La mala parte

* Las restricciones (108) le obligan a pensar en el flujo entero y aritmética de 64 bits.
* Si te olvidas de que `C(x, 2)` es cero cuando `x < 2`, obtendrás resultados negativos.

-...

### The Ugly Part

* La fórmula final tiene muchos “offsets” (como “limit+1”) que son fáciles de deslizar.
* Un solo tipo en el término combinatorio puede convertir la solución de correcto a salvajemente equivocado.

-...

## Intuición – Desde las estrellas y las barras hasta la inclusión – Exclusión

Sin un límite superior, el número de triples enteros no negativos `(a,b,c)` con `a+b+c = n` es el resultado clásico *stars & bars*:

`` `
T = C(n + 2, 2) // elegir 2 separadores entre N+2 posiciones
`` `

La dificultad es el límite superior**.
Debemos eliminar todos los triples donde al menos un niño recibe más que el límite.
La forma más directa es la Inclusión – Exclusión (PIE):

`` `
respuesta = T
– 3 * (# soluciones con un límite de confianza)
+ 3 * (soluciones# con un límite de título y límite de título)
– (# soluciones con un límite de confianza Y b  título y límite de confianza)
`` `

¿Por qué 3 y por qué +3?
* Hay 3 niños simétricos para la primera resta.
* Hay 3 pares sin orden para la segunda adición.
* Sólo una manera de que los tres superen.

-...

## Calculando cada PIE Mandato

Define

`` `
C2(x) = x*(x-1)/2 si x 2
0 de lo contrario
`` `

### 1. Todos los triples (sin límites)

`` `
T = C2(n + 2)
`` `

### 2. Un niño excede el " límite "

Let `a' = a - (limit+1) ≥ 0`.
Luego `a' + b + c = n - (limit+1)`.
Número de soluciones:

`` `
t1 = C2( n - limit + 1 )
`` `

(Si 'n - limite + 1 < 2` el término es 0.)

### 3. Dos niños superan el límite

Let `a' = a - (limit+1)`, `b' = b - (limit+1)`.
Luego `a' + b' + c = n - 2*(limit+1)` → `n - 2*limit - 2`.
Número de soluciones:

`` `
t2 = C2( n - 2*limit )
`` `

### 4. Los tres niños exceden de " límites "

Que todo sea cambiado: `a' + b' + c' = n - 3*(limit+1)` → `n - 3*limit - 3`.
Número de soluciones:

`` `
t3 = C2( n - 3*limit - 1 )
`` `

-...

Final cerrado Form Formula

`` `
respuesta = C2(n + 2)
– 3 * C2(n - limit +1)
+ 3 * C2(n - 2*limit)
– C2(n - 3*limit - 1)
`` `

Todos los valores intermedios encajan en enteros firmados de 64 bits porque
`n ≤ 108` → el binomio más grande `C(n+2,2)` ♥ 5·1015 se realizó 263.

-...

## Complexity Analysis

Silencio Silencio Silencio Silencio
Silencio----------------
tención Compute 4 binomials tención **O(1)** Silencio **O(1)**

La solución es constante a tiempo y espacio constante – perfecto para los límites dados.

-...

## Code Implementations

A continuación se encuentran soluciones listas para pasar en **Java**, **Python**, y **C+**.
Todos usan aritmética 64-bit (`long` / `int64_t`).

-...

## Python 3

``python
Solución de clase:
def distribution Candies(self, n: int, limit: int) - int:
# helper: C(x, 2) (0 if x ■ 2)
def C2(x: int) - título int:
retorno x * (x - 1) // 2 si x 2 más 0

total = C2(n + 2)
t1 = C2(n - limit +1) # one child √≥ limit
t2 = C2(n - 2 * limit) # dos niños
t3 = C2(n - 3 * limit -1) # todos los tres títulos

total de retorno - 3 * t1 + 3 * t2 - t3
`` `

-...

## Java 17

``java
Clase Solución {
larga privada C2(long x) {
retorno (x >= 2) ? (x * (x - 1) / 2) : 0;
}

public long distribution Candies(int n, int limit) {
total largo = C2(long) n + 2);
larga t1 = C2(long) n - límite + 1); // un niño
larga t2 = C2(long) n - 2L * limit); // dos hijos ⇩
t3 largo = C2(long) n - 3L * límite - 1); // los tres  Conf límite

retorno total - 3 * t1 + 3 * t2 - t3;
}
}
`` `

-...

### C+17

``cpp
Clase Solución {
larga duración C2(long long x) {}
retorno (x >= 2) ? (x * (x - 1) / 2) : 0;
}
public:
Distribución larga Candies(int n, int limit) {
largo tiempo total = C2(static_cast seleccionadolong largo(n) + 2);
largo t1 = C2(static_cast seleccionadolong largo(n) - limit + 1); // one œ limit
t2 largo largo = C2(static_cast seleccionadolong largo(n) - 2LL * limit); // dos √≥n
t3 largo largo = C2(static_cast seleccionadolong largo(n) - 3LL * limit - 1); // all ⇩

retorno total - 3 * t1 + 3 * t2 - t3;
}
};
`` `

-...

## Cómo probar

``text
Entrada: n = 5, límite = 2
Producto: 3

Entrada: n = 3, límite = 3
Producto: 10

Entrada: n = 1, límite = 1
Producto: 3 (0,0), (0,0), (0,0,1) )
`` `

Siéntete libre de conectar esto al IDE online de LeetCode.

-...

Consejos para su próxima entrevista de codificación

1. **Busca atajos combinatorios** – `estrellas ' barras casi siempre produce una fórmula 'C(n+2, 2)`.
2. **Use Inclusión – Exclusión para los límites superiores** – es una línea única una vez que escriba el ayudante de la C2.
3. **Guardar contra el desbordamiento** – siempre arrojado a 64 bits antes de la multiplicación.
4. **Validar la fórmula en los casos límite** ( " n " ≤ " , " n " .

-...

### SEO Etiquetas " Palabras clave

- `distribuir caramelos entre niños `
- `código de texto 2927 `
- `O(1) solution combinatorics `
- Entrevista de exclusión de la inclusión `
- Consejos de entrevista de codificación `
- algoritmo de entrevista de trabajo `
- 'c++ java python leetcode `

-...

Codificación feliz – que esta solución limpia, O(1) te aterrice el trabajo que buscas!