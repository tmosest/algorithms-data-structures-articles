-...
Título: LeetCode 960. Eliminar columnas para hacer clasificadas III -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Problema – LeetCode 960: * Columnas completas para hacer clasificadas III*

# Objetivo #
Dada una serie de `n` cuerdas de igual longitud `m`, elimine el número mínimo de columnas para que **cada** cadena restante esté en orden lexicográfico no disminuyente (es decir, sus caracteres están ordenados de izquierda a derecha).

Silenciosidad involuntaria involuntaria
Silencio----------------------------
Silencio 1 Silencioso `["babca", "bbazb"] TENIDO `3` TENIDO Suprímase columnas `0,1,4` → `["bc", "az"]. Silencio
TENIDO 2 TENIDO `[edcba]` ANTE `4` TEN cualquier columna izquierda rompería el orden. Silencio
Silencio 3 Silencio `["ghi","def","abc"]` Silencio `0` Silencio Todas las filas ya clasificadas. Silencio

Limitaciones
`` `
1 ≤ ≤ 100
1 ≤ ≤ 100
strs[i] consiste en minúsculas letras en inglés
`` `

-...

## 2. Intuición – Subsecuencia de Columna Valide más larga

Si guardamos un subconjunto de columnas, deben respetar la regla de orden **para todas las filas**.
Piense en cada columna como un “caracter” y queremos la subsecuencia más larga de las columnas que es **compatible**:

`` `
Columna j puede preceder columna i
≤ strs[i]
`` `

Si encontramos la subsecuencia más larga (llamada L), entonces las eliminaciones mínimas son `m - L`.

El problema es esencialmente la subsequencia de aumento más larga (LIS)** en el conjunto de columnas con una comparación personalizada.
Debido a que `m ≤ 100`, una simple `O(m2 · n)` solución de programación dinámica es lo suficientemente rápida.

-...

## 3. Algoritmo (Programación Dinámica)

`` `
dp[i] = longitud de la subsequencia válida más larga que termina en la columna i
respuesta = 0

para i = 0 ... m-1
dp[i] = 1 // subsequence of length 1 (just column i)
para j = 0 ... i-1
si la columna j puede preceder la columna i // comprobar todas las filas
dp[i] = max(dp[i], dp[j] + 1)
respuesta = max(respuesta, dp[i])

retorno m - respuesta
`` `

*Comprobando “column j puede preceder la columna i”*
Ábrete todas las filas.
Si cualquier `strs[r][j] ¢ strs[r][i]`, el par es inválido → ruptura.
Si todas las filas pasan, el par es válido.

Complejidad del tiempo: `O(m2 · n) `
Complejidad espacial: `O(m)`

-...

## 4. Implementaciones de referencia

#### 4.1 Java

``java
importar java.util*;

Solución de la clase pública {}
public int minDeletionSize(String[] strs) {
int n = strs.length; // número de filas
int m = strs[0].length(); // número de columnas

int[] dp = nuevo int[m];
int best = 0;

para (int i = 0; i)
dp[i] = 1; // al menos esta columna solo
para (int j = 0; j) {}
si (puedePrecede(estrs, j, i) {
dp[i] = Math.max(dp[i], dp[j] + 1);
}
}
mejor = Math.max(best, dp[i]);
}
volver m - mejor; // columnas para eliminar
}

* Regresar verdadero si la columna j puede preceder la columna i para todas las filas */
booleano privado precede(String[] strs, int j, int i) {
para (String s : strs) {
si (s.charAt(j) {}
devolver falso;
}
}
retorno verdadero;
}
}
`` `

-...

#### 4.2 Python

``python
Solución de clase:
def min Size(self, strs: List[str]) - int:
n, m = len(strs), len(strs[0])
*m
mejor = 0

para i en rango(m):
para j en rango(i):
si todo (s[j] <= s [i] para s en ptrs:
dp[i] = max(dp[i], dp[j] + 1)
mejor = max(best, dp[i])

regreso m - mejor
`` `

-...

#### 4.3 C++

