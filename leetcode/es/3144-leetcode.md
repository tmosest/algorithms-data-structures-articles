-...
Título: LeetCode 3144. Partición mínima de subestring de la frecuencia de caracteres iguales -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 3144 – Parte mínima de subestring de igual carácter Frecuencia
■ **LeetCode ← Programación Dinámica Silencio O(n2·26) *

-...

## TL;DR
Dada una cadena de minúsculas `s`, dividirla en las subestrings más pequeñas posibles de tal manera que * cada subestring es “balanceado”* – cada personaje en la subestring aparece el mismo número de veces.
Resolvemos el problema con un DP clásico que funciona en **O(n2·26)** tiempo y **O(n)** espacio.

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencioso **C+** Silencio O(n2·26)
Silencio **Java** Silencio O(n2·26) Silencio
Silencioso **Python** Silencio O(n2·26)

-...

## 1. Reposición de problemas

■ **Minimum Substring Partition of Equal Character Frequency**
■
■ ** Entrada: ** `s` - una cadena de longitud `1 ... 1000` que contiene sólo letras minúsculas.
■ **Resultado:** el número mínimo de subestrings en una partición de `s` donde cada subestring es *balanceado*.
■ Una subestring es **balanced** si todos los caracteres que aparecen en ella ocurren el mismo número de veces.

Ejemplo
`` `
s = "ababcc"
particiones válidas: ("abab", "c", "c") , ("ab", "abc", "c") , ("ababcc")
particiones inválidas: ("a", "bab", "cc") , ("aba", "bc", "c") , ("ab", "abcc")
`` `

-...

## 2. Intuición " Estrategia "

* Consideramos la cuerda de izquierda a derecha.
* Let `dp[i]` be the minimal number of balanced substrings needed to cover the prefix `s[0 ... i]`.
* Por cada `i` miramos hacia atrás e intentamos poner fin a un subestring equilibrado en `i`.
* Mientras se mueve el puntero inicial `j` desde `i` hasta `0` mantenemos la frecuencia de cada personaje en `s[j ... i]`.
* Si la ventana actual es equilibrada, podemos terminar la partición en `i` como `dp[j-1] + 1`.
* La respuesta es `dp[n-1]`.

La ventana corredera que comprueba *balancedness* es **O(26)** por paso (sólo 26 letras).
Así, la complejidad general es **O(n2·26)**.

-...

## 3. Prueba de corrección

Demostramos que el DP descrito anteriormente produce la partición óptima.

### Lemma 1
Para cualquier índice `i`, `dp[i]` equivale al número mínimo de subestrings equilibrados necesarios para cubrir el prefijo `s[0...i]`.

*Proof. *
Mostramos por inducción sobre 'i'.

*Base:* `i = 0`.
La única subestring es `s[0]`.
Si es equilibrado (siempre es cierto porque un personaje ocurre una vez) `dp[0] = 1`.
De lo contrario no existe partición, pero el problema garantiza al menos una partición existe, por lo que la lema sostiene.

*Paso de introducción:*
Supongamos que la lema contiene todos los índices " realizados i " .
When computing `dp[i]` examinamos cada posible inicio `j` del último subestring: `j  Iberia [0, i]`.
Si `s[j...i]` es equilibrado, entonces el resto de la cadena `s[0...j-1]` se puede dividir de forma óptima en subestrings dp[j-1]` por la hipótesis de inducción.
Por lo tanto `dp[j-1] + 1` es un tamaño de partición factible para prefijo `i`.
Tomar el mínimo sobre todo lo posible " j " da el tamaño óptimo para " i " .
Así, `dp[i]` es óptimo. ∎



### Lemma 2
El procedimiento que mantiene las frecuencias de carácter al analizar hacia atrás identifica correctamente si `s[j...i]` es equilibrado.

*Proof. *
Mantenemos un array `freq[26]` donde `freq[c]` cuenta los casos de letra " c " en la ventana actual.
Después de añadir `s[j]`, recomputamos `minFreq ' y `maxFreq ' entre todos `freq[c] ît 0`.
`minFreq == maxFreq` iff cada frecuencia no cero equivale al mismo valor, que es precisamente la definición de una subestring equilibrada. ∎



