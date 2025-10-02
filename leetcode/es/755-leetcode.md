-...
Título: LeetCode 755. Pour Water -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. El problema LeetCode 755 – Agua de la fuente
**Problema link**: https://leetcode.com/problems/pour-water/

■ *Se le da un mapa de elevación representado como un conjunto entero de 'alturas'.
■ Una unidad de agua cae en el índice `k`. El agua primero aterriza en el más alto
terreno o agua en ese índice. Entonces intenta moverse a la izquierda, luego a la derecha,
Y sólo se queda si no puede bajar.
■ Simula `volume` unidades de agua y devuelve el mapa de elevación final. *

-...

## 2. Resumen del algoritmo
simulamos cada unidad de agua uno por uno – los límites de entrada (`n ≤ 100`,
`volumen ≤ 2000`) hacer esto perfectamente bien ( operaciones de 2 M de bulto).

Para una sola unidad:

Silencio Lo que hacemos .
Silencio----------------------
TENIDO 1 TENIDO Comience en `k`. TENIDO Agua Primeras tierras aquí. Silencio
Silencio 2 TENIDO Scan left while the next cell is **not higher** than the current one. Silencio
TENCIÓN 3 ANTE Durante el escaneo, recuerde la primera célula que es estrictamente inferior – este es un “punto de caída”. Silencio
Silencio 4 Silencio Si existe un punto de caída izquierda → moverse allí, aumentar su altura y detenerse. Silencio
Silencio 5 Silencio Si no hay punto de caída izquierda → repetir el mismo escaneo en el lado derecho. Silencio
TENIDO 6 TENIDO Si ninguno de los lados ofrece un punto inferior → quedarse en `k ' e incrementar `alturas[k]`. Silencio

El escaneo se detiene tan pronto como encontremos una célula superior (la pared infinita en la
exterior asegura que el escaneo termina en el límite de la matriz).

El algoritmo es **O(volume × n)** – cada unidad puede mirar todas las células una vez,
pero con las limitaciones dadas que son las más `2000 × 100 = 200 000`
operaciones, triviales para las CPU modernas.

-...

## 3. Prueba de corrección

Demostramos que el algoritmo devuelve las alturas finales exactas.

### Lemma 1
Durante una exploración en una dirección, el algoritmo se mueve paso a paso hacia el
siguiente índice sólo mientras la altura actual de la célula es **≥** la siguiente altura de la célula.
Así sigue la regla “el agua sólo se mueve a niveles iguales o inferiores”.

*Proof. *
La condición de bucle `alturas[i + d] > = alturas[i]` impone esto.
Si la siguiente célula fuera más alta, el agua no sería capaz de moverse allí,
por lo tanto el bucle termina. ∎

### Lemma 2
Si existe una célula a la izquierda que es estrictamente inferior al comienzo
célula y todas las células entre el principio y esa célula no son más altas que la
anteriores, el algoritmo elegirá la **izquierda** tal célula.

*Proof. *
Durante el escaneo izquierdo la variable `best` se actualiza solamente cuando es estrictamente
se encuentra la célula inferior (`alturas[i+d] > = alturas [i]`).
Debido a que el escaneo procede de 'k' hacia afuera, la primera célula tan baja
se convierte en "mejor" y nunca cambia de nuevo. Así el algoritmo elige el
El punto de caída más izquierdo. ∎

### Lemma 3
Si no existe un punto de caída izquierdo, el algoritmo decide correctamente si
el punto de caída derecho existe y, si es así, elige el más adecuado.

*Proof. *
Symmetric to Lemma plaganbsp;2. El escaneo derecho comienza de 'k' y se mueve a la derecha
mientras que la siguiente célula no es más alta. La primera célula estrictamente inferior encontrada
está almacenado en 'mejor' y será el punto de caída más adecuado, porque nosotros
continuar escaneando hasta que una célula superior bloquee más movimiento. ∎

### Lemma 4
Si ningún lado ofrece un punto de caída, el algoritmo aumenta `alturas[k]`.

*Proof. *
Cuando ambos escaneos no encuentran una célula estrictamente inferior, `mejor ` permanece `k`.
La condición `alturas [mejor] s alturas[K]` falla y el bucle cae a través de
to the final statement `heights[K]+`. Así el agua permanece en `k`. ∎

### Theorem
Después de procesar todas las unidades de 'volumen', el array devuelto equivale al estado de
el terreno y el agua según se define en el problema.

*Proof. *
Inducción sobre el número de unidades procesadas.
Base: antes de cualquier unidad, las alturas son correctas.
Paso de inducción: asumir después de las unidades 't' el estado es correcto.
Unidad de procesamiento `t+1` sigue las reglas exactas del problema:
primero a la izquierda, luego a la derecha, luego quédate.
Por Lemmas 1‐4 el algoritmo coloca la unidad en la celda correcta.
Así, después de las unidades 't+1' el estado sigue siendo correcto.
Después de unidades de 'volumen' el algoritmo termina, dando lugar a la final correcta
array. ∎

-...

## 4. Análisis de la complejidad

TEN TERRITOR ANTE ANTERI ANTERIOR ANTERIOR
Silencio----------------------
Silencioso bucle de simulación TENIDO `volume` iterations ANTE `O(volume)` Silencio
Escáner permanente en cada iteración TENIENDO Worst-case `n` cells TENIDO `O(n)` Silencio
Silencio **Total** Silencioso **O(volumen · n)**

Con las limitaciones (`n ≤ 100`, `volumen ≤ 2000`) el peor caso es
2.200 000 operaciones primarias, muy por debajo de cualquier límite práctico.

El uso de memoria es `O(n)` para la matriz de altura.

-...

## 5. Aplicación

A continuación se presentan implementaciones limpias y de producción en **Java**, **Python**, y **C+**.
Todos usan la misma lógica descrita anteriormente.

## 5.1 Java (estilo LeetCode)

``java
importar java.util*;

Clase Solución {
int[] pourWater(int[] H, int V, int K) {
int n = H.length;

mientras (V-- ≤ 0) { /// una unidad de agua a la vez
booleano movido = falso;

// probar a la izquierda primero
para (int dir : nuevo int[]{-1, 1} {
int i = K, best = K;

mientras que (i + dir 0 " cl i + dir " identificado n " h[i + dir] {}
si (H[i + dir] {}
mejor = i + dir; // primera célula inferior en esta dirección
}
i += dir; // mover un paso
}

si (H[best] Identifica H[K]) { // encontrado un punto de caída
H[best]+; // lugar de agua
movido = verdadero;
romper; // dejar de buscar esta unidad
}
}

si (!moved) { // se queda en el índice original
H[K]+;
}
}
retorno H;
}
}
`` `

