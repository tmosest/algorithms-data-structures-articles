-...
Título: LeetCode 1590. Hacer Sum Divisible por P -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
1. LeetCode 1590 – “Make Sum Divisible por P”
■ **Objetivo** – Retire el sub-arrayo contiguo * esmalte* para que la suma de los números restantes sea divisible por " p " .
■ **Constraint** – Todo el array no puede ser eliminado.

-...

## 🔍 Problem Recap (inglés + chino)

** English**
`` `
Entrada: nums = [3,1,4,2], p = 6
Producto: 1 (remove [4])
`` `

**Chino* *
■ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪
■ ** Hundimiento del golpe**

-...

##  Settlement Solution Overview

1. **Computar la suma total**.
*Si* `S % p == 0`, ya somos buenos → retorno `0`.
2. # Objetivo de la sub-array #
El sub-array que quitamos debe tener una suma cuyo modulo restante `p` igual
`rem = S % p`.
3. **Sumas de prefijo + HashMap**
* Iterate una vez a través de la matriz manteniendo un modulo de la suma prefijo en funcionamiento.
* Almacene el índice *latest* en el que cada valor modulo aparece en un mapa de hash.
* Para cada índice `i` con el prefijo actual `cur`, queremos un prefijo anterior
'prev' such that
`cur – prev ngel rem (mod p)` → `prev У (cur – rem) mod p`.
Si existe tal `prev`, el sub-array `(prev+1 ... i)` es un candidato.
4. **Track the minimal length**.
5. **Si no hay candidato** → devolver `-1`.
6. **Importante** – do **not** permite que la longitud del candidato sea toda la matriz.

Esto produce **O(n)** tiempo y **O(n)** espacio auxiliar.
Todos los cálculos usan enteros de 64 bits para evitar el desbordamiento.

-...

## 🧑 💻 Code Implementations

A continuación se presentan implementaciones limpias y de producción en **Java**, **Python** y **C+**.
Cada archivo es autocontenido y sigue la misma lógica.

### 1. Java 17

``java
importa java.util. HashMap;

Solución de la clase pública {}
*
* Encontrar la longitud del subarray más pequeño para eliminar
* para que la suma de los elementos restantes sea divisible por p.
*
* @param nums array de números enteros positivos
* @param p divisor
* @return minimal subarray length or -1 if impossible
*/
public int minSubarray(int[] nums, int p) {}
total largo = 0;
para (int x : nums) total += x;

int rem = (int) (total % p);
si (rem == 0) retorno 0; // ya divisible

HashMap hizoInteger, Integer título pref = nuevo HashMap correctamente();
pref.put(0, -1); // mango prefijo que comienza en 0
prefijo largo = 0;
int best = nums.length; // inicializar con el peor caso

para (int i = 0; i)
prefijo += nums[i];
int cur = (int) (prefix % p);
necesidad int = (cur - rem + p) % p; // modulo ajuste

Integer prevIdx = pref.get(necesitado);
si (prevIdx != null) {
mejor = Math.min(best, i - prevIdx);
}
pref.put(cur, i); // mantener el último índice
}

volver mejor == nums.length ? -1 : mejor;
}
}
`` `

### 2. Python 3

``python
de la importación Lista

Solución de clase:
def minSubarray(self, nums: List[int], p: int) - título int:
total = suma (nums)
rem = total % p
si rem == 0:
retorno 0

pref = {0: -1} # prefix_mod - titulado last_index
prefijo = 0
best = len(nums)

for i, v in enumerate(nums):
prefijo += v
cur = prefijo % p
necesidad = (cur - rem) % p
si es necesario en pref:
mejor = min(best, i - pref[need])
pref[cur] = i

regreso -1 si mejor == len(nums) más mejor
`` `

### 3. C+17

``cpp
Incluido el título
#include ■unordered_map Conf
#include >

Clase Solución {
public:
int minSubarray(std::vector identificadoint limitada nums, int p) {}
long long total = 0;
para (int x : nums) total += x;

int rem = static_cast correctamenteint(total % p);
si (rem == 0) retorno 0;

std::unordered_map armonizado, int confidencial pref; // mod - título último índice
pref[0] = -1;
prefijo largo largo = 0;
int best = static_cast autorizado(nums.size());

para (int i = 0; i) ++i) {
prefijo += nums[i];
int cur = static_cast
int need = (cur - rem + p) % p;

auto = pref.find(necesita);
si (lo != pref.end())
mejor = std::min(best, i - it- Confsegundo);

pref[cur] = i; // mantener la posición más reciente
}

