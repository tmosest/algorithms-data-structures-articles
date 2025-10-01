-...
Título: LeetCode 1840. Altura máxima del edificio -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## Maximum Building Altura – LeetCode 1840
### (Hard ← Greedy ← O(M log M) – M = #restrictions)

■ *Problema*
■ Se le da `n` nuevos edificios en una línea (`1 ... n`).
* El edificio 1 debe tener altura 0.
* Los edificios adyacentes pueden diferir en la mayoría de 1.
* Algunos edificios tienen un límite superior: `restrictions[i] = [id, maxAltura]`.
■ Regrese el **máxima altura posible** del edificio más alto.

■ **Constraints**
≤ 109
* `0 ≤ restricciones. longitud ≤ min(n-1, 105) `
* Cada `id` es único y √≥ 1.
* `0 ≤ maxAltura ≤ 109 `

■ ** Objetivo** – escribir código limpio y listo para la producción en Java, Python y C++ y explicar los *bueno*, *bad*, y *muy* partes de la solución.

-...

## 1. Intuición " Greedy Insight

La única cosa que limita la altura de un edificio es la restricción *más cercana* en cada lado y la regla *adiferencia adyacente*.

Si miramos dos restricciones consecutivas (o la restricción virtual en el edificio 1), las alturas que podemos asignar a los edificios en entre debe satisfacer

`` `
[j] – h[j+1]
`` `

y también no pueden exceder las dos alturas “abundantes”.
Habida cuenta de las dos alturas fronterizas `hL` (a id `x`) y `hR` (a id `y '), la altura más alta posible dentro del intervalo es simplemente

`` `
max(hL, hR) + (y – x) – SilenciohL – hR habit ) / 2
`` `

porque podemos subir desde el límite inferior hasta que salgamos de la distancia.
Así que el problema se reduce a

1. **Ordenar todas las restricciones por id** (más el punto obligatorio `1,0`).
2. **Clip** la altura de cada restricción de ambos lados para que la diferencia a su vecino nunca exceda la distancia entre ellos.
3. **Esque cada intervalo** y computa la altura máxima alcanzable allí.

Es un clásico barrido codicioso.

■ *Por qué funciona* Las limitaciones son todas *local* (diferencias adyacentes) y *monotonic* (sin beneficio para elevar un edificio más allá de la restricción más cercana). Al forzar las alturas a ser tan bajas como sea necesario en ambos lados, garantizamos que siempre podemos satisfacer todas las restricciones manteniendo la posibilidad de un alto pico intacto.

-...

## 2. Casos de borde " Ugly " Piezas

Silencio
Silencio...
Silencio Grande `n` (hasta 1.000 millones) – iterating sobre cada edificio es imposible. Silencio Necesidad de utilizar enteros de 64 bits ( " largo " ) porque `máxAltura + distancia' puede rebosar de 32 bits. Silencio
Silencio No hay restricciones en absoluto: el edificio más alto está simplemente en la posición `n`. Silencio Manejo cuidadoso de la restricción *virtual* en `n` (no hay un límite superior real, pero la regla de la diferencia adyacente sigue siendo aplicable). Silencio
Las restricciones no incluyen el edificio 1 o el edificio n. Silencio
← Clasificación O(M log M) donde M ≤ 105 está bien, pero debe ser implementado correctamente. Silencio Usar un par/tuple que mezcla tipos int y largos puede llevar a errores sutiles. Silencio

-...

## 3. El Algoritmo Optimal

