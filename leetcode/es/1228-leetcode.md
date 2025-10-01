-...
Título: LeetCode 1228. Número perdido en la progresión aritmética -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Missing Number in Arithmetic Progression – LeetCode 1228
**Java, Python & C++ + guía de entrevistas**

-...

## 1. Introducción

■ **LeetCode 1228 – “Missing Number in Arithmetic Progression”**
■ * Un solo número fue eliminado de una progresión aritmética que aumenta o disminuye estrictamente (AP). Encuentra el elemento que falta. *

El problema es una pregunta de entrevista clásica que prueba su comprensión de las secuencias aritméticas, el manejo de los bordes y la lógica de tiempo constante. Dominarlo le da una solución limpia para mostrar en su currículum, una respuesta sólida para entrevistas técnicas, y la confianza al abordar problemas más difíciles de “rellenar trucos”.

-...

## 2. Declaración de problemas

``text
Dado un árrr de matriz entero que contiene todos los elementos de una progresión aritmética estrictamente monotónica de longitud n+1
excepto un elemento que fue eliminado (no el primer o último elemento), encontrar el número perdido.

Devuelve el número perdido.
`` `

Silencioso Campo Silencio Descripción
Silencio...
Silencioso `arr` permanente array of size `n` (n ≥ 3)
Silencio `n` duración de la matriz de entrada
tención `n+1` Silencioso tamaño original de la AP antes de la eliminación

■ *Examples*
[5, 7, 11, 13] Producto " 9 "
[15, 13, 12] → salida `14`

-...

## 3. Limitaciones

Silencio Parameter Silencio Mínimo Silencio Máximo Silencio
Silencio----------------------------------------------------
Silencio `n` Silencio 3 Silencio 105 Silencio El tamaño de la entrada puede ser grande; O(n) es necesario. Silencio
Silencio `arr[i]` Silencio -109 Silencio 109 Silencio 32‐bit integers signed. Silencio
Silencio La progresión es **strictamente monotónica** (aumento o disminución). Silencio
Silencio El elemento perdido es **nunca el primero o el último** de la secuencia original. Silencio

-...

## 4. Comprender el problema

Una progresión aritmética (AP) tiene una diferencia constante `d`.
Si eliminamos un elemento de una progresión de longitud `k+1`, el array resultante tiene elementos 'k', y **exactamente un par adyacente tendrá una brecha de `2·d`** – el lugar donde ocurrió la eliminación.

*¿Por qué sólo uno de esos pares? *
Debido a que cada otro par adyacente en el array restante sigue siendo consecutivo en el AP original y por lo tanto difiere por exactamente `d`.

La tarea se reduce a:
1. ** Determinar la verdadera diferencia `d`.**
En una matriz de ≥ 4 elementos, podemos observar las tres primeras diferencias y elegir la que aparece al menos dos veces.
2. **Situar el par anómalo** donde la diferencia es `2·d` y calcular el número perdido como `previous + d`.

Casos de borde:
- **`n = 3`** - la regla de la “mayoridad” no se puede aplicar porque sólo tenemos dos diferencias. La diferencia de menor magnitud es la real `d`.
- ** Negativo `d`** - el AP puede estar disminuyendo; el algoritmo maneja signos naturalmente.

-...

## 5. Tiempo aproximado (o n), espacio O 1)

1. **Computar las tres primeras diferencias** ( " diff1 " , " diff3 " ).
2. **Identificar la diferencia correcta `d`**:
* If `diff1 == diff2` or `diff1 == diff3` → `d = diff1`; otherwise `d = diff2`.*
3. **Scan una vez** desde el segundo elemento hasta el segundo punto:
*Cuando `arr[i] - arr[i-1]!= d`, el número perdido es `arr[i-1] + d`.
El bucle termina inmediatamente – no es necesario comprobar el último elemento porque el elemento perdido no puede estar en los extremos del array. *
4. **Caso especial `n = 3`**:
*Las dos diferencias disponibles dan `d` como la que tiene un valor absoluto más pequeño.
Si la primera diferencia es igual a `2·d`, el número perdido se encuentra después del primer elemento; de lo contrario se encuentra después del segundo. *

El algoritmo nunca modifica el array de entrada y se ejecuta en un solo pase lineal.

-...

## 6. Aplicación

A continuación se muestran las implementaciones limpias, entrevistadas en **Java, Python, y C++**.

-...

### 6.1 Java

``java
importar java.util*;

Clase Solución {
public int missingNumber(int[] arr) {
int n = arr.length;
(n == 3) {
int diff1 = arrr[1] - arr[0];
int diff2 = arr[2] - arr[1];
int d = Math.abs(diff1) diff1 : diff2;
si (diff1 == 2 * d) {}
retorno arr[0] + d; // desaparecido después de arr[0]
. ♫ ... {
retorno arrr[1] + d; // desaparecido después de arr[1]
}
}

int diff1 = arrr[1] - arr[0];
int diff2 = arr[2] - arr[1];
int diff3 = arr[3] - arr[2];

int d = (diff1 == diff2 tención eterna diff1 == diff3) ? diff1 : diff2;

para (int i = 1; i)
si (arr[i] - arr[i - 1] != d) {}
retorno arr[i - 1] + d;
}
}
regreso -1; // nunca debe llegar aquí
}
}
`` `

