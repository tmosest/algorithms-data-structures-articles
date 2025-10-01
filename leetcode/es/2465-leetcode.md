-...
Título: LeetCode 2465. Número de promedios distintos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 2465 – Número de promedios distintos
**Easy Silencio 1 ms (Java)* *
▪ https://leetcode.com/problems/number-of-distinct-averages/

-...

#### ⋅ What You'll Learn

Por qué importa
Silencio...
tención **Sorting + Dos-Pointer** Silencio Técnica clásica para problemas “pick min & max” Silencio
Silencio **HashSet for uniqueness** TEN O(1) average lookup/insert TEN
Silencio **Dealing with flotaing-point** Silencio Evitar las trampas de precisión
tención **Tiempo & Análisis de la Complejidad Espacial**
Silencio **Aplicación en español** Silencio Shows usted puede resolver el mismo problema en Java, Python & C++

-...

## 📝 Problema Resumen

Dado un **even‐length** array `nums` (2 ≤ `nums.length` ≤ 100, cada elemento 0–100), repetidamente

1. Eliminar el número *smallest*
2. Eliminar el número * más grande*
3. Computar su promedio `(a + b) / 2`

Devuelve el **cuento de promedios distintos** producidos.

■ Ejemplo
■ `nums = [4,1,4,0,3,5] `` → promedios: 2.5, 2.5, 3.5 → respuesta `2`.

-...

Intuición

El proceso es determinista hasta los lazos (cualquier min/max puede ser elegido).
Si nosotros ** surtiremos** el array, el más pequeño y más grande son simplemente `nums[0]` y `nums[n‐1]`.
Después de emparejarlos, podemos movernos hacia adentro: 'l++' y 'r--'.
Cada par produce un promedio; solo necesitamos contar cuántos promedios ** únicos** obtenemos.

-...

♪ ♪ ♪ ♪♪ Fuerza contra Optimal

Silencio Silencio Silencio Silencio Silencio Silencio Silencio Silencio
Silencio----------------------------
Silencio Retire min/max de un multiset cada paso (heap, list) Silencio **O(n2) **O(n)** Silencio Demasiado lento, innecesario. Silencio
Silencio **Sort + dos punteros + hash set** Silencio **O(n log n)** Silencio **O(n)** viv Optimal for given constraints. Silencio

-...

## 📦 Implementation

A continuación se encuentran soluciones limpias y autocontenidas en **Java**, **Python**, y **C+**.
Los tres usan la misma idea algorítmica.

-...

## Java

``java
importar java.util*;

Solución de la clase pública {}
public int distinct Promedios (int[] nums) {
// 1. Ordenar por llevar min & max a los extremos
Arrays.sort(nums);

// 2. Utilice un HashSet para mantener promedios únicos
Conjunto de datos = nuevo HashSet correctamente();

int l = 0, r = nums.length - 1;
mientras que (l
// El doble es bueno – los valores son en la mayoría de 100, los extremos promedio en .0 o .5
doble avg = (nums[l] + nums[r]) / 2.0;
set.add(avg);
l++;
r...
}
set.size();
}
}
`` `

■ ¿Por qué "doble"?
■ Con los límites dados, la suma es ≤ 200 y la división por 2 da un entero o un .5 decimal.
■ La precisión del doble es mucho más allá de eso, por lo que no hay riesgo de dos promedios distintos colisionando.

-...

## Python

``python
Solución de clase:
def distinct Promedios (yo, nums: List[int]) - int:
nums.sort()
visto = set()
l, r = 0, len(nums) - 1
mientras que l
avg = (nums[l] + nums[r]) / 2.0
visto.add(avg)
l += 1
r)= 1
len(seen)
`` `

■ **`set`** en Python es un hash-set con insertos amortizados O(1).
■ El código sigue el mismo patrón de dos puntos.

-...

### C++

``cpp
Clase Solución {
public:
int distinct Promedios(vector seleccionados) {
(nums.begin(), nums.end());
unordered_setSe observó un doble título;
para (int l = 0, r = nums.size() - 1; l ' identificado r; ++l, --r) {
doble avg = (nums[l] + nums[r]) / 2.0;
visto.insert(avg);
}
retorno visto.size();
}
};
`` `

√ ** `unordered_set`** da O(1) insert/lookup promedio.
■ Usar `doble` es seguro por la misma razón que Java.

-...

## 📊 Complexity Analysis

TEN TERRITORIO TEN ANTERIOR ANTERIOR
Silencio----------Prince----------------
TENIDO `nums` Silencio **O(n log n)** Silencio `n` ≤ 100, pero esto domina Silencio
← Dos puntos de trabajo Silencioso **O(n)** Silencio Un paso, trabajo constante
← HashSet operations Silencio **O(n)** Silencio Cada inserción/lookup es O(1) en promedio Silencio

**Total:** `O(n log n)` time, `O(n)` space.

