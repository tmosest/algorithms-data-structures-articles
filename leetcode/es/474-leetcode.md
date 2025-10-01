-...
Título: LeetCode 474. Unos y ceros -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🧩 LeetCode 474 – *Ones and Zeroes*
### The Good, The Bad, and The Ugly – A Job‐ Interview‐ Guía lista

■ **Keywords**: LeetCode 474, Ones and Zeroes, programación dinámica, knapsack, entrevista de trabajo, ingeniero de software, algoritmo, entrevista de codificación, desafío de codificación, estructuras de datos, DP 2-dimensional, preparación de entrevista, curriculum vitae, Java, Python, C++

-...

Declaración de problemas

Le han dado una serie de cadenas binarias `strs` y dos enteros `m` y `n`.
Encuentra el tamaño del subconjunto más grande de `estrs` tal que el subconjunto contiene ** en la mayoría de `m` ceros** y ** en la mayoría de `n` s**.

`` `
Entrada:
strs = ["10","0001","111001","1"0"]
m = 5
n = 3

Producto:
4 // {"10","0001","0"} es el subconjunto óptimo
`` `

← Constraints
Silencio...
← ≤ strs.length ≤ 600
Ø 1 ≤ strs[i].length ≤ 100
Silencioso strs[i] consiste sólo en '0' y '1'
TENIDO 1 ≤ m, n ≤ 100

-...

#### 2down⃣ ¿Por qué este problema marca su cartera de entrevistas

TENIDO FACTURO ANTERIOR Por qué importa
Silencio...
Silencio **Classic 0/1 Knapsack** Silencio Muchas empresas piden variaciones del problema de la mochila. Probar que puede adaptarlo a una capacidad bidimensional muestra comprensión profunda del DP. Silencio
tención **DP State‐Space Reduction** ← From `O(L * m * n)` to `O(m * n)` by iterating backs. Este cambio es un patrón favorito en las entrevistas de codificación. Silencio
Silencio **Edge‐Case Handling** ← Requiere contar ceros/ones, manejar grandes entradas, y asegurar que no se desborde – todas las buenas pruebas “clean-code”. Silencio
Silencio **Multi‐Language Mastery** Silencio Mostrando el mismo algoritmo en Java, Python y C++ demuestra el pensamiento de algoritmos lingüísticos-agnósticos – un gran plus en los equipos de varios bloques. Silencio

* Tip* Los términos de búsqueda como "LeetCode 474 solución", "Ones and Zeroes dynamic programming", y "0/1 knapsack interview question" son palabras clave que los reclutadores utilizan al escanear los blogs candidatos.

-...

Intuición de la llave

Piense en el problema como una mochila de dos dimensiones**:

- **Dimensiones de peso:** número de ceros (`0`) y número de uno (`1`).
- *Capacidad: * `m` ceros and `n` ones.
- **Valor de imagen:** cada cadena contribuye `1` al tamaño total del subconjunto.

Puede incluir o excluir cada cadena exactamente una vez – lógica clásica 0/1 knapsack.

**Key trick**: Iterate **backwards** al actualizar la tabla DP para evitar volver a utilizar la misma cadena varias veces.

-...

Algoritmo (Bottom‐Up DP)

``text
dp[z][o] = tamaño máximo del subconjunto utilizando a la mayoría de z ceros y o

para cada cuerda s en púas:
z0 = cuenta de '0' en s
o1 = cuenta de '1' en s
para z de m a z0:
para o desde n hasta o1:
dp[z][o] = max(dp[z][o], dp[z - z0][o - o1] + 1)

retorno dp[m][n]
`` `

**La complejidad* *

- **Tiempo: ** `O(L * m * n)` donde `L = strs.length`.
- **Espacio: ** `O(m * n)` (2‐D array).

Los lazos atrasados aseguran que cada cadena se utiliza a la mayor parte de una vez, convirtiendo el DP 3-D en un DP 2-D.

-...

#### 5down⃣ Código (Java, Pitón, C++)

##### 5.1 Java

``java
// LeetCode 474 – Ones and Zeroes (Java)
Solución de la clase pública {}
public int findMaxForm(String[] strs, int m, int n) {
int[][] dp = nuevo int[m + 1][n + 1];

para (String s : strs) {
int[] cnt = countZerosOnes(s);
int ceros = cnt[0];
int one = cnt[1];

// Iteración posterior asegura comportamiento 0/1
para (int z = m; z >= ceros; z--) {}
para (int o = n; o >=es; o--) {}
dp[z][o] = Math.max(dp[z][o], dp[z - ceros] [o - ones] + 1);
}
}
}
dp[m][n];
}

int privado[] Cuenta ZerosOnes(String s) {
int[] c = nuevo int[2];
(int i = 0; i) s.length(); i++) {
c[s.charAt(i) - '0']+; // '0' - índice de confianza 0, '1' - índice de confianza 1
}
c) Retorno c;
}
}
`` `

