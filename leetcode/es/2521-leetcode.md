-...
Título: LeetCode 2521. Factores Prime distintos del producto de Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Problema Recap
**2521. Factores Prime distintos del producto de Array* *
Dado un array `nums` de números enteros positivos (`2 ≤ nums[i] ≤ 1000`), devuelve el número de **distintos** factores principales que aparecen en el producto de todos los elementos.

■ *Examples*
■ *Input*: `[2,4,3,7,10,6]` → ** Producto**: `4` (factores: 2, 3, 5, 7)
■ * Input*: `[2,4,8,16]` → ** Producto**: `1` (factor: 2)

El sencillo “multiply todos los números y factor el producto” se desborda al instante. El truco es factorar cada elemento *individualmente* y combinar los resultados en un conjunto de primos.

-...

¿Por qué este blog?
- **SEO-friendly** palabras clave: *leetcode 2521, distintos factores principales, array product, Java solution, Python solution, C++ solution*
- Cubiertas **Bien**, **Bad**, y **Ugly** aspectos de enfoques comunes
- Le ayuda a destacar en entrevistas técnicas y entrevistas de codificación

-...

Solución Optimal – Sieve + Factorización

### Por qué funciona
* El número máximo posible en la matriz es sólo 1 000, por lo que todos los factores principales son ≤ 1000.
* Pre-compute todos los primos hasta 1 000 con el Sieve de Eratosthenes (O(√1000)).
* Por cada número que dividimos por cada primo hasta que ya no se puede dividir.
* A `HashSet` (Java), `set` (Python), or `unordered_set` (C++) collects the unique primes.