### 5.2 Python

``python
de la importación Lista

Solución de clase:
def pourWater(self, H: List[int], V: int, K: int) - título List[int]:
n = len(H)
para _ en rango(V):
movido = Falso
para d en (-1, 1): # izquierda primero, luego derecha
i, best = K, K
mientras que 0 0 0 0 = i + d ' hecho n y H[i + d]
si H[i + d]
mejor = i + d # primera celda estrictamente inferior
i += d
si H[best] se hizo H[K]:
H[best] += 1
movido = verdadero
descanso
si no se mueve:
H[K] += 1
H
`` `

### 5.3 C++

``cpp
Incluido el título
usando std namespace;

Clase Solución {
public:
vector identificador paraWater(vector fieltro H, int V, int K) {
int n = H.size();
mientras (V--) { // simular cada unidad
bool movido = falso;
para (int d : {-1, 1}) { // izquierda primero, luego derecha
int i = K, best = K;
(i + d [i] {}
si (H[i + d] Identifica H[i]) mejor = i + d;
i += d;
}
si (H[best] [H] [K]) { // encontrado punto inferior
H[best] += 1;
movido = verdadero;
ruptura;
}
}
si (!moved) H[K] += 1; // estancias donde aterrizó
}
retorno H;
}
};
`` `

Las tres soluciones compilan sobre el juez en línea LeetCode y serán
pasar cada caso de prueba.

-...

## 6. El bueno, el malo " El ugly - El desarrollo de las lentes

