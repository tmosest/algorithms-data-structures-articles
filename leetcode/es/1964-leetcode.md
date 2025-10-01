-...
Título: LeetCode 1964. Encuentra el Curso de Obstáculo Valido más largo en cada posición -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

## 1. LeetCode 1964 – *Encuentra el Curso de Obstáculo Valide más largo en cada posición*
**Hard** Silencio O(n log n) Silencio Java Silencio Python Silencio C++

■ Se le da un array `obstacles`.
■ Por cada índice `i` debe elegir una subsequencia que **incluye** `obstacles[i]`,
не es ** no disminuyendo**, y tiene la longitud máxima posible.
■ Devuelve un array `ans` donde `ans[i]` es esa longitud máxima.

La manera clásica de resolver esto es **Clasificación de la Paciencia** (el mismo truco que se utiliza para
Subsequence de aumento más largo).
Mantenemos un array auxiliar `dp` donde `dp[len]`. es el final más grande posible
valor* de una subsequencia no disminuyente de longitud `len + 1` que ya se ha visto.
Mientras escaneamos los obstáculos de izquierda a derecha buscamos binaria para la posición
donde el obstáculo actual encajaría en `dp`.
Esa posición + 1 es la respuesta para este índice.
Si el obstáculo extiende la subsequencia más larga hasta ahora lo empujamos hacia 'dp',
de lo contrario reemplazamos el valor existente – el reemplazo garantiza que el
subsequence end value stays as small as possible, which keep the array óptimo
para futuros elementos.

A continuación encontrará una implementación limpia y lista para la producción en **Java**, **Python** y **C+**.

■ ¿Por qué los SEO-tags? * *
■ Si estás apuntando a un rol codicioso, LeetCode 1964 es una entrevista perfecta
Ejemplo. Destacando “LeetCode 1964 solución Java”, “Curso de Obstáculo más largo
“Binary Search O(n log n)” etc. en el artículo hará que el rango post
CIO para los reclutadores que buscan candidatos inteligentes.

-...

### 1.1 Java ( 2024‐Style)

``java
Clase Solución {
int[] longestObstacleCourseAtEachPosition(int[] obstacles) {}
int n = obstáculos. longitud;
int[] dp = nuevo int[n]; // dp[len] – menor valor final de longitud len+ 1
int[] ans = nuevo int[n];
int len = 0; // la longitud más larga actual

para (int i = 0; i)
// estilo superior-bound: primer índice con los obstáculos de valor
int pos = Arrays.binarySearch(dp, 0, len, obstacles[i] + 1);
si (pos ecto 0) pos = -pos - 1; // standard upperBound

// Actualizar la matriz dp
dp[pos] = obstáculos[i];

// si aprobamos al final, aumentar la longitud global
si (pos == len) len++;

ans[i] = pos + 1; // longitud de subsequencia que termina en i
}
devolver los ans;
}
}
`` `

*¿Por qué `obstacles[i] + 1`? *
Utilizamos 'upper_bound' (primer elemento ** más alto que la clave).
Agregar `1` al obstáculo convierte el requisito de “no disminuir” en un estricto
creciente búsqueda.

-...

### 1.2 Python ( 3.10+ )

``python
de la importación de bisect_right
de la importación Lista

def longestObstacleCourseAtEachPosition(obstacles: List[int]) - título List[int]:
"
Paciencia clasificación + búsqueda binaria (O(n log n)).
"
dp = [] # dp[len] – menor valor final para subsequence of length len+ 1
ans = []

para x en obstáculos:
# bisect_right devuelve el primer índice con valor √ x (ajuste)
pos = bisect_right(dp, x)
si pos == len(dp):
dp.append(x)
más:
dp[pos] = x
ans.append(pos + 1)

Retorno
`` `

*Tip:* `bisect_right` es exactamente el `upper_bound` que necesitamos.
Si accidentalmente usas `bisect_left` la respuesta será **off por uno**.

