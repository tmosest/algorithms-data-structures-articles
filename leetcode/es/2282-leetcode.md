-...
Título: LeetCode 2282. Número de personas que pueden ser vistos en una rejilla -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🧩 2282. Número de personas que pueden ser vistos en una rejilla
### 📌 Problema Resumen
Se le da una matriz de 'm x n' ' alturas' donde cada entrada es un entero positivo.
A person at `(row1, col1)` puede ver a otra persona en `(row2, col2) ` Sólo si

* `(row1 == row2 ' pl1 # O # `(row1 < row2
* Cada persona estrictamente entre ellos es más corta que **ambos** de ellos.

Devuelve una matriz `respuesta` donde `respuesta[i][j]` es el número de personas que la persona en `(i, j)` puede ver.

■ **Constraints**
√≥ - `1 ≤ alturas. longitud, alturas[i].length ≤ 400`
[j] ≤ 105 `

-...

## 🎯 Why This Problem Rocks for a Technical Interview
* **Real-world relevance** – Piensa en cámaras de vigilancia o problemas de visión en el juego.
* **Multiple data‐structures** – Combina arrays, lazos y una pila **monotónica**.
* **Puntos de puntuación** – Muestra que puede manejar casos de borde (igual altura) y escribir código O(mn limpio).
* ** Alto LeetCode "interview‐ready" calificación** – Muchos reclutadores hacen esta pregunta específicamente.

-...

## 🧠 The Insight: Monotonic Stack for Both Directions

Para cada fila (derecha a izquierda) y cada columna (de abajo a arriba) mantenemos una pila **disminución** de alturas.
Cuando encontramos una nueva altura:

1. Mientras que la pila superior `t` es **shorter** que `h`, la persona actual puede ver `t` → aumentar el conteo y pop `t`.
2. Si la pila es **no vacía** después de la popping, la persona actual también puede ver la **primera persona más alta** en la pila → aumento de nuevo.
3. Empuje `h` sobre la pila sólo si es **no igual** a la parte superior actual (para evitar alturas iguales de doble cuenta).

Hacer esto una vez por todas las filas (de derecha a izquierda) y una vez por todas las columnas (de abajo a arriba) da la respuesta final en el tiempo `O(mn).

-...

## 📚 Code Implementations

### 1Ω⃣ Java (Monotonic Stack, O(mn))

``java
importar java.util*;

Solución de la clase pública {}
int[][] ver People(int[] heights) {}
en alturas. longitud;
int n = heights[0].length;
int[][] ans = nuevo int[m][n];

// ---- Analizar cada columna (abajo → arriba) ----
para (incluido el col = 0; col = n; col++) {}
Deque cumplióInteger confianza stack = nuevo ArrayDeque correspondió();
for (int row = m - 1; row >= 0; fila...) {}
int h = heights[row][col];
mientras (!stack.isEmpty() " p {}
ans[row][col]++; // ver una persona más corta
stack.pop();
}
si (!stack.isEmpty()) {}
ans[row][col]++; // ver el primero más alto
}
si (stack.isEmpty() {}
stack.push(h); // empujar sólo si la altura es nueva
}
}
}

// ---- Analizar cada fila (derecha → izquierda) ----
for (int row = 0; row < m; row++) {}
Deque cumplióInteger confianza stack = nuevo ArrayDeque correspondió();
para (int col = n - 1; col }= 0; col--) {}
int h = heights[row][col];
mientras (!stack.isEmpty() " p {}
ans[row][col]++; // ver una persona más corta
stack.pop();
}
si (!stack.isEmpty()) {}
ans[row][col]++; // ver el primero más alto
}
si (stack.isEmpty() {}
stack.push(h);
}
}
}

devolver los ans;
}
}
`` `

■ *Puntos clave*
* Dos pases independientes: **rows** (derecha a izquierda) y **columns** (de abajo a arriba).
* `ArrayDeque ' utilizado como pila para O(1) push/pop.
* Evite empujar alturas iguales para mantener la pila estrictamente disminuyendo.

-...

### 2down⃣ Python (Monotonic Stack, O(mn))

``python
de la importación Lista

