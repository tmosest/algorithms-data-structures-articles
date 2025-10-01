-...
Título: LeetCode 2533. Número de buenas cuerdas binarias -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
##  Detention 2533 – Number of Good Binary Strings
**Medium tención 1 ≤ minLength ≤ maxLength ≤ 105 ≤ 1 ≤ 1Grupo, ceroGrupo ≤ maxIngth* *

■ En una cadena binaria *buena*
■ 1. Duración [minLength, maxLength]
■ 2. Cada bloque consecutivo de `1's tiene una longitud que es un múltiple de `uno Grupo
■ 3. Cada bloque consecutivo de `0`s tiene una longitud que es un múltiple de `cero Grupo
■ 4. (Zero se considera un múltiplo de todo)

Devuelve el número de cadenas buenas modulo 1 000 000 007.

-...

## 🚀 High‐Level Idea

Las limitaciones (maxLength ≤ 105) prohíben enumerar todas las cadenas.
En su lugar, observe que una buena cuerda puede ser construida **incrementalmente**:

* A partir de una cadena vacía (longitud = 0, que satisface la regla “multiple”).
* Los apéndices de cada paso
* `oneGroup ' consecutive `1`s, **or* *
Consecuentemente.

Así que si sabemos cuántas buenas cadenas de longitud `i` existen (`dp[i]`), podemos obtener los recuentos de longitudes más largas añadiendo los dos posibles tamaños de bloque.

Esta es una recurrencia de programación dinámica clásica *bottom‐up*.

`` `
dp[0] = 1 // cuerda vacía
para i = 1 ... maxLength
si ≥ unGroup: dp[i] += dp[i - oneGroup]
si ≥ ceroGroup: dp[i] += dp[i - ceroGroup]
dp[i] %= MOD
`` `

La respuesta es la suma de `dp[i]` para todos `i` en `[minLength, maxLength]`.

La recurrencia se ejecuta en **O(maxLength)** tiempo y necesidades **O(maxLength)** memoria – lo suficientemente rápido para 105.

-...

## ♥ Code Walk‐Through (Java)

``java
importar java.util*;

Clase Solución {
int final estático privado MOD = 1_000_000_007;

public int goodBinaryStrings(int minLength, int maxLength,
int one Grupo, número ceroGrupo) {}

// dp[i] = número de buenas cadenas de longitud i
int[] dp = nuevo int[maxLength + 1];
dp[0] = 1; // hilo vacío

resultado largo = 0;

para (int i = 1; i) = maxLength; i++) {
si
dp[i] = (dp[i] + dp[i - oneGroup]) % MOD;
}
si
dp[i] = (dp[i] + dp[i - ceroGroup]) % MOD;
}
si
resultado = (resultado + dp[i]) % MOD;
}
}

Resultado de retorno (int)
}
}
`` `

**Puntos clave* *

Silencio TENIDO ANTERIOR ANTERIOR
Silencio...
Silencio `dp[0] = 1` Silencio La cuerda vacía cuenta como un prefijo válido (cero es un múltiplo de todo). Silencio
Silencio `if (i не= oneGroup)` Silencio Sólo se extiende cuando tenemos suficiente espacio para un nuevo bloque. Silencio
Silencio `result += dp[i]` Silencio Sólo suma cuando la longitud cumple con el requisito mínimo. Silencio

-...

## ♥ Code Walk‐Through (Python)

``python
Solución de clase:
MOD = 1_000_000_007

def goodBinaryStrings(self, minLength: int, maxLength: int,
oneGroup: int, ceroGroup: int) - Conf int:

dp = [0] * (maxLength + 1)
dp[0] = 1 cuerda vacía
Resultado = 0

para i en rango(1, maxLength + 1):
si me cierro uno Grupo:
dp[i] = (dp[i] + dp[i - oneGroup]) % self. MOD
si yo >= ceroGroup:
dp[i] = (dp[i] + dp[i - ceroGroup]) % yo. MOD
si me cierro MinLength:
resultado = (result + dp[i]) % yo. MOD

Resultado de retorno
`` `

La misma lógica, sólo la sintaxis pitónica.

-...

## ♥ Code Walk‐Through (C++)

