-...
Título: LeetCode 1477. Encontrar dos sub-arrayos no superpuestos cada uno con sumo objetivo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1477 – Find Two Non-overlapping Sub-arrays Every With Target Sum
** Complejidad en el tiempo**
** Complejidad del espacio:*

A continuación encontrará soluciones limpias y preparadas para la producción en **Java**, **Python**, y **C+** que resuelven LeetCode 1477 en tiempo lineal.
Después del código proporcionamos un blog completo optimizado SEO que explica el problema, los obstáculos y el elegante truco O(n) que hace de esto una pregunta de entrevista *must‐know*.

-...

## 1down Java Solution

``java
importar java.util*;

Clase Solución {

int public int minSumOfLengths(int[] arr, int target) {}
int n = arr.length;
// minLenFromLeft[i] – sub-array más corto terminando en o antes
int[] left = new int[n];
// minLenFromRight[i] – sub-array más corto empezando en o después de i
int[] right = new int[n];

// -------- Primer paso : izquierda → derecha ----------
int minLen = Integer.MAX_VALUE;
int start = 0, sum = 0;
para (int end = 0; end יnt; end++) {}
sum += arr[end];
mientras que (sumo objetivo de título) {
sum -= arr[start++];
}
si (sum == target) {
minLen = Math.min(minLen, end - start + 1);
}
izquierda[end] = minLen; // almacenar la mejor longitud hasta `end`
}

// -------- Segundo paso : derecha → izquierda --------
minLen = Integer.MAX_VALUE;
start = n - 1;
suma = 0;
para (fino único = n - 1; fin 0; end--) {}
sum += arr[end];
mientras que (sumo objetivo de título) {
sum -= arrr[start...];
}
si (sum == target) {
minLen = Math.min(minLen, start - end + 1);
}
right[end] = minLen; // almacenar la mejor longitud de `end `
}

// -------- Combinar...
int best = Integer.MAX_VALUE;
para (int i = 0; i)
si (izquierda) ■ Integer.MAX_VALUE " recto[i + 1]
mejor = Math.min(best, left[i] + right[i + 1]);
}
}

devolver mejor == Integer. ¿MaX_VALUE? -1 : mejor;
}
}
`` `

■ **Por qué funciona* *
* Ventana deslizante encuentra cada sub-array cuya suma equivale a `target` en O(n).
* Mantenemos la longitud más corta que termina (o comienza) en cada índice.
* Los dos arrays `izquierda' y `derecha' codifican el sub-array “mejor” para el lado izquierdo y el lado derecho de cualquier punto de división.
* El bucle final simplemente intenta cada punto de división – el par óptimo se encuentra en O(n).

-...

## 2down⃣ Python Solution

``python
de la importación Lista

Solución de clase:
def minSumOfLengths(self, arr: List[int], target: int) - título int:
n = len(arr)

# left[i] = longitud más corta de sub-array terminando a o antes de
* n
# right[i] = longitud más corta de sub-array comenzando a o después de i
* n

# ---- left → right ----
S = 0
l = 0
min_len = flotante('inf')
para r en rango(n):
s += arr[r]
mientras que el objetivo de .
s -= arr[l]
l += 1
si s == objetivo:
min_len = min(min_len, r - l + 1)
izquierda[r] = min_len

# ---- right → left ----
S = 0
r = n - 1
min_len = flotante('inf')
para l en rango(n - 1, -1, -1):
s += arr[l]
mientras que el objetivo de .
s -= arr[r]
r)= 1
si s == objetivo:
min_len = min(min_len, r - l + 1)
derecha[l] = min_len

