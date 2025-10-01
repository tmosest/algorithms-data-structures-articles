-...
Título: LeetCode 354. Ruso Doll Envelopes -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Mastering LeetCode 354 – “Russian Doll Envelopes”

Silencio Idioma Silencio Código Silencio
Silencio...
Silencio **Java** Silencioso [Aplicación de Java] (#java-implementation)
Silencio **Python** Silencio [Python implementation] (#python-implementation) Silencio
Silencio **C+** Silencio [C+++](#c-implementation)

■ ¿Por qué leer esto? * *
■ Si se está preparando para una entrevista de ingeniería de software, “Russian Doll Envelopes” es un problema clásico de nivel duro que prueba la clasificación de trucos, programación dinámica y búsqueda binaria.
■ Este post le da una solución **completa, lista para la producción** en Java, Python y C++, además de una profunda inmersión en el *bueno, el malo, y el feo* de resolverlo.

-...

# 🧩 Problem Overview

**LeetCode 354 – Ruso Doll Envelopes**

■ Se le da una lista de sobres donde `envelopes[i] = [wi, hola]`.
■ Un sobre se puede colocar dentro de otro *iff* **ambos** su anchura *y* altura son estrictamente más pequeñas.
■ Devuelve el número máximo de sobres que puedes anidar.

*Ejemplo*
[[5,4],[6,4],[6,7],[2,3]] → **3** (`[2,3] → [5,4] → [6,7]`)

**Constraints* *

- `1 ≤ sobres.length ≤ 105 `
- `1 ≤ wi, hola ≤ 105 `

-...

# ❌ The Good, the Bad, and the Ugly #

Lo que es bueno para la vida Lo que es malo Qué es Ugly
Silencio--------------------------------------------------------------
Silencio **Aprobación** Silencio Reducir a la Subsequencia de Incremento más largo (LIS) → `O(n log n)` Silencio Naïve DP (`O(n2)`) falla en 105 entradas latitud Olvidar el truco *height-descending* para los anchos iguales → respuesta incorrecta
Silencio **Sorting** Silencio Ordenar por ancho asc, alto desc Silencio Ordenar por ambos asc puede llevar a los sobres de la misma anchura que se tratan incorrectamente ← Ordenar errores causa TLE o WA si no es cuidadoso tención
Silencio **Binary Search** Silencio Reuse `Arrays.binarySearch` o costumbre de bajo límite Silencio Mis‐handling índices negativos conduce a fuera de límites ← Implementar su propia búsqueda binaria incorrectamente (media sobreflujo) ←
Silencio **Espacio** Silencio O(n) para DP array Silencio Memoria adicional para arrays de copia Silencio No liberando la memoria en grandes entradas
Silencio **Readability** Silencio Clear helper for LIS ← Responsabilidades mixtas en una sola función ← Lambdas inlines o clases anónimas

-...

# The Optimal Solution: `O(n log n)` Enfoque

1. **Envelopes de la tierra**
- Width **ascending**.
- Si los anchos son iguales, clase de altura **descendientes**.
- ¿Por qué descender?
- Envelopes con el mismo ancho no puede anidar.
- Al poner el más alto primero, evitamos contarlo dos veces en LIS.

2. **Extract Heights**
Después de ordenar, tenemos una secuencia de alturas donde el ancho de cada sobre ya está aumentando.

3. **Compute LIS on Heights* *
- Usar un método clásico de corte de paciencia (búsqueda binaria en un array de 'dp').
- `dp[i]` almacena la cola más pequeña posible de una subsequencia creciente de la longitud `i+1`.
- La longitud de la subsecuencia creciente más larga es la respuesta.

¿Por qué LIS?
■ Después de ordenar, cualquier secuencia anidada válida debe tener alturas estrictamente crecientes. Por lo tanto, el problema se reduce a encontrar la subsequencia creciente más larga de las alturas.

-...

Detalles de la Implementación

A continuación encontrará implementaciones limpias, listas para copiar para **Java, Python y C+**.
Los tres usan el mismo núcleo algoritmo: ordenar + LIS con búsqueda binaria.

-...

## 📌 Java Implementation

``java
importa java.util. Arrays;
importa java.util. Comparador;

Solución de la clase pública {}

// Ayudante: Aumento más largo Subsequence mediante búsqueda binaria
longitud de entrada privada OfLIS(int[] nums) {
int[] dp = nuevo int[nums.length];
int len = 0;

para (int num : nums) {
int i = Arrays.binarySearch(dp, 0, len, num);
i = i + 1); // punto de inserción
dp[i] = num;
si (i == len) len++;
}
Len de retorno;
}

int public maxEnvelopes(int[][] sobres) {}
// 1Ω⃣ Ordenar por ancho asc, desc de altura para anchos iguales
Arrays.sort(envelopes, new Comparator madeint[] {}
@Override
int compare(int[] a, int[] b) {
si (a[0] == b[0]) retorno b[1] - a[1]; // altura descendiendo
volver a [0] - b[0]; // ancho ascendente
}
});

// 2Ω⃣ Alturas de extracción
int[] heights = nuevo int[envelopes.length];
para (int i = 0; i) se realizaron sobres.length; i++) {
alturas[i] = sobres[i][1];
}

