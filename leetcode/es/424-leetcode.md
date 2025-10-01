-...
Título: LeetCode 424. Reemplazo de carácter repetitivo más largo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Reemplazo de caracteres repetidos más largo – LeetCode 424
*Java • Python • C++ Soluciones + In‐Depth Blog Post*

-...

Declaración de problemas

■ **Denle una cuerda `s` que consiste en sólo letras mayúsculas y un entero `k`, usted puede cambiar a la mayoría de `k' caracteres en `s` a cualquier otra letra mayúscula. Devuelve la longitud de la subestring más larga que puede contener la misma letra después de los reemplazos. #

■ *Ejemplo*
* * * * * * * * * * * * * * * * = * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
√≥ `s = "AABABBA", k = 1` → **4** (cambiar el medio `A` a `B` → `"AABBBBA" → `"BBBBBB"

**Constraints* *

Silencio
Silencio...
TENIDO `1 ANTE = s.length = 10^5 ' TENIDO `0 Silencio
Silencio `s` contiene sólo letras mayúsculas Silencio

-...

## 📌 Why This Problem is a “Must‐Know” for Interviews

* **Venta de deslizamiento clásico** – demuestra el dominio de la técnica de dos puntos.
* **Frequency Counting** – muestra comodidad con mapas de hash / arrays de tamaño fijo.
* **Optimal Time vs. Space** – perfecto para discutir oficios asintoticos.
* **Real‐World Analogy** – problemas de limpieza / normalización de datos.

-...

## 🧠 Core Idea – Sliding Window + “Keep the Most Frequent Char”

Cuando miramos cualquier subestring, lo único que importa es:

1. La longitud de la ventana
2. El conteo del carácter **más frecuente** dentro de esa ventana

Si la longitud de la ventana desciende el recuento del char más frecuente es **≤ k**, podemos cambiar los caracteres restantes a ese char frecuente, haciendo todo el uniforme de la ventana.
De lo contrario, la ventana es inválida y debemos reducirla de la izquierda.

El truco es que el valor más frecuente es **monotónico** – nunca disminuye a medida que crece la ventana, por lo que podemos mantener una sola variable `maxFreq` y actualizarla sólo cuando el recuento de un nuevo personaje se hace más grande.

-...

## 📈 Time & Space Complexity

Silencio
Silencio...
tención **Tiempo** Silencioso `O(n)` – cada índice se añade y se elimina al máximo una vez. Silencio
Silencio** – array fijo de tamaño 26 (o diccionario de tamaño ≤ 26). Silencio

-...

## 🤓 Edge Cases " Common Pitfalls

Silencio
Silencio...
Silencio 1 TENIDO Olvídate de restar la frecuencia de char saliente al reducir la ventana. Silencio Siempre decremento `freq[s] - 'A']' antes de mover `izquierda. Silencio
TENIDO 2 TENIDO Utilizando `int` para `maxFreq` pero no actualizándolo cuando disminuye. **No** recomputar `maxFreq` en contracción – mantenerlo monotónico; sólo *aumenta*. Silencio
TENIDO 3 TENIDO Utilizando `seguido= k` vs `se realizó k` en el cheque de validez. La condición correcta es `windowLen - maxFreq ' significa= k`.
Silencio 4 ← Off‐por-uno en el cálculo de la longitud de la ventana (`end - izquierda + 1`). TENIDO Use `end - left + 1` o `end + 1 - left`. Silencio

-...

Código - Java

``java
Solución de la clase pública {}
*
* Reemplazo de caracteres repetidos más largo (LeetCode 424)
*
* @param s La cadena de entrada de letras mayúsculas.
* @param k El número máximo de reemplazos permitido.
*Retorno La longitud de la subestring más larga que se puede hacer todo lo mismo.
*/
int carácterReplacement(String s, int k) {
int left = 0; // ventana start
int maxFreq = 0; // frecuencia más alta en la ventana actual
int[] freq = nuevo int[26]; // frecuencia de cada carta

int best = 0; // mejor ventana longitud vista

para (derecho = 0; derecho) {}
int idx = s.charAt(right) - 'A';
freq[idx]++; // incluir nuevo char

maxFreq = Math.max(maxFreq, freq[idx]);

// Si necesitamos más cambios de k, encoge de izquierda
si (derecha - izquierda + 1 - maxFreq √ k) {}
int leftIdx = s.charAt(left) - 'A';
freq[leftIdx]--; // remove char leaving window
izquierda++; // ventana de movimiento
}

mejor = Math.max(mejor, derecha - izquierda + 1);
}

devolver mejor;
}
}
`` `

-...

## 🐍 Code – Python

``python
Solución de clase:
def carácterReplacement(self, s: str, k: int) - int:
"
Ventana deslizante con matriz de frecuencia fija (tamaño 26).
"
izquierda = 0
max_freq = 0
[0] * 26
mejor = 0

por derecho, ch in enumerate(s):
idx = ord(ch) - ord('A')
freq[idx] += 1
max_freq = max(max_freq, freq[idx])

si la derecha - izquierda + 1 - max_freq
freq[ord(s[left]) - ord('A')] 1
izquierda += 1

mejor = max(best, right - left +1)

mejor
`` `

-...

## 🥶 Code – C++

