-...
Título: LeetCode 3116. Kth Cantidad más pequeña con una combinación de denominación única -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
1. Código de Solución

A continuación encontrará tres implementaciones de producción para **LeetCode 3116 – "Kth Smallest Amount With Single Denomination Combination"**.
Los tres usan la misma idea:

1. **Inclusión–Exclusión** para contar cuántas cantidades “válidas” son ≤ X.
2. **Binary Search** sobre el espacio de respuesta.
3. Aritmética de 64 bits (Java `long`, Python `int`, C++ `long') para permanecer dentro de los límites.

■ *Por qué funciona* *
■ Cada denominación se puede utilizar infinitamente muchas veces, pero las monedas de denominaciones * diferentes* no pueden mezclarse.
■ Para un conjunto fijo de denominaciones, cada cantidad alcanzable es un múltiplo de
" lcm(S) " (menos comunes).
■ Inclusión–Exclusión nos permite contar el número de múltiplos de *cualquier* lcm evitando las intersecciones de doble contabilización.

-...

## 1.1 Java (Java 17)

``java
importar java.util*;

Solución de la clase pública {}

/** Punto de entrada principal para LeetCode. */
public long findKthSmallest(int[] coins, int k) {
int n = coins.length;
// Todos los subconjuntos no vacíos – 2^n - 1 posibilidades
Lista realizadaLong ratio lcmList = nuevo ArrayList fiel(1 iere n);

// Pre-compute lcm para cada subconjunto y recuerde su signo
para (enmascarado = 1; mascarilla)
lcm largo = 1;
para (int i = 0; i) {}
si (mask > (1 > ) 0) {
lcm = lcm(lcm, coins[i]);
}
}
// Inclusión – Signo de exclusión: + para el tamaño extraño, – incluso para el tamaño
bits int = Integer.bitCount(mask);
lcmList.add(bits % 2 == 1 ? lcm : -lcm);
}

largo bajo = 1, alto = largo.MAX_VALUE; // alto puede ser muy grande
mientras (bajo)
largo medio = bajo + (alto - bajo) / 2;
si (en medio, lcmList)
baja = media + 1; // respuesta es mayor
. ♫ ... {
alta = media; // respuesta puede ser media o menor
}
}
Retorno bajo;
}

* Cuente cuántas cantidades ≤ objetivo son representables. */
cuenta de larga duración privada (objetivo largo, Lista) {
cnt largo = 0;
para (long lcm : lcmList) {
cnt += target / lcm; // negativo lcm automáticamente subtracts
}
cnt de retorno;
}

/** Ayudantes clásicos gcd / lcm que nunca rebosan. */
gcd (long a, long b) {}
mientras (b!= 0) {
tmp largo = un % b;
a = b);
b = tmp;
}
devolver a;
}

lcm (long a, long b) {}
volver a / gcd(a, b) * b; // (a/gcd)*b nunca rebosa 64‐bit
}
}
`` `

*Por qué el código es seguro*
`a / gcd(a, b)` se realiza primero, por lo que nunca multiplicamos dos grandes números que podrían desbordarse.
El espacio de búsqueda está limitado por `Long.MAX_VALUE`; la búsqueda binaria se detiene cuando `low == high`, que está garantizada a ser la respuesta porque la función `contra(x)` es monotónica.

-...

## 1.2 Python 3

``python
de la importación de matemáticas gcd
de la importación Lista

Solución de clase:
def find KthSmallest(self, coins: List[int], k: int) - Propiedad int:
n = len(coins)
lcm_list = []

# Pre-compute lcm for every non-empty subset
para máscaras en el rango(1, 1  se hizo n):
l = 1
para i en rango(n):
si máscara " (1 " )
l = l * monedas[i] // gcd(l, coins[i])
bits = bin(mask).count('1')
lcm_list.append(l if bits % 2 == 1 else -l)

