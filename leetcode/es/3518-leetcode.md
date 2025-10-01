-...
Título: LeetCode 3518. Rearme Palindromic más pequeño II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 3518. Rearme Palindromico más pequeño II
## Un "Easy‐to‐Read" Java / Python / C++ Solución + un blog de trabajo

-...

#### TL;DR

* ** Objetivo:** Regresar el palindrome más pequeño de *k*-th lexicographically que se puede formar mediante la permutación de una determinada cadena palindromica *s*.
* **Constraint:**
* `1 ≤ Новыеных ≤ 104`
* `1 ≤ k ≤ 106`
* `s` contiene sólo minúsculas letras inglesas y está garantizada a ser un palindromo.
*Core Idea*
* Un palindrome está completamente determinado por su *primera mitad* (y posiblemente un personaje medio).
* Cuenta cuántas permutaciones son posibles para cada prefijo de la primera mitad utilizando un coeficiente *multinomial*.
* Escoge la carta más pequeña que mantiene el número de permutaciones restantes ≥ k.

Las siguientes secciones recorren la intuición, el algoritmo, la complejidad y la implementación en **Java, Python y C+**.
Después del código incluimos un artículo de blog pulido y amigable con SEO que puedes copiar-paste en tu cartera o LinkedIn para mostrar tu pensamiento de entrevista.

-...

## 1. Recapitulación de problemas (en inglés sencillo)

■ Te han dado una cuerda que ya es un palindromo.
■ Reorganizar sus cartas (cualquier permutación) mientras el resultado siga siendo un palindromo.
■ Entre todas las permutaciones palindrómicas distintas, la salida **k‐th** en orden lexicográfico.
■ Si hay menos de *k* permutaciones, producir una cadena vacía.

■ *Examples*
* ``abba'`, k = 2 → `'baab'`
* `aaa'`, k = 2 → `'" (sólo `'aaa'' existe)
* `'bacab'`, k = 1 → `'abcba'` (primero en orden)

-...

## 2. Intuición: “Si el Palindrome es todo lo que necesitamos”

Un palindromo lee el mismo avance y retroceso.
Si conocemos los caracteres que ocupan las posiciones **primera `⌊n/2⌋`**, toda la cuerda está fijada:

`` `
primero Medio + (medio char, si hay) + inverso(primero mitad)
`` `

Así que el *problema* se reduce a:

1. **Encuentra el personaje medio** (hay en la mayoría uno, porque la cadena de entrada es un palindromo).
2. **Construir la primera mitad** de longitud `halfLen = n / 2`.
3. El palindrome *k*‐th es sólo la primera mitad que construimos, seguido por el char medio (si hay) y su revés.

El desafío es *cómo construir la primera mitad* eficientemente, sabiendo cuántas permutaciones son todavía posibles después de cada elección provisional.

-...

## 2. Contando las Permutaciones restantes – Coeficiente Multinomial

Si la frecuencia de un personaje *c* en la primera mitad es `cnt[c]`, entonces el número de formas distintas de organizar el multiset restante de letras es

`` `
multinomial(cnt) = (cnt[0] + ... + cnt[25])! / (cnt[0]! · ... · cnt[25]!)
`` `

Debido a que los valores factoriales crecen extremadamente rápido, nosotros **nunca necesitamos calcular el número exacto** – sólo necesitamos saber si es **≥ k** o ** secuestrado k**.
Así que captamos el resultado en `MAX = 1_000_001` (uno más que el más grande posible 'k') y abortar el cálculo tan pronto crucemos ese umbral.

El coeficiente binomial `C(n, k)` se utiliza internamente:

`` `
C(n, k) = n! / (k! · (n-k)!)
`` `

Tanto `multinomial()` como `binom()` se implementan con *terminación temprana* para mantener el tiempo de ejecución minúscula.

-...

## 3. Construcción de la Primera Media

Para cada posición 'pos' en la primera mitad (de izquierda a derecha):

