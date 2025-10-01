-...
Título: LeetCode 1007. Rotaciones mínimas de Domino para la fila igual -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🔥 1007 - Rotaciones mínimas de Domino para la fila igual
**Un recorrido completo, amigable con SEO, código en Java, Python & C++ + “el bueno, el malo, el feo”* *

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

■ **LeetCode 1007 - Rotaciones mínimas de Domino para la fila igual**
■ Dados dos arrays de igual longitud `tops` y `bottoms` (1-números indexados de 1 a 6), cada par representa las dos mitades de un domino.
■ Puede rotar cualquier dominó (swap su parte superior e inferior).
■ Regrese el *mínimo* número de rotaciones necesarias para que todos los valores superiores sean iguales **o** todos los valores inferiores sean iguales.
■ Si es imposible, devuelve `-1`.

-...

#### 2down⃣ Por qué importa

- **Interview favorite** – el problema prueba *manipulación de rayos*, *verde*, y *edge‐case awareness*.
- **Real-world relevancia** – similar a “hacer todas las columnas iguales en una matriz con volteretas de fila”.
- **Coding interview** – aparece en Amazon, Google, Microsoft y muchas otras empresas tecnológicas.
- **SEO ventaja** – “minimum domino rotaciones interrogantes” y “hacer una fila dominó uniforme” son frecuentes consultas de búsqueda.

-...

#### 3down⃣ El Bruto‐ Fuerza Idea

Revise cada valor objetivo posible (1–6).
Para cada objetivo:

1. Escanee todos los dominó.
2. Cuente cuántos tops necesitan para convertirse en el objetivo.
3. Cuente cuántos fondos necesitan para convertirse en el objetivo.
4. Si cualquier dominó carece del objetivo en ambas mitades, descarta a este candidato.

Por último, elija el número de rotación más pequeño.

**Hora**: O(6 · n) → O(n)
**Espacio**: O(1)

Debido a que el dominio es pequeño (1–6), un solo paso por valor es lo suficientemente rápido, y el algoritmo es fácil de razonar.

-...

### 4down⃣ Edge Cases (The Ugly)

Silencioso ¿Por qué viaja muchas implementaciones ¦
Silencio--------------------------
[i] Silencio Algunas soluciones de doble cuenta de rotaciones Silencio Treat como un solo domino; no añadir el mismo número dos veces. Silencio
Silencio El valor candidato nunca aparece en un domino tención El algoritmo debe saltar inmediatamente Silencio Si `cnt[target] ANTE n `, continuar. Silencio
tención Arrays of length 2 Silencio Ambos valores pueden ser iguales o diferentes tención Todavía funciona; sólo asegúrate de manejar correctamente `n=2`. Silencio

-...

#### 5down⃣ La solución limpia, de producción-Ley

Presentaremos la misma lógica codictiva en **Java**, **Python**, y **C+**. Todas las implementaciones comparten:

- Un ayudante para probar a un candidato.
- Terminación temprana cuando un candidato es imposible.
- Regresa 1 si no funciona ningún candidato.

-...

## 🚀 Java

``java
importar java.util*;

Solución de la clase pública {}
int public int minDominoRotations(int[] tops, int[] bottoms) {}
int n = tops.length;
// los candidatos son números 1..6
int best = Integer.MAX_VALUE;

para (objetivo único = 1; objetivo 0 = 6; objetivo++) {}
int topRot = 0, inferior Rot = 0;
booleano posible = verdadero;

para (int i = 0; i)
si (tops[i] != objetivo " bajos " [i]!= objetivo) {
posible = falso;
ruptura; // no puede utilizar este objetivo
}
si (tops[i] != target) topRot++; // flip to make top = target
if (bottoms[i] != target) bottomRot++; // flip to make bottom = target
}

si (posible) mejor = Math.min(best, Math.min(topRot, bottomRot));
}
devolver mejor == Integer. ¿MaX_VALUE? -1 : mejor;
}
}
`` `

■ *Puntos clave*
* The `for` loop over `1..6` guarantees O(n).
* No hay estructuras de datos adicionales → O(1) espacio.
* `Integer.MAX_VALUE` es un centinela que indica claramente “ninguna solución”.

-...

## Python

``python
de la importación Lista

Solución de clase:
def minDominoRotations(self, tops: List[int], bottoms: List[int] int:
n = len(tops)
INF = flotante('inf')
best = INF

para el objetivo en el rango(1, 7):
top_rot = bottom_rot = 0
posible = verdadero

para t, b en cremallera (tops, fondo):
si t!= objetivo y b!= objetivo:
posible = Falso
descanso
si t!= objetivo:
top_rot += 1
si b!= objetivo:
bottom_rot += 1

si es posible:
mejor = min(mejor, min(top_rot, bottom_rot))

retorno -1 si mejor == INF else best
`` `

