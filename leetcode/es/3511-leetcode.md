-...
Título: LeetCode 3511. Hacer un rayo positivo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📈 Make a Positive Array – 3511
**LeetCode – Medium – O(n) Greedy + Prefix Sum**
*Se le permite reemplazar cualquier elemento con cualquier entero entre \(-10^{18}\) y \(10^{18}\).
Encuentra el número mínimo de reemplazos necesarios para hacer la matriz “positiva”. *

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

■ Un array es **positivo** si *todo* sub-arrayo de longitud **≥ 3** tiene una suma **positiva**.
■
■ Puede realizar la siguiente operación en cualquier número de veces:
■ Reemplazar un elemento en `nums` con cualquier entero en el rango \([-10^{18},10^{18}]\).
■
■ ** Objetivo:** Devuelve el número mínimo de operaciones necesarias.

Por qué funciona
Silencio------------------------------------------------
TENIDO 1 TENIDO `[-10, 15, -12]` TENIDO `1 `` TENIDO Reemplazar `-10` por `0` hace la totalidad de la matriz suma `3`. Silencio
TENIDO 2 TENIDO `[-1,-2,3,-1,2,6] TENIENDO `1 `` TENIDO Replacing `-2` by `1` fija todos los sub-arrayos de 3 longitud que no eran positivos. Silencio
TENIDO 3 TENIDO `[1,2,3]` TENIDO `0` ANTE Ya positivo. Silencio

■ **Constraints**
√≥(3 \le n \le 10^5\)
[i] \le 10^9\)

-...

#### 2down⃣ Key Insight

Cada sub-array de longitud **≥ 3** contiene un sub-array de longitud **exactamente 3**.
Si *todo* sub-array longitud‐3 tiene una suma positiva, entonces **todo** sub-array más largo será automáticamente positivo también (ya que es una suma de superposición de bloques positivos de 3-longitud).

Por lo tanto sólo necesitamos hacer cumplir la positividad en **todas las ventanas de 3 pies**.

-...

#### 3down⃣ Greedy + Prefix Sum Approach

1. **Error de la suma de prefijo** `pref[i] = sum(nums[0 ... i]) `
*Nos permite calcular la suma de cualquier ventana en O(1). *

2. **Scan el array de izquierda a derecha* *
Mantener `maxPref` = suma máxima de prefijo vista hasta ahora (inicialmente `0`).
Para cada posición 'i' (el último índice de una ventana de 3'):

- La suma de la 3-ventana que termina en 'i' es
`ventana Sum = pref[i] - MaxPref`.
- Si 'ventana' significa 0`, debemos cambiar un elemento dentro de esta ventana.
Cuenta una operación, set `maxPref = pref[i]` (Trate toda la ventana como “fixed” por hacerlo cero), y **saca los dos siguientes índices** (`i += 2`).
Skipping es seguro porque el reemplazo que imaginamos fijaría cualquier sub-array que incluya estas posiciones.

3. Devuelve el número de operaciones.

■ ¿Por qué saltar? #
■ Después de reemplazar un elemento en la ventana `[i-2, i]`, cualquier sub-array que todavía contiene cualquiera de los dos índices siguientes ya contendría el elemento reemplazado (y por tanto positivo), por lo que no puede volver a ser no positivo.
■ Saltar las garantías nunca duplicamos un reemplazo necesario.

-...

#### 4down⃣ Complejidad

Un pase lineal.
- **Espacio**: \(O(n)\) para la matriz de suma prefijo (puede reducirse a \(O(1)\) si guardamos una suma de rodaje).
En la práctica el espacio extra está bien para \(n \le 10^5\).

-...

Aplicación

A continuación se encuentran soluciones limpias y de producción en **Java**, **Python**, y **C+**.

■ **Nota**: Los comentarios de código explican la lógica y le ayudan a adaptarla para entrevistas o retos de codificación de trabajo.

-...

#### 5.1 Java (LeetCode)

``java
importar java.util*;

