-...
Título: LeetCode 3095. Subarray más corto con OR al menos K I -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 3095 – Subarray con O al menos K I

**Recapto de problemas* *
Dado un conjunto de enteros no negativos `nums` (length ≤ 50, cada `nums[i]` ≤ 50) y un entero `k` (0 ≤ k ■ 64), encontrar la longitud del sub-array contiguo más corto cuya bitwise OR es **≥ k**.
Regrese `-1' si no existe tal sub-array.

Debido a que las limitaciones son pequeñas, funciona una solución **brute‐force** `O(n2)`, pero a los entrevistadores les encanta ver una ventana * deslizante* + * tabla de frecuencia de bits* que escala a `n = 105`. A continuación encontrará el código de producción, idioma-agnóstico (Java, Python, C++) seguido de un post de blog amigable SEO que cubre el *bueno, el malo, y el feo* de la solución.

-...

## 1. Código de producción y lectura

■ *Las tres implementaciones comparten el mismo núcleo algoritmo:*
* una ventana corredera `[izquierda, derecha]` que crece a la derecha,
[0...31] que mantiene seguimiento de cuántos números en la ventana actual fija cada bit,
* un `orValue` dinámico que se recomputa desde la mesa cuando la ventana está enraizada.

#### 1.1 Java

``java
importar java.util*;

Clase Solución {

// Añade x a la ventana actual
vacío privado add(int x, int[] cnt, int[] orVal) {
para (int b = 0; b)
si ((x " (1 " ) 0) {
(++cnt[b] == 1) // primer número con este conjunto de bits
oVal[0] TENIDO= 1 Se realizó b; // establecer el bit en el valor OR
}
}
}

// Elimina x de la ventana actual
anulación privada (int x, int[] cnt, int[] orVal) {
para (int b = 0; b)
si ((x " (1 " ) 0) {
si... 0) // no más números con este bit
orVal[0] &= ~(1 > se hizo b); //
}
}
}

public int minimumSubarrayLength(int[] nums, int k) {
int n = nums.length;
int minLen = Integer.MAX_VALUE;
int[] cnt = nuevo int[32]; // frecuencia de cada bit en la ventana
int[] oVal = {0}; // envuelto int para que podamos mutarlo

para (int left = 0, right = 0; right Identificado n; right+) {}
add(nums[right], cnt, orVal);

mientras (oVal[0] √= k) { // ventana ya es suficientemente grande
minLen = Math.min(minLen, right - left + 1);
remove(nums[left], cnt, orVal);
izquierda++; // encogimiento de la izquierda
}
}

volver minLen == Integer.MAX_VALUE ? -1 : minLen;
}
}
`` `

**Las complejidades* *

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio Ventana deslizante + bit counts  durable `O(n)` Silencio `O(1)` (32-int table)

-...

### 1.2 Python

``python
Solución de clase:
def minimumSubarrayLength(self, nums: List[int], k: int) - título int:
n = len(nums)
min_len = flotante('inf')
cnt = [0] * 32 # tabla de frecuencia
or_val = 0

izquierda = 0
por derecho, val in enumerate(nums):
# expandir la ventana a la derecha
para b en rango(32):
si vale √≠anos b ' 1:
cnt[b] += 1
si cnt[b] == 1:
or_val Silencio= 1

# Contrato mientras el OR satisface la condición
mientras que o_val k y izquierdas = derecha:
min_len = min(min_len, right - left +1)

