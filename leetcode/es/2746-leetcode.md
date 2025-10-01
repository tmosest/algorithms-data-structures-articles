-...
Título: LeetCode 2746. Decremental String Concatenation -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Decremental String Concatenation – 2746
## A Complete Java / Python / C++ Solution + SEO‐Optimized Blog Post to Boost Your Job Hunt

-...

## Tabla de contenidos

Silencio Sección Silencio Lo que aprenderás
Silencio...
Silencio 1. Problema Resúmenes Silencio Lo que el problema LeetCode pide realmente para la vida
Silencio 2. Brute‐Force vs. DP TEN ¿Por qué la solución ingenua falla y por qué DP brilla
Silencio 3. The “Good” – The Optimal DP Approach tención State design, transition, and implementation details
Silencio 4. The “Bad” – Common Pitfalls TENED-por-uno errores, soplado de memoria, manejo innecesario de cuerdas
Silencio 5. The “Ugly” – Edge Cases " Debugging  durable Handling single-word arrays, duplicate letters, etc. Silencio
Silencio 6. Código de idiomas múltiples Silencio Java, Python, C++ – los tres en un archivo ←
Silencio 7. SEO > Cuidador Consejos Silencio Cómo este artículo puede conseguir que usted note por los reclutadores
Silencio 8. TL;DR TENIDO Sábanas trampa rápidas

-...

## 1. Panorama general de los problemas

LeetCode 2746 – ** “Concatenación de cuerdas ornamentales”** –
Dado un array `palabras[]` de `n` cadenas de minúsculas, tenemos que realizar `n-1` operaciones de unión:

- `join(x, y)` = `x + y` **unless** el último char de `x` equivale al primer char de `y`; luego eliminamos * uno* de esos caracteres duplicados (la unión todavía produce una cuerda válida).
- En el paso `i` podemos anexar `palabras[i]` después de la cadena actual o prependiéndola.

** Objetivo**: minimizar la longitud de la cadena final concatenada.
`1 ≤ n ≤ 1000, 1 ≤ las palabras de vida [i] sometida ≤ 50`.

-...

## 2. Brute‐Force vs. DP

¿Te acercas a las personas que viven en el tiempo? Silencio
Silencio--------------------------------------
Silencio Enumerate all 2^(n‐1) unirse a pedidos + mantener toda la cadena Silencio O(2^n * n * L) Silencio O(L) ❌ – TLE for n=1000 Silencio
Silencio DP over **full string** (memoizing the exact string) Silencio O(n * 50 * 2^n) Silencio O(n * 2^n * 50) Silencio ❌ – exponential Silencio
Silencio DP over **start < end characters** Silencio **O(n · 262)** Silencio **O(n · 262)** Silencio ↑

La visión clave: el contenido *exacto* de la cadena intermedia nunca importa, sólo sus primeros y últimos caracteres y su longitud. ¿Por qué?
Cuando nos unimos a dos cuerdas, la única superposición posible es el par *adjacent* de caracteres – el último char de la cuerda izquierda y el primer char de la cuerda derecha. Todos los demás personajes no son afectados. Así, un DP 3dimensional ( ' dp[i][s][e] ' ) es suficiente.

-...

## 3. El “bien” – Optimal DP Approach

#### State

`dp[i][s][e]` – minimal **extra** longitud agregada concatenando palabras `i ... n-1` si la cadena actual (ya construida) comienza con `s` y termina con `e`.
- `s, e  Iberia {0 ... 25}` (indices de letras 'a'‐'z').
- La longitud *total* al final es `totalSum – maxReduction`, donde `totalSum` es la suma de todas las longitudes de la palabra.
- `maxReduction` es el número de caracteres duplicados que logramos eliminar.

### Transition

Que la siguiente palabra sea `w = palabras[i]` con el primer char `cs` y el último char `ce`.

1. **Anexo después** (corte actual + w)

- Nuevo comienzo = `s` (sin cambios).
- Nuevo final = "ce".
- Si `e == cs`, eliminamos un carácter ⇒ **+1** duplicado.
- Else ⇒ **0** duplica.

2. **Preparado antes** (w + cadena actual)

- Nuevo comienzo.
- New end = `e`.
- Si `ce == s`, eliminamos un carácter ⇒ **+1** duplicado.
- Else ⇒ **0** duplica.

El DP elige el recuento duplicado *maximum* (porque estamos maximizando las eliminaciones, que equivalen a minimizar la longitud final).

`` `
dp[i][e] = max(
(e==cs? 1 : 0) + dp[i+1][s][ce],
(ce==s ? 1 : 0) + dp[i+1][cs][e]
)
`` `

### Initialization

`dp[0][firstWord] [lastWord] = 0` – empezamos con la primera palabra; todavía no hay duplicados adicionales.

### Resultado

Después de llenar la tabla, la respuesta es

`` `
minLength = totalSum - max(dp[0][first][last] for all first,last)
`` `

Porque `dp[0][first][last]` ya contiene los duplicados *maximum* que se pueden lograr cuando se procesa todo el array.

### Complexity

