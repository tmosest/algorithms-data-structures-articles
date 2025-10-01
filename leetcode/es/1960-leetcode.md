-...
Título: LeetCode 1960. Maximum Product of the length of Two Palindromic Substrings -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. El problema – 1960. Producto máximo de la longitud de dos subestrings palindromicos

■ **Given** una cadena `s` (2 ≤  vidas eternas ≤ 105), encontrar **dos subestrings paleindromicos no superpuestos** cuyo producto de longitudes es maximal.
■ Devuelve ese producto máximo.

TEN SON SON SON SON SON SON SON SON SON 
Silencio----------------------------------------------------
Silencio 1 Silencioso `'ababbb'` Silencio `9` Silencio `'aba' (3) and `'bbb'` (3) → 3 × 3 = 9
Silencio 2 Silencioso `'zaaaxbbby'` Silencio `9` Silencio `'aaa' (3) and `'bbb'` (3) → 3 × 3 = 9

¿Por qué es difícil? #
- Debemos comprobar todo palindrome de longitud.
- La cadena puede ser de 100 000 caracteres de largo, por lo que un enfoque O(n2) es imposible.
- Las dos subestrings no deben superponerse, lo que significa que debemos combinar la información de *ambos* lados de la cadena.

La clave es usar **El algoritmo de Manacher** para conseguir todos los palindromas de longitud extraña en tiempo lineal, luego combinar prefijo y sufijo-maximums.

-...

## 2. Resumen del algoritmo

1. **El palindrome más largo y completo en cada centro* *
`odd[i]` = longitud máxima extraña de un palindrome centrado en el índice `i` (Manacher).
(La fuerza está garantizada a ser extraña.)

2. **Edificio prefijo de matriz máxima**
`pref[i]` = longitud de palindromo más larga en `s[0...i]`.
Recurrencia: `pref[i] = max(pref[i-1], odd[i]).

3. **Construir sufijo de matriz máxima**
`suff[i]` = longitud de palindromo más larga en `s[i...n-1]`.
Recurrencia: `suff[i] = max(suff[i+1], odd[i]).

4. # Dobla la cuerda una vez #
Para cada posición de división `i' (0 ≤ i) el primer palindromo debe terminar en o antes `i`, el segundo debe comenzar en o después de 'i+1`.
El mejor producto para esa división es `pref[i] * suff[i+1]`.

5. *Toma el máximo sobre todas las divisiones*.

**Las complejidades* *

- Tiempo: **O(n)** – un paso para Manacher, dos pases lineales para prefijo/suffix, un pase lineal para la división.
- Memoria: **O(n)** – arrays `odd`, `pref`, `suff`.

-...

## 3. Código

A continuación encontrará implementaciones limpias y listas de producción en **Java**, **Python**, y **C+**.
Los tres resuelven el problema en el mismo tiempo O(n) y O(n) espacio.

-...

### 3.1 Java

``java
importar java.util*;

Solución de la clase pública {}
int public int maxProduct(String s) {
int n = s.length();
int[] odd = manacherOdd(s);
int[] pref = nuevo int[n];
int[] suff = nuevo int[n];

// prefijo max
pref[0] = odd[0];
para (int i = 1; i) {}
pref[i] = Math.max(pref[i - 1], odd[i]);
}

// sufijo max
[n] = odd[n] - 1);
para (int i = n - 2; i 0; i--) {
suff[i] = Math.max(suff[i + 1], odd[i]);
}

int best = 0;
para (int i = 0; i)
mejor = Math.max(best, pref[i] * suff[i + 1]);
}
devolver mejor;
}

* Manacher para palindromas de longitud impar */
int privado[] Manacher Odd(String s) {
int n = s.length();
int[] d = nuevo int[n]; // d[i] = radio máximo (la longitud media)
int center = 0, right = 0;
para (int i = 0; i)
int k = (i i) correctamente? Math.min(d[center + right - i], right - i) : 1;
mientras (i - k >= 0 " , i + k " , no " .charAt(i - k) == s.charAt(i + k)
k++;
}
d[i] = k;
si (i + k ître derecho) {
centro = i;
derecho = i + k;
}
}
int[] oddLen = nuevo int[n];
para (int i = 0; i)
oddLen[i] = d[i] * 2 - 1; // convert radius to length
}
Retorno extrañoLen;
}