-...

### 6.2 Python

``python
de la importación Lista

Solución de clase:
def missingNumber(self, arr: List[int] int:
n = len(arr)
si n == 3:
diff1 = arr[1] - arrr[0]
diff2 = arr[2] - arr[1]
d = diff1 si abs(diff1)
arrr[0] + d if diff1 == 2 * d) arr[1] + d

diff1 = arr[1] - arrr[0]
diff2 = arr[2] - arr[1]
diff3 = arr[3] - arrr[2]
d = diff1 si diff1 == diff2 o diff1 == Diff3 más diff2

para i en rango(1, n - 1):
si arr[i] - arr[i - 1] != d:
retorno arr[i - 1] + d
regreso -1 # nunca alcanzado
`` `

-...

### 6.3 C++

``cpp
Incluido el título
#include >

Clase Solución {
public:
int missingNumber(std::vector identificadoint
int n = arr.size();
(n == 3) {
int diff1 = arrr[1] - arr[0];
int diff2 = arr[2] - arr[1];
int d = std::abs(diff1)
si (diff1 == 2 * d) retorno arr[0] + d;
arrr[1] + d;
}

int diff1 = arrr[1] - arr[0];
int diff2 = arr[2] - arr[1];
int diff3 = arr[3] - arr[2];
int d = (diff1 == diff2 tención eterna diff1 == diff3) ? diff1 : diff2;

para (int i = 1; i) {}
si (arr[i] - arrr[i - 1] != d) retorno arr[i - 1] + d;
}
retorno -1; //
}
};
`` `

-...

## 7. Alternativa (Brute‐Force) – ¿por qué no?

Una solución ingenua intenta cada número posible entre `arr[0]` y `arr[n-1]` y comprueba si se ajusta a un AP.
Es **O(n2)** y TLE en grandes entradas. Es útil para la práctica, pero **nunca** para la producción o una entrevista.

-...

## 8. Test‐Driven Edge Cases

← Input Silencio Esperado Silencio Por qué funciona
Silencio------------------------
Silencio `[1, 4, 7, 10]` Silencio `13` Silencio d = 3; brecha después del último elemento, pero la regla garantiza que lo atraparemos antes del final. Silencio
Silencio `[10, 8, 6, 4]` Silencio `2` Silencio Disminuir AP; d = ‐2, par anómalo es `10–4 = 6` (2·d). Silencio
Silencio `[5, 15, 25]` Silencio `10` Silencio Incrementando AP con d = 10; el par medio es 10. Silencio
Silencio `[2, 1, 0]` Silencio `-1` Silencio Disminuir AP con d = ‐1; desaparecido después del primer elemento. Silencio
Silencio `[3, 3]` Silencio *inválido* Silencio La longitud de la matriz debe ser ≥ 3 (problema garantiza esto). Silencio

-...

## 9. Why This Solution Rocks for Interviews

1. **Zero‐memory** – Constante espacio extra.
2. **Escaneo de sonido** – Tiempo lineal, que coincide con la complejidad necesaria.
3. **Dispone de APs cada vez mayores* Se conserva la señal de `d`.
4. **Lógica absoluta** – Usted puede explicar “diferencia de la mayoría” y “diferencia anómala” en unas pocas oraciones.
5. **Extensible** – El mismo patrón resuelve “encontrar el segundo elemento que falta” o “encontrar el índice que falta en un árbol de búsqueda binaria” con leves pinzas.

-...

## 10. Variaciones " Extensiones

Silencioso Variación Silencioso Cómo adaptarse
Silencio--------------
Silencio **Encontrar dos números desaparecidos** Silencio Dos brechas serán `2·d` y `3·d`. Detecta ambos y computa los dos elementos perdidos. Silencio
Silencio **Progresión no monotónica** Silencio Computar la diferencia media `d = (arr[-1] - arr[0]) / n` (división entero). Luego proceder con el escaneo. Silencio
Silencio **Large integers (64-bit)** Silencio Use `long` en Java/C++ o `int` en Python (la int de Python no está abundada). Silencio

-...

## 11. Pensamientos finales

*Missing Number in Arithmetic Progression* es un problema engañosamente sencillo que esconde un patrón sutil.
Dominar este patrón:
- Construye una base sólida** para resolver problemas de “gap” (por ejemplo, falta de subsequencia, elemento faltante en un array ordenados).
- Demuestra claridad algorítmica a los gerentes de contratación.
- Te da un snippet reutilizable para cualquier entrevista que implique secuencias aritméticas o escaneos de tiempo lineal.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