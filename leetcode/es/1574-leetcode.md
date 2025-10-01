-...
Título: LeetCode 1574. Subarray más corto para ser eliminado para hacer Array Ordenar -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1574 – “Shortest Subarray to be Removed to Make Array Sorted”

■ *Problema*: Dado un array entero `arr`, retire un sub-array contiguo (puede estar vacío) para que los elementos restantes estén en orden no-disminución. Devuelve la longitud del sub-array más corto que se puede quitar.

Dificultad para vivir Medio tiempo para vivir
Silencio----------------------------------
Ø 105 Ø 0 ≤ arrr.length ≤ 109 ¦
TENIDO Tiempo TENIDO O(n) TENIDO O(1) extra space TENIDO

A continuación se presentan soluciones de producción en **Java**, **Python** y **C+**.
Después del código nos sumergimos en un artículo de blog de sangre completa que explica el *bueno, el malo y el feo* de este problema – ideal para pulir tus notas de entrevista o escribir un artículo de búsqueda de trabajo.

-...

## 🔧 1. Solución Java

``java
importar java.util*;

Clase Solución {
int findLengthOfShortestSubarray(int[] arr) {
int n = arr.length;
// 1 / ⃣ El prefijo más largo que no disminuye
int left = 0;
mientras (izquierda + 1) se hacía arrr[izquierda] arr[izquierda + 1]) izquierda++;

// El array ya está clasificado
si (izquierda == n - 1) retorno 0;

// 2Ω⃣ Sufijo no disminuyente
int right = n - 1;
mientras (derecho √≥ 0 " pÃ3rrr [derecha - 1] י= arr[derecha]) derecho...

Inicio con los dos candidatos obvios
int ans = Math.min(n - left - 1, right);

// 4 millas ⃣ Dos puntos de fusión: mantener la parte de prefijo de la longitud i,
// mantener la parte de sufijo a partir de j, y comprobar la brecha
int i = 0, j = derecha;
mientras (i י= izquierda " p " ) {
si (arr[i] <= arr[j]) { // puede mantener arrr[i] y arr[j]
ans = Math.min(ans, j - i - 1); // delete middle
i++; // probar un prefijo más largo
} otra { // necesidad de mover sufijo puntero
j++;
}
}
devolver los ans;
}
}
`` `

■ **La complejidad**:
• Tiempo – **O(n)** (tres escaneos lineales)
• Espacio – **O(1)**

-...

## 🔧 2. Solución de pitón

``python
de la importación Lista

Solución de clase:
def findLengthOfShortestSubarray(self, arr: List[int]) - título int:
n = len(arr)

# El prefijo más largo que no disminuye
izquierda = 0
mientras que la izquierda + 1 se realizó n y arrr[izquierda] se realizó= arr[izquierda + 1]:
izquierda += 1
si la izquierda == n - 1:
retorno 0

# El sufijo más largo que no disminuye
derecho = n - 1
y arrr [derecha - 1]
derecho -= 1

as = min(n - left - 1, right) # dos triviales

i, j = 0, correcto
mientras que yo hice la izquierda y j
si arrr[i]
as = min(ans, j - i - 1)
i += 1
más:
j += 1
Retorno
`` `

■ *La complejidad*
• Tiempo – **O(n)**
• Espacio – **O(1)**

-...

## 🔧 3. C++ Solución

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int findLengthOfShortestSubarray(vector fieltro unido arr) {
int n = arr.size();
// Prefijo más largo que no disminuye
int left = 0;
mientras (izquierda + 1) se hacía arrr[izquierda] arr[izquierda + 1]) izquierda++;

si (izquierda == n - 1) retorno 0; // ya ordenados

