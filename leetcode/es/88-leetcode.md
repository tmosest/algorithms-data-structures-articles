-...
Título: LeetCode 88. Merge Sorted Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

## 🚀 LeetCode 88 - Merge Sorted Array
*Dificultad* Fácil
** Idiomas:** Java Silencio Python Silencio C++
** Complejidad del tiempo:** *(m + n)* (optimal)
** Complejidad del espacio:** *O(1)* (en lugar)

■ **¿Quieres aterrizar esa entrevista de instrucciones de datos? * *
■ Problemas de masterización como *Merge Sorted Array* muestra a los reclutadores que sabes escribir código limpio y óptimo y puedes pensar en términos de *time* vs. *space*. A continuación encontrará una profunda inmersión – la “buena, la mala y la fea” – más soluciones de producción en tres idiomas principales.
■ **Keywords:** Merge Sorted Array, Leetcode 88, entrevista problema de codificación, algoritmo O(m+n) Java, Python, soluciones C++, preparación de entrevistas de trabajo, entrevista de estructura de datos, consejos de entrevista técnica.

-...

Problema Recap

Se le dan dos arrays enteros que ya están ordenados en orden de no disminuir:

Silencio Variable Silencio Significado Silencioso
Silencio------------------------
Silencio `nums1` Silencio Primera matriz, **tiene espacio para `m + n` elementos**. Los primeros " elementos " son válidos, los últimos `n ' son `0 ' y significan como " amor " .
TENIDO `M` TENIDO Número de elementos válidos en `nums1`.
TENIDO `nums2` TENIDO Segunda matriz, todos los elementos `n` son válidos.
TENIENDO `n` TENIDO Número de elementos en `nums2`.

Su tarea es combinar `nums2` en `nums1` de tal manera que la matriz resultante se ordena en orden no-disminución. La fusión debe suceder **en lugar** (sin asignación de matriz adicional).

■ *Ejemplo*
" texto
[1,2,3,0,0,0], m = 3
[2,5,6], n = 3
[1,2,3,5,6]
" `

-...

## 🎯 Why This Problem Rocks in Interviews

1. **Showcases pointer manipulation** – Los reclutadores les encanta ver cómo manejan los índices.
2. **El intercambio de espacio a tiempo** – el seguimiento pide tiempo O(m + n), destacando su comprensión de algoritmos óptimos.
3. **Concientización por caso Edge** – arrays de longitud cero, números negativos, valores idénticos, etc.
4. **Common startner error** – utilizando `Arrays.sort` en toda la matriz (O(m+n)log(m+n)))) en lugar de una fusión lineal.

-...

El bueno, el malo, el feo

TENIDO Aspecto TENIDO Qué Apuntar Para Silencio Qué Para Evitar Silencio Por qué Importa TENIDO
Silencio------------------------------- La vida eterna
Silencio **Bien** Silencio *O(m + n) tiempo, O(1) espacio* se fusiona desde el **end**. Silencio Silencio En lugar, ninguna asignación adicional, lógica puntero clara. Silencio
Silencio **Bad** Silencio Sobre-pensamiento: usando un "sort" integrado o creando un nuevo array. TEN ANTERIOR Extra O(m + n) espacio o O(m+n)log(m+n)) tiempo – se ve descuidado en una pantalla de entrevista. Silencio
Silencio **Ugly** Silencio Off‐por-one bugs: olvidándose de que el amortiguador de `nums1` está al final, mal manejo de arrays vacíos. Silencio

-...

## 🛠י Solución Optimal (O(m + n))

## Core Idea

Traverse **Desde el final** de ambos arrays:

1. Mantener tres índices:
- `i = m‐1` (último elemento válido en `nums1`)
- `j = n-1` (último elemento en `nums2`)
- `k = m + n - 1` (última posición en `nums1`)

2. Mientras que " j " 0`:
- Si 0` **and** `nums1[i] œ nums2[j]`, place `nums1[i]` at `nums1[k]`.
- Else place `nums2[j] ' a `nums1[k].
- Mueva el puntero correspondiente a la izquierda y decremento 'k'.

3. Si `j ' se vuelve negativo, los elementos restantes `nums1` ya están en su lugar; si `i` se vuelve negativo, el bucle termina temprano (mantener `nums2` ya se copian).

### Why It Works

- Nunca sobreescribimos un valor que no ha sido considerado aún porque nos estamos moviendo desde el final hacia el frente.
- Cada elemento se mueve al máximo una vez → **Tiempo lineal**.
- No hay matriz adicional → **Espacio auxiliar constante**.

-...

## 📦 Code Implementations

■ **Consejo:** Prueba con los casos de borde de los ejemplos, especialmente `m = 0`, `n = 0`, y números negativos.

## Java

``java
Solución de la clase pública {}
public void merge(int[] nums1, int m, int[] nums2, int n) {
int i = m - 1; // último índice válido en nums1
int j = n - 1; // último índice en nums2
int k = m + n - 1; // último índice en nums1 general

mientras que (j >= 0) { // sólo necesita comprobar nums2
si (i >= 0 ' nums1[i]  Confes nums2[j]) {}
nums1[k--] = nums1[i--];
. ♫ ... {
nums1[k--] = nums2[j--];
}
}
}
}
`` `