``cpp
Clase Solución {
public:
int minDeletionSize(vector seleccionados) {
int n = strs.size();
int m = strs[0].size();
vector implicado dp(m, 1);
int best = 0;

para (int i = 0; i) {}
para (int j = 0; j)
bool ok = verdadero;
para (int r = 0; r) {}
si (strs[r] [j]
}
si (ok) dp[i] = max(dp[i], dp[j] + 1);
}
mejor = max(best, dp[i]);
}
retorno m - mejor;
}
};
`` `

-...

## 5. El Bien, El Mal, El Mal

Silencio Silencio
Silencio------------Prince------
Silencio **Problema Entendimiento** Silencio Clear: encontrar mínimas supresiones → más larga subsequence de la columna válida Mis-reading “row” vs “column” ordering → solución errónea ← Sobre-optimizar con estructuras de datos elegantes cuando `m ≤ 100 ` Silencio
Silencio ** Algorithm Choice** Silencio Simple DP (`O(m2·n)`) es rápido y fácil de razonar  Más complejo LIS con árbol de segmento es innecesario ← Tratar de usar betmasks o bitset DP → overkill ←
Silencio **Edge Cases** Silencio Handles `m = 1`, todas las filas ya clasificadas ¦ Olvidando subtractarse de `m` → respuesta incorrecta Silencio No revisar todas las filas para cada par → bugs silenciosos
Silencio **Estilo de codificación** ← Ayudante limpio `canPrecede` mejora la legibilidad ¦ Los bucles inline se vuelven difíciles de depurar ← Mixing 0‐based and 1-based indices → off-by-one errors TEN
Silencio **Testing** Silencio Pruebas de la unidad para muestras, casos aleatorios Silencio No hay pruebas → confianza bajo tención Stress‐testing on 100x100 datos aleatorios
Silencio **Complejidad** Silencio Linearitmic en la práctica (tiny constants) Silencio O(m3) DP would TLE ¦ Memoria soplado con la matriz de `m2 cuando no es necesario

**Takeaway:** Mantener la solución simple, probar a fondo, y recordar que las restricciones del problema permiten una solución DP limpia.

-...

## 6. SEO‐Optimized Blog Artículo

■ *Título*
■ * Columnas completas para hacer clasificadas III – LeetCode 960 – Java, Python, C++ DP Solution & Interview Tips*

■ **Meta Descripción (Ω155 chars):**
■ Master LeetCode 960 “Delete Columns to Make Sorted III” con una clara solución O(m2·n) DP en Java, Python y C++. Aprende las partes buenas, malas y feas de las entrevistas de codificación.

-...

### 1. Introducción

Si estás preparando entrevistas de ingeniería de software, **LeetCode 960 – Eliminar las columnas para hacer clasificadas III** es una grapa. El reto prueba su capacidad para pensar en las subsecuencias, programación dinámica y manejo cuidadoso de datos multidimensionales. A continuación, caminamos a través de una solución DP limpia, proporcionamos implementaciones en **Java**, **Python**, y **C+**, y discutir errores comunes que pueden costar en una entrevista.

### 2. Recaptación de problemas

Dado un conjunto de cadenas de longitud igual, podemos eliminar cualquier conjunto de índices de columna. Después de las eliminaciones, **toda fila** debe ser ordenada en orden no-disminución. Devuelve el número mínimo de eliminaciones necesarias.

■ Ejemplo
"Babca" → Eliminar columnas `{0,1,4}` → Resultado `["bc","az"] → **3 eliminaciones**.

### 3. ¿Por qué una subsecuencia creciente más larga (LIS) en las columnas?

Si guardamos un subconjunto de columnas, deben respetar la regla de orden **para todas las filas**.
Así podemos tratar cada columna como una “carta” y buscar la subsequencia más larga de las columnas que es compatible: para cualquier columna anterior `j` y posterior columna `i`, todas las filas satisfacen `estrs[r] [j] ≤ strs[r][i].

La longitud máxima `L' de tal subsequence nos dice cuántas columnas podemos guardar. La respuesta es simplemente `m - L`.

Debido a que las limitaciones (`m, n ≤ 100`) son pequeñas, un enfoque de programación dinámico directo es suficiente.

### 4. The DP Formula

`` `
dp[i] = 1
para J en [0, i]
si la columna j puede preceder i (ver todas las filas):
dp[i] = max(dp[i], dp[j] + 1)
`` `

La condición de ayudante “column j puede preceder i” significa:
``text
[j] ≤ strs[r][i]
`` `
Si alguna fila viola esto, el par es inválido.

La respuesta es `m - max(dp)`.

### 5. Código en 3 idiomas

##### Java
``java
Solución de la clase pública {}
public int minDeletionSize(String[] strs) {
int n = strs.length, m = strs[0].length();
int[] dp = nuevo int[m];
int best = 0;

para (int i = 0; i)
dp[i] = 1;
para (int j = 0; j) {}
si (puedePrecede(estrs, j, i) {
dp[i] = Math.max(dp[i], dp[j] + 1);
}
}
mejor = Math.max(best, dp[i]);
}
retorno m - mejor;
}

booleano privado precede(String[] strs, int j, int i) {
para (String s : strs) {
si (s.charAt(j)
}
retorno verdadero;
}
}
`` `

#### Python
``python
Solución de clase:
def min Size(self, strs: List[str]) - int:
n, m = len(strs), len(strs[0])
*m
mejor = 0

para i en rango(m):
para j en rango(i):
si todo (s[j] <= s [i] para s en ptrs:
dp[i] = max(dp[i], dp[j] + 1)
mejor = max(best, dp[i])

regreso m - mejor
`` `

###### C++
``cpp
Clase Solución {
public:
int minDeletionSize(vector seleccionados) {
int n = strs.size(), m = strs[0].size();
vector implicado dp(m, 1);
int best = 0;

para (int i = 0; i) {}
para (int j = 0; j)
bool ok = verdadero;
para (int r = 0; r)
si (strs[r] [j]
si (ok) dp[i] = max(dp[i], dp[j] + 1);
}
mejor = max(best, dp[i]);
}
retorno m - mejor;
}
};
`` `

### 6. Análisis de la complejidad

- **Tiempo:** `O(m2 · n)` – en la mayoría de `100 * 100 * 100 = 1.000.000 de operaciones, insignificante.
- **Espacio: ** `O(m)` - un array DP.

### 7. Errores de entrevista común

¿Por qué no se puede arreglar la vida?
Silencio--------------------------
Silencio **Asumiendo que sólo las filas adyacentes importan** Silencio La condición debe mantener para *toda* fila. ANTERIOR sobre todas las filas al comprobar un par. Silencio
Silencio **Using `m2` but ignoring `n`** tención Las comparaciones de filas negativas hacen que el DP sea inválido. ← En el bucle de `j ' i `, iterate over all rows. Silencio
TEN **Mis‐indexing** Ø Off‐por-one errores son comunes con cadenas basadas en 0. TENIDO A los índices 0-basados en todo. Silencio
Silencio **Retorno de `m - max(dp)` incorrectamente** Silencio Si te olvidas de restar de `m`, la respuesta será `max(dp)` en lugar. Silencio Recordar que eliminaciones = columnas dejados. Silencio

### 8. Por qué esto importa para su cuidador

* Programación Dinámica* Dominar a DP en un array 2-D muestra un pensamiento algoritmo fuerte —esencial para backend, ingeniería de datos, o roles completos.
- **Multi‐Language Skillset:** Saber cómo implementar la misma lógica en **Java**, **Python**, y **C++** muestra versatilidad; los reclutadores valoran a los candidatos que pueden cambiar contextos.
*Descomposición del proyecto* Reconocer la analogía de LIS muestra su capacidad de abstraer un requisito complejo en un subproblema más simple, una habilidad de entrevista apreciada.

### 9. Próximos pasos

1. Ejecute las soluciones proporcionadas contra casos de prueba aleatorios (las pruebas ocultas de LeetCode son a menudo grandes).
2. Añade tus propias pruebas de unidad para escenarios de borde (`m=1`, ya ordenados, completamente sin surtido).
3. Práctica explicando la fórmula DP en voz alta – entrevistadores quieren que pienses en el lugar.

### 9. Conclusión

Leet El código 960 es una introducción suave y potente a la programación dinámica de matrices. Al tratar el problema como LIS en las columnas y utilizando un `O(m2·n)` limpio DP, puedes resolverlo eficientemente en cualquier idioma. Mantenga el código simple, maneje todas las filas y evite las trampas comunes. Buena suerte rompiendo este problema - y su próxima entrevista de ingeniería de software!

-...

#### 9.1. Lista rápida para entrevistadores

- **Leer el aviso cuidadosamente** - columnas vs filas.
- Explique su enfoque antes de la codificación.
- ** Funciones de ayuda para la lectura.
Pruebe su solución mentalmente en todas las muestras.
- *La complejidad de la mención* para mostrar conciencia.

-...

¡Feliz codificación!

-...

■ *¿Quieres más preparación para la entrevista? Suscríbete a nuestro boletín semanal para análisis a fondo de problemas LeetCode, patrones de algoritmos y historias de entrevistas reales. *

-...

#### 9.2 Palabras clave

- Eliminar columnas para hacer clasificadas III
- LeetCode 960
- Solución del DP
- Programación dinámica
- Más larga subsequence
- Aplicación de Java
- Solución de pitón
- algoritmo C++
- Entrevista de ingeniería de software
- Coding interview patterns

-...

**End of article. #