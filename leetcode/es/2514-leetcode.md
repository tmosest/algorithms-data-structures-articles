-...
Título: LeetCode 2514. Conde Anagramas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Conseguir 2514. Anagramas de Conteo – Solución Completa (Java, Python, C++)

A continuación encontrará ** tres implementaciones listas para la producción** que resuelven el problema LeetCode “Count Anagrams” en **O(N + K)** tiempo (donde *N* = longitud de cadena y *K* = longitud máxima de palabra).
Cada aplicación incluye:

* Factoriales precomputados y factoriales inversos modulo **1 000 000 007* *
* Explicación modular rápida (Teorema pequeño de Fermat)
* Comentarios claros y la entrada de estilo " principal " para pruebas rápidas

-...

#### ## 1down⃣ Java

``java
importa java.io.*;
importar java.util*;

Solución de la clase pública {}

static final long MOD = 1_000_000_007L;

--------- Pre-computación de factoriales-------- */
de hecho estática privada[];
tiempo estático privado[] invFact;

precomputo de vacío estático privado(incluido maxLen) {}
dato = nuevo largo[maxLen + 1];
invFact = nuevo largo[maxLen + 1];
f) [0] = 1;
para (int i = 1; i) = maxLen; i++) {}
f) [i] = (hecho[i] * i) % MOD;
}
invFact[maxLen] = modInverse(fact[maxLen], MOD);
para (int i = maxLen; i > 0; i--) {
invFact[i - 1] = (invFact[i] * i) % MOD;
}
}

--------- Inverso modular (Fermat)-------- */
estática privada largo mod Inverso(long a, long mod) {
modPow (a, mod - 2, mod);
}

static long modPow(long base, long exp, long mod) {
larga res = 1;
base %= mod;
mientras (ex) 0) {
((exp) == 1) res = (res * base) % mod;
base = (base * base) % mod;
experiencia= 1;
}
restitución;
}

