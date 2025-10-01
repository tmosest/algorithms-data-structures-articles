-...
Título: LeetCode 1775. Arrays de Sum iguales con número mínimo de operaciones -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Equal‐Sum Arrays with Minimum Number of Operations
**Una solución de entrevista completa (Java / Python / C+++) + un blog “Good‐Bad‐Ugly”* *

■ **SEO Tags** – Leetcode, Equal Sum Arrays, Java, Python, C+++, algoritmo codicioso, entrevista pregunta, entrevista de algoritmos, estructuras de datos, entrevista de trabajo, entrevista de codificación, instrucciones de datos, preparación de entrevistas

-...

## 1. Recaptación de problemas

■ **Leetcode #1775 – Equal Sum Arrays With Minimum Number of Operations* *
■ **Dificultad:**

Se le dan dos arrays enteros `nums1` y `nums2`.
Cada elemento está en el rango `[1, 6]`. En una operación se puede cambiar *cualquier elemento* en *cualquier matriz* a cualquier valor de `1` a `6`.
Devolver el número **minimo** de operaciones necesarias para que la suma de `nums1` sea igual a la suma de `nums2`.
Si es imposible, devuelve `-1`.

TEN SON SON SON SON SON SON SON SON SON 
Silencio----------------------------------------------------
TENIDO 1 TENIDO `nums1 = [1,2,3,4,5,6] ' , `nums2 = [1,1,2,2,2,2] ' TENIDO `3` TENIDO Cambio `nums2[0] → 6`, `nums1[5] → 1`, `nums1[2] → 2`.
TENIDO 2 TENIDO `nums1 = [1,1,1,1,1,1,1]`, `nums2 = [6] TENIDO `-1` Silencio Imposible – no podemos disminuir la suma de `nums1` suficiente o aumentar `nums2` suficiente. Silencio
TENIDO 3 TENIDO `nums1 = [6,6] ' , `nums2 = [1] ' Silencio Reducir dos `6`s a `2` y aumentar `1` a `4`. Silencio

**Constraints* *

- 1 ≤ nums1.length, nums2.length ≤ 105 `
- `1 ≤ nums1[i], nums2[i] ≤ 6

El problema se ve engañosamente simple – sólo tienes que pensar en *cuantos* cambios, no *que* elementos. Esta observación conduce a una solución codictiva muy rápida.

-...

## 2. The Core Idea

1. **Computa las sumas actuales. #
" , " , " , " .
2. **Si las sumas ya son iguales → 0 operaciones. #
3. **Si la suma máxima posible de una matriz es aún más pequeña que la suma mínima posible del otro → imposible (`-1`). * *
(e.g. `len(nums1)*6 ' se entiende len(nums2)*1 ' o vice-versa.)
4. **De lo contrario, que el arreglo con la suma más grande sea `grande', el otro sea `pequeño'.**
*disminuir* valores en `grande` ** o** * aumentar* valores en `pequeña ' .
La diferencia `diff = sumBig - sumSmall` es la cantidad total que debemos cerrar.

5. **Contar el “poder” de cada elemento** – cuánto puede contribuir a cerrar la diferencia en una operación:
- Para un elemento `x` en `grande`, podemos **disminuirlo a `1`, por lo que la disminución máxima es `x-1`.
- Para un elemento `y' en `pequeña', podemos **aumentar** a `6`, por lo que el aumento máximo es `6-y`.
Guarde estos en un array de frecuencias `freq[1..5]` Donde `freq[d]` = cuántas operaciones pueden cerrar **exactamente** `d` unidades de diferencia.

6. **Greedy:** Utilice los mayores cambios posibles primero (5, 4, 3, 2, 1).
Por cada `d' de 5 abajo a 1:
`` `
use = min( freq[d], ceil(diff / d) )
operaciones += uso
diff -= use * d
si se apagan
`` `

Debido a que cada operación elimina la mayor diferencia posible, el enfoque codicioso es óptimo.

El algoritmo se ejecuta en **O(n)** tiempo (sólo atravesar ambos arrays una vez) y utiliza **O(1)** espacio extra (`freq[6]).

-...

## 3. Full Implementations

A continuación encontrará código limpio y bien comunicado para **Java, Python y C+**.
Los tres siguen el mismo esquema algorítmico.

