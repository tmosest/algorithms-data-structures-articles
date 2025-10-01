-...
Título: LeetCode 484. Encontrar Permutation -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## Leetcode 484 – Find Permutation
### "El Bien, el Mal, y el Ugly" de resolver un problema de entrevista clásica
*(Java fort Python Silencio C++) – O(n) time, O(1) auxiliary space)*

-...

#### TL;DR
* **Problema** – Construir la permutación más pequeña de la `[1 ... n]` que satisface un patrón de “Yo” (aumento) y “D” (disminución).
* **Solución** – Escanear la cuerda una vez, y cada vez que se encuentra una carrera de “D” consecutivo, revertir ese segmento del orden natural `[1, 2, ...].
* Por qué importa* La técnica codicioso de establo o ventanilla deslizante es un patrón frecuente en entrevistas (arrayos, pilas, codicioso). Dominarla muestra que puede traducir una cadena de restricciones en un orden óptimo en tiempo lineal.

-...

## 1. Recaptación de problemas

■ ** Entrada**: `s` - una cadena de longitud *n-1*, cada personaje es `'I' o `'D'`.
■ **La salida**: la permutación lexicográficamente más pequeña `perma' de `[1 ... n] que satisfice
" `
[i] == 'I' Alternativa perm[i]
[i] == 'D' Alternativa perm[i]
" `

■ **Constraints**
* 1 ≤ s.length ≤ 105
* s only contains `'I'` or `'D'`

■ *Ejemplo*
[2, 1, 3] (el más pequeño entre `[2,1,3]` y `[3,1,2]`)

-...

## 2. La visión de la salud

*Si ignoramos las limitaciones por un momento, el orden natural `[1,2,3,...]` es la permutación lexicográficamente más pequeña. *

Una carrera de ''D' fuerza un **disminuir** subsequence.
En una subsecuencia decreciente, la permutación lexicográfica más pequeña se obtiene mediante **reversando** que corre.

**Por qué invertir obras* *
* Supongamos que tenemos una carrera 'I' de longitud 'k+1' empezando en el índice 'i'.
* Los números que ocuparán las posiciones `i ... i+k` son los siguientes `k+1` números naturales: `i+1, i+2, ..., i+k+1`.
* La inversión da `i+k+1, ..., i+2, i+1`, que es el arreglo más pequeño que está disminuyendo estrictamente.

Así, todo el algoritmo se reduce a:

`` `
perm = [1, 2, ..., n]
por cada bloque "D" consecutivo [l ... r] en s:
inverso perm[l ... r+1]
de retorno
`` `

El truco es realizar la inversión **en lugar** mientras escanea la cadena, evitando una pila explícita o un array extra.

-...

## 3. The Three Idiomatic Implementations

A continuación se encuentran soluciones limpias, listas de producción en Java, Python y C++.
Todo se ejecuta en el tiempo `O(n)`, utilizar sólo el array de salida como espacio auxiliar (`O(1)` extra).

-...

### 3.1 Java

``java
importar java.util*;

Solución de la clase pública {}
int[] findPermutation(String s) {
int n = s.length() + 1;
int[] perm = nuevo int[n];

// Llenar con el orden natural 1..n
para (int i = 0; i)

int i = 0; // índice actual en s
mientras (i) {}
si (s.charAt(i) == 'I') { // nada que hacer
i++;
continuar;
}

// golpeamos una carrera 'D'. Encontrar su fin
int start = i;
mientras (i) == 'D') i++;

// perm inversa [start ... i] (inclusive)
int left = start, right = i;
mientras (izquierda)
int tmp = perm[left];
perm[left] = perm[right];
perm[right] = tmp;
izquierda++;
Bien...
}
}

retorno perm;
}