def count(x: int) - título int:
volver suma(x // l para l en lcm_list)

Lo, hola = 1, 2 ** 63 - 1 # Python int is unbounded but we cap it
mientras que lo hizo hola:
media = (lo + hola) // 2
si cuenta(mid)
lo = mitad + 1
más:
hola = media
regreso
`` `

* Notas de pitón*
* `int` es arbitrario-precisión, por lo que no nos preocupamos por el desbordamiento.
* `2**63-1` se utiliza para reflejar el límite largo de Java; el algoritmo todavía convergería si usamos un límite aún mayor.

-...

## 1.3 C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
larga búsqueda KthSmallest(vector interpretadoint instantes monedas, int k) {
int n = coins.size();
vector de larga duración lcm_list;
lcm_list.reserve(1 >

// Pre-compute lcm para cada subconjunto no vacío
para (enmascarado = 1; mascarilla)
largo l = 1;
para (int i = 0; i) {}
si (mask " (1 " ) {
l = lcm(l, (long long)coins[i]);
}
}
bits int = __ builtin_popcount(mask);
lcm_list.push_back(bits " 1 ? l : -l);
}

autoconteo = [ cl](long long x) {
largas res = 0;
para (long long l : lcm_list)
res += x / l; // negativo l resta automáticamente
restitución;
};

long lo = 1, hola = LLONG_MAX;
mientras (lo cautivado) {
largo largo medio = lo + (hi - lo) / 2;
si (cuenta(medio)) lo = medio + 1;
más hola = medio;
}
devolver lo;
}

privado:
// gcd / lcm ayudantes que evitan el desbordamiento
largo largo gcd(long long a, long long long b) {}
(b) { long t = a % b; a = b; b = t; }
devolver a;
}

largo largo lcm(long long a, long long b) {}
volver a / gcd(a, b) * b; // (a/gcd)*b seguro en 64 bits
}
};
`` `

-...

# 2. Blog Artículo – “Mastering LeetCode 3116: El Bien, el Mal y el Ugly”

■ **Keywords**: LeetCode 3116, Kth Smallest Amount, Inclusion–Exclusion, Binary Search, Algorithm Interview, Coin Problem, Coding Interview, Programming Challenges, Interview Tips

-...

## 2.1 Problema general

LeetCode 3116 – *Kth Smallest Amount With Single Denomination Combination* – te da un conjunto de denominaciones de monedas **distinct** y te pregunta:

■ *Tienes un suministro infinito de cada moneda, pero no puedes mezclar diferentes denominaciones. ¿Cuál es la cantidad **k‐th menor** que se puede hacer? *

Las limitaciones hacen de este un problema clásico “contra valor”:

* `coins.length ≤ 15` – lo suficientemente diminuto como para permitir la enumeración bit-mask.
* `coins[i] ≤ 25` – pequeños valores de moneda.
* `k ≤ 2·109` – la respuesta puede ser enorme, hasta `Long. MAX_VALUE`.

Usted tiene que producir una respuesta **exact** entero.

-...

## 2.2 Why Brute Force Fails

Un algoritmo ingenuo:

1. Generar todos los múltiplos de cada moneda hasta un enorme límite.
2. Incorpóralos.
3. Escoge el k‐th.

Incluso con un límite como `109`, generaría decenas de millones de números – demasiado lento y con mucha memoria. Además, la respuesta podría estar mucho más allá de cualquier límite simple.

Por lo tanto, necesitamos un enfoque contable más inteligente.

-...

## 2.3 The Insight: Inclusion–Exclusion + Binary Search

### 2.3.1 Inclusión–Exclusión

Para cualquier subconjunto `S` de denominaciones, cada cantidad alcanzable es un múltiplo de `lcm(S)` (menos común múltiple).
Si contamos cuántos múltiplos de `lcm(S)` son ≤ X, obtenemos `⌊X / lcm(S)⌋`.

Pero no podemos simplemente resumir todos los subconjuntos porque un número que es un número múltiple de *ambos* `lcm(A)` y `lcm(B)` sería doble-contada.
**Inclusión-Exclusión** arregla esto:

`` `
conteo(X) = gia (-1)^(Principalidad) _ ⌊X / lcm(S)
sobre todos los subconjuntos no vacíos S
`` `

El signo es ** positivo** cuando el tamaño del subconjunto es extraño, **negativo** cuando incluso.

Con `n ≤ 15`, hay en la mayoría de subconjuntos `2n−1 = 32,767` – trivial a pre-compute.

### 2.3.2 Binary Search

`contra(X)` es una función que no disminuye.
Podemos buscar binariamente el más pequeño `X` tal que `contra(X) ≥ k`.
Debido a que `k` puede ser hasta `2·109`, el espacio de búsqueda es grande, pero el log2(29) ♥ 32 iteraciones - rápido.

La clave es usar **64-bit** aritmética (`long’ / `long’) para evitar el desbordamiento.
El lcm de hasta 15 números, cada ≤ 25, encaja cómodamente en 64 bits:
`257 ≈ 6.1·109`, y el producto de los 15 es en la mayoría de `2515 ♥ 9.3·1019` – todavía se hizo `9.22·1018` (`Long.MAX_VALUE`).

-...

## 2.4 Pitfalls de Implementación (El Ugly)

Silencio Pitfall Silencio Lo que sucede Silencioso
Silencio--------------------------
* b / gcd(a, b)` puede rebosar antes de la división. TENIDO Compute `a / gcd(a, b)` primera: `lcm = (a / gcd) * b`.
Silencio ** Alto límite demasiado bajo** Silencio Si usted cap `alto' en `k * max_coin`, usted puede perder la respuesta si está arriba. Silencio Use `Long.MAX_VALUE` o `LLONG_MAX`. El algoritmo todavía converge porque sólo necesitamos monotónica, no un límite superior exacto. Silencio
Silencio **Firmativa de lcm negativo** Silencio Trastornando accidentalmente sólo lcm positivo y luego ignorando el signo conduce a la venta excesiva. tención Almacene cada lcm con su signo (±). `contra(X)` entonces utiliza `X / lcm` directamente; un lcm negativo automáticamente resta. Silencio
Silencio **Tiempo de salidas en Python** Silencio Resumiendo más de 32k lcm valores en cada iteración es fino, pero usando `2**63-1` como límite superior conduce a grandes enteros que son lentos. Mantener el límite pequeño (por ejemplo, `2**63-1`) y dejar que la entrada de Python maneje cualquier desbordamiento. Silencio

-...

## 2.5 Why the Approach is Optimal

* **Pre-computación**: Valores de 32k lcm → O(2n) ♥ 104 operaciones.
* **Counting**: `O(2n)` divisions per `count(X)`.
* **Binary Search**: 64 iteraciones × 32k divisiones ♥ 2 millones de divisiones enteros – segundo segundo en cualquier idioma.

El consumo de memoria es insignificante: almacenamos solamente la lista de lcm (~64 kB).
Por lo tanto la solución es *optimal* dadas las limitaciones.

-...

## 2.6 Common Interview Mistakes

TENIDO MÁS INVESTIGACIÓN ANTERIOR ANTERIOR Cómo evitar
Silencio----------------------------
tención Assuming k‐th value equals `k * min_coin`. Use búsqueda binaria con cuenta exacta. Silencio
TENIDO Mixing `int ' y `long ' en Java. Mantenga todo en 'long'. Compute `(a / gcd(a, b)) * b`. ←
Silencio Olvidar el signo en la inclusión – exclusión. Respuesta incorrecta para muchos casos de prueba. TENIDO Almacenar explícitamente `±lcm` para cada subconjunto. Silencio
Silencio Utilizando `int` para la búsqueda atada en C++. Silencio `count(mid)` puede desbordarse, causando un comportamiento indefinido. ← Use `LLONG_MAX` y cuidadoso cálculo lcm. Silencio

-...

## 2.7 Takeaway: Build a Counting Function, Then Search

Cuando se enfrenta a “k‐th menor” bajo restricciones que hacen imposible la enumeración, el patrón común es:

1. **Count** – Construir una función monotónica rápida `f(x)` que le dice cuántos valores ≤ x satisfacer la propiedad.
2. **Binary Search** – Encuentra el umbral donde `f(x) ≥ k`.

Esta estrategia aparece en problemas como:

* K‐th divisible number (LeetCode 1794).
* K‐th feo número (LeetCode 264).
* Valor K‐th mayor en una matriz.

LeetCode 3116 es simplemente una variante que te obliga a combinar subconjuntos * diferentes* de monedas. Dominar el patrón de inclusión-exclusión le ayudará a conquistar muchos otros puzzles “contra-por subset”.

-...

## 2.8 Interview‐Friendly Checklist

✔ ✔ Silencio Lista de verificación
Silencio.
TENIDO TENIDO ANTERIOR Uso **bit‐mask** para enumerar todos los subconjuntos (≤ 32k). Silencio
TENIDO TENIDO ANTERIOR Compute `lcm` safe: `a / gcd(a, b) * b`. ANTE
TENIDO TENIDO ANTERIOR Almacene el signo de cada subconjunto (`+` para el tamaño extraño, `-` para incluso). Silencio
TENIDO TENIDO ANTERIOR Escribe una `cuenta(x)` que itera sobre la lista pre-computada. Silencio
TENIDO TENIDO ANTERIOR búsqueda binaria sobre `[1, Long.MAX_VALUE]` (o `LLONG_MAX`). Silencio
TENIDO TENIENDO TERRITORIO Use `long`/`long ́ en todas partes en Java / C++. Silencio
TENIDO TENIDO TENIDO Persianas de prueba: `k = 1`, `k` en la parte superior, moneda única, todas las monedas. Silencio

-...

## 2.9 Pensamientos Finales

LeetCode 3116 es un maravilloso micro-challenge que te obliga a:

1. **Reconocimiento** que contar por valor es mejor que generar valores.
2. **Aplicar** Inclusión–Exclusión correctamente.
3. **Combina** la cuenta con una búsqueda de monotona.

La solución resultante es limpia, matemáticamente elegante, y funciona en micro segundos en cualquier CPU moderna. Dominar este patrón le dará una poderosa herramienta para su próxima entrevista de codificación.

¡Feliz codificación! 🚀

-...



# 3 Observaciones de clausura

*Las implementaciones Java, Python y C++ arriba están listas para sumisión en LeetCode. *
*El artículo del blog está estructurado para guiar a los lectores de la intuición a la implementación, destacando los obstáculos comunes y cómo evitarlos. *

Siéntete libre de copiar, pegar y ejecutar los fragmentos en tu IDE o en el editor LeetCode. ¡Buena suerte en tu entrevista!