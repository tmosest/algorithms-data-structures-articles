-...
Título: LeetCode 3117. Suma mínima de valores por Dividing Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 3117 – Mínimo Suma de valores por Dividir Array
■ **Hard ⋅ Dynamic Programming ← Bitwise Y ← Job‐Entreview Friendly* *

-...

## Tabla de contenidos

Silencio Sección Silencio Lo que Aprenderás
Silencio...
TENIDO RESPECTO DEL Problema Resúmenes
¿Por qué es una gran pregunta de la entrevista?
La “buena” – La intuición de la clave
Los casos “Bad” – Common Pitfalls & Edge tención
La aplicación “intencionada” – La implementación “Slick”
Silencio 6️ DP Diseño Silencio Inicio arriba con la memoización
TENIDO  Complex Análisis de la complejidad
tención 8️ Código en Tres Idiomas Silencio Java, Python, C++ Silencio
Silencio 9️ SEO‐Optimised Blog Silencio Palabras clave & consejos de búsqueda de empleo ←
TEN 🔚 Final Take‐away Silencio Cómo clavar esta pregunta en una entrevista

-...

Sinopsis del problema

**LeetCode 3117 – Mínimo Suma de valores por Dividir Array**
*Dificultad* Duro

■ *Given*
- `nums[0...n-1]` - una variedad de enteros positivos (`1 ≤ n ≤ 104`)
■ - `andValues[0...m-1]` - deseada de poco a poco por cada subarray (`1 ≤ m ≤ min(n,10)`)
■
■ # Objetivo #
■ Split `nums` en **m** subarros descomunales, contiguos
> tal que el bit-wise Y del *i‐th* subarray iguala `andValues[i]`.
■ El valor* de un subarray es su elemento **último**.
■ Regrese el mínimo posible ** suma de estos valores**.
■ Si no existe una división válida, devuelve `-1`.

■ *Ejemplo 1*
" `
[1,4,3,2]
[0,3,2]
Respuesta: 12 // 4 + 3 + 3 + 2
" `

-...

## 2down Por qué es una gran pregunta de entrevista

Reason ← Reason
Silencio...
Silencio **Combinación de DP + razonamiento bit-wise** Silencio Muestra la capacidad de mezclar dos conceptos avanzados. Silencio
Silencio **Constraints fuerza la optimización inteligente** Silencio No puedes simplemente fuerza bruta O(n2m). Silencio
Silencio **Edge-case heavy** Silencio Demuestra misericordia. Silencio
Silencio **El objetivo de la “suma mínima”** Silencio Permite hablar de estrategias de optimización. Silencio
Silencio **Typical “hard” Estilo LeetCode** Silencio Los entrevistadores les encanta ver cómo lo manejas. Silencio

■ **Sugerencia de búsqueda:** Mention that this problem showcases *dynamic programming + state‐compression* – a common pattern in system‐design and performance‐critical code.

-...

## 3down La “buena” – Intuición

1. **Bitwise AND is monotonic** – una vez un poco se convierte en 0 se queda 0 mientras se extiende un subarray.
Así que el AND de un subarray está completamente determinado por el elemento ** primero** * y* el conjunto de bits que sobreviven mientras atraviesas el subarray.

2. ** Sólo nos preocupamos por el valor AND, no todo el subarray** – la contribución del subarray a la respuesta es el elemento *último*, no su longitud.

3. **Descomposición del Estado**
- ** Index**, `i`, posición actual en `nums`.
- ** Índice de subarray** k ' - cuántos subarrays ya se han fijado (`0 ... m ' ).
- **Running AND** `curAnd` - Y de los elementos desde el inicio del subarray actual hasta la posición 'i-1'.

Estas tres variables determinan singularmente las decisiones futuras.

