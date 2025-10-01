-...
Título: LeetCode 2491. Divide jugadores en equipos de igual habilidad -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 LeetCode 2491 – Divide Players Into Teams of Equal Skill
** Idiomas**: Java, Python, C++
**La complejidad**: O(n log n) time, O(1) extra space (in-place sort)

-...

### 1. Recaptación de problemas

Se le da un **even-length** array `skill` (`1 ≤ habilidad[i] ≤ 1000`).
Tienes que emparejar a los jugadores (tamaño 2) para que ** cada par tenga la misma habilidad total**.
Si eso es posible, devuelva el **sumo de la química** (producto de habilidades en cada par); de lo contrario devuelva `-1`.

-...

### 2. Por qué Ordenar + Obras de dos puntos

1. **Sorta** la matriz – entonces el valor más pequeño está en la parte delantera y la más grande en la parte posterior.
2. Si existe una partición válida, el par que contiene el valor *smallest* también debe contener el valor * más grande*, porque cualquier otra opción haría la suma más pequeña que el objetivo requerido.
3. Después de fijar el primer par, el siguiente más pequeño y el siguiente más grande debe añadir de nuevo al mismo objetivo, y así sucesivamente.
4. Si algún par se desvía de esa suma, una partición válida es imposible.
5. Mientras emparejamos también acumulamos el producto para obtener la química total.

Así un solo escaneo lineal después de ordenar da la respuesta.

-...

### 3. Aplicación del Código

A continuación se encuentran soluciones limpias y de producción para **Java**, **Python**, y **C+**.

-...

##### 3.1 Java

``java
importa java.util. Arrays;

Solución de la clase pública {}
public long dividePlayers(int[] habilidad) {
Arrays.sort(skill); // O(n log n)
int n = habilidad.length;
int target = habilidad[0] + habilidad[n-1]; // suma que cada par debe alcanzar
química larga = 0;

para (int i = 0; i)
si (skill[i] + habilidad[n-1-i] != target) {
retorno -1; // imposible
}
química += (long) habilidad[i] * habilidad[n-1-i];
}
devolver química;
}
}
`` `

**Explicación**
* `Arrays.sort(skill)` clasifica el array en lugar.
* El bucle corre `n/2` veces – espacio extra constante.
* El elenco a `long` evita el desbordamiento (producto máximo 1000 × 1000 = 1 000 000, seguro, pero la suma puede llegar a 10^11 por n = 10^5).

-...

##### 3.2 Python 3

``python
de la importación Lista

Solución de clase:
def divide Jugadores(auto, habilidad: List[int]) - título int:
habilidad.sort() # O(n log n)
n = len(skill)
objetivo = habilidad[0] + habilidad[-1] # suma de par requerida
química = 0

para i en rango(n // 2):
si habilidad[i] + habilidad[n - 1 - i]!= objetivo:
retorno -1
química += habilidad[i] * habilidad[n - 1 - i)
química de retorno
`` `

¿Por qué funciona Python?
* `list.sort()` modifica la lista en lugar.
* El aritmético entero en Python es sin límites, por lo que no se preocupa el desbordamiento.
* La lógica es idéntica a Java y C++.

-...

##### 3.3 C++ (GNU ++17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
larga distancia Jugadores(vector seleccionados) {
(skill.begin(), habilidad.end()); // O(n log n)
int n = habilidad.size();
int target = habilidad.front() + habilidad.back(); // par sum that must match

larga química larga = 0;
para (int i = 0; i) {}
si (skill[i] + habilidad[n - 1 - i] != target) {
retorno -1; // imposible
}
química += 1LL * habilidad[i] * habilidad[n - 1 - i];
}
devolver química;
}
};
`` `

**Notas*
* `1LL * ...` fuerza multiplicación de 64 bits.
* `sort()` utiliza introsort – rápido y estable para la mayoría de los insumos.

-...

### 4. Análisis de la complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio Ordenación Silencioso **O(n log n)** Silencio **O(1)** (en lugar)
Silencioso pareado* **O(n)** Silencio **O(1)**
Silencio **Total** Silencio**

n ≤ 10^5`, por lo que la solución pasa fácilmente todas las pruebas de LeetCode.

