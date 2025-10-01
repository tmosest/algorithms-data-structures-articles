-...
Título: LeetCode 2950. Número de subestrings divisibles -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2950 – Number of Divisible Substrings
** Tipo de problema:** Mediana
**Tiempo de tiempo:** 2 s (conejo O(9 · n))
**Límite de espacio:** 256 MB

-...

### 1. Declaración sobre problemas

■ Cada carta de Inglés de minúscula se asigna a un dígito (ver la tabla de abajo).
■ Un **substring** de una cadena es cualquier secuencia contigua, no vacía de caracteres.
■ Una subestring es **divisible** si la suma de los valores mapeados de sus caracteres es divisible por su longitud.
■ Dada una cadena `palabra' (1 ≤ tenciónword perpetua ≤ 2000), devuelve el número de subestrings divisibles de `palabra`.

Silencio tóxico tóxico
Silencio...
TENIDO A, b ANTERIOR 1
TENIDO C, d, e TENIDO 2
Silencio f, g, h
Silencio, j, k Silencio 4
Silencio, m, n Silencio 5
TENIDO O, P, q TENIDO 6
TENIDO , s, t ANTE LAS 7
tención u, v, w Silencio 8
Silencio x, y, z Silencio 9

*Ejemplos*

Silencioso `palabra` respuesta permanente
Silencio--------------------
Silencio `asdf` Silencio 6 Silencio ver la tabla de la muestra en la declaración del problema
Silencioso `bdh` Silencio 4 Silencio `'b', `'d', `'h', ``, `'bdh'`
. . . . . . . . . . . . . . . .

-...

### 2. Intuición: “promedio = entero”

Para una subestring de longitud `p`, sus valores mapeados sean `f(c1)...f(cp)`.
La subestring es divisible iff

`` `
f(c1)+f(c2)+...+f(cp)
- Es un entero.
p
`` `

Así, el valor **promedio** de la subestring debe ser un entero entre 1 y 9.

Si arreglamos un promedio de 'a' (1 ≤ a ≤ 9) podemos preguntar: *cuántas subestrings tienen un promedio exactamente 'a'? *

Para un `a' dado

`` `
f(c1)+...+f(cp) = p · a
(f(c1)-a) + ... + (f(cp)-a) = 0
`` `

Así que el problema se reduce a contar sub-arrays cuya suma **transformada es cero**.
Eso se puede hacer en tiempo lineal con un truco prefijo-sum + hash‐map.

Debido a que sólo hay 9 promedios posibles, simplemente repetimos el escaneo lineal 9 veces – **O(9 · n)** en general.

-...

### 3. Algoritmo (medidas exactas)

1. **Preparar la asignación**
`int val[26] = {1,1,2,2,3,4,4,5,5,6,7,7,8,8,8,9,9}; ``

2. **Respuesta = 0**

3. Por cada `a' de 1 a 9
* `diff[i] = val[word [i]-'a'] - a` (valor desformado)
* Computar la suma prefijo de `diff` y almacenar cada prefijo en un hash-map
( " prefijo[sum] " = cuántas veces esta suma ha aparecido hasta ahora).
* Cada vez que la actual suma de prefijo `s` se ve de nuevo, todos los sub-arrays entre las dos posiciones tienen suma 0 → todos tienen promedio `a`.
* Incrementar la respuesta por el número de pares de sumas iguales de prefijo.

4. Devuelve la respuesta.

-...

### 3. Pseudocode

`` `
ans = 0
para una en 1..9:
mapa = mapa de hash vacío // clave = suma de prefijo, valor = frecuencia
mapa[0] = 1 // prefijo vacío
Cura = 0
para cada personaje ch en palabra:
cur += valor[ch] - a
ans += mapa.getOrDefault(cur, 0)
mapa[cur] = map.getOrDefault(cur, 0) + 1
Retorno
`` `

-...

### 4. Análisis de la complejidad

TEN TERRITOR ANTERIOR ANTERIOR ANTE ANTERIOR ANTE ANTE ANTE ANTE ANTE ANTE ANTE
Silencio----------------------
TENIDO TIEMPO TENIDO 9 · TERRITORIO TENIDO **O(9 · n)** (Aplauso 18 000 operaciones para el peor de los casos `n = 2000`) Silencio
TENIDO Memoria TENIDO tamaño del mapa de Hash (el mapa es recreado 9 veces, pero cada copia es descartada inmediatamente)

Ambos límites se cumplen fácilmente para las limitaciones dadas.

-...

### 5. Implementaciones de referencia

■ Las siguientes soluciones siguen la misma lógica y se pueden pegar directamente en la pestaña LeetCode “Custom”.

-...

##### 5.1 Java

``java
Clase Solución {
/ / / 1- asignación basada para 'a'. '
privada estática final int[] MAP = {
1, 2, 2, 3, 3, 3, 4, 4, 4,
5, 5, 5, 6, 6, 7, 7, 8, 8, 9, 9
};

public long divisible Subestrings(String word) {
ans largas = 0;
int n = word.length();

para (int avg = 1; avg = 9; avg++) {}
/ / prefijo suma hash mapa
HashMap hizoInteger, Integer confianza prefCnt = nuevo HashMap incorrecto();
prefCnt.put(0, 1); // prefijo vacío

int cur = 0;
para (int i = 0; i)
int val = MAP[word.charAt(i) - 'a'];
cur += val - avg; // transformar a valor - avg
ans += prefCnt.getOrDefault(cur, 0);
prefCnt.put(cur, prefCnt.getOrDefault(cur, 0) + 1);
}
}
devolver los ans;
}
}
`` `

