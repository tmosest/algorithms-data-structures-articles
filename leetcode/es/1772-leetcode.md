-...
Título: LeetCode 1772. Características Ordenar por Popularidad -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1772 – “Características de la popularidad”
■ **El bueno, el malo, y el feo** de resolver un problema de la frecuencia mediana

■ **Keywords**: LeetCode 1772, Características Ordenar por Popularidad, Java, Python, C++, entrevista, algoritmo, mapa de hash, tipo estable, complejidad, consejos de entrevista de trabajo

-...

## 🚀 Quick Overview

Silencio Idioma Silencio tiempo Silencioso Silencioso
Silencio--------------------------------
Silencio **Java** Silencio O(F + R + F log F) Silencio O(F + R) Silencio Usos `HashMap` + `Arrays.sort` con un comparador personalizado. Silencio
Silencio **Python** Silencio O(F + R + F log F) Silencio O(F + R) Silencio Usos `colecciones. Counter` + `sorted`. Silencio
Silencio **C+** Silencio O(F + R + F log F) Silencio O(F + R) Silencio Usos `unordered_map` + `sort` con a lambda. Silencio

■ **F** – número de características (`≤ 104`)
■ **R** - número de respuestas ( " ≤ 102 " , cada una hasta " 103 " ).

-...

Problema Recap

Se te da:

- `características ': un array de **unique** palabras (longitud ≤ 10).
- `responses`: una serie de oraciones, cada palabra separada por un solo espacio.

**Popularidad** de una característica = número de respuestas que contienen la característica **al menos una vez**.

Clasifique la matriz de las características en ** no aumento** orden de popularidad.
Si dos características empatan, mantenga el orden original (tipo estable).

-...

Lo que hace este problema “Medium”

1. **Deduplicación por respuesta** – una sola respuesta puede mencionar una característica varias veces, pero debe contar sólo una vez.
2. ** Ordenación estable** – no puede simplemente ordenar por frecuencia; los lazos deben respetar el índice original.
3. **Gran tamaño de entrada** – hasta 104 características, por lo que un enfoque de O(F2) sería un tiempo de salida.

-...

## Solution Idea

1. ** Mapa de frecuencia** – almacenar una cuenta para cada característica.
Usar un `HashMap realizadoString,Integer confianza` (Java), `unordered_map madestring,intilo `` (C++), o `Counter` (Python).

2. **Proceso de cada respuesta**
* Dividir en palabras.
* Poner las palabras en un `HashSet` / `unordered_set` / `set` para mantener sólo palabras únicas.
* Por cada palabra única que existe en el conjunto de características, aumenta su frecuencia.

3. **Sorta*
* En Java: `Arrays.sort(features, comparator)` – comparador examina la frecuencia del mapa.
* In Python: `sorted(features, key=lambda f: (-freq[f], index_map[f])`.
* En C++: `std::sort(features.begin(), features.end(), comp)` con una lambda que utiliza el mapa.

La comparación mantiene automáticamente el índice original de los lazos porque la matriz de las características está clasificada **en su lugar**, y el orden original se conserva cuando las frecuencias son iguales (comportamiento de tipo estable del Java/Python `sorted` y C+++ `sort` con una clave estable).

-...

## 📄 Code

### Java (Java 17)

``java
importar java.util*;

Clase Solución {
public String[] sortFeatures(String[] features, String[] responses) {}
// 1. Mapa de frecuencia
Mapa seleccionadoString, Integer frecuentementeq = nuevo HashMap Quería();
para (String f : características) {}
freq.put(f, 0);
}

// 2. Apariciones contables
for (String response : responses) {}
Criar[] palabras = respuesta.split(");
Establecer:String confía visto = nuevo HashSet incorrecto(Arrays.asList(words));
para (String w : visto) {
si (freq.containsKey(w)) {}
freq.put(w, freq.get(w) + 1);
}
}
}

// 3. Tipo estable por frecuencia (descendencia)
// Java's Arrays.sort es estable sólo para objetos,
// pero usando una comparación que mantiene el orden original funciona.
Integer[] idx = nuevo Integer[features.length];
para (int i = 0; i) funciones.length; i++) idx[i] = i;

Arrays.sort(idx, (i, j) - título {
int fi = freq.get(features[i]);
int fj = freq.get(features[j]);
si (fi != fj) regreso Integer.compare(fj, fi); // desc
retorno Integer.compare(i, j); // orden original
});

