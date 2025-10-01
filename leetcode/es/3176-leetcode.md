-...
Título: LeetCode 3176. Encontrar la longitud máxima de una buena subsequencia I -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Finding the Maximum length of a Good Subsequence (LeetCode 3176)

■ **TL;DR** – Use un DP *twodimensional* que mantenga la mejor longitud para cada posible *número de “romperes”* (`k`) y *valor máximo* visto.
■ ** Complejidad** – `O(n·k)` tiempo, `O(n·k)` espacio (Ω 500 × 25).
■ **Idiomas** – Java, Python, C++.

-...

## 1. Recaptación de problemas

Se le da un array entero `nums` (tamaño ≤ 500) y un entero no negativo `k` (≤ 25).
A **good** subsequence `seq` satisfies:

`` `
# of i in [0, tenciónseq sometida-2] such that seq[i] != seq[i+1] ≤ k
`` `

En otras palabras, la subsecuencia puede contener a lo más " rupturas " entre elementos iguales consecutivos.
Devuelve la *máximo longitud posible* de tal subsequencia.

-...

## 2. Why a DP on `k ' and "last value " works

Si escaneamos `nums` de izquierda a derecha, en cada paso debemos decidir si **to** el elemento actual en la subsequencia o **skip**.

* Cuando lo tomamos, surgen dos casos:
* **Ningún nuevo descanso** – el elemento anterior en la subsequencia es igual al actual.
→ `rompers` se mantiene igual.
* **Nuevo descanso** – el elemento anterior es diferente y se nos permite utilizar un descanso más ( < k > 0 > ).
→ `rompers` aumenta por uno.
* Cuando lo saltamos, nada cambia.

La respuesta óptima para un prefijo depende solamente de:
1. Cuántos descansos hemos utilizado hasta ahora (`i`).
2. Lo que el valor **último** en la subsequencia es (`a`), porque sólo este valor decide si se necesita un nuevo descanso.

Por lo tanto podemos mantener

`` `
dp[i][a] = longitud máxima de una buena subsequencia vista hasta ahora
que usa exactamente yo rompe y termina con valor
`` `

Durante la exploración actualizamos `dp` en *reverse* orden de `i` (para evitar volver a utilizar el elemento actual en la misma iteración).

-...

## 3. La transición del DP

Por cada elemento `a` en `nums`:

`` `
para mí de k down a 0
// Opción 1: continuar la carrera actual (sin nuevo descanso)
cand1 = dp[i] + 1

// Opción 2: iniciar una nueva carrera con un número diferente
// (sólo si tenemos un valor anterior y todavía tenemos descansos a la izquierda)
cand2 = (i ≤ 0) ? res[i-1] + 1 : 0

dp[i][a] = max(dp[i][a], cand1, cand2)
res[i] = max(res[i], dp[i][a]) // res[i] = la mejor longitud para cualquier último valor
`` `

`res[i]` mantiene la mejor longitud sobre *all* los últimos valores para un `i' fijo, que se necesita para `cand2`.
Después de procesar toda la matriz, la respuesta es `res[k]`.

-...

## 4. Código - Java

``java
importar java.util*;

Clase Solución {
public int maximumLength(int[] nums, int k) {
// dp[i] – mapa de último valor a mejor longitud con i breaks
@SuppressWarnings("unchecked")
Mapa realizadoInteger, Integer {] dp = nuevo HashMap[k + 1];
para (int i = 0; i <= k; i++) dp[i] = nuevo HashMap entendido();

int[] res = nuevo int[k + 1]; // mejor longitud para cada i sobre todos los últimos valores

para (int a : nums) {
para (int i = k; i 0; i--) {
int v = dp[i].getOrDefault(a, 0);
// Continúa.
v = Math.max(v + 1, (i ю 0 ? res[i - 1] + 1 : 0));
dp[i].put(a, v);
res[i] = Math.max(res[i], v);
}
}
devolver res[k];
}

// Conductor rápido para pruebas locales
public static void main(String[] args) {
Solución s = nueva solución ();
System.out.println(s.maximumLength(new int[]{1,2,1,1,3}, 2)); // 4
System.out.println(s.maximumLength(new int[]{1,2,3,4,5,1}, 0)); // 2
}
}
`` `

-...

## 5. Código - Python

``python
de las colecciones importadas por defecto
de la importación Lista

Solución de clase:
def maximumLength(self, nums: List[int], k: int) - título int:
# dp[i] – dict: last value la mejor longitud con i rompe
dp = [defaultdict(int) for _ in range(k + 1)]
res = [0] * (k +1) # la mejor longitud para cada i sobre todos los últimos valores