// 3Ω⃣ Ejecutar LIS en alturas
longitud de retornoOfLIS(alturas);
}
}
`` `

**Las complejidades* *

- Tiempo: `O(n log n)` (sorting + LIS)
- Espacio: `O(n)` ( matriz de altura + DP)

-...

## 📌 Python Implementation

``python
de la importación de bisect_left
de la importación Lista

Solución de clase:
def maxEnvelopes(self, sobres: List[List[int]) - Conf int:
# 1 Ordenar: ancho asc, desc de altura
sobres.sort(key=lambda x: (x[0], -x[1]))

# 2⃣ Alturas de extracción
alturas = [h para _, h en sobres]

# 3️ LIS via patient sorting
dp = [] # dp[i] = cola más pequeña de la longitud i+ 1
para h en alturas:
idx = bisect_left(dp, h)
si idx == len(dp):
dp.append(h)
más:
dp[idx] = h
len(dp)
`` `

**Las complejidades* *

- Tiempo: `O(n log n) `
- Espacio: `O(n)`

-...

## 📌 C++ Implementation

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxEnvelopes(vector seleccionadovector seleccionado) {}
// 1Ω⃣ Ordenar: ancho asc, alto desc
kind(envelopes.begin(), sobres.end(),
[](cont auto cho a, const auto golpe b) {
si (a[0] == b[0]) devuelve un[1]
volver a [0] ANTEB[0]; // ancho asc
});

// 2Ω⃣ Alturas de extracción
vector alturas;
heights.reserve(envelopes.size());
para (auto golpe e : sobres) alturas.push_back(e[1]);

// 3ΩIS LIS utilizando bajo_bound
vector asignadoint título dp; // dp[i] = cola más pequeña de longitud i+ 1
para (int h : alturas) {}
auto = inferior_bound(dp.begin(), dp.end(), h);
dp.push_back(h);
*it = h;
}
devolver estática_cast seleccionado(dp.size());
}
};
`` `

**Las complejidades* *

- Tiempo: `O(n log n) `
- Espacio: `O(n)`

-...

# 🔍 Pitfalls comunes > Cómo evitarlos

Silencio Pitfall Silencio Por qué sucede 
Silencio...
Silencio **Sorting por altura ascendiendo** por igual anchos TENIDO Resultados en una cadena de sobres con la misma anchura, que viola la estricta regla de “conejo” TENIDO altura **descendiente** cuando los anchos son iguales TEN
Silencio **Using `Arrays.binarySearch` incorrectly** (Java) Los índices negativos deben ser volteados Silencioso `i = -(i + 1);` Silencio
Silencio **Desbordamiento de la búsqueda interna** (`mid = l + (r-l)/2`) Silencio Con rangos `int` hasta `105`, el desbordamiento no es un problema, pero para el uso de la seguridad la forma segura ¦
Silencio **O(n2) DP on 105 input** Silencio TLE, la memoria soplado
Silencio **Off‐by-one en la implementación de LIS** ← Longitud de subsequencia Wrong Silencio de punto de inserción doble-ver

-...

# 📈 Performance Analysis

← Algorithm ← Tiempo Silencioso
Silencio--------------------------
Silencio **Naïve DP** (`O(n2)`) Silencio ~5 × 1010 operaciones (1052) Silencio `O(n)` Silencio No es factible
Silencio ** Ordenación + LIS** (`O(n log n)`) Silencio ~106–107 operaciones Silencioso `O(n)` Silencio Trabaja cómodamente bajo 1 segundo límite de tiempo
Silencio **Optimized DP with Binary Search** Silencio Igual que antes La única diferencia es la claridad de la aplicación

**Por qué `O(n log n)` pasa fácilmente* *

- Clasificación de 100 000 elementos ♥ 100 000 × log2(100 000) ♥ 1.7 × 106 comparaciones.
- búsqueda binaria de LIS: otra Ω 1.7 × 106 operaciones.
- Total 4 × 106 operaciones primitivas → ~0.01–0.02 s en jueces modernos.

-...

Entrevista a Puntos de conversación listos

1. **Explicar la analogía de la muñeca rusa**: secuencias anidadas ↔ estrictamente aumento de pares.
2. **Por qué la clasificación es necesaria**: reduce la comparación de 2 dimensiones a LIS 1-dimensional.
3. **El truco de alto-descendente**: maneja los anchos iguales correctamente.
4. **Detalle el método de clasificación de la paciencia**: `dp` array, búsqueda binaria, `lower_bound`.
5. **La complejidad**: mostrar grande O y por qué cumple con las limitaciones.
6. ** Casos de edge**: sobre único, todos sobres iguales, entrada sin surtido.
7. **Posibles extensiones**: si se permite “≥” en lugar de “propiedad” , utilizarías `bisect_right`.

■ *Consejo*: Mantenga la explicación sucinta pero resalta el truco inteligente (altura-descendiente). Eso es lo que los entrevistadores aman.

-...

# 🎯 Summary

- ** Objetivo**: Max envoltorios anidados → LIS en alturas después de la clasificación inteligente.
- ** Algorithm**: `O(n log n)` (sort + clasificación de la paciencia).
- **Implementaciones**: Java, Python, C++ – lista para pruebas de codificación o entrevista.
- Errores comunes**: dirección de clasificación incorrecta, DP ingenuo, búsqueda binaria mal manejada.

Al dominar este problema, usted estará equipado para abordar ** cualquier problema que pueda ser reducido a LIS**, y tendrá una gran historia para su próxima entrevista de codificación.

Feliz codificación, y buena suerte en su viaje de entrevista! 🚀

-...

*No dude en dejar las preguntas en los comentarios o compartir sus propias variaciones de la solución. *