-...
Título: LeetCode 3344. Array de tamaño máximo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Panorama general de los problemas

**LeetCode 3344 – Máximo Sized Array**
■ **Dificultad:**
■ **Tags: ** Búsqueda binaria, Manipulación de bits, Matemáticas

■ ** Declaración sobre los problemas* *
■ Se le da un entero positivo.
■ Definir una matriz 3-D `A` del tamaño `n × n` como
[j] [k] = i * (j OR k)` para todos `0 ≤ i, j, k iere n`.
■ Encuentre el entero más grande `n` tal que la suma de *todos* elementos en `A` no exceda `s`.

-...

## 2. Intuición

La solución ingenua construiría el array y lo resumía – imposible para `n` 10.
La clave es obtener una fórmula **conformada** para la suma que se puede evaluar en el tiempo O(log n).

Vamos.

`` `
T(n) = egaj=0..n-1 Governing=0.n-1 (j OR k)
`` `

Entonces la suma total es

`` `
total n) = evai=0.n-1 i
* (n-1) * n / 2 (1)
`` `

Así que todo el problema se reduce a la computación `T(n)` eficientemente.



### 2.1 Computing `T(n)`

Para un solo bit `b` (valor `2^b`) la contribución de este bit a `(j OR k)` es `2^b` cuando, al menos, uno de `j' o `k' tiene ese bit set.

`` `
pares donde bit b es 0 en (j OR k) = (número de j con bit b = 0)2
`` `

If `cntZero(b)` es el recuento de los números `traducidos n` cuyo 'b`‐th bit es 0, entonces

`` `
bit_contribution(b) = (n2 - cntZero(b)2) * 2^b
`` `

`cntZero(b)` se puede encontrar observando el patrón periódico del bit:

`` `
período = 2^(b+1)
fullPeriods = n / período
período de permanencia = n %
cntZero(b) = fullPeriods * 2^b + max(0, remainder - 2^b)
`` `

Summing the contribution for all bits where `2^b ' da `T(n)`.



#### 2.2 Binary Search

Una vez que podamos evaluar `total(n)` en O(log n) tiempo, buscamos binaria para el mayor `n` con
`total(n) ≤ s`.

El rango de búsqueda se puede encontrar duplicando un límite superior hasta que la suma exceda `s` – esto garantiza un límite superior ajustado.



-...

## 3. Prueba de corrección

Demostramos que el algoritmo devuelve el máximo `n` satisfacer la condición.

### Lemma 1
Para cualquier `n`, `total(n) = T(n) * (n-1) * n / 2`.

*Proof. *
Total n) = evai=0.n-1 i * Governingj (j OR k)`.
La doble suma interior no depende de " yo " ; que sea " T n) " .
Así `total(n) = T(n) *  Elisabethi i`.
La suma de los primeros 'n-1' enteros es '(n-1)n/2`. ∎



### Lemma 2
Para cualquier posición de bits " b " , el número de pares " (j,k) " , donde el bit " b " es 1 igual a 1
n2 – cntZero(b)2`.

*Proof. *
`(j OR k)` has bit `b` equal to 0 iff both `j` and `k` have bit `b` equal to 0.
Hay `cntZero(b)` tales números para cada uno de `j` y `k`.
De ahí el número de pares donde el bit es 0 es `cntZero(b)2`.
Todos los pares restantes (`n2 – cntZero(b)2`) fijan el bit. ∎



### Lemma 3
La función del algoritmo `calcT(n)` devuelve el valor exacto de `T(n)`.

*Proof. *
Por cada bit `b` con `2^b < n`, el algoritmo:

1. Computes `cntZero(b)` via la fórmula del período (exacto, derivado del patrón binario).
2. Añade `(n2 – cntZero(b)2) * 2^b` al acumulador.

Por Lemma adultnbsp;2 esto es precisamente la contribución del bit `b` a `T(n)`.
Resumiendo todos los bits relevantes reconstruye la suma doble completa. ∎



### Theorem
`maxSizedArray(s)` devuelve el entero máximo `n` de tal manera que la suma de todos los elementos de `A` no excede `s`.

*Proof. *
*Monotonicidad. *
`total(n)` está aumentando estrictamente en `n` porque cada capa agregada aporta una cantidad no negativa.
Por lo tanto, el predicado `total(n) ≤ s` es monotone: verdadero para todos `n ≤ n* y falso para todos `n  título n*, donde `n* es la respuesta deseada.

