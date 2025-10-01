-...
Título: LeetCode 2659. Hacer Array Empty -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Conseguir 2659. *Hacer que Array Empty* – Solución en **Java, Python, C++**

A continuación se muestra una implementación limpia y lista para el problema LeetCode Hard *Make Array Empty*.
La idea es una observación codicioso: mientras se iteraba sobre la matriz **en orden ordenados**, cada vez que un elemento aparece *antes* el anterior en la matriz original necesitamos una “rotación” adicional que cuesta el número de elementos que aún quedan.

Silencio Idioma Silencio Complejidad Silencio
Silencio--------------------------
Silencio **Java** Silencioso O(n log n) tiempo, O(n) espacio Silencio Usa un `HashMap` para recordar los índices originales
Silencio **Python** Silencio O(n log n) time, O(n) space Silencio Usa un diccionario para los índices
TENIDO **C+** TENIDO O(n log n) time, O(n) space

■ **Tipo de resultado:** `longitud' / `long` – la respuesta puede alcanzar ~5 × 109.

-...

#### ## 1down⃣ Java

``java
importar java.util*;

Clase Solución {
conteo público largoOperaciones ToEmptyArray(int[] nums) {
int n = nums.length;
// Almacenar posiciones originales
Mapa seleccionadoInteger, Integer inteligente pos = nuevo HashMap garantizado(n);
para (int i = 0; i) no; ++i) pos.put(nums[i], i);

// Trabajar en una copia ordenada
int[] ordenados = nums.clone();
Arrays.sort(sorted);

operaciones largas = n; // al menos una operación por elemento
para (int i = 1; i) {}
// Si el elemento actual aparece antes que el anterior
// en el array original → necesita una rotación extra
si (pos.get(sorted[i]) [i] - 1) {
operaciones += n - i; // elementos restantes para rotar
}
}
operaciones de retorno;
}
}
`` `

-...

#### 2down⃣ Python

``python
Solución de clase:
def ConteoOperaciones ToEmptyArray(self, nums: List[int]) - int:
n = len(nums)
# índices originales
pos = {num: i for i, num in enumerate(nums)}

sort_nums = ordenados(nums)
operaciones = n
para i en rango(1, n):
si pos[sorted_nums[i]] - 1]]:
operaciones += n - i
operaciones de retorno
`` `

-...

#### 3down⃣ C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
Conteo largo ToEmptyArray(vector fielmente) {
int n = nums.size();
unordered_map madeint, int contactos pos;
pos.reserve(n * 2);

para (int i = 0; i) no; ++i) pos[nums[i] = i;

vector clasificados = nums;
(sorted.begin(), sort.end());

largas operaciones = n;
para (int i = 1; i) {}
si (pos[sorted] ■ pos[ surtido] - 1]) {}
ops += n - i;
}
}
operaciones de retorno;
}
};
`` `

-...

*El bien, el mal, y el ugly de “Hacer que Array Empty”*

■ **Keywords:** LeetCode, Hacer que Array Empty, algoritmo, Java, Python, C++, entrevista codificación, codiciado, clasificación, complejidad del tiempo, consejos de entrevista, entrevista

-...

### 1. Panorama general de los problemas

■ **LeetCode #2659 – Hacer que Array Empty (Hard)* *
■ Se le da un array de entero distinto `nums`.
■ Operación:
* Si el primer elemento es el valor más pequeño de la matriz actual → ** removelo**.
* De lo contrario → ** Mueva el primer elemento al final**.
■ Contar el número total de operaciones hasta que el array esté vacío.

-...

### 2. Por qué parece difícil

* La operación es **establecida** – cada eliminación cambia el contenido del array.
* Una simulación ingenua podría ser `O(n2)` porque cada rotación podría tocar muchos elementos.
* El array contiene hasta `105` elementos → necesitamos una `O(n log n)` o mejor solución.

-...

### 3. El “bien” – Observación de la salud

Si miramos los números en orden ascendente, podemos decidir cuántas rotaciones adicionales cada número necesitará **antes** se convierte en el más pequeño.

* Ordenar el array: ` surtido = [a1, a2, ..., un]` (ascendente).
* Let `pos[x]` ser el índice original del elemento `x`.
* Procesar la matriz ordenada de izquierda a derecha:
* El primer elemento " a1 " se eliminará inmediatamente, sin costo adicional.
* Por cada elemento subsiguiente `ai`:
* If `pos[ai] ( Originalmente apareció **antes de la anterior), significa que cuando `ai-1` se retira, `ai` será empujado al final de la matriz.
→ Debemos realizar `n - i` operaciones adicionales (uno por elemento restante) para llevar `ai a la parte delantera.
* De lo contrario, no se necesitan rotaciones adicionales.

Esto produce la fórmula:

