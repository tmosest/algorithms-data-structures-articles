-...
Título: LeetCode 3533. Divisibilidad concatenada -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 “Concatenated Divisibility” – A Full‐Stack Deep Dive (Java Silencio Python Silencio C++)
■ *Master este LeetCode Hard en 30 min → Aterrice su software de sueño papel de ingeniería. *

-...

## 1. Declaración de problemas

■ Se le da un array `nums` de **positivos** enteros (tamaño ≤ 13) y un entero positivo `k` (≤ 100).
■ A *permutation* of `nums` is said to form a **divisible concatenation** if the number obtained by concatenating the decimal representation of the integers in that order is divisible by `k`.
■ **Regresar la permutación más pequeña de la lexicografía** que satisface la condición.
■ Si no existe tal permutación, devuelve una lista vacía.

*Examples*

Silenciosos `nums` Silenciosos `k`
Silencio----------
TENIDO `[3,12,45] ' TENIDO 5 TENIDO `[3,12,45]
Silencioso[10,5]
TENIDA `[1,2,3] ' Silencio 5 TENIDO `[]

-...

## 2. ¿Por qué es difícil?

* The naïve approach enumerates all `n!` permutations → impossible even for `n = 13`.
* Los números concatenantes y el control de la divisibilidad se desbordarán `int64` para muchos casos.
* Debemos hacer un seguimiento de **remainder modulo k** mientras construimos la concatenación.
* También necesitamos el orden válido **léxicográficamente más pequeño** – que es una optimización adicional.

La solución estándar es un **DP + Bitmask** con recursión + memoización – exactamente el patrón utilizado para los problemas tipo “Traveling Salesman” pero con un estado restante.

-...

## 3. Idea de alto nivel

1. **Estado**
* `mask` – bitmask of the numbers that have already been placed.
* `rem` – resto del número formado hasta ahora, modulo `k`.

2. **Transición**
Para cada número no utilizado `x`:
* Compute `len(x)` – número de dígitos decimales de `x`.
* Compute `pow10[len(x)] % k` once at the beginning.
* Nuevo resto:
``text
nuevoRem = (rem * pow10[len(x)] + x) % k
`` `
* Recuerde en `mask tención (1 obedecidoidx)` y `newRem`.

3. *Base*
Cuando todos los bits se ponen (`mask == all`):
* If `rem == 0` → una permutación válida, devolver la lista vacía.
* De lo contrario → imposible, volver `null`.

4. ** Minimización lexicográfica* *
En la recursión, números iterados ** surtidos en orden ascendente**.
Tan pronto como encontremos a un niño *válido*, precindimos el número actual a su solución y paramos – porque el primer éxito será el más pequeño (ya que probamos números en orden ascendente).

5. *Memoización*
Los resultados de la tienda en un 'Map madeLong, List Garantizado' o un array de 2-D `dp[mask][rem]` para evitar la recomputación.
Key = `(mask ≤ 100`, 7 bits son suficientes).

-...

## 4. Aplicación del Código

A continuación se encuentran soluciones limpias y autocontenidas en **Java**, **Python**, y **C+**.
Los tres usan la misma lógica DP-mask, para que puedas elegir tu idioma favorito para la entrevista.

■ **Tip** – Muestra este código en tu GitHub o en una carpeta de "leetcode_solution". Programador de amor limpio y testable snippets.

#### 4.1 Java

``java
importar java.util*;

Solución de la clase pública {}

// ---
// API pública requerida por LeetCode
// ---
int[] concatenatedDivisibility(int[] nums, int k) {
int n = nums.length;
total Máscara = (1 < > >

// Pre-compute 10^len(x) % k para cada número
int[] pow10Mod = nuevo int[n];
para (int i = 0; i)
int len = numDigits(nums[i]);
pow10Mod[i] = modPow10(len, k);
}

// Ordenar una vez – asegura que probamos candidatos en orden ascendente
int[][] indexado = nuevo int[n][2]; // {original Índice, valor}
para (int i = 0; i < n; i++) indexado[i] = nuevo int[]{i, nums[i]};
Arrays.sort(indexed, Comparator.comparingInt(a - título a[1]));

// Memo mesa: máscara → rem → solución
Lista de datos: memo = nueva lista[1] [k];
Lista realizadaInteger mejor = dfs(0, 0, total Máscara, k, nums, pow10Mod, indexed, memo);

si (mejor == null) devuelve nuevo int[0];
int[] ans = nuevo int[best.size()];
para (int i = 0; i) mejor.size(); i++) ans[i] = best.get(i);
devolver los ans;
}

// ---
// Recursive DP con memoización
// ---
Lista privada dfs(enmascarado, int rem,
total Máscara, int k,
nums,
int[] pow10Mod,
int[][] indexado,
Lista NombradaInteger título[] [] memo) {

si (mask == totalMask) { // todos los números colocados
volver rem == 0 ? nuevo ArrayList recomendado() : null;
}
si (memo[mask] [rem] != null) devolver memo[mask][rem];

Lista de datos: Respuesta del título = nulo;

// Pruebe cada número no utilizado en orden ascendente
para (int[] par : indexado) {}
int idx = par[0], val = par[1];
si (mask " (1 " ) 0) continuar; // ya utilizado

int newRem = (int)(rem * (long)pow10Mod[idx] + val) % k);
Lista realizadaInteger menor = dfs(mask tención (1 Identificar idx), nuevoRem,
total Máscara, k, nums, pow10Mod,
indexado, memo);
si (hijo != null) { // primer golpe es lexicográficamente menor
niño.add(0, val); // prependiente número de corriente
respuesta = niño;
ruptura;
}
}

memo[mask] [rem] = respuesta;
respuesta de retorno;
}

// Utilidad: número de cifras decimales
int privada numDigits(int x) {
int cnt = 0;
cnt++; x /= 10; }
cnt de retorno;
}

// 10^len % k – computed by repeated multiplication
int privado modPow10(int len, int k) {
p = 1 % k;
para (int i = 0; i) i = i++) p = (p * 10) % k;
retorno (int)p;
}
}
`` `

-...

#### 4.2 Python

``python
Solución de clase:
def concatenatedDivisibility(self, nums: List[int], k: int) - título List[int]:
n = len(nums)
total = (1 0)

# Pre-compute (10^len(x)) % k
* n
para i, val en enumerate(nums):
dígitos = len(str(val)))
pow10[i] = pow(10, digits, k)