■ **Por qué es elegante* *
> > > pares > fondos inferiores – sin indexación manual.
* `float('inf')` es el centinela natural de Python.
* El código es ~10 líneas de largo – ideal para entrevistas rápidas.

-...

## 🥇 C+

``cpp
Incluido el título
#include >
usando std namespace;

Clase Solución {
public:
int minDominoRotations(vector fielint círculo tops, vector implicaint modales) {}
int n = tops.size();
int best = INT_MAX; // sentinel

para (objetivo único = 1; objetivo 0 = 6; ++objetivo) {}
int topRot = 0, inferior Rot = 0;
bool possible = true;

para (int i = 0; i) {}
si (tops[i] != objetivo " bajos " [i]!= objetivo) {
posible = falso;
ruptura;
}
si (tops[i] != objetivo) ++topRot;
si target) ++bottom Rot;
}

si (posible)
mejor = min(best, min(topRot, bottomRot));
}
volver mejor == INT_MAX ? -1 : mejor;
}
};
`` `

■ **C++ Notas específicas**
" Use `INT_MAX ' de `sección de límites ' .
* < > > > > > > > > > > > > > > > > } > > > > > } > > > > > >

-...

### 6 millas] Tiempo & Complejidad Espacial Recaptura

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio Java Silencio O(n) Silencio O(1)
TENIDO Python TENIDO O(n) ANTERIOR O(1) TENIDO
TENIDO C++ TENIDO O(n) TENIDO O(1)

Las tres soluciones comparten las mismas garantías asintoticas.

-...

### 7 carreras El Bien, el Mal

Silencio Silencio
Silencio------------Prince------
Silencio **Readability** Silencio Borrar los bucles " prematuras del código que construye una matriz de frecuencia de 7 tamaños (innecesario) Silencio Soluciones que cuentan rotaciones dos veces para 'tops[i]==bottoms[i] " Silencio
Silencio **Performance** Silencio Single O(n) scan per candidate ← Utilizar un hash‐map del tamaño 7 está bien, pero añade ~O(1) space tención Soluciones que verifican a los 6 candidatos, pero también construyen una tabla de frecuencia de 6 tamaño → trabajo extra trivial
Silencio **Edge‐case handling** Silencio Todos los 6 valores probados, sentinel para “no solución” Silencio Muchas soluciones de Python olvidan saltar candidatos imposibles → `-1` se devuelve incorrectamente Ø Java o C++ que devuelven 0 cuando ambos arrays son idénticos – respuesta incorrecta Silencio

■ **Takeaway** – El escaneo codicioso más simple no sólo es rápido, también es *robust* cuando usted trata los casos de borde correctamente.

-...

### 📚 Pensamientos Finales > Consejos de Entrevista

1. **Explicar la idea del candidato** – a los entrevistadores les encanta ver el razonamiento: “el objetivo debe aparecer en cada domino”.
2. **Hablar sobre la salida temprana** – si un candidato falla en el índice 4, no hay necesidad de terminar la exploración.
3. **Mención del dominio constante** – porque 1–6 es diminuto, podemos permitirnos O(6 · n).
4. **Mostrar el ayudante** – opcionalmente escribir una función separada `testTarget(t, b, target)` para mantener el código modular.
5. **Edge case demonstration** – give the interviewer a quick example (`tops = [1,2]`, `bottom = [2,1]` → respuesta `1`).

-...

Conclusión amigable

Si se está preparando para una entrevista técnica, el problema ** "Minimum Domino Rotations for Equal Row"** es un deber-conocimiento.
- Google searches: * “minimum domino shifts interview”*, *“dominoes make row uniform”*, *“LeetCode 1007 solution”*.
- Empresas: Amazon, Google, Microsoft, Uber, Meta, etc.
- Solución: un escaneo codicioso limpio en tiempo O(n), espacio O(1), con cuidadoso manejo de mitades idénticas.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