-...
Título: LeetCode 573. Simulación de ardilla -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 573. Simulación de ardilla
**Dificultad:**
**LeetCode URL:**

■ ** Objetivo** – La ardilla comienza en una celda dada, debe recoger *todas* nueces una por una, dejar caer cada tuerca debajo del árbol y finalmente regresar al árbol.
■ **Movimiento** – Cuatro direcciones solamente (hasta, abajo, izquierda, derecha).
■ ** Salida** – El número mínimo de movimientos requerido.

-...

## 📌 Core Insight

Cuando recoges una nuez, siempre tienes que caminar:

1. **Del árbol a la nuez** (o de la ardilla a la nuez si es el primero).
2. **De la tuerca de regreso al árbol** para dejarlo caer.

Si sumamos ingenuamente *2 × distancia(negro, árbol)* por cada tuerca duplicamos la pierna que la ardilla toma *primera* de su posición inicial a la primera tuerca.
Lo mejor que podemos hacer es elegir la tuerca que da el mayor *salvado*:

`` `
ahorro = distancia (no, árbol) – distancia (no, ardilla)
`` `

Por lo tanto, la distancia mínima es:

`` `
total = 2 × distancia (negro, árbol)
mínimo = total – max(salvar)
`` `

Esta fórmula se ejecuta en **O(n)** tiempo y **O(1)** espacio extra.

-...

##  Settlements

A continuación encontrará tres soluciones limpias y preparadas para la producción: una en **Java**, **Python**, y **C+**.
Todos usan el mismo ayudante de distancia de Manhattan.

## Java

``java
Solución de la clase pública {}
int public int minDistance(int height, int ancho,
int[] árbol, int[] ardilla,
int[][] tuercas] {
total = 0;
int maxSaving = Integer.MIN_VALUE;

para (int[] nuez : nueces) {
int ToTree = manhattan(nut, tree);
int ToSquirrel = manhattan(nut, ardilla);

total += ToTree * 2;
MaxSaving = Math.max(maxAhorro, distToTree - distToSquirrel);
}

retorno total - maxAhorro;
}

int privada manhattan(int[] a, int[] b) {
devolver Math.abs(a[0] - b[0]) + Math.abs(a[1] - b[1]);
}
}
`` `

## Python

``python
Solución de clase:
def minDistance(self, height: int, broad: int,
árbol: List[int], ardilla: List[int],
tuercas: List[List[int]) - título int:
total = 0
max_saving = flotante('-inf')

para la nuez en las nueces:
dist_tree = self._manhattan(nut, tree)
dist_squirrel = self._manhattan(nut, squirrel)

total += 2 * dist_tree
max_saving = max(max_saving, dist_tree - dist_squirrel)

total - Max.

@staticmethod
def _manhattan(a: List[int], b: List[int] int:
retorno abs(a[0] - b[0]) + abs(a[1] - b[1]
`` `

### C++

