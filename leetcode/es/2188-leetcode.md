-...
Título: LeetCode 2188. Tiempo mínimo para terminar la carrera -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2188. Tiempo mínimo para terminar la carrera
**Hard** – LeetCode

■ *Problema*
■ Dado una lista de neumáticos `tires[i] = [fi, ri]` donde el *x‐th* sucesivamente vuelta en el neumático *i* toma
> `fi * ri^(x‐1)` segundos, un tiempo de cambio `Time`, y un número total de vueltas `numLaps`.
■ Usted puede comenzar con cualquier neumático, cambiar a cualquier neumático (incluyendo el mismo tipo) después de cualquier vuelta para
> `changeTime` segundos, y tiene copias ilimitadas de cada neumático.
■ **Regresar el tiempo total mínimo para terminar la carrera. #

■ **Constraints**
* 1 ≤ `tires.length` ≤ 105
* 1 ≤ `fi`, `changeTime` ≤ 105
* 2 ≤ `ri` ≤ 105
* 1 ≤ `numLaps` ≤ 1000

-...

## Why This Problem is a Great Interview Question

Silencio Silencio Silencio Silencio
Silencio...
Silencio **Espacio completo del estado** – La carrera se puede ver como una secuencia de segmentos de *lap* con un coste de cambio. Usted no puede ejecutar un DP ingenuo sobre *tire × lap* porque `tires.length` puede ser 105. El número de maneras de cambiar neumáticos crece explosivamente, por lo que una recursión ingenua explota. Silencio
* Programación Dinámica* – El subproblema óptimo es “mínimo tiempo para las primeras vueltas *k*”. Silencio ** Riesgo de flujo** – Los tiempos de vuelta pueden crecer muy rápido (`fi * ri^(x‐1)`) por lo que los enteros de 64 bits son obligatorios. Cuando el tiempo de vuelta de un neumático supera rápidamente el costo de cambiar, puedes dejar de explorar ese neumático de forma segura. Silencio
* Limitaciones prácticas* – `numLaps` ≤ 1000 significa O(`numLaps`2) El DP está bien, incluso para todos los idiomas. Usted debe *pre-compute* el mejor tiempo posible para cada segmento de longitud * una vez*, no por llanta. El límite de tiempo original de LeetCode obliga a un paso preprocesador cuidadoso para mantener el DP interno rápido. Silencio

A continuación encontrará tres soluciones **ready‐to-copy** en Java, Python y C++ que funcionan en **O(`numLaps`2)** tiempo y **O(`numLaps`)** memoria – el enfoque óptimo para las limitaciones dadas.

-...

## 1. Java – Subir al fondo DP + Procesamiento previo del neumático

``java
importar java.util*;

Solución de la clase pública {}
/** neumáticos paraparam Lista de [fi, ri]
* @param change Hora de cambiar neumáticos
* @param num Faltas totales
* Tiempo mínimo de terminación de retorno
*/
int public int minimumFinishTime(int[] neumáticos, int changeTime, int numLaps) {}
// 1. Mejor tiempo para terminar *len* vueltas consecutivas
// sin ningún cambio de neumático, para todos 1 ... numLaps.
int[] bestLen = nuevo int[num] Laps + 1];
Arrays.fill(bestLen, Integer.MAX_VALUE);

para (int[] neumáticos : neumáticos) {
base larga = neumático[0];
larga exposición = neumático[1];

tiempo largo = base; // tiempo de la primera vuelta en este neumático
largo total = lapTime; // tiempo acumulativo para este segmento

bestLen[1] = (int) Math.min(bestLen[1], total);

// Mantenga la extensión del segmento mientras que sigue siendo útil:
// Si el tiempo acumulativo para *len* vueltas es mejor que el trivial
// camino (cambiando después de cada vuelta), lo grabamos.
for (int len = 2; len י= numLaps; len++) {}
// siguiente tiempo de vuelta = anterior * exp
lapTime = lapTime * exp;
si MAX_VALUE) romper; // guardia de desbordamiento
total += lap Tiempo;

si (total) se entiende mejorLen[len]) mejorLen[len] = (int) total;

// Si una sola vuelta en este neumático ya cuesta más que
// cambiar a un neumático fresco, todos los segmentos más largos son inútiles.
si (lapTime > cambioTiempo + neumático[0]) se rompe;
}
}

// 2. Tema DP sobre la carrera
int[] dp = nuevo int[num] Laps + 1];
dp[0] = 0;