- **Tiempo**: `O(n · 262)` ♥ `6.7 × 105` operaciones para n=1000.
- **Espacio**: igual, alrededor de 676 k enteros ♥ 3 MB.

-...

## 4. El “Bad” – Pitfalls comunes

Por qué duele la vida Arreglarse
Silencio--------------------------
Silencio **Usando cadenas enteras** en las teclas DP ← Memoria exponencial (estring hashing) Silencio Únicamente almacenar primero/últimos charcos Silencio
Silencio **Off‐by-one indices** for `i` in the loop ← Dirección de transición incorrecta Silencio Inicio de i=1 (desde que la palabra 0 está fijada)
Silencio **Asumiendo que la eliminación siempre reduce la longitud** Silencioso cuando los charcos difieren Silencio Revisar la igualdad explícitamente
Silencio **Utilización de la recursión sin memoización** Silencio Rebosa de Stack por 1000 palabras Silencio Uso iterante DP o top-down + memo Silencio
Silencio **No restar 1 del totalSum** cuando se elimina un duplicado ← Sobre-cuenta la longitud ← Mantener una `reducción` contrarrespuesta independiente

-...

## 5. El “Ugly” – Edge Cases " Debugging

← Edge Silencio Por qué importa ¦ Debug tip ←
Silencio...
Silencio `n = 1` Silencio No te unas, responde = `len(word0)` Silencio Regreso temprano
Silencio Palabras que comienzan y terminan con la misma letra (por ejemplo, “aaa”) Silencio Puede eliminar **dos** duplicados si se adjuntan a ambos lados Silencio La transición DP maneja ambos lados por separado
← Duplicar letras en el interior de una palabra (por ejemplo, “abba”)
Silencio Todas las palabras iguales a un carácter único (“a”, “a”, ...) Silencio Cada uno elimina un duplicado Silencio DP todavía funciona – `maxReducción = n-1` Silencio

**Debugging tip**: print `dp[i][s][e]` for small `n` (≤ 5) and verify against brute‐force enumeration to ensure transitions are correct.

-...

## 6. Lenguaje múltiple Código

A continuación encontrará **tres** soluciones completas, autocontenidas – una para cada uno de los idiomas de entrevista más populares.

``txt
# Nombre del archivo: 2746_DecrementalStringConcatenation.cpp
# Compile: g++ -std=c+17 -O2 -pipe -static -s -o sol 2746_DecrementalStringConcatenation.cpp
# Run: ./sol

- Sí.
* 1️ LeetCode 2746 – Decremental String Concatenation
* 2️ DP over first/last characters (O(n·262))
* 3️ Java, código Python & C++ en un archivo
- Sí.

#include יbits/stdc++.h
usando std namespace;

// ------ C++ ------
Clase CppSolution {}
public:
int minimizeConcatenated Longitud(vector seleccionador) {}
int n = words.size();
total = 0;
para (auto &w: words) total += (int)w.size();

si (n == 1) devuelve palabras [0].size();

// dp[i][s][e] = duplicados máximos de i.n-1 con inicio s, final e
INF_NEG = -1e9;
vector realizadoarray realizadoarray realizado,26 título,26 título dp(n, {});
para (int s=0;s obtenidos26;s+)
para (int e=0;e obtenidos26;e+)
dp[0][e] = INF_NEG;

// Inicializar con primera palabra
int fs = words[0] [0] - 'a';
int fe = words[0].back() - 'a';
para (int s=0;s obtenidos26;s+)
para (int e=0;e obtenidos26;e+)
dp[0][e] = INF_NEG;
dp[0][fs][fe] = 0; // no duplicates yet

para (int i=1;i obtenidos;i+) {
array observadoarray identificado,26 caracteres,26 títulos = dp[i-1];
para (int s=0;s obtenidos26;s+)
para (int e=0;e obtenidos26;e+)
ndp[s][e] = INF_NEG;

cadena const curva w = palabras[i];
int cs = w[0] - 'a';
int ce = w.back() - 'a';

para (int s=0;s obtenidos26;s+) {}
para (int e=0;e obtenidos26;e+) {
int cur = dp[i-1][s][e];
si (cur == INF_NEG) continúan;

// 1. Apéndice después
int add1 = (e == cs) ? 1 : 0;
ndp[s][ce] = max(ndp[s][s], cur + add1);

// 2. Prepensión antes
int add2 = (ce == s) ? 1 : 0;
ndp[cs][e] = max(ndp[cs][e], cur + add2);
}
}
dp[i] = ndp;
}

int best = 0;
para (int s=0;s obtenidos26;s+)
para (int e=0;e obtenidos26;e+)
mejor = max(best, dp[n-1][s][e]);

retorno total - mejor;
}
};

// ------ Python ------
clase PythonSolution:
def minimizeConcatenated Duración (auto, palabras: list[str]) - int:
n = len(palabras)
total = suma(len(w) para w en palabras)
si n == 1:
len(words[0])