-...

### 1.3 C++ (Moderno, estilo 2024)

``cpp
Incluido el título
#include >

Clase Solución {
public:
std:::vector obtenidosint confianza longestObstacleCourseAtEachPosition(std:::vector correspondint implica obstáculos) {}
std:::vector obtenidosint titulada dp; // dp[len] – valor final mínimo de longitud len+ 1
std::vector obtenidosint titulada ans;
para (int x : obstáculos) {}
/ // upper_bound: primer elemento
auto it = std::upper_bound(dp.begin(), dp.end(), x);
int pos = it - dp.begin();
(it == dp.end()))
dp.push_back(x); // extender la longitud más larga
más
*it = x; // reemplazar para mantener el valor final mínimo
ans.push_back(pos + 1); // longitud de subsequencia que termina en este índice
}
devolver los ans;
}
};
`` `

■ **¿Por qué 'upper_bound' en lugar de 'lower_bound'?* *
■ Queremos una subsecuencia que no disminuye.
" upper_bound " guarantees we insert *after* all elements equal to `x`, ensuring the
La subsequencia de √ no disminuye y la matriz de dp sigue siendo óptima.

-...

## 2. El Bien, el Mal y el Ugly – Una Guía de Entrevista de 2024

■ *Un artículo completo, amigable con SEO, que busca trabajo para cualquier persona que se prepare para un
Entrevista técnica. *

-...

### 2.1 Introduction – Why LeetCode 1964 Matters

- **Keyword-rich**: “LeetCode 1964”, “Curso de Obstáculo Valide más largo”, “Entrevista del PPD
problema”, “entrevista de codificación”, “ algoritmo de entrevista de trabajo”, “Java/Python/C++”.
- Búsqueda de reclutadores para candidatos que puedan resolver *Hard* LeetCode preguntas con
código limpio y eficiente.
- LeetCode 1964 es un reto de programación dinámica del mundo real que aparece en
muchos bancos de preguntas de entrevista.

-...

### 2.2 El Bien - Lo que hace que este problema sea una gran entrevista

Feature Silencio Por qué Ayuda a vivir
Silencio...
Silencio ** analogía del mundo real** Silencio cursos de obstáculo espejo problemas de planificación de la vida real (por ejemplo, programación). Silencio
Silencio ** Escalas a O(n log n)** Silencio Demuestra el conocimiento del candidato de estructuras de datos avanzadas. Silencio
Silencio **Language‐agnostic** Silencioso en Java, Python, C++. Perfecto para carteras multi-idioma. Silencio
Silencio **No-trivial DP** Silencio Muestra la capacidad de transformar una ingenua solución O(n2) en una óptima. Silencio

■ *Resultado*: Usted mostrará a los reclutadores que puede pasar de una idea de fuerza bruta a una
Un algoritmo óptimo en menos de un minuto.

-...

### 2.3 Los malos – los saltos comunes

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio...
Silencio usando **`lower_bound`** (primer `conejo=`) en lugar de ** " upper_bound "** (primer ` ' ) Silencio `obstacles[i] ' debe ser **incluido**; necesitamos un índice *principalmente creciente* para el nuevo valor. Silencio
Silencio Olvídate de añadir **1** al resultado de la investigación binaria tención `pos` es un índice basado en cero; `ans[i] = pos + 1`. Silencio
Silencio Modificación de la matriz original de `obstacles` para mantener `dp` separado para evitar corromper los datos de entrada. Silencio
Silencio No inicializar el tamaño de `dp` correctamente ANTE `dp` puede ser un vector de longitud `n` (máximo posible longitud de subsequencia). Silencio
TEN Utilizar la recursión para la búsqueda binaria en idiomas con pequeña pila TEN Utilizar la búsqueda binaria iterativa para permanecer dentro de los límites de la pila. Silencio

-...

### 2.4 The Ugly – Edge Cases That Sneak in

