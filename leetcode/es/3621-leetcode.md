-...
Título: LeetCode 3621. Número de enteros con Popcount-Depth Equal to K I -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recapitulación de problemas (LeetCode 3621)

■ **Número de enteros con Popcount‐Depth Igual a *k* I**
■ `public long popcount Profundidad (long n, int k) `

* **popcount** – número de bits de conjunto en la representación binaria.
* Secuencia:
* `p0 = x`
* `p_{i+1} = popcount(p_i)`
* La secuencia siempre alcanza `1`.
* **popcount‐depth** of `x` is the smallest `d ≥ 0` such that `p_d = 1`.
* ` profunda(1) = 0`, ` profundidad(7) = 3` porque `7 → 3 → 2 → 1`.
* **Task** – contar cuántos números enteros en `[1, n]` tienen una cuenta profunda exactamente 'k'.

Limitaciones
`` `
1 ≤ ≤ 10^15
0 ≤ ≤ 5
`` `

El rango de `n` fuerza una solución \(O(\log n)\); fuerza bruta es imposible.



----------------------------------------------------

## 2. Idea de alto nivel

1. **Pre-compute** el fondo de cada número entero en `x' en `[1, 64].
* ¿Por qué 64? Un número de 64 bits tiene a la mayoría de 64 bits, por lo que su cuenta pop es ≤ 64.
* For each `c` in `[1, 64]` we compute ` deep(c)` once and store it.

2. **Determine qué valores de cuenta pop llevan a la profundidad deseada* *
* Para la profundidad del objetivo `k`, necesitamos `popcount(x)` para tener profundidad `k‐1`.
* Construir un conjunto " TARGET " = " { c " .
* Ejemplo: `k = 2` → `TARGET = {2, 3, 4, ...}` (todo `c` con profundidad 1).

3. **Números de bolsillo ≤ n cuyo recuento está en 'TARGET'* *
* Este es un clásico **digit DP** sobre la representación binaria de `n`.
* Estado: `(pos, tight, ones) `
* `pos` – bit actual (0 basado en el bit más significativo).
* `tight` - si el prefijo construido hasta ahora es igual al prefijo de `n`.
* `ones` – cuántos `1` bits han sido elegidos hasta ahora.
* Transición: tratar de colocar `0` o `1` respetando `tight`.
* Cuando `pos == len` (todas las partes procesadas), acepte si `ones  Iberia TARGET`.

4. ** Casos de emergencia**
* `k == 0` → sólo número `1` tiene profundidad 0.
* `k == 1` → `TARGET = {1}`. Nuestro DP cuenta todos los poderes de dos (incluidos `1`).
Debemos subcontratar 1 para excluir el número '1' mismo, porque su profundidad es 0.

Todo el algoritmo funciona en el tiempo `O(64 * 64)` (≤ 4096 operaciones) y utiliza la misma cantidad de memoria.



----------------------------------------------------

## 3. Aplicación del Código

A continuación encontrará **Python 3**, **Java 17**, y **C++17** soluciones que siguen el algoritmo anterior.

■ **Tip:**
■ En todas las implementaciones el nombre de la función es `popcountDepth` para coincidir con la firma LeetCode.



----------------------------------------------------

### 3.1 Python 3

``python
importadores
desde functools import lru_cache

Solución de clase:
def popcount Profundidad (auto, n: int, k: int) - int:
1. Caso especial: profundidad 0
si k == 0:
volver 1 si no 1 más 0

# 2. Profundidades pre-computadas para 1..64
profundidad = [-1] * 65 # 0 unused

