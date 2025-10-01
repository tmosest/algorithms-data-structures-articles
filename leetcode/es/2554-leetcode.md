-...
Título: LeetCode 2554. Número máximo de enteros a elegir de un rango Yo...
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## LeetCode 2554 – ** Número máximo de números enteros a elegir de un rango I**
### The Good, The Bad, and The Ugly – A Job‐Ready Guide

Silencio Sección Silencioso Descripción
Silencio...
Silencio **Problema** Silencio Dada una lista de enteros *bloqueados*, un valor máximo `n`, y un presupuesto `maxSum`, elige el mayor número posible de enteros distintos de la gama `[1, n]` que son **no** prohibidos y cuya suma total no excede `maxSum`. Silencio
TEN **Audiencia de emergencia** TENIDO Ingenieros de Front-end / back-end, candidatos de entrevista de algoritmos, y cualquiera que busque una entrevista de codificación de estilo LeetCode. Silencio
Silencio **Core Concepts** ¦ Greedy, boolean array / hash‐set, time‐space trade‐off. Silencio
Silencio **Idiomas** viv Java, Python, C++ (disponibles de código). Silencio

■ **SEO Palabras clave**: LeetCode 2554, Maximum Number of Integers to Choose From a Range, array solution, Java, Python, C++, algoritmo codicioso, prep de entrevista, entrevista de codificación, pensamiento algoritmo, consejos de entrevista de trabajo.

-...

### 1. Reposición de problemas

Se te da:
- `int[] prohibida` - una lista de números que no puede elegir.
- `int n` - el límite superior del rango `[1, n]`.
- `in maxSum` - la suma máxima que se le permite acumular.

Devuelve el **conteo máximo** de números enteros distintos que puedes elegir que satisface:
- Cada número elegido latitud[1, n].
- Cada número elegido es *no* en `banned`.
- La suma de números elegidos ≤ `maxSum`.

-...

### 2. Intuición

La estrategia óptima es *verde*:
Elige primero los números permitidos más pequeños.
¿Por qué?
- Los números más pequeños consumen lo menos del presupuesto, lo que le permite añadir más números antes de golpear `maxSum`.
- Ya que cada número se puede tomar a la mayor parte de una vez, no hay ventaja de saltar un pequeño número a favor de uno más grande.

Así podemos:
1. Marca todos los números prohibidos.
2. Iterate from `1` to `n` in increasing order, skipping banned numbers.
3. Mantenga una suma en ejecución; deténgase tan pronto como añada el siguiente número excedería `maxSum`.

-...

### 3. Casos de borde

Silenciosos en la situación
Silencio...
Silencio Todos los números están prohibidos.
Silencio `maxSum` es más pequeño que el menor número permitido. Silencio
Silencioso `maxSum` es enorme (por ejemplo, `10^9`) y `n` es pequeño. Todos los números permitidos pueden ser tomados. Silencio
Silencio `banned` contiene números fuera de `[1, n]`. Silencio Son irrelevantes. Silencio
Silencio `n` es hasta `10^4`, `banned.length` hasta `10^4`. Aún es tiempo lineal. Silencio

-...

### 4. Análisis de la complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio Marcando números prohibidos Silencioso `O(banned.length)` (n+1`) Silencio
viv Greedy scan Silencioso `O(n)`
Silencio **Total** Silencio **`O(n + banned.length)`** Silencio **`O(n)`** (continuado en relación con las limitaciones, ~104) Silencio

Porque `n` ≤ `104`, una simple matriz booleana es rápida y fácil de razonar. Si `n` fuera más grande (por ejemplo, `109`), cambiaríamos a un conjunto de números prohibidos e iterar sólo sobre los números permitidos, pero eso es innecesario aquí.

-...

### 5. Aplicación del Código

