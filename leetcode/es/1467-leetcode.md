-...
Título: LeetCode 1467. Probability of a Two Boxes having the Same Number of Distinct Balls -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1467 – “Probability of a Two Boxes having the Same Number of Distinct Balls”
■ **Hard Silencio 8 colores, 48 bolas máx. *

-...

#### 1ICK⃣ Problema Resumen

Te han dado un array `balls[]` Donde `balls[i]` es el número de bolas de color `i`.
Todas las bolas " 2 n " (la suma de la matriz) se encolan uniformemente al azar y luego:

* # El primero # # # # y las bolas van a # # el segundo #
* Las bolas siguen siendo*

Las dos cajas son *distinguibles* (es decir, [a] b) es diferente de [b] (a)).
Devuelve la probabilidad de que las dos cajas contengan el número ** del mismo número de colores distintos**.
Se aceptan respuestas dentro del `10−5` del valor real.

■ *Examples*
■ 1. `balls = [1,1]` → `1.00000`
■ 2. `balls = [2,1,1]` → `0.66667`
■ 3. `balls = [1,2,1,2]` → `0.60000`

-...

## 2down Por qué este problema es digno de entrevista

TENIDO ANTERIOR ANTERIENTE ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTE ANTE
Silencio------------...
tención **High difficulty** – tests combinatorial thinking " DP. Silencio **La combinación puede ser intimidante** para los entrevistados. Silencio **Large factoriales** → flujo entero si no tienes cuidado. Silencio
tención **Clean constraints** – 8 colores, 48 bolas → pequeño espacio de estado. **Necesito pensar en términos de “siempre”**, no sólo cuenta. Silencio ** Casos de Edge** – balanceado `n1` vs `n2` pero diferentes conteos distintos. Silencio
Silencio **Multiple languages** – Java, Python, C++. Silencio **Muchas posibles formulaciones DP** → elegir el más simple. Silencio **Precisión de punto flotante** – debe usar `doble` o `float64`. Silencio

-...

## 3down La idea central

1. **Elige cuántos de cada color van a la caja 1* *
Para el color `i` con bolas `cnt`, elija `k` (`0 ≤ k ≤ cnt`) para ir al recuadro 1, el resto (`cnt‐k`) ir al recuadro 2.

2. **Cuenta el número de “siempre”** para esa elección
El número de maneras de elegir qué bolas de ese color van al recuadro 1 es `C(cnt, k)` (coeficiente económico).

3. **Acumulado**
* `n1` – bolas totales en el recuadro 1
* `n2` – bolas totales en el recuadro 2
* `c1` – colores distintos en el recuadro 1
* `c2` – colores distintos en el recuadro 2
* `ways` – producto de los coeficientes binomiales hasta ahora

4. **Cuando todos los colores se procesan**
* If `n1 == n2`, we have a **valid shuffle** – add `ways` to `total`.
* If also `c1 == c2`, add `ways` to `valid`.

5. **Respuesta** – `válida / total`.

Debido a que el número total máximo de bolas es 48, una simple búsqueda de profundidad primera (DFS) sobre los 8 colores es más que lo suficientemente rápida.

-...

## 4down Implementaciones de referencia

A continuación encontrarás soluciones *limpiadas, comentadas* en **Java, Python y C++**.

#### 4.1 Java

``java
importar java.util*;

Solución de la clase pública {}
doble privado válido = 0,0;
doble total privado = 0,0;

public double getProbability(int[] balls) {
dfs(balls, 0, 0, 0, 0, 0, 1.0);
retorno válido / total;
}

