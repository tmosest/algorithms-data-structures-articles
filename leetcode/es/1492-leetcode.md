-...
Título: LeetCode 1492. El factor kth de n -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# The K‐th Factor of **n** - LeetCode 1492
**A Deep Dive, Code Solutions en Java / Python / C++ & a Job‐Ready Blog Post**

■ **TL;DR** – Encuentra el divisor más pequeño *k* de un número *n*.
■ Complejidad: **O(√n)** (mucho mejor que el análisis ingenuo O(n)).
■ Idiomas: Java, Pitón, C++.
■ Las secciones del blog: lo bueno, lo malo, lo feo.
■ Palabras clave SEO: *kth factor of n, LeetCode 1492, coding interview, algoritmo, O(√n) solution, interview prep*.

-...

## Tabla de contenidos

TEN TERRITORIO TENIDO Enlace ANTE
Silencio...
Problema Recap Silencio #1-problema-recap
Silencio 2️ Brute‐Force vs. Optimised TEN #2-brute-force-vs-optimised TEN
TENIDO 3 PUEBLOS O (√n) Solución Silencioso #3-o√n-solución Silencio
Silencio 4️ Código en Java Silencio #4-código en-java Silencio
tención 5️ Código en Python Silencio #5-code-in-python
tención 6️ Código en C++ Silencio
La buena vida en la vida
Silencio 8️ La mala vida #8-la-bad
tención 9️ El Ugly Silencio #9-the-ugly
Silencio 🔟 Entrevista Consejos confidencialidad #10-interview-tips
Silencio | Referencias Silencioso #11-referencias

-...

Problema Recap

■ **LeetCode 1492 – El factor k‐th de *n***
■ **Given** dos números enteros positivos `n` y `k`, devuelven el factor más pequeño de `n`.
■ Si `n` tiene menos de `k ' factores, vuelva `-1`.

■ *Examples*
1. `n = 12, k = 3` → factores `[1, 2, 3, 4, 6, 12]` → respuesta `3`.
2. `n = 7, k = 2` → factors `[1, 7]` → respuesta `7`.
[1, 2, 4] → respuesta `-1`.

■ **Constraints**
■ `1 ≤ ≤ n ≤ 1000`.

■ **Siguiente**: Resolver en *menos que* `O(n)`.

-...

## 2down Bru Brute‐ Fuerza vs. Optimizada

Silencio Silencio Silencio Silencio Silencio Silencio Silencio Silencio
Silencio----------------------------
Silencio **Brute‐Force** – iterate i = 1...n, collect factors TEN **O(n)** Silencio **O(1) ** NOVEDAD Funciona porque *n* ≤ 1000, pero no óptima para entradas más grandes. Silencio
Silencio **Optimised** – iterate i = 1...√n, collect pairs TEN **O(√n)** Silencio **O(1)** Silencio de visores; mucho más eficiente para grandes *n* (por ejemplo, 10^9). Silencio

-...

Solución

1. **Recoge la primera mitad de los divisores* *
Iterate `i` from `1` to `n`.
Si `i` divide `n`, apéndice `i` a una lista `smallDivs`.

2. **Cuelga la segunda mitad sobre la mosca**
Si `k` ≤ `smallDivs.size()`, la respuesta es `smallDivs[k-1]`.
De lo contrario, los factores restantes son `n/i` para cada divisor `i` en orden inverso.
Computa cuántos saltamos (`k - smallDivs.size()`) y devuelve el adecuado.

3. **Retorno -1 si nos quedamos sin divisores* *

¿Por qué? * *
■ Cada divisor `d` √n pares con un divisor `n/d` se hizo √n.
■ Por lo tanto, sólo necesitamos comprobar hasta √n para descubrir todos los pares de factores*.

-...

Código en Java

``java
*
* 1492. Factor k-th de n
* https://leetcode.com/problems/the-kth-factor-of-n/
*/
Clase Solución {
int Factor(int n, int k) {
// Lista de factores de almacenamiento
Lista realizadaInteger menor = nuevo ArrayList implicado();

int limit = (int) Math.sqrt(n);
para (int i = 1; i) = límite; i++) {}
(n % i == 0) {
pequeños.add(i);
}
}

// Si k está dentro de la lista de factores pequeños
si (k <= small.size()) {}
retorno pequeño.get(k - 1);
}

// Los factores restantes son n / i para el orden inverso
int remaining = k - small.size();
int total = n / límite; // número de grandes factores
si (remanente del total de >) retorno -1; // no suficientes factores

// Consiga el factor más grande (que permanece)
// Ejemplo: pequeño = [1,2,3], restante = 1 - título que queremos n/3
int idx = pequeño.size() - restante; // índice en pequeña lista
retorno n / pequeño.get(idx);
}

// Quick main para pruebas locales
public static void main(String[] args) {
Solución sol = nueva solución ();
System.out.println(sol.kthFactor(12, 3)); // 3
System.out.println(sol.kthFactor(7, 2)); // 7
System.out.println(sol.kthFactor(4, 4)); // -1
}
}
`` `

■ *Puntos clave*
* `Math.sqrt` → doble; cast to int for loop boundary.
* Almacenamos sólo los divisores *pequeños*; los *grandes* son derivados lazily.
* Complejidad: `O(√n)` tiempo, `O(√n)` espacio para la lista de pequeños divisores.

-...

Código en Python

``python
# 1492. El factor k-th de n
# Python 3

Solución de clase:
def kthFactor(self, n: int, k: int) int:
pequeños = []
límite = int(n ** 0.5)
para i en rango(1, límite + 1):
si n % i == 0:
pequeños.append(i)

si k ?
retorno pequeño[k] - 1]

