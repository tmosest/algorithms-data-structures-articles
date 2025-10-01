-...
Título: LeetCode 2543. Compruebe si punto es accesible -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 2543 – *Comprobar si el punto es alcanzable*
**Target audience** – cualquiera que se prepare para una entrevista técnica o busque dominar matemáticas algorítmicas.
**Idiomas** – Java, Python, C++
*Key Take-away* – **Puedes alcanzar \(targetX, targetY)\) de \(1,1)\) iff \(\gcd(targetX, targetY)\) es un poder de 2.**

A continuación encontrará una implementación lista para cada idioma y un artículo de estilo blog que explica el razonamiento, las trampas y las ideas de entrevista.

-...

## 1. Código

#### 1.1 Java

``java
importar java.util*;

Solución de la clase pública {}
booleano público es alcanzable(int targetX, int targetY) {
// gcd de java.lang. Matemáticas (Java 17+)
int g = Math.gcd(targetX, targetY); // o java.math. BigInteger
// Compruebe si g es un poder de dos: sólo un bit set
(g " (g - 1)) == 0;
}
}
`` `

■ ¿Por qué `Math.gcd`?**
■ Java 17+ expone `Math.gcd`. Si usted está en un JDK antiguo, sólo importa `java.math. BigInteger` o escribir una pequeña función Euclid.

### 1.2 Python 3

``python
de la importación de matemáticas gcd

Solución de clase:
def isReachable(self, targetX: int, targetY: int) Bool:
g = gcd(targetX, targetY)
# Power‐of‐two test: only one bit set
(g " (g - 1)) == 0
`` `

■ **Python 3.9+** ya incluye `math.gcd`; de lo contrario `gcd` se puede escribir manualmente.

### 1.3 C++ (GCC/Clang)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
bool isReachable(int targetX, int targetY) {
int g = std::gcd(targetX, targetY); // C++17
retorno (g " (g - 1)) == 0; // poder de dos?
}
};
`` `

■ **`std::gcd`** es parte de `traducidonumeric confianza` en C++17; `traebits/stdc+++.h] lo tira automáticamente.

■ **Tip para entrevistadores** – Si se le pide que implemente el GCD usted mismo, simplemente deje caer un clásico bucle Euclid:

``cpp
int myGcd(int a, int b) {
(b) { a %= b; swap(a, b); }
devolver a;
}
`` `

-...

## 2. Artículo de estilo Blog

■ *No dude en copiar—pasar el artículo en un blog Markdown, un post de LinkedIn o una cartera personal. *

``markdown
# Check if Point Is Reachable – The Good, the Bad, and the Ugly
Una profunda cueva en LeetCode 2543 para Java, Python & C++

## Tabla de contenidos
- [Problema general](#problema vista previa)
- [The Mathematical Insight] (#the-mathematical-insight)
- [Pasaje Algorítmico](#algorithmic-walk-through)
- [Casos de complejidad y borde](#complejidad--casos de escalera)
- [Las Pitfallas Comúnes (El Ugly)](#common-pitfalls)
- [Entrevista Consejos " Escapadas](#interview-tips)
- [Por qué importa en un proceso de contratación] (#why-it-matters)
- [Más lectura " práctica] (Leer más)
`` `

### Problema general

`` `
Usted está de pie en la coordenadas (1, 1) en una rejilla de entero infinito.
Usted puede aplicar repetidamente uno de los siguientes movimientos:

1 (x, y) → (x, y - x)
2️ (x, y) → (x - y, y)
3️ (x, y) → (2*x, y)
4️ (x, y) → (x, 2*y)

Dado dos enteros targetX y targetY (1 ≤ targetX, targetY ≤ 1e9), determinar si es posible alcanzar (targetX, targetY) de (1, 1) utilizando cualquier secuencia de movimientos.
`` `

A primera vista esto parece un problema de búsqueda de gráficos, pero es un clásico *numerario* puzzle. Un ingenuo BFS volaría – el espacio del estado está sin límites. La verdadera magia viene de entender cómo las operaciones afectan al mayor divisor común (GCD) de las dos coordenadas.

## The Good – A One‐Line GCD Check