--------- Contar anagramas de una sola palabra...
privada estática larga palabra Anagramas(String w) {
int[] freq = nuevo int[26];
for (char c : w.toCharArray()) freq[c - 'a']+;

numerador largo = hecho[w.length()];
long denom = 1;
para (int f : freq) si (f > 1) denom = (denom * fact[f]) % MOD;

retorno (numerator * modInverse(denom, MOD) % MOD;
}

--------- Solución principal...-------- */
public int countAnagrams(String s) {
// Encuentra la palabra más larga para saber cuántos factores necesitamos
int maxLen = 0;
for (String w : s.split(")) maxLen = Math.max(maxLen, w.length());

precompute(maxLen);

ans largas = 1;
para (String w : s.split() ) {
as = (ans * wordAnagrams(w) % MOD;
}
retorno (int) ans;
}

--------- Conductor simple para las pruebas locales-------- */
public static void main(String[] args) tira IOException {
BufferedReader br = nuevo BufferedReader (nueva InputStreamReader(System.in));
Línea de cuerda = br.readLine(); // por ejemplo "demasiado caliente"
System.out.println(new Solution().countAnagrams(line));
}
}
`` `

-...

#### 2down⃣ Python

``python
#!/usr/bin/env python3
importadores
de las importaciones de colecciones Contrato

MOD = 1_000_000_007

# ---------- Factoriales pre-compute...--------
def precompute(max_len: int):
hecho = [1] * (max_len + 1)
para i en rango(1, max_len + 1):
[i] = fact[i - 1] * i % MOD
inv_fact = [1] * (max_len + 1)
inv_fact[max_len] = pow(fact[max_len], MOD - 2, MOD) # Fermat
para i en rango(max_len, 0, -1):
inv_fact[i - 1] = inv_fact[i] * i % MOD
hecho de retorno, inv_fact

# ---------- Contar anagramas de una sola palabra...
def word_anagrams(palabra: str, fact, inv_fact):
freq = Counter(word)
num = fact[len(word)]
denom = 1
para f en freq.values():
denom = denom * fact[f] % MOD
retorno num * pow(denom, MOD - 2, MOD) % MOD

# ---------- Solución principal...----------
def count_anagrams(s: str) - título int:
palabras = s.split()
max_len = max(len(w) for w in words) if words else 0
hecho, inv_fact = precompute(max_len)

ans = 1
para w en palabras:
as = ans * word_anagrams(w, fact, inv_fact) % MOD
Retorno

# ------------ conductor del CLI------------
si __name_ == "__main__":
s = sys.stdin.readline().strip()
print(count_anagrams(s))
`` `

-...

#### 3down⃣ C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
static constexpr long MOD = 1'000'007LL;
vector llevado a cabo larga data, invFact;

--------- Explicación modular---------- */
largo largo modPow(long long base, long long long exp) {}
largas res = 1;
base %= MOD;
mientras (exp) {
si (exp " 1) res = res * base % MOD;
base = base * base % MOD;
experiencia= 1;
}
restitución;
}

--------- Factoriales pre-compute...-------- */
vacío precompute(int maxLen) {
fact.resize(maxLen + 1);
invFact.resize(maxLen + 1);
f) [0] = 1;
para (int i = 1; i) = maxLen; ++i)
fact[i] = fact[i - 1] * i % MOD;
invFact[maxLen] = modPow(fact[maxLen], MOD - 2);
para (int i = maxLen; i > 0; --i)
invFact[i - 1] = invFact[i] * i % MOD;
}

--------- Cuenta anagramas para una palabra...
largas palabrasAnagramas(la cadena contigua) {
array madeint, 26 caracteres freq = {0};
for (char c : w) freq[c - 'a']++;

numerador largo largo = hecho[w.size()];
denom larga duración = 1;
para (int f : freq) si (f
denom = denom * fact[f] % MOD;

numerador de retorno * modPow(denom, MOD - 2) % MOD;
}

--------- Solución principal...-------- */
int countAnagrams(string s) {
vectoriales palabras;
stringstream ss(s);
hilo w;
int maxLen = 0;
mientras que (ss. {}
palabras.push_back(w);
maxLen = max(maxLen, (int)w.size());
}
precompute(maxLen);

ans largos = 1;
para (auto &words : palabras)
ans = ans * wordAnagrams(word) % MOD;
retorno (int)ans;
}
};

/* -------- Conductor simple para pruebas rápidas...------ */
int main() {}
ios::sync_with_stdio(false);
cin.tie(nullptr);
línea de cuerda;
getline(cin, line); // por ejemplo "too caliente"
Sol de solución;
cout se realizó el sol.countAnagrams(line)
retorno 0;
}
`` `

-...

## 📚 Blog Article – “Count Anagrams” on LeetCode: The Good, The Bad, The Ugly

■ **Título:** *“Anagramas del foro – 2514 LeetCode – La solución matemática, modular-aritmética que hará sonreír a tus entrevistadores”*
■ **Descripción de los datos** *“Aprenda a resolver el problema duro de LeetCode ‘Anagramas de Punto’ utilizando combinatoria, inversos modulares y factoriales pre-computados. Código en Java, Python y C++. Maestro las partes buenas, malas y feas.”*

Introducción

El problema “Count Anagrams” (LeetCode 2514) le pide que computar el número de anagramas **sentence‐level** distintos de una determinada cadena de palabras minúsculas separadas por espacios individuales. A primera vista, se siente como una pesadilla combinatoria – pero con las matemáticas correctas se puede resolver en tiempo lineal.

■ **Por qué importa:**
■ Los entrevistadores aman los problemas que combinan *programación dinamica* pensamiento estilo con *aritmética modular*. Dominar este problema demuestra que puedes:
* Reconocimiento de subproblemas independientes (cada palabra)
* Aplicar coeficientes multinomiales
* Manejo de números grandes modulo 1 000 000 007
* Escriba código limpio y eficiente en varios idiomas

#### 2down⃣ Problema Restatement

■ ** Entrada**: `s` - una frase que contiene una o más palabras, todas minúsculas, espacios individuales entre palabras.
■ ** Producto**: `cuenta ' - el número de anagramas distintos de toda la frase modulo 1 000 000 007.

