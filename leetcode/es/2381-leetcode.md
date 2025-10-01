-...
Título: LeetCode 2381. Cartas de Cambio II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 2381 – *Shifting Letters II*: A Full‐Stack Solution (Java Silencio Python Silencio C++)
■ **El bueno, el malo y el feo - y cómo asar este problema en una entrevista de trabajo* *

-...

## 🎯 Problema Recap (Easy → Medium)

■ **Shifting Letters II**
■ Dada una cadena de minúsculas `s ' y una matriz 2-D ' turnos ' , cada entrada `[start, end, dir]` representa un rango actualizado:
■ - `dir = 1` → cambiar cada letra en 's[start ... end]` **Adelante** (`a → b`, `z → a`).
■ - `dir = 0` → cambiar cada letra en `s[start ... end]` **backward** (`a → z`, `b → a`).
■ Devuelve la cadena final después de todas las operaciones.

**Constraints* *

Silencio .
Silencio...
TENIDO `1 ≤ s.length ≤ 5·104` TENIDO `1 ≤ turnos.length ≤ 5·104` TENIDO `0 ≤ inicio ≤ extremo Silencio
Silencioso `direction  Marítima {0,1}` Silencio `s` contiene sólo letras minúsculas 

-...

♪ ♪ ♪♪ Este problema es un *Goldmine* para entrevistas

1. ** Actualización rápida + consulta de puntos** – caso de uso clásico para arrays de diferencia / sumas prefijo.
2. **Manipulación de cuerdas + modulo arithmetic** – prueba la comprensión de bajo nivel de ASCII/Unicode.
3. **La eficiencia del tiempo** – la ingenua `O(n · m)` es demasiado lenta; se espera que la óptima `O(n+m).
4. **Language‐agnostic** – se puede resolver en cualquier idioma popular; muestra que conoce las estructuras de datos independientemente de la sintaxis.

-...

## 🧠 Intuition: From “Apply Every Shift” to “Apply All Shifts at Once”

Imagina que tenías que procesar actualizaciones de 50 k en una cadena de 50 k – aplicar cada turno uno por uno sería ~2.5 billones de cambios de carácter, demasiado lento.
El truco: **graba el efecto neto para cada índice en un solo paso**.

1. **Diferencia array** – almacenar la *diferencia* entre índices consecutivos.
2. **Suma de prefijo** – transformar la matriz de diferencia en el cambio neto real para cada personaje.
3. **Aplicar el cambio neto** – envolver alrededor del alfabeto con el modulo 26.

Este es un libro de texto *range update, punto de consulta* problema.

-...

## 🏗י Step‐by‐Step Algorithm

← Paso Silencioso Descripción Silencioso Código Silencio
...------------------------------------
Silencio 1 TENIDO Crear 'diff` array de tamaño `n+1` (todas las ceros). TENIDA `int[] diff = nuevo int[n+1];` Silencio
Silencio 2 Silencio para cada `[l, r, dir]`:
" nbsp; sensiblenbsp;• `shift = dir == 1 ? +1 : -1`
" nbsp; sensiblenbsp;• `diff[l] += cambio `
" nbsp; limitadanbsp;• `diff[r+1] -= shift ' peru `diff[l] += shift; diff[r+1] -= shift;`
Silencio 3 Silencio Compute prefix sum → `net[i]` (cambio acumulativo hasta el índice `i`). Silencio `int cur = 0; for (i ...) cur += diff[i]; net[i] = cur;` Silencioso
Silencio 4 Silencio para cada personaje " c " en la posición "
" nbsp " , `shiftVal = (net[i] % 26) + 26 ' (seguros positividad)
& nbsp; afectadasnbsp;`c' = (char)('a' + (c - 'a' + shiftVal) % 26)
Silencio 5 Silencio Únete a todos los caracteres modificados → cadena final. Silencio `regresar nuevo StringBuilder(...) a String();` Silencio

¿Por qué modulo 26?
El cambio hacia adelante por `+k` o hacia atrás por `-k` equivale a `+k mod 26`.
Añadiendo 26 antes de " 26 " garantiza que el resultado no sea negativo.

-...

## 📦 Code Implementations

