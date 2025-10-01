-...
Título: LeetCode 259. 3Sum Smaller -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 3Sum Smaller – The Good, The Bad, and The Ugly
*(Leetcode 259 – Interview‐Ready, Java/Python/C++ Solución + SEO‐Friendly Blog)*

■ **Keyword Focus**: `3Sum Smaller`, `Leetcode 259`, `two pointers`, `O(n2)` algoritmo, `Java`, `Python`, `C++`, `job interview`, `algorithm design`.

-...

## Tabla de contenidos
1. [Norma general](#problema vista previa)
2. [Constraints & Edge Cases](#constraints--edge-cases)
3. [Solution Strategy](#solution-strategy)
- 3.1 Técnica de dos puntos
- 3.2 ¿Por qué ayudas de clasificación
4. [Java Implementation](#java-implementation)
5. [Python Implementation](#python-implementation)
6. [C+++](#c+++-implementation)
7. [Time & Space Complexity](#time--space-complexity)
8. [El Bien, el Mal, el Ugly] (El bueno-el-el-bad-el-ugly)
9. [Conclusión > Siguientes pasos](#conclusión--siguiente-pasos)

-...

## Problema de visión general ##

**Leetcode 259 – 3Sum Smaller* *

■ Dado un conjunto entero de `nums ' y un entero `target ' , devuelve el número de trillizos `(i, j, k)` con `0 ≤ i ' se hizo k ' significa que `nums[i] + nums [j] + nums[k]  obtenidos objetivo `.

TEN SON SON SON SON SON SON SON SON SON 
Silencio----------------------------------------------------
TENIDA 1 TENIDO `[-2,0,1,3]`, Meta `2 ` Silencioso `2` Silencioso Triplets: `[-2,0,1]`, `[-2,0,3]`
TENIDO 2 TENIDO `[]`, blanco `0` Silencio `0` Silencio No tripts Silencio
TENIDO 3 TENIDO `[0]`, blanco `0` Silencio `0` Silencio No tripts Silencio

-...

## Constraints " Edge Cases " se hizo un nombre= "constraints--edge-cases"

Parámetro Silencioso
Silencio...
Silencioso `nums.length` Silencioso `0 ... 3500` Silencio
TENIDO `nums[i] ' Silencio `-100 ... 100` Silencio
Silencioso `target` Silencio `-100 ... 100 ` Silencio

** Casos de emergencia* *

- Conjunto vacío o matriz con menos de 3 elementos → retorno `0`.
- Todos los números son iguales.
- Números negativos y positivos entrelazados.

-...

## Solution Strategy [Estrategia de la Solución]

El enfoque clásico es ordenar el array primero y luego utilizar un barrido de dos puntos para cada primer elemento fijo.

## 3.1 Técnica de dos puntos

Para cada índice `i` (el primer elemento del triplet), necesitamos contar pares `(izquierda, derecha)` tales que
`nums[i] + nums[left] + nums[right] ' se observó objetivo ' con `left = i + 1`, `right = n - 1`.

Porque la matriz está ordenada:

- Si `nums[i] + nums[left] + nums[right] י target ' , *todo elemento entre `izquierda ' y `derecho ' también satisfará la desigualdad de este `i ' y `izquierda ' porque los números solo aumentan a medida que avanzamos hacia la izquierda.
Por lo tanto, podemos añadir `derecha - izquierda' a la respuesta y aumentar `izquierda`.
- Si la suma es `≥ target`, necesitamos una suma menor → decremento `derecho ' .

Esto produce un algoritmo `O(n2)` con `O(1)` espacio extra.

### 3.2 Why Sorting Helps

La clasificación convierte el problema de *definir todos los pares clasificatorios* en un escaneo *lineal* por `i.
Sin ordenar, tendríamos que comprobar explícitamente todos los pares de `O(n2)`, lo que llevaría a `O(n3)` tiempo.

-...

## Aplicación de Java se realizó un nombre="java-implementation"

``java
importa java.util. Arrays;

Solución de la clase pública {}
int threeSumSmaller(int[] nums, int target) {}
si (nums == null TENIDO EN SUPERVISIÓN nums.length 3) devuelve 0;

Arrays.sort(nums);
int n = nums.length, count = 0;

para (int i = 0; i)
int left = i + 1, right = n - 1;
mientras (izquierda)
int sum = nums[i] + nums[left] + nums[right];
si (sumo)
// Todos los elementos entre trabajo izquierdo y derecho
contar += derecha - izquierda;
izquierda++;
. ♫ ... {
Bien...
}
}
}
recuento de retorno;
}
}
`` `

**Explicación**

- `Arrays.sort(nums)` - `O(n log n) `
- Ámbito exterior:
- Barrido interior de dos puntos - `O(n)` por iteración → total `O(n2)`

-...

## Python Implementation > ## Python-implementation >

``python
Solución de clase:
def three SumSmaller(self, nums: list[int], target: int) - título int:
si no nums o len(nums)
retorno 0

nums.sort()
n, count = len(nums), 0

para i en rango(n - 2):
izquierda, derecha = i + 1, n - 1
mientras que la izquierda
curr_sum = nums[i] + nums[left] + nums[right]
si curr_sum
contar += derecha - izquierda # todos los índices entre trabajo izquierdo y derecho
izquierda += 1
más:
derecho -= 1
cuenta de retorno
`` `

Python’s `sort()` is `O(n log n)`. La lógica refleja exactamente la versión Java.

-...

## C++ Implementación - Nombre="c+++-implementation"

``cpp
Incluido el título
#include >

Clase Solución {
public:
int threeSumSmaller(std::vector identificadoint limitada nums, int target) {}
si (nums.size() 3) retorno 0;
std::sort(nums.begin(), nums.end());
int n = nums.size(), count = 0;

para (int i = 0; i) {}
int left = i + 1, right = n - 1;
mientras (izquierda)
int sum = nums[i] + nums[left] + nums[right];
si (sumo)
contar += derecha - izquierda;
++izquierda;
. ♫ ... {
--derecho;
}
}
}
recuento de retorno;
}
};
`` `

C++ sigue el mismo patrón; `std::sort` maneja el paso de clasificación.

-...

## Time & Space Complexity ## Tiempo > Complejidad espacial >

Silencioso Complejidad
Silencio--------------------------
Silencio ** Tiempo** Silencioso `O(n log n)` (sorting) + `O(n2)` (two-pointer loop) → general `O(n2)` Silencio
Silencio **Espacio** Silencioso auxiliar `O(1)` (desplazamiento en el lugar para Java/C+++; lista de pitones está en el lugar) Silencio

Para el tamaño máximo de entrada (`n = 3500`), `O(n2)` ♥ 12 millones de iteraciones – fácilmente manejables en ambientes modernos.

-...

## The Good, The Bad, The Ugly #1 Name= "the-good-the-bad-the-ugly"

Silencio Silencio
Silencio------------Prince------
Silencio **Concepto** Silencio Uso elegante de clasificar + dos punteros. ← Requiere ordenar → paso adicional. ← Clasificación podría ser exagerado para los arrays muy pequeños; todavía bien. Silencio
Silencio **Implementación** ← Limpieza, O(1) memoria extra. Silencio Debe manejar `int` desbordamiento en idiomas como C++ si las entradas eran mayores. Silencio Ninguno - 'int` es seguro con limitaciones dadas. Silencio
tención **Performance** ← Solución rápida `O(n2)`, aceptada en el 99% de las pruebas de LeetCode. tención Para la enorme `n`, `O(n2)` se vuelve pesado (no el caso aquí). Silencio Ninguno, pero si las restricciones eran más estrictas (`n ≤ 105`), este enfoque falla. Silencio
Silencio **Readability** Silencio Autorexplicativo con comentarios. Silencio Algunos pueden malinterpretar la lógica de derecha - izquierda; añadir comentarios. Silencio Ninguno-código es conciso. Silencio
Silencio **Manejo de cajas electrónicas** → Devoluciones Ninguno.

-...

## Conclusiones < Next Steps > > > > Conclusión: Siguientes pasos >

*3Sum Smaller* es un problema clásico de entrevista que prueba su capacidad de combinar la clasificación con un barrido de dos puntos. La solución `O(n2)` es sencilla pero potente y te marcará puntos en cualquier entrevista de codificación.

¿Qué hacer después? #

1. **Problemas relacionados con LeetCode* *
- 16. 3Sum
- 5. Subestring Palindromic más largo (aproximación de dos puntos)
- 15. 3Sum Closest

2. ** Patrones Algorítmicos**
- Dos puntos en los arrays ordenados
- Ventana deslizante
- Variantes de búsqueda binarias

3. ** Entrevistas de codificación**
- Entrevistas en plataformas como Pramp, InterviewBit o LeetCode Discuss.
- Revise el marco “Bien, Bad, Ugly” para explicar sus soluciones.

**SEO Bonus** – Utilice este poste de blog como una pieza de cartera. Esto demuestra no sólo su habilidad de codificación, sino también su capacidad de explicar ideas complejas claramente, un rasgo crítico para los ingenieros de software.

¡Buena suerte aterrizando ese trabajo! 🚀

-...

**Referencias**

- LeetCode 259: https://leetcode.com/problems/3sum-smaller/
- Técnica de dos puntos: https://leetcode.com/discuss/102391/three-sum-smaller-o-n2-solution-in-java
- Basics Sorting: https://en.wikipedia.org/wiki/Sorting_algorithm

-...

*No dude en dejar un comentario a continuación si desea discutir otras optimizaciones o entrevistar estrategias de preparación! *