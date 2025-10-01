-...
Título: LeetCode 1554. Diferencia de cuerdas por un personaje -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Solving LeetCode 1554 – “Trings Differ by One Character”

■ **TL;DR**
■ Utilice un * hash polínomio* para reducir cada palabra a un solo entero.
■ Por cada posición `i` eliminar la contribución del `i`‐th carácter y comprobar si dos palabras se vuelven iguales.
" Time = O(N·M), Space = O(N).

-...

Problema Recap

`` `
Entrada : String[] dict (todas las palabras la misma longitud, única, minúscula)
Producto: verdadero si alguna palabra difiere exactamente por un personaje en el mismo índice
falso de otro modo
`` `

Silencioso en la exposición
Silencio------------
Silencio ["abcd", "acd", "aacd"] Silencio verdadero Silencio "abcd" vs "aacd" difieren sólo en el índice 1 Silencio
Silencio ["ab", "cd", "yz"]
Silencio ["abcd", "cccc", "abyd", "abab"] Silencio verdadero Silencio "abcd" vs "abyd" difieren en el índice 2 Silencio

Limitaciones
* `Principio sobre la vida ≤ 10^5`
* `len(word) = M ≤ 10` (porque todas las palabras son de igual longitud)
* Cada palabra es única y consta de sólo `a‐z`.

-...

Algoritmo polinomio Hash + Set

