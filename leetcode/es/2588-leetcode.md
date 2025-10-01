-...
Título: LeetCode 2588. Cuenta el número de hermosas subarrays -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código de Solución (Java, Python & C++)

``java
/* Java – LeetCode 2588: Cuenta el número de hermosas subarrays */
/* Hora : O(n) Espacio: O(n) */
Clase Solución {
público largo hermoso Subarrays(int[] nums) {
// mapa de frecuencia de los valores de prefijo XOR
HashMap Haga clic en Integer, Integer frecuentementeq = nuevo HashMap incorrecto();
freq.put(0, 1); // prefijo vacío tiene XOR = 0

ans largas = 0;
int pref = 0;
para (int x : nums) {
pref ^= x; // actual prefijo XOR
ans += freq.getOrDefault(pref, 0); // todos los prefijos anteriores con la misma forma XOR una hermosa subarray
freq.put(pref, freq.getOrDefault(pref, 0) + 1);
}
devolver los ans;
}
}
`` `

``python
# Python – LeetCode 2588: Cuenta el número de hermosas subarrayas
# Hora : O(n) Espacio : O(n)
de las importaciones de colecciones Contrato

Solución de clase:
def hermosa Subarrays(self, nums: list[int]) - int:
freq = Counter({0: 1}) # prefijo XOR 0 ocurre una vez (prefijo vacío)
pref = ans = 0
para x en nums:
pref ^= x
ans += freq[pref]
freq[pref] += 1
Retorno
`` `

``cpp
// C++ – LeetCode 2588: Cuenta el número de hermosas subarrayas
// Hora : O(n) Espacio : O(n)
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
largo largo largo hermoso Subarrays(vector obtenidosint implicados nums) {
unordered_map madeint,int confianza freq{0,1};
ans largos = 0;
int pref = 0;
para (int x : nums) {
pref ^= x;
ans += freq[pref];
++freq[pref];
}
devolver los ans;
}
};
`` `

Las tres implementaciones comparten la misma idea: mantener un prefijo‐ Mapa XOR y cuenta cuántas veces ha aparecido el mismo prefijo XOR. Cada par de XORs de prefijo igual define un subarray cuyo XOR es 0, es decir, un subarray ** hermoso**.



----------------------------------------------------

## 2. Blog Artículo – “El Bien, el Mal, y el Ugly of Beautiful Subarrays”

### 2.1 Título & Meta Descripción (SEO)

- **Título:** "Hermosos Subarrayos: Una profunda cueva en LeetCode 2588 – El Bien, El Mal El Mal”
- **Meta Descripción:** “Aprenda a resolver LeetCode 2588 con un prefijo limpio” Algoritmo XOR. Obtener código en Java, Python, C++, además de consejos de estilo entrevista para aterrizar su próximo trabajo. ”

-...

#### 2.2 Introduction

¿Alguna vez has mirado a un problema de LeetCode que se ve engañosamente simple pero resulta ser una pregunta *trick*?
LeetCode **2588 – Cuenta el número de hermosas subarrays** es uno de esos rompecabezas. En la superficie se trata de manipulación de bits y subtracciones pares, pero la matemática subyacente es elegantemente capturada por la operación XOR.

En este artículo diseccionaremos el problema, caminaremos a través de una solución limpia, lista para la producción, y resaltaremos:

Silencio Qué aprender ← Por qué importa
Silencio...
Silencio **Bien** – La visión de “aha” que *beautiful* Alternativa *XOR = 0* Silencio convierte un bucle cuadrático en tiempo lineal
Silencio **Bad** – Problemas comunes (off-by‐one, mapa incorrecto, desbordamiento) Silencio Evita la entrevista errores
Silencio **Evidentemente** – Casos de borde oculto (todos ceros, gran entrada) Silencio muestra la robustez de una solución del mundo real

-...

### 2.3 Declaración de problemas (versión corta)

■ **Given** un array `nums` de longitud `n` (`1 ≤ n ≤ 105`) donde cada elemento es `0 ≤ nums[i] ≤ 106`,
■ **Cuente** el número de subarrays contiguos que pueden reducirse a todos los ceros seleccionando repetidamente dos índices con un conjunto común de bits `k ' y restando `2k ' de ambos.

■ Los submarinos que ya son todos los ceros cuentan como hermosos.

-...

### 2.4 El bien: el hermoso = XOR 0

Cuando se resta `2k` a partir de dos números que ambos tienen el 'k`‐th bit set, usted efectivamente se mueve ese bit **out** de ambos números. Repita esta operación para todos los bits, terminará con cero *iff* la XOR de todos los números en el subarray es cero.

¿Por qué XOR? #
`a XOR b = 0`
Si miras la representación binaria del subarray, cada operación cancela un bit común de dos números. La *paridad* (conteo o incluso conteo) de bits de conjunto para cada posición debe ser incluso para todos los bits a desaparecer – eso es exactamente lo que XOR‐zero garantiza.

