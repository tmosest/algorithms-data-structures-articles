-...
Título: LeetCode 1893. Compruebe si todos los números enteros en un rango están cubiertos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1893 – “Comprobar si todos los números enteros en un rango están cubiertos”

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio **Java** Silencio O(n + m) Silencio O(m)
Silencio **Python** Silencio O(n + m) Silencio O(m) Silencio
Silencio **C+** Silencio O(n + m) Silencio O(m) Silencio

n = número de rangos, m = tamaño del universo entero (≤ 50)*

■ *Por qué esto importa* – Este problema de “cover‐check” es un *clásico* para coding-interviews, especialmente para los roles que se centran en ** manipulación de rayos, sumas prefijo, y arrays de diferencia**. Dominarlo demuestra una solución de dominio O(1) limpia que escala a grandes insumos.

-...

Resumen del problema

Se te da:

- `ranges`: una lista de intervalos enteros inclusivos `[start1,end1], ...].
- Dos límites "izquierda" y "derecha".

** Objetivo:** Regresar `verdad` si cada entero `x` con `izquierda ≤ x ≤ derecho` se encuentra dentro de al menos uno de los intervalos proporcionados. De lo contrario devuelve `false`.

-...

## 2down Bru Brute‐Force Solution (Naïve)

Revise cada entero en `[izquierda, derecha]` contra todos los intervalos.

``python
def is_covered_bruteforce(ranges, left, right):
para x en rango(izquierda, derecha+1):
si no cualquier(start <= x <= final for start, end in ranges):
Retorno Falso
Retorno
`` `

- **Hora:** `O(derecha-izquierda+1) * n)` – peor-case 2500×50 = 125k operations (aceptable para LeetCode pero no elegante).
- **Espacio:**.

-...

## 3Ω⃣ Solución Optimal – Difference Array (Line Sweep)

Debido a que el universo está atado (`1..50`), podemos mantener un array de *diferencia* que registra cuando una cobertura comienza y se detiene.

#### 3.1 Intuición

1. Por cada intervalo `[l, r]`, incremento `diff[l]` por `1`.
2. Decrement `diff[r+1]` by `1` (since `r` is inclusive).
3. Prefix‐sum `diff` da el número de intervalos activos en cada entero.
4. Mientras escaneamos, si alcanzamos un número en `[izquierda, derecha]` con 0 intervalos activos, la respuesta es 'falsa'.

#### 3.2 Code

#### Python

``python
def is_covered(ranges: list[list[int]], left: int, right: int) - título Bool:
"
O(n + m) tiempo, espacio O(m)
m == 51 porque 1 <= start,end
"
diff = [0] * 52 # índices 1..50; 51 utilizado para r+1 cuando r=50

para l, r en rangos:
diff[l] += 1
diff[r + 1] -= 1

activo = 0
para i en rango(1, 51):
activo += diff[i]
si la izquierda es la derecha y la activa 0:
Retorno Falso
Retorno
`` `

##### Java

``java
Solución de la clase pública {}
public boolean isCovered(int[][] rangos, int left, int right) {
int[] diff = nuevo int[52]; // índices 1..50, 51 para r+1
para (int[] r : ranges) {
diff[r]]++; // inicio de cobertura
diff[r[1] + 1]--; // final of coverage
}

int active = 0;
para (int i = 1; i) = 50; i++) {
activo += diff[i];
si (i √≥= left ' l ' = derecha ' activa == 0) {
devolver falso;
}
}
retorno verdadero;
}
}
`` `

###### C++

``cpp
Clase Solución {
public:
bool isCovered(vector seleccionadovector identificadoint convenientemente limitado, int left, int right) {
int diff[52] = {}; // 1..50, 51 for r+1

para (autor : rangos) {}
diff[r]]++; // start
diff[r[1] + 1]--; // end+1
}

