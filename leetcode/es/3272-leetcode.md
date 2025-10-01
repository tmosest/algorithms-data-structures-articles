-...
Título: LeetCode 3272. Encontrar el conde de buenos números
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 📌 LeetCode 3272 – “Encontrar el conde de buenos números”

■ *Problema*
■ Se le dan dos enteros `n` (1 ≤ n ≤ 10) y `k` (1 ≤ k ≤ 9).
■
■ *A k‐palindromic integer* es un palindrome divisible por `k`.
■ *Un buen entero* es un número de `n`‐digit cuyos dígitos se pueden reorganizar en un entero k-palindromic (sin ceros principales).
■ ** Objetivo:** Devuelve el número de buenos números de números enteros.

Las limitaciones son pequeñas, por lo que es posible una solución combinatoria exacta. A continuación encontrará:

Silencio Idioma Silencio Solución Silencio Tiempo Silencioso
Silencio----------------------------
Silencio **Java** Silencio TENIDO TENIDO TENIDO O(10 interpretasup confianzan/2 recomendado/supilo] Silencio O(1) Silencio
Silencio **Python** Silencio TENIENDO TERRITORIO O(10 instruccionesup confianzan/2 made/sup confianza) TEN O(1) ANTE
Silencio **C++** Silencio TENIENDO TENIDO TENIDO O(10 instrucciones adicionales)

■ ¿Por qué te importa? Este problema es un escaparate perfecto para los entrevistadores: prueba retroceso, combinatoria, memoización factorial y manejo de persianas (saliendo ceros). Dominarlo te ayudará a aterrizar tu próxima posición de técnico o de desarrollador.

-...

## 🧩 Problema de ruptura

1. ** Generación de palindrome**
The number of `n`‐digit palindromes is at most `10^(ceil(n/2)) ' , i.e. at most 10 000 when `n=10`. Podemos forzarlos a todos.

2. # Verificar k‐palindromic #
Convertir cada palindrome en un entero y probar divisibilidad por `k`.

3. # Buenas noticias #
Para cada palindromo k-palindromico, necesitamos saber cuántas permutaciones distintas de sus dígitos producen un entero válido de 'n'-digit (sin ceros líderes).
* Permutaciones totales = `n! / (freq[0]! * ... * freq[9]!)`.
* Permutaciones inválidas (primer dígito = 0) = `(n‐1)! / (freq[0]-1)! * ... * freq[9]!)`.
* Permutaciones válidas = total – inválidas.

4. **Deduplicado**
Dos palindromas diferentes pueden compartir el mismo multiset de dígitos; debemos contar cada dígito único multiset sólo una vez.

-...

## 🧠 Algorithm in Plain English

`` `
respuesta = 0
visitado = conjunto vacío de mapas de frecuencia de dígitos

para cada palindrome n-digit P:
si P % k == 0:
freq = mapa de frecuencia de dígitos en P
si no freq en visitado:
total = n! / prod(freq[d]!)
ceroRem = si freq[0] > 0 entonces (n‐1)! / prod(freq[d]! con freq[0] reducido por 1) más 0
respuesta += total - ceroRem
visitado.add(freq)
respuesta
`` `

Porque `n ≤ 10`, podemos pre-compute factoriales hasta 10 una vez y reutilizarlos.

-...

## 📚 Code

A continuación se presentan implementaciones limpias y idiomáticas en **Java**, **Python**, y **C+**.

### 1. Java

``java
importar java.util*;

Solución de la clase pública {}
privada estática final largo[] FACT = nuevo largo[11];
Estática
FACT[0] = 1;
para (int i = 1; i) = 10; i++) FACT[i] = FACT[i - 1] * i;
}

permCount(int[] freq, int total) {
long res = FACT[total];
para (int f : freq) res /= FACT[f];
restitución;
}

permCountZero(int[] freq, int total) {
si (freq[0] == 0) retorno 0;
freq[0]--; // reserva el cero líder
long res = FACT[total - 1];
para (int f : freq) res /= FACT[f];
freq[0]+; // restaurar
restitución;
}

cuenta de largo públicoGoodIntegers(int n, int k) {
respuesta larga = 0;
Establecer:String titulada visitado = nuevo HashSet correctamente();

int[] half = new int[(n +1) / 2];
generar(0, half, n, k, visited, answerHolder - confianza answer += responseHolder);
respuesta de retorno;
}

vacío privado genera(int pos, int[] la mitad, int n, int k,
Conjunto indicadoString confianza visitado, java.util.function.LongConsumer add) {
si (pos == media longitud) {}
int[] dígitos = buildPalindrome(half, n);
valor largo = 0;
para (int d : digitos) valor = valor * 10 + d;
(valor % k == 0) {
int[] freq = nuevo int[10];
para (int d : digitos) freq[d]++;
Clave de cuerda = Arrays.toString(freq);
si (!visited.contains(key)) {
visitado.add(key);
add.accept(permCount(freq, digits.length) -
permCountZero(freq, digits.length));
}
}
retorno;
}
para (int d = (pos == 0 ? 1 : 0); d ing= 9; d+) {
[pos] = d;
generar (pos + 1, mitad, n, k, visitado, añadir);
}
}

int privado[] buildPalindrome(int[] half, int n) {
int[] p = nuevo int[n];
para (int i = 0; i) a media longitud; i++) {
p[i] = p[n - 1 - i] = half[i];
}
si (n % 2 ==1) { //
int mid = half[half.length - 1];
p[half.length - 1] = mid;
}
retorno p;
}
}
`` `