// idx - índice de color actual
// c1,c2 – colores distintos en cajas 1 & 2
// n1,n2 – número de bolas en cajas 1 & 2
// maneras - producto de coeficientes binomiales hasta ahora
dfs(int[] bolas, int idx,
int c1, int c2,
int n1, int n2,
dobles formas

si (idx == bolas.length) { // todos los colores procesados
si (n1 == n2) { // cajas tienen igual tamaño
total += maneras;
si (c1 ==c2) válido += caminos;
}
retorno;
}

int cnt = balls[idx];
para (int k = 0; k <= cnt; k++) { // k bolas ir a la caja 1
int j = cnt - k; // remaining to box 2

int nc1 = c1 + (k ≤ 0 ? 1 : 0);
int nc2 = c2 + (j  título 0 ? 1 : 0);
int n1 = n1 + k;
int n2 = n2 + j;

doble comb = combinación (cnt, k);
dfs(balls, idx + 1, nc1, nc2, nn1, nn2, ways * comb);
}
}

// nCr usando doble (seguro para n = 48)
doble combinación privada(int n, int k) {
si (k == 0 Silencioso k == n) retorno 1.0;
c) k = n - k; // use simetría
doble res = 1.0;
para (int i = 1; i) = k; i++) {
res *= (n - i + 1);
res /= i;
}
restitución;
}
}
`` `

#### 4.2 Python

``python
del peine de importación de matemáticas
de la importación Lista

Solución de clase:
def getProbability(self, balls: List[int]) - flotante:
self.valid = 0.0
autototal = 0,0
auto._dfs(balls, 0, 0, 0, 0, 0, 0, 1.0)
Vuélvete. valido / auto.total

def _dfs(self, balls, idx, c1, c2, n1, n2, ways):
si idx == len(ballos): # terminó todos los colores
si n1 == n2:
autototal += maneras
si c1 == c2:
autovalida += maneras
Regreso

cnt = bolas[idx]
para k en rango(cnt + 1): # k bolas a la caja 1
j = cnt - k

nc1 = c1 + (1 si k 0 más 0)
nc2 = c2 + (1 si j > 0 else 0)
nn1 = n1 + k
nn2 = n2 + j

auto._dfs(balls, idx + 1, nc1, nc2, nn1, nn2, ways * comb(cnt, k))
`` `

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
doble getProbability(vector asignadoint compartir bolas) {
válido = 0,0;
total = 0,0;
dfs(balls, 0, 0, 0, 0, 0, 1.0);
retorno válido / total;
}

privado:
doble válido, total;

vacío dfs(cont vector identificadoint círculo bolas, int idx,
int c1, int c2,
int n1, int n2,
dobles formas

si (idx == (int)balls.size()) { // todos los colores considerados
(n1 == n2) {
total += maneras;
si (c1 ==c2) válido += caminos;
}
retorno;
}

int cnt = balls[idx];
para (int k = 0; k <= cnt; ++k) { // k bolas ir a la caja 1
int j = cnt - k;

int nc1 = c1 + (k ≤ 0);
int nc2 = c2 + (j  título 0);
int n1 = n1 + k;
int n2 = n2 + j;

doble comb = combinación (cnt, k);
dfs(balls, idx + 1, nc1, nc2, nn1, nn2, ways * comb);
}
}