int active = 0;
para (int i = 1; i) = 50; ++i) {}
activo += diff[i];
si (i √≥= left ' l ' = derecha ' activa == 0) {
devolver falso;
}
}
retorno verdadero;
}
};
`` `

#### 3.3 Complexity

- **Hora:** `O(n + 50)` ♥ `O(n)` (linear en el número de rangos).
- **Espacio: ** `O(52)` ♥ `O(1)` - memoria extra constante.

-...

## 4VIEW — Good, Bad & Ugly

Silencio Silencio
Silencio------------Prince------
Silencio **Concept** Silencio Usa un array de *diferencia* – un clásico truco lineal-time Silencio Requiere conocimiento de line‐sweep / suma prefix (puede no estar familiarizado)
Silencio **Implementación** tención Extremadamente concisa; sólo dos lazos TENIDO Índice `r+1` puede parecer extraño; fuera-por-uno errores comunes TEN duro-a-debug cuando el universo cambia; necesidad de redimensionar la matriz
Silencio **Performance** Silencio O(1) space, O(n) time – óptima  duración La fuerza bruta es O(derecha-izquierda +1)*n) – lento para grandes gamas ANTERIOR Por `m` enorme (por ejemplo, 10^9) este enfoque falla; necesita una línea de barrido sobre los eventos ANTE
Silencio **Readability** Silencio Fácil para los ingenieros experimentados Silencio Podría ser intimidante para los principiantes Silencio Si el entrevistador espera una solución de “sort-intervalos”, este dif-array podría ser visto como overkill ¦

■ **Takeaway** – Master the *difference array* trick; it’s a go‐to pattern for range‐update/count problems. En entrevistas, puede comenzar con una explicación clara de la idea, luego implementar la versión de array de tamaño constante. Si el entrevistador presiona para una solución genérica (universo sin límites), puede cambiar a una línea de barrido basada en eventos.

-...

## 5down Casos de prueba

``python
Ejemplo 1
afirma is_covered([1,2],[3,4],[5,6]], 2, 5) == True

# Ejemplo 2
afirma is_covered([1,10],[10,20], 21, 21) == Falso

# Edge: intervalos superpuestos
afirma is_covered([1,3],[2,5],[4,6]], 1, 6) == True

# Edge: single number not covered
afirma is_covered([1,5]], 6, 6) == False

# Cobertura completa
afirma is_covered([1,50]], 1, 50) == Cierto.
`` `

-...

Artículo del Blog optimizado

■ ### “How to Crack LeetCode 1893 in 5 Minutes – A Java/Python/C++ Guide for Job Interviews”

-...

##### ##

- LeetCode 1893
- Comprueba si todos los números están cubiertos
- entrevista de codificación
- matriz de diferencia
- prefijo suma
- barrido de línea
- pregunta de entrevista de algoritmos
- Solución Java LeetCode
- Python LeetCode
- Entrevista de codificación C++

-...

Artículo

-...

### 1. Introducción

En entrevistas de ingeniería de software, a menudo verá preguntas que preguntan si *todo entero en un rango está cubierto por un conjunto de intervalos*. LeetCode 1893 es el ejemplo canónico. Aunque las limitaciones se ven diminutas (`1 ≤ inicio ≤ final ≤ 50`), el problema es un **puerta** a conceptos de algoritmos básicos: sumas prefijas, arrays de diferencia y líneas-sweep. Dominarlo no sólo aumenta su calificación de LeetCode sino también señales a los reclutadores que usted entiende la manipulación eficiente de la matriz.

-...

### 2. Recaptación de problemas

Usted recibe una serie de intervalos inclusivos y dos límites `izquierda y 'derecha'. Regresar `verdad ' si cada entero `x` con `izquierda ≤ x ≤ derecho` se encuentra dentro al menos un intervalo. Esta es una prueba de *cubrición*: `[1,2],[3,4],[5,6]]` abarca `[2,5]` → `verdad ' [[1,10],[10,20] ' no ** cubre `21` → `false`.

-...

### 3. ¿Por qué un enfoque ingenuo es malo

Un doble bucle que prueba cada entero contra cada intervalo es simple, pero es **O((right‐left+1) × n)**. En LeetCode aún puedes pasar (125 k operaciones), pero en una entrevista pasarás unos segundos preciosos en una solución * ligeramente no óptima*. El equipo de trabajo quiere ver que piensa **line‐sweep** antes de “sólo brute-forcing”.

-...

### 3.1 Estrategia Optimal: Difference Array

Silencio Silencio Silencio Silencio Silencio
Silencio--------------------
Silencio 1 Silencio ** Incremento** `diff[l]` por `1` por cada intervalo `[l,r]`. Silencio marca el *start* de la cobertura. Silencio
Silencio 2 Silencio **Decreto** `diff[r+1]` por `1`. Silencio Dado que el intervalo es inclusivo, la cobertura termina *después* `r`. Silencio
Silencio 3 Silencio Computar una suma prefijo sobre `diff`. Silencio Da la cuenta de intervalos activos en cada entero. Silencio
Silencio 4 ¦ Mientras escanea, si un entero en `[izquierda, derecha]` tiene 0 intervalos activos → `false`. Silencio Detección inmediata de una brecha. Silencio

■ **Por qué es O(n + m) vs O(right-left+1)*n)** – *pre-aggregate* todos los inicios/ends en un solo pase, luego un solo pase lineal sobre el array 51-slot (constant). No hay cheques repetidos en cada intervalo.

