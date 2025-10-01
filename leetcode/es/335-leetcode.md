-...
Título: LeetCode 335. Autocruzamiento -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Solución – Un paso, O(n) tiempo " O(1) espacio

El problema de “autocrossing” clásico se puede resolver en un solo escaneo lineal
Revisando sólo los últimos movimientos.
Porque la dirección siempre gira en sentido contrario (North → Oeste → Sur → Este → ...),
el camino sólo puede intersectarse en algunos patrones específicos:

Silencio tóxico La situación
Silencio--------------...
Silencio **Standard** – el segmento i‐th cruza el segmento i-2. TENIDO `dist[i] Èste= dist[i‐2] " нет[i‐1] Silencio
tención **Especial 4-paso** – el segmento i‐th toca el segmento i‐3 (cuando i≥4). Silencio `dist[i‐1] == dist[i‐3] Silencio
tención **Especial 5-paso** – el segmento i-th corta un lazo abierto en los 5 pasos anteriores (cuando i≥5). [i‐4] < > > > [i-4] < > > > > > > > [i‐1] + dist[i-5] > < > > > > > > } > Silencio

Si alguna de estas tres condiciones es verdadera, el camino se ha cruzado.
De lo contrario continuamos escaneando hasta el final del array.

### Por qué funciona

- Después de cada cuatro movimientos la dirección repite, así que el único posible nuevo
intersección es con un segmento que fue dibujado **2** o **4** hace unos pasos.
- El tercer caso se ocupa de la situación “superior” donde el quinto segmento
superpone un bucle creado por los segmentos anteriores.
- Las condiciones se derivan de las longitudes relativas de los involucrados
segmentos; son necesarios y suficientes para que ocurra un cruce.

### Complexity

TEN TERMINAR TENIDO Análisis ANTE
Silencio...
Silencio **Hora** Silencioso `O(n)` – uno pasa a través de la matriz
Silencio** – sólo se utilizan algunas variables enteros

-...

## 2. Código

A continuación se muestran las implementaciones de un paso limpio en **Java**, **Python**, y **C+**.

#### 2.1 Java

``java
Solución de la clase pública {}
*
* Devuelve la verdad si el camino definido por la distancia[] se cruza.
* @param distancia una serie de números enteros positivos
* @return true if self-crossing, false otherwise
*/
booleano público es SelfCrossing(int[] distance) {}
si (distancia == null ¦
devolver falso; // menos de 4 movimientos no pueden cruzar
}

para (int i = 3; i) i++) {
// Caso 1: Línea actual cruza la línea 2 pasos atrás
si (distance[i] distancia[i - 2] "
distancia[i - 1]
retorno verdadero;
}

// Caso 2: La línea actual toca la línea 3 pasos atrás
si
distancia[i - 1 == distancia[i - 3] "
distancia[i] + distancia[i - 4] distancia[i - 2) {
retorno verdadero;
}

// Caso 3: La línea actual cruza un bucle abierto en los últimos 5 movimientos
si
distancia[i - 2] - 4] "
distancia[i] + distancia[i - 4] distancia[i - 2] "
distancia[i - 1] + distancia[i - 5] distancia[i - 3] "
distancia[i - 1]
retorno verdadero;
}
}

devolver falso;
}
}
`` `

### 2.2 Python

``python
Solución de clase:
def es SelfCrossing(self, distance: list[int]) - conviene bool:
""Retorno Verdadero si la caminata se cruza.""
si len(distance)
Retorno Falso

para i en rango(3, len(distance)):
# 1er caso
si (distance[i] distancia[i - 2] y
distancia[i - 1] <= distancia[i - 3]):
Retorno

# 2nd case
si 4 y 4
distancia[i - 1 == distancia[i - 3] y
distancia[i] + distancia[i - 4] distancia[i - 2]
Retorno

# 3rd case
si
distancia[i - 2] > distancia[i - 4] y
distancia[i] + distancia[i - 4] distancia[i - 2] y
distancia[i - 1] + distancia[i - 5] distancia[i - 3] y
distancia[i - 1] <= distancia[i - 3]):
Retorno

Retorno Falso
`` `

### 2.3 C++

