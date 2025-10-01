-...
Título: LeetCode 3362. Zero Array Transformation III -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

## 1. Código – Java / Python / C++ (Zero Array Transformation III)

``text
LeetCode 2719 – Zero Array Transformation III
`` `

Silencio Idioma Silencio Nombre del archivo Silencio Highlights Silencio
Silencio----------------------------
Silencio **Java** Silencioso `Solution.java` Silencioso Usos `Arrays.sort` + dos `PriorityQueue`s (máximo salto para fines, min‐heap para consultas ya utilizadas) Silencio
Silencio **Python** Silencio `solución.py` ¦ Utiliza `heapq` + dos contadores - uno para consultas activas, uno para intervalos "utilizados"  durable
Silencio **C+** Silencioso `Solution.cpp` Silencioso Usos `sort ' , `priority_queue hicisteint titulado `` (max‐heap) y un vector de los “créditos de la sentencia”

■ **NOTE** – Las tres implementaciones siguen la misma estrategia *greedy + line‐sweep* que garantiza el número mínimo de operaciones requeridas.
■ La respuesta es simplemente `totalQueries - usedQueries` (o el tamaño del montón que queda después del barrido).

-...

#### 1.1 Java Implementation

``java
// --------- LeetCode 2719 - Transformación de rayos cero III...
importar java.util*;

Solución de la clase pública {}
*
* @param Una variedad de enteros (nums)
* @param lista de consultas de [l,r] operaciones
* @retorno máximo número de consultas extraíbles o -1 si imposible
*/
int public int maxRemoval(int[] A, int[][ ] {
int n = A.length, q = queries.length;

// 1 / ⃣ Ordenar consultas por índice de inicio (l)
Arrays.sort(queries, (x, y) - título Integer.compare(x[0], y[0]));

// 2  Max Max‐heap para todos los fines de las consultas “disponibles”
PrioridadPregunta realizadaInteger confía h = nueva PrioridadQueue decir (Collections.reverseOrder());

// 3Ω⃣ endCount[i] – cuántas consultas escogidas terminan *después de* posición i
int[] endCount = nuevo int[n + 1];
int used = 0; // number of currently active consultas
int pos = 0; // index in queries[]

para (int i = 0; i)
// eliminar las consultas que acaban de terminar
utilizado -= endCount[i];

// añadir nuevas consultas que comienzan en o antes
mientras (posiciones)
h.offer(queries[pos][1]); // push end index
pos++;
}

// necesitamos decrementos A[i] en la posición i
mientras (utilizado) {}
si (h.isEmpty()
retorno -1;
}
int e = h.poll(); // elegir la consulta final más lejos
endCount[e + 1]++; // dejará de afectar después de e
us++; // ahora tenemos una consulta más activa
}
}

/* Consultas adicionales = todas las consultas que nunca fueron elegidas */
Devuelve las consultas. longitud - utilizada;
}
}
`` `

-...

### 1.2 Python Implementation

``python
# --------- LeetCode 2719 – Zero Array Transformation III...
importación heapq
de la importación Lista

Solución de clase:
def maxRemoval(self, A: List[int], consultas: List[List[int]]) int:
"
Greedy + line‐sweep con un max‐heap.
"
# 1 / 1 / } ordenar el índice inicial
consultas.sort()
n, q = len(A), len(queries)

# 2️ max‐heap for end of all "available" consultas
h = [] # pithon's heapq es un min‐heap - Usar negativos
end_cnt = [0] * (n +1) # cuántas consultas escogidas terminan después de i
utilizado = 0
pos = 0

para i en rango(n):
# 3 comentarios de las consultas de liberación que han terminado
utilizado -= end_cnt[i]

# 4️ add new queries that start now
q y consultas [pos] [0] <= i:
heapq.heappush(h, -queries[pos][1] # store negative to simulate max‐heap
pos += 1

# 5downs Necesitamos decrementos A[i] en el índice i
mientras se utilizaba A[i]:
si no h o -h [0]
retorno -1
e = -heapq.heappop(h) # pick farthest-ending query
end_cnt[e + 1] += 1
usados += 1

Las consultas restantes son las extraíbles
devolver len(h)
`` `

-...

#### 1.3 C++ Aplicación

``cpp
// --------- LeetCode 2719 - Transformación de rayos cero III...
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxRemoval(vector asignadoint A, vector alcanzadovector realizador realizado en búsquedas individuales {}
int n = (int)A.size(), q = (int)queries.size();
sort(queries.begin(), queries.end()); // sort by start l

prioridad_queue hicisteint confianza h; // max‐heap of end
vector implicado usuario finalCnt(n + 1, 0); // cuántas consultas escogidas terminan después de i
int used = 0; // number of active queries
int pos = 0; // index in queries[]

para (int i = 0; i) {}
// liberación consultas terminadas
utilizado -= endCnt[i];

// añadir nuevas consultas disponibles
mientras (posiciones)
h.push(queries[pos][1]); // push end index
++pos;
}