A continuación se presentan soluciones limpias y idiomáticas para **Java**, **Python**, y **C+**.
Todos funcionan en **O(n + m)** tiempo y **O(n)** espacio extra.

■ **Tip** – En entrevistas, pregunte si necesita manejar un número extremadamente grande de turnos (por ejemplo, > 106). Las mismas escalas de ideas de rayos de diferencia; simplemente use un acumulador de 'long' para evitar el desbordamiento.

-...

## Java (Java 17+)

``java
Clase Solución {
public String shiftingLetters(String s, int[][] shifts) {}
int n = s.length();
int[] diff = nuevo int[n + 1]; // diferencia array

// 1. Aplicar todas las actualizaciones de rango
(int[] op : shifts) {}
int l = op[0], r = op[1];
int dir = op[2];
int delta = dir == 1 ? 1 : -1; // +1 para adelante, -1 para atrás
diff[l] += delta;
diff[r + 1] -= delta;
}

// 2. Suma de prefijo + aplicar cambios a cada personaje
StringBuilder sb = nuevo StringBuilder(n);
int cur = 0;
para (int i = 0; i)
cur += diff[i];
int shift = (cur % 26) + 26) % 26; // ensure [0,25]
char base = s.charAt(i);
char newChar = (char) ('a' + (base - 'a' + cambio) % 26);
sb.append(newChar);
}
devolver sb.toString();
}
}
`` `

-...

## Python 3

``python
Solución de clase:
def shiftingLetters(self, s: str, shifts: List[List[int]) - título str:
n = len(s)
[0] * (n +1)

# Actualizaciones de rango
para l, r, dir en turnos:
delta = 1 si es diferente -1
diff[l] += delta
diff[r + 1] -= delta

# Suma de prefijo + cambios de aplicación
Cura = 0
res = []
para i, ch in enumerate(s):
cur += diff[i]
cambio = cur % 26 # Python maneja negativos bien
new_ch = chr(ord(ch) - 97 + cambio) % 26 + 97)
re.append(new_ch)
volver ".join(res)
`` `

-...

### C++ (C+17)

``cpp
Clase Solución {
public:
cambio de cadenaCartas (cadenamiento s, vector seleccionadovector seleccionado) {}
int n = s.size();
vector implicado dieff(n + 1, 0);

// 1. Actualizaciones de rango
para (auto &op : cambios) {}
int l = op[0], r = op[1], dir = op[2];
int delta = dir ? 1 : -1; // +1 adelante, -1 atrás
diff[l] += delta;
diff[r + 1] -= delta;
}

// 2. Suma de prefijo + aplicación
Resultado de cadena;
result.reserve(n);
int cur = 0;
para (int i = 0; i) {}
cur += diff[i];
int shift = (cur % 26) + 26) % 26; // normalize to [0,25]
char newChar = 'a' + (s[i] - 'a' + cambio) % 26;
result.push_back(newChar);
}
Resultado de retorno;
}
};
`` `

-...

## 📊 Complexity Analysis

Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio **Todas las 3 soluciones** Silencioso `O(n + m)` (barredor lineal sobre cadena + actualizaciones) Silencio `O(n)` (difference array + result buffer)
Silencio **La mayor magnitud del cambio en el caso** Silencioso `O(1)` por carácter (modulo 26)

¿Por qué es suficiente? #
- Cada actualización toca dos posiciones en `diff` → `O(m)`.
- Un barrido sobre `s` para construir sumas prefijas y mutar caracteres → `O(n)`.

-...

## 🔍 Good, Bad & Ugly: A Deep Dive

Silencio Silencio
Silencio------------Prince------
Silencio **Concept** Silencio Clear separation between *update* and *query* → diferencia array. Los estudiantes que sufren a menudo se olvidan de añadir el centinela `+1` (`diff[r+1] -= delta`). Los valores negativos de modulo pueden producir subflujos de `carâ (por ejemplo, `-1 % 26 = -1` en algunos idiomas). Silencio
Silencio **Implementación** Silencio One‐pass prefix sum + single `StringBuilder` / `StringBuilder`. Silencio Usando `ArrayList Haga clic enInteger confianza` o `int[]` of wrong size may cause `ArrayIndexOutOfBoundsException`. Silencio
TEN ** Casos de Edge** TEN Modulo 26 garantiza el envoltorio para cualquier cantidad de cambio. ← Olvidar `+26` antes de `% 26` da resultados negativos en Java ' C+++. Silencio En Python, olvidar convertir `shift % 26` a positivo puede todavía funcionar, pero la claridad se pierde. Silencio
Silencio **Readability** Silencioso `diff[l] += delta; diff[r+1] -= delta;` es cristalino. Silencio `for i in range(n): cur += diff[i];` es conciso pero puede ocultar la intención. Silencio Usar `cur` como un total de funcionamiento está bien; evite confundir nombres variables como `sum` (reservido palabra clave en C++). Silencio
TEN **Testing** TENIDO Crear pruebas con cambios alternativos hacia adelante/hacia atrás para asegurar el envolvimiento. Silencio Check `s="az"`, shifts=[0,1,0] → `"yz"`. Silencio Stress test with 5 × 104 operations to confirm performance. Silencio