*Binary Search Correctness. *
El algoritmo duplica el límite superior hasta que `total(r) √° s `, asegurando la verdadera respuesta está en `[l, r]`.
La búsqueda binaria entonces repetidamente a mitad del intervalo preservando al invariante que la verdadera respuesta está dentro de los límites actuales.
Cuando el bucle termina, `l` es el valor más pequeño con `total(l) ≤ s`, por lo que `l-1` es el valor más grande con `total(l-1) ≤ s`.
Así el algoritmo devuelve el máximo correcto `n`. ∎



-...

## 4. Análisis de la complejidad

Dejar `B = ⌊log2 n⌋ + 1` – el número de bits relevantes.

TEN TERRITORIO TEN TERRITORIDAD
Silencio...
Silencioso `calcT(n)` Silencio **O(B)** ♥ **O(log n)**
TENIDO `total(n)` Silencio **O(log n)**
Silencioso búsqueda binaria (log n iterations) **O(log n)2)** – insignificante para `n ≤ 106` Silencio
Silencio general **O(log n)2)** tiempo, **O(1)** espacio extra tención

Con `s ≤ 1015`, `n` nunca excede aproximadamente `2·106`, por lo que el algoritmo es fácilmente lo suficientemente rápido.



-...

## 5. Implementaciones de referencia

A continuación se presentan tres soluciones completas y compilables: **Java**, **Python**, y **C+**.
Todos utilizan aritmética de 64 bits ( " largo " ) porque los resultados intermedios pueden alcanzar ~1018.

-...

### 5.1 Java

``java
importa java.io. BufferedReader;
importa java.io. InputStreamReader;
importar java.util.StringTokenizer;

Solución de la clase pública {}
------- Conteo de números, no con bit b = 0 -------
ceros largos privados InBit(long n, int b) {
largo plazo = 1L = 1L = 1);
largo completo = n / período;
largo rem = n % período;
cntZero largo = completo * (1L)
largo = Matemáticas.max(0L, rem - (1L) obtenidas b));
cntZero + extra;
}

------- Sum of (j OR k) over 0 י= j,k
calcT largo privado (long n) {}
larga suma = 0;
para (incluido b = 0; (1L)
cntZero largo = cerosInBit(n, b);
pares largos ConBit = n * n - cntZero * cnt Cero;
suma += paresConBit * (1L se realizó b);
}
restitución;
}

------- Total suma de la matriz 3-D para el tamaño n -------
total privado (largo n) {}
t largo = calcT(n);
larga coeff = n * (n - 1) / 2; // Governing i de 0 a n-1
devolver t * coeff;
}

public int maxSized Array(long s) {
larga baja = 1, alta = 1;
mientras (total (alto)
alto 0 = 1; // doble
}
mientras (bajo)
largo medio = (bajo + alto) / 2;
si (total(mid)
baja = media + 1;
. ♫ ... {
alto = medio;
}
}
(int) (low - 1);
}

/* Conductor (para pruebas manuales)
el vacío estático público principal (String[] args) lanza Excepción {
BufferedReader br = nuevo BufferedReader (nueva InputStreamReader(System.in));
StringTokenizer st = nuevo StringTokenizer(br.readLine());
long s = Long.parseLong(st.nextToken());
System.out.println(new Solution().maxSizedArray(s));
}
}
`` `

-...

### 5.2 Python 3

``python
importadores

Solución de clase:
def ceros_in_bit(self, n: int, b: int) - Propiedad int:
(b + 1)
total = n // período
rem = n % period
cnt_zero = completo * (1 , seleccionados b)
extra = máx(0, rem - (1 0)
cnt_zero + extra

def calc_t(self, n: int) - int:
res = 0
b = 0
mientras que (1 se hizo b)
cnt_zero = self.zeros_in_bit(n, b)
pares_with_bit = n * n - cnt_zero * cnt_zero
res += pares_with_bit * (1  se realizó b)
b += 1
retorno

def total(self, n: int) - título int:
t = self.calc_t(n)
coeff = n * (n - 1) // 2
t * coeff

def maxSized Array(self, s: int) - título int:
Lo, hola = 1, 1
mientras que auto.total(hi)
hola
mientras que lo hizo hola:
media = (lo + hola) // 2
si auto.total(mid)
lo = mitad + 1
más:
hola = media
devolver lo - 1

si __name_ == "__main__":
s = int(sys.stdin.readline().strip())
print(Solution().maxSizedArray(s))
`` `

-...

### 5.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
/* ---- cuenta de números 0...
largos ceros InBit(largo n, int b) {
largo largo plazo = 1LL se realizó (b + 1);
largo tiempo completo = n / período;
largo rem = n % período;
cntZero largo largo = completo * (1LL)
largo tiempo extra = máx(0LL, rem - (1LL  observado b));
cntZero + extra;
}

/* ---- T(n) : sum of (j TENIDO K) over 0
largo largo largo calcT(largo largo n) {}
larga suma = 0;
para (incluido b = 0; (1LL 0)
cntZero largo = cerosInBit(n, b);
pares largos ConBit = n * n - cntZero * cnt Cero;
suma += paresConBit * (1LL  se realizó b);
}
restitución;
}

/* ---- suma total del 3‐ D array for size n ---- */
larga duración total(largo largo n) {}
largo t = calcT(n);
larga larga coeff = n * (n - 1) / 2; //
devolver t * coeff;
}