■ *Por qué esto es genial* *
■ - `mientras (j. 0)` garantiza que terminemos de copiar `nums2`.
" La guardia " 0` nos protege de acceder a `nums1[-1]`.
No `Arrays.sort`, ninguna matriz extra.

-...

## Python

``python
Solución de clase:
def merge(self, nums1: List[int], m: int,
nums2: List[int], n: int Ninguno.
"
No devuelva nada, modifique nums1 en su lugar.
"
i, j, k = m - 1, n - 1, m + n - 1
mientras j 0:
si >= 0 y nums1[i] œ nums2[j]:
nums1[k] = nums1[i]
I -= 1
más:
nums1[k] = nums2[j]
j)= 1
k -= 1
`` `

■ #Pythonic touch #
- Usa nombres variables claros `i`, `j`, `k`.
√≥ - La condición de bucle `mientras j не= 0` asegura que se coloquen todos los elementos `nums2`.

-...

### C++

``cpp
Clase Solución {
public:
vacuno merge(vector identificadoint ánimo nums1, int m,
vector significado
int i = m - 1; // último elemento válido en nums1
int j = n - 1; // último elemento en nums2
int k = m + n - 1; // último índice en nums1 general

mientras que (j >= 0) {
si (i >= 0 ' nums1[i]  Confes nums2[j]) {}
nums1[k--] = nums1[i--];
. ♫ ... {
nums1[k--] = nums2[j--];
}
}
}
};
`` `

■ **C++ matices**
√≥ - Utiliza referencia para evitar copiar `nums1`.
■ - `vector asignadointю ` mantiene la firma que LeetCode espera.

-...

## 📚 Step‐by‐Step Walkthrough ( Ejemplo Java)

Silencio Silencio Silencio Silencio Silencio Silencio Silencio
Silencio--------Prince--------
TENIDO 1 TENIDO `i = 2`, `j = 2`, `k = 5` TENIDO Apuntadores en los extremos
TENIDO 2 TENIDO `nums1[i] = 3`, `nums2[j] = 6` → place `6` at `nums1[5]` TENIDA `nums1 = [1,2,3,0,0,6] Silencio
Silencio 3 Silencio `j = 1`, `k = 4` Silencio
TENIDO 4 TENIDO `nums1[i] = 3`, `nums2[j] = 5` → place `5` TENIDO `nums1 = [1,2,3,0,5,6] Silencio
Silencio 5 Silencioso `j = 0`, `k = 3` Silencio ...
Silencio 6 Silencioso `nums1[i] = 3`, `nums2[j] = 2` → lugar `3` Silencio `nums1 = [1,2,3,5,6] Silencio
Silencio 7 Silencio `i = 1`, `k = 2` Silencio ...
Silencio 8 Silencioso `nums1[i] = 2`, `nums2[j] = 2` → lugar `2` Silencio `nums1 = [1,2,3,5,6] Silencio
Silencio 9 Silencio `j = -1` → extremos del bucle ← Merge terminó Silencio

-...

## 🎯 Interview‐Ready Checklist

1. **Declarar las limitaciones** – `nums1.length == m + n`, `nums2.length == n`.
2. **Explicar tiempo/espacio trade‐off** – “Haremos tiempo O(m+n) y espacio O(1). ”
3. ** Casos de borde hundido** – `m == 0`, `n == 0`, elementos iguales.
4. **Mostrar el enfoque puntero** – enfatizar “a partir del final” para evitar la sobreescritura.
5. **Write clean code** – nombres de variables claros, comentarios donde sea necesario.
6. **Test mentalmente** – correr a través de un par de escenarios en la pizarra.

■ **Pro tip**: Si el entrevistador pide el tiempo *seguir* (O(m + n)), señala que el algoritmo anterior ya lo logra. Si piden un espacio *(m + n)*, mencione que usted podría utilizar un array temporal pero derrota el propósito de la fusión en lugar.

-...

## 📈 SEO Snapshot (Meta Tags " Snippets)

``html
> < > > > > > > > > > >
Contenido de "Solve LeetCode 88 Merge Sorted Array en Java, Python y C++ con un algoritmo O(m+n) óptimo en el lugar. Aprende las trampas, los casos de borde y los consejos de entrevista."
Contenido de "Merge Sorted Array, Leetcode 88, problema de entrevista, algoritmo O(m+n), Java merge array, Python merge array ordenados, C++ merge array, coding interview prep"
`` `

■ **Por qué esto ayuda* *
■ Estas etiquetas superan su artículo en resultados de búsqueda para cualquier persona que busque dominar este problema específico de LeetCode, perfecto para los reclutadores escaneando carteras de candidatos.

-...

## ⋅ Final Takeaway

- **Bueno**: El enfoque de tres puntos desde atrás es limpio, lineal y en lugar.
- **Bad**: Usar 'sort' o asignar memoria extra muestra una falta de pensamiento óptimo.
Olvidando que el búfer está al final, lleva a "ArrayIndexOutOfBounds".

Dominar este problema demuestra su capacidad para leer limitaciones, diseñar un algoritmo eficiente y escribir código de producción. Traiga este conocimiento a su próxima entrevista técnica, y mostrará a los reclutadores que está listo para abordar retos de estructuración de datos en el mundo real.

Buena suerte, y feliz codificación! 🚀