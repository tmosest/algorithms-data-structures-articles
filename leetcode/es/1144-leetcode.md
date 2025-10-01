-...
Título: LeetCode 1144. Disminuir Elementos Para Hacer Array Zigzag -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1144. Disminuir elementos para hacer Array Zigzag
**LeetCode #1144 ← Medium Silencioso

■ * Objetivo*
■ Dado un conjunto entero `nums`, en un movimiento se puede decrementar cualquier elemento por 1.
■ Devuelve el número mínimo de movimientos requeridos para transformar `nums` en una matriz *zig‐zag*, es decir.
√≥ - cada elemento incluso indexado es mayor que sus elementos adyacentes ( ' A[0] неле A[1] > > )
√≥n - o cada elemento con índices impares es mayor que sus elementos adyacentes ( ' A[0] > A[1] > > >

-...

## ¿Por qué es un problema de entrevista clásica?

* **Introducción simple* → fácil de verbalizar durante una entrevista.
* **Dos opiniones alternativas** (even‐peaks vs. odd‐peaks) → muestra la capacidad del candidato para manejar la lógica ramificadora.
* **Greedy / decisiones locales** → perfecta para la enseñanza * "por qué obras codictivas"*.
* ** Limitaciones pequeñas (≤ 1000)** → el entrevistador puede esperar una solución O(n) sin enfatizar sobre el rendimiento.

-...

## The Greedy Idea – “Fix the bad peaks”

Para cada índice `i` sólo necesita saber si es **actualmente un pico** con respecto a sus dos vecinos.
Si no es un pico, podemos bajarlo hasta que se convierta en un pico válido.
La forma más barata es bajarlo lo suficiente como para ser *strictamente* más pequeña que la menor de sus dos vecinos.

`` `
cost(i) = max(0, nums[i] - min(nums[i‐1], nums[i+1]) + 1)
`` `

*El `+1` garantiza una desigualdad estricta. *
Si el índice está en el límite (`i==0` o `i==n-1`) el vecino desaparecido es tratado como "infinito", es decir, el elemento nunca necesita ser reducido para ese lado.

-...

## Dos soluciones independientes

Computamos el costo total para dos escenarios independientes:

1. **Incluso los índices deben ser picos** ( " A[0] " A[2] " ).
2. **Los índices extraños deben ser picos** ( " A[0] " )

La respuesta es el mínimo de los dos totales.

Debido a que cada elemento es inspeccionado una vez, el algoritmo se ejecuta en **O(n)** tiempo y utiliza **O(1)** espacio extra.

-...

## 1. Aplicación de Java

``java
importar java.util*;

Clase Solución {
int moves públicosToMakeZigzag(int[] nums) {
int evenCost = 0; // picos en posiciones uniformes
int oddCost = 0; // picos en posiciones extrañas
int n = nums.length;

para (int i = 0; i)
// Determinar el límite inferior requerido de los vecinos
Int lowerBound = Integer.MAX_VALUE;
si 0) inferiorBound = Math.min(lowerBound, nums[i - 1]);
si (i + 1 י n) inferiorBound = Math.min(lowerBound, nums[i + 1]);

// Si el elemento actual ya es más bajo que ambos vecinos, sin costo
si {}
int cost = nums[i] - menorBound + 1;
(i) == 0)/incluso índice
incluso Costo += costo;
más
oddCost += costo;
}
}
devolver Math.min(evenCost, oddCost);
}
}
`` `

■ *Puntos clave*
* `Integer.MAX_VALUE` garantiza que el lado con ningún vecino es ignorado.
* El bit‐op `i ' es una pequeña velocidad sobre `i % 2`.
* No hay arrays adicionales – el espacio es constante.

-...

## 2. Aplicación de los pitones

``python
Solución de clase:
def moves ToMakeZigzag(self, nums: List[int]) int:
even_cost = odd_cost = 0
n = len(nums)

para i en rango(n):
inferior = flotante('inf')
si yo 0: inferior = min(más bajo, nums[i - 1])
si i + 1 י n: inferior = min(abajo, nums[i + 1])

si nums[i] √≥ inferior:
cost = nums[i] - inferior + 1
si i % 2 == 0:
costo +=
más:
odd_cost += cost

