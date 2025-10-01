-...
Título: LeetCode 1178. Número de palabras válidas para cada Puzzle -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Para una palabra para ser *válido* para un rompecabezas

* cada letra de la palabra debe aparecer en el rompecabezas
* la primera letra del rompecabezas debe aparecer en la palabra

Porque un rompecabezas tiene **exactamente 7 letras distintas**, una palabra que contiene más de 7
diferentes cartas nunca pueden ser válidas.
El rompecabezas puede contener cada carta a la mayor parte de la vez, por lo que para fines contables sólo
cuidado sobre el *set* de letras de una palabra – los duplicados no importan.

----------------------------------------------------

##### 1. Representar un conjunto de letras con un bitmask

Para las 26 letras inferiores utilizamos un entero de 26 bits.

`` `
bit i (0-basado) es 1 Alternativa la letra (i + 'a') está presente
`` `

Ejemplo

`` `
palabra = "apple" → letras {a, p, l, e}
máscara = 0b000...00101110 (bits for a,l,p,e are 1)
`` `

* Construir una máscara para una palabra es `O(vivir palabras)`.
* Dos palabras que usan exactamente el mismo conjunto de letras obtienen la misma máscara.

----------------------------------------------------

##### 2. Contar palabras para cada máscara

`freq[mask]` = cuántas palabras en la entrada utilizan exactamente el conjunto de la letra descrita
por `mask`.
Sólo las máscaras que contienen a la mayoría de 7 bits se almacenan – todas las otras palabras son ignoradas
porque nunca pueden coincidir con un rompecabezas.

Building `freq` is linear in the total length of all words (≤ 3 × 106).

----------------------------------------------------

##### 3. Enumerar todos los subconjuntos de un rompecabezas que contienen la primera letra

Para un rompecabezas 'puz'

`` `
mask_p = bitmask of all 7 letters of puz
primer_bit = bit correspondiente a puz[0]
`` `

Todas las palabras válidas para este rompecabezas deben usar un subconjunto de `mask_p` que también
contiene `first_bit`.
El rompecabezas tiene sólo 7 letras, por lo que hay en la mayoría de subconjuntos `2^7 = 128`.
Los enumeramos de manera eficiente mediante la iteración sobre todos los submascos de `mask_p`:

`` `
sub = mask_p
mientras sub:
si sub contiene primer_bit:
respuesta += freq.get(sub, 0)
sub = (sub - 1) > mask_p
`` `

El bucle funciona en `O(2^7)` por rompecabezas – lo suficientemente rápido para 105 rompecabezas.

----------------------------------------------------

##### 4. Prueba de corrección

Demostramos que el algoritmo devuelve el número exacto de palabras válidas para cada
rompecabezas.

-...

##### Lemma 1
Por cada palabra `w` el algoritmo aumenta `freq[mask(w)]` exactamente una vez.

Proof.

* Mientras procesamos una palabra construimos una máscara de sus letras distintas
(`mask(w)`).
* Aumentamos `freq[mask(w)] ' una vez después de insertar la palabra en el trie
(o directamente en el diccionario).
Ningún otro paso modifica `freq[mask(w)]. ∎



##### Lemma 2
Para un rompecabezas `p` y cualquier subconjunto `S ⊆ letters(p)` que contiene " p " ,
el algoritmo añade `freq[mask(S)]` a la respuesta de `p`.

Proof.

During the enumeration of submasks of `mask(p)` every subset `S`
ocurre exactamente una vez como "sub".
Si `sub` contiene el primer bit, el algoritmo ejecuta

`` `
respuesta += freq.get(sub, 0) // sub == máscara(S)
`` `