// Resultado de construcción
String[] result = new String[features.length];
para (int i = 0; i) las características indicadas.length; i++) {
result[i] = features[idx[i];
}
Resultado de retorno;
}
}
`` `

■ **¿Por qué esta versión Java? * *
■ *Uses `Integer[]` for stable ordering because `Arrays.sort` on primitiva `int[]` no es estable. *
■ *El array índice mantiene índices originales para romper corbatas. *

-...

### Python 3 (≥ 3.7)

``python
de las importaciones de colecciones Contrato
de la importación Lista

Solución de clase:
def sortCaracterísticas(self, features: List[str], responses: List[str]) - Propiedad Lista[str]:
# Mapa de frecuencia
freq = Counter({f: 0 for f in features})

# Cuenta apariciones por respuesta
para resp in responses:
palabras = resp.split()
para w en set(words):
si w en freq:
freq[w] += 1

# Mapa de índice original para romper corbatas
idx = {f: i for i, f in enumerate(features)}

# Ordenar: primero por -freq (desc), luego por índice original (asc)
volver ordenados (características, key=lambda f: (-freq[f], idx[f])
`` `

■ ¿Por qué Python?
■ *Built‐in `Counter` + `sorted` hace que el código concise.
■ *La lambda da O(F log F) clasificación, que es óptima. *

-...

### C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vectores seleccionados, clasificar caracteresCaracterísticas(vector seleccionados) {
// Mapa de frecuencia
unordered_map detectstring, int confianza freq;
para (contiguo cadena reducida f : características) freq[f] = 0;

// Cuenta apariciones por respuesta
for (const cordular resp : responses) {}
unordered_set obtenidosstring confianza visto;
Palabra de cuerda;
istringstream iss(resp);
mientras que (es la palabra нелиле palabra) visto.insert(palabra);
for (const cordón w : seen)
si (freq.find(w) != freq.end()) freq[w] += 1;
}

// Mapa del índice original
unordered_map detectstring, int título idx;
para (int i = 0; i) = (int)features.size(); ++i) idx[features[i] = i;

// Ordenar con lambda
type(features.begin(), features.end(),
[T](Cont cordón a, const cordón d) {
si (freq[a] != freq[b]) devuelve freq[a]
idx[a] Identifica idx[b]; // original
});

características de retorno;
}
};
`` `

■ ** Notas C++**
■ *Usa `reglamento de extracción de palabras y `unordered_set` para la deduplicación.
■ *Lambda captura los mapas índice de frecuencia & por referencia. *

-...

## 📈 Complexity Analysis

Silencio Silencio Java Silencio Python
Silencio--------Prince----------------
Silencio Construir el mapa de freq **O(F)** Silencio **O(F)** Silencio**
← Respuestas del proceso Silencioso **O(total words)** ≤ O(R × maxLen) Silencio **O(total words) **O(total words)**
Silencioso Deduplicación por respuesta Silencio **O(palabras por resp)** Silencio mismo Silencio mismo
TENIDO TERRITORIO **O(F log F)** Silencio **O(F log F)** Silencio **O(F log F)**
Silencio **Total** Silencio **O(F + R + F log F)** TENIENDO lo mismo TENIDO
Silencioso **Espacio** Silencioso **O(F + R)**

■ **Por qué no estamos usando una cola de prioridad* *
■ Un min‐heap daría O(F log F) también, pero el tipo simple estable es más fácil razonar y menos error-prone en los ajustes de entrevista.

-...

## ⋅ Common Pitfalls (The Bad & Ugly)

Silencio Pitfall Silencio Por qué duele Silencio
Silencio--------------------------
Silencio **Counting duplica en una respuesta** Silencio Si acabas de dividir y bucle, aparecerán dos palabras dobles en la misma frase. ← Deduplicar con un set antes de aumentar. Silencio
Silencio **No-stable sorting** Silencio `Arrays.sort` en `int[]` no es estable, por lo que los brotes de corbatas pueden brillar las características incorrectamente. Utilice un array índice o una matriz de objetos para preservar el orden. Silencio
Silencio **Splitting en espacios ciegamente** Silencio Las oraciones pueden contener múltiples espacios o espacios líderes/trailing. TENIENDO `Split()` (Python), `aprendizaje ` (C+++), o `String.split(" ")` (Java). Todos ignoran los espacios consecutivos por defecto. Silencio
Silencio **Respuestas más importantes** Silencio Dividir cada respuesta con `String.split()` es O(length of sentence). Silencio aceptable porque R es pequeña (`≤ 102`). Silencio
Silencio ** Collisions hash in unordered_map** Silencio En C++ entradas extremas pueden desencadenar el peor maletín O(F) por lookup. Cuento del cubo reservado: `unordered_map identificadostring,int confianza freq; freq.reserve(features.size()*2);` ←

-...

## 🎤 Interview Tips

