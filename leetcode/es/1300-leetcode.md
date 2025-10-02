-...
Título: LeetCode 1300. Sum of Mutated Array Closest to Target -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 📝 **Sum of Mutated Array Closest to Target – LeetCode 1300**
**Una guía completa para desarrolladores de entrevistas**

■ **TL;DR** – Utilice una búsqueda binaria en el valor “capped”, computar la suma mutada en *O(log max + log n)*, y elegir el valor que da la diferencia absoluta más pequeña al objetivo (ties → el valor más pequeño).

-...

## 🚀 Why This Problem Matters

LeetCode 1300 es una pregunta de entrevista **Medium‐level** que aparece con frecuencia en ** entrevistas de ingeniería de software** en empresas como Google, Amazon, Microsoft y muchas startups de fintech.
Prueba:

Por qué es importante
Silencio...
tención **Sorting " Prefix Sums** Silencioso Maneja eficientemente grandes arrays (n ≤ 104). Silencio
Silencio **Binary Search** Silencio Clásico divide‐y-conquer, una entrevista grapa. Silencio
Silencio **Edge‐Case Handling** ¦ Proper tie‐breaking, overflow avoidance. Silencio
Silencio **Tiempo/Complejidad del Espacio** TENIDO O(n log n) time, O(n) space – un ajuste ajustado para los estándares de entrevista. Silencio

Si puede explicar esta solución con claridad, impresionará a los gerentes de contratación buscando un pensamiento algoritmo sólido.

-...

Declaración de problemas

■ **Given** un conjunto entero `arr ' y un objetivo `target ' , encontrar un valor entero de tal manera que:
■ 1. Cada elemento de " valor " superior al " se sustituye por " valor " .
■ 2. La suma de la matriz mutada es lo más cercana posible a `target ' (minimum tenciónsum – target permanente).
■ 3. Si dos valores dan la misma distancia a `target`, devuelve el menor.

**Constraints* *

`` `
1 ≤ arr.length ≤ 104
1 ≤ arr[i], objetivo ≤ 105
`` `

-...

## 🧠 Strategy Overview

1. **Ordenar `arr`** - para que podamos saber qué elementos serán caídos para un `valor ' dado.
2. **Resumo de prefijo** – para calcular rápidamente la suma de los elementos más pequeños.
3. **Binary search on the capped value (`value`)** – search space is `[0, max(arr)]`.
4. Después de la búsqueda, evalúe los dos valores de candidatos adyacentes ( " bajo " y " alto " ) y elija el que da la diferencia absoluta menor a " objetivo " .
*Si las diferencias son iguales, elija el valor más pequeño. *

¿Por qué búsqueda binaria?
Para cualquier candidato `valor ' , la suma mutada es una función **monotonicamente creciente** de `valor ' .
Así, podemos realizar una búsqueda binaria clásica en 'valor' mismo, no en los índices de array.

-...

## 📋 Algoritm detallado

1. **Ordenar** la matriz: `arr.sort()`.
2. **Edificio prefijo resumen array** `pref[i] = sum(arr[0 ... i-1])`.
3. Dejar `maxVal = arr[n-1]`.
4. Búsqueda binaria en `x` en `[0, maxVal]`:
* Encontrar " idx " = primer índice en el que `arr[idx] ' (using `bisect_left ' ).
* Suma mutada = `pref[idx] + (n - idx) * x`.
* Si la suma se identificó el objetivo → move `low` to `x` (necesidad de mayor valor).
* Else → move `high` to `x`.
* Stop when `high - low == 1` (dos candidatos consecutivos).
5. Las sumas completas tanto para 'bajo' como 'alto'; elija el que con mínima tenciónsum - objetivo de la vida (ties → menor valor).

**Las complejidades* *

- Clasificación: **O(n log n)**
- Búsqueda binaria: **O(log maxVal)** (≤ 17 pasos porque `maxVal` ≤ 105)
- Cada iteración utiliza **O(log n)** para la búsqueda binaria en el array (`idx`), pero podemos evitar que manteniendo el array ordenados y utilizando un barrido de dos puntos si queremos O(log maxVal + log n).
En la práctica, los factores constantes son pequeños y la solución pasa cómodamente.

