-...
Título: LeetCode 1686. Juego de piedra VI -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recapitulación de problemas – LeetCode 1686: Juego de piedra VI

■ **Alice** y **Bob** toman turnos eligiendo una piedra de un montón de piedras.
■ Cada piedra *i* tiene dos valores:
* `aliceValues[i]` – puntos Alice recibe si toma la piedra
* `bobValues[i]` – puntos Bob recibe si toma la piedra
■ Ambos jugadores juegan **optimally** y se conocen las listas de valor del otro.
■ Después de que todas las piedras sean tomadas, quien tenga la puntuación total mayor gana
(`1` para Alice, `-1` para Bob, `0` para una corbata).

Limitaciones
`` `
1 ≤ n ≤ 105
1 ≤ aliceValues[i], bobValues[i] ≤ 100
`` `

-...

## 2. Intuición – ¿Por qué “Sort by a+b”?

Piense en la *diferencia* entre las puntuaciones finales de los dos jugadores.
Si Alice toma la piedra `i` ella gana 'aliceValues[i]`.
Si Bob toma la misma piedra más tarde habría ganado `bobValues[i]`.

En lugar de mirar los dos valores por separado, observe que **la opción que maximiza la *diferencia* `alice - bob` es equivalente a maximizar la suma `alice + bob`**:

`` `
Alice toma piedra i → +aliceValues[i] para Alice
Bob toma la piedra i → -bobValues[i] para Alice (porque los puntos de Bob no son de Alice)

Impacto de diferencia = aliceValues[i] + bobValues[i]
`` `

Por lo tanto, a cada vuelta el jugador cuyo turno es debe agarrar la piedra restante con el mayor ** valor combinado** `alicia + bob`.
Una vez que las piedras están clasificadas por esa llave, los jugadores simplemente alternan las elecciones:

* turn 0 (Alice) → tomar la primera piedra en el orden
* turn 1 (Bob) → tomar la segunda piedra
* ... y así sucesivamente.

Debido a que cada giro elimina la *mejor* piedra restante para el jugador actual, esta estrategia codictiva es óptima.

-...

## 3. Algoritm

1. Crear una lista de `n` triples `(alicia, bob, sum = alice + bob)`.
2. Ordenar la lista en **descendiente** orden de `sum`.
3. Simular el juego:
* Para incluso los índices (`0,2,4,...`) añadir `alice` a la puntuación de Alice.
* For odd indices (`1,3,5,...`) add `bob` to Bob’s score.
4. Compare los dos totales y regrese `1`, `-1`, o `0`.

Complejidad del tiempo: **O(n log n)** (excluye el sur).
Complejidad espacial: **O(n)** para la lista auxiliar.

-...

## 4. Implementaciones de referencia

#### 4.1 Java

``java
importar java.util*;

Solución de la clase pública {}
Clase privada estática Piedra {
int alice, bob, sum;
Piedra(incluido alice, int bob) {
este.alice = alice;
esto.bob = bob;
this.sum = alice + bob;
}
}

piedra int GameVI(int[] aliceValues, int[] bobValues) {}
int n = aliceValues.length;
Piedra[] piedras = nueva Piedra[n];
para (int i = 0; i)
piedras[i] = nueva Piedra(aliceValues[i], bobValues[i]);
}

Arrays.sort(stones, (s1, s2) - Integer.compare(s2.sum, s1.sum));

long aliceScore = 0, bobScore = 0;
para (int i = 0; i)
(i) == 0) {/ El turno de Alice
alice Puntuación += piedras[i].alice;
} más { // El turno de Bob
bobScore += stones[i].bob;
}
}

volver Long.compare(aliceScore, bobScore);
}
}
`` `

■ ¿Por qué 'long'?
■ Las puntuaciones pueden ser de hasta " n " 100 " ( " 107 " ), de forma segura dentro " , pero el uso " largo " elimina cualquier riesgo de desbordamiento cuando el compilador optimiza.

-...

#### 4.2 Python

``python
Solución de clase:
def stone GameVI(self, aliceValues: List[int], bobValues: List[int]) - int:
# Build list of (sum, alice, bob)
piedras = clasificadas
[(a + b, a, b) for a, b in zip(aliceValues, bobValues)],
inversa
)

alice, bob = 0, 0
i, (_, a, b) en enumerado(piedras):
si i % 2 == 0:
alice += a
más:
bob += b

retorno (alice не bob) - (alice не bob) # 1 / -1 / 0
`` `