■ **Explicación de las partes clave**
* `permCount` / `permCountZero` use pre-computed factorials.
* `visited` almacena una representación de cadena del array de frecuencia para deduplicar.
* Back-tracking `generate` construye todas las mitades posibles del palindrome, reflejando para obtener el número completo.

-...

### 2. Pitón

``python
importar matemáticas
de las importaciones de colecciones Contrato

def countGoodIntegers(n: int, k: int) - título int:
hecho = [1] * 11
para i en rango(1, 11):
[i] = fact[i - 1] * i

def total_perm(freq, tot):
res = fact[tot]
para f en freq.values():
res //= fact[f]
retorno

def cero_perm(freq, tot):
si freq.get(0, 0) == 0:
retorno 0
freq[0] -= 1
res = fact[tot - 1]
para f en freq.values():
res //= fact[f]
freq[0] += 1
retorno

visitados = set()
ans = 0

media_len = (n +1) // 2

def backtrack(pos, half):
no local
si pos == ...
# Build palindrome
dígitos = mitad + mitad [:-1] si n % 2 == 0 más mitad + mitad [-2:-1]
valor = int(''.join(map(str, digits)))
si el valor % k == 0:
freq = Counter(digits)
llave = tuple( surtido(freq.items()))) # Dedupe
si la clave no es visitada:
visitado.add(key)
freq_arr = [freq.get(i, 0) for i in range(10)]
total = total_perm(freq_arr, n)
cero = cero_perm(freq_arr, n)
ans += total - cero
Regreso

inicio = 1 si pos = 0 más 0
para d en rango(start, 10):
mitad [pos] = d
backtrack(pos + 1, half)

backtrack(0, [0] * half_len)
Retorno
`` `

-...

### 3. C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
static constexpr long long FACT[11] = {
1.1,2,6,24,120,720,5040,40320,362880,3628800
};

larga duración total Perm(cont array madeint,10 lecciones frecuentes, int tot) {
long res = FACT[tot];
para (int f : freq) res /= FACT[f];
restitución;
}

largo tiempo ceroPerm(arrayo significado,10 caracteres, int tot) {
si (freq[0] == 0) retorno 0;
freq[0]--; // reserva líder cero
long res = FACT[tot-1];
para (int f : freq) res /= FACT[f];
freq[0]+; // restaurar
restitución;
}

public:
larga cuenta GoodIntegers(int n, int k) {
ans largos = 0;
unordered_set obtenidosstring fiel visto; // cadena de frecuencia para dedupe

vector asignado medio(n +1)/2);
función recomendadavoid(int) = dfs = (int pos) {
si (pos == (int)half.size()) {}
vectores:
para (int i=0;i obedechalf.size();+i) {}
dígitos[i] = mitad[i];
dígitos[n-1-i] = mitad[i];
}
Val largo largo=0;
para (int d:digits) val=val*10+d;
si
array madeint,10 confianza freq{}; freq.fill(0);
para (int d:digits) freq[d]++;
clave de cuerda;
para (int i=0;i observado10;i++) key+=to_string(freq[i])+'#;
si (ver.insert(key).second) {
ans += totalPerm(freq,n) - ceroPerm(freq,n);
}
}
retorno;
}
para (int d=(pos==0?1:0); d obtenidos=9; ++d) {
[pos]=d;
dfs(pos+1);
}
};

dfs(0);
devolver los ans;
}
};
`` `

