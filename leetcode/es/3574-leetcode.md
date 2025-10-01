-...
Título: LeetCode 3574. Maximizar Subarray GCD Score -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 3574. Maximizar la puntuación de Subarray GCD
**Hard** Ø 1500 ≤ n ≤ 1500 Ø 1 ≤ nums[i] ≤ 109  1 ≤ k ≤ n

■ Puede doblar cualquier elemento a la mayor parte de la vez, pero puede realizar al máximo **k** tales operaciones.
■ Una puntuación de sub-array = (longitud de sub-array) × (GCD del sub-array).
■ Devuelve la puntuación máxima alcanzable después de lo más **k** duplicaciones.

-...

### 1. Intuición

* Duplicar un elemento solo lo multiplica por 2.
* El GCD de un sub-array sólo puede aumentarse por factores de 2 – todo lo demás ya es compartido por todos los elementos.
* Vamos a tener en cuenta cada número como

\[
nums[i] = 2^{e_i}\; \cdot\; a_i, \qquad a_i\ \text{odd}
\]

`e_i` es el exponente del bit más bajo (`_construidoin_ctz` en C++, `Integer.numberOfTrailingZeros` en Java, `x ' truco en Python).
La parte extraña `a_i` no puede cambiarse duplicando; sólo el exponente `e_i` puede crecer a 1 si duplicamos el elemento.

* For a fixed sub-array `[l ... r]` el GCD de las partes extrañas es un único número impar `g`.
El GCD de todo el sub-array es entonces

\[
GCD = g \; \cdot\; 2^{\min\{e_l,\dots,e_r\}
\]

duplicar un elemento que ya tiene el exponente *mínimo* aumentará el GCD por otro factor 2.
Duplicar cualquier otro elemento no cambia el GCD porque el exponente mínimo permanece igual.

* Por lo tanto, para un submarino sólo nos importa

1. **`g`** - gcd de las partes extrañas.
2. **`minE`** - menor exponente entre los elementos.
3. **`cntMin`** - ¿Cuántos elementos de la sub-array tienen exponente `minE`.

Si 'cntMin ≤ k`, podemos duplicar todos esos elementos 'cntMin` → GCD se duplica.

-...

### 2. Algoritm

`` `
mejor = 0
para l = 0 ... n-1:
g = 0
minE = INF
cntMin = 0
para r = l ... n-1:
g = gcd(g, a[r]) // a[r] = nums[r]
e = exponente[r] // ceros que siguen de nums[r]

si e
minE = e
cntMin = 1
si minE:
cntMin += 1

len = r - l + 1
base = len * g * (1LL ANTE
mejor = max(best, base)

si cntMin
mejor = max(best, base * 2) // podemos duplicar todos los elementos min‐exponentes
mejor
`` `

* **La complejidad del tiempo* Dos bucles anidados → **O(n2)** (≤ 2 · 106 iteraciones para n = 1500).
* **La complejidad del espacio** – O(1) extra (sólo unos pocos enteros / largos).
* Todo aritmético encaja en 64 bits firmados (`long` en Java / C++ / Python’s int).

-...

### 3. Prueba de corrección

Demostramos que el algoritmo devuelve la puntuación GCD máxima alcanzable.

#### Lemma 1
Para cualquier sub-array `S`, que `g` sea el GCD de sus partes extrañas, `minE` el exponente mínimo, y 'cntMin` el número de elementos que alcanzan `minE`.
The GCD of `S` without any doubling is `g · 2^{minE}`.

*Proof. *
Cada elemento puede ser escrito como `2^{e_i} · a_i` con extraño `a_i`.
The GCD of the odd parts is `g`.
El GCD de los poderes de dos es el exponente más pequeño, `minE`.
Así el GCD es su producto. ∎



#### Lemma 2
Si doblamos todos los elementos 'cntMin' que tienen exponente `minE`, el GCD de `S' se convierte en
g · 2^{minE+1}`; duplicar cualquier otro elemento no puede aumentar el GCD.

*Proof. *
Duplicar un elemento con el exponente `e_i` aumenta a `2^{e_i+1}·a_i`.
Si `e_i не minE`, el exponente mínimo entre los elementos sigue siendo `minE`, por lo que el GCD permanece `g·2^{minE}`.
Si `e_i = minE`, el nuevo mínimo se convierte en `minE+1`, por lo que el GCD aumenta exactamente por un factor 2. ∎



#### Lemma 3
Para cualquier sub-array `S`, el máximo GCD obtenido después de la mayoría de las duplicaciones 'k' es

`` `
score(S) = len(S) * g * 2^{minE} if cntMin ⇩ k
score(S) = len(S) * g * 2^{minE+1} if cntMin ≤ k
`` `

*Proof. *
Si `cntMin не k`, no podemos duplicar todos los elementos mínimos, por lo que lo mejor que podemos hacer es mantener el GCD como en Lemma 1.
Si 'cntMin ≤ k`, podemos duplicar todos esos elementos (utilizando en la mayoría de las operaciones 'cntMin ≤ k'), logrando el GCD más grande por Lemma 2.
Ninguna otra combinación de duplicaciones puede aumentar aún más el GCD porque todos los demás elementos tienen exponente ≥ `minE`. ∎



##### Theorem
El algoritmo produce la puntuación GCD máxima alcanzable después de las duplicaciones más `k`.

*Proof. *
Durante el doble bucle, cada sub-array posible se examina exactamente una vez.
Para ese sub-array el algoritmo calcula `base = len · g · 2^{minE}` (Lemma 1).
Si `cntMin ≤ k`, también evalúa `base·2` (Lemma 2).
Por Lemma 3 estas son precisamente las mejores puntuaciones alcanzables para ese sub-array.
La variable `mejor' mantiene el máximo de todas esas puntuaciones, por lo que después de que todas las sub-arrayas se procesan `mejor` equivale al óptimo global. ∎



-...

### 4. Aplicación

A continuación se presentan soluciones completas y compilables en **Java**, **Python**, y **C+**.

-...

###### 4.1 Java

``java
importar java.util*;

Solución de la clase pública {}
// GCD para int – trabaja para todos los valores
int gcd (int a, int b) {}
mientras (b!= 0) {
t = un % b;
a = b);
b = t;
}
devolver a;
}

public long maxGCDScore(int[] nums, int k) {
int n = nums.length;
// Pre-compute exponents and odd parts
int[] exp = nuevo int[n];
int[] odd = nuevo int[n];
para (int i = 0; i)
int e = Integer.numberOfTrailingZeros(nums[i]); // exponent of lowest set bit
exp[i] = e;
odd[i] = nums[i]  Confía en e; // cambio derecho por e bits
}

long best = 0;

para (int l = 0; l ' il; n; l++) {}
int g = 0;
int minE = Integer.MAX_VALUE;
int cntMin = 0;

para (int r = l; r) {}
g = gcd(g, odd[r]);

int e = exp[r]
si
minE = e;
cntMin = 1;
} si (e == minE) {
cntMin++;
}

Long len = r - l + 1;
base larga = lavabo * g * (1L)
mejor = Math.max(mejor, base);

si
mejor = Math.max(mejor, base * 2); // doble todos los elementos mínimos
}
}
}

devolver mejor;
}
}
`` `

*Compile & run:*
``bash
javac Solution.java
java Solution // call maxGCDScore(...) de un arnés de prueba
`` `

-...

##### 4.2 Python 3

``python
importadores
de la importación de matemáticas gcd
de la importación Lista

Solución de clase:
def maxGCDScore(self, nums: List[int], k: int) - Conf int:
n = len(nums)

# Pre-compute exponent of low set bit and odd part
exp = [0]
extraño = [0]
para i, val en enumerate(nums):
e = (val & -val).bit_length() - 1 # trailing ceros via x & -x
exp[i] = e
odd[i] = val >

mejor = 0

para l en rango(n):
g = 0
minE = n + 1 centinela
cntMin = 0

para r en rango(l, n):
g = gcd(g, odd[r])

e = exp[r]
si e
minE = e
cntMin = 1
elif e == minE:
cntMin += 1

longitud = r - l + 1
base = longitud * g * (1  won)
mejor = max(best, base)

si cntMin
mejor = max(best, base * 2)

mejor
`` `

-...

##### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

int main() {}
ios::sync_with_stdio(false);
cin.tie(nullptr);

int n, k;
si (!(cin нелин n нених) devuelve 0;
vector realizado largo tiempo nums(n);
para (int i = 0; i ' i); ++i) cin ' nums[i];

// Pre-compute exponents and odd parts
vector asignadoint confianza exp(n);
vector significado(n)
para (int i = 0; i) {}
int e = __constructionin_ctzll(nums[i]); // exponent of lowest set bit
exp[i] = e;
odd[i] = nums[i] √≥ título e; // odd part
}

long long best = 0;

para (incluido l = 0; l) {}
int g = 0;
int minE = INT_MAX;
int cntMin = 0;

para (int r = l; r) {}
g = std::gcd(g, odd[r]);

int e = exp[r]
si
minE = e;
cntMin = 1;
} si (e == minE) {
++cntMin;
}

larga longitud = r - l + 1;
long long base = len * g * (1LL ANTE)
mejor = max(best, base);

si
mejor = máximo (mejor, base * 2); // doble todos los elementos min‐exponentes
}
}
}

