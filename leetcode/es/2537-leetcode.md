-...
Título: LeetCode 2537. Cuenta el número de buenas subarrayas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2537 – Cuenta el número de buenas subarrayas
*LeetCode* Silencio *Java* Silencio* *Python* Silencio* *Sliding‐Window* *Job Interview*

A continuación encontrará una implementación lista para la producción para **Java, Python y C++** que resuelve el problema LeetCode **2537 – Cuenta el número de buenas subarrays** en el tiempo *O(n)* utilizando la técnica clásica de dos puntos de venta corredera.

-...

### 1. Recaptación de problemas

■ **Definición** – Un subarray es *bueno* si contiene **al menos `k` pares de elementos iguales**.
■
Input: `int[] nums` (responsable ≤ 105, 0 ≤ nums[i] ≤ 109) and `int k` (0 ≤ k ≤ 109).
■ Producto: el número de subarrays *buenos* (retorno tipo `long`/`long`).

La solución bruta-force examinaría cada subarray (O(n2)), que es demasiado lenta para las limitaciones. El truco de la ventana deslizante lo convierte en un algoritmo de tiempo lineal.

-...

## 2. Sliding‐Window Insight

Silencio Lo que *track* Silencio Por qué funciona
Silencio...
Silencio Frequency map (`freq`) TEN nos permite saber cuántas veces aparece un valor en la ventana actual. Silencio
TENIDO `pairs` - número de pares iguales en la ventana actual TENIDO Añadiendo un elemento de valor `x` crea `freq[x]` nuevos pares (ya que cada uno de los actuales `freq[x]` ocurrencias pueden emparejar con el nuevo). Silencio
Silencio `izquierda ' - puntero izquierdo de la ventana Cuando la ventana es buena (`pairs` ≥ `k`), cada subarray que comienza en un índice ≤ `izquierda ' y termina en el índice derecho actual es bueno. El número de esos subarrays equivale a " izquierda " . Silencio

*Key loop invariante* – Después de encoger la ventana mientras permanece bien, la ventana `[izquierda ... derecha] `` es la ventana *smallest* que termina en `derecha' que aún satisface el requisito. Así, todos los subarrays que terminan en `derecha' que comienzan **antes** `izquierda' están garantizados para ser buenos, y agregamos `izquierda' a la respuesta.

-...

## 3. Implementaciones de referencia

## Java

``java
importa java.util. HashMap;
importa java.util. Mapa;

Solución de la clase pública {}
*
* Devuelve el número de buenos subarrays en el tiempo O(n).
* @param nums la matriz de enteros
* @param k el número requerido de pares
* @return the count of good subarrays (long to avoid overflow)
*/
public long countGood(int[] nums, int k) {
Mapa seleccionadoInteger, Integer frecuentementeq = nuevo HashMap Quería();
int left = 0; // límite izquierdo de la ventana actual
ans largas = 0;
pares int = 0; // número de pares iguales dentro de la ventana

para (derecho = 0; derecho) {}
int cur = nums[right];
// Añadiendo cur añade freq[cur] nuevos pares
pares += freq.getOrDefault(cur, 0);
freq.put(cur, freq.getOrDefault(cur, 0) + 1);

// Arranca la ventana mientras tenemos suficientes pares
mientras (pairs не= k) {
ans += nums.length - right; // todos los subarrays que comienzan en 'izquierda' son buenos
int left Val = nums[left];
int leftFreq = freq.get(leftVal);

// Remoción de la izquierda Val reduce el número de pares por (leftFreq - 1)
pares -= (leftFreq - 1);
(izquierda) 1) {
freq.remove(leftVal);
. ♫ ... {
freq.put(leftVal, leftFreq - 1);
}
izquierda++;
}
}
devolver los ans;
}
}
`` `

-...

## Python

``python
de las colecciones importadas por defecto
de la importación Lista

def countGood(nums: List[int], k: int) - título int:
"
Cuenta buenos subarrays en tiempo O(n).
:param nums: List[int] – array de entrada
:param k: int – número requerido de pares iguales
: retorno: int – número de buenos subarrays
"
freq = defaultdict(int) # elemento → frecuencia en la ventana actual
izquierda = 0 # límite izquierdo de la ventana
pares = 0 # número de pares iguales en la ventana
ans = 0

por derecho, val in enumerate(nums):
# Adding new element creates `freq[val]` new pairs
pares += freq[val]
freq[val] += 1

# Mientras la ventana sigue siendo buena, encogiéndolo desde la izquierda
mientras que pares
# All subarrays starting from current 'left' to 'right' are good
ans += derecha - izquierda + 1
left_val = nums[left]
left_freq = freq[left_val]

# Removing left_val reduce pares by (left_freq - 1)
pares -= (left_freq - 1)
freq[left_val] = left_freq - 1
izquierda += 1

Retorno
`` `

