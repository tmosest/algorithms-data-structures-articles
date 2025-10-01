-...
Título: LeetCode 3523. Hacer que Array no disminuye -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Código de Solución

A continuación se presentan tres soluciones completas, listas para enviar – una en **Java**, una en **Python**, y otra en **C+** – que resuelven LeetCode 3523 *Hacer Array No disminuir*.

▪ restablecimiento *El enfoque “simplemente ambicioso” es correcto para este problema.
■ Mantiene cada elemento que no es más pequeño que el elemento guardado anterior e ignora el resto.
■ La matriz resultante es la matriz no decreciente más larga posible que puede obtenerse fusionando sub-arrays en sus valores máximos. *

-...

## Java

``java
- 3523. Hacer Array No-disminuir
// Duración: O(n), Memoria: O(1)

Clase Solución {
public int maximumPossibleSize(int[] nums) {
int size = 0;
int prev = Integer.MIN_VALUE; // cualquier valor menor que el elemento más pequeño

para (int num : nums) {
si (num >= prev) { // mantener este elemento
prev = num;
tamaño++;
}
}
tamaño de retorno;
}
}
`` `

-...

## Python

``python
# 3523. Hacer Array No-disminuir
# Runtime: O(n), Memory: O(1)

Solución de clase:
def maximumPossibleSize(self, nums: List[int]) int:
tamaño = 0
prev = flotante('-inf') # cualquier valor menor que el elemento más pequeño

para las numidades:
si num >= prev: # mantener este elemento
prev = num
tamaño += 1

tamaño de retorno
`` `

-...

### C++

``cpp
- 3523. Hacer Array No-disminuir
// Duración: O(n), Memoria: O(1)

Clase Solución {
public:
int maximumPossibleSize(vector seleccionadoint limitada nums) {
int size = 0;
int prev = INT_MIN; // cualquier valor menor que el elemento más pequeño

para (int num : nums) {
si (num >= prev) { // mantener este elemento
prev = num;
++tamaño;
}
}
tamaño de retorno;
}
};
`` `

-...

## 2down⃣ Blog Article – “Make Array Non-decreasing: The Good, The Bad, and The Ugly”

■ **Keywords**: *Make Array Non-decreasing, LeetCode 3523, entrevista desafío de codificación, algoritmo codicioso, subsequencia no disminuyente más larga, solución Java, solución Python, solución C+++, entrevista de datos, entrevista de algoritmos, consejos de entrevista de codificación, entrevista de ingeniería de software, publicación de trabajo SEO, preparación de entrevista técnica. *

-...

#### Introduction

LeetCode 3523 – *Make Array Non-decreasing* – es un problema engañosamente simple pero perspicaz que a menudo se acumula en entrevistas de ingeniería de software. Le pide realizar operaciones **cero o más** en un array, donde cada operación colapsa un sub-array en un solo elemento igual a su valor máximo. Después de todas las operaciones, la matriz resultante debe ser **no disminuir**. Su objetivo: **maximizar el tamaño del array final**.

¿Por qué importa esto?
En el código del mundo real, a menudo se le pide que transforme los datos con mínima pérdida de información. Este problema te obliga a pensar en *cuán lejos puedes mantener elementos intactos* mientras sigues respetando las restricciones del orden. Es una ilustración clásica de una estrategia codictiva: mantener todo lo que puedas y descartar el resto.

-...

#### 1down⃣ El Bien - ¿Por qué funciona la Solución Greedy

###### 1.1 Intuición

Imagínese caminar a través de la matriz de izquierda a derecha.
- **Si el elemento actual es al menos tan grande como el último elemento que decidió mantener**, usted puede mantenerlo con seguridad – no romperá la propiedad no-disminución.
- **Si es más pequeño**, usted * debe combinarlo en el elemento anterior (perdiendo su propia contribución) o dejarlo completamente. Merging no puede ayudarle más tarde porque cualquier fusión con un elemento más pequeño sólo reemplaza el sub-array con el máximo mayor; el elemento más pequeño nunca será útil.

Por lo tanto, un **single pass** que mantiene los elementos “buenos” es suficiente.

##### 1.2 Argumento formal

Sea `prev` el valor del último elemento guardado.
- Cuando `num не= prev`, el array `prev, num` ya no está disminuyendo.
- Cuando " año " , cualquier sub-array que termine en `num ' que incluya `prev ' tendrá el máximo `prev ' (ya que `prev ' es mayor). Replacing that sub-array with `prev` keep the array non-decreasing but reduces size by at least one.
Por lo tanto, *cualquier* solución óptima mantendrá a todos los elementos satisfechos `num ±= prev`, y soltar el resto.

##### 1.3 Time & Space Complexity

Silencio Idioma Silencio Tiempo Complejidad Silencio
Silencio...
Silencio en Java **O(n)** Silencio **O(1)**
TENIDO Python TENIDO **O(n)** ANTERIOR **O(1)**
Silencio C++ Silencio **O(n)** Silencio **O(1)**

`n` es la longitud de la matriz (hasta 200 000). Un pase lineal es el más rápido posible.

-...

#### 2down⃣ Los malos – saltos comunes

