-...
Título: LeetCode 3247. Número de subsecuencias con Odd Sum -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Problema Recap – LeetCode 3247
**Número de consecuencias con sumo extraño* *
■ Dado un conjunto entero de `nums`, cuente todas las subsecuencias cuyo elemento suma es **odd**.
■ Devuelve el modulo de respuesta \(10^9+7\).

■ **Constraints**
√≥ - \(1 \leq n = \text{nums.length} \le 10^5\)
[i] \le 10^9\)

-...

## 2down Key Insight

Para una subsecuencia sólo importa la *paridad** de su suma.

* Si agregamos un número **odd** a una subsequencia existente, su paridad cambia.
* Añadiendo un número **** mantiene la paridad sin cambios.

Esto nos permite mantener ** sólo dos contadores**:

Silencioso
Silencio----------------------------
Silencio # de subsecuencias vistas hasta ahora con una suma impar de subsecuencias vistos hasta ahora con una suma uniforme Silencio Actualizado después de inspeccionar cada elemento array ¦

Cuando nos encontramos con un nuevo número `x` podemos decidir:

Silencioso `x ' parity Silencio Nuevo `oddCnt`
Silencio------------------------------------------------------
Silencio **Odd** Silencio `oddCnt + evenCnt + 1` *(existing odds, existing evens flipped, new subsequence `[x]`)* Silencio `oddCnt + evenCnt`  durable
*(existiendo las probabilidades duplicadas, con o sin `x`)* * inclusoCnt + 1` *(existiendo las probabilidades duplicadas + `[x]*)* Silencio

Todas las operaciones se realizan modulo \(10^9+7\).

El algoritmo es un solo paso: **O(n)** tiempo, **O(1)** espacio extra.

-...

## 3down⃣ Solution Code

A continuación se presentan implementaciones limpias y de producción en **Java**, **Python**, y **C+**.
Cada aplicación sigue la misma lógica del DP descrita anteriormente.

-...

### 3.1 Java

``java
importar java.util*;

Solución de la clase pública {}
static final long MOD = 1_000_000_007L;

public int subsequenceCount(int[] nums) {
largas probabilidades = 0;
largo incluso = 0;

para (int num : nums) {
(num) == 1) { // número impar
long newOdd = (odd + incluso + 1) % MOD;
nuevo Incluso = (odd + even) % MOD;
extraño = nuevo Odd;
incluso = nuevo Incluso;
} más { // incluso número
long newOdd = (odd * 2) % MOD;
nuevo Incluso = (incluso * 2 + 1) % MOD;
extraño = nuevo Odd;
incluso = nuevo Incluso;
}
}
(int) odd; // odd Cnt tiene la respuesta
}
}
`` `

-...

#### 3.2 Python

``python
Solución de clase:
MOD = 1_000_000_007

def subsequence Conde(self, nums: List[int]) - título int:
extraño, incluso = 0, 0
para las numidades:
si num % 2: # extraño
new_odd = (odd + incluso + 1) % yo. MOD
new_even = (odd + even) % self. MOD
extraño, incluso = new_odd, new_even
# incluso #
new_odd = (odd * 2) % self. MOD
new_even = (even * 2 + 1) % self. MOD
extraño, incluso = new_odd, new_even
Vuelta raro
`` `

-...

### 3.3 C++

``cpp
Clase Solución {
public:
int subsequenceCount(vector seleccionadoint limitada nums) {
const long MOD = 1'000'000'007LL;
larga distancia = 0, incluso = 0;

para (int num : nums) {
(num) { // odd
largo tiempo nuevoOdd = (odd + incluso + 1) % MOD;
largo tiempo nuevo Incluso = (odd + even) % MOD;
extraño = nuevo Odd;
incluso = nuevo Incluso;
♪ otra vez { // incluso
long long long newOdd = (odd * 2) % MOD;
largo tiempo nuevo Incluso = (incluso * 2 + 1) % MOD;
extraño = nuevo Odd;
incluso = nuevo Incluso;
}
}
volver estática_cast seleccionado(odd);
}
};
`` `

-...

## 4down El Bien, el Mal, y el Ugly

Lo que es bueno para la vida Lo que es malo para la vida
Silencio------------------------------------------------------
Silencio **Concepto** Silencio Simple parity-based DP → O(n) time, O(1) space Silencio Ninguno ← Ninguno
Silencio **Brute‐Force** ← Subconjuntos Exponentiales (2^n) Silencio Tiempo exponencial > memoria → TLE/MLE ANTERI Estack rebosa si la recursión no es cuidadosa
Silencio **Memoización de hombros** Silencio Fácil de razonar (estado = `index, parity`) ← Necesidades O(n) profundidad de recidiva, mesa de memo extra ANTE Recursión profundidad de 10^5 → desbordamiento de pila; más lento que iterante
Silencio **Bottom‐Up DP** Silencio Coincide con la solución iterativa por encima de TENSlightly more code if you store arrays ¦ Overkill – you don't need an array of size n TEN

■ **Por qué el DP iterativo es la estrella de entrevistas* *
■ *Fast*: un escaneo, trabajo constante por elemento.
■ *Robust*: sin riesgo de límites de recursión, sin grandes arrays auxiliares.
■ *Clear*: dos números, dos reglas – fácil de explicar en una pizarra.

-...

## 5VIEW⃣ Complexity Analysis

TENCIÓN TERRITOR TENIDA Cálculo
Silencio----------
Silencio **Tiempo** Silencioso `O(n)` – un paso sobre la matriz Silencioso
Silencio** – sólo dos contadores de 64 bits
Silencio ** Operaciones de Marruecos** y también – cada paso utiliza algunas operaciones de `% MOD`

-...

## 6down⃣ Interview‐Ready Tips

1. **Explicar la observación de la paridad primero** – esto te muestra entender por qué sólo dos estados son suficientes.
2. **Espera un pequeño ejemplo** (por ejemplo, `[1, 2, 3]`) al actualizar `oddCnt ' y `evenCnt ' .
3. **Mención del modulo** – muchos entrevistadores esperan que usted evite el desbordamiento temprano.
4. **Hablar de alternativas** (fuerza bruta, DP con array) y por qué los descartó.
5. **Mostrar el código** en su idioma preferido, manteniendo nombres variables autodescriptivos (`odd`, `even`).

-...

## 7down W Wrap‐Up

El problema “Número de Subsecuencias con Odd Sum” es un ejemplo clásico de cómo una simple observación (reflexión de la paridad) puede convertir un problema combinatorio aparentemente exponencial en un DP de tiempo lineal.
La solución es compacta, eficiente y lingüísticamente agnóstica, lo que lo convierte en un gran punto de conversación de entrevistas.

■ **SEO Palabras clave**: LeetCode 3247, número de subsecuencias con suma impar, solución Java DP, solución Python DP, solución C++ DP, codificación de entrevistas, entrevista de algoritmos, prep de entrevista de trabajo, O(n) DP, paridad de programación dinámica, modulo 1e9+7.

¡Buena suerte en tu viaje de codificación! 🚀