Solución de clase:
def verPersonas (auto, alturas: Lista[Lista[int]) - No. List[List[int]]:
m, n = len(heights), len(heights[0])
ans = [[0] * n for _ in range(m)]

# Escanear cada columna inferior - # superior
para col en rango(n):
pila = []
para fila en rango(m - 1, -1, -1):
h = alturas[row][col]
mientras que la pila y h [-1]:
ans[row][col] += 1
stack.pop()
si la pila:
ans[row][col] += 1
si no apilar o h!= [-1]:
stack.append(h)

Escanear cada fila derecha izquierda
para fila en rango(m):
pila = []
para col en rango(n - 1, -1, -1):
h = alturas[row][col]
mientras que la pila y h [-1]:
ans[row][col] += 1
stack.pop()
si la pila:
ans[row][col] += 1
si no apilar o h!= [-1]:
stack.append(h)

Retorno
`` `

■ *Por qué este código Python está limpio*
* Los listados (`stack`) actúan como una pila con `append` / `pop`.
* Dos for-loops mantienen la lógica simétrica y fácil de leer.

-...

### 3down⃣ C++ (Monotonic Stack, O(mn))

``cpp
Incluido el título
#include >

Clase Solución {
public:
std:::vector obtenidosstd::vector realizadoint títulos verPersonas(estd::vector seleccionados:::vector seleccionadoint frecuentemente limitadas altas) {}
int m = heights.size();
int n = heights[0].size();
std::vector obtenidosstd::vector realizadoint títulos(m, std::vector fielint(n, 0));

// Pase de columna: inferior - título arriba
para (int col = 0; col )
std::stack madeint
for (int row = m - 1; row >= 0; --row) {
int h = heights[row][col];
mientras (!st.empty() " {}
++ans[row][col];
st.pop();
}
si (!st.empty()) ++ans[row][col];
si (st.empty() Silenciosos h != st.top() st.push(h);
}
}

// Paso de fila: derecha - título izquierda
para (infiler fila = 0; hilera)
std::stack madeint
para (int col = n - 1; col 0; --col) {
int h = heights[row][col];
mientras (!st.empty() " {}
++ans[row][col];
st.pop();
}
si (!st.empty()) ++ans[row][col];
si (st.empty() Silenciosos h != st.top() st.push(h);
}
}
devolver los ans;
}
};
`` `

■ **Highlights**
> > > < > > > > > > > > > > > >
* La misma lógica que las soluciones Java/Python, pero con idiomas C++.

-...

## 📊 Complexity Analysis

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencioso Columna pasar Silencioso `O(mn)` Silencio
tención Row pass Silencioso `O(mn)` Silencio `O(n)` (stack)
Silencio **Total** Silencioso **`O(mn)`** Silencio **`O(m + n)`** (matricidad de salida + personal)

Con `m, n ≤ 400`, el algoritmo funciona cómodamente en 1 ms de las máquinas modernas.

-...

## ♥ Edge‐Case Checklist

← Edge Case Silencio Por qué importa Silencio Cómo funciona el código
Silencio------------------
Silencio **Las mismas alturas** Silencio Ellos bloquean la visión para el otro. Nunca empujamos una altura que iguala la parte superior de la pila actual. Silencio
tención **Single row/column** Silencio Sólo existe una dirección. Los lazos siguen funcionando, pero la otra dirección pasa es trivial. Silencio
Silencio **Todas las alturas iguales** Silencio Todo el mundo sólo puede ver al vecino inmediato. tención Stack permanece vacío después de cada empuje; cada persona ve exactamente 1 persona (si hay). Silencio
Silencioso **Las alturas aumentan estrictamente** Silencio Cada persona puede ver a todos por delante. Silencio Mientras que el bucle abre a todas las personas más cortas, entonces cuenta el más alto. Silencio

-...

## 🎯 SEO‐Optimized Blog Post

### Title
*Master LeetCode 2282 – Número de personas que pueden ser vistos en un Grid” – Java, Python, C++ Solución Monotonic Stack + Entrevista Consejos**

## Meta Descripción
■ Solve LeetCode 2282 en **O(mn)** con una pila monotónica.
√ Full Java, Python, e implementaciones C+++ + información de entrevista.
■ Aprenda por qué este problema es un conocimiento imprescindible para entrevistas de instrucciones de datos.

-...

Blog Artículo

Introducción

Si usted está apuntando a un papel de ingeniería de software, el **Número de personas que pueden ser vistos en un problema Grid** es una entrevista clásica.
Prueba:

* Comprensión de traversal de matriz 2-D.
* Capacidad para diseñar una pila monotónica.
* Estilo de codificación limpio a través de idiomas.

A continuación, caminamos a través del problema, el truco **monotonic‐stack**, proporcionar código **full en Java, Python, y C+**, y compartir ideas de entrevista amigable.

-...

## ## 2down⃣ Problema Recap

- ** Entrada**: `m x n` matriz `alturas'.
- Regla de visibilidad**: Una persona en `(i, j)` sólo puede ver a la gente a la derecha ** o** abajo, siempre que cada persona intermedia sea estrictamente más corta.
- ** Objetivo**: Para cada celda, cuenta a la gente visible.

-...

#### 3down⃣ The Core Idea: Dos pasos con una estaca monotónica

1. **Escáneo de color (Bottom → Top)* *
* Trate cada columna como un array 1‐D.
* Mantener una pila decreciente** de alturas.
* Cuando la altura actual `h` es más alta que la parte superior de la pila, podemos ver esa persona → aumento cuenta " pop.
* Después de saltar, si la pila no está vacía, la persona actual también puede ver la primera persona más alta → otro aumento.
* Empujar `h` sobre la pila sólo si es * diferente* desde la parte superior actual para evitar alturas iguales de doble cuenta.

2. **Escáneo externo (derecho → Izquierda)**
* Repita la misma lógica en cada fila.
* Los dos escaneos son independientes – la matriz de salida se actualiza acumulativamente.

La combinación asegura que contamos con personas bien visibles y poco visibles en tiempo lineal.

-...

### 4down⃣ Language‐Specific Implementations

*Ya hemos incluido los fragmentos Java, Python y C++ en la sección “Aplicaciones de Code”. *
Siéntete libre de meterlos en tu IDE local y corre con los casos de muestra.

-...

#### 5down⃣ ¿Por qué esta solución Rocks for Interviews

* **Time‐Efficiency** – O(mn) es óptimo; los entrevistadores aman un razonamiento asintotico claro.
* **Space‐Efficiency** – Sólo una pila por fila/columna – demuestra conciencia de la memoria.
* Agnosticismo de lengua* Muestra que puede traducir la misma lógica a cualquier idioma, una habilidad muy valiosa para diversos apilamientos tecnológicos.

-...

### 6down⃣ Interview Tips

Silencioso Tip Silencioso Explicación
Silencio...
Silencio **Explicar la pila invariante** Silencio "La pila siempre almacena una secuencia decreciente estrictamente de alturas." Silencio
Silencio **Discuss equal heights** Silencioso “Las mismas alturas se bloquean entre sí; por eso saltamos empujando duplicados”. Silencio
Silencio **Visualizar con un diagrama** Silencio Dibujar una pequeña cuadrícula y caminar a mano el algoritmo; es una gran manera de convencer al entrevistador de su comprensión. Silencio
Silencio ** Casos de borde de mención** Silencio Mostrar conciencia de los escenarios de fila/columna y altura uniforme. Silencio
Silencio **Hablar sobre la complejidad** Silencio State `O(mn)` tiempo y `O(m + n)` espacio explícitamente – entrevistadores apreciar análisis rápido y preciso. Silencio

-...

### 7 carreras Take- Away

- **Las pilas monotónicas** son el pan y la mantequilla para los problemas de visibilidad 1‐D/next‐greater-element.
- **Dos pases** (columnas primero, filas segundas) aseguran la cobertura completa en 2-D.
- Mantener la pila **disminuir estrictamente** y saltar alturas iguales – esa es la sutileza que hace correcto el algoritmo.

Dominar este problema significa que usted está bien preparado para una amplia gama de preguntas de array-and-stack el día-una entrevista.

-...

#### 8down⃣ Pensamientos finales

Ya sea que sea un dev de Java backend, un científico de datos Python, o un ingeniero de sistemas C++, LeetCode 2282 le da una victoria rápida para impresionar a los reclutadores.
Implementa el código, prueba con matrices aleatorias y práctica explicando la lógica en voz alta – la entrevista te lo agradecerá.

Buena suerte, y feliz codificación! 🚀

-...

#### 9Ω⃣ Call‐to‐Action

*Drop a comment below if you’d like a deep dive into other LeetCode visibility problems! *

-...

**Author**: [Su nombre] – Aficionado a la estructura de datos " Contratación-tech‐lead.
**Tags**: #LeetCode, #DataStructures, #MonotonicStack, #Java, #Python, #CPlusPlus, #EntreviewPrep, #SoftwareEngineering

-...

*Y eso es todo*

Con estas implementaciones y explicaciones de entrevista, usted está listo para ace LeetCode 2282 y demostrar sus habilidades de pila a cualquier gerente de contratación. ¡Feliz codificación!