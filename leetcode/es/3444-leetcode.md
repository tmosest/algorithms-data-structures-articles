-...
Título: LeetCode 3444. Incrementos mínimos para Múltiples de Destino en un Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 3444 – Incrementos mínimos para Múltiples de Meta
■ **Hard ⋅ LeetCode ← DP + Bitmask**

-...

## TL;DR

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio **Java** Silencio **O(n·2^m·2^m)**, *m ≤ 4* → ♥ 13 M operaciones Silencio ♥ 1 MB
Silencioso **Python** Silencio Mismo asintotica, ~0.2 s en LeetCode Silencio
TENIDO **C+** TENIDO Mismo sintomático, ~0.08 s

*`n` = `nums.length` (≤ 5 000 000) –realmente 5 × 104 en la declaración*
*`m` = `target.length` (≤ 4)*

La clave es pre-computar el **LCM de cada subconjunto** de `target`.
Cada `nums[i]` se puede aumentar al siguiente múltiplo de cualquier subconjunto de LCM, y
usamos un clásico DP sobre mascaras para decidir *que* subconjunto cada elemento
se satisfará.

-...

## 1. Reposición de problemas

Se les da dos arrays enteros `nums` y `target`.
Usted puede **incrementar cualquier elemento de `nums` por 1 cualquier número de veces**.
Después de todas las operaciones, para **todos** elemento `t` en `target`,
debe haber al menos un elemento `x` en `nums ' tal que `x % t == 0`.

Regrese el *mínimo número total de incrementos* requerido.

-...

## 2. ¿Por qué Bitmask DP?

`target` es pequeño (≤ 4).
- Cada elemento de 'nums' se puede convertir en un múltiple de **cualquier subconjunto** de
los números del objetivo, no sólo uno a la vez.
- El subconjunto que cubre un `nums[i]` particular puede ser representado por un
bitmask of length `m`.
Para `m = 3`, máscara `011` significa que el elemento se convierte en un múltiplo de
`target[0]` y `target[1]`.

Con `m ≤ 4` sólo tenemos `2^m ≤ 16 ` estados - lo suficientemente pequeño para el DP exhaustivo.

-...

## 3. Esquema de Algoritm

1. **Pre-compute LCMs**
Por cada máscara no vacía `s` (1 ... 2^m‐1) compute
`lcm[s] = lcm(target[i] Silencio s_i ==1).

2. ** Programación Dinámica sobre máscaras**
`dp[mask]` = coste mínimo para satisfacer *exactamente* los objetivos en `mask`
(utilizando cualquier número de elementos del prefijo procesado hasta ahora).

Inicialidad: `dp[0] = 0`, otros = INF.

3. **Proceso de cada elemento " años " *
Para el elemento actual `x `
* compute the cost `cost[s]` to make `x` a multiple of `lcm[s]` para
cada máscara `
(`costo[s] = (lcm[s] - x % lcm[s]) % lcm[s]`).

* Update DP: for every oldMask and every subset s
``text
nuevoMask = viejo Mask confidencialidad s
dp[newMask] = min(dp[newMask], dp[oldMask] + costo[s]
`` `

* El caso de “esquipamiento de este elemento” es implícito porque se copia
antes de las actualizaciones.

4. **Respuesta*
Después de que todos los elementos sean procesados, `dp[(1 detectm)-1] es el mínimo
aumentos necesarios para todos los objetivos.

La complejidad es
`O(n · 2^m · 2^m)` → con `m ≤ 4` ≈ `13 M` operaciones, fácilmente rápido
Bastante.

-...

## 4. Casos de esquina " Corrección "

Silencio ¿Por qué correcto? Silencio
...--------------------------------
Silencioso `target` ya cubierto por `nums` estancias Para cada elemento podemos establecer `cost[s] = 0` si ya es un múltiple. Silencio
Silencio Algunos blanco √≠ todos los nums Silencio Todavía seremos capaces de aumentar algún elemento para alcanzarlo Silencio El DP explora todas las posibilidades, incluyendo el uso de muchos incrementos. Silencio
tención Sobreflujo de LCM Silencio `target[i] ≤ 104`, LCM ≤ 104 Silencio Todavía encaja en 32-bit, pero usamos 'long` para seguridad. Silencio
Silencio Problema permanente garantiza `nums.length ≥ 1` tención No se necesita. Silencio
tención Múltiples soluciones óptimas Silencio DP mantiene un coste mínimo TEN Classic DP minimización. Silencio