// necesidad A[i] decrementos en la posición i
mientras (utilizado) {}
si (h.empty()
retorno -1;
int e = h.top(); h.pop();
endCnt[e + 1]++; // dejará de afectar después de e
++utilizados;
}
}
// Todas las consultas que nunca fueron elegidas son extraíbles
(int)h.size();
}
};
`` `

Los tres códigos funcionan en **O(n + q) log q)** tiempo y **O(n + q)** espacio, cómodamente dentro de los límites de 1 s / 256 MB para el problema.

-...

## 2. Blog Artículo – “Zero Array Transformation III: The Good, The Bad, The Ugly”

■ **Keywords** – LeetCode, Zero Array Transformation III, problema de codificación de entrevistas, algoritmo codicioso, cola prioritaria, barrido de línea, Java, Python, C++, entrevista de trabajo, estructuras de datos, algoritmo, búsqueda de empleo, entrevista de programación, entrevista de datos.

-...

#### 2.1 Introduction

Si estás cazando un rol de ingeniería de software, una de las maneras más rápidas de mostrar tus cómputos algorítmicos es haciendo frente a un problema *LeetCode* que combina los conocimientos de datos estructura con el razonamiento codicioso. **Zero Array Transformation III** es un escaparate perfecto: es un problema moderno y amigable para entrevistas que requiere una solución limpia y óptima y ofrece una gran conversación de inicio con su futuro empleador.

-...

### 2.2 Declaración de problemas (refrascada)

■ **Given**:
- Un array `nums` de longitud `n` (0-indexed), cada elemento `nums[i]` es un entero no negativo.
Una lista de preguntas. Cada consulta es un par " [l, r] " que significa “destruir todos los elementos `nums[l] ... nums[r] ' por 1”.
■
■ **Task**: Encontrar el número máximo de consultas que se pueden eliminar mientras que todavía se puede reducir cada `nums[i] a cero o debajo aplicando *algunos* de las consultas restantes (cada consulta se puede utilizar al máximo una vez).
■ Si es imposible hacer cada elemento cero, vuelva `-1`.

**Constraints* *
- 1 ≤ n, q ≤ 5 · 104
- `0 ≤ nums[i] ≤ 5 · 104
- No.

-...

### 2.3 Why This Problem is Interview‐Friendly

1. **Overlaps " Greedy** – Usted tiene que decidir *que* consultas a utilizar, y esa decisión depende del *cubrimiento* de cada consulta.
2. **Priority Queue Mastery** – Muchos candidatos se atascan en “cómo elegir la consulta correcta” – una prueba clásica de conocimiento prioritario.
3. **Line Sweep Intuition** – Una combinación perfecta de barrido y codicioso que se ve limpio en un escenario de pizarra blanca.
4. **Space " Time Trade‐off** – Solving it in `O(n+q) log q)` demuestra una conciencia de rendimiento asintotico.

-...

#### 2.4 Solution Overview

1. **Transformar el problema** – En lugar de buscar *extra* consultas directamente, computamos el *mínimo* número de consultas requeridas para cero el array.
*Respuesta = `totalQueries - minimumUsedQueries`.*

2. **Line‐sweep de izquierda a derecha* *
- Mientras caminamos por el array, mantenemos:
- `utilizado ' - el número de consultas activas que actualmente están cubriendo la posición `i.
- Un max-heap (`h`) conteniendo los índices finales de *todas las consultas disponibles* que comienzan antes o en `i.
- En cada índice `i` necesitamos exactamente 'nums[i]` decrementos.
- Si `utilizado  nu nums[i]`, escogemos codiciadamente la consulta que termina más lejos a la derecha (`h.top()`), porque nos mantiene “cubiertas” por el tramo más largo posible.
- Cuando termina una consulta elegida, registramos que dejará de cubrir la matriz *después* su índice final, para que podamos decrementar más adelante `utilizado`.

2. ** Manejo del caso de Edge** –
- Si en cualquier momento el montón está vacío o el índice final más lejano de la consulta es ``, la matriz no puede ser cero → retorno `-1`.

3. **Extracción de resultados** – Después del barrido, el montón sostiene todas las consultas que fueron **nunca** elegidas. Esos son exactamente los extraíbles.

-...

### 2.5 Step‐by‐Step Walk‐Through (Java Pseudocode)