■ **Tip** – Las tres soluciones comparten la misma idea fundamental. Puede copiar-pasar las funciones de ayudante combinatorio entre idiomas con cambios mínimos.

-...

## 📈 Complexity Analysis

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
Silencio ** Tiempo** Silencioso `O(10^(ceil(n/2))' – en la mayoría de 10 000 iteraciones
Silencio** (además del conjunto visitado que tiene en la mayoría de 10 mapas de dígitos distintos) Silencio

La precomputación factorial es insignificante (`O(10)`).

-...

## 🎯 SEO‐Optimized Blog Post

A continuación se muestra un artículo listo para publicar que utiliza las palabras clave que pidió. Siéntase libre de copiarlo en su blog personal, Medium, Dev.to, o en un artículo de LinkedIn para aumentar su visibilidad en línea.

-...

# Encuentre el conde de los buenos números: LeetCode 3272 (Java, Python, C++)

**Keywords:** *LeetCode 3272, encontrar el recuento de buenos enteros, k-palindromic, algoritmo de entrevista, solución Java, solución Python, solución C++, entrevista de codificación, entrevista de trabajo, entrevista de ingeniería de software, entrevista de alta definición, entrevista de tech-lead, diseño de algoritmos, código de trabajo listo, desafío de codificación, solución algoritmo. *

-...

Introducción

Si te estás preparando para una entrevista de ingeniería de software, pronto te encontrarás mirando problemas que combinan **back-tracking** y **combinatorics**. LeetCode 3272 – “Encuentra el Conde de Buenos Integers” – es uno de esos desafíos. Te pide que:

- Generar todos los palindromas de 'n' dígitos (n ≤ 10).
- Filtrar aquellos que son divisibles por un pequeño entero `k` (1 ≤ k ≤ 9).
- Cuente cuántas permutaciones únicas de los dígitos de cada palindromo calificado crean un número válido de 'n' dígitos (sin ceros líderes).

Mientras las limitaciones se ven diminutas, la solución es una gran demostración de:

- Primera búsqueda (DFS) en la mitad de los dígitos.
- Pre-computación de factores para permutaciones exactas.
- Deduplicación usando un mapa de frecuencia.
- Maneje por caso para ceros líderes.

**¿Por qué es esto un “must-solve” para los reclutadores? * *
Los entrevistadores aman problemas que prueban *exacto* contando en lugar de aproximaciones. Muestra que puedes pensar en combinatoria, memoización y manipulación de cuerdas/array – todas las habilidades que se traducen directamente al código de producción.

-...

Declaración de problemas (Re-Written)

■ ** Entrada**:
" in n " - el número de dígitos (1 ≤ n ≤ 10).
" in k " - el divisor (1 ≤ k ≤ 9).
■
■ **Output**:
"long " - el número de buenos números de números enteros.

Un número **k-palindromic** es un palindrome divisible por `k`.
Un ** buen entero** es cualquier número de 'n`‐digit que puede ser permutado (sin ceros líderes) en un entero k-palindromic.

■ *Examples*
" texto
√ n = 3, k = 1 → 27 (Todos los números de 3 dígitos son buenos porque cada número puede ser reorganizado en un palindrome divisible por 1)
3, k = 3 → 4 (Sólo 3 dígitos como 121, 232, 343, 454 son buenos)
" `

-...

## 3down Brute‐ Estrategia de la Fuerza

Debido a que `n` es al menos 10, el recuento de posibles palindromas es en la mayoría de `10^(ceil(n/2)'.
Incluso para 'n = 10', eso es sólo 10 000 palindromas – perfectamente manejable.

1. **Generar todos los 'n`‐digit palindromes** mediante la elección repetitiva de los primeros 'ceil(n/2)' dígitos.
2. **Mirror** la mitad elegida para crear el palindrome completo.
3. **Ver divisibilidad**: `pal % k == 0`.
4. **Las permutaciones** de los dígitos del palindromo que califican tienen un cero líder.

