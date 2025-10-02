-...
Título: LeetCode 565. Array Nesting -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 565. Array Nesting – Java / Python / C++ Soluciones + In‐Depth Blog

■ ** Objetivo** – Camina a través de una solución limpia, O(n) a LeetCode 565 "Array Nesting", y mostrarte un artículo **blog** que es **Amigable ** para que puedas conseguir una entrevista tecnológica.

-...

Problema Recap (LeetCode 565)

Se le da una permutación `nums` de longitud `n` (`0 ... n‐1`).
Para cada índice `k`, construir un conjunto

`` `
s[k] = { nums[k], nums[nums[k]], nums[nums[nums[k]]], ... }
`` `

Para cuando se repita un valor.
Devuelve la longitud **maximum** de todos estos conjuntos.

-...

## 2down Key Insight

Porque `nums` es una permutación, siguiendo los índices desde cualquier punto de partida formará un **ciclo**.
Así el problema se reduce a: * encontrar el ciclo más largo en un gráfico dirigido donde cada nodo tiene exactamente un borde saliente. *

Puede detectar ciclos **en lugar** marcando nodos visitados (por ejemplo, fijandolos a un valor centinela).
Esto da **O(n)** tiempo y **O(1)** espacio extra.

-...

## 3down Código de referencia (Java / Python / C++)

A continuación se incluyen implementaciones autocontenidas, listas para pasar.
Los tres siguen la estrategia *en lugar marcado*.

-...

### 3.1 Java

``java
Solución de la clase pública {}
public int arrayNesting(int[] nums) {
int maxLen = 0;
int final MARK = Integer.MAX_VALUE; // sentinel for visited

para (int i = 0; i)
si (nums[i] == MARK) continúan; // ya visitado

int start = i;
int currLen = 0;

// caminar el ciclo, marcando índices visitados
(nums[start]!= MARK) {
int next = nums[start];
nums[start] = MARK; // mark visited
inicio = siguiente;
curr Len++;
}
maxLen = Math.max(maxLen, currLen);
}
volver maxLen;
}
}
`` `

■ ¿Por qué `int start = i`? #
■ El bucle exterior comienza en cada índice; 'comienza' sigue la cadena.
■ Marcando con las garantías de `MARK` nunca revisitamos un nodo.

-...

#### 3.2 Python

``python
Solución de clase:
def arrayNesting(self, nums: List[int] - int:
max_len = 0
MARK = carro('inf') # sentinel for visited

para i en rango(len(nums)):
si nums[i] == MARK:
continuar

curr = i
cnt = 0
mientras que nums[curr]!= MARK:
nxt = nums[curr]
nums[curr] = MARK # mark visited
curr = nxt
cnt += 1

max_len = max(max_len, cnt)

volver max_len
`` `

■ **Tip** - Usando `float('inf')` funciona porque todos los valores de la matriz son ``.

-...

### 3.3 C++

``cpp
Clase Solución {
public:
int arrayNesting(vector fielint círculo nums) {
const int MARK = INT_MAX; // sentinel
int maxLen = 0;

para (int i = 0; i) ++i) {
si (nums[i] == MARK) continúan; // ya visitado

int curr = i;
int cnt = 0;
(nums[curr]!= MARK) {
int nxt = nums[curr];
nums[curr] = MARK; // mark visited
curr = nxt;
++cnt;
}
maxLen = max(maxLen, cnt);
}
volver maxLen;
}
};
`` `

■ ¿Por qué no?
■ Todos los elementos están en `[0, n-1]`, por lo que `INT_MAX` es un marcador seguro.

-...

## 4VIEW⃣ Blog Article – “Array Nesting: The Good, The Bad, and The Ugly”

■ **Seo Target Keywords* *
■ *LeetCode 565 Array Nesting*, *Solución de anidación de rayos*, *Java Python C++*, *Preguntas de entrevista de LeetCode*, *explicación de anidación de radio*, *detección de ciclos de gráficos*,*

-...

#### 4.1 Introducción

■ *LeetCode 565 – Array Nesting* es un rompecabezas aparentemente sencillo que te enseña mucho acerca de **graph traversal**, **cycle detection**, y **in-place algoritmos**. En este artículo, caminaré a través del problema, la solución más limpia, las trampas (“bad”) y los casos de borde menos obvios (“muy”). Al final, estarás listo para llegar a esta pregunta en una entrevista.

-...

### 4.2 Declaración de problemas (reescrito)

■ Se le da un array entero `nums` de longitud `n` donde cada valor es un entero único en `[0, n-1]`.
■ Para cualquier índice inicial `k`, definir una secuencia: `nums[k]`, `nums[nums[k]]`, `nums[nums[nums[k]]], ...
■ Para antes, repetirías un valor.
■ Devuelve la longitud máxima entre todas estas secuencias.

■ *Examples*

Silencios en la vida
Silencio------------------------------
Silencio [5,4,0,3,1,6,2] Silencio 4 Silencio Un set más largo: `{5,6,2,0}` Silencio
Silencio [0,1,2] Silencio 1 Silencio Cada elemento forma un self-loop. Silencio

-...

#### 4.3 El “Bien”: In‐ Lugar Ciclo Contando

