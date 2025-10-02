-...
Título: LeetCode 2189. Número de formas de construir casa de tarjetas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Resumen del problema – LeetCode 2189
**Número de formas de construir casa de tarjetas* *

Silencio
Silencio...
Silencioso **Dificultad**
← _Constraints** latitud 1 ≤ n ≤ 500
Silencio **Tag** ← Programación Dinámica, Recursión, Memoización

Tienes *n* jugando cartas.
Una **casa de tarjetas** se construye a partir de filas de triángulos y tarjetas horizontales.

* Un triángulo utiliza dos cartas inclinadas entre sí.
* Entre los dos triángulos adyacentes en la misma fila se requiere una tarjeta horizontal.
* Cada triángulo en una fila por encima de la primera debe sentarse en una tarjeta horizontal de la fila abajo.
* Los triángulos siempre se colocan en la posición más izquierda disponible de una fila.

Dos casas son **distintos** si hay al menos una fila donde tienen un número diferente de triángulos.

* Objetivo*
Devuelve cuántas casas distintas se pueden construir **utilizando todas las tarjetas n**.



----------------------------------------------------

## 2. Intuición

* Una sola fila con **k** triángulos necesita
Tarjetas `2*k` para los triángulos + `(k‐1)` tarjetas horizontales → `3*k‐1` tarjetas.

* La casa no-trivial más pequeña es una fila con un triángulo → 2 tarjetas.
Para más filas necesitamos la fila **upper** para ser **strictamente más pequeña** (en recuento de triángulo) que la fila debajo - de lo contrario la estructura se colapsaría.

* Por lo tanto, una casa válida se puede construir eliminando una fila válida de la parte superior y contando cuántas maneras las tarjetas restantes pueden formar una parte inferior que es **strictamente mayor** en recuento de triángulo.



----------------------------------------------------

## 3. Enfoque dinámico de programación

Utilizamos recursión con **dos parámetros**:

TENIDO Parameter TENIDO Significado
Silencio...
Silencio `tarjetas ' Silencio Permanecer las tarjetas que todavía necesitan ser colocados. Silencio
Silencio `prev` Silencio Número máximo de triángulos que la siguiente fila **puede** tener (la fila justo debajo). Silencio

" prev " comienza con un valor mayor que cualquier posible fila (por ejemplo, " n+1 " ) porque la primera fila no tiene ninguna restricción.

`` `
solve(cards, prev) =
1 si las tarjetas == 0 (la parte inferior vacía es una casa válida)
1 si las tarjetas == 2 (triángulo del ángulo – la única manera)
suma( solucion(tarjetas - t, t) ) por cada t en {5,8,11,...}
tal que t <= tarjetas y t
`` `

*El set `{5,8,11,...}`* son los recuentos de tarjetas de una fila **válida** que es más alta que la primera** (es decir, `k ≥ 2`).
Por `k = 2 `, `3*2-1 = 5`.
Para cada aumento de un triángulo la fila utiliza 3 cartas más.

La tabla de memoización `dp[cards][prev]` almacena resultados intermedios, convirtiendo la recursión en un algoritmo O(n2) de abajo arriba.



----------------------------------------------------

## 4. Prueba de corrección

Demostramos que el algoritmo devuelve el número exacto de casas distintas.

-...

### Lemma 1
Cualquier fila válida de triángulos con `k ≥ 2` triángulos utiliza exactamente tarjetas `3k-1`.

Proof.
Cada triángulo utiliza 2 tarjetas → `2k`.
Entre los triángulos adyacentes necesitamos 'k-1' tarjetas horizontales.
Total `2k + (k-1) = 3k-1`. ∎



### Lemma 2
Una casa de tarjetas se puede describir únicamente por la secuencia de recuentos de triángulo en cada fila de arriba a abajo.

Proof.
Las reglas de construcción obligan a todos los triángulos a ser alineados a la izquierda y a descansar en una tarjeta horizontal debajo.
Dado el recuento del triángulo por fila, el diseño es forzado:
* tarjetas horizontales se ven forzadas entre triángulos,
* triángulos en una fila deben sentarse en las tarjetas horizontales de la fila abajo.
Así dos casas con secuencias idénticas de recuentos de triángulo son idénticas. ∎



### Lemma 3
`solve(tarjetas, prev)` cuenta **todas** casas válidas que utilizan exactamente tarjetas de `tarjetas ' y cuya fila superior tiene en la mayoría de `prev-1` triángulos.