■ **Resultado:** Un subarray es hermoso **iff** la XOR de todos sus elementos equivale a `0`.

-...

### 2.5 El Algoritmo - Prefijo XOR + HashMap

1. Prefix XOR array**
`pref[i] = nums[0] ^ nums[1] ^ ... ^ nums[i]`.

2. **Observación**
XOR de subarray `l.r` es `pref[r] ^ pref[l-1]`.
This equals `0` **iff** `pref[r] == pref[l‐1]`.

3. **Counting pairs with equal prefix XOR**
Iterate una vez más de `nums`, manteniendo un mapa de frecuencia de XORs prefijos vistos.
Para cada nuevo prefijo:
- Todos los índices previamente vistos con la misma forma de subarrays hermosas que terminan en el índice actual.
- `ans += freq[p]`.
- `freq[p]+`.

4. **Edge‐Case** - Prefijo vacío
Inicia el mapa con `{0: 1}` para que los subarrays que comienzan en el índice `0` se cuenten correctamente.

**Las complejidades* *

Silencioso Complejidad
Silencio...
← Tiempo Silencioso **O(n)** – un escaneo, operaciones de hah en tiempo constante
vivir el espacio **O(n)** – mapa contiene los valores de prefijo más 'n+1` distintos

-...

### 2.6 El mal: errores comunes

← Mistake Silencio Lo que parece
Silencio--------------...
Silencio Olvídate de contar los subarrays que comienzan en el índice `0` Silencio No inicial `{0: 1}` ¦
TENIDO Utilizando `int` para la respuesta cuando `n = 105` Silencio May overflow 32‐bit TENIDO Use `long` (Java) / `long long` (C+++) / `int` but cast to `int64` (Python maneja grandes ints)
Silencio Mis‐implementing XOR en lugar de la resta ¦ `pref ^= num` vs `pref -= num` ¦ Mantener XOR; la operación es conceptual, no una subtracción real ←
← Off‐by‐uno en el bucle (utilizando `for (int i = 1; i י= n; ++i)` con matriz basada en 0) Silencio Saltar el primer elemento ANTE Iterate sobre el array directamente, o ajustar cuidadosamente índices TENIDO

-...

### 2.7 The Ugly: Edge Cases and Performance Hurdles

Silencio Caso Edge Silencio Por qué importa
Silencio------------------------------
Silencio Todos los ceros (0,0,0,...) TENIDO Cada subarray es hermoso; cuenta es `n(n+1)/2`. El algoritmo naturalmente produce este resultado porque cada prefijo XOR permanece `0`. Silencio
Silencio Gran entrada (`n = 105`, `nums[i] = 106`) TENIDO El tamaño del mapa crece a `n+1`, todavía bien en la memoria. tención Uso `noordered_map` (C++) o `HashMap` (Java) – dan operaciones promedio O(1). Silencio
Silencio Valores de prefijo extremadamente escasos (p. ej., sólo 0 y 1) tención Mapa se mantiene diminuto – sin problema. No es necesario un manejo especial. Silencio

-...

### 2.8 Interview‐ Consejos listos

1. **Explicar el truco XOR primero** – los entrevistadores aman el momento “aha”.
2. **Mostrar la reducción** de O(n2) fuerza bruta a O(n) con un mapa.
3. **Discuten tiempo " espacio-offs** – tal vez mencionar un árbol de Fenwick o un árbol de segmento si preguntan.
4. **Pregunte aclarando preguntas** sobre la indexación basada en cero frente a una sola base; confirme cómo los subarrays “beltos” se definen para todos los arrays cero.
5. **Code en una pizarra** – escribe la inicialización hash‐map explícitamente; demuestra la atención al detalle.

-...

### 2.9 Código Final (Todos los Idiomas)

■ **Java** – Usa `HashMap` y una respuesta `long`.
■ **Python** – Usa `Counter` y el apoyo integrado en gran medida.
■ **C++** – Utiliza `unordered_map` para el caso promedio O(1).

Cada snippet está listo para pegar en el editor LeetCode o un repo de producción.

-...

### 2.10 Conclusión

LeetCode 2588 es un ejemplo de libro de texto de cómo un profundo conocimiento matemático (beautiful ж XOR 0) puede convertir un problema complejo de manipulación bit en un ejercicio de contabilidad lineal-time.

Entendiendo:

- **El Bien*
- **El malo * (insectos comunes),
- **El Ugly** (casos fuertes)

Usted no sólo asará este problema, pero también será capaz de explicarlo con confianza en cualquier entrevista de codificación.

■ **Siguiente paso:** Trate de implementar la misma idea en un idioma que está menos familiarizado con, o ajustar el mapa para utilizar un `TreeMap` y ver el impacto en el tiempo de ejecución.

Buena suerte, y que su próxima entrevista vaya *afortunadamente*!