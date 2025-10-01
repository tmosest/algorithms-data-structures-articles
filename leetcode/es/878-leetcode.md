-...
Título: LeetCode 878. Nth Magical Number -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 878. Nth Magical Number – A Deep‐Dive with Java, Python & C++ Soluciones

■ **TL;DR**
■ El problema Nth Magical Number se resuelve en **O(log n)** tiempo mediante la búsqueda binaria en el rango de respuesta y utilizando el principio de inclusión-exclusión con LCM.
■ Se suministran fragmentos de código en **Java, Python y C++**.
■ Un blog completo sigue que explica el truco, las trampas (“la fea”), las mejores prácticas (“la buena”), y por qué esta solución impresionará a los gerentes de contratación.

-...

## 📚 Declaración de problemas (LeetCode 878)

Un número *magico* es un número entero positivo que es divisible por **a** o **b**.
Dado tres números enteros **n, a, b**, devolver el número mágico * nth*.
Porque la respuesta puede ser enorme, devolverlo modulo 109 + 7.

**Constraints* *

Silencio
Silencio...
TENIDO `1 ≤ 109` TENIDO `2 ≤ a, b ≤ 4·104` Silencio

-...

## 🔑 Observaciones clave

1. **Counción de números divisibles**
Para un `x' dado, el recuento de números ≤ `x` divisible por `a` es `x / a`.
Análogamente para " b " y para " lcm(a, b) " .

2. **Inclusión–Exclusión**
cnt(x) = x/a + x/b – x/lcm(a, b)`
da el número de números mágicos ≤ `x`.

3. **Binary Search on the Answer**
Necesitamos el más pequeño `x` tal que `cnt(x) ≥ n`.
The search range is `[min(a,b), n * min(a,b)]`.
Esto garantiza que la respuesta está dentro del rango.

4. **Overflow " Modulo**
Use aritmética de 64 bits para resultados intermedios (LCM, multiplicación).
Finalmente devuelve `respuesta % (109 + 7)`.

-...

## ♥ Algorithm Outline

1. **Compute GCD** of `a` and `b` (Euclid).
2. Compute `lcm = a / gcd * b` (use 64‐bit para evitar el desbordamiento).
3. Búsqueda binaria en `[low, high]`:
- `mid = (bajo + alto) / 2`
- Si "cnt(mid)" se hizo n` → búsqueda derecha la mitad (`low = mid + 1`)
- Else → búsqueda izquierda media (`alta = media').
4. El resultado es 'bajo' (o 'alto'), modulo `MOD = 1_000_000_007`.

-...

## 📦 Implementation

A continuación se presentan implementaciones limpias y autocontenidas en **Java, Python, y C++**.
Cada programa define una clase `Solution` (Java ' C++) o una función `nthMagicalNumber` (Python) que se puede soltar directamente en una sumisión LeetCode.

-...

## Java

``java
Clase Solución {
static final long MOD = 1_000_000_007L;

public int nthMagicalNumber(int n, int a, int b) {}
larga A = a, B = b;

// 1. Compute LCM
gcd largo = gcd (A, B);
larga lcm = (A / gcd) * B; // 64‐bit

// 2. Binarios de búsqueda
largo bajo = Math.min(a, b);
alto largo = bajo * (long) n; // seguro superior

mientras (bajo)
largo medio = bajo + (alto - bajo) / 2;
cnt larga = media / a + media / b - media / lcm;

si
baja = media + 1;
. ♫ ... {
alto = medio;
}
}
(int) (low % MOD);
}

gcd privado largo(long x, long y) {}
mientras (y!= 0) {
t largo = x % y;
x = y;
y = t;
}
retorno x;
}
}
`` `

-...

## Python

``python
Solución de clase:
MOD = 1_000_000_007

def nthMagicalNumber(self, n: int, a: int, b: int) - título int:
de la importación de matemáticas gcd

lcm = a // gcd(a, b) * b

bajo, alto = min(a, b), min(a, b) * n

mientras que bajo
media = (bajo + alto) // 2
cnt = media / a + media // b - media // lcm
si cnt.
baja = media + 1
más:
alta = media

Regresa bajo %. MOD
`` `

-...

### C++