cout se hizo mejor
retorno 0;
}
`` `

Los tres programas tienen **O(n2)** tiempo de ejecución y **O(1)** memoria auxiliar, satisfaciendo los límites.

-...

## 5. Discusión en el blog

### 5.1 Problema Recap

■ *Se puede duplicar en la mayoría de los elementos **k** (una vez por elemento) y desea el más alto `(length × GCD)` de cualquier sub-array. *

El giro clave es que sólo los poderes de dos pueden verse afectados por una duplicación; todos los demás factores comunes ya están presentes en el GCD.

## 5.2 Why Two Nested Loops are Good

Con `n ≤ 1500` el número total de sub-arrays es

\[
\frac{n(n+1)}{2} \le 1\,125\,750
\]

Incluso con el cálculo interno del GCD (tiempo constante) esto está muy por debajo de un segundo en las CPU modernas.
Una búsqueda de fuerza bruta que recomputa el GCD desde cero para cada sub-array sería *O(n3)* y TLE – nuestro GCD incremental inteligente lo mantiene *O(n2)*.

### 5.3 Common Pitfalls

Silencio Pitfall Silencio
Silencio...
Silencio Usando enteros de 32 bits para el producto final (`len * g * 2^minE`) puede rebosar ¦ Use `long` (Java) / `long long` (C++) / Python arbitra‐precision int sometida
Silencio Olvídate de cambiar la parte *odd* correctamente TENIENDO `odd[i] = nums[i] NUESTRA E[i]` (Java/C+++) o `odd[i] = nums[i] // (1 ANTERIEDE E[i])` (Python)
Silencio Usar `_construidoin_ctz` en cero Silencio `nums[i]` es siempre ≥ 1, tan seguro. Silencio
¦ Mis-counting `cntMin` (debe reasentarse cuando aparezca un nuevo exponente más pequeño) Silencio Reset `cntMin = 1` cuando `e iere minE`.

### 5.4 Complexity Summary

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio Pre-procesamiento de exponentes " rare parts Silencio O(n)
Silencio Dos bucles anidados Silencio O(n2) Silencio O(1) Silencio
Silencio en general **O(n2)**

Para el peor caso `n = 1500` esto es sólo sobre 2 × 106 iteraciones internas - lo suficientemente rápido.

## 5.5 Por qué la solución es elegante

* Nunca tocamos el array original; trabajamos en su representación condicionada.
* Todo el problema se reduce a mantener la pista del **mínimo exponente** en una ventana deslizante.
* La duplicación se trata como una multiplicación *condicional* por 2 – sin necesidad de un DP complicado.

### 5.6 SEO > Tags

*LeetCode 3574*
- **Maximizar la puntuación del GCD**
- Operaciones duplicadas
- Ray GCD
- **O(n2) solución**
- **Two-pointer GCD trick* *
- **C++ O(n2) GCD**
- Integro de 64 bits de java**

-...

¡Feliz codificación