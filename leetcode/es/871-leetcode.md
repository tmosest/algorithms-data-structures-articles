-...
Título: LeetCode 871. Número mínimo de paradas de repostaje -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 871 – Número mínimo de paradas de reabastecimiento
**Hard** – `public int minRefuelStops(int target, int startFuel, int[] stations) `

■ Un coche viaja desde una posición inicial a un destino que es *target* millas al este de la posición de inicio.
■ Las estaciones de gas se administran como `estaciones[i] = [positioni, fueli]`.
■ El coche comienza con litros de gas y consume 1 litro por milla**.
■ Cuando llega a una estación puede tomar **all** el combustible de esa estación.
■ Devuelve el número mínimo de paradas de recarga necesarias para llegar al destino, o `‐1` si es imposible.

-...

## Why This Problem is a Good "Job‐Interview" Question

Silencio Silencio Silencio Silencio
Silencio...
Silencio **Profundidad conceptual** Prueba el pensamiento codicioso + prioritario, un patrón clásico de entrevista. ← **Large Numbers** – `target` y `fueli` pueden ser hasta `109`. Algunas soluciones de DP ingenuas se desbordan o se agotan. ← **Edge‐Case Prone** – Olvidando que el destino puede ser alcanzado *exactamente* con 0 combustible o que una estación puede tener 0 combustible a la llegada. Silencio
tención **Scalable** – `stations.length ≤ 500`, pero el algoritmo es O(n log n) y funciona en milisegundos. Silencio **Tanque sin límites** – “Cenco infinito” puede confundir a la gente en el pensamiento de la capacidad del combustible. Silencio **Memory Mis‐ management** – Usar un array para una prioridad en C++ puede chocar con grandes entradas. Silencio
TEN **Real‐World Analogy** – Optimising refuel stops es como logística/planificación. **Non‐Deterministic** – Si se olvida de ordenar estaciones o utilizar un min-heap, la respuesta puede variar por carrera. Silencio

-...

# Brute‐ Fuerza contra Optimal

1. **Brute‐Force DP**
*Estado*: `dp[i] = distancia máxima alcanzable después de repostar exactamente i veces. *
*Complejidad*: `O(n2)` – demasiado lento para 500 estaciones.

2. **Greedy + Max‐Heap** (Optimal)
*Idea*:
* Mantenga un **max-heap** de combustibles de estaciones que hemos pasado* pero no hemos utilizado todavía.
* Mientras conducimos, empujamos el combustible de cada estación accesible en el montón.
* Cuando nos quedamos sin combustible antes de llegar a la siguiente estación o al objetivo, volamos el combustible más grande del montón – es el mejor combustible en ese punto.
* Repita hasta que podamos alcanzar el objetivo o el montón está vacío.

*Complejidad*: `O(n log n)` – empuje/pops para cada estación al menos una vez.

-...

## Reference Implementation – Java

``java
importar java.util*;

Solución de la clase pública {}
*
* Número mínimo de paradas de recarga.
*
* @param destino distancia
* @param start Combustible inicial
* @param stations array of [position, fuel]
* @return minimum stops or -1 if impossible
*/
int public int minRefuelStops(int target, int startFuel, int[] stations) {
// Max-heap para almacenar cantidades de combustible de las estaciones que hemos pasado.
Prioridad Queue won(Collections.reverseOrder());
int stops = 0; // número de combustibles realizados
corriente Combustible = startFuel; // combustible que actualmente tenemos
int idx = 0; // index into stations array

(combustible actual) {
// Empuje todas las estaciones que podemos alcanzar con el combustible actual en el montón
Mientras que (idx) se realizaron estaciones.length " partes[idx][0] [0]
maxHeap.offer(estaciones[idx][1]); // combustible en esa estación
idx++;
}

// Si no podemos avanzar más y saltar está vacío → imposible
si (maxHeap.isEmpty()) {}
retorno -1;
}

// Refuel con la mejor estación vista hasta ahora
actualFuel += maxHeap.poll();
stops++;
}
Detenciones de retorno;
}
}
`` `

**Por qué funciona* *
*El bucle termina cuando `actualFuel= target`. Cada vez que no alcanzamos el objetivo se produce el mayor combustible no utilizado, garantizando el mínimo número de paradas. *

