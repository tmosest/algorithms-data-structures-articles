-...
Título: LeetCode 2730. Encontrar la Subestring semi-repetitiva más larga -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recaptación de problemas

√ **2730. Encontrar la Subestring Semi‐Repetitive* *
■ **Dificultad:**
■ **Introducción:** una cadena de dígitos `s` (`1 ≤ Entendido ≤ 50`, cada char es `'0'...'9''
■ **Resultado:** la longitud del subestring contiguo más largo que contiene ** en la mayoría de un** par adyacente de dígitos idénticos.

Una subestring es *semi-repetitiva* si hay **cero o uno** índices `i ' tal que
`substr[i] == substr[i+1]`.
Ejemplos:
- "0010" - un par (`00`) → válido
- '00101022' - dos pares (`00`, `22`) → inválido

Necesitamos la longitud **maximum posible** de tal subestring.



----------------------------------------------------

## 2. Algoritmo – Ventana deslizante (Two‐Pointer)

El problema clásico “en la mayoría de una violación” se puede resolver con un pase **single** utilizando una ventana deslizante:

Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio 1. Silencio Mantenga dos índices `izquierda ' y `derecha ' - la ventana actual `[izquierda, derecha]`. Silencio
Silencio 2. Silencio Mantenga un contador `repeats` - cuántos pares iguales adyacentes están dentro de la ventana. Silencio
Silencio 3. TENIENDO `derecho' de `0` a `n‐1`. Después de moverse, compruebe si `s[right] == s[right‐1]`. Si es así, aumenta `repeats`. Silencio
Silencio 4. Silencio Mientras que `repeats ' 1`, move `left` forward one step. Si pasa un par (`s[left] == s[left‐1]`) decremento `repeats`. Silencio
Silencio 5. Respuesta actualizada con `derecha - izquierda + 1`. Silencio

Debido a que cada índice se mueve a la mayor parte de la vez, el algoritmo funciona en **O(n)** tiempo y utiliza **O(1)** espacio extra.



----------------------------------------------------

## 3. Implementaciones de referencia

A continuación se presentan soluciones limpias y idiomáticas en **Java, Python y C++**.
Todos siguen la misma lógica de la ventana deslizante descrita anteriormente.

■ **Tip:**
■ Use `charAt` (Java), indexación directa (Python, C++) y tenga cuidado con errores fuera de cada uno al comprobar el par que termina en el nuevo `derecho' o comienza en el nuevo `izquierda.

-...

### 3.1 Java

``java
*
* LeetCode 2730 – Subestring Semi‐Repetitive
*
* Complejidad del tiempo: O(n)
* Complejidad espacial: O(1)
*/
Clase Solución {
int longestSemiRepetitive Substring(String s) {
int n = s.length();
int left = 0; // límite izquierdo de la ventana
int repetidos = 0; // número de pares iguales adyacentes en la ventana

para (derecho = 1; derecho) {}
// ¿Hemos creado un nuevo par adyacente añadiendo s[right]?
si (s.charAt(right) == s.charAt(right - 1)) {
repeticiones++;
}

// Ventilador hasta que tengamos un par
mientras que (repeticiones 1) {
// Moviendo a la izquierda un par lo quita de la ventana
si (s.charAt(left) == s.charAt(left + 1)) {}
repite...
}
izquierda++;
}
}
// La longitud de la ventana más larga es n - izquierda (derecha termina en n-1)
retorno n - izquierda;
}
}
`` `

-...

#### 3.2 Python

``python
Solución de clase:
def longestSemiRepetitiveSubstring(self, s: str) int:
n = len(s)
izquierda
repeticiones = 0 # número de pares iguales adyacentes

para derecho en rango(1, n):
si s[right] == s[right - 1]:
repeticiones += 1

mientras repeticiones 1:
si s[left] == s[left + 1]:
repeticiones -= 1
izquierda += 1

retorno n - izquierda
`` `