-...

Contando permutaciones válidas

Denotamos la frecuencia de cada dígito en un palindrome como `freq[0...9]`.
The total number of distinct permutations of the `n` digits is:

" `
¡No! * freq[1]! * * freq[9]!)
" `

¡Pre-compute factoriales hasta 10! una vez y reutilizarlos.

**Pero debemos excluir las permutaciones que comienzan con cero. #
Si el palindromo contiene al menos un cero, nosotros:

- Reducir el número de ceros por 1.
- Computar las permutaciones de los dígitos restantes.
- Restaurar la cuenta cero después.

El número de permutaciones “malas” (línea cero) es:

" `
(n-1)! / (freq[0]-1)! * (freq[1]! * ... * freq[9]!)
" `

La subcontratación de la mala cuenta del total da el número de permutaciones *válidas* para ese palindromo.

-...

Deduplicación

Los palindromas múltiples pueden compartir las mismas frecuencias de dígitos.
For instance, `121` and `212` have the same `freq = {1:2, 2:1}`.
Sólo necesitamos contar cada configuración de frecuencia distinta una vez.

Almacenamos una representación de cadena del array de frecuencias en un 'set`/`unordered_set` e ignoramos duplicados.

-...

## 5VIEW⃣ Full Implementations

### 5.1 Java

``java
Clase Solución {
static final long[] FACT = {1,1,2,6,24,120,720,5040320,362880,3628800};

total privado largoPerm(int[] freq, int n) {
long res = FACT[n];
para (int f : freq) res /= FACT[f];
restitución;
}

privado largo ceroPerm(int[] freq, int n) {
si (freq[0] == 0) retorno 0;
freq[0]...
long res = FACT[n-1];
para (int f : freq) res /= FACT[f];
freq[0]+;
restitución;
}

cuenta de largo públicoGoodIntegers(int n, int k) {
Establecer contactos visualizados = nuevo HashSet correspondiente();
ans largas = 0;
int half = (n+1)/2;

int[] halfDigits = nuevo int[half];
backtrack(0, halfDigits, n, k, seen, ansRef - Propiedad {
ans += ansRef;
});

devolver los ans;
}

retroceso de vacío privado(int pos, int[] half, int n, int k, Conjunto seleccionadoSe ve, Consumidor garantizadoLong confianza) {}
si (pos == media longitud) {}
// Construye palindrome completo
int[] dígitos = nuevo int[n];
para (int i=0;i obedechalf.length;i+) {}
dígitos[i] = dígitos[n-1-i] = mitad[i];
}
val=0 largo;
para (int d:digits) val = val*10 + d;
(valor k == 0) {
int[] freq = nuevo int[10];
para (int d:digits) freq[d]++;
Clave de cuerda = Arrays.toString(freq);
si (ver.add(key)) {}
consum.accept(total Perm(freq, n) - ceroPerm(freq, n));
}
}
retorno;
}
para (int d=(pos==0?1:0); d obtenidos=9; ++d) {
[pos] = d;
backtrack(pos+1, half, n, k, seen, consumer);
}
}
}
`` `

■ *El código anterior utiliza `Consumer seleccionadoLong `` para acumular la respuesta, pero puede reemplazarla fácilmente con un campo de clase simple. *

### 5.2 Python

``python
importar matemáticas
de las importaciones de colecciones Contrato

def countGoodIntegers(n: int, k: int) - título int:
hecho = [1]*11
para i en rango(1,11): fact[i] = fact[i-1]*i

def total_perm(freq, n):
res = fact[n]
for v in freq.values(): res //= fact[v]
retorno

def cero_perm(freq, n):
if freq.get(0,0)=0: return 0
freq[0]-=1
res = fact[n-1]
for v in freq.values(): res //= fact[v]
freq[0]+=1
retorno

media = (n+1)//2
visitados = set()
ans=0

