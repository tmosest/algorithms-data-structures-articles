-...
Título: LeetCode 2126. Destruyendo asteroides -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

Destruyendo asteroides – 2126. LeetCode – Un problema de entrevistas de trabajo

**Keywords:** LeetCode 2126, Destruyendo asteroides, algoritmo de salud, Clasificación, matriz de frecuencia, Java, Python, C++, Preparación de entrevistas, entrevista de ingeniería de software, Estructuras de datos, diseño de algoritmos

-...

## 1. Panorama general de los problemas

Se le da un entero «masa» – la masa inicial de un planeta – y un array `asteroides` donde `asteroids[i]` es la masa del asteroide *i*‐th.
El planeta puede chocar con los asteroides en cualquier orden**.
* Si la masa actual del planeta es **≥** la masa del asteroide, el asteroide es destruido y su masa se añade al planeta.
* Si la masa del planeta es ** **** la masa del asteroide, el planeta es destruido.

**Retorno** `verdad ' si es posible destruir * todos* asteroides, de lo contrario `falso ' .

**Constraints* *

Silencio Variable
Silencio...
TENIDO `mass` TENIDO 1 ... 10 instruccionesup conveniente5
TENIDO `asteroids.length` TENIDO 1 ... 10 instruccionesup conveniente5
Silencioso `asteroids[i]` Silencio 1 ... 10 wonsup conveniente5 recomendado/sup confianza Silencio

-...

## 2. Intuición

Para crecer lo más rápido posible, siempre debe absorber el asteroide *smallest* que el planeta puede derrotar.
Si usted absorbe un asteroide más grande primero, usted podría perder la oportunidad de crecer lo suficiente para tomar un ligeramente más grande después.

Así, la estrategia óptima es:

1. **Sorta** las masas de asteroides en orden ascendente.
2. Itea a través de la lista ordenada, agregando la masa de cada asteroide a la masa del planeta siempre que sea posible.
3. Si en cualquier momento el planeta no puede absorber el asteroide actual, nunca se puede absorber más tarde (porque todos los asteroides restantes son iguales o más grandes).

Esta estrategia codictiva garantiza que si existe una solución, la encontrará.

-...

## 3. Algoritmo (Greedy + Sorting)

`` `
// ascender
para cada uno en asteroides:
si masa >= a:
masa += a
más:
devolver falso
retorno verdadero
`` `

**Por qué funciona* *

- La masa del planeta sólo aumenta cuando absorbe con éxito un asteroide.
- El asteroide más pequeño que queda es el más fácil de absorber; si no puedes absorberlo, no puedes absorber ninguno más grande.
- Absorber el primero más pequeño sólo puede aumentar la masa del planeta, nunca disminuirla, así que la elección avaricia es segura.

-...

## 4. Análisis de la complejidad

