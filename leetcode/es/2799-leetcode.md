-...
Título: LeetCode 2799. Cuenta completa Subarrays in an Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1. Resumen del problema – LeetCode 2799 “Count Complete Subarrays”

** Objetivo** – Contar cuántos sub-arrayos contiguos de una matriz entero contienen *exactamente* el mismo número de elementos distintos como toda la matriz.

Silencio # Silencio Ejemplo Silencio `nums` Silencio `distinct(nums)` tención completas sub-arrays
La vida... la vida... la vida... la vida... la vida... la muerte...
[1,3,1,2,2]
Silencio 2 Silencioso `[5,5,5,5]` Silencio `1` Silencio **10** (todas las sub-array)

**Constraints* *

* `1 ≤ nums.length ≤ 1000`
* `1 ≤ nums[i] ≤ 2000`

El reto es resolverlo más rápido que la ingenua `O(n2)` fuerza bruta, que estaría bien para `n=1000`, pero todavía se siente como una entrevista “Bandera roja”.

-...

## 2. El “bien, el mal y el ugly” de las soluciones comunes

Silencio Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio Brute‐force (`O(n2)`) ← Simple de escribir, fácil de entender TENIDO Tiempo cuadrático – no ideal para más grande `n` habit Ninguno (no necesario)
ventana deslizante con mapa de hash (`O(n)`) TEN Tiempo lineal, mínimo espacio extra TEN Requiere cuidadoso manejo del tamaño de la ventana TENN Ninguno – limpio si codificado correctamente TEN
Silencio Dos puntos con frecuencia de matriz (`O(n)`) Silencio No hash maps – actualizaciones constantes de tiempo Silencio Necesitas valor máximo predeterminado (2000) TEN Harder para adaptarse para mayores rangos TEN

■ **Conclusión** El enfoque *sliding ventana* es el lugar dulce – tiempo lineal, lógica simple y sencillo para explicar en una entrevista.

-...

## 3. Sliding‐Window Insight (Pseudo‐Code)

1. **Computar `k`** – el número de elementos distintos en toda la matriz.
k = tamaño(set(nums)) '
2. **Traverse con dos punteros** `izquierda ' y `derecha ' .
Mantenga un mapa de frecuencia 'cnt' para la ventana actual.
3. Siempre que la ventana contiene **exactamente `k` valores distintos**:
* Cada sub-array que comienza entre la izquierda y la derecha actual (inclusiva) y termina en la derecha es *completa*.
* Cuenta con ellos: `respuesta += derecha - izquierda + 1.
* Arranque la ventana desde la izquierda para encontrar el siguiente comienzo posible.
4. Continúe hasta que la derecha llegue al final.

Esto da un **`O(n)`** algoritmo de tiempo y `O(k)` espacio.

-...

## 4. Código completo – Tres idiomas

A continuación se presentan implementaciones de producción, concisas en **Java, Python, y C++**.
Los tres resuelven el problema en tiempo lineal.

La versión C++ utiliza un 'vector fielint' de tamaño `2001` para actualizaciones de frecuencias O(1), evitando la sobrecarga sin orden_map.

### 4.1 Java (estilo LeetCode)

``java
importar java.util*;

Clase Solución {
int countCompleteSubarrays(int[] nums) {
// 1. conteo distinto de toda la matriz
Establecer:Integer confiar all = nuevo HashSet correctamente();
para (int x : nums) all.add(x);
int k = all.size();

// 2. ventana corredera
int[] freq = nuevo int[2001]; // 1 י= nums[i]
int distinct = 0, left = 0, ans = 0;

para (derecho = 0; derecho) {}
si (freq[nums[right]+ == 0) distinto++;

// reducir hasta que la ventana tiene exactamente k valores distintos
mientras (distinto == k) {
ans += nums.length - right; // all subarrays terminando en 'right '
si (--freq[nums[left]] == 0) distinto...
izquierda++;
}
}
devolver los ans;
}
}
`` `

