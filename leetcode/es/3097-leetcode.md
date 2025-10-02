-...
Título: LeetCode 3097. Subarray con OR al menos K II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📌 Shortest Subarray With OR at least K (LeetCode 3097)

**Keywords** – LeetCode 3097, subarray más corto OR, bitwise OR, escaparate deslizante, solución Java, solución Python, solución C++, algoritmo de entrevista, entrevista

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

Dado un array `nums` de enteros no negativos y un entero `k`, encontrar la longitud del *shortest* subarray no vacío cuyo bitwise **OR** es **≥ k**.
Regrese `-1' si no existe tal subarray.

*Constraints*

Silencio
Silencio...
TENIDO `1 ≤ nums.length ≤ 2 × 105` TENIDO `0 ≤ nums[i] ≤ 109` ANTE
Silencioso `0 ≤ k ≤ 109`

El problema aparece “fácil” a primera vista, pero las limitaciones hacen imposible una solución ingenua O(n2).

-...

#### 2down⃣ ¿Por qué el enfoque de Naïve falla

La idea directa es:

`` `
para cada índice de inicio i
o = 0
para cada índice final j ≥ i
o confidencialidad= nums[j]
si o >= k: grabar j-i+1 y romper
`` `

Complejidad del tiempo: **O(n2)** → 4 × 1010 operaciones para el peor caso.
El uso de la memoria está bien, pero el tiempo de funcionamiento es demasiado alto para 2 × 105 elementos.

-...

#### 3down⃣ La estrategia ganadora – Ventana deslizante + Cuentas de bits

Intuición

Cuando extendemos la ventana a la derecha, el OR de la ventana sólo puede **aumentar** (los bits sólo pueden girar desde 0 → 1).
Cuando nos encogemos de la izquierda, los bits pueden desaparecer sólo si el bit era único al elemento que estamos eliminando.

Debido a que los números encajan en 32 bits (`≤ 109  obtenidos 231`), podemos mantener un array `cnt[32]` Donde
`cnt[i]` = cuántos números en la ventana actual tienen el `i`‐th bit set.

Desde `cnt` podemos reconstruir el OR actual en O(32) estableciendo un poco si `cnt[i] > 0 `.

##### 🧪 Algorithm

`` `
izquierda = 0
ans = INF
cnt[32] = {0}

por derecho en 0 .. n-1
añadir bits of nums[right] to cnt

mientras que la izquierda: k
ans = min(ans, right-left+1)
remove bits of nums[left] from cnt
izquierda++

devolver ans == INF ? -1 : ans
`` `

*Agregar / eliminar bits* es simplemente aumentar / decrementar los recuentos para cada bit que se establece en el número.

###### 📈 Complexity

- Cada elemento se añade una vez y se elimina una vez → **O(n)** actualizaciones.
- Cada actualización toca a la mayoría de 32 bits → **O(32 · n) ♥ O(n)**.
- Reconstrucción del OR en el bucle de `mientras' es O(32), tiempo constante.

Uso de la memoria: **O(32)** → trivial.

-...

#### 4down⃣ Edge‐ Lista de verificación de casos

Silencio Caso confidencialidad Por qué funciona Silencio Notas Silencio
Silencio------------------------
TENIDA `k == 0` Silencioso O de cualquier elemento es ≥ 0 Silencio Subarray más corto es siempre la longitud 1 Silencio
Silencio Ningún subarray llega a `k` Silencio `ans` se queda `INF` Silencio
TENIDO `nums` todos los ceros TENIDO O nunca aumenta TENIDO Igual que antes
TENIDA `nums` longitud 1 TENCIÓN Elemento único revisado una vez que NOVED funciona naturalmente

-...

#### 5down⃣ Aplicación del Código

■ **Tip:** Los fragmentos de código de abajo están listos para la producción. Utilizan las mismas funciones de ayuda claras para añadir/removir bits y reconstruir el OR.

##### 5.1 Java

``java
importar java.util*;

Clase Solución {
public int minimumSubarrayLength(int[] nums, int k) {
int[] cnt = nuevo int[32];
int left = 0, ans = Integer. MAX_VALUE;

para (derecho = 0; derecho) {}
addBits(cnt, nums[right], 1);

mientras (izquierda) {}
as = Math.min(ans, right - left + 1);
addBits(cnt, nums[left], -1);
izquierda++;
}
}
Regresa a == Integer. MAX_VALUE ? -1 : ans;
}

vacío privado addBits(int[] cnt, int num, int delta) {}
para (int i = 0; i)
si ((num нелиних i) == 1) cnt[i] += delta;
}
}

