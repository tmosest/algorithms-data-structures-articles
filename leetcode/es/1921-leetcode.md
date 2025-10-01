-...
Título: LeetCode 1921. Eliminar el número máximo de monstruos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Eliminar el número máximo de monstruos
* Un profundo riesgo sobre un problema de LeetCode clásico (Time‐O(n), Space‐O(n)* *

-...

## Problema Restatement

Silencio
Silencio...
Silencio **Given** Silencio `dist[i]` – distancia de monstruo *i* del objetivo. *i*. Silencio
En cada turno podemos eliminar un monstruo. Un monstruo que llega a tiempo 't' (número entero de turnos) antes de que tengamos la oportunidad de dispararle ganará. Silencio
Silencio ** Objetivo** Silencio Encuentra el número máximo de monstruos que podemos eliminar antes de que cualquier monstruo alcance el objetivo. Silencio

■ **La salida** – el número de monstruos que podemos eliminar.

-...

## 1. Intuición – “¿Cuándo llega un monstruo? ”

Un monstruo necesita `ceil(dista / velocidad)` se convierte en el objetivo.
¿Por qué “ceil”?

* `dist = 4`, `velocidad = 3` → toma 1.33 vueltas, por lo que llega a su turno **2**.
* `dist = 2`, `velocidad = 2` → alcanza la vuelta **1.

Así **El tiempo de llegada** es:

``text
llegada = ceil( dist / velocidad )
`` `

Si `arrival` es mayor que el número de monstruos que tenemos, simplemente significa que el monstruo llegará *después* ya hemos terminado eliminando a todos – podemos ignorarlo de forma segura.

-...

## 2. Solución clásica – cola prioritaria

La solución más común (y la que se ve más a menudo en LeetCode) es:

1. **Computa el tiempo de llegada** de cada monstruo.
2. **Sorta** todos los tiempos de llegada.
3. Camina a través de ellos: tan pronto como golpeamos a un monstruo cuyo tiempo de llegada `≤ giro actual ` paramos – ese giro es la respuesta.

`` `
(arrivalTimes)
para (vuelto = 0; girar)
si (arrivalTimes[turn] <= turn) de vuelta;
}
retorno n;
`` `

*Time*: `O(n log n)` (a causa del tipo)
*Espacio*: `O(n)` (para la variedad de horarios de llegada)

Si bien esto es lo suficientemente rápido para la mayoría de los casos de prueba, podemos hacerlo mejor – **O(n) tiempo**.

-...

## 3. The Bucket / “Counting Sort” Trick – O(n) Hora

La observación clave:
*Para que un monstruo sobreviva hasta girar `t`, su tiempo de llegada debe ser ≤ `t`. *

En lugar de clasificar, nosotros **bucket** monstruos por su hora de llegada.

`` `
n = dist.length
balde[i] = número de monstruos que llegan a la vuelta i (0-indexed)
`` `

Sólo necesitamos cubos hasta `n‐1`. Si el tiempo de llegada de un monstruo es ≥ `n`, llegará después de que ya hayamos terminado eliminando a todos – nunca causa problemas.

**Paso 1 - Construir los cubos**

``text
para cada monstruo
llegada = ceil(dist[i] / speed[i]
si la llegada
cubo[arrival]++
`` `

**Paso 2 – Escanear los cubos**

Caminamos por los turnos en orden.
A su vez `i` ya hemos eliminado monstruos 'eliminados'.
Si **más monstruos están esperando en este turno que los giros que hemos sobrevivido**, es decir.

`` `
eliminados + cubo[i]
`` `

entonces algún monstruo alcanzará el objetivo antes de que podamos disparar – nos detenemos y regresaremos.
De lo contrario, añadimos los monstruos de este giro a `eliminar' y continuar.

Si terminamos el escaneo sin regresar, podemos eliminar a todos los monstruos – la respuesta es `n`.

** Algoritmo completo (estilo pitón)* *

``python
def eliminarMaximum(dist, speed):
n = len(dist)
* n

para d, s en zip(dist, speed):
llegada = math.ceil(d / s)
si la llegada se realizó n:
cubo[arrival] += 1

eliminados = 0
para i en rango(n):
si se eliminan + cubo[i]
Regreso
eliminada += cubo[i]

retorno n
`` `

**Por qué funciona* *

* A su vez `i` tenemos exactamente `i+1` oportunidades de fuego (torno 0, giro 1, ..., giro i).
* Si en cualquier momento `i` el número de monstruos que ya han llegado (`eliminated + cubo[i]`) excede el número de oportunidades (`i+1`), algún monstruo gana - no podemos ir más allá.
* Si llegamos al final de los cubos, hemos tenido suficientes vueltas para disparar una vez a la hora de llegada de cada monstruo, así que todos los monstruos son eliminados.

