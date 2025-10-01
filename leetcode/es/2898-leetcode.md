-...
Título: LeetCode 2898. Maximum Linear Stock Score -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📈 2898 – Maximum Linear Stock Score
#Medium** - LeetCode

■ ** Objetivo** – Escoge una subsequencia de días tal que por cada par consecutivo
> `price[i] – price[j] == i – j`.
■ Maximice la suma de los precios elegidos.

A continuación se muestra una solución **ready‐to-copy** en **Java**, **Python** y **C+** (O(n) time, O(n) space) seguido de un **SEO-friendly blog** que explica el truco, los trade-offs, y por qué es una gran entrevista-punto-hablado.

-...

## 1. Resumen de la solución

Silencio Idioma Silencio Idea clave
Silencio--------------------------
Silencio **Java** Silencioso `precio - índice` (1-basado) → cubo, suma por cubo Silencio `O(n)` tiempo, `O(n)` espacio Silencio
Silencio **Python** Silencio Igual que Java – use `defaultdict` TENIDO `O(n)` tiempo, `O(n)` espacio Silencio
Silencio **C+** Silencio `unordered_map observadolong long,long long `` Silencio `O(n)` time, `O(n)` espacio Silencio

*¿Por qué funciona el precio – índice? *
Para una subsecuencia lineal la diferencia entre los dos precios consecutivos equivale a la diferencia entre los índices:

`` `
precio[i] – precio[j] = i – j (i ît j)
`` `

Rearrange:

`` `
precio[i] – i = precio[j] – j
`` `

Así que todos los índices seleccionados comparten el mismo **key** `price – index`.
Simplemente agrupamos precios por esa llave y elijamos el cubo con la suma más grande.

-...

## 2. Código de referencia

#### 2.1 Java

``java
importar java.util*;

Clase Solución {
public long maxScore(int[] prices) {
Mapa seleccionadoInteger, Cubo largo = nuevo HashMap garantizado();
respuesta larga = 0L;

para (int i = 0; i) i 0 precios.length; i++) { // 0-based index
int key = prices[i] - (i + 1); // 1‐based key
long newSum = bal.getOrDefault(key, 0L) + precios[i];
balde.put(key, newSum);
respuesta = Math.max(respuesta, newSum);
}
respuesta de retorno;
}
}
`` `

### 2.2 Python

``python
de las colecciones importadas por defecto
de la importación Lista

