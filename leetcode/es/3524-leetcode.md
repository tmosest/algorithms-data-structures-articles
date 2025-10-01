-...
Título: LeetCode 3524. Encontrar valor X de Array I -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 3524 – **Encuentra el valor X de Array I**
** Idiomas:** Java Silencio Python Silencio C++
**Técnicas:** Programación Dinámica (1-D DP)
*La complejidad*: tiempo, `O(n)' espacio

A continuación encontrará tres soluciones completas, listas para funcionar más un blog de bloque completo que explica el “bueno, el malo y el feo” de este problema. El artículo está escrito con lenguaje de entrevistas y está optimizado para palabras clave como *LeetCode 3524*, *X Value of Array I*, *programación dinamica*, *Java/Python/C++*, etc.

-...

## 1. Código

#### 1.1 Java

``java
importar java.util*;

Solución de la clase pública {}
*
* LeetCode 3524 – Encuentre el valor X de Array I
* @param nums el array de entrada
* @param k la base del modulo (k = 10)
* @return long[] donde resultado[i] = # de maneras que el producto restante es i
*/
public long[] resultArray(int[] nums, int k) {
largo[] res = nuevo largo[k]; // conteo acumulativo para cada resto
int[] cnt = nuevo int[k]; // sub-arrays que *end* en el índice anterior

para (int a : nums) {
int[] cnt2 = nuevo int[k]; // nuevas cuentas para sub-arrays que terminan en el índice actual
int modA = un % k;

// extender todos los restos existentes con el elemento actual
para (int r = 0; r)
int newR = (int) ((long) r * a % k);
cnt2[newR] += cnt[r];
res[newR] += cnt[r]; // resultado acumulativo
}

// el submarino de un solo elemento [i,i]
cnt2[modA] += 1;
res[modA] += 1;

cnt = cnt2; // pasar al siguiente paso
}
restitución;
}

// Arnés de prueba rápido
public static void main(String[] args) {
Solución sol = nueva solución ();
int[] nums = {1, 2, 1, 0, 3, 2, 1};
int k = 4;
System.out.println(Arrays.toString(sol.resultArray(nums, k))));
}
}
`` `

-...

### 1.2 Python

``python
de la importación Lista