■ La expresión " (alice " bob) - (alice " ) " es una forma concisa de volver " 1 " , 1 " o " 0 " .

-...

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int stoneGameVI(vector fieltro aliceValues, vector asignadoint frecuentemente limitado bobValues) {}
int n = aliceValues.size();
vector asignadotuple obtenidos,int,int,int títulos de piedras; // (sum, alice, bob)
Stone.reserve(n);
para (int i = 0; i)
piedras.emplace_back(aliceValues[i] + bobValues[i],
aliceValues[i], bobValues[i]);

(piedras.begin(), Stone.end(),
[](cont auto cho x, const auto cho y) {}
de vuelta conseguir se obtiene 0 título(x)
});

Alice largo = 0, bob = 0;
para (int i = 0; i) {}
(i % 2 == 0) // El turno de Alice
alice += conseguir realizada1(pies[i]);
// El turno de Bob
bob += get won2(stones[i]);
}

si (alice > bob) retorno 1;
si (alicia) devuelto -1;
retorno 0;
}
};
`` `

-...

## 5. Blog Artículo – “El Bien, el Mal y el Ugly of Stone Game VI”

■ **Keywords:** Stone Game VI, LeetCode 1686, algoritmo codicioso, clasificación, teoría del juego, codificación de entrevistas, pensamiento algoritmo, complejidad del tiempo, complejidad del espacio, entrevista de trabajo, prep

-...

### 5.1 Introduction

En entrevistas de codificación, los problemas que mezclan la teoría del juego con las estructuras de datos clásicas son comunes. **Stone Game VI** es uno de estos problemas. Si bien su declaración puede parecer intimidante, la solución óptima es sorprendentemente simple: * surtido por la suma de los dos valores de los jugadores y jugar codicioso*. Este artículo camina a través de esa visión, los obstáculos que podría encontrar, y por qué este enfoque es un gran escaparate para su cartera de entrevistas.

-...

### 5.2 El Bien - Lo que funciona y por qué

Silencio ¿Qué es lo que pasa?
Silencio...
Silencio **Sorting by `alice + bob`** Silencio El valor combinado de una piedra es la ventaja exacta que da al jugador actual sobre el oponente. Eligiendo el máximo `sum` maximiza el diferencial de puntuación a cada vuelta. Silencio
Silencio **Alternating Turns** Silencio Después de ordenar, el juego se reduce a una secuencia determinista: Alice toma índices 0, 2, 4...; Bob toma 1, 3, 5.... No es necesario adoptar nuevas decisiones. Silencio
Silencio **O(n log n) Tiempo** Silencio Ordenar domina, pero con `n ≤ 105` el algoritmo encaja cómodamente en los límites de tiempo en cualquier plataforma. Silencio
Silencio **O(n) Espacio Extra** Silencio Almacenamos una gama ligera de tuples (o structs). No es necesario un montón pesado o una recursión. Silencio
Silencio **Código Azul** Silencio La solución es unas líneas largas en cualquier idioma, por lo que es fácil de explicar en el lugar. Silencio

■ **Takeaway:** Cuando el problema se reduce a una opción óptima * global*, una estrategia avaricia a menudo supera formulaciones de programación dinámica más complejas.

-...

### 5.3 The Bad – Common Mistakes & Edge Cases

Por qué rompe la vida Fijar
Silencio-----------------------------Prince--
Silencio **Sorting by `alice` or `bob` alone** Silencio Ignora la perspectiva del oponente. Una piedra que parece buena para Alice puede ser terrible para Bob. Silencio Ordenar por `alice + bob`. Silencio
Silencio **Usando un min-heap y siempre saltando el más pequeño** tención Invierte el objetivo; usted está dando las mejores piedras. Usar un salto máximo o descender. Silencio
Silencio **Asumiendo que `int` es seguro para las puntuaciones** Silencio Mientras `int` puede retener hasta ~2 mil millones, es más seguro utilizar `long`/`long` para sumas para proteger contra futuras modificaciones. Silencio Use enteros de 64 bits para puntajes acumulativos. Silencio
Silencio **Ignorar la manipulación de la corbata** Silencio Volver a un valor incorrecto para un sorteo conduce a un veredicto equivocado. ← Compara con detalle las puntuaciones: `scoreA √≥n scoreB ? 1 : (scoreA י scoreB ? -1 : 0);` Silencio
TEN **Off‐by-one errors in turn simulation** TENS Mixing 0‐based vs 1‐based indices leads to swapped turn. TEN Use `(i &1) == 0` para los turnos de Alice si los índices comienzan a 0. Silencio

■ *Tipo de depuración* Imprima el orden ordenados y simular los primeros giros manualmente para confirmar la lógica de alternancia.

-...

### 5.4 The Ugly – When Greedy Might Fail (and How to Spot It)

La solución avaricia *siempre* trabaja para el juego de Piedra VI porque el juego es **cero-sum** con información perfecta y no estados ocultos. Sin embargo, es fácil malinterpretar el problema como un clásico “pick el valor más alto” juego (como Nim). Si los valores de piedra eran dinámicos (por ejemplo, cambiando después de cada selección) o si los jugadores tenían información oculta, una estrategia avaricia podría ser suboptimal.

¿Qué hay que ver?

* Valores de piedra Dinámica* Si la selección de una piedra altera el `alice + bob` de otros, necesitará un enfoque DP o minimax.
*Información incompleta* Si un jugador no conoce los valores del otro, no puede calcular el diferencial de puntuación exacta.
- **Multiple se mueve por turno* Si un jugador puede tomar más de una piedra por turno, la lógica de alternancia se rompe.

Al encontrar tales variaciones, empezar por enumerar algunos estados manualmente y comprobar si elegir el mejor movimiento local puede conducir a un peor resultado mundial. Esto revelará rápidamente si se necesita una solución más sofisticada (DP, minimax o búsqueda de árbol de juego).

-...

## 5.5 ¿Por qué este problema es un deber tener en tu libro de entrevistas?

1. **Demonstrates Game‐Theoretic Insight** – Impresionará a los entrevistadores con su capacidad de ver más allá de lo obvio y capturar la ventaja del oponente.
2. **Agnosticismo en idioma** – El mismo algoritmo se traduce sin esfuerzo en Java, Python, C++, Vaya, o incluso JavaScript. Demostrar que puede codificar la misma lógica en el idioma preferido de la entrevista.
3. **Scales to Constraints** – Los entrevistadores aman soluciones que manejan las limitaciones de los bordes elegantemente; nuestro algoritmo `O(n log n)` hace sólo eso.
4. **Fácil de comunicar** – En 3-5 minutos se puede esbozar el problema, el truco "a+b", y la simulación de giro, dejando al entrevistado enfocarse en su razonamiento en lugar de codificación de caldera.

■ **Pro Tip:** En una entrevista en vivo, explique primero la idea *score diferencial*. Escribe el valor combinado de una piedra, y muestra que elegir la mayor `sum` maximiza la ventaja. Entonces deja el código.

-...

### 5.6 Pensamientos de clausura

Stone Game VI es un escaparate perfecto de * elegancia algorítmica*. Su solución es:

1. *Conceptualmente limpio* – Una línea de clasificación y un solo pase.
2. **Robust** – Maneja todas las limitaciones, lazos y grandes sumas.
3. **Interview-friendly** – Short, explainable, and language‐agnostic.

Dominar este problema te proporciona un fuerte ejemplo de pensamiento codicioso, visión teórica del juego y práctica eficiente de codificación, todas las habilidades esenciales para el aterrizaje que codiciaron el papel de ingeniería del software.

-...

### 5.7 Call to Action

- **Práctica** el enfoque codicioso en una caja de arena (LeetCode, HackerRank, o su propio compilador).
- **Compartir** su solución en GitHub con un README conciso explicando el truco 'alice + bob`.
- **Discuss** las trampas que resaltamos durante tu próxima entrevista de mock.

