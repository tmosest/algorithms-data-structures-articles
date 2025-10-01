-...
Título: LeetCode 1943. Describe la pintura -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 Problema Recap - LeetCode 1943 "Describe la pintura"

■ **Objetivo** – Convertir un conjunto de segmentos de color, superpuestos en una línea de números en el conjunto mínimo de segmentos no superpuestos de medio bloque que describen correctamente cada *mixed color* en la línea.
■ ** Salida** – Para cada nuevo segmento `[l, r)` producimos el *sum* de todos los colores que están presentes en ese intervalo (el “color mezclado” es un conjunto de colores distintos, pero sólo devolvemos la suma).

-...

### Por qué es un problema de entrevista clásica

* **Line Sweep** – la técnica canónica para tratar con intervalos que cambian en puntos finales.
* ** Estructuras de datos** – árboles de búsqueda binaria equilibrados (`TreeMap`/`std::map`) o * arrays de diferencias*.
* **Edge-cases** – manejo de “holes” (partes no pintadas) y rangos superpuestos que tienen la misma suma pero diferentes conjuntos de colores.
* **La complejidad** – `O(n log n)` (map) o `O(n + maxCoord)` (array) – ambos aceptables para las limitaciones.

-...

## 👨 💻 Solution Idea – Line Sweep with a Difference Map

1. **Recoge todas las coordenadas "interesantes"** – cada punto de inicio o final de un segmento.
2. **Store the delta of color sum at each point* *
* Añadir `color` en el *start* de un segmento.
* Subtract `color` at the *end* of a segment.
3. **Ordenar las coordenadas** (o usar un mapa determinado) y ordenar.
4. Mantener un funcionamiento " corriente Sum`.
5. Cada vez que el `currentSum > 0` y la siguiente coordenadas difieren del anterior, emite un segmento `[prevCoord, currCoord)` con la suma actual.
6. Pasar intervalos donde `currentSum == 0` – no están pintados.

Debido a que cada color en la entrada es *unique*, el conjunto de colores activos cambia cada vez que la suma cambia. Por lo tanto una suma numérica pura es suficiente para la salida.

-...

## 📦 Code

A continuación se presentan soluciones limpias y idiomáticas en **Java, Python y C++**.
Cada solución utiliza el mismo algoritmo; sólo los datos de estructura difieren.

-...

### Java (Aplicación basada en la matriz rápida)

``java
importar java.util*;

Solución de la clase pública {}
public List made(int[] segmentos) {}
// Max endpoint ≤ 1e5 + 1 (el extremo “medio cerrado”)
int final MAX = 100001;
largo[] diff = nuevo largo [MAX + 2]; // diff[i] = cambio en la suma en i
boolean[] isEndpoint = nuevo booleano[MAX + 2];

// Dibujo de la diferencia
para (int[] seg : segmentos) {}
int start = seg[0], end = seg[1];
color largo = seg[2];
diff[start] += color;
diff[end] -= color;
isEndpoint[start] = true;
isEndpoint[end] = true;
}

Lista seleccionadaLista realizadaLong confianza Resultado = nuevo ArrayList recomendado();
long current = 0; // running sum
int prev = 0; //

para (int i = 1; i)= MAX + 1; i++) {
si (esEndpoint[i] " corriente " 0) {
// Intervalo de pintura [prev, i) con suma actual
result.add (Arrays.asList(long)prev, (long)i, current));
}
prev = isEndpoint[i] ? i : prev; // salto sólo en puntos finales
actual += diff[i];
}
Resultado de retorno;
}
}
`` `

**La complejidad* *

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencioso edificio diff Silencio `O(n)` Silencio `O(maxCoord)` Silencio
Silencioso matriz de escanning Silencioso `O(maxCoord)`
Silencio Total Silencio `O(n + maxCoord)` ♥ `O(1e5)` Silencio `O(maxCoord)` Silencio

-...

### Python (Using `sortedcontainers` or built‐in `dict`)

``python
de la importación Lista
de las colecciones importadas por defecto

Solución de clase:
def splitPainting(self, segments: List[List[int]) - No. List[List[int]]:
diff = defaultdict(int)
extremos = set() # coordenadas que son puntos finales reales

# Construir mapa de la diferencia
para s, e, c en segmentos:
diff[s] += c
diff[e] -= c
end.add(s)
end.add(e)

# Lista clasificada de todas las coordenadas interesantes
coords = ordenados(en adelante)

res = []
corriente = 0
prev = coords[0] # first endpoint

para i en rango(1, len(coords)):
curr = coords[i]
corriente += diff[prev]
si es actual 0:
re.append([prev, curr, current])
prev = curr

retorno
`` `