-...

#### 5.2 Python

``python
Solución de clase:
# mapping table: 0 → a, 1 → b, 2 → c, etc.
_MAP = [
1, 2, 2, 3, 3, 3, 4, 4, 4,
5, 5, 5, 6, 6, 7, 7, 8, 8, 9, 9
]

def divisible Subestrings(self, word: str) - título int:
ans = 0
n = len(palabra)

para avg en rango(1, 10):
Pref = {0: 1}
Cura = 0
para ch en palabra:
cur += self._MAP[ord(ch) - 97] - avg
ans += pref.get(cur, 0)
pref[cur] = pref.get(cur, 0) + 1
Retorno
`` `

-...

#### 5.3 C++

``cpp
Clase Solución {
public:
largas largas divisiblesSubstrings(string word) {
static const int MAP[26] = {
1, 2, 2, 3, 3, 3, 4, 4, 4,
5, 5, 5, 6, 6, 7, 7, 8, 8, 9, 9
};

ans largos = 0;
int n = word.size();

para (int avg = 1; avg = 9; ++avg) {
unordered_map madeint, int confidencial prefCnt;
prefCnt.reserve(n + 1);
prefCnt[0] = 1; // prefijo vacío
int cur = 0;
por (char ch : word) {
cur += MAP[ch - 'a'] - avg;
ans += prefCnt[cur];
++prefCnt[cur];
}
}
devolver los ans;
}
};
`` `

-...

## 🚀 “Cómo resolver el código de Leet 2950: Número de subestrings visibles” – Una guía de blogs

■ **Emergido público:** entusiastas de LeetCode, entrevistadores, estudiantes de algoritmos de estructura de datos
■ **Core keywords:** *Leetcode 2950*, *Número de Subestrings Divisibles*, *subestrings divisibles*, *prefix sum trick*, *letter mapping to digits*

-...

### 1. Por qué “Número de Subestrings Divisibles” suena como una pregunta de truco

El nombre mismo indica que tenemos que pensar en **divisibilidad** y **sustancias**.
Si ignoras la asignación de letra a dígitos y simplemente fuerza bruta todas las subestrings `O(n2)`, llegarás al límite de tiempo.
El verdadero truco es reconocer que el *medio* de los valores mapeados tiene que ser un ** entero** (1–9).

-...

### 2. El truco del “medio = entero”

1. **Average = integer** – for a substring of length `p`

`` `
(suma de valores mapeados) / p debe ser un entero
`` `

2. **Fix an average `a`** (1–9) and ask
*“¿Cuántas subestrings tienen este promedio exacto?”*

3. **Transforma el array**
Por cada posición " compute `value[i] - a ' .
Ahora una subestring tiene un promedio de **iff** la suma transformada sobre esa subestring es **cero**.

