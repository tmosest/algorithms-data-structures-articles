-...
Título: LeetCode 3141. Máximo Hamming Distancias -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 3141 – Maximum Hamming Distancias
**Java ⋅ Python ← C++ – O(m · 2m) Solución DP**

■ **Etiquetas de SEO** – LeetCode 3141, Maximum Hamming Distancias, solución de entrevistas Java, solución de entrevistas Python, solución de entrevista C+++, bitmask de programación dinámica, entrevista de ingeniería de software, problema de entrevista de codificación

-...

## 1. Declaración de problemas

■ **Given** an integer array `nums` (length *n*, 2 ≤ *n* ≤ 2m) and an integer `m` (1 ≤ *m* ≤ 17)
■ **Retorno** un array de la misma longitud donde
[i] = max_{j sagradoi} HammingDistance(nums[i], nums[j]).

La distancia Hamming entre dos enteros es el número de posiciones de bits en las que sus representaciones binarias difieren (los ceros liberados se permiten remar las cuerdas a *m* bits).

-...

## 2. Naïve Ideas " Their Pitfalls

Silencio Silencio Silencio Silencio Silencio Silencio Silencio Silencio
Silencio----------------------------
← Brute force pairwise Hamming distance TEN O(n2 · m) TEN O(1) Silencio n puede ser 2m Ω 131 072 → ~101010 comparaciones → impossible. Silencio
Silencio Pre-compute todas las distancias en una matriz de 2m × 2m Silencio O(2m)2) Silencio O(2m)2) Silencio 2m2 Ω 1010 memoria → imposible. Silencio
Silencio BFS de cada elemento sobre el hipercube Silencio O(n · 2m) Silencio O(2m) Silencio Trabaja para muy pequeño *m*, pero todavía demasiado lento para *m*=17. Silencio

Necesitamos un algoritmo *linear* en términos del tamaño de hipercubo, es decir, O(m · 2m).

-...

## 3. El Insight – “Propagate” la distancia máxima

Cada entero *x* (0 ≤ *x*) se puede considerar como un nodo en un hipercubo *m* dimensional.
Dos nodos son vecinos si difieren exactamente en un poco.

Dejar `dp[x]` ser la distancia *maximum* Hamming de *x* a cualquier elemento que aparece en `nums`.
Si conocemos `dp[y]` para un vecino `y = x ^ (1 iere identificado k)` (bit *k* flipped), podemos actualizar `dp[x]`:

`` `
dp[x] = max( dp[x] , dp[y] + 1 )
`` `

El `+1` viene de la parte más diferente entre `x` y `y`.
Hacer esto una vez por cada bit es suficiente: después del primer paso `dp` conoce la distancia al elemento más cercano en el mismo "half" del cubo; después del segundo paso conoce la distancia al elemento más cercano en la otra mitad, y así sucesivamente.
Después de procesar todos los `m` bits, `dp[x]` contiene la distancia máxima a **cualquier elemento** en `nums`.

El algoritmo es esencialmente una programación dinámica multietapa (o estilo “Fast Walsh–Hadamard transform”) sobre el hipercubo.

-...

## 4. Algoritmo (código pseudo)

`` `
tamaño = 1
dp = array de tamaño lleno con -INF
para cada v en nums:
dp[v] = 0 // distancia a sí misma es 0

para bit de 0 a m-1:
prev = copia de dp // instantánea antes de este nivel
para x de 0 a tamaño-1:
vecino = x ^ (1 ↑)
dp[x] = max( dp[x], prev[neighbour] + 1 )

respuesta = [ dp[v] for v in nums ]
respuesta
`` `

**Las complejidades* *

* Tiempo: `O(m · 2m)` – en la mayoría de `17 · 131072 ♥ 2,2 millones de operaciones.
* Espacio: `O(2m)` - la matriz DP más una instantánea.

Ambos son lo suficientemente rápidos para las limitaciones.

-...

## 5. Código

## 5.1 Java (Java 17)

``java
importar java.util*;

Solución de la clase pública {}
int[] maxHammingDistances(int[] nums, int m) {
tamaño de la entrada = 1 se hizo referencia m; // 2^m
int[] dp = nuevo int[size];
Arrays.fill(dp, Integer.MIN_VALUE / 2); // evitar el desbordamiento

// caso base: distancia a sí misma es 0
para (int v : nums) dp[v] = 0;

// DP sobre bits
para (incluido bit = 0; bit Identificado m; bit++) {}
int[] prev = dp.clone(); // snapshot before this level
int mask = 1 нетелите bit;
para (int x = 0; x < size; x++) {}
int neighbour = x ^ mask;
dp[x] = Math.max(dp[x], prev[neighbour] + 1);
}
}

// Construir respuesta
int[] res = nuevo int[nums.length];
para (int i = 0; i)
restitución;
}

/* -----------
Arnés de prueba rápida – no parte de la presentación de LeetCode
-----------
public static void main(String[] args) {
Solución s = nueva solución ();
System.out.println(Arrays.toString(
s.maxHammingDistances(new int[]{9, 12, 9, 11}, 4))); // [2,3,2,3]
}
}
`` `