Solución de clase:
def maxScore(self, prices: List[int] int:
cubo = defaultdict(int)
mejor = 0
para i, precio en enumerado(precios): # i is 0‐based
clave = precio - (i +1) # 1-based key
cubo[key] += precio
mejor = máximo (mejor, cubo[key])
mejor
`` `

### 2.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
largo tiempo maxScore(vector fieltro precios) {}
unordered_map cubo;
ans largos = 0;
para (size_t i = 0; i) ++i) {
largo largo largo llave = (long long)prices[i] - (long long)(i + 1);
cubo[key] += precios[i];
ans = max(ans, balde[key]);
}
devolver los ans;
}
};
`` `

-...

## 3. Blog Post – “Maximum Linear Stock Score: The Good, The Bad, and the Ugly”

■ **Target Audience:** Java/Python/C++ desarrolladores que se preparan para entrevistas técnicas, reclutadores y entusiastas del algoritmo.
■ ** Palabras clave principales:** *Maximum Linear Stock Score*, *LeetCode 2898*, *Java solution*, *Python solution*, *C++ solution*, *hashmap trick*, *interview problem*, *O(n) algoritmo*.

-...

#### 3.1 Introducción

■ Cuando abres LeetCode 2898 *Maximum Linear Stock Score*, lo primero que puede morderte es la condición aparentemente "odd":
> `price[i] – price[j] == i – j`.
■ Parece un rompecabezas dinámico o de dos puntos, pero el verdadero truco es una línea única: **bucket por `price - index`**.

Este artículo recorre por qué funciona ese truco de cubo, sus pros y contras, y cómo explicarlo con confianza en una entrevista.

-...

### 3.2 Restante el problema

Tenemos un array `prices[1...n]` (1-indexed).
Elija una subsequencia `indexes = [i1] Secuencia i2 se hizo ... ik]` tal que por cada par adyacente

`` `
precios[ij] - precios[ij-1] = ij - ij-1 (1)
`` `

El **score** es simplemente la suma de los precios seleccionados.
Debemos maximizarlo.

-...

#### 3.3 Intuición & Transformación

Reescribir (1) moviendo términos:

`` `
precios[ij] - ij = precios[ij-1] - ij-1
`` `

El lado izquierdo es **constante** para todos los índices en una subsequencia lineal.
Así que todos los días elegidos comparten el mismo valor

`` `
clave = precio - índice
`` `

Si agrupamos todos los días por esta clave y sumamos los precios dentro de cada grupo, el grupo con la suma más grande es la respuesta.

■ **¿Por qué esto no se pierde ninguna subsequencia óptima? * *
■ Cualquier subsequencia óptima debe satisfacer (1), por lo tanto todas sus llaves son iguales.
■ Por el contrario, elegir todos los índices con una clave en particular satisfies automáticamente (1).
■ Por lo tanto la mejor respuesta es la suma máxima del cubo.

-...

### 3.4 La “buena” – Simplicidad y Velocidad

* **Tiempo** – O(n) porque escaneamos el array una vez.
* **Espacio** – O(n) peor caso (todo elemento tiene una clave distinta).
* **Implementation** – 5-line hash‐map update in Java/Python/C++.
* **Big‐O Friendly** – Handles `n = 10^5` cómodamente; `price ≤ 10^9`, so we use `long`/`int64_t`.

■ *Entreview‐Friendly*: Puedes explicarlo en 30 segundos – “Group by price‐index difference”.

-...

### 3.5 El "Bad" – Pitfalls ocultos

¿Qué sucede?
Silencio...
Silencio Usando el índice basado en 0 incorrectamente ← Off‐by‐one key → balde incorrecto TENS Subtract `i+1` en lugar de `i` Silencio
Silencio El desbordamiento de la suma vertida `precio * n` puede exceder de 32 bits  durable Use 64-bit (`long`/`long') Silencio
Silencio Olvidar la clave inicial tención Mapa puede contener ceros para claves invisibles Silencio `getOrDefault` o `unordered_map::operator[]` mangos claves faltantes

-...

### 3.6 The “Ugly” – Over-engineering

Algunos entrevistados tratan de utilizar árboles de segmentos, árboles Fenwick o tablas DP.
Estos enfoques añaden complejidad innecesaria y tiempo de riesgo o errores.
Sigue el truco **hash‐map de cubo** a menos que el entrevistador desee explícitamente una solución más elaborada.

-...

### 3.7 Walk‐Through Ejemplo

`` `
precios = [1, 5, 3, 7, 8]
índices (1 basado): 1 2 3 4 5

clave = precio - índice:
1-1 = 0
5-2 = 3
3-3 = 0
7-4 = 3
8-5 = 3

Buckets:
0 → [1, 3] sum = 4
3 → [5, 7, 8] suma = 20 <-- max

Respuesta = 20
`` `

-...

### 3.8 Testing Your Implementation

Silencio Test confidencialidad esperada
Silencio...
Silencioso `[5, 6, 7, 8, 9]
Silencioso[10]
TENIDA `[1, 2, 3, 4, 5]
[1, 1000000000]
Silencio `[1,2,4,8,16,32]` Silencio 1+2+4+8+16+32 = 63 (todas las acciones clave 0)

Escribe pruebas de unidad en el marco de tu idioma o utiliza el parque infantil LeetCode.

-...

### 3.9 Complejidad Recaptura

- **Tiempo**: `O(n)` - pase único sobre el array.
- **Espacio**: `O(n)` - el tamaño del mapa equivale al número de teclas distintas.
- **Scalability**: Handles the maximum constraints (`n = 10^5`, `price ≤ 10^9`) in milliseconds.

-...

### 3.10 Por qué es una gran pregunta de entrevista

1. **Trick Revealed** – Demuestra el reconocimiento del patrón: convertir una limitación de la diferencia en una clave.
2. **Multiple Languages** – Muestra que puedes resolverlo en Java, Python, C++ (y incluso JavaScript).
3. **Tiempo Eficiente** – Puede resolverlo con un solo bucle; sin tablas de DP o recursión.
4. ** Casos Edge** – Estimula la discusión sobre el desbordamiento, la indexación y las colisiones precipitadas.

-...

### 3.11 Consejo de clausura

- **Explicar la transformación** claramente antes de escribir código.
- **Mostrar las actualizaciones del mapa** paso a paso.
- **Desbordamiento de la mención** si usa idiomas con anchos fijos de entero.
- **Amuebla con análisis de complejidad** – A los reclutadores les encanta ver que piensas en el rendimiento.

¡Feliz codificación, y que la tecla 'precio - índice' siempre te lleve a la puntuación más alta! 🚀

-...

### 3.12 SEO Captura

TENCIÓN TERRITORIO TERRITORIO
Silencio...
tención Título Silencioso “Maximum Linear Stock Score – LeetCode 2898 Java Python C++ Solution”
tención Meta Descripción Silencioso “Solve LeetCode 2898 en tiempo O(n). Leer Java, Python, código C++ y guía de preparación de entrevistas.” Silencio
Silencio H1 Silencio “Maximum Linear Stock Score – A Hash‐Map Trick”
Silencio H2 Silencioso “Restatement del Problema”, “Intuición”, “Código de Java”, “Código del Python”, “Código C++”, “Complejidad”, “Consejos de Intervisión”
← Alt Texto Silencioso “LeetCode 2898 ejemplo diagrama”, “Java hashmap code snippet”, “Python defaultdict example”, “C++ unordered_map code”

Añadir el artículo a tu blog, compartirlo en LinkedIn, y ver crecer el tráfico de búsqueda de trabajo!