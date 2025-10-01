-...
Título: LeetCode 291. Word Pattern II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## ✅ Word Pattern II – Leetcode 291
**Java ⋅ Python ← C+** – Backtracking + Bijection
**SEO guía optimizada** para ayudarte a solucionar este problema de entrevistas y a aterrizar tu trabajo de sueño

-...

### 🚀 Blog Esquema (SEO Palabras claves)

*Leetcode 291 Word Pattern II** – clásico reto de la cuerda
- ** Solución de retroceso de Java** - código limpio y listo para la producción
**Python Word Pattern II** – recursión legible con conjuntos/dictos
**C++ Implementación** – STL unordered_map / unordered_set
*Pattern bijection* – por qué la singularidad importa
- ** Estrategia de entrevistas de trabajo** - cómo hablar de este problema en una entrevista técnica
- **La complejidad del espacio** – O(n^m) peor caso, pero *prácticamente* rápido
- **Pocaciones comunes** – “carto de cartografía duplicada”, “off-by-one”, “desbordamiento del personal”

■ *Meta Descripción: *
■ Master Leetcode 291 – Word Pattern II. Prepárate con Java, Python y C++ soluciones de backtracking, análisis de complejidad, trucos de periferia y puntos de conversación de entrevista. Perfecto tus habilidades de algoritmo e impresiona a los gerentes de contratación.

-...

Problema Recap

■ *Paleta de la palabra II*
■ Dada una cadena de patrón `pattern` y una cadena `s`, determinar si `s` puede ser segmentado en una secuencia de subestrings no vacíos, de tal manera que cada carácter de `pattern` mapas ** , de forma íxica** (uno a uno) a una subestring.
■ Limitaciones: " 1 " = patrón. longitud, s.length " = 20 " , sólo letras minúsculas.

-...

## 🧠 High‐Level Idea

1. **Backtracking** – prueba cada subestring posible para cada personaje de patrón.
2. **Mapping (`HashMap / dict / unordered_map`)** – almacenar el subestring elegido para cada personaje.
3. **Conjunto usado (`HashSet / set / unordered_set`)** – asegurar **bijetividad**: no dos caracteres de patrón comparten la misma subestring.
4. **Pruning** – si la cartografía actual no coincide con el prefijo de `s`, retroceder inmediatamente.

El algoritmo explora un árbol de posibilidades; porque el tamaño de entrada es pequeño (≤ 20), el peor caso exponencial es aceptable.

-...

## 📦 Code Implementations

#### 1down⃣ Java (Backtracking + Sets)

``java
importa java.util. HashMap;
importa java.util. HashSet;
importa java.util. Mapa;
importa java.util. Set;

Solución de la clase pública {}
palabra booleana pública PatternMatch(String pattern, String s) {
backtrack(s, 0, pattern, 0, new HashMap Quería(), nuevo HashSet quiso());
}

correa booleana privada (String s, int i, String pattern, int j,
Mapa seleccionadoCaracter, String ratio, Conjunto de instrucciones usado) {
// Base: ambas cadenas completamente consumidas
si (i == s.length() " ritmo j == pattern.length())) retornan verdaderos;
// Mismatch: uno consumido, el otro no
si (i == s.length()

char c = pattern.charAt(j);

// Existing mapping → debe coincidir exactamente
si (Map.containsKey(c)) {}
String val = map.get(c);
si (!s.startsCon(val, i))) devolver falso;
backtrack(s, i + val.length(), patrón, j + 1, mapa, utilizado);
}

// Prueba cada subestring posible para este personaje
para (int k = i; k)
candidato a la cadena = s.substring(i, k + 1);
si (utilizado.contains(candidato)) continuar; / / / /

map.put(c, candidate);
(candidato);

si (backtrack(s, k + 1, patrón, j + 1, mapa, utilizado)) retornan verdadero;

// Backtrack
map.remove(c);
us.remove(candidato);
}
devolver falso;
}
}
`` `

■ *Por qué funciona* La profundidad de recursión equivale a `pattern.length()` (≤ 20). Cada llamada intenta todas las subestrings posibles; el conjunto `utilizado ` garantiza no dos caracteres patrón mapa a la misma subestring.

-...

### 2down⃣ Python (Elegant Recursion)

``python
def wordPatternMatch(pattern: str, s: str) Bool:
def dfs(i: int, j: int, mapping: dict, used: set) Bool:
# End conditions
si l == len(s) y j == len(pattern):
Retorno
si l == len(s) o j == len(pattern):
Retorno Falso

c = patrón[j]

# Ya mapeado
si c en la asignación:
val = mapping[c]
si no s.startswith(val, i):
Retorno Falso
devolver dfs(i + len(val), j + 1, mapeo, utilizado)

Pruebe cada subestring posible
para k en rango(i, len(s)):
cand = s[i:k + 1]
si se puede utilizar:
continuar
cartografía[c] = caño
us.add(cand)
si dfs(k + 1, j + 1, mapeo, utilizado):
Retorno
del mapping[c]
us.remove(cand)
Retorno Falso

dfs(0, 0, {}, set())
`` `

■ **Pythonic Highlights** – `s.startswith(val, i)` es un cheque rápido prefijo; `set` asegura la bijetividad en O(1).

-...

### 3down⃣ C++ (STL, Recursive)