-...

### 3.3 C++

``cpp
Clase Solución {
public:
int longestSemiRepetitive Substring(string s) {
int n = s.size();
int left = 0; // límite izquierdo de la ventana
int repetidos = 0; // número de pares iguales adyacentes

para (derecho = 1; derecho)
si (s[right] == s[right - 1]) repite++;

mientras que (repeticiones 1) {
si (s[left] == s[left + 1]) repite...
izquierda++;
}
}
retorno n - izquierda; // longitud de la ventana
}
};
`` `

Los tres códigos funcionan en tiempo lineal, usan memoria auxiliar constante, y están listos para sumisión.



----------------------------------------------------

## 4. Artículo del Blog – “El Bien, el Mal y el Ugly of Semi‐Repetitive Substrings”

■ **Keyword‐Rich Título:**
■ * Subestrings semi-repetitivos: El Bien, El Mal, El Ugly – Un LeetCode 2730 Deep‐ Buceo (Java, Python, C++)*
■
■ *Por qué esto importa* Este problema es un desafío de ventana deslizante de libro de texto que a los entrevistadores les encanta porque prueba:
■ 1. **Array/string traversal** – ¿puedes vigilar los pares adyacentes?
■ 2. ** Técnica de dos puntos** – ¿puede reducir/expandir una ventana de manera eficiente?
■ 3. **Manejo por caso electrónico** - ¿Qué hay de cadenas de dígitos idénticos o longitud‐1?
■
■ Desembarcar esto en su currículum demuestra dominio de algoritmos *O(n)*, una habilidad imprescindible para ingenieros de software en sistemas de producción.

-...

#### 4.1 El Bien

1. **Linear Complexity* *
La solución visita cada personaje sólo una vez. En entrevistas, los candidatos suelen caer en trampas cuadráticas. Mostrando un **O(n)** acercamiento instantánea indica la madurez algorítmica.

2. **Espacio-Eficiente* *
Sólo se utilizan algunas variables enteros: una cantidad constante de memoria extra. El equipo de trabajo aprecia soluciones que pueden escalar a insumos muy grandes.

3. * Claridad conceptual*
La ventana corredera es una *single, idea limpia*: “mover a la derecha, contar violaciones, encoger a la izquierda mientras que las violaciones confianza1”. No hay bucles anidados, no hay estructuras auxiliares de datos, fácil de explicar y depurar.

4. **Idioma-Independiente* *
La misma lógica funciona en Java, Python, C++, Vamos, etc. Esta portabilidad demuestra un profundo entendimiento de patrones algorítmicos más allá del azúcar sintáctico.

-...

### 4.2 The Bad

1. **Misunderstanding the “Pair” Count**
Un error común de novato es contar ** caracteres duplicados** en lugar de * pares iguales adyacentes*.
- **El recuento duplicado** permitiría incorrectamente cadenas como `"1212" (sin duplicados) pero rechaza `"123444"`. (duplica pero sólo un par adyacente).
- La clave es examinar los índices *adyacentes*: `s[i] == s[i+1]`.

