-...
Título: LeetCode 3315. Construir el Array Bitwise Mínimo II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 3315 – Construir el Array Mínimo de Rastreo II
■ **LeetCode Medium ← Bit‐Manipulation Silencio Java Silencio Python ← C++**

-...

♪♪ ¿Qué pregunta el problema?

Dada una lista de *prime* números `nums`, construir un array `ans' de la misma longitud para que

`` `
ans[i] OR (ans[i] + 1) = nums[i]
`` `

and `ans[i]` debe ser el entero no negativo ** que satisface la ecuación.
Si no existe tal entero, ponga `-1' en esa posición.

■ *Examples*
[2, 3, 5, 7] → ans = [-1, 1, 4, 3]
[11, 13, 31] → ans = [9, 12, 15] `

-...

## 🧩 La observación clave

Mira la representación binaria de una primera 'p' (recordar, el único poder de-dos primo es `2`).

`` `
p = 5 (101b) → ans = 4 (100b)
p = 13 (1101b) → ans = 12 (1100b)
p = 7 (111b) → ans = 3 (011b)
p = 11 (1011b)→ ans = 9 (1001b)
`` `

¿Qué es común en todos estos casos?

*La respuesta se obtiene mediante la eliminación del bit **justo más recto que es parte de una carrera consecutiva de 1s**. *

Formalmente:

1. Cuenten el número de senderos `1`s (`t`) en `p`.
(es decir, mientras que el bit menos significativo es `1`, cambiar a la derecha y aumentar `t`.)
2. If `t == 0` (only `p == 2` tiene esta propiedad), la respuesta es `-1`.
3. De lo contrario, substrato `2^(t‐1) ' de `p`:

`` `
as = p – 2^(t-1)
`` `

¿Por qué funciona esto?
`ans ' will have all trailing bits equal to `1` Excepto el más adecuado de esa carrera.
Cuando añadas `1`, un transporte gira que `1` de vuelta a `0` y propaga un paso a la izquierda, por lo que el OR
con `ans` recrea exactamente la primera original.

-...

## 📦 Implementation

### 1. Java

``java
importar java.util*;

Clase Solución {
public int[] minBitwiseArray(List won) {
int n = nums.size();
int[] ans = nuevo int[n];
para (int i = 0; i)
int p = nums.get(i);
(p == 2) { // el único primo que es un poder de dos
as[i] = -1;
continuar;
}
int t = 0; // cuenta de seguimiento 1s
tmp = p;
(tmp) == 1) {
t++;
tmp > 1;
}
as[i] = p - (1 " 0 " )
}
devolver los ans;
}
}
`` `

### 2. Python 3

``python
Solución de clase:
def minBitwiseArray(self, nums: List[int]) List[int]:
res = []
para p en nums:
si p == 2: # no hay solución para 2
res.append(-1)
continuar
t = 0
tmp = p
mientras que tmp
t += 1
tmp > 1
re.append(p - (1 iere consignado (t - 1)))
retorno
`` `

### 3. C++

``cpp
Clase Solución {
public:
vector implicado menosBitwiseArray(vector realizadoint compartir nums) {
vector significar uns
para (int p : nums) {
si (p == 2) { // potencia máxima de dos
ans.push_back(-1);
continuar;
}
int t = 0; // trailing 1s
tmp = p;
(tmp) {
++t;
tmp > 1;
}
as.push_back(p - (1  se hizo (t - 1)));
}
devolver los ans;
}
};
`` `

-...

## 📈 Complexity Analysis

* **Time** – `O(n · log M)`
" n " = longitud de " años " , " M " = valor primario máximo.
El bucle que cuenta el seguimiento 1s toca cada bit a la vez.
* **Espacio** – auxiliar `O(1)` (aparte de la matriz de salida).

-...

El bueno, el malo, el feo

Silencio Silencio
Silencio------------Prince------
Silencio **Intuición** Silencio Patrón binario simple – eliminar un solo poco Silencio Requiere notar el patrón en primos Silencio Ninguno – el patrón podría ser perdido Silencio
Silencio **Implementación** Silencio Un paso por número, ninguna recursión Silencio Special‐case for `2` TEN Over-complicated if one try to use bit-shifts in a loop TEN
Silencio **Performance** tención Linear en bits, bien debajo de los límites Silencio O(n log M) está bien para `n ≤ 100` Silencio Ninguno – algoritmo es óptimo peru
Silencio **Edge Cases** Silencio Handles all primes (incluyendo 2) Requiere explícitamente `2` cheque Silencio Failing to treat `2` would break correctness TEN
Silencio **Readability** Silencio Nombres variables claros (`t`, `tmp`) Silencio Podría ser mal leído si bit‐ops no está familiarizado tención Evite las variables adicionales para la claridad TEN

-...

## 📚 Why This Blog Helps Your Job Hunt

* **SEO-friendly keywords** – *LeetCode solution*, *bitwise array*, *Java*, *Python*, *C++*, *minimum bitwise array*, *coding interview*, *algorithm analysis*.
* ** Estructura** – Declaración de problemas → Insight → Código → Complejidad → Discusión → SEO meta-descripción.
El equipo de trabajo suele esquiar para encontrar rápidamente las partes clave.
* ** Profundidad técnica** – Demuestra el dominio de trucos bitwise, propiedades de número primo y diseño de algoritmos limpios.
* ** Código práctico** – Tirantes listos para copiar en tres idiomas principales; muestra versatilidad.
* * Automarcación* Añadir una pequeña bio y un enlace a tu GitHub/LinkedAl final, convertir a los lectores en candidatos.

-...

## 🚀 Take‐away

* La respuesta siempre existe ** excepto** para la primera `2`.
* La solución es tan simple como *cuenta los senderos, subtract `2^(t‐1)*.
* Aplicarlo en un solo pase, y tienes una respuesta óptima y lista para entrevistas.

Feliz codificación, y que su entrevista sea tan libre de errores como este truco de bitwise!