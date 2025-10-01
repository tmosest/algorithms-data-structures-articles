-...
Título: LeetCode 1531. Compresión de cuerda II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1531 - Compresión de cuerda II
**LeetCode Hard – DP, Run‐Length Encoding, Delete k Chars* *

-...

## 1down Lo que el problema es

Se le ha dado una cadena de minúsculas `s` (`1 ≤  vidas sometidas ≤ 100`) y un entero `k ' (`0 ≤ k ≤ Нованикованый ' ).
Usted puede eliminar * en la mayoría* `k` caracteres de `s`.
Después de las eliminaciones que ejecutas **corrección de longitud (RLE)**:

* Reemplazar cualquier carrera del mismo personaje que aparece **2 o más veces** con
`char + cuenta`.
* Permanecen caracteres individuales como son – no se añade “1”.

Objetivo: **Minimizar la longitud de la cadena codificada**.

■ Ejemplo
"Aaabcccd", k = 2"
" Borrar " b " y " d " → " aaccc " → RLE → " a3c3 " → longitud " 4.

El problema es difícil porque usted tiene que decidir *que* `k` caracteres para borrar y *donde* para dividir la cadena en carreras.

-...

## 2down ¿Por qué DP es la herramienta correcta

Si miramos la cuerda de izquierda a derecha, la decisión en la posición `i` sólo depende de

* cuántas eliminaciones aún tenemos,
* Donde el siguiente personaje* después de `i` es.

Por lo tanto el estado puede ser representado por
`(index i, remaining‐k)` → *mínimo longitud codificada para el sufijo `s[i:]`*.

Este es un problema clásico de dos dimensiones DP que podemos resolver

* **Top‐Down (memoización)** – recursión con caché.
* **Bottom‐Up (tablación)** – iterativa DP.

