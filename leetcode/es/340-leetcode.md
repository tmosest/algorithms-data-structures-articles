-...
Título: LeetCode 340. Subestring más larga con la mayoría de los caracteres distintos K -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 340 – Subestring más largo con el Distinto de la mayoría de K Carácteres
■ **Keywords**: LeetCode 340, Ventana deslizante, solución HashMap, O(n), Java, Python, C++, Preparación de entrevistas, Algoritmo, Estructuras de datos

-...

#### 📌 Problema general

- **Título**: Subestring más largo con el Distinto de la mayoría de K Carácteres
- Dificultad.
- ** Entrada**:
- `s`: a string of length `1 ≤ Никовый ≤ 5·104`
- `k`: un entero `0 ≤ k ≤ 50`
- **Output**: Longitud de la subestring contiguo más larga que contiene **no más que** `k` caracteres distintos.

■ *Ejemplo*
*(substring = "eceba", k = 2  contactos 3` *(substring = "ece")*

-...

### 🧠 Why This Problem Matters

- Interview Gold‐Mine**: Esta pregunta prueba su capacidad para pensar en *O(n)* tiempo, utilizar técnicas de dos puntos, y gestionar la frecuencia cuenta de manera eficiente.
- **Common Pitfall**: Brute‐force O(n2) o O(n3) soluciones obtienen TLE en grandes insumos.
- **Habilidades transferibles**: Ventana deslizante, uso del mapa de hash, manipulación de punteros – todo básico en el diseño del sistema y codificación del mundo real.

-...

## 🛠ف El “Bueno” – El enfoque clásico de deslizamiento de Windows

### ## 1down I Idea

Mantener una ventana `[izquierda, derecha] `` tal que el substring `s[left..right]`. contiene a la mayoría de caracteres distintos.
- Ampliar `derecha' un paso a la vez.
- Al añadir un nuevo personaje hace que el número de caracteres distintos exceda `k`, encoja la ventana de la izquierda hasta que se restablezca la condición.

#### 2down⃣ Estructura de datos

Un mapa de frecuencia (`HashMap` / `unordered_map` / `collections. Counter`) rastrea cuántas veces aparece cada personaje en la ventana actual.

#### 3down⃣ Pasos

Silencio Silencio Silencio Silencio Silencio
Silencio--------Prince----------
Silencio 1 Silencio Inicializar `izquierda = 0`, `maxLen = 0`, mapa vacío.
Silencio 2 Silencio Iterate `right` from 0 to n‐1. Silencio O(n) Silencio
Silencio 3 TENIENTES Increment freq of `s[right].
Silencio 4 Silencio Mientras que el tamaño del mapa √Ī k: decrement freq de `s[left]`, eliminar si cero, `left+`. ¦
TENIDO 5 TENIDO Actualizar `maxLen = max(maxLen, right - left +1).
Silencio 6 Silencio Regresar `maxLen`. Silencio O(1) Silencio

Tiempo total `O(n)`, espacio `O(k)` (caso inferior cuando todos los caracteres son distintos y `k = 50`).

-...

## 💥 The “Bad” – Naïve Brute Force

- Enumerar todas las subestrings: `O(n2)` tiempo, `O(1)` espacio para contar con un `Set`.
- O utilizar un bucle anidado y mantener un array de frecuencia para cada subestring: aún `O(n2)`.

**Resultado**: Fails on 5·104 length strings – 2.5 billion substrings → TLE.

-...

## 😈 The “Ugly” – Edge‐Case Mess

Silencioso Caso Edge ¿Qué puede salir mal? Silencio
Silencio--------------------
TENIDA `k == No hay subestring permitido → respuesta Silencio Handle temprano. Silencio
Subtítulos en la cuerda vacía Regreso temprano. Silencio
Silencio Todos los personajes idénticos ¦ Window crece a cadena completa. Silencio Funciona bien, pero ver el tamaño del mapa nunca > k. Silencio
←= número de chars únicos en s` ← La cuerda entera es válida. Silencio Funciona automáticamente, pero sigue siendo bueno para comprobar el regreso temprano si es necesario. Silencio

-...

## 🖥ح Code Implementations

A continuación se encuentran soluciones limpias y de producción en **Java**, **Python**, y **C+**.

-...

## Java

``java
importa java.util. HashMap;
importa java.util. Mapa;

Solución de la clase pública {}
longitud pública OfLongestSubstringKDistinct(String s, int k) {
si (k == 0 Silencioso s == null Silencioso s.isEmpty()) devuelve 0;

int left = 0, maxLen = 0;
Mapa seleccionadoCaracter, Integer frecuentementeq = nuevo HashMap Quería();

para (derecho = 0; derecho) {}
char r = s.charAt(right);
freq.put(r, freq.getOrDefault(r, 0) + 1);

mientras (freq.size() > k) {}
char l = s.charAt(left++);
int count = freq.get(l) - 1;
(cuenta == 0) freq.remove(l);
más freq.put(l, count);
}

maxLen = Math.max(maxLen, derecha - izquierda + 1);
}
volver maxLen;
}
}
`` `

-...

## Python 3

``python
de las colecciones importadas por defecto

Solución de clase:
def lengthOfLongestSubstringKDistinct(self, s: str, k: int) - título int:
si k == 0 o no s:
retorno 0

izquierda = 0
max_len = 0
freq = defaultdict(int)

por derecho, char in enumerate(s):
freq[char] += 1

mientras len(freq)
freq[s[left] -= 1
si freq[s[left] == 0:
del freq[s[left]]
izquierda += 1

max_len = max(max_len, right - left + 1)

volver max_len
`` `

-...

### C++

``cpp
#include ■unordered_map Conf
#include ■string
#include >

Clase Solución {
public:
longitud intOfLongestSubstringKDistinct(cont std::string severa s, int k) {
si (k == 0 Silencioso s.empty()) devuelve 0;

std::unordered_map determinadachar, int confianza freq;
int left = 0, maxLen = 0;

para (derecho = 0; derecho)
freq[s[right]]++;

mientras (freq.size() √≥ static_cast seleccionasize_t confianza(k)) {
si (--freq[s] == 0)
freq.erase(s[left]);
++izquierda;
}

maxLen = std::max(maxLen, derecha - izquierda + 1);
}
volver maxLen;
}
};
`` `

-...

## 🧩 How the Code Works (Step‐by‐Step)

1. **Initialization** – `izquierda ' apunta al comienzo de la ventana actual, `maxLen` registra la mejor longitud encontrada, `freq` tiendas carácter cuenta.
2. **Expand** – Para cada `derecha', agregue el carácter a `freq`.
3. **Contract** – Mientras tenemos demasiados caracteres distintos, encogiendo la ventana de la izquierda: decrementar el conteo, eliminar si cero, y mover `izquierda'.
4. **Actualizar** – Después de cada expansión, la ventana es válida. Actualizar `maxLen` si la ventana actual es más grande.
5. **Retorno** – Después del bucle, `maxLen` tiene la longitud de la subestring más larga.

-...

## 📊 Complexity Analysis

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
TENIDO EL TIEMPO ANTERIENTE **O(n)** TENIENTES **O(n)**
TENIDO EL ESPACIO TENIDO **O(k)** Silencio**
tención *n* = duración infligida de `s ' , duración infligida de `s ' .

*¿Por qué espacio? *
El mapa de frecuencia nunca contiene más de las teclas " k+1 " (una vez que supera " k " , encogemos).

-...

##  Errores comunes > Cómo evitar Ellos

← Mistake ← Consequence
Silencio----------------------------
Olvídate de manejar `k == 0` Silencio Returns wrong non‐zero length Silencio Add early guard Silencio
Silencio Usando `HashSet` en lugar de mapa de frecuencia Silencio No se puede encoger correctamente cuando aparecen charcos duplicados Silencio Usar un mapa para seguir conteos Silencio
tención Actualización después de la contracción bucle tención
tención Off‐by‐one errores en el tamaño de la ventana Silencio Duración incorrecta Uso `derecha - izquierda + 1` para la ventana inclusiva Silencio

-...

## 🔧 Otras optimizaciones

← Técnica Silenciosa Cuando se utiliza Silencioso
Silencio------------------------------
Silencio **Dos-Pointer (ya utilizado)** Silencio Siempre Silencio
Silencio **Pre-allocate Array for ASCII** Silencio Las cuerdas son ASCII Silencio acceso continuo más rápido que HashMap  durable
Silencio **Evitar `HashMap.getOrDefault` en Java 8+** Silencio Rendimiento crítico Silencio Uso `compute` o `merge` para el código conciso

■ *Tip*: Para los entrevistadores que valoran **claridad sobre micro-optimizaciones**, el enfoque HashMap/Counter es ideal. Para sistemas de producción, un array (tamaño 256) puede afeitar unos pocos microsegundos.

-...

## ✅ Test Suite (Python)

``python
unidad de importación

clase TestLongestSubstring(unittest. TestCase:
def setUp(self):
self.sol = Solution()

def test_examples(self):
self.assertEqual(self.sol.lengthOfLongestSubstringKDistinct("eceba", 2), 3)
self.assertEqual(self.sol.lengthOfLongestSubstringKDistinct("aaa", 1), 2)

def test_edge_cases(self):
self.assertEqual(self.sol.lengthOfLongestSubstringKDistinct("", 0), 0
self.assertEqual(self.sol.lengthOfLongestSubstringKDistinct("abc", 0), 0
self.assertEqual(self.sol.lengthOfLongestSubstringKDistinct("abc", 5), 3)
self.assertEqual(self.sol.lengthOfLongestSubstringKDistinct("a", 1), 1)

def test_large(self):
s = "a" * 50000
self.assertEqual(self.sol.lengthOfLongestSubstringKDistinct(s, 1), 50000)

si __name_ == "__main__":
unittest.main()
`` `

Ejecute la prueba 'python3.py` para garantizar la cobertura del 100%.

-...

## 🎯 Takeaway – What Look For

1. **Correcto** – Maneja todos los casos de borde.
2. **Tiempo " Eficiencia Espacial** – O(n) tiempo, O(k) espacio.
3. ** Código Clean** – Nombres variables claros, guardias tempranos, caldera mínima.
4. **Problema‐Solving Mindset** – Reconocer la ventana deslizante como el ajuste natural.

■ *Job‐Ready Tip*: Practica explicar tu solución en voz alta. Los entrevistadores les encantan las explicaciones concisas y bien estructuradas que resaltan la visión algorítmica y los intercambios.

-...

### ##

Leet Code 340 es un problema clásico de ventanilla deslizante que se puede resolver en tiempo lineal. Al dominar este patrón, no sólo está preparado para esta pregunta específica, sino también equipado para una serie de problemas de entrevista que involucran subestrings, subarrays y limitaciones de frecuencia.

¡Feliz codificación, y que su próxima entrevista llame a la clase 'Solution' que acaba de escribir! 🚀