-...
Título: LeetCode 1053. Permutación anterior con un solo golpe -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1053. Permutación anterior con un solo sorbo – un completo Guía
*(Java fort Python Silencio C++)*

■ ¿Quieres llegar a la pregunta *Excelente permutación con un súbito* en una entrevista de LeetCode?
■ Aquí hay un **paso a paso**, un algoritmo claro, tres soluciones de producción, y un blog optimizado SEO que hará que su currículum sea notado por los reclutadores.

-...

### 🚀 TL;DR

* **Problema** – Encuentra la permutación más grande de la lexicografía más pequeña que la matriz dada usando **Exactamente un swap**.
* **Core idea** – Scan from the right to locate the first “dip” (`arr[i] > ) >
****Key swap** – Elija el elemento más adecuado que es **smaller** que el más grande ** entre tales candidatos (para mantener el resultado lo más grande posible).
* ** Complejidad** – **O(n)** tiempo, **O(1)** espacio extra.
* ** Casos de edge** – Ya es la permutación más pequeña, los valores duplicados, los arrays de un solo elemento.

-...

Declaración de problemas (LeetCode 1053)

■ Dada una variedad de enteros positivos `arr` (no necesariamente distintos), devuelve la permutación lexicográficamente más grande que `arr`, que se puede hacer con exactamente un swap.
■ Si no se puede hacer, entonces devuelva el mismo array.

*Examples*

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
TENIDO `[3,2,1] `` TENIDO `[3,1,2]` TENIDO SUSP `2` y `1`. Silencio
TENIDO `[1,1,5]` TENIDO `[1,1,5]` TENIDO Ya la menor permutación. Silencio
TENIDO `[1,9,4,6,7]` TENIENDO `[1,7,4,6,9]` TENIDO . Silencio

-...

##  tuya El enfoque "bueno, malo"

Silencio, cariño.
Silencio----------------------------
Silencio ** Diseño Algorítmico** Silencio Un solo paso de derecha a izquierda para encontrar el *primer índice decreciente*. Un doble bucle que comprueba cada par – `O(n2)` – pierde tiempo. tención Brute‐force generación de permutación y clasificación – imposible para `n ≤ 104`. Silencio
Silencio **Handling Duplicates** Silencio Realice un seguimiento del candidato *derecha-más* para evitar intercambiar números iguales que rindan la misma matriz. Los duplicados de Ignorar pueden producir el índice equivocado o ningún cambio. TENIDOS La primera ocurrencia de un número menor podría producir la permutación posible *smallest*, no la más grande. Silencio
Silencio **La complejidad** Silencioso `O(n)` tiempo, `O(1)` espacio – óptimo para entrevista. Silencio `O(n2)` tiempo, todavía pasa pequeñas pruebas pero no aceptable para grandes insumos. ¡Oh, Dios mío! tiempo – astronómicamente lento. Silencio
Silencio **La simplicidad del oso** Silencio Un bucle de ayuda, un swap – fácil de leer. ← Sobre-ingeniería con funciones de ayuda innecesarias. Silencio

-...

## 🧠 Core Algorithm (Pseudocode)

`` `
1. Encontrar i = último índice tal que arrr[i] se hizo arrr[i-1].
Si ninguno existe → array ya es el más pequeño; retorno arr.

2. En el sufijo arr[i ... final], encontrar el elemento
x que es arrr[i-1] y lo más grande posible.
Si existen duplicados de x, elija la más izquierda (cerca a i-1)
para asegurar que el array final sea el más grande.

3. Swap arr[i-1] y x.

4. Regresa arr.
`` `

¿Por qué funciona esto?
La primera posición decreciente es el lugar más adecuado donde el array se puede hacer más pequeño. Para mantener el resultado lo más grande posible, cambiamos el elemento * más grande* más pequeño del sufijo, y elegimos la ocurrencia **a la derecha** de ese elemento para evitar reducciones innecesarias causadas por duplicados.

-...

## 📦 Solutions

### Java – `Solution.java `

``java
importar java.util*;

Clase Solución {
int[] prevPermOpt1(int[] arr) {
int n = arr.length;
int i = n - 1;

// 1. Encuentra el primer par decreciente de la derecha.
mientras (i √≥ 0 ' pÃ3nt arr[i - 1] i...

si 0) retorno arr; // ya mínimo

int pivote = i - 1;

// 2. Encontrar el elemento más adecuado . arrr[pivot] y lo más grande posible.
int target Idx = -1;
int target Val = Integer.MIN_VALUE;

para (int j = pivote + 1; j
si (arr[j] > arrr[pivot] " arrr[j]
targetVal = arr[j];
objetivo Idx = j;
}
}

// 3. Swap
int tmp = arrr[pivot];
arrr[pivot] = arrr[targetIdx];
arr[targetIdx] = tmp;

retorno arr;
}

// Opcional principal para la prueba manual rápida
public static void main(String[] args) {
Solución s = nueva solución ();
System.out.println(Arrays.toString(s.prevPermOpt1(new int[]{1, 9, 4, 6, 7})));
}
}
`` `

**Explicación**
*El bucle `mientras (i √≥ 0 ' √≥ arrr[i-1] Yo...
da la vuelta más derecha.
*El bucle interior* mantiene al mejor candidato (`targetVal`) que es más pequeño que el pivote.
Finalmente realizamos el intercambio.

-...

### Python – `solution.py `

``python
de la importación Lista

Solución de clase:
def prevPermOpt1(self, arr: List[int] List[int]:
n = len(arr)
i = n - 1

# 1. Localice el primer par decreciente.
mientras que yo 0 y arrr[i - 1]
I -= 1

si yo == 0:
Ya es la permutación más pequeña.

pivote = i - 1

# 2. Encontrar el elemento más adecuado . arrr[pivot] con valor máximo.
target_idx = 1
target_val = 1
para j en rango(pivot + 1, n):
si arrr[j] se hizo arrr[pivot] y arr[j]
target_val = arrr[j]
target_idx = j

# 3. Swap
arrr[pivot], arrr[target_idx] = arrr[target_idx], arrr[pivot]
retorno arrr

# Prueba rápida opcional
si __name_ == "__main__":
s = Solución()
print(s.prevPermOpt1([1, 9, 4, 6, 7]))
`` `

-...

### C++ – `solution.cpp `

``cpp
Incluido el título
#include >

Clase Solución {
public:
std:::vector obtenidosint confianza prevPermOpt1(std::vector fieltro arrr) {
int n = arr.size();
int i = n - 1;

// 1. Encuentra el primer par decreciente de la derecha.
i) i)
si 0) retorno arr; // ya mínimo

int pivote = i - 1;

// 2. Encuentra al mejor candidato para intercambiar.
int target Idx = -1;
int target Val = -1;
para (int j = pivote + 1; j
si (arr[j] > arrr[pivot] " arrr[j]
targetVal = arr[j];
objetivo Idx = j;
}
}

// 3. Swap
std::swap(arr[pivot], arr[targetIdx]);
retorno arr;
}
};
`` `

**Consejo:** El algoritmo se ejecuta en *O(n)* tiempo y utiliza *O(1)* espacio extra, perfecto para limitaciones de entrevista.

-...

## 📝 Blog Post Draft

-...

### Title
**LeetCode 1053: Permutación previa con una sola gota – Maestro la Solución O(n) (Java, Python, C++)* *

## Meta Descripción
Aprenda a resolver LeetCode 1053, “Permutación Anterior con un solapa”, en Java, Python y C++. Obtenga el algoritmo completo, el manejo de los bordes, y un blog listo para trabajar con palabras clave SEO.

#### Introduction
Cuando los entrevistadores le dan la permutación anterior de LeetCode con One Swap*, están probando su capacidad para razonar sobre permutaciones, manejar duplicados y escribir código limpio. Este artículo explica el problema, camina a través de un algoritmo codicioso, y le da tres implementaciones de producción. Ya sea que seas desarrollador de Java, un pithonista o un guru C++, te irás con un fragmento de código que puedes dejar en tu próxima entrevista o cartera.

### Problema general
*Te han dado una serie de números enteros positivos. Usted debe producir la matriz lexicográficamente más grande que es estrictamente menor que el original, utilizando exactamente un swap. Si no existe tal swap, devuelve el array original. *

### Core Insight – “First Decreasing Index”
El lugar más adecuado donde el array disminuye (`arr[i] Identificar arr[i‐1]`) es donde se puede hacer el array más pequeño. Cualquier cosa a su izquierda ya es óptima; cualquier cosa a su derecha debe ser alterada para obtener el mayor resultado posible.

## Step‐by‐Step Algorithm
1. **Escana desde el final** para encontrar el primer índice `i` donde `arr[i-1].
2. Si no existe tal `i`, el array ya es la permutación más pequeña - retornarlo.
3. En el sufijo `arr[i ... end]`, encontrar el elemento que es
* Small than `arr[i-1]` **y** la más grande posible entre estos elementos.
4. **Swap** `arr[i-1]` con ese elemento.

### Por qué funciona
El primer par decreciente garantiza que el array se vuelve más pequeño. Al elegir el elemento más pequeño * más grande* del sufijo, mantenemos el prefijo (que determina el orden lexicográfico) lo más grande posible. Elegir la ocurrencia más correcta maneja los duplicados de forma segura: si el mismo número aparece varias veces, el intercambio con el más izquierdo dejaría un número mayor más adelante en el array, que nunca es deseable.

### Handling Edge Cases
Silencio Caso confidencialidad ¿Qué hacer?
Silencio----------------------
Silencio **Already Minimal** Silencio Regresar original array Silencio No hay pareja decreciente existe Silencio
Silencio **Duplicados** Silencio Elija el candidato más adecuado ¦
Silencio **Elemento único** Silencio Regresar lo antes posible No swap possible tención

### Complexity Analysis
* **Tiempo** – `O(n)` (un paso para encontrar el dip, otro pase para encontrar al candidato).
* **Espacio** – `O(1)` (en lugar de modificación).

## Código Walkthrough – Java

*(Incluya el snippet Java de antes con comentarios line‐by-line.) *

## Code Walkthrough – Python

*(Incluya el fragmento de Python de antes con comentarios concisos.) *

### Code Walkthrough – C++

*(Incluya el snippet C++ desde antes con comentarios.) *

## What Interviewers are looking for
*Reconocimiento del patrón codicioso, correcto manejo de duplicados, y código limpio y testable. *

### Quick Test Cases

← Intromisión esperada
Silencio...
TENIDA `[3,2,1] ' Silencio `[3,1,2] ' Silencio
TENIDA `[1,1,5]` Silencio `[1,1,5]
. . Silencio
TENIDA `[1] TENIDA `
TENIDO `[2,2,2,1,2]` ANTE `[2,1,2,2]

Ejecute los snippets proporcionados para verlos en acción.

## SEO & Job‐Search Friendly Tips
- Usar palabras clave: **“LeetCode 1053”, “Permutación anticipada con un solo súbito”, “Pregunta de entrevista de Java”, “Reto de codificación de Python”, “Permutación de matriz C++”.* *
- Añada un enlace a su GitHub repo (por ejemplo: https://github.com/nombre/soluciones de código electrónico).
- Ofrezca un PDF descargable de la solución para los reclutadores que prefieren referencias rápidas.
- Mencione su “O(n) solución óptima” y “manos duplicados”: a los reclutadores les encanta.

## Palabras finales
Ahora has disecado el 1053 de LeetCode en su forma más simple. Saque cualquiera de los tres fragmentos en su cartera, incluya la explicación del algoritmo en su currículum, y confíe en abordar este problema de permutación en su próxima entrevista de codificación.

-...

### Conclusión
*Con el algoritmo y tres implementaciones limpias a mano, usted puede reclamar con confianza la victoria sobre LeetCode 1053. ¡Feliz codificación y buena suerte en tu próxima entrevista! *

-...

Este proyecto combina una explicación algorítmica detallada con comentarios centrados en entrevistas y contenido optimizado SEO. Siéntase libre de ajustar el tono o añadir diagramas visuales para que coincida con su estilo de blog personal.

-...

## 🎯 Final Takeaway

- **Problema**: Mayor permutación estrictamente menor que el original con un swap.
- **Solución**: Encontrar el más adecuado, intercambiar con el mayor elemento sufijo menor.
- ** Complejidad**: Tiempo óptimo `O(n)`, `O(1)` espacio.
- **Code**: Java, Python, C++ snippets listos para entrevistas o carteras.
- **Blog**: Un borrador listo para publicar con palabras clave de SEO y cobertura de periferia.

Buena suerte, y que sus entrevistadores estén impresionados tanto por su código como por el blog que se mostrará con orgullo! 🚀