Silencio Lo que los entrevistadores buscan Silencio Cómo lo muestra nuestra solución
Silencio------------------------------
Silencio ** Estructuras de datos** Silencio Uso de mapas de hash / conjuntos de hash para búsquedas O(1). Los tres códigos construyen un mapa de hash para la frecuencia y un hash set para la deduplicación. Silencio
Silencio ** Pensamiento algorítmico** Silenciosamente Decomponer el problema en la contabilización + clasificación. Silencio Clara separación de pasos en explicación. Silencio
Silencio **Edge-case handling** Silencio Respuestas vacías, características nunca apareciendo, lazos. El Código de Vida representa a todos; " set() "/ " unordered_set " no garantiza una doble contabilización. Silencio
Silencio **Concienciación de la actuación** Silencio Complejidad O(F log F) es óptima dadas limitaciones. tención Tiempo " análisis espacial proporcionado. Silencio
Silencio **Características de idiomas** Silencio Uso de bibliotecas integradas (`Counter`, `unordered_map`, `std::sort`). Silencio Muestra familiaridad con las herramientas estándar. Silencio

■ **Muéstrate de tu proceso de pensamiento* *
■ Cuando se le pide implementar esto, caminar a través del razonamiento: ¿Por qué la deduplicación? ¿Por qué necesitamos una clasificación estable? ¿Cómo hacemos un seguimiento de los índices? Esa narrativa impresiona a los entrevistadores mucho más que el código final.

-...

## The Good

- **Simplicidad** – frecuencia contando + clasificando es directo una vez que entiendes las limitaciones.
- **Language‐agnostic** – la misma lógica funciona en Java, Python, C++ y muchos otros idiomas.
- **Stable sort** – funciones de clasificación integradas preservan naturalmente el orden original de los lazos, por lo que no necesita un pase separado.

-...

## ⋅d The Bad

- **Gran tamaño de entrada** – ingenuo O(F2) clasificación (por ejemplo, tipo burbuja) TLE.
- ** Costo de deduplicación** – crear un `HashSet` por respuesta puede ser caro si las respuestas son largas, pero aquí el recuento de respuesta es pequeño, por lo que está bien.
- **Memory overhead** – almacenar todas las palabras de todas las respuestas en un conjunto podría duplicar el uso de la memoria si no es cuidadoso; sólo mantenemos un conjunto por respuesta para mantener la huella de memoria baja.

-...

## The Ugly

**Usando un tipo no estable con una simple comparación* *
*En Java, `Arrays.sort` en tipos primitivos es **no** estable, por lo que debe manejar índices usted mismo (como en el código anterior). *

- **Misinterpretando “al menos una vez”* *
*Muchos candidatos cuentan menciones totales, no respuestas únicas. *
*Esto conduce a respuestas erróneas en casos de prueba como:*
``text
características = ["alfa", "beta"]
respuestas = "alpha alpha beta", "beta beta"]
`` `
* Popularidad correcta: alfa = 1, beta = 2.*

- Separadores codificados por miedo**
*Asumiendo que solo un espacio puede causar fallos si la entrada contiene pestañas o múltiples espacios. *
*Robust dividir con regex o extracción de corriente es más seguro. *

-...

## 📚 Take‐ Home Mensajes

1. **Frecuencia + deduplicación** es un patrón común de entrevista.
2. **Mantenga índices originales** útiles para romper corbatas o tipos estables.
3. **Use bibliotecas estándar** para mantener el código limpio y reducir errores.
4. **Análisis de la complejidad temprana** – O(F log F) es el costo mínimo para clasificar `características`.

-...

## 🎯 Ready to Ace Your Next Interview

- **Practice** el problema en LeetCode; es un campo de entrenamiento perfecto *contra frecuencia*.
- **Explicar** el enfoque en voz alta; a los entrevistadores les encanta escuchar su razonamiento.
- **Mención** las persianas (de oraciones vacías, palabras duplicadas) – muestra atención al detalle.
- **Hablar sobre el rendimiento** - por qué elegiste O(F log F) clasificando y no algo más lento.

■ **Pro tip**: Mientras se codifica, mantenga una lista mental:
■ 1. ¿Deduplicamos por respuesta?
■ 2. ¿Es el tipo estable o cortamos manualmente corbatas?
■ 3. ¿Hemos manejado todas las palabras que tal vez no estén en 'features'?

Una vez que pueda responder con confianza a estos, impresionará a los gerentes de contratación que buscan código limpio, eficiente y confiable.

-...

Pensamientos finales

LeetCode 1772 puede parecer “medio” en papel, pero esconde detalles sutiles que son material de entrevista de oro. Dominar este problema demuestra:

- **Agarro fuerte de las estructuras de datos** (mapas, conjuntos).
- ** Claridad algorítmica** (deduplicación, clasificación estable).
- ** Sensibilización sobre la calidad de la pareja** (capacidad, manejo del borde).

Muéstralo en tu cartera o GitHub – ¡es una victoria rápida para tu próxima entrevista de codificación! Feliz codificación 🚀.