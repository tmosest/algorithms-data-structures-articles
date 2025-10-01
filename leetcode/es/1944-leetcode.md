-...
Título: LeetCode 1944. Número de personas visibles en una cola -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
1. Código de Solución

A continuación se presentan tres implementaciones completamente independientes de la solución óptima `O(n)` para LeetCode 1944 “Número de personas visibles en una cola”.
Los tres utilizan la idea **next‐taller** (una pila monotónica bajo la capucha) y tienen la lógica idéntica.

-...

## 1.1 Java

``java
importa java.util. Arrays;

Solución de la clase pública {}

*
* Devuelve el número de personas que cada persona puede ver a la derecha.
* @param alturas array de alturas distintas
* @return array of counts
*/
int[] canSeePersonsCount(int[] heights) {}
si (alturas == nulo TENIDO alturas.length 1) {
devolver nuevo int[]{0};
}

int n = alturas. longitud;
int[] nextTaller = nuevo int[n]; // índice de primera persona a la derecha que es más alto (o n)
int[] result = new int[n];

siguienteTaller[n - 1] = n; // nadie a la derecha de la última persona
result[n] - 1] = 0;

para (int i = n - 2; i 0; --i) {
int j = i + 1; // comenzar con el vecino inmediato
int cnt = 1; // siempre puedo ver j

// Mientras j es más corto que yo, saltar todo el bloque que j puede ver
mientras (j < n " altos[j] se realizaron alturas[i]) {}
j = nextTaller[j]; // salto a la siguiente persona más alta de j
cnt++; // j mismo es visible
}

// Si terminamos porque llegamos al final de la matriz, hemos contado un extra
si (j == n) cnt...

siguienteTaller[i] = j; // tienda para futuras consultas
result[i] = cnt;
}

Resultado de retorno;
}

// Arnés de prueba simple
public static void main(String[] args) {
Solución sol = nueva solución ();
int[] h1 = {10,6,8,11,9};
System.out.println(Arrays.toString(sol.canSeePersonsCount(h1))); // [3, 1, 2, 1, 0]

int[] h2 = {5,1,2,3,10};
System.out.println(Arrays.toString(sol.canSeePersonsCount(h2))); // [4, 1, 1, 0]
}
}
`` `

-...

## 1.2 Python

``python
de la importación Lista

Solución de clase:
def canSeePersonsCount(self, heights: List[int]) List[int]:
si no alturas o len(alturas)
Regreso [0]

n = len(alturas)
siguiente_taller = [n] * n # índice de la primera persona más alta a la derecha
Resultado = [0]

# La última persona no ve a nadie
siguiente_taller[n-1] = n
resultado[n-1] = 0

para i en rango(n-2, -1, -1):
j = i + 1
cnt = 1 # siempre puede ver al vecino inmediato

mientras j  observado n y alturas [j] se realizaron alturas[i]:
j = next_taller[j] # skip whole block that j can see
cnt += 1

si j == n:
cnt -= 1

next_taller[i] = j
resultado[i] = cnt

Resultado de retorno

Prueba rápida...
si __name_ == "__main__":
sol = Solución()
print(sol.canSeePersonsCount([10,6,8,5,11,9])
print(sol.canSeePersonsCount([5,1,2,3,10]) # [4, 1, 1, 0]
`` `

-...

## 1.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector implicado puedeVerPersonsCount(vector seleccionadoint círculos altos) {}
int n = heights.size();
si (n י= 1) retorno {0};

vector implicado siguienteTaller(n, n); // índice de la primera persona más alta a la derecha
vector significado(n, 0);

// última persona ve a nadie
siguienteTaller[n-1] = n;
result[n-1] = 0;

para (int i = n-2; i 0; --i) {
int j = i + 1;
int cnt = 1; // siempre puede ver al vecino

mientras (j < n " altos[j] se realizaron alturas[i]) {}
j = nextTaller[j]; // saltar el bloque que j puede ver
cnt++;
}

si (j == n) cnt...

siguienteTaller[i] = j;
result[i] = cnt;
}
Resultado de retorno;
}
};

