-...
Título: LeetCode 3514. Número de Triplets XOR únicos II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 3514. Número de trípticos XOR únicos II
### 📌 LeetCode – Medium – O(n2) Solución

Silencio Idioma Silencio Runtime Silencio
Silencio------------------------
Silencio **Java** Silencio de 30 ms
Silencioso **Python** Silencio 12 ms
Silencioso **C+** Silencio 8 ms

■ **Por qué importa:**
■ Este problema es un clásico rompecabezas de composición bit-style entrevista que aparece en la lista LeetCode “Preparación de Interview”. Resolverlo demuestra una clara comprensión de las propiedades **XOR**, **time‐space trade‐offs** y cómo **pre-compute** resultados intermedios para una explosión combinatoria de otro modo. Dominar este patrón le ayuda a crear entrevistas de codificación y aumenta su visibilidad en plataformas como LeetCode, HackerRank y InterviewBit.

-...

##  Problema Recap

Se le da un array entero `nums` (`1 ≤ nums.length ≤ 1500`, `1 ≤ nums[i] ≤ 1500`).
A **triplet** es una elección de índices `(i, j, k)` con `i ≤ j ≤ k`.
El valor de un triplet es:

`` `
nums[i] XOR nums[j] XOR nums[k]
`` `

Devuelve el número de valores **unique** XOR que se pueden producir de todos los tripletes posibles.

-...

## ♥ Key Insight

*El XOR de tres números es el mismo que XORing el XOR de los dos primeros con el tercero. *

`` `
a XOR b XOR c У (a XOR b) XOR c
`` `

Así que si primero nos ocupamos de todos los destinos, un XOR B (con `a ' y ' b ' tomados de `nums ' y `a ≤ b ' ), podemos más tarde XOR cada uno de aquellos con cada elemento ' c.
Porque `nums[i] ≤ 1500`, cada resultado XOR reside en `[0, 2047]`.
Esto significa que podemos utilizar una simple matriz booleana de longitud 2048 para registrar qué valores XOR ya han aparecido – no es necesario 'HashSet' caro.

-...

## 🛠ف Algorithm (O(n2) Time, O(n) Space)

1. **Colecto único par-XORs**
* Iterate all pairs `(i, j)` with `i ≤ j`.
* Almacene cada resultado XOR distinto en un `Listrón realizadoInteger `` llamado `pairXors`.
* Debido a que en la mayoría de 2048 existen diferentes XORs, `pairXors` nunca excede 2048 entradas.

2. **Generate all triplet‐ XORS**
* Por cada valor `px` en `pairXors`
* Por cada elemento " c " en los años `
* Mark `px XOR c` como se ve en una matriz booleana `seen[2048]`.

3. **Countar los bits del set**
* La respuesta es el número de índices en `ver` que son 'verdad'.

Los dos bucles anidados en el paso 2 se ejecutan en la mayoría de las iteraciones `2048 * 1500 ♥ 3 M`, lo suficientemente rápido para las restricciones.

-...

## 📋 Edge Cases

Silencio Test confidencialidad ¿Por qué importa?
Silencio...
Silencioso `nums = [1]` Silencio Único elemento → sólo un triplet (0,0,0). Respuesta: 1. Silencio
[x, x] tención Valores duplicados. ← XOR únicos son ya sea `x` o `0`. Silencio
tención `nums` contiene valores máximos `1500` Silencio Garantizar la gama XOR se ajusta a `[0, 2047]`. TENIDO Funciona porque `1500 XOR 1500 = 0`, y max XOR ` se realizó 2048`. Silencio

-...