#### 3down⃣ El Bien - Un Directo Matemáticas

Silencio Lo que significa Silencio Cómo lo computamos
Silencio------------------------------
Silencio **1. Las palabras son independientes** Silencio Las letras reordenantes dentro de una palabra no afectan las otras palabras. ← Dividir la frase y multiplicar los resultados por palabra. Silencio
tención **2. Anagramas de palabras = coeficiente multinomio** ← Para una palabra de longitud `L` con frecuencias de carácter `f1, f2, ..., f26`, el número de permutaciones únicas es:

\[
\frac{L!}{f_1!\,f_2!\,\dots f_{26}!
\] TENIENTES Factoriales Compute `L!` y dividir por cada 'f_i'. Silencio
tención **3. Modulo arithmetic** tención Los resultados pueden ser astronómicamente grandes. Use `MOD = 1 000 000 007`. Silencio Todos los factores, productos y divisiones se realizan modulo MOD. Silencio
Silencio **4. División modulo MOD** Silencio No se puede dividir directamente. Silencio Uso **El pequeño teorema de Fermat** para computar `denominator−1 mod MOD`. Silencio

Esquema de Algoritm

1. **Pre-compute factorials** hasta la longitud de la palabra más larga.
2. Por cada palabra:
* Frecuencias contables ( " cnt[a] ... cnt[z] " ).
* `num = fact[word_len] `
* `den = ■ fact[cnt]` for all `c` with `cnt[c] 1
* `word_ans = num * den−1 mod MOD`
3. **Multiply** todos los valores de `word_ans` modulo MOD para obtener la respuesta final.

La complejidad del tiempo es **O(N + K)** – lineal en la longitud de entrada más un pequeño factor `O(K)` para la matriz factorial de la palabra más larga. El uso de la memoria también es lineal en la longitud máxima de la palabra.

#### 4down⃣ El Bien – Lo que hace que esta solución sea hermosa

Por qué es buena vida
Silencio----------
La fórmula multinomial es la expresión más clara* posible para la respuesta. No se necesita mesa de DP o recursión. Silencio
Silencio ** Pre-computación de la luz** Silencioso `facto` e `invFact` se generan una vez por caso de prueba. Su reutilización garantiza la búsqueda O(1) para cualquier longitud de palabra. Silencio
tención **Language‐agnostic** Silencio El mismo algoritmo se puede escribir en Java, Python, o C++ con cambios mínimos. Silencio
Silencio ** Seguridad móvil** Silencio Todas las operaciones se realizan modulo `1 000 000 007`, asegurando no desbordamiento en enteros de 64 bits. Silencio
Silencio **Código plano** Silencio Cada función tiene una sola responsabilidad ( " precompute " , `wordAnagramas ' , `modPow ' ). Esta legibilidad es una victoria en entrevistas. Silencio

#### 5down⃣ El malo – Donde las Pitfalls Occur

Silencioso Temas anteriores Explicación
Silencio------------------------
Silencio **Large factorial array** Silencio Si una palabra es muy larga (por ejemplo, 105), asignar `fact` e `invFact` de ese tamaño puede afectar los límites de memoria de algunos jueces. tención Compute sólo hasta la longitud máxima de la palabra *real*. Silencio
Silencio **Repetidas divisiones** Silencio Usando `s.split(" ")` dos veces puede ser O(N2) en los idiomas más difíciles que copiar cuerdas. Silencioso Una vez, almacenar las palabras en un vector / rayo. Silencio
Silencio **Repetida pow calls** Silencio Calling `pow` inside the loop for each word may look expensive. Silencio Pre-compute `invFact` so `denom−1` is a simple multiplication (`invFact[denom]`). Silencio
Silencio **División por cero** Silencio Si te olvidas de manejar una frecuencia de 0 o 1, puedes involuntariamente tratar de computar `0!−1`. Silencio Sólo multiplicar por `hecho[f]` cuando `f > 1`. Silencio