1. **Todos los elementos son iguales*
Ejemplo: " [5,5] " → respuesta `[1,2,3,4]`.
*¿Por qué rompe soluciones ingenuas?* Porque todos los elementos pueden ser anexados;
sigue creciendo.

2. **Estrictamente decreciente array**
Ejemplo: `[4,3,2,1]` → respuesta `[1,1,1,1]`.
La investigación binaria siempre regresa `0`, así que nunca extendemos `dp`.

3. ** Valores de entrada más altos (hasta 109)* *
Asegúrese de utilizar `long`/`long `` si estás tentado a añadir 1 al valor
antes de buscar. El algoritmo en sí solo necesita comparación, no aritmética.

-...

### 2.5 Quick‐ Código de inicio (Java / Python / C++)

■ **Copy‐paste listo** – simplemente caer en su IDE o una ventana LeetCode “submitir”.

``java
// Java 17+ (formato LeetCode)
Clase Solución {
int[] longestObstacleCourseAtEachPosition(int[] obstacles) {}
int n = obstáculos. longitud;
int[] dp = nuevo int[n];
int[] ans = nuevo int[n];
int len = 0; // longitud más larga vista hasta ahora

para (int i = 0; i) {}
int pos = binariaSearch(dp, 0, len, obstacles[i]); // first ⇩
dp[pos] = obstáculos[i];
si (pos == len) len++;
ans[i] = pos + 1;
}
devolver los ans;
}

int privado binarioSearch(int[] dp, int left, int right, int target) {}
int l = izquierda, r = derecha;
mientras (l <= r) {
int m = (l + r) 1;
si (dp[m] <= target) l = m + 1;
r = m - 1;
}
retorno l; // índice superior
}
}
`` `

``python
# Python 3.10+ (formato LeetCode)
de la importación de bisect_right
de la importación Lista

def longestObstacleCourseAtEachPosition(obstacles: List[int]) - título List[int]:
dp = [] # valor final más pequeño para cada longitud
ans = []

para x en obstáculos:
pos = bisect_right(dp, x) # primer índice con valor
si pos == len(dp):
dp.append(x)
más:
dp[pos] = x
ans.append(pos + 1)

Retorno
`` `

``cpp
// C+17 (formato LeetCode)
Incluido el título
#include >

Clase Solución {
public:
std:::vector obtenidosint confianza longestObstacleCourseAtEachPosition(std:::vector correspondint implica obstáculos) {}
ptd::vector obtenidosint título dp; // valor final mínimo para cada longitud
std::vector obtenidosint titulada ans;

para (int x : obstáculos) {}
auto it = std::upper_bound(dp.begin(), dp.end(), x);
int pos = it - dp.begin();
(it == dp.end()))
dp.push_back(x);
más
*it = x;
ans.push_back(pos + 1);
}
devolver los ans;
}
};
`` `

-...

## 3. Wrap‐Up – Tome el siguiente paso

- **Mostrar**: Agregue soluciones LeetCode 1964 a su cartera de GitHub.
**Explicar**: Use los puntos de bala del artículo en su curriculum vitae: “Solved LeetCode 1964
en Java con O(n log n) DP” etc.
- **Practice**: Repita la lógica de búsqueda binaria en similar "DP + búsqueda binaria"
problemas (por ejemplo, “Maximum Score from Removing Stones” o “Longest Increasing
Subsequence”).
- **Entrevista**: Cuando se pide un problema *Hard*, mencione el obstáculo
analogía, luego describir el DP de Patience-Sorting en 30 segundos.

■ **Su próximo Recruiter‐Ready Move** – enviar estas soluciones, publicar este artículo,
√≥n y ver la entrevista ofrece rodar.

-...

■ Pensamiento final**: Mastering LeetCode 1964 demuestra que no eres sólo un
> coder; usted es un solucionador de problemas estratégicos** que puede navegar “el bueno,
> mal, y feo” de diseño de algoritmos – exactamente lo que cualquier función de software senior necesita.