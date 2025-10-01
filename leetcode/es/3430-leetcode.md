-...
Título: LeetCode 3430. Sumas máximas y mínimas de la mayoría de las subarrayas de tamaño K -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recapitulación de problemas (LeetCode 3430)

■ **Sumas mínimas y mínimas de la mayoría de los subarrayos K de tamaño**
> `public long minMaxSubarraySum(int[] nums, int k) `

Given an integer array `nums` (fortnums sometidas ≤ 80 000) and a positive integer `k ' (k ≤ ¦

`` `
[ max(subarray) + min(subarray) ]
`` `

Se consideran todas las subarrayas de longitudes `1 ... k`.
La respuesta puede ser muy grande, por lo que se devuelve como un entero firmado de 64 bits.

-...

## 2. Why This Problem is a “Job‐Interview” Magnet

* **La presión de la complejidad del tiempo** – O(n log n) o O(n) es necesaria para elementos de 80 k.
* **Maestría de estructuras de datos** – pilas monotónicas, sumas prefijo, y matemáticas a mano.
* **Mathematical insight** – Contando subarrays que contienen un elemento particular como el máximo o mínimo respetando una tapa de longitud.

Mostrando un limpio La solución O(n) es una manera segura de impresionar a los gerentes de contratación en plataformas como LeetCode, Hired o una entrevista técnica.

-...

## 3. Resúmenes de solución de alto nivel

1. **Comentar la contribución de cada elemento como máximo. #
Para cada índice `i` encontramos:
* `LMax[i]` – cuántos elementos a la izquierda podemos extender mientras conservamos `nums[i]` el *strictamente* más grande.
* `RMax[i]` – ¿Cuántos elementos a la derecha podemos extender mientras conservamos `nums[i]` el *greater‐than o igual* (es decir, no menor).

2. **Comentar la contribución de cada elemento como mínimo. #
Los arrays analógicos `LMin[i]` y `RMin[i]` se construyen con comparaciones opuestas.

3. **Para cada elemento computa cuántas subarrayas de longitud ≤ k la contienen como máx/min.**
El subarray debe elegir una distancia izquierda `x  Iberia [0, L-1]` y una distancia derecha `y  divisa [0, R-1]` con
`x + y + 1 ≤ k`.
El número de pares válidos `(x, y)` es el valor devuelto por la función helper `count(L, R, k)`.

4. **Acumular el total**:
`answer += nums[i] * (count(LMax[i], RMax[i], k) + count(LMin[i], RMin[i], k)`.

Los cuatro escaneos direccionales se realizan con una sola pila monotónica cada uno, dando tiempo **O(n)** y **O(n)** memoria extra.

-...

## 4. La Fórmula de Conteo de Piezas

El subproblema central: **Cuantos pares (x, y) satisfacen* *
`0 ≤ x ■ L`, `0 ≤ y ' se hizo R`, y `x + y + 1 ≤ k`?

Vamos.

`` `
Xmax = min(L-1, k-1) // mayor distancia izquierda posible que todavía puede caber
`` `

Para cualquier `x' en `[0, Xmax]` el lado derecho puede ser en la mayoría `min(R, k - x)`.

Define

`` `
a = min(Xmax, k - R) // límite donde k - x ñ R ( lado derecho saturado)
`` `

*Si es ≥ 0*:
All `x = 0 ... a` contribute `R` subarrays (right side never limited).
Sum1 = (a + 1) * R.

*Remanente `x = a + 1 ... Xmax`*:
Aquí el lado derecho está limitado por la longitud, contribuyendo `k - x`.
Sum2 = ega(k - x) = k * (Xmax - a) - egax.
(Xmax + a) * (Xmax - a) / 2.

El recuento total es `Sum1 + Sum2`.
Todo aritmético encaja en enteros firmados de 64 bits porque `L, R ≤ 80 000` y `k ≤ 80 000`.

-...

## 5. Full Implementations

A continuación encontrará soluciones limpias y bien adaptadas en **Java, Python y C++**.
Los tres usan la misma idea monotónica-stack + conteo a mano.

## 5.1 Java (estilo LeetCode)

``java
importa java.util. ArrayDeque;
importa java.util. Deque;

Clase Solución {
public long minMaxSubarraySum(int[] nums, int k) {
int n = nums.length;
long[] LMax = nuevo largo[n];
long[] RMax = nuevo largo[n];
long[] LMin = nuevo largo[n];
long[] RMin = nuevo largo[n];

--- max left (strictly decreasing) ---
Deque cumplióInteger confianza st = nuevo ArrayDeque correspondió();
para (int i = 0; i) {}
mientras (!st.isEmpty() " frutos nums[st.peek()] " nums[i]) st.pop();
LMax[i] = st.isEmpty() ? i + 1 : i - st.peek();
st.push(i);
}

--- max right (no aumento) ---
st.clear();
para (int i = n - 1; i 0; --i) {
mientras (!st.isEmpty() " nums[st.peek()] " nums[i]) st.pop();
RMax[i] = st.isEmpty() ? n - i : st.peek() - i;
st.push(i);
}

----- min left (strictly increasing) ---
st.clear();
para (int i = 0; i) {}
mientras (!st.isEmpty() " nums[st.peek()] " nums[i]) st.pop();
LMin[i] = st.isEmpty() ? i + 1 : i - st.peek();
st.push(i);
}

---- min right (no-disminuir) ---
st.clear();
para (int i = n - 1; i 0; --i) {
mientras (!st.isEmpty() " nums[st.peek()] " nums[i]) st.pop();
RMin[i] = st.isEmpty() ? n - i : st.peek() - i;
st.push(i);
}

ans largas = 0;
para (int i = 0; i) {}
cntMax = conteo(LMax[i], RMax[i], k);
cntMin = count(LMin[i], RMin[i], k);
ans += (long) nums[i] * (cntMax + cntMin);
}
devolver los ans;
}

/** cuantas subarrays de longitud = k contienen nums[i] como máx/min */
cuenta larga privada (long L, long R, int k) {
Xmax largo = Math.min (L - 1, k - 1);
si (Xmax ) 0) retorno 0; // no posible subarray

largo a = Math.min (Xmax, k - R);
larga res = 0;

si 0) { // lado derecho saturado
res += (a +1) * R;
}

larga izquierda = un + 1; // distancias izquierda restantes
larga derecha = Xmax;
si (izquierda)
Long len = derecha - izquierda + 1;
larga sumaX = (izquierda + derecha) * lino / 2; //
res += k * len - sumX; // Governing(k - x)
}
restitución;
}
}
`` `

## 5.2 Python 3 (LeetCode)

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def minMaxSubarraySum(self, nums: List[int], k: int) - título int:
n = len(nums)
LMax = [0] * n
RMax = [0] * n
LMin = [0]
RMin = [0]

# max left (strictly decreasing)
st = deque()
para i, val en enumerate(nums):
mientras que st y nums [st[-1]]
st.pop()
LMax[i] = i + 1 si no st i - st[-1]
st.append(i)

# max right (non‐increasing)
st.clear()
para i en rango(n - 1, -1, -1):
mientras que st y nums[st] [i]:
st.pop()
RMax[i] = n - i if not st [-1] - i
st.append(i)

# min left (strictly increasing)
st.clear()
para i, val en enumerate(nums):
mientras que st y nums[st [-1] val:
st.pop()
LMin[i] = i + 1 si no st else i - st[-1]
st.append(i)

# min right (non‐decreasing)
st.clear()
para i en rango(n - 1, -1, -1):
mientras que st y nums[st[-1] не nums[i]:
st.pop()
RMin[i] = n - i if not st [-1] - i
st.append(i)

def cnt(L: int, R: int, k: int) - Propiedad int:
Xmax = min(L - 1, k - 1)
si Xmax se hizo 0:
retorno 0
a = min(Xmax, k - R)
res = 0
si un >= 0:
res += (a +1) * R
izquierda = 1 + 1
derecho = Xmax
si se deja a la derecha:
len_ = derecha - izquierda + 1
sum_x = (izquierda + derecha) * len_ // 2
res += k * len_ - sum_x
retorno

ans = 0
para i en rango(n):
ans += nums[i] * (cnt(LMax[i], RMax[i], k) + cnt(LMin[i], RMin[i], k)

Retorno
`` `

### 5.3 C++ (GNU ++17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
largo tiempo minMaxSubarraySum(vector realizadoint limitada nums, int k) {
int n = nums.size();
vector de larga duración LMax(n), RMax(n), LMin(n), RMin(n);

// max left : estrictamente decreciente pila
deque indicaint
para (int i = 0; i) {}
mientras (!st.empty() " frutos nums[st.back()] " se entiende= nums[i]) st.pop_back();
LMax[i] = st.empty() i + 1 : i - st.back();
st.push_back(i);
}

// max right : non‐increasing stack
st.clear();
para (int i = n - 1; i 0; --i) {
mientras (!st.empty() ' nums[st.back()]
RMax[i] = st.empty() ? n - i : st.back() - i;
st.push_back(i);
}

// min izquierda : estrictamente creciente pila
st.clear();
para (int i = 0; i) {}
mientras (!st.empty() ' nums[st.back()] √= nums[i]) st.pop_back();
LMin[i] = st.empty() i + 1 : i - st.back();
st.push_back(i);
}

// min a la derecha : no-disminuir la pila
st.clear();
para (int i = n - 1; i 0; --i) {
mientras (!st.empty() " frutos nums[st.back()] " nums[i]) st.pop_back();
RMin[i] = st.empty() ? n - i : st.back() - i;
st.push_back(i);
}

autoconteo = [ cl](long long L, long long long R, int k) - título largo
largo Xmax = min(L - 1, (long long)k - 1);
si (Xmax 0) devuelve 0;
largo a = min(Xmax, (long long)k - R);
largas res = 0;
si 0) {
res += (a + 1) * R; // lado derecho saturado
}
larga izquierda = 1 +;
largo derecho = Xmax;
si (izquierda)
larga longitud = derecha - izquierda + 1;
larga larga suma = (izquierda + derecha) * lino / 2;
res += (long)k * len - sumx;
}
restitución;
};

ans largos = 0;
para (int i = 0; i) {}
ans += (long long)nums[i] *
(count(LMax[i], RMax[i], k) + count(LMin[i], RMin[i], k));
}
devolver los ans;
}
};
`` `

Las tres soluciones funcionan en tiempo **O(n)**, usan **O(n)** memoria auxiliar, y son totalmente compatibles con las interfaces de presentación LeetCode Java/Python/C++.

-...

## 6. Pitfalls comunes " Cómo evitarlos

Silencio Pitfall Silencio ¿Por qué sucede?
Silencio...
Silencio **Using a non-decreasing stack for both directions** tención Los límites izquierdo y derecho requieren reglas de comparación *diferentes* (`≤` vs `traducido`). Mixing them changes `L`/`R` values and leads to over/undercounting. Mantener *dos* pases distintos para máx y min, y utilizar la comparación correcta ( < = > para máx izquierdo > > > ). Silencio
Silencio **Iterating over `x` for every element** Silencio Incluso con `O(n)` array size, un bucle interior sobre `L' se convertiría en O(n2). TENIDO Utilizar la fórmula arrugada derivada arriba – sólo un puñado de operaciones aritméticas por elemento. Silencio
Silencio **Overflow of 32‐bit integers** Silencio La suma de los subarrays puede exceder `2^31‐1`. Silencio Uso `long` (Java), `int64_t` (C++), o los enteros arbitrarios de apreciación de Python. Silencio
Silencio **Off‐by‐one in length limitt** Silencio La condición es `x + y + 1 ≤ k`, no `x + y ≤ k`. Silencio Recordar restar `1` de `k` cuando computing `Xmax` (`k-1`). Silencio

-...

## 7. Análisis de la complejidad

TEN TERRITOR TEN SON ANTERIOR ANTERIOR TERRITORIO
Silencio----------Prince----------------
Silencio Cuatro escaneos monotónicos para establos Silencio **O(n)** Silencio **O(n)**
Silencio Contando con `cuenta()` por elemento Silencio **O(n)** Silencio **O(1)**
Silencio La acumulación final Silencio **O(n)** Silencio
Silencio **Total** Silencio**

Con `n ≤ 80 000`, todas las soluciones encajan cómodamente dentro de los límites estrictos de LeetCode (conformar 0,2 s tiempo de ejecución, se realizó 20 MB de memoria).

-...

## 8. Takeaway

La clave para resolver el “Sum of Subarray Ranges” (LeetCode 2104) reside eficientemente en dos ideas:

1. **Pre-compute** el máximo alcance izquierdo/derecha para cada elemento como el subarray *maximum* y *mínimo* utilizando dos pases monotónicos separados.
2. **Cuente** los subarrays elegibles con una fórmula aritmética ** ( " cuenta() " ) que elimina la necesidad de bucles anidados.

Una vez que estos dos bloques de construcción están en su lugar, la suma final es un simple pase lineal.

-...

### 🎯 Quick Recap for Interviewers

- Explicar la necesidad de comparaciones *diferentes* por lado.
- Mostrar la fórmula de " cuenta " derivada y subrayar su naturaleza " O(1) " .
- Mención de que la respuesta final es la suma de `nums[i] * (cntMax + cntMin)`.

Este enfoque demuestra la maestría sobre las pilas monotónicas, el razonamiento prefijo/suffix y la aritmética cuidadosa—skills altamente valorados en las entrevistas de codificación.

-...

## 8. TL;DR

- **Problema**: Suma de `max(subarray) - min(subarray)` sobre todas las subarrayas de longitud `≤ k`.
- **Solución**: Cuatro pases monotónicos para computar los límites `L`/`R` para máx y min, luego utilizar una fórmula compacta para contar los subarrays elegibles por elemento.
- *Hora*: `O(n)`, **Pace**: `O(n)`.
- **Idiomas**: Soluciones de trabajo completas en **Java**, **Python**, y **C+**.

¡Feliz codificación! 🚀

-...

*Si ha encontrado útil esta guía, considere protagonizarla en GitHub y compartirla con amigos preparándose para el ** "Sum of Subarray Ranges" (LeetCode 2104)** entrevista pregunta! *