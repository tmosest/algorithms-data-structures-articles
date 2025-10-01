-...
Título: LeetCode 3347. Frecuencia máxima de un elemento después de realizar operaciones II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 3347. Frecuencia máxima de un elemento después de realizar operaciones II
■ **Hard Silencio Público**
■ *Java • Python • C++ – Solución de 3 idiomas + artículo de preparación de entrevistas para SEO*

-...

#### TL;DR
Usted tiene un array `nums`, un rango `[-k, k]` y un número limitado de operaciones `numOperations`.
Cada operación le permite elegir un índice *no utilizado* y añadir cualquier valor de `[-k, k]` a él.
Usted quiere maximizar el número de elementos iguales que pueden terminar en el array.

La estrategia óptima es un **sweep-line sobre todos los puntos finales del intervalo**.
Tiempo: `O(n log n)` - ordenar 3 n puntos finales.
Memoria: `O(n)` – contadores + mapa de eventos.

A continuación encontrará soluciones de trabajo completas en **Java, Python, y C++**, además de un artículo **blog completo** que explica el problema, el algoritmo, las trampas, y por qué es una gran pregunta de entrevista.

-...

## 🧩 Problema Restatement

`` `
Input
nums – array de tamaño 1 ... 10^5
k – 0 ... 10^9
numOperaciones – 0 ... nums.length

Operación (mínimas repetidasOperaciones)
1. Elige un índice que no haya sido elegido antes.
2. Añadir un entero v donde -k ≤ v ≤ k a nums[i].

Objetivo
Devuelve la frecuencia máxima posible (es decir, cuántos elementos son iguales) de cualquier valor después de realizar todas las operaciones.
`` `

■ *Ejemplo*
■ `nums = [1,4,5] , k = 1 , numOperaciones = 2 `
■ Podemos transformar el array en `[1,4,4]` → frecuencia de `4` = 2.

-...

## 🔍 Observaciones clave

1. **Objetivo accesible* *
Para un elemento `a` se puede alcanzar cualquier objetivo `t` en el intervalo cerrado `[a-k , a+k]` con * una* operación (o 0 si `a == t`).

2. **Intervalos en la línea número**
Cada entrada de matriz nos da un intervalo de posibles valores finales:
`` `
a → [a-k , a+k]
`` `
El problema se convierte en: encontrar un punto 't' que está cubierto por los intervalos más.

3. ** Presupuesto de las operaciones**
- Los elementos ya iguales a " no " son " libres " .
- Podemos convertir en la mayoría de las `numOperaciones' otros elementos que cubren `t`.

Por lo tanto, la mejor frecuencia en un punto `t` es
`` `
cnt[t] + min(numOperaciones , cover[t] - cnt[t]
`` `
Donde
* `cnt[t]` - ¿Cuántos elementos ya no son
* `cover[t]` – ¿Cuántos intervalos contienen “t” (es decir, cuántos elementos están dentro de “k” de “t”.

4. **Todos los puntos útiles son puntos finales**
La función `cover(t)` sólo cambia en el extremo izquierdo o derecho de un intervalo.
Es suficiente para barrer todas las coordenadas distintas que aparecen como
* `a - k` (interval start)
* `a + k + 1` (uno más allá del final del intervalo, para un clásico “+1 / -1” barrido).

5. *Off‐by-one safety*
El evento en `a + k + 1` elimina el intervalo **después** el último entero que puede alcanzar `t`.
Por eso agregamos **+1** al punto final derecho.

-...

##  Settlement Sweep‐Line Algorithm (Illustrated)

`` `
para cada valor a nums:
cnt[a] += 1
eventos[a] - k] += 1 //
eventos[a + k + 1] -= 1 // intervalo extremos (después de +1)

ordenar todas las claves en eventos → puntos[]
activo = 0
respuesta = 0

para p en puntos [] (orden de asignación):
activo += eventos[p] // #intervalos que cubren p
ya = cnt.get(p, 0)
extra = min(activo - ya, numOperaciones)
candidato = ya + extra
respuesta = max(respuesta, candidato)
`` `

*El barrido garantiza que en cualquier momento sabemos exactamente cuántos índices se pueden convertir en ese punto. *

-...

## 🚀 Three Working Implementations

#### ## 1down⃣ Java

``java
importar java.util*;

Solución de la clase pública {}
int public maxFrequency(int[] nums, int k, int numOperaciones) {}
Mapa seleccionadoInteger, Integer ratio = nuevo HashMap Quería(); // frecuencias de valor existentes
Mapa seleccionadoLong, Integer pocos eventos = nuevo HashMap garantizado(); // +1 al principio, -1 después de final

para (int a : nums) {
count.merge(a, 1, Integer::sum);

long left = (long) a - k;
larga derecha = (long) a + k + 1; // una pasada el intervalo
eventos. merge(izquierda, 1, entero::sum);
eventos. merge(right, -1, Integer::sum);
}

Lista de puntos de contactoLong = nuevo ArrayList correctamente(events.keySet());
Collections.sort(points);

long active = 0; // current #intervals covering the point
int best = 0;

(long p : points) {
activo += events.get(p);
int ya = count.getOrDefault(int) p, 0);

// ¿Cuántos de los otros índices que cubren p todavía podemos cambiar?
int extra = (int) Math.min(active - already, numOperations);
int candidate = ya + extra;
mejor = Math.max(mejor, candidato);
}
devolver mejor;
}
}
`` `

■ *La complejidad*
■ *Time* `O(n log n)` – sorting at most `3n` endpoints
■ *Memory* `O(n)` – dos mapas de hash

-...

#### 2down⃣ Python

``python
de las importaciones de colecciones Contrato
de la importación Lista