### Theorem
El algoritmo devuelve el número mínimo posible de subestrings equilibrados que cubren toda la cadena `s`.

*Proof. *
Por Lemma adultnbsp;1, `dp[n-1]` es óptimo para toda la cadena.
El algoritmo produce `dp[n-1]`.
Por lo tanto el algoritmo es correcto. ∎



-...

## 4. Análisis de la complejidad

****Time:**
* El bucle exterior sobre `i` (`n` iterations).
* Loop interior sobre `j` (`≤ n` iterations).
* Para cada `j` actualizamos las frecuencias en **O(1)** y verificamos el equilibrio en **O(26)**.
→ `O(n2·26)` ♥ `O(n2)` para `n ≤ 1000`.

* **Espacio*
* `dp` array: `O(n)`.
* Conjunto de frecuencias: `O(26)`.
→ `O(n)` total.



-...

## 5. Implementaciones de referencia

A continuación se encuentran soluciones limpias, comentadas y listas para pasar en **C+**, Java**, y Python**.
Los tres siguen la misma estrategia del DP.

-...

## 5.1 C++ (GNU C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
// Ayudante a probar si una ventana es equilibrada
bool estático esBalanced(cont array observadoint, 26 con frecuencia) {}
int mn = INT_MAX, mx = 0;
para (int f : freq) {
(f == 0) continuar;
mn = min(mn, f);
mx = max(mx, f);
}
retorno mn == mx; // mn==mx iff todas las frecuencias no cero iguales
}

int minimumSubstringsInPartition(string s) {
int n = s.size();
vector significado dp(n, n); // dp[i] = subestrings mínimos para prefijo [0,i]
para (int end = 0; end יnt; ++end) {
matriz obtenida, 26 contacto francés {}; // cero
para (int start = end; start >= 0; --start) {
freq[s[start] - 'a']++; // extender la ventana a la izquierda
si (esBalanced(freq)) { // ventana [start,end] es equilibrado
int candidate = (start == 0) ? 1 : dp[start - 1] + 1;
dp[end] = min(dp[end], candidate);
}
}
}
dp.back();
}
};
`` `

-...

### 5.2 Java (Java 17)

``java
importar java.util*;

Solución de la clase pública {}
// Compruebe si la matriz de frecuencia actual representa una subestring equilibrada
booleano estático privado esBalanced(int[] freq) {
int min = Integer.MAX_VALUE, max = 0;
para (int f : freq) {
(f == 0) continuar;
min = Math.min (min, f);
max = Math.max(max, f);
}
retorno min == max;
}

mínimo público SubstringsInPartition(String s) {
int n = s.length();
int[] dp = nuevo int[n];
Arrays.fill(dp, n); // gran valor inicial

para (int end = 0; end יnt; end++) {}
int[] freq = nuevo int[26];
para (int start = end; start >= 0; start--) {}
freq[s.charAt(start) - 'a']+;
si (estáBalanced(freq))) {}
int cand = (start == 0) 1 : dp[start - 1] + 1;
dp[end] = Math.min(dp[end], cand);
}
}
}
dp[n - 1];
}
}
`` `

-...

## 5.3 Python 3 (3.11)

``python
de la importación Lista

Solución de clase:
@staticmethod
def is_balanced(freq: List[int]) - conviene bool:
""Retorno Verdadero si todas las frecuencias no cero son iguales.""
mn, mx = Ninguno, ninguno
para f en freq:
si f == 0:
continuar
si mn es Ninguno o f < mn:
mn = f
si mx es Ninguno o f > mx:
mx = f
retorno mn == mx

def minimumSubstringsInPartition(self, s: str) - título int:
n = len(s)
dp = [n] * n # dp[i] = min subestrings for prefix [0,i]

para fines en rango(n):
[0] * 26
para comenzar en rango(fin, -1, -1):
freq[ord(s[start]) - 97] += 1
si auto.is_balanced(freq):
cand = 1 si comienza == 0 más dp[start - 1] + 1
dp[end] = min(dp[end], cand)

