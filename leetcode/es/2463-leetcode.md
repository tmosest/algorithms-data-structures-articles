-...
Título: LeetCode 2463. Distancia total mínima viajada -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 2463 – Distancia total mínima Viajó
**Hard** – 100 % soluciones resueltas, **100 % aceptación**

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

Te dan

Silencioso `robot` Silencioso `factory' Silencio
Silencio...
Silencio `robot[i]` – la posición del eje X de robot *i*  durable `factory[j] = [posj, limitj] ` – posición y cuántos robots esta fábrica puede reparar

Todos los robots comienzan rotos y son libres de elegir ** una dirección (izquierda o derecha) al principio.
Se mueven a la misma velocidad, nunca chocan, y paran cuando llegan a una fábrica que todavía tiene una ranura de repuesto.
Si se alcanza el límite de una fábrica, el robot simplemente pasa por ella.

* Objetivo*
Establecer las instrucciones iniciales para que *todo* robot sea reparado y la distancia total viajada** es **minimo**.

■ **Constraints**
Ø • `1 ≤ robot.length, factory.length ≤ 100`
• `-109 ≤ robot[i], factory[j][0] ≤ 109 `
• `0 ≤ fábrica[j][1] ≤ robot.length `
* Siempre es posible reparar todos los robots.

-...

#### 2down⃣ Por qué parece difícil

Los robots son libres de caminar en cualquier dirección, y las fábricas tienen diferentes capacidades.
Un ingenuo “enviar cada robot a su fábrica más cercana” es incorrecto porque la capacidad de una fábrica puede ser agotada, obligando a un robot a ir más lejos.

La visión clave:
**Una vez que los robots y las fábricas se clasifican en el eje X, la asignación óptima siempre utilizará un * bloque contiguo* de robots para cada fábrica. * *
¿Por qué?
Mover un robot izquierda mientras un robot más cercano va a la derecha aumentaría la distancia total debido a la convexidad de la función de valor absoluto.

Con esta propiedad podemos resolver el problema mediante la programación dinámica sobre posiciones ordenadas.

-...

### 3down⃣ Solution Overview (DP)

1. **Sorta*
* `robots` – ascendiendo por posición
* `factorias' - ascender por posición

2. ** Estado de desplazados**
" dp[i][j] " - distancia total mínima para reparar los primeros robots " i " utilizando las primeras fábricas de " j " (se garantiza la reparación de todos los robots " i " ).

3. **Transición**
Por cada fábrica `j` decidimos cuántos de los últimos `k` robots (`k` de `0` a `limit[j]`) son reparados por él:

``text
dp[i][j] = min over k ( dp[i-k][j-1] + costo(robots[i-k+1 ... i] → factory[j]) )
`` `

4. **Costo**
"cost(l ... r → pos)` = eva vivrobots[p] – pos habit for p = l... r.
Desde `m ≤ 100`, podemos calcular esto en O(m) sobre la marcha; es barato y mantiene la implementación simple.

5. **Respuesta*
`dp[m][n]` donde `m = robots.size()` y `n = fábricas.size()`.

-...

### 4down⃣ Correctness Proof (Sketch)

*Lema 1 - Asignación contigua*
Para cualquier solución óptima, si los robots " a " b " se reparan por fábrica " f " y " d " ( " a " d " ) son reparados por otra fábrica, intercambiando " d " con " b " no puede aumentar la distancia total.
La prueba utiliza la desigualdad del triángulo y la convexidad de tenciónx – y sufrimiento.
Así una solución óptima se puede reordenar para que los robots asignados a una determinada fábrica forman un bloque contiguo.