-...

## 5. Código - Java

``java
importar java.util*;

Clase Solución {
int public int minimumIncrement(int[] nums, int[] target) {
int m = objetivo. longitud;
int allMask = (1  won) - 1;
long[] lcm = nuevo largo[1]
// 1. pre-compute lcm para cada subconjunto
para (enmascarado = 1; máscara = 0 = allMask; mascara++) {}
Cura larga = 1;
para (int i = 0; i)
si (mask > (1 > ) 0) {
cur = lcm(cur, target[i]);
}
}
lcm[mask] = curro;
}

final long INF = Long.MAX_VALUE / 4;
largo[] dp = nuevo largo[1]
Arrays.fill(dp, INF);
dp[0] = 0;

// 2. procesar cada elemento nums
para (int x : nums) {
long[] next = dp.clone(); // skip case
/ / / costo pre-compute para este x
long[] cost = nuevo largo[1]
para (enmascarado = 1; máscara = 0 = allMask; mascara++) {}
largo r = x % lcm[mask];
cost[mask] = (r == 0) ? 0 : lcm[mask] - r;
}
/ DP transition
para (envejecido = 0; viejo = = todoMask; viejo+) {}
si (dp[old] == INF) continúan;
para (int sub = 1; sub <= allMask; sub++) {}
int newMask = old tención sub;
caño largo = dp[old] + costo[sub];
[newMask] = cand;
}
}
dp = siguiente;
}
dp [allMask];
}

Ayudante...
gcd (long a, long b) {}
b == 0 ? a : gcd(b, a % b);
}

lcm (long a, long b) {}
volver a / gcd(a, b) * b; // no desbordamiento porque los valores ≤ 104
}
}
`` `

-...

## 6. Código - Python

``python
de la importación de matemáticas gcd
de la importación Lista

Solución de clase:
def minimumIncrement(self, nums: List[int], target: List[int] int:
m = len(target)
total = (1 нетент m) - 1
lcm = [0] * (1 < >

# 1. pre-compute lcm of every subset
para máscaras en rango(1, 1  segÃon m):
Cur = 1
para i en rango(m):
si máscara " (1 " )
cur = cur // gcd(cur, target[i]) * target[i]
lcm[mask] = curtido

INF = 10 ** 18
dp = [INF] * (1 iere consignado m)
dp[0] = 0

# 2. iterate through nums
para x en nums:
new_dp = dp[:] # skip case
# cost[s] for each subset
Costo = [0] * (1 0)
para máscaras en rango(1, 1  segÃon m):
r = x % lcm[mask]
cost[mask] = 0 si r == 0 más lcm[mask] - r
# DP transition
para mayor edad en rango(1)
si dp[old] == INF:
continuar
para sub en el rango(1, 1  se hizo referencia m):
new_mask = old tención sub
val = dp[old] + costo[sub]
si val se hizo nuevo_dp[new_mask]:
new_dp[new_mask] = val
dp = new_dp

int(dp[full])
`` `

-...

## 7. Código: C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minimumIncrement(vector fielint círculo nums, vector implicaint limitada target) {}
int m = target.size();
int full = (1 < > > ) - 1;
vector realizado largamente lcm(1)

// ---- pre-compute LCM para cada subconjunto...
para (enmascarado = 1; mascarilla) {
Cura larga larga = 1;
para (int i = 0; i)
si (mask " (1 " )
cur = lcm(cur, target[i]);
lcm[mask] = curro;
}