## 3.1 Solución Java (O(n))

``java
// 1775. Arrayos de Sum iguales con número mínimo de operaciones
// Java 17, solución O(n) – matriz de frecuencia + codicioso
Clase Solución {
public int minOperations(int[] nums1, int[] nums2) {
int sum1 = 0, sum2 = 0;
(int x : nums1) sum1 += x;
(int x : nums2) sum2 += x;

// 1. sumas ya iguales
si (sum1 == sum2) devuelve 0;

// 2. Caso imposible
int len1 = nums1.length, len2 = nums2.length;
si (len1 * 6 " ) len2 Silencioso len2 * 6 = len1) retorno -1;

// 3. asegúrate de la suma1 > sum2, de otro modo cambiar roles
si (sumo) 1
devolver minOperaciones(nums2, nums1);
}

int diff = sum1 - sum2; // diferencia positiva necesitamos cerrar
int[] freq = nuevo int[6]; // freq[1..5] – posible tamaño del cambio

// 4. recoger el poder de cada elemento
para (int x : nums1) { // big array
freq[x - 1]++; // disminución x - título 1
}
para (int y : nums2) { // pequeño array
freq[6 - y]+; // increase y - 6
}

// 5. avaricioso del mayor cambio posible
int ops = 0;
para (int d = 5; d 1; d...) {
si (diff <= 0) se rompe;
int usable = diff / d; // cuántos d‐ops completos cabe
si (diff % d!= 0) usable++; // +1 si permanece
int take = Math.min (freq[d], usable);
ops += take;
diff -= take * d;
}
operaciones de retorno;
}
}
`` `

■ *Puntos clave*
* El array de frecuencias tiene sólo 5 entradas (index 0 sin usar).
* No hay estructuras extra de datos como montones – esto mantiene el uso de la memoria insignificante.

-...

### 3.2 Python (Python 3.10, O(n) solution)

``python
# 1775. Arrayos de la misma graduación con número mínimo de operaciones
# Python 3.10 – O(n) solución codictiva

def minOperations(nums1: list[int], nums2: list[int] int:
sum1, sum2 = sum(nums1), sum(nums2)

si suma1 == suma2:
retorno 0

# Imposible cheque
si len(nums1) * 6  obtenidos len(nums2) o len(nums2) * 6  won(nums1):
retorno -1

# Asegurar nums1 tiene la suma más grande
si la suma1 se refiere a la suma2:
volver minOperaciones(nums2, nums1)

diff = sum1 - sum2
freq = [0] * 6 # freq[1..5] – cantidad una sola operación puede cerrar

para x en nums1: # gran matriz: max disminución x-1
freq[x - 1] += 1
para y en nums2: # pequeño array: max increase 6-y
freq[6 - y] += 1

operaciones = 0
para d en rango(5, 0, -1): # uso codicioso mayores cambios
si se apagan 0:
descanso
use = min(freq[d], (diff + d - 1) // d) # ceil(diff/d)
ops += use
diff -= use * d

operaciones de retorno
`` `

-...

### 3.3 C++ (O(n) solution)

``cpp
// 1775. Arrayos de Sum iguales con número mínimo de operaciones
// C++20, O(n) solución codictiva – matriz de frecuencia
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minOperaciones(vector fielint círculo nums1, vector implicadoncia nums2) {
long sum1 = 0, sum2 = 0;
(int x : nums1) sum1 += x;
(int x : nums2) sum2 += x;

si (sum1 == sum2) devuelve 0;

int n1 = nums1.size(), n2 = nums2.size();
si (n1 * 6LL ANTE n2 TENIDO N2 * 6LL ANTE n1) retorno -1;

si (sum 1 < sum2) { // swap para hacer la suma1
devolver minOperaciones(nums2, nums1);
}

diff largo largo = suma1 - sum2; // diff positivo
int freq[6] = {0};

para (int x : nums1) freq[x - 1]++; // gran array – puede caer a 1
para (int y : nums2) freq[6 - y]++; // pequeño array – puede subir a 6

int ops = 0;
para (int d = 5; d 1 " diff " 0; --d) {
int use = min(freq[d], (int)(diff + d - 1) / d)); // ceil
ops += use;
diff -= 1LL * use * d;
}
operaciones de retorno;
}
};
`` `

■ Los tres códigos son idénticos en la lógica, sólo una sintaxis diferente.
■ Compile with `javac Solution.java`, `python3 solution.py`, g++ -std=c++20 solution.cpp -O2 -o solution`.