■ **¿Por qué `ans += right - left + 1`?**
■ Una vez que encontremos la izquierda mínima que todavía mantiene la ventana buena, cada subarray que comienza en `izquierda' ** o posterior** y termina en `derecha' también contendrá al menos 'k' pares. El recuento de tales subarrays es exactamente `derecha - izquierda + 1`.

-...

### C++

``cpp
Incluido el título
#include ■unordered_map Conf
usando std namespace;

Clase Solución {
public:
*
* @param nums la matriz de enteros
* @param k el número requerido de pares
* @return the number of good subarrays (long long to avoid overflow)
*/
largo largo largo conteoGood(vector seleccionóint círculo nums, int k) {
unordered_map madeint, int confianza freq;
ans largos = 0;
int left = 0; // límite izquierdo de la ventana
pares largos = 0; // número de pares iguales dentro de la ventana

para (derecho = 0; derecho)
int cur = nums[right];
// Agregar cura crea freq[cur] nuevos pares
pares += freq[cur];
++freq[cur];

// Arranca la ventana mientras tenemos suficientes pares
mientras (pairs не= k) {
ans += nums.size() - right; // todos los subarrays que comienzan en 'izquierda' son buenos
int left Val = nums[left];
int leftFreq = freq[leftVal];

// Remoción de la izquierda Val reduce pares por (leftFreq - 1)
pares -= (leftFreq - 1);
(izquierda) 1) freq.erase (leftVal);
freq[leftVal] = leftFreq - 1;
++izquierda;
}
}
devolver los ans;
}
};
`` `

■ **Consejo:** En muchas soluciones aceptadas verá la variable `k` siendo decrementada/incrementada para rastrear la cuota de par restante. La lógica es equivalente a lo que describimos anteriormente – sólo un estilo de contabilidad ligeramente diferente.

-...

## 4. El “bueno, malo” de esta solución

Lo que hace que sea bueno para la vida Lo que es Tricky
Silencio------------------------------------------...
Silencio **Bien** Silencio Tiempo lineal, fácil de entender una vez que el truco de la cuenta par es captado.
Silencio **Bad** Silencio Usted debe mantener `k` *mutable* o mantener un contador separado de `pairs`; mezclar los dos puede conducir a errores. TEN ANTE TENED-por-uno errores al añadir/remover desde la ventana. Silencio
Silencio **Ugly** Silencio La lógica de que “cerrar un elemento aumenta los pares por su frecuencia actual” no es obvia a primera vista. Silencio vivir Olvidar actualizar el mapa después de decrementar las frecuencias puede producir “-1”. Silencio

-...

## 5. SEO‐Optimized Blog Post

### 🎯 Master LeetCode 2537: Cuenta el número de buenas subarrayas

Si te estás preparando para una entrevista de ingeniería **software** o un standcamp ** de codificación** y quieres as **LeetCode 2537 – Cuenta el número de buenas subarrayas**, estás en el lugar correcto.
En este artículo:

1. Descomponer el algoritmo **-ventana deslizante** que trae la complejidad del tiempo de **O(n2)** a **O(n)**.
2. Proveer código limpio y listo para la producción en **Java**, **Python**, y **C+**.
3. Explicar los trozos complicados, las trampas y cómo hablar de esta solución en una entrevista.

##### Palabras clave:
- LeetCode 2537
- Cuenta el número de buenas subarrayas
- Ventana deslizante
- Entrevista de algoritmo de Java
- Python coding challenge
- explicación del algoritmo C++
- algoritmo de entrevista de trabajo

-...

### 📌 ¿Qué es un Subarray “bueno”?

■ Un subarray es **bueno** si contiene al menos "k" pares de elementos iguales.
■ Un par es un par de índices `(i, j)` con `i 'i' hechos j` y `nums[i] == nums[j]`.

La solución ingenua comprobaría cada subarray y contaría sus pares, dando tiempo **O(n2)**. Eso no es factible para 'n ≤ 100.000'.

-...

### 🧠 Sliding‐Window to the Rescue

El corazón de la solución es un enfoque **2 puntos**:

- **Punto derecho** expande la ventana un elemento a la vez.
- **El puntero izquierdo** encoge la ventana mientras que la ventana aún satisface el requisito del par.

Truco clave:
*Cuando agregas un nuevo elemento de valor `x`, el número de nuevos pares equivale a la frecuencia actual de `x` en la ventana. *
Así guardamos un ** mapa de frecuencia** y un mostrador de 'pairs' en ejecución.

El invariante después de reducir la ventana es:
*`[izquierda... derecha]` es la ventana más pequeña que todavía contiene al menos pares 'k'. *
Todas las subarrayas que terminan en `derecha' y comienzan **antes** `izquierda` son automáticamente buenas.

