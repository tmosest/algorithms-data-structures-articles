-...
Título: LeetCode 1999. Más pequeño Gran Múltiple Hecho de Dos Digitos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🧩 1999. Más pequeño Múltiple Hecho de Dos dígitos
**Problema de LeetCode** – Medium
**SEO Palabras clave:** *Smallest Greater Multiple Made of Two Digits, LeetCode 1999, solución Java BFS, solución Python, solución C++, algoritmo de entrevista, consejos de entrevista de trabajo*

-...

## 🚀 TL;DR

* Dado `k, digit1, digit2`, encontrar el entero más brillante ** que
1. Is **strictly larger** than `k`,
2. Es un *multiple de `k**,
3. Consistas **sólo** de los dos dígitos `digit1` y `digit2`.
* Retorno `-1' si tal número no existe o excede `INT_MAX`.

**Solución** – Breadth‐First Search (BFS) sobre los números construidos de los dos dígitos.
Complejidad: `O(2^len)` donde `len` ≤ 10 (porque `INT_MAX` tiene 10 dígitos).
Memoria: `O(2^len)`.

-...

## 📄 Declaración de problemas (de LeetCode)

``text
Dado tres números enteros, k, digit1, y digit2, usted quiere encontrar el entero más pequeño que es:
1. Más grande que k,
2. Un múltiple de k,
3. Comprised of only the digits digit1 and/or digit2.
Devuelve al más pequeño tan entero. Si no existe tal entero o el entero excede el límite de un entero firmado de 32 bits (2^31-1), retorno -1.
`` `

**Constraints* *

- 1 ≤ ≤ 1000
- 0 ≤ dígito1, dígito2 ≤ 9

-...

## 🛠ר} Core Idea

El espacio de búsqueda es el conjunto de todos los números que se pueden escribir con los dos dígitos permitidos.
Porque queremos que el **smallest** tal número, explorando números en *aumento de longitud* y *ordenléxicográfico* garantiza el primer número válido que encontramos es la respuesta.

¿Por qué BFS? #
* Los números de visitas BFS aumentan la longitud, por lo que el primer partido está garantizado a ser mínimo.
* La longitud máxima que necesitamos explorar es 10 (ya que `2^31‐1` tiene 10 dígitos).
* El factor ramificador es sólo 2 (digit1 o digit2), por lo que el espacio del estado es pequeño (`≤ 2^10 = 1024` nodos).

-...

## 🔧 Implementación (Python, Java, C++)

A continuación se presentan implementaciones limpias y preparadas para cada idioma.
Siéntete libre de copiar-paste en tu IDE o una caja de arena LeetCode.

-...

### Python 3 (BFS)

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def find Integer(self, k: int, digit1: int, digit2: int) int:
si el dígito1 == dígitos2 y dígitos1 == 0:
retorno -1 # sólo ceros - título imposible

# Los dígitos iniciales no pueden ser cero (los ceros liberados son inválidos)
start_digits = []
si digit1 != 0:
start_digits.append(digit1)
si digit2 != 0 y digit2 != dígito1:
start_digits.append(digit2)

q = deque(start_digits)

INT_MAX = 2 ** 31 - 1

mientras q:
q.popleft()
si num > k y num % k == 0:
Retorno num

# Append next digit only if we don't exceed INT_MAX
si num <= INT_MAX // 10:
para d in (digit1, digit2):
nuevo_num = num * 10 + d
si nuevo_num se hizo= INT_MAX:
q.append(new_num)

retorno -1
`` `

-...

## Java (Iterative BFS)

``java
importa java.util. ArrayDeque;
importa java.util. Deque;

Clase Solución {
public int find Integer(int k, int digit1, int digit2) {
// Caso de borde: ambos dígitos son cero
si (digit1 == 0 " componente digit2 == 0) retorno -1;

Deque cumplió la cola de Integer] = nuevo ArrayDeque correspondió();

// cola de semillas con dígitos de inicio no cero
si (digit1!= 0) queue.offer(digit1);
si (digit2 != 0 " límite digit2 != digit1) queue.offer(digit2);

final long INT_MAX = (1L ' hecho 31) - 1; // 2^31 - 1

(!queue.isEmpty()) {}
int cur = queue.poll();

si (curre √≥ k ' curva % k == 0) Cura de retorno;

si (curo 0= INT_MAX / 10) {
// Número de apéndice1
largo siguiente = cur * 10L + dígito1;
si (anexto) = INT_MAX) queue.offer(int) next);

// Apéndice 2 (evitar duplicar cuando los dígitos son iguales)
si (digit2 != digit1) {
siguiente = cur * 10L + dígito2;
si (anexto) = INT_MAX) queue.offer(int) next);
}
}
}
retorno -1;
}
}
`` `

-...

### C++ (BFS alternativo)

``cpp
#include >
#include < > >

Clase Solución {
public:
int find Integer(int k, int digit1, int digit2) {
si (digit1 == 0 " componente digit2 == 0) retorno -1;

std::queue madeint
si (digit1!= 0) q.push(digit1);
si (digit2 != 0 " límite digit2 != digit1) q.push(digit2);

const long long INT_MAX_LL = static_cast obtenidos long {INT_MAX);

(!q.empty()) {
int cur = q.front(); q.pop();

si (curre √≥ k ' curva % k == 0) Cura de retorno;

si (curo 0 = INT_MAX_LL / 10) {
largo siguiente = 1LL * cur * 10 + dígito1;
q.push(static_cast correctamenteint(next));

si (digit2 != digit1) {
siguiente = 1LL * cur * 10 + dígito2;
q.push(static_cast correctamenteint(next));
}
}
}
retorno -1;
}
};
`` `

