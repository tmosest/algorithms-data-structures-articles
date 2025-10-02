-...
Título: LeetCode 702. Buscar en un Array Clasificado de tamaño desconocido -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Mastering LeetCode 702: Buscar en un Array de tamaño desconocido
### The Good, the Bad, and the Ugly – A Complete Interview‐Ready Guide

■ **Keywords:** *LeetCode 702*, *búsqueda ordenada array unknown size*, *ArrayReader*, *exponential search*, *búsqueda binario*, *pregunta de interés*, * Solución de Java*, *Solución de Pitón*, *Solución de C++*, *entrevista de ingenieros de software*, *entrevista de video

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

■ **LeetCode 702 – Buscar en un rayo de tamaño desconocido* *
■ Se le da un array clasificado `secreto` con elementos únicos y estrictamente crecientes.
■ El tamaño de la matriz es desconocido y no se puede acceder directamente. En lugar de ello, interactúa con la interfaz proporcionada `ArrayReader`:

``text
int get(int index)
`` `

* Si `index` está dentro de los límites, devuelve `secret[index]`.
* Si el índice está fuera de los límites, devuelve `Integer. MAX_VALUE` (o `2^31-1`).

Usted debe escribir `búsqueda (lector de ArrayReader, int target)` que devuelve el índice de `target` o `-1` si no existe, utilizando **O(log n)** tiempo y **O(1)** espacio extra.

-...

#### 2down⃣ El Bien: Un limpio, elegante Dos- Solución de fase

1. **Expand the Search Window (Exponential Search)* *
* Comience con `[left = 0, right = 1]`.
* While `get(right)` no está fuera de los límites ** y** menos que el objetivo, doble `derecha'.
* Esto garantiza que eventualmente corchemos el objetivo entre `izquierda ' y `derecha ' .

2. **Binary Search Inside the Bracket**
* Búsqueda binaria clásica con `mid = izquierda + (derecha-izquierda)/2`.
* Compare `get(mid)` al objetivo; ajuste `left`/`right` en consecuencia.
* Deténgase cuando el valor coincida o la ventana colapse.

Ambas fases juntas se ejecutan en `O(log T)` donde `T` es el índice más pequeño que es el objetivo o el primer índice fuera de límites - exactamente el límite logarítmico requerido.

##### Por qué es genial

* **Simplicity:** Sólo dos bucles, sin recidiva.
* **Deterministic:** No depende del tamaño de la matriz – escala a 104 o más.
* **Memory‐efficient:** Constante espacio adicional.
* *Industry-ready:** Funciona con la verdadera API de LeetCode `ArrayReader` (o cualquier envoltura que se comporta igual).

-...

#### 3down⃣ El mal: Pitfalls comunes para evitar

Silencio Pitfall Silencio Por qué Romper Silencio
Silencio-----------------------------Prince--
Silencio **Accessing out‐of-bounds indices without check** Silencio `reader.get(i)` puede devolver `2^31-1` – tratarlo como un centinela, no como un valor real. tención Siempre prueba `valor == entero.MAX_VALUE` antes de comparar con el objetivo. Silencio
Silencioso **Usando `mientras (get(right) sin un cheque encuadernado** Silencio Podría rebosar `derecha' o llamar `get` en índices negativos. Parar cuando `get(right) == Integer.MAX_VALUE` o cuando la duplicación rebosaría `Integer. MAX_VALUE`. Silencio
Silencio **Binary search `mid = (izquierda + derecha) / 2`** Silencio Puede rebosar para grandes índices. Use `mid = izquierda + (derecha - izquierda) / 2`. Silencio
Silencio **Retorno `derecho' después de bucle** Silencio Si el objetivo no se encuentra, usted podría devolver por error un índice válido. TEN Vuelta `-1` cuando el bucle termina sin un partido. Silencio
Silencio **Ignorando la propiedad "unica, que aumenta estrictamente"** Silencio Algunas soluciones suponen duplicados o datos no variados. No se necesita acción; el algoritmo depende de la monotónica. Silencio

-...

#### 4down⃣ The Ugly: Over‐Engineering & Hidden Tricks

* **Recursive Binary Search** – Añade función-call overhead y riesgo de apilar desbordamiento para rangos muy grandes.
* **Preparar el tamaño de la matriz** – Imposible bajo las limitaciones del problema; intentar hacerlo derrota el propósito.
* **Binary Search on `Integer.MAX_VALUE** – Tratar al centinela como valor regular puede llevar a bucles infinitos si no se maneja cuidadosamente.
* **Usando `Math.min` para `mid`** - Innecesario y más lento que la fórmula segura.

■ **Bottom line:** Mantenlo *simple* y *robust*. Cualquier truco inteligente que complica el código sólo dañará su puntuación de entrevista.

-...

### 5down⃣ Full Code – Java, Python, & C++

■ ** Nota:** Todas las implementaciones utilizan la misma estrategia de dos fases. Los fragmentos de código a continuación están listos para pegar en su caja de presentación IDE o LeetCode.

-...

#### 5.1 Java (LeetCode Submission)

``java
*
* Esta es la interfaz API de ArrayReader.
* No debe implementarlo, ni especular sobre su implementación.
*/
interfaz ArrayReader {}
int get (int index);
}

