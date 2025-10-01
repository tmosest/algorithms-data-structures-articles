-...
Título: LeetCode 3036. Número de subarrayos que coinciden con un patrón II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. El Código - Tres idiomas

A continuación encontrará una aplicación **ready‐to-copy** de la solución óptima para LeetCode 3036
`Número de Subarrayos que coinciden con un patrón II`.
La solución se ejecuta en **O(n + m)** tiempo y **O(m)** espacio auxiliar, utilizando el KMP
(“Knuth–Morris–Pratt”) idea de unión de cadenas en un array *comparison*.

¿Por qué KMP? *
■ Después de convertir el array numérico en un array de `-1, 0, 1` que
El problema se convierte en “oculto, =, >” entre elementos adyacentes
> un problema exacto de patrón de unión en una cadena entero - exactamente lo que
■ KMP está destinado.

-...

### 1.1 Java – `Solution.java `

``java
importar java.util*;

Solución de la clase pública {}

--------- Construye la matriz de lps (preprocesamiento de KMP) ----------
privado vacío estático buildLps(int[] pat, int[] lps) {
int m = pat.length;
int len = 0; // longitud del sufijo prefijo más largo anterior
lps[0] = 0; // lps[0] es siempre 0

por (int i = 1; i) {
si (pat[i] == pat[len]) {}
len++;
lps[i] = len;
i++;
. ♫ ... {
si 0) {
len = lps[len - 1];
. ♫ ... {
lps[i] = 0;
i++;
}
}
}
}

/* ----- API principal -----
public int countMatchingSubarrays(int[] nums, int[] pattern) {}
int n = nums.length;
int m = patrón. longitud;
(m == 0) retorno 0;

/* Construir el array “comparison” para los nums (tamaño n‐1) */
int[] cmp = nuevo int[n - 1];
para (int i = 0; i)
si (nums[i] se hicieron nums[i + 1]) cmp[i] = 1; // “conejo” → 1
si (nums[i]
más cmp[i] = 0; // “=” → 0
}

/* KMP requiere el patrón mismo, así que lo mantenemos como está. */
int[] lps = nuevo int[m];
buildLps(pattern, lps);

--------- Búsqueda de KMP en cmp-------- */
int i = 0; // index for cmp[]
int j = 0; // index for pattern[]
respuesta int = 0;

mientras que (i Ге cmp.length) {}
si (cmp[i] == patrón[j]) {}
i++; j++;
}

si (j == m) { /// un partido completo encontrado
respuesta++;
j = lps[j - 1]; // continuar buscando la próxima superposición
} más si (i Ге cmp.length & п cmp [i] != patrón[j]) {}
si (j!= 0) j = lps[j - 1];
i++;
}
}
respuesta de retorno;
}
}
`` `

■ **Compilación y funcionamiento* *
, ``bash
Solución javac. java
> java -jar leetcode. el arnés LeetCode llamará a ContMatchingSubarrays
" `

-...

### 1.2 Python – `solution.py `

``python
Solución de clase:
# ---------- Preprocesamiento de KMP...----------
def _build_lps(self, pat):
m = len(pat)
lps = [0] * m
longitud = 0
i = 1
mientras que yo me hice
si pat[i] == pat[length]:
longitud += 1
lps[i] = longitud
i += 1
más:
si la longitud!= 0:
longitud = lps[longitud - 1]
más:
lps[i] = 0
i += 1
Regreso lps

# ---------- API principal...--------
def countMatchingSubarrays(self, nums: List[int], patrón: List[int]) - título int:
n, m = len(nums), len(pattern)
si m == 0:
retorno 0

# Build the comparison array for nums (size n-1)
(n - 1)
para i en rango(n - 1):
si nums[i] [i + 1]:
cmp[i] = 1 # > >
elif nums[i] œ nums[i + 1]:
cmp[i] = -1 # "tratado"
más:
cmp[i] = 0 # "="

# Build KMP failure table
lps = self._build_lps(pattern)

# KMP search
I = j = 0
respuesta = 0
mientras que yo hice el favor.
si cmp[i] == patrón[j]:
i += 1
j += 1
si j == m: # partido completo
respuesta += 1
j = lps[j - 1]
elif i < > len(cmp) and cmp[i] != patrón[j]:
si j!= 0:
j = lps[j - 1]
más:
i += 1
respuesta
`` `

■ *Running*
, ``bash
■ Python -m solución de prueba unitaria. Py # arnés de prueba opcional
" `

-...