``cpp
Clase Solución {
public:
int minDistance(int height, int ancho,
vector implicado, árbol pequeño, vectorial
vector realizador realizador realizado injertado
largo largo total = 0; // utilizar largo tiempo para evitar el desbordamiento
Long long maxSaving = LLONG_MIN;

para (contigo auto cho nut : tuercas) {
larga distancia Árbol = manhattan (no, árbol);
largo tiempo distSquirrel = manhattan(nut, ardilla);

total += 2 * dist Árbol;
maxSaving = max(maxSaving, distTree - distSquirrel);
}
volver estática_cast seleccionado(total - maxAhorro);
}

privado:
long long manhattan(const vector conectado a, const vector implicado
devolver llabs(a[0] - b[0]) + llabs(a[1] - b[1]);
}
};
`` `

-...

## 📚 Blog Article – “Squirrel Simulation: The Good, the Bad, and the Ugly”

■ **SEO Palabras clave:** *Squirrel Simulation LeetCode*, *minDistance algoritmo*, *Java Python C++ Solución*, *problema de codificación de perspectiva*, * Distancia de Manhattan*, *diseño de algoritmo*

-...

### 1. Introducción

El problema **Squirrel Simulation** es un problema básico en LeetCode para aquellos que se preparan para las entrevistas de codificación. Le pide que encuentre el número mínimo de movimientos que una ardilla debe hacer para recoger todas las nueces y dejarlas debajo de un árbol, moviéndose sólo hacia arriba, abajo, izquierda o derecha. Aunque la declaración se siente caprichosa, en realidad toca en conceptos algorítmicos clásicos: **Manhattan distance** y **grita optimización**.

### 2. Why This Problem Rocks

- *Clear Constraints* No hay obstáculos, sólo límites de red.
- No es necesario que BFS Como no hay obstáculos, la distancia de Manhattan es exacta.
- **O(n) Solución** – Un solo paso a través de la lista de nueces le da la respuesta al instante.

### 3. La Solución Elegante – “El Bien”

← Paso Silencioso Lo que sucede
...------------------------------
Silencio 1 ← Compute **dist(nut, tree)** por cada nuez. Silencio Da las dos piernas que siempre serán tomadas: a los árboles y a la espalda. Silencio
Silencio 2 Silencio Sum `2 * dist(nut, tree)`. Cuento doble porque cada nuez necesita un viaje redondo. Silencio
Silencio 3 Silencio Compute **salvando** = `dist(nut, tree) – dist(nut, squirrel)`. Silencio Si empezamos con esta tuerca, reemplazamos la *tree → tuerca* con *squirrel → tuerca*. Silencio
Silencio 4 latitud Subtract the largest **saving** from the total. Esa es la primera nuez posible; todas las demás nueces permanecen en el patrón de ida y vuelta. Silencio

■ Resultado** – Un movimiento mínimo cuenta en tiempo lineal y espacio extra constante.

### 4. Casos de borde y Gotchas – “El mal”

Con hasta 5.000 nueces, el flujo entero puede colarse. Use `long' en C++ o `long` en Java/Python `int ` (que no tiene límites) de forma segura.
- Células inalcanzables El problema garantiza que todas las tuercas y el árbol están dentro de los límites, por lo que no se necesita un camino de determinación. Si el problema cambiara para incluir obstáculos, el atajo simple de Manhattan sería inválido.
- Coordenadas negativas Las limitaciones dicen que las coordenadas no son negativas, pero una implementación debe ser lo suficientemente robusta para manejar cualquier valor entero.

### 5. Cuando las cosas se mezclen – “El Ugly”

Si usted iba a hacer frente a una variante donde la ardilla no puede atravesar ciertas células (por ejemplo, “agujeros” o “agua”), el atajo de Manhattan se descompone. Necesitarías:

1. **Computación de Sendero Bruto** – BFS de cada nuez al árbol y de la ardilla a cada nuez, que es O(n · (h·w)).
2. ** Programación Dinámica o TSP** – El problema se transforma en una variante del vendedor itinerante, que es NP-hard.

Así, mientras que el problema de la simulación de ardilla es una maravillosa herramienta de enseñanza, extendiéndola sin cuidado rápidamente espirales en territorio de complejidad.

### 6. ¿Por qué deberías amar la solución

Una sola vuelta, un método de ayuda y un poco de matemáticas.
- **Performance** – Corre en microsegundos en las típicas pilas de entrevistas.
*Adaptability* – El patrón (doble cuenta + ahorro máximo restante) aparece en otros problemas de “colecta y vuelta”.

### 7. Escolta para entrevistas de trabajo

- **Descubre el argumento de Greedy** - Explicar por qué elegir la tuerca con el ahorro máximo da el primer movimiento óptimo.
- **Hablar de la complejidad** – O(n) tiempo, O(1) espacio es un gran punto de venta.
- **Mostrar versatilidad del lenguaje** – Proporcionar soluciones en Java, Python y C++ para demostrar amplitud.

-...

Conclusión

El problema de la simulación de ardilla es un ejemplo brillante de cómo un desafío aparentemente juguetón puede ilustrar el pensamiento algoritmo poderoso. Al aprovechar las distancias de Manhattan y un ajuste codicioso inteligente, obtenemos una solución elegante y eficiente.

Si usted está puliendo su preparación de entrevistas, la elaboración de un proyecto de cartera, o simplemente disfrutando de la alegría de codificación, este problema y su solución ofrecen una mezcla encantadora de claridad, desafío y dominio.

¡Feliz codificación, y que sus ardillas siempre recojan las nueces de la manera más corta posible!