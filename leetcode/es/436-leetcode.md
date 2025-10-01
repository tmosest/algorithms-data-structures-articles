-...
Título: LeetCode 436. Encontrar la Interval derecha -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Leetcode 436 – **Find Right Interval**
*Desde soluciones fáciles de entender hasta el código de entrevistas de trabajo (Java / Python / C++). *

-...

## TL;DR – The One‐Line Solution

``text
Intervalo derecho = primer inicio ≥ intervalo.end ( surtido por inicio)
`` `

* Clasifique los intervalos por sus valores de arranque (conservando los índices originales).
* Para cada intervalo ejecutar una búsqueda binaria en el orden comienza a localizar el
inicio más pequeño que es ≥ el intervalo actual 'end`.
* Si se encuentra, devuelve el índice original de ese intervalo; de lo contrario devuelve `-1`.

Complejidad: **O(n log n)** tiempo, **O(n)** espacio extra.

-...

## ¿Por qué este problema es una “Mina de Oro de Interview”

* **Core Concepts Tested**: clasificación, búsqueda binaria, mapas de hash, punteros.
* **Idiomas**: Java, Python, C++ – los idiomas de entrevista más comunes.
* **Variantes**: La misma lógica se aplica a “Encontrar el próximo mayor elemento”,
“Buscar en Rotated Sorted Array”, etc.
* **Entreview Talking-Points**:
* Explicar por qué es necesaria la clasificación.
* Discuss the use of `Map` / `unordered_map` to preserve original indices.
* Hablar sobre los bordes (sin intervalo adecuado, valores negativos).
* Optimize for time vs. space.

Si puedes explicar esta solución con claridad en **menos de 5 minutos** ganarás el favor de muchos entrevistadores.

-...

## 1. Recaptura de problemas (Leetcode 436)

Dado un array `intervalos` donde cada elemento es `[start, end]` y cada `start`
es único, para cada intervalo encontrar el índice del intervalo *derecha*:

* Un intervalo adecuado `j` satisfies `start[j] ≥ end[i]`.
* Entre todos estos intervalos, elija el uno con el valor inicial **minimum**.
* Si no existe, devuelve `-1`.

Devuelve una serie de índices de intervalo derecho para cada intervalo en el orden
originalmente dado.

**Constraints* *

confidencialidad Parámetro Silencioso Tamaño Silencioso
Silencio------------------------
TENIDA `intervals.length` Silencio `1 ... 2·104` Silencio
TENIENDO `intervalos[i].length` TENIDO `2` TENIDO
TENIDO `-106 ≤ inicio ≤ final ≤ 106` Silencio TEN 
los valores de `start ' son únicos

-...

## 2. The Greedy + Binary Search Idea

1. **Keep Original Indices** – crear una lista de pares `(start, originalIndex)`.
2. **Sort by Start** – ahora podemos realizar búsquedas binarias en `start`.
3. **Binary Search** – para cada intervalo 'end', encontrar el *limitado inferior* en el
ordenada comienza: el primer comienzo que es ≥ `end`.
4. **Respuesta** – si existe tal comienzo, su índice original almacenado es la respuesta;
de lo contrario `-1`.

Por qué funciona:
Todo comienza son únicos → el orden ordenado es estricto, por lo que el límite inferior es
bien definido. Porque arreglamos una vez, cada búsqueda es `O(log n)`.

-...

## 3. Aspectos destacados de la aplicación

Silencio Idioma Silencio Key Library Silencio
Silencio------------
Silencio **Java** Silencioso `Arrays.binarySearch`, `Mapa realizadaInteger,Integer confianza`, `Arrays.sort` Silencio
Silencio **Python** Silencio `bisect_left`, `sorted`, `dict` 
TENIDO **C+** TENIENDO `lower_bound`, `vector obedeciópair madeint,intenta ``, `unordered_map` ANTE

Todas las soluciones son **iterative** (no recursion) y evitan operaciones costosas
dentro del bucle.

-...

## 4. Código (Java, Python, C++)

### 4.1 Java – Clean, Interview‐ Listo

``java
importar java.util*;

Solución de la clase pública {}
int[] findRightInterval(int[][] intervalos) {
int n = intervalos. longitud;
int[] response = new int[n];

// (start, originalIndex)
int[][] startIdx = nuevo int[n][2];
para (int i = 0; i)
startIdx[i][0] = intervalos[i][0];
startIdx[i][1] = i;
}
// ordenar por valor inicial
Arrays.sort(startIdx, Comparator.comparingInt(a - título a[0]));

// extracto ordenados comienza a buscar binario
int[] comienza = nuevo int[n];
para (int i = 0; i) no; i++) comienza[i] = startIdx[i][0];