1. *Poderes de precomputación*
`pow[i] = BASE^i mod MOD` for `i = 0 ... M-1`.
" BASE = 257 " (primer primer título " 256, trabaja para todos los ASCII)
`MOD = 1 000 000 007` (grande para evitar el desbordamiento)

2. ** Hash every word**
`hash(w) = Governing (w[j] * pow[j] mod MOD`

3. *Para cada índice*
*Crear un set de hachís fresco*.
*Por cada palabra* compute `hashSinChar = (hash[w] – w[i]*pow[i] mod MOD`
* If `hashSinChar` already in `seen` → two words differ only at `i`* → return `true`.
Else añadirlo a `seen`.

4. Retorno `falso'** si no se encontró pareja.

■ **Por qué funciona* *
■ La eliminación de la contribución de un solo personaje de la hash polinomio da la hash de la subestring *remanente*.
■ Si dos palabras difieren sólo en la posición 'i', sus hahes de "removed‐char" son idénticos – lo atrapamos en el conjunto.
■ Las colisiones son astrónomos poco probables con un entero de 64 bits y un módulo 1e9+7.

-...

### ##  Settlement Correctness Proof

*Seamos dos palabras que difieren sólo en el índice k. *

- Sus hashes completos difieren sólo por `Δ = (w1[k] - w2[k]) * pow[k]`.
- Retirar 'k' de ambos hashes da `h1' = h1 - w1[k]*pow[k]` y `h2' = h2 - w2[k]*pow[k]`.
- Desde `h2 = h1 + Δ`, tenemos
`h2' = h1 + Δ - w2[k]*pow[k] = h1 + (w1[k])*pow[k] - w2[k]*pow[k] = h1 - w1[k]*pow[k] = h1'.
Así `h1' = h2'.

Por el contrario, si dos palabras "removed‐char" hashes son iguales en algún índice 'k', la única diferencia entre las palabras puede ser en 'k', porque todos los otros caracteres contribuyen a los dos hashes. Por lo tanto difieren en la mayoría de un carácter; la singularidad de las palabras garantiza que es exactamente uno. ∎

-...

#### ⏱{ >} Análisis de la Complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
← Pre-compute powers Silencio O(M) Silencio O(M)
Silencio Compute all hashes Silencio O(N·M) Silencio O(N)
Silencio Principal bucle Silencioso O(N·M) Silencio O(N) por iteración (set)
Silencio **Total** Silencio**

Con `N ≤ 10^5` y `M ≤ 10`, esto funciona cómodamente bajo 1 segundo en los tres idiomas.

-...

## 🧪 Code Implementations

A continuación se encuentran soluciones limpias y de producción en **Java**, **Python**, y **C+**.
Cada uno sigue la misma idea algoritmo e incluye comentarios para la claridad.

-...

## Java

``java
importar java.util*;

Solución de la clase pública {}
public boolean differByOne(String[] dict) {
si (dict == null tención eterna dict.length ) devolver falso;
final int BASE = 257; //
larga final MOD = 1_000_000_007L; // 1e9+7
int L = dict[0].length();

// 1 / 1 / ⃣ pre-compute powers
long[] pow = new long[L];
pow[0] = 1;
para (int i = 1; i)
pow[i] = (pow[i - 1] * BASE) % MOD;
}

// 2/50/⃣ compute full hashes
long[] hashes = new long[dict.length];
para (int i = 0; i)
long h = 0;
String s = dict[i];
para (int j = 0; j)
h = (h + s.charAt(j) * pow[j]) % MOD;
}
hashes[i] = h;
}

// 3Ω⃣ tratar de eliminar cada posición
para (int pos = 0; pos " ) {}
Establecer contactoLong caracteres vistos = nuevo HashSet fiel();
para (int i = 0; i)
largo sin = (hashes[i] - dict[i].charAt(pos) * pow[pos]) % MOD;
si (sin < 0) sin += MOD; // mantener positivo
si (!seen.add(sin))) devolver verdadero; // duplicar → diferir por uno
}
}
devolver falso;
}
}
`` `

-...

## Python

``python
de la importación Lista

Solución de clase:
def diferenciaByOne(self, dict: List[str]) - título bool:
si no dict o len(dict)
Retorno Falso

BASE = 257
MOD = 1_000_000_007
L = len(dict[0])

# Pre-compute powers
pow = [1]
para i en rango(1, L):
pow[i] = (pow[i - 1] * BASE) % MOD

# Full hashes
hashes = []
para s en dict:
h = 0
for j, ch in enumerate(s):
h = (h + ord(ch) * pow[j] % MOD
hashes.append(h)

# Remove one char per position
para pos en rango(L):
visto = set()
para i, s en enumerado(dict):
sin = (hashes[i] - ord(s[pos]) * pow[pos] % MOD
si no fuera visto:
Retorno
visto.add(sin)
Retorno Falso
`` `

-...

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
bool differByOne(vector seleccionadosstring limitada dict) {
si (dict.size()
const long long BASE = 257;
const long MOD = 1'000'000'007LL;
int L = dict[0].size();

// 1. poderes pre-compute
vector realizado largamente largas puw(L);
pow[0] = 1;
para (int i = 1; i)
pow[i] = (pow[i-1] * BASE) % MOD;

// 2. hashes completo
vector realizado largo tiempo h(dict.size());
para (size_t i = 0; i) ++i) {
long val = 0;
para (int j = 0; j)
val = (val + dict[i][j] * pow[j]) % MOD;
h[i] = val;
}

// 3. tratar de eliminar cada posición
para (int pos = 0; pos " )
unordered_set obtenidos largo visto;
para (size_t i = 0; i) ++i) {
largo tiempo sin = (h[i] - dict[i] [pos] * pow[pos]) % MOD;
sin += MOD;
si (!seen.insert(sin).second) regresan verdadero;
}
}
devolver falso;
}
};
`` `

■ **Tip** – Use `uint64_t` (2^64) en lugar de un módulo si desea dejar por completo la operación `%`; la probabilidad de colisión es esencialmente cero para las limitaciones dadas.

-...

## 🤔 Why This Algorithm Is Interview‐Ready

✔ Alimentación Silencio Por qué importa
Silencio...
Silencio **O(N·M)** Silencio Conozca la dificultad (`10^5` palabras)
Silencio **No loops anidados** ¦ Mantenga el código simple " readable ←
Silencio **La prueba matemática** Silencio le da confianza para explicarlo en una entrevista Silencio
Silencio **Handles negatives** Silencio Shows you care about edge cases (Java & C++ use `%` careful) Silencio

* Lista de comprobación de la entrevista*

1. **Comienza con la idea de fuerza bruta** – es fácil de explicar y generalmente aceptado en la primera ronda.
2. **Mostrar puede mejorar** – introducir el hash polinomio, explicando por qué reduce una cadena a un solo número.
3. ** Riesgo de colisión de mención** – ser honesto; nadie puede garantizar un hash perfecto, pero usted puede elegir un módulo grande o un flujo de 64 bits para hacerlo insignificante.
4. **Explicar tiempo & espacio** – los entrevistadores les encanta ver al grande O derivado de las limitaciones.
5. **Hablar sobre los casos de borde** – lista vacía, palabras de letras individuales, cartas identificativas, etc.

-...

## 🧠 "Bueno, malo, feo" de la solución

Silencio Silencio
Silencio------------Prince------
*Tiempo de iluminación*, trabaja para hasta 105 palabras, constante `M` mantiene la memoria baja.
Silencio **Bad** Silencio Las colisiones del hash Rare podrían reportar erróneamente `false` → `true`. Silencio Mitigated mediante el uso de un gran mod o de 64 bits de sobrebordamiento.
Silencio **Efectivamente** tención Gestión de aritmética modular en Java/C++ (`%` y valores negativos) puede ser propensa a errores. tención Evite usando aritmética de 64 bits sin firmar o un lenguaje que auto-wraps (`unsigned long` en C++). TEN – TEN

■ **Pro tip:** Si le preocupan las colisiones en un entorno de producción, mantenga un *pair de hashes* (por ejemplo, dos moduli diferentes) o retroceda a un paso de verificación cuando se encuentre un hash duplicado.

-...

## 📝 Testing & Validation

Silencio Test ← Input Silencio esperada Resultado
Silencio--------------------------...
TENIENDO UNA VOLVER RESPECTO ANTE LAS RESPUESTAS
Silencio Una sola palabra:
Silencio Todas las palabras idénticas excepto un char Silencio `["abcde", "abfde", "abgde"].
Silencio Todas las palabras difieren de 2 chars Silencio `["abc", "def", "ghi"] ' Silencio `false` ¦
Silencio Max tamaño (`10^5`) palabras al azar Silencio – Silencio Runs Гле ✔

Generar casos de prueba con `random.sample` o un generador personalizado para tener confianza.

-...

## 📚 Interview Tips

TENIDO TÉpico TENIDO Qué a la Mención ANTERIOR Por qué Ayuda a vivir
Silencio...
Silencio ** Diseño Algorithm** Silencio Comience con un enfoque bruto-force, a continuación, identificar el "un carácter" restricción → conduce naturalmente a la idea precipitada. tención Muestra problemas-solviendo la mentalidad. Silencio
Silencio ** Estructuras de datos** tención Utilice un hash set para detectar duplicados en O(1). Silencio mantiene el espacio óptimo. Silencio
Silencio **La complejidad** Silencio Explicar O(N·M) y por qué satisface las limitaciones. tención cuantifica la eficiencia. Silencio
Silencio **Edge-cases** ← Empty input, single word, all words identical length. ← Demuestra minuciosidad. Silencio
Silencio ** Manejo de la colisión** tención La probabilidad de mención y mitigación. Silencio muestra conciencia de las trampas del mundo real. Silencio

-...

## ❓ Preguntas frecuentes

Silencio
Silencio...
Silencio **¿Puedo usar una comparación de 'String' después de la eliminación de un char?** Silencio Sí, pero eso sería O(N2·M) en el peor caso – inaceptable para 105 palabras. Silencio
Silencio **¿Qué pasa si M fuera más grande (por ejemplo 1000)?** Silencio El algoritmo todavía sería O(N·M), pero 105·1000 es 108 operaciones – línea fronteriza. Es posible que se necesite un enfoque diferente (principio de giro o precipitación). Silencio
Silencio **¿Desbordamiento de las entradas de 32 bits?** Silencio En Java/Python/C++ utilizamos 64 bits (`long long`/`int64`) además de un módulo para mantener los valores.
Silencio **¿Por qué no utilizar `noordered_set directamente? Eso almacenaría cadenas completas – memoria O(N·M) y búsquedas más lentas. Hashing comprime cada cadena a un entero, ahorrando espacio y tiempo. Silencio

-...

## ⋅ Conclusion

El truco de hash polinomio convierte un problema aparentemente “estring-heavy” en un puñado de operaciones enteros.
Con sólo unas pocas líneas de código, usted satisface las limitaciones, mantiene el algoritmo rápido, y están listos para impresionar a los entrevistadores.

■ **Takeaway** – Cuando te preguntan “¿Hay un par que difiere de un personaje?”, piensa “hash every word → remove one char → look for duplicates”.
■ Esa mentalidad es exactamente lo que muchas empresas tecnológicas buscan: soluciones *limpiadoras, eficientes y bien justificadas*.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🎯