**La complejidad* *

Silencio
Silencio...
Silencio **Hora** Silencioso `O(n)` – un paso a cubo, un paso a escanear. Silencio
Silencio **Espacio** Silencioso `O(n)` – el conjunto de cubos. Silencio

-...

## 4. Implementaciones de referencia

A continuación encontrará el mismo algoritmo escrito en **Java 17**, **C+17** y **Python 3**.
Los tres son 1 a 1 traducciones de la lógica descrita anteriormente y están listos para pegar a su editor.

-...

#### 4.1 Java 17

``java
importar java.util*;

Solución de la clase pública {}
intrépido público Maximum(int[] dist, int[] speed) {
int n = dist.length;
int[] cubo = nuevo int[n];

// Construir cubos
para (int i = 0; i)
int arrival = (int) Math.ceil((double) dist[i] / speed[i]);
si (arrival)
cubo[arrival]+;
}
}

// Botes de escáner
int eliminada = 0;
para (int i = 0; i)
si (eliminada + cubo [i]
retorno i;
}
eliminada += cubo[i];
}
retorno n;
}
}
`` `

-...

### 4.2 C+17

``cpp
Incluido el título
#include >

Clase Solución {
public:
Intento eliminar Máximo (std:::vector fielint implicados dist, std::vector fieltro velocidad) {
int n = dist.size();
std::vector seleccionado 0);

// Construir cubos
para (int i = 0; i) {}
int arrival = static_cast correctamenteint(std::ceil(static_cast seleccionadodouble(i) / speed[i]));
si (arrival)
++panol[arrival];
}
}

// Botes de escáner
int eliminada = 0;
para (int i = 0; i) {}
si (eliminada + cubo [i]
retorno i;
}
eliminada += cubo[i];
}
retorno n;
}
};
`` `

-...

#### 4.3 Python 3

``python
importar matemáticas
de la importación Lista

Solución de clase:
def eliminar Maximum(self, dist: List[int], speed: List[int] int:
n = len(dist)
* n

# Construir cubos
para d, s en zip(dist, speed):
llegada = math.ceil(d / s)
si la llegada se realizó n:
cubo[arrival] += 1

# Escanear cubos
eliminados = 0
para i en rango(n):
si se eliminan + cubo[i]
Regreso
eliminada += cubo[i]

retorno n
`` `

-...

## 5. “Bueno – malo – feo” perspectiva

Silencio
Silencio...
Silencio **Bien** Silencioso *(n)* tiempo, *O(n)* espacio. Maneja todos los casos de borde. Lógica muy clara (bono & escaneo). Silencio
Silencio **Bad** Silencio La matriz de cubo puede ser grande (`n` up to 200 000). Si muchos monstruos llegan después de `n` giros, son simplemente ignorados – pero todavía asignamos la matriz completa. Silencio
Silencio **Ugly** Silencio Una solución de orden prioritario ingenuo es simple pero `O(n log n)`. Si sólo necesitas la respuesta para una sola consulta, el truco del cubo puede sentir un poco “magico” y difícil de justificar a un entrevistador escéptico. Silencio

-...

## 6. Lo que los entrevistadores quieren

1. **Explicar su pensamiento** – empezar con “Voy a calcular los tiempos de llegada” y mostrar que los ordenará.
2. **Mostrar usted puede optimizar** – preguntar si podemos hacer mejor que `O(n log n)`. Traiga la idea del cubo, y explique el “≤ giro” invariante.
3. ** Casos de borde hundido** – por ejemplo, `dist[i] == 0`, `speed[i] == 1`, o todos los monstruos llegan después de `n`.
4. **Tiempo de tiempo-Space trade‐off** – puedes mencionar que si la memoria está en una prima, puedes mantener la lista ordenada en lugar de cubos.

-...

## 6. Final Takeaway

La solución “bucket” es un ejemplo clásico de *sorting‐by-counting* cuando las teclas (tiempos de llegada) están sujetas por `n.
Golpea el enfoque estándar de prioridad por un factor claro de *log n* y sigue manteniendo el código legible.

Cuando se le pide que resuelva este problema en una entrevista:

1. **Mostrar la solución de búsqueda de prioridad directa** (menos claro que entiendes la mecánica básica).
2. **Pregunte** si existe un enfoque más eficiente.
3. **Presentar el truco del cubo** – explicar el invariante clave (`eliminated + cubo[i] > i`) y por qué ignorar los tiempos de llegada ≥ `n` es seguro.
4. **Envuelve con la complejidad** y un rápido análisis de la cordura sobre las limitaciones.

Buena suerte, y que tus disparos siempre golpeen el objetivo adecuado! 🚀