``text
1. preguntas de tipo l
2. h = max‐heap de extremos
3. endCount = [0 ... n] // cuántas consultas escogidas terminan después de que yo
4. utilizado = 0, pos = 0
5. para mí en 0 ... n-1:
usada -= endCount[i] // liberación consultas terminadas
q " consultas [pos].l
h.push(queries[pos].r) // nueva consulta disponible
pos += 1
mientras se utiliza  nu nums[i]:
si h.isEmpty o h.peek()
e = h.pop() // consultas de extremo
endCount[e+1] += 1 // se detendrá después de e
usados += 1
6. total de retorno
`` `

Los fragmentos de código Java, Python y C++ en la primera sección implementan este algoritmo en un solo paso.

-...

### 2.6 The Good

¿Qué es impresionante? Silencio
Silencio...
Silencio **Optimal** – La elección codictiva “pick the query end farthest” es provablemente óptima. Silencio
Silencio **claritud** – Un solo bucle, dos simples estructuras de datos; puedes dibujar la lógica en menos de 30 segundos. Silencio
TEN **Language‐agnostic** – Funciona igualmente bien en Java, Python y C++ – perfecto para una pantalla de teléfono *técnica* donde puedes cambiar idiomas. Silencio
Silencio **Test-ready** – Escriba `unittest`/`pytest`/`gtest` en minutos para mostrar su solución pasa todos los casos de esquina. Silencio

-...

### 2.7 The Bad

Silencios comunes
Silencio...
Silencio **Pensando en “removear todo menos una consulta”** – No darse cuenta de que necesitamos el *minimo* conjunto de consultas. Silencio
Silencio **Escaneo de línea + selección de fuerza bruta** – O(`n·q`) soluciones de tiempo en los casos de prueba más grandes. Silencio
Silencio ** Orientación incorrecta del montón** – Utilizando un min-heap donde se requiere un máximo-heap conduce a la selección de la consulta "wrong" y bucles infinitos. Silencio
TEN **Ignorando los créditos finales** – Olvídate de marcar cuando una consulta elegida deja de cubrir lleva a resultados dobles y incorrectos. Silencio

-...

### 2.8 The Ugly

■ *“¿Y si la matriz es gigantesca? ¿Y si las consultas son demasiados? ¿Cómo manejo los casos de borde?”*

En entrevistas del mundo real se puede encontrar:

* Valores muy altos* El avaricioso todavía funciona; sólo necesita suficientes consultas de cobertura.
- **Cobertura de separación** – Si muchas consultas son cortas y el array tiene un valor enorme en algún índice, rápidamente llegarás a la rama '-1' – un buen momento para discutir “por qué es imposible”.
- **Presión de memoria** - Un vector ingenuo de tamaño `n·q` explotará. El truco de 'endCount' mantiene la memoria lineal.

-...

### 2.9 Cómo hablar En una llamada

1. **Sketch la línea de barrido** – Dibujar una línea de índice, colocar todos los intervalos de consulta, y señalar los intervalos “disponibles” vs “elegidos”.
2. **Explicar la regla avaricia** – “Siempre usamos el intervalo que se extiende más lejos porque mantiene nuestras opciones abiertas durante el mayor tiempo posible. ”
3. **La mención del montón** – “La ‘PrioridadQueue’ de Java es ideal; el ‘heapq’ de Python con valores negados funciona también. ”
4. **Mostrar las matemáticas** – “El tiempo de descanso es `O(n+q) log q)` porque cada empuje/pop es 'log q`. La memoria es `O(n+q)` porque mantenemos una simple matriz de contadores. ”
5. **Cobertura de prueba de alto nivel** – “Caso de emergencia: todos los ceros → respuesta = `q`. Caso imposible → `-1`.

-...

### 2.10 TL;DR for Your Resume

■ * Transformación de rayos de mar III*
• Greedy + barrido + max-heap
• `O(n+q) log q)` time, `O(n+q)` espacio
• Implementado en Java, Python y C++ (listo para entrevista)

Añadir esto a su cartera, ejecutarlo contra los *Casos de Prueba de Muestra* de LeetCode, y tendrá una historia lista para compartir que muestra que puede *leer* un array, *pensar* sobre intervalos superpuestos, y *implement* una solución óptima, todo dentro de un solo pase.

-...

## 3. Lista de verificación de inicio rápido para su entrevista

1. **Leer el problema** – subrayar “número mínimo de consultas requeridas” vs “máximo desmontable”.
2. **Respuestas por índice de inicio** – O(q log q).
3. **Sweep de izquierda a derecha** – Mantener un contador de consultas activas.
4. **Use un max‐heap** – Elija el intervalo más lejano cuando necesite más cobertura.
5. **Release consultas terminadas** – Subtract from the active counter using `endCount[i]`.
6. **Retorno de `totalPreguntas - usadoPreguntas** - Esa es la respuesta que te piden.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