-...

## 4. Análisis “bueno – malo – ugly”

#### 4.1 Good

Silencio ¿Por qué es buena vida Lo que te jactarás en tu entrevista
Silencio----------------
Silencio **O(n) tiempo** – lineal en el número total de elementos.
TEN **O (1) espacio** – sólo una matriz de frecuencia de 6 elementos.
Silencio **Ningún montón / sin clasificación** – el algoritmo es puro contar.
TEN **Determinista** – ninguna aleatoriedad o rompe corbatas.
Silencio **Extremely readable** – el código es sólo unos cuantos lazos y un array. Silencio

Estas propiedades se traducen en una solución *rápida y fiable* que funciona en todos los periféricos, y lo más importante, es *fácil de explicar**. Eso es un gran plus en entrevistas.

-...

### 4.2 Mal (las posibles trampas)

Silencio Pitfall Silencio Cómo evitarlo
Silencio...
Silencio **Comprobación imposible incorrecta** – olvidando el *length × 6* vs. *length × 1* lógica significa que puede devolver una respuesta incorrecta para los arrays que no pueden alcanzar la suma requerida. Silencio Siempre realizar la prueba de imposibilidad **antes** intercambiar los arrays. Silencio
Silencio **Mezcla de signos** – si siempre asumes `sum1  Conf suma2` pero olvídate de cambiar, el diff se vuelve negativo y el bucle codicioso no funcionará. vivir los arrays si `sum1  obtenidos suma2`, o equivalentemente, siempre tratar 'grande' como el que tiene la suma más grande. Silencio
Silencio **Desbordamiento entero** – aunque las sumas están sujetas por `6 * 105`, cuando resume muchos números que debe utilizar `long`/`long'. Silencio En Java use `long`, en C++ `long', en Python la int incorporada no está abundada. Silencio
Silencio **Zero-indexing freq** – asegúrese de que nunca acceda a `freq[0]` (Sólo necesitamos 1..5). tención Inicializar `int[] freq = nuevo int[6]`; ignorar índice 0. Silencio
* División de techo* – olvidando el (diff % d == 0 ? 0 : 1)` parte puede llevar a demasiadas operaciones. Silencioso Uso `(diff + d - 1) / d` para calcular `ceil(diff/d)` con seguridad. Silencio

-...

#### 4.3 Ugly – Por qué el problema se siente más difícil de lo que es

1. **El “poder de un elemento” no es obvio. #
A primera vista usted podría pensar que necesita elegir qué elemento cambiar.
La información clave es que sólo te importa *cuántas unidades* puedes cerrar por operación, no *qué elemento*.
Recuerde que cada elemento puede reducirse a `1` o crecer a `6`.

2. **Balancing the two arrays.**
La decisión de operar siempre en el array *larger* es simple, pero tienes que recordar cambiar los roles si es necesario.

3. **División de techo dentro del bucle codicioso. #
Muchas personas usan `diff / d` y olvidan los +1 cuando `diff % d != 0`.
El truco es `ceil(diff/d) = diff / d + (diff % d ? 1 : 0)`.

4. **Edge-case “imposible” cheque** – algunos entrevistadores podrían no mencionarlo.
Es fácil pasar por alto que `len(nums1)*6` todavía podría ser inferior a `len(nums2)*1`.

5. **Testing on huge arrays** – la solución es lineal, pero no debe utilizar accidentalmente una estructura de datos 'O(n log n)` como un montón.
Eso todavía pasará con Leetcode, pero te costará mucho tiempo de ejecución.

-...

## 5. Enfoque alternativo

Si prefieres *realmente* mantener los elementos más prometedores en una cola de prioridad, el algoritmo todavía funciona, pero es **O(n1 + n2) log(n1 + n2))** y consume más memoria.

** Medidas de alto nivel**