``cpp
Clase Solución {
public:
bool es SelfCrossing(vector asignadoint frecuentemente distancia) {}
si (distance.size() ANTE 4) devolver falso;

para (int i = 3; i) ++i) {
Caso 1
si (distance[i] distancia[i - 2] "
distancia[i - 1]
retorno verdadero;
}

// Caso 2
si
distancia[i - 1 == distancia[i - 3] "
distancia[i] + distancia[i - 4] distancia[i - 2) {
retorno verdadero;
}

// Caso 3
si
distancia[i - 2] - 4] "
distancia[i] + distancia[i - 4] distancia[i - 2] "
distancia[i - 1] + distancia[i - 5] distancia[i - 3] "
distancia[i - 1]
retorno verdadero;
}
}
devolver falso;
}
};
`` `

Los tres francotiradores se ejecutan en el tiempo `O(n)` y utilizan sólo espacio extra constante.

-...

## 3. Artículo del Blog

■ *Título*
■ Auto-Crossing en LeetCode 335: El Bien, el Mal y el Ugly

■ **Meta‐Description* *
■ Aprende a resolver LeetCode 335 – “Auto Crossing” – en Java, Python y C++ con un algoritmo de un paso o n). Entender la lógica del patrón, las trampas y los casos de borde. Perfecto su preparación de entrevistas para preguntas de algoritmo.

-...

#### 3.1 Introducción

Cuando se trata de entrevistas de algoritmos, problemas de LeetCode que implican geometría o simulación de ruta a menudo parecen intimidantes. “El autocruzamiento” (Problema 335) es uno de esos desafíos: caminas en una espiral en sentido contrario y necesitas determinar si tu camino se cruza.

A primera vista, usted podría pensar que tiene que mantener un conjunto completo de coordenadas o utilizar una rutina de intersección de segmento de línea—una pesadilla O(n2). Pero el verdadero secreto está en el patrón **directional** del paseo. Una vez que lo vea, la solución colapsa a un puñado de simples controles de desigualdad.

Este post caminará a través de esa visión, presentará una solución concisa de un paso, discutir las trampas comunes, y le dará código listo para copiar en Java, Python y C++. Al final, usted será capaz de explicar el problema, el algoritmo, y la lógica del perímetro a cualquier panel de entrevista.

-...

#### 3.2 Problema Recap

Usted comienza en el origen `(0,0)` en un plano 2-D.
Usted recibe un array `distancia[]` de números enteros positivos.
Muévete.

1. `distance[0]` meters **North**
2. `distance[1] ́ meters **West**
3. `distance[2]` meters **South**
4. `distance[3]` meters **East**
5. ... y repetir en sentido contrario.

Vuélvete 'verdad' si el camino se cruza; de lo contrario `falso'.

■ **Constraints**
≤ 10^5`
• `1 ≤ distancia[i] ≤ 10^5`

El reto es hacerlo en ** tiempo lineal** y ** espacio constante**.

-...

### 3.3 El Bien - ¿Por qué funciona un Pase Uno

Debido a que la dirección cambia previsiblemente (Norte → Oeste → Sur → Este → Norte ...), cada nuevo segmento sólo puede interseccionar los segmentos anteriores en un **muy limitado conjunto de maneras**.

Después de los primeros cuatro movimientos la dirección repite, por lo que cualquier nuevo segmento sólo puede tocar:

- El segmento dibujado hace dos movimientos (un giro de 90°).
- El segmento dibujado hace tres movimientos (un giro de 180°, es decir, un “touch”).
- El segmento dibujado hace cinco movimientos (una situación “sobre” que cierra un bucle).

Estas son las únicas posibilidades que pueden producir un cruce. El resto del avión ya está “limpiado” por el patrón anterior.

Por lo tanto, sólo necesitamos seguir las últimas distancias, sin necesidad de una lista de coordenadas o de una rutina de intersección de línea.

-...

### 3.4 Los malos – errores comunes

Por qué Fails
Silencio--------------------------
Silencio **Usando una lista de coordenadas completas** Silencio O(n2) tiempo y memoria O(n), además de errores de punto flotante. Silencio
Silencio **Verificar sólo dos pasos atrás** Silencio Perdiendo el caso “touch” cuando el segmento i‐th es igual al i‐3rd. Silencio Agregue la condición “touch” de 4 pasos. Silencio
Silencio **Usar comparaciones de posición absoluta** ← Requiere posiciones de recomputación en cada paso; innecesario.  Use desigualdades relativas entre distancias. Silencio
Silencio **Simetría de la simetría** Silencio El camino puede tener longitudes asimétricas; el cruce puede ocurrir en patrones irregulares. Use las condiciones exactas derivadas de la geometría. Silencio

-...

## 3.5 The Ugly – Edge Cases That Trip You Up