-...

### ## 🛠ف Code - Java, Python, C++

Ya hemos proporcionado las implementaciones completas arriba. En entrevistas, se puede elegir el idioma con el que se siente más cómodo, pero la lógica es idéntica:

``java
// Java
public long countGood(int[] nums, int k) { ... }
`` `

``python
# Python
def countGood(nums: List[int], k: int) - título int: ...
`` `

``cpp
// C++
largo largo largo conteoGood(vector seleccionóint círculo nums, int k) { ... }
`` `

■ **¿Por qué usamos 'long' (o 'long' en Java)? * *
■ La respuesta puede ser tan grande como `n * (n+1) / 2`, que supera la gama de enteros de 32 bits para grandes entradas.

-...

### 📌 Talking About the Solution in an Interview

■ **Pregunta:** Explique cómo se acercaría a LeetCode 2537. ”
**Respuesta (TL;DR):* *
■ “Yo usaría una ventana deslizante. Mantengo un mapa de frecuencias y un mostrador de 'pairs'. Al deslizar el puntero derecho, agrego la frecuencia actual del nuevo elemento a `pairs`. Entonces sigo moviendo el puntero izquierdo hasta que `pairs` cae debajo de `k`. Cada vez que la ventana es buena añadiré el número de subarrays que comienzan antes del puntero izquierdo a mi respuesta. ”

Si el entrevistador pide **por qué esto es lineal**:
- El puntero derecho se mueve **n** veces.
- Cada movimiento de puntero izquierdo también se mueve a lo más ** n** veces.
- Todas las operaciones en el mapa del hash son *amortizadas* O(1).
- El tiempo total es **O(n)**, memoria **O(min(n, distinct values)**.

-...

#### 🏁 Take‐away

- Ventana deslizante + mapa de frecuencia = la solución estándar oro para LeetCode 2537.
- El truco de par es el momento "Eureka": *add `freq[x]` cuando insertas `x`*.
- Tener código limpio en **Java, Python, C++** muestra que entiende los lenguajes específicos mientras mantiene la idea central sin cambios.

¡Buena suerte! 💪 Recuerda, la clave para aterrizar ese papel de ingeniería de software no es sólo tener una solución correcta sino ser capaz de explicar *por qué* funciona. ¡Feliz codificación!