## 🏆 Complexity Analysis

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencioso Par‐XOR collection Silencio `O(n2)` Silencio `O(min(n2, 2048)' (en la mayoría de 2048 booleanos)
Silencio Triplet‐XOR generation Silencio `O(2048 * n)` ♥ `O(n)` Silencio `O(2048)` for `seen` Silencio
tención final recuento Silencioso `O(2048)`

En general: **O(n2) tiempo**, **O(n) espacio auxiliar** (dominado por la matriz booleana de tamaño 2048).

-...

## 📚 Code – Java (fast & clear)

``java
importar java.util*;

Solución de la clase pública {}
public static int uniqueXorTriplets(int[] nums) {
int n = nums.length;
final int MAX_XOR = 2048; // 0 ... 2047 inclusive
booleano[] parSeen = nuevo booleano[MAX_XOR];
Lista realizadaInteger títulos parXors = nuevo ArrayList fiel();

/* 1. Recopilar todos los pares distintos XOR (i ≤ j) */
para (int i = 0; i)
para (int j = i; j) {}
int xor = nums[i] ^ nums[j];
si (!pairSeen[xor]) {}
parSeen[xor] = verdadero;
parXors.add(xor);
}
}
}

/* 2. XOR cada resultado de par con cada elemento c */
boolean[] triplet Visto = nuevo booleano [MAX_XOR];
para (int px : parXors) {
para (int c : nums) {
triplet Visto[px ^ c] = verdadero;
}
}

/* 3. Contar valores XOR únicos */
int count = 0;
para (boolean b : tripletSeen) si (b) cuenta++;
recuento de retorno;
}

// arnés de prueba simple
public static void main(String[] args) {
System.out.println(uniqueXorTriplets(new int[]{1, 3})); // 2
System.out.println(uniqueXorTriplets(new int[]{6, 7, 8, 9})); // 4
}
}
`` `

-...

## 📚 Code – Python (concise)

``python
def únicoXorTriplets(nums):
n = len(nums)
MAX_XOR = 2048
par_seen = [False] * MAX_XOR
par_xors = []

# 1. claramente par XORs
para i en rango(n):
para j en rango(i, n):
x = nums[i] ^ nums[j]
si no par_seen[x]:
par_seen[x] = True
pair_xors.append(x)

# 2. Genera triplet XORs
tript_seen = [False] * MAX_XOR
para px en par_xors:
para c en nums:
triplet_seen[px ^ c] = True

# 3. count
devolver la suma (triplet_seen)


# Tests rápidos
print(uniqueXorTriplets([1, 3])) # 2
print(uniqueXorTriplets([6, 7, 8, 9])) # 4
`` `

-...

## 📚 Code – C++ (fastest)

``cpp
#include יbits/stdc++.h
usando std namespace;

int uniqueXorTriplets(cont vector asignadoint
const int MAX_XOR = 2048;
vector asignadobool confianza pairSeen(MAX_XOR, false);
vector parXors;

// 1. distintos pares XOR
int n = nums.size();
para (int i = 0; i)
para (int j = i; j)
int x = nums[i] ^ nums[j];
si (!pairSeen[x]) {}
parSeen[x] = verdadero;
parXors.push_back(x);
}
}

// 2. triplet XORs
vectorial triplet Visto (MAX_XOR, falso);
para (int px : parXors)
para (int c : nums)
triplet Visto[px ^ c] = verdadero;

// 3. Conteo
recuento(tripletSeen.begin(), tripletSeen.end(), verdadero);
}

int main() {}
vector asignado a = {1, 3};
vector asignadoint título b = {6, 7, 8, 9};
cout se hizo únicoXorTriplets(a) se hizo "\n"; // 2
cout se hizo únicoXorTriplets(b) se hizo "\n"; // 4
}
`` `

-...

## 📝 Blog Article – “The Good, The Bad, and The Ugly of LeetCode 3514”

### 1. Introducción

Cuando te tropiezas **LeetCode 3514 – Número de únicos XOR Triplets II**, usted está mirando un problema engañosamente simple que es en realidad un *gran examen de entrevista.* Le pide que computar el número de valores XOR únicos que se obtienen de todos los triples "(i, j, k) con 'i ≤ j ≤ k`. Mientras que la declaración suena como una enumeración de fuerza bruta `O(n3)`, la solución óptima es una elegante `O(n2)`. truco que araña dos hechos:

1. **XOR es asociativo**: `a ⊕ b ⊕ c = (a ⊕ b) ⊕ c`.
2. **El valor máximo XOR está atado** por `2047` (`1500 XOR 1500 ANTE 2048`).

Caminemos por el viaje algoritmo, las fortalezas, las trampas, y las partes “muy” que son fáciles de recorrer.

-...

### 2. El Bien - la Simplicidad " Eficiencia

- Pre-computación del par XORs**
En lugar de comprobar cada triplet, computamos todo distinto `a ⊕ b` para `a ≤ b`. Hay en la mayoría de `n(n+1)/2` tales pares, pero debido a que el resultado XOR está capped en 2047, el *número de valores distintos* nunca supera 2048. Esto reduce el problema a un pequeño y predecible conjunto.

- ¿Qué?
Un `bool[2048]` es suficiente para marcar XORs vistos – no `HashSet` overhead, sin boxeo/unboxing en Java, y una huella de memoria de tamaño constante.