// prueba simple
int main() {}
Solución s;
vector h1 = {10,6,8,5,11,9};
auto r1 = s.canSeePersonsCount(h1);
para (int x : r1) cout se hizo x se hizo "
cout se hizo 'n';

vector h2 = {5,1,2,3,10};
auto r2 = s.canSeePersonsCount(h2);
para (int x : r2) cout se hizo x se hizo "
cout se hizo 'n';
}
`` `

-...

# 2. Artículo del Blog

■ **Título** – Mastering LeetCode 1944: *Número de personas visibles en una cola* – Monotonic Stack " Next‐ Técnica superior
■ **Tags** – #LeetCode #EntreviewPrep #AlgorithmDesign #Java #Python #C++ #MonotonicStack #CodingInterview

-...

## 2.1 Why This Problem Rocks in Interviews

- **Lógica de visibilidad** – Captura una condición no-trivial “línea de visión” que no es un problema clásico de la ventana deslizante o de dos puntos.
- **Scale** – Las restricciones (`n ≤ 105`) lo convierten en un parque de juegos perfecto para las estructuras de datos avanzadas: * pila monotónica*.
- **Las señales de reclutamiento** – Resolver esto en O(n) con un razonamiento claro muestra su capacidad de convertir una fuerza bruta ingenua en un algoritmo listo para la producción – exactamente lo que los roles altos demandan.

-...

## 2.2 Problema de recuperación

■ Dada una matriz `alturas' de **distintos** alturas enteros, cada elemento representa la altura de una persona que está en una cola de izquierda a derecha.
■ Una persona puede ver a otra persona a la derecha si *todas* personas entre ellas son *principalmente más cortas** que el *shorter* de los dos.
■ Devuelve un array `respuesta` donde `respuesta[i]` iguala el número de personas que la persona i-th puede ver a la derecha.

-...

## 2.3 Naïve O(n2) Brute‐Force

``text
para i = 0 ... n-1:
para j = i+1 ... n-1:
si todo el mundo entre i y j es más corto que min (alturas [i], alturas[j]):
respuesta[i] += 1
`` `

### Pitfalls

Problema en la vida ¿Por qué duele la vida
Silencio...
Silencio **Tiempo Quadratico** Silencio Para `n = 100 000`, ~1010 operaciones → time‐out. Silencio
TEN **O(1) space** TENENCIA Aceptable, pero el algoritmo es opaco para los entrevistadores. Silencio
Silencio **Hard to extend** Silencio difícil para explicar por qué funciona; los reclutadores prefieren una narrativa clara de la estructura de datos. Silencio

-...

## 2.4 Insight: Monotonic Stack

■ La observación clave:
■ *Al caminar de derecha a izquierda, una persona puede ver a toda la gente en un bloque **no creciente** hasta que la primera persona más alta bloquee la vista. *

Esto naturalmente se presta a una pila decreciente **monotónica**:
- Cada entrada de pila almacena el *index* de una persona cuya altura es ** más alta que** la siguiente entrada en la pila.
- Mientras procesamos a una nueva persona `i`, podemos ** saltar** sobre bloques enteros que son más cortos que `i`, porque cada persona dentro de tal bloque ya se sabe que es visible a `i`.

-...

## 2.5 Next‐Taller Approach (O(n) amortized)

La idea es pre-computar, por cada índice `i`, el *index de la primera persona más alta a su derecha* (`nextTaller[i]`).
Si ya sabemos `nextTaller[j]` para un vecino más corto `j`, podemos saltar toda la sub-array `[j+1 ... nextTaller[j]-1]` en un solo paso.

### Algorithm Steps

1. **Initializar**
- `nextTaller[n-1] = n` (ninguno a la derecha).
- `respuesta[n-1] = 0`.

2. **Traverso de derecha a izquierda**
- Dejar `j = i + 1` (el vecino inmediato).
- " cnt = 1 " (persona " siempre ve " j " ).
- Mientras que las alturas [j] significaban alturas [i]:
- `j = nextTaller [j]` (salto a la siguiente persona más alta de `j`).
- 'cnt+'.
- Si nos detuvimos porque `j == n`, contamos uno demasiados → 'cnt--'.
- Almacenar `nextTaller[i] = j ' y `reswer[i] = cnt`.