retorno dp[-1]
`` `

-...

## 6. Blog Post – “El Bien, el Mal, y el Ugly of Balanced‐Substring Partitioning”

### 6.1 Introduction

Si usted es un candidato de ingeniería de software mirando entrevistas de alta tecnología, probablemente ha visto LeetCode **3144 – Parte mínima de subestring de la frecuencia de caracteres iguales**.
Es un *medium‐difficulty* DP puzzle que es un gran escaparate de habilidades de solución de problemas.
Vamos a diseccionar por qué este problema es un trabajo-interview oro‐mine, explorar el elegante DP que lo resuelve, y hablar de las trampas que pueden tropezar con usted.

■ **Keywords**: LeetCode, preguntas de entrevista, programación dinámica, subestrings equilibrados, entrevista de trabajo, ingeniero de software, C++, Java, Python, pensamiento algoritmo.

-...

### 6.2 El Bien - Lo que lo hace una gran pregunta de entrevista

Por qué es válida
Silencio...
tención **Clear Constraints** tención Duración ≤ 1000, sólo letras minúsculas – permite soluciones O(n2) sin preocuparse por los límites de tiempo. Silencio
TEN **DP‐Friendly** TEN La propiedad óptima de la partición conduce naturalmente a un DP unidimensional. Silencio
Silencio **Multiple Languages** ← Solvable en C+++, Java o Python – demuestra versatilidad del lenguaje. Silencio
Silencio **Logical Decomposition** Silencio Lo rompes en “es esta ventana equilibrada?” y “¿podemos terminar una partición aquí?” – bueno para probar la comunicación. Silencio
Silencio **Edge‐Case Rich** ← Las cuerdas individuales o todas las letras son triviales, pero los patrones mixtos (por ejemplo, “ababcc”) te empujan a probar la equilibrio correctamente. Silencio

Los entrevistadores aman problemas donde existe un DP ** limpio y provable**, porque le permite explicar su razonamiento paso a paso y recibir información inmediata sobre la corrección.

-...

### 6.3 Las malas – trampas comunes y errores

1. **Misreading “balanced”* *
*Usted podría pensar que una subestring es equilibrada si *algunos* caracteres son iguales, no *todo* que aparecen. *
La condición correcta es **todas las frecuencias no cero son idénticas**.

2. **Using Extra Data Structures* *
*Muchos candidatos construyen un `Map realizadoCaracter, Integer `` dentro del bucle interior. *
Si bien es funcional, esto añade sobrecarga; un array de tamaño 26 es más rápido y más fácil de razonar.

3. **Forgetting the Prefix DP Transition**
La recurrencia `dp[end] = min(dp[end], dp[start-1] + 1) es esencial.
Skipping the `dp[start-1]` part gives wrong responses for prefixes that already contain several balanced substrings.

4. **Boundary Off‐By-One**
Cuando `start == No hay prefijo izquierdo.
Olvidar manejar esto correctamente lleva a índices negativos o a resultados incorrectos.

5. **Subestimación de la ejecución**
Usted podría pensar que `O(n2·26)` es "rápido", pero escribiéndolo incorrectamente (por ejemplo, frecuencias recomputantes desde el arañazo en el bucle interior) lo empujarán hacia 'O(n3)` y el tiempo fuera.

-...

### 6.4 The Ugly – What to Watch For in Your Own Code

* Recomputación innecesaria* *
Algunas soluciones ingenuas recomputan todo el array de frecuencia para cada par `(start, end)`.
El cheque O(26) es barato, pero la reconstrucción de la matriz cada vez cuesta O(n) y rompe el presupuesto del tiempo.

* **Wrong Balancedness Check* *
Un error frecuente es comparar `freq.min()` y `freq.max()` sobre *all* 26 letras, incluyendo ceros.
Puesto que los ceros bajan `min`, usted va a marcar incorrectamente ventanas como desequilibrado.
La clave es saltar cero frecuencias.

* **DP Array Initialization* *
Establecer `dp[i]` a `i+1` (caso peor) es seguro, pero inicializarlo a `n` (longitud de la cuerda) es más intuitivo.
No llenarlo correctamente puede dejar valores altos que nunca se actualizan.

* ** Leak de memoria en C++**
Olvídase de `arrayo realizado, 26 `freq {};` o utilizando un 'in freq crudo[26] ` que no se restablece cada `end` contaminará las ventanas posteriores.

-...

### 6.5 Walkthrough – The Clean DP You'll Tell Your Interviewer

