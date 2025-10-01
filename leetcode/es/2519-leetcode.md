-...
Título: LeetCode 2519. Cuenta el número de índices K-Big -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Mastering LeetCode 2519 – “Cuente el número de índices K‐Big”

■ ¿Por qué leer esto? * *
* Obtener una solución clara y lista para la producción en **Java, Python & C+**.
* Entender el *bueno* (intuición), *bad* (pocas comunes) y *ugly* (cascos de caso entero).
• Aprende dos técnicas poderosas: *dos priority‐queues* (O(n log k)) y un *Fenwick tree* (O(n log M)).
* Pulsa tu estilo de entrevista: estarás listo para explicar, codificar y optimizar en el lugar.

■ **SEO-keywords** – *LeetCode 2519, k-big indices, entrevista coding question, Java priority queue, Python heap, C++ priority_queue, Árbol Fenwick, entrevista algorítmica, estructuras de datos, gran notación O, soluciones de entrevistas de codificación. *

-...

## 1. Declaración de problemas (parafrasada)

■ **Input**
"nums " – 0‐indexed integer array (`1 ≤ len(nums) ≤ 105`)
" k " - entero positivo ( " 1 ≤ k ≤ len(nums) "

■ **Definición**
* Índice " i " is **k‐big**
* Hay por lo menos " índices distintos " idx1 " i " con `nums[idx1] " nums[i] " ;
* hay por lo menos `k` distintos índices `idx2 i` con `nums[idx2] ' se hicieron nums[i].

■ **Task**
■ Devuelve el número de índices k-big.

■ *Ejemplo*
" texto
> nums = [2,3,6,5,2,3], k = 2 → 2
" `

-...

## 2. Intuición " Observaciones clave

TENCIÓN ANTERIOR Por qué importa
Silencio...
Silencio ** lado izquierdo** – Necesitamos saber *cuántas cifras más pequeñas existen a la izquierda*. Si conocemos el *k‐th menor* de la izquierda, podemos decidir inmediatamente. Silencio
TEN **A la derecha** – Simétrico: necesitamos el *k‐th más pequeño* a la derecha. Silencio
Silencio ** Estructura monotónica** – Por cada índice sólo necesitamos *el tamaño del conjunto “smallest k”*; no nos importan sus valores exactos. Silencio
Silencio **Dos pasos de escaneo lineal** – Computar la información del lado izquierdo primero, luego barrer de derecha a izquierda para verificar el lado derecho y el lado izquierdo simultáneamente. Silencio
← **Time vs Space trade‐off** – `O(n log k)` con colas prioritarias es lo suficientemente simple y rápido; el árbol de Fenwick da `O(n log M)` (M = valor máximo) y utiliza sólo arrays. Silencio

-...

## 3. El enfoque “bien” – Dos-Prioridad-Queues (O(n log k)))

### 3.1 Pasos de Algoritmo

1. *Paso de izquierda*
*Mantenga un máximo de tamaño `k`* (es decir, cola prioritaria en orden descendente).
Por cada `i' de izquierda a derecha:
* Si el tamaño del montón es `k` **y** el elemento más grande en el montón (`top ' ) es ` nums[i]`, entonces sabemos que hay por lo menos `k ' elementos más pequeños a la izquierda → marca `izquierda Bien [i] = verdadero.
* Empuje `nums[i] en el montón. Si el tamaño de la pila supera `k ' , pop el máximo (que es el más grande entre el más pequeño `k ' ).

2. **Paso derecho** – Haga lo mismo de derecha a izquierda:
* Use un nuevo max-heap de tamaño `k`.
* Cuando el montón tiene elementos de `k ' y su `top ' significa `nums[i]`, entonces * lado derecho* es bueno.
* Combinar con la anterior `leftGood[i]`; si ambas verdadera → respuesta de aumento.
* Empuje `nums[i]` y pop if size ' k`.

3. **Retorno** la respuesta acumulada.

#### 3.2 Por qué funciona

*El montón siempre contiene los valores más pequeños vistos hasta ahora. *
Si el máximo del montón ( " alto " ) es " nums[i] " , eso significa que todo elemento en el montón es " nums[i] " , así que tenemos por lo menos `k ' tales elementos.
De lo contrario, todavía no tenemos elementos más pequeños.

#### 3.3 Complexity

Silencio Silencio Silencio Silencio
Silencio----------------
TENIDO Cada empuje/pop es `O(log k)` Silencio `O(n log k)` para heap + `O(n)` para `izquierda Good` array ←
Silencio Total Silencio **`O(n log k)`** Silencio **`O(n + k)`** (dominant `O(n)` due to boolean array) Silencio

Porque `k ≤ n ≤ 105`, esto satisface fácilmente las limitaciones.

-...

## 4. Los casos de “Bad” – errores comunes " Edge

Silencioso tóxico tóxico
Silencio------------
Silencio **Using a min‐heap** Silencio Condicion debe ser `heap.size() == k ' heap.peek() será el *smallest* → incorrecto. Use un **max-heap** (orden reversa). Silencio
Silencio **Pulsando después del cheque** Silencio Si usted empuja primero, usted podría incluir el elemento actual en el conteo. tención Check **before** inserting. Silencio
Silencio **Off‐by-one cuando se retira del lado derecho** Silencio Para el índice `i`, no debemos considerar 'nums[i] ' en el lado derecho. Silencio Inicio derecho pasar con un montón *vacío* y *primero* presionar el valor actual después del cheque. Silencio
tención **Ignorando los valores duplicados** Silencio condición requiere ** números estrictamente más pequeños**.
Silencio **No aclarar el montón entre pases** Silencio Paso izquierdo todavía puede tener elementos en el paso derecho. Silencio Reinicializar el montón. Silencio

-...

## 5. La Alternativa “Ugly” – Fenwick Tree (Binary Indexed Tree)

Si prefiere soluciones * basadas en rayos*, un árbol de Fenwick que cuenta ocurrencias de valores funciona bien.
Idea clave: mantener dos árboles Fenwick de frecuencia – uno para el lado izquierdo (`izquierda') y otro para el lado derecho (`derecha derechaTree`).
Durante la exploración:

1. Inicialmente, todos los elementos pertenecen a `rightTree`.
2. Para cada índice " i " (comenzando desde " k " a " n-k-1 " para garantizar suficientes elementos en ambos lados):
* Remove `nums[i]` de derecho Árbol.
* Query `leftTree.prefixSum(nums[i]-1)` and `rightTree.prefixSum(nums[i]-1)` to know how many *strictly smaller* numbers exist on each side.
* Si ambos cuentan ≥ `k`, respuesta de aumento.
* Add `nums[i]` to `left Árbol.

Las consultas/actualizaciones de los árboles de Fenwick son `O(log M)` donde `M` es el valor máximo en `nums` (≤ 105 después de la compresión).
El espacio es `O(M)` y no se requiere montón.

■ **¿Cuándo usar? #
■ * Necesitas manejar muy grande `k` cerca de `n`* o *quieres un factor logístico determinista independiente de `k`*.
■ *Estás cómodo con una indexación basada en 1 y sumas prefijo. *

-...

## 6. Código de muestra – Los tres idiomas

■ Cada snippet compila en su propia presentación de LeetCode.
■ Los nombres de clase y las firmas de método coinciden con la plantilla oficial del problema.

-...

### 6.1 Java

``java
importa java.util. Prioridad Queue;
importa java.util. Colecciones;

Clase Solución {
int kBigIndices(int[] nums, int k) {
int n = nums.length;
boolean[] leftGood = new boolean[n];

--------- Paso de la izquierda...
Prioridad Búsquedas realizadasInteger confianza leftHeap = nueva PrioridadQueue Curso(Collections.reverseOrder());
para (int i = 0; i)
si (izquierdaHeap.size() == k " izquierdoHeap.peek() {}
leftGood[i] = true;
}
leftHeap.offer(nums[i]);
si (leftHeap.size() √ k) leftHeap.poll();
}

--------- Pase derecho...
respuesta int = 0;
Prioridad Búsquedas realizadasInteger correctamenteHeap = nueva PrioridadPregunta indicada(Collections.reverseOrder());
para (int i = n - 1; i 0; i--) {
si (derechaHeap.size() == k " rectoHeap.peek()  nu nums[i]) {}
si (izquierda Buena) respuesta++;
}
rightHeap.offer(nums[i]);
(rightHeap.size() √ k) rightHeap.poll();
}

respuesta de retorno;
}
}
`` `

-...

### 6.2 Python

``python
importación heapq
de la importación Lista

Solución de clase:
def kBigIndices(self, nums: List[int], k: int) - título int:
n = len(nums)
[False] * n

--- Izquierda a la derecha...
left_heap = [] # Python's heapq is a min‐heap → store negatives to get a max‐heap
para i, val en enumerate(nums):
si len(left_heap) == k and -left_heap[0]  Detectado val:
left_good[i] = True
heapq.heappush(left_heap, -val)
si len(left_heap)
heapq.heappop(left_heap)

--- Derecho a la izquierda...
right_heap =
ans = 0
para i en rango(n - 1, -1, -1):
si len(right_heap) == k y -right_heap[0] se hicieron nums[i]:
si izquierda_good[i]:
ans += 1
heapq.heappush(right_heap, -nums[i])
si len(right_heap)
heapq.heappop(right_heap)

Retorno
`` `

-...

### 6.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int kBigIndices(vector asignadoint limitada nums, int k) {
int n = nums.size();
vector identificador confianza izquierdaGood(n, 0);

--- Paso izquierdo...
priority_queue seleccionaint Salto; // max‐heap por defecto
para (int i = 0; i) {}
si (izquierdaHeap.size() == k " izquierdoHeap.top() {}
leftGood[i] = 1;
}
leftHeap.push (nums[i]);
si (leftHeap.size() √ k) leftHeap.pop();
}

