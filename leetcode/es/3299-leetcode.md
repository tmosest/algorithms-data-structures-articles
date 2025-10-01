-...
Título: LeetCode 3299. Suma de las consecuencias consecutivas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📌 Problem Recap – Sum of Consecutive Subsequences (LeetCode 3299)

Dado un array entero `nums` (1 ≤ `nums[i]` ≤ 105, 1 ≤ `nums.length` ≤ 105), un ** subsequencia consecutiva** es un subsequence no vacío cuyos elementos forman una progresión aritmética que aumenta estrictamente o disminuye con diferencia ±1.
El *valor* de una subsequencia es la suma de sus elementos.

** Objetivo** – devolver la suma de los valores de **all** subsequences no vacías consecutivos modulo 109+7.

■ *Ejemplo*
[1, 4, 2, 3]
■ Subsequences consecutivos:
[4] ``, ``, `[2]`, ``, ``, `[1,2]`, `[2,3]`, `[4,3]`, `[1,2,3] ``
■ Suma de valores = 31

-...

## 🔑 Solution Overview

La enumeración ingenua O(2n) es imposible.
Observa:

* Una subsequencia consecutiva puede dividirse en una carrera creciente y una carrera decreciente.
* Si procesamos la matriz **para adelante** podemos calcular, por cada valor `v`,
* " cntInc[v] " , cuántas subsecuencias crecientes terminan con el valor `v `
*`sumInc[v]* – el valor total de esas subsecuencias
* Del mismo modo, un pase **backward** da las partes decrecientes.

Con estos dos pases podemos combinar los recuentos y sumas para obtener la respuesta final en **O(n + maxValue)** tiempo y **O(maxValue)** memoria (maxValue ≤ 105).

### Por qué funciona

For a fixed value `x` that appears at position `i`:

1. **Aumento del lado**: toda subsequencia que termine en `x' debe haberse extendido de una subsequencia que terminó en `x-1' inmediatamente antes de `i.
*Nuevo recuento* = " cntInc[x-1] + 1 " ( "+1 " para la subsecuencia que consiste en sólo " x " ).
*Nueva suma* = `sumInc[x‐1] + x * (cntInc[x‐1] + 1).

2. **Disminución del lado** – simétrico, utilizando `x+1` como valor anterior.

La contribución total de todas las subsecuencias que terminan en `x` es la suma de las dos partes, menos la subsequencia de un solo elemento doble contada (manejada naturalmente por las ecuaciones DP).

El mismo DP funciona en el paso atrasado para la dirección decreciente. Por último, para cada valor `v` añadimos las sumas de ambos pases y restamos la subsecuencia de un solo elemento contada.

Todas las operaciones se realizan modulo **M = 1 000 000 007**.

-...

## 📄 Code Implementations

### 1. Java (O(n) DP on values)

``java
importa java.util. HashMap;

Solución de la clase pública {}
int final estático privado MOD = 1_000_000_007;

int sumOfConsecutiveSubsequences(int[] nums) {
int maxVal = 0;
para (int v : nums) maxVal = Math.max(maxVal, v);

long[] cntInc = nuevo largo[maxVal + 2];
long[] sumInc = new long[maxVal + 2];
long[] cntDec = new long[maxVal + 3];
long[] sumDec = new long[maxVal + 3];

// Paso adelante – dirección creciente
para (int v : nums) {
c = cntInc[v - 1] + 1;
long s = sumInc[v - 1] + v * c;
cntInc[v] = (cntInc[v] + c) % MOD;
sumInc[v] = (sumInc[v] + s) % MOD;
}

// Pase atrás – dirección decreciente
para (int i = nums.length - 1; i √≥= 0; --i) {
int v = nums[i];
c = cntDec[v + 1] + 1;
long s = sumDec[v + 1] + v * c;
cntDec[v] = (cntDec[v] + c) % MOD;
sumDec[v] = (sumDec[v] + s) % MOD;
}

ans largas = 0;
para (int v = 1; v) {}
as = (ans + sumInc[v] + sumDec[v]) % MOD;
// subtracto doble contado elemento único subsequence
as = (ans - v + MOD) % MOD;
}
retorno (int) ans;
}
}
`` `

**Las complejidades* *