-...

### 5. El Bien, el Mal, El Ugly

Silencio Silencio
Silencio------------Prince------
Silencio ** La elegancia algorítmica** Silencio Ordenar + dos puntos es *O(n log n)*, óptima para valores arbitrarios ← Requisitos clasificación – no se puede reducir al tiempo lineal sin restricciones adicionales  Si la entrada ya está clasificada, todavía clasificamos (sobrecarga innecesaria)
Silencioso **Implementación sencillez** Silencio Todos los idiomas comparten código casi idéntico Silencio Muy pocas líneas, pero olvidando el elenco 'long' en Java/C++ causa el desbordamiento en enormes entradas.
Silencio **Uso de memoria** Silencio Tipo in-place – insignificante overhead ← Requiere una copia si queremos preservar la matriz original Silencio Algunos jueces en línea no aceptan la mutación en lugar – deben copiar de todos modos
Silencio **Edge-cases** tención Handles mono-pair arrays, duplicates, y grandes valores tención Ninguno – algoritmo es determinista ¦ Si `skill.length` es extraño (aunque las restricciones lo prohíben) → comportamiento indefinido Silencio
Silencio **Readability** Silencio Nombres variables claros (`target`, `chemistry`) Silencio Muy tesor – un novicio puede luchar contra la vida Ninguno – el código es intencionalmente corto, pero la documentación sigue siendo necesaria

-...

### 6. SEO‐Optimized Blog Artículo

■ **Título**: *LeetCode 2491 – Divide Players Into Teams of Equal Skill: Java, Python, " C++ Soluciones*
■ **Meta Descripción**: Aprende el algoritmo O(n log n) óptimo para LeetCode 2491. Obtenga paso a paso Java, Python, y C++ código, además de una profunda inmersión en la estrategia de dos puntos.

-...

##### 6.1 Introduction

Si usted está cazando para eso siguiente **LeetCode entrevista pregunta**, “Divide Players Into Teams of Equal Skill” (Problem 2491) es un desafío clásico *medium* que prueba clasificación, lógica de dos puntos, y manejo cuidadoso del flujo entero.
En este post caminaremos a través de una solución limpia y lista para la producción, proporcionaremos implementaciones en **Java**, **Python**, y **C+**, y resaltaremos los aspectos *bueno*, *bad* y *muy* del enfoque.

■ **Keywords**: LeetCode 2491, dividir jugadores en equipos, igual habilidad, solución Java, solución Python, solución C++, dos punteros, clasificar algoritmo, programación competitiva, diseño de algoritmos

-...

#### 6.2 Declaración de problemas (Re-phrased for Clarity)

Se le da un array `skill[]` de longitud uniforme.
La tarea: emparejar a los jugadores de tal manera que *todo par tiene la misma habilidad total*.
Si esa partición es posible, devuelve la suma de la *química* de cada par (producto de habilidades).
De lo contrario, devuelve `-1`.

* Limitaciones*:
- `2 ≤ habilidad.length ≤ 10^5` (even)
- `1 ≤ habilidad[i] ≤ 1000`

-...

#### 6.3 Why Sorting + Two‐Pointers is the Key

