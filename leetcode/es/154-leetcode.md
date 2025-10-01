-...
Título: LeetCode 154. Encontrar Mínimo en Rotated Sorted Array II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
1. El Código - Tres idiomas

A continuación se presentan tres soluciones compactas y de producción para **LeetCode 154 – Encontrar Mínimo en Rotated Sorted Array II**.
Los tres usan la misma idea de búsqueda binaria y manejan con gracia la presencia de valores duplicados.

-...

## 1.1 Java

``java
Java 17 */
importar java.util*;

Solución de la clase pública {}
*
* Encuentra el elemento mínimo en una matriz ordenada rotada que puede contener duplicados.
* @param nums array no vacío de enteros, rotado 1..n veces
* @revertir el elemento más pequeño
*/
int findMin(int[] nums) {
int left = 0, right = nums.length - 1;

mientras (izquierda)
int mid = left + (right - left) / 2;

si (nums[mid] {}
// min está en la mitad derecha
izquierda = media + 1;
} si (nums [mid] [derecha] {}
// min está en la mitad izquierda (incluyendo mediados)
derecha = media;
. ♫ ... {
// nums[mid] == nums[right] – no puede decidir, encogerse con seguridad
Bien...
}
}
devolver nums[izquierda];
}
}
`` `

-...

## 1.2 Python

``python
# Python 3
Solución de clase:
def findMin(self, nums: List[int] - int:
"
Devuelve el elemento mínimo en una matriz ordenada rotada con duplicados.
Usa una variante de búsqueda binaria que degrada a tiempo lineal sólo cuando duplicados
que la decisión sea ambigua.
"
izquierda, derecha = 0, len(nums) - 1
mientras que la izquierda
media = (izquierda + derecha) // 2
si nums[mid] ¢ nums[right]:
izquierda = media + 1
elif nums[mid] [derecha]:
derecha = media
# nums[mid] == nums[right]
derecho -= 1
volver nums[izquierda]
`` `

-...

## 1.3 C++

