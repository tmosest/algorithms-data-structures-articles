-...
Título: LeetCode 658. Encontrar K Elementos más cercanos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

## 658. Encontrar K Elementos más cercanos – De la Teoría a la Producción-Ley Código

**Keywords:** LeetCode 658, Encuentra K Closest Elementos, algoritmo de dos puntos, búsqueda binaria, cola de prioridad, Java, Python, C++, entrevista de algoritmos, solución O(n), preparación de entrevistas, entrevista de codificación

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

■ **Given** a *sorted* integer array `arr`, and two integers `k` and `x`,
■ **Retorno** los enteros " k " en `arr ' que están más cerca de `x ' .
■
■ La lista devuelta también debe ser clasificada en orden ascendente.
■
■ Si dos números están igualmente cerca de 'x', el número más pequeño gana.

TEN SON SON SON SON SON SON 
Silencio------------
TENIDO 1 TENIDO `arr = [1,2,3,4,5]`, `k = 4`, `x = 3 ` TENIDO `[1,2,3,4] ` Silencio
TENIDO 2 TENIENDO `arr = [1,2,3,4,5]`, `k = 4`, `x = -1` TENIDO `[1,1,2,3] ` Silencio

**Constraints* *

`` `
1 ≤ k ≤ arr.length ≤ 104
arr se clasifica en orden ascendente
-104 ≤ arr[i], x ≤ 104
`` `

-...

## ## 2down⃣ Algoritmic Choices – The Good, The Bad, The Ugly

Silencio Silencio Silencio Silencio Silencio Silencio
Silencio--------------...
Silencio **Two‐pointer escaparate** TEN O(n) time, O(1) extra space – simple de entender y código TENENCIA Necesita un manejo cuidadoso de la lógica de ruptura de corbatas (abs‐diferencences) ANTERI Utilizado raramente en entrevistas; puede ser pasado por alto en comparación con los trucos de búsqueda binaria TENIDO
TEN **Binary‐search with sliding window** TEN O(log n) time, O(1) space – optimiza for large arrays TENED Más complejo para implementar correctamente; off-by-one bugs common TEN Algunos entrevistadores aman este “trick” pero pueden ser exigentes acerca de la fórmula de comparación ANTE
Silencio **Priority queue (max‐heap of size k)** Silencio Fácil de razonar acerca de “mantener el k mejor hasta ahora” Silencio O(n log k) tiempo, espacio O(k) – más lento en grandes entradas Silencio Las operaciones de Heap pueden convertirse en un cuello de botella; no el más óptimo para los arrays ordenados ←
Silencio **Brute force + sort** ← Conceptualmente simple Silencio O(n log n) time, not acceptable for 104 size Silencio demasiado lento para las típicas limitaciones de entrevista

■ **Bottom line:** Para una matriz ordenada, la ventana corredera de dos puntos es el *sweet spot* – tiempo lineal, espacio constante, y naturalmente respeta el requisito de pedido.

-...

#### 3down⃣ Ventana deslizante de dos puntos – el código “bueno”

##### 3.1 Concepto

Mantenemos dos índices, "izquierda" y "derecha", que delimitan una ventana de candidatos.
Mientras que el tamaño de la ventana es mayor que `k ' , dejamos caer el extremo * lejano* de la ventana:

`` `
si vulnerarr[izquierda] - x lecciones нели наные [derecha] - x sufrimiento → left++ // el extremo izquierdo está más lejos
más → derecha - // el extremo derecho es más lejos o igual
`` `

Cuando `derecha - izquierda + 1 == k`, la ventana contiene exactamente la respuesta.

###### 3.2 Complexity

- **Tiempo:** O(n) – cada elemento es examinado al máximo una vez.
- **Espacio:** O(1) - sólo dos índices y una lista de resultados.

-...

## 📌 Java Implementation

``java
importar java.util*;

Solución de la clase pública {}
*
* Encuentra los enteros k en una matriz ordenada que están más cerca de x.
*
* @param arr el array ordenados
* @param k número de elementos para regresar
* @param x valor de destino
* @return una lista que contiene los k elementos más cercanos en orden ascendente
*/
public List won(int[] arr, int k, int x) {
int left = 0;
int right = arr.length - 1;

// Arranque la ventana hasta que sólo los elementos k permanezcan
mientras que (derecha - izquierda + 1  título) {}
si (Math.abs(arr[left] - x)
izquierda++; // izquierda es más lejos – soltarlo
. ♫ ... {
derecha--; // derecha es más lejos (o la corbata con izquierda más pequeña)
}
}

// Copiar la ventana en una lista
Lista de resultadosInteger título = nuevo ArrayList correctamente(k);
para (int i = izquierda; i) = derecha; i++) {}
result.add(arr[i]);
}
Resultado de retorno;
}
}
`` `