Todo el problema se desploma en una operación **Single GCD** y una prueba *poder-de-dos*. Es por eso que la “Solución GCD de una sola línea” es popular en LeetCode:
``gcd ' (gcd-1) == 0```
trabaja en O(log min(x, y)) tiempo y espacio O(1). Los tres pasos principales son:

1. Compute `g = gcd(targetX, targetY)` (Templo Euclidean).
2. Extiende cada factor de 2: `mientras (g % 2 == 0) g /= 2;` (opcional).
3. Si el `g` restante es 1 → accesible; de lo contrario → no alcanzable.

The `g ' (g-1)` El truco es un truco de cuenta de bits que te dice si `g` tiene exactamente un bit set - es decir, `g` es 2^k.

## The Bad – Why Naïve BFS Fails

* **Infinito espacio estatal** – Los movimientos dobles coordenadas, por lo que el árbol de búsqueda explota exponencialmente.
* **El soplo de memoria** – Incluso una primera búsqueda que mantiene un `HashSet identificado(x, y) titulado` alcanzará el límite de 256 MB rápidamente para valores cercanos a 1e9.
* **Time‐out** – Repetir sustracciones `(x, y-x)` y `(x-y, y)` es equivalente al algoritmo de Euclidean, pero usted estaría escribiendo a mano en el bucle de BFS, perdiendo factores constantes.

■ **Take‐away:** En una entrevista, comience preguntando * ¿Cómo cambia el GCD bajo cada operación?* Esta pregunta naturalmente dirige la discusión hacia el algoritmo y poderes de Euclid de dos.

### Los conceptos erróneos – comunes

¿Por qué está mal?
Silencio...
Silencio *“Si una coordinación es incluso, dividirlo por 2 y seguir adelante.”* Silencio También debe considerar la paridad de la otra coordenadas y su GCD. Pasar el paso del GCD puede llevar a respuestas incorrectas cuando ambos números son extraños. tención Siempre compute el GCD primero; automáticamente representa todos los poderes de dos en ambas coordenadas. Silencio
"Use (x-y) ↔ (x+y) cuando se revierte 2*x ↔ x/2."* Silencio `x±y` mantiene el GCD invariante; revertir `2*x` como `x/2` está bien, pero 'x±' se mantiene válido porque GCD(x±y, y) = GCD(x, y). Silencio
Silencio *“Power of two = only even factors.”* tención Un poder de dos medios *todo* factores principales son 2, pero el número puede ser extraño (es decir, 1). TENIENDO `bitCount` o el `x ' (x-1)` truco para comprobar *sólo un poco se establece*, no sólo “evenidad”. Silencio

### ¿Por qué Poder de 2?

Cada vez que duplicas una coordenadas, el GCD se multiplica por 2. A partir de \(1,1)\) donde \(\gcd=1\), la única manera de conseguir un objetivo GCD aparte de 1 es aplicando repetidamente las operaciones * duplicando*. Por lo tanto, el GCD final debe ser \(2^k\). Si aparece algún factor principal extraño, nunca podrás producirlo desde \(1,1)\).

-...

## 3. Discusión de entrevistas

### 3.1 ¿Por qué este problema es entrevista de oro

* **Mathematical insight** – Demuestra cómo traducir un problema en la teoría de números (GCD, algoritmo de Euclidean).
* ** La elegancia algorítmica** – Una línea en cualquier idioma, pero el razonamiento no estrivial.
* **Edge-case mastery** – Maneja los extremos de las limitaciones limpiamente (1 ≤ valor ≤ 1e9).
* **Congruencia en el idioma cuadrado** – Muestra que puedes resolverlo en Java, Python, C++ – un plus para roles que requieren múltiples pilas de tecnología.

### 3.2 Muestra Entrevista Conversación

■ ** Interviewer:** “Estamos de pie en \(1,1)\). Podemos duplicar X, doble Y, restar Y de X, o restar X de Y. ¿Es siempre posible llegar a un punto arbitrario \(a,b)\)? ”

■ **Candidato:** “Debemos ver cómo cada operación cambia el GCD. Las subtracciones mantienen el GCD sin cambios; duplicar lo multiplica por 2. Así que desde \(1,1)\) el GCD sólo puede ser \(1,2,4,\dots\). Por lo tanto, podemos alcanzar \(a,b)\) iff \(\gcd(a,b)\) es un poder de 2. ”

■ **Entrevistador:** "Excelente. ¿Cómo codificarías eso? ”