■ **¿Por qué `ans += nums.length - right`?**
■ Una vez la ventana `[izquierda ... derecha]` tiene exactamente `k` elementos distintos, extendiéndolo a la derecha preserva la propiedad.
■ All sub-arrays `[i ... right]` where `i` ranges from `left` to `right` are complete.
■ El número de esas sub-arrayas equivale a `derecha - izquierda + 1`.
■ El bucle de arriba hace lo mismo al revés: para cada `derecha', contamos el número de * posiciones de inicio* que producen un sub-array completo que termina en `derecha'.
■ Añadiendo `nums.length - right` cuenta todos los sub-arrays que terminan ** después de** `derecha' también (el algoritmo invariante asegura la corrección).

-...

### 4.2 Python 3

``python
de las colecciones importadas por defecto

Solución de clase:
def countCompleteSubarrays(self, nums: list[int] int:
k = len(set(nums)) # distintos elementos en toda la matriz
freq = defaultdict(int)
diferenciada = 0
izquierda = 0
ans = 0

por derecho, val in enumerate(nums):
si freq[val] == 0:
diferenciado += 1
freq[val] += 1

mientras que distinto == k:
# todos los subarrays terminando en 'derecha' que comienzan desde 'izquierda' o más tarde
ans += len(nums) - right
freq[nums[left]] -= 1
si freq[nums[left] == 0:
-= 1
izquierda += 1
Retorno
`` `

■ **Pythonic touchs**:
* ' defaultdict(int)`* reemplaza la inicialización manual del mapa.
* `len(nums) - right`* es la misma idea que la versión Java.

-...

#### 4.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int countCompleteSubarrays(vector efectuadoint frecuentemente limitado) {
// 1. conteo distinto de toda la matriz
unordered_set obtenidostodos(nums.begin(), nums.end());
int k = all.size();

// 2. ventana corredera
vector asignadoint confianza freq(2001, 0); // 1 י= nums[i] י= 2000
int distinct = 0, left = 0, ans = 0;

para (derecho = 0; derecho)
si (freq[nums[right]+ == 0) distinto++;

mientras (distinto == k) {
ans += (int)nums.size() - right; // subarrays completos que terminan en 'right '
si (--freq[nums[left]] == 0) distinto...
++izquierda;
}
}
devolver los ans;
}
};
`` `

■ **¿Por qué no `unordered_map`?* *
> `vector seleccionadoint título` da una actualización de frecuencia constante y mantiene el uso de la memoria predecible – perfecto para los límites de entrada de LeetCode.

-...

## 5. Recaptación de la complejidad

Silencio Idioma Silencio Tiempo Silencioso
Silencio...
Silencio Java Silencioso `O(n)` Silencio `O(k)` (frequency array)
Silencio Python Silencio `O(n)` Silencio `O(k)` (dict)
TENIDO C++ TENIDO `O(n)` Silencio `O(k)` (array of size 2001) TENIDO

Tanto las complejidades algorítmicas *time* como *space* están bien dentro de las limitaciones y se pueden lanzar con confianza en una entrevista.

-...

## 6. SEO‐Optimized Blog Artículo

■ **Palabras clave:**
*LeetCode 2799* Silencio* *Count Complete Subarrays* *Sliding Window* *Sliding Window* *Java / Python / C+ Solución* *Entrevista de instrucciones de datos* *Pregunta de interés explicada*

-...

### 6.1 Title & Meta‐Description

`` `
LeetCode 2799 – Contar Subarrays completos ← Sliding‐Window, Java/Python/C+ Soluciones
`` `

■ *Meta‐Description (160 chars)*:
“Solve LeetCode 2799 (Count Complete Subarrays) en tiempo lineal. Aprende una técnica de ventanilla deslizante limpia con códigos Java, Python y C++ que es perfecta para tu próxima entrevista de codificación. ”

-...

### 6.2 The Post

■ **H1**: Mastering LeetCode 2799: Count Complete Subarrays
■ **H2**: ¿Por qué este problema es una gema de entrevista oculta
■ **H3**: Estrategia Sliding-Window (en inglés)
■ **H3**: Java, Python & C++ implementaciones (listos para pegar en LeetCode)
■ **H3**: Análisis de la complejidad Consideraciones de casos
■ **H3**: Entrevista común Pitfalls y cómo evitarlos
■ **H3**: Consejos de práctica y lectura posterior

■ **Introducción (con unas 200 palabras)**
■
" texto
■ “Count Complete Subarrays” es una pregunta engañosamente sencilla que prueba su capacidad de combinar dos conceptos clásicos: el recuento de elementos distintos y el patrón de ventana deslizante. Es problema LeetCode 2799, pero también es una entrevista perfecta para cualquier desarrollador de backend, especialista en datos o ingeniero del sistema. En este post te acompaño a través del problema, te doy una solución lineal limpia, te mostraré el código en tres idiomas populares, y te explicaré por qué el método de ventanilla deslizante golpea la solución cuadrática ingenua.
" `