#... combinar...
as = flotante('inf')
para i en rango(n - 1):
si la izquierda[i] se hacía flotar('inf') y la derecha[i + 1]
as = min(ans, left[i] + right[i + 1]

retorno -1 si ans == flotante('inf')
`` `

-...

## 3down C C++ Solución

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minSumOfLengths(vector identificadoint tendrían que hacerlo, int target) {
int n = arr.size();
vector implicado izquierdo(n, INT_MAX), derecha(n, INT_MAX);

// izquierda → derecha
int l = 0, sum = 0, best = INT_MAX;
para (int r = 0; r) {}
suma += arr[r];
, mientras que (sumir el objetivo principal) suma -= arr[l++];
si (sum == target) mejor = min(best, r - l + 1);
izquierda [r] = mejor;
}

// derecha → izquierda
int r = n - 1, best2 = INT_MAX;
suma = 0;
para (int l2 = n - 1; l2 0; --l2) {
suma += arr[l2];
mientras que (sumir el objetivo principal) suma -= arr[r];
si (sum == target) best2 = min(best2, r - l2 + 1);
right[l2] = best2;
}

// combinar
int ans = INT_MAX;
para (int i = 0; i)
si (izquierda) INT_MAX " derecha[i + 1]!= INT_MAX)
ans = min(ans, left[i] + right[i + 1]);

volver ans == INT_MAX ? -1 : ans;
}
};
`` `

-...

# 📚 Blog Article – *The Good, The Bad, The Ugly*
**Título**: *Mastering LeetCode 1477: Find Two Non-Overlapping Sub-arrays With Target Sum – The Good, The Bad, The Ugly*

-...

## Introduction

Al entrevistar para **software-engineering** roles, LeetCode 1477 “Encontrar dos sub-arrayos no superpuestos Cada Con Suma de Destino” es un problema clásico que prueba la capacidad de un candidato para combinar ** sumas de prefijo**, ** ventanas deslizantes**, y ** programación dinamica** en un solo paso.

En este artículo:

1. **Declarar el problema** en lenguaje claro.
2. Camina por **naïve** intentos y por qué fallan.
3. Presentar la solución **optimal O(n)** con un avance claro.
4. Mostrar ** implementaciones completas** en Java, Python y C++.
5. Discuss ** comunes trampas** y consejos de entrevista.

Siéntase libre de copiar-pasar los fragmentos de código, ejecutarlos en su máquina local, y añadirlos a su cartera.

-...

## Problema Declaración (Simplificada)

Se le da un array `arr` de números enteros positivos y una suma de objetivo `t`.
Encontrar dos sub-arrayos no superpuestos* de tal manera que la suma de cada sub-array equivale a `t`.
Devuelve la longitud total *mínimo* de esas dos sub-arrayas.
Si es imposible, devuelve `-1`.

■ **Constraints**
≤ 105 `
" 1 ≤ arr[i] ≤ 103
≤ 108

-...

## 1down Las buenas – ideas intuitivas

Silencio tóxico Complejidad
Silencio--------------------------...
Silencio **Brute‐Force** (dos lazos anidados + otro lazo anidado) Silencio simple para implementar Silencio demasiado lento para 'n=105` Silencio
Silencio **Dos Pointer (ventana deslizante)** Silencio Handles números positivos agradablemente Silencio Todavía demasiado lento
Silencio **Prefix Sum + HashMap** Silencio `O(n)` Silencio Tiempo lineal Silencio Extra `O(n)` memoria, sutil manejo de índices

La parte *good* es que con **positivos enteros** podemos explotar la propiedad *monotónica* de sumas: expandir una ventana sólo aumenta la suma, disminuyendo sólo la suma. Esta es la clave para una solución lineal **2 puntos**.

-...

## 2down Los malos – saltos comunes

Por qué falla en la vida
Silencio...
Silencio **Retirar “mejor sub-array a la izquierda” como una sola variable global** Necesitamos la sub-arraya *shortest* que termina *donde* a la izquierda de un punto de división, no sólo la última. Silencio
Silencio **No propagar las mejores longitudes** Silencio Después de encontrar un sub-array terminando en `i`, debes recordar que lo mejor hasta `i' podría ser aún más corto en un índice anterior. Silencio
Silencio **Uso de dos escaneos independientes sin fusionarse** Silencio Dividir el array en dos partes y resolver cada uno de ellos de forma independiente falta de optimizaciones cruzadas. Silencio
TEN **Over-complicating with dynamic programming states** TEN El espacio estatal explota; un simple enfoque prefijo de dos pasos / suffix basta. Silencio

-...

## 3down Soluciones Ugly – Soluciones over-Engineered

Algunos candidatos agregan búsqueda binaria, árboles de segmento, o incluso `unordered_map` sobre sumas prefix para cada posible índice final.
Aunque son *técnicamente correctos*, son:

- Oído leer.
- ¿Por qué?
- **Hard to explain in an interview* *

Cuando una pregunta de entrevista permite una solución lineal y limpia, los enfoques *ugly* sólo dañarán su puntuación.

-...

Solución Optimal O(n) – Ventana deslizante + Prefijo/Suffix

#### 4.1 Overview

1. **Left → Right Pass**
* Para cada índice `i`, encontrar el sub-array más corto que termina en o antes 'i' y suma a `t`.
* Almacene esta mejor longitud en array `left[i]`.

2. *Derecho → Paso Izquierdo*
* Análogamente, para cada índice `i`, computar el sub-array más corto que comienza en o después de `i`.
* Store in array `right[i]`.

3. *Merge*
* Por cada punto de división posible " i " ( " 0 ≤ i " ), combinar " izquierda " y " derecha " .
* El mínimo de `izquierda[i] + derecha[i+1]` es la respuesta.

### 4.2 Why It Works

- La ventana ** deslizante** garantiza que comprobamos *todo* sub-array cuya suma es exactamente `target`.
- El array "izquierda" *propaga la longitud más corta vista hasta ahora, haciendo que cada punto de división sea consciente del mejor sub-array izquierdo.
- La matriz derecha hace lo mismo por el lado derecho.
- Como cada sub-array se descubre en *(n)*, y el paso de fusión es otro *(n)*, el tiempo de ejecución total es *linear*.

#### 4.3 Pseudocode

`` `
n = longitud(arr)
izquierda = array of INF[n]
right = array of INF[n]

# Paso izquierdo
suma = 0; comienzo = 0; mejor = INF
para terminar en 0.n-1:
suma += arr[end]
mientras que suma objetivo:
suma -= arr[start]; start++
si suma == objetivo:
mejor = min(best, end - start +1)
izquierda[end] = mejor

# Paso derecho
suma = 0; final = n-1; mejor = INF
para empezar en n-1..0:
suma += arr[start]
mientras que suma objetivo:
sum -= arr[end]; end--
si suma == objetivo:
mejor = min(best, end - start +1)
right[start] = best

# Merge
respuesta = INF
para mí en 0.n-2:
INF y derecha[i] i+1]
respuesta = min(respuesta, izquierda[i] + derecha[i+1])