■ **Consejo:** Use `long ' for the running sum to avoid overflow when `maxSum` is close to `109`.

-...

##### 5.1 Java

``java
importar java.util*;

Clase Solución {
public int maxCount(int[] prohibida, int n, int maxSum) {
// Marca números prohibidos en una matriz booleana
booleano[] prohibidoArr = nuevo booleano[n + 1];
para (int num : banned) {
[num] = verdadero;
}

larga suma = 0;
int count = 0;

// Greedy: elija los números más pequeños permitidos
para (int i = 1; i) = n; i++) {
si (bannedArr[i]) continúan; // skip banned
si (sum + i > maxSum) descanso; // presupuesto excedido
suma += i)
contar++;
}
recuento de retorno;
}
}
`` `

-...

#### 5.2 Python

``python
Solución de clase:
def maxCount(self, banned: List[int], n: int, maxSum: int) - título int:
prohibida_set = set(banned) # O(1) look‐ups
sum_val = 0
Conteo = 0

para i en rango(1, n + 1):
si estoy en ban_set:
continuar
si sum_val + i > max Sum:
descanso
sum_val += i
Cuenta += 1
cuenta de retorno
`` `

■ ¿Por qué un `set'?
■ Para `n ≤ 104`, ambos array y conjunto están bien; un conjunto mantiene el código simple y funciona si `n` crece.

-...

#### 5.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxCount(vector fielint implica prohibido, int n, int maxSum) {}
// Números prohibidos
vector asignadobool confianza prohibidaArr(n + 1, false);
para (int x : banned)
si (x.

larga suma = 0;
int count = 0;

para (int i = 1; i) = n; ++i) {}
si (bannedArr[i]) continúan;
si (sum + i > maxSum) se rompen;
suma += i)
++cuenta;
}
recuento de retorno;
}
};
`` `

-...

### 6. “El Bien, el Mal, el Ugly” de este problema

¿Qué es lo que hace que sea?
Silencio--------------------------------------------
tención **La simplicidad** Silencioso Fácil de entender; la prueba avaricia es directa. La redacción del problema puede ser un poco verbosa; usted debe parse cuidadosamente. La solución ingenua podría llegar a todos los números incluso cuando muchos están prohibidos, dando lugar a trabajos innecesarios. Silencio
tención **Scalability** tención El tiempo lineal funciona para las limitaciones dadas (`n ≤ 104`). tención Para mucho más grande `n` necesitará una estructura de datos más inteligente (por ejemplo, árbol de segmento). ← Olvidar usar una suma de 64 bits puede causar flujos sutiles. Silencio
Silencio **Testing** Silencio Un puñado de casos de esquina cubren casi todos los modos de falla. TEN Requiere manejar tanto números prohibidos fuera del rango y presupuestos extremos. Silencio Algunos entrevistadores pueden agregar restricciones ocultas (por ejemplo, múltiples casos de prueba en una sola carrera). Silencio
Silencio **Interview Value** Silencio Demuestra el razonamiento codicioso, la manipulación de conjuntos y rayos, el manejo minucioso de los bordes. No es un problema clásico de DP o grafito; puede ser considerado “demasiado fácil” para los roles mayores. La solución puede ser “demasiado corta” para los entrevistadores que esperan una discusión más profunda (por ejemplo, por qué la codicia es óptima). Silencio

**Takeaway for Interviews:**
Explicar la intuición codicioso, dibujar la prueba de que elegir los números más pequeños disponibles es óptima, y discutir los cambios de tiempo/espacio. Esto demuestra no sólo la habilidad de codificación sino también el pensamiento algorítmico.

-...

### 7. Resumen SEO-Optimizado

■ **LeetCode 2554** – * Número máximo de enteros a elegir de un rango I*
■ Aprende una solución codictiva limpia en **Java, Python, y C++**.
■ Master array vs. hash-set techniques, handle edge cases, and get interview-ready.
■ ¿Listo para tu próxima entrevista de codificación? Practique este problema y agréguelo a su cartera.

-...

##### Quick Reference

``text
Entrada: prohibida = [1,6,5], n = 5, maxSum = 6
Producto: 2 // elegir 2 y 4

Entrada: prohibida = [1,2,3,4,5,6,7], n = 8, maxSum = 1
Producto: 0 // nada cabe

Entrada: prohibida = [11], n = 7, maxSum = 50
Producto: 7 // elegir 1..7, suma=28
`` `

¡Feliz codificación, y buena suerte aterrizando ese trabajo!