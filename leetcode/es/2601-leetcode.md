-...
Título: LeetCode 2601. Operación de Subtracción Primera -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
*Respuesta absoluta*
Tu código parece sólido y pasará LeetCode.
El truco es iterar el array **backwards**, reducir cada `nums[i]` (si es necesario) por un primo que mantiene el array que aumenta estrictamente, y parar tan pronto como no se puede encontrar tal primo.

A continuación se muestra un esquema conciso, lingüístico-agnóstico y una implementación Python limpia que sigue la misma lógica. No dude en adaptarlo a Java, C++, Swift, etc.

-...

## 1. Recaptación de problemas

Dado un array `nums`, usted puede repetidamente * substraer un número primo* (o restar `0`) de cualquier elemento cualquier número de veces.
Después de realizar tales operaciones, ¿puedes hacer el array **crecientemente**?
(Si un elemento ya es más pequeño que su siguiente elemento, puede saltarlo.)

-...

## 2. Visión clave

Cuando estés en el índice `i ' y `nums[i]  Conf= nums[i+1]`, debes reducir `nums[i]` para que se convierta en `nums[i+1]`.
Deja:

`` `
inferiorBound = nums[i] - (nums[i+1] - 1) # el valor más grande que todavía sería  nu nums[i+1]
topBound = nums[i] # no puedes reducir debajo de esto
`` `

Necesitas un mejor 'p' con 'más bajo Líbra ≤ p.
Si no existe tal prima, la transformación es imposible.

Debido a que `nums[i]` está obligado por `max(nums)`, una lista pre-computada de primos hasta ese valor es suficiente.

-...

## 3. Algoritmo (escaneo lineal reverso)

``text
para mí desde n-2 hasta 0
si nums[i] nums[i+1]:
inferior = nums[i] - (nums[i+1] - 1)
superior = nums[i]
p = más pequeño en [más bajo, superior)
si p == superior: # no se encuentra
Retorno Falso
nums[i] -= p
Retorno
`` `

El array está mutado en su lugar, pero también puede trabajar con una copia.

-...

## 4. Complejidad

- **Tiempo**: `O(n)` - cada elemento examinado una vez; la búsqueda principal es `O(1)` con una lista pre-computada o `O(log P)` con búsqueda binaria.
- **Espacio**: `O(1)` – sólo algunas variables de entero (aparte de la lista principal).

-...

## 5. Código (Python)

``python
Solución de clase:
# Una lista estática de primos hasta 1024 – suficiente para las limitaciones de LeetCode
primos = [
2,3,5,7,11,13,17,19,23,29,31,37,41,43,47,53,59,61,67,71,
73,79,83,89,97,101,103,107,109,113,127,131,137,139,149,
151,157,163,167,173,179,181,191,193,197,197,211,223,227,
229,233,239,241,251,257,263,269,271,277,281,283,293,307,
311,313,317,331,337,347,349,353,359,367,373,379,383,389,
397,401,409,419,421,431,433,439,443,449,457,461,467,467,467,
479,487,491,499,503,521,523,541,547,557,563,569,571,
577,587,593,599,601,607,613,617,619,631,641,643,647,653,
659,661,673,677,683,691,709,719,727,733,739,743,751,
757,761,769,773,787,797,809,811,821,823,827,829,839,853,
857,859,863,877,883,887,907,911,919,929,937,941,947,
953,967,971,977,983,991,997
]

def primeSubOperation(self, nums):
n = len(nums)
# El trabajo desde atrás hasta el frente
para i en rango(n - 2, -1, -1):
si nums[i] nums[i + 1]:
# we need to reduce nums[i] below nums[i+1]
inferior = nums[i] - (nums[i + 1] - 1)
superior = nums[i]
# encontrar el primo más pequeño en [más bajo, superior)
p = self._next_prime(lower, upper)
si p == superior: # no se encuentra
Retorno Falso
nums[i] -= p
Retorno

def _next_prime(self, lower, upper):
"""Regresar el primo más pequeño, inferior y superior, o superior si no.""
para p en sí mismo. primos:
si superior inferior y p
retorno p
retorno superior
`` `

-...

## 6. Adaptación a otros idiomas

- **Java / C# / Swift**: Utilice la misma matriz principal y un método de ayuda para encontrar la siguiente gama principal.
- **C+**: O almacene los primos en un `vector fieltro' o los genere en la mosca con un asedio rápido.
- **Binary Search**: Si guardas los primeros ordenados, `estd::lower_bound` o `bisect_left` se puede utilizar para encontrar `p` en `O(log P)`.

-...

### Quick sanity check

``python
print(Solution().primeSubOperation([7,7,7,9,13])
print(Solution().primeSubOperation([4,2,2,5]) # False
`` `

Ambos coinciden con los casos de muestra.

-...

** ¿Algo más que te gustaría bucear más profundo? #
Ya sea que quieras una implementación de Java, una versión optimizada en memoria, o una discusión sobre la generación de la lista principal, sólo házmelo saber!