// Sufijo más largo que no disminuye
int right = n - 1;
mientras (derecho √≥ 0 " pÃ3rrr [derecha - 1] י= arr[derecha]) derecho...

int ans = min(n - left - 1, right); // two simple deletions

// Dos puntos de fusión
int i = 0, j = derecha;
mientras (i י= izquierda " p " ) {
si (arr[i] {}
ans = min(ans, j - i - 1);
++i;
. ♫ ... {
++j;
}
}
devolver los ans;
}
};
`` `

■ *La complejidad*
• Tiempo – **O(n)**
• Espacio – **O(1)**

-...

## 📚 4. Blog Artículo – “El Bien, el Mal” el Ugly de LeetCode 1574”

■ **Título**: El Bien, el Mal el Ugly de LeetCode 1574 – Subarray más corto para ser eliminado para hacer Array Ordenar*
■ **Meta Descripción**: Master LeetCode 1574 con una profunda inmersión en su solución óptima, trampas y explicación de entrevista. Ideal para ingenieros de software que buscan impresionar a los gerentes de contratación.

-...

Introducción

Cuando los reclutadores buscan una agudeza algorítmica, a menudo le dan problemas que *mira* fácil pero ocultan los obstáculos ocultos. **LeetCode 1574** es uno de estos problemas: *Remover un sub-array para que el array restante no disminuye.* En la superficie se siente como una simple “remueva el segmento malo más grande” pregunta, pero la solución óptima hinges en una fusión de dos puntos y manejo cuidadoso de los casos de borde.

En este artículo:

- Explique por qué un enfoque ingenuo falla
- Mostrar la solución óptima **O(n)** en 3 idiomas
- Discuss the *good, the bad, and the feo* desde una perspectiva de entrevista
- Proporcione consejos de entrevista “tomada” que puede mencionar en el teléfono

-...

#### 2down⃣ El problema en inglés sencillo

Se le da un array entero `arr`. Puedes eliminar *one* sub-array contiguo (los elementos que eliminas no tienen que ser contiguos en el array final, simplemente se eliminan). Después de la eliminación, los elementos **remanentes deben ser ordenados en orden no disminuyente**.

Su tarea: devolver el número mínimo de elementos** que tiene que eliminar.

*Examples*

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
TENIDO `[1, 2, 3, 10, 4, 2, 3, 5]` TENIDO `3` TENIDO Suprímase `[10, 4, 2]` → `[1, 2, 3, 3, 5]`. Silencio
Silencio `[5, 4, 3, 2, 1]` Silencio `4` Silencio La matriz está disminuyendo estrictamente; mantenga cualquier elemento único. Silencio
Silencio `[1, 2, 3]` Silencio `0` Silencio Ya ordenados. Silencio

-...

#### 3down⃣ ¿Por qué?

Un primer pensamiento común: *“Encuentra el prefijo más largo y sufijo, luego elimina todo entre.”*
Esto le da una respuesta de `derecha - izquierda - 1`, pero no siempre es óptima. Por ejemplo:

`` `
arr = [1, 3, 5, 2, 4, 6]
`` `

- Prefijo más largo: `[1, 3, 5]`
- Sufijo más largo:
- Eliminar el medio → `3` elementos eliminados.

Pero en realidad podemos eliminar `[5, 2]` (2 elementos) y todavía tienen `[1, 3, 4, 6]` ordenados.
El defecto es que debemos mantener al menos un elemento del sufijo** que *se adapta* después del prefijo.

Otra idea ingenua: probar todas las posibles eliminaciones a través de dos bucles anidados (`O(n2)`), que pasarán el tiempo por `n = 105`.

Así que necesitamos un algoritmo **O(n)** que fusiona inteligentemente el sufijo prefijo mientras respeta la limitación de orden.

-...

### 4down⃣ The Optimal O(n) Strategy – Two‐Pointer Merge

1. **Identificar el prefijo más largo que no disminuye**
Escáner desde la izquierda hasta `arr[i]. Que ese índice sea "izquierda".

2. ** Identificar Sufijo No Disminuir*
Escáner desde la derecha hasta `arr[j-1]. Que ese índice sea "derecho".

3. **Si toda la matriz ya está clasificada** (`izquierda == n-1`), la respuesta es `0`.

4. **Initializar Respuesta** con dos candidatos obvios:
- Eliminar todo después del prefijo → `n - izquierda - 1`
- Borrar todo antes del sufijo → 'derecha'

4. *Merge con dos punteros*
- Set `i = 0`, `j = right`.
- Mientras que " yo " , izquierda " y " ,
- Si 'arr[i] Puedes quedarte con las dos.
* Eliminar el segmento medio* → candidato = `j - i - 1`.
Incremento `i` para probar un prefijo más largo.
- Else ( "arr[i] el elemento sufijo actual no puede permanecer después de `arr[i]`.
Mover `j` adelante para encontrar un elemento sufijo que es lo suficientemente grande.

4. **Retorno Mínimo**

Este algoritmo visita cada elemento al máximo dos veces → **O(n)** tiempo y **O(1)** espacio.

-...

#### 5down⃣ El Código – “Bien, el Mal”

#### 5.1 Bien - La Explicación de la Entrevista

- **Escaneo de línea** – muestra que usted entiende la importancia de * pre-computar* índices de límites.
- **Two-pointer merging** – demuestra trucos avanzados de puntero (común en “Suceso de Incremento Mayor” o “Deleciones mínimas para mantener el orden”).
- ** Manejo de maletas Edge** – el guardia `si (izquierda == n-1)` demuestra que piensa en entradas ya clasificadas.

■ *Entrevista Tip*: “En un paso lineal, puedo capturar rápidamente los límites ordenados, luego combinarlos con una técnica de dos puntos para respetar las limitaciones de orden. ”

#### 5.2 Bad – Los saltos comunes

Silencio Pitfall Silencio Reason Silencio
Silencio------------
Silencio **Ignorando la condición de “fits después”** Silencio elimina demasiados elementos o pierde una eliminación más corta. tención Compare el último elemento guardado del prefijo con el primer elemento guardado del sufijo. Silencio
Silencio **Using nested loops** Silencio O(n2) → TLE for `n=105`. Silencio Usar dos escaneos lineales y un solo paso de dos puntos. Silencio
Silencio **Casos de bordes de apariencia superior** (`arr=[1]`, todos los elementos iguales o estrictamente disminuyendo). tención puede producir `-1' o índice incorrecto.  Agregue el comprobante “ya ordenado” y mantenga “i” = izquierda” / `j  observado n’ límites. Silencio