¿Por qué está mal?
Silencio...
Silencio **Tratarlo como una subsequencia de mayor crecimiento (LIS)** Silencio LIS considera cualquier subsequencia; aquí usted no puede reordenar elementos, sólo fusionarse. Use la regla codicioso “guarde si ≥ prev” en lugar de O(n log n) LIS. Silencio
Silencio **Usando una pila o deque para simular fusiones** ← Sobre-ingeniería; el efecto de la operación es trivial (sustitución con máx.). tención Un pase basta; no es necesario tener estructuras de datos adicionales. Silencio
Silencio **Asumiendo que puedes mantener a todos los pares que no disminuyen** Silencio Podrías saltarte un elemento posterior que podría ser guardado si te hubieras fusionado con los anteriores. El algoritmo codicioso maneja automáticamente esto: si un elemento posterior es más pequeño, se salta, independientemente de las fusiones anteriores. Silencio
Silencio **Ignorando los casos de borde (todos iguales, todos disminuyendo)** Silencio Puede llevar a errores fuera por uno. tención Inicializar `prev` a un número muy pequeño (`INT_MIN`, `-inf`, o `Integer.MIN_VALUE`). Silencio

-...

#### 3down⃣ Los escenarios de Ugly – Edge‐Case Traps

Silencio ¿Qué pasa? Silencio
Silencio...
Silencio **Números muy grandes (hasta 2 × 105)** Silencio Usar `int` en Java o C++ está bien; pero evitar `short` o `byte`. Silencio Stick con 32 bits firmados enteros. Silencio
Silencio ** Valores negativos** Silencio Las restricciones del problema garantizan positivo, pero si se modifica, el algoritmo todavía funciona con `prev = -inf`. Silencio Garantizar `prev` comienza más bajo que cualquier elemento posible. Silencio
tención **Emplety array** tención LeetCode garantiza al menos un elemento, pero la codificación defensiva es buena. Regresar 0 si la matriz está vacía. Silencio
Silencio **Todo disminuyendo** Silencio Podrías pensar equivocadamente que puedes mantener todo. El algoritmo guarda correctamente sólo el primer elemento. Silencio
Silencio **Todo igual** Silencio Algunos podrían pensar que puedes mantener todo. Puesto que cada elemento es igual a `prev`, usted mantiene todo - el resultado es `n`. Silencio

-...

### 4down Bon Bonus – Why This Problem is a Great Interview Question

1. **Claridad de Constraints** – Conjunto simple de enteros, operación fija.
2. ** Solución inmediata** – Un paso, una comparación.
3. **Deep Insight** – Te enseña a reconocer cuando una estrategia codictiva es óptima.
4. **Hora de Presión Amistosa** – Puedes codificar en 5 minutos, pero todavía necesitas explicar el razonamiento.

Una buena respuesta durante una entrevista:
■ “I'll iterate through the array, keeping a `prev` variable. Si el elemento actual es ≥ `prev`, lo guardaré y actualizaré `prev`. De lo contrario lo saltaré. Esto produce el tamaño máximo porque cualquier elemento más pequeño que el anterior nos obligaría a combinarlo con el elemento anterior, reduciendo el tamaño. El algoritmo es tiempo O(n) y espacio O(1). ”

-...

#### 5down⃣ Pensamientos finales

♪Make Array No-disminuir* es una hermosa ilustración de ** "mantenla si usted puede, de lo contrario dejarlo caer"**. La solución avaricia no sólo es eficiente sino también elegante: captura la esencia de la operación sin ninguna estructura auxiliar de datos.

Ya sea que esté escribiendo Java para LeetCode, Python para una entrevista de codificación, o C++ para una entrevista a nivel de sistemas, la lógica sigue siendo idéntica. Sólo recuerde inicializar `prev` a un valor más pequeño que cualquier elemento de matriz, luego atravesar una vez y contar los elementos “buenos”.

-...

##### 📌 Quick Reference – Code Snippets

Silencio Idioma Silencio Líneas Clave Silencio
Silencio...
Silencio **Java** Silencioso `for (int nums : nums) { if (num ю= prev) { prev = num; size++; } ' ¦
Silencio **Python** Silencio `for num in nums: if num Ê= prev: prev = num; tamaño += 1o de abril de 1994
Silencio **C+** Silencioso `for (int nums : nums) { if (num √≥= prev) { prev = num; ++size; } }`

-...

### 🚀 SEO Takeaway

Si usted está buscando para ser notado por los reclutadores o escáneres résumé automatizados, incluyen ** palabras clave** tales como:

- “Make Array Solución no disminuyente”
- “LeetCode 3523 Java”
- “Python algoritmo codicioso”
- “Entrevista de transformación de matriz C++”
- “La subsecuencia más larga no disminuyente”
- “Interview coding challenge solutions”

Estos términos son altamente buscados por los gerentes de contratación que buscan candidatos con cortes algorítmicos. Combinelos con los fragmentos de código de arriba, y tendrá un escaparate sólido para su cartera o LinkedIn.

¡Feliz codificación, y que sus arrays siempre permanezcan sin disminuir!