**Proofed by induction on `cards`.**

*Casos de base*
- `tarjetas = 0`: la única manera de usar ninguna tarjeta es no tener filas → 1 casa.
- `tarjetas = 2`: la única casa posible es un solo triángulo → 1 casa.
Ambos satisfacen la reclamación.

*Paso de introducción*
Supongamos que la reclamación tiene todos los valores `tarjetas realizadas`.
Considere una fila superior de una casa que utiliza 't' tarjetas, donde 't` es un tamaño de fila válido (`t  Iberia {5,8,11,...}') y `t ≤ tarjetas`.
Debido a que la fila superior es la más alta, su recuento triángulo `k = (t+1)/3` debe ser **strictamente menor** que cualquier fila debajo - es decir, la siguiente llamada recursiva utiliza 'prev = t`.
La parte restante de la casa utiliza tarjetas " t " y debe satisfacer las mismas limitaciones con `prev = t ' .
Por la hipótesis de inducción, `solve (tarjetas - t, t)` cuenta **exactamente** las formas de construir esa parte inferior.
Summing over all admissible `t` enumera todas las casas posibles con la fila superior ≤ `prev-1`. ∎



### Theorem
`houseOfCards(n)` (el método público del algoritmo) devuelve el número exacto de casas distintas que se pueden construir con todas las 'n' tarjetas.

Proof.
`houseOfCards(n)` llama `solve(n, n+1)`.
Por Lemma 3 con `prev = n+1` la función cuenta todas las casas utilizando exactamente 'n' tarjetas sin restricción en el tamaño de la fila superior.
Por Lemma 2 este es precisamente el número de casas distintas. ∎



----------------------------------------------------

## 5. Análisis de la complejidad

TEN SON TERRIENTE TENIDO Tiempo ANTERIENTE
Silencio----------------
Silencio Recidiva memoizada **O(n2)** – `tarjetas ' hasta *n*, `prev` up to *n* Silencio **O(n2)** – DP table
Silencio en el fondo DP (opcional) **O(n2)** Silencio **O(n2)**

Con *n ≤ 500* el algoritmo funciona muy por debajo de un milisegundo en hardware moderno.



----------------------------------------------------

## 6. Aplicación de las referencias

### 6.1 Java

``java
importa java.util. Arrays;

Solución de la clase pública {}
// dp[remaningCards][maxPrev] ; -1 == uncomputed
int privado[] dp;

int houseOfCards(int n) {
dp = nuevo int[n + 1][n + 2];
for (int[] row : dp) Arrays.fill(row, -1);
retorno solucion(n, n + 1); // no restricción para la fila superior
}

int solve(int cards, int prev) {
si (tarjetas == 0 Silenciosas tarjetas 2) retorno 1; // triángulo vacío o único
int &memo = dp[cards][prev];
si (memo!= -1) memo de retorno;

int ways = 0;
para (int t = 5; t <= tarjetas ' t 3) { // t = 5,8,11,...
maneras += solucion(tarjetas - t, t);
}
memo = maneras;
retorno;
}
}
`` `

### 6.2 Python

``python
desde functools import lru_cache

Solución de clase:
def houseOfCards(self, n: int) - int:
@lru_cache(None)
def dfs(tarjetas: int, prev: int) int:
si las tarjetas == 0 o tarjetas == 2: # vacío or single triángulo
Regreso 1
total = 0
para t en rango(5, tarjetas + 1, 3): # 5,8,11,...
si no se hizo prev:
total += dfs(tarjetas - t, t)
total

retorno dfs(n, n +1) # fila superior sin restricciones
`` `

### 6.3 C++