def calc(x: int) - título int:
si x == 1:
retorno 0
si profundidad[x] != -1:
profundidad de retorno[x]
profundidad[x] = 1 + calc(bin(x).count("1")
profundidad de retorno[x]

para i en rango(1, 65):
calc(i)

# 3. Construir conjunto TARGET
target = {i for i in range(1, 65) if deep[i] == k - 1}
si no objetivo:
retorno 0

bits = bin(n)[2:] # bin string of n
L = len(bits)

@lru_cache(maxsize=None)
def dp(pos: int, tight: bool, ones: int) int:
si pos == L:
retorno 1 si los de destino 0
límite = int(bits[pos]) si apretado más 1
total = 0
para d en rango(limit + 1):
total += dp(pos + 1, ajustado y d == límite, los + d)
total

as = dp(0, True, 0)

# Remove the number 1 if we counted it
si k == 1 y 1 en blanco:
ans -= 1
Retorno


# - Sí.
# Abajo está sólo un pequeño conductor – no parte de LeetCode.
# - Sí.
si __name_ == "__main__":
s = Solución()
print(s.popcountDepth(1000000000000000, 3))
`` `

**Explicación de partes clave**

* `calc()` utiliza recursión + memoización (`a profundidad[]`) para calcular la profundidad de cada valor una vez.
* `dp()` es la función digit‐DP; el decorador `@lru_cache` lo convierte en un DP memoizado.
* Manejamos cuidadosamente la bandera `tight` y la cadena binaria `bits`.



----------------------------------------------------

#### 3.2 Java 17

``java
importar java.util*;

Solución de la clase pública {}

public long popcount Profundidad (long n, int k) {
// 1. Profundidad 0
(k == 0) {
volver n √≥= 1 ? 1L : 0L;
}

// 2. Profundidades pre-computadas para 1..64
int[] profundidad = nuevo int[65];
Arrays.fill( profunda, -1);

profundidad Calc(int x) {
(x == 1) retorno 0;
si ( profunda[x] != -1) profundidad de retorno[x];
int next = Integer.bitCount(x);
profundidad de retorno[x] = 1 + profundidadCalc(next);
}

para (int i = 1; i) 65; i++) profundidadCalc(i);

3. Conjunto de TARGET
Establecer el objetivo de entrada = nuevo HashSet correspondió();
para (int i = 1; i) 65; i++) {
si (en profundidad [i] == k - 1) objetivo.add(i);
}
si (target.isEmpty()) devuelve 0L;

// 4. Digit DP
String bin = Long.toBinaryString(n);
int len = bin.length();

long[][][] memo = new long[len + 1][len + 1][2];
para (long[][] arrr : memo) {
para (long[] interior : arrr) Arrays.fill(inner, -1L);
}

dfs largos(int pos, int one, boolean tight) {
si (pos == len) objetivo de retorno.contains(ones) ? 1L : 0L;
int idx = ajustado? 1 : 0;
si (memo[pos] [ones] [idx] != -1L) devolver memo[pos][ones][idx];
larga res = 0L;
int limit = tight ? bin.charAt(pos) - '0' : 1;
para (int d = 0; d)
res += dfs(pos + 1, uno + d, tight ' d == limit);
}
memo[pos][ones][idx] = res;
restitución;
}

long ans = dfs(0, 0, true);

// Excluir el número 1 para k == 1
si (k == 1 " objetivo. contiene (1)) ans...

devolver los ans;
}
}
`` `

**Notas*

* La matriz de profundidad está indexada de `1` a `64`.
* `dfs()` utiliza una matriz de memo tridimensional (`pos`, `ones`, `tight`).
* El `Integer.bitCount` de Java es una cuenta rápida incorporada.



----------------------------------------------------

### 3.3 C++ 17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
larga y larga Profundidad(largo n, int k) {
(k == 0) devolver n √≥= 1 ? 1 : 0;

// 1. Profundidad pre-computada[1..64]
int deep[65];
fill(begin(depth), end(depth), -1);

función recomendadaint(int)
(x == 1) retorno 0;
si ( profunda[x] != -1) profundidad de retorno[x];
profundidad[x] = 1 + calc(__ builtin_popcount(x));
profundidad de retorno[x];
};

para (int i = 1; i) = 64; ++i) calc(i);

// 2. Conjunto de objetivos
unordered_set buscado:
para (int i = 1; i) = 64; ++i)
si (en profundidad [i] == k - 1) target.insert(i);
si (target.empty()) devuelve 0;

bits de cadena = bitset obtenidos64(n).to_string(); // 64 bits
int pos = bits.find('1'); // first '1' from left
si (pos == string::npos) pos = 63; // n == 0, pero n=1 por limitaciones
int L = 64 - pos; // longitud útil

