-...
Título: LeetCode 2217. Encontrar Palindrome Con la longitud fija -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**K‐th Palindrome – una solución basada en matemáticas* *

Por una longitud fija `L` que hacemos **no** tenemos que enumerar todos los números `L`‐digit.
Un palindrome está completamente determinado por su *izquierda mitad* – la mitad derecha es sólo
al revés.
Así que sólo tenemos que considerar los números

`` `
10^(ceil(L/2)-1) , 10^(ceil(L/2)-1)+1 , ... , 10^(ceil(L/2))-1
`` `

(`ceil(L/2)` es el número de dígitos de la mitad izquierda).

----------------------------------------------------

### 1. ¿Cuántos palindromas de longitud L existen?

`` `
conteo(L) = 9 * 10^(ceil(L/2)-1)
`` `

`10^(ceil(L/2)-1)` es la mitad izquierda más pequeña (`1 0 ... 0`), el dígito principal
no puede ser `0`. El factor `9` proviene de los posibles dígitos principales `1...9`.

----------------------------------------------------

### 2. Construir el palindrome k‐th

Para un determinado `k ( 1-basado )`:

`` `
media = (k-1) + 10^(ceil(L/2)-1) # izquierda mitad como entero
izquierda = str(half)
derecha = izquierda[:len(left)-L%2] # caer el dígito medio si L es extraño
pal = izquierda + derecha[:-1] # concatenate ' reverse
`` `

Toda la expresión es devuelta como un entero de 64 bits (`long` en Java,
En Python.

----------------------------------------------------

### 3. Código (Java)

``java
Clase Solución {
privado largo getPalindrome(long k, int halfLen, int L) {
long leftNum = (k - 1) + (long)Math.pow(10, halfLen - 1); // left part
Pendiente izquierda = Long.toString(leftNum);
Cierre a la derecha = izquierda.substring(0, left.length() - (L % 2)); // drop mid
volver Long.parseLong(left + nuevo StringBuilder(right).reverse());
}

public long[] kthPalindrome(int[] consultas, int L) {
int n = consultas. longitud;
long[] ans = new long[n];

int halfLen = (L +1) / 2; // ceil(L/2)
maxCnt largo = 9L * (long)Math.pow(10, halfLen - 1); // 9 * 10^(halfLen-1)

para (int i = 0; i) {}
long k = consultas[i];
si (k Ø máxCnt) {
as[i] = -1;
. ♫ ... {
ans[i] = getPalindrome(k, halfLen, L);
}
}
devolver los ans;
}
}
`` `

----------------------------------------------------

### 4. Código (Pytón)

``python
Solución de clase:
def kthPalindrome(self, queries: List[int], intLength: int) List[int]:
media = (intLength +1) // 2
base = 10 ** (half - 1) # más pequeña izquierda
max_cnt = 9 * 10 ** (half - 1)

ans = []
para k en consultas:
si k > max_cnt:
ans.append(-1)
más:
izquierda = str(base + k - 1)
derecha = izquierda [:-1]
intLength % 2 == 1:
derecha = derecha[1:]
ans.append(int(left + right))
Retorno
`` `

----------------------------------------------------

### 5. Por qué funciona esto

* El número de palindromas de longitud `L` es en la mayoría de `9 * 10^(ceil(L/2)-1), que cabe
cómodamente en un entero de 64 bits para las limitaciones del problema.
* La mitad izquierda es simplemente el número 'k'‐th en el rango
`[10^(ceil(L/2)-1) , 10^(ceil(L/2)))-1]`.
* Al reflejar esta mitad obtenemos el palindromo inmediatamente – sin enumeración,
sin recidiva, sin gran uso de memoria.

----------------------------------------------------

Resultado**

El algoritmo se ejecuta en el tiempo de `O (las vidas eternas) y `O(1)` espacio auxiliar,
resolver el problema de manera eficiente incluso para los límites máximos.