-...
Título: LeetCode 3404. Conteo de Subsecuencias Especiales -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 3404 – Conteo de las consecuencias especiales
*Una solución completa y lista para entrevistas en Java, Python y C++ + un blog “bueno-bad-ugly”*

-...

## TL;DR

Silencio Idioma Silencio Tiempo Silenciosos Espacio ✔
Silencio--------------...
Silencio Java Silencio **O(n2)** Silencio **O(n2)** Silencio ↑
Silencio Silencio Silencio **O(n2)** Silencio **O(n2)** Silencio ↑
TENIDO C++ Silencio **O(n2)** Silencio **O(n2)** Silencio TENIENDO TERRENO

■ *Por qué esto importa* – El problema “Count Special Subsequences” es un ejercicio de entrevista perfecto que prueba su capacidad de pensar en *ratios* y *programación dinamica* sobre una subsecuencia de 4 índices. Entréguelo y se sentirá confiado en abordar una amplia gama de problemas LeetCode Medium.

-...

## Problema Recap

Dado un array `nums` de números enteros positivos (tamaño 7–1000), cuenta el número de subsecuencias de 4-index `(p, q, r, s) ` tal que

* " p " )
* " q - p " 1 " , " , " s - r " 1 " (hay al menos un elemento entre los dos índices)
* `nums[p] * nums[r] == nums[q] * nums[s] `

Devuelve el recuento total.

-...

## High-Level Insight

La condición `nums[p] * nums[r] == nums[q] * nums[s] puede ser reescrito como una ** igualdad ratio**:

`` `
nums[p] / nums[q] == nums[r] / nums[s]
`` `

Si arreglamos `q ' y `r ' , el lado izquierdo depende sólo de los índices `traducidos q ' y el lado derecho depende sólo de los índices `` ' .
Podemos pre-cuentar todas las proporciones posibles para los pares “derecha” (r, s)” y luego, para cada posible “p”, añadir las ratios coincidentes del lado izquierdo.

Esto produce una solución **O(n2)**:
* 2 bucles anidados para construir el mapa del lado derecho
* 2 bucles anidados para escanear el lado izquierdo y acumular la respuesta

-...

## Edge‐ Caso " Precisión " Pitfall

Utilizar números de punto flotante para ratios puede introducir pequeños errores de redondeo cuando el numerador y el denominador son grandes.
Una aplicación robusta utiliza una fracción **reducida** ( " gcd(numer, denom) " ) como clave.
(Por el bien de la brevedad en este artículo, vamos a mostrar la versión de Java de doble base – pasa todas las pruebas de LeetCode, pero si quieres código a prueba de balas utiliza el enfoque de la fracción reducida.)

-...

## Code Walk‐through (Java)

``java
importar java.util*;

Solución de la clase pública {}
public long numberOfSubsequences(int[] nums) {
int n = nums.length;
respuesta larga = 0;
// Mapa obtenidosratio, contando confianza para pares (r, s) donde r ≤ q + 1
Mapa seleccionadoDoble, Long√≥ rightRatioCount = nuevo HashMap correspondió();

// Iterate r desde n-3 hasta 4 (inclusive)
para (inc. r = n - 3; r
// Construir el mapa para todos s 1
para (int s = r + 2; s
doble ratio = nums[r] / (doble) nums[s];
rightRatioCount.merge(ratio, 1L, Long::sum);
}

int q = r - 2;
// Para cada p posible se hizo q - 1, añadir conteos coincidentes
para (int p = 0; p < q - 1; p+) {
doble ratio = nums[q] / (doble) nums[p];
respuesta += rightRatioCount.getOrDefault(ratio, 0L);
}
}
respuesta de retorno;
}
}
`` `

### Puntos clave

TEN TERRITORIO ANTERIOR ANTERIOR
Silencio--------------------
Silencio Construir `rightRatioCount` Silencio Contar todos los pares válidos `(r, s)' para la actual `q` Silencio O(n) por `r`
Escáner izquierdo lado izquierdo (`p`) Silencio Sum coincide con el lado derecho Silencio O(n) por `q` Silencio
Silencio general Silencio Dos bucles anidados sobre `r ' y `q`  durable **O(n2)** tiempo ←

-...

## Python Implementation

``python
de las colecciones importadas por defecto
de la importación de matemáticas gcd

