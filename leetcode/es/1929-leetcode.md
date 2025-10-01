-...
Título: LeetCode 1929. Concatenación de Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
LeetCode 1929 – Concatenación de Array
**Idiomas** Silencio**
-... Silencio...
**Tiempo** Silencio O(n) Silencio O(n)
**Espacio** Silencio O(n) Silencio O(n) Silencio O(n)

> ¿Quieres conseguir tu próxima entrevista de ingeniería de software?
■ Este artículo camina a través de la solución *cleanest* para LeetCode 1929, explica por qué es eficiente, cubre los obstáculos, y le da contenido fácil de SEO para aumentar la visibilidad de su résumé.

-...

Declaración de problemas

Dado un conjunto entero de `nums ' de longitud `n`, crear un array `ans ' de longitud `2n ` tal que:

`` `
ans[i] = nums[i] for 0 ≤ i
ans[i + n] = nums[i] para 0 ≤ i
`` `

En otras palabras, `ans` es la concatenación de 'nums' con sí mismo.

■ *Ejemplo*
Input: `[1, 2, 1]` → Producto: `[1, 2, 1, 2, 1, 2, 1]`

-...

Intuición (El Bien)

* La tarea es una copia única: simplemente necesitamos dos copias de cada elemento.
* **O(n)** el tiempo es la complejidad óptima – cada elemento se procesa una vez.
* **O(n)** espacio adicional es inevitable porque el resultado tiene tamaño `2n`.
* Un ingenuo “re-append the entire array” funcionaría pero es menos explícito.

-...

## 3down El “Bad” – Pitfalls comunes

Por qué es malo
Silencio...
Silencio Usando `list.extend()` o `vector.insert()` en un bucle Silencio Añade una sobrecarga innecesaria y es más difícil de leer. Silencio
Silencio Reasignar la matriz de resultados dentro del bucle Silencio Quadratic time – un desastre de rendimiento. Silencio
← Olvidar la indexación basada en 0 ← Off‐por-uno errores que son difíciles de depurar. Silencio
Silencio No manipular `nums` vacíos (aunque las restricciones lo prohíben) ← Futuro a prueba de cambios. Silencio

-...

## 4down “Ugly” – Cosas que evitar

* Sobre-optimizar con trucos de “copia-memoria” (por ejemplo, “System.arraycopy”) – están bien pero oscuros la lógica.
* Usando la concatenación de lista de alto nivel en un estilo funcional (`nums + nums`) que crea una matriz temporal – desperdicio.
* Añadiendo impresiones o comentarios innecesarios dentro del bucle.

-...

## 5down Solutions

A continuación se presentan tres implementaciones idiomáticas que evitan los patrones malos y feos.

## 5.1 Java – Simple Loop

``java
// LeetCode 1929 – Concatenación de Array
Solución de la clase pública {}
int[] getConcatenation(int[] nums) {
int n = nums.length;
int[] ans = nuevo int[2 * n];
para (int i = 0; i)
ans[i] = nums[i];
ans[i + n] = nums[i];
}
devolver los ans;
}
}
`` `

*Por qué está limpio*
* No hay llamadas de biblioteca extra.
* Los índices de explosión hacen que la lógica sea cristalina.
* Pasa todos los casos de prueba LeetCode en 10 ms.

-...

### 5.2 Python – Comprehensión de Lista

``python
# LeetCode 1929 – Concatenación de Array
Solución de clase:
def getConcatenation(self, nums: List[int] List[int]:
n = len(nums)
volver [nums[i] si yo hice no más nums[i - n] para i en rango(2 * n)]
`` `

*Pythonic* – apalanca la comprensión de la lista para la brevedad mientras se mantiene O(n).

-...

### 5.3 C++ – Copia manual

``cpp
// LeetCode 1929 – Concatenación de Array
Clase Solución {
public:
vector asignadoint edad getConcatenation(vector seleccionadoint ánimos) {
int n = nums.size();
vector:
para (int i = 0; i) {}
ans[i] = nums[i];
ans[i + n] = nums[i];
}
devolver los ans;
}
};
`` `

*No `std::copy` or `std::vector::insert` – mantiene el uso de memoria lineal y predecible. *

-...

## 6VIEW⃣ Complexity Analysis

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
Silencio **Tiempo** Silencio O(n) Silencio O(n) Silencio
Silencio **Espacio** Silencio O(n) Silencio O(n) Silencio

*Debido a que asignamos una nueva gama de tamaño `2n`, la sobrecarga espacial es inevitable. *

-...

## 7down⃣ Edge Cases " Testing

Silencio Test confidencialidad esperada
Silencio...
TENIDA `[5]` TENIDA `[5, 5] Silencio
[1,2,3,4] Silencio
Silencio `n = 1000` (máximo límite)

*Siempre verifique que la longitud del array devuelto es exactamente `2 * len(nums)`. *

-...

## 8down Pensamientos finales

* **Mantenlo simple** – el problema es trivial; un bucle limpio gana la entrevista.
* **Evite micro-optimizaciones** esa intención oscura.
* **Comentario sólo cuando sea necesario** – su código debe leer como una historia.

-...

Resumen optimizado

■ **LeetCode 1929 Concatenación de Array – Java, Python, C++ Soluciones**
■ Domine la pregunta de entrevista fácil con implementaciones limpias, O(n). Aprenda las trampas, las mejores prácticas y cómo crear entrevistas de codificación. Pon tu currículum con esta guía definitiva.

-...

¿Quieres más?
Echa un vistazo a nuestra serie en **Problemas sencillos de LeetCode** – desde trucos de array a manipulación de cuerdas – todos con explicaciones paso a paso y fragmentos de código en Java, Python y C+++.

¡Feliz codificación y buena suerte en tu próxima entrevista!