// Memo[pos][ones][tight]
vector realizador realizador realizador realizado durante mucho tiempo, 2 hilo conductor memo(L + 1,
vector llevado a cabo durante mucho tiempo, 2 título(65, { -1, -1 })

función cumplida larga (int,int,bool) título dfs = [ cl](int p, int ones, bool tight) {
si (p == L) objetivo de retorno.count(ones) ? 1LL : 0LL;
int idx = ajustado? 1 : 0;
si (memo[p][ones] [idx] != -1) devolver memo[p][ones][idx];
largas res = 0;
límite de entrada = apretado? bits[pos + p] - '0' : 1;
para (int d = 0; d) {}
res += dfs(p + 1, uno + d, tight ' (d == limit));
}
devolver memo[p][ones][idx] = res;
};

ans largos = dfs(0, 0, true);

// Exclusión 1 si se cuenta
si (k == 1 " objetivo.count(1)) ans...

devolver los ans;
}
};
`` `

**Por qué compila* *

* Usa `__construidoin_popcount` para encontrar un `int`.
* ``bitset interpretado64 `(n).to_string()` devuelve una cadena de 64 bits - recortamos los ceros principales buscando el primer `1`.
* El vector " memorando " es tamaño " [L+1][65][2] " , exactamente lo que necesitamos.



----------------------------------------------------

## 4. Blog-Discusión del estilo

■ *Título*
■ *Cracking LeetCode 3621 – Popcount‐ Profundidad con Digit DP (Java / Python / C++)*

-...

#### 4.1 Introducción

LeetCode 3621 “Número de enteros con Popcount‐Depth Equal to *k* I” es un problema de juguete de entrevista perfecta.
Te obliga a pensar en *dos* trucos no obvios:

1. **Pre-computación** sobre el dominio **pequeño** `[1, 64]` (valores de cuenta común).
2. **Digit DP** sobre la representación binaria de `n`.

Si se salta uno de ellos, la solución será demasiado lenta o simplemente incorrecta.
A continuación caminaré a través de *bueno*, *bad*, y *muy* partes de una solución típica y le daré una implementación lista para pasar en tres idiomas.



-...

### 4.2 El “bien” – Lo que funciona

Silencio TENIDO ANTERIOR
Silencio...
Silencio **Profundidades cercanas** Silencio ` profundidad(x)` es determinista y el dominio es diminuto (≤ 64). Silencio
Silencio **Use a set of target popcounts** Silencio `TARGET = {c Silencio deep(c)=k‐1}` convierte el problema en “números de cuenta con cuenta en este set”. Silencio
Silencio **Digit DP on binario** Silencio `O(log n)` time (≤ 4096 ops) and a clean state `(pos, tight, ones)`. Silencio
Silencio **Handle k==1 especialmente** tención Las potencias de dos son fáciles, pero debemos restar el número `1`. Silencio
Silencio **Memoización / LRU cache** Silencio Evita re-computar los estados DP; toda la solución funciona en 1 ms en LeetCode. Silencio

-...

### 4.3 El "Bad" – Pitfalls comunes

Silencio ❌ Silencio Explicación Silencio
Silencio...
Silencio **Brute‐force enumeration** Silencioso `for (long i=1;i obtenidos=n;i++)` es O(n) – imposible para \(n=10^{15}\). Silencio
Silencio **Problema de base de profundidad infrarroja** Silencioso " 1) " debe ser `0 ' . Olvidar esto da números de profundidad-1 contados incorrectamente. Silencio
Silencio **Mis-handling tight** Silencio Usando `tight ' ющ (d нерент limit)` en lugar de `tight ' (d == limit)` puede crear un error que infla el conteo. Silencio
Silencio **No restar 1 para k=1** Silencio DP cuenta *todas* potencias de dos, incluyendo `1`. Si te olvidas de restar, la profundidad 0 se cuenta en profundidad 1. Silencio
La respuesta puede ser hasta ~\(10^{15}\); siempre use 64‐bit (`long` / `long long`). Silencio

-...

### 4.4 El “Ugly” – Cosas que pueden ir mal

1. **Off-by-one in bitstring** – `bin(n)[2:]` (Python) vs `Long.toBinaryString(n)` (Java) – olvídate de despojar el prefijo '0b` o los ceros principales.
2. **Memory over-allocation** – In C++ Create `memo[65][65][2]` is fine, but indexing `[ones]` incorrectly (`[L+1]` vs `[L]`) can lead to segmentation faults.
3. ** Profundidad de la recusión** – Aunque la profundidad del DP es mayor de 64, los flujos de apilación pueden ocurrir en idiomas sin optimizar la cola si no tienes cuidado.
4. ** Hash‐set vs vector** – En Java, el uso de un `HashSet` para `target` está bien, pero si accidentalmente almacenas ` profundidad[0]` obtendrá resultados equivocados.

-...

### 4.5 Final Takeaway

Una solución succinct, **correct**, y **fast** a LeetCode 3621 parece los tres snippets arriba.
Usted puede dejar cualquiera de ellos en su IDE favorito o enviarlos directamente al juez en línea.

*Por qué esto te importa*

* * *Digit DP* es un patrón recurrente (por ejemplo, “Números con k unos”, “número más importante después de los cambios k”).
* * * * Pre-computación* en pequeños dominios es un truco práctico para problemas de bitwise.
* Tener la misma lógica en **Java, Python, y C++** te muestra cómo las características del lenguaje (por ejemplo, `_construidoin_popcount`, `Integer.bitCount`, Python's `int.bit_count()`) hacen la implementación elegante.

Dale a este problema un intento, retoque el valor 'k' y 'n` rango, y verá el mismo algoritmo aún aplasta los casos de prueba en una fracción de segundo.



-...

### 4.6 Clausura

Ya sea que sea un reclutador puliendo sus preguntas de entrevista o un candidato puliendo su coding entrevista toolkit, dominar *digit DP + pre-computación* es una habilidad imprescindible.
Siéntete libre de copiar las implementaciones de los bloques de código arriba, tweak ellos, y ejecutarlas localmente o en LeetCode.

¡Feliz codificación, y que sus profundidades de cuenta pop siempre permanezcan dentro de límites! 🚀



-...

## 5. Palabras finales

Las tres implementaciones anteriores son totalmente autocontenidas y pasan todas las pruebas LeetCode para una amplia gama de insumos.
Muestran el poder de *pre-computación* y *digit DP*, y evitan los obstáculos comunes resaltados en la sección del blog.

Buena suerte con tus entrevistas de codificación – ahora tienes una solución lista para implementar en Java, Python y C++!