3. **Retorno** el array de respuesta.

■ **Por qué es correcto** – Cada `cnt` cuenta cada persona que es o *directamente* visible (`j`) o es parte de un **block** de personas estrictamente más cortas que `j` puede ver.
■ Porque `nextTaller[j]` es siempre la primera persona más alta más allá de ese bloque, nunca doble cuenta o extrañamos a nadie.

-...

## 2.6 Walkthrough Ejemplo

Ejecutemos el algoritmo en `alturas = [10, 6, 8, 5, 11, 9]`.

TENIDO i TENIDO alturas[i] TENIDO J start ANTE LAS Personas Visibles TENIDO NextTaller[i] Silencio
Silencio------------------------------------------------------
Silencio 5 Silencio 9 Silencio – Silencio 0 Silencio 6 (n)
Silencio 4 Silencio 11 Silencio 5 Silencio 1 (9)
Silencio 3 Silencio 5 Silencio 4 Silencio 1 (11)
TENIDO 2 TENED 8 TENIDO 3 TENIDO 1 (5) → saltar a 4 (11) → +1 = 2 TENIDO 4 TENIDO
TENIDO 1 TENIDO 6 TENIDO 2 TENIDO 1 (8) → saltar a 4 (11) → +1 = 2 TENIDO 4 TENIDO
TENIDO 0 TENIDO 10 TENIDO 1 TENIDO 1 (6) → salto a 2 (8) → +1 = 2 → salto a 4 (11) → +1 = 3 TEN 4 ANTE

Resultado: `[3, 1, 2, 1, 0]`.

-...

## 2.7 Complexity Analysis

TEN TERMIN TEN ANTE Complejidad
Silencio...
TENIDO Tiempo TENIDO `O(n)` amortizado (cada índice es empujado/producido al máximo una vez)
← Espacio Silencioso `O(n)` para `nextTaller` y el array de respuesta (no hay una pila explícita en el código final)

■ ¿Por qué amortizar?
■ A pesar de que el bucle interno puede funcionar muchas veces, cada índice es “desperdiciado” al máximo porque se elimina de la pila cuando se encuentra una persona más alta. Por lo tanto el número total de iteraciones de bucle sobre todo el pase es ≤ 2 n.

-...

## 2.8 Código en tres idiomas

*(Ver los fragmentos de código arriba)*

Cada implementación sigue el mismo esqueleto lógico:

``text
para mí desde n-2 hasta 0:
j = i + 1
cnt = 1 // vecino inmediato
mientras j  observado n y alturas [j] se realizaron alturas[i]:
j = nextTaller[j] // saltar sobre un bloque de personas más cortas
cnt += 1
si j == n: cnt -= 1 // contamos uno demasiado
siguienteTaller[i] = j
respuesta[i] = cnt
`` `

El código Java, Python y C++ difieren sólo en sintaxis, no en sustancia algorítmica.

-...

## 2.9 Edge‐ Lista de verificación de casos

¿Qué sucede?
Silencio...
Silencio [0] Silencio Sin gente, sin visibilidad. Silencio
Silencio 1` Silencio Devuelve `[0]` Silencio La última persona no ve a nadie. Silencio
Silencio Aumentan todas las alturas (por ejemplo, `[1,2,3,4]`) Silencio Cada persona ve sólo al vecino TENIDO El bucle de `mientras' nunca corre porque `j` nunca es más corto. Silencio
Silencio Todas las alturas disminuyen (por ejemplo, `[4,3,2,1]`) Silencio Primera persona ve a todos los demás TENIDO El bucle de `mientras' corre hasta `j == n`; restamos uno al final. Silencio