■ **Tip** – Si prefieres los insertos/lookups de O(log n), utiliza 'contenedores variados. SortedDict` (pip install).
■ El código anterior se ejecuta en `O(n log n)` debido a la clasificación del punto final (`n ≤ 2·104`).

-...

### C++ (Fast array + `vector`)

``cpp
Incluido el título
#include >
usando std namespace;

Clase Solución {
public:
vector realizador realizado durante mucho tiempo estipulado splitPainting(vector seleccionado seleccionado: {}
const int MAX = 100001; // máxima coordenadas + 1
vector realizado largamente dieff(MAX + 2, 0);
vector asignado título esEnd(MAX + 2, 0);

para (auto &seg : segmentos) {}
int s = seg[0], e = seg[1];
largo c = seg[2];
diff[s] += c)
diff[e] -= c;
isEnd[s] = isEnd[e] = 1;
}

vectorial realizador realizado durante mucho tiempo res;
Cura larga larga = 0;
int prev = 0;

para (int i = 1; i)= MAX + 1; ++i) {
(isEnd[i] " curva " 0) {
res.push_back({prev, i, cur});
}
prev = isEnd[i] i : prev;
cur += diff[i];
}
restitución;
}
};
`` `

**¿Por qué `vector seleccionado' para 'esEnd'?* *
`bool` puede tener una sobrecarga definida por la implementación. Un `char` es un byte y es suficiente para marcar si una coordinación es un punto final real.

-...

## 📚 Blog detallado – “Describe la pintura” en el estilo de un blog de entrevista técnica

-...

# How to Master LeetCode 1943 – “Describe la pintura”

■ **Keywords:** LeetCode 1943, Describe la pintura, barrido de líneas, solución Java, solución Python, solución C++, entrevista de algoritmos, entrevista de codificación, entrevista de trabajo, estructuras de datos, BST equilibrado, matriz de diferencias.

-...

## Tabla de contenidos

1. Declaración de problemas
2. Observaciones clave
3. Algoritmo - Diferencia del sudor de líneas Mapa
4. 📦 Three Clean Implementations
5. Наливали las cascadas comunes ( partes “Bad” " Ugly " )
6. Recibir Qué hacer hincapié en una entrevista
7. 📈 Cómo mostrar su solución en una cartera
8. 💼 ¿Por qué este problema te hace trabajar?
9. 📚 Leer más " Recursos "

-...

## 1. Declaración de problemas (Recap.)