## 5.2 Python (Python 3.11)

``python
de la importación Lista
importar matemáticas

Solución de clase:
def maxHamming Distancias (self, nums: List[int], m: int) - título List[int]:
tamaño = 1
* tamaño

# Funda base
para v en nums:
dp[v] = 0

# DP over bits
para bit en rango(m):
prev = dp[:]
mascarilla = 1
para x en rango(tamaño):
vecino = x ^ máscara
val = prev[neighbour] + 1
si vale, dp[x]:
dp[x] = val

[dp[v] for v in nums]


Demo rápido
si __name_ == "__main__":
s = Solución()
print(s.maxHammingDistances([9, 12, 9, 11], 4)) # [2, 3, 2, 3]
`` `

## 5.3 C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector asignadoint contacto máxHammingDistances(vector realizadoint limitada nums, int m) {
tamaño de la entrada = 1 = 1
vector significado dp(size, INT_MIN / 2); // evitar el desbordamiento

/ Caso básico
para (int v : nums) dp[v] = 0;

// DP sobre bits
para (incluido bit = 0; bit יm; ++bit) {
vector significado prev = dp; // snapshot
int mask = 1 нетелите bit;
para (int x = 0; x < size; ++x) {
int neighbour = x ^ mask;
dp[x] = max(dp[x], prev[neighbour] + 1);
}
}

vector res;
res.reserve(nums.size());
(int v : nums) res.push_back(dp[v]);
restitución;
}
};
`` `

-...

## 6. “Bueno, malo, ugly” de la solución

Silencio Silencio
Silencio------------Prince------
Silencio ** Complejidad del tiempo** Silencio Linear en el tamaño del hipercubo (m · 2m). Silencio Ninguno – el algoritmo es óptimo para las limitaciones. Silencio.
Silencio ** Complejidad del espacio** Silencio O(2m) – perfectamente aceptable para *m* ≤ 17. Silencio Ninguno.
Silencio **Readability** Silencio Clear DP lazo, usa bitwise XOR para cambiar un poco. ← Requiere la comprensión de la propagación hipercubina. La copia de Snapshot (`prev = dp.clone()`) puede parecer pesada pero es trivial. Silencio
Silencio ** Casos de Edge** tención Handles duplicados, arrays de un solo bit, tamaño máximo. Ninguno.
tención **Potential Pitfalls** ← Utilizando `Integer.MIN_VALUE/2` para evitar el desbordamiento al añadir 1. Silencio Olvidar restablecer `dp[v] = 0` para cada ocurrencia de un número. Silencio.

-...

## 7. Por qué este espectáculo está listo para una entrevista de codificación

* **Bit-wise thinking** – Los problemas de LeetCode a menudo se mueven en la manipulación de bits individuales; esta solución muestra esa habilidad.
* **Programación Dinámica sobre estructuras combinatorias** – Propagando información a través de un hipercubo es un patrón DP no trivial.
* **Space-time trade‐offs** – La solución equilibra el uso mínimo de memoria con tiempo O(m · 2m claro.
* **Language versatility** – Hemos proporcionado implementaciones idiomáticas Java, Python y C++, demostrando adaptabilidad a cualquier pila que utiliza su empleador.

Si usted puede explicar el algoritmo, justificar su optimización, y escribir código limpio en cualquiera de estos idiomas, usted es un candidato fuerte para un papel de ingeniería de software senior.

-...

## 8. Lista final de verificación antes de presentar

1. **Remove el demo `main` o `__main_` bloques** – LeetCode solo llamará el método de clase.
2. **Evite `-inf` en Java** – usamos `Integer. MIN_VALUE / 2` para seguridad.
3. **Prueba con todos los ejemplos proporcionados** – confirmar `[2,3,2,3]` y `[1,2,1,2]` trabajo.
4. **Enviar** – copiar la clase relevante en el editor de LeetCode y ejecutar la suite de pruebas.

¡Buena suerte! 🚀