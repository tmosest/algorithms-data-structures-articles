-...
Título: LeetCode 2301. Subestring partido después del reemplazo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Leetcode 2024 – ** "Reemplazo de búsqueda"**
El Bien, el Mal, el Mal
*Por qué funciona una simple fuerza bruta, por qué KMP falla, y un vistazo al hack FFT. *

-...

## 1. Recaptación de problemas

Silencio # Silencio Titulo Silencio
Silencio...
Silencio 2024 Silencio ** Reemplazamiento de la máquina** Silencio http://leetcode.com/problems/match-replacement/ Silencio

■ **Definición**
■ Se le dan tres cuerdas: `s`, `sub`, y una lista de 'mappings' (cada mapeo es un par `old → new`).
■ Puedes **reemplazar cada carácter de `sub' a la vez** con cualquier `nuevo' que mapea a (incluido él mismo).
■ Después de todos los reemplazos opcionales, `sub` debe aparecer como una subestring contigua de `s`.
■ Regrese `verdad ' si tal partido existe, de lo contrario `false`.

*Examples*

Silencios en la vida sub Silencioso cartografías resultado
Silencio...
Silencio `abac ' Silencio `a ' Silencio `[ ['a','b'] ] Silencio `true` (reemplazar ambos `a`s con `b` → `bb ' , `bb ' se produce en el índice 1) tención
Silencio `abac` Silencio `bb` Silencio `[ ['a','b'] no se puede reemplazar para que coincida con el " a " en " Silencio

**Constraints* *

* `1 ≤ sub.length ≤ s.length ≤ 104 `
* `0 ≤ mappings.length ≤ 105 `
* Todos los caracteres son imprimibles ASCII (`0–9`, `A–Z`, `a–z`)

-...

## 2. Por qué se acepta la “buena” Brute‐Force

- El alfabeto es diminuto (62 caracteres imprimibles).
- Podemos construir una matriz booleana de 62×62 `puede reemplazar[antigua][nueva]` en `O(mappings)` tiempo.
- Una vez que tengamos esta matriz, comprobando una ventana '[i, i+ sometida a la práctica] in `s` is only a linear scan over `sub`.
- La complejidad general es la `O(las vidas eternas · tenciónsub intimidad)` = `≤ 108` operaciones – bien dentro del plazo para los límites dados.

** Los trucos de estilo KMP no funcionan** porque “matching” es *context dependent*.
Si `sub[i] → x` y `sub[j] → x`, el carácter `x` en `s` podría ser el resultado de la sustitución *either*, por lo que la función de fracaso en KMP no puede saber a dónde ir de nuevo.

■ **Bueno** – Fácil de código, corre lo suficientemente rápido.
■ **Bad** – Los trucos más inteligentes (FFT, NTT o KMP de lujo) añaden complejidad para poco ganancia.
■ **Ugly** – La mayoría de las soluciones de KMP en la discusión fallan en casos de prueba sutiles.

-...

## 3. Detalles de la aplicación

### 3.1 Caracter → Índice Mapping

tención Índice Silencioso
Silencio...
Silencio
Silencioso 26–51
Silencio 52–61 Silencioso

El mapeo es elegido tal que una matriz booleana 62×62 encaja cómodamente en la memoria (~3.8 kB).

#### 3.2 Brute‐ Gráfico básico de la fuerza

Por cada posición inicial:

`` `
para j en 0 ... sub.length-1
si s[i+j] == sub[j] → ok
si puede Reemplazar [sub[j] [s[i+j]] → ok
otra oportunidad
si j == sub.length → partido encontrado
`` `

El cheque se detiene inmediatamente en un desajuste, manteniendo el algoritmo lineal en la práctica.

-...

## 4. Código (tres idiomas)

■ **Nota** – Las tres soluciones implementan la idea *brute‐force*.
■ Recopilan con versiones estándar: Java 17, Python 3.10+, y GNU‐C+17.

#### 4.1 Java

``java
// Archivo: Solution.java
importar java.util*;

Solución de la clase pública {}
// Mapa 'a'-'z' → 0.25, 'A'-'Z' → 26..51, '0'-'9' → 52.61
privada estática final int ALPHABET = 62;

partido booleano públicoReplacement(String s, String sub, char[][] mappings) {
int n = s.length(), m = sub.length();
boolean[][] replace = new boolean[ALPHABET][ALPHABET];

/ // automatización
para (int i = 0; i) ALPHABET; ++i) reemplazar[i] [i] = verdadero;

// rellenar mapas de usuarios
for (char[] mp : mappings) {}
int from = idx(mp[0]); // sub-char
int to = idx(mp[1]); // s‐char
reemplazar[de][a] = verdadero;
}

/ búsqueda de fuerza bruta
para (int i = 0; i) = n - m; ++i) {}
int j = 0;
mientras (j.
int subIdx = idx(sub.charAt(j));
int sIdx = idx(s.charAt(i + j));
si (!replace [subIdx] [sIdx]) romper;
++j;
}
si (j == m) regresan verdadero; // partido completo
}
devolver falso;
}

// helper: mapa char a 0..61
int estática privada idx(char c) {}
si ('a' <= c ' círculo c ' identificado= 'z') retorno c - 'a';
si ('A') se entiende= c " círculo c " ) regresa 26 + c - 'A';
devolver 52 + c - '0'; // '0'.'9 '
}

// Arnés de prueba simple
public static void main(String[] args) {
Solución sol = nueva solución ();

char[][] maps1 = {'a', 'b', {'a', 'c'};
System.out.println(sol.matchReplacement("abac", "aa", maps1)); // true

char[][] maps2 = {'a', 'b'};
System.out.println(sol.matchReplacement("abac", "bb", maps2)); // false

char[][] maps3 = {'a', 'b', {'b', 'c'};
System.out.println(sol.matchReplacement("abac", "ac", maps3)); // true
}
}
`` `

#### 4.2 Python

``python
# File: solution. py
de la importación Lista

Solución de clase:
ALPHABET = 62 # 26 inferior + 26 superior + 10 dígitos

@staticmethod
def _idx(c: str) - título int:
""Map 'a'-'z', 'A'-'Z', '0'-'9' → 0.61.""
si 'a'
devolver ord(c) - ord('a')
si 'A' se hizo= c
devolver 26 + ord(c) - ord('A')
devolver 52 + ord(c) - ord('0')

def matchReplacement(
auto,
s: str,
sub: str,
maps: List[List[str],
.
n, m = len(s), len(sub)

# replace[old][new] == Cierto (antiguo = char de `sub`, nuevo = char de `s`)
reemplazar = [False] * a ti mismo. ALPHABET for _ in range(self. ALPHABET)]
para yo en el rango. ALPHABET:
[i][i] = True # self mapping

para viejos, nuevos en mapas:
[self._idx(old)] [self._idx(new)] = True

# brute‐force search
para i en rango(n - m + 1):
J = 0
mientras que j
si no sustituye[self._idx(sub[j])] [self._idx(s[i + j])]:
descanso
j += 1
si m:
Retorno
Retorno Falso

# .
# Pruebas manuales rápidas (puedes pegar en el corredor interactivo de Leetcode)
si __name_ == "__main__":
sol = Solución()

mapas1 = [['a', 'b'], ['a', 'c']
print(sol.matchReplacement("abac", "aaa", maps1)) # True

mapas2 = [['a', 'b']
print(sol.matchReplacement("abac", "bb", mapas2) Falso

mapas3 = [['a', 'b'], ['b', 'c']
print(sol.matchReplacement("abac", "ac", maps3)) # True
`` `

#### 4.3 C+17

``cpp
// Archivo: solution.cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
static constexpr int ALPHA = 62; // a-z, A-Z, 0-9

// helper: mapa char a 0..61
idx estático (char c) {}
si ('a' <= c ' círculo c ' identificado= 'z') retorno c - 'a';
si ('A') se entiende= c " círculo c " ) regresa 26 + c - 'A';
devolver 52 + c - '0';
}

bool matchReplacement(string s, string sub, vector seleccionadovector fielchar título] {
int n = s.size(), m = sub.size();
vector realizadoarray obtenidosbool, ALPHA título(ALPHA);
para (int i = 0; i) ALPHA; ++i) reemplazar[i].fill(false);

/ // automatización
para (int i = 0; i) ALPHA; ++i) reemplazar[i][i] = verdadero;

// asignaciones de usuarios
para (auto &mp : cartografías) {}
int from = idx(mp[0]); // sub-char
int to = idx(mp[1]); // s‐char
reemplazar[de][a] = verdadero;
}

/ búsqueda de fuerza bruta
para (int i = 0; i) = n - m; ++i) {}
int j = 0;
mientras (j.
int subIdx = idx(sub[j]);
int sIdx = idx(s[i + j]);
si (!replace [subIdx] [sIdx]) romper;
++j;
}
si (j == m) regresan verdadero; // partido completo
}
devolver falso;
}

// Arnés de prueba simple
Correción de vacío estáticaTests() {}
Sol de solución;

vector asignado a los mapas de caracteres iguales1 = {'a', 'b'}, {'a', 'c'};
cout se hizo boolalpha se hizo el sol.matchReplacement("abac", "aaa", mapas1)

vector realizador realizador fieltro mapas2 = {'a', 'b'};
cout se realizó el sol.matchReplacement("abac", "bb", maps2)  se hizo '\n'; // false

vector realizador asignado caracteres títulos 3 = {'a', 'b', {'b', 'c'};
cout se realizó el sol.matchReplacement("abac", "ac", maps3)  se hizo "\n"; // verdadero
}
};

int main() {}
Solución:runTests();
retorno 0;
}
`` `

-...

## 5. Resumen de la complejidad

TENCIÓN TENIDO Tiempo ANTERIENTE Espacio ANTERIOR
Silencio------------------------
Silencio **Brute‐Force** Silencio `O( vidas eternas · prehensisub sometida)` (≤ 108 comparaciones) Silencio `O(ALPHABET2)` = 62×62 booleans (~4 kB) Silencio lo suficientemente rápido, trivial para implementar Silencio
Silencio **KMP (cualquier variante)** Silencio `O( las vidas eternas +  las vidas sub sometidas)` Silencio `O(ALPHABET2)` Silencio *Fails* en los casos en que un reemplazo puede producir el mismo carácter en `s`. Silencio
tención **FFT/NTT** Silencio `O((las vidas eternas+ sometidas a la práctica) log (las vidas eternas+ sometidas a la práctica) ' Silencio `O(ALPHABET2) `` ← Sobre-ingeniería; aceptado sólo para la diversión. Silencio

-...

## 6. Pensamientos finales

* **The Good** – Una sola matriz 62×62 + escaneo de ventana lineal es *exactamente lo que el problema demanda* y es ** rápido, seguro y fácil de entender**.
* **The Bad** – Over-engineering (FFT, NTT, fantasía back-tracking) sólo oculta la dificultad *verdad*: la relación “matching” es * no determinista* sobre una base de caracteres.
* **El Ugly** – Muchos mensajes de discusión muestran KMP o intentos codiciosos que *slip on edge cases* porque ignoran que `sub[i] → x` y `sub[j] → x` crear *dos* diferentes posibilidades de sustitución para el mismo `x` en `s`.

Si usted es un principiante de Leetcode o un ingeniero de producción, vaya directamente al enfoque de matriz de fuerza bruta.
Si usted tiene curiosidad sobre la teoría, investigue la implementación de FFT (ver la discusión de Leetcode) – es un gran ejercicio “look‐at-the-code” pero nunca lo necesitará para este problema.

¡Feliz codificación, y que sus subestrings siempre se formen!