■ **¿Por qué la comparación de 'Math.abs'? * *
■ La regla de ruptura de corbatas del problema ( " perpetuaa-x sometida == TENB-x intimidad " → " a " b " ) ya está satisfecha por mantener el índice *smaller* a la izquierda.
■ Si las distancias son iguales, la rama 'else' mantiene el lado izquierdo (el menor número), exactamente igualando el requisito.

-...

## 🐍 Python Implementation

``python
de la importación Lista

Solución de clase:
def findClosestElements(self, arr: List[int], k: int, x: int) - título List[int]:
izquierda, derecha = 0, len(arr) - 1

mientras que a la derecha - izquierda + 1 ≤ k:
si abs(arr[left] - x) √≥ abs(arr[right] - x):
izquierda += 1
más:
derecho -= 1

retorno arr[izquierda:right+1]
`` `

■ La versión de Python es casi idéntica – la rebanada `arr[left:right+1]` da la sub-lista ordenada directamente.

-...

## 🧩 C++ Implementation

``cpp
Incluido el título
#include >

Clase Solución {
public:
std:::vector seleccionadoint confianza findClosestElements(std::vector fieltro arr, int k, int x) {
int left = 0;
int right = arr.size() - 1;

mientras que (derecha - izquierda + 1  título) {}
si (std::abs(arr[left] - x) ¢ std::abs(arr[right] - x))
++izquierda; // gota izquierda
más
--derecho; //derecho
}

retorno std::vector seleccionado(arr.begin() + izquierda, arr.begin() + derecha + 1);
}
};
`` `

■ Utilizando `std:::vector `'s iterator constructor hace el resultado copiando conciso.

-...

## 4down Por qué esta solución gana en entrevistas

1. **Lógica clara y concisa** – No hay bucles nidos ni estructuras de datos complejas.
2. **Tiempo óptimo** – O(n) supera el O(n log n) clasificando la base de referencia.
3. **Espacio-amigable** – Constante memoria extra; se ajusta a las expectativas de la entrevista “solución óptima”.
4. ** Huellas desgarradoras implícitamente** – No hay cheques adicionales `si (a < b)`, sólo el orden natural de la matriz.

■ Los entrevistadores aman una solución que * hace* algo interesante *y* se mantiene simple. El método de dos puntos marca las dos cajas.

-...

## 5down SE SEO‐Optimized Blog Meta

- **Título:** LeetCode 658 – “Encontrar elementos más cercanos” Algoritmo explicado (Java/Python/C++)
- **Meta Descripción:** Master LeetCode 658 con una rápida solución de dos puntos O(n) en Java, Python y C++. Aprende lo bueno, malo y feo de enfoques algorítmicos.
- **Keywords:** LeetCode 658, Encontrar K Closest Elements, algoritmo de dos puntos, búsqueda binaria, preparación de entrevistas, entrevista de codificación, Java, Python, C++, explicación de algoritmo, solución O(n).

-...

Pensamientos finales – El lado “Ugly”

Aunque el enfoque de dos puntos es perfecto para la entrada ordenada, ** no generalizar** a los arrays sin surtido.
Si la entrada no fuera surtido, necesitará un máximo de tamaño `k` (primera cola de prioridad), que introduce `O(n log k)` tiempo.
Por lo tanto, siempre confirma que la matriz está ordenada antes de elegir el truco de ventana deslizante.

-...

#### 🚀 Takeaway

Para * arrays surtidos*, **la ventana corredera de dos puntos** es tu algoritmo de ir a LeetCode 658.
Cumple las limitaciones, respeta la regla de ruptura de corbatas, y tiene una clara prueba de corrección de entrevista.

Buena suerte en su próxima entrevista – ahora usted puede alejarse con un *clean* implementación y un blog que será descubierto por otros entrevistados en busca de “LeetCode 658 soluciones”.