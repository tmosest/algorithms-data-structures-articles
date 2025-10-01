-...
Título: LeetCode 1316. Distinct Echo Substrings -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## Distinct Echo Substrings – LeetCode 1316
### Una guía detallada del problema, el algoritmo y los obstáculos

■ **Keywords** – *Distinct Echo Substrings*, *LeetCode 1316*, *echo substring algoritmo*, *rolling hash*, *string manipulation*, *C++ Solución*, *Solución de Java*, *Solución de pitón*, * algoritmo de O(n2)*, *hashing for strings*, *preguntas de entrevista*

-...

### 1. Declaración de problemas (LeetCode 1316)

Se le da una cuerda **`text`** (sólo letras minúsculas, `1 ≤ text.length ≤ 2000`).
Una subestring es un subestring **echo** si se puede escribir como **`XY`** donde las dos mitades son idénticas (`X == Y`).
Por ejemplo, en ``abcabc'`, ``abcabc'` es una subestring de eco porque puede dividirse en `'abc'` + `'abc'`.
Su tarea es devolver el número de subestrings de eco **`text`**.

-...

### 2. Lo que hace interesante este problema

Silencio Silencio Silencio Silencio
Silencio...
Silencio **Definición simple** – “la mitad equivale a la mitad” se siente intuitiva. Silencio ** Fuerza bruta-fuerza exponencial** – comprobar cada subestring (`O(n3)`) es una pesadilla incluso para `n = 2000`. Silencio **Las colisiones de Hash** – un hash ondulado monomod puede producir respuestas incorrectas si no es cuidadoso. Silencio
TEN **O(n2) existen soluciones** – LeetCode permite hasta 2000 chars, por lo que un algoritmo cuadrático está bien. TEN **Memory concerns** – almacenar cada subestring puede volar la memoria. Silencio **TLE para la comparación ingenua de cuerdas** – cada prueba de igualdad puede escanear caracteres `O(n)`. Silencio
Silencio **Tecnica reutilizable** – la idea rodante-hash es un bloque de construcción para muchos problemas de cuerda. tención **Eligerar el módulo base** – elegir una mala base o módulo puede llevar a muchas colisiones o desbordamiento. Silencio **Python’s slicing overhead** – soluciones ingenuas Python pueden llegar fácilmente a límites de tiempo en grandes entradas. Silencio

-...

### 3. Idea básica - O(n2) enfoque ondulado

1. **Pre-compute prefix hashes** –
`H[i] = (text[0] * p^(i-1) + text[1] * p^(i-2) + ... + text[i-1]) mod M`.
Con una base " p " (por ejemplo, 91138233) y un gran `M ' (por ejemplo, 109+7).
También podemos hacer doble presión con otro módulo (`M2`) para protegernos contra las colisiones.

2. *Comprobar cada subestring de longitud*
Por cada índice inicial " i " y por cada posible media longitud " ( " 1 ... (n-i)/2 "):
* `hash1 = getHash(i, i+len-1) `
* `hash2 = getHash(i+len, i+2*len-1) `
Si `hash1 == hash2` el substring `text[i:i+2*len]` es un substring eco.

3. **Mantenga subestrings distintos** –
Almacene la cadena real en un `HashSet` (Java), `set` (Python), o `unordered_set` (C++).
Usar un par de hash (dos valores mod) en el set es seguro y más rápido que construir la cadena, pero la cadena garantiza la corrección.

4. **Retorna el tamaño del set**.

■ ¿Por qué funciona en O(n2)? * *
■ Inspeccionamos `O(n2)` pares `(i, len)` y cada retrieval de hash es O(1).
■ La inserción final `substring` o `hash pair` es O(1) amortizado.

-...

### 4. Alternativas " por qué no son elegidos

Silencio Silencio Silencio Silencio Silencio Silencio Silencio Silencio
Silencio----------------------------
Silencio Brute‐force triple loop (`O(n3)`) Silencio 8 billion ops for `n=2000` Silencio O(1) Silencio Too slow TEN
← Igualdad de cadenas y cadenas (`O(n3)`) TENIDO Igual que antes TENIDO O(1) NOVEDAD Únicamente funciona para pequeñas entradas
Silencio **Rolling hash + set** (`O(n2)`) Silencio TENIENDO TERRENO `O(n2)` maletín peor, pero el conjunto de subestrings distintos es generalmente mucho más pequeño TEN La solución elegida
TENIDO SUffix array + LCP TENIDO `O(n log n)` Silencioso para esta restricción

-...

### 5. Escasos desfavorables

* ** Collisions hash** – un solo mod 64‐bit hash puede teóricamente collide. El doble esfuerzo reduce la probabilidad de negligencia.
* ** Patrones repetidos muy largos** – por ejemplo "aaaaa"a" crea muchos subestrings de eco; el uso de memoria del conjunto podría crecer.
Usar un par de hash en el set mantiene la memoria atada.
* **Python string slicing** – crea nuevas cuerdas cada vez. Para 2000 caracteres esto está bien, pero en límites de tiempo estrechos es posible que necesite utilizar la representación `hash` o `int`.

-...

### 6. Las soluciones finales

A continuación encontrará código listo para funcionar en **Java, Python, y C++**.
Los tres usan una técnica de rodaje con doble escobilla (excepto Python donde el hash integrado de 64 bits suele ser suficiente para las pruebas ocultas de LeetCode).

■ **Tip**: Si usted está enviando a LeetCode, elija el idioma con el que más se siente: las diferencias de tiempo de ejecución son insignificantes para este problema.

-...

## Java Solution (LeetCode 1316)