``cpp
Clase Solución {
public:
static const int MOD = 1'000'007;

int goodBinaryStrings(int minLength, int maxLength,
int one Grupo, número ceroGrupo) {}
vector implicado dp(maxLength + 1, 0);
dp[0] = 1; // hilo vacío
largas res = 0;

para (int i = 1; i) = maxLength; ++i) {
si
dp[i] = (dp[i] + dp[i - oneGroup]) % MOD;
si
dp[i] = (dp[i] + dp[i - ceroGroup]) % MOD;
si
res = (res + dp[i]) % MOD;
}
volver estática_cast seleccionado(res)
}
};
`` `

-...

## 📈 Complexity Analysis

Silencio Silencio Java Silencio Python Silencio C++
Silencio...
Silencio **Tiempo** Silencioso `O(maxLength)` Silencio `O(maxLength)` Silencio
Silencio **Espacio** Silencioso `O(maxLength)` Silencio `O(maxLength)` Silencio

Tanto el tiempo como el espacio son lineales en la longitud máxima de la cuerda – perfectamente bien para 105.

-...

## 🎯 Bien, el Mal, y el Ugly

Silencio Silencio
Silencio...
Silencio **Diseño** Silencio Clear recurrence; bottom-up DP TEN TEN ANTE ANTE TENIDO TENIDO
Silencio **Edge Cases** tención Handles de longitud cero como múltiple; minLength=1 Silencio TENIENDO TENIDO
tención **Readability** Silencios simples, comentarios
Silencio **Scalability** Silencio Tiempo lineal/espacio Silencio TENIDO Silencio
Silencio **Potential Pitfalls** ← Olvidar el modulo después de cada adición
Silencio ** Uso de memoria** Silencio Únicamente `máximoLongitud+1` enteros NOVED QUIÉN ANTERIVAR ANTERIVISTA ANTERIVADA
Silencio **Aproximación alternativa** ← Memoización de arriba abajo (recursiva) Нели ующую puede llegar a la profundidad de recursión en grandes entradas
Silencio **Optimización** Silencio Ninguno necesita Нели вый полекововани нельный нельный уютентельный нетели нентеный уютеный ующе ующе ующе ный уюте нененени уюте ующеный уюте ующе ующе уюте уютени ный уютеный ующеный ующеный уютенененый ный уютентентеный уютеный ующенененененененененененый у

¿Por qué? Arriba está el ganador**
- Evita los límites de la pila de recursión.
- Paso único sobre el rango de longitud.
- No hay necesidad de estructuras de datos adicionales más allá de la matriz de `dp`.

-...

## 🎯 SEO‐Optimized Blog Post

■ *Título*
■ *Cracking LeetCode 2533 – Número de buenas cadenas binarias – Java, Python & C++ DP Tutorial*

■ **Meta Descripción**
■ Master LeetCode 2533 con una solución de programación dinámica clara en Java, Python y C++. Aprende el algoritmo, la complejidad y las ideas de entrevista.

■ **Keywords**
■ LeetCode 2533, Número de buenas cuerdas binarias, programación dinámica, entrevista de codificación, solución Java, solución Python, solución C++, entrevista de ingeniero de software, diseño de algoritmos

-...

#### Introduction

Cuando vi por primera vez **LeetCode 2533 – Número de buenas cuerdas binarias**, pensé que era sólo otro problema de las cadenas de cuentas. ¿El giro? Los bloques de cuerda deben ser *multiples* de tamaños de grupo dados.
En una entrevista, el entrevistador suele querer que muestres dos cosas:

1. Usted entiende las limitaciones y puede elegir un algoritmo eficiente.
2. Puede traducir ese algoritmo en código idiomático y limpio en su idioma elegido.

A continuación, paso por la solución DP que se ejecuta en **O(n)** tiempo, le doy listo para pasar Java, Python y C++ snippets, y explicar por qué este enfoque es perfecto para una entrevista de codificación.

-...

## Problema de reestablecimiento

Un *bueno* de cadena binaria satisfies:

- Longitud .
- Cada carrera consecutiva de '1's tiene una longitud que es un múltiple de 'unGroup'.
- Cada carrera consecutiva de '0's tiene una longitud que es un múltiple de 'cero' Grupo.

Devuelve el número de cuerdas buenas modulo `109+7`.

Las limitaciones hacen imposible una enumeración ingenua (`2^maxLength` strings). Necesitamos una solución *linear*.

-...

### The Core Insight

Una buena cuerda puede ser **crewn** de una cadena vacía agregando repetidamente un bloque de longitud `oneGroup' o `zeroGroup`.
Si denotamos:

`` `
dp[i] = número de buenas cadenas de longitud exacta i
`` `

entonces para cualquier `i':

`` `
dp[i] = (dp[i - oneGroup] si ≥ oneGroup) +
(dp[i - ceroGroup] si ≥ ceroGroup)
`` `

Debido a que la cadena vacía (longitud 0) satisface la condición múltiple, empezamos con `dp[0] = 1`.
La respuesta final es la suma de `dp[i]` para todos `i` en `[minLength, maxLength]`.

-...

### Step‐by‐Step Implementation

1. **Initializar** `dp[0] = 1`.
2. **Iterate** `i` from `1` to `maxLength`.
3. ** Actualizar** `dp[i]` utilizando la recurrencia (cuidado con `i - bloque` sólo si no es negativo).
4. **Modulo** el resultado después de cada adición para evitar el desbordamiento.
5. **Acumular** en la respuesta cuando `i ≥ minLength`.

Esto es lo que parecen las tres soluciones de lenguaje – sólo diferencias de sintaxis.

-...

## Java, Python, > C++ Código

*(Código completo snippets arriba)*

■ **Consejo para el entrevistador**
■ “¿Recordaste aplicar el modulo después de cada adición?” – El entrevistador te probará en el flujo entero.

-...

### Complejidad Discusión

- **Tiempo**: Tocamos cada índice una vez - `O(maxLength)`.
- **Espacio**: Una matriz de tamaño `maxLength+1` - `O(maxLength)`.

Con `maxLength ≤ 105`, esto funciona en milisegundos en máquinas modernas.

-...

### Interview‐Ready Variations

Silencioso Variación Silencioso Cuándo utilizar ← Pros
Silencio...
Silencio **Bottom‐Up DP (el anterior)** Silencio La mayoría de las entrevistas TENIDO Simple, no recursión, rápido TENIDO Ninguno TENIDO
Silencio **Top‐Down Memoization** Silencio Si prefieres la recursión Silencio Easier para escribir inicialmente la profundidad de la Recursión puede alcanzar el límite de Python; ligeramente más lento debido a las llamadas de función tención
Silencio **Recursivo + Memo** Silencio Para pequeñas limitaciones Silencio Estilo funcional elegante Silencio Mismo riesgo de profundidad Silencio

-...

### Por qué esta solución Rocks

✔ Cambios en la Explicación
Silencio...
TENIDO *Tiempo de iluminación* TENIDO Handles 105 en 1 s
*Single array* tención Minimal Memory overhead. Silencio
Silencio *Aritmética móvil* Silencio Evita el flujo de 64 bits. Silencio
Silencio *Lógica azul* Silencio Un bucle, dos condicionales – perfecto para una respuesta de entrevista limpia. Silencio

-...

### Wrap‐Up

- **LeetCode 2533** es un gran problema de entrevistas para probar * compresión del estado* y *block‐based DP*.
- La recurrencia es **directamente derivada** de la descripción del problema "crecer la cadena".
- El código Java, Python y C++ está listo para la producción: comentado completamente, utiliza constantes y respeta la limitación modulo.

Si estás preparando una entrevista con *software Engineer*, esta solución demuestra:

- Comprensión profunda de las limitaciones.
- Capacidad para diseñar una recurrencia DP.
- Fluencia en tres de los idiomas de entrevista más populares.

Buena suerte, y feliz codificación! 🚀

-...

### Take‐away Code Snippets

Silencio Idioma Silencio Código Silencio
Silencio...
[Java snippet] (#java)
[Python snippet] (#python)
Silencio **C+** Silencio [C+++](#cpp)

-...

**No dude en copiar—pasar estas soluciones a su editor local o panel de presentación LeetCode. ¡Feliz solución