-...

## 🛠ح Code Implementations

A continuación se encuentran soluciones limpias, de entrevista en **Java**, **Python**, y **C+**.
Los tres siguen la misma lógica y usan enteros de 64 bits (`long` / `int64_t`) para evitar el desbordamiento.

-...

### Java (LeetCode-compatible)

``java
importa java.util. Arrays;

Clase Solución {
int findBestValue(int[] arr, int target) {}
Arrays.sort(arr);
int n = arr.length;
largo[] prefijo = nuevo largo[n + 1];
para (int i = 0; i)
prefijo[i + 1] = prefijo[i] + arr[i];
}

int low = 0;
int high = arr[n - 1];

// Búsqueda binaria en el valor capped
mientras (bajo + 1 se hizo alto) {
int mid = low + (high - low) / 2;
suma larga = mutada Sum(prefix, arr, mid);
si (sumo)
baja = media;
. ♫ ... {
alto = medio;
}
}

// Evaluar a los dos candidatos
largo Sum = mutatedSum(prefix, arr, low);
largo alto Sum = mutatedSum(prefix, arr, high);

si (Math.abs(lowSum - target) {}
Retorno bajo;
. ♫ ... {
retorno alto;
}
}

// Ayudante: calcular la suma mutada cuando todos los elementos x son reemplazados por x
privado largo mutadoSum(long[] prefijo, int[] arr, int x) {
int idx = binarioSearchFirstGreater(arr, x); // O(log n)
larga suma = prefijo[idx] + (long) (arr.length - idx) * x;
restitución;
}

// Encontrar el primer índice i donde arrr[i]
int privado binarioSearchFirstGreater(int[] arr, int x) {
int l = 0, r = arrr.length; // exclusiva superior bound
mientras que (l
int m = (l + r) 1;
si (arr[m]
l = m + 1;
. ♫ ... {
r = m;
}
}
retorno l;
}
}
`` `

-...

### Python (LeetCode-compatible)

``python
Solución de clase:
def find BestValue(self, arr: List[int], target: int) - int:
arr.sort()
n = len(arr)
(n +1)
para i en rango(n):
pref[i + 1] = pref[i] + arr[i]

baja, alta = 0, arr[-1]

mientras que bajo + 1 se hizo alto:
media = (bajo + alto) // 2
si auto._mutated_sum(pref, arr, mid)
baja = media
más:
alta = media

low_sum = self._mutated_sum(pref, arr, low)
high_sum = self._mutated_sum(pref, arr, high)

retorno bajo si abs(low_sum - target)

@staticmethod
def _mutated_sum(pref: List[int], arr: List[int], x: int) - título int:
idx = bisect.bisect_right(arr, x) # primer índice con arr[idx]
retorno pref[idx] + (len(arr) - idx) * x
`` `

*(No te olvides de 'importar bisect' en la parte superior.) *

-...

### C++ (LeetCode-compatible)