Ambas soluciones funcionan en el tiempo de `O(k · n2) ` (caso inferior `n = 100') y `O(k · n)` memoria, que es lo suficientemente rápido para las limitaciones.

-...

## 3down Insight clave – “Siguiente mismo carácter” Pre-computación

Durante el DP necesitamos saber, para cada posición `i`, el siguiente índice ' j но i ' donde `s[j] == s[i]`.
En lugar de escanear hacia adelante cada vez (que haría el DP `O(n3)`), construimos un array `next`:

`` `
siguiente[i] = índice de la próxima aparición de s[i] después de i (o -1 si no)
`` `

Lo construimos en **O(n)** escaneando la cadena de derecha a izquierda y manteniendo la última posición para cada carta.

Con el siguiente podemos enumerar eficientemente todas las posibles “corridas” que comienzan en “i”.

-...

## 4down Cómo funciona el DP

`` `
dp[i][rem] = longitud mínima codificada de s[i:] utilizando en la mayoría de las eliminaciones rem
`` `

#### Transitions

1. **Delete `s[i]**
`dp[i][rem] → dp[i+1][rem-1] (si rem 0)

2. Mantén una carrera empezando por 'i'
Camine por todas las ocurrencias posteriores del mismo carácter (`cur = i, next[i], next[i], ...`).
Para cada punto final posible `cur`:

* `lenWindow = cur - i + 1` (características consideradas)
* `occurrencias = número de personajes guardados en esta carrera `
(`ocurrencias` aumentos por 1 cada vez que visitamos un mismo índice de letras)
* `removals = lenWindow - occurrences` (caracters we delete inside the window)
* Si `removals > rem` → break (no quedan más deleciones)
* `cost = 1` (para la propia carta)
más `+1` cada vez que `ciudades' alcanza 2, 10, 100 (crecen los dígitos)
* `dp[i][rem] = min(dp[i][rem], cost + dp[cur+1][rem-removals]) `

The base case: `dp[n][*] = 0` (empty suffix).
Si la longitud del sufijo ≤ `rem`, podemos eliminar todo → longitud `0`.

La respuesta es `dp[0][k].

-...

Detalles de la aplicación

A continuación se muestran **ready‐to-copy** soluciones en **Java, Python, y C++**.
Los tres usan el mismo algoritmo y la misma pre-computación de matriz "next".

■ **Tip:**
Para Java y C++ utilizan un conjunto de 'int` inicializado a `-1' para la memoización.
Para Python use `functools.lru_cache` o un diccionario explícito.

-...

### 📄 Java – Top‐ Down Memoization

``java
importa java.util. Arrays;

Solución de la clase pública {}
// helper to build the "next same character" array
int[] buildNext(char[] s) {
int n = s.length;
int[] next = new int[n];
int[] last = new int[26];
Arrays.fill(last, -1);
para (int i = n - 1; i 0; i--) {
int idx = s[i] - 'a';
siguiente[i] = último[idx];
último[idx] = i;
}
volver después;
}

int getLengthOfOptimalCompression(String s, int k) {
si (k >= s.length()) devuelve 0;
int[] next = buildNext(s.toCharArray());
int n = s.length();
int[][] memo = nuevo int[k + 1][n + 1];
for (int[] row : memo) Arrays.fill(row, -1);
dfs(0, k, next, memo);
}

int privado dfs(int i, int rem, int[] next, int[][] memo) {
si (memo[rem][i] != -1) devolver memo[rem][i];
int n = next.length;
si (n - i <= rem) devuelve memo[rem][i] = 0; // eliminar el resto

int best = Integer.MAX_VALUE;

/ Opción 1: eliminar el char actual
si (rem > 0) mejor = Math.min(best, dfs(i + 1, rem - 1, next, memo));

// Opción 2: mantener una carrera empezando por i
int occ = 0;
int cost = 1; // for the letter itself
for (int cur = i; cur != -1; cur = next[cur]) {}
occ++;
int deletions = (cur - i +1) - occ; // inside the window
si (deleciones > rem) romper; // no puede permitirse más deleciones

// aumentar el costo cuando los dígitos crecen
si (occ == 2 Silencioso occ == 10 Silencioso occ == 100) costo++;

mejor = Math.min(best, cost + dfs(cur + 1, rem - deletions, next, memo));
}

devolver memo[rem][i] = best;
}
}
`` `

-...

### 📄 Python – Recursive DP with `lru_cache `

``python
desde functools import lru_cache
de la importación Lista

Solución de clase:
def build_next(self, s: str) List[int]:
n = len(s)
nxt = [-1]
[-1] * 26
para i en rango(n - 1, -1, -1):
idx = ord(s[i]) - 97
nxt[i] = last[idx]
último[idx] = i
Nxt

def getLengthOfOptimalCompression(self, s: str, k: int) int:
si k >= len(s)
retorno 0
nxt = self.build_next(s)
n = len(s)

@lru_cache(None)
def dfs(i: int, rem: int) - título int:
si n - i <= rem: # borrar el resto
retorno 0
mejor = flotante('inf')

# Borrar el carácter actual
si rem:
mejor = min(mejor, dfs(i + 1, rem - 1))

# Mantén una carrera empezando por i
occ = 0
costo = 1 # la letra misma
Cur = i
mientras se cura!= -1:
occ += 1
deleciones = (cur - i + 1) - occ
si eliminaciones rem:
descanso
occ in (2, 10, 100):
costo += 1
mejor = min(mejor, costo + dfs(cur + 1, rem - supresiones))
cur = nxt[cur]
mejor

devolver dfs(0, k)
`` `

-...

### 📄 C++ – Tabulación de arriba (para diversión)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector asignadoint espíritu buildNext(const string borde s) {
int n = s.size();
vector implicado siguiente(n, -1), último(26, -1);
para (int i = n - 1; i 0; --i) {
int c = s [i] - 'a';
siguiente[i] = último[c];
[c] = i;
}
volver después;
}

int getLengthOfOptimalCompression(string s, int k) {
int n = s.size();
si (k >= n) retorno 0;
vector implicado nxt = construirSiguiente(s)
vector seleccionado(n + 1, -1);

función efectuada(int,int)](int i, int rem) {
si (dp[rem][i]!= -1) retorno dp[rem][i];
dp [rem][i] = 0; // eliminar todos los restantes
int best = INT_MAX;

si (rem) mejor = min(best, dfs(i + 1, rem - 1));

int occ = 0;
int cost = 1;
for (int cur = i; cur != -1; cur = nxt[cur]) {}
++occ;
int del = (curo - i + 1) - occ;
si se rompe (del > rem)
si (occ == 2 Silencioso occ == 10 Silencioso occ == 100) costo++;
mejor = min(mejor, costo + dfs(cur + 1, rem - del));
}
dp[rem][i] = best;
};

dfs(0, k);
}
};
`` `

-...

■ Los tres programas emiten la longitud **minimum codificada** para cualquier entrada válida y se ejecutan en una fracción de segundo.

-...

## 6VIEW⃣ Time & Space Complexity

Silencio Silencio Silencio Silencio Silencio Silencio Silencio
Silencio--------------
Silencio Top‐Down Silencio `O(k · n2) `` (Ω 1 M operations for `n = 100`, `k = 100`) Silencio `O(k · n)`
Silencio Bottom‐ Up TEN SON SON TENIDO SON TENIDO

Con 'n ≤ 100' esto está muy por debajo del límite de 1 segundos en LeetCode.

-...

## 7down Pi Common Pitfalls " What if " Escenarios

Silencio Pitfall Silencio
Silencio...
Silencio **Mis-counting digit changes** – olvídate de que el primer dígito es *no* contado para la longitud 1 corre. Silencio Añádase el costo sólo cuando las " circunstancias " se conviertan en " 2 " , 10 " o " 100 " . Silencio
Silencio **Omitiendo el caso base de “deletrear el resto”** – DP nunca alcanza la longitud de `0` para sufijos totalmente delebles. Silencio Add `if (n-i <= rem) return 0;` early. Silencio
Silencio **Construir `next` incorrectamente** – utilizando `s[i]` en lugar de `s[cur]` en el bucle. Silencio Construir `next` de derecha a izquierda; utilizar `último[26]`. Silencio
**Utilización de la profundidad de recursión 100** – La recursión de pitón puede alcanzar el límite. TENIDO Aumentar el límite de recursión (`sys.setrecursionlimit(2000)`) o utilizar `@lru_cache`. Silencio
Silencio ** Actualizaciones de costos incorrectos** – agregando dígitos para '1` carreras de longitud. Sólo se actualizará cuando `ocurrencias ' está en `{2, 10, 100}`. Silencio

-...

## 8down Lo que significa para tu próxima entrevista

* **Mostrar DP state design** – explicar claramente las dos dimensiones.
* **Procesamiento previo de alta luz** – la construcción de la matriz "next" le salva de una solución cúbica.
* **La complejidad del debate** – `O(k·n2)` es aceptable aquí; si obtienes un límite de tiempo excedido comprobar si estás escaneando hacia adelante dentro del bucle DP.
* ** Casos de emergencia** – `k ≥ n` → respuesta es `0`.
`k = 0` → simplemente codifica la cadena original.

Este problema es un *must‐know* para cualquier persona que se ocupe de un rol de ingeniería de software senior o una entrevista de información-ciencia donde los problemas de LeetCode Hard son comunes.

-...

Pensamientos finales

*String Compression II* es más que simplemente “delete k caracteres”; se trata de *optimal run segmentation*.
Un DP limpio que respeta la relación “iguiente mismo carácter” es el corazón de la solución.

Si puede explicar el estado, la transición y la complejidad, impresionará a los entrevistadores y obtendrá la respuesta “Sí” en su currículum.

Buena suerte – ¡tienes esto! 🚀

-...

## 🔑 SEO Palabras clave

- Compresión de cuerda II**
# LeetCode Hard #
*Programación Dinámica*
- **Codificación de Rin-Length**
*Características* *
- Solución del DP de Java**
*Python DP Solution*
- **C++ DP Solution**
* Entrevista de codificación*
- Pregunta de interés**
*Job Interview Prep*
* Explicación de algoritmo* *
**Reto de codificación* *

Siéntete libre de compartir este post en LinkedIn, Medium o tu blog personal, está lleno de todos los reclutadores de palabras clave y los administradores de contratación adoran!