# Remove nums[left] from window
para b en rango(32):
si nums[left] √Īo b ' 1:
cnt[b] -= 1
si cnt[b] == 0:
or_val &= ~(1 >
izquierda += 1

regreso -1 si min_len == flotante('inf') más min_len
`` `

-...

#### 1.3 C++

``cpp
Clase Solución {
public:
int minimumSubarrayLength(vector seleccionadoint limitada nums, int k) {
const int BITS = 32
vector implicado cnt(BITS, 0);
int orVal = 0;
int minLen = INT_MAX;
int left = 0;

auto añadir = [fr](int x) {
para (int b = 0; b)
si (x " (1 " ) {}
(++cnt[b] == 1)
oVal TENIDO= 1 , se realizó b;
}
}
};

autoextracción = [fr](int x) {
para (int b = 0; b)
si (x " (1 " ) {}
si... 0)
oVal " = 1 " se entiende b);
}
}
};

para (derecho = 0; derecho) {}
add(nums[right]);

mientras (oVal √≥= k) {}
minLen = min(minLen, right - left + 1);
remove(nums[left++]);
}
}

regreso minLen == INT_MAX ? -1 : minLen;
}
};
`` `

-...

## 2. Blog Post – *“El Bien, el Mal y el Ugly of the OR‐Sliding‐Window”*

■ **Seo Focus Keywords* *
■ *shortest sub-array OR LeetCode*, *bitwise OR interview problem*, *array sliding window solution*, *job interview data‐structure*, *bit‐frequency table technique*, *Java Python C++ solutions*, *candidate interview tips*

-...

### Title
**Mastering LeetCode 3095: Cómo encontrar el Sub-Array más corto con OR ≥ k (Java / Python / C++)* *

-...

## Meta Descripción (160 chars)
Desbloquear la solución más rápida a LeetCode 3095 utilizando una ventana deslizante + tabla de frecuencia bit. Java, Python & C++, más explicaciones de entrevista.

-...

#### ## 1down⃣ Por qué los entrevistadores aman este problema

* **Bit-wise reasoning** – Muéstrale que entiende la manipulación de bits, un tema básico de CS.
* **Ventana deslizante** – Muestra que puedes convertir “fuerza bruta” en una solución *O(n)*.
* ** Optimización del espacio** – contador de 32 pulgadas es un clásico *O(1)* truco extra del espacio.
* **Scalability** – El mismo código funciona para `n = 105` y `k = 236`.

Si puede entregar lo anterior en tres idiomas con código limpio y comentado, se destacará a los reclutadores y gerentes de contratación.

-...

#### 2down⃣ El Bien - ¿Por qué Esta aproximación de rocas

TENIDO VALORACIÓN ANTERIOR Por qué importa
Silencio...
Silencio **Linear Time** Silencio `O(n)` incluso para grandes arrays – entrevistadores aman algoritmos que escalan. Silencio
Silencio **O(1) Espacio Extra** Silencio mesa 32-int – no hay memoria dinámica. Silencio
Silencio **Venta de deslizamiento determinista** Silencio Garantiza el sub-array *shortest* se encuentra tan pronto como se cumple la condición. Silencio
Silencio ** Código Idiomático** Silencio Clear `add`/`remove` helpers, making the logic transparent in any language. Silencio
Silencio **Test‐Driven** tención Fácil de probar cada ayudante (`add`, `remove`, `orVal` update). Silencio

■ *Consejo:* En Java, envuelve el valor OR en una matriz de un solo elemento (`int[] oVal = {0}`) para que los métodos de ayuda puedan mutarlo – un truco sutil pero crucial que mantiene la orden de código.

-...

#### 3down⃣ Los malos – saltos comunes

Cómo evitarlo
Silencio...
Silencio **Desbordamiento de cuenta de punto** Silencio Todos los números son ≤ 50 → sólo baja 6 bits utilizados, pero conservamos 32 bits para mantenerse genéricos. Silencio
Silencio **Forgetting to clear bits** Silencio Después de eliminar un número, compruebe si el recuento de bits llega a 0 **antes** despejar el bit OR. Silencio
Silencio **Index mala gestión** Silencio Los límites de las ventanas deslizantes deben ser inclusivos a la izquierda, excluyendo a la derecha en algunos idiomas; mantenga un ojo en la derecha - izquierda + 1`. Silencio
Silencio **Off‐by‐one in the while loop** Silencio El bucle " mientras tanto (oVal "= k) " debe reducirse antes de actualizar "minLen " para capturar la ventana *shortest*. Silencio

-...

#### 4down⃣ El Ugly – Cuando las cosas van mal

1. **Recomputación O desde cero**
*La forma ingenua es recomputar el valor OR por iterating sobre la ventana otra vez. *
Esto da tiempo de `O(n2) ', aceptable para 'n = 50' pero desastroso para grandes insumos.

2. **Using a HashMap of Integers**
*Algunos candidatos crean un 'Mapa realizada' de bit → contar. *
Si bien es correcto, la parte superior de las búsquedas de mapas y boxeo/unboxing pueden ser órdenes de magnitud más lentas que una variedad de primitivos.

3. **Optimización para una pequeña entrada**
*Escribir una compleja ventana deslizante para `n ≤ 50` es demasiado. *
Los entrevistadores aprecian el nivel de complejidad *derecha* – no “demasiado simple” ni “demasiado loco”.

-...

#### 5down⃣ Puntos de conversación de lectura

Respuesta sugerida ante la pregunta
Silencio...
Silencio *¿Por qué tabla de frecuencia parcial en lugar de recomputar O en cada eliminación?* Silencio Porque recomputar O desde cero sería `O(bits)` para cada psiquiatra. La mesa nos permite aclarar trozos en tiempo constante. Silencio
Silencio *¿Podemos hacer mejor que `O(n)`?* Silencio Con estas limitaciones, `O(n)` es óptimo. Para la versión "II", todavía necesita una ventana corredera; `O(n)` se mantiene óptima. Silencio
*¿Qué hay de números negativos?* El problema garantiza números no negativos. Si se permitieran los negativos, tendría que tratar el bit de la señal por separado. Silencio
Silencio *¿Cómo se comporta el algoritmo cuando k es 0?* Silencio El OR de cualquier sub-array no vacío es ≥ 0, por lo que la respuesta es siempre 1 (el sub-array más pequeño). El algoritmo manejará esto naturalmente. Silencio

-...

## 3. SEO‐Optimised Blog Post (Ω 900 palabras)

■ **Headline** – * “How to Nail LeetCode 3095: Shortest Subarray With OR ≥ k – A Complete Java/Python/C++ Guide”*

**Slug** – `leetcode-3095-shortest-subarray-or-at-least-k`

■ **Meta Descripción** – *“Solve LeetCode 3095 con el algoritmo de frecuencia más rápido deslizante + bit-window en Java, Python y C++. Entender los pros y contras, ver código limpio, y asar su próxima entrevista de instrucciones de datos.”*

### 3.1 Introducción

`` `
Si se está preparando para una entrevista de ingeniería de software, LeetCode 3095 es un problema clásico “bit-wise OR” que prueba tanto su pensamiento de bajo nivel como su capacidad de escribir código limpio y escalable. En este post, te guiaré a través de tres soluciones de producción – una base de fuerza bruta O(n2), el enfoque escalable deslizante-ventana + bit-frecuencia, y cómo la misma lógica se traduce en Java, Python y C++. Al final, usted sabrá:
- Lo que hace que el truco de la ventana deslizante sea poderoso,
- Cuando se puede utilizar con seguridad la solución O(n2) más simple,
- Cómo evitar errores sutiles que superan a muchos candidatos.
`` `

### 3.2 Problema Recap (Equipo 100 palabras)

`` `
Dado un array `arr` y un entero `k`, encontrar el submarino contiguo más pequeño cuyo bitwise OR es por lo menos `k`. Todos los números no son negativos, por lo que el bit de signo es irrelevante. La solución ingenua comprueba cada sub-array posible, conduciendo a O(n2). Mostraremos por qué es insuficiente para grandes conjuntos de datos y presentar un algoritmo de tiempo lineal que mantiene constante el uso de la memoria.
`` `

### 3.3 Brute‐Force O(n2) (Ω 150 palabras)

`` `
Si bien este algoritmo es aceptable para la limitación de 50 elementos del problema, da una buena base de “prueba de la salud” y le ayuda a verificar sus soluciones más avanzadas. Aquí hay un pequeño fragmento en Python:

`` `

*(Insert Python brute‐force snippet)*

`` `
La clave es computar OR en la mosca mientras se extiende la ventana, pero cuando se contrae, tiene que volver a computar el OR de nuevo – eso es lo que mata el rendimiento en entradas más grandes.
`` `

### 3.4 The Sliding‐Window + Bit‐Frequency Table (Ω 400 palabras)

■ *Explicar el concepto: la ventana deslizante mantiene un sistema operativo de funcionamiento; la matriz de cuenta bit mantiene la frecuencia; la eliminación es tiempo constante. *

`` `
Comenzamos caminando por el algoritmo en inglés claro:
1. Inicia los punteros izquierdo y derecho al inicio del array.
2. Ampliar el puntero derecho, añadir bits a la tabla de frecuencias y actualizar el quirófano de funcionamiento.
3. Mientras que el funcionamiento OR satisfies `or_val √= k`, actualice la mejor respuesta y se contraiga de la izquierda.
4. Continuar hasta que el puntero derecho llegue al final.

La visión crítica es que nunca recomputamos el valor OR desde cero al eliminar un elemento. En su lugar, decrementamos la frecuencia de cada bit que aparece en el número eliminado y sólo despejamos el bit OR si su cuenta llega a cero. Esto mantiene cada operación O(1), dando un tiempo de funcionamiento total O(n).

A continuación se muestra el código exacto para cada idioma. Observe cómo los ayudantes (`add`/`remove`) mantienen el bucle principal corto y legible. Para Java, el valor OR está envuelto en un array de un elemento para que los métodos de ayuda puedan mutarlo. En Python, utilizamos una comprensión de la lista para mantener la lógica concisa. En C++, empleamos una lambda para mantener el código de ayuda inline.
`` `

*Insert code snippets side-by‐side or use a code‐block per language. *

### 3.5 Casos de borde > Consejos (tome 150 palabras)

`` `
- k == 0: Cualquier sub-array es válido – la respuesta es siempre 1. Su algoritmo devolverá 1 naturalmente.
- k > max_possible_OR: Si k es más grande que el OR de todo el array, la respuesta es -1. El algoritmo sale con gracia con INT_MAX / inf.
- Pequeños arrays: Mientras que una ventana deslizante está sobre-configurada para n <= 50, los reclutadores aprecian ver que escribe una solución óptima de todos modos.
`` `

### 3.6 Preguntas de la entrevista común (convocar 150 palabras)

`` `
P: ¿Por qué guardamos 32 bits aunque los valores de entrada utilizan sólo 6 bits?
R: Guardar 32 bits mantiene la solución genérica y protege contra futuros cambios. También se alinea con el tamaño entero de la mayoría de los idiomas.

P: ¿Y si el array contenía números negativos?
R: Los números negativos introducen el bit de señal. El algoritmo todavía funcionaría si tratamos el signo por separado o convertimos números a representaciones no firmadas.

P: ¿Es seguro utilizar un diccionario para la tabla de frecuencias en Python?
R: Funciona pero presenta sobrecarga. Un array de 32 enteros es más rápido y más eficiente en memoria.
`` `

### 3.7 Takeaway " Call‐to‐Action (Ω 100 palabras)

`` `
LeetCode 3095 es un micro-curso en manipulación de bits, ventanas correderas y diseño de algoritmos agnósticos de lenguaje. Al dominar el truco de la tabla de frecuencias bit, usted será capaz de abordar una gama de problemas de array “OR/AND” con confianza. Utilice los fragmentos de código a continuación para practicar en su máquina local o integrarlos en su repo GitHub para la preparación de entrevistas lista para portafolio.

¿Listo para enfrentar desafíos más poco a poco? Explore mis otros mensajes sobre problemas “Bitwise AND” y “Sub-array XOR”. ¡Feliz codificación!
`` `

### 3.8 Cierre (Aplausos 50 palabras)

`` `
¿Quieres ver la misma lógica en acción? Echa un vistazo a GitHub Gist que lo acompaña con las implementaciones completas Java, Python y C++. Deja un comentario si estás atrapado en un caso de borde particular - vamos a conquistar LeetCode juntos!
`` `

-...

## ## 4down⃣ Publish & Share

1. **Post on Medium/Dev.to** – use las palabras clave en el encabezado y las etiquetas.
2. **Cross‐post to Linked En** – añadir un breve fragmento y enlace al artículo completo.
3. **SEO Check** – Asegurar la densidad de palabras clave es ~1–2%, se llenan las etiquetas meta, y el artículo es al menos 800 palabras.
4. **Engage** – Responder a los comentarios, pedir a los lectores que fork el repo, y ofrecer una sesión de revisión de código privado para algunos comentaristas.

-...

#### 5down⃣ Cómo este Blog te ayuda a conseguir el trabajo

* **Showcase** – Comparte el blog en tu curriculum vitae o portafolio; los reclutadores harán clic.
* **Búsqueda** – Los buscadores de empleo que buscan la solución “LeetCode 3095” aterrizarán en su página.
* **Credibilidad** – Demuestra comprensión profunda a través de múltiples idiomas.
* **Comunidad** – Hacer comentarios sobre Medium o Dev.to puede llevar a las referencias.

-...

## 4. Lista de verificación rápida para su entrevista

1. 🚀 *¿Tiene el código de ventanilla deslizante listo en Java, Python y C++? *
2. 🔍 * ¿Puede explicar `add`/`remove` en menos de 2 minutos? *
3. Recibir *Casos de bordes más bajos: k = 0, k = max(arr), números negativos? *
4. 💬 * Prepare puntos de conversación para las preguntas “por qué”. *

Si marcas todas las cajas, no solo estás resolviendo LeetCode 3095 – lo estás convirtiendo en un escaparate de iniciación profesional.

-...

■ ¡Feliz entrevista!

-...

Eso es – una respuesta totalmente autocontenida que le da código en tres idiomas, una explicación concisa pero profunda, y un poste de blog listo para SEO para atraer a los reclutadores. ¡Buena suerte!