-...

## 🎤 Interview Checklist

 ✔ Cambios en la vida
La vida... la vida...
✔ Cambios en la vida “¿Conoces la técnica del array de diferencia?” tención Mostrar usted puede transformar un problema de actualización de rango en una solución de tiempo lineal. Silencio
¿Por qué utilizamos el modulo 26? ← Demonstrate la comprensión de alfabetos cíclicos. Silencio
¿Qué hay desbordamiento? ¿Puede cambiar las cantidades ser enorme?” Silencio Discuss usando `long` o `BigInteger` si es necesario. Silencio
¿Cómo modificaría esto para una sola dirección de cambio? Silencio Hablar sobre sumas parciales vs. sumas acumulativas. Silencio
¿Qué pasa si necesitábamos preguntar la cuerda después de cada turno? Actualización de rango, búsqueda de puntos vs. suma prefijo; mencione el árbol de Fenwick para actualizaciones dinámicas. Silencio

-...

## ♥ Bonus: Ampliación de la Idea

- **Generalizar a los alfabetos arbitrarios** - sustituir `26` por `ALPHA`.
- ** Casos de prueba Multiple** – envuelve toda la lógica en un bucle y reutiliza el array 'diff'.
- **Streaming input** – en una entrevista real, usted podría transmitir la cadena y aplicar la suma de prefijo en la mosca para mantener el uso de la memoria mínima.

-...

## The Takeaway

- **Bueno**: La matriz de diferencia es *intuitiva*, *fast* y *language‐agnostic*.
- **Bad**: Una solución ingenua de `O(n·m)` es tentadora pero te atascará en los límites de tiempo.
- **Ugly**: Olvidar normalizar los valores negativos del modulo es una trampa común que bloquea su código en Java/C++.

Domina este patrón, y ganarás puntos para el pensamiento **eficiente** y **aplicación limpia**—dos cualidades que cualquier gerente de contratación ama.

-...

Cómo usar esto en tu próxima entrevista

1. **Explicar el problema** en sus propias palabras (rango actualización + consulta de puntos).
2. **Mostrar la diferencia-array truco** en una pizarra antes de codificación.
3. **Pregunta aclarando preguntas** (por ejemplo, “¿Está garantizada la cadena ser pequeña?”) – muestra la escucha activa.
4. **Write clean code** with comments (as above).
5. **Discuten la complejidad** explícitamente.
6. **Envolver** con un ejemplo de prueba rápida para demostrar corrección.

-...

## 🔚 Palabras finales

LeetCode 2381 es más que un rompecabezas de desplazamiento de cadenas – es un micro-lesson en la manipulación de datos ** eficiente**.
Implementarlo en Java, Python y C++, presentar el algoritmo claramente, y estarás listo para impresionar a los gerentes de contratación en gigantes tecnológicos, startups o tu próxima entrevista de codificación.

■ **Recordar:** La clave es *“Recordar las diferencias, luego resumirlas”*. Una vez que se internaliza eso, la misma mentalidad resuelve un enorme espectro de preguntas de entrevista (reformaciones de rango, problemas de intervalo, sumas acumulativas, etc.).

¡Feliz codificación, y que su próxima entrevista vaya a su lado!