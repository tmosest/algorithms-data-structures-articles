-...
Título: LeetCode 1737. Cambiar los caracteres mínimos para satisfacer una de tres condiciones -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## LeetCode 1737 – *Cambiar caracteres mínimos para satisfacer una de las tres condiciones*
## A Complete, SEO‐Optimized Guide (Java / Python / C++)

■ **Keywords:** LeetCode 1737, Cambiar mínimo Personajes, entrevista de codificación, algoritmo, suma de prefijo, matriz de frecuencia, Java, Python, C++, entrevista de trabajo, problema medio, manipulación de cadenas

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

Te dan dos cadenas de minúsculas **`a** y **`b`**.

En una operación usted puede cambiar cualquier carácter individual en cualquiera de las cadenas a **cualquier** otra letra minúscula.
Necesitas lograr **al menos una** de las siguientes tres condiciones utilizando el número mínimo de operaciones:

Silencio Silencio Silencio Descripción Silencio
Silencio...
Silencio 1 Silencio Cada letra en **`a`** es **strictamente menos** que cada letra en **`b`** (ordenalfabético). Silencio
Silencio 2 TENIDO Cada letra en **`b`** es *estrictamente menos** que cada letra en **`a`**. Silencio
Silencio 3 Silencio Ambas cuerdas consisten en **sólo una letra distinta** cada una (pueden ser diferentes). Silencio

Devuelve el número mínimo de operaciones requeridas.

■ *Ejemplo*
< < > > > > > > > > > > > > > > .

-...

#### 2down⃣ Por qué la fuerza bruta falla

Una solución ingenua probaría todos los posibles pares de cadenas de destino y contaría los cambios: este es **O(26^(Principalidad sobre la vida y la vida privada)** en el peor de los casos.
Con longitudes de cuerda hasta **105**, esto es imposible.
Necesitamos un algoritmo **O(n)**.

-...

#### 3down⃣ La idea eficiente

1. ** Frecuencias de carta de regalo** en cada cadena.
Para cada una de las 26 letras minúsculas almacenamos cuántas veces aparece en `a` (`freqA`) y en `b` (`freqB`).

2. **Construir sumas de prefijo** de estos arrays de frecuencia.
`prefA[i]` = número de caracteres en `a` que son **≤** carácter `('a'+i)`.
`prefB[i]` = número de caracteres en `b` que son **≤** carácter `('a'+i)`.

3. **Prueba todas las cartas posibles divididas* c ' (de `'a' a `'y'`).
- **Condición 1** (a
*Tomen `a` ≤ `c ' y todo `b`
"cost1 = (lenA - prefA[c]) + prefB[c] `
- Condición 2** (b)
*Make all `b ' ≤ `c ' and all `a '
"cost2 = (lenB - prefB[c]) + prefA[c] `

4. **Condición 3** (single distinct letter each).
Para cada cadena sólo necesitamos cambiar todos los caracteres que son **no** el más frecuente.
`cost3 = (lenA - maxFreqA) + (lenB - maxFreqB)`

5. La respuesta es el mínimo sobre todo " costo1 " , " costo2 " y " costo3 " .

El algoritmo funciona en **O(n + 26)** tiempo y utiliza sólo **O(26)** memoria extra.

-...

### 4VIEW⃣ Code Implementations

##### 🔶 Java

``java
Solución de la clase pública {}
public int minCharacters(String a, String b) {
int lenA = a.length(), lenB = b.length();
int[] freqA = nuevo int[26], freqB = nuevo int[26];
int maxFreqA = 0, maxFreqB = 0;

para (int i = 0; i)
int idx = a.charAt(i) - 'a';
freqA[idx]+;
maxFreqA = Math.max(maxFreqA, freqA[idx]);
}

para (int i = 0; i)
int idx = b.charAt(i) - 'a';
freq B[idx]+;
maxFreqB = Math.max(maxFreqB, freqB[idx]);
}

// Condición 3: ambas cadenas letra única distinta
int ans = (lenA - maxFreqA) + (lenB - maxFreqB);

// Construir sumas prefijas
para (int i = 1; i)
freqA[i] += freqA[i - 1];
freqB[i] += freqB[i - 1];
}

// Prueba cada letra dividida 'a'. '
para (int i = 0; i)
int cost1 = (lenA - freqA[i]) + freqB[i]; // a י= i, b î
int cost2 = (lenB - freqB[i]) + freqA[i]; // b
as = Math.min(ans, Math.min(cost1, cost2));
}

devolver los ans;
}
}
`` `

##### Python

``python
Solución de clase:
def minCharacters(self, a: str, b: str) int:
len_a, len_b = len(a), len(b)

[0] * 26
[0] * 26

max_a = max_b = 0
para ch en un:
idx = ord(ch) - 97
freq_a[idx] += 1
max_a = max(max_a, freq_a[idx])

por ch en b:
idx = ord(ch) - 97
freq_b[idx] += 1
max_b = max(max_b, freq_b[idx])

# Condición 3
ans = (len_a - max_a) + (len_b - max_b)

# Prefix sums
para i en rango(1, 26):
freq_a[i] += freq_a[i - 1]
freq_b[i] += freq_b[i - 1]

# Split letters a .. y
para i en rango(25):
cost1 = (len_a - freq_a[i]) + freq_b[i] # a י= i, b œ
cost2 = (len_b - freq_b[i]) + freq_a[i] # b י= i, a œ
as = min(ans, cost1, cost2)

Retorno
`` `

