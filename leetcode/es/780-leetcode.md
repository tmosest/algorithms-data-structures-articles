-...
Título: LeetCode 780. Puntos de alcance -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 Mastering LeetCode 780 – Puntos de Alcance
**A Deep‐ Dive Blog Post (Java + Python + C++)**
■ *“El bueno, el malo y el feo” de este clásico rompecabezas de entrevista. *

-...

## Tabla de contenidos
1. [Norma general](#problema vista previa)
2. [Por qué este problema se mete a los entrevistadores](por qué este problema-piedras-interviewers)
3. [The Naïve Approach ' Its Pitfalls] (#the-naïve-approach)
4. [The Optimal Back‐Tracking Algorithm](#optimal-back-tracking)
5. [Step‐by‐Step Implementation](#step-by-step-implementation)
6. [Code: Java, Python, C++](#code)
7. [Time & Space Complexity](#complexity)
8. [Casos de Edge " Errores comunes] (casos de identificación)
9. [The Good, The Bad, The Ugly](#good-bad-ugly)
10. [Pensamientos finales > Consejos de entrevista](Pensamientos finales)
11. [Referencias " Lectura posterior](#referencias)

-...

## Problema de visión general ##

■ **LeetCode 780 – Puntos de Alcance**
■ Dificultad:
■ **URL:**

Dados los enteros `sx, sy, tx, ty`, determinar si puede transformar el punto `(sx, sy)` en `(tx, ty)` utilizando sólo las operaciones:
- `(x, y) → (x, x + y) `
- `(x, y) → (x + y, y) `

Todos los valores están en el rango `1 ... 10^9`.

-...

## Why This Problem Rocks Interviewers ## This-the-problem-rocks-interviewers ##

1. **Mathematical Insight** – Requiere reconocer un patrón de ingeniería inversa.
2. **Edge‐Case Awareness** – Debes pensar en el desbordamiento, la divisibilidad y las salidas tempranas.
3. **Eficiencia del espacio** – Debe resolverse sin recurrencia para evitar desbordamientos de pila en grandes entradas.
4. **Clear Algoritmic Design** – Demuestra la capacidad de transformar un proceso adelante en un proceso atrasado.

■ *Job aspirantes que clavan este problema muestran una fuerte comprensión del pensamiento algoritmo. *

-...

## The Naïve Approach < Its Pitfalls > se hizo un nombre= "el-naïve-approach >

Una búsqueda directa (BFS) de `(sx, sy)` explorar todos los movimientos posibles explotará exponencialmente.
- **Tiempo:** Sin límites; puede golpear millones de estados antes de golpear `10^9`.
- **Espacio:** No manejable para grandes rangos de entrada.
- **Practica:** Fallos en pruebas oficiales; errores TL/ML.

*Evite BFS – es el “muy” de este problema. *

-...

## The Optimal Back‐Tracking Algorithm se hizo un nombre="optimal-back-tracking"

## Core Idea

En lugar de crecer de `(sx, sy)` hacia afuera, encoger de `(tx, ty)` hacia atrás a `(sx, sy)`.

- Si el paso anterior fue el siguiente: porque la única manera de aumentar `x` es añadiendo `y`.
- Simétricamente, si `ty > tx`, el paso anterior fue `(tx, ty - tx)`.

### Usando Modulo para Skip Redundant Steps

La resta repetida del valor más pequeño equivale a " tx %= ty " (o `ty %= tx ' ) cuando el valor más pequeño es aún más pequeño que la contraparte del objetivo.
Esto colapsa muchos pasos en uno y mantiene el bucle eficiente.

### Condiciones de cancelación

1. **Success: ** `tx == sx ' plom == sy `
2. **Imposible:** `tx ' sx ' o `ty ' `
3. **Comprobación rápida:** Si `tx == ty`, sólo podemos parar si ambas coordenadas comienzan igual al objetivo o si la otra dimensión coincide después de la reducción modular.

-...

## Step‐by‐Step Implementation > > > > > >

``text
mientras que tx. Sí.
si tx == ty: # no puede seguir adelante; check divisibility
descanso
si tx .
si me gusta:
tx %= ty # skip many subtractions at once
# ty == sy → sólo una dimensión puede crecer
(tx - sx) % ty == 0
# Ty #
si tx.
tx
más:
retorno (ty - sy) % tx == 0
tx == sx y ty == sy
`` `

-...

## Code: Java, Python, C++ se hizo un nombre="code"

## Java (O(1) space)

``java
// LeetCode 780 - Puntos de Alcance
Solución de la clase pública {}
public boolean reachingPoints(int sx, int sy, int tx, int ty) {
mientras (tx >= sx " sensible= sy) {
(tx == ty) break;
si (tx > ty) {
tx %= ty;
(tx - sx) % ty == 0;
. ♫ ... {
si (tx √≥ sx) ty %= tx;
(y - sí) % tx == 0;
}
}
tx == sx ' ty == sy;
}
}
`` `

Python (Python 3)

``python
# LeetCode 780 - Puntos de Alcance
Solución de clase:
def reachingPoints(self, sx: int, sy: int, tx: int, ty: int) - título Bool:
mientras que tx. Sí.
si tx == ty:
descanso
si tx .
si me gusta:
tx %= ty
más:
(tx - sx) % ty == 0
más:
si tx.
tx
más:
retorno (ty - sy) % tx == 0
retorno tx == sx y ty == Sy
`` `

### C++ (C+17)

``cpp
// LeetCode 780 - Puntos de Alcance
Clase Solución {
public:
bool reachingPoints(int sx, int sy, int tx, int ty) {
mientras (tx >= sx " sensible= sy) {
(tx == ty) break;
si (tx > ty) {
tx %= ty;
(tx - sx) % ty == 0;
. ♫ ... {
si (tx √≥ sx) ty %= tx;
(y - sí) % tx == 0;
}
}
tx == sx ' ty == sy;
}
};
`` `

-...

## Time & Space Complexity > ## Time > Space Complexity

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio Java Silencio **O(log (max(tx,ty)))** Silencio **O(1)** Silencio
TENIDO Python TENIDO **O(log (max(tx,ty))** TEN **O(1)** TENIDO
TENIDO C++ TENIDO **O(log (max(tx,ty))** Silencio **O(1)** Silencio

*El factor logarítmico proviene de las operaciones repetidas del modulo, que reducen drásticamente las coordenadas de destino. *

-...

## Casos de bordes " Errores comunes " significa un nombre= "edge-cases "

← Caso Edge tóxico Por qué Es importante
Silencio...
TENIDO `sx == tx ' sy == ty` TEN Ya at the target TEN Vuelta `verdad ' inmediatamente ANTE
TENIDO `tx ANTERITORIO ANTERITORIO ANTERIOR ANTERIOR ANTERITORIO ANTERIOR ANTERIOR ANTERIOR TERMINARá; el cheque final devuelve `falso` Silencio
Silencio `tx == ty` pero no igual a comenzar No se puede mover más atrás Break loop y realizar la verificación de la divisibilidad
tención Grandes entradas cerca `10^9` ← Reflujo potencial si se utiliza la subtracción ¦ Utilizar el modulo para evitar muchas subtracciones ANTE

-...

## The Good, The Bad, The Ugly #1 name="good-bad-ugly"

Silencio Silencio
Silencio------------Prince------
Silencio ** Idea Algorítmica** Silencio Elegante retro-tracking reduce la complejidad de exponencial a logarítmica Silencio Requiere cuidadoso manejo de cheques de divisibilidad Silencio Ninguno si usted cae de vuelta a BFS Silencio
Silencio **Code Complexity** Silencio ~20 líneas de código limpio y legible Silencio Ninguno Silencio
Silencio **Performance** Silencio Trabaja para todos los límites de `10^9` Ninguno Silencioso BFS será TLE/MLE Silencio
Silencio **Readability** ← La aritmética modular es intuitiva para los coders experimentados TEN Algunos pueden encontrar modulo magic obscure ANTE Las soluciones Recursivas pueden desbordar la pila

■ *El “muy” aquí es principalmente el error inicial de probar BFS. Una vez retrocedido, la solución se convierte en una alegría de leer. *

-...

## Pensamientos Finales > Consejos de Entrevista > = nombre= "pensamientos finales"

1. ** Explique primero el razonamiento inverso.** A los entrevistadores les encanta escuchar el proceso de pensamiento.
2. **Mostrar el truco del modulo.** Muestra la madurez algorítmica.
3. Casos de discusión. Hable sobre cuándo `tx == ty`, o cuando una coordinación es igual a su valor inicial.
4. **La complejidad de la mención.** Prepárate para explicar por qué tu solución es `O(log n)` y no exponencial.

■ *Mastering this problem is a solid “proof‐of-concept” that you can solve hard interview questions with clean, efficient code. *

-...

## Referencias " Leer más " significar "

- Problema LeetCode 780: " https://leetcode.com/problems/reaching-points "
- Editorial & Soluciones (Java/Python/C++):
- i) https://leetcode.com/problems/reaching-points/solutions/114732/java-simple-solution-with-explanation-by-vb8h/año
- i) https://leetcode.com/problems/reaching-points/solutions/1774665/best-and-obvious-solutions-by-singhjp006-i2vk/año
- i) https://leetcode.com/problems/reaching-points/solutions/5204364/java-beats-100-by-deleted_user-aif0/

-...

### 🚀 Boost Your Interview Score
■ ¿Listo para impresionar a sus gerentes de contratación? Practica este problema, comparte tu solución en GitHub y etiqueta con **#LeetCode780 #AlgorithmDesign**. ¡Buena suerte!

-...

*SEO Palabras clave: LeetCode 780, Solución de Puntos de Alcance, Java, Python, C++, entrevista de algoritmos, entrevista técnica, consejos de entrevista de trabajo, entrevista de codificación, BFS vs back-tracking. *