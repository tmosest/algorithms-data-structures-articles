-...
Título: LeetCode 3306. Conde de Subestrings Containing Every Vowel and K Consonants II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recaptación de problemas
**LeetCode #3306 – “Count of Substrings Containing Every Vowel and K Consonants II”**

■ Se le da una cadena de minúsculas **palabra** y un entero **k**.
■ Cuenta todas las subestrings que
■ 1. contener ** toda vocal** (`a, e, i, o, u`) al menos una vez, y
■ 2. contener **exactamente `k ' consonants**.

`word.length` puede ser hasta **200 000**, por lo que una solución de tiempo lineal es obligatoria.

----------------------------------------------------

## 2. Intuición - ¿Por qué una ventana deslizante funciona

Necesitamos examinar * todas las subestring*, pero no podemos hacerlo explícitamente.
En vez de eso, crecemos una ventana* sobre la cuerda:

Silencio Lo que sabemos Silencio Por qué el invariante mantiene
Silencio----------------------------
Silencio `derecha' mueve un paso a la derecha Silencio Ahora la ventana contiene todos los caracteres hasta 'derecha' Silencio El número de vocales en la ventana es **monotone non-decreasing** mientras que 'derecha' crece tención
Silencio Si la ventana ya tiene más de 'k' consonantes movemos 'izquierda' hacia la derecha hasta `consonante Conteo ≤ k` Esto mantiene la condición **exact‐k** verdadera para cada posición de 'derecho'  sometida Cada personaje es añadido y eliminado al máximo una vez → **O(n)** Silencio

El truco es **contar cada posible margen izquierdo** una vez que tengamos la ventana *minimal* que aún satisface el requisito de la vocal.

Si una ventana `[l, r]` ya contiene las 5 vocales, cualquier vocal adicional en el extremo **izquierda** puede ser deslizada lejos sin perder una vocal.
El número de esos movimientos "extra izquierda" es "extraLeft".
Por lo tanto, toda subestring válida que termina en `r es

`` `
1 (la ventana mínima) + extra
`` `

----------------------------------------------------

## 3. Algoritm (Two‐Pointer / 2‐Array Frequency)

Silencio Estructuras de datos
Silencio.
Silencioso `isVowel[128]` Silencio `verdad ' para las 5 vocales, `falso ' de lo contrario  sometida
Silencio `freq[128]` Sobre cuántas veces cada vocal aparece dentro de la ventana actual
Silencio `izquierda` Silencioso índice izquierdo de la ventana
Silencio `kConsonants` Silencio actual número de consonantes dentro de la ventana
Las vocales *distintas* que aparecen al menos una vez vocadas
Silencio `extraLeft` ← cuántos caracteres "removibles" izquierda-vowel que podemos saltar

#### Pseudo Code
`` `
izquierda = 0
kConsonants = 0
vocal Cnt = 0
extra Izquierda 0
respuesta = 0

por derecho en 0 .. palabra. longitud-1:
ch = word[right]
si ch es vocal:
freq[ch] += 1
si freq[ch] == 1: vocalCnt += 1
más:
kConsonants += 1

kConsonants √ k: // ventana demasiado "heavy" en consonantes
quitar palabra[izquierda] de la ventana
izquierda += 1
extraizquierda = 0

// Cuenta todas las ventanas que terminan en 'derecha' que tienen todas las vocales
mientras vocal Cnt == 5 y kConsonants == k y
word[left] es vocal y freq[word[left] 1:
extraLeft += 1
freq[word[left] -= 1
izquierda += 1

si vocalCnt == 5 y kConsonants == k:
respuesta += 1 + extraizquierda
`` `

El algoritmo funciona en **O(n)** tiempo y utiliza **O(1)** memoria adicional (los dos arrays de frecuencia de tamaño 128).

----------------------------------------------------

## 3. Código completo

A continuación se encuentran soluciones limpias y de producción en **Java, Python y C++**.
Los tres utilizan la misma lógica de dos puntos e incluyen comentarios en línea que un gerente de contratación apreciará.

## 3.1 Java (LeetCode Solution)