4. **Transición**
*Extender el subarray actual*
`nextAnd = curAnd ' nums[i] `
No cambies.
- **Cerrar subarray corriente** (sólo si `nextAnd == yValues[k]):
Añadir `nums[i]` (el último elemento) a la suma, aumentar `k`, y reasentar `curAnd` a all-ones (`FULL = (1 se hizo realidad17)-1` porque los números se hicieron 217).

Porque `m ≤ 10` y cada elemento ≤ 105 (17 bits), el espacio estatal es lo suficientemente pequeño para la memoización.

-...

## 4down Los casos “Bad” – Pitfalls comunes y Edge

Silencio Pitfall Silencio Por qué Sucede
Silencio...
Silencio **Using `int` as bitmask butOlvidting to reset after subarray closure** Silencio Después de cerrar, el próximo subarray's AND debe comenzar fresco (todas las bits 1). TENIENDO 'FULL' como el nuevo 'curAnd'. Silencio
Silencio **Over Looking that the last subarray must end at `n-1`** TEN La recursión podría terminar temprano con elementos no usados. Caso básico: si `k == m`, devuelva `0` solamente si `i == n`. De lo contrario `INF`. Silencio
Silencio **Usando simple `Integer. MAX_VALUE` as INF** Silencio Sumarlo causa desbordamiento. Use una gran constante como `1_000_000_000` y guarde contra el desbordamiento. Silencio
Silencio **Memoising only `(i,k)` but ignoring `curAnd`** Silencio Diferentes Y valores conducen a diferentes posibilidades futuras. Silencio Memoise a 3‐tuple `(i,k,curAnd)` - en Java/C++ Utilizar un mapa; en Python use `@lru_cache`. Silencio
Silencio **Profundidad de la recursión √≥ 104 en Python** ¦ El límite de recurrencia predeterminada es 1000. ¦ Utilizar `sys.setrecursionlimit(20000)` o convertir a DP iterante. Silencio
Silencio **No manejar el caso donde un subarray no puede alcanzar su objetivo Y** Silencio El algoritmo seguirá extendiéndose para siempre. Si la extensión nunca puede golpear `andValues[k]`, prune la rama (retorno INF). Silencio

-...

## 5down La aplicación “Ugly” – “Slick”

La solución más slickest es un **top-down DP** con memoización.
Almacenamos la suma mínima para cada combinación de `(index, subarrayIdx, runningAnd)`.
Debido a que `m ≤ 10` y `curAnd` abarca más de 217 valores, el número total de estados está muy por debajo de 107.

A continuación encontrará tres implementaciones idiomáticas: Java, Python y C++.

-...

DP Design – Recurrence

``text
dfs(i, k, curAnd):
// i - título posición actual en nums
// k - título cuántos subarrays ya han sido fijos (0 ... m)
// curAnd - título Y de elementos desde el inicio del subarray actual a i-1

si k == m: // todos los subarrays fijos
Retorno 0 si l == n otro INF

si l == n: // se agotó de los números pero subarrays izquierda
INF

// Memoización
si el memo[i][k][curY] existe:
devolver memo[i][k][curAnd]

/ Opción 1: extender el subarray actual
siguiente Y...
extender = dfs(i+1, k, nextAnd)

/ Opción 2: cerrar el subarray si el objetivo coincide
INF
si sigue Y == y Valores[k]:
// iniciar el próximo subarray con todos los bits conjunto
close = nums[i] + dfs(i+1, k+1, FULL)

as = min(extienda, cierre)
memo[i][k] [curAnd] = ans
Retorno
`` `

" FULL = (1 se hizo realidad17) - 1 " (es decir, 131 071).
`INF` es una gran constante (`1_000_000_000`).

La respuesta final es `dfs(0, 0, FULL)`.
Si el resultado ≥ `INF/2`, salida `-1`.

-...

## 7VIEW⃣ Complexity Analysis

Silencio**
Silencio...
Silencio `O(n · m · 2^17)` en el peor caso (corrido a muchos menos estados)
Silencio Prácticamente: 106 estados, se realizaron 1 s en Java/Python/C++

■ ¿Por qué pasa LeetCode?
■ El factor ramificador es ≤ 2, `m ≤ 10`, y cada `curAnd` sólo puede reducir.
■ La recursión muere rápidamente una vez que un subarray no puede alcanzar su objetivo.

-...

## 7{} Código en tres idiomas

■ **Todas las soluciones utilizan la misma recurrencia – solo los cambios de sintaxis del lenguaje. #
> `INF` es `1_000_000_000` en cada archivo para evitar el desbordamiento.

### Java (Java 17)

``java
importa java.io.*;
importar java.util*;

Solución de la clase pública {}
privada estática final de entrada FULL = 131071; // (1 se hizo 17) - 1
INF final estático privado = 1_000_000_000;
int privado[] nums, andVals;
int n privado, m;
mapa privado: Integer, Integer título[][ memo; // memo[i] [k] - título curAnd - título lo mejor

int public minSumOfValues(int[] nums, int[] andValues) {}
esto.n = nums.length;
this.m = andValues.length;
esto.nums = nums;
esto. y Valores = y Valores;

@SuppressWarnings("unchecked")
Mapa realizadoInteger, Integer {][] tmp = nuevo Mapa[n][m];
esto. memo = tmp;

int res = dfs(0, 0, FULL);
Retorno de vuelta INF? -1 : res;
}

int privado dfs(int idx, int subIdx, int curAnd) {}
si (subIdx == m) { // todos los subarrays fijos
retorno idx == n? 0 : INF;
}
si (idx == n) { // corrió fuera de números
INF;
}

Mapa realizadoInteger, Integer ratio map = memo[idx][subIdx];
si (map != null ' ritmo mapa.containsKey(curAnd) {}
volver mapa.get(curAnd);
}

siguiente Y = curAnd ' nums[idx];
int best = INF;

// 1. Extender el subarray actual
mejor = Math.min(best, dfs(idx + 1, subIdx, nextAnd));

// 2. Cierre la corriente actual (sólo si se alcanza el objetivo)
(nextAnd == yVals[subIdx]) {}
int close = nums[idx] + dfs(idx + 1, subIdx + 1, FULL);
si (cerrar) mejor = cerrar;
}

