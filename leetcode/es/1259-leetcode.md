-...
Título: LeetCode 1259. Handshakes That Don't Cross -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1down⃣ Handshakes That Don't Cross – 1259
### 🔍 Resumen del problema (LeetCode)

■ Se le da incluso a un número de personas "num People" de pie en un círculo.
■ Cada persona sacude las manos con exactamente otra persona, por lo que hay 'numPeople/2` apretones de manos en total.
■ Cuenta el número de formas distintas para realizar los apretones de manos **sin ningún cruce de dos apretones de manos**.
■ Devuelve el modulo de respuesta **1 000 000 007**.

**Constraints* *

Silencios humanos Silencio min Silencio máx.
Silencio--------------------------
Ø 2 ≤ numPersonas ≤ 1000 Silencio 2

El ejemplo
- `num People = 4 → 2`
- `num People = 6 → 5`

-...

## 2down Las matemáticas detrás de la respuesta – Números catalanes

Si dibujas a la gente alrededor de un círculo y conectas pares de apretón de manos con líneas rectas, la condición de no cruzar significa que las líneas forman un **no cruzar el juego perfecto** en un polígono convexo.

El número de tales coincidencias para un polígono convexo con vértices de 2k es exactamente el número **k‐th catalán**:

\[
C_k = \frac{1}{k+1}\binom{2k}{k} = \sum_{i=0} {k-1} C_i \cdot C_{k-1-i}
\]

Así que por el problema sólo necesitamos
\[
\text{answer} = C_{\,numPeople/2} \pmod{1\,000\,007}
\]

-...

## 3Ω⃣ Solución de programación dinámica (O(n2))

En lugar de computar coeficientes binomiales e inversos modulares (que también está bien), podemos construir los números catalanes con una recurrencia clásica DP:

`` `
dp[0] = 1 // polígono vacío
dp[2] = 1 // un apretón de manos
para mí de 4 a n paso 2:
dp[i] = 0
para j del 2 al i-2 paso 2:
dp[i] += dp[j] * dp[i-j] (mod M)
`` `

**Por qué funciona* *
- Par a la primera persona con alguien en la posición `j`.
- Las personas entre ellas forman un polígono más pequeño de vértices.
el resto forma un polígono de vertices 'i-j'.
- Multiplicar el número de formas para ambas partes y suma sobre todas las cosas válidas.

**La complejidad* *

Silencio Silencio Silencio Silencio
Silencio----------------
Silencioso bucle exterior TENIDO \(O(n/2)\) Silencio
← Inner loop Silencio \(O(n/2)\)
TENIDO Total TENIDO \(O(n^2)\) Silencio

Con `n ≤ 1000`, `O(n2)` (con 500 000 iteraciones) es trivial.

-...

## 4down Implementaciones de referencia

A continuación se presentan implementaciones limpias y listas para copiar en **Java**, **Python**, y **C+**.
Todos son `O(n2)` y manejan correctamente el modulo.

■ **Tip:**
■ En Java y C+ utilizan `long long`/`int64_t` durante la multiplicación para evitar el desbordamiento.
■ En Python `int` es la precisión arbitraria, por lo que es más simple.

-...

#### 4.1 Java

``java
importa java.io.*;
importar java.util*;

Clase Solución {
static final long MOD = 1_000_000_007L;

público número DeWays(int n) {
// n está garantizado ser uniforme
long[] dp = new long[n + 1];
dp[0] = 1;
dp[2] = 1;

para (int i = 4; i) = n; i += 2) {
larga suma = 0;
para (int j = 2; j 2) {
suma = (sum + dp[j] * dp[i - j]) % MOD;
}
dp[i] = sum;
}
dp[n];
}
}
`` `

**Cómo funcionar (prueba rápida): * *

``java
clase pública Principal {}
public static void main(String[] args) {
Solución s = nueva solución ();
System.out.println(s.numberOfWays(4)); // 2
System.out.println(s.numberOfWays(6)); // 5
}
}
`` `

-...

#### 4.2 Python

``python
MOD = 1_000_000_007

def number_of_ways(n: int) - título int:
# N es incluso
dp = [0] * (n +1)
dp[0] = 1
dp[2] = 1

