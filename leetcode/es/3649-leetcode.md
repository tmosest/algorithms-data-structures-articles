-...
Título: LeetCode 3649. Número de pares perfectos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 3649 – Número de pares perfectos
*Medium** – `O(n log n)` time, `O(n)` espacio

■ *Problema*
■ Se le da un array entero `nums`.
■ Un par de índices " i, j) " (con " i " ) es **perfecto**, con
" a = nums[i] " y " b = nums[j] `
" `
не min( vuestra vida - b vuestra vida,  vuestra intimidad + b vuestra intimidad)
√Max( vuestra vida - b vuestra vida,  vuestra vida + b vuestra vida) √Max( vuestra vida,  vuestra intimidad)
" `
■ Devuelve el número de pares perfectos distintos.

■ *Examples*
■ *`nums = [0,1,2,3]` → `2` parejas perfectas*
■ *`nums = [-3,2,-1,4]` → `4` parejas perfectas*
*`nums = [1,10,100,1000]` → `0` parejas perfectas*

-...

### 🚀 TL;DR – Las matemáticas detrás de la solución

Si sólo observamos los valores *absoluto* `x = Silencioa eterna` y `y = Silenciob habit` y los clasificamos de tal manera que `x ≤ y`, las dos desigualdades por encima de colapsar a una sola condición de rango:

`` `
(x + 1) / 2 ≤ y ≤ 2 * x (1)
`` `

Así que un par es perfecto **iff** el valor absoluto más grande se encuentra dentro de este intervalo.

Por lo tanto el algoritmo es:

1. Convertir cada elemento en su valor absoluto.
2. Clasificar la lista.
3. Para cada elemento " x " (en el índice " i " ) cuentan cuántos elementos subsiguientes " sí " satisfacen (1) utilizando la búsqueda binaria.
4. Sum cuenta – esa es la respuesta.

El truco es que la búsqueda binaria nos da el número de valores 'y' en el rango deseado en el tiempo `O(log n)`.
Complejidad general: **O(n log n)**.

-...

## 📚 Full Solutions

A continuación se presentan implementaciones limpias y de producción en **Java**, **Python**, y **C+**.
Los tres usan la misma lógica descrita anteriormente.

-...

## Java

``java
importa java.util. Arrays;

Solución de la clase pública {}
public long perfectPairs(int[] nums) {
int n = nums.length;
long[] abs = new long[n];
para (int i = 0; i)
abs[i] = Math.abs(long) nums[i]); // long to avoid overflow
}

Arrays.sort(abs);

respuesta larga = 0;
para (int i = 0; i)
x largo = abs[i];
larga izquierda = (x + 1) / 2; // ceil(x+1)/2)
derecho largo = 2 * x;

/ // índices de primer izquierda y primera derecha
int lo = inferiorBound(abs, left, i + 1, n);
int hi = upperBound(abs, right, i + 1, n);

respuesta += (long) (hi - lo);
}
respuesta de retorno;
}

// primer índice en [start, end) con arrr[idx] >= objetivo
int private int lowerBound(long[] arr, long target, int start, int end) {
int l = start, r = end;
mientras que (l
int m = (l + r) 1;
si (arr[m] cautivo) l = m + 1;
r = m;
}
retorno l;
}

// primer índice en [start, end) con arrr[idx]
int privado superiorBound(long[] arr, long target, int start, int end) {
int l = start, r = end;
mientras que (l
int m = (l + r) 1;
si (arr[m] ]= target) l = m + 1;
r = m;
}
retorno l;
}
}
`` `

**Por qué esto es bueno para las entrevistas* *

TENIDO VALORACIÓN ANTERIOR Por qué importa
Silencio...
TENIDO `long` en todas partes TENENCIA Evita el desbordamiento accidental al computar `2*x` Silencio
← Ayudantes de investigación binaria dedicada Silencio Mantiene el loop central concise " auto-explicativo
← O-notación en comentarios Silencio le muestra *por qué* cada paso es eficiente Silencio

-...

## Python

``python
importador bisect

Solución de clase:
def perfectPairs(self, nums: list[int] int:
# 1. Valores absolutos + clasificación
abs_vals = ordenados(abs(x) por x en nums)

n = len(abs_vals)
ans = 0

para i, x en enumerado(abs_vals):
izquierda = (x + 1) // 2 # ceil(x+1)/2)
derecho = 2 * x

# bisect_left/right work on the whole list,
Así que cortamos la vista que nos importa.
lo = bisect.bisect_left(abs_vals, left, i + 1, n)
hola = bisect.bisect_right(abs_vals, right, i + 1, n)

ans += hola - lo

Retorno
`` `