`` `
para cada personaje c en 'a'.'z' (en orden ascendente):
si cnt[c] == 0: continuar

# Try putting c at this position
cnt[c]...
restante = multinomial(cnt) # número de permutaciones para el sufijo

si quedamos >= k:
apéndice c del resultado
ir a la siguiente posición
más:
k -= restante # saltar todas las permutaciones comenzando con c
cnt[c]+
`` `

Debido a que la cadena es un palindrome, **todo** permutación válida de la primera mitad corresponde a un palindrome entero único – no hay duplicación en las dos mitades.

-...

## 4. Análisis de la complejidad

TEN TERRITOR TEN SON ANTERIOR
Silencio------Prince--------
Frecuencia permanente contando Silencioso `O(n)`
TENIDO Encontrar el char medio TENIDO `O(26)`
TENIDO Computing first half ANTE `O(halfLen · 26 · B)` Silencio Para cada una de las posiciones `halfLen ≤ 5 000`, intentamos en la mayoría de 26 letras. `B` es el número de multiplicaciones dentro de `binom()`, que está obligado por ~20 porque el valor explota más allá de `1 000 001` después de un puñado de multiplicaciones. Silencio
Silencioso Asamblea final Silencio inversa cadena y concatenación
Silencio **Total** Silencioso **`O(n · 26 · 20)` → prácticamente `O(n)`** Silencio Los factores constantes son pequeños. Silencio

El uso de la memoria es `O(26)` (frequency arrays) + `O(n)` para la cadena de salida – muy por debajo de los límites.

-...

## 5. Implementación - Tres idiomas

■ **Nota:**
■ Todas las implementaciones mantienen el valor combinatorial *en* en `MAX = 1_000_001`.
El primer palindromo está en `k = 1`.

### 5.1 Java

``java
importar java.util*;

Solución de la clase pública {}
static final long MAX_K = 1_000_001L;

public String smallestPalindrome(String s, int k) {
int[] freq = nuevo int[26];
para (char ch : s.toCharArray()) freq [ch - 'a']+;

// char medio (si hay)
carbon mid = 0;
para (int i = 0; i)
(freq[i] " 1) == 1) { //
media = (char) (a' + i);
freq[i]--; // quitar el medio uno
ruptura;
}
}

// media frecuencia
int[] half = new int[26];
int halfLen = 0;
para (int i = 0; i)
[i] = freq[i] / 2;
halfLen += half[i];
}

long total = multinomial(half);
si (k > total) regresan "; // no suficientes permutaciones

StringBuilder first = new StringBuilder();
para (int pos = 0; pos " ) {}
para (int c = 0; c) {}
si (half[c] == 0) continuar;
[c]--; // uso provisional c
largos caminos = multinomial(half);
si (siempre >= k) { // mantener c
primer.append((char) ('a' + c));
ruptura;
} más { / / / saltar todas esas permutaciones
k -= maneras;
[c]++; // restaurar
}
}
}

String rev = nuevo StringBuilder(primer).reverse().toString();
Regreso medio == 0 ? first + rev : first + mid + rev;
}

multinomial (int[] cnt) {
int tot = 0;
para (int c : cnt) tot += c;
larga res = 1;
para (int i = 0; i)
int c = cnt[i];
(c == 0) continuar;
res = res * binom(tot, c);
si (res ю= MAX_K) devuelve MAX_K;
tot -= c;
}
restitución;
}