*Lemma 2 – DP Recurrencia*
Assume we have repaired the first `i-k` robots using the first `j-1` factory excellently (`dp[i-k][j-1]`).
Adding factory `j` to repair robots `i-k+1 ... i ' produce una solución válida para los primeros robots ' i ' utilizando las primeras fábricas ' , y su costo es exactamente la expresión de transición.
Cualquier solución óptima debe construirse de esta manera debido a Lemma 1.
Por lo tanto, `dp[i][j]` almacena el coste óptimo para ese subproblema.

*Theorem* – `dp[m][n]` equivale a la distancia total mínima requerida para reparar todos los robots.
Mediante la inducción sobre " i " y " j " , el DP explora todas las asignaciones viables que respetan los límites de fábrica, y por Lemma 2 se considera cada asignación óptima.
Por lo tanto el algoritmo es correcto. ∎

-...

#### 5down⃣ Análisis de la complejidad

TEN TERRITORIO TEN TERRITORIDAD
Silencio...
Silencio Ordenar robots Silencio `O(m log m)` Silencio
TENIDO Fábricas de clasificación Silencio
Ø > Ø > ≤ > > 100 · 100 = 106 > Silencio
Silencio Cálculo de costos por transición TENIDO `O(m)` pero constante amortizada debido a pequeñas limitaciones TEN
Silencio **Total** Silencioso `O(106)` tiempo, `O(m · n)` memoria (~104) Silencio

Ambos están fácilmente dentro de los límites de Java, Python y C++.

-...

### 6down⃣ Edge Cases " Pitfalls

← Mala práctica tóxico Lo que va mal
Silencio--------------------------
Silencio No clasificar primero ¦ Assignments puede cruzar fábricas, conduciendo a soluciones sub-optimales o inválidas.
Silencio Olvídate de que un robot puede empezar *at* a una fábrica Silencio Perdiendo el caso de cero distancia ← Handle `resóbot - fábrica de vida = 0` automáticamente latitud
Silencio Usando una “fábrica de reposo” codicioso viola las limitaciones de capacidad, aumenta la distancia  durable Use DP como se describe ←
Silencio Over-optimizing cost calculation with complex math tención presenta fallos, difícil de leer Silencio Compute con un simple bucle; las limitaciones son minúsculas

-...

### 7فs Code Implementations

A continuación se muestran soluciones limpias y comentadas en **Java, Python y C++**.
Cada uno de ellos sigue el enfoque del DP esbozado anteriormente.

-...

#### 🔷 Java (Java 17)

``java
importar java.util*;

Solución de la clase pública {}
public long minimum TotalDistance(List seleccionadaInteger inteligente robot, int[][] fábrica) {
int m = robot.size();
int n = fábrica. longitud;

// 1. Ordenar robots y fábricas por posición
Collections.sort(robot);
Arrays.sort(factory, Comparator.comparingInt(a - título a[0]));

// Convertir robots en array para indexación rápida
long[] r = new long[m];
para (int i = 0; i)

// 2. Mesa del DP (para evitar el desbordamiento)
long[][] dp = new long[m + 1][n + 1];
para (int i = 0; i)
Arrays.fill(dp[i], Long.MAX_VALUE / 4);
dp[0][0] = 0;

// 3. Transición del DP
para (int j = 1; j)
int pos = factory[j - 1][0];
int limit = factory[j - 1][1];

para (int i = 0; i) {}
// considerar la asignación de robots k (0..limit) a esta fábrica
para (int k = 0; k) = límite " k " i; + k) {
largo prev = dp[i - k][j - 1];
si (prev == Long.MAX_VALUE / 4) continúan;

// costo de los robots móviles (i-k .. i-1) a esta fábrica
costo largo = 0;
para (int p = i - k; p i); ++p)
cost += Math.abs(r[p] - pos);

dp[i][j] = Math.min(dp[i][j], prev + cost);
}
}
}
dp[m][n];
}
}
`` `

-...

Python (Python 3.11)

``python
de la importación Lista
importar matemáticas

Solución de clase:
mínimo TotalDistance(self, robot: List[int], factory: List[List[int]) - int:
robot.sort()
factory.sort(key=lambda x: x[0])

m, n = len(robot), len(factory)
r = robot

INF = 10 ** 18
dp = [INF] * (n + 1) para _ en rango(m + 1)]
[0] [0] = 0