-...

## 2.10 Good, Bad, Ugly – What Interviewers Care About

Silencio Silencio
Silencio------------Prince------
Silencio **Hora** Silencio O(n) pasa todas las pruebas rápidamente. Silencio O(n2) es *unacceptable* en los límites dados. Silencioso Olvidar manejar el caso “última persona” puede dar silenciosamente `0` en lugar de `1`. Silencio
tención **Espacio** Silencioso `O(n)` arrays auxiliares (simple a reason). Silencio Muchas estructuras auxiliares pueden volar la memoria en entradas extremadamente grandes. El uso de una ingenua recursión (rebote de techo) es una trampa fea. Silencio
Silencio **Readability** Silencio Monotonic stack es un patrón de libro de texto, fácil de explicar. ← Obscure bit‐twiddling trucos puede ocultar la lógica subyacente. Silencio Sobre-commentar dentro de los bucles puede llegar a ser imprevisible; el código magro pero explicativo es mejor. Silencio
Silencio **Correcto** Silencio Saltar sobre *centre* bloques visibles no garantiza un doble encuentro. tención Manual `mientras que la lógica puede sobrecontarse accidentalmente si se olvida el caso final de la radiografía. No manejar el escenario “exactamente igual altura” (aunque el problema garantiza alturas distintas) puede romper otros problemas similares. Silencio
Silencio **Entrevista Narrative** Silencio “Me di cuenta de que una vez que conozco a la siguiente persona más alta, todas las personas en medio son visibles; por lo tanto puedo saltarlas en un salto.” “Probé primero un bucle anidado, pero fue demasiado lento”. “Me perdí en un complicado mantenimiento de pilas y olvidé actualizar el contador correctamente”. Silencio

-...

## 2.11 Interview Take‐aways

1. **Understand the geometry** – visualize the queue, picture a line of sight, and think in terms of “blocks” of people.
2. **Traducir el problema en una pila monotónica** – este es un patrón común para los problemas de “visibilidad” o “nexto mayor elemento”.
3. **Explicar el *por qué* de cada paso** – los reclutadores aman una justificación clara para por qué se puede saltar un bloque.
4. ** Casos de borde de fusión** – esto demuestra la programación defensiva. Incluso si la entrada garantiza alturas distintas, es bueno hablar de variantes de igual altura.
5. **Write limpio, código mínimo** – se puede resolver en Python, Java, o C+++; la idea central permanece igual.

-...

## 2.12 Conclusiones

■ El problema de cola “Visibilidad” es un micro-cosmos de diseño de algoritmo moderno: se encuentra en la intersección de razonamiento combinatorio y uso eficiente de la estructura de datos.
■ Resolviéndolo limpiamente en O(n) escaparates mastery sobre pilas monotónicas y elegancia algorítmica – un combo ganador para los roles de software senior.

-...

## 2.13 Más lectura & práctica

- **Siguiente Elemento Mayor** – problema clásico de LeetCode.
- ** Muro de latón (Codility)** – utiliza una pila para calcular los cambios de altura de la pared.
- ** Rectángulo Largest en Histograma** – un giro dinámico de programación en la lógica de la pila.
- **Sliding Window Maximum** – también depende de una cola monotónica.

-...

■ **TL;DR:**
■ 1. Reconocer “bloqueos visibles” → monotónico decreciente pila.
■ 2. Pre-compute `nextTaller[i]` mientras atraviesa de derecha a izquierda.
■ 3. Saltar sobre bloques, ajustar el contador, y manejar el caso del extremo de la raya.
■ 4. Aplicar en cualquier idioma; el núcleo algoritmo permanece igual.

-...

*Feliz codificación, y que su línea de vista siempre sea clara en cada entrevista! *