privada binom larga (int n, int k) {
si (k > n) retorno 0;
c) k = n - k;
largo r = 1;
para (int i = 1; i) = k; i++) {
r = r * (n - i +1) / i;
si (r >= MAX_K) devuelve MAX_K;
}
retorno r;
}
}
`` `

-...

### 5.2 Python

``python
de la importación Lista

MAX_K = 1_000_001

Solución de clase:
def más pequeño Palindrome (self, s: str, k: int) - confiar str:
[0] * 26
por ch en s:
freq[ord(ch) - 97] += 1

# Middle char (si hay)
mitad = ' '
para i en rango(26):
si freq[i] >
media = chr(97 + i)
freq[i] -= 1
descanso

media = [f // 2 para f en freq]
media_len = sum(half)

total = self.multinomial(half)
si k > total:
Retorno '

primero = []
para _ en rango(half_len):
para c en el rango(26):
si la mitad [c] == 0:
continuar
[c] -= 1
maneras = auto.multinomial(half)
si maneras >= k:
primer.append(chr(97 + c))
descanso
k -= maneras
[c] += 1

first_half = ''.join(first)
volver first_half + mid + first_half[:-1]

def multinomial(self, cnt: List[int]) - int:
tot = sum(cnt)
res = 1
para c en cnt:
res *= self.binom(tot, c)
si res MAX_K:
retorno MAX_K
tot -= c
retorno

def binom(self, n: int, k: int) - int:
si k > n:
retorno 0
si k > n - k:
k = n - k
r = 1
para i en rango(1, k + 1):
r = r * (n - i +1) // i
si r MAX_K:
retorno MAX_K
retorno
`` `

-...

### 5.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
static constexpr long MAX_K = 1000001L;

public:
cuerda más pequeña Palindrome(estring s, int k) {
array madeint,26 titulada freq{};
for(char ch: s) freq[ch-'a']++;

// media char
carbon mid = 0;
para(int i=0;i observado26;i+){
si (freq[i]
media = char(a'+i);
freq[i]...
ruptura;
}
}

array madeint,26 titulado half{};
int halfLen = 0;
para(int i=0;i observado26;i+){
[i] = freq[i]/2;
halfLen += half[i];
}

long total = multinomial(half);
si (k > total) regresar ";

cuerda primero;
para(int pos=0; pos obtenidoshalfLen; ++pos){
para(int c=0;c obtenidos26;c++){
si (la mitad [c]==0) continúan;
media[c]--; // try c
largos caminos = multinomial(half);
si {}
primero.push_back(char('a'+c));
ruptura;
}else{
k -= maneras;
[c]++; // undo
}
}
}

cadena rev = primero;
(rev.begin(), rev.end());
if(mid==0) return first + rev;
volver primero + mediados + rev;
}

privado:
largo multinomial(cont array madeint,26 `cnt) const {
long tot = 0;
para(int c: cnt) tot += c;
larga res = 1;
para(int c: cnt){
si (c==0) continúan;
res *= binom(tot, c);
si (res >= MAX_K) devuelve MAX_K;
tot -= c;
}
restitución;
}

largo binom(long n, long k) const {
(k]n) retorno 0;
si(k]n-k) k=n-k;
largo r=1;
para(long i=1;i won=k;i+){
r = r * (n-i+1) / i;
si (r título=MAX_K) devuelve MAX_K;
}
retorno r;
}
};
`` `

-...

## 6. Cómo utilizar estas soluciones

- **LeetCode / Interview**: copy the `Solution` class / methods into the platform’s editor.
- Pruebas locales.

``python
sol = Solución()
print(sol.smallestPalindrome("abcba", 1)) # abcba
print(sol.smallestPalindrome("abcba", 3)) # bcbab
`` `

-...

## 7. Resumen – Por qué esto importa para su resumen

* **Agarro sólido de combinatoria** – explicando factoriales, binomio, multinomio, y cómo aplicarlos en el diseño del algoritmo.
* **Eficiencia de la pronta determinación** – un truco común de entrevista para grandes cálculos enteros.
* ** Gran construcción con conocimiento del estado futuro** – demuestra una profunda comprensión de los problemas de “elegir el próximo paso correcto”.
* **Clean, código idiomático en tres idiomas** – muestra la versatilidad como ingeniero de software.

Incluya este problema en su cartera o como punto de conversación en entrevistas técnicas para impresionar a los gerentes de contratación: “Puedo construir un palindrome en tiempo lineal utilizando combinatoria, incluso bajo restricciones estrictas. ”

Feliz codificación, y que su próxima entrevista de trabajo acepte su primer palindromo con `k = 1`!