--- Paso derecho...
prioridad_queue hicisteint derecho Salto;
int ans = 0;
para (int i = n - 1; i 0; --i) {
si (derechaHeap.size() == k " pulsa rightHeap.top() {}
si (izquierda Buena) ++ans;
}
rightHeap.push (nums[i]);
(rightHeap.size() √ k) rightHeap.pop();
}

devolver los ans;
}
};
`` `

■ **Nota**: Los tres francotiradores se ejecutan en **O(n log k)** tiempo y utilizan sólo una matriz booleana + dos montones.

-...

## 6. 6‐Step “Entreview‐Ready” Lista de verificación

Silencio Qué decir / hacer en la vida
Silencio...
Silencio 1. Clarify “strictamente más pequeño” vs “≤” _ “Asegúrese de contar con números estrictamente más pequeños”. Silencio
Silencio 2. Elija la estructura de datos Silencio "Usaré dos saltos máximos porque sólo necesitamos el k más pequeño de cada lado." Silencio
Silencio 3. Escribe el pase izquierdo Silencioso “Primero cheque, luego insertar; de esa manera el elemento actual no se cuenta.” Silencio
Silencio 4. Pase derecho TENIDO “La misma lógica, pero necesitamos evitar contar el elemento actual en el lado derecho”. Silencio
Silencio 5. Verificar la condición combinada Silencioso “Tanto a la izquierda como a la derecha debe ser verdad → hemos encontrado un índice k‐big.” Silencio
Silencio 6. Complejidad TENIDO “O(n log k) tiempo, espacio O(n) – pasa fácilmente 105 restricciones.” Silencio
Silencio 7. Casos de borde TENIDO “Valores duplicados, fuera por uno, aclarando el montón, usando el máximo salto.” Silencio

-...

## 7. Consejos de prueba

Silencio Test TENIDO Resultado esperado
Silencio...
TENIDO `nums = [1,2,3,4,5], k = 1` TENIDO 4 TENIDO Cada índice excepto el primero tiene por lo menos uno más pequeño en la izquierda ' derecha. Silencio
tención `nums = [5,4,3,2,1], k = 2` Silencio 0 Silencio Ningún índice tiene valores *smaller* en ambos lados. Silencio
TENIDO `nums = [1,1,1,1,1], k = 1` TENIDO 0 ANTE No hay valores estrictamente menores. Silencio
TENIDO `nums = [105, 1, 1, ..., 1], k = 1` TENIDO 1 TENIDO El primer elemento es k‐big porque hay muchos más pequeños a la derecha. Silencio
tención Random large array + random `k` Silencio Pasas 2-second limit  durable Use `random.randint(1, 105)` y verificar con fuerza bruta para pequeña `n`. Silencio

-...

## 8. Pensamientos finales

* **Two-priority-queues**: más rápido al código, elegante y satisface plenamente las limitaciones del problema.
* **Fenwick árbol**: genial si necesitas evitar saltar sobre la cabeza o si ya estás familiarizado con los TBIs.
* Mantenga siempre *strictamente más pequeño* y *off-by-one* matones en mente – son las gremlins de entrevista habitual.

Siéntase confiado: ahora puede abordar LeetCode 2519 en **Java, Python, y C++** mientras explica el *por qué* y *cómo* a un gerente de contratación.

-...

**Feliz codificación " buena suerte en su próxima entrevista! * *