* Tiempo: `O(n + maxValue)` (≤ O(n) en la práctica)
* Memoria: `O(maxValue)` (conejo 4 × 105 largos →

-...

### 2. Python (O(n) DP with dictionaries)

``python
MOD = 1_000_000_007

def sum_of_consecutive_subsequences(nums):
max_val = max(nums)
cnt_inc = [0] * (max_val + 2)
sum_inc = [0] * (max_val + 2)
cnt_dec = [0] * (max_val + 3)
sum_dec = [0] * (max_val + 3)

Adelante
para v en nums:
c = cnt_inc[v - 1] + 1
s = (sum_inc[v - 1] + v * c) % MOD
cnt_inc[v] = (cnt_inc[v] + c) % MOD
sum_inc[v] = (sum_inc[v] + s) % MOD

# Backward pass
for v in reversed(nums):
c = cnt_dec[v + 1] + 1
s = (sum_dec[v + 1] + v * c) % MOD
cnt_dec[v] = (cnt_dec[v] + c) % MOD
sum_dec[v] = (sum_dec[v] + s) % MOD

ans = 0
para v en rango(1, max_val + 1):
ans = (ans + sum_inc[v] + sum_dec[v] % MOD
ans = (ans - v + MOD) % MOD # remove double counted single element
Retorno
`` `

-...

### 3. C++ (O(n) DP with vector)

``cpp
#include יbits/stdc++.h
usando std namespace;

const int MOD = 1'000'007;

int sumOfConsecutiveSubsequences(vector interpretadoint hombro nums) {
int maxVal = *max_element(nums.begin(), nums.end());
vector realizado largo tiempo cntInc(maxVal + 2, 0), sumInc(maxVal + 2, 0);
vector realizado largamente confianza cntDec(maxVal + 3, 0), sumDec(maxVal + 3, 0);

// Adelante
para (int v : nums) {
largo c = cntInc[v - 1] + 1;
long long s = (sumInc[v - 1] + 1LL * v * c) % MOD;
cntInc[v] = (cntInc[v] + c) % MOD;
sumInc[v] = (sumInc[v] + s) % MOD;
}

// Pase trasero
para (int i = nums.size() - 1; i √≥= 0; --i) {
int v = nums[i];
largo c = cntDec[v + 1] + 1;
long long s = (sumDec[v + 1] + 1LL * v * c) % MOD;
cntDec[v] = (cntDec[v] + c) % MOD;
sumDec[v] = (sumDec[v] + s) % MOD;
}

ans largos = 0;
para (int v = 1; v) {}
as = (ans + sumInc[v] + sumDec[v]) % MOD;
ans = (ans - v + MOD) % MOD; // eliminar doble elemento único contado
}
volver estática_cast seleccionado(ans)
}
`` `

-...

## 📚 Blog Article – “The Good, The Bad, and The Ugly of Solving LeetCode 3299”

### Title
**Sum of Consecutive Subsequences – The Good, The Bad, and The Ugly (O(n) DP on Values)* *

## Meta Descripción
Aprende cómo romper LeetCode 3299 en tiempo de entrevista. Caminamos por el truco DP, las trampas y el código en Java, Python y C++. Obtenga consejos de entrevista que los reclutadores aman!

### ¿Por qué?
Si usted está preparando una entrevista **Software-ingeniería** o buscando mostrar su problema-solviendo chops en su currículum, LeetCode 3299 es un *gran punto de conversación*. Prueba:

* **Prueba** – usted debe ver el *valor* de una subsequencia como una suma de una ejecución de los `±1` valores.
* **Space-time trade‐offs** – manejando 105 valores de manera eficiente.
* **Careful modulo arithmetic** – un clásico “gotcha” para muchos candidatos.

A continuación hay una guía completa que mantendrá impresionados a los entrevistadores.

-...

### 1. El bueno – elegante DP en el espacio de valor

* **Tiempo de trabajo* Una vez que usted piensa en términos de *valores* en lugar de posiciones, la solución colapsa a dos pases.
* ** Recidiva intuitiva** – `cnt[v] = cnt[v-1] + 1` y `sum[v] = sum[v-1] + v * cnt[v]`.
Estos son simples de derivar y fáciles de recordar.
* **Low Memory** – un vector de tamaño `max(nums)+2` es pequeño en comparación con la entrada.

**Take‐away**: Si puede reescribir un problema complejo de “subsequencia” en una recurrencia sobre valores de elementos, a menudo desbloquea una solución lineal.

-...

### 2. Los malos – las caídas comunes que rompen su código

Silencio Pitfall Silencio Por qué sucede 
Silencio...
Silencio **Usando `int` for sums** Silencio `sumInc` puede alcanzar 105 * 105 * 105 ♥ 1015 Silencioso `long long` (Java `long`, Python `int` is unbounded, C++ `long long') Silencio
Silencioso ** Modulo de Micción** Silencioso Las Sutracciones pueden ser negativas para siempre Add `MOD` before `% MOD` Silencio
Silencio **Cuento doble de elementos únicos** Silencio Aumentar y disminuir pases ambos añadir `[x]` Subtract `x` una vez al final
Silencio **Sexo fuera de los límites** Silencio `cntInc[v-1]` cuando `v=1`  Allocate size `maxVal+2` y comienza desde `v-1 ⇩= 0. Silencio
Silencio **Tiempo de salidas en grande `maxValue`** Silencio Si asignas un array para 109 valores Silencio Cap el tamaño a `max(nums)+2` (≤ 105) o usa `unordered_map`

-...

### 3. El Ugly - Cuando la Fuerza Bruta Idea Misleads

Muchos candidatos comienzan enumerando todas las subsecuencias, esperando que la poda ayude. Incluso después de la poda, el factor de ramificación sigue siendo enorme. La parte “muy” se está dando cuenta de que ** no se puede iterar sobre subsequences** – se debe iterar sobre **valores**.
Cuando finalmente averiguas el DP, el código parece compacto, pero la verdadera lucha está recordando los términos *plus‐1* para la nueva subsequencia de un solo elemento y manejar correctamente la dirección decreciente.

-...

### 📈 Complejidad Recap (SEO Palabras clave)

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio Java Silencio O(n) Silencio O(105)
Silencio Python Silencio O(n) Silencio O(105)
Silencio C++ Silencio O(n) Silencio O(105)

*“O(n) DP on values”* y *”modulo 109+7”* son los términos que los reclutadores suelen preguntar en entrevistas de codificación.

-...

#### 🎯 Interview Tips

1. Cierra la recurrencia en una pizarra. Dibuja un pequeño ejemplo, escriba `cntInc[v]`, `sumInc[v]` en el tablero, y muestre cómo se actualizan.
2. **Explicar los dos pases**: hacia adelante para aumentar, hacia atrás para disminuir. Esto demuestra que puedes pensar en la simetría.
3. *Mención del truco del modulo* “Todas las operaciones se realizan mod M, por lo que necesitamos añadir `M` antes de tomar `% M` para evitar negativos. ”
4. **Mostrar su código** – resaltar los dos lazos. Los entrevistadores aman código limpio, auto-commentedo.
5. **Hablar sobre casos de borde** – arrays de elementos únicos, todos los elementos iguales, patrones alternantes. Esto indica un profundo entendimiento.

-...

### 💼 Cómo usar este artículo en tu búsqueda de empleo

* **SEO Palabras clave** – “Sum of Consecutive Subsequences”, “LeetCode 3299 solution”, “DP on values”, “Java DP interview”, “Python coding interview”, “C++ LeetCode solutions”, “software engineering interview tips”.
* **Social Media Hook** – “Cracked LeetCode 3299 en O(n) – aquí está el truco que hizo que los reclutadores asienten!”
* **Call‐to‐Action** – Invitar a los lectores a dejar un comentario con sus propias soluciones o pedir una sesión de programación de pares.

-...

## Final Thought

El *Good* es el DP limpio que funciona en tiempo lineal.
El *Bad* es la tentación de fuerza bruta o de pensar demasiado en la definición de subsequencia.
El *Ugly* es el sutil manejo fuera de uno y modulo que viaja hasta ingenieros experimentados.

Dominar este problema muestra que puede **extraer un problema aparentemente combinatorio en una simple recurrencia** – un personal de habilidad busca en cada ingeniero de software senior. 🚀

-...

¡Feliz codificación y buena suerte en tu próxima entrevista!