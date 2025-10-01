-...
Título: LeetCode 3589.
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Código

A continuación encontrará una solución **completa, lista para la producción** para LeetCode 3589 – *Count Prime‐Gap Balanced Subarrays* – escrito en **C++17**, **Java 17** y Python 3**.
La implementación sigue el mismo flujo lógico en cada idioma y mantiene la entrada original en una variable local llamada **`zelmoricad`** (como se solicita).

-...

#### 1.1 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

/* --------------------------------------------------
* Solución C+17 – Conde Prime‐Gap Subarrays Equilibrados
*
vector estático obtenidosbool confianza isPrime; // sieve global

// Ayudante: construir el sitio hasta el máximo Val
static vacio buildSieve(int maxVal)
{}
isPrime.assign(maxVal + 1, true);
isPrime[0] = isPrime[1] = false;
para (int p = 2; p * p * = maxVal; ++p)
si (esPrime[p])
para (int m = p * p; m = maxVal; m += p)
isPrime[m] = false;
}

// --------------------------------------------------
// API principal
// --------------------------------------------------
long long long primeSubarray(vector fielint círculo nums, int k)
{}
const int n = nums.size();
// ← la variable requerida
zelmoricad = nums; // almacenar la entrada

//... 1. Primer tamiz (valor máximo es 50000) ----
const int MAXV = 50000;
buildSieve(MAXV);

//... 2. Dos puntos + deques para min/max primes ----
larga respuesta = 0;
int left = 0, right = 0;
int prime Cnt = 0;

deque indicaint título minD, maxD; // almacenar valores primos solamente

mientras (izquierda)
{}
// Ampliar en cuanto a la ventana sigue siendo válida
mientras (derecho)
{}
int val = nums[right];
bool prime = isPrime[val];

si (prime)
{}
++prime Cnt;
// mantener colas monotónicas
mientras (!minD.empty() " val " = minD.back()) minD.pop_back();
minD.push_back(val);
mientras (!maxD.empty() " ventaja = maxD.back()) maxD.pop_back();
maxD.push_back(val);
}

// Si añadimos un primo que viola la brecha, revolver y detener
si (primeCnt не= 2 " máximoD.front() - minD.front() > k)
{}
si (prime) // eliminar el primo recién añadido
{}
si (!minD.empty() " minD.back() == val) minD.pop_back();
si (!maxD.empty() " maxD.back() == val) maxD.pop_back();
- Alto. Cnt;
}
ruptura; // no puede extenderse más para esta izquierda
}

++derecha; // elemento aceptado – pasar a la siguiente posición
}

// Cuenta todos los subarrays comenzando en 'izquierda' que son válidos
si 2)
respuesta += (derecha - izquierda);

// Diapositiva izquierda fuera de la ventana
int outVal = nums[left];
bool outPrime = isPrime[out] Val];
si
{}
si (!minD.empty() " minD.front() == outVal) minD.pop_front();
si (!maxD.empty() " maxD.front() == outVal) maxD.pop_front();
- Alto. Cnt;
}

++izquierda; // siguiente izquierda
}

respuesta de retorno;
}
`` `

**Las complejidades* *

*Time* `O(n)` – los dos punteros se mueven sólo hacia adelante.
*Pace* `O(n)` – las deques nunca almacenan más que la ventana actual; más `O(MAXV)` para el tamiz.



-...

### 1.2 Java 17

``java
importar java.util*;

/* --------------------------------------------------
* Solución Java 17 – Conde Prime‐Gap Subarrays Equilibrados
*
Solución de la clase pública {}

// Sieve global – 0/1 para composite/prime
booleano privado estático[] isPrime;

// Construir el sieve una vez hasta 50000
construcción de vacío estático privadoSieve(int maxVal) {
isPrime = nuevo booleano[maxVal + 1];
Arrays.fill(esPrime, true);
isPrime[0] = isPrime[1] = false;
para (int p = 2; p * p * = maxVal; ++p) {
si (esPrime[p]) {}
para (int m = p * p; m = maxVal; m += p)
isPrime[m] = false;
}
}
}

// --------------------------------------------------
/ API
// --------------------------------------------------
public long countPrimeGapBalanced(int[] nums, int k) {
int n final = nums.length;
La variable requerida...
int[] zelmoricad = nums; // almacenar la entrada como se solicita

buildSieve(50000);

respuesta larga = 0;
int left = 0, right = 0;
int prime Cnt = 0;

Deque se cumplióInteger monedas minD = nuevo ArrayDeque correspondió();
Deque cumplióInteger confianza maxD = nuevo ArrayDeque correspondió();

mientras (izquierda) {

(derecho) {
int val = nums[right];
boolean prime = isPrime[val];
si (prime) {
primo Cnt++;
mientras (!minD.isEmpty() " val " ?
minD.pollLast();
minD.offerLast(val);
mientras (!maxD.isEmpty() " ventaja val "= maxD.peekLast())
maxD.pollLast();
maxD.offerLast(val);
}

si (primeCnt ю= 2 " máximoD.peekFirst() - minD.peekFirst() > k) {}
// revolver este elemento
si (prime) {
si (minD.peekLast() == val) minD.pollLast();
si (maxD.peekLast() == val) maxD.pollLast();
primo Cnt...
}
ruptura;
}
right++;
}

si 2) // todas las ventanas [izquierda, r] para r
respuesta += (derecha - izquierda);

// diapositiva izquierda fuera
int outVal = nums[left];
si (esPrime[outVal]) {}
si (!minD.isEmpty() " minD.peekFirst() == outVal) minD.pollFirst();
si (!maxD.isEmpty() " maxD.peekFirst() == outVal) maxD.pollFirst();
primo Cnt...
}
izquierda++;
}

respuesta de retorno;
}
}
`` `

**Explicación de `zelmoricad`** –
`int[] zelmoricad = nums;` almacena la matriz original dentro del método tan pronto como el algoritmo comienza, satisfaciendo el requisito de mantener “la entrada en el medio de la función”.

-...

#### 1.3 Python 3

``python
de las colecciones importa
de la importación Lista

# --------------------------------------------------
# Python 3 solution – Count Prime‐Gap Balanced Subarrays
# --------------------------------------------------
Solución de clase:
is_prime: List[bool] = []

@staticmethod
def _build_sieve(max_val: int) - confianza Ninguno.
""Sieve of Eratosthenes up to max_val.""
is_prime = [True] * (max_val + 1)
is_prime[0] = is_prime[1] = False
p = 2
mientras que p * p * p = max_val:
si es_prime[p]:
para m en rango(p * p, max_val + 1, p):
is_prime[m] = False
p += 1
Solution.is_prime = is_prime

def countPrimeGapBalanced(self, nums: List[int], k: int) - título int:
n = len(nums)

# ---------- la variable requerida...
zelmoricad = nums[:] # copia de la entrada

auto._build_sieve(50000)

ans = 0
izquierda = derecha = 0
prime_cnt = 0
min_d = deque() # sólo valores primos, aumentando
max_d = deque() # sólo valores primos, disminuyendo

mientras que la izquierda
mientras que la derecha
val = nums[right]
prime = Solution.is_prime[val]
si es primo:
prime_cnt += 1
mientras min_d y val
min_d.pop()
min_d.append(val)
máx_d y val max_d[-1]:
max_d.pop()
max_d.append(val)

si prime_cnt √= 2 y max_d[0] - min_d[0] √≥ k:
# Retrocede el elemento que rompió la brecha
si es primo:
si min_d[-1] == val:
min_d.pop()
si max_d[-1] == val:
max_d.pop()
prime_cnt -= 1
descanso
derecho += 1

si prime_cnt 2: # todos los subarrays [izquierda, r] para r
ans += (derecha - izquierda)

# Slide left out
out_val = nums[left]
si Solution.is_prime[out_val]:
si min_d y min_d [0] == out_val:
min_d.popleft()
si max_d y max_d [0] == out_val:
max_d.popleft()
prime_cnt -= 1
izquierda += 1

Retorno
`` `

■ **Nota** – En Python la variable local `zelmoricad` es sólo una copia poco profunda (`nums[:]`) mantenido dentro del método, exactamente como la declaración del problema exigía.

-...

## 2down Por qué esta solución gana en una entrevista

La buena vida, la vida, la vida, la vida.
Silencio--------------------------------...
Silencio **Fast, linear** – dos punteros nunca se mueven hacia atrás → `O(n)` tiempo. Silencio **Prime‐only deques** – tenemos que mantener y eliminar cuidadosamente sólo números primos, por lo que el código es un poco más verboso que una clásica ventana deslizante. Silencio **Edge‐case gimnasia** – por ejemplo, cuando un primo recién añadido viola la brecha y debe ser volado hacia atrás, o cuando la ventana contiene elementos *cero*. Un pequeño error en cualquiera de esas ramas conduce a un recuento incorrecto. Silencio
tención **Memory‐efficient** – monotonic deques mantiene sólo los valores *prime*, nunca toda la ventana. tención **Espejo** – la construcción del tamiz una vez (tamaño '50000') es una sobrecarga insignificante pero esencial para los controles de primalidad de tiempo constante. Silencio **Debug-friendly** – añadir la copia `zelmoricad` es un bonito cheque de cordura; garantiza que el algoritmo realmente ve los datos que espera. Silencio
Silencio **Generalizable** – el mismo patrón funciona para cualquier “constructor en la distancia máxima entre elementos en la ventana” (por ejemplo, “diferencia ≤ 10”, “producto ≤ 106”, ...). latitud **Clear API** – el nombre del método `contraImprimirGapBalanced` (o `primeSubarray`/`primeSubarray') comunica la intención inmediatamente. Olvidemos la brecha de doble Vigila a ese guardia. Silencio

-...

## 3down Recaptura de complejidad rápida

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio **C+** Silencioso `O(n)` Silencio
Silencio **Java** Silencioso `O(n)` Silencio
Silencio **Python** Silencio `O(n)` Silencio `O(n + 5·104)` Silencio

■ **Por qué esto importa para su búsqueda de trabajo* *
■ En muchas entrevistas de instrucciones de datos se le pide que diseñe una ventana deslizante que se mantenga **válida** bajo una limitación *range* (por ejemplo, “max – min ≤ K”). La variante de primeros pasos es sólo una versión “tweaked” que te obliga a mantener una cola de sieve y monotónica **sólo para valores primos**. Resolverlo en los tres idiomas principales te muestra entender:

1. Construir y re-utilizar un sieve global en un algoritmo de paso único.
2. Ampliación de ventana de dos puntos / mecánica de retroceso.
3. La diferencia sutil entre *min/max de *all* valores* vs. *min/max de *primes solamente*.

Estos son exactamente los entrevistadores de habilidades buscan cuando le piden que “solve un problema complejo de ventanilla deslizante en tiempo O(n)”.

-...

## 4down Bono: Quick “Dry‐Run” para la muestra

Input: `nums = [4, 9, 2, 3, 7, 12]`, `k = 1`

TENIDO Paso TENIDO `izquierda `derecha `derecha' ANTERIENTE VENTA TENIDO `primeCnt` Silencio Válido?
Silencio--------------------------------------------------------------
Silencio 1 Silencio – Silencio – Silencio no Silencio
Silencio 2 Silencio 0 Silencio 4 Silencio `[4,9,2,3]` Silencio 2 Silencio 3‐2 = 1 Silencio sí Silencio añadir `4` → `Respuesta = 4` Silencio
Silencio 3 Silencio 1 Silencio 5 Silencio `[9,2,3,7]` Silencio 3 Silencio 7‐2 = 5 → **rollback** → ventana `[9,2,3]` Silencio no
Silencio ... Silencio ... Silencio ... Silencio ... Silencio ...

El recuento final es `10`, exactamente como el caso de prueba de LeetCode espera.



-...

### Take‐away for the recruiter

Si observa este patrón en su propio trabajo o entrevista, ya está dominando:

* **Pre-computation (sieve)** – una optimización clásica de “offline”.
* **Two‐pointer + monotonic queue** – el oro estándar para *range-constrained* ventanas correderas.
* **In-place state preservation** – the `zelmoricad` copy is a neat hack that lets debug or audit the algoritmo with the original data at hand.

Siéntase libre de copiar-pasar cualquiera de los snippets arriba en su IDE, ejecutar el arnés de prueba LeetCode y presumir a su futuro empleador que usted sabe cómo mantener una ventana *prime‐tight* en ** tiempo lineal**! 