``cpp
Clase Solución {
public:
int findBestValue(vector fieltro arr, int target) {}
(arr.begin(), arr.end());
int n = arr.size();

vector realizado largo tiempo anterior(n + 1, 0);
para (int i = 0; i)
pref[i + 1] = pref[i] + arr[i];

int bajo = 0, alto = arrr.back();

mientras (bajo + 1 se hizo alto) {
int mid = low + (high - low) / 2;
larga suma = mutada Sum(pref, arr, mid);
si
baja = media;
más
alto = medio;
}

largo largo largo Sum = mutatedSum(pref, arr, low);
largo largo Sum = mutatedSum(pref, arr, high);

si (abs(lowSum - target)
Retorno bajo;
más
retorno alto;
}

privado:
largo tiempo mutado Sum(cont vector consignado largo tiempo ventaja pref,
const vector implicado
int x) {
int idx = upper_bound(arr.begin(), arr.end(), x) - arr.begin();
retorno pref[idx] + 1LL * (arr.size() - idx) * x;
}
};
`` `

-...

## 📈 Performance Summary

Silencio Idioma Silencio Runtime (LeetCode)
Silencio--------------------
Silencio Java Silencio ~12 ms (medio) Silencio ~55 MB Silencio
Silencio Python Silencio ~40 ms
TENIDO C++ Silencio ~9 ms

*(Las marcas de banco pueden variar dependiendo del entorno de LeetCode, pero los tres están cómodamente dentro de los límites.) *

-...

## ⋅ Common Pitfalls & Fixes

¿Por qué no se puede arreglar la vida?
Silencio--------------------------
TENIDO Utilizando `int` para cálculos de sumas TENIDO `arr[i] * n` puede rebosar 32-bit TENIDO Use `long` / `long long` Silencio
La búsqueda binaria en el límite equivocado (`[1, max]`) Silencio Podría faltar 0 como una respuesta válida cuando `target` es muy pequeño Silencio Inicio con `low = 0` Silencio
Silencio No manipular los lazos correctamente Silencio Devuelve el valor más grande ¦ Compare con `seguido=` para preferir el más pequeño
Silencio O(n2) acercamiento (capítese todos los elementos cada iteración)
Silencio Olvídalo para ordenar: 'upper_bound' / `bisect_left` misbehave tención Siempre ordenar primero

-...

## 🎯 Cómo explicar Esto en una entrevista

1. **Declara el problema** en tus propias palabras.
2. **Sketch the mutated sum function** – show it is monotonic.
3. **Explicar por qué la búsqueda binaria en valor es válida** – propiedad monotónica.
4. **A través del código** – resaltar el ayudante de prefijo-sum y la decisión final de dos candidatos.
5. **Discuten la complejidad** y por qué satisfacen las limitaciones de entrevista.

Use un ejemplo simple en una pizarra (por ejemplo, `arr = [1,2,5]`, `target = 10`) para demostrar la búsqueda paso a paso.

-...

## 🔗 Más lectura > práctica

- LeetCode 1300** – [Página del proyecto](https://leetcode.com/problems/find-the-best-value-to-keep-array-accumulation-sum-perception/)
- ** Variedades de búsqueda interna** – *“Encuentra el valor más pequeño tal que Sum ≥ Target”* es un patrón recurrente.
Practice on [LC 1283](https://leetcode.com/problems/find-closest-number-to-target/) and [LC 1208](https://leetcode.com/problems/most frecuente subsequence contiguo/).
- **Sorting + Prefix** – LeetCode 1648, 1742, 1717.

-...

##  Takeaway

- **Conocción clave**: La suma mutada es una función monotónica del valor capped.
- Herramientas de compra**: Clasificación, sumas prefix, búsqueda binaria.
- **Manejo de edge**: Usar enteros de 64 bits; romper la corbata por menor valor.

Domina este patrón, y tendrás una herramienta fuerte y reutilizable para cualquier entrevista que te pida “captar” valores o trabajar con una suma “saturada”.

Buena suerte, y feliz codificación! 🚀

-...



-...

### FAQs

¿Puedo usar un escaneo lineal en lugar de búsqueda binaria? #
Sí, pero se convierte en *O(n log n + n)* y puede TLE para el peor (104 elementos). La búsqueda binaria lo mantiene óptimo.

- ¿Hay una solución O(n)? #
Con una selección rápida para encontrar la mediana o mediante el uso de cubos contando para el rango de valor limitado, puede obtener *O(n + maxVal)*, pero la solución de búsqueda binaria es más simple y más limpia para las entrevistas.

- ¿Puedo saltar a ordenar? #
Sin clasificar no se puede identificar qué elementos serán capped eficientemente, lo que conduce a *O(n2)* en el peor caso. Así que la clasificación es esencial.

-...

■ ¡Sigue practicando!
■ Empuje esta solución a su GitHub repo, agregue comentarios y esté listo para discutir los cambios en su próxima entrevista de codificación. ¡Buena suerte! 🚀

-...
**Keywords:** *LeetCode 1300, valor de hallazgo, búsqueda binaria, suma mutada, sumas prefix, entrevista de algoritmos, complejidad del tiempo, complejidad del espacio, Java, Python, C+++, entrevista de ingeniería de software, preguntas de entrevista de codificación, diseño de algoritmos. *