### 1.3 C++ – `solution.cpp `

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
--------- Preprocesamiento de KMP: construir la matriz de lps -------- */
vacio buildLps(cont vector identificadoint círculo palma, vector identificadoint
int m = pat.size();
lps.assign(m, 0);
int len = 0; // anterior sufijo de prefijo más largo
por (int i = 1; i) {
si (pat[i] == pat[len]) {}
len++;
lps[i] = len;
i++;
. ♫ ... {
si 0)
len = lps[len - 1];
más
lps[i] = 0, i++;
}
}
}

--------- API principal...------ */
int countMatchingSubarrays(vector identificadoint círculo nums, vector identificadoint círculo marginal patrón) {}
int n = nums.size(), m = pattern.size();
(m == 0) retorno 0;

/* Construir el array de comparación para nums (tamaño n-1) */
vector implicado cmp(n - 1);
para (int i = 0; i) {}
si (nums[i] se hicieron nums[i + 1]) cmp[i] = 1; // “ título”
si (nums[i]
más cmp[i] = 0; // “=”
}

/* Preprocesamiento KMP en el patrón */
vectores:
buildLps(pattern, lps);

* * Búsqueda de KMP */
int i = 0, j = 0, respuesta = 0;
mientras (i < cmp.size()) {}
si (cmp[i] == patrón[j]) {}
++i; ++j;
}

si (j == m) { // partido completo
++respuesta;
j = lps[j - 1];
} si (i < cmp.size() " п cmp[i] != patrón[j] {}
si (j!= 0)
j = lps[j - 1];
más
++i;
}
}
respuesta de retorno;
}
};
`` `

■ **Compilación**
, ``bash
, g++ -std=c+17 -O2 -pipe -static -s solution.cpp -o solución
" `

-...

## 2. Una visión rápida del enfoque óptimo

TENCIÓN TENIDO Tiempo ANTERIENTE Espacio ANTERIOR
Silencio------------------------
Silencio **Brute‐Force** Silencio **O(n · m)** Silencio O(1) Silencio Simple de escribir pero TLE en las pruebas de 105 tamaños. Silencio
Silencio **Sliding‐Window + Hash** Silencio **O(n)** Silencio O(n) Silencio Usa un hash ondulado; riesgo de colisión (rare pero posible). Silencio
Silencio **KMP on Comparison Array** Silencio **O(n + m)** Silencio **O(m)** Silencio libre de colisión, determinista, fácil de razonar. Silencio

### 2.1 Lo que parece el Array de Comparación

Por `nums = [1, 3, 2, 4]`:

`` `
1 0 3 → 1
3 Ø 2 → -1
2 > 4 → 1
`` `

Así que el array de comparación es `[1, -1, 1]`.
El patrón permanece `[1, -1, 1]` (exactamente los mismos valores).
Ahora la tarea es: *“cuántas veces aparece la cadena de enteros ‘pattern’
esta cadena de comparación?”* – una pregunta clásica de KMP.

-...

## 3. Blog Artículo – “Cracking LeetCode 3036 con KMP (Java, Pitón, C++)”

■ **Keywords**: *Leetcode 3036*, *Número de Subarrays que coinciden con un patrón II*, *KMP*, *Java*, *Python*, *C++*, * entrevista de codificación*, *diseño de algoritmo*, *prep* de entrevista de trabajo.

-...

#### 3.1 Introducción

■ **LeetCode 3036 – Número de subarrayos que coinciden con un patrón II**
√ es un problema engañosamente simple pero altamente valorado que prueba el candidato
Capacidad de reconocer patrones, transformar datos y aplicar un clásico
algoritmo de unión de cadenas (KMP).
■ Para cualquier persona que se prepare para entrevistas de codificación en las principales empresas tecnológicas, masterización
> este problema es un “must‐know” porque demuestra:

- Comprensión profunda de la manipulación de los rayos** y programación dinamica**.
- Capacidad para identificar un problema como una tarea oculta **estring-matching**.
- Competencia en **Java, Python y C+** – los tres idiomas más a menudo
solicitado en entrevistas.

-...

### 3.2 Declaración de problemas (Corta & Dulce)

■ Dados dos arrays enteros `nums` (tamaño *n*) y `pattern` (tamaño *m*),
■ contar cuántos submarinos contiguos de 'nums' tienen el **exacto mismo
patrón de dirección** como `pattern`.
■ El patrón direccional se define por comparaciones:
* `pattern[i] = 1` → el elemento sub-array en la posición *i* es **greater* *
* `pattern[i] = -1` → el elemento sub-array en la posición *i* es **less* *
* `pattern[i] = 0` → el elemento sub-array en la posición *i* es **igual* *

■ *Regresa el recuento total. *

-...

### 3.3 Why Brute‐ Fracasos de fuerza (buenas razones)