def backtrack(pos, half):
no local
si pos==half:
dígitos = mitad + mitad [:-1] si n%2=0 más mitad + mitad [-2:-1]
val = int('.join(map(str,digits)))
si vale=0:
freq = Counter(digits)
llave = tuple( surtido(freq.items())))
si la clave no es visitada:
visitado.add(key)
ans += total_perm(freq, n) - cero_perm(freq, n)
Regreso

para d en rango(1 si pos=0 otra 0, 10):
backtrack(pos+1, half+[d])

backtrack(0, [])
Retorno
`` `

### 5.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
static constexpr long long FACT[11] = {1,1,2,6,24,120,720,5040,40320,362880,3628800};

larga duración total Perm(cont array madeint,10 círculo frecuenciaq, int n){
long res = FACT[n];
para (int f : freq) res /= FACT[f];
restitución;
}

largo tiempo ceroPerm(arrayación obtenida,10 confianza freq, int n){
si (freq[0]==0) devuelve 0;
freq[0]--; // reserva líder cero
long res = FACT[n-1];
para (int f : freq) res /= FACT[f];
freq[0]+;
restitución;
}

public:
larga cuenta GoodIntegers(int n, int k){
unordered_set obtenidosstring confianza visto;
ans=0 largos;
vector contratado medio(n+1)/2);

función recomendadavoid(int) = dfs=[ cl](int pos){
si (pos==half.size()) {}
vectores:
para(int i=0;i obedechalf.size();+i) {}
dígitos[i]=digits[n-1-i]=half[i];
}
Val largo largo=0;
for(int d:digits) val=val*10+d;
si
array madeint,10 confianza freq{}; freq.fill(0);
para(int d:digits) freq[d]+;
clave de cuerda;
para(int i=0;i observado10;i++) key+=to_string(freq[i])+'#;
si (ver.insert(key).second) {}
ans += totalPerm(freq,n) - ceroPerm(freq,n);
}
}
retorno;
}
para(int d=(pos==0?1:0);d obtenidos=9;+d){
[pos]=d;
dfs(pos+1);
}
};

dfs(0);
devolver los ans;
}
};
`` `

-...

## 4down Por qué la solución importa

← Feature Silencio Lo que los entrevistadores esperan en la vida Cómo este problema proporciona tención
Silencio--------------------------------------------
Silencio **Exact Contando** Silencioso `O(n! / ...)` estilo contando en lugar de heurística. ← Utiliza pre-computación factorial para calcular las permutaciones exactamente. Silencio
Reducir el espacio estatal para los palindromos. ← Back-tracking on `(n+1)/2` digits. Silencio
Silencio **Deduplicación** Silencio Evitar el recuento excesivo. TEN Stores cadena de frecuencia en un conjunto. Silencio
Silencio ** Casos de Edge** Silencio Handle liderando ceros, extraña/hasta longitud. Silencio Zero‐permutation helper no garantiza cero líder. Silencio

Estos patrones son ** grado de producción**: pre-compute las cosas pesadas una vez, use los bucles iterativos, y guarde contra los casos de borde.

-...

## 5down Takeaways for the Job‐Entreview

1. **Mostrar su capacidad para diseñar un DFS limpio** que funciona en *half* los dígitos.
2. **Explicar por qué importa la pre-computación factorial** para el recuento exacto – elimina los errores de redondeo.
3. **Mención del paso de la deduplicación** – es una optimización sutil pero crucial.
4. ** Demostrar el manejo de los ceros principales** – una fuente clásica de errores.

Si presentas esta solución en una entrevista, demostrarás tanto *información algorítmica* como *aplicación limpia*, exactamente lo que demandan las posiciones superiores de devoto o de plomo tecnológico.

-...

## 6down Palabras finales

LeetCode 3272 es un **mini-clase** en conteo combinatorio.
Ya sea que lo resuelva en Java, Python o C++, la lógica sigue siendo idéntica.
Su *clean, código bien documentado* no sólo ganará puntos de entrevista, sino que también impresionará a los reclutadores que lean sus entradas del blog.

■ **Siguientes pasos**
■ 1. Practicar el problema en LeetCode y grabar el tiempo de ejecución para cada idioma.
■ 2. Escribir la solución en al menos dos idiomas para fortalecer la fluidez del lenguaje cruzado.
■ 3. Publicar su solución (como este artículo) y pedir comentarios a los pares.

¡Feliz codificación! 🚀