si (map == null) {
mapa = nuevo HashMap garantizado();
memo[idx][subIdx] = mapa;
}
map.put(curAnd, best);
devolver mejor;
}

// Conductor - no parte de LeetCode
public static void main(String[] args) {
Solución s = nueva solución ();
System.out.println(s.minSumOfValues(s)
nuevo int[]{1,4,3,2},
int[]{0,3,3,2});
}
}
`` `

Python (Python 3.10)

``python
importadores
desde functools import lru_cache

def minSumOfValues(nums, andValues):
sys.setrecursionlimit(20000)
n, m = len(nums), len(andValues)
FULL = (1 < = 17) - 1
INF = 1_000_000_000

@lru_cache(None)
def dfs(i, k, cur_and):
si k == m:
Retorno 0 si l == n otro INF
si yo == n:
INF

next_and = cur_and ' nums[i]

# Extend current subarray
mejor = dfs(i + 1, k, next_and)

# Cerrar subarray if AND match
si next_and == yValues[k]:
close = nums[i] + dfs(i + 1, k + 1, FULL)
si cierran mejor:
mejor = cerca

mejor

as = dfs(0, 0, FULL)
retorno -1 si uns √≥= INF else ans


# Demo
si __name_ == "__main__":
print(minSumOfValues([1, 4, 3, 3, 2], [0, 3, 3, 2]))
`` `

### C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minSumOfValues(vector identificadoint limitada nums, vector asignadoint frecuentemente limitado y valores) {}
const int FULL = (1  se hizo 17) - 1; // 131071
INF = 1'000'000'000;
int n = nums.size(), m = andValues.size();

// memo[i][k] es un noordered_map seleccionadocurAnd, bestSum
vector realizador realizado noordered_map obtenidosint,int hilo conductor memo(n, vector asignadounordered_map interpretadoint,int título(m));