para i en rango(4, n + 1, 2):
total = 0
para j en rango(2, i, 2):
total = (total + dp[j] * dp[i - j] % MOD
dp[i] = total

retorno dp[n]


si __name_ == "__main__":
print(number_of_ways(4)) # 2
print(number_of_ways(6)) # 5
`` `

-...

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

const long MOD = 1'000'000'007LL;

int numberOfWays(int n) {
vector de largo plazo dp(n + 1, 0);
dp[0] = 1;
dp[2] = 1;

para (int i = 4; i) = n; i += 2) {
long long total = 0;
para (int j = 2; j 2) {
total = (total + dp[j] * dp[i - j]) % MOD;
}
dp[i] = total;
}
volver estática_cast seleccionado(dp[n]);
}

int main() {}
cout Identificado númeroOfWays(4)
cout Identificado númeroOfWays(6) se realizó endl; // 5
}
`` `

-...

## 5down Blog Post: “Handshakes That Don't Cross – The Good, The Bad, and the Ugly”

-...

### 5.1 Headline & Meta-Description (SEO‐Ready)

■ **Título:** Handshakes That Don't Cross – Un simple DP a Ace LeetCode 1259
■ **Meta‐Description:** Aprenda las matemáticas detrás del problema del apretón de manos sin cruzar, vea las soluciones de Java/Python/C++, y consiga entrevistas con snippets de código claro. Perfecto para su próxima entrevista técnica!

-...

### 5.2 Introduction

■ Imagínate a un grupo de amigos de pie en un círculo, cada uno sacudiendo las manos con exactamente otro. ¿Cuántas maneras pueden hacer esto sin que crucen los apretones de manos? Esta pregunta engañosamente simple es un problema duro clásico de LeetCode (#1259) y una gran trampa de entrevista.
■ En este artículo, vamos a diseccionar el problema, explicar por qué la respuesta es un número catalán, mostrar una implementación DP limpia, y darle tres soluciones listas para copiar en **Java**, **Python**, y **C+**. A lo largo del camino, hablaremos de lo bueno, lo malo y lo feo de diferentes enfoques para que puedas elegir el correcto para tu entrevista o desafío de codificación.

-...

### 5.3 The Good – Why DP is a Natural Fit

- **Recurrencia de línea** – Cada par de apretones de manos divide el círculo en dos sub-circles independientes.
*Evita la Pitfall Combinatorics* – No se puede contar con todos los apretones de manos y cruces de subtractos; la estructura combinatoria es no-trivial.
- ** Tiempo-Eficiente** – `O(n2)` es fácilmente rápido para `n ≤ 1000`.
- **Amigo Aritmético Moderno** – Trabaja con un solo módulo (`1 000 000 007`).

-...

### 5.4 Los malos – Mis pasos comunes

TENCIÓN ANTERIOR ANTERIOR Por qué Fails ANTE
Silencio...
TEN **Usando factoriales sin inversos modulares** Silencio Rebosarás y necesitarás computar inversos modulares, lo que añade complejidad innecesaria. Silencio
Silencio **Asumiendo que todos los emparejamientos son válidos** Silencio Ignorar la restricción “no cruzada” conduce a configuraciones astronómicamente muchas inválidas. Silencio
Silencio **O(n3) fuerza bruta** Silencio Incluso con la poda, 1000 personas dan ~109 iteraciones—imposible en el tiempo. Silencio
Silencio **Using `int` for multiplication in Java/C++** Silencio `dp[j] * dp[i-j] puede exceder el rango de 32 bits; use `long ' / `long`.

-...

## 5.5 El Ugly – ¿Por qué “Números Catalán” podría ser exagerado

- ** Complejidad Coeficiente Binomial** – Complejidad \(C_k\) vía \(\frac{1}{k+1}\binom{2k}\) requiere inversas modulares y pre-computación factorial.
*Potential Off‐By-One Errores * – Manejar índices de `k ' vs. `k-1` puede acercarte.
- **Less Intuitive for Interviewers** – Algunos entrevistadores pueden preferir ver la lógica DP desplegándose en lugar de una fórmula de un solo sentido.

-...

### 5.6 Final Takeaway

Un DP conciso que refleja la estructura combinatoria del problema es la solución más segura, rápida y más fácil de entrevista. Evita los obstáculos, permanece dentro de los límites de tiempo, y demuestra claramente su comprensión de la recursión y la aritmética modular.

-...

### 5.7 Bono – Consejos de rendimiento

- **Pre-allocate arrays** una vez; no repetida asignación de memoria en bucles.
- **Use `long long'** (C++), `long` (Java), o incorporado `int` (Python) para evitar el desbordamiento.
- **Mod después de cada adición/multiplicación** para mantener los números pequeños.
- **Si estás preparado para un reto**: computar los números catalanes en `O(k)` utilizando un solo bucle con la fórmula \(C_{k+1} = \frac{2(2k+1)}{k+2}C_k\) e inversos modulares; esta es una gran entrevista “ credito extra” movimiento.

-...

Pensamientos de clausura

■ El problema “Handshakes That Don't Cross” es una combinación perfecta de combinatoria, recursión y aritmética modular. Dominar no sólo le da una solución O(n2) limpia, sino que también demuestra una profunda comprensión de cómo un rompecabezas aparentemente simple esconde una estructura clásica catalana.
■ Mantenga los fragmentos de código útiles, practique explicando el razonamiento DP, y estará listo para impresionar a su próximo reclutador o as de la entrevista de codificación. ¡Feliz codificación!

-..