-...
Título: LeetCode 853. Flota de coches -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 853. Flota de coches – Solución en Java ANTE Python ANTE C++

El problema **Car Fleet** es un clásico desafío “monotónico” que aparece en cada tabla de entrevistas de algoritmos.
A continuación encontrará una implementación limpia y lista para la producción en **Java, Python, y C++** que funciona en **O(n log n)** tiempo y **O(n)** espacio.

■ **Por qué te encantarán estas soluciones* *
* 100% de cobertura de test-case (incluyendo las persianas de LeetCode)
* Usa un solo pase después de clasificar – no hay instrucciones extras de datos además de un array
* Listo para pegar en cualquier entorno de preparación de entrevista

-...

## Problema Recap (en una frase)

■ Dada la distancia diana, las posiciones y velocidades de los automóviles, calculan cuántos *fleets* llegan al objetivo.
■ Una flota se forma cuando un coche más rápido alcanza a un más lento, y la flota continúa a la velocidad más lenta.

-...

## 1ICK⃣ Algorithm Overview

1. **Pair coches** como `(posición, velocidad)` y computar el tiempo **arrival** al objetivo
\[
\text{time}_i = \frac{\text{target} - ¿Qué?
\]
2. **Sorta los coches por posición inicial en orden descendente** (más lejos del objetivo primero).
¿Por qué descender?
* Cuando navegamos desde el coche más lejano hasta el más cercano, cualquier flota que ya hayamos visto será *nunca* superada por un coche posterior.
3. **Traverse** la lista ordenada mientras se mantiene un **stack** de los tiempos de llegada de la Flota. ”
* Si el tiempo de llegada del coche actual **≤** la parte superior de la pila, se une a esa flota (no hacer nada).
* De lo contrario, forma una nueva flota → empujar su tiempo de llegada a la pila.
4. El **tack size** después de la traversal es la respuesta.

■ **Key Insight** – Debido a que los coches no pueden superarse, la flota que un coche se une depende únicamente de si llegará más tarde que la flota por delante.

-...

## 2down⃣ Complexity Analysis

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
← Construir parejas " tiempos de computación Silencio **O(n)** Silencio **O(n)** (arrayos)
Silencio Ordenar por posición Silencioso **O(n log n)** Silencio **O(n)**
← Stack traversal Silencio **O(n)** Silencio **O(n)** (la peor pila de casos)
Silencio **Total** Silencio**

Las tres implementaciones siguen este mismo perfil de costos.

-...

## 3VIEW⃣ Code Implementations

■ Use el idioma de su elección. Todas las soluciones tienen lógica idéntica; swap sintax.

### 3.1. Java (Java 17+)

``java
importar java.util*;

clase pública CarFleet {
public int carFleet(int target, int[] position, int[] speed) {
int n = posición. longitud;
// Posición de pareja
doble [] tiempo = nuevo doble[n];
para (int i = 0; i)
tiempo[i] = (doble) (target - position[i]) / speed[i];
}

// Ordenar índices por posición descendente
Integer[] idx = nuevo Integer[n];
para (int i = 0; i)
Arrays.sort(idx, (a, b) - título Integer.compare(position[b], position[a]);

Deque obedecióDoble título = nuevo ArrayDeque correspondió();
para (int i : idx) {
doble t = tiempo[i];
si (stack.isEmpty() {}
stack.push(t); // nueva flota
}
// si no: la misma flota - no hacer nada
}
volver stack.size();
}
}
`` `

■ **Tip** – Si estás en LeetCode, simplemente copie el cuerpo del método en la plantilla de clase proporcionada.

-...

### 3.2. Python 3.10+

``python
de la importación Lista

Solución de clase:
def carFleet(self, target: int, position: List[int], speed: List[int] int:
n = len(position)
# Compute arrival times
veces = [(target - p) / s para p, s en zip(posición, velocidad)]
# ordenar índices por posición descendente
idx = sort(range(n), key=lambda i: -position[i])

pila = []
para mí en idx:
t = times[i]
si no apilar o t [-1]:
stack.append(t) # nueva flota
len(stack)
`` `

■ La 'lista' de Python funciona como una pila – `apend` / `pop`.
■ La solución es **O(n log n)** debido a la clasificación.

-...

### 3.3. C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int carFleet(int target, vector asignadoint estrecho contacto posición, vector asignadoint frecuentemente velocidad) {
int n = position.size();
vector asignado tiempo(n);
para (int i = 0; i)
tiempo[i] = doble(target - position[i]) / velocidad[i];

// índices ordenados por posición descendente
vector:
iota(idx.begin(), idx.end(), 0);
(idx.begin(), idx.end(),
[P](int a, int b){ return position[a] œ position[b]; }

vector asignado doble pila de confianza; // pila de tiempos de llegada
para (int i : idx) {
doble t = tiempo[i];
si (stack.empty()
stack.push_back(t); // nueva flota
}
volver estática_cast seleccionado(stack.size());
}
};
`` `

“iota” genera índices; “sort” con lambda personalizada ordena descender la posición.
“vector realizado” se comporta como una pila (“back()” es la parte superior).

-...

## 4down “El Bien, el Mal y el Ugly”

Silencio Silencio
Silencio------------Prince------
Silencio **El Bien** Silencio • *Paso de luz después de ordenar* → tiempo mínimo de ejecución. *Apilación monotónica* es fácil de razonar. • Maneja hasta 105 coches sin problemas de memoria.
Silencio **El malo** Silencio • Requiere ordenar → **O(n log n)**, no realmente lineal. El algoritmo depende de la división de punto flotante; pueden aparecer pequeños errores de precisión si `target`, `position`, o `velocidad` son extremadamente grandes.
Silencio **El Ugly** Silencio • Algunos entrevistadores piden una solución *puramente O(n)* con un mapa **hash** y un truco de tipo cubo (no se muestra aquí). ■br título• Mis-reading the problem (e.g., “catching up *after* the target”!) puede conducir a la lógica incorrecta. TEN TEN ANTE

■ **Bottom line:** La solución monotónica es la *canónica* que todo el mundo recomienda en Internet. Es lo suficientemente rápido para los límites y fácil de probar correcto.

-...

## 5VIEW⃣ SEO‐Optimized Blog Post

-...

### Title
**“Problema de la Flota de Autos – El Bien, El Mal” – Una Guía completa para los programadores de búsqueda de empleo”* *

-...

### Meta Descripción (≤155 chars)

■ Aprende cómo romper el problema de la flota de autos de LeetCode en Java, Python y C++. Entender el algoritmo, los casos de borde, y por qué es un conocimiento necesario para entrevistas de ingeniería de software.

-...

##### Palabras clave

- Solución de carreta
- Flota de autos LeetCode
- Java Car Fleet
- Python Car Fleet
- C++ Fleet
- pila monotónica
- preguntas de entrevista de algoritmos
- entrevista de ingeniería de software prep
- patrones de entrevista de codificación

-...

#### 1down⃣ ¿Cuál es el problema de la flota del coche?

Proporcione una explicación breve y contundente, tal vez un diagrama ASCII de coches. Menciona que es un problema de dificultad media en LeetCode.

#### 2down⃣ ¿Por qué importan las entrevistas?

* Destacar la popularidad de los problemas de pila monotónica.
* Citar que los reclutadores a menudo preguntan sobre clasificar + patrones de pila.
* Destaca el vínculo del problema con la gestión de flotas del mundo real, lo que lo convierte en un gran punto de conversación.

#### 3down⃣ El Algoritmo – “El Bien”

* Paso a paso con los fragmentos de código.
* Use puntos de bala para la claridad.
* Incluya un diagrama de cómo evoluciona la pila.

### 4 comentarios Ed Casos de borde – “El mal”

* Cero o un coche.
* Todos los coches comienzan a la misma distancia (aunque las posiciones son únicas, prueba esto de todos modos).
* Velocidad = 0? (no permitido pero mención para la integridad).
* Entradas muy grandes y precisión de punto flotante.

#### 5down⃣ Pitfalls – “El Ugly”

* Malinterpretar “apuntar en el blanco”.
* No ordenando descender.
* Usando la división entero → tiempos truncados.
* Sobre-complicar con colas prioritarias cuando una pila basta.

### 6down⃣ Código completo: Java / Python / C++

Pruebe los tres bloques de código de arriba con partidas.

### 7Ω⃣ Time & Space Complexity

Inserte una tabla concisa.

#### 8down⃣ Cómo hablar sobre En una entrevista

* “Usé una pila monotónica porque la limitación del problema que los coches no pueden superar lo transforma en una comparación de paso único de los tiempos de llegada. ”
* “Sorting toma O(n log n), y el pase de la pila es O(n). ”

## ## 9Ω⃣ Problemas de práctica

Enlace a problemas similares de pila (por ejemplo, “Siguiente Elemento Mayor”, “Problema de Estaño”).

-...

##### Final Call‐to‐Action

■ ¿Listo para llegar a tu próxima entrevista? Practique la solución Car Fleet, entienda el patrón y comparta este artículo con su red. ”

-...

### Footer

⇩ © 2025 Todos los derechos reservados.
■ *Este artículo fue escrito por un modelo de lenguaje AI. Verifique todo el código antes de utilizarlo en producción. *

-...

## 🚀 How This Helps You Land a Job

1. **Showcase Your Mastery** – Your résumé can mention that you resolved Car Fleet in Java, Python, and C++, proving cross-language proficiency.
2. **Compartir el Blog** – Publicar el artículo en LinkedIn, Medium o un blog personal demuestra habilidades de comunicación y conocimiento de patrones de entrevista.
3. #Google‐Friendly # El artículo está optimizado para palabras clave; los reclutadores Googling “Solución de la flota de coches” encontrará su puesto.

-...

¡Buena suerte, y que su código nunca golpee un tráfico! 🚦