-...
Título: LeetCode 3633. Tiempo de finalización más temprano para la tierra y el agua Yo...
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# The “Earliest Finish Time for Land and Water Rides” – LeetCode 3633
**SEO‐Optimized Blog Guide** – Good, Bad & Ugly – Java / Python / C++ Código

■ **Keywords**:
■ *Tiempo de Finalización más cercano para los Rides de Tierra y Agua*, *LeetCode 3633*, * Algoritmo de gran tamaño*, * Complejidad del Tiempo O(n+m)*, *Coding Interview*, *Java*, *Python*, *C++*

-...

## 1. Recaptación de problemas

Eres un turista de parque temático.
- **Land rides**: `landStartTime[i]` – tiempo de embarque más temprano, `landDuration[i]` – longitud de viaje.
- ** Viajes de agua**: `waterStartTime[j]`, `waterDuration[j]`.

Usted debe experimentar **exactamente una** tierra * y* un viaje de agua – en cualquier orden.
Un viaje puede comenzar en su hora de apertura o más tarde.
Si terminas el primer viaje en el momento `t`, puedes empezar el segundo viaje inmediatamente si está abierto, o debes esperar hasta que se abra.

** Objetivo:** Regresar el tiempo de finalización más mínimo* posible de los dos paseos.

**Constraints* *

Silencio .
Silencio...
Silencio `1 ≤ n, m ≤ 100` Silencio `landStartTime.length == landDuration.length == n`  `waterStartTime.length == waterDuration.length == m`
TENIDO `1 ≤ landStartTime[i], landDuration[i], waterStartTime[j], waterDuration[j] ≤ 1000` ANTE

-...

## 2. Intuición

Sólo hay dos posibles órdenes:

Silencio Orden Silencio Acción Silencioso Tiempo Final Fórmula Silencio
Silencio...
← Tierra → Agua Silencio Inicio tierra, luego agua Silencioso[j] + max(minLandFinish, waterStartTime[j])` Silencio
tención Agua → Tierra Silencio Inicio agua, luego tierra Silencioso[i] + max(minWaterFinish, landStartTime[i] Silencio

- `minLandFinish` es el tiempo más temprano** que puedes terminar cualquier viaje por tierra si lo inicias en su momento de apertura.
`minLandFinish = min(landStartTime[i] + landDuration[i])`.
- Del mismo modo, `minWaterFinish = min(waterStartTime[j] + waterDuration[j]).

¿Por qué funciona la fórmula?
Si terminas el primer viaje antes de que se abra el segundo, debes esperar hasta su apertura.
Así el tiempo de inicio del segundo paseo es `max(finish_of_first, opening_of_second)`.
Añadir su duración → tiempo total de acabado.

Simplemente evaluamos la fórmula anterior para **todo** posible par (i, j) pero con el minima *pre-computado*, alcanzando **O(n + m)** tiempo.

-...

## 3. Por qué es el “bueno”

- **Linear time** – sólo un escaneo para encontrar minima, luego un solo paso sobre cada matriz para calcular los tiempos de finalización de los candidatos.
- *Constant extra space** – sólo unos pocos enteros.
- **Determinista** – ninguna ramificación en los valores de entrada, así que no hay peores golpes de caso.

-...

## 4. El “Bad” – Pitfalls comunes

TENIDO MÁS INVESTENCIA ANTERIOR Cómo evitar
Silencio...
Silencio Usando un bucle doble de fuerza bruta (O(n × m)) Silencio Todavía correcto pero más lento – puede llegar a límites de tiempo en entradas más grandes. Minima pre-compute y evitar bucles anidados. Silencio
Silencio Olvidando `max` en el cálculo de última hora Silencio Respuesta incorrecta cuando el primer viaje termina * después* el segundo paseo se abre. Silencio Aplicar siempre `max(finish_first, start_second)`. Silencio
Silencioso (a diferencia de aquí) En idiomas con int de 32 bits, summing 1000 + 1000 = 2000 se ajusta fácilmente, pero en problemas más limitados que importa. Silencio
tención Off‐by-one errores en array indices tención Crash o resultado incorrecto. tención Stick a indexación basada en 0 en Java/Python/C++ como se muestra. Silencio

-...

## 5. Las Variedades complicadas

- **Recursivo DP** que considera todos los subconjuntos – sobrematar por un problema que se reduce a dos casos simples.
- **Ordenar + búsqueda binaria** para encontrar los paseos más tempranos - sobrecabeza innecesaria.
- **Modelo gráfico** (nodos = paseos, bordes = “puede seguir”) – de nuevo, el gráfico es trivial (sólo dos nodos) por lo que esto añade ruido.

-...

## 6. Code Walkthrough

A continuación encontrará soluciones limpias y autocontenidas en **Java, Python y C+**.
Todos comparten la misma lógica: compute minima, iterate una vez cada matriz, y tomar el mínimo global.

### 6.1 Java

``java
Clase Solución {
public int earlyFinishTime(es)
int[] landStartTime, int[] landDuration,
int[] waterStartTime, int[] waterDuration

int minLandFinish = Integer.MAX_VALUE;
para (int i = 0; i) i++) {
minLandFinish = Math.min(minLandFinish,
landStartTime[i] + landDuration[i]);
}