Clase Solución {
public int makeArrayPositive(int[] nums) {
int n = nums.length;
long[] pref = new long[n];
pref[0] = nums[0];
para (int i = 1; i) {}
pref[i] = pref[i - 1] + nums[i];
}

int ops = 0;
maxPref largo = 0; // mejor suma prefijo hasta ahora
para (int i = 0; i <= n - 3; i++) {
// sum of window nums[i] + nums[i+1] + nums[i+2]
ventana larga Sum = pref[i + 2] - maxPref;
si (ventana)
ops++; // reemplazar un elemento en esta ventana
maxPref = pref[i + 2]; // fingir que esta ventana se convirtió en 0
i += 2; // saltar los siguientes dos índices
. ♫ ... {
maxPref = Math.max(maxPref, pref[i]); // update best prefix
}
}
operaciones de retorno;
}
}
`` `

-...

#### 5.2 Python 3

``python
Solución de clase:
def makeArrayPositive(self, nums: List[int]) int:
n = len(nums)
* n
pref[0] = nums[0]
para i en rango(1, n):
pref[i] = pref[i - 1] + nums[i]

operaciones = 0
max_pref = 0 # mejor prefijo visto hasta ahora
I = 0
mientras que yo
window_sum = pref[i + 2] - max_pref
si ventana_sum 0:
ops += 1
max_pref = pref[i + 2]
i += 3 # saltar los siguientes dos índices también
más:
max_pref = max(max_pref, pref[i])
i += 1
operaciones de retorno
`` `

-...

#### 5.3 C++ (g+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int makeArrayPositive(vector fielint implicados nums) {
int n = nums.size();
vector realizado largo tiempo pref(n);
pref[0] = nums[0];
para (int i = 1; i) no; ++i) pref[i] = pref[i-1] + nums[i];

int ops = 0;
largo tiempo maxPref = 0; // mejor prefijo hasta ahora
para (int i = 0; i) {}
ventana larga Sum = pref[i+2] - maxPref;
si (ventana)
++ops; // cambiar un elemento
maxPref = pref[i+2]; // ventana considerada fija
i += 2; // saltar los siguientes dos índices
. ♫ ... {
maxPref = max(maxPref, pref[i]); // mantener el mejor prefijo
}
}
operaciones de retorno;
}
};
`` `

-...

### 6down Good Good, Bad & Ugly – Lo que debes tener en mente

TENIDO ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIENTE
Silencio------------
Silencio TENIENDO Greedy es **optimal** – no hay necesidad de retroceder. ❌ La lógica de Skipping puede ser confusa – siempre explica por qué saltas 2 índices. Olvidar el rango de sumas prefijo ( " largo " / " largo " ) conduce a desbordamiento. Silencio
TEN TENIENDO Un solo escaneo lineal – se ajusta a las limitaciones de entrevista. TEN ❌ Algunas soluciones usan arrays adicionales innecesariamente; prefieren las sumas rodantes. Misreading the “sub-array length” 2" condición (algunos piensan ≥ 3” – correcto es “ 2”). Silencio
TENIDO TENIDO Fácil de probar la corrección: cada sub-array largo contiene una ventana de 3. ❌ La gente podría intentar DP y perder el tiempo – codicioso es más simple. No manejar el caso en el que `n ' 3 ' (aunque las restricciones lo prohíben). Silencio
TENIDO TENIDO Trabaja para valores grandes negativos y positivos porque utilizamos 'long`/`long'. ❌ Over-optimizing: usted podría saltar la matriz de prefijo y utilizar una suma deslizante, pero asuntos de claridad. Si usted reemplaza el elemento con un número negativo muy grande en el ejemplo, puede que todavía necesite otra operación – asegúrese de elegir un valor que neutraliza la ventana (0 o positivo). Silencio

-...

### 7 carreras Por qué este blog te ayuda a aterrizar un trabajo

- **Clear explicación algoritmo** – entrevistadores les encanta el razonamiento conciso.
**Multiple language implementations** – show you can code in Java, Python, and C++.
- ** Contenido amigable de SEO** – palabras clave como “Hacer un Array Positivo”, “Leetcode 3511”, “altitmo inteligente”, “O(n) solución” se situará en alto.
- ** Consejos prácticos** – la tabla “Good/Bad/Ugly” da a los entrevistadores una hoja de trampas.

Utilice este artículo como referencia al prepararse para las entrevistas de codificación, y no dude en adaptar los fragmentos de código para sus propios proyectos o cartera.

-...

### 8 pescuestion;DR

1. *Solo importan ventanas de 3 pulgadas. *
2. Escanee izquierda a derecha con una suma prefijo.
3. Cuando una suma de 3-ventana ≤ 0, cuenta una operación, tratar esa ventana como fija, y saltar los siguientes dos índices.
4. Devuelve el total de operaciones – es el mínimo.

¡Feliz codificación, y que los dioses de la entrevista estén contigo! 🚀