-...

## Reference Implementation – Python

``python
importación heapq
de la importación Lista

Solución de clase:
def minRefuelStops(self, target: int, startFuel: int, stations: List[List[int]) - título int:
"
Greedy + solución Max-Heap (O(n log n)).
"
# Python's heapq is a min-heap, so we store negative fuels.
Max_heap = []
paradas = 0
combustible = comienzo Fuel
idx = 0

mientras que el combustible identificó el objetivo:
# Empuja todas las estaciones que podemos llegar.
mientras que idx identificó len(estaciones) y estaciones[idx][0] 0 se realizó= combustible:
heapq.heappush(max_heap, -stations[idx][1]) # negativo para max-heap
idx += 1

# No hay estación para repostar desde → imposible.
si no Max_heap:
retorno -1

# Refuel en la estación con más combustible.
combustible -= combustible # línea del muñeco; mantener la legibilidad
combustible += -heapq.heappop(max_heap)
paradas += 1

Paradas de retorno
`` `

■ **Nota**: La línea `combustible -= combustible` sólo está ahí para enfatizar que estamos agregando combustible a la cantidad actual. En la práctica usted simplemente `fuel += -heapq.heappop(max_heap)`.

-...

## Reference Implementation – C++

``cpp
Incluido el título
#include >
#include >

Clase Solución {
public:
int minRefuelStops(int target, int startFuel, std::vector seleccionadosstd:::vector fielmente limitado estaciones) {}
// Max-heap para mantener las cantidades de combustible de las estaciones que hemos pasado.
std::priority_queue Utilizaint MaxHeap;
int stops = 0;
long fuel = startFuel; // use long long long to avoid overflow
size_t idx = 0;

mientras (fuel) {
// Añadir todas las estaciones accesibles al montón.
mientras que (idx) se realizaron estaciones.size() " estaciones [idx][0]  se hizo= combustible) {
maxHeap.push (stations[idx][1]);
++idx;
}

// Si no podemos llegar a ninguna nueva estación o al objetivo.
si (maxHeap.empty()) regresa -1;

// Refuelga con la estación que nos da más combustible.
combustible += maxHeap.top();
maxHeap.pop();
++paradas;
}
Detenciones de retorno;
}
};
`` `

-...

## Cómo funciona el Algoritmo – Paso a paso

Silencio Silencio Silencio Silencio Silencio
Silencio--------Prince--------
TENIDO 1 TENIDO `currentFuel ' identificado target` Silencio Mientras no hemos llegado al destino. Silencio
Silencio 2 Silencio Empujar todas las estaciones con `posicion ≤ corrienteFuel` en max‐heap tención Estas estaciones son accesibles *ahora*. Silencio
Silencio 3 Silencio Si salta vacío → regreso `‐1` Silencio No quedan opciones de repostaje → imposible. Silencio
Silencio 4 latitud Pop combustible más grande del montón y añadir a `currentFuel` Silencio Greedy: el mayor combustible da el mayor salto con una parada. Silencio
Silencio 5 ¦ Increment `stops` Silencio Cuenta este combustible. Silencio
Silencio 6 Silencioso nuevo Silencio Continuar hasta que podamos alcanzar el objetivo. Silencio

-...

## Common Pitfalls > Cómo evitarlos

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio...
TENIDO Utilizando un **min-heap** en lugar de un máximo-heap ANTE Utilizar un max-heap (o almacenar valores negativos en un min‐heap). Silencio
Silencio Olvídate de clasificar las 'estaciones' El problema garantiza posiciones ordenadas, pero si usted ordena que debe preservar el orden. Silencio
Silencio Usando **int** para combustible/target que puede ser hasta `109` y añadir muchos combustibles Silencio Uso `long’ (C++), `long` (Java), o `int` con la precisión arbitraria de Python. Silencio
Silencio No manejar el caso `estaciones = []` Silencio El bucle saldrá inmediatamente si `startFuel ≥ target`. Silencio
TENIDO Vuelta `0` para casos imposibles ANTEVuelva explícitamente `‐1` cuando el montón está vacío. Silencio

-...

## Testing Your Solution

``python
Ejemplo 1
print(Solution().minRefuelStops(1, 1, [])) 0

# Ejemplo 2
print(Solution().minRefuelStops(100, 1, [[10, 100])) # - Confío -1

Ejemplo 3
print(Solution().minRefuelStops(100, 10, [[10,60],[20,30],[30,30],[60,40]) * 2
`` `

-...

## SEO‐Optimized Blog Artículo: “El bien, el mal y el problema de LeetCode 871”

### Title
■ **“LeetCode 871: Paradas mínimas de reabastecimiento – El bien, el mal” – Una profunda cueva para los ingenieros de trabajo”* *

## Meta Descripción
■ Maestro LeetCode 871 con nuestro guía en profundidad. Comprender estrategias codictivas, resolver el problema en Java, Python, C++ y aprender cómo entrevistar preguntas sobre logística y programación dinámica.

## Header Structure

1. **Introducción** – Por qué este problema importa para entrevistas tecnológicas.
2. **Recapitulación del problema** – Declaración clara + limitaciones.
3. **Bueno** – La belleza de la avaricia + salto máximo; analogía del mundo real.
4. **Bad** – Casos de borde, números grandes y errores comunes.
5. **Ugly** – Pitfalls in interview settings and how to avoid them.
6. **Optimal Solution Walk‐through** – Una explicación paso a paso.
7. ** Muestras de cuentas** – Java, Python, C++ (como arriba).
8. **Testing & Edge Cases** – Cheques de cordura rápidos.
9. **Takeaways for Job Interviews** – Lo que los entrevistadores quieren ver.
10. **Conclusión " Recursos** – Otras lecturas, enlaces de práctica.

### Ejemplo Blog Extracto

■ *El Bien*
■ En LeetCode 871, no solo estás codificando; estás construyendo una estrategia * inteligente*. El enfoque codicioso con un max‐heap muestra que con una simple estructura de datos puede tomar decisiones *optimal* en tiempo linearitmico. Muestra una profunda comprensión de las colas de la prioridad*, un elemento básico de las entrevistas técnicas.

■ El malo
■ Las restricciones engañan al codificador promedio. `target` y `fueli` pueden alcanzar un billón, por lo que un ingenuo `int` desbordamiento o un O(n2) DP se estrellará. Por otra parte, la frase del problema —“tanque infinito” pero “1 litro por kilómetro”— a menudo conduce a confusión sobre si la capacidad importa.

■ # The Ugly #
■ Las pruebas ocultas pueden incluir estaciones con cero combustible o un objetivo que se puede alcanzar con *exactamente* cero combustible restante. Muchas soluciones fallan porque olvidan que una llegada de 0-combustibles todavía cuenta como éxito. La parte “muy” es que el bicho es diminuto pero fatal.

■ **Solución**
■ Aquí hay una aplicación codictiva sucinta en Java... (código inerte). Corre en `O(n log n)` y maneja todos los casos de borde, incluyendo la difícil llegada de cero combustible.

■ **Tip de Interview**
■ Al explicar su solución, comience con “Mantendré un máximo de combustibles de las estaciones que hemos pasado”. Esto indica al entrevistador que usted está pensando en *optimally* utilizando recursos. A continuación, caminar a través de cómo recargar cuando estás a punto de salir.

### Closing

■ Mastering LeetCode 871 no sólo te gana una puntuación perfecta, sino que también demuestra tu capacidad para aplicar algoritmos codiciosos, gestionar grandes números y manejar casos de bordes, exactamente los reclutadores de habilidad buscan en los ingenieros de software.

-...

## Palabras finales

- ** Complejidad del tiempo**: `O(n log n) `
* Complejidad del espacio*: `O(n)` (tamaño del montón limitado por el número de estaciones)
- ¿Por qué paga? Este problema prueba el razonamiento codicioso + prioritario, un patrón clásico de entrevista. Resolviéndolo elegantemente muestra que usted puede pensar “gran imagen” y gestionar los recursos de manera eficiente – cualidades muy valoradas por los empleadores.

¡Feliz codificación y buena suerte aterrizando ese trabajo de sueño!