restantes = k - len(small)
# Número de factores grandes es divisores totales menos pequeños
total_large = (len(small) * 2) - (1 if limit * limit == n else 0)
si resta total_large - len(small):
retorno -1

# Index in small list for the required large divisor
idx = len(small) - remaining
retorno n // pequeño[idx]

Prueba rápida
si __name_ == "__main__":
sol = Solución()
print(sol.kthFactor(12, 3)) # 3
print(sol.kthFactor(7, 2)) # 7
print(sol.kthFactor(4, 4)) # -1
`` `

■ **Tocados pitónicos* *
* Use la comprensión de la lista para `pequeña'.
* Compute `limit = int(n ** 0.5)`.
* Maneja los cuadrados perfectos correctamente (`n == limite * limit`).

-...

Código C+++

``cpp
// 1492. El factor k-th de n
// C+17

#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int kthFactor(int n, int k) {
vector pequeña;
límite int = sqrt(n);
para (int i = 1; i) = límite; ++i) {}
(n % i == 0)
pequeño.push_back(i);
}

si (k <= (int)small.size())
retorno pequeño[k - 1];

int remaining = k - small.size();
// Cuenta de divisores grandes
total Grande = (int)small.size() * 2
- (limite * limit == n? 1 : 0);

si (mantenimiento √≥ totalLarge - (int)small.size())
retorno -1;

int idx = (int)small.size() - remaining;
retorno n / pequeño[idx];
}
};

int main() {}
Sol de solución;
cout se realizó el sol.kthFactor(12, 3)
cout se realizó el sol.kthFactor(7, 2)
cout se realizó el sol.kthFactor(4, 4)
retorno 0;
}
`` `

■ **C++ Highlights* *
* `sqrt ' vuelve doble; cast to int.
" Use `vector garantizadoint ' para los pequeños divisores.
* Mantenga el código compacto pero legible.

-...

## 7 carreras El Bien

Por qué es buena vida
Silencio----------
Silencio ** Complejidad óptima** – `O(√n)` es ideal para grandes `n`. Silencio
← **La simplicidad** – Sólo un bucle hasta √n; no hay estructuras de datos pesadas. Silencio
tención **Espacio-Eficiente** – Tiendas en la mayoría de los enteros √n. Silencio
**Readability** – Nombres variables claros (`small`, `remaining`). Silencio
La misma lógica se aplica a Java, Python, C++. Silencio

-...

## 8down El malo

Silencio Tema Silencio Lo que sucede
Silencio...
_Brute‐Force** – iterating to `n` puede ser lento para `n` hasta 106 o 109. Silencio
Silencio ** Lista innecesaria** – si sólo necesita el factor k-th, almacenar todos los divisores pequeños es demasiado. Silencio
TEN **Edge Cases** – olvidando el cheque perfecto para cubrir el divisor medio. Silencio
Silencio **Code Complexity** – verbose `if/else` anidar puede ocultar la lógica. Silencio

-...

## 9 carreras El Ugly

■ La solución *ugly* es a menudo la primera que escribe:
■ 1. **Lazos codificados por miedo**
■ 2. **Mix of loops & recursion* *
■ 3. **No hay salida temprana**
■ 4. **Messy variable names**

``java
// Ugly Java
int[] f = nuevo int[1000]; // overkill array
int cnt = 0;
para (int i = 1; i) = n; i++) {
(n % i == 0) {
f[cnt++] = i;
}
}
si (k = cnt) regresa f[k - 1];
retorno -1;
`` `

■ *Por qué es feo*
* Usa un array de tamaño fijo en lugar de una lista dinámica.
tiempo, lejos de ser óptimo.
* Sin manejo de cuadrados perfectos.
* Pobre nombre (`f`, `cnt`).

-...

## 🔟 Interview Tips

1. **Clarificar el problema** – Pregunte si `k` es 1-basado (sí, LeetCode utiliza 1-basado).
2. **Explicar el emparejamiento del divisor** – `i` y `n/i`.
3. **La complejidad del Estado es una victoria.
4. **Edge Cases** – cuadrados perfectos, `k` más grande que los divisores totales, `n == 1`.
5. **Espera un ejemplo**, por ejemplo, `n = 36`, `k = 5`.
6. **Mención de una salida limpia** – retorno `-1` temprano si imposible.
7. **Mostrar el código** – mantenerlo conciso, probar con entradas de muestra.
8. **Discuten alternativas** – fuerza bruta, listas de factores precomputados, memoización para consultas repetidas.

■ **Recordar:** Los entrevistadores valoran *claridad* y *eficiencia* más que el rendimiento bruto. Una solución bien estructurada con buenos comentarios marcará alto en entrevistas técnicas.

-...

## 📚 Referencias

1. Problema de LeetCode 1492 – Identificado https://leetcode.com/problems/the-kth-factor-of-n/σ
2. Soluciones de muestra de la comunidad (variables idiomas).
3. La factorización oficial del editorial O(√n).
4. Blogs de programación competitiva en la enumeración de divisores.

-...

## 🎯 SEO‐Optimised Conclusion

El *k‐th Factor de n* (LeetCode 1492) es un problema de entrevista clásico que prueba la comprensión de la simetría divisor, la optimización de la complejidad y las prácticas de codificación limpias. La solución óptima `O(√n)` es simple, elegante y funciona para números muy grandes, por lo que es un gran escaparate en su cartera.

Al compartir fragmentos de código en **Java, Python y C++**, usted demuestra la versatilidad del lenguaje, un plus para los gerentes de contratación. El blog acompañante cubre los aspectos *bueno*, *bad* y *muy*, proporcionando a los entrevistadores una descripción clara y profesional.

¿Listo para la próxima entrevista de codificación? Sumérgete en el código, practica casos de borde y mantiene la lógica limpia. Buena suerte – ¡tienes esto! 🚀

-..