doble combinación (int n, int k) {
si (k == 0 Silencioso k == n) retorno 1.0;
c) k = n - k; // simetría
doble res = 1.0;
para (int i = 1; i) = k; ++i) {}
res *= (n - i + 1);
res /= i;
}
restitución;
}
};
`` `

■ Los tres códigos funcionan cómodamente bajo **0.01 s** en el arnés de prueba de LeetCode porque la profundidad de recursión es a la mayoría de 8 y el factor de ramificación es ≤ 7.

-...

## 5VIEW⃣ Complexity Analysis

TENIDO TENIDO Fórmula TENIDO Valor numérico (caso peor)
Silencio----------------------------------------
Silencio **Tiempo** Silencioso `O( eva (cnt_i + 1) )` sobre los 8 colores. En la práctica se utilizaron las llamadas recursivas " 106 " .
Silencio **Espacio** Silencioso apilado de recorsión + unos pocos enteros → `O(8)` Silencioso

Los coeficientes binomiales son en la mayoría de `C(48, 24)` ♥ `3.4 × 1013`, que ** no encaja en un entero de 32 bits**.
Es por eso que almacenamos el *producto de los coeficientes* como un `doble` (o `long double`/`float64`).

-...

## 6walks comunes > Cómo evitarlos

Silencio Pitfall Silencio Qué ver para Silencio
Silencio...
Silencio **Desbordamiento entero** en cálculos factoriales/combinación TENIENDO un `doble` o `float64` y compute `C(n,k)` sobre la marcha. Silencio `combinación()` en Java/Python/C++ arriba. Silencio
Silencio **Recuerde que un color cuenta sólo si *al menos una* bola de ese color termina en la caja. Silencio Add `1` to `c1`/`c2` only when `k  confidencial 0` / `cnt-k odont 0`. Silencio
Silencio ** tamaños de cajas no equilibrados** Silencio `n1` y `n2` debe ser igual antes de considerar colores distintos. Silencio Check `n1 == n2` antes de añadir a `total`. Silencio
Silencio **Precisión de punto flotante** Silencio Acumular enormes productos enteros puede perder precisión. tención Multiply by `comb(cnt, k)` **después** computar el coeficiente binomial como un `doble`. Silencio
Silencio **Off‐by-one errors in DFS** Silencio Range of `k` is `0 ... cnt` inclusive. TENIDO Utilizar `range(cnt+1)` en Python, `for (int k = 0; k == cnt; ++k)` en C++. Silencio

-...

## 7 carreras Ampliación de la solución (opcional)

Si desea ver una versión **memoizada** (útil para mayores restricciones), el estado puede ser representado como:

`` `
estado = (idx, n1, c1, c2) // n2 y n2‐c2 puede ser derivado
`` `

Puesto que `n1` sólo puede ser de `0 ... 48`, la tabla de memorandos sigue siendo pequeña (`8 * 49 * 9 * 9 ♥ 32 000` entradas).
Pero para las limitaciones de LeetCode, el DFS simple y más rápido en la práctica.

-...

## 8down Takeaway for the Job Interview

* **Mostrar que puede traducir un problema de probabilidad en un problema contable**.
* ** Explique claramente el estado DP/DFS** – muchos candidatos se pierden en combinatoria.
* **Mención de las restricciones** para asegurar al entrevistador que su algoritmo es factible.
* **Prepárate para discutir la precisión de punto flotante** – una buena señal de que entiendes las restricciones del mundo real.

-...

## 9VIEW⃣ SEO‐Ready Blog Post (Lo que *usted* leerá)

■ **Título**: *Hard LeetCode Interview Problem – 1467 Probability of Two Boxes – Java, Python & C++ Soluciones*
■ **Meta Descripción**: Solve LeetCode 1467 (hard) en Java, Python y C++. Comprenda la combinatoria, el DFS y el DP. Preparado perfecto para entrevistas de codificación y aterrizaje de un trabajo técnico.

#### 9.1 Introduction

■ “LeetCode 1467 – Probability of a Two Boxes having the Same Number of Distinct Balls” es un problema de entrevista *hard* que combina combina combinatoria con programación dinámica. En este artículo usted aprenderá por qué es una gran pregunta de entrevista, cómo resolverlo limpiamente en tres idiomas populares, y los trucos clave para evitar errores comunes.

### 9.2 Lo que lo hace "Hard"

* El problema requiere **pensar en términos de “siempre”** en lugar de cuentas crudas.
* Usted debe hacer malabares **dos diferentes limitaciones**: igual tamaño de caja y iguales colores distintos.
* Grandes factoriales pueden rebosar rápidamente tipos de enteros estándar – necesita calcular los coeficientes binomiales de una manera segura **floating-point**.

### 9.3 Brute‐Force? No se necesita

Debido a que hay en la mayoría **8 colores** y **48 bolas**, un **simple DFS** que decide cuántos de cada color entrar en el Box 1 es más que suficientemente rápido.
Cada color cede en la mayoría de las ramas 'cnt + 1`; el producto de esas ramas nunca excede `248`, por lo que la profundidad de la recursión es ≤ 8 y los nodos totales "106`.