para una en las numidades:
para i en rango(k, -1, -1):
Opción 1: continuar corriendo
val = dp[i][a] + 1
Opción 2: nuevo descanso
si yo 0:
val = max(val, res[i - 1] + 1)
dp[i][a] = val
res[i] = max(res[i], val)

retorno res[k]

# Quick driver for local testing
si __name_ == "__main__":
s = Solución()
print(s.maximumLength([1, 2, 1, 3], 2)) # 4
print(s.maximumLength([1, 2, 3, 4, 5, 1], 0))
`` `

-...

## 6. Código: C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
máximo Longitud(vector realizadoint limitada nums, int k) {
// dp[i] – unordered_map: última relación calidad- la mejor longitud con i rompe
vector noordered_map obtenidosint,int títulos dp(k + 1);
vector asignadoint edad res(k + 1, 0); // la mejor longitud para cada i sobre todos los últimos valores

para (int a : nums) {
para (int i = k; i 0; --i) {
int val = dp[i][a] + 1; // continue run
si (i > 0) val = max(val, res[i - 1] + 1); // nuevo descanso
dp[i][a] = val;
res[i] = max(res[i], val);
}
}
devolver res[k];
}
};

// Conductor rápido para pruebas locales
int main() {}
Solución s;
cout se llevó a cabo s.maximumLength({1, 2, 1, 1, 3}, 2)
cout se realizó s.maximumLength({1, 2, 3, 4, 5, 1}, 0) se realizó endl // 2
retorno 0;
}
`` `

-...

## 7. El Bien, el Mal, y el Ugly

TENIDO Aspecto TENIDO Lo que funcionó ANTERIOR Por qué importa
Silencio...
Silencio **Bien – Intuitivo DP** Silencio El estado "(rompers used, last value)`" captura exactamente lo que necesitamos. Silencio Mantiene la solución tanto simple como eficiente (`O(nk)`). Silencio
Silencio **Bien – Salvar el espacio * Silencio Usando `unordered_map`/`defaultdict` en lugar de una tabla completa `n × k` reduce la memoria a la mayoría de `k × distintos(valores)` (≤ 25 × 500). Silencio Maneja el rango de valor 10^9 sin enormes tablas de hash. Silencio
Silencio **Bad – Edge Cases** Silencio Cuando `k = 0`, la transición debe saltar `res[-1]`. El código maneja explícitamente esto. Silencio Un error común fuera de cada uno. Silencio
Silencio **Bad – Retroceder Loop** Silencio Updating `dp[i]` in *descending* order of `i` is mandatory. Un bucle delantero rompe la corrección. tención Evita usar el mismo elemento dos veces en un paso. Silencio
Silencio **Ugly – Large `k`** Silencio Si `k` fuera más grande (por ejemplo, 500), el algoritmo se degradaría a `O(n^2) ` o usar demasiada memoria. El problema limita a propósito mantener `k ≤ 25`. Silencio
Silencio **Ugly – Detalle de Implementación** Silencio Algunos idiomas (por ejemplo, Java) requieren trucos de borrado tipo para arrays genéricos. El calentador oculto puede distraer del núcleo algorítmico. Silencio

-...

## 8. SEO‐Optimized Summary for Job Interviews

- **Keywords**: LeetCode, Good Subsequence, DP, Dynamic Programming, Interview, Coding Interview, Algorithm, Python, Java, C++
- **Meta Descripción**: “Master LeetCode 3176 – Longitud máxima de una buena subsequencia. Aprende una solución O(n·k) DP en Java, Python y C++. Perfecto para su próxima entrevista de ingeniería de software. ”
**H1**: “Programación Dinámica – LeetCode 3176 Buena Subsecuencia”
- ** Call‐to-Action**: “¿Quieres marcar más alto en entrevistas de codificación? Pruebe implementar este DP eficiente en su idioma preferido hoy! ”

-...

## 9. Pensamientos finales

LeetCode 3176 es un gran parque infantil para mostrar:

1. **Problema descomposición** – elegir el estado DP adecuado.
2. **Handling Large Ranges** – con mapas de hash en lugar de arrays densos.
3. **Idiomas específicas de idiomas** – uso eficiente del mapa en Java, Python, C++.

Si puedes explicar el DP en **menos de 2 minutos** y entregar el código anterior en una entrevista de trabajo, demostrarás tanto *información algorítmica* como *aplicación limpia*—exactamente lo que buscan los entrevistadores. ¡Feliz codificación!