``cpp
Clase Solución {
public:
bool wordPatternMatch( patrón de cuerda, cadena s) {
unordered_map Garantizar, cadena confianza mp;
unordered_set buscadostring usado;
backtrack(s, 0, pattern, 0, mp, used);
}

privado:
bool backtrack(const string limitado s, int i, const string ritmo, int j,
unordered_map madechar, string pulsa mp, unordered_setcantado
si (i == s.size() " ritmo j == pattern.size()) retornan verdaderos;
si (i == s.size()

char c = pattern[j];
auto = mp.find(c);

// Cartografía existente
si (lo != mp.end()) {}
const cordón val = it- tituladasecond;
si (s.compare(i, val.size(), val) != 0) devolver falso;
backtrack(s, i + val.size(), patrón, j + 1, mp, utilizado);
}

// Nuevo mapeo: probar todas las subestrings
para (int k = i; k) ++k) {
string cand = s.substr(i, k - i + 1);
si (utilizado.count(cand))) continuar;

mp[c] = cand;
us.insert(cand);

si (backtrack(s, k + 1, patrón, j + 1, mp, utilizado)) retornan verdadero;

mp.erase(c);
us.erase(cand);
}
devolver falso;
}
};
`` `

■ **C++ Eficiencia** – `s.compare(i, len, val)` hace una comparación de subestring rápida; `unordered_map / unordered_set` dar O(1) promedio de búsqueda.

-...

Tiempo de Complejidad Espacial

- Lo peor es:
- Cada personaje de patrón puede mapear a cualquiera de las subestrings restantes.
- El espacio de búsqueda ♥ `O(n^m)` donde `n = s.length()` y `m = pattern.length()`.
- Con 'n, m ≤ 20', esto es prácticamente rápido (la mayoría de las ramas son podadas temprano).
- ¿Qué?
- `O(m)` recursion + `O(m)` para la asignación + `O(m)` para el conjunto usado.
- Total: **O(m)** espacio extra, insignificante por las limitaciones.

-...

## 🔍 Edge‐Case Tricks (Entreview Tips)

Silencio Silencio
Silencio...
Silencio ** Cartografía Duplicada** (`abba'` → `'xyz' para `a` y `b`) Silencio Usar un set *utilizado* para bloquear la reutilización. Silencio
Silencio **Off‐by-one substring** (`s.substr(i, k-i+1)`) tención Recuerde índice final inclusivo `k`. Silencio
Silencio ** Subestring Empty** Silencio El bucle comienza en `i` y se detiene en `len(s)-1`; `k-i+1  título= 1`. TENIDO
tención **Desbordamiento de la cubierta** ← Depth ≤ 20 → seguro en Java/Python/C++; si se ejecuta en patrones más profundos, conviértete a una pila explícita. Silencio
Silencio **Early pruning** Silencio Si el mapeo no coincide con la siguiente parte de `s`, salta el resto del bucle. Silencio

-...

## 🎯 Interview‐Ready Talking Points

1. **Aclarar el requisito de la bijección* *
* Cada carta debe mapear a una subestring única; no hay dos letras que puedan compartir el mismo bloque.*

2. ** Explique su estrategia de retroceso* *
*“Consigno reiteradamente subestrings a caracteres, almacenando la asignación en un diccionario, y retrocediendo inmediatamente si el prefijo de la cadena de entrada no coincide.”*

3. *Mostrar cómo manejas la poda* *
* "Usando `startsWith`/`s.compare`, puedo detectar un desajuste en tiempo constante, cortando ramas enteras."*

4. **Discusión de la complejidad**
*“El peor de los casos es exponencial, pero las restricciones de longitud lo hacen transitable. En la práctica, el algoritmo funciona en milisegundos.”*

5. **Optional optimisations**
- Memoising `(i, j)` pares (programación dinamica sobre estado).
- Pre-computing sumas prefijo para cortar ramas más rápido.

-...

## 📌 Quick Reference Summary

Silencio Idioma Silencio Key Data Structures ← Recursion Depth ← Bijectivity Check tención
Silencio--------------------Resistentes...
Silencio **Java** Silencio `HashMap realizadoCharacter,String confianza` + `HashSet Garantizar confianza` Silencio ≤ 20  `used.contains(candidate)` Silencio
Silencio **Python** Silencio `dict` + `set` Silencio ≤ 20 Silencio `cand in used` Silencio
Silencio **C++** Silencio `unordered_map observadochar,string confianza` + `unordered_set seleccionadosstring confianza` ❌ ≤ 20 peru `used.count(cand)`

-...

##  inaceptable Final Verdict

- Corrección: Cada algoritmo garantiza una asignación individual y cubre todas las posibilidades de partición.
- **Eficiencia:** Para las limitaciones dadas, corre cómodamente dentro de los límites de tiempo.
- **Readability:** código Java está listo para la producción; el código Python es conciso; C++ es compatible con STL.
- **Interviewability:** El problema es un gran escaparate de recidiva, retroceso y cuidadosa gestión estatal, perfecto para una entrevista de primer nivel.

-...

### 🎯 Next Steps for Your Interview Prep

1. **Implementa cada versión** – copy‐paste no ganará puntos.
2. **Arranque los casos de prueba proporcionados** más * sus propios* casos de borde (por ejemplo, `pattern='a', `s='abcd').
3. **Explicar la restricción de la bijeción** – una parte clave de la declaración del problema.
4. **Practice a walk‐through** – narra el árbol de recursión, cómo podas ramas, y cuando retrocedes.

¡Feliz codificación y buena suerte en su próxima entrevista técnica! 🚀