■ **Candidato:** [Las arenas sobre la línea única mostrada arriba.]

■ **Entrevistador:** ¿Qué hay de la complejidad del tiempo? ”

■ **Candidato:** El algoritmo de Euclid funciona en \(O(\log(\min(a,b)))\). La prueba de potencia de dos es tiempo constante. En general \(O(\log n)\) tiempo y \(O(1)\) espacio.”

### 3.3 Errores comunes a Highlight

TENIDO MENSAJE TENIDO Cómo encontrarlo ANTERIOR
Silencio...
Silencio Usando `x / 2` cuando `x` es extraño durante el reverso BFS ← Producirá estados no enteros Silencio Stop reverse BFS cuando ambas coordenadas son extrañas; comprueba GCD en su lugar ←
Silencio Comprobando sólo que " g % 2 == 0` ◾ Misinterprets “poder de dos” como “incluso” 0. Silencio
Silencio Olvidar que los movimientos de resta mantienen al GCD en la vida Pensará que el GCD cambia después de 'x-y' tención Probar que `gcd(x±y, y) = gcd(x, y)` utilizando el teorema de Euclides viv

-...

## 4. Blog Artículo (SEO‐Optimized)

``markdown
# Check if Point Is Reachable – The Good, the Bad, and the Ugly
**LeetCode 2543, GCD, Power of 2, Algorithmic Pensando, Java, Python, C+* *

■ *Preparado para la preparación de la entrevista de software prep, matemáticas algorítmicas y amantes de la codificación. *

Declaración de problemas

Usted está en la coordenadas **(1, 1)** en una rejilla de entero infinito.
Usted puede realizar cualquiera de los siguientes movimientos **cualquier número de veces**:

1. `(x, y) → (x, y – x)`
2. `(x, y) → (x – y, y)`
3. `(x, y) → (2·x, y)`
4. `(x, y) → (x, 2·y) `

Dados enteros `targetX` y `targetY` (1 ≤ targetX, targetY ≤ 109), ¿puedes alcanzar `(targetX, targetY)`?

■ ** Objetivo:** Producto `True` si es accesible, de lo contrario `False`.

## 🔍 The Good – A One‐Liner Solution

Si usted piensa que este es un problema de traversal gráfico, usted está perdiendo el **Math escondido detrás de los movimientos**.
Una solución limpia y simple es:

``python
retorno math.gcd(targetX, targetY) " (math.gcd(targetX, targetY) - 1) == 0
`` `

En Java, Python y C++ esto funciona en *O(log min(x, y))* tiempo y *O(1)* espacio.
La magia reside en cómo cada operación afecta al divisor común más grande (GCD)**.

## The Mathematical Insight

* Subtracciones (`x±y`) **No cambies** el GCD.
* Doubling a coordinate multiplies the GCD by **2**.

De `(1, 1)` el GCD comienza a 1 y sólo puede convertirse en `2, 4, 8, ...`.
Así, el GCD de cualquier punto alcanzable debe ser un **poder de dos**.

## Probando GCD Invariancia

`gcd(x ± y, y) = gcd(x, y)` es un corolario del algoritmo de Euclid.
La subcontratación `y` de `x` equivale a un paso del algoritmo de Euclides; el GCD nunca cambia.

## Power of 2 Test

Un número `n` es un poder de 2 si tiene **exactamente un bit**.
El clásico truco de bits:

`` `
(n " (n-1) == 0 → cierto si n es 1, 2, 4, 8, ...
`` `

o en C++/Java/Python moderno:

`` `
bitCount(n) == 1
`` `

## Глали El Mal - ¿Por qué Naïve BFS falla

* ** Explosión estatal** – Cada doble movimiento puede empujarte dos veces más lejos.
* **Memory limit** – Incluso con un `HashSet`, almacenar todos los pares alcanzables hasta 1e9 es imposible.
* **Time‐out** – Un BFS no optimizado alcanzaría fácilmente el límite de 1 s en LeetCode.

■ *Lesson for interviewers:* Siempre pregunte *“¿Qué invariante podemos rastrear?”* y llegará rápidamente al GCD.

## The Ugly – Common Pitfalls

Por qué rompe la vida Cómo corregir
Silencio--------------------------- La vida eterna
Silencio Dividir un número impar por 2 durante la búsqueda inversa ¦ Genera estados no-integer ¦ Abort cuando ambos números son extraños; use GCD en su lugar ¦
tención de chequeo `g % 2 == 0` Silencio interpreta “poder de 2” como “incluso” 0. Silencio
Silencio Ignorando que la resta conserva los valores intermedios engañosos de GCD en la solución

## 🚀 Interview Tips

1. ** Explique primero la intuición del GCD. #
2. *Mostrar el poder de dos condiciones* usando trucos de bits.
3. **Discusa la complejidad del tiempo**: El algoritmo de Euclid funciona en tiempo *logarítmico*.
4. ** Casos de borde de fusión**: `targetX` o `targetY` equivale a 1; ambas coordenadas extrañas pero GCD 1 → alcanzable.

## 🎁 Why It Matters in Hiring

* ** Demostra profundidad** – La teoría del número muestra que puedes pensar más allá de la fuerza bruta.
* **Language‐agnostic** – Solvable en Java, Python y C++.
* **Eficiente** – Conoce los estrictos límites de tiempo y memoria de LeetCode.
* **Stand‐out skill** – Un candidato que explica esto elegantemente gana puntos de brownie extra.

## 📚 Further Practice

- LeetCode: [Número de maneras de reorganizar una cuerda](https://leetcode.com/problems/number-of-ways-to-rearrange-a-string/)
- HackerRank: [GCD LCM Challenge](https://www.hackerrank.com/challenges/gcdlcm)
- Codeforces: [Subtractions and Multiplications](https://codeforces.com/problemset/problem/1472/C)

`` `

### Why It Matters in a Hiring Process

* ** Capacidad cuantitativa** – Funciones que implican estructuras de datos, criptografía o código crítico de rendimiento buscan candidatos que puedan identificar invariantes.
* **Código limpio* La línea única demuestra dominio sobre funciones incorporadas como `math.gcd`, `std::gcd`, o 'BigInteger' de Java.
* **La gestión del tiempo** – Pasas minutos probando el teorema y segundos codificación; eso muestra eficiencia bajo presión de entrevista.

■ **Pro Tip:** Par el artículo con una sesión de codificación en vivo en un sitio web de cartera. Mostrar la prueba de tiempo de ejecución contra valores aleatorios 1e9 para convencer a los reclutadores de su confianza.

-...

## 5. Lectura adicional

1. ** “Teoría de Númber para los programadores”** – Una serie de artículos que explican GCD, LCM y aritmética modular en un contexto de programación.
2. ** “El Algoritmo de Euclid en O(log n)”** – explicación de algoritmo clásico con pseudocódigo.
3. **LeetCode discusión** – Buscar “2543 GCD” para ver discusiones comunitarias sobre variaciones.

-...

■ **End of article. #
`` `

-...

## 5. Resumen

* **Tres idiomas, el mismo algoritmo** – el cheque GCD de una línea.
* **Evite naïve BFS** – el espacio estatal es infinito; la matemática le da una solución de tiempo constante.
* **Entrevistar el éxito** – muestra el razonamiento matemático, la elegancia algorítmica y la competencia entre bastidores.
* **Coloquio de impacto** – Demuestra la capacidad de un candidato para convertir un problema de fuerza bruta en una solución limpia y teórica, exactamente lo que quieren los reclutadores de tecnología.

-...

## Palabras finales

- *Si usted está construyendo un sitio web personal o un poste de blog, copiar el Markdown arriba. *
- *Confíe en la descripción del problema para que coincida con el estilo de su cartera. *
- *Recuerde incluir los tres fragmentos de código y el diálogo de entrevista; a los reclutadores les encanta ver tanto el código como el proceso de pensamiento. *

¡Feliz codificación, y buena suerte en la preparación de la entrevista!
`` `

-...

Siéntase libre de ajustar los encabezados, agregue imágenes (por ejemplo, un diagrama de la red se mueve), o incruste los fragmentos de solución en bloques de código. El objetivo es mostrar profundidad de comprensión manteniendo la explicación concisa y amigable.
`` `

-...

Con el artículo y los tres snippets de solución que está totalmente equipado para mostrar **LeetCode 2543** como un testamento de su algoritmo y habilidades matemáticas. ¡Feliz codificación y buena suerte en tu próxima entrevista!