■ *“Mantendremos un DP de 1’D para prefijos y deslizaremos una ventana hacia atrás, actualizando un array de frecuencia de 26’size. Cuando esa ventana está equilibrada actualizamos la entrada DP.”*

1. **Definición DP**
`dp[i] = min number of balanced substrings for prefix up to i`.
*¿Por qué 1-D?* Porque sólo necesitamos la partición óptima para el prefijo anterior – no se requieren tablas 2-D.

2. Escaneo de fondo
Para cada "fino", mueva `comienza' hacia la izquierda, actualizando `freq[s[s]].
Comprobar equilibrio en O(26).

3. * Prueba de fondo*
Use `min` y `max` de frecuencias no cero.
`min == max` → balanceado.

4. **Transición**
`candidato = dp[start-1] + 1` (o `1` si el inicio es 0).
Mantenga el mínimo sobre todos los inicios factibles.

5. Resultado**
`dp[n-1]` es la respuesta óptima.

-...

### 6.6 Consejos de práctica

Silencioso Cómo dominar la vida
Silencio...
Silencio **Implement All Three Languages** Silencio Shows puedes traducir la lógica a C+++, Java y Python. Silencio
Silencio **Write Unit Tests** tención Validate en cadenas triviales, cuerdas todas iguales, patrones alternantes y cadenas aleatorias. Silencio
Silencio **Explicar Mientras Codificación** Silencio Camina a través de actualizaciones 'dp`, mantenimiento de frecuencias y cheques equilibrados - entrevistadores les encanta el razonamiento verbal. Silencio
Silencio **Time Your Runs** Silencio En LeetCode, ejecute 5 casos de prueba al azar y note el tiempo de ejecución – asegura que su solución es eficiente. Silencio

-...

### 6.7 Conclusiones

LeetCode 3144 es más que un problema del DP de “medio”; es un **compacto escaparate de habilidades clave de entrevista**: análisis de limitaciones limpias, programación dinámica, manejo minucioso del borde y aplicación eficiente.

Al dominar el DP mostrado arriba y entender los obstáculos comunes, usted estará listo no sólo para responder la pregunta, sino para impresionar a sus entrevistadores con lógica clara y código robusto.

**Feliz codificación, y que sus entrevistas de trabajo sean tan equilibradas como las subestrings que va a particionar!**

-...

### 6.8 Palabras finales

Si se está preparando para una entrevista de ingeniería de software, incluya LeetCode **3144** en su lista de práctica.
La solución DP es lo suficientemente directa como para codificar en 30 minutos, pero el razonamiento detrás de ella es lo suficientemente profundo para ganar elogio de los entrevistadores mayores.

Buena suerte, y recuerde: * las soluciones equilibradas son a menudo las mejores! *

-...

### 7. Lista de verificación para la retirada

1. **DP on prefixes** – `dp[i] = min(dp[j-1] + 1)` sobre todas las ventanas equilibradas `[j ... i]`.
2. **O(26) cheque equilibrado** – compare min y max de frecuencias no cero.
3. **Cuidado con ceros** – deben ser ignorados al determinar la equilibrio.
4. ** Manejo del caso de Edge** – `comienza == 0` → candidate = 1.
5. ** Prácticas óptimas específicas de idiomas** – cero-inicialización, verificación de límites y funciones de ayuda claras.

Use las implementaciones de referencia arriba como punto de partida, tweak them to fit your style, and practice explaining the algoritmo out loud – that's what makes you a standout candidate. 🚀

-...



■ **Author:** Tu amigable Mentor de Algoritm*
■ **Fecha:**
■ **Tags:** LeetCode, preparación de entrevistas, programación dinámica, C+++, Java, Python, subestrings equilibrados, preguntas de entrevistas algoritmoicas.

-...



### 8. Observaciones finales

Ya sea que esté codificación en C++, Java o Python, la solución DP arriba es una forma *canónica* para abordar LeetCode 3144.
Siéntase libre de adaptarlo, añadir la memoización o experimentar con ventanas correderas.
Buena suerte, y que sus subestrings equilibrados siempre sean perfectamente equilibrados! 🚀



-...



*Preparado para: Ingenieros listos para entrevistas. *
*Sea libre de soltar este código en su repositorio o GitHub Gist y lo refiera en su cartera. *



-...



#



-...



[End of Technical Note]