Se le da un array `segments`, cada elemento `[start, end, color]`.
Todos los valores de color son únicos.
La tarea: producir el *mínimo* conjunto de segmentos no superpuestos semicerrados que describen correctamente los colores mezclados en la línea.
Presentar una lista de `[izquierda, derecha, sum_of_colors]` para cada intervalo pintado.
Intervalos sin color (`sum == Debe ser omitido.

Constraints: `1 ≤ n ≤ 20000`, `1 ≤ inicio ≤ 100000`, todos los colores ≤ `109`.

-...

## 2. Observaciones clave

TENCIÓN ANTERIOR Por qué importa
Silencio...
Silencio ** Cambio de punto** Silencio Un segmento comienza o termina sólo en coordenadas enteros. Silencio
Silencio **Colores únicos** Silencio El conjunto de colores activos cambia si la suma numérica cambia. Silencio
Silencio **Half‐closed** Silencio `end` es *no* parte del segmento, por lo que podemos utilizar un array de diferencia sin errores fuera de cada uno. Silencio
Silencio **No se pintan “agujeros”** Silenciosos Intervalados donde se ignoran “currentSum == 0”. Silencio
Silencio **Sorting required** Silencio Necesitamos las coordenadas en orden ascendente para realizar un barrido. Silencio

-...

## 3. Algoritmo – Línea Sudadera con un Mapa de Diferencia

1. *Crea un mapa delta*
* For every segment `[s, e, c]`: `delta[s] += c`, `delta[e] -= c`.
* Almacenar tanto " como " en un conjunto de " puntos finales " .
2. **Sort `endpoints`** – esto nos da la orden de barrido.
3. Traverso
* Keep `curSum = 0`, `prev = first_endpoint`.
* Para cada coordenadas `x` en orden ordenado:
* `curSum += delta[prev]`.
* Si "curSum " , salida `[prev, x, curSum] ' .
* `prev = x`.
4. Devuelve la lista.

Debido a que la suma es estrictamente positiva para cualquier intervalo pintado, podemos saltar rangos no pintados y no necesitamos reconstruir el *set* de colores.

-...

## 4. Tres implementaciones limpias

■ **Tip** – La lógica central es idéntica; sólo la elección de la estructura de datos difiere.

Silencio Idioma Silencio Preferente Estructura de Datos Silencio Complejidad del Tiempo Silencio
Silencio------------------------------------------ La vida--
Silencio Java  suya Array (`diff`) + matriz booleana (`isEndpoint`) Silencio `O(n + maxCoord)` Silencio `O(maxCoord)` Silencio
Silencio Python Silencio `defaultdict` + `set` (sorted later) Silencio `O(n log n)` Silencio `O(n)` Silencio
TENIDO C++ TENIDO `vector realizado largo `` + `vector fielchar `` Silencio `O(n + maxCoord)` ANTE `O(maxCoord)` Silencio

-...

## Java – Array basado (más performant)

``java
importar java.util*;

Solución de la clase pública {}
public List made(int[] segmentos) {}
int final MAX = 100001; // 1e5 + 1 es seguro
largo[] diff = nuevo largo [MAX + 2];
boolean[] isEnd = nuevo booleano[MAX + 2];

para (int[] seg : segmentos) {}
int s = seg[0], e = seg[1];
c = seg[2];
diff[s] += c)
diff[e] -= c;
isEnd[s] = true;
isEnd[e] = true;
}

Lista seleccionadaLista realizadaLong confianza ans = nuevo ArrayList recomendado();
Cura larga = 0;
int prev = 0;

para (int i = 1; i)= MAX + 1; i++) {
(isEnd[i] " curva " 0) {
ans.add (Arrays.asList(long)prev, (long)i, cur));
}
prev = isEnd[i] i : prev;
cur += diff[i];
}
devolver los ans;
}
}
`` `

-...

### Python – Usando un mapa

``python
de las colecciones importadas por defecto
de la importación Lista

Solución de clase:
def splitPainting(self, segments: List[List[int]) - No. List[List[int]]:
diff = defaultdict(int)
extremos = set()

para s, e, c en segmentos:
diff[s] += c
diff[e] -= c
end.add(s)
end.add(e)

coords = ordenados(en adelante)
res = []
Cura = 0
prev = coords[0]

para i en rango(1, len(coords)):
cur += diff[prev]
si cursé 0:
re.append([prev, coords[i], cur])
prev = coords[i]

retorno
`` `

■ **Si usted necesita estrictamente 'O(n log n)'** (que surja domina), esto ya satisface los límites.
■ El código es 80 % más corto que la solución “map‐only” y mantiene la misma lógica.

-...

### C++ – Array basado (altamente eficiente)

``cpp
Incluido el título
usando std namespace;

Clase Solución {
public:
vector realizador realizado durante mucho tiempo estipulado splitPainting(vector seleccionado seleccionado: {}
const int MAX = 100001;
vector realizado largamente dieff(MAX + 2, 0);
vector asignado título esEnd(MAX + 2, 0);

para (auto &seg : segmentos) {}
int s = seg[0], e = seg[1];
largo c = seg[2];
diff[s] += c)
diff[e] -= c;
isEnd[s] = isEnd[e] = 1;
}