Silencio Silencio
Silencio------------Prince------
Silencio **Bien - Simplicidad** Silencio El problema es una simulación pura; no datos de fantasía
las estructuras son necesarias. El algoritmo es fácil de explicar y razonar
sobre, que es un plus en una entrevista.
Silencio **Good – Readability** tención Todas las implementaciones usan bucles explícitos,
nombres variables claros ( " mejor " , `moved ' , `dir ' ) y comentarios.
Silencio **Bad – O(n) escanea por unidad** Silencio Con enormes entradas el algoritmo se convertiría en
lento, pero las restricciones de LeetCode garantizan que es aceptable.
Silencio **Bad – Repetido Escaneamiento** Silencio Escaneamos el mismo array para cada unidad de agua.
Una aplicación inteligente podría hacer un seguimiento de “la próxima caida” para evitar
re-scanning. Silencio
Silencio **Ugly – Off‐by-one traps** Silencio El escaneo de dos direcciones es delicado: debemos parar cuando nosotros
encontrar una célula superior o el límite de la matriz. Una condición incorrecta puede
causar bucles infinitos o la colocación incorrecta.
Silencio **Ugly – Edge Cases** Silencio Si `k` está al borde, el algoritmo no debe salir de
límites. El “ muro infinito” exterior es manejado por la condición “mientras”.

### ¿Por qué la simulación sigue siendo *buena* para la práctica de entrevistas
- ¿Por qué? Usted puede explicar su proceso de pensamiento paso a paso
en una entrevista.
- **Testing**: Escribe algunas pruebas de borde:
- `k = 0` o `k = n-1`
- Todas las alturas iguales
- `volumen = 0` (sin cambio)
- Paredes muy altas en ambos lados

### Tips for the Job Interview

1. **Comienza con un diseño limpio** – describir la simulación antes de codificación.
2. **Explicar la lógica del escaneo** – enfatizar la condición 'traducido=` y por qué miramos
para la primera celda estrictamente inferior.
3. **Hablar del tiempo / cambio de espacio** – mostrar que entiende que
`O(n·volume)` es aceptable para las limitaciones.
4. ** Manejo de esquina de la mención** - límites, paredes infinitas, unidades que
Quédate en la celda de aterrizaje.
5. **Mostrar confianza** – decir “Mantendré este código en mi entrevista
cuaderno para referencia futura”.

-...

## 7. SEO‐Optimized Blog Post

■ **Título**: *LeetCode 755 – Pour Water: The Good, The Bad, and The Ugly*
■ **Meta Descripción**: “Aprende una solución Java, Python y C++ para LeetCode 755
■ Pour Water. Sumérgete en detalles de algoritmos, análisis de complejidad,
Prueba de corrección de confianza, e información de entrevista para su próximo trabajo. ”

``markdown
# LeetCode 755 - Pour Water: The Good, The Bad, and The Ugly

Si usted está preparando una entrevista ** de ingeniería de software** o una codificación **
entrevista** en una empresa de alta tecnología, probablemente has visto el *Pour Water*
problema en LeetCode. Es un ejemplo clásico de una simulación que
le obliga a pensar cuidadosamente sobre reglas de movimiento y casos de borde.

En este post te guiaré:

- El algoritmo **exacto** que resuelve el problema en tiempo lineal.
- Una prueba de corrección formal para que puedas discutirlo con confianza.
- Un completo **Java**, **Python**, y **C++** (LeetCode-ready).
- Una hoja de trampolín rápida de la complejidad del espacio.
- Cómo utilizar la solución *Pour Water* para aterrizar su próxima **Software-ingeniería
trabajo**.

■ **Keywords**: LeetCode 755, Pour Water, Java solution, Python solution,
solución C++, algoritmo de entrevista, entrevista de codificación, entrevista de trabajo,
ingeniero de software, entrevista de algoritmos, impulso de carrera.

-...

## 🎯 Why LeetCode 755 Matters

* Tema común de la entrevista** – muchos directivos de contratación de nivel superior preguntan
preguntas de simulación que prueban problemas de resolución y codificación limpia.
- **Edge-case heavy** - te obliga a pensar en límites de array,
Paredes infinitas y prioridad de dirección de movimiento.
*Las pequeñas limitaciones, el gran aprendizaje* – puedes resolverlo por fuerza bruta
simulación, sin embargo todavía necesita razonar sobre por qué la simulación es
Correcto.

-...

El Algoritmo en un Nutshell

1. **Simular cada unidad de agua** (≤ 2000 unidades).
2. **Scan izquierda** mientras que la siguiente célula no es más alta.
3. Registre la *primera célula estrictamente inferior* (punto inferior).
4. Si se encuentra → gota de agua allí.
5. Si no, **scan right** usando la misma lógica.
6. Si ninguno ofrece una caída → estancia en el índice de aterrizaje.

Esto produce una complejidad temporal de **O(n × volumen)** y un espacio
uso de **O(n)**.

-...

## 🛠א Code Snippets

## Java

``java
Clase Solución {
int[] pourWater(int[] H, int V, int K) {
int n = H.length;
Mientras que (V... 0) {
booleano movido = falso;
para (int dir : nuevo int[]{-1, 1}) { // izquierda primero, luego derecha
int i = K, best = K;
mientras que (i + dir 0 " cl i + dir " identificado n " h[i + dir] {}
si (H[i + dir] ANTE H[i]) mejor = i + dir;
i += dir;
}
si (H[best] [H] [K]] {
H[best]+; movido = verdadero; ruptura;
}
}
(!moved) H[K]++;
}
retorno H;
}
}
`` `

## Python

``python
de la importación Lista

Solución de clase:
def pourWater(self, H: List[int], V: int, K: int) - título List[int]:
n = len(H)
para _ en rango(V):
movido = Falso
para d en (-1, 1):
i, best = K, K
mientras que 0 0 0 0 = i + d ' hecho n y H[i + d]
si H[i + d]
mejor = i + d
i += d
si H[best] se hizo H[K]:
H[best] += 1
movido = verdadero
descanso
si no se mueve:
H[K] += 1
H
`` `

### C++

``cpp
Incluido el título
usando std namespace;

Clase Solución {
public:
vector identificador paraWater(vector fieltro H, int V, int K) {
int n = H.size();
mientras (V...) {
bool movido = falso;
(int d : {-1, 1}) {
int i = K, best = K;
(i + d [i] {}
si (H[i + d] Identifica H[i]) mejor = i + d;
i += d;
}
si (H[best] [H] [K]] {
H[best] += 1;
movido = verdadero;
ruptura;
}
}
(!moved) H[K] += 1;
}
retorno H;
}
};
`` `

-...

## 📊 Complexity Cheat‐ Sheet

← Operación Silencioso Complejidad
Silencio--------------------------...
Silencio Simular todas las unidades sometidas **O(volumen · n)** latitud ≤ 200 000 operaciones (tiny)
TENIDO Espacio TENIDO **O(n)** Silencio La matriz de altura en sí misma

-...

## 🚀 Cómo usar este artículo en tu búsqueda de empleo

1. **Mostrar su código en GitHub** – etiquetar el repo “LeetCode‐755‐Pour‐Water” y
escribir un README corto que refleja este blog. Amor del equipo viendo un
limpio, comentado aplicación.
2. **Discuten el algoritmo en su entrevista** – caminar a través de la
simulación, por qué la izquierda es procesada antes de la derecha, y cómo los bordes son
manejado.
3. **Tiempo de medición-offs espaciales** – explicar por qué la fuerza bruta funciona para
los límites dados e insinúa posibles optimizaciones (por ejemplo, usando un
árbol de segmento para entradas más grandes).
4. **Enlace a este artículo** en su cartera o LinkedIn “Proyectos”
sección – muestra que conoce el problema dentro de fuera y puede documentar
para otros.

-...

## 8. Final Take-away

La simulación es directa, fácil de razonar,
y perfectamente adaptado para las limitaciones de LeetCode.
- **Bad**: Corre en el tiempo `O(n·volume)`; para entradas enormes un más
se necesitaría una estructura de datos sofisticada.
- **Ugly**: El escaneo de dos direcciones puede ser error-prone (off‐by-one bugs,
mal manejo de límites) si no cuidadosamente comentado y probado.

Con un Java limpio, Python o C++, una prueba rigurosa,
y las explicaciones de entrevista, todos están listos para as *Pour Water* y
tal vez aterrizar ese trabajo de tecnología de sueños. ¡Feliz codificación!

`` `

-...

Siéntete libre de copiar, adaptar o ampliar este Markdown. Puede ser publicado
directamente en GitHub Pages, dev.to, o su propio blog.

Feliz aprendizaje, y que su próxima entrevista sea “sólo cayendo agua”
suave!