-...
Título: LeetCode 3635. Hora de finalización más temprana de los ríos de tierra y agua II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📚 Tiempo de finalización más temprano para los ríos de tierra y agua II - La solución completa
■ **Un problema práctico de entrevistas que prueba la intuición codicioso, manipulación de arrays y habilidades de complejidad del tiempo* *
■ **Idiomas:** Java TENIDO Python ANTE C++

-...

### 1. Recaptación de problemas

Se le dan dos listas de atracciones del parque temático:

Silencio **Categoría** TENIENDO `duration[i]` Silencio
Silencio------------------------------------
← Viajes en tierra Silencioso `landStartTime[i]` TENIDA `landDuration[i]` Silencio
Silencio Paseos en el agua 'waterStartTime[j]` " WaterDuration [j] " Silencio

*Debes montar *Exactamente un viaje por tierra* y *exactamente un viaje por agua*, en cualquier orden. *

Un paseo puede comenzar en su hora de apertura o en cualquier momento posterior.
Después de terminar un paseo se puede abordar inmediatamente el otro (si ya está abierto) o esperar a que se abra.

** Objetivo:** Devuelve el *tiempo de finalización más mínimo posible* para ambos paseos.

■ **Constraints**
≤ 1 ≤ n, m ≤ 5 · 104, 1 ≤ tiempo, duración ≤ 105

-...

### 2. Intuición – ¿Por qué funciona un escáner saludable

Las únicas decisiones que importan son:

1. ¿Qué paseo eliges **primero** (tierra o agua).
2. Qué paseo específico escoge de esa categoría.

El *time* que termina el primer viaje es independiente de la elección del segundo paseo, porque siempre puedes esperar a que el segundo viaje se abra.
Por lo tanto, para una orden dada** (Land → Agua o Agua → Tierra) sólo necesita el tiempo de acabado * más temprano* de la primera categoría:

* `minLandFinish = min(landStart[i] + landDuration[i] `
* `minWaterFinish = min(waterStart[j] + waterDuration[j] `

Una vez que sepas la primera vez que puedes terminar el primer viaje, el tiempo de llegada para cada paseo de la segunda categoría se convierte en:

`` `
terminar = duración_de_second_ride
+ max( early_finish_of_first_category,
open_time_of_second_ride )
`` `

El `max` maneja el tiempo de espera si el segundo viaje no está abierto todavía.

Así podemos:

1. Pre-compute `minLandFinish` y `minWaterFinish` en **O(n+m)**.
2. Para cada viaje de agua computar el tiempo de llegada para el pedido *Land→Water*.
3. Para cada viaje por tierra computar el tiempo de llegada para el pedido *Water→Land*.
4. La respuesta es el mínimo de todos estos candidatos - todavía **O(n+m)**.

No se requiere clasificación ni búsqueda binaria – escaneos lineales puros.
Esta visión avaricia nos da una **O(n+m)** tiempo, **O(1)** solución espacial.

-...

### 3. El Código - 3 idiomas

##### 3.1 Java

``java
importar java.util*;

Solución de la clase pública {}
public int earlyFinishTime(es)
int[] landStartTime, int[] landDuration,
int[] waterStartTime, int[] waterDuration

int minLandFinish = Integer.MAX_VALUE;
para (int i = 0; i) i++) {
minLandFinish = Math.min(minLandFinish,
landStartTime[i] + landDuration[i]);
}

int minWaterFinish = Integer.MAX_VALUE;
para (int i = 0; i) i++) {
minWaterFinish = Math.min(minWaterFinish,
waterStartTime[i] + waterDuration[i]);
}

respuesta int = Integer. MAX_VALUE;

/* Tierra primero → Agua segundo */
para (int j = 0; j)
acabado int = aguaDuración[j] + Math.max(minLandFinish,
waterStartTime[j]);
respuesta = Math.min(respuesta, final);
}

/* Agua primero → Tierra segunda */
para (int i = 0; i) i++) {
acabado int = landDuration[i] + Math.max(minWaterFinish,
landStartTime[i]);
respuesta = Math.min(respuesta, final);
}