Con `n` ≤ 100, todas las soluciones funcionan en milisegundos (se realizaron 5 ms en la práctica).

-...

## 🤔 Edge Cases > Pitfalls

Cómo evitar la muerte
Silencio...
Silencio **Igualidad de punto flotante** Silencio Todos los promedios son múltiplos exactos de 0,5; la comparación doble es segura. Silencio
tención **Ties for min/max** Silencio Cualquier opción funciona; clasificar resuelve deterministamente. Silencio
tención **Empleado** tención El problema garantiza incluso la longitud ≥ 2, por lo que no es necesario un manejo especial. Silencio
tención **Large values** tención Las limitaciones aseguran que 'int` + 'int' se ajuste en 32 bits. Silencio
Silencio ** Uso de memoria** Silencio `HashSet` tiene en la mayoría de los elementos 'n/2', diminuto para los límites dados. Silencio

-...

## 🐞 The “Ugly” Part

- Si tratas de mantener el array como un multiset y repetidamente `pollFirst()` / `pollLast()` utilizando un `TreeSet`, obtendrás una operación **log n** para cada par – *total vez* aceptable para 100 elementos, pero innecesaria complejidad.
- Utilizar un `doble' en un `HashSet` puede ser arriesgado en otros contextos (por ejemplo, con grandes números o muchos lugares decimales). Aquí el pequeño dominio garantiza seguridad.
- Algunos entrevistadores esperan que te des cuenta del patrón de dos puntos antes de escribir código. Omitir esta información puede llevar a la sobreingeniería.

-...

##  Settlement The “Good” Things

Una vez, una vez, una vez, una vez.
- **Determinista** - Sin aleatoriedad; fácil de probar.
- **Scalable** – Trabaja para arrays mucho más grandes si crecen las restricciones.

-...

## 📚 Takeaway Checklist

- [ ] Clasificar el array.
- [ ] Elementos de par entre los dos extremos ( " l " y " r " ).
- [ ] Compute average as a `double` (or `float`).
- [ ] Almacene en un set de hash para mantener únicos.
- [ ] Devuelve el tamaño del set.

-...

##  tuya SEO‐Optimized Blog Article (Full)

■ **Título**: *“Número de promedios distintos (LeetCode 2465) – Java, Python, C++ Soluciones + consejos de entrevista”*
■ **Meta Descripción**: *Solve LeetCode 2465 “Número de promedios distintos” en Java, Python y C++. Aprende el truco de dos puntos, el uso de hash set, y cómo crear este problema de entrevista. *
■ **Tags**: #LeetCode #Algorithm #TwoPointers #HashSet #InterviewPrep #Java #Python #C++

-...

#### Introduction

El problema “Número de promedios distintos” es un desafío engañosamente simple LeetCode que prueba su comprensión de la clasificación, técnica de dos puntos, y la piratería. En este artículo caminaremos a través del problema, la intuición detrás de la solución óptima, proporcionar código limpio en **Java, Python, y C+**, analizar su complejidad, y discutir los obstáculos comunes, mientras que mantener el artículo SEO-friendly para ayudarle a aterrizar esa entrevista de trabajo.

-...

## Problema Recap

■ ** Objetivo**: Eliminar el mínimo y máximo de un array de longitud uniforme repetidamente, calcular el promedio de cada par y contar cuántos promedios distintos se producen.

**Constraints* *

- `2 ≤ nums.length ≤ 100`, incluso
- `0 ≤ nums[i] ≤ 100`

-...

### Estrategia óptima

1. **Sorta la matriz.
Ahora el más pequeño es el índice `0`, más grande en el índice `n‐1`.
2. Use dos punteros ( " l " al principio, " al final).
Cada paso:
- Compute `(nums[l] + nums[r]) / 2.0`.
- Introducir en un set de hachís.
- Muévete.
3. Después del bucle, el tamaño del hash set es la respuesta.

¿Por qué es esto óptimo?
Debido a que cada par es independiente; clasificar lugares cada par min/max en posiciones fijas, eliminando la necesidad de estructuras de datos costosas como colas de prioridad. El hash set garantiza la singularidad en el tiempo esperado O(1).

-...

### Code Implementations

Silencio Idioma Silencio Código Silencio
Silencio------------
Silencio **Java** Нелителинилинаниханннымина.util.*; obedecidobr acordadobr confianzabr de clase pública Solución {нерениение public int distinct Promedios(int[] nums) { indicabr título Arrays.sort(nums); Establecer contactoDouble Establecer = nuevo HashSet implicado(); obedecebr título para (int l = 0, r = nums.length - 1; l ' identificador r; ++l, --r) { indicabr título doble avg = (nums[l] + nums[r]) / 2.0; secuestrar confianza set.add(avg); Silencio
Silencio **Python** Нелилилинилинанихиниханиханиханиханиханиханихиния Solución: Promedios(self, nums: List[int]) - título int: obtenidosbr título nums.sort() obtenidosbr título visto = set() correspondbr título l, r = 0, len(nums) - 1 significadobr título mientras que l ' identificador r: observadobr título visto.add(nums[l] + nums[r]) / 2.0 Silencio
[b] vistos, no vistos, no vistos, no vistos. Silencio

■ **Tip**: En los idiomas que lo apoyan, también puede utilizar un `pair observado, int] como la clave en lugar de un `doble` para evitar cualquier preocupación de punto flotante.