1. **Observación** – La matriz es una permutación → cada nodo tiene fuera de acuerdo 1 → el gráfico es una colección de ciclos descomunales.
2. ** Objetivo** – Encuentra el ciclo más largo.
3. **Metodoxo** – Camina de cada nodo no visto, marcando nodos visitados con un centinela (INT_MAX` / `float('inf')`).
4. *La complejidad*
*Tiempo*: `O(n)` – cada elemento visitado al máximo una vez.
*Pace*: `O(1)` – sólo algunas variables de entero (sin contenedor extra).

■ Este enfoque es *el estándar de oro* para entrevistas: utiliza memoria mínima extra y demuestra una comprensión profunda de los ciclos de gráficos.

-...

### 4.4 El "Bad": Naïve HashSet o Recursion

Por qué es malo
Silencio------------
Silencio **HashSet** – Para cada `k` utilice un `HashSet` para registrar los valores visitados. Silencio Extra `O(n)` espacio por iteración; total `O(n^2)` caso peor si se aplica incorrectamente. Silencio
Silencio **Recursivo DFS** – Seguir Recursivamente `nums` hasta una repetición. La profundidad de las pilas puede llegar a " n " ; riesgo de desbordamiento de las pilas para grandes entradas ( " n ≤ 105 " ). Silencio

■ Incluso si estos pasan en LeetCode, son *unidiomatic* para entrevistadores que buscan soluciones eficientes.

-...

### 4.5 The “Ugly”: Edge Cases ' Subtleties

Silencioso Temas anteriores Explicación
Silencio------------------------
Silencioso **Colisión del santuario** – Usando un valor que podría aparecer en `nums`. TEN En este problema todos los valores `traducidos n`, por lo que el uso `INT_MAX` es seguro. Silencio
tención **Large `n`** – Sobreflujo en profundidad de recursión o marcación. TENIDO A los bucles iterativos. Silencio
tención **Non-permutation input** – LeetCode garantiza una permutación, pero si fueras a generalizar, tendrías que manejar valores repetidos o números perdidos. Silencio Use un array " visualizado " o hashset para guardar. Silencio

■ Manejar estas sutilezas muestra madurez y atención al detalle.

-...

### 4.6 Code Walk‐Through (Java Ejemplo)

``java
para (int i = 0; i)
si (nums[i] == MARK) continúan; // ya visitado

int curr = i;
int cnt = 0;
(nums[curr]!= MARK) {
int next = nums[curr];
nums[curr] = MARK; // mark as visited
curr = siguiente;
cnt++;
}
maxLen = Math.max(maxLen, cnt);
}
`` `

*Cada bucle sigue un ciclo distinto, nunca revisitando ningún nodo porque inmediatamente lo sobreescribimos con el centinela. *

-...

### 4.7 Consejos de optimización

TENIDO TERRITORIO ANTERIOR
Silencio...
Silencioso **Use `int` sentinel** – `INT_MAX` o `-1` Silencio Evita asignar una gran matriz auxiliar. Silencio
Silencio **Iterate en el lugar** – No crea nuevas listas Silencio mantiene la huella de memoria mínima. Silencio
Silencio **Perfil** – Para arrays muy grandes, compruebe que la actualización centinela está inlineda por el compilador JVM/C++. ← Elimina la cabeza oculta. Silencio

-...

### 4.8 Preguntas frecuentes (FAQ)

Respuesta a la respuesta
Silencio...
Silencio *¿Puedo usar un HashSet para marcar los nodos visitados?* Silencio Sí, pero cuesta `O(n)` espacio extra. Preferir el centinela en el lugar. Silencio
Silencio *¿El centinela alterará la entrada para llamadas posteriores?* Silencio En LeetCode, cada caso de prueba está aislado. Para proyectos reales, copie el array primero. Silencio
*¿Por qué no usar Tortoise‐Hare de Floyd?* Encuentra un ciclo que comienza en un nodo específico, pero todavía necesitas explorar todos los nodos. La marcación en lugar es más simple. Silencio

-...

#### 4.9 Conclusiones

■ El problema LeetCode 565 “Array Nesting” es una ilustración clásica de la detección del ciclo ** en un gráfico funcional.
■ Al marcar los nodos visitados *en su lugar*, logramos **O(n) tiempo** y **O(1) espacio**, que es la solución más amigable para las entrevistas.
■ Evite los enfoques ingenuos HashSet o recursivos; son “malos” para el rendimiento y la seguridad de pila.
■ Por último, recuerde los casos de borde (coliciones de frasco, grandes entradas) – manejarlos impresionará a los gerentes de contratación.

■ **Siguientes pasos**
■ 1. Practicar el mismo patrón en problemas como “Número de Islas” o “Cíclo de Listas enlazadas”.
■ 2. Comparte tu solución en GitHub y escribe un blog corto (como éste) para mostrar tu proceso de pensamiento.
■ 3. Prepárate para explicar el enfoque en un campo de entrevista de 5 minutos.

¡Feliz codificación!

-...

## 5down Referencia rápida – Search‐Engine Friendly Meta

Silencio en el campo
Silencio...
Silencio **Título** Silencioso Array Nesting – LeetCode 565 Solución en Java, Python, C++
Silencio **Descripción** Silencio Aprende el algoritmo óptimo en el lugar para LeetCode 565 “Array Nesting”. Full Java, Python, y C++ implementaciones + entrada de blog lista para entrevistas. Silencio
Silencio **Keywords** Silencio LeetCode 565, nido de matriz, detección de ciclos de gráficos, solución Java, solución Python, solución C++, codificación de entrevistas, algoritmo O(n) y problemas óptimos de LeetCode Silencio
TEN **URL Slug** Silencioso array-nesting-leetcode-565-solution TEN

■ Incluir estas meta etiquetas ayudará a los reclutadores a buscar la solución "Array Nesting" encontrar su contenido.

-...

■ *¡Buena suerte en tus entrevistas de codificación!* *