Clase Solución {
int search (lector de lector de radio, int target) {
// 1 / ⃣ Búsqueda exponencial para encontrar un límite que definitivamente contiene el objetivo
int left = 0, right = 1;
mientras (verdad) {
int val = read.get(right);
si (val == Integer.MAX_VALUE ANTERIVADA EN SUPERVISIÓN val √≥= target) se rompen;
izquierda = derecha;
derecho = 1; // doble la ventana
si (derecho 0) { // guardia de desbordamiento
derecho = entero.MAX_VALUE;
ruptura;
}
}

// 2VIEW⃣ Búsqueda binaria clásica en [izquierda, derecha]
mientras (izquierda)
int mid = left + (right - left) / 2;
int midVal = read.get (mid);

si (midVal == target) regresan a mediados;
si (midVal == Integer.MAX_VALUE TENIDO ANTERIOR EN SUPERVISIÓN DE MEDIO
derecha = media - 1;
. ♫ ... {
izquierda = media + 1;
}
}
retorno -1; // no encontrado
}
}
`` `

-...

#### 5.2 Python

``python
# La interfaz ArrayReader es proporcionada por LeetCode
# class ArrayReader:
# def get(self, index: int) - int: ...

Solución de clase:
def search(self, lector: 'ArrayReader', target: int) - título int:
izquierda, derecha = 0, 1

# Expansión exponencial del límite derecho
Mientras Verdadero:
val = read.get(right)
si vale == 2**31 - 1 o val mento= objetivo:
descanso
izquierda = derecha
derecho = 1 doble la ventana
si la derecha >= 2**31 - 1: Evitar el desbordamiento
derecho = 2**31 - 1
descanso

# Búsqueda binaria en el rango consolidado
mientras que la izquierda:
media = izquierda + (derecha - izquierda) // 2
mid_val = lector.get(mid)

si mid_val == target:
retorno
si mid_val == 2**31 - 1 o mid_val  YO objetivo:
derecho = mitad - 1
más:
izquierda = media + 1

retorno -1
`` `

-...

#### 5.3 C++

``cpp
// Assume ArrayReader se define como sigue:
// clase ArrayReader {}
// public:
// int get(int index);
};

Clase Solución {
public:
int search(ArrayReader &reader, int target) {}
int left = 0, right = 1;

// Búsqueda exponencial para encontrar un límite superior
mientras (verdad) {
int val = read.get(right);
si (val == INT_MAX TENIDO EN VIVO val MENT= target) se rompen;
izquierda = derecha;
derecho = 1; // doble la ventana
si (derecho 0) { // guardia de desbordamiento
derecho = INT_MAX;
ruptura;
}
}

// Búsqueda binaria en [izquierda, derecha]
mientras (izquierda)
int mid = left + (right - left) / 2;
int midVal = read.get (mid);

si (midVal == target) regresan a mediados;
si (midVal == INT_MAX TENIDO TENIDO MEDIO A mediados de Val MENTE) {
derecha = media - 1;
. ♫ ... {
izquierda = media + 1;
}
}

retorno -1; // objetivo no encontrado
}
};
`` `

-...

#### 6VIEW⃣ Complexity Analysis

← Paso Silencioso tiempo Complejidad Silencio
Silencio...
Silencio Búsqueda Exponencial Silencio **O(log k)** (k = índice de objetivo o primer out-of-bounds) Silencio **O(1)** Silencio
Silencioso búsqueda binaria Silencioso **O(log k)** Silencio **O(1)**
Silencio **Total** Silencio**

*El algoritmo cumple con el tiempo de funcionamiento y espacio extra constante requerido. *

-...

### 7 Cambios en la entrevista—Ley Tips

Silencioso Tip Silencioso Explicación
Silencio...
Silencio **Explicar las dos fases por adelantado** Silencio Shows usted entiende por qué no puede sólo la investigación binaria desde el principio. Silencio
**Mención del centinela (`Integer. MAX_VALUE`)** Silencio Clarifies manejo de fuera de límites. Silencio
tención **Discuss edge cases** ← Vacío (no permitido por restricciones), objetivo inferior al primer elemento, objetivo mayor que el último elemento. Silencio
Silencio **Hablar sobre el desbordamiento** Silencio Por qué `mid = izquierda + (derecha - izquierda)/2` es más seguro que `(izquierda + derecha)/2`. Silencio
Silencio **Mostrar el código en su idioma favorito** Silencio Si los entrevistadores prefieren Java, Python o C++, estén listos para escribirlo en vivo. Silencio

-...

#### 8down⃣ Cómo esto es lo que su búsqueda de trabajo

* **LeetCode Mastery:** Problema 702 es un clásico “interview favorite” que muestra su comprensión de búsqueda binaria, búsqueda exponencial y manejo centinela.
* Confianza Algorítmica* El enfoque de dos fases demuestra una manera sistemática de manejar tamaños desconocidos – un patrón que aparece en muchos sistemas del mundo real.
* **Multi‐Language Proficiency:** Proporcionar soluciones Java, Python y C++ demuestra que eres versátil y listo para diversas bases de código.
* **SEO‐Optimized Blog:** Mediante la publicación de un artículo detallado, usted aumenta su visibilidad en los motores de búsqueda – los reclutadores suelen buscar “LeetCode 702 soluciones” o “búsqueda de tamaño desconocido”.
* Portfolio Boost* Agregue el código y el blog a su GitHub y LinkedIn. Tag the repository with `leetcode`, `array-search`, `binary-search`, `algorithm-interview`.

-...

### ## 9walk⃣ Final Takeaway

El problema 702 es solvable con una solución logarítmica ** corta, robusta y provablemente*. Evite la sobreingeniería, tenga en mente el desbordamiento, y trate siempre `Integer. MAX_VALUE` como centinela. Con el código anterior y la estrategia de entrevista esbozada, usted está totalmente equipado para llegar a esta pregunta — y para ser notado por los gerentes de contratación.

¡Feliz codificación, y que sus entrevistas sean tan limpias y eficientes como esta solución! 🚀

-..