4. **Subarros de suma cero**
Classic prefix‐sum + hash‐map truco:
``text
pref[0] = 0
para cada uno i:
pref[i+1] = pref[i] + diff[i]
cualquier par (l,r) con pref[l] == pref[r] ⇒ sum of diff[l.r-1] == 0
`` `

5. **Repetir para los 9 promedios** – total complejidad `O(9 · n)`.

-...

### 3. Por qué esto supera la ingenua solución O(n2)

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
Silencio Brute‐force Silencio O(n2) Silencio 20002 Ω 4 millones de cheques – todavía está bien, pero la constante es alta. Silencio
tención Prefix‐sum + truco promedio tención O(9 · n) tención 9 × 2000 = 18 000 operaciones – casi insignificante. Silencio
Silencio espacio adicional Silencio O(n) Silencio Sólo un hash‐map por promedio. Silencio

El test-suite LeetCode es generoso, pero los entrevistadores aman soluciones que funcionan en tiempo lineal después de un pequeño factor constante.

-...

### 4. Detalles de la aplicación

##### 4.1 Mapping table

El problema define un mapeo no alfabético:

`` `
a,b → 1
c,d,e → 2
f,g,h → 3
i,j,k → 4
l,m,n → 5
o,p,q → 6
r,s,t → 7
u,v,w → 8
x,y,z → 9
`` `

La mayoría de las soluciones pre-crean una variedad de longitud 26 para que `valor[ch - 'a']` se ejecuta en O(1).

##### 4.2 Códigos

A continuación se presentan implementaciones limpias y listas de producción en los tres idiomas más comunes.

-...

################################################################################################################################################################################################################################################################

■ Usa un `HashMap observadoInteger, Integer `` para las frecuencias prefijo.

``java
Clase Solución {
privada estática final int[] MAP = { /* 26‐element mapping */ };

public long divisible Subestrings(String word) {
ans largas = 0;
int n = word.length();

para (int avg = 1; avg = 9; avg++) {}
HashMap hizoInteger, Integer confianza prefCnt = nuevo HashMap incorrecto();
prefCnt.put(0, 1);
int cur = 0;
para (int i = 0; i)
cur += MAP[word.charAt(i) - 'a'] - avg;
ans += prefCnt.getOrDefault(cur, 0);
prefCnt.put(cur, prefCnt.getOrDefault(cur, 0) + 1);
}
}
devolver los ans;
}
}
`` `

####### 4.2.2 Python

■ Usa un diccionario para las frecuencias prefijo.

``python
Solución de clase:
_MAP = [1,2,2,2,3,3,4,4,5,5,6,6,7,7,8,8,9,9]

def divisible Subestrings(self, word: str) - título int:
ans = 0
para avg en rango(1, 10):
Pref = {0: 1}
Cura = 0
para ch en palabra:
cur += self._MAP[ord(ch)-97] - avg
ans += pref.get(cur, 0)
pref[cur] = pref.get(cur, 0) + 1
Retorno
`` `

################################################################################################################################################################################################################################################################

■ Utiliza `unordered_map` con `reserve` para evitar rehashing.

``cpp
Clase Solución {
public:
largas largas divisiblesSubstrings(string word) {
static const int MAP[26] = { /* 26‐element mapping */ };
ans largos = 0;
int n = word.size();

para (int avg = 1; avg = 9; ++avg) {
unordered_map madeint,int titulada prefCnt;
prefCnt.reserve(n+1);
prefCnt[0] = 1;
int cur = 0;
por (char ch : word) {
cur += MAP[ch-'a'] - avg;
ans += prefCnt[cur];
++prefCnt[cur];
}
}
devolver los ans;
}
};
`` `

-...

### 5. Prueba de su solución

1. **Edge case**: `'aaaa'` - todos los valores son 1, por lo que cada subestring tiene un promedio de 1 → respuesta = `n*(n+1)/2`.
2. **Random strings** – generar `palabra` de longitud 2000, comprobar contra el solucionador de fuerza bruta O(n2) para la corrección.
3. **Prueba del estrés** – ejecutar muchos casos aleatorios para asegurar que no se desborde (la respuesta se ajusta a " largo " ).

-...

### 6. Takeaway

- Reconocer las restricciones ocultas: el promedio de los dígitos mapeados debe ser un entero.
- Convierta el problema en contar subarrays de cero suma** – una técnica clásica.
- Mantener el mapeo como un array para las búsquedas O(1).
- Repetir por cada uno de los 9 promedios posibles - lineal en general.

Con esta mentalidad, resolverás a LeetCode 2950 en un flash e impresiona a los entrevistadores con un algoritmo limpio y eficiente.

-...

■ *Feliz codificación, y que su próxima entrevista sea una brisa!* 🚀

-...



**End de la guía. #