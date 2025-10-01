-...
Título: LeetCode 2961. Exposición modular doble -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📘 Double Modular Exponentiation – LeetCode 2961
### (Java ← Python ← C++ – Soluciones + Un Blog‐Style Deep‐Dive)

■ ** ID del proyecto:** 2961
■ **Dificultad:**
■ **Keywords:** `modular exponentiation`, `LeetCode`, `Java`, `Python`, `C+`, `coding interview`, `algorithm design`, `O(n)`.

-...

Problema Recap

Se le da un array 'variables', donde cada elemento es un cuádruple
`[a, b, c, m]`.
Un índice `i` is **good** si

`` `
(a^b % 10) ^ c) % m == objetivo
`` `

Devuelve una lista de todos los índices buenos (cualquier orden).

TEN SON SON SON SON SON SON 
Silencio------------
[2,3,10],[3,3,3,3,1], [6,1,1,4]], `target = 2` Silencio `[0, 2] ` Silencio
TENIDO 2 TENIDO `variables = [[39,3,1000,1000]] ' , `target = 17` ANTE `[]

Limitaciones
- 1 ≤ variables. longitud ≤ 100
- 1 ≤ a, b, c, m ≤ 10^3`
- `0 ≤ blanco ≤ 10^3`

-...

## 2down ¿Por qué es un problema “bueno”?

Silencio TENIDO ANTERIOR ANTERIOR
Silencio...
Silencio **Simplicidad + Profundidad** Silencio La declaración es fácil de leer pero oculta problemas sutiles con el desbordamiento y la aritmética modular. Silencio
Silencio **Entrevista común Tema** Silencio La exponencia modular es un elemento básico en muchas entrevistas de codificación (RSA, funciones de hash, etc.). Silencio
Silencio **Multiple Languages** ← Demuestra cómo se aplica la misma lógica en Java, Python y C++. Silencio
tención ** Enfoque escalable** Silencioso Aunque las limitaciones son pequeñas, la solución escala a exponentes muy grandes si es necesario. Silencio

-...

## 3down El “Bad” – Potential Pitfalls

Silencio ❌ ❌ Pitfall Silencio Cómo evitarlo Silencio
Silencio...
Silencio **Overflow** Silencio `a^b` puede explotar (por ejemplo, `1000^1000`). tención Compute `pow(a, b, 10)` directamente con exponentiación modular – nunca dejar crecer el valor intermedio. Silencio
Silencio ** Orden de Modulo** Silencio Mis-ordering the `%` operations can change the result. Siga la fórmula exactamente: primero `% 10`, luego potencia `c`, luego `% m`. Silencio
Silencio **Edge Case `m = 1`** Silencio Cualquier cosa `% 1` es `0`. Silencio Trátelo explícitamente o confíe en aritmética modular: `pow(x, y, 1)` siempre volverá `0`. Silencio
Silencio **Using Built‐In `pow` incorrectly** Silencio En Python, `pow(a, b)` devuelve la potencia exacta, no el resultado modular. TENIDO Use `pow(a, b, mod)` (forma de tres brazos) o implemente rápida-pow. Silencio

-...

## 4down El “Ugly” – Por qué puede parecerse a mísy

- Los bucles repetidos para cada exponente pueden hacer el código largo.
- La implementación ingenua puede parecer bucles anidados, oscureciendo la lógica modular.
- El uso de diferentes tipos de datos ( " in " , `long ' , `BigInteger ' ) en todos los idiomas puede ser confuso.

La clave para una solución **clean** es *abstracting* la exponencia modular en una función de ayuda.

-...

## 5down La solución más limpia – One‐Liner Core