public:
int maxSized Array(long long s) {}
largo lo = 1, hola = 1;
mientras (total(hi)
mientras (lo cautivado) {
largo largo medio = (lo + hola) / 2;
si (total(mid) <= s) lo = medio + 1;
más hola = medio;
}
retorno (int)(lo - 1);
}
};

--------- Conductor (opcional) ---------- */
int main() {}
ios::sync_with_stdio(false);
cin.tie(nullptr);
long s;
si {}
cout se realizó Solution().maxSizedArray(s)
}
retorno 0;
}
`` `

-...

## 6. Casos de prueba

TEN TERRITOR ANTERIOR ANTERIOR
Silencio...
Silencio `5` Silencio `1`
Silencioso
Silencio
TENIDO `1000000000000000000` TENIDO `2000000` (con límite máximo para la entrada)

Siéntete libre de pegar cualquiera de los fragmentos en tu IDE y prueba más.



-...

## 6. Preguntas frecuentes

Respuesta a la respuesta
Silencio...
Silencio **¿Por qué no usar un bucle doble ingenuo?** Silencio La suma interna `T(n)` crece cuadráticamente; un bucle ingenuo O(n2) sería demasiado lento para `n Ω 106`. Silencio
Silencio **¿Necesitamos grandes enteros?** tención 64-bit (`long') basta porque el valor intermedio más grande está por debajo de 1018, cómodamente dentro firmado 64-bit. Silencio
Silencio **¿Podemos usar la fórmula del período en Python?** Silencio Sí – Los enteros de precisión arbitraria de Python hacen que el cálculo sea seguro. Silencio
Silencio **¿Y si `s` es 0?** Silencio El problema garantiza `s ≥ 1`; de lo contrario la respuesta sería `0`. Silencio
TEN **¿Es el algoritmo estable para muy grande `s`?** ANTE Duplicar el límite superior garantiza que la búsqueda binaria comienza con un rango correcto; el algoritmo funciona hasta el límite de 64 bits. Silencio

-...

## 7. Pensamientos finales

La información clave es que ** cada bit se comporta independientemente** y sigue un patrón periódico simple.
Al explotar esta estructura, reducimos un aparentemente pesado 3‐ D problema a un puñado de operaciones logarítmicas, permitiendo una elegante solución binaria de investigación que es provablemente correcta y a la vez rápida.



-...

## 8. Referencias

- El método bit-pattern periódico es un truco estándar utilizado en problemas que implican sumas bitwise OR/AND (ver, por ejemplo, “Sum of AND/OR de todos los pares” en LeetCode).
- La búsqueda binaria de monotone es una técnica algorítmica clásica para encontrar condiciones de límites en un predicado ordenado o monotone.



-...

## 9. TL;DR

1. **Compute `T(n)`** – sum of `(j OR k)` – iterating over bits.
2. **Compute total sum** with the closed‐form `total(n) = T(n) * (n-1)n/2`.
3. **Binary‐search** the maximum `n` with `total(n) ≤ s`.

Todos los pasos se ejecutan en `O(log n)2) tiempo y `O(1)` espacio, dando una solución rápida y correcta en Java, Python, y C++.



-...

¡Feliz codificación