TEN TERMIN TENIDO Tiempo ANTERIENTE Espacio ANTE
Silencio----------Prince------
Silencio Ordenar Silencio **O(n log n)** (donde *n* = `asteroids.length`) Silencio **O(1)** – clasificación en el lugar (Java `Arrays.sort`, Python `list.sort`, C++ `sort ' ) Silencio
TENIDO ANTERIORACIÓN ANTERIOR **O(n)** Silencio **O(1)**
Silencio **Total** Silencio**

■ **Nota:**
■ Si las masas de asteroides están ligadas por una pequeña constante (≤ 10 realizadassup confianza5) un *contando tipo* (`O(n + maxMass)`) puede reducir el tiempo a linear, pero el tipo clásico es más simple y lo suficientemente rápido para los límites dados.

-...

## 5. Casos de borde

Silencioso en el caso
Silencio...
Silencio **Mass ya ≥ todos los asteroides** Silencio El bucle absorberá todo; volver `true`. Silencio
Silencio **Un asteroide único más pesado que la masa** Silencio inmediatamente `false`. Silencio
Silencio **Multiple idéntico asteroides pesados** Silencio Una vez que fallas en uno, fallarás en todos los idénticos. Silencio
Silencio **Mass o tamaño de asteroides hasta 10 entradasup Intérprete/sup Intérprete** Utilizar `long` (Java) o `long long` (C++) para evitar el desbordamiento al resumir muchos asteroides. Silencio

-...

## 6. Aplicación del Código

A continuación se presentan implementaciones limpias y de entrevista en **Java**, **Python**, y **C+**. Cada uno sigue la estrategia codicioso + clasificación e incluye comentarios para la claridad.

### 6.1 Java

``java
importa java.util. Arrays;

Solución de la clase pública {}
*
* Determina si el planeta puede destruir todos los asteroides.
*
* @param masa inicial planeta masa
* @param asteroids array of asteroid masss
* @return true if all asteroids can be destroyed, false otherwise
*/
asteroides booleanos públicos Destruidos (en masa, asteroides int[]) {}
// Ordenar en orden ascendente
Arrays.sort(asteroids);

larga corriente Masa = masa // Uso largo para evitar el desbordamiento

para (int a : asteroides) {}
si (actualMass >= a) {}
corriente Masa +=a;
. ♫ ... {
devolver falso; // No puedo absorber este asteroide
}
}
retorno verdadero; // Todos los asteroides destruidos
}
}
`` `

### 6.2 Python

``python
de la importación Lista

Solución de clase:
def asteroids Destruido (yo mismo, masa: int, asteroides: List[int]) - ratio bool:
"
Solución saludable: absorber el asteroide más pequeño que puedas.
"
asteroides.sort() # Ascending
corriente = masa

para un en asteroides:
si la corriente es:
corriente += a
más:
Retorno Falso
Retorno
`` `

### 6.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
asteroides bool Destruido(en masa, vectorial implicado asteroides) {}
kind(asteroids.begin(), asteroids.end()); // Ascendencia
largo largo cur = masa; // 64-bit para evitar el desbordamiento

para (int a : asteroides) {}
si (cuerdo >= a) cur += a;
volver falso;
}
retorno verdadero;
}
};
`` `

■ **Consejo para entrevistas:**
■ Explique que usas los enteros nativos de `long' (C++), `long` (Java) o Python para manejar la masa acumulativa de forma segura.

-...

## 7. El Bien, el Mal, y el Ugly

Silencio Silencio
Silencio------------Prince------
tención ** Sencillez algorítmica** ← Greedy + tipo es intuitivo y fácil de explicar. ← Requiere clasificar, que es *(n log n)*. ← Malentender la elección codicioso puede conducir a respuestas erróneas. Silencio
Silencio **La complejidad del tiempo** tención Lo suficientemente rápido para 10 elementos opcionalesup conveniente5 objetos/sup confianza. ← Clasificación podría ser considerado exagerado si usted sabe que los datos ya están ordenados. Silencio Usar una estructura de datos ineficiente (por ejemplo, cola de prioridad con repetidas eliminaciones) puede añadir una sobrecarga innecesaria. Silencio
Silencio **Uso del espacio** Silencio In‐place sorting → O(1) extra. Silencio Sorting modifica el array de entrada – puede ser indeseable si el array debe permanecer inalterable. No usar un tipo de conteo cuando `maxMass` es pequeño; pierdes tiempo clasificando una enorme matriz. Silencio
Silencio **Manejo de edge** TEN Larga manijas desbordamiento; salida temprana en el fracaso. Silencio Ninguno. Silencio Olvidar lanzar a 'long' puede causar errores sutiles cuando la masa planetaria crece más allá de 2 instrucciones-conocidoso31 escrito/sup confianza−1. Silencio
Silencio **La claridad del cuerpo** Silencio limpio, autodocumentado. ← Requiere una breve explicación de por qué funciona codicioso. La solución puede romper la solución. Silencio

**Takeaway:** La solución codicioso + clasificación es la manera “buena”. Si estás entrevistando a una empresa tecnológica que valora *velocidad* y *implicidad*, explica la intuición, muestra el código y ganarás la entrevista.

-...

## 8. Cierre optimizado de SEO

*Si estás buscando un trabajo en ingeniería de software, dominar problemas de entrevistas como **Destruir asteroides** demuestra tu capacidad para aplicar algoritmos codiciosos y razonar sobre estrategias óptimas. Practicar tales problemas de LeetCode aumenta sus habilidades de solución de problemas, hace que su curriculum vitae se destaca, y muestra administradores de contratación que usted puede escribir código limpio y eficiente en **Java**, **Python**, o **C+**.*

■ **Listo para conquistar la próxima entrevista de codificación? * *
> Práctica problemas codiciosos: Regiones redondeadas, “Maximum Subarray”, “Stone Game”.
√ - Construir un proyecto personal que utiliza la clasificación " lógica codictiva (por ejemplo, un juego simple AI).
√ - Mantener un GitHub repo con soluciones anotadas – a los reclutadores les encanta ver código real.

¡Feliz codificación y buena suerte en tu próxima entrevista!

-..