``cpp
Clase Solución {
public:
int carácterReplacement(string s, int k) {
vector implicado freq(26, 0);
int left = 0, maxFreq = 0, best = 0;

para (derecho = 0; derecho) {}
int idx = s[right] - 'A';
freq[idx]+;
maxFreq = max(maxFreq, freq[idx]);

si (derecha - izquierda + 1 - maxFreq √ k) {}
freq[s[left] - 'A']--
++izquierda;
}

mejor = max(best, right - left + 1);
}
devolver mejor;
}
};
`` `

-...

## 📚 In‐Depth Blog Post – “The Good, The Bad, and the Ugly”

#### Introduction

■ **Reemplazo de caracteres repetidos más largo** (LeetCode 424) es un problema aparentemente simple que esconde una profunda visión de la optimización *ventana* y *reserva de frecuencia*. Es una grapa en las carteras de entrevistas por buena razón: prueba la capacidad de un candidato para:
■
■ 1. Formular una ventana corredera invariante
■ 2. Mantener eficientemente el estado auxiliar
■ 3. Razón sobre los límites de los peores casos
■ 4. Comunicar claramente su enfoque
■
■ En este artículo caminaremos por el “bueno” (por qué el algoritmo es elegante), el “malo” (pocas comunes y conceptos erróneos), y el “muy” (menos enfoques optimistas que todavía funcionan pero que te rechazarán en una entrevista de tiempo).

### The Good – Una elegante solución de salchicha

1. **Invariable**
*La ventana es válida si `windowLen - maxFreq ' significa= k`.*
Este único cheque garantiza que nunca necesitamos escanear toda la ventana para los cambios.

2. **Monotonic `maxFreq`**
*Por qué podemos saltarnos la recomputación*
`maxFreq` sólo aumenta a medida que expandemos la ventana. Incluso si dejamos caer el char más frecuente, el anterior `maxFreq` sigue siendo un *bajo atado* en el verdadero máximo para la ventana reducida. Esta sutileza nos permite mantener el algoritmo lineal sin pases extra.

3. **O(1) Space**
Un array fijo de 26 puntos es trivial en comparación con la longitud 10^5 potencial de la cadena.

### El mal – Lo que suele romper candidatos

Problema de la vida Silencioso
Silencio...
Silencio **Recomputación de la frecuencia en contra** Silencio O(n2) tiempo Silencio Mantener `maxFreq` monotónico, no recomputar
Silencio **Wrong ventana longitud formula** latitud Off‐by-one bugs  durable Use `right - left + 1` consistently TENIDO
Silencio **Usando `traducido= k` incorrectamente** Silencio Casos de prueba precavidos Silencio estado de validación con ejemplos simples (`"AB", k=1` → 2) Silencio
Silencio **Mutable state after loop** ← Soberano respuesta final ← Track `best` separately or compute at loop end ←

### The Ugly – Alternatives That Still Pass but Don't Scale

TENCIÓN ANTERIENTE Complejidad ANTERIOR Por qué Es Ugly ANTE
Silencio...
Silencio **Binary Buscar sobre la longitud de la respuesta + cheque** Silencio `O(n log n)` ¦ Factor logarítmico extra; más código
Silencio **Brute‐Force with nested loops** Silencio `O(n2)` Silencio Exceeds time limits for 105 Silencio
Silencio **Using a `Map madeCharacter, Deque woningInteger confianza`** Silencio `O(n)`, pero las constantes más pesadas ¦

Aunque estos enfoques podrían ganar en casos de prueba pequeños, los entrevistadores buscan soluciones *limpiadas y óptimas*.

### How to Talk About En una entrevista

1. **Declara el problema en tus propias palabras** – te asegura entender el objetivo.
2. **Explicar la ventana corredera invariante** – mostrar que estás pensando en términos de ventanas *válidas/inválidas*.
3. **Discuss `maxFreq` monotonicity** - que es el crux que lo mantiene lineal.
4. ** Casos de borde de fusión** – por ejemplo, `k = 0`, `s` de longitud 1, todos los caracteres idénticos.
5. **Hablar de la complejidad** – a los entrevistadores les encanta ver una justificación clara `O(n)`/`O(1)`.

#### Summary

Tiempo lineal, espacio constante, invariante elegante.
- **Bad**: Comune, recomputación, condición equivocada.
- **Ugly**: Variantes cuadráticas o binarias que pierden tiempo.

Mastering this problem signals that you can handle *dynamic constraints* and *frequency-based optimizations*—skills highly Prized by top tech companies.

-...

## 🎯 SEO‐Optimized Closing

■ ¿Buscando aterrizar un papel de ingeniería de software? Mastering **LeetCode 424 – Reemplazo de caracteres repetidos más largo** muestra su competencia en **sliding ventana**, **string manipulación**, y **optimal algoritmo design**.
■ Sumérgete en nuestras soluciones Java, Python y C++, lee el blog detallado para el **bueno, malo y feo** de esta pregunta de entrevista clásica, y aumenta tu confianza de entrevista hoy!

-...

## 📎 Bonus – Quick Test Harness (Optional)

``java
public static void main(String[] args) {
Solución sol = nueva solución ();
System.out.println(sol.characterReplacement("ABAB", 2)); // 4
System.out.println(sol.characterReplacement("AABBA", 1)); // 4
}
`` `

``python
si __name_ == "__main__":
sol = Solución()
print(sol.characterReplacement("ABAB", 2)) # 4
print(sol.characterReplacement("AABABBA", 1)) # 4
`` `

``cpp
int main() {}
Solución s;
cout se realizó s.characterReplacement("ABAB", 2) se realizó endl // 4
cout se realizó s.characterReplacement("AABABBA", 1) se realizó endl // 4
}
`` `

¡Feliz codificación y buena suerte en tu próxima entrevista!