para (int i = 0; i)
int end = intervalos[i][1];
int pos = lowerBound(starts, end); // custom lower bound
respuesta[i] = (pos < n) ? startIdx[pos][1] : -1;
}
respuesta de retorno;
}

// Búsqueda binaria estándar para el límite inferior
int private int lowerBound(int[] arr, int target) {}
int lo = 0, hola = arrr.length;
mientras (lo cautivado) {
int mid = (lo + hola) 1;
si (arr[mid]) lo = medio + 1;
más hola = medio;
}
devolver lo;
}
}
`` `

■ ¿Por qué no "Arrays.binarySearch"?
> `Arrays.binarySearch` devuelve un índice sólo cuando la clave está presente; de lo contrario
> it devuelve un punto de inserción negativo. `lowerBound` es más clara y evita
doble negaciones.

-...

### 4.2 Python – Elegante y legible

``python
de la importación de bisect_left
de la importación Lista

Solución de clase:
def findRightInterval(self, intervalos: List[List[int]) - No. List[int]:
# (start, original_index) ordenados por principio
(intervalo[0], idx) para idx, intervalo en enumerado(intervalos))
set_starts = [s for s, _ in starts]

res = []
para terminar en (intervalo[1] para intervalos):
pos = bisect_left(sorted_starts, end)
re.append(starts[pos][1] si pos < len(starts) else -1)
retorno
`` `

-...

### 4.3 C++ – Alto rendimiento & Clásico

``cpp
Incluido el título
#include >

Clase Solución {
public:
std:::vector seleccionadoint confianza findRightInterval(std::vector seleccionadosstd:::vector fielint implica intervalos de contacto) {}
int n = intervalos.size();
std:::vector obtenidosstd::pair seleccionado, int confía startIdx(n); // (start, original idx)

para (int i = 0; i) {}
startIdx[i] = {intervalos[i][0], i};
}

std::sort(startIdx.begin(), startIdx.end(),
[](cont auto cho a, const auto golpe b){ return a.first Identifica b.first; });

std::vector seleccionado empiezo(n);
para (int i = 0; i) no; ++i) comienza[i] = startIdx[i].first;

std::vector garantizadoint
para (int i = 0; i) {}
int end = intervalos[i][1];
auto it = std::lower_bound(starts.begin(), starts.end(), end);
ans[i] = (it != starts.end()) ? startIdx[it - starts.begin()].second : -1;
}
devolver los ans;
}
};
`` `

■ **¿Por qué usar 'std::lower_bound'?**
■ Implementa directamente la búsqueda binaria del primer elemento ≥ `target`
- exactamente lo que necesitamos.

-...

## 5. El Bien, el Mal, el Ugly

Silencio Silencio
Silencio------------Prince------
Silencio ** Complejidad del tiempo** Silencio `O(n log n)` es óptimo para datos no variados. TEN Ninguno – el algoritmo ya es óptimo. Silencio.
Silencio ** Complejidad del espacio** Silencioso `O(n)` para la matriz de inicio ordenada. Silencioso superior de los índices de almacenamiento, pero inevitable.
tención **Code Simplicity** tención Paso único + búsqueda binaria. ← Requiere la comprensión de “un límite más bajo”. Silencio Si tratas de usar montones o truco de dos puntos, se pone desordenado. Silencio
Silencio ** Casos de Edge** tención Handles inicia, grandes rangos. Necesidad de recordar utilizar 64 bits si rango " in "  durable Olvidar que los valores `start ' son únicos puede romper la lógica. Silencio
TEN **Language‐Specific Pitfalls** TEN Java: `Arrays.binarySearch` valores negativos. Silencio Python: `bisect_left` vs `bisect_right`. Silencio C++: iterator arithmetic off‐by-one. Silencio

**Bottom Line:** Sigue el patrón ** surtido + búsqueda binaria**. Está limpio, rápido y cubre todos los casos de borde.

-...

## 6. SEO‐Optimized Blog Artículo

### Title
**Leetcode 436 – Find Right Interval: Java / Python / C++ Soluciones Guía de entrevista**

## Meta Descripción
Master Leetcode 436 “Find Right Interval” con soluciones paso a paso en Java, Python y C++. Aprenda el algoritmo óptimo, los cambios y las explicaciones de entrevista para aumentar su preparación de entrevistas de codificación.

-...

#### 1down⃣ ¿Qué es “Encontrar la Interval derecha”?

**436** de Leetcode le pide que encuentre, para cada intervalo, el intervalo más pequeño cuyo inicio es al menos el final del intervalo actual. Es un problema clásico de “buscar el siguiente valor mayor” pero con intervalos.