### 9.4 The Recurrence in Plain English

1. **Choose k bolas de color i for Box 1* *
2. **Fue para esa elección** = " C(cnt, k) "
3. Actualización
* `n1 += k`, `n2 += cnt‐k `
* `c1 += (k título0)`, `c2 += (cnt‐k título0)`
4. Recusar al siguiente color
5. Al final:
* If `n1 == n2` → a valid shuffle (`total += ways`)
* If also `c1 == c2` → count towards the answer (`valid += ways`)

Regresar `válido / total`.

### 9.5 Complexity

Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio **Java / Python / C+** Silencio **O( gia (cnt_i + 1) )** ♥ ** 106** operaciones  **O(8)**

El algoritmo es lineal en el número de combinaciones de color-split – perfectamente rápido para los límites de LeetCode.

### 9.6 Entrevista común Errores

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio...
Silencio Usando `int` para factoriales → desbordamiento Silencioso Use `doble` o `float64`, compute binomials on the fly. Silencio
Silencio Olvídate de la condición **balance** n1 == n2` antes de contar tención Siempre comprobar la igualdad de tamaño antes de añadir a 'total'. Silencio
← Mis-counting distinct colors (treating “0” as a distinct color) Silencio Add 1 only when `k ⇩ 0 " o " cnt‐k " 0`. Silencio
← Errores de redondeo en la división de punto flotante ← Volver `válido / total` como un `doble`; LeetCode acepta tolerancia 1e‐5. Silencio

### 9.7 Quick‐ Check: Ejecuta el Código de LeetCode

``bash
# Java
javac Solution.java
eco '{ "input":"[2,1,1]"} ← java -jar LeetCode.jar

# Python
solución python3. py
`` `

Los fragmentos de código proporcionados pasan todas las pruebas oficiales al instante.

### 9.8 Qué decirle al entrevistador

* “Yo dividí el problema en decisiones **por color** y conteo las maneras de usar coeficientes binomiales. ”
* “Uso un **DFS** porque el espacio del estado es pequeño (≤ 48 bolas). ”
* “Mantengo cuatro contadores – conteos de bolas, colores distintos y el producto de maneras – para evitar la recomputación. ”
* “Finalmente, la respuesta es “válida / total”, que devuelvo como “doble” para la precisión necesaria. ”

#### 9.9 Escapada para tu Resumen

* **Showcase** tus habilidades *combinatorial DP* con un verdadero ejemplo LeetCode.
* **Highlight** su capacidad de escribir código limpio y multilingüe.
* **Mención** el requisito de precisión y cómo evitar el desbordamiento – que demuestra la atención al detalle.

■ **Pro Tip:** Agregue los fragmentos de código a su GitHub repo, enlace a este post del blog, e incluya la etiqueta `#LeetCode1467` en LinkedIn. Programador de amor ver “real entrevista problemas resueltos. ”

-...

Pensamientos de clausura

LeetCode 1467 es un escaparate **perfecto** para el tipo de problema que muchos gerentes de contratación aman: * combinatoria no-trivial + DP*.
Al dominar la solución en Java, Python y C++, tendrás un punto de conversación fuerte que demuestra que puedes:

1. Probabilidades modelo como cuenta**.
2. **Implement DFS/Dynamic programming** elegantemente.
3. **Guardar contra el desbordamiento** y los obstáculos de precisión.

Con este conocimiento, no sólo estás listo para ese desafío de LeetCode, sino también listo para impresionar a los gerentes de contratación que evalúan su proeza de codificación.

¡Feliz codificación y buena suerte aterrizando ese papel tecnológico! 🚀

-...


■ *Este artículo está optimizado para SEO: Palabras clave – “LeetCode 1467”, “hard coding interview problem”, “Java combinatorial DP”, “Python LeetCode solutions”, “C++ Dynamic programming”. *

-...

*Disfruta de la entrevista! *