-...

### 6.3 El Post (texto completo)

``markdown
# Mastering LeetCode 2799: Count Complete Subarrays

■ **Keywords:** LeetCode 2799, Conde Complete Subarrays, ventana deslizante, codificación de entrevistas, solución Java, solución Python, solución C++

## Por qué este problema importa
En la mayoría de las entrevistas de codificación, los entrevistadores buscan dos cosas:

1. ** Corrección** – ¿Su algoritmo siempre devuelve la respuesta correcta?
2. **Elegancia** - ¿El código es corto, legible y explicable?

“Count Complete Subarrays” marca alto en ambos conteos cuando se resuelve con una ventana deslizante.
Te obliga a razonar sobre **cuántas sub-arrays comienzan en cada índice**—exactamente el tipo de *contando* entrevistadores de trucos amor.

-...

## 1. Recaptación de problemas

Dado un array entero `nums`, cuenta cuántos sub-arrays contiguos contienen **exactamente** el mismo número de enteros distintos como todo el array.

■ *Ejemplo:*
> `nums = [1,3,1,2,2]` → 3 números distintos → 4 sub-arrays completos.

-...

## 2. El Bien, el Mal, el Ugly

TENIDO TERRITORIO PROS TENIDO CONSAS ANTERIOR Cuando se utiliza
Silencio--------------------------
Silencio Brute‐force (`O(n2)`) Silencio TENIDO Easy to code ❌ Quadratic, can fail on 105 size arrays ← Rarely used in interviews; only for small constraints Silencio
TENIDO Sliding window (`O(n)`) TENIDO LÍNEA linear, clear logic ❌ Debe entender window‐shrink invariants Silencio **Mejor** para entrevistar & producción
Silencio Dos puntos con matriz de frecuencias TENIDO Sin mapas de hash TENIDO ❌ Necesidades valor fijo consolidado Silencio Uso cuando `max(nums[i])` es pequeño (como 2000)

■ **Bottom line:** El truco de la ventana deslizante es la solución de ir a la que siempre debe mostrar en una entrevista.

-...

## 3. Sliding‐Window Intuition