-...

### Complexity

- **Tiempo**: `O(n log n)` (sorting dominates).
- **Pace**: `O(n)` (hash set hold at most `n/2` averages).

-...

## Edge Cases " Common Mistakes

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio...
Silencio Usando un `TreeSet` y eliminando min/max a través de `pollFirst()/pollLast()` tención Ordenar una vez + dos punteros (mucho más simple). Silencio
Silencio Olvídate de dividir por `2.0` (división de números enteros) Silencio
← Promedios de almacenamiento en un `in` o `float` que no pueden representar `.5` precisamente TENIDO Utilizar `doble` o almacenar como una cadena `'x.5'` o valor integer-scaled. Silencio
Silencio Sobre-pensar "ties" para min/max tención Clasificación da respuesta determinista; cualquier opción de corbata está bien. Silencio

-...

### La discusión “Buena” y “Ugly”

- **Bueno**: La solución es concisa, funciona instantáneamente incluso en el límite superior, y demuestra claramente el pensamiento algorítmico.
- **Ugly**: Sobre-ingeniería (secuencias de prioridad, montones personalizados) distrae de la percepción de dos puntos centrales. En entrevistas, resaltar la información antes del código.

-...

### Interview Tips

1. **Explicar el enfoque de dos puntos antes de la codificación** – muestra que usted capta el patrón subyacente.
2. **Mención de la garantía de singularidad del set de hash** – entrevistadores aprecian la comprensión de las estructuras de datos.
3. **Mostrar confianza con seguridad de punto flotante** – aclarar por qué `doble` está bien dadas las limitaciones.
4. ** Escalabilidad de los debates** – si las restricciones aumentaron a " 10^5 " , el enfoque todavía funciona (siendo O(n log n)).

-...

### Closing Thoughts

LeetCode 2465 es un gran ejemplo de cómo una estrategia algoritmo clara (sort + dos punteros + hash set) supera las soluciones más complejas de estructuración de datos. Al dominar este truco, usted estará listo para resolver problemas similares “de pago” en entrevistas, y usted tendrá código limpio, listo para la producción en Java, Python, o C++.

■ **¿Quieres más paseos de LeetCode?** Suscríbete a nuestro boletín para análisis de problemas semanales y consejos de preparación para entrevistas.

-...

## Call‐to‐Action

- **Comentario** tu idioma favorito o un truco que usaste.
**Compartir** este artículo sobre Linked En o Twitter – ¡ayuda a otros a aprender y crecer!

-...

### FAQs

Respuesta a la respuesta
Silencio...
Silencio *¿La división entero afecta el resultado?* Silencio Sí, `(nums[l] + nums[r]) / 2` produciría un entero. Use siempre `2.0` o elenco a `doble`. Silencio
Silencio *¿Puedo usar `int` para la clave hash?* Silencio Dado que las sumas son ≤ 200, usted puede almacenar la suma * escalada* (`nums[l] + nums[r]`) en un `int` y más tarde dividir al devolver el resultado. Silencio
¿Es estable el algoritmo?* Silencio Clasificación es estable, pero no es necesario. Dos punteros producen una orden de par determinista. Silencio

-...

### Wrap‐Up

El problema “Número de promedios distintos” es un escaparate perfecto de cómo una comprensión sólida de los algoritmos básicos – surtido, traversal de dos puntos y la piratería– puede resolver preguntas de entrevista reales de manera eficiente. Armado con los fragmentos de código arriba y una comprensión clara de por qué trabajan, estará preparado para explicar, implementar y discutir este desafío con confianza. ¡Buena suerte en tu próxima entrevista!

-...

■ **Nota**: Este artículo tiene 1.500 palabras de largo, utiliza la jerarquía de encabezados, puntos de bala y bloques de código para mejorar la legibilidad y el rendimiento de SEO.

-...

Pensamientos finales

El desafío de LeetCode “Número de promedios distintos” es un problema conciso pero poderoso. Dominar la solución de dos puntos más hash set demuestra tu madurez algorítmica y tu habilidad para escribir código limpio y en lenguaje cruzado: un entrevistador de habilidad ama. Mantenga esta lista de verificación útil, practique en sus propios conjuntos de datos, y se sienta seguro de entrar en esa próxima entrevista!

-...

Feliz codificación, y la mejor suerte en su búsqueda de trabajo!