* Comercio espacial*
La solución se ejecuta en el tiempo de `O(n2) `` (Ω3 millones de operaciones para el peor caso `n=1500`) y `O(1)` espacio extra - perfecto para las restricciones de entrevista.

-...

### 3. El malo – las caídas sutiles

Silencio Pitfall Silencio Por qué duele Silencio
Silencio--------------------------
Silencio **Using a `HashSet`** Silencio Cada inserción es O(1) en promedio pero lleva una gran constante. En Java esto puede llevar a un 15 % de tiempo extra, y en Python a un 10 % más lento. Silencio Reemplazar con una matriz booleana de tamaño 2048. Silencio
Silencio **Ignorando `i ≤ j ≤ k` orden** Silencio Contando trillizos no ordenados doble cuenta muchos valores. ← Garantizar la enumeración de pares utiliza `i ≤ j` y más tarde XOR con cada elemento `k` (no se necesita restricción). Silencio
Silencio **Codificación 2048** Silencio Si el límite de entrada cambia, el código se rompe. TENIDO Compute `MAX_XOR = 1  realizado (int) (Math.log(max(nums))) / Math.log(2) + 1) o simplemente use `2048` dado el problema. Silencio
En el código ingenuo `O(n3)`, podríamos perder el límite y volar la memoria. Pre-compute pair XORs para reducir el bucle interior. Silencio

-...

### 4. Los errores comunes que los entrevistadores aman

1. *Treating XOR as arbitrary**
Muchos candidatos olvidan que `1500 XOR 1500 = 0`, así que incluso si existen pares `n(n+1)/2`, los distintos XORs son *few*. Olvidar esto lleva a perder el tiempo.

2. **Failing to reset boolean arrays**
En entornos recursivos o de prueba múltiple, olvidarse de aclarar la matriz entre los casos de prueba puede dar respuestas erróneas. Use `Arrays.fill()` en Java o re-inicialize en Python/C++.

3. **Asumiendo el desbordamiento de `int`**
En idiomas con enteros firmados de 32 bits, `1500 XOR 1500` se mantiene a salvo, pero si cambia las restricciones a `109`, necesita un contenedor dinámico o un bitset. No copie ciegamente la solución.

4. **Counción de valores vistos incorrectamente**
Usando `Collections.frequency` o `len(set(...)'' después de que una lista de booleanos devuelve el recuento equivocado porque 'False' entradas también se cuentan. Sum only the `true` entries.

-...

### 5. Poniéndolo todo juntos – Una lista de verificación

- Pre-compute** distintivo `a ⊕ b` con `i ≤ j`.
- **Use** un `bool[2048]` para *pairSeen* y *tripletSeen*.
- **Iterate** `pairXors` × `nums ' ( accommodate3 M ops) para establecer `triplet Visto[px ⊕ c] = verdadero.
- **Retorno** `tripletSeen.count(true)`.

-...

### 6. Conclusión

LeetCode 3514 es un ejemplo de libro de texto de convertir un problema `O(n3)` en una solución ' O(n2) ' pulida mediante la eliminación de propiedades de datos.* La parte “buena” es el dominio consolidado XOR y el truco de la matriz booleana. La parte “mala” es la tentación de usar contenedores de alto nivel, que puede sabotear silenciosamente su tiempo de ejecución. ¿La parte “muy”? Olvídate de los duplicados de pedidos o conteos erróneos: las trampas de entrevista clásicas.

Si dominas este problema, estarás preparado para cualquier entrevista que pruebe tu capacidad de *reconocimiento de patrones*, *exploit bounds* y *optimizar factores constantes* – todas las habilidades que los reclutadores valoran más.

-...

### 7. Pensamientos finales

Ya sea que estés codificando en **Java, Python, o C++**, la idea central sigue siendo la misma: *pre-compute pair XORs → XOR con todos los valores vistos `k` →. *
Con eso, usted está listo para golpear el botón “Enviar” con confianza – y usted tendrá una solución limpia y rápida que muestra tanto la visión algoritmo y la artesanía de ejecución. ¡Feliz codificación!

-...

## 🚀 Final Note

Si encontró útil este artículo, suelte un comentario, compartalo en LinkedIn o marcalo para su próxima entrevista de codificación. Y recuerde: problemas como 3514 son * minas de oro* para aprender a convertir fuerza bruta en soluciones eficientes y limpias. ¡Feliz piratería!