#### 5.2 Python

``python
LeetCode 474 – Unos y Cero (Python 3)
Solución de clase:
def findMaxForm(self, strs: List[str], m: int, n: int) - título int:
dp = [0] * (n + 1) para _ en rango(m + 1)]

para s en strs:
ceros, unos = s.count('0'), s.count('1')
para z en rango(m, ceros - 1, -1):
para o en rango(n, uno - 1, -1):
dp[z][o] = max(dp[z][o], dp[z - ceros][o - ones] + 1)

retorno dp[m][n]
`` `

#### 5.3 C++

``cpp
// LeetCode 474 – Unos y ceros (C++)
Clase Solución {
public:
int findMaxForm(vector identificadosstring consigo strs, int m, int n) {
vector seleccionado(n + 1, 0)

para (la cuerda contigua : strs) {
int ceros = 0, uno = 0;
para (cara c : s) {}
si (c == '0') ceros++; otros más++;
}

para (int z = m; z ceros; --z) {
para (int o = n; o не=es; --o) {
dp[z][o] = max(dp[z][o], dp[z - ceros] [o - ones] + 1);
}
}
}
dp[m][n];
}
};
`` `

-...

### 6down⃣ Edge Cases " Common Pitfalls

Silencioso asunto confidencialidad Lo que fue incorrecto
Silencio...
Silencio **Off‐by‐one** in DP indices TENIDO Utilizando "z "= ceros " pero accediendo a " dp[z - ceros " puede ir negativo ¦ Loop desde `m` hasta `zeros`, inclusive
Silencio **Large input strings** Silencio Contando ceros/ones a través de `s.count('0')` en Python es O(length) Silencio Todavía necesario; tiempo total limitado por las restricciones
Silencio **Desbordamiento entero** Silencio No hay problema en Java/Python; C++ utiliza `int` (fits 32-bit) Silencio Asegurar capacidades `m, n  won= 100` → safe 
Silencio ** cuerda vacía** Silencioso `cuenta('0')` y `cuenta('1')` son 0 → todavía válido Silencio Código lo maneja naturalmente
Silencio **Tiempo límite** Silencio Los bucles anidados `L*m*n` pueden golpear 6 operaciones e7 en el peor de las vidas Aceptables para 1 s límite en la mayoría de los jueces; considerar la poda si `m` o `n` pequeña latitud

-...

### 7 Cambios en la entrevista—Ley Tips

1. ** Explique la analogía de 2-D DP**: “Estamos empacando una bolsa que puede contener ceros X y Y. ”
2. **Mostrar hacia atrás iteración**: “Esto asegura que cada cadena se utilice una vez. ”
3. **La complejidad del debate**: "O(Lmn) time, O(mn) space; con `m,n≤100 ` está bien. ”
4. ** Optimizaciones de la mención**: “Si contamos con ceros/ones pre-compute, evitamos reescanear cada cadena. ”
5. ** legibilidad de alta luz**: “Clear nombres variables (“zeros”, “ones”) y métodos de ayuda ayudan a mantener la capacidad. ”

-...

### 8️ Bonus – Top-Down Memoization (Optional)

``java
// Java versión memoizada
public int findMaxFormMemo(String[] strs, int m, int n) {
int[][] memo = nuevo int[m+1][n+1];
for (int[] row : memo) Arrays.fill(row, -1);
dfs (estrs, 0, m, n, memo);
}

int privado dfs(String[] strs, int idx, int ceros, int ones, int[] memo) {
si (idx == strs.length) devuelve 0;
si (memo[zeros] [ones] != -1) devolver memo[zeros][ones];

int z = strs[idx].chars().filter(c - título c == '0').count();
int o = strs[idx].chars().filter(c - título c == '1').count();

int exclude = dfs(strs, idx+1, ceros, uno, memo);
int include = 0;
si
incluir = 1 + dfs(estrs, idx+1, ceros - z, uno - o, memo);

devolver memo[zeros][ones] = Math.max(excluir, incluir);
}
`` `

-...

#### 9Ω Final Final Take‐ Away

- **Problema**: 2-D 0/1 knapsack (zeros) → DP clásico.
- **Solución**: PD con bucles hacia atrás → `O(L*m*n)` tiempo, `O(m*n)` espacio.
- **Por qué importa**: Demuestra programación dinámica, espacio/tiempo, y codificación limpia en Java/Python/C++.
- **Job‐Interview Impact**: Talk about knapsack intuition, complex, edge cases, and language-agnostic thinking to impress hiring managers.

■ **SEO CTA:** *Si quieres dominar LeetCode 474 y aterrizar tu papel de ingeniería de software de sueño, bucear en este post, practicar los fragmentos de código, y compartir tus propias variaciones en GitHub. Seguir para obtener más información sobre DP, preparación de entrevistas y consejos de crecimiento profesional! *

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