#### 5.3 Ugly – The Hidden “Trick” That Breaks the Naïve Idea

■ **El Ugly** es la realización de que *no puedes pegar el prefijo y sufijo arbitrariamente*.
■ Es tentador pensar que puedes “esquipar” el medio y mantener el sufijo. Pero si `arr[left] > arr[right]`, el elemento sufijo no puede seguir el prefijo, por lo que debe mover el puntero sufijo hasta que encuentre un elemento "compatible".

En la práctica, muchos candidatos se quedan atrapados en esta trampa exacta, dando lugar a respuestas incorrectas.
La clave es tratar el puntero de sufijo como un **búsqueda** en lugar de un segmento fijo.

-...

#### 5down⃣ Entrevista Take‐ Aways

1. **Declara tu plan primero**
“Encontraré el prefijo y sufijo más largos, luego trataré de fusionarlos mientras mantiene el orden. ”
Esto demuestra que está estructurando la solución.

2. **Explicar el cheque de Edge‐Case* *
“Si la matriz ya está ordenada, no podemos eliminar nada. ”
Esta pequeña línea suele salir con candidatos.

3. # Discusión de la Idea de dos puntos #
“Voy a caminar por el array de izquierda y derecha, luego mover los punteros hasta que encuentre un par que mantenga el orden. ”
Destaca por qué es **linear**.

4. ** Complejidad de la mención Temprano* *
“Mi algoritmo funciona en tiempo O(n) y espacio O(1), satisfaciendo las limitaciones. ”

5. **Optional Python/Java/C++ Code Snippet**
Compartir una de las soluciones anteriores en el teléfono; los reclutadores aprecian ver que puede escribir el código correcto en el lugar.

-...

#### 5down⃣ Conclusión

LeetCode 1574 es un problema engañosamente sutil que recompensa a los que:

- Reconocer el *boundary* de prefijo ordenados/suffix
- Comprender la necesidad de un *merge* que preserve el orden
- Aplicar una técnica de dos puntos** para lograr tiempo lineal

Con las tres soluciones limpias y agnósticas más arriba, usted está listo para golpear cualquier entrevista técnica que le haga esta pregunta. Recuerde enfatizar **por qué las soluciones ingenuas fallan** – demuestra una visión más profunda del algoritmo.

¡Feliz codificación, y puede aplastar esa próxima entrevista de contratación! 🎯

-...

### 🎤 Interview Tip Cheat‐ Sheet

Silencio tóxico Qué decir
Silencio...
Silencio **Phone screen** Silencio “Encontraré primero el prefijo y sufijo más largos, y luego los fusionaré con un escaneo de dos puntos”. Silencio
"Mi solución es lineal y utiliza espacio constante, por lo que escala a la máxima limitación de 105". Silencio
Silencio **Code review** Silencio “El truco clave es asegurar que el elemento sufijo que guarda es mayor o igual al último elemento del prefijo elegido”. Silencio

-...

#### 🔗 Enlaces útiles

- LeetCode 1574 Discussion: https://leetcode.com/problems/shortest-subarray-to-be-removed-to-make-array-sorted/discuss/
- Guía Técnica de dos puntos: https://leetcode.com/articles/two-pointer-solution/
- Java Interview Prep: https://www.javaworld.com/article/3201234/learn-30-java-interview-questions.html

-...

¡Feliz entrevista! Si te resultó útil este artículo, compártalo en LinkedIn o Twitter con #LeetCode #CodingInterview. 🚀