1. Compute `k` = número de elementos distintos en toda la matriz.
2. Camine por la matriz con dos punteros (“izquierda”, “derecha”.
3. Mantener un mapa de frecuencia " cnt " para la ventana `[izquierda ... derecha] " .
4. Cuando la ventana tiene exactamente `k` elementos distintos:
* Cada sub-array que comienza entre `izquierda ' y `derecha ' (inclusiva) y termina en `derecha ' es “completo”.
* Cuenta con ellos: `respuesta += derecha - izquierda + 1.
* Diapositiva `izquierda ' a la derecha hasta que la ventana contenga menos de `k ' elementos distintos, entonces continúe.

Esta lógica funciona en el tiempo `O(n)` y utiliza sólo `O(k)` memoria extra.

-...

## 4. Código en tres idiomas

### 4.1 Java (LeetCode listo)

``java
Clase Solución {
int countCompleteSubarrays(int[] nums) {
Establecer:Integer confiar all = nuevo HashSet correctamente();
para (int x : nums) all.add(x);
int k = all.size();

int[] freq = nuevo int[2001]; // 1 י= nums[i]
int distinct = 0, left = 0, ans = 0;

para (derecho = 0; derecho) {}
si (freq[nums[right]+ == 0) distinto++;

mientras (distinto == k) {
ans += nums.length - right; // all sub-arrays terminando en 'derecha' y más allá
si (--freq[nums[left]] == 0) distinto...
izquierda++;
}
}
devolver los ans;
}
}
`` `

### 4.2 Python 3

``python
de las colecciones importadas por defecto

Solución de clase:
def countCompleteSubarrays(self, nums: list[int] int:
k = len(set(nums))
freq = defaultdict(int)
diferenciada = 0
izquierda = 0
ans = 0

por derecho, v in enumerate(nums):
si freq[v] == 0: diferencia += 1
freq[v] += 1

mientras que distinto == k:
ans += len(nums) - right
freq[nums[left]] -= 1
si freq[nums[left] == 0: distinct -= 1
izquierda += 1
Retorno
`` `

#### 4.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int countCompleteSubarrays(vector efectuadoint frecuentemente limitado) {
unordered_set obtenidostodos(nums.begin(), nums.end());
int k = all.size();

vector asignadoint confianza freq(2001, 0);
int distinct = 0, left = 0, ans = 0;

para (derecho = 0; derecho)
si (freq[nums[right]+ == 0) distinto++;

mientras (distinto == k) {
ans += (int)nums.size() - right;
si (--freq[nums[left]] == 0) distinto...
++izquierda;
}
}
devolver los ans;
}
};
`` `

Los tres compilan bajo el ambiente de LeetCode y se ejecutan en **`O(n)`** tiempo.

-...

## 7. Cómo explicar Esto en una entrevista

1. **Declarar el problema en una frase. #
*“Los submarinos que tienen el mismo número de elementos distintos en toda la matriz.”*
2. **Mostrar el paso previo a la comunicación. #
k = len(set(nums))
3. ** Dibuja un diagrama rápido** de la ventana corredera:
`` `
nums: 1 3 1 2 2
idx: 0 2 3 4
izquierda → derecha
`` `
4. **Explicar el invariante** – “Cuando la ventana tiene exactamente ‘k’ números distintos, extendiéndolo a la derecha mantiene la propiedad. ”
Así podemos contar todas las sub-arrayas que terminan en "derecha" en un solo disparo.
5. ** Casos del borde de la mención** – por ejemplo, cuando `k == 1 ` cada sub-array es válido; el algoritmo todavía funciona porque la ventana siempre alcanzará `k` en el primer elemento.

-...

## 8. Pensamientos finales > Entrevista Take‐away

* **Por qué la ventana deslizante es entrevista-finalmente* *
* Es un patrón clásico; a los entrevistadores les encanta ver que lo observan.
* Te muestra entender **tiempo–intercambios espaciales**.
* Puedes explicar la intuición rápidamente (bajo 2 min).

* **Common Mistake** – Olvidando reducir la ventana correctamente.
* Fijación: Mantenga un contador de elementos distintos y deslice `izquierda ' hasta que el conteo caiga por debajo de `k ' .

* **Practice Idea** – “Count Complete Subarrays” puede ser un gran calentamiento para problemas como *“Count sub-arrays con exactamente K distintos enteros”* (LeetCode 992) y *“Subarray product less than K”* (LeetCode 713).

-...

### Sugerido Próximos pasos

1. **Descargar el código en los casos de prueba de LeetCode** – copiar el chip Java, Python o C++.
2. **Agregar más casos de prueba** en su propio IDE:
* `[1,1,1]` → `6` (todas las sub-arrayas).
* `[1,2,3,4]` → `1` (sólo toda la matriz).
3. **Explorar variaciones** – por ejemplo, “en la mayoría de K distintos” vs. “exactamente K distintos”.
4. **Agregue la solución a su GitHub repo** y enlacela en su perfil de LinkedIn como un “Coding Interview Readme”.

■ **Listo para la próxima entrevista de codificación? * *
■ Practica este problema y el patrón de ventanilla deslizante y podrás impresionar tanto a los gerentes de contratación como a los sistemas automatizados de clasificación.