El algoritmo recto O(*n* · *m*) verifica cada sub-arrayo posible
y lo compara con el patrón.
Con limitaciones de hasta 100 000 elementos, esto se vuelve poco práctico:

``python
para empezar en rango(n - m + 1):
match = True
para k en rango(m):
si compare(nums[start + k], nums[start + k + 1]) != patrón[k]:
partido = Falso; descanso
`` `

Complejidad del tiempo: `O(105 · 105)` → **excede el límite de 1 segundo** en LeetCode.

-...

### 3.4 La vista clave – Convertirse en un rayo de comparación

1. **Construir un array de “dirección”** para `nums` de longitud `n-1`:
- ``Consiente' → `1`
- ``Objetivo' → 1
- `=` → `0`

2. **El patrón en sí es ya una secuencia de `1, -1, 0`**.
Por lo tanto, simplemente buscamos 'pattern' dentro del array de comparación.

3. **No hay memoria extra para la piratería**; sólo una transformación lineal de la
array original.

-...

## 3.5 ¿Por qué KMP es la herramienta correcta

- **Determinista**: A diferencia de los métodos basados en hash, KMP nunca falla debido a colisiones.
- **Eficiente**: Preprocesamiento tarda `O(m)` tiempo; la búsqueda toma `O(n)`.
**Simple**: La tabla de fracasos (`lps`) garantiza la progresión lineal incluso
después de una coincidencia.

-...

### 3.6 Aspectos destacados de la implementación

Silencio Idioma Silencio Clásico Silencioso Código Silencio
Silencio--------------
Silencio **Java** Silencioso `int[] cmp = nuevo int[n-1]` Silencio `si (nums[i] י nums[i+1]) cmp[i] = 1;` Silencio
Silencio **Python** Silencio Comprensión de la lista + ayudador KMP  durable `cmp[i] = 1 si nums[i] -1` Silencio
Silencio **C++** Silencio `vector interpretadointilo cmp(n-1);` TENIDO `cmp[i] = (nums[i] 1 : -1;`

■ **Tip**: En el arnés Java de LeetCode, asegúrese de que la firma del método coincida con
√ `conteo público intMatchingSubarrays(int[] nums, int[] pattern)`.

-...

### 3.7 Complexity Analysis (What Interviewers Love)

TENIDO TERRITORIO ANTERIOR ANTERIOR ANTERIOR KMP (Optimal)
Silencio------------------------------------------
Silencioso tiempo Silencioso `O(n·m)` Silencioso
Silenciosos en el espacio " O(1) " , Silencio

■ La complejidad lineal del tiempo garantiza que incluso las pruebas más difíciles con
*n* = 105 y *m* = 105 corren bajo unos pocos milisegundos.

-...

### 3.8 Pitfalls comunes " Good Bad " Practices

Silencio Pitfall Silencio
Silencio...
Silencio Olvídate de que el array de comparación tiene longitud *n‐1* TENIDO Use `if (i iere cmp.size())` guard. Silencio
Silencio Sobre-complicar usando 'int[][]` para rebanadas de 2-D tención Stick a un array de comparación de 1-D. Silencio
Silencio Usando un hash sin manipular colisiones ¦ Prefer KMP para la corrección garantizada. Silencio
← Mezclando “conejército” y “ < < > > > > > Semántica en el array de comparación. Silencio

-...

## 3.9 Real‐World Takeaway

■ **LeetCode 3036** es un excelente ejemplo de ** "reforma de la estructura de datos"**.
■ Muchos problemas de entrevista ocultan un núcleo de parpadeo de patrón; girando el problema
CIO en una forma algorítmica familiar (aquí, KMP) es una habilidad poderosa.
■ Aplicarlo en **Java, Python, C+**, y tendrás un versátil, probado
Solución que impresiona a los entrevistadores en Google, Amazon, Microsoft y más.

-...

### 3.10 Call to Action

■ Practicar las siguientes variaciones:

1. **Añada una nueva dirección** ( " 2 " que significa " diferencia " ) y
adapte el array de comparación en consecuencia.
2. ** Cambiar el requisito** a “al menos *k* coincidencias superpuestas”.
3. **Traducir la solución a Go** (para su próxima entrevista).

■ Recuerda: **El código bueno es elegante, correcto y rápido**.
■ La solución KMP arriba marca todas esas cajas.

-...

## 4. Conclusión

Tenemos:

- Realizar implementaciones de producción en Java, Python y C++.
- Mostrar la transformación de un problema de array-pattern a una búsqueda de KMP.
- Proporcionó un blog listo para publicar que destaca por qué masterizar LeetCode 3036
es esencial para el éxito de la entrevista de codificación.

¡Feliz codificación y buena suerte en tu próxima entrevista!