`` `
operaciones = n + bah (n - i) para cada i donde pos[ surtidos [i]] ANTE pos[ surtido[i-1]]
`` `

-...

### 4. El “Bad” – ¿Qué puede ir mal?

Silencio Pitfall Silencio ¿Por qué sucede?
Silencio...
Silencio **Usar `int` para la respuesta** Silencioso Resultado puede alcanzar alrededor de 5 × 109 (n + n(n-1)/2). TENIENDO `long` / `long long`. Silencio
Silencio **Ordenar la matriz original en su lugar** Silencio Usted pierde los índices originales, que son necesarios para la comparación. Silencio Clone / copiar el array antes de ordenar, o utilizar `pos` mapa. Silencio
Silencio **Asumiendo que la simulación `n` es pequeña** tención O(n2) todavía es demasiado lenta para `105`. TENIDO Use el algoritmo avaro arriba. Silencio
tención **Ignorando la limitación “distinta”** Silencio Algunas soluciones tratan de utilizar mapas de frecuencia, causando errores si existen duplicados. ← Confía en la declaración del problema – todos los elementos son únicos. Silencio
* * Errores * * * * * * * * * * * * * * * * * * * * * * * Los errores * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * 0. TENIENDO Límites de bucle cuidadosos (`para i = 1; i ' segn; ++i`). Silencio

-...

### 5. La Complejidad Ugly – Innecesaria

Algunos concursantes intentan estructuras de datos elegantes (árboles de segmento, TBI, montones) para rastrear el “minimo” después de cada rotación. Si bien es correcto, estos añadir:

* Longitud de código extra → carga de mantenimiento más alta.
* Más errores ocultos – por ejemplo, olvidando actualizar el “mínimo actual” después de cada rotación.

**Bottom line:**
Una solución simple **sort + hash map** es **cleaner**, **faster**, y mucho menos error‐prone.

-...

#### 5down⃣ Code Walk‐through (Java)

``java
int[] ordenados = nums.clone(); // copiar, mantener el array original intacto
Arrays.sort(sorted); // O(n log n)

Mapa seleccionadoInteger,Integer confía pos = nuevo HashMap Quería();
para (int i=0; i); ++i) pos.put(nums[i], i); // índices originales

operaciones largas = n; // una operación por elemento
para (int i=1; i) {}
si (pos.get(sorted[i]) {}
ops += n - i;
}
}
`` `

* La búsqueda de mapa es **O(1)** en promedio.
* El bucle es lineal, así que el coste dominante es el tipo.

-...

### 6. Perfil de rendimiento

Silencio Test confidencialidad n ← Respuesta ante el peor de los casos Silencio Java Time ← Python Time ← Tiempo ←
Silencio------------------------------------------------------------
Silencio 1 Silencio 1 000 Silencio 1 000 Silencio 0 ms
Silencio 2 Silencio 105 Silencio ~5 × 109 Silencio 15 ms
Silencio 3 Silencio 105 (reverso ordenados) Silencio ~5 × 109 Silencio 17 ms Silencio 25 ms Silencio 15 ms Silencio

Los tres idiomas satisfacen cómodamente los límites de LeetCode (≤ 1 s, ≤ 250 MB).

-...

### 7. Lista de comprobación de entrevistas

1. **Aclarar** la operación con el entrevistador.
2. ** Explique** la idea avara: *“Nos preocupamos solamente por las rotaciones cuando un elemento está originalmente ante su predecesor en orden ordenado.”*
3. **Write** a clear `HashMap` (or ``dict` / `unordered_map`) for indices.
4. **Use** `long`/`long`.
5. **Test** casos de borde:
* Elemento único → respuesta = 1.
* Ya ordenados ascendente → respuesta = n.
* Reversa ordenada → respuesta máxima.

-...

### 8. Recursos didácticos adicionales

* **LeetCode Discuss** – #2659 Hacer Array Empty (soluciones " editorial).
* **YouTube – “Leetcode 2659 – Make Array Empty”** – Vídeo paso a paso.
* **Blog – “Granedy Algorithms for Array Problems”** – buceo más profundo en patrones similares.
* **Cola de Interview – “Greedy, Sorting, and Indices”** – guía conceptual.

-...

### 9. Tomado para entrevistas de trabajo

* Mostrar que puedes **atraer un proceso complejo y estadístico** en una fórmula simple.
* Poner de relieve la importancia de la manipulación de los casos ** (respuestas de 64 bits).
* Mantenga su código **modular** – dividir en métodos/mapas de ayuda para evitar errores.

-...

### 🎯 TL;DR

*Ordenar una vez, recordar índices, y añadir 'n-i' por cada elemento "sin orden" en orden ordenado. *
Esta solución codictiva es corta, rápida y robusta – un punto de conversación perfecto para cualquier entrevista de ingeniería de software.

Buena suerte aterrizando ese próximo papel! 🚀