-...

### 4. Aspectos destacados de la aplicación

##### Java

``java
public boolean isCovered(int[][] rangos, int left, int right) { ... }
`` `

" int[52]; " – memoria constante.
* Dos bucles: uno para llenar `diff`, otro para escanear y salir temprano.

#### Python

``python
def is_covered(ranges, left, right): ...
`` `

√≥n • `diff = [0] * 52` – La lista de pitones es eficiente en memoria para pequeños dominios.
• Usar `cualquier(iniciar)= x <= final para comenzar, terminar en rangos)' en la versión ingenua para ver la diferencia.

###### C++

``cpp
bool isCovered(vector identificadovector identificadoint ánimo limitada rangos, int left, int right) { ... }
`` `

• matriz estatica `int diff[52]` – cero-inicialización en C++ es trivial.
• Tiempo de compilación más rápido debido a la asignación de pilas.

-...

### 5. Lo que los entrevistadores realmente buscan

Silencio Hint ← ¿Por qué?
Silencio...
Silencio Explicar el *diferencia array* en inglés claro antes de codificación. Muestra que usted entiende el “juego de prefijo-sum” y puede articularlo. Silencio
tención Mención que `r+1` es seguro porque el universo está atado. ← Evita sorpresas “off-by-one”. Silencio
Silencio Ofrezca una solución alternativa de “intervalos variados” si se le pide. Flexibilidad: puedes pivotar a una línea de barrido sobre eventos para universos más grandes. Silencio

■ **Pro tip:** Si la primera solución del entrevistador es *naïve*, pivote rápidamente a la matriz de diferencias. El equipo de trabajo ama a un candidato que puede **reconocer una oportunidad para la optimización**.

-...

### 6. Hoja de Cheat de Complejidad

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio Java Silencio **O(n + m)** → **O(n)** Silencio **O(m)** → **O(1)** Silencio
Silencio Python Silencio **O(n + m)** Silencio **O(m)**
TENIDO C++ TENIDO **O(n + m)** Silencio **O(m)** Silencio

(≤ 50), m = tamaño del universo (≤ 51). *

-...

### 7. Pensamientos finales

- **LeetCode 1893** no es sólo un rango de comprobación – es un *signal* que usted capta los trucos de estructura de datos básicos.
- El patrón de la diferencia es **portable**: utilícelo para "range addition", "range sum queries", y muchas otras grapas de entrevista.
- En una coding-interview, presentar la idea primero, luego entregar la implementación de array de tamaño constante. Si el reclutador pregunta sobre la escalabilidad, explique cómo el mismo concepto puede extenderse a un *sweep‐line* sobre los puntos del evento.

-...

### 8. ¿Listo para Nailar su próxima entrevista de trabajo?

- Escribe la solución en **Java** (estático de escribir + OOP).
- Pruébalo en **Python** (conciso, legible).
- Validar con **C+** (orientada al desempeño).

Añadir estas soluciones a tu cartera, empujarlas a GitHub, y cuando los reclutadores busquen “LeetCode 1893 Java”, tu código aparecerá en la parte superior. ¡Buena suerte con tu preparación de entrevistas! 🚀

-...

### 📌 TL;DR

- **Use un array de diferencia** – 2 bucles, memoria constante, tiempo lineal.
- **Explica la lógica** claramente; los reclutadores aman una respuesta bien estructurada.
- **Incluye pruebas de periferia** – muestra que has pensado a través de escenarios “malos” y “muy”.

-...

##### 📥 Descargar todo el código

``bash
# Java
curl -o Solution.java https://pastebin.com/raw/xxxxxxxxxx

# Python
Curl -o solución. py https://pastebin.com/raw/xxxxxxxx

# C++
curl -o solution.cpp https://pastebin.com/raw/xxxxxxxxxx
`` `

(Reemplazar `xxxxxxxx` con el hash de Pastebin real o su propia copia alojada.)

-...

Entendido *Ahora estás listo para responder a LeetCode 1893 como un profesional, reclutadores de impresiones, y aterrizar ese trabajo de ingeniería de software. *