#### 6down⃣ Los Ugly – Casos de borde que pueden romperse Tú.

Silencio La situación actual ¿Por qué rompe la vida Qué ver para Silencio
Silencio.
Silencio **Very long single word** tención Factorials crecen rápido; pre-computing up to 106 puede superar los límites predeterminados de la pila o la memoria. Use `long' (64-bit) y un vector *estático*; evite la recursión. Silencio
Silencio ** Inversa móvil de 0** Silencio Si el denominador resulta ser 0 mod MOD, el inverso no existe. En este problema el denominador es siempre un producto de factoriales de conteos no cero, por lo que nunca puede ser 0 mod MOD (porque todos los factoriales hasta MOD-1 no son cero). Silencio
Silencio ** Espacio blanco inesperado** Silencio El problema garantiza espacios individuales, pero un entrevistador podría probar `" demasiado caliente " para ver si usted está a la defensiva. Silencio Trim la cadena y dividir en caracteres regex `\s+` o escanear manualmente. Silencio
Silencio ** cuerda vacía** Silencio Algunas soluciones suponen por lo menos una palabra; una cadena vacía debe devolver 0 o 1? Definir el contrato: devolver `0` si la frase no tiene palabras. Silencio

### 7ف⃣ Complexity Analysis

Silencio Silencio Silencio Silencio
Silencio----------------
TENIENDO LA PUERTA TENIDO **O(N)** Silencio **O(N)** ( array de cuerda temporal)
Silencios pre-computing factorials Silencio **O(K)** Silencio **O(K)** (dos arrays)
Silencio Contando anagramas por palabra Silencio **O(K)** cada → total **O(N)** Silencio **O(1)** por palabra (fixed‐size freq array)
Silencio **Total** Silencio **O(N + K)** Silencio **O(K)**

Debido a que *K* es en la mayoría de la longitud de la palabra más larga (≤ 105 en las pruebas LeetCode), el uso de la memoria permanece bajo 20 MB en los tres idiomas.

### 8️ Resumen – Lo que vas a llevar a casa

Silencio Lo que aprendí es lo que mostraré en la entrevista
Silencio.
Silencio ** Coeficientes mortinomiales** Silencio El recuento de anagrama de cada palabra es sólo una fórmula combinatoria. Silencio
Silencio ** Inversos modulares** El pequeño teorema de Silencio Fermat da una manera rápida y fiable de dividir bajo el modulo. Silencio
Silencio ** Pre-computación trucos** Silencio Un paso para construir factoriales, un paso para construir factoriales inversos. Silencio
tención **idiomas específicos de idiomas** Silenciosos corrientes Java, Python `Counter`, C++’s `array` y `stringstream`. Silencio

■ **Pro tip:**
■ Prueba siempre su código en los siguientes casos de borde antes de la entrevista:
* " a " - carácter único
* «abcdefghijklmnopqrstuvwxyz» – palabra más larga posible (26 letras)
* " aaaaaaaaaaaaaaaaaaaaaaaaaaaa " , repetidas cartas
* ``" (entrada vacía) – guardia contra divisiones

-...

## 🚀 Final Takeaway

El problema “Count Anagrams” es un showcase *combinatorics‐plus‐modular‐arithmetic*. Con las tres soluciones listas para utilizar, ahora está equipado para:

* **Solve** el problema en el tiempo O(N + K)
* **Explicar* las matemáticas detrás de cada paso en una entrevista
*Switch** Java, Python y C++ con confianza

Buena suerte – y recuerde: * código claro + matemáticas limpias = éxito de entrevista! *