El módulo «bisecto» de Python es un envoltorio delgado alrededor de la investigación binaria de C, dando el mismo rendimiento «O(n log n).

-...

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
largo tiempo perfectoPairs(vector fielmente unidos nums) {
int n = nums.size();
vector llevado a cabo largo plazo abstenVals(n);
para (int i = 0; i)
absVals[i] = llabs(long long)nums[i]); // llabs - confianza long long

(absVals.begin(), absVals.end());

ans largos = 0;
para (int i = 0; i) {}
largo largo x = absVals[i];
larga izquierda = (x + 1) / 2; // ceil
larga derecha = 2 * x;

auto lo = lower_bound(absVals.begin() + i + 1, absVals.end(), left);
auto hola = upper_bound(absVals.begin() + i + 1, absVals.end(), right);
ans += hola - lo;
}
devolver los ans;
}
};
`` `

-...

## 📈 Complexity Analysis

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
TENIDO Convertirse en abs TENIDO `O(n)` Silencio
Silencio Ordenanza sobre la vida `O(n log n)` Silencio `O(1)` extra (en el lugar)
tención binaria-búsqueda para cada `x` Silencioso `O(n log n)`
Silencio **Total** Silencio** Silencio

El algoritmo escala cómodamente hasta las limitaciones máximas (`n = 100.000`, `resistentes[i] permanecen ≤ 10^9`).

-...

Qué entrevistadores Care About

¦ Subtítulos Lo que el entrevistador busca para la vida Cómo la solución Excels / Falls Short TEN
Silencio--------------------
Silencio **Bien** Silencio * Claridad*, *tiempo-optimidad*, *prueba el concepto* Silencio La simplificación de matemáticas (1) es elegante; la búsqueda binaria mantiene el código limpio. Silencio
Silencio **Bad** Silencioso *Mantenimiento de persianas* Silencio Los valores Zero son correctamente contados – un caso de esquina sutil. Silencio
Silencio **Ugly** Silencio *Overflow pitfalls* Silencio Multiplying `x` by `2` podría desbordar una entrada de 32 bits, por lo que utilizamos `long / long`. En Java el reparto a 'long' es esencial. Silencio

*Entrevista de claves*

1. **Siempre busque una reducción** – convertir dos desigualdades en un solo rango es un truco común de LeetCode.
2. **Binary search on a classified array** le da un *count* en tiempo logarítmico – una poderosa herramienta para las consultas de gama.
3. ** Tenga cuidado con el desbordamiento** – cuando se multiplica hasta `1e9`, utilice tipos de 64 bits.

-...

## 📌 TL;DR for Your Resume / Interview

*“Resolví LeetCode 3649 en Java/Python/C++ con un algoritmo de `O(n log n)` que transforma el problema en una simple consulta de rango en valores absolutos ordenados, aprovechando la búsqueda binaria para contar eficientemente.”*

- Mention `ceil(x+1)/2)` and `2*x` as the critical bounds.
- Búsqueda binaria de alto nivel (`lower_bound` / `upper_bound` / `bisect_left` / `bisect_right`).
- Emphasize *time* y *space* complejidad.

-...

¿Quieres practicar más?

Silencio Idioma Silencio Enlace al Código Completo (GitHub Gist)
Silencio...
TEN Java TENEDIDOS: https://gist.github.com/yourusername/abc123 Silencio
TEN Python ANTERITO ANTERIEDICIA http://gist.github.com/yourusername/def456 Silencio
TENIDO C++ TENIDO ANTERIED http://gist.github.com/yourusername/ghi789 Silencio

Siéntete libre de clonar, realizar pruebas y ajustar la solución a tu estilo.

¡Feliz codificación y buena suerte rompiendo esa entrevista de LeetCode! 🚀

-...

■ **Keywords** – LeetCode Número de pares perfectos, LeetCode 3649, algoritmo de par perfecto, solución de búsqueda binaria de Java, solución de bisecto Python, solución C++ inferior_bound, complejidad de tiempo, prep de entrevista.