1. Ponga cada elemento de la matriz de suma más pequeña en un max-heap (`+5` potencial).
2. Ponga cada elemento del array de suma más grande en un min-heap (`-5` potencial).
3. Mientras que " diff " 0 " , ponga al mejor candidato del montón apropiado, cambielo al extremo ( " 1 " o " 6 " ), empuje el nuevo valor, actualice " , y conte una operación.
4. Si las tapas de los montones ya están en sus extremos (`1` en min-heap o `6` en max-heap) y `diff` todavía  título 0 → imposible.

Este enfoque es conceptualmente fácil para los entrevistadores ver pero es más lento y utiliza más memoria.

-...

## 6. Cómo prepararse para esta cuestión

Silencio ¿Por qué importa?
Silencio...
Silencio ** Algoritmos de granedía** Silencio La solución principal es codicioso: “utiliza el cambio más grande primero”. Practica con cobertura de intervalos, cambio de monedas, selección de actividades. *Cracking the Coding Interview*, “Greedy” section on LeetCode Silencio
Silencio **Counting / Frequency Arrays** Silencio Tendrás que pensar en términos de “posible tamaño de cambio” en lugar de la identidad de elemento. *Algorithms on LeetCode* – “Counting Sort”, “Prefix Sum”
Silencio **Edge‐Case Thinking** Silencio El control imposible y el manejo de señales son sutiles. Practicar casos de esquina en arrays de longitudes variables. *Exercism* o *HackerRank*
Silencio **Intuición Matemática** Silencio El truco de división 'ceil' es común en muchas preguntas de entrevista. Artículo sobre GeeksforGeeks
Silencio **Maestría en la Complejidad del Tiempo** Silencio Comprende cuando `O(n log n)` vs `O(n)` asuntos. Cheat Sheet* (LeetCode)
Silencio **Testing** Silencio LeetCode le permite crear enormes casos de prueba para confirmar la linealidad.

## Plan de estudio rápido (7 días)

Silencio . .
Silencio...
Silencio 1 ← Lea la declaración del problema lentamente, parafrase en sus propias palabras. Silencioso Leetcode 1775
Silencio 2 TEN Escribe la solución de matriz de frecuencia desde cero. Solución sobre la vida
Silencio 3 ← Explicar cada paso en voz alta; enséñalo a un pato de goma.
Silencio 4 ← Pruebe la variante prioritaria; compare plazos de ejecución. ← Leetcode “Time Complexity” tab
Silencio 5 ← Escribe casos de prueba: aleatorios, todos los mismos números, casos imposibles. Silenciosas declaraciones en Python
Silencio 6 Silencio Entrevista Mock con un amigo: explicar la solución en 5 minutos. Entrevista de mock para ti
Silencio 7 ← Revisión Good‐Bad‐Ugly analysis, jot key points on a tramp sheet. Silencio Notas personales

-...

## 7. Conclusiones

- La solución avaricia **O(n)** usando un array de frecuencia es el estándar *oro* para 1775 en Leetcode.
- Muestra linealidad, memoria constante, y un enfoque de contabilidad limpio, ideal para cualquier entrevista de ingeniería de software.
- Recuerden las pocas trampas y la lógica imposible de comprobar; eso los apartará de los candidatos que pasan por alto las persianas.

¡Buena suerte! Y si estás atascado, recuerda: **contar la cantidad que puedes cerrar por operación, elegir la más grande, y repetir**. Esa es la fórmula ganadora. 🚀

-...

**Bonus**: He aquí un breve fragmento para ejecutar las tres implementaciones en los mismos datos de prueba, para asegurarse de que todos estén de acuerdo:

``cpp
// solution.cpp – arnés de prueba para las tres implementaciones
#include יbits/stdc++.h
usando std namespace;

// (Insert C++ Clase de solución aquí)

// Solución de pitón como puntero de función - omitido para brevedad

int main() {}
vector a{3,2,3,2};
vector asignadoint edad b{3,5,3,4};
Solución s;
cout se realizó s.minOperaciones(a, b)
}
`` `

Compilar y ejecutar – el resultado debe coincidir con la salida esperada de Leetcode.

Codificación feliz, y que su entrevista sea *fast, limpia y resistente al borde*! .

-...

*No dude en dejar un comentario si necesita más explicación o tiene una variante de este problema que le gustaría discutir. *