para j en rango(1, n + 1):
pos, limite = fábrica[j - 1]
para i en rango(m + 1):
para k en rango(limit + 1):
si k > i: descanso
si dp[i - k] [j - 1] == INF: continue
cost = sum(abs(r[p] - pos) for p in range(i - k, i)))
dp[i][j] = min(dp[i][j], dp[i - k][j - 1] + cost)

retorno dp[m][n]
`` `

-...

#### 🔗 C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
largo plazo mínimo TotalDistance(vector seleccionado] robot, vector asignadovector fieltro fábrica {
(robot.begin(), robot.end());
(factory.begin(), factory.end(),
[](cont vector identificadoint círculo a, const vector identificadoint círculo b){ return a[0] ■ b[0]; }

int m = robot.size(), n = factory.size();
vector llevado a cabo larga duración r(robot.begin(), robot.end());

const long INF = 4e18;
vector se llevó a cabo larga duración confianza dp(m + 1, vector se llevó mucho tiempo(n + 1, INF)
dp[0][0] = 0;

para (int j = 1; j)
int pos = factory[j-1][0];
int limit = factory[j-1][1];
para (int i = 0; i) {}
para (int k = 0; k) = límite " k " i; + k) {
si (dp[i-k][j-1] == INF) continúan;
long cost = 0;
para (int p = i-k; p < i; ++p)
cost += llabs(r[p] - pos);
dp[i][j] = min(dp[i][j], dp[i-k][j-1] + cost);
}
}
}
dp[m][n];
}
};
`` `

■ **Nota:**
■ Las tres implementaciones emplean un bucle triple, pero permanecen cómodamente dentro del presupuesto de operación **106** porque `m, n ≤ 100`.

-...

#### 8down⃣ Lo que hace que esta solución se destaque

Silencio**
Silencio--------------------------
Silencio • DP intuitivo después de ordenar. Silencio • Olvídate de las coordenadas negativas – puede llevar a la desbordación o a resultados incorrectos. Silencio • El manejo de capacidades puede ser sutil: una fábrica puede reparar robots **cero**, por lo que debemos permitir `k = 0`. Silencio
Silencio • Costo computado con un simple bucle – ninguna matemática difícil. Silencio • Greedy “fábrica de seguridad” es tentador pero incorrecto. Silencio • Mucha gente sobre-optimiza DP y hace que el código no esté disponible. Silencio
Silencio • Funciona en todos los idiomas principales con memoria extra mínima. Silencio • No usar `long` / `long' puede desbordarse en grandes coordenadas. Silencio • Mixing indices (`1-based` vs `0-based`) puede ser confuso. Silencio

-...

#### 8down⃣ Bono: Costo más rápido (Opcional)

Si desea reducir el factor constante, puede pre-computar sumas de prefijo de posiciones de robot y luego utilizar la fórmula

`` `
cost(l ... r → pos) =
(pos * k) - (prefix[r] - prefijo[l-1]) si los robots están a la izquierda de pos
(prefix[r] - prefijo[l-1]) - (pos * k)
`` `

pero para los límites dados el bucle simple es **clearer** y menos error-prone.

-...

#### 9Ω⃣ SEO Cheat‐ Sheet

Silencio Palabra clave Silencioso
Silencio...
Silencioso `leetcode 2463` Silencio Título, problema enlace, código comentario Silencio
Silencio `minimum total distance traveled` Silencio Header, descripción del problema  sometida
Silencioso `programación dinámica ' Vista general de la solución, sección DP
Silencioso `java python c++ Solución ' ¦
problema de fábrica de robots TENCIÓN Ejemplo, sección de periferia
Silencio `reparación de robots ' Problema de vida narrativa

Añadir estos a su blog, artículo, o README y usted clasificará para cada búsqueda que un LeetCoder hace en este rompecabezas!

-...

### 10VIEW⃣ TL;DR

* Ordenar robots y fábricas → DP sobre posiciones ordenadas → Transición: “asignar los últimos robots k a la fábrica actual” → O(106) tiempo, O(104) memoria.
Los tres principales idiomas: **Java, Python, C+** – listo para copiar.

Bien.
Mal.
Genial.
Ahora es todo **DONE**!

¡Feliz codificación, y que su distancia total permanezca mínima!