``text
valor = pow(pow(a, b, 10), c, m)
`` `

En Python esto es literalmente una línea.
En Java y C++ lo envolvemos en un ayudante 'modPow'.

-...

## 6VIEW⃣ Code – Three Languages

### 6.1 📜 Java

``java
importa java.util. ArrayList;
importa java.util. Lista;

Solución de la clase pública {}
// Exposición modular rápida: (base^exp) % mod
privado largo modPow(long base, long exp, long mod) {
resultado largo = 1 % mod;
base %= mod;
mientras (ex) 0) {
((exp) == 1) resultado = (resultar * base) % mod;
base = (base * base) % mod;
experiencia= 1;
}
Resultado de retorno;
}

public List won(int[] variables, int target) {}
Lista realizadaInteger correctamente = nuevo ArrayList correctamente();
para (int i = 0; i)
int a = variables[i][0];
int b = variables[i][1];
int c = variables[i][2];
int m = variables[i][3];

largo primero = modPow(a, b, 10); // (a^b) % 10
segundo largo = modPow (primero, c, m); // (first^c) % m

si (segundo == objetivo) {
bueno.add(i);
}
}
devolver bien;
}
}
`` `

■ **Por qué es rápido** – `modPow` se ejecuta en *O(log exp)*, por lo que todo el algoritmo es *O(n log max(b,c)*.

-...

### 6.2 Python

``python
de la importación Lista

Solución de clase:
def getGoodIndices(self, variables: List[List[int], target: int) - título List[int]:
bueno = []
para i, (a, b, c, m) en enumerado(variables):
primer = pow(a, b, 10) # (a^b) % 10
segundo = pow (primero, c, m) # (first^c) % m
si segundo == objetivo:
bueno.append(i)
Regresa bien.
`` `

■ Python’s built‐in `pow(base, exp, mod)` es conciso y altamente optimizado.

-...

### 6.3 📜 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
largo largo mod Pow(long long base, long long exp, long long mod) {
resultado largo = 1 % mod;
base %= mod;
mientras (ex) 0) {
si (exp " 1) resultado = (resultar * base) % mod;
base = (base * base) % mod;
experiencia= 1;
}
Resultado de retorno;
}

public:
vector identificador obtenerGoodIndices(vector seleccionador seleccionador implicados iguales variables, int target) {}
vector bien;
para (int i = 0; i) ++i) {
largo a = variables[i][0];
largo b = variables[i][1];
largo c = variables[i][2];
largo m = variables[i][3];

largo primero = modPow(a, b, 10); // (a^b) % 10
largo segundo = modPow (primero, c, m); // (first^c) % m

si (segundo == objetivo) bueno.push_back(i);
}
devolver bien;
}
};
`` `

■ Utiliza el mismo ayudante de `modPow` para la claridad y la velocidad.

-...

## 7VIEW⃣ Complexity Analysis

← Aspect Silencio Java Silencio Python Silencio C++
Silencio------------...
Silencio **Tiempo** Silencio `O(n · (log b + log c) ' Silencio `O(n · (log b + log c)) ' Silencio `O(n · (log b + log c) Silencio
tención **Espacio** Silencioso auxiliar " O(1) " (además de la lista de resultados)
tención **El peor de los casos** tención 100 × (10 + 10) operaciones

Incluso para el tamaño máximo de entrada (100 filas), esto funciona en milisegundos.

-...

## 8VIEW⃣ SEO‐Optimized Blog Article

-...

# Double Modular Exponentiation – LeetCode 2961
## Your Complete Guide: Java, Python, C++ Solutions & Interview‐ Listos Insights

■ ¿Te estás preparando para una entrevista de codificación? * *
■ Este artículo explica cómo romper el problema *Exposición modular doble* de LeetCode (2961) en **Java**, **Python**, y **C+**. Caminaremos a través del algoritmo, resaltaremos las trampas comunes, y le daremos código de producción que puede caer en su cartera o su próxima entrevista.

-...

## Por qué este problema importa

- **La exponencia móvil** es una de las preguntas más frecuentes* en entrevistas técnicas.
- LeetCode 2961 prueba su capacidad de combinar **Aritmética modular** con ** Operaciones de potencia** — habilidades esenciales para los roles que implican criptografía, seguridad o ciencia de datos.
- Resolviéndolo en múltiples idiomas muestra *pensamiento lingüístico-agnóstico*, un rasgo clave que buscan los entrevistadores.

-...

## La declaración del problema en inglés sencillo

Dada una serie de cuádruples `[a, b, c, m]`, encontrar todos los índices donde

`` `
(a^b % 10) ^ c) % m == objetivo
`` `

devuelve la verdad.

-...

## ¿Por qué es un “bueno” problema de entrevista

Silencio . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 
Silencio...
Silencio **Especificación completa** tención Fácil de leer pero lo suficientemente sutil para requerir un pensamiento cuidadoso. Silencio
Silencio **Demonstrates core CS knowledge** ← Aritmética modular es fundamental para la criptografía y la piratería. Silencio
Silencio ** Solución en idioma materno** Silencio Shows usted puede resolverlo en **Java**, **Python**, **C+** (y más). Silencio
El mismo algoritmo funciona para los exponentes astronómicos grandes si reemplazas el «pow» incorporado con una eficiente rutina de exponentiación modular. Silencio

-...

## Common Mistakes (El "Bad")

- *Overflow*: `a^b` puede explotar; nunca computar todo el poder.
- * Orden Modulo*: Hacer '% m' primero o cambiar '% 10' puede cambiar la respuesta.
*Edge case `m = 1`*: `% 1` es siempre `0`.
- *Python misuse*: `pow(a, b)` devuelve todo el poder, no el resultado modular.

■ Evite esto utilizando *fast modular exponentiation* (`pow(a, b, mod)` en Python, un ayudante en Java/C++).

-...

## Keeping the Code Clean (The “Ugly” to “Good” Transition)

El cálculo básico es

``text
valor = pow(pow(a, b, 10), c, m)
`` `

Encapsular esto en un ayudante («modPow») y el resto del código se convierte en un conciso `for-loop`.
No hay bucles anidados, no manual `mientras'-aperturas para cada exponente.

-...

## Solución en Java

``java
privado largo modPow(long base, long exp, long mod) { ... }
public List Normativa: Integer obtieneGoodIndices(int[][] variables, int target) { ... }
`` `

-...

## Solución en Python

``python
def getGoodIndices(self, variables: List[List[int], target: int) - título List[int]:
bueno = []
para i, (a, b, c, m) en enumerado(variables):
primero = pow(a, b, 10)
segundo = pow (primero, c, m)
si segundo == objetivo:
bueno.append(i)
Regresa bien.
`` `

-...

## Solución en C++

``cpp
largo largo modPow(long long base, long long long exp, long long mod) { ... }
vector identificador obtenerGoodIndices(vector seleccionador identificador implicados iguales variables, int target) { ... }
`` `

-...

## Complexity

- **Tiempo**: `O(n · (log b + log c)' – insignificante para las limitaciones dadas.
- **Espacio**: auxiliar.

-...

## Takeaway

- La exponentiación modular es un tema de *debido* para entrevistas.
- Implementar un pequeño ayudante (`modPow`) para mantener el código legible en Java, Python y C++.
- Test edge cases (`m == 1`, `target == 0`, grandes exponentes).

Con los fragmentos de código arriba, usted está listo para enviar su solución o impresionar a los administradores de contratación que piden: **“¿Cómo resolvería la doble exposición modular?”* *

Buena suerte, y feliz codificación! 🚀

-...

### 🔑 Palabras clave > Meta‐Tags

- Doble exposición modular
- LeetCode 2961
- Coding Entrevista Algoritmos
- Exposición modular de Java
- Python `pow` con Mod
- C++ Modular rápido Poder
- Preparación de entrevistas
- Preguntas de entrevista técnica
- Codificación segura
- Entrevista de trabajo

-...

**Feliz codificación y que su próxima entrevista sea una “buena”* *