// Para pruebas rápidas
public static void main(String[] args) {
Solución sol = nueva solución ();
System.out.println(sol.maxProduct("ababbb"); // 9
System.out.println(sol.maxProduct("zaaaxbbby"); // 9
}
}
`` `

**Puntos clave* *

- `manacher Odd ' regresa *odd* longitudes de palindrome directamente.
- Los arrays Prefix/suffix almacenan la longitud máxima hasta ahora / desde el final.
- El bucle final considera cada división una vez.

-...

#### 3.2 Python

``python
Solución de clase:
def maxProduct(self, s: str) - título int:
n = len(s)

Manacher for odd palindromes...
d = [0] * n # radio
centro = derecha = 0
para i en rango(n):
k = 1 si me consiente= right else min(d[center + right - i], right - i)
mientras yo... 0 y i + k Identificado n y s[i - k] == s[i + k]:
k += 1
d[i] = k
si yo + k Bien.
centro, derecha = i, i + k

extraño = [2 * r - 1 para r en d] # longitud extraña en cada centro

# --- prefijo y sufijo máximos ---
* n
* n
pref[0] = odd[0]
para i en rango(1, n):
pref[i] = max(pref[i - 1], odd[i]

[n] = odd[n] - 1]
para i en rango(n - 2, -1, -1):
suff[i] = max(suff[i + 1], odd[i]

# -... combinar sobre divisiones...
mejor = 0
para i en rango(n - 1):
mejor = max(best, pref[i] * suff[i + 1])

mejor


# Arnés de prueba simple
si __name_ == "__main__":
sol = Solución()
print(sol.maxProduct("ababbb") # 9
print(sol.maxProduct("zaaaxbbby") # 9
`` `

-...

### 3.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxproduct(string s) {
int n = s.size();
vector implicado extraño = manacherOdd(s)
vector implicado pref(n), suff(n);

pref[0] = odd[0];
para (int i = 1; i)
pref[i] = max(pref[i-1], odd[i]);

suff[n-1] = odd[n-1];
para (int i = n-2; i 0; i)
suff[i] = max(suff[i+1], odd[i]);

int best = 0;
para (int i = 0; i)
mejor = max(best, pref[i] * suff[i+1]);

devolver mejor;
}

privado:
vector asignadoint edad manacherOdd(const string &s) {
int n = s.size();
vector asignadointento d(n, 1); // radius
int center = 0, right = 0;
para (int i = 0; i) {}
int k = (i i) correctamente) min(d[center + right - i], right - i) : 1;
mientras (i - k >= [i+k] ++k;
d[i] = k;
si (i + k ître derecho) {
centro = i;
derecho = i + k;
}
}
vector:
para (int i = 0; i)
oddLen[i] = d[i]*2 - 1; // longitud, no radio
Retorno extrañoLen;
}
};

// prueba
int main() {}
Sol de solución;
cout se hizo sol.maxProduct("ababbb")
cout se hizo sol.maxProduct("zaaaxbbby")
}
`` `

-...

## 4. Blog Artículo – “El Bien, el Mal y el Ugly de Leetcode 1960”

■ **Título**: *El Bien, el Mal y el Ugly de Leetcode 1960 – Dominar el Producto Máximo de Dos Subestrings Palindromic*
■ **Descripción de los datos**: Aprende a resolver Leetcode 1960 en Java, Python y C++ con una solución O(n). Entender las trampas, los cortes comerciales y el enfoque de entrevista amigable usando el algoritmo de Manacher.

-...

#### 4.1 Por qué este problema importa

Los entrevistadores aman los problemas que le obligan a pensar en ** subestructuras óptimas** y ** tiempo lineal** trucos.
Leetcode 1960 es una mezcla perfecta:

- Pide dos subestrings palindrómicos sin superposición*.
- La restricción Ø 105 garantiza que no se puede permitir cheques cuadráticos.
- La respuesta gira en las longitudes *máximo palindrome* en cada lado de una división, no en las subestrings actuales.

Cracking este problema muestra que puedes:

- Use *El algoritmo de Manacher* para computar radios de palindrome en O(n).
- Combina resultados con escaneos prefijo/suffix en un solo pase.
- Manejar las condiciones del límite limpiamente.

-...

#### 4.2 El Bien

Silencio Lo que aprendemos
Silencio----------
Silencio **Linear time** Silencio Impresionará a los entrevistadores con una solución O(n) donde la mayoría de los enfoques ingenuos son O(n2). Silencio
Silencio **La magia de Manacher** Silencio Un algoritmo que puede ser reutilizado para muchos problemas de palindroma. Silencio
tención **Prefix‐suffix DP** tención Técnica clásica para combinar dos mitades de una cadena. Silencio
Silencio **Código limpio** Silencio Todas las tres implementaciones son sucintas y fáciles de leer – un plus para revisión de código. Silencio
tención **Language‐agnostic** TEN Java, Python, C++ están disponibles todas las soluciones, mostrando su versatilidad. Silencio

-...

#### 4.3 The Bad

Silencio Pitfall Silencio Cómo evitarlo
Silencio...
Silencio **Mixing up radius and length** Silencio Siempre recuerda que el `d[i] de Manacher es un *radius*; la longitud extraña es `2*d[i] - 1`.
Silencio ** Index off‐by-one on splits** Silencio Splits debe ser entre `i` y `i+1`. Un error común es incluir caracteres superpuestos. Silencio
Silencio **Neglecting odd‐length requirement** Silencio Si usas un algoritmo de palindromo completo (incluyendo longitudes), debes filtrar o ignorar incluso longitudes. Silencio
Silencio **Usando mucho tiempo donde la int es suficiente** Silencio El producto de dos longitudes ≤ 105 cada ajuste en 32 bits firmado int. Evite conversiones innecesarias de 64 bits a menos que la entrevista pregunte explícitamente. Silencio

-...

### 4.4 The Ugly

Silencio Comportamiento Ugly _ Por qué es feo
Silencio--------------------------------
Silencio **O(n2) fuerza bruta** Silencio Probar cada par de centros y expandir es tentador pero conduce a TLE en 105 cuerdas. Silencio
Silencio **Dos dimensiones DP** Silencio Algunas soluciones construyen erróneamente una tabla de la existencia del palindromo, soplando la memoria. Silencio
Silencio **Hashing complejo** Silencio Rolling hash puede detectar palindromas en O(1) después de O(n) preprocesamiento, pero las constantes son enormes y el código es frágil. Silencio
Silencio **Over-engineering the split** Silencio La gente trata de ordenar los palindromos por longitud y luego elegir codiciadamente dos, que falla cuando los palindromas se superponen de maneras complejas. Silencio

-...

### 4.5 How to Nail the Interview

1. **Explicar las limitaciones** – Destacar la necesidad de tiempo lineal.
2. **Describe Manacher en palabras** – “Mantiene una ventana de palindrome actual y refleja el lado izquierdo para adivinar radio. ”
3. #Mostrar el truco del prefijo # “Sólo necesitamos el mejor palindromo que termina antes de una división y lo mejor que comienza después. ”
4. ** Casos de ventaja de discusos** – ¿Y si no hay palindromo en un lado? La respuesta es 0, que se maneja automáticamente.
5. **Offer the code** – Proveer los snippets Java/Python/C++.
6. **Respuestas preguntas de seguimiento** – “¿Y si se permitían longitudes?” o “¿Podemos devolver las subestrings? ”

-...

### 4.6 SEO Palabras clave (para la búsqueda de empleo)

- Leetcode 1960
- Producto máximo de dos substrings palindrómicos
- Solución Java Leetcode 1960
- Solución pitón Leetcode 1960
- Solución C++ Leetcode 1960
- Entrevista de algoritmo Manacher
- algoritmo de subestring Palindrome
- Problema de palindrome lineal
- Problemas de entrevista de ingeniero de software
- Preguntas de entrevista de codificación

-...

### 4.7 Takeaway

■ **Masterizando el código Leetcode 1960** es más que una prueba de manipulación de cadenas – es un escaparate de pensamiento algoritmo, elegancia de código y comunicación de entrevistas.
■ Al combinar la detección lineal de palindrome de Manacher con una simple fusión de prefijo/suffix, obtendrá una solución limpia y óptima que impresionará a cualquier gestor de contratación.

¡Feliz codificación, y buena suerte aterrizando ese trabajo de sueño! 🚀