volver mejor == nums.size() ? -1 : mejor;
}
};
`` `

-...

## 📘 Blog Artículo: "El Bien, el Mal, y el Ugly de LeetCode 1590"

■ *“Make Sum Divisible por P” – una pregunta engañosamente sencilla de entrevista que esconde trampas sutiles. Vamos a romperlo, explorar casos de borde, y aprender cómo clavarlo en su próxima entrevista de codificación. *

#### ## 1down⃣ Bien – Lo que hace Este problema es amistoso

Por qué ayuda a vivir
Silencio----------
tención **Single Pass** tención Un escaneo lineal con un hashmap da tiempo O(n). Silencio
Silencio **Remanente Determinista** Silencio El resto del objetivo es simplemente `total % p`. Silencio
tención **Clear Mathematical Insight** ← Removing a sub-array with remainder `rem` guarantees divisibility. Silencio
Silencio **Wide Test Coverage** Silencioso Las pruebas ocultas de LeetCode son casos de borde de verificación: eliminación vacía, casos imposibles, números grandes. Silencio

#### 2down⃣ Mala... Los Tricky Corners

Silencio Pitfall Silencio Por qué rompe la vida
Silencio------------
Silencio ** Desbordamiento de enteros** puede ser > 2^31‐1. Use 64-bit (`long`/`long`). Silencio
Silencio **Modulo con números negativos** Silencio En Java/C++ `-1 % p` es negativo. Use `(cur - rem + p) % p`. Silencio
La declaración lo prohíbe. Un ingenuo “mínimo de n” devolverá incorrectamente `n` en lugar de `-1`. Silencio
Silencio **HashMap Iniciaization** latitud Olvidar insertar `0 → -1` extraña a los candidatos que comienzan en el índice `0`. Silencio
Silencio **Usando “primera ocurrencia” solamente** tención Mantener sólo el primer índice puede perder un sub-array más corto más tarde. Mantenga la ocurrencia * más reciente* para cada modulo. Silencio
Silencio **O(n2) Brute‐Force** Silencio Pasa pequeñas pruebas pero TLE en entradas más grandes. Silencio

### 3down U Ugly – When the Interviewer Tricks You

■ El entrevistador podría pedirle que adapte la solución para ** actualizaciones dinamicas** o para **mantener múltiples consultas**. El principio subyacente todavía sostiene, pero necesitará:

* **Pre-compute prefix sums** y almacenarlos en un array.
* Use ** prefijo suma diferencia** para responder preguntas en O(1).
* Para las actualizaciones, reconstruir el hashmap o utilizar un árbol de segmento si se requieren muchas actualizaciones.

#### 4down⃣ Lista de comprobación de entrevistas

- **Leer la declaración cuidadosamente** – note la cláusula “no puede borrar toda la matriz”.
-Use aritmética de 64 bits en todas partes.
- **Normalize modulo results** to be non-negative before looking up the hashmap.
- **Initializar el hashmap con `{0: -1}`** - esto maneja sub-arrays que comienzan en el índice 0.
- **Retorno `-1` si la mejor longitud es igual al tamaño de la matriz**.
- **Explica tu algoritmo en inglés claro** antes de bucear en código.

■ **Consejo:** Practicar el patrón de “prefix‐sum + hashmap” en otros problemas (por ejemplo, * Subarray más largo con Sum Zero*, *Maximum Size Subarray Sum Equals k*, *Subarray Division Problems*). Una vez que lo dominas, verás que muchos problemas “difíciles” se reducen a un patrón similar.

### 5down⃣ SEO‐Friendly Keywords

* LeetCode 1590
* Hacer Sum Divisible por P
* Problema de codificación de entrevistas
* Solución Java
* Solución de pitón
* Solución C++
* Suma de prefijo
* Técnica HashMap
* Complejidad del algoritmo
* Datos Entrevista de estructuras

#### 6down⃣ Final Take‐ Away

■ **El núcleo de este problema es una hermosa mezcla de aritmética y data‐structure savvy. #
*Bien*: Tiempo lineal, pendiente de blanco claro.
*Bad*: Cuidado con el desbordamiento, el modulo negativo, y la restricción “plel array”.
*Evidentemente*: Cuando te olvides del hashmap o pruebes una fuerza bruta cuadrática, el arnés de prueba te marcará inmediatamente.

Si puede articular este razonamiento durante una entrevista y entregar uno de los tres fragmentos de código limpios y listos para la producción arriba, usted será un candidato fuerte para cualquier papel centrado en el algoritmo. ¡Feliz codificación!

-...

**No dude en copiar los fragmentos de código en su IDE y ejecutar los casos de prueba proporcionados. ¡Buena suerte con tu entrevista! * *