``cpp
// C+17
Clase Solución {
public:
int findMin(vector identificadoint círculo nums) {
int left = 0, right = (int)nums.size() - 1;
mientras (izquierda)
int mid = left + (right - left) / 2;
si (nums[mid] {}
izquierda = media + 1;
} si (nums [mid] [derecha] {}
derecha = media;
} más { // nums[mid] == nums[right]
--derecho;
}
}
devolver nums[izquierda];
}
};
`` `

-...

# 2. Blog Artículo – “El Bien, el Mal, y el Ugly of Finding the Minimum in a Rotated Sorted Array II”

## Title
**El Bien, el Mal, y el Ugly de LeetCode 154 – Encontrar Mínimo en Rotated Sorted Array II* *

## Meta‐Description
Master LeetCode 154 en Java, Python y C++ con una solución binaria clara que maneja duplicados. Aprende las trampas, los cambios de tiempo de ejecución y los consejos de entrevista que impresionarán a los gerentes de contratación.

-...

## 2.1 Introduction

*Si alguna vez has mirado a una matriz ordenada rotada que contiene duplicados, probablemente has sentido una mezcla de frustración y curiosidad. *
LeetCode 154, “Find Minimum in Rotated Sorted Array II”, es un problema clásico de entrevista que prueba:

- Intuición de investigación interna**
- ** Casos de bordes ajustables** (especialmente duplicados)
**Asegurar el tiempo de ejecución* *

A continuación, diseccionamos el problema, caminamos a través de una solución limpia en tres idiomas, y destacamos los aspectos **bueno**, **bad**, y **en términos generales** que los entrevistadores les encanta probar.

-...

## 2.2 Problema de recuperación

■ ** Entrada** – `nums`, una matriz no vacía de enteros, originalmente ordenados en orden ascendente, pero rota entre 1 y `n` veces.
■ **Duplicados permitidos** – por ejemplo, `[2,2,2,0,1]`.
■ ** Objetivo** – Devuelve el elemento más pequeño.

### Constraints
- 1 ≤ ≤ 5000
- `-5000 ≤ nums[i] ≤ 5000`

-...

## 2.3 Naïve Approaches – The “Ugly” Ones

TENCIÓN ANTERIENTE Complejidad ANTERIOR Por qué Es Ugly ANTE
Silencio----------------------------------------
Silencio **Escaneo de línea** – iterate and keep a running minimum Silencio **O(n)** time, **O(1)** espacio Silencio Funciona pero derrota el propósito de "rotated" (sin velocidad logarítmica). Silencio
Silencio ** Búsqueda binaria completa** sin manipular duplicados Silencio **O(log n)** promedio pero **incorrecto** para casos como `[2,2,2,0,1]` TEN Fails porque el pivote no se puede decidir cuando `mid == right`. Silencio
TEN **Ordenar el array** y elegir el primer elemento TEN **O(n log n)** tiempo, **O(n)** espacio TENIDO Sobrekill; destruye el requisito espacial O(1). Silencio

El reto es *mantener lo mejor* (velocidad logarítmica) mientras *tolerando lo peor* (duplica que borre el límite de decisión).

-...

## 2.4 El Optimal Binary‐Search – La parte “buena”

### 2.4.1 Intuición

En un array *rotated* ordenados sin duplicados, el punto de pivote (donde se envuelve el array) se puede encontrar porque el elemento más adecuado es siempre parte de la mitad “alta”.
Si `nums[mid] ¢ nums[right]`, el mínimo está en la mitad **right**; de lo contrario está en la parte **izquierda** (incluido `mid`).

### 2.4.2 Manejo Duplicados – El Twist “Ugly”

Cuando `nums[mid] == nums[right]`, no podemos determinar qué lado tiene el mínimo.
El movimiento más seguro es reducir la ventana de búsqueda por * un elemento*: `derecha--`.
Esto puede degradar el rendimiento a **O(n)** en el peor caso (por ejemplo, un array lleno del mismo valor), pero garantiza la corrección.

### 2.4.3 Step‐by‐Step (Python)

``python
izquierda, derecha = 0, len(nums) - 1
mientras que la izquierda
media = (izquierda + derecha) // 2
si nums[mid] ¢ nums[right]:
izquierda = media + 1 min en la mitad derecha
elif nums[mid] [derecha]:
derecha = mitad # min en la mitad izquierda (medio incluido)
# nums[mid] == nums[right]
derecho -= # ventana encogida con seguridad
volver nums[izquierda]
`` `

La misma lógica se aplica a Java y C++ (ver la sección del código anterior).

### 2.4.4 Análisis de complejidad

Silencioso Escenario Silencioso Tiempo Silencioso
Silencio--------------
Silencio **Mejor / promedio** (muchos duplicados)
Silencio ****** (todos los elementos iguales)

El peor de los casos sólo ocurre cuando el array está muy duplicado; en datos de entrevistas reales esto es raro, por lo que el algoritmo sigue siendo “lo suficientemente rápido”.

-...

## 2.5 Common Pitfalls " Interview‐ Consejos listos

Silencio Pitfall Silencio Reparar la entrevista
Silencio------------------------------
TENIDO Utilizando `mid = (izquierda + derecha) / 2` sin control de desbordamiento TENIDO `mid = izquierda + (derecha - izquierda) / 2` Silencio Mostrar conciencia de la sobrefluencia de entero (importante en Java/C++). Silencio
Silencio Olvidar moverse `derecha' cuando `nums[mid] == nums[derecha] ` Silencio 1` ← Emphasize that this is *necessary* for correctness with duplicates. Silencio
TENIENDO `nums[right]` en lugar de `nums[left]` después de la vuelta Silencio Regresar `nums[left]` Silencio Después de `left == right`, ya sea está bien, pero el uso de `izquierda ` mantiene la lógica consistente. Silencio
Silencio Asumiendo que el array está rotado al menos una vez TENCIÓN Revisar `nums[0] Identificar nums[-1]` para saltar la búsqueda binaria si no rota ANTE Demonstrates edge‐case awareness. Silencio