Solución de clase:
def maxFrequency(self, nums: List[int], k: int, numOperations: int) - Conf int:
cnt = Counter(nums) # frecuencias existentes
eventos = Counter() # +1 a la izquierda, -1 a la derecha+ 1

para una en las numidades:
izquierda = a - k
derecho = + k + 1 exclusivo
sucesos[izquierda] += 1
sucesos[derecha] -= 1

puntos = ordenados (eventos)
activo = 0
mejor = 0

para p en puntos:
activos += eventos[p]
ya = cnt.get(p, 0)
extra = min(activo - ya, numOperaciones)
candidato = ya + extra
mejor = max(best, candidate)

mejor
`` `

■ **¿Por qué `derecho = un + k + 1`?**
■ Mantiene el intervalo * cerrado* en `a + k`.
■ Después de esta coordinación dejamos de contar ese elemento.

-...

#### 3down⃣ C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxFrequency(vector fieltro implicado nums, int k, int numOperaciones) {}
unordered_map realizado largo, int contacto cnt; // valor → freq
unordered_map se realizó durante mucho tiempo, ent contacto ev; // punto de evento → delta

para (int a : nums) {
cnt[a]+;

largo largo l = estática_cast seleccionadolong long(a) - k;
largo largo r = estática_cast efectuado largo largo(a) + k + 1; // exclusiva
ev[l] += 1;
ev[r] -= 1;
}

vector de puntos de larga data;
puntos.reserve(ev.size());
for (auto &p : ev) points.push_back(p.first);
(puntos.begin(), points.end());

long long long active = 0;
int best = 0;

para (long long p : points) {}
activo += ev[p];
int ya = cnt.count(p) ? cnt[p] : 0;
int extra = static_cast didint(min(active - already, static_cast obtenidoslonglar(numOperations)));
mejor = max(best, already + extra);
}
devolver mejor;
}
};
`` `

■ **Tip** – siempre lanzado a 'long long' al añadir `k` para evitar el desbordamiento accidental, aunque 2 × 10^9 se ajuste a `int`.

-...

El bueno, el malo, el feo

¿Qué es lo mejor que está viviendo?
Silencio..
TENIDO TENIENDO TENIDO • `O(n log n)` – lo suficientemente rápido para 10^5. (no FFT). • Intuición geométrica clara. La línea de números es enorme (hasta 10^9), por lo que debemos **comprimir** coordenadas. Silencio • Off‐por-uno en la creación de eventos (`+1` a la derecha). puede llevar a desbordamiento. • Olvidando que los índices ya son iguales al costo de destino **0** operaciones. Silencio
La línea Sweep es un patrón clásico de estilo entrevista. • Demuestra conocimiento de sumas prefijas, conteo de eventos y compresión basada en mapas. Usted debe manejar **unused‐index** limitación – muchos candidatos olvidan que los elementos ya iguales al objetivo son libres. Silencio • Usar un `TreeMap` en lugar de un vector+sort conduce a eventos `O(n log n)` pero un factor adicional de registro para cada actualización – todavía bien pero menos limpio. Silencio
TENIDO ❌ TENEDO • Si `k` es 0, el algoritmo degenera a la "frecuencia máxima existente" – trivial para probar. TEN • Si intentas una ingenua “traer cada posible bucle “t””, llegarás a “O(n * range)” – imposible. Silencio • Números negativos erróneos en teclas “longas largas” cuando regreses a “int” (ver para ‘INT_MIN’). Silencio

-...

Soluciones alternativas (por qué el sudor es mejor)

Silencio Silencio Silencio Complejidad
Silencio--------------------------
Silencio **Binary Search + Prefix Sum** Silencio `O(n log M)` (M = max value) Н Works if you only need *max* frequency but *without* `numOperations` limit. Silencio
Silencio **Dos-Pointer / Ventana deslizante** Silencioso `O(n)` Únicamente aplicable cuando `k` es lo suficientemente pequeño que el objetivo debe ser un valor existente; falla cuando `k` es grande. Silencio
Silencio ** Árbol del segmento** Silencioso `O(n log M)` soporta Peso pesado; innecesario cuando el barrido es más fácil. Silencio

El barrido es la solución general más limpia y rápida para la declaración del problema completo.

-...

## 📈 Complexity Analysis

`` `
Let n = nums.length
`` `

*Eventos generados*: `3 n` (inicio, final+1, y puntos de valor existentes)
*Sorting*: `O(3n log 3n)` ♥ `O(n log n) `
*Sweep*: lineal in number of distinct points, `O(n)`

Memoria:
- " cnt " - a la mayoría de las " teclas distintas "
- `events ' - at most `2n` keys
→ `O(n)`.

-...

## 🎤 Why This Problem Rocks for Interviews

1. ** Pensamiento geométrico** – visualiza valores como intervalos, haciendo intuitiva la solución.
2. **La compresión coordinada** – enseña cómo manejar grandes rangos.
3. **Evento contando** – clásico truco prefijo-sum en la mosca.
4. **Operaciones presupuesto** – obliga a los candidatos a pensar en *free* versus *paying* índices.
5. ** Manejo de maletas** – `k = 0`, valores negativos, gran `k` toda la robustez de prueba.

Si usted puede explicar el algoritmo en * minutos*, usted está mostrando profundidad de comprensión que va más allá de DP de nivel superficial o clasificando trucos.

-...

## 📌 Takeaway

*Utilice una línea de barrido con eventos “+1 / -1” para contar cuántas entradas de array se pueden convertir en cada posible valor final. Agregue el presupuesto de operaciones en el cálculo y obtendrá la frecuencia final óptima en el tiempo `O(n log n). *

-...

¡Feliz codificación! 🧑

-...

*Si tienes alguna pregunta, deja un comentario a continuación o comparte tus propias soluciones. ¡Mantengamos la discusión! *