# Clasificar índices por valor para obtener orden lexicográfico
idxs = sort(range(n), key=lambda i: nums[i])

memo: Dict[Tuple[int, int], Optional[List[int]] = {}

def dfs(mask: int, rem: int) - confianza Opcional[List[int]:
si máscara == total:
retorno [] si rem == 0 más Ninguno
llave = (mask, rem)
si llave en memo:
devolver memo[key]

para mí en idxs:
si mascara " (1 " )
continuar
new_rem = (rem * pow10[i] + nums[i] % k
niño = dfs(mask tención (1 iere identificado i), new_rem)
si el niño no es Ninguno:
memo[key] = [nums[i]] + niño
devolver memo[key]

memo[key] = Ninguno
No.

res = dfs(0, 0)
Retorno res si la res no es ninguna otra []
`` `

-...

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector implicado concatenadoDivisibilidad(vector realizadoint compartir nums, int k) {
int n = nums.size();
int allMask = (1  won) - 1;

// Pre-computación 10^len(x) % k
vector asignadoint confianza pow10mod(n);
para (int i = 0; i) {}
int len = 0, tmp = nums[i];
(tmp) { len++; tmp /= 10; }
largo p = 1;
para (int j = 0; j) = len; + j) p = (p * 10) % k;
pow10mod[i] = (int)p;
}

// Tipos de índices para el orden lexicográfico
vector:
iota(idx.begin(), idx.end(), 0);
(idx.begin(), idx.end(),
[](int a, int b){ return nums[a] [b]; });

// Tabla DP: memo[mask] [rem] = permutación opcional
vector seleccionado, vector asignadovector seleccionado(k));
vector se llevó a cabobool confianza vis(1 seleccionado, vector asignadobool confianza(k,false));

función cumplidactora indicadaint(int,int) título dfs = [ cl](int mask, int rem) - título vector asignadoint {}
si (mask == allMask) {
devolver rem == 0 ? vector fiel() : vector asignado {-1};
}
si (vis[mask][rem]) devuelve memo[mask][rem];
vis[mask] [rem] = verdadero;

para (int id : idx) {
si continúan (mask " (1 se hizo));
int newRem = (int)(rem * 1LL * pow10mod[id] + nums[id]) % k);
vector implicado niño = dfs(mask tención (1 se realizó), newRem);
si (!child.empty() " paciente child[0]!= -1) { // encontrado
child.insert(child.begin(), nums[id]);
memo[mask] [rem] = niño;
el niño de retorno;
}
}
memo[mask] [rem] = vector asignadoint confianza{-1};
devolver memo[mask][rem];
};

vector implicado uns = dfs(0, 0);
si (!ans.empty() " sensible ans[0] == -1) ans.clear(); // no solution
devolver los ans;
}
};
`` `

■ ¿Por qué el centinela? * *
■ Es una bandera “imposible” ligera que evita cheques “nullptr” en C++.

-...

## 5. Análisis de la complejidad

Silencio DP Version ← Tiempo Silencioso
Silencio------------------
Silencio **Recursivo + Memo** (todos los 3 idiomas) Silencio **O( 2n · k · n )** – cada estado revisa cada número no utilizado.
TENIDO ANTERIOR Por `n ≤ 13`, `k ≤ 100`, que es en la mayoría de `8192 · 100 · 13 ♥ 107 ' operaciones - fácilmente 0.1 s en las CPU modernas. Silencio
TENIDO ANTERIOR **Espacio**: `dp[mask][rem]` → `2n · k` estados, cada uno almacenando una lista de hasta 'n' ints:
`O( 2n · k · n )` ♥ algunos megabytes. Silencio

*El truco de éxito de la ordenada reduce la ramificación real: tan pronto como golpeamos a un niño válido dejemos de la bucle, por lo que en la práctica el algoritmo es *linear en el número de estados*. *

-...

## 6. Lista de verificación Edge‐Case

Silencio Test confidencialidad Por qué importa
Silencio...
Silencio **Todos los números de un dígito** – por ejemplo, `[11,22,33]`, `k = 3` Silencio `pow10Mod` se convierte en `10 % 3 = 1` → transición simplifica. Silencio
Silencio **Gran número (≥ 109)** – por ejemplo: `[999999999, 123456] Silencio Nunca construimos el entero entero concatenado – sólo quedan pendientes. Silencio
Silencio **k = 1** Silencio Cada permutación es válida – la respuesta es sólo la matriz ordenada. Silencio
Silencio ** Ninguna solución** Silencioso Asegúrese de volver `[]` en lugar de `[null]` o `-1`. Silencio
Silencio ** Valores duplicados** tención Problema garantiza *distintos* enteros, por lo que no se requiere un manejo especial. Silencio

-...

## 7. Cómo probar

``bash
# Java
javac Solution.java
# Python
Python - "Seguido"
de la solución de importación
print(Solution().concatenatedDivisibility([3,12,45],5))
PY
# C++
g++ -std=c+17 solution.cpp "
`` `

Asegúrese de añadir pruebas de unidad para los tres ejemplos anteriores y algunos casos aleatorios ( " aleatorios(0) " para la reproducibilidad).

-...

## 8. Preguntas frecuentes de entrevista

Respuesta Corta de la respuesta
Silencio------------
*¿Podemos hacer esto sin ordenar?* Sí, pero usted necesita generar todas las permutaciones en el orden lexicográfico, que derrota el propósito. Ordenar es O(n log n) y trivial. Silencio
*¿Qué pasa si ‘k’ no es la primera?* No importa – las obras aritméticas modulares para cualquier entero `k`. Silencio
*¿Por qué no utilizar DP sobre el número de dígitos en lugar de números?* Debido a que el espacio del estado estallaría – el número de longitudes de dígitos posibles es mucho mayor que el número de números (`n`). Silencio
*¿Qué pasa si se permiten duplicados?* Usted necesita almacenar los recuentos de cada número en la máscara; todavía doable pero no en este problema. Silencio
*¿Hay una solución avaricia?* No – el problema es NP‐hard en general; DP es el enfoque estándar. Silencio

-...

## 9. Cómo se resuelve la declaración del problema

■ *Se les da una serie de enteros distintos `nums` y un entero `k`. Encuentra la matriz más pequeña (en orden lexicográfico) que puede obtenerse permutando `nums ' tal que el entero concatenado es divisible por `k`. *

El DP proporcionado encuentra la permutación **léxicográficamente más pequeña** que satisface la restricción de divisibilidad, o devuelve una matriz vacía si es imposible – exactamente lo que el problema exige.

-...

## 9. ¿Por qué esto te importa?

*Ha visto un problema que a primera vista parece una búsqueda de fuerza bruta sobre todas las permutaciones `n!`. La información clave es trabajar con **remanentes** y utilizar **bitmask DP** para prune el espacio de búsqueda dramáticamente. *

Dominar este patrón le permitirá abordar toda una clase de problemas de “concatenación y divisibilidad”, y el código anterior es una plantilla lista para usar que puede adaptarse para concursos de entrevistas.

Buena suerte - ¡Ahora ve a clavar esa entrevista! 🚀

-...

*Preparado por: [Su nombre]*
*Fecha: 2023‐08‐08*