1. **Añada el punto obligatorio** `(1, 0)` a la lista de restricciones.
2. **Ordenar** la lista construyendo id.
3. **Paso futuro** - para cada restricción 'i' (comenzando desde el segundo), conjunto
`altura[i] = min( altura[i], altura[i-1] + (id[i] - id[i-1] )
4. **Paso de retorno** - para cada restricción `i' (comenzando desde el segundo), establecido
`altura[i] = min( altura[i], altura[i+1] + (id[i+1] - id[i] )`
5. *Computar la respuesta*
* Inicializar `ans = 0`.
* Por cada par consecutivo `(i, i+1)` en la lista, vamos `d = id[i+1] - id[i]`, `hL = height[i], `hR = altura[i+1]`.
`peak = max(hL, hR) + ( d - abs(hL - hR) ) / 2`.
`ans = max(ans, peak)`.
* También maneje el último segmento para construir `n`: `peak = height[last] + (n - id[last])`.
Actualizar `ans` en consecuencia.

El algoritmo funciona en **O(M log M)** tiempo y **O(M)** memoria – perfectamente adaptado para los límites.

-...

## 4. Código

A continuación se presentan implementaciones totalmente recomendadas en **Java**, **Python**, y **C+**.
Los tres usan enteros de 64 bits para evitar el desbordamiento.

-...

#### 4.1 Java

``java
importar java.util*;

*
* LeetCode 1840 - Altura máxima del edificio
* solución Greedy O(M log M)
*/
Clase Solución {

int public int maxBuilding(int n, int[][] restrictions) {}
// Lista de {id, altura}
Lista cumplida [] lista de contactos = nuevo ArrayList correctamente();

// Punto de partida obligatorio
list.add(new long[]{1L, 0L});

// Agregar restricciones reales
para (int[] r : restricciones) {}
list.add(new long[]{r[0], r[1]});
}

// Ordenar por id
list.sort(Comparator.comparingLong(a - título a[0]));

int m = list.size();

// Adelante
para (int i = 1; i)
long dist = list.get(i)[0] - list.get(i - 1)[0];
long allowed = list.get(i - 1)[1] + dist;
si (list.get(i)[1]
list.get(i)[1] = permitido;
}
}

// Pase trasero
para (int i = m - 2; i 0; i--) {
long dist = list.get(i +1)[0] - list.get(i)[0];
long allowed = list.get(i + 1)[1] + dist;
si (list.get(i)[1]
list.get(i)[1] = permitido;
}
}

// Respuesta completa
ans largas = 0;

// Intervalos entre restricciones
para (int i = 0; i)
idL largo = list.get(i)[0];
long hL = list.get(i)[1];
idR largo = list.get(i + 1)[0];
hR largo = list.get(i + 1)[1];

dist = idR - idL;
pico largo = Math.max(hL, hR) + (dist - Math.abs(hL - hR))) / 2;
si (peak > ans) ans = pico;
}

// Último segmento a la construcción n (sin restricción superior)
El último Id = list.get(m - 1)[0];
long lastH = list.get(m - 1)[1];
pico largo End = lastH + (n - lastId);
si (peakEnd > ans) ans = pico Fin;

// ans se ajusta en 32-bit porque las restricciones lo garantizan
retorno (int) ans;
}
}
`` `

-...

#### 4.2 Python