respuesta de retorno;
}
}
`` `

-...

###### 3.2 Python

``python
Solución de clase:
def earlyFinishTime(
auto,
tierra StartTime: List[int],
landDuration: List[int],
agua StartTime: List[int],
waterDuration: List[int]
) int:
min_land_finish = min(l + d for l, d in zip(landStartTime, landDuration))
min_water_finish = min(w + d para w, d in zip(waterStartTime, waterDuration)

as = flotante('inf')

# Land first → Water second
para w, d en zip(waterStartTime, waterDuration):
acabado = d + máx(min_land_finish, w)
as = min(ans, end)

# Water first → Land second
para l, d en zip(landStartTime, landDuration):
acabado = d + máx(min_water_finish, l)
as = min(ans, end)

Retorno
`` `

-...

##### 3.3 C++

``cpp
Incluido el título
#include >
#include < > >

Clase Solución {
public:
int earlyFinishTime(
std::vector obtenidosintю terrenoStartTime,
std:::vector obtenidosint
std::vector seleccionado empuje limitado aguaStartTime,
std:::vector seleccionado empolvado con aguaDuración

int minLandFinish = INT_MAX;
para (size_t i = 0; i) ++i)
minLandFinish = std::min(minLandFinish,
landStartTime[i] + landDuration[i]);

int minWaterFinish = INT_MAX;
para (size_t j = 0; j ++j)
minWaterFinish = std::min(minWaterFinish,
waterStartTime[j] + waterDuration[j]);

int ans = INT_MAX;

// Tierra primero → Agua segundo
para (size_t j = 0; j ++j) {
acabado int = aguaDuración[j] +
std::max(minLandFinish, waterStartTime[j]);
ans = std::min(ans, end);
}

// Agua primero → Tierra segundo
para (size_t i = 0; i) ++i) {
acabado int = landDuration[i] +
std::max(minWaterFinish, landStartTime[i]);
ans = std::min(ans, end);
}

devolver los ans;
}
};
`` `

-...

### 4. Artículo del Blog – “El Bien, el Mal y el Ugly”

■ **SEO‐Optimized Title:**
■ *El tiempo de finalización más rápido para los ríos de tierra y agua II – Un problema de entrevista práctica (Java, Python, C++)*

-...

##### 4.1 Introducción

Los entrevistadores aman problemas que prueban el razonamiento codicioso, array traversal y código limpio.
“El tiempo de finalización más difícil para los ríos de tierra y agua II” es un desafío canónico de media-dificultad LeetCode que hace exactamente eso.

En este post caminamos:

1. Problema de comprensión " limitaciones
2. La intuición codicioso que convierte una tarea combinatoria aparentemente compleja en un escaneo **O(n+m)**
3. Una solución completa en Java, Python y C++
4. Pocamientos comunes (el “Bad”) y cómo evitarlos
5. Extensiones que puede discutir para mostrar profundidad (el “Ugly”)

Al final tendrás una referencia *listo-a-paste* para cada idioma y un punto de conversación que demuestra tu capacidad de simplificar bajo límites de tiempo ajustados.

-...

#### 4.2 Problema Recap (bueno)

- **Lo que debe elegir: * exactamente una tierra y un paseo en agua.
- **Order no importa** – puedes elegir primero.
- ** Entradas altas**: 50 000 paseos por categoría → necesitamos tiempo lineal.

-...

#### 4.3 ¿Por qué el enfoque ingenuo falla (Bad)

Un primer intento natural es:

``text
para cada viaje por tierra
para cada paseo de agua
prueba ambas órdenes
`` `

Eso sería **O(n·m)**, demasiado lento para 5 × 104 viajes por categoría.
Los entrevistadores detectarán rápidamente el soplo cuadrático y esperarán que encuentres una estrategia mejor.

-...

#### 4.4 The Greedy Insight (Good)

- **Key insight:** el tiempo *finish de la primera categoría* es independiente de qué paseo tomará más adelante.
- Computar el *acabado más temprano* de la primera categoría una vez (`minLandFinish`, `minWaterFinish`).
- Para la segunda categoría, el tiempo de acabado se convierte en una fórmula simple usando `max` para la espera.
- Escanear todos los paseos de la segunda categoría → Actualizar mínimo global.

Todo esto es **un paso** por matriz – sin clasificación, sin montones, sin búsqueda binaria.

■ **Por qué es genial para entrevistas* *
■ *Escaneos de línea* muestran que puede identificar el cuello de botella real.
■ *El razonamiento agudo* demuestra que no estás forzando brutamente sino explotando la estructura de problemas.
■ *Código completo* (nombres variables, bucles separados para cada pedido) muestra mantenibilidad.