vector realizador llevado a cabo larga larga larga experiencia
Cura larga larga = 0;
int prev = 0;

para (int i = 1; i)= MAX + 1; ++i) {
(isEnd[i] " curva " 0) {
ans.push_back({prev, i, cur});
}
prev = isEnd[i] i : prev;
cur += diff[i];
}
devolver los ans;
}
};
`` `

-...

## 🧩 “Good”, “Bad”, y “Ugly” – What to Keep " What to avoid

Subtítulos en la categoría Silencio bueno Silencio
Silencio--------------...
Silencio ** Algorithm** tención Barrido lineal; estable incluso con gran `maxCoord`. Silencio Iteración sin surtido de coordenadas crudas → puntos finales perdidos. Silencio Utilizar un *plain* mapa no deseado e iterando arbitrariamente – produce un orden incorrecto. Silencio
Silencio **Data‐structure** Silencio `TreeMap` / `std::Map` para llaves ordenadas. Silencio `vector garantizadobool `` para endpoints (trabajos pero ligeramente desordenados). TENIDO Utilizando `ArrayList seleccionadaInteger confianza` + `HashMap madeInteger, Long `` entonces clasificando *sólo las teclas delta* – faltan coordenadas que tienen `delta == 0`. Silencio
Silencio **Complejidad** Silencio `O(n log n)` – fino para los límites de LeetCode. Silencio `O(n2)` – barrido ingenuo sin ordenar. Silencio `O(n + maxCoord)` – eficiente pero puede ser exagerado si las coordenadas son enormes. Silencio
Silencio **Manejamiento por caso de Corner** Silencioso Skip when `currentSum == Olvídate de actualizar `prev` sólo en los puntos finales. Emitir intervalos de longitud cero (`[x, x)`), causando respuesta incorrecta. Silencio
Silencio **Readability** Silencio Nombres variables claros (`currentSum`, `prevCoord`). tención Dense lógica de una línea – difícil de depurar. " La seguridad del tipo " . Silencio

■ **Bottom line** – el enfoque array-difference es el más limpio para los entrevistadores; la versión basada en mapa es más fácil de leer si no estás cómodo con el indexado de array.

-...

## 🚀 How This Problem Helps You Land Your Dream Job

1. **Demonstrates Core Data‐Structure Knowledge** – Mapa, Tree, Array.
2. **Mostrar código limpio " Manejo por caso de Edge** – los entrevistadores aman soluciones que no se bloquean en `end == 0`.
3. **Exhibe Pensamiento Algorítmico** – transformando un problema de “pintura” en una línea *sweep* – un patrón clásico de problemas de entrevista.
4. **Portfolio Ready** – Sube la solución con comentarios " pruebas unitarias a GitHub o LinkedIn.
5. **Blog Post / Medium Article** – Compartir este artículo, como antecede, demuestra que usted puede comunicar ideas complejas.
6. **Idioma sobre plataformas de codificación** – Añada el problema a su lista "Top 50 resuelto" en LeetCode, Codeforces, HackerRank.

-...

## 📚 Más lectura

Silencioso recurso
Silencio...
Silencio “Cracking the Coding Interview” – Capítulo sobre *Interval Scheduling* ← Problemas de línea de barrido clásico. Silencio
“Algoritmos sobre datos geométricos” – Coursera tención Técnicas de línea de barrido avanzada. Silencio
← “GeeksforGeeks – Line Sweep Algorithm” _ Múltiples ejemplos y explicaciones visuales. Silencio
Silencio “Universidad de Entrevista de Coding” (GitHub) _ Lista completa de preguntas de entrevista, incluyendo 1943. Silencio

-...

### Closing Thought

Mastering LeetCode 1943 es una prueba *soft-skill* – no solo estás resolviendo un rompecabezas; estás demostrando que puedes:

- **Traducir un problema a las estructuras de datos* *
- ** Casos de borde hundido elegantemente**
- **Código legible, mantenible* *
*Explica tu razonamiento claramente* *

Ponga esta solución en su cartera, emparejarla con un blog limpio, y brillará en cualquier entrevista de codificación o en LinkedIn. ¡Buena suerte! 🚀

-...

¡Feliz codificación! *