respuesta de retorno == INF ? -1 : respuesta
`` `

-...

## 5VIEW⃣ Full Implementations

Ya presentamos el código completo en las secciones anteriores.
Siéntete libre de meterlos en tu repositorio; te recomendamos añadir ** pruebas de unidad** para los siguientes casos:

1. `arr = [1,2,1,2,1,1,1]`, `t=3` → `answer = 3` (e.g., `[1,2]` y `[2,1]`).
2. `arr = [1,1,1,1,1,1,1,1]`, `t=7` → `answer = -1` (no dos sub-arrays disjoint).
3. Caso de borde: " longitud " 1 → siempre `-1`.

-...

## 6down⃣ Interview Tips

Silencioso Cómo utilizarlo
Silencio...
Silencio **Explicar su plan primero** Silencio Esbozo “dos escaneos + combinar” antes de escribir código. Silencio
Silencio **Use un valor tonto** (INF`) para denotar “no hay sub-array encontrado todavía”. tención Evita errores fuera por uno. Silencio
Silencio **Preguntar preguntas aclaratorias** Silencio Confirme que todos los números son positivos (garantizados por limitaciones). Silencio
Silencio ** Comprobación de la complejidad del tiempo** funcionará en alrededor de 0.01 s para 'n=105` en un portátil típico. Silencio
Silencio **Discuss edge cases** Silencio Show you considered empty splits and overlapping conditions. Silencio

-...

## 7down W Wrap‐Up

LeetCode 1477 es una ilustración perfecta de cómo una estructura de datos *simple* (dos arrays) y un algoritmo *simple* (ventana deslizante) pueden resolver un problema aparentemente complejo en tiempo lineal.

**Key Takeaways**:

- Recuerde **propagate** la mejor longitud de sub-array a todos los índices.
- Un enfoque **2-pass** (prefijo + sufijo) es a menudo el más limpio.
- Mantenga el código ** legible** y **bien comentado**—eso es lo que buscan los entrevistadores.

¡Feliz codificación y buena suerte con tu próxima entrevista! 🚀

-...

## Referencias

- Problema oficial de LeetCode: https://leetcode.com/problems/find-two-non-overlapping-sub-arrays-each-with-target-sum/
- Soluciones y discusión sobre LeetCode discutir foro.
- tutorial de ventana deslizante: https://leetcode.com/articles/two-sum-ii/
- Técnica de suma de prefijo: https://leetcode.com/articles/shortest-subarray-with-sum-at-least-k/

-...

¡Feliz entrevista!

-...

*Author: [Su nombre]* – *Ingeniero de software ← Algorithm Enthusiast*
*Sígueme en GitHub / Linked Para más contenido algoritmo. *


-...

*Cuento jurado: ~1300*
*Hora de leer: ~8 minutos*
*Keywords: LeetCode, algoritmo, entrevista, ventana deslizante, suma prefijo, Java, Python, C++ *


-...

¡Disfruta!