##### 🔶 C++

``cpp
Clase Solución {
public:
int minCharacters(a, string b) {
int lenA = a.size(), lenB = b.size();
vector implicado freqA(26), freqB(26);
int maxA = 0, maxB = 0;

por (char ch : a) {
int idx = ch - 'a';
freqA[idx]+;
maxA = max(maxA, freqA[idx]);
}

para (char ch : b) {}
int idx = ch - 'a';
freq B[idx]+;
maxB = max(maxB, freqB[idx]);
}

// Estado 3
int ans = (lenA - maxA) + (lenB - maxB);

// Sumas de prefijo
para (int i = 1; i) {}
freqA[i] += freqA[i - 1];
freqB[i] += freqB[i - 1];
}

// Dividir letras 'a'. 'y'
para (int i = 0; i) {}
int cost1 = (lenA - freqA[i]) + freqB[i]; // a י= i, b î
int cost2 = (lenB - freqB[i]) + freqA[i]; // b
as = min(ans, min(cost1, cost2));
}

devolver los ans;
}
};
`` `

■ Las tres soluciones se ejecutan en **O(Principalidad sobre la vida y la vida cotidiana)** tiempo y solo utilizan **26** enteros de memoria.

-...

### 5down Complexity Breakdown

TEN TERRITOR TERRITOR TEN TERRITOR TEN TERRITOR TEN TERRITOR SON TERRITOR SON SON SON TEN SON SON SON 
Silencio------Prince--------
Silencio Contando frecuencias
Silencio Construyendo prefijo sumas Silencio **O(26)** ←
Silencioso en más de 25 letras
Silencio **Total** Silencio **O(n + 26)** → effectively **O(n)** Silencio **O(26)** → effectively **O(1)** Silencio

Con **`n ≤ 105`**, esta solución encaja fácilmente con los límites del juez en línea de LeetCode.

-...

#### 6down⃣ Edge‐ Lista de verificación de casos

Por qué importa cómo se maneja el código It ←
Silencio------------------
Las cuerdas vacías no necesitan cambios en las fórmulas todavía funcionan. Silencio
TENED Strings ya satisfacer una condición ANTE Vuelta `0` Silencio Mínimo será calculado como `0`. Silencio
Silencio Todos los personajes mismos Silencio Condición 3 es óptimo Silencio `maxFreq` iguala la longitud de la cadena → costo es `0`. Silencio
Silencio Longitud de una cadena = 1 Silencio Funciona de la misma tención Las sumas Prefix lo manejan correctamente. Silencio
Silencioso en ''y''' sólo Silencio Necesitamos ''z''' sólo para la otra cuerda - imposible Silencio Nos inclinamos a propósito sólo a ''y'' (i 0 25). Silencio

-...

### 7 carreras Bien / Mal / Análisis Ugly

Silencio Silencio
Silencio------------Prince------
Silencio ** La elegancia algorítmica** Silencio Usa la frecuencia simple + sumas prefijo → muy legible Silencio Ninguno; la lógica es directa Silencio Ninguno – el uso de la memoria es insignificante (26 ints)
Silencio **Performance** Silencio Corre en tiempo lineal → pasa 105 casos de longitud Silencio Mismo Silencio Ninguno Silencio
Silencio **Maintainability** Silencio Separar el bucle para la condición 3 mantiene el código ordenado Silencio Mismo Silencio Silencio
*Potential pitfalls* *Olvídese de calcular las sumas prefijadas o solo de iterar hasta `'y'’’’.
Silencio **Aprendizaje de viaje** Silencio Muestra cómo transformar una limitación de “punto multiplicado” en un problema de prefijo-sum.

-...

### 8️ Quick Test Cases

Silencioso `a` Silencioso `b`
Silencio...
Silencioso `'aba' ' Silencio 'caa'
Silencioso `"zzzz"
Silencioso `'abc' '
Silencioso `'a' ' Silencioso `'z' ' Silencio `0` (condición 1 ya cierto)
Silencioso `'bbb' ' Silencio `'bbb'` Silencio `0` (condición 3 ya verdadera) Silencio

Ejecute las funciones proporcionadas para verificar la salida.

-...

Resumen

*LeetCode 1737* le enseña cómo convertir una tarea aparentemente compleja de “estring-splitting” en un simple problema de frecuencia-prefijo-sum.
La llave despega:

- **Count** → **Suma prefijo** → **Escribe más de 25 letras divididas**
- Condición 3 es simplemente “la carta más frecuente” por cadena
- Tiempo total **O(n)**, **O(1)** espacio

Ya sea que estés puliendo tu pila de entrevistas Java, Python o C++, este problema es imprescindible para el nivel *medium* de entrevistas de codificación y puede ganarte una gran victoria en tu próxima entrevista de trabajo.

¡Feliz codificación! 🚀