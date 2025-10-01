-...
Título: LeetCode 3334. Encontrar el Factor Máximo Puntuación de Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 3334 – “Encuentra el Factor Máximo Puntuación de Array”
*Un problema de LeetCode Medium convertido en una estrella de interrevisión laboral. *

-...

## Tabla de contenidos
1. [Problema Recap](#problema-recap)
2. [Por qué importa para las entrevistas](#why-it-matters)
3. [Intuición " Casos de borde](#intuición)
4. [Brute‐Force vs. Optimal Approach](#approaches)
* 4.1. Brute‐Force (O(n2))
* 4.2. Prefix/Suffix GCD " LCM (O(n))
5. [Time & Space Complexity](#complexity)
6. [Implementación en tres idiomas](#implementaciones)
* Java
* Python
* C++
7. [Testing the Solution](#testing)
8. [Bueno, malo y lleno del problema] (#bueno-bad-ugly)
9. [Wrap-Up & Job‐Ready Tips](#wrap-up)
10. [SEO " Keywords](#seo)

-...

## Problema Recapitular ## Nombre="problema-recap"

■ **Given an integer array `nums` (1 ≤ nums.length ≤ 100, 1 ≤ nums[i] ≤ 30),**
■ **Remove a la mayoría de un elemento para maximizar el “punto del factor” del array restante**
■ Donde
√ ** puntuación del factor = GCD(todos los elementos restantes) × LCM(todos los elementos restantes). #
■
■ Devuelve esa puntuación máxima.
■ Nota: GCD & LCM de un solo elemento son el elemento en sí; un array vacío da la puntuación 0.

-...

## ¿Por qué importan las entrevistas?

LeetCode 3334 es una pregunta de entrevista clásica** porque prueba:

Por qué importa
Silencio...
Silencio **Teoría del número** ¦ Entendiendo las propiedades de GCD & LCM, protección de la desbordación
Silencio ** Programación dinámica / prefix‐suffix** Silencio Construyendo soluciones eficientes para problemas de “remove uno”
Silencio **Análisis de la complejidad** Silencio Proving O(n) vs. O(n2) Silencio
Silencio **Estilo de codificación** latitudes limpias, reutilizables utilidades GCD/LCM

Si usted clavó este problema, usted mostrará reclutadores que usted puede:

- Traducir una definición matemática en código
- Optimize brute‐force to linear time
- Casos de borde de mano con gracia

-...

## Intuición " Casos de bordes " significa un nombre=intuición "

* La puntuación factorial de toda la matriz es nuestra base de referencia.
* La eliminación de un elemento puede cambiar tanto el GCD como el LCM, a veces drásticamente.
* Debido a que `nums[i] ≤ 30`, LCM nunca supera 230 (~1 B) cuando se combina con GCD (que es al menos 30), por lo que un entero de 64 bits ( ' largo ' ) es seguro.
* Casos de borde:
* Longitud del rayo = 1 → quitar nada es óptimo; puntuación = `x2`.
* Array contiene todos los 1’s → GCD = 1, LCM = 1 → puntuación = 1.
* Eliminación de cualquier elemento cuando todos los números son iguales deja el mismo GCD/LCM.

-...

## Brute‐Force vs. Optimal Approach #1 name="approaches"

### 4.1 Brute‐Force (O(n2))

Computa GCD/LCM para cada subconjunto que excluye en la mayoría de un elemento.

``pseudo
maxScore = 0
para mí en [-1 ... n-1]: // -1 significa "remover nada"
corrienteGCD = 0
actualLCM = 1
para j in [0 ... n-1]:
si j == i: continuar
corrienteGCD = gcd GCD, nums[j])
currentLCM = lcm(currentLCM, nums[j])
maxScore = max(maxScore, currentGCD * currentLCM)
`` `

**Pros:** Sencillo, sin estructuras de datos adicionales.
**Cons:** Tiempo O(n2); no ideal si `n` fuera grande.

### 4.2 Prefix / Suffix GCD " LCM (O(n))

La observación clave: GCD/LCM del array sin elemento `i` iguala el **prefijo hasta `i‐1` combinado con el sufijo después de `i`**.

1. Precompute
* `prefGCD[k]` = GCD of `nums[0 ... k] `
* `prefLCM[k]` = LCM of `nums[0 ... k] `
* `sufGCD[k]` = GCD of `nums[k ... n‐1] `
* `sufLCM[k]` = LCM of `nums[k ... n‐1] `

2. Por cada índice:
* `gcdSinI = gcd(prefGCD[i-1], sufGCD[i+1])` (fronteras)
* `lcmSinI = lcm(prefLCM[i-1], sufLCM[i+1])`
* `score = gcdSinI * lcmSinI `

3. Considere también el caso de “sin eliminación” (score de toda la matriz).

**Por qué funciona* *
GCD and LCM are associative and commutative:
gcd(a,b,c) = gcd(gcd(a,b),c) y similarly for LCM.
Así se puede construir la matriz sin un elemento combinando las dos mitades.

**Las complejidades* *
* Tiempo: O(n)
* Espacio: O(n) (cuatro arrays auxiliares)

-...

## Time & Space Complexity > ## Time > Space Complexity

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
Silencio Brute‐Force Silencio **O(n2)** Silencio **O(1)**
Silencioso Prefix/Suffix **O(n)** Silencio **O(n)**

Dada las limitaciones (`n ≤ 100'), ambos pasan cómodamente.
Sin embargo, los entrevistadores a menudo esperan la solución de tiempo lineal.

-...

## Implementación en tres idiomas = nombre= "implementaciones"

A continuación se encuentran soluciones limpias y autocontenidas para Java, Python y C++.

■ **Consejo:** La función GCD está integrada en Java (`java.math.BigInteger.gcd`) y Python (`math.gcd`). En C++ utilizamos `std::gcd` de `traducidonumeric ``.

-...

### 1. Java (Java 17)

``java
importar java.util*;

Solución de la clase pública {}
privada estática larga gcd(long a, long b) {}
mientras (b!= 0) {
t largo = un % b;
a = b);
b = t;
}
devolver a;
}

privada estática larga lcm(long a, long b) {}
si (a == 0 Silencioso 0) retorno 0;
devolver un / gcd(a, b) * b; // dividir primero para evitar el desbordamiento
}

public long maxScore(int[] nums) {
int n = nums.length;
si (n == 1) retorno (long) nums[0] * nums[0];

long[] prefGcd = new long[n];
largo[] prefLcm = nuevo largo[n];
long[] sufGcd = new long[n];
long[] sufLcm = new long[n];

[0] = nums[0];
prefLcm[0] = nums[0];
para (int i = 1; i) {}
prefGcd[i] = gcd(prefGcd[i - 1], nums[i]);
prefLcm[i] = lcm(prefLcm[i - 1], nums[i]);
}

sufGcd[n - 1] = nums[n - 1);
sufLcm[n - 1] = nums[n] - 1);
para (int i = n - 2; i 0; i--) {
sufGcd[i] = gcd(sufGcd[i + 1], nums[i]);
sufLcm[i] = lcm(sufLcm[i + 1], nums[i]);
}

long best = prefGcd[n - 1] * prefLcm[n - 1]; // no removal

para (int i = 0; i)
long g = (i == 0) ? sufGcd[1] : (i == n - 1) ? prefGcd[n - 2] : gcd(prefGcd[i - 1], sufGcd[i + 1]);
long l = (i == 0) ? sufLcm[1] : (i == n - 1) ? prefLcm[n - 2] : lcm(prefLcm[i - 1], sufLcm[i + 1]);
mejor = Math.max(best, g * l);
}
devolver mejor;
}

// controlador para cheque de cordura rápido ---
public static void main(String[] args) {
Solución s = nueva solución ();
System.out.println(s.maxScore(new int[]{2,4,8,16})); // 64
System.out.println(s.maxScore(new int[]{1,1})); // 1
System.out.println(s.maxScore(new int[]{5})); // 25
}
}
`` `

-...

### 2. Python (Python 3.10)

``python
importar matemáticas
de la importación Lista

Solución de clase:
def maxScore(self, nums: List[int] int:
n = len(nums)
si n == 1:
nums[0] * nums[0]

pref_gcd = [0]
* n
Suf_gcd = [0]
[0] * n

pref_gcd[0] = pref_lcm[0] = nums[0]
para i en rango(1, n):
pref_gcd[i] = math.gcd(pref_gcd[i - 1], nums[i])
pref_lcm[i] = pref_lcm[i - 1] // math.gcd(pref_lcm[i - 1], nums[i]) * nums[i]

suf_gcd[-1] = suf_lcm[-1] = nums[-1]
para i en rango(n - 2, -1, -1):
suf_gcd[i] = math.gcd(suf_gcd[i + 1], nums[i])
suf_lcm[i] = suf_lcm[i + 1] // math.gcd(suf_lcm[i + 1], nums[i]) * nums[i]

mejor = pref_gcd[-1] * pref_lcm[-1] # no removal

para i en rango(n):
g = suf_gcd[1] si l == 0 otro pref_gcd[n] - 2] if i == n - 1 else math.gcd(pref_gcd[i - 1], suf_gcd[i + 1])
l = suf_lcm[1] si l == 0 other pref_lcm[n - 2] if i == n - 1 else (pref_lcm[i - 1] // math.gcd(pref_lcm[i - 1], suf_lcm[i + 1]) * suf_lcm[i + 1])
mejor = max(best, g * l)

mejor

# Pruebas manuales rápidas
si __name_ == "__main__":
s = Solución()
print(s.maxScore([2,4,8,16])) # 64
print(s.maxScore([1,1]) # 1
print(s.maxScore([5]) # 25
`` `

-...

### 3. C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
long long gcdll(long long a, long long long b) {}
(b) { long t = a % b; a = b; b = t; }
devolver a;
}

largo largo lcmll(long long a, long long long b) {}
si (a == 0 Silencioso 0) retorno 0;
devolver a / gcdll(a, b) * b; // dividir primero
}

largo tiempo maxScore(vector interpretadoint círculo nums) {
int n = nums.size();
(n ==1) devolver 1LL * nums[0] * nums[0];

vector llevado a cabo larga duración prefGcd(n), prefLcm(n), sufGcd(n), sufLcm(n);

prefGcd[0] = prefLcm[0] = nums[0];
para (int i = 1; i) {}
prefGcd[i] = gcdll(prefGcd[i-1], nums[i]);
prefLcm[i] = lcmll(prefLcm[i-1], nums[i]);
}

sufGcd[n-1] = sufLcm[n-1] = nums[n-1];
para (int i = n-2; i 0; --i) {
sufGcd[i] = gcdll(sufGcd[i+1], nums[i]);
sufLcm[i] = lcmll(sufLcm[i+1], nums[i]);
}

long long best = prefGcd.back() * prefLcm.back(); // no removal

para (int i = 0; i) {}
long g = (i == 0) ? sufGcd[1] : (i == n-1) ? prefGcd[n-2] : gcdll(prefGcd[i-1], sufGcd[i+1]);
largo l = (i == 0) ? sufLcm[1] : (i == n-1) ? prefLcm[n-2] : lcmll(prefLcm[i-1], sufLcm[i+1]);
mejor = max(best, g * l);
}
devolver mejor;
}
};
`` `

-...

## Testing the Solution ## Testing the Solution

``bash
# Java
javac Solution.java
Java Solution
# Python
solución python3. py
# C++
g++ -std=c+17 -O2 solution.cpp -o sol
./sol
`` `

Entradas de muestra (puede copiar-pasar en un arnés de prueba):

← Intromisión esperada
Silencio...
TENIDA `[2,4,8,16]
TENIDA `[1,1,1]
Silencioso[5]
TENIDA `[4,4]
TENIDO `[3,6,9]` TENIDO `18` (remove 9 → GCD = 3, LCM = 6, score = 18)

-...

## Good, Bad, and Ugly of the Problem > ## Good, Bad, and Ugly of the Problem

Silencio Silencio
Silencio------------Prince------
Silencio **Matemática claridad** Silencio La definición es *limpio* y autoexplicativo. ← GCD/LCM puede ser confuso para candidatos pesados no pequeños. ← Sobre-ingeniería: tratar de pre-computar cada sub-array posible. Silencio
Silencio **Pasa de optimización** ← Prefix/suffix truco directo. Muchos entrevistadores esperan que “vea la asociación” rápidamente. Silencioso incomprendido que LCM es *no* linearizable puede llevar a la aceptación O(n2). Silencio
Silencio **El riesgo de flujo** tención 64 bits enteros son seguros aquí. Algunas soluciones se olvidan de dividir antes de multiplicarse en LCM. Silencio Olvidando que `a*b` puede rebosar *incluso para pequeños a,b* en idiomas sin soporte integrado de 128 bits. Silencio
Silencio **Testing** Silencio Pruebas de unidad sencillas suficiente. ← Casos de borde con un solo elemento o todos a menudo se pierden. El caso de “sin eliminación” que se pierde lleva a una respuesta incorrecta por `[1] o `[30]. Silencio

-...

## Wrap‐Up " Job‐Ready Tips " se hizo un nombre= "wrap-up"

1. **Comienza con el boceto de fuerza bruta** – aclara el espacio problemático.
2. **Piensa en “remover uno” como “prefijo + sufijo”** – un patrón que aparece en muchos problemas de matriz (por ejemplo, “Maximum Subarray After Deleting One Element”).
3. **Auxiliadores reutilizables Write GCD/LCM**; utilice funciones integradas cuando sea posible.
4. **Test on edge cases** (length = 1, all 1’s, all same, mixed small/large).
5. **Explicar su intuición en voz alta** durante una entrevista; los reclutadores se preocupan por su proceso de pensamiento tanto como el código final.

■ *Si puede implementar 3334 en menos de 30 segundos, es probable que esté listo para abordar otros medios LeetCode (por ejemplo, 1646, 1461, 1519) con confianza. *

-...

## SEO > Palabras claves > > >

*LeetCode 3334*
- Encontrar el Factor Máximo Puntuación de Array
- GCD LCM problema de eliminación de array
- Manipulación lineal a tiempo
- Problema de entrevista de teoría de números
- Java/Python/C++ Soluciones LeetCode
- Problemas de preparación de entrevistas
- Preguntas sobre algoritmos de entrevista de trabajo

Agregue las etiquetas anteriores a su blog, GitHub repo, o cartera para aumentar la visibilidad entre los reclutadores que buscan desafíos de “LeetCode Medium”, “Teoría de los nanos”, o “Manipulación de los rayos”.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