Silencio Caso Edge Silencio Típico error TEN Cómo el algoritmo lo maneja TENIDO
Silencio----------------------------------------------------------------
Silencio **Exactamente 4 movimientos** Silencio Algunas implementaciones olvidan manejar `i == 4 ' adecuadamente. La segunda condición ( " i " 4`) revisa el escenario táctil. Silencio
Silencio **Gran número causando desbordamiento** Silencio Añadiendo dos valores de `int` pueden desbordar `int` en Java/C++. Silencio Use `long` o cast to `long` during addition (`distance[i] + distance[i-4]`. Silencio
Silencio **Las mismas longitudes que crean los bucles degenerados** Silencio Una secuencia como `[1,1,1,1,1]` puede parecer no traicionar, pero la regla de 5 pasos lo captura. La tercera condición representa el bucle “sobre la marcha”. Silencio
Silencio **Introducción muy larga** tención Recursión o asignación excesiva puede llegar a límites. TEN Ierative loop with constant auxiliary storage. Silencio

-...

### 3.6 El Algoritmo en Detalle

``text
para mí de 3 a n-1
si la distancia[i] >= distancia[i-2] // más o igual al segmento 2 pasos atrás
y distancia[i-1] <= distancia[i-3] // el segmento medio no es más largo
retorno verdadero

si me cierro 4 y 4
distancia[i-1] == distancia[i-3] // tocando el segmento de 3 pasos hacia atrás
y distancia[i] + distancia[i-4] distancia[i-2]
retorno verdadero

si me cierro 5 y 5
distancia[i-2] > distancia[i-4] // apertura de un bucle
y distancia[i] + distancia[i-4] distancia[i-2]
y distancia[i-1] + distancia[i-5] distancia[i-3]
y la distancia[i-1]
retorno verdadero

devolver falso
`` `

Los tres bloques corresponden exactamente a los tres escenarios de cruce explicados anteriormente.

-...

### 3.7 Complexity Analysis

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
Silencio **Hora** Silencioso `O(n)` – un escaneo Silencioso `O(n)` – un escaneo Silencioso `O(n)` – un escaneo
tención **Espacio** Silencioso `O(1)` – 5–6 variables enteros Silencioso `O(1)` Silencio

El algoritmo funciona para `n = 10^5` cómodamente en todas las plataformas principales.

-...

### 3.8 Code Snippets

##### Java

``java
Solución de la clase pública {}
booleano público es SelfCrossing(int[] distance) {}
si (distancia == null TENIDO distancia. longitud 4) devolver falso;
para (int i = 3; i) i++) {
si (distance[i]
distancia[i-1] <= distancia[i-3]) devolver verdadero;
si
distancia[i-1] == distancia[i-3]
distancia[i] + distancia[i-4] >= distancia[i-2]) volver verdadera;
si
distancia[i-2]
distancia[i] + distancia[i-4] }= distancia[i-2]
distancia[i-1] + distancia[i-5] >= distancia[i-3]
distancia[i-1] <= distancia[i-3]) devolver verdadero;
}
devolver falso;
}
}
`` `

#### Python

``python
Solución de clase:
def es SelfCrossing(self, distance: list[int]) - conviene bool:
si len(distance)
Retorno Falso
para i en rango(3, len(distance)):
si la distancia[i] √≥= la distancia[i-2] y la distancia[i-1]
Retorno
si >= 4 y distancia[i-1] == distancia[i-3] y \
distancia[i] + distancia[i-4] distancia[i-2]:
Retorno
si >= 5 y la distancia[i-2]
distancia[i] + distancia[i-4] }= distancia[i-2] y \
distancia[i-1] + distancia[i-5] >= distancia[i-3] y \
distancia[i-1] ANTE= distancia[i-3]:
Retorno
Retorno Falso
`` `

###### C++

``cpp
Clase Solución {
public:
bool es SelfCrossing(vector asignadoint frecuentemente distancia) {}
si (distance.size() ANTE 4) devolver falso;
para (int i = 3; i) ++i) {
si (distance[i]
distancia[i-1] <= distancia[i-3]) devolver verdadero;
si
distancia[i-1] == distancia[i-3]
distancia[i] + distancia[i-4] >= distancia[i-2]) volver verdadera;
si
distancia[i-2]
distancia[i] + distancia[i-4] }= distancia[i-2]
distancia[i-1] + distancia[i-5] >= distancia[i-3]
distancia[i-1] <= distancia[i-3]) devolver verdadero;
}
devolver falso;
}
};
`` `

Siéntete libre de copiar, pegar y correr. Recuerde probar los casos difíciles:

``text
[1,2,3,4] falso
[1,1,1,1] - título verdadero (touch case)
[1,1,2,1,1,1,1] - título verdadero (5-step loop)
`` `

-...

### 3.9 Cómo discutir Esto en una entrevista

1. ** Explique el patrón de movimiento**: “Caminamos Norte → Oeste → Sur → Este → ..., así que después de los primeros 4 pasos la dirección repite. ”

2. **Declarar las limitadas posibilidades de intersección**:
- Dos pasos atrás (90° vuelta).
- Tres pasos atrás (180° táctil).
- Cinco pasos atrás (cierre de bucle).

3. **Presentar las desigualdades**:
Muestra las tres condiciones.
Use un diagrama simple si está en papel.

4. **Mención de la complejidad del tiempo/espacio**:
`O(n)` time, `O(1)` space.

5. **Hablar sobre seguridad de la periferia**:
Manejo de desbordamiento, controles de longitud de la matriz, grandes entradas.

Esta explicación concisa y rigurosa demuestra la profundidad de la comprensión, un sello distintivo de un ingeniero de software de primer nivel.

-...

### 4. Conclusión

LeetCode 335 “Auto Crossing” es engañosamente simple una vez que vea el patrón *directional*. La clave es tratar el problema como una secuencia de desigualdades relativas** en lugar de geometría absoluta. Con esa perspectiva, un algoritmo de paso único emerge naturalmente.

Cubrimos:

- ¿Por qué?
- Lo que... de las trampas comunes.
- El **cómo** de la manipulación de la periferia.
- Código listo para usar en **Java, Python, C+**.

Ahora usted puede abordar con confianza esta pregunta, explicar su solución en cualquier idioma, e impresionar a los entrevistadores con la elegancia y la eficiencia. ¡Feliz codificación y buena suerte en tu próxima entrevista!