``java
importar java.util*;

Solución de la clase pública {}
public int distinct EchoSubstrings(String text) {
int n = text.length();
// Dos modulos para el doble corte
MOD1 final largo = 1_000_000_007L;
último largo MOD2 = 1_000_000_009L;
final largo BASE = 91138233L; // base al azar

// Hashes prefijo
long[] pref1 = new long[n + 1];
long[] pref2 = new long[n + 1];
long[] pow1 = new long[n + 1];
long[] pow2 = new long[n + 1];
pow1[0] = pow2[0] = 1;
para (int i = 0; i)
int c = text.charAt(i) - 'a' + 1; // 1..26
pref1[i + 1] = (pref1[i] * BASE + c) % MOD1;
pref2[i + 1] = (pref2[i] * BASE + c) % MOD2;
pow1[i + 1] = (pow1[i] * BASE) % MOD1;
pow2[i + 1] = (pow2[i] * BASE) % MOD2;
}

// Helper to compute hash of substring [l, r] (inclusive)
java.util.función.BiFunción realizadaInteger, Integer, Long[] getHash =
(l, r) - título nuevo Long[] {}
(pref1[r + 1] - pref1[l] * pow1[r - l + 1] % MOD1 + MOD1) % MOD1,
(pref2[r + 1] - pref2[l] * pow2[r - l + 1] % MOD2 + MOD2) % MOD2
};

Establecer los ecos del nuevo HashSet identificado();
para (int i = 0; i)
para (int len = 1; i + 2 * len = n; len++) {
Long[] h1 = getHash.apply(i, i + len - 1);
Long[] h2 = getHash.apply(i + len, i + 2 * len - 1);
si (h1[0].equals(h2[0]) ' h1[1].equals(h2[1])) {
ecoes.add(text.substring(i, i + 2 * len));
}
}
}
retorno echoes.size();
}
}
`` `

-...

## Python Solution

``python
def distinct EchoSubstrings(texto: str) - título int:
n = len(texto)
MOD1, MOD2 = 10**9 + 7, 10**9 + 9
BASE = 91138233

# Prefix hashes
pref1, pref2 = [0] * (n + 1), [0] * (n + 1)
pow1, pow2 = [1] * (n + 1), [1] * (n + 1)
para i, ch in enumerate(texto, 1):
val = ord(ch) - 96 # a- título1, b- título2 ...
pref1[i] = (pref1[i-1] * BASE + val) % MOD1
pref2[i] = (pref2[i-1] * BASE + val) % MOD2
pow1[i] = (pow1[i-1] * BASE) % MOD1
pow2[i] = (pow2[i-1] * BASE + val) % MOD2

def get_hash(l: int, r: int):
"""Hash of text[l:r+1], 0-based inclusive.""
h1 = (pref1[r+1] - pref1[l] * pow1[r-l+1]) % MOD1
h2 = (pref2[r+1] - pref2[l] * pow2[r-l+1]) % MOD2
(h1, h2)

ecos = set()
para i en rango(n):
para longitud en rango(1, (n-i)//2 + 1):
h1 = get_hash(i, i+length-1)
h2 = get_hash(i+length, i+2*length-1)
si h1 == h2:
ecoes.add(text[i:i+2*length])
len(echoes)
`` `

■ *Por qué esto funciona en LeetCode*
■ El arnés de prueba de LeetCode utiliza semillas aleatorias ocultas y un límite de tiempo de 1 s, pero un hash de rodamiento de 64 bits con dos moduli es efectivamente libre de colisión para todos los casos de prueba.

-...

## C++ Solución

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int distinct EchoSubstrings(texto de la cadena) {}
int n = text.size();
const long long MOD1 = 1'000'007LL;
const long long MOD2 = 1'000'000'009LL;
const long long BASE = 91138233LL;

vector realizado largamente confianza pref1(n+1,0), pref2(n+1,0);
vector obtenidos largamente largas puw1(n+1,1), pow2(n+1,1);

para (int i=0;i obtenidos;i++){
int val = text[i]-'a'+1; // 1..26
pref1[i+1] = (pref1[i]*BASE + val)%MOD1;
pref2[i+1] = (pref2[i]*BASE + val)%MOD2;
pow1[i+1] = (pow1[i]*BASE)%MOD1;
pow2[i+1] = (pow2[i]*BASE)%MOD2;
}

auto getHash = [ cl](int l,int r)- títuloarray obtenidoslong,2 título{
long long h1 = (pref1[r+1] - pref1[l]*pow1[r-l+1])%MOD1;
h1+=MOD1;
long long h2 = (pref2[r+1] - pref2[l]*pow2[r-l+1])%MOD2;
h2+=MOD2;
volver {h1,h2};
};

unordered_set ecos;
para (int i=0;i obtenidos;i++){
para (int len=1; i+2*len obtenidos=n; ++len){
auto h1 = getHash(i,i+len-1);
auto h2 = getHash(i+len,i+2*len-1);
(h1==h2)
ecoes.insert(text.substr(i,2*len));
}
}
retorno echoes.size();
}
};
`` `

-...

## 7. Palabras finales

*La definición “half iguala la mitad” es engañosamente simple, pero un enfoque de onda cuadrática convierte el problema en una rutina limpia y eficiente. *
Siéntase libre de copiar una de las tres soluciones anteriores, ajustar la base o el módulo si se encuentra en un caso de esquina, y tendrá una respuesta rápida y sin fallos a **LeetCode 1316** – y también habrá aprendido un patrón que le ayudará a abordar muchas otras preguntas de entrevista de manipulación de cadenas. ¡Feliz codificación!