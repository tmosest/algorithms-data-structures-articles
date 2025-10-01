-...
Título: LeetCode 3287. Encuentre el valor máximo de secuencia de Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 3287 – Encuentra el valor máximo de secuencia de Array
*Hard – LeetCode*

Silencio Idioma Silencio Complejidad
Silencio--------------------------
Silencioso **Java** Silencio O(n · k · 32) ♥ 2.6 M ops ANTERIEDO DE LOS MERCADOS Java 17 escrito/summary título...
Silencio **Python** TEN O(n · k · 32) ANTERIEDA DEtallanes incluidos consistenciasummary confianzaPython 3.11(s)/summary título...
Silencio **C++** Silencio O(n · k · 32) 23 escrito/summario título...

■ **Por qué esto importa para su cartera de entrevistas**
■ El problema te obliga a combinar ** selección de subsecuencia** con **bitwise OR/XOR** – dos grapas en entrevistas de codificación.
■ Dominar este patrón de DP-bitmask muestra que puede razonar sobre las limitaciones, el espacio del estado y la enumeración eficiente – una habilidad imprescindible para los roles de backend senior.

-...

## TL;DR

* El objetivo: elegir una subsequencia de longitud `2k` (elementos k, entonces elementos k) para maximizar
`(OR del primer k) XOR (OR del último k)`.
* Debido a que cada `nums[i]` es `Según 27`, el OR de cualquier grupo encaja en 5 bits → **32 posibles máscaras OR**.
* Use dos tablas DP:
* **prefijo DP** – índice más temprano en el que se puede lograr un OR dado con elementos exactamente "t".
* **Suffix DP** – último índice en el que se puede lograr un OO dado con elementos exactamente `t`.
* Después de llenar ambas tablas, iterate sobre todos los pares de máscara, compruebe que el índice de prefijo identificó sufijo, y tome el máximo XOR.

-...

## Full Solution (Java)

``java
importar java.util*;

Solución de la clase pública {}
int maxValue(int[] nums, int k) {
int n = nums.length;
int int final MAX_MASK = 1 > 0..31 (since nums[i] , 27)
final int INF = n + 1; // imposible index marker

// ---- Prefijo DP: primer índice para obtener OR=mask con elementos t ----
int[][] pref = nuevo int[k + 1][MAX_MASK];
para (int t = 0; t <= k; t++) Arrays.fill(pref[t], INF);
pref[0][0] = -1; // 0 elementos antes del array

para (int i = 0; i)
int val = nums[i];
// iterate t in reverse to avoid re-using the same element
para (int t = Math.min(k, i + 1); t {}
para (enmascarado = 0; mascarilla) {}
si (pref[t-1] [mask] [mask] = i - 1) { // podemos tomar este elemento
int newMask = máscara tención val;
pref[t][newMask] = Math.min(pref[t][newMask], i);
}
}
}
}

// registrar el índice más temprano para cada máscara OR
int[] first = new int[MAX_MASK];
Arrays.fill(first, INF);
para (enmascarada = 0; mascarilla) realizada MAX_MASK; mascarilla++) primero [mask] = pref[k][mask];

// ---- Suffix DP: último índice para obtener OR=mask con elementos t ----
int[][] suff = nuevo int[k + 1][MAX_MASK];
para (int t = 0; t <= k; t++) Arrays.fill(suff[t], -INF);
suff[0][0] = n; // 0 elementos después de la matriz

para (int i = n - 1; i 0; i--) {
int val = nums[i];
para (int t = Math.min(k, n - i); t {}
para (enmascarado = 0; mascarilla) {}
si (suff[t-1] [mask] i + 1) {
int newMask = máscara tención val;
[t] [newMask] = Math.max(suff[t] [newMask], i);
}
}
}
}

// registrar el último índice para cada máscara OR
int[] last = new int[MAX_MASK];
Arrays.fill(last, -INF);
para (enmascarada = 0; mascarilla) realizada MAX_MASK; mascara++) último [mask] = suff[k][mask];

//... Escanee todos los pares de máscaras para obtener el mejor XOR...
respuesta int = 0;
para (int m1 = 0; m1 = MAX_MASK; m1+) {}
si (primero[m1] == INF) continúan; // no puede conseguir este OR en prefijo
para (int m2 = 0; m2 ) {}
si (último[m2] == -INF) continúan; // no puede conseguir este OR en sufijo
si (primero[m1] se hacía [m2]) // los índices no superponen
respuesta = Math.max(respuesta, m1 ^ m2);
}
}
respuesta de retorno;
}
}
`` `

### Por qué funciona

* **Estado** – `pref[t][mask]` tiendas *el índice más pequeño* en el que podemos elegir `t` elementos hasta ese punto cuyo OR iguala `mask`.
Si sigue siendo " INF " , el OR es inalcanzable con elementos exactamente " no " .
* Transición – incluye el elemento actual `nums[i]`: `newMask = oldMask tención nums[i]`.
Mantenemos el índice más temprano porque lo compararemos más adelante con el índice de sufijo *latest*.
* El sufijo DP es simétrico – almacenamos el índice *latest*, por lo tanto iteramos hacia atrás.

La respuesta final es la máxima sobre todos los pares de máscaras que respetan la restricción del orden ( " pref[m1] " .

-...

## Full Solution (Python)

``python
de la importación Lista

Solución de clase:
def maxValue(self, nums: List[int], k: int) - Conf int:
n = len(nums)
MAX_MASK = 1 0 0 0.31
INF = n + 1 marcador imposible

# ---- prefijo dp : primer índice --
pref = [INF] * MAX_MASK for _ in range(k +1)]
pref[0][0] = -1 # antes del primer elemento

para i, val en enumerate(nums):
para t en rango(min(k, i +1), 0, -1):
para máscaras en rango(MAX_MASK):
si pref[t] [mask] [mask] 0 = i - 1: # puede utilizar este elemento
new_mask = máscara Silencioso val
pref[t][new_mask] = min(pref[t][new_mask], i)

primero = [pref[k][m] for m in range(MAX_MASK)]

Sufijo dp: último índice...
[-INF] * MAX_MASK for _ in range(k +1)]
[0] [0] = n # después del último elemento

para i en rango(n - 1, -1, -1):
val = nums[i]
para t en rango(min(k, n - i), 0, -1):
para máscaras en rango(MAX_MASK):
si suff [t - 1] [mask] i + 1:
new_mask = máscara Silencioso val
[t] [new_mask] = max(suff[t] [new_mask], i)

último = [suff[k][m] for m in range(MAX_MASK)]

#... Escanear todos los pares de máscara...
ans = 0
para m1 en rango(MAX_MASK):
si primero[m1] == INF: continue
para m2 en rango(MAX_MASK):
if last[m2] == -INF: continue
si primero[m1] se hizo último[m2]:
ans = max(ans, m1 ^ m2)
Retorno
`` `