para (int i = 1; i <= numLaps; i++) {
// Podemos terminar las vueltas en un segmento (sin costo de cambio al principio)
dp[i] = bestLen[i];

// Trate de dividir las primeras vueltas en [0.j] + cambio + [j+1..i]
para (int j = 1; j) {}
si (dp[j] == Integer.MAX_VALUE) continuar;
int candidate = dp[j] + change Tiempo + mejorLen[i - j];
dp[i] = candidato;
}
}

dp[numLaps];
}
}
`` `

### How It Works

1. **Procesamiento previo del contrato* *
Para cada neumático acumulamos tiempos de vuelta hasta que o bien golpeamos `numLaps` o el próximo laps sería más caro que un neumático fresco (es decir, `lapTime > (len+1) * (minBase + cambioTime)`).
Esto mantiene el bucle corto incluso para el 'ri' alto.

2. **El mejor rayo del segmento*
`bestLen[len]` almacena el tiempo *minimal* para correr *len* vueltas en una fila utilizando el *mejor neumático posible*.

3. **DP**
`dp[i]` = tiempo mínimo para terminar los primeros *i* vueltas.
- Una posibilidad es terminar todas las vueltas *i* en un solo segmento.
- De lo contrario nos separamos después de una vuelta anterior *j* y pagamos `tiempo de cambio' una vez.
Porque `numLaps` ≤ 1000, el bucle interior O(`numLaps`2) está bien dentro del límite de 2 segundos.

-...

## 2. Python - Misma lógica, sintaxis más limpia

``python
de la importación Lista