-...

#### 2down⃣ ¿Por qué te importa?

* **Entrevista de oro* Clasificación + búsqueda binaria muestra que conoce los fundamentos de la estructura de datos.
* **Job-ready:** Empresas como Google, Amazon y Stripe preguntan variaciones de esto.
* **Cross‐language:** La lógica es idéntica en Java, Python y C++ – perfecta para carteras multilingües.

-...

#### 3down⃣ La Solución Optimal en un Nutshell

1. **Mantenga índices** – almacene los pares de `(start, originalIndex).
2. **Ordenar por inicio** – un pase O(n log n).
3. **Binary search** – para cada "end", encontrar el límite inferior en el orden comienza.
4. ** Índice de retorno** – si se encuentra, utilice el índice original almacenado; de lo contrario `-1`.

-...

### 4down⃣ Step‐by‐Step Walkthrough (Python)

``python
de la importación de bisect_left

def findRightInterval(intervalos):
(s, i) para i, (s, _) en enumerado(intervalos))
set_starts = [s for s, _ in starts]
Resultado = []

para _, e en intervalos:
pos = bisect_left(sorted_starts, e)
result.append(starts[pos][1] si pos י len(starts) else -1)
Resultado de retorno
`` `

*Time*: `O(n log n) `
*Pace*: `O(n)`

-...

### 5down⃣ C++ & Java Code (Same Idea)

* **C++** – utiliza `std::lower_bound`.
* **Java** – utiliza la costumbre `lowerBound` para evitar confusión con `Arrays.binarySearch`.

Ambos están bajo 40 líneas, completamente compilables y listos para Leetcode.

-...

### 6 millas] Entrevista Puntos de conversación

1. ¿Por qué ordenar?
*Necesitamos encontrar rápidamente el siguiente inicio ≥ final. La clasificación convierte el problema en una búsqueda binaria. *

2. **¿Por qué búsqueda binaria? #
*Estamos buscando el inicio de calificación *smallest*; el límite inferior lo da en `O(log n)`. *

3. ** Comercio de espacio* *
* Almacenamos una matriz auxiliar de inicios + índices. Todavía espacio lineal, pero mucho más barato que una solución de salto. *

4. ** Casos de emergencia**
*No hay intervalo adecuado → retorno `-1`.
* Valores de inicio negativos " grandes gamas → use " (range ±106 se ajusta cómodamente). *

5. ** Soluciones alternativas**
*TreeMap (Java) / std::map (C++) – O(n log n) pero factor constante más alto.
*PriorityQueue approach – O(n2) el peor caso. *

-...

### 7ف⃣ TL;DR – Quick Reference

Silencio Idioma TENIDO Funciones clave TENIDO Complejidad
Silencio----------------------------------
Silencio **Java** Silencioso `Arrays.sort`, custom `lowerBound`  durable `O(n log n)` Silencio
Silencio **Python** Silencio `bisect_left`, `sorted` Silencio `O(n log n)` Silencio
Silencio **C+** Silencio `estd::sort`, `std::lower_bound` Silencio `O(n log n)` Silencio

-...

#### 8down⃣ Takeaway

El problema “Find Right Interval” es un escaparate perfecto de * surtido + búsqueda binaria*.
Dominar esta solución demuestra a los reclutadores que pueden:

* Reducir una búsqueda aparentemente compleja a un patrón algoritmo estándar.
* Escribir código limpio, cross-language.
* Hable con confianza sobre los cambios de tiempo/espacio.

¡Feliz codificación y buena suerte con tu próxima entrevista! 🚀

-...

Recursos de bonificación

Silencio Tema Silencio Recurso
Silencio...
Silenciosos fundamentales de la búsqueda binaria [GeeksforGeeks – Binary Search] (https://www.geeksforgeeks.org/binary-search/) Silencio
Silencio Entrevista cursos de preparación latitud LeetCode Explorar, Cracking the Coding Interview ←
Silencio Portfolio showcase Silencio GitHub repos with language tags, Leetcode submission Estadísticas Silencio

-...

Pensamientos finales

Ahora que tienes:

* **Tres soluciones completas* (Java, Python, C++).
* Una lógica algorítmica clara**.
* A **ready‐to‐publish blog article** to showcase in your résumé.

Usted está listo para convertir Leetcode 436 en una victoria de cartera y seguro que codiciaron la entrevista de codificación. Sigue practicando y explorando variaciones: ¡el siguiente reto está justo a la vuelta de la esquina! .

-...

*© 2024 Tu Viaje de Codificación. *

-...

### Word Count
♥ 900 palabras (listos para SEO, conciso y fácil de esquiar).