-...

#### 4.5 Edge Cases " Defensive Coding (Bad)

- **Viaje sencillo** por categoría: nuestra fórmula todavía funciona porque `min()` sobre un elemento está bien.
- **Large integer sums**: `startTime + duration` puede alcanzar 200 000, todavía dentro de 32 bits de entrada firmado.
- **Iniciación de respuesta**: use `Integer. MAX_VALUE` (Java), `INT_MAX` (C++), o `float('inf')` (Python).

-...

#### 4.6 “Ugly” – Los entrevistadores de cosas podrían preguntar

1. ¿Podemos resolverlo en el lugar? * *
*Sí – la solución anterior utiliza sólo espacio extra constante. *

2. **¿Y si los arrays no estaban surtidos? #
*Sin impacto – sólo estamos haciendo escaneos lineales. *

3. **¿Qué hay de más de dos categorías? * *
*La misma idea generaliza: mantener el tiempo mínimo de acabado de la primera categoría, iterate sobre el resto. *

4. **Proof of óptimaity** – usted puede dar un breve argumento:
*Dado un pedido, elegir el primer paseo con el tiempo de acabado más pequeño no puede retrasar el segundo viaje, porque se permite la espera. *

5. **Space-optimised alternative** – use streaming (Java 8 streams, generadores de pitón).

Los entrevistadores pueden probar su capacidad para **probar** por qué la elección codictiva es óptima; estar listos para articular que la expresión `max` exactamente modela el tiempo de espera y que elegir un final posterior para el primer viaje nunca puede ayudar el segundo viaje.

-...

#### 4.7 Take‐ Lista de verificación

- ☐ Comprender la decisión de dos pasos (orden + paseo específico).
- ☐ Pre-compute `minLandFinish` & `minWaterFinish`.
- ☐ Escanee la otra categoría y computar el tiempo de acabado utilizando `max`.
- Mantener el mínimo global.
- ☐ Escriba código limpio, autodocumentado (nombres variables claros, comentarios).
- ☐ Tiempo-complexidad: **O(n+m)**, Space‐complexity: **O(1)**.

-...

#### 4.8 How This Helps You Get Hired

* Los entrevistadores quieren candidatos que pueden:
- Reduzca una explosión combinatoria a un escaneo lineal.
- Razón sobre “esperar” como operación “max”.
- Producir código limpio y lingüístico.

* Mostrar esta solución en tu GitHub, incluir la discusión anterior, y etiqueta tu perfil con `Java`, `Python`, `C+`, `LeetCode`, `Greedy`, `Array`.

■ **Keywords**: tiempo de llegada temprano, paseos por tierra, paseos por el agua, algoritmo codicioso, problema de entrevista, LeetCode mediano, entrevista de codificación Java, entrevista de Python, entrevista C++.

-...

#### 4.9 TL;DR

`` `
1/ Finalizar la primera categoría
2/ Por cada paseo de la segunda categoría:
terminar = duración + máx( early_finish_of_first, opening_time )
3 ⃣ Repetir para ambos pedidos y tomar el mínimo global
`` `

■ **Tiempo:** O(n+m)
■ **Espacio:** O(1)

Feliz codificación, y que su próxima entrevista se sienta como un viaje suave! 🎢

-...



### 5. Prueba rápida – Entradas de muestra

TENIDO ANTERIOR esperada
Silencio...
Silencio `landStartTime=[1,2,4] ``Secuenciar `landDuration=[5,4,2]` secuestrar confianza `waterStartTime=[3,5,1]` secuestrar confianza`waterDuration=[6,3,4]`
Silencio `landStartTime=[5] `` obedecbr confianza`landDuration=[5]` obedeció abr ``waterStartTime=[1] ``se hizo lo siguiente: ' WaterDuration=[1] ←

Ejecute cualquiera de los snippets arriba en su IDE favorito para verificar.

-...

### 6. Palabras finales

Este problema es un gran escaparate para:

- * algoritmos codiciosos de tiempo libre*
- *Clar, código de mantenimiento*
- *La fluidez en idioma corsé*

Añade la implementación de referencia a tu hoja de trampa de entrevista personal y tendrás un punto de conversación sólido para cualquier entrevista técnica. ¡Buena suerte! 🚀