1. Después de ordenar, el más pequeño (`skill[0]`) y el más grande (`skill[n-1]`) debe formar la suma del par **target**.
2. El siguiente más pequeño y más grande (`skill[1]` " matar[n-2] " Debe añadirse a ese objetivo, y así sucesivamente.
3. Un solo pase lineal valida la partición *y* acumula la química.

La belleza: el algoritmo es **O(n log n)** debido al tipo, y **O(1)** memoria extra.

-...

#### 6.4 Step‐by‐Step Pseudocode

`` `
especie(skill)
objetivo = habilidad[0] + habilidad[última]
química = 0
para mí en 0 .. n/2 - 1
si habilidad[i] + habilidad[n-1-i] != objetivo
retorno -1
química += habilidad[i] * habilidad[n-1-i]
química de retorno
`` `

-...

#### 6.5 Código completo – Tres idiomas

■ *Los siguientes snippets están listos para pegar en el editor de LeetCode. *

#Java #
``java
importa java.util. Arrays;
Solución de la clase pública {}
public long dividePlayers(int[] habilidad) {
Arrays.sort(skill);
int n = skill.length, target = habilidad[0] + habilidad[n-1];
química larga = 0;
para (int i=0;i obtenidos/2;i+) {
si (skill[i] + habilidad[n-1-i]!= target) retorno -1;
química += (long) habilidad[i] * habilidad[n-1-i];
}
devolver química;
}
}
`` `

Python
``python
Solución de clase:
def divide Jugadores(auto, habilidad: List[int]) - título int:
habilidad.sort()
n, target = len(skill), habilidad[0] + habilidad[-1]
chem = 0
para i en rango(n//2):
si habilidad[i] + habilidad[n-1-i] != objetivo: retorno -1
chem += habilidad[i] * habilidad[n-1-i]
Retorno de quimio
`` `

**C++**
``cpp
Clase Solución {
public:
larga distancia Jugadores(vector seleccionados) {
(skill.begin(), habilidad.end());
int n = habilidad.size(), target = habilidad.front() + habilidad.back();
largo largo largo quimio = 0;
para (int i=0;i obtenidos/2;i+) {
si (skill[i] + habilidad[n-1-i]!= target) retorno -1;
chem += 1LL * habilidad[i] * habilidad[n-1-i];
}
devolver la quimio;
}
};
`` `

-...

#### 6.6 Complexity & Edge Cases

* **Tiempo**: `O(n log n)` – dominado por el tipo.
* **Espacio**: `O(1)` – ordenar en su lugar, sólo algunas variables primitivas.
* **Overflow**: In Java/C++ use `long`/`long long`; Las fortalezas de Python son de precisión arbitraria.

-...

#### 6.7 The Good, Bad, and Ugly

Silencio Silencio
Silencio------------Prince------
← Algorithm ← Simple, óptimo O(n log n) Silencio Requiere ordenar incluso si ya está clasificado ← Unnecesario ordenar si la entrada ya está clasificada 
TENIDO Código ANTERIOR Casi idéntico a través de idiomas ← Olvidar 64 bits lanzados en Java/C++ causa desbordamiento ← Debugging sutil C++ fallos de desbordamiento
tención Readability ← Nombres claros (`target`, `chemistry`) Silencio Extremadamente cortos – los novatos pueden perder el 'long' cast Н Ninguno – código es conciso pero necesita documentación

-...

##### 6.8 Takeaway for Interviews

* Destacar la intuición **2 puntos**: más pequeño + más grande debe coincidir con el objetivo.
* Mención **Desbordamiento del entero** manejo en lenguajes estaticamente escritos.
* Mostrar que el algoritmo es *deterministic* y *fast* – puntos de conversación perfectos para una entrevista de ingeniería de software.

-...

#### 6.9 Palabras finales

Problema 2491 es un gran escaparate de cómo un clásico * surtido + dos puntos* truco puede convertir un problema de pareo aparentemente combinatorio en un solo pase lineal.
Con los snippets de código Java, Python y C++ arriba estarás listo para **solverlo en LeetCode o **crush** en una entrevista en vivo.

¡Feliz codificación! 🚀

-...

**Búsqueda-engine friendly tags* *
`#LeetCode2491`, `#DividePlayersIntoTeamsOfEqualSkill`, `#JavaSolution`, `#PythonSolution`, `#CppSolution`, `#TwoPointers`, `#SortingAlgorithm`, `#Competitive Programación " , Prep`, `# AlgorithmDesign `

-...

¡Feliz entrevista!