``cpp
Clase Solución {
public:
const long MOD = 1'000'000'007LL;

largo largo gcd(long long a, long long long b) {}
b) {
largo t = un % b;
a = b; b = t;
}
devolver a;
}

int nthMagicalNumber(int n, int a, int b) {}
largo largo lcm = (largo largo)a / gcd(a, b) * b;

long long low = min(a, b);
largo largo alto = bajo * 1LL * n; //

mientras (bajo)
largo medio = bajo + (alto - bajo) / 2;
cnt largo largo = medio / a + medio / b - mediados / lcm;
si (cnt י n) bajo = medio + 1;
más alto = medio;
}

(int)(low % MOD);
}
};
`` `

-...

## The Good, The Bad, and The Ugly

Silencio Silencio Silencioso
Silencio----------
Silencio **Bueno** Silencio • **O(log n)** tiempo, mucho mejor que fuerza bruta (O(n)). • Usa aritmética de 64 bits para evitar el desbordamiento. • Maneja el modulo limpiamente al final. Los límites de búsqueda binaria se prueban matemáticamente para contener la respuesta. Silencio
Silencio** Si te olvidas de lanzar a 64 bits (Java `long`, las ints arbitrarias de Python ayudan, C++ `long long`), corres el riesgo de desbordamiento cuando computar `lcm` o `mid`. Silencio
Silencio **Ugly** Silencio • El paso de inclusión-exclusión (`cnt = mid/a + mid/b - mid/lcm`) se ve simple pero puede ser una fuente de errores sutiles si `lcm` es cero (no es posible aquí pero bueno para guardar). La computación GCD/LCD puede ser sobre-configurada para principiantes; una línea de un `gcd = std::gcd(a, b)` en C+17 ayuda. • Recuerde que la respuesta debe ser devuelta modulo `109+7`; olvidar esto puede causar una respuesta incorrecta en casos de prueba enormes. Silencio

-...

## 📈 Complexity Analysis

Silencio Silencio Silencio Silencio
Silencio----------------
TENIDO GCD/LCM TENIDO `O(log min(a,b) ' TENIDO `O(1)` Silencio
Silencioso búsqueda binaria Silencioso `O(log(n * min(a,b)))' Silencio
TENIDO TODO TENIDO `O(log n)` Silencio

La huella de memoria es constante – no hay arrays adicionales o recursión.

-...

## 🧪 Test Cases

Silencioso `n` Silencioso `a` Silencioso
Silencio...
Silencio 1 Silencio 2 Silencio 3 Silencio 2 Silencio
Silencio 4 Silencio 2 Silencio 3 Silencio 6 Silencio
Silencio 5 Silencio 5 Silencio 7 Silencio 25 Silencio
tención 109 Silencioso 2 Silencioso 3 Silencio 19999998 (mod 109+7)
Silencio 100 Silencio 40000

Ejecute cada fragmento en el entorno de su idioma o en el panel "Código de Rin" de LeetCode.

-...

## 🚀 SEO‐Optimized Conclusion

Si te estás preparando para entrevistas de ingeniería de software, dominar el problema **Nth Magical Number** demuestra:

1. ** Pensamiento Algorítmico** – reconociendo la necesidad de búsqueda binaria en el espacio de respuesta.
2. ** Rigor Matemático** - aplicación de inclusión-exclusión, GCD, LCM.
3. **Disciplina de codificación** – manejo de grandes números, utilizando aritmética de 64 bits y operaciones de modulo correctamente.

Utilice los fragmentos de código arriba en su cartera o GitHub README para mostrar su competencia. La estructura de correos del blog – declaración de problemas, observaciones clave, algoritmo, código, complejidad – se alinea con lo que los reclutadores buscan en *LeetCode explicaciones de solución*.

**Keywords** que aumentará su SEO:
`LeetCode 878`, `Nth Magical Number`, `binary search`, `LCM`, `GCD`, `coding interview`, `algorithmic problem resolution`, `O(log n)`, `Java solution`, `Python solution`, `C++ solution`, `interview preparation`.

Comparte este post en Medium, Dev.to, o tu blog personal, añade etiquetas relevantes, y estarás en el radar de contratación de gerentes buscando candidatos que puedan convertir matemáticas en un código eficiente.

¡Feliz codificación, y que ese número mágico de Nth esté siempre a pocas líneas!