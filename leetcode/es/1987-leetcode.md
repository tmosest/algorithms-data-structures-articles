-...
Título: LeetCode 1987. Número de subsecuencias únicas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

## 🚀 LeetCode 1987 - Number of Unique Good Subsequences
**Java ⋅ Python ← C+ Soluciones + SEO‐Optimised Blog Post**

■ ¿Quieres conseguir tu próxima entrevista de ingeniería de software? Mastering **LeetCode 1987** le dará una victoria rápida en la pista de “programación dinámica”, y este post le guiará a través de la *mejor* manera de resolverlo, por qué es elegante, y cómo hablar de ello en una entrevista de trabajo.

-...

## Tabla de contenidos
1. [Declaración sobre el proyecto] (declaración sobre el problema)
2. [Intuición " Insight clave](#intuición)
3. [Solución de programación Dinámica](#dp)
4. [Análisis de complejidad](#complejidad)
5. [Casos Corner " Pitfalls comunes] (casas de bellota)
6. [Code Snippets](#code)
* Java
* Python
* C++
7. [The Good, The Bad, The Ugly](#good-bad-ugly)
8. [Interview‐Ready Talking Points](#interview-talk)
9. [SEO Summary](#seo)

-...

"problema-estado"
## 1. Declaración de problemas

■ **Número de buenas consecuencias únicas* *
■ Se le da una cadena binaria "binaria".
■ Una subsecuencia **buena es una subsequencia no vacía que no empieza con un cero líder a menos que sea exactamente '0'.
■ Encontrar el número de **unique** buenas subsequences de `binary`.
■ Devuelve el modulo de respuesta \(10^9 + 7\).

■ *Examples*
* `binary = "001" → response = 2 (`0'`, `1')
* `binary = "11" → reply = 2 (`"1', `"11')
* `binary = '101'` → reply = 5 (`0'`, `'1', ``, `'10'`, `'11'`, `'101''')

■ **Constraints**
* \(1 \leq \text{len(binary)} \leq 10^5\)
* `binary` contains only `'0'` and `'1'`.

-...

"Intuición"
## 2. Intuición

La cadena es binaria, por lo que una buena subsequencia sólo puede terminar en `'0'` o `'1'.
Piense en construir subsecuencias ** un personaje a la vez**:

* **`ceroEnd`** - número de subsecuencias únicas buenas que terminan con un '0'**.
* **`oneEnd`** - número de subsecuencias únicas buenas que terminan con un '1'**.

Cuando leemos un nuevo personaje:

tención Char TENIDO Efecto sobre `zeroEnd` Efecto involuntario en `oneEnd` Silencio
Silencio--------operfecto--
Silencio `'0'` Silencio Podemos anexar este `'0'` a cada subsequencia que **entendía con un `'1'** → `ceroEnd += oneEnd`. No podemos empezar una nueva subsequencia no vacía con un `'0'` a menos que sea el carácter único `'0'`. Silencio
No hay cambio. Podemos anexar esta `'1' a cualquier subsequencia existente (`ceroEnd + OneEnd`) **o** iniciar un nuevo subsequence de un solo personaje `"1" → `oneEnd += cero End + oneEnd + 1`. Silencio

Finalmente, la respuesta es `cero End + OneEnd`.
Pero si la cadena contenía por lo menos un `'0'`, la subsecuencia única `'0' es **no** contado arriba, por lo que agregamos un extra `1` en ese caso.

El DP entero se ejecuta en **O(n)** tiempo y **O(1)** memoria.

-...

Identificar un nombre= "dp"
## 3. Solución de programación dinámica

``text
Inicializar:
ceroEnd = 0 // subsequences terminando con '0'
oneEnd = 0 // subsequences terminando con '1 '
hasZero = falso // ¿Vimos un '0' en absoluto?

Para cada personaje c en binario:
si c == '0':
ceroEnd = (zeroEnd + oneEnd) % MOD
tiene Cero = verdadero
más: // c == '1'
oneEnd = (zeroEnd + oneEnd + 1) % MOD

respuesta = (zeroEnd + oneEnd + (hasZero ? 1 : 0) % MOD
`` `

`MOD = 1_000_000_007`.

-...

"Nombre="complejidad"
## 4. Análisis de la complejidad

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencioso cadena de escaneo una vez Silencioso **O(n)**
Silencio Operaciones de Modulo Silencio O(1) cada una

Para `n = 10^5`, esto está muy por debajo de los límites.

-...

Identificar un nombre= "casas de bellota"
## 5. Casos de esquina " Cascadas comunes

Silencio Caso Edge Silencio Por qué importa
Silencio...
Silencio String tiene **no** `'0'' Silencio No debemos añadir el extra '0' TENIDO Pista `haZero` o cuenta ceros primero ANTE
Silencio Todos los ceros (`'0000'`) Únicamente una única subsequencia buena: `'0'` Silencio `zeroEnd` se convierte en 0, `haZero` verdadera → respuesta = 1 Silencio
tención Gran entrada ( ' 10^5 ' s)  sometida Riesgo de desbordamiento infligido Uso 64-bit ( 'long ' / `long long ' ) durante adición antes mod Silencio
TEN Modulo mis-placement TEN Respuesta incorrecta para grandes números TEN siempre aplicar `% MOD` después de cada adición ANTE

-...

Identificar un nombre="código"
## 6. Código Snippets

## Java

``java
Solución de la clase pública {}
int final estático privado MOD = 1_000_000_007;

int numberOfUniqueGoodSubsequences(String binario) {
largo cero Fin = 0, oneEnd = 0;
boolean hasZero = false;

para (int i = 0; i) i++) {
char c = binario. charAt(i);
si {}
ceroEnd = (zeroEnd + oneEnd) % MOD;
tiene Cero = verdadero;
} más { / / / '1 '
oneEnd = (zeroEnd + oneEnd + 1) % MOD;
}
}
(int)((zeroEnd + oneEnd + (hasZero ? 1 : 0)) % MOD);
}
}
`` `

## Python

``python
Solución de clase:
MOD = 10**9 + 7

def numberOfUniqueGoodSubsequences(self, binario: str) - Propiedad int:
cero_end = one_end = 0
has_zero = False

para ch en binario:
si ch == '0':
cero_end = (zero_end + one_end) % self. MOD
has_zero = True
# 1'
one_end = (zero_end + one_end + 1) % yo. MOD

(zero_end + one_end + (1 if has_zero else 0) % self. MOD
`` `

### C++

``cpp
Clase Solución {
public:
static const int MOD = 1e9 + 7;
int numberOfUniqueGoodSubsequences(string binario) {
largo cero Fin = 0, oneEnd = 0;
bool hasZero = falso;

for (char c : binario) {
si {}
ceroEnd = (zeroEnd + oneEnd) % MOD;
tiene Cero = verdadero;
} más { // c == '1 '
oneEnd = (zeroEnd + oneEnd + 1) % MOD;
}
}
volver estática_cast seleccionado((zeroEnd + oneEnd + (hasZero ? 1 : 0)) % MOD);
}
};
`` `

-...

Identificar un nombre= "buen-bad-ugly"
## 7. El Bien, el Mal, El Ugly

Silencio Silencio
Silencio------------Prince------
Silencio ** La elegancia algorítmica** Silencio O(n) tiempo, memoria O(1) – un solo pase DP Silencio La enumeración de Naïve es O(2^n) – imposible para n=105 Silencio Olvidar el extra “0” para cuerdas que contienen ceros conduce a un sutil fallo apagado por uno
TEN **Implementación claridad** TENED Dos contadores + una bandera – fácil de leer TEN Recidiva compleja o enfoques basados en hash-set pueden obscurecer la lógica ANTERI Mixing data types (int vs long) puede causar desbordamiento – una entrevista frecuente deslizar TEN
Silencio **Scalability** Silencio Funciona hasta 105 chars con aritmética de 64 bits Una solución de retroceso golpeará los límites de pila Silencio El valor de mod codificado duro se puede colocar erróneamente antes de la adición, dando resultados incorrectos tención
Silencio **Entrevistar punto de vista** Silencioso “Yo trato el problema como dos DP del estado.” Silencio “Usé un set de fuerza bruta.” Silencio “Me olvidé de manejar el único caso de 0”. Silencio

-...

Identificar un nombre= "interview-talk"
## 8. Puntos de conversación de lectura

1. **Explicar la definición de una buena subsequencia** – resaltar la regla “sin ceros líderes”.
2. **Declarar el DP estados** – `zeroEnd` y `oneEnd` – por qué son suficientes.
3. **Walk through the transition** – show how appending a character updates the counters.
4. **Mostrar la agregación final** – por qué añadimos `1` si existiera cero.
5. **La complejidad** – tranquiliza al entrevistador sobre el tiempo O(n) y la memoria O(1).
6. **Movimiento por caso directo** – mención de cuerda de todo cero, todos, y el modulo guard.
7. **Extensión opcional** – cómo lo adaptaría si necesitáramos contar también con subsecuencias *no únicas*.

-...

"Seo" significa "seo"
## 9. Resumen del SEO

- **Title Tags**: “LeetCode 1987 – Número de subsecuencias únicas (Java, Python, C++)”
- **Meta Descripción**: “Solve LeetCode 1987 con O(n) DP. Lea nuestras soluciones Java, Python y C++, consejos de entrevista y una profunda inmersión en el algoritmo. ”
*Headings**: `# LeetCode 1987`, `# Java Solution`, `## Python Solution`, `# C++ Solución `
- **Keywords**: *LeetCode 1987*, *Número de Buenas Subsecuencias*, *programación dinamica*, * Solución java*, * Solución Pitón*, *Solución C++*, *entrevista de trabajo*, *ingeniero de software*, *análisis de algoritmos*, *subsecuencias de cadena binario*.
- ** Enlaces internos**: Enlace a otros blogs de algoritmos (“Programación Dinámica con Dos Estados”) y a la página del problema LeetCode.

Con esta estructura, los motores de búsqueda indexarán el artículo bajo los términos más relevantes, atrayendo a los desarrolladores que se preparan para codificar entrevistas o enfrentar retos de LeetCode.

-...

¡Feliz codificación!
Siéntase libre de forjar este repositorio o adaptar los snippets a su idioma preferido. Buena suerte en la próxima entrevista: su solución DP es un punto de conversación sólido que muestra tanto el pensamiento algoritmo como la codificación limpia.