2. **Off‐by‐One Errores**
Los límites de la ventana son una fuente frecuente de errores:
- Olvidando ajustar `izquierda' después de la eliminación del par.
- Usando `s[left] == s[left-1]` en lugar de `s[left] == s[left+1]` cuando mueve el puntero izquierdo.

3. ** Casos de emergencia**
- Cadenas de caracteres individuales ( ' vidas eternas == 1`) - la respuesta es 1.
- Cadenas identitarias (`"111111"') – la subcadena válida más larga es `2`.
- Cuerdas con muchos dígitos alternos (`"1010101"`) – el algoritmo no debe reducirse innecesariamente.

-...

#### 4.3 The Ugly

1. *Over-engineering*
Algunas soluciones introducen arrays adicionales, pilas o mapas de hash para hacer un seguimiento de ocurrencias.
- Aunque son inteligentes, añaden complejidad y posibles errores.
- La ventana corredera es **la solución mínima**; las estructuras de datos adicionales sólo aumentan el tiempo/espacio.

2. **Recursivo o Divide‐and‐Conquer Approach**
- La recuperación para la partición de subestring puede llevar a a apilar el desbordamiento en entradas largas.
- Un método divide‐y-conquer que fusiona los resultados de dos mitades todavía debe manejar pares de límites, a menudo conduce a dolores de cabeza en la esquina.

3. ** Fuerza bruta ciega* *
- Probar cada subestring (`O(n2)`), contando pares dentro de cada uno, es **slow** y se TLE en las pruebas ocultas de LeetCode.
- Peor, da a los entrevistadores la impresión de no conocer el patrón de dos puntos.

-...

### 4.4 Step‐by‐Step Walkthrough (Java)

``java
para (derecho = 1; derecho) {}
// 1. ¿El nuevo char creó un nuevo par adyacente?
si (s.charAt(right) == s.charAt(right - 1)) {
repeticiones++; // ahora tenemos una violación más
}

// 2. Arranque hasta que tengamos una violación
mientras que (repeticiones 1) {
si (s.charAt(left) == s.charAt(left + 1)) {}
repeticiones--; // quitamos un par de la ventana
}
izquierda++; // mover el límite izquierdo hacia adelante
}
}
retorno n - izquierda; // longitud de ventana más larga
`` `

*Por qué funciona esto: *
- Cuando se mueve `derecha', la única nueva violación que puede aparecer es entre 'derecho-1' y 'derecho'.
- Cuando los `repeats` exceden `1`, debemos contratar la ventana de la izquierda.
- La eliminación del personaje más izquierdo también puede eliminar un par (`izquierda ' y `izquierda+1`).
- Cada índice se procesa un número constante de veces → tiempo lineal.

-...

### 4.5 Testing Strategy

Silencio Test ← Input Silencio esperada
Silencio----------------------------
Silencio 1 Silencio `"52233" Silencio `4` Silencio `"5223"
Silencio 2 Silencioso `"5494"
Silencio 3 Silencio `"1111111" Silencio `2`
TENIDO 4 TENIDO `"121212" " TENIDO `6` TENIDO No hay pares adyacentes TENIDO
Silencio 5 Silencio `"00101022" Silencio `5` Silencio más largo antes de golpear el segundo par
Silencio 6 Silencio `"1"
Silencio 6 Silencioso `"" Silencioso `0` Silenciosa cuerda vacía (LeetCode nunca proporcionará esto)

Utilice un pequeño arnés de prueba de unidad para cada idioma (JUnit, pytest, o `assert`).

-...

### 4.6 Takeaway for

- Muestra tu razonamiento. Explique que cuenta * pares adyacentes*, no duplicados.
- **Destaque la ventana corredera**: "dos punteros, un contador de violación. ”
- ** Manejo de borde de fusión**: `"11" → respuesta `2`.
- **Añada una corta prueba de linearidad**: “Cada personaje se visita al máximo dos veces. ”

Estos puntos te hacen memorable en una entrevista técnica y muestran una mentalidad limpia y lista para la producción.



----------------------------------------------------

## 5. Pensamientos finales

Los problemas de subestring semi-repetitivos, mientras que aparentemente nicho, son una lente **grande** para evaluar sus problemas de resolución. La técnica de ventanilla deslizante es uno de los patrones de entrevista más solicitados; dominarla con problemas como LeetCode 2730 le da un borde.

Ya sea que esté codificación en Java, Python o C++, recuerde:

1. **Asociado, no duplicado* *
2. ** ventana de dos puntos**
3. **Espacio constante**
4. *Cobertura por caso*

Deja esto en tu cartera, compártela en GitHub, y estarás bien posicionado para impresionar a los gerentes de contratación y compañeros por igual. ¡Feliz codificación!