``python
Solución de clase:
def maxBuilding(self, n: int, restrictions: List[List[int]) - título int:
# List of tuples (id, height) as ints
lst = [(1, 0)]
lst.extend(restrictions)

# Sort by id
lst.sort(key=lambda x: x[0])

Adelante
para i en rango(1, len(lst)):
dist = lst[i][0] - lst[i-1][0]
permitido = lst[i-1][1] + dist
si lst[i][1] √≥ permitió:
lst[i] = (lst[i][0], allowed)

# Backward pass
para i en rango(len(lst)-2, -1, -1):
dist = lst[i+1][0] - lst[i][0]
permitido = lst[i+1][1] + dist
si lst[i][1] √≥ permitió:
lst[i] = (lst[i][0], allowed)

# Compute answer
ans = 0
para i en rango(len(lst)-1):
idL, hL = lst[i]
idR, hR = lst[i+1]
dist = idR - idL
pico = max(hL, hR) + (dist - abs(hL - hR)) // 2
as = max(ans, pico)

Último segmento a n
last_id, last_h = lst[-1]
as = max(ans, last_h + (n - last_id))
Retorno
`` `

-...

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxBuilding(int n, vector identificadovector identificadoint ánimo limitado) {}
// vector de pares {id, height} usando largo tiempo
vector de garantía realizable largo, largo tiempo v)
v.emplace_back(1LL, 0LL);
para (autor : restricciones)
v.emplace_back(r[0], r[1]);

(v.begin(), v.end()); // sort by id

int m = v.size();

// Adelante
para (int i = 1; i) {}
long dist = v[i].first - v[i-1].first;
largo tiempo permitido = v[i-1].second + dist;
si (v[i].second ⇩ permitido) v[i].second = permitido;
}

// Pase trasero
para (int i = m-2; i 0; --i) {
long dist = v[i+1].first - v[i].first;
largo tiempo permitido = v[i+1].second + dist;
si (v[i].second ⇩ permitido) v[i].second = permitido;
}

ans largos = 0;

// Intervalos entre restricciones
para (int i = 0; i) {}
long idL = v[i].first, hL = v[i].second;
long idR = v[i+1].first, hR = v[i+1].second;
dist largo largo = idR - idL;
pico largo = max(hL, hR) + (dist - llabs(hL - hR)) / 2;
ans = max(ans, peak);
}

// Último segmento para construir n
long long last_id = v.back().first, last_h = v.back().second;
ans = max(ans, last_h + (long long)n - last_id);

volver estática_cast seleccionado(ans)
}
};
`` `

-...

## 5. Por qué esta solución es *production-ready*

Críterion Silencio Lo que hicimos
Silencio...
Silencio **La complejidad del tiempo** Silencioso `O(M log M)` – aceptable para `M ≤ 100 000`. Silencio
Silencio **La complejidad del espacio** Silencioso `O(M)` – no hay necesidad de tocar cada uno de los hasta 1.000 millones de edificios. Silencio
Silencio **La seguridad del flujo** Silencio Todos los valores intermedios utilizan 64 bits (`long`/`long'). Silencio
Silencio **Readability** Silencio Nombres variables como `idL`, `hL`, `peak` hacer la intención obvia. Silencio
Silencio **Testing** Silencio El código maneja cero, uno y muchas restricciones sin casquillo especial en el bucle principal. Silencio
Silencio **Edge‐case safety** Silencio El recortado hacia adelante garantiza que cada par de puntos consecutivos satisface la regla de distancia, eliminando la necesidad de un cheque de viabilidad complejo más adelante. Silencio

-...

## 6. Resumen

TENIDO Aspecto TENIDO ANTERIOR
Silencio...
Silencio **Bien** Silencio Simple barrido codicioso, escaneos lineales, fórmula clara para el pico del intervalo. Silencio
Silencio **Bad** Silencio Ninguno—tiempo y memoria son óptimos. Silencio
Silencio **Ugly** Silencio Uso cuidadoso de tipos de 64 bits y puntos virtuales para `n`. Silencio

Este patrón de ** surtido + análisis de intervalos de dos caras** aparece en muchos problemas (por ejemplo, “Construir la Fence”, “Maximum Subarray with Constraints”), y el mismo razonamiento se aplica: hacer cumplir las limitaciones localmente, luego computar el óptimo global de los límites recortados.

-...

## 7. Cómo aplicar este conocimiento

* **Entrevista** – describir el barrido codicioso y la fórmula del pico del intervalo en menos de 5 minutos.
* ** Código de producción** – añadir comprobaciones defensivas (por ejemplo, verificar " n " prendas " no nulas " ).
* **Testing** – crear pruebas de unidad cubriendo:
* Sin restricciones.
* Limitación única lejos de ambos extremos.
* Múltiples restricciones superpuestas.
* Grande `n` con pocas restricciones.
* Casos que obligan al recortado hacia adelante o hacia atrás a entrar en vigor.

Con esta fundación se pueden abordar con confianza las variaciones de los problemas de “construcción” que aparecen en entrevistas de codificación, competiciones y software de planificación arquitectónica del mundo real. ¡Feliz codificación!

-...

**Keywords**: *Maximum Building Height*, *LeetCode 1840*, *Greedy Sweep*, *O(M log M)*, *adjacent difference*, *restriction clipping*, *Java*, *Python*, *C+*, *edge cases*.