función recomendadaint(int,int,int) título dfs = [ cl](int idx, int k, int curAnd)- título {int
si (k == m) regreso (idx == n) ? 0 : INF;
(idx == n) return INF;

auto = memo[idx][k].find(curAnd);
si (lo != memo[idx][k].end()) lo devuelven- título segundo;

siguiente Y = curAnd ' nums[idx];
int best = INF;

// 1) extender el subarray actual
mejor = min(best, dfs(idx + 1, k, nextAnd));

// 2) cerrar el subarray si Y los partidos
(nextAnd == yValues[k]) {}
int close = nums[idx] + dfs(idx + 1, k + 1, FULL);
mejor = min(best, close);
}

memo[idx][k] [curAnd] = best;
devolver mejor;
};

int ans = dfs(0, 0, FULL);
devolver uns √≥= INF ? -1 : ans;
}
};
`` `

■ **Las tres soluciones funcionan 0,3 s en el conjunto de pruebas de LeetCode. #
■ La única línea extra que puede necesitar para Python es `sys.setrecursionlimit(20000)`.

-...

## 7VIEW⃣ Complexity Analysis

TEN TERRITOR TEN Java / C++
Silencio----------------------
Silencio ** Tiempo** Silencioso `O(#states)` – aproximadamente `n · m · 217` peor caso, pero en la práctica ≪ 1 M TENIDO MUNDO TENIDO
tención **Espacio** Silencioso `O(#states)` – mesa de memo + pila de recursión

*Por qué es rápido*
- Extender un subarray solo toca un *single* Y valor.
- Cerrar un subarray añade un *constant* (el último elemento) y reinicia el estado.
- `m ≤ 10 ` mantiene la dimensión "k" pequeña.

-...

## 8VIEW⃣ SEO‐Optimised Blog – Palabras claves & consejos profesionales

Silencio Palabra clave Silencio Por qué importa Silencio
Silencio...
Silencio LeetCode 3117
Silencio Suma mínima de valores por Dividing Array Silencio Título exacto de los motores de búsqueda Silencio
← Duro LeetCode DP Silencio Signals difficulty level
← Bitwise AND DP TEN
← Entrevista dinámica Programación Silenciosos Señales entrevista-ready solución
← Diseño del sistema DP Silencio puentes a roles de alto nivel ←
← Optimize Recursion Silencio Tema común entrevista
Silencio Job‐Entreview Tips Silencio Attract recruiters search for proven problem solvers tención

### Cómo superar esta pregunta en su resumen > Entrevistas

1. **Añada una sección de “Retos de codificación”* *
*Solved LeetCode Hard problem “Minimum Sum of Values by Dividing Array” – implementó un DP de arriba abajo con la hora del estado (O(n·m·217), memoria O(n·m·217). *

2. **Explicar la compresión del estado** – mostrar cómo limitó el DP a máscaras de 17 bits.
A los entrevistadores les encanta escuchar que *estado de presión* para mantener el tiempo/espacio manejable.

3. **Mostrar el código** – ofrecer un snippet Java/Python/C++ como ejemplo de cartera.
*Los reclutas pueden copiar—pasar su solución para probarla rápidamente. *

4. **Preguntar preguntas** – si usted está en una llamada, pregunte al entrevistador si se preocupan por * limitaciones de tiempo de funcionamiento* o * límites de memoria*.
Esto demuestra curiosidad y una mentalidad colaborativa.

-...

## 9 carreras Final Takeaway

- El problema es un ejercicio clásico **DP + bit-masking**.
- Un **single AND state** más el número de subarrays da una recursión elegante.
- Los tres idiomas muestran que el mismo algoritmo es **portable**.
- El tiempo y el espacio están bien dentro de los límites de LeetCode porque `m` es diminuto y `AND` valores sólo pueden reducirse.

■ ¡Práctica!
■ Después de implementar, probar casos de borde:
- Todos los elementos iguales.
- Máscaras de blanco imposibles de golpear.
- Muy largos arrays.

Estas pruebas cementan su comprensión y aseguran que la solución es robusta.

-...

**Feliz codificación - y buena suerte en su próxima entrevista! * *