int privado corrienteOr(int[] cnt) {
int val = 0;
para (int i = 0; i)
si (cnt[i] 0) val Silencio= (1 , se hizo i);
}
Val de retorno;
}
}
`` `

#### 5.2 Python

``python
de la importación Lista

Solución de clase:
def minimumSubarrayLength(self, nums: List[int], k: int) - título int:
cnt = [0] * 32
izquierda, ans = 0, flotante('inf')

por derecho, num in enumerate(nums):
auto._add_bits(cnt, num, 1)

mientras que la izquierda es correcta= derecha y auto._current_or(cnt)
ans = min(ans, right - left +1)
auto._add_bits(cnt, nums[left], -1)
izquierda += 1

retorno -1 si ans == flotante('inf')

@staticmethod
def _add_bits(cnt: List[int], num: int, delta: int) - título Ninguno.
para i en rango(32):
si (num нелиных i) >
cnt[i] += delta

@staticmethod
def _current_or(cnt: List[int]) - título int:
val = 0
para i, c en enumerate(cnt):
si c:
val tención= (1 Гленте i)
retorno val
`` `

#### 5.3 C++

``cpp
Clase Solución {
public:
int minimumSubarrayLength(vector seleccionadoint limitada nums, int k) {
array obtenidos, 32 hilos cnt{}; // todos los ceros inicialmente
int left = 0, ans = INT_MAX;

para (derecho = 0; derecho)
addBits(cnt, nums[right], 1);

mientras (izquierda) {}
ans = min(ans, right - left + 1);
addBits(cnt, nums[left], -1);
++izquierda;
}
}
(ans == INT_MAX) ? -1 : ans;
}

privado:
vacío añadirBits(arrayación obtenida, 32 pulsa cnt, int num, int delta) {}
para (int i = 0; i) {}
si (num нелиних i) " 1)
cnt[i] += delta;
}
}

corriente O(cont array observado, 32 puntos sensibles) {
int val = 0;
para (int i = 0; i)
si (cnt[i] 0)
val TEN= (1 ANTE)
Val de retorno;
}
};
`` `

-...

#### 6down⃣ El Bien, el Mal, y el Ugly

Silencio Silencio
Silencio------------Prince------
Silencio ** Complejidad en el tiempo** Silencio O(n) → pasa fácilmente ← Naïve O(n2) podría TLE TENIDO Las operaciones de bitwise infundadas (por ejemplo, la reconstrucción de OR con un bucle sobre 64 bits) todavía podría ser **slow** ←
Silencio **Espacio** Silencioso (32 ints) Silencio Extra `o` array not needed Silencio Olvidar reiniciar los recuentos conduce a **incorrecto O** Silencio
Silencio **Implementación** Silencio Ayudantes claras ( " AddBits " , `currentOr`) → legibilidad Silencio Ninguno Silencioso Sobre-ingeniería (por ejemplo, árboles de segmento) por un problema de 32 bits
Silencio **Portabilidad** Silencio Obras en Java, Python, C++ Silencio Algunos idiomas necesitan integers de 64 bits Silencio En Java, `1 se hizo 31` es negativo pero sigue siendo correcto - puede confundir a los recién llegados
Silencio **Maintainability** ← Reusable bit-count logic ← Ninguno TENIDO Utilizando `unordered_map interpretadoint,int ``por bit would be **overkill** Silencio

-...

### 7 carreras Cómo aterrizar esa entrevista

1. **Mostrar el Proceso del Pensamiento** – Comience por explicar por qué un nulo doble es demasiado lento.
2. **Explain OR Monotonicity** – Los entrevistadores les encanta ver que usted entiende la propiedad central que hace una ventana deslizante viable.
3. **Highlight Constant‐Time Bit Operations** – Mention that 32 bits → constant, so the “inner” loop is still O(1).
4. **Test Edge Cases** – Pida al entrevistador que piense en `k == 0`, todos los ceros, etc.
5. **Mention Space** – 32 contadores son insignificantes; incluso puedes comprimirlos en un entero de 32 bits si quieres ser elegante.
6. **Código limpio de palabras** – Como se muestra anteriormente, utilice funciones de ayuda y evitar números mágicos.

■ *“¿Por qué estás añadiendo y eliminando pedazos? ¿No es o asociativo?”*
■ Respuesta: “Es asociativo, pero porque necesitamos detectar cuando el OR cae por debajo de k mientras se encoge, rastreamos cuántos elementos contribuyen a cada bit. Eso nos hace saber cuando un poco desaparece. ”

-...

### 7 carreras Final Takeaway

- **LeetCode 3097** es un ejemplo de libro de texto de cómo una simple observación (el OR sólo crece) le permite convertir una fuerza bruta O(n2) en un algoritmo de ventana deslizante O(n).
- La información clave es mantener una serie de bits **frecuencia en lugar de recomputar el OR desde cero.
- La solución es *language‐agnostic*: funciona en Java, Python, C++ y cualquier otro idioma con enteros de 32 bits.

■ **Pro-tip for recruiters**: Mención de que su solución utiliza operaciones de bits de tiempo constante*, haciéndolo *super rápido* incluso en los límites superiores de las limitaciones. Ese es exactamente el tipo de “performance‐aware” entrevistadores de pensamiento están buscando.

¡Feliz codificación! 🚀