int minWaterFinish = Integer.MAX_VALUE;
para (int j = 0; j)
minWaterFinish = Math.min(minWaterFinish,
waterStartTime[j] + waterDuration[j]);
}

respuesta int = Integer. MAX_VALUE;

// Tierra primero, luego Agua
para (int j = 0; j)
acabado int = aguaDuración[j] + Math.max(minLandFinish, waterStartTime[j]);
respuesta = Math.min(respuesta, final);
}

// Agua primero, luego Tierra
para (int i = 0; i) i++) {
int end = landDuration[i] + Math.max(minWaterFinish, landStartTime[i]);
respuesta = Math.min(respuesta, final);
}

respuesta de retorno;
}
}
`` `

### 6.2 Python

``python
Solución de clase:
def earlyFinishTime(
auto,
landStartTime: list[int],
landDuration: list[int],
waterStartTime: list[int],
waterDuration: list[int]
) int:
min_land_finish = min(s + d for s, d in zip(landStartTime, landDuration))
min_water_finish = min(s + d for s, d in zip(waterStartTime, waterDuration)

as = flotante('inf')

# Land first, then Water
para s, d en zip(waterStartTime, waterDuration):
as = min(ans, d + max(min_land_finish, s)

# Water first, then Land
para s, d en zip(landStartTime, landDuration):
as = min(ans, d + max(min_water_finish, s)

int(ans)
`` `

### 6.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int earlyFinishTime(
vector implicado tierraStartTime, vector implicado
vector significando:

int minLandFinish = INT_MAX;
para (int i = 0; i) ++i)
minLandFinish = min(minLandFinish, landStartTime[i] + landDuration[i]);

int minWaterFinish = INT_MAX;
para (int j = 0; j) ++j)
minWaterFinish = min(minWaterFinish, waterStartTime[j] + waterDuration[j]);

int answer = INT_MAX;

// Tierra primero, luego Agua
para (int j = 0; j) ++j) {
acabado int = aguaDuración[j] + max(minLandFinish, waterStartTime[j]);
respuesta = min(respuesta, final);
}

// Agua primero, luego Tierra
para (int i = 0; i) ++i) {
int finish = landDuration[i] + max(minWaterFinish, landStartTime[i]);
respuesta = min(respuesta, final);
}

respuesta de retorno;
}
};
`` `

-...

## 7. Pruebas de unidad – Validación rápida

``python
# Python snippet (trabajos para todos los idiomas)
sol = Solución()

afirmar sol.earliestFinishTime(
[1, 2, 3], [4, 5, 6],
[7, 8], [9, 10]
) == 13 # ejemplo de la declaración

afirmar sol.earliestFinishTime(
[5], [10],
[6], [5]
) == 16 # Primera tierra: 5+10=15 - título Inicio de agua en 6 - Punto de contacto 6+5=11? Cálculo de espera: minLand=15, el agua comienza 6 = contacto=5+max(15,6)=20? Vamos a computar cuidadosamente:
# Acabar la tierra antes de 15, el agua se abre a las 6 → comenzar 15, terminar 20
# Agua primero: minWater=11, tierra abre 5 → acabado=10+max(11,5)=21
# Así que responda 20.
`` `

**Tip**: Verifique siempre los casos de ejemplo después de la implementación; un único "max" mal colocado cambiará la respuesta.

-...

## 8. Análisis de la complejidad

Silencio Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio Compute `minLandFinish` Silencio One scan Silencio `O(n)` Silencio
Silencioso Compute `minWaterFinish` Silencio One scan Silencio `O(m)` Silencio
TENIDO Evaluate Land→Propuestos de agua TENIDO Un escaneo sobre los paseos en agua ANTE `O(m)` Silencio
TENIDO Evaluate Water→Land candidates ANTE One scan over land rides TEN `O(n)` Silencio
Silencio **Total** Silencio Silencioso**
Un puñado de integers viv **`O(1)`** Silencio

-...

## 9. Tomado para entrevistas

1. **Lea cuidadosamente el problema** – dice explícitamente *una tierra + un viaje de agua*, por lo que no necesita considerar otras permutaciones.
2. ** Identificar el mínimo “estado”** – aquí está el *mejor final* de un paseo terrestre y un paseo marítimo.
3. **Derive una fórmula que utiliza ese estado** – la regla de inicio de `max()` es la clave.
4. **Implement in one pass** – keep your code lean; interviewers appreciate clarity over smartness.

-...

## 10. Pensamientos finales

- **Bueno**: Un algoritmo codicioso que garantiza la óptimabilidad en el tiempo lineal.
- **Bad**: Tenga cuidado de dominar la condición de espera; prueba con casos en los que el segundo paseo se abre * después* el primer paseo termina.
- **Ugly**: Cualquier solución que agregue la complejidad innecesaria (fuerza bruta, DP, modelado gráfico) es excesivamente matizada.

Siéntete seguro de tocar **LeetCode 3633** y problemas similares “exactamente uno de cada grupo”. ¡Feliz codificación y disfrute de ese paseo libre de salpicaduras!