-...

¡Feliz codificación!
`` `

-...

■ ** Call‐to‐action (bottom of post): #
■ “Déle a LeetCode 2799 la solución de la ventanilla deslizante, agréguela a su cartera y utilícela como un calentamiento para cualquier próxima entrevista. ¡Feliz solución!
`` `

-...

### 9. Observaciones finales

Este artículo ofrece una solución **completa, lista para copiar** para LeetCode 2799 y le muestra cómo hablar de ello como un ingeniero experimentado.
Con los fragmentos de código y el explicador de entrevistas en su arsenal, se establecerá para su próxima entrevista de codificación, e impresionará a los reclutadores que están cazando soluciones concisas y eficientes.

-...

## 10. Recursos adicionales

* Problema de LeetCode 2799 – `https://leetcode.com/problems/count-complete-subarrays/`
* Patrón de ventanilla deslizante: https://leetcode.com/tag/sliding-window/`
* Contando distintos elementos: https://leetcode.com/tag/hashtable/`
* Cuestiones de entrevista conexas: https://leetcode.com/tag/subarray/`
* Medium article on sliding window – `https://medium.com/@michael_zhang/` (example)

-...

### 11. Fin de Blog Post

-...

■ **Cuento de palabras:** ~750 palabras (se ajusta a un blog de entrevista de 700–900 palabras).
■ **Siguiente paso:** Publish on a personal blog or Medium with the meta tags above and link it from your GitHub README.

-...

## 12. ¿Listo para tu próxima entrevista?

Mantenga el truco de la ventana deslizante en su bolsillo.
Suelte el código en Java, Python o editor C++ de LeetCode, ejecútelo y prepárate para explicarlo en menos de dos minutos.
Acabas de enfrentar a LeetCode 2799, ¡bien hecho!

`` `

-...

### 6.4 Artículo final del Blog

-...

■ **Wrap‐up** – El artículo es conciso, utiliza las palabras clave apuntadas, y presenta la solución en un formato que es instantáneamente utilizable por los desarrolladores que se preparan para las entrevistas de codificación.

-...

## 9. Lista de verificación de publicación

1. **Añada un `Readme.md`** en su GitHub repo con los tres fragmentos de código y una breve explicación.
2. **Pon el artículo en Medium** con las etiquetas anteriores.
3. **Compartir el artículo en Twitter**:
`` `
Simplemente resuelto LeetCode 2799 (Count Complete Subarrays) en O(n) usando una ventana corredera! Echa un vistazo a códigos Java/Python/C++ y cómo explicarlo en entrevistas. #codinginterview #leetcode
`` `

4. **Agregue el problema a su lista de preparación de entrevistas** – practicar variaciones y probar con arrays aleatorios.

-...

#### 10. Palabras finales

Ahora tienes:

* **Un entendimiento completo** de *Count Complete Subarrays* y por qué la ventana deslizante es el patrón óptimo.
* ** Soluciones de lectura a paso** en Java, Python y C++.
* **Una explicación de entrevista pulida** que es concisa y demuestra el pensamiento algorítmico.

Armado con esto, usted puede abordar con confianza LeetCode 2799 e impresionar a los entrevistadores que valoran tanto la corrección como la elegancia. ¡Feliz codificación!

`` `

-...

### 6.5 Fin del puesto

■ Este post del blog se puede copiar en un archivo Markdown, publicado en Medium o su sitio personal, y se clasificará bien para las palabras clave específicas mientras que proporciona valor inmediato a los desarrolladores que se preparan para las entrevistas de codificación.

-...


**END OF POST** (Markdown)

-...

#### 6.6 Conclusiones

* El artículo está bajo palabras de 1 k, utiliza las palabras clave apuntadas, y camina un lector de declaración de problema a código.
* Los snippets Java, Python y C++ están listos para LeetCode e ilustran el truco de la ventana deslizante.
* Explicar la solución en una entrevista es directa y muestra intuición algorítmica.

-...

■ **Feliz codificación, y buena suerte con su próxima entrevista! * *

-...

**Post Complete.**