Solución de clase:
def numberOfSubsequences(self, nums: list[int] int:
n = len(nums)
ans = 0
# Use la fracción reducida como clave para evitar errores flotantes
derecho = defaultdict(int)

para r en rango(n - 3, 3, -1):
para s en rango(r + 2, n):
g = gcd(nums[r], nums[s])
llave = (nums[r] // g, nums[s] // g) # (num, den)
derecha[key] += 1

q = r - 2
para p en rango(q - 1):
g = gcd(nums[q], nums[p])
llave = (nums[q] // g, nums[p] // g)
ans += right.get(key, 0)

Retorno
`` `

■ ¿Por qué la fracción reducida? #
■ Cada proporción es únicamente representada por un par `(num/g, den/g)` donde `g = gcd(num, den)`. No hay pérdida de precisión flotante, y las apariencias son O(1).

-...

## C++ Aplicación

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
long numberOfSubsequences(vector fielint implicados nums) {
int n = nums.size();
ans largos = 0;
unordered_map detectado largo, largo largo derecho del usuario; // clave = num

auto makeKey = [](int num, int den) - largo
largo largo a = num, b = den;
retorno (a Генте 32) ^ b; // 32‐bit embalaje
};

para (int r = n - 3; r 4; --r) {
para (int s = r + 2; s)
int g = std::gcd(nums[r], nums[s]);
tecla larga largo = hacer Key(nums[r] / g, nums[s] / g);
++right[key];
}

int q = r - 2;
para (int p = 0; p < q - 1; ++p) {
int g = std::gcd(nums[q], nums[p]);
tecla larga largo = hacer Key(nums[q] / g, nums[p] / g);
auto = derecha.find(key);
(it != right.end()) ans += it- Confsegundo;
}
}
devolver los ans;
}
};
`` `

■ **Packing trick** – La clave es un entero de 64 bits que concatena el numerador reducido y el denominador. Funciona porque `nums[i] <= 1000` → 10 bits cada uno, muy por debajo de 32.

-...

## Good, Bad, Ugly - Qué aprender

TENIDO ANTERIOR ANTERIOR ANTERIOR ❌ Qué hay que ver para TEN 😱 Ugly Traps ANTE
Silencio----------------------------------------------------...
Silencio **Bueno** Silencio • Una reducción elegante a una relación de igualdad realizadabr confianza• O(n2) es óptima para n ≤ 1000 requeridobr título• Usa sólo memoria O(n2) Silencio Silencio
Silencio **Bad** Silencio • Las proporciones de punto flotante pueden fallar en los casos de borde (por ejemplo, 500 / 499) Silencio • Comparación de la igualdad doble es frágil – use claves basadas en gcd TEN ANTE
• Olvídate de la restricción de “al menos un elemento entre índices” → por cada uno de los errores obtenidosbr título• Incorrect loop bounds (off by one) leading to out‐of-range errors obtenidosbr confianza• Usar `Map madeDouble,Long titulado` en Java sin `merge` adecuado conduce a `NullPointerException` Silencio

■ **Takeaway** – Siempre validar los rangos de bucle cuidadosamente. El requisito de “gap” adicional del problema significa que debe comenzar `r ' en `n-3 ' , no `n-2 ' , y `q ' en `r-2 ' , etc.

-...

## SEO‐Optimized Blog Headline & Meta

*Título*
“Master LeetCode 3404 – Conteo de las consecuencias especiales (Java, Python, C++ Solutions)”

**Meta Descripción:**
Aprende a resolver LeetCode 3404 “Count Special Subsequences” en O(n2) tiempo. Lea las implementaciones completas Java, Python y C++, entienda el truco de relación y prepárese para entrevistas.

**Keywords:**
`Count Special Subsequences`, `LeetCode 3404`, `Java solution`, `Python solution`, `C++ solution`, `DP ratio`, `interview question`, `algorithm analysis`, `O(n^2)`

-...

## Pensamientos finales

* El DP basado en la relación es el corazón de este problema.
* El truco 'gcd' elimina las preocupaciones de precisión flotantes y hace que su solución a prueba de balas.
* La complejidad del tiempo es **bien dentro de las limitaciones de LeetCode**, y el uso del espacio es modesto.

**Listo para tu próxima entrevista? #
Practique este problema, lo implemente en su idioma de elección, y esté preparado para explicar la racionalidad y los obstáculos durante una entrevista de codificación. ¡Buena suerte! 🚀