// Arnés de prueba simple
public static void main(String[] args) {
System.out.println(Arrays.toString(
nueva solución().findPermutation("DI")); // [2,1,3]
System.out.println(Arrays.toString(
nueva solución().findPermutation("I")); // [1,2]
}
}
`` `

**Por qué esta es la implementación “buena” de Java* *

Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio Single pass through `s ' TENIDO `O(n)` time
Silencio No hay pila auxiliar o lista Silencioso `O(1)` espacio Silencio
Silencio Intención clara: relleno natural + reversal selectiva Silencio fácil de leer " mantener 

-...

#### 3.2 Python

``python
def find_permutation(s: str) - título list[int]:
n = len(s) + 1
perm = list(range(1, n + 1)) # orden natural

I = 0
mientras que yo...
si s[i] == 'I':
i += 1
continuar

comienza = i
mientras que yo hice el len(s) y s [i] == 'D':
i += 1

# Inverso perm[start : i+1] in place
perm[start:i+1] = invertido(perm[start:i+1])

de retorno

# Demo
si __name_ == "__main__":
print(find_permutation("DI") # [2, 1, 3]
print(find_permutation("I") # [1, 2]
`` `

La asignación de la rebanada de Python con `reversed()` da un reversal de una línea – la *Pythonic* manera.

-...

### 3.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector identificador confianza encontrarPermutation(string s) {
int n = s.size() + 1;
vector:
iota(perm.begin(), perm.end(), 1); // 1, 2, ..., n

int i = 0;
mientras (i) {}
si (s[i] == 'I') { ++i; continue; }

int start = i;
mientras (i)s.size() " sensible s[i] == 'D') ++i;

// inverso perm[start .. i]
inverso(perm.begin() + inicio, perm.begin() + i + 1);
}
retorno perm;
}
};

int main() {}
Sol de solución;
auto res = sol.findPermutation("DI");
para (int x : res) cout
cout se hizo 'n';
}
`` `

C++ `iota ' y `reverse ' mantengan el codificador de forma eficiente.

-...

## 4. El Bien, el Mal, y el Mal

TENIDO ESTADO ANTERIOR Lo que pasa es cómo evitar dolor
Silencio...
TEN **El Bien** TENIDO Un solo pase lineal, sólo operaciones enteros, sin contenedores adicionales. Use ayudantes incorporados ( " yota " , " reversa " , rebanada de asignación) para mantener el código legible. Silencio
Silencio **El mal** Silencio Intentar construir una pila manualmente conduce a errores **off-by-one** y factores constantes más altos. Si necesita una pila, utilice un `deque ' o `vector fielint ` y pop/push cuidadosamente. Silencio
Silencio **El Ugly** ← Mezcla la lógica “reversa” dentro de un bucle interno que también modifica el array puede crear bucles anidados confusos. ← Separar la lógica: 1) identificar el bloque ''D', 2) realizar una sola inversión. 3) Continuar escaneando. Silencio

■ **Tip de Interview** – Si alguna vez se le pide que *explica* esta solución, comience por escribir el orden natural, luego ilustre cómo una `D` gobierna una inversión. Mostrar un diagrama rápido de una cadena de muestra: `D I D` → `[1 2 3 4 5 6]` → posiciones inversas 0‐2 → `[3 2 1 4 5 6]` → continuar.

-...

## 5. Casos de borde " Complejidad

Silencioso Caso Silencioso
Silencio...
[1, 2] Silencio
TENIDA `s` = `'D'' TENIDA `[2, 1]` Silencio
TENIDO TODO `I's TENIDO `[1, 2, ..., n]
TENIDO TODO `D`s TENIDO `[n, n-1, ..., 1]` Silencio

**La complejidad* *

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
TENIDO EL TIEMPO TENIDO `O(n)` TENIDO `O(n) Silencio
Silenciosos en el espacio " O(1) " (disposición de salida) Silencio

La limitación de tamaño de entrada (105) se maneja cómodamente en los tres idiomas.

-...

## 6. Bono - A Stack‐ Alternativa basada (para el debate)

Una solución clásica de “stack” empuja índices a una pila cada vez que se ve un `'I' o el fin de la cuerda, luego los pone para establecer valores.
Aunque todavía `O(n)`, utiliza una pila extra de tamaño `O(n)` y puede ser ligeramente más lento en la práctica debido a la sobrecarga de memoria.

``java
Señalamiento:Integer confía st = nuevo Stack correspond();
int val = 1;
para (int i = 0; i) = s.length(); i++) {
st.push(i);
si (i == s.length()
mientras (!st.isEmpty()) perm[st.pop()] = val++;
}
}
`` `

Utilice esto sólo si se le pide explícitamente que demuestre el uso de la pila; de lo contrario la inversión de la ventana deslizante es más limpia.

-...

## 7. SEO " Career‐Boosting Takeaway

1. **Keywords** – *Leetcode 484, Encontrar Permutación, apilación avaricia, tiempo lineal, problema de entrevista, solución Java Python C++, algoritmo O(n) de entrevista de trabajo codificación*
2. **Título** – *“Master Leetcode 484: Find Permutation – Greedy in Java, Python & C+”*
3. **Meta description** – *Aprende la manera más rápida de resolver Leetcode 484, “Encontrar la permutación”. Ver implementaciones Java, Python y C++, análisis de complejidad y explicaciones de entrevista. *

■ *Por qué esto importa para los reclutadores* El patrón de traducir una restricción de cadena en una orden de matriz es una pregunta de entrevista frecuente para funciones de ingeniería de software. Demostrar una solución clara, O(n) en varios idiomas muestra versatilidad y fluidez algorítmica.

-...

## 8. Pensamientos finales

* Mantenga el código **simple**: orden natural + reversales apuntadas.
* Prueba con algunos ejemplos hechos a mano, especialmente casos de borde.
* Cuando se discute en una entrevista, pasee por el ejemplo en una pizarra, mostrando cómo cada ''D'' corre mueve un segmento.

¡Feliz codificación y buena suerte aterrizando ese próximo trabajo! 🚀