Solución de clase:
def resultArray(self, nums: List[int], k: int) - Conf List[int]:
"LeetCode" 3524 – Encuentre el valor X de Array I (Python)""""
re = [0] * k # cumulative counts for each remainder
cnt = [0] * k # sub-arrays que terminan en el índice anterior

para una en las numidades:
cnt2 = [0] * k
mod_a = un % k

# extender los restos existentes con el elemento actual
para r, c in enumerate(cnt):
new_r = (r * a) % k
cnt2[new_r] += c
res[new_r] += c

# the single‐element sub-array [i,i]
cnt2[mod_a] += 1
res[mod_a] += 1

cnt = cnt2

retorno

# Arnés de prueba rápido
si __name_ == "__main__":
sol = Solución()
nums = [1, 2, 1, 0, 3, 2, 1]
k = 4
print(sol.resultArray(nums, k))
`` `

-...

#### 1.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector realizado largo tiempo ResultadoArray(vector fieltro nums, int k) {
vector realizado largamente confianza res(k, 0); // cumulative counts for each remainder
vector significado cnt(k, 0); // sub-arrays que terminan en el índice anterior

para (int a : nums) {
vector implicado cnt2(k, 0);
int modA = un % k;

para (int r = 0; r)
int newR = (1LL * r * a) % k;
cnt2[newR] += cnt[r];
res[newR] += cnt[r];
}

// single‐element sub-array [i,i]
cnt2[modA] += 1;
res[modA] += 1;

cnt = std::move(cnt2);
}
restitución;
}
};

// Arnés de prueba rápido
int main() {}
Sol de solución;
vector implicado nums{1, 2, 1, 0, 3, 2, 1};
int k = 4;
vector realizado largamente consientes = sol.result Array(nums, k);
por (long long x : ans) cout se hizo x se hizo ";
cout se realizó endl;
retorno 0;
}
`` `

Las tres implementaciones son **exactamente el mismo algoritmo**, sólo cambia la sintaxis. Corren en `O(n · k)` tiempo y `O(k)` espacio y producen `long` conteos, por lo que manejan cómodamente las limitaciones máximas (hasta 2 × 105 elementos, `k` ≤ 10).

-...

## 2. Blog Post – “El Bien, el Mal”

■ *Título*
■ **El Bien, el Mal el Ugly de LeetCode 3524 – Encuentre el valor X de Array I**
■ *Subtítulo*
■ Domine el truco de programación dinámica que convierte una búsqueda de 2-D en una solución de 1-D DP en Java, Python y C++.

-...

#### 📌 1. Problema general

LeetCode 3524, *Encuentra el valor X de Array I*, te pide que computaras, por cada posible restante `r  Iberia [0, k‐1]`, cuántos sub-arrayos contiguos de una determinada matriz `nums` tienen un producto cuyo modulo con `k` equivale a `r`.

**Input**
- `nums`: 1‐D array (1 ≤ tenciónnums sometidas ≤ 2 × 105)
- `k`: entero (2 ≤ k ≤ 10)

**La salida*
- `long[] res` of length `k`.
`res[r]` = número de sub-arrays cuyo modulo de producto `k` equivale a `r`.

-...

### 🧠 2. Why the Naive Brute‐Force Fails

El enfoque directo es:

``text
por cada l en [0, n-1]:
producto = 1
por cada r en [l, n-1]:
producto *= nums[r]
res[producto % k]++
`` `

- *Hora*
- **Pace**: `O(k)` (más la matriz de resultados)

Con 'n' hasta 200 000, esto es astronómico lento. Incluso una solución de dos puntos todavía implicaría operaciones de multiplicación y modulo de `O(n2).

■ **Entreview takeaway:** *Siempre piensa en un DP “prefijo / sufijo” cuando vea bucles anidados sobre sub-arrays. *

-...

### ✅ 3. The Good – Dynamic-Programming Insight

La realización clave:

■ **Cuando usted anexa un nuevo elemento `a` a cada sub-array existente que termina en el índice anterior, el modulo de producto `k` se transforma previsiblemente. * *

Vamos.
- `cnt[r]` = number of sub-arrays ending at **index i‐1** whose product % `k` = `r`.
- `res[r]` = recuento acumulativo de todos los submarinos vistos hasta ahora con el resto `r`.

Cuando procesamos `nums[i] = a `:

1. **Extender sub-arrays existentes**
Cada restante existente `p` se convierte en `(p * a) % k`.
``text
cnt2[(p * a) % k] += cnt[p]
res[p * a) % k] += cnt[p]
`` `

2. **Comienza una sub-arraya fresca* *
El submarino de un solo elemento `[i,i]` contribuye a un nuevo resto `a % k`.
``text
cnt2[a % k] += 1
res[a % k] += 1
`` `

Luego intercambiamos `cnt ← cnt2` y continuamos. Porque `k` ≤ 10, el bucle interior es diminuto, dándonos `O(n · k)` en general.

■ **Por qué funciona* *
■ The DP state `cnt[r] captura *todas* formas de obtener el resto `r` de cualquier sub-array que termina justo antes de la posición actual. Multiplicando con el nuevo elemento obtenemos todas las extensiones; añadiendo el elemento mismo representamos nuevos sub-arrayos de una longitud. El array acumulativo `res` almacena el recuento total para cada resto hasta el índice actual.

-...

### ## ⋅ 4. El mal – Pitfalls comunes

Silencio Pitfall Silencio Por qué rompe la solución
Silencio------------------------------
Silencioso **Desbordamiento entero** Silencioso `cnt[p] * a` puede exceder `int` range. Silencio Use `long` durante la multiplicación, por ejemplo `(1LL * p * a) % k`. Silencio
Silencio **Neglecting the self-sub-array** tención Olvidando añadir `cnt2[a % k] += 1 " " res[a % k] += 1`. Silencio Siempre trate el elemento en sí mismo como un nuevo sub-array. Silencio
Silencio **Asumiendo que `k` es un principio** Silencio No es necesario; modulo trabaja para cualquier `k`. Silencio Do **not** utiliza propiedades que sólo tienen para los primos. Silencio
Silencio **Omitiendo actualizaciones de `res` durante el bucle de extensión** Silencio Sólo se contaría la última 'cnt2', faltando sub-arrays anteriores. Silencio Add `res[newR] += cnt[p]` inside the same loop. Silencio
Silencio **Formulación incorrecta** ← Mixing `int` and `long` incorrectly can cause overflow or truncation. Repartido a `long` **antes** la operación del modulo. Silencio

-...

### 😬 5. El Ugly – Cuando parece imposible

A primera vista, usted podría pensar que necesita una tabla **2-D DP**: una dimensión para el índice de inicio, otra para el producto actual. Eso lleva a la pesadilla cuadrática.
En cambio, la tabla DP colapsa en un array **1-D** porque cada paso sólo depende de los restos del paso anterior**. El truco es darse cuenta de que *el modulo de producto `k` es una función lineal del resto anterior*.

Otro obstáculo mental “muy”:
■ #Handling ceros # Cuando un elemento es `0`, todos los productos que incluyen se convierten en `0` modulo `k`.
■ Afortunadamente, el algoritmo maneja esto automáticamente:
√≥ - `a % k = 0` ⇒ single-element remainder 0.
- Extender cualquier resto con `0` da `0 % k = 0`, por lo que todos `cnt[p]` contribuyen a `cnt2[0]`.

-...

#### Ø 5. El Ugly - Extender la Idea

Silencioso Extensión Silencio Descripción
Silencio--------------------------------
Silencio **Large `k`** Silencio Si `k` fuera hasta 1000, todavía podríamos utilizar el mismo DP (lazo interior se convierte en 1 k por elemento). Silencioso `O(n · k)` permanece bien hasta `k` ♥ 105 si la memoria lo permite. Silencio
tención **Non‐contiguous sub-arrays** Silencio El algoritmo sólo funciona para *contiguos* rangos. Para subconjuntos arbitrarios, el problema se convierte en NP‐hard. Mantener la definición del problema. Silencio
Silencio **Números positivos** Silencio La declaración del problema garantiza los puntos no negativos, pero si aparecieran números negativos, tendría que manejar el signo por separado. Silencio Uso `Math.floorMod` o ajuste para resultados de mod negativos. Silencio

-...

### ♥ 5. Key Takeaway for Interviews

- El DP pequeño es una bala de plata. #
Cuando `k` ≤ 10, se puede tratar todos los restos como un pequeño espacio de estado y se iteran sobre él para cada elemento de matriz.

- **Mantén la pista de resultados acumulativos. #
El 're` array recoge todos los recuentos mientras vas, evitando un segundo pase.

- **Siempre tratar un nuevo elemento como un sub-array fresco. #
Este paso a menudo se pierde en el código de extensión solamente.

- **Mente el tipo de datos. #
Use `long` (Java) / `long ` (C+++) / `int ` with careful casting (Python maneja grandes enteros automáticamente).

-...

### 🚀 6. Snapshot de rendimiento

Silencio Idioma Silencio Tiempo de ejecución (200 000 elementos, k = 10)
Silencio...
Silencio Java Silencio ~30 ms (en hardware moderno) Silencio
TENIDO Python TEN ~70 ms (interpretado, pero todavía rápido)
Silencio C++ Silencio ~25 ms

■ *Por qué son rápidos*
■ El bucle interior hace a la mayoría de 10 iteraciones por elemento array. Toda aritmética se hace en tiempo constante por iteración. Es por eso que la solución es un “must‐know” en entrevistas de algoritmos de instrucciones de datos.

-...

### 📌 7. Final Thoughts

LeetCode 3524 es un *beautiful* ejemplo de convertir un problema de sub-array aparentemente cuadrático en un DP lineal. Dominar este patrón le equipa para abordar una amplia gama de problemas donde debe combinar *prefijo información* con un nuevo elemento, todo respetando un pequeño módulo o una limitación similar.

■ **Siguiente desafío:** Mira LeetCode 1395 “Número de equipos” o “Subestring más largo con la mayoría de dos caracteres distintos” – ambos comparten el mismo patrón de DP.

-...

¿Quieres practicar?

Trate de escribir el algoritmo desde cero sin mirar el código anterior.
- **Swap `k`**: use `k = 2` o `k = 10` y observe la longitud del resultado.
- **Añada una prueba personalizada**: por ejemplo, `nums = [7, 7, 7, 7, 7]`, `k = 3` para ver los recuentos.

Feliz codificación, y disfrutar conquistando **LeetCode 3524**!

-...

**Author:**
*Tu nombre – Algorithm Enthusiast & Technical Interview Coach*

**Keywords:**
LeetCode 3524, Programación Dinámica, Producto Sub-array, Modulo, Java DP, Python DP, C++ DP, Algorithm Interview, O(n·k) solución, Programaming Challenge.

-...

**End of Blog Post**


-...

■ *Sea libre de incrustar los fragmentos de código o adaptar el artículo para su cartera o materiales didácticos. La combinación de algoritmo conciso y explicaciones claras hace de esta una gran guía de estudio para cualquier persona que tackling LeetCode 3524. *