Así `freq[mask(S)] `` se añade exactamente una vez. ∎



##### Lemma 3
Una palabra `w` se cuenta en la respuesta para un rompecabezas `p` **
`w` es una palabra válida para `p`.

Proof.

*(**Si la parte**)*
Assume `w` is valid for `p`.
Todas las letras de `w` están en `p`, así que `mask(w) ⊆ máscara(p)`.
También `p[0]  Iberia w`, por lo que `mask(w)` contiene el primer bit.
Por lo tanto `mask(w)` aparece como un submasco `sub` de `mask(p)` que contiene
por primera vez, y por Lemma plaganbsp;2 su frecuencia se añade a la respuesta.

*(**Sólo si parte**)*
Asumir el algoritmo añade `freq[mask(S)]` para un subconjunto `S ⊆ letters(p)`
que contiene " p " .
Cada palabra contada en esta frecuencia utiliza exactamente las letras de `S`.
Todas esas cartas figuran en " p " (por definición de " S " ) y " p[0] " . está en `S`,
por lo tanto cada palabra satisface las dos condiciones para ser una palabra válida
for `p`. ∎



################################################################################################################################################################################################################################################################ Theorem
Para cada rompecabezas `p` el algoritmo produce el número exacto de palabras válidas
de la lista de entrada.

Proof.

Por Lemma adultnbsp;3 una palabra contribuye a la respuesta para 'p' exactamente cuando es
válido para `p`.
Lemma implicabsp;1 garantiza que la contribución de cada palabra se cuente una vez
en `freq[mask]`.
Por lo tanto la suma producida por el algoritmo equivale al número de palabras válidas
for `p`. ∎



----------------------------------------------------

##### 5. Análisis de la complejidad

Vamos.

`` `
N = número de palabras (≤ 10^5)
M = número de rompecabezas (≤ 10^5)
`` `

*Building `freq`*
`O(longitud total de palabra)` ≤ 3 × 106

*Pregunta por rompecabezas*
Cada puzzle enumera ≤ 128 submasks
`O(2^7) = O(1)` → `O(M)` general

*Memoria*
En la mayoría de un diccionario entrada por máscara diferenciada
`≤ 2^26`, pero sólo aquellos con ≤ 7 bits se almacenan - en la mayoría 27 × N ≤ 10^5 entradas.

----------------------------------------------------

##### 6. Aplicación de la referencia (Python 3)

``python
de la importación Lista, Dict

Solución de clase:
def findNumOfValidWords(self, words: List[str], puzzles: List[str]) - título List[int]:
# ---------- construir diccionario de frecuencia --------
Dict [int, int] = {}
para w en palabras:
máscara = 0
para ch en set(w): letras distintas
mascarilla TENIDO= 1 TENIDO (ord(ch) - 97)
# Skip words that cannot match any puzzle
si mascara == 0 o mascara.bit_count() 7:
continuar
freq[mask] = freq.get(mask, 0) + 1

# ---------- respuesta para cada rompecabezas --------
res = []
para puz en rompecabezas:
mask_p = 0
por ch en puz:
mask_p TENIDO= 1  Se hizo (ord(ch) - 97)
first_bit = 1 > > (ord(puz[0]) - 97)

ans = 0
sub = mask_p
mientras sub:
si sub " first_bit:
ans += freq.get(sub, 0)
sub = (sub - 1) > mask_p
res.append(ans)

retorno
`` `

El código sigue exactamente el algoritmo probado correcto arriba y es
plenamente compatible con la firma de funciones LeetCode.

----------------------------------------------------

##### 6. Aplicación de referencia (C++)

Si prefiere C++ la misma idea se puede escribir sucintamente:

``cpp
Clase Solución {
public:
vector asignadoint confianza encontrarNumOfValidWords(vector asignadosstring iguales palabras, vector identificadostring compartir puzzles) {}
unordered_map madeint,int confianza freq; // mask - Cuenta
freq.reserve(words.size()*2);

para (continuar cadena w : palabras) {
int mask = 0;
para (carc : w) máscara Silencio= 1  Se realizó (c - 'a');
si (__construidoin_popcount(insigned)mask)
freq[mask]+; // Lemma 1
}
}

vector significar uns
ans.reserve(puzzles.size());

para (const cordón plagado puz : rompecabezas) {}
int mask = 0;
para (carc : puz) máscara Silencio= 1 Identificado (c - 'a');
primero Un poco = 1 se hizo (puz[0] - 'a');

int cnt = 0;
int sub = máscara;
(sub) { // enumerar submasks
if (sub " firstBit) { // contains first letter
auto = freq.find(sub);
si (lo != freq.end()) cnt += it- confíasecond;
}
sub = (sub - 1) " máscara;
}
ans.push_back(cnt);
}
devolver los ans;
}
};
`` `

Ambas implementaciones se ejecutan fácilmente dentro de los límites de LeetCode.