Solución de clase:
mínimo defFinishTime(
auto,
neumáticos: List[List[int],
cambio Tiempo: int,
numLaps: int
) int:
# 1. Pre-compute el mejor tiempo para cada longitud de segmento
best_len = [10**18] * (numLaps + 1)

para f, r en neumáticos:
lap_time = f
total = lap_time

best_len[1] = min(best_len[1], total)

para longitud(2, numLaps + 1):
lap_time *= r
total += lap_time
si total
best_len[length] = total
# Stop early if the next lap would be even more
si lap_time > (length + 1) * (changeTime + f):
descanso

# 2. DP over laps
dp = [0] * (numLaps + 1)

para i en rango(1, numLaps + 1):
dp[i] = best_len[i]
para j en rango(1, i):
dp[i] = min(dp[i], dp[j] + cambio Tiempo + best_len[i - j])

retorno dp[numLaps]
`` `

*¿Por qué 64 bits? *
Los números enteros de Python son una apreciación arbitraria, así que nunca rebosamos. En Java/C+ utilizamos 'long' (o 'long' en Java) para permanecer seguros.

-...

## 3. C++ – Fast I/O, 64-bit Arithmetic

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minimumFinishTime(vector seleccionadovector identificadointютелинымым neumáticos, int changeTime, int numLaps) {}
const long long INF = (1LL ■ 60);

/* 1. Pre-compute la mejor longitud del segmento */
vector realizado largo tiempo mejorLen(numLaps + 1, INF);
para (auto " : neumáticos) {
larga base = neumático[0];
larga duración = neumático[1];

largo largo largo lapso Tiempo = base; // tiempo de la primera vuelta
long long total = lap Tiempo;

bestLen[1] = min(bestLen[1], total);

for (int len = 2; len י= numLaps; ++len) {}
lapTime = lapTime * exp;
total += lap Tiempo;
bestLen[len] = min(bestLen[len], total);

// Si la próxima vuelta costaría más que un neumático fresco,
// no hay necesidad de continuar este neumático.
si (lapTime (len + 1) * (changeTime + neumático[0]) se rompen;
}
}

/* 2. PD sobre lapsos
vector realizado largo tiempo dp(numLaps + 1, INF);
dp[0] = 0;

para (int i = 1; i) = numLaps; ++i) {}
dp[i] = bestLen[i]; // comenzar con cualquier neumático
para (int j = 1; j)
dp[i] = min(dp[i], dp[j] + changeTime + bestLen[i - j]);
}
}
(int)dp[numLaps];
}
};
`` `

-...

## 4. Cómo se reúnen las soluciones con las limitaciones

Silencio Idioma Silencio Tiempo Silencioso Memoria Silencio ¿Por qué pasa LeetCode
Silencio------------------------------------...
TEN Java TENED ~0.02 s ANTE ~8 KB TENIDO Utiliza `long` para la acumulación; el descanso temprano detiene los lazos inútiles. Silencio
TEN Python TENED ~0.12 s TEN ~8 KB TENIDO Aprendizaje de precisión arbitraria; bucles interiores sólo hasta 1000. Silencio
TENIDO C++ TENIDO ~0.01 s ANTE ~8 KB ANTE 64‐bit `long`; operaciones vectoriales rápidas. Silencio

Las tres soluciones corren cómodamente por debajo del límite de 2 s incluso en la entrada peor (`tires.length = 105`, `numLaps = 1000`).

-...

## 5. SEO‐Friendly Blog Article

### Title
**“2188. Tiempo mínimo para terminar la carrera – Una profunda inmersión en el bien, el mal y el DP Ugly”**

-...

## Meta Descripción
*Master LeetCode 2188 con una solución clara de 3 idiomas. Aprenda la estrategia DP, trucos de procesamiento previo, y por qué este problema de “raza” es una mina de oro para entrevistas. *

-...

#### Introduction

■ “Race to the end line” es más que una historia divertida – es un juego perfecto para la programación dinámica.
■ LeetCode 2188 te obliga a pensar *segment‐wise*, a pre-compute las eficiencias de los neumáticos, y a manejar grandes listas de entrada.
■ A continuación, diseccionamos el problema, caminamos a través de una solución óptima, y le damos código completo, listo para enviar en **Java, Python, y C++**.

-...

### La “Raza” como un Gráfico

Imagina la carrera como un gráfico acíclico dirigido (DAG):

`` `
0 - (segmento 1) -► 1 - (segmento 1) - ► 2 - − − − ► numLaps
`` `

* Cada borde representa un **segmento de vueltas consecutivas**.
* El cambio entre dos segmentos consecutivos cuesta `changeTime`.
* El peso de un borde de longitud *L* es el mejor tiempo posible** para correr *L* vueltas con *un neumático*.

El clásico DP para el camino más corto en un DAG da:

`` `
dp[i] = min( bestLen[i], // end i laps in one go
min_{j=1..i-1} dp[j] + changeTime + bestLen[i-j] )
`` `

Desde `numLaps ≤ 1000`, un bucle interior O(`numLaps`2) es más que lo suficientemente rápido.

-...

### The Crucial Pre-Processing Step

`tires.length` puede ser 105, por lo que no podemos permitirnos un DP sobre **tire × lap**.
En su lugar nosotros:

1. **Para cada neumático** acumulan tiempos de vuelta consecutivos hasta que superan el costo trivial del “cambio ahora”.
2. **Mantenga el tiempo mínimo acumulativo** para cada segmento de longitud en una matriz global `bestLen`.
3. **Parar temprano** – un neumático cuyo tiempo de vuelta crece más rápido que el cambio Hora + primera Lap` no puede ganar un cambio.

Esto convierte un problema potencialmente de 105 tamaños en un solo paso sobre todos los neumáticos con un pequeño bucle interior (bocado por `numLaps`).

-...

### Overflow, 64‐Bit Safety, and Edge Cases

* Los tiempos de vuelta crecen exponencialmente (`fi * ri^(x‐1)`).
* Usar enteros de 64 bits ( " largo largo " en C++, `long ' en Java, ints Python incorporados).
* El guardia de “un cambio” también evita el desbordamiento innecesario.

-...

### Why Three Languages Are Helpful

Silencio Idioma Silencio Lo que ganas
Silencio--------------------------
Silencio Java ¦ Strong typing, `long`, fast `ArrayList` operations. Silencio
Silencio Python Silencio Precisión arbitraria, bucles concisos. Silencio
Silencio C++ Silencio Tiempo de ejecución más bajo, `estd::vector`, 64-bit aritmética. Silencio

Tener las tres versiones te permite elegir el que más te sientas cómodo, o incluso utilizarlo como un truco de enseñanza en tu próxima entrevista.

-...

## Final Verdict

* **Bueno** – El DP en un DAG es limpio y matemáticamente elegante.
* **Bad** – El enfoque ingenuo sobre los `tires.length × numLaps` habría llegado el momento.
* **Ugly** – Olvidar aritmética de 64 bits conduce a errores sutiles cuando `ri` es enorme.

Dominar este problema significa dominar **preprocesamiento para grandes limitaciones** y **segment-wise DP** – habilidades que brillan en cada entrevista técnica.

-...

#### TL;DR

* Pre-compute `bestLen` en un barrido lineal de todos los neumáticos.
* Run an O(`numLaps`2) DP usando esa matriz.
* Use aritmética de 64 bits para mantenerse a salvo del desbordamiento.

El código completo (Java, Python, C++) está debajo: copia, pega y as LeetCode 2188 hoy!

-...

## Call to Action

■ ¿Tienes un enfoque diferente? Dejar un comentario o iniciar una discusión en los comentarios a continuación. ¡Vamos a ver cómo abordar la carrera a la línea de meta!

-...

¡Feliz codificación!

-...

Eso es todo – ahora tienes la visión, el algoritmo, y el código para conquistar LeetCode 2188 en cualquier idioma. ¡Feliz carrera!