-...

## 📚 Why This Works – Step‐by‐Step

1. **Empieza con los dígitos no cero más pequeños. #
Cualquier número válido no puede comenzar con `0`.
Por lo tanto, sembramos la cola BFS con los dos dígitos permitidos si no son cero.

2. **Primera Exploración. #
*Queue* → pop → check → Enqueue children (`cur*10 + digit`).
Debido a que siempre aparecen los números más cortos ( dígitos más bajos) primero, el primer número que satisface las dos condiciones está garantizado ser el mínimo.

3. *Desbordamiento de la colonia*
Nunca generamos números mayores que `INT_MAX`.
Antes de pasar un nuevo dígito, comprobamos `cur ' = INT_MAX / 10`.
Esto garantiza el número resultante en un entero firmado de 32 bits.

4. *Exacto total*
Tan pronto como encontremos un número que es ` ' k ' y divisible por `k ' , lo devolvemos.
No es necesario explorar niveles más profundos.

5. **Regresar -1 si se agota la cola. * *
Si el BFS completa sin encontrar un número válido, la respuesta es `-1`.

-...

Análisis de la Complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio Construyendo todos los números de los candidatos **O(2^L)**, donde `L ≤ 10` (digits of INT_MAX) Silencio **O(2^L)** para la cola y el estado visitado

Como `L` es a la mayoría de 10, el algoritmo funciona en microsegundos incluso para el peor caso.
Está muy por debajo del límite de tiempo de LeetCode de 1 segundo.

-...

## 🐛 Edge Cases " Ugly " Scenarios

Por qué importa cómo nuestro código maneja It ←
Silencio...
Los dos dígitos son 0 Silencio El único número posible sería 0, que no es ≤ `k` Silencio Inmediata `-1` regreso Silencio
Silencio `digit1 == dígito2` Silencio Encuueríamos números duplicados, potencialmente causando bucles infinitos Silencio Revisamos `digit2 != dígitos1` antes de encubrir el segundo dígito
¿Se permiten ceros líderes? tención Números como `012` son inválidos tención Los dígitos de inicio nunca son cero
Silencio Desbordamiento después de la multiplicación Silencioso `cur * 10 + d` puede exceder `int` Utilizamos " largo " (o " largo " ) y comparamos con "INT_MAX " Silencio
Silencio Muy grande `k` cerca de `INT_MAX` Silencio No hay números 'k` se puede construir Silencio BFS agotará la cola y devolverá `-1` Silencio

-...

## 🎯 Bueno, malo, y lleno del problema

Silencio Silencio
Silencio------------Prince------
Silencio **Problem Clarity** Silencio Claras limitaciones y objetivos
Silencio **Búsqueda espacial** Silenciosa pequeña (≤ 1024 nodos)
Silencio **Multiple Solutions** Silencio DFS, BFS, DP, BFS with remainder pruning Silencio Algunas ingenuas implementaciones de DFS pueden explotar Silencio Recursive DFS sin la memoización puede llegar a los límites de profundidad de recursión
Silencio **Testing Dificultad** Silencio Los casos de Edge están bien definidos. El caso `k = 1, dígitos = {0,1}` pruebas que nunca devolvemos 0
Silencio ** Valor de la vista** Silencio Muestra comprensión de la teoría del número de BFS Silencio Podría ser percibido como "trivial" Silencio Requiere un manejo reflexivo de los principales ceros y el desbordamiento

**Takeaway:**
Este problema es un gran juguete de entrevista porque combina BFS simple con cheques número-teoría y manejo cuidadoso de desbordamiento. Prueba la capacidad de un candidato para razonar sobre limitaciones y casos de borde sin ahogarse en estructuras de datos complejas.

-...

## 📈 SEO‐Optimized Blog Summary

- **Título: ** *“LeetCode 1999 – Más pequeño Gran Hecho de Dos Digitos (Java, Python, C++)*
- **Meta Descripción:** *“Aprenda a resolver LeetCode 1999 con BFS en Java, Python y C++. Descubra casos de borde, complejidad y consejos de entrevista.”*
- **Keywords:** LeetCode 1999, el más pequeño Múltiple, BFS, solución Java, solución Python, solución C++, algoritmo de entrevista, consejos de entrevista de trabajo, desafío de programación.
- ** Estructura:** Intro → Declaración de problemas → Limitaciones → BFS Enfoque → Código (Python, Java, C++) → Casos de borde → Complejidad → Good/Bad/Ugly → Conclusión.

Siéntete libre de incrustar los bloques de código y capturas de los resultados de LeetCode para aumentar el compromiso y compartir en LinkedIn o Twitter.

-...

Pensamientos de clausura

* La solución **BFS** es el enfoque más limpio y eficiente.
* Garantiza la mínimaidad porque exploramos los números para aumentar la longitud.
* Manejo de la desbordamiento y el caso de borde duplicado-digit hace que el código sea robusto.
* Este problema es perfecto para la preparación de entrevistas: es corto, sin embargo prueba BFS, manejo de desbordamiento y atención al detalle.

¡Buena suerte con tus entrevistas de codificación! 🚀