retorno min(even_cost, odd_cost)
`` `

■ Python está muy cerca de la lógica Java – sólo cambios de sintaxis.
El papel de “sin vecino” es “float('inf')”.

-...

## 3. Aplicación C++

``cpp
Clase Solución {
public:
int movesToMakeZigzag(vector identificadoint limitada nums) {
mucho tiempo Costo = 0, oddCost = 0; // use long long for safety
int n = nums.size();

para (int i = 0; i) {}
int lower = INT_MAX;
si (i > 0) inferior = min(más bajo, nums[i-1]);
si (i + 1 י n) inferior = min(abajo, nums[i+1]);

si (nums[i]
int cost = nums[i] - inferior + 1;
(i % 2 == 0) inclusoCost += costo;
más extraño Costo += costo;
}
}
volver estática_cast seleccionado(min(evenCost, oddCost));
}
};
`` `

■ ¿Por qué 'largo'?
■ En el peor de los casos cada elemento puede ser 1000 y podríamos añadir hasta 500 × 1000 Ω 500 000.
■ Todavía encaja en " in " , pero el uso de " largo " garantiza que no se desborde si crecen las restricciones.

-...

## Good, Bad & Ugly: What Interviewers Look For

Silencio **Aspecto** Silencio ** Lo que funciona** Silencioso**
Silencio----------------------------
tención **Greedy correctness** Silencio Reasonable explanation that lowering a bad peak cannot hurt future peaks ← Ignoring the `+1` for strictness tención Siempre double‐check inequalities tención
Silencio **Manejo diario** Silencio Tratar a los vecinos desaparecidos como “infinito” o saltar el cheque Silencio Off‐por-uno errores (“i-1 √= 0`, `i+1 י n`) Silencio Uso de la función de ayuda o pre-computado min Silencio
Silencio **La complejidad del tiempo** ← O(n) single pass tención Extra O(n) arrays o bucles anidados
Silencio **Complejidad del espacio** TEN O(1) auxiliary TENIDO Crear copias del array TENIENTES Recuerde que el limite `n ≤ 1000` es indulgente, pero los entrevistadores esperan óptima vida
Silencio **Readability** Silencio Nombres variables claros, comentarios Silencio Números mágicos (`1`) sin explicación Silencio Usar nombres significativos (`evenCost`, `oddCost`, `lower`) Silencio
Silencio **Edge cases** tención Handles único elemento, todos iguales, estrictamente decrecientes arrays Silencio Asumees al menos dos elementos viv Siempre test with `n=1` ←

-...

## Testing Your Solution

``python
def test():
sol = Solución()
afirmar sol.movesToMakeZigzag([1,2,3]) == 2
afirmar sol.movesToMakeZigzag([9,6,1,6,2]) == 4
afirmar sol.movesToMakeZigzag([3]) == 0 # elemento único
afirmar sol.movesToMakeZigzag([5,4,3,2,1]) == 4 # ¿Ya zigzag? computador
print("Todas las pruebas pasadas")
test()
`` `

Ejecute lo anterior para las tres implementaciones; deben producir los mismos resultados.

-...

## SEO‐Optimized Blog Article

■ **Título (H1):**
■ *“Master LeetCode 1144: Disminuir los elementos para hacer que Array Zigzag – Java, Python, C++ Soluciones " Entrevista Insights”*

■ **Meta Descripción (Ω155 chars):**
■ *Aprenda el algoritmo codicioso para LeetCode 1144 (Disminuir Elementos para Hacer Array Zigzag). Obtenga Java, Python, código C++, análisis de complejidad, manejo de bordes y consejos de entrevista. *

-...

### 1. Introducción

■ ¿Qué es un Zigzag Array? * *
■ Una secuencia que se alterna entre los picos y los valles: `A[0] > A[1] > A[2]  Confía A[3] > ... > o lo contrario.
■ ¿Por qué es interesante? #
■ Te obliga a pensar localmente (cada elemento vs. vecinos) mientras optimiza globalmente (movimientos totales).

### 2. Reposición de problemas

■ Dados `nums[0 ... n‐1]` (1 ≤ n ≤ 1000, 1 ≤ nums[i] ≤ 1000), devolver el número mínimo de movimientos de decremento necesarios para convertir el array en un zigzag.
■ Un movimiento: `nums[i] = nums[i] - 1.

### 3. Intuición

* Un pico debe ser mucho mayor que sus vecinos.
* Si no lo es, la solución más barata es bajarlo lo suficiente.
* La optimización de esta solución local se debe a que la reducción de un pico no puede mejorar el requisito de ningún otro elemento – sólo potencialmente relaja las limitaciones de los vecinos.

### 4. Algoritm de paso a paso

1. **Initializar dos contadores**: `evenCost` y `odd Costo.
2. **Arrastre a través de todos los índices** `i = 0 ... n‐1`.
* Find `lowerBound = min(nums[i-1], nums[i+1])` (ignorar a los vecinos desaparecidos).
* If `nums[i] œ lowerBound`, compute `cost = nums[i] - abajoBound + 1`.
* Add `cost` to `evenCost` if `i` is even, else to `odd Costo.
3. **Retorno `min(evenCost, oddCost)**.

### 5. Análisis de la complejidad

TEN TERRITOR TEN Fórmula ANTE ANTE ANTE ANTE
Silencio--------------------
TENIDO Tiempo TENIDO ÚNICO paso sobre la matriz Silencio **O(n)** Silencio
TENIDO Espacio TENIDO Variables auxiliares constantes

### 6. Casos de borde

← Input Silencio ¿Por qué importa?
Silencio...
TENIDO `[1] TENIDO Único elemento TENIDO `0` (ya zigzag) TENIDO
TENIDO `[5,5]` Silencio Todo igual TENIDO `2 ` (elemento medio más bajo)
Silencio `[10,1,10,1,10]` Silencio Ya zigzag (pocas altas) Silencio `0` Silencio
TENIDO `[1,1000,1,1000,1]` TENIDO Grandes picos TENIDO `999 ` (más bajo elemento) TENIDO

### 7. Código en tres idiomas

*Java, Python, C++ snippets (ver arriba). *
*Todos comparten la misma lógica, difierendo sólo en sintaxis. *

### 8. Pitfalls comunes en entrevistas

1. **El olvido de la condición estricta de “propiedad”** – conduce a movimientos de baja contabilidad.
2. **Manejo incorrecto de los límites** – `i-1 ' 0 ' o `i+1 > > n ' cheques.
3. **Usando `conejo=` en lugar de `conejo` al comparar con los vecinos** - causa bucles infinitos en una implementación ingenua.
4. **Over-engineering** – construir nuevos arrays o utilizar la recursión innecesariamente.

### 9. Enfoques alternativos

* ** Programación Dinámica** – sobrematar para este problema; la codicia es óptima.
* ** Solución de dos pasos** – primer paso de cálculo requiere disminuciones, segunda suma de pase. Igual que codicioso pero dividido en pasos.
* **Bit-masking** – no aplicable; el patrón es fijo (peaks at even/odd indices).

#### 10. Conclusión

LeetCode 1144 es un escaparate perfecto para una estrategia codictiva limpia.
Al centrarse en las violaciones locales y corregirlas con un mínimo esfuerzo, puede garantizar el óptimo global.
Las implementaciones Java, Python y C++ se ejecutan en tiempo lineal, usan espacio constante y manejan con gracia todos los casos de borde.

■ **Listo para la entrevista? #
■ Practique el patrón codicioso, entienda por qué funciona, y recuerde explicar la estricta desigualdad y lógica de límites.
■ ¡Buena suerte!

-...

### 11. Call to Action

■ Si encontró este artículo útil, **Suscríbete** a nuestro boletín para pasarelas semanales de problemas de entrevista.
■ Deje un comentario con sus propias pruebas de periferia o pregunte sobre el próximo desafío de LeetCode.

-...

## Final Checklist Antes de la entrevista

1. **Explicar la idea avaricia** – no sólo “trabaja”.
2. **Mostrar el manejo de límites** – ilustrar con un diagrama corto.
3. **En vivo a través de un caso de prueba rápida** – por ejemplo, `[1,2,3]`.
4. **Las complejidades de la mención** – siempre tengan en cuenta.
5. **Mantenga el código legible** – nombres significativos, comentarios.

Con la solución, la rutina de pruebas, y las ideas de la entrevista, usted está listo para convertir el problema *Zigzag* de un rompecabezas en una entrevista de confianza.