-...

## 2.6 El "Bad" – Cuando se convierte en ineficiente

Si un entrevistador alimenta un conjunto de datos como `[1,1,1,1,1,0]`, el algoritmo llevará a cabo `n-1` iteraciones porque `derecha--` nunca elimina la ambigüedad.
Si bien sigue siendo correcto, esto revela una limitación de complejidad **tiempo** que debe discutir:

■ *“Los Duplicados pueden hacer que la búsqueda binaria se degrada a tiempo lineal. En la práctica, sin embargo, los casos de prueba de LeetCode son equilibrados, por lo que el algoritmo sigue siendo eficiente.”*

Este es un momento excelente para hacer preguntas claras: *“¿Los datos de la prueba contienen muchos duplicados?”* y para explicar sus compensaciones.

-...

## 2.7 Extensiones " Variaciones

Silencioso Variación Silencio Qué considerar Silencio Sugerido Enfoque
Silencio--------------------
Silencio **LeetCode 33 – Buscar en Rotated Sorted Array** Silencio No hay duplicados, búsqueda de objetivos Silencio Búsqueda binaria clásica con detección de pivotes
Silencio **LeetCode 148 – Lista de clasificación** Silencio Lista enlazada, O(n log n) time ¦ Bottom‐up merge sort (sin memoria adicional) Silencio
tención **Arrays with Negative Numbers** tención La misma lógica se aplica sin cambios; `int` maneja valores negativos Silencio

Estos son buenos temas de seguimiento para una discusión de entrevista más profunda.

-...

## 2.8 Takeaway for the Job‐Seeker

1. **Conoce el truco básico de búsqueda binaria** – detección de pivotes a través de `nums[mid].
2. **Handle duplica con gracia** – `derecha-` es la técnica más simple, correcta y fácil de entrevista.
3. **Explicar cambios de complejidad** – mostrar conciencia de que el peor de los casos es lineal pero el promedio es logarítmico.
4. **Proporciona código limpio, comentado** – como hicimos en Java, Python y C++.
5. **Hablar sobre los casos de borde** – tales como arrays ya ordenados o arrays con todos los elementos iguales.

Si usted puede articular estos puntos durante una entrevista, impresionará a cualquier gerente de contratación con su pensamiento algoritmo y sus habilidades de comunicación.

-...

## 2.9 Final Code Snippets (All Three Languages)

``java
// Java
int findMin(int[] nums) {
int left = 0, right = nums.length - 1;
mientras (izquierda)
int mid = left + (right - left) / 2;
si (nums[mid] > nums[right]) izquierda = medio + 1;
si no (nums[mid] [derecha]) derecha = medio;
si no...
}
devolver nums[izquierda];
}
`` `

``python
# Python
def findMin(self, nums: List[int] - int:
izquierda, derecha = 0, len(nums) - 1
mientras que la izquierda
media = (izquierda + derecha) // 2
si nums[mid] ¢ nums[right]:
izquierda = media + 1
elif nums[mid] [derecha]:
derecha = media
más:
derecho -= 1
volver nums[izquierda]
`` `

``cpp
// C++
int findMin(vector identificadoint círculo nums) {
int left = 0, right = nums.size() - 1;
mientras (izquierda)
int mid = left + (right - left) / 2;
si (nums[mid] > nums[right]) izquierda = medio + 1;
si no (nums[mid] [derecha]) derecha = medio;
-derecho;
}
devolver nums[izquierda];
}
`` `

-...

## 2.10 Pensamientos de clausura

LeetCode 154 es más que un rompecabezas; es una prueba **comunicación**.
Domine la lógica de búsqueda binaria, mantenga su código legible, y esté listo para discutir cómo los duplicados afectan el tiempo de ejecución.

Esa es la mezcla perfecta del **bueno, el malo, y el feo** que cualquier papel de ingeniería de software de alto nivel espera.

-...

*Feliz codificación, y buena suerte con tus entrevistas! *