-...

## Full Solution (C++)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxValue(vector fielint nums, int k) {
const int n = nums.size();
const int MAX_MASK = 1 > 0 > 5; // 32 máscaras porque nums[i] c) 27
int INF = n + 1; // índice imposible

/* prefijo DP : primer índice para OR=mask con elementos t */
vector realizador realizado, 32 títulos pref(k + 1);
for (int t = 0; t <= k; ++t) pref[t].fill(INF);
pref[0][0] = -1; // 0 elementos antes del array

para (int i = 0; i) {}
int val = nums[i];
para (int t = min(k, i + 1); t 1; --t) {
para (enmascarado = 0; mascarilla)
si (pref[t-1] [mask] [traducido]= i-1) { // puede elegir este elemento
int newMask = máscara tención val;
pref[t][newMask] = min(pref[t][newMask], i);
}
}
}
}
vector contratado primero(MAX_MASK, INF);
para (enmascarado = 0; mascarilla) realizada MAX_MASK; ++mask) primero [mask] = pref[k][mask];

/* sufijo DP : último índice para OR=mask con elementos t */
vector realizador realizado, 32 títulos suff(k + 1);
para (int t = 0; t <= k; ++t) suff[t].fill(-INF);
suff[0][0] = n; // 0 elementos después de la matriz

para (int i = n - 1; i 0; --i) {
int val = nums[i];
para (int t = min(k, n - i); t 1; --t) {
para (enmascarado = 0; mascarilla)
si (suff[t-1] [mask] i + 1) {
int newMask = máscara tención val;
[t] [newMask] = max(suff[t] [newMask], i);
}
}
}
}
vector identificador último(MAX_MASK, -INF);
para (enmascarada = 0; mascarillas) realizadas MAX_MASK; ++mask) duran [mask] = suff[k][mask];

/* Escanee todos los pares de máscaras para encontrar el mejor XOR */
int ans = 0;
para (int m1 = 0; m1)
si (primero[m1] ==INF) continúan;
para (int m2 = 0; m2 = MAX_MASK; ++m2) {
si (last[m2] == -INF) continúan;
si (primero[m1] se hacía [m2]) ans = max(ans, m1 ^ m2);
}
}
devolver los ans;
}
};
`` `

-...

## Good, Bad, & Ugly of the DP‐Bitmask Pattern

Silencio Lo que aprendimos tóxico Cómo muestra la habilidad
Silencio...
Silencio **Bien** Silencio • **Tiny state space** (32 máscaras) – muestra que puede reducir el problema a través de restricciones. **Linear DP** sobre posiciones – fácil de implementar, depurar y probar. ← Demonstrates * optimización de la limpieza* – convirtiendo una idea exponencial en una rutina de tiempo lineal. Silencio
Silencio** La declaración habla de *subsecuencias* (no subarrays) – muchos codificadores ingenuos probarán una combinación de índices de fuerza bruta (O(n2·k2)). El tamaño de la máscara OR es *no obvio*; usted necesita notar el truco “tratado 27”. ← Reveals *atención al detalle*: capturar una restricción oculta y convertirla en una gran velocidad. Silencio
Silencio **Ugly** Silencio • Gestión de arrays DP de 2 dimensiones (`t × máscara`) puede ser desordenado en idiomas que no soportan grandes arrays multidimensionales fuera de la caja. Algunas soluciones mantienen la mesa completa de DP aunque sólo necesitamos la fila 'k`‐th. tención Muestra *mantenibilidad de código*: cómo refactorizar un DP denso en dos arrays unidimensionales ( " primero " ) para la claridad. Silencio

-...

## Takeaway for the Interview

* **Mostrar su mentalidad impulsada por la restricción** – identificar que `nums[i] " significa sólo 32 valores OR posibles.
* **Explicar el DP** – lo que significa cada dimensión, por qué mantenemos índices *earliest* vs. *latest*, y por qué el escaneo final da la respuesta óptima.
* **Hablar sobre los casos de borde** – prefijos de longitud cero / suffixes, manejo de infinidad negativa, y cómo se elige el “marcador imposible”.

Este problema es un ejemplo perfecto para ilustrar que un entrevistado puede traducir una descripción combinatorial en un algoritmo limpio y eficiente que funciona en *tiempo lineal*. La maestría del patrón DP‐Bitmask es una señal fuerte de * madurez algorítmica* y *intuición de solución de problemas* – rasgos muy apreciados por la contratación de gerentes buscando ingenieros de software de primer nivel.