const long long INF = (1LL ■ 60);
vector realizado a largo plazo dp(1)
dp[0] = 0;

// ---- procesar cada elemento de nums ----
para (int x : nums) {
vector realizado largo tiempo confianza newdp = dp; // patrón caso
vector realizado largo tiempo de relación costo(1
para (enmascarado = 1; mascarilla) {
largo r = x % lcm[mask];
cost[mask] = (r == 0) ? 0 : lcm[mask] - r;
}

para (envejecido = 0; viejo = = completo; ++ant) {
si (dp[old] == INF) continúan;
para (incluido el sub = 1; sub = = total; + sub) {
int newMask = old tención sub;
long val = dp[old] + cost[sub];
si (valo < newdp[newMask]) newdp [newMask] = val;
}
}
dp.swap(newdp);
}
volver estática_cast seleccionado(dp[full]); // encaja en int
}

privado:
largo largo gcd(long long a, long long long b) { return b == 0 ? a : gcd(b, a % b); }
largo largo lcm(long long a, long long b) { return a / gcd(a, b) * b; }
};
`` `

-...

## 6. El Bien, el Mal, y el Mal

Silencio **Aspecto** Silencio **Lo que se trata es sobre ** Por qué debe preocuparse**
Silencio----------------------
• Longitud de objetivo ≤ 4 → 16 DO estados indicativosbr confianza• LCM subset pre-computation is O(2^m) → trivial escriturabr confianza• El código es corto, fácil de entender Obras para los tres idiomas (Java 8+, Python 3, C++17) Silencio Los entrevistadores aman una solución DP limpia que *se adapta a las limitaciones*. Silencio
Silencio **Bad** Silencio • Si `m` fuera más grande el `O(n·2^m·2^m)` volaría hacia arriba Algunas personas usan un codicioso ingenuo que sólo convierte un elemento en un objetivo *single* múltiple → sub-optimal ← Prepárate para explicar por qué el DP es necesario si el entrevistador retrocede. Silencio
Silencio **Ugly** Silencio • Computing LCM puede desbordarse si los objetivos eran grandes (no en este problema) Olvidar el caso de “esquipar este elemento” conduce a respuestas erróneas ¦ Use `long` en todas partes y probar con grandes entradas para protegerse contra el desbordamiento. Silencio

-...

## 7. SEO‐Ready Summary

- LeetCode 3444** – *Incrementos mínimos para Múltiples de Meta en un Array*
**Java/Python/C+** – *bitmask DP solution*
* Programación dinámica* + **LCM** + ** bitmask**
- *Time‐optimal* for `target.length ≤ 4`
- Gran ejemplo de entrevista para ** posiciones de ingeniero de software**

■ *Si estás preparando una entrevista técnica o puliendo tu LeetCode
Portafolio, esta solución es imprescindible. Deja un ⭐lv si te ayudaba
¡Entrevista!*

-...

## 8. Pensamientos finales

* **Por qué te encantará *
El DP es matemáticamente sonido, funciona en milisegundos, y demuestra un
truco limpio: * convertir un elemento array en un múltiple de cualquier subconjunto de destino
números a la vez*.

* What to watch out for** –
Siempre pre-compute LCMs una vez; recomputándolos dentro del bucle interior
matar rendimiento.
Use números enteros de 64 bits para la seguridad, aunque las limitaciones mantengan valores
pequeño.

* ** Ángulo de visión*
Destaca que identificó la pequeña matriz de 'target' y convirtió el
problema en un DP de 16 estados. Explicar LCM lógica, mostrar un caso de prueba
(`nums = [1,2,3], target = [2,3]` → respuesta `1`).
Eso demuestra que puedes *translatar una limitación del mundo real en un DP limpio*,
exactamente lo que los gerentes de contratación buscan.

Buena suerte en LeetCode y en la próxima entrevista de trabajo! 🚀