■ Una solución limpia a Stone Game VI es una placa de calidad * código* que dice: “Puedo resolver problemas complejos con algoritmos elegantes y eficientes. ”

-...

### 6. Preguntas frecuentes

Respuesta a la respuesta
Silencio...
*¿Puedo usar un tipo estable?* tención La estabilidad no es necesaria, pero no duele si desea salida determinista. Silencio
*Qué pasa si `aliceValues[i] + bobValues[i]` ¿Es lo mismo para las piedras múltiples?* Su orden relativo no importa, ya que todas esas piedras producen el mismo diferencial de puntuación. Silencio
*¿Hay una solución lineal a tiempo?* Con valores encuadernados (≤100) se podría utilizar el conteo en **O(n + M)** donde `M = 200`. Sin embargo, los arrays contables pueden superar el beneficio para `n = 105`. Silencio

-...

## 6. Pensamientos finales

El marco “bueno, malo y feo” convierte una pregunta de entrevista aparentemente difícil en un momento de aprendizaje. Al entender *por qué* clasificar por la suma funciona, evitas las trampas comunes y presentas una solución clara y óptima que demuestra un pensamiento algoritmo fuerte.

¡Feliz codificación, y que su próxima entrevista vaya tan suavemente como el valor combinado de una piedra! 🚀

-...

*Preparado por: Tutor de Algoritmo Amistoso*
*No dude en adaptar los fragmentos de código o artículo para adaptarse a su marca y cartera personal. *