# dp[i][es] = duplicados máximos de i.n-1
dp = [[ -1 for _ in range(26)] for _ in range(26)] for _ in range(n)]
fs, fe = ord(words[0][0]) - 97, ord(words[0] [-1]) - 97
dp[0][fs][fe] = 0

para i en rango(1, n):
cs, ce = ord(words[i][0]) - 97, ord(words[i] [-1]) - 97
new_dp = [[-1]*26 for _ in range(26)]
para s en rango(26):
para e en rango(26):
cur = dp[i-1][s][e]
si se cura == -1: continuar

# Append after
add1 = 1 si e == cs 0
new_dp[s][ce] = max(new_dp[s] [ce], cur + add1)

# Prependiendo antes
add2 = 1 if ce == s else 0
new_dp[cs][e] = max(new_dp[cs][e], cur + add2)

dp[i] = new_dp

mejor = 0
para s en rango(26):
para e en rango(26):
mejor = max(best, dp[n-1][s][e]

total de retorno - mejor

# ------ Java ------
/*
* Java 17 – Decremental String Concatenation (LeetCode 2746)
* Tiempo: O(n · 262) Espacio: O(n · 262)
*/
clase pública JavaSolution {}
public int minimizeConcatenated Longitud(String[] palabras) {
int n = words.length;
total = 0;
for (String w : words) total += w.length();
si (n == 1) devuelve palabras [0].length();

int[][][] dp = nuevo int[n][26];
para (int i = 0; i)
para (int s = 0; s)
Arrays.fill(dp[i][s], -1);

int fs = words[0].charAt(0) - 'a';
int fe = words[0].charAt(words[0].length() - 1) - A;
dp[0][fs][fe] = 0;

para (int i = 1; i) {}
int cs = words[i].charAt(0) - 'a';
int ce = words[i].charAt(words[i].length() - 1) - A;
int[][] siguiente = nuevo int[26][26];
para (int s = 0; s)
Arrays.fill(next[s], -1);

para (int s = 0; s) {}
para (int e = 0; e)
int cur = dp[i - 1][s][e];
si (cur == -1) continúan;

// Apéndice después
int add1 = (e == cs) ? 1 : 0;
siguiente[s][ce] = Math.max(next[s][s], cur + add1);

// prepensión antes
int add2 = (ce == s) ? 1 : 0;
siguiente[cs][e] = Math.max(next[cs][e], cur + add2);
}
dp[i] = siguiente;
}

int best = 0;
para (int s = 0; s)
para (int e = 0; e)
mejor = Math.max(best, dp[n - 1][s][e]);

retorno total - mejor;
}
}

// ------ Conductor ------
int main() {}
// C++ demo
CppSolution cpp;
vector asignado palabras clave_cpp = {"ab", "ba", "ab"};
cout se realizó la respuesta "C+++: "

// Python demo
PythonSolution py;
Lista de palabras: "B", "ba", "ab"
System.out.println("Python answer: " + py.minimizeConcatenatedLength(words_py));

// Java demo
JavaSolution java;
String[] words_java = {"ab", "ba", "ab"};
System.out.println("Java answer: " + java.minimizeConcatenatedLength(words_java));
}
`` `

**Nota**: Para la presentación real de LeetCode, suba la clase relevante (Java, Python o C++) solo; el resto es sólo para su comodidad.

-...

## 7. 📚 Qué tomar Away

1. **Transformar el problema**:
*De* “mínima longitud”
*To* “maximize deletions” → más simple DP.

2. **Keep DP declara mínimo**: primeros/últimos chars, no cadenas enteras.

3. **Maximizar duplicados** (no minimizar) en el DP para lograr la minimización final.

4. **Siempre doble comprobación** casos de borde con fuerza bruta para pequeñas entradas.

5. **Write clean, modular code** – las soluciones anteriores funcionan en cualquier entorno de codificación.

-...

## 7Ω⃣ TL;DR (Takeaway for Interviews)

- Usar un DP **2-D** sobre caracteres `primer' y `últimos.
- La transición agrega una eliminación sólo cuando los faros coinciden.
- Maximizar las eliminaciones → minimizar la longitud.
- La complejidad es trivial para n=1000: ~7 × 105 operaciones.
- Evite las teclas DP de acceso completo; utilice arrays enteros.

¡Buena suerte en tu próxima entrevista! 🚀
`` `

-...

## 7. TL;DR (Takeaway for Interviews)

1. *Key Insight*
Reducir el estado a los primeros y últimos caracteres de cada palabra.
2. **DP Formulation**:
Maximizar el número de eliminaciones (duplica) en lugar de contar la longitud.
3. ** Resultado**:
`finalLength = totalSum - maxDuplicates`.
4. **La complejidad**:
`O(n · 262)` tiempo y espacio – se ajusta fácilmente a las limitaciones de 1 segundo.

-...

## Final Thought

Dominar este problema aumentará su confianza en manejar tareas de *estring DP*. El mismo enfoque (estados → bordes, max/min, iterative DP) se puede reutilizar para otros problemas de estilo “maximum deletion” como **minimum adyacente swaps** o **optimal concatenations**.

¡Feliz codificación! ▪