### Complexity
TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
Silencio **Hora** Silencioso `O(n * π(1000) ♥ O(n * 168)` Silencio `O(n * π(1000)' Silencio
tención **Espacio** Silencioso `O(π(1000)` (conjunto de primos)

-...

##  Settlement Code in Three Languages

#### ## 1down⃣ Java – Clean " Idiomatic

``java
importar java.util*;

Solución de la clase pública {}
// Pre-computados primos hasta 1000
privada estática final lista hecha PRIMES = sieve(1000);

Lista estática privada realizadaInteger confianza sieve(limite único) {
boolean[] isPrime = nuevo booleano[limit + 1];
Arrays.fill(esPrime, true);
isPrime[0] = isPrime[1] = false;
para (int p = 2; p * p = límite = p++) {}
si (esPrime[p]) {}
para (int k = p * p; k == limit; k += p) {}
isPrime[k] = false;
}
}
}
Lista realizadaInteger Principals = nuevo ArrayList correctamente();
para (int i = 2; i) = límite; i++) {}
(isPrime[i]) primes.add(i);
}
devolver primos;
}

public int distinct PrimeFactors(int[] nums) {
Establecer:Integer título únicoPrimes = nuevo HashSet fiel();
para (int val : nums) {
factor(val, uniquePrimes);
}
retorno únicoPrimes.size();
}

factor de vacío privado (en el punto num, Conjunto) {
para (int p : PRIMES) {
si (p * p * p > num) romper;
(num % p == 0) {
result.add(p);
(num % p == 0) num /= p;
}
}
si 1) { // restante
result.add(num);
}
}
}
`` `

■ **Bueno** – Reutiliza una lista de primeros pre-computados, O(1) factor Lookup.
■ **Bad** – Usa `ListectoInteger `` para primos; un `int[]` sería ligeramente más rápido.
■ **Ugly** – No hay inicializador estático para el tamiz; cada objeto `Solución' lo recompone si no `estático`. El código anterior declara que es 'estático' evitar esto.

-...

Python - Concise & Pythonic

``python
de la importación de matemáticas isqrt
de la importación Lista

# Pre-compute primos hasta 1000
def sieve(limit: int) - título List[int]:
is_prime = [True] * (limit + 1)
is_prime[0] = is_prime[1] = False
para p en rango(2, isqrt(limit) + 1):
si es_prime[p]:
para k en rango(p * p, límite + 1, p):
is_prime[k] = False
[i for i, v in enumerate(is_prime) if v]

PRIMES = sieve(1000)

Solución de clase:
def distinct PrimeFactors(self, nums: List[int]) - int:
único = set()
para las numidades:
self._factor(num, unique)
len(unique)

def _factor(self, num: int, unique: set) - Ninguno.
para p en PRIMES:
si p * p * p > num:
descanso
si num % p == 0:
único.add(p)
mientras que num % p == 0:
num //= p
si num 1:
único.add(num)
`` `

■ **Bien** – Leverages Python’s `set` y lista de comprensión.
■ **Bad** – El tamiz se recomienda cada vez que se importa el módulo (pero está bien para LeetCode).
■ **Ugly** – El código todavía se remonta a *todas* prima hasta 1000 para cada número, incluso si `num` es pequeño. Un enfoque más inteligente se detendría una vez `num == 1`.

-...

### 3down⃣ C++ – orientada al rendimiento

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
privado:
vector estático:

vector estático implicado construirPrimes(limite único) {
vector asignadobool confianza esPrime(limit + 1, true);
isPrime[0] = isPrime[1] = false;
para (int p = 2; p * p = límite = ++p)
si (esPrime[p])
para (int k = p * p; k == limit; k += p)
isPrime[k] = false;
vectoriales:
para (int i = 2; i) = límite; ++i)
si (esPrime[i]) primes.push_back(i);
devolver primos;
}

public:
int distinctPrimeFactors(vector fielint limitada nums) {
unordered_set se realizó uniq
para (int val : nums) {
factor(val, uniq);
}
devolver uniq.size();
}

privado:
factor de vacío(int num, unordered_set) {
para (int p : primes) {
si (p * p * p > num) romper;
(num % p == 0) {
uniq.insert(p);
(num % p == 0) num /= p;
}
}
si (num ≤ 1) uniq.insert(num);
}
};

vector Solución::primes = Solución::buildPrimes(1000);
`` `

■ **Bueno** – Usa el miembro estático para construir los primos una vez, compartido en todas las instancias.
■ **Bad** – El encabezado `bits/stdc++.h` no es estándar pero conveniente en LeetCode.
■ **Ugly** – El "noordered_set" puede re-hash si el número de primos únicos crece; en la práctica esto es insignificante.

-...

## 🔍 El Bien, el Mal, y el Ugly

← Subtítulos Lo que te va a encantar _ Lo que te va a sudar sobre la vida Evitar en todos los costos Silencio
Silencio------------------------------------------
Silencio **Bien** Silencio • Los primos pre-computados evitan la división de prueba repetida. • Set/HashSet garantiza la singularidad en O(1). • Linear en `n` y trivial en la práctica.
Silencio **Bad** Silencio • Algunas soluciones re-factorizan los mismos principios para cada elemento (cosa pero todavía) se realizaron 2 000 operaciones. • Usando `Set` puede asignar muchos objetos pequeños en Java/Python. Silencio • Re-computing sieve per instance (Java) <br título• Precoces generales (hasta 10 000) cuando 1 000 suffices (Python).
Silencio **Ugly** Silencio – Silencio – Silencio • Multiplying the whole array (overflow). • Dividir Recursivamente sin una condición de descanso. • Guardar el producto completo en un factoring largo y largo (riesgo de exceso). Silencio

-...

## 📚 Quick‐Start Cheat Sheet

``text
1. Construir lista de primos hasta 1000 (Espejo de Eratosthenes).
2. Para cada número de nums:
a. Para cada p primitiva:
i. Si p * p * p > num → romper.
ii. Si num % p == 0: add p to set; divide num by p hasta que no sea divisible.
b. Si num ≤ 1: añadir num (el primo restante) para establecer.
3. Set.size().
`` `

-...

## 🎯 Why This Blog Helps Your Job Hunt

1. **Keyword‐rich Title & Headings** – Los motores de búsqueda lo marcan para *leetcode*, *distinct prime factors*, *Java/Python/C+*.
2. **Clear, paso a paso código snippets** – El equipo puede copiar y ejecutar al instante.
3. **Deep dive into pitfalls** – Te muestra no sólo la respuesta correcta sino por qué no deberías hacerlo de esa manera.
4. **Seo-friendly meta-descripción** – Corto, pegajoso, y empaquetado con términos relevantes.
5. **Formato profesional** – bloques de código, tablas y una narrativa limpia hacen que el artículo parezca pulido.

■ **Descripción de los datos (consignación de 150 créditos)* *
■ *Solve LeetCode 2521 – Distintos Prime Factors of Product of Array. Java, Python, C++ code, analysis of good/bad/ugly approaches, and interview-ready explanations. *

-...

Llamado a Acción

■ ¿Quieres empezar tu próxima entrevista de codificación?
≤ - **Descargar** el repo GitHub con las tres soluciones.
*Clone* y haz las pruebas.
√≥ - **Compartir** este post en LinkedIn/Dev.to y dejar que los reclutadores vean su estilo de solución de problemas!

¡Feliz codificación! 🚀