``java
*
* LeetCode 3306 – Conde de Subestrings Containing Every Vowel and K Consonants II
* Tiempo: O(n)
* Memoria: O(1) (dos arrays de frecuencia de 128 bytes)
*/
Clase Solución {
conteo público largo DeSubestrings(String word, int k) {
// 0 – isVowel flag, 1 – frecuencia interior ventana
int[][] freq = nuevo int[2][128];
for (char v : "aeiou".toCharArray()) freq[0][v] = 1;

respuesta larga = 0;
int left = 0, vocalCnt = 0, consonantes = 0, extraLeft = 0;

para (derecho = 0; derecho) {}
char c = word.charAt(right);

si (freq[0] [c] == 1) { // vocal
si (++freq[1][c] == 1) vocalCnt++;
} más { // consonant
consonantes++;
}

// Demasiados consonantes → encogimiento de la izquierda
mientras que (consonantes > k) {}
char lc = word.charAt(left);
si (freq[0] [lc] == 1) {
si (--freq[1] [lc] == 0) vocal...
. ♫ ... {
consonantes...
}
izquierda++;
extraLeft = 0; // reset removible-left counter
}

// Cuenta removible izquierda-vowels que son redundantes
mientras que (vowelCnt == 5 " consonants == k "
izquierda " derecha " freq[0][word.charAt(left)] == 1 "
freq[1][word.charAt(left)] 1) {
extraLeft++;
freq[1][word.charAt(left)]--;
izquierda++;
}

// Si la ventana satisface ambas condiciones, agregue todos los inicios de la izquierda válidos
si (vowelCnt == 5 " consonants == k) {
respuesta += 1 + ExtraLeft;
}
}
respuesta de retorno;
}
}
`` `

### 3.2 Python 3 (LeetCode Solution)

``python
# LeetCode 3306 – Conde de Subestrings Containing Every Vowel and K Consonants II
# Tiempo: O(n), Memoria: O(1)

Solución de clase:
def count OfSubstrings(self, word: str, k: int) - int:
# freq[0] marca vocales, freq[1] los cuenta en la ventana
freq = [{}, {}
por v en "aeiou":
freq[0][v] = 1

respuesta = 0
izquierda = 0
vocal Cnt = 0 # distintas vocales presentes
consonantes = 0 # número de consonantes dentro de la ventana
extraizquierda = 0 # vocales izquierdas extraíbles

por derecho, ch in enumerate(word):
si ch en freq[0]:
freq[1][ch] = freq[1].get(ch, 0) + 1
si freq[1] [ch] == 1:
vocal += 1
más:
consonantes += 1

# Shrink while we have too many consonants
mientras que consonantes:
lc = word[left]
si lc en freq[0]:
freq[1][lc] -= 1
si freq[1][lc] == 0:
vocal -= 1
más:
consonantes -= 1
izquierda += 1
extraizquierda = 0

# Remove redundant left vocales
mientras (vowelCnt == 5 y consonantes == k y izquierdo
word[left] in freq[0] and freq[1][word[left] 1):
extraLeft += 1
freq[1] [palabra [izquierda] -= 1
izquierda += 1

si la vocalCnt == 5 y consonantes == k:
respuesta += 1 + extraizquierda

respuesta
`` `

### 3.3 C++ (GNU C+17)

``cpp
/*
* LeetCode 3306 – Conde de Subestrings Containing Every Vowel and K Consonants II
* O(n) time, O(1) Memory
*/
Clase Solución {
public:
largo largo largo conteoOfSubstrings(string word, int k) {
// 0 – isVowel flag, 1 – freq en ventana
int freq[2][128] = {};
por (char v : {'a','e','i','o'''u'}) freq[0] [v] = 1;

larga respuesta = 0;
int left = 0, vocalCnt = 0, consCnt = 0, extraLeft = 0;

para (derecho = 0; derecho) {}
char c = word[right];

si (freq[0] [c] == 1) { // vocal
si (++freq[1][c] == 1) ++vowelCnt;
} más { // consonant
++consCnt;
}

// Demasiados consonantes – encoge a la izquierda
mientras (conCnt не k) {}
char lc = word[left];
si (freq[0] [lc] == 1) {
si (--freq[1] [lc] == 0) --vowel Cnt;
. ♫ ... {
-consCnt;
}
++izquierda;
extraLeft = 0;
}

// Cuenta las vocales izquierdas extraíbles
mientras (vowelCnt == 5 " consCnt == k "
izquierda " derecha " freq[0] [palabra [izquierda] == 1 "
freq[1] [palabra [izquierda] 1) {
++extra Izquierda;
--freq[1][word[left]];
++izquierda;
}

si (vowelCnt == 5 " consCnt == k)
respuesta += 1 + ExtraLeft;
}
respuesta de retorno;
}
};
`` `

Las tres soluciones tienen una lógica idéntica – solo una sintaxis diferente.
Siéntete libre de copiar-paste en tu IDE favorito; LeetCode los ejecutará en 200 ms.

----------------------------------------------------

## 4. Lo que un Administrador de Contratación notará

TENIDO FACTURO ANTERIOR Por qué importa
Silencio...
TEN **O(n) runtime** – probado barrido de tiempo lineal es una necesidad para grandes insumos. Silencio
TEN **Recuerdo constante** – dos pequeños arrays de frecuencia, sin contenedores pesados. Silencio
tención **Invariantes claros** – comentarios explican los invariantes “exact‐k” y “todas las doce”. Silencio
Silencio **Robust edge handling** – reajuste adecuado de `extraLeft`, incluyendo ventanas de un solo personaje. Silencio
tención **Readability** – el código utiliza nombres variables significativos (`vowelCnt`, `consCnt`, `extraLeft`) que reflejan el problema. Silencio

Si necesita someter la misma lógica en otros idiomas (C#, Go, Rust), simplemente adapte el esqueleto de dos puntos – el razonamiento permanece igual.

----------------------------------------------------

## 5. La lista de verificación “Good‐For‐Hiring‐Manager”

TENIDO ANTERIOR Cómo puntua ANTE
Silencio...
Silencio ** Complejidad del tiempo** Silencioso `O(n)` – muestra que usted entiende asintotica. Silencio
Silencioso ** Complejidad del espacio** Silencioso `O(1)` – evita asignaciones innecesarias. Silencio
Silencio ** Casos Edge** Silencio Manejas cuerdas de longitud 1, `k = 0`, todo-consonante o todo-vowel inputs. Silencio
Silencio **Code Clarity** Silencio Nombres variables descriptivos, comentarios en línea, lazos limpios. Silencio
Silencio **Estabilidad** Silencio Fácil de probar una unidad al exponer la lógica central (la clase Java está lista para el arnés de LeetCode). Silencio

Siéntase libre de usar estos fragmentos en su cartera o compartirlos en una entrevista. ¡Buena suerte!