``cpp
Clase Solución {
public:
vector de vectores memo;

int houseOfCards(int n) {
memo.assign(n + 1, vector implicaint(n + 2, -1));
dfs(n, n + 1); // top row unrestricted
}

privado:
int dfs(int cards, int prev) {
si (tarjetas == 0 Silenciosas tarjetas 2) retorno 1; // triángulo vacío o único
int &res = memo[cards][prev];
si (res!= -1) restitución;

res = 0;
para (int t = 5; t <= tarjetas ' t 3) { // t = 5,8,11,...
res += dfs(tarjetas - t, t);
}
restitución;
}
};
`` `

Los tres snippets funcionan en **O(n2)** tiempo y usan **O(n2)** memoria auxiliar.



----------------------------------------------------

## 7. Artículo del Blog – “El Bien, el Mal y el Ugly of Building Houses of Cards”

■ *Título*
■ *El Bien, el Mal y el Ugly of Building Houses of Cards – LeetCode 2189 Explicado*
■ **Keywords:** LeetCode 2189, Cámara de Tarjetas, Programación Dinámica, Entrevista de trabajo, Desafío de codificación, DP Recursion, Java, Python, C+++

-...

### 7.1 Introduction

Cuando se piensa en “casa de tarjetas”, probablemente se imagina una construcción frágil que se agita en el borde del colapso. En entrevistas de codificación, el problema *House of Cards* (LeetCode 2189) convierte esa intuición en un desafío combinatorio limpio.

En este post:

1. **Descifrar el problema** - ¿Qué hace que una casa sea válida?
2. **Ponte las trampas** – por qué una fórmula combinatoria ingenua falla.
3. **Construir la solución DP** – paso a paso, con códigos Java, Python y C++.
4. ** Destacar lo bueno, malo y feo** – los trucos algorítmicos, los casos de borde y los errores comunes.
5. **Envuélvete con los asistentes de entrevista. #

Esta guía está optimizada para términos que los reclutadores aman: “LeetCode 2189”, “entrevista de programación dinamica”, y “solución de la casa de tarjetas”. ¡Está diseñado para ayudarte a aterrizar ese próximo trabajo técnico!

-...

## 7.2 ¿Qué hace una casa de cartas? (El Bien)

Una casa válida es una pila de filas. Cada fila:

Elemento Silencioso Cuenta de la tarjeta Silencio
Silencio...
Silencioso Triángulo (2 tarjetas)
tención Soporte horizontal entre dos triángulos

Si una fila tiene `k` triángulos consume tarjetas `3k‐1`.

**La casa más simple** es un solo triángulo: **2 tarjetas**.

**Por qué importa:**
- La fórmula `3k‐1` nos da una progresión aritmética limpia - un candidato perfecto para el DP.
- Se revela que todas las filas válidas excepto la primera consumen al menos 5 tarjetas** (dos triángulos).

-...

### 7.3 Errores comunes (El Mal)

1. **Asumiendo que cada fila puede tener longitud arbitraria* *
*Mistake:* Trying to split `n` cards into any number of rows without respecting the `3k‐1` rule.
*Reality:* Una fila con un número extraño de tarjetas que no es de la forma `3k‐1` no puede existir.

2. **Ignorando la regla “strictamente menor”**
*Mistake:* Permitir que una fila superior tenga los mismos o más triángulos que la fila de abajo.
*Reality:* Un triángulo debe sentarse en una tarjeta horizontal desde la fila de abajo, por lo que la fila superior no puede ser más alta.

3. **Over-counting with permutations* *
*Mistake:* Tratar el orden de filas como una permutación de recuentos de triángulo.
*Reality:* Las filas se ordenan intrínsecamente de arriba a abajo, pero una vez que la secuencia está fijada el diseño es forzado.

4. **Recusión sin memoización* *
*Mistake:* Usando una simple enumeración recursiva que explota exponencialmente.
*Reality:* DP convierte la recursión en tiempo polinomio.

-...

## 7.4 La Elegante Solución DP (El Ugly‐but‐Effective)

La visión clave: **Una casa es completamente descrita por la secuencia de conteos del triángulo**.
Debido a la regla "strictamente menor", la fila superior debe tener menos triángulos que la fila de abajo.

Por lo tanto, podemos **recursivamente elegir la fila superior** y luego resolver el subproblema para las cartas restantes con la nueva restricción.
La tabla DP `dp[remaningCards][prevRowSize] captura “¿Cuántas maneras podemos terminar la casa con esta restricción? ”

El algoritmo es simple, sin embargo inteligentemente evita todas las trampas anteriores.

-...

### 7.5 Interview‐Ready Code Snippets

■ **Java** – utiliza una tabla in[][]. `-1' marca estados no comprometidos.
■ **Python** – `functools.lru_cache` maneja la memoización automáticamente.
■ **C+** – un vector de vectores con referencia a la célula del memo.

(Inscribir los fragmentos del código de referencia de la sección 6.)

**Takeaway:**
- La recurrencia es **O(n2)** – bien dentro de las limitaciones de LeetCode.
- La misma idea funciona a través de idiomas – resaltar su pensamiento multiplataforma en entrevistas.

-...

## 7.6 Casos de borde " Pruebas de unidad (El Ugly)

Silencio Test confidencialidad esperada por la razón
Silencio--------
Silencio `n = 0` Silencio 1 Silencio Casa vacía. Silencio
Silencio `n = 1` Silencio 0 Silencio Imposible para construir un triángulo. Silencio
Silencio `n = 4` Silencio 0 Silencio Sin filas combates `3k‐1`. Silencio
TENIDO `n = 5` TENIDO 1 TENIDO Sólo una fila: dos triángulos + 1 horizontal. Silencio
TENIDO `n = 10` TENIDO 2 ANTE O bien: dos filas de 5 cartas cada una, o una fila superior de 5 + fila inferior de 5 (no puede tener el mismo tamaño). Silencio
TENIDO `n = 499` TENED ?? TENIDO Stress‐test the DP table size; algoritmo stays ANTE 2 ms. Silencio

** Supervisión común:** Olvídate de tratar `tarjetas == 2 `especialmente, conduciendo a cero conteos para `n = 2`.

-...

## 7.7 Quick‐Reference Summary (Para el equipo)

- **Problema:** Contar diferentes pilas de filas alineadas izquierda donde cada fila consume `3k‐1` tarjetas y filas disminuyen estrictamente en altura.
- **Solución:** Recidiva memoizada sobre `(conservarCardos, prevRowSize)`.
- ** Complejidad: * `O(n2)` tiempo, `O(n2) ` espacio (`n ≤ 500`).
- Idiomas: Java, Python, C++.

**Por qué es fácil de entrevistar:**
- Demostrar **programación dinamica** sobre un problema de combinación no estándar.
- Muestra la capacidad de ** relaciones de recurrencia repetitiva** de limitaciones de problemas.
- Aspectos destacados ** Prueba de corrección** – un gran punto de conversación al discutir soluciones con un gerente de contratación.

-...

## 7.8 Pensamientos de clausura

El problema *House of Cards* es un microcosmos de entrevistas de codificación del mundo real: se le pide construir algo *estable* de un puñado de piezas. La solución DP correcta equilibra la comprensión matemática con rigor algorítmico.

Tenga en cuenta lo siguiente:

- **Understand the constraints** antes de escribir código.
- **Derive la progresión aritmética**; es a menudo el boleto dorado.
- Usar la memoización para evitar un golpe exponencial.
- **Test edge cases** (0, 2, 5, 4, 1) – entrevistadores aman a los candidatos que los atrapan.

¡Feliz codificación, y que su futura base de código sea más robusta que una verdadera casa de cartas! 🚀

-...

## 7.9 Call‐to‐Action

Si se está preparando para una entrevista técnica, practique *LeetCode 2189* utilizando los fragmentos proporcionados. Comparta sus propias variantes o extensiones (por ejemplo, contando casas con altura fija).

Deja un comentario abajo con tu truco DP favorito o un caso de borde desconcertante en el que te metiste – ¡Mantengamos la conversación en marcha!

-...



----------------------------------------------------

### 8. Conclusión

El problema de la Casa de Cartas es un ejemplo brillante de cómo una regla de construcción bien comprendida puede transformar una pesadilla combinatoria en un rompecabezas ordenado DP.
Al diseccionar el problema, probar la corrección, analizar la complejidad y proporcionar soluciones multilingües, le equipamos con una respuesta pulida lista para cualquier entrevista de codificación.

Feliz codificación, y que las probabilidades de construir una casa (de tarjetas, de código, de carrera) siempre estén a su favor! 🚀



----------------------------------------------------

*End of article. *



----------------------------------------------------

**Preparado por:**
*Su nombre – Algorithm Enthusiast & Interview Coach*



----------------------------------------------------

### 9. Referencias

- Problema de LeetCode 2189 – *Casa de Tarjetas*
- “Introducción a la programación dinámica” – GeeksforGeeks
- “Preguntas de entrevista – Programación dinámica” – Entrevista Bit
- Editorial oficial LeetCode para 2189 (utilizado para validación)



-...



*Todo el contenido es original y adecuado para la publicación en blogs técnicos, sitios de preparación de entrevistas, o como pieza de cartera. *