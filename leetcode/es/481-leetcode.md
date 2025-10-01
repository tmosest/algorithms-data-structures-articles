-...
Título: LeetCode 481. Pendiente mágica -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 481. Pendiente Mágica – Código & Blog

-...

### 1. Recaptación de problemas

A **magical string** `s` consists only of the digits `1` and `2`.
Si usted mira el *run‐length* de dígitos idénticos consecutivos en `s`, el
secuencia de esas longitudes de ejecución es exactamente 's' en sí.

`` `
s = 1 22 11 2 1 22 1 22 11 2 11 22 ...
↑ ↑ ↑ ↑ ↑ ↑ ↑
longitudes = 1 2 2 1 1 2 1 2 2 1 2 1 2 ...
`` `

Dado un entero `n (1 ≤ n ≤ 10^5)`, devuelve cuántos `'1'' aparecen en el
primer `n` caracteres de `s`.

-...

### 2. Brute‐Force vs. Optimal

Silencio Silencio Silencio Silencio Silencio Silencio Silencio Silencio
Silencio----------------------------
Silencio Build `s` character‐by-character up to `n` TEN **O(n)** Silencio **O(n)** Silencio Funciona para las limitaciones, pero `StringBuilder` en Java o concatenación repetida en Python puede ser costoso. Silencio
Silencio Pre-compute run‐lengths in an array and generate `s` on the fly Silencio **O(n)** Silencio **O(n)** Silencio Solución óptima más común. Silencio
Silencio Definición Recursiva con la memoización Silencio **O(n)** Silencio **O(n)** Silencio Funciona pero sobrematar para este tamaño. Silencio

■ **Bien** – O(n) tiempo, O(n) memoria, directo a entender.
■ **Bad** – Usar la concatenación de `String` en Java/Python puede alcanzar el tiempo cuadrático.
■ **Ugly** – Algunas soluciones en línea utilizan `LinkedList` o recursión, que añaden una sobrecarga innecesaria y ocultan la lógica.

-...

### 3. Algoritmo (Tiempo de Trabajo, O n) Espacio)

1. **Pre-allocate** un `int[] s` de longitud `n` para almacenar la cuerda mágica como
números 1 o 2.
2. `s[0] = 1`, `s[1] = 2`, `s[2] = 2`.
Estos son los primeros tres dígitos que satisfacen la definición.
3. Mantenga dos puntos:
* `idx` – el índice en `s` que estamos leyendo actualmente para conocer la longitud de ejecución.
* `cur` – la posición actual a la que estamos escribiendo en `s`.
4. Mientras que "cur"
* `len = s[idx]` (run‐length: either 1 or 2).
* `val = 3 - s[cur-1]` – rebosa entre 1 y 2.
* Write `len` copies of `val` into `s` starting at `cur`.
Para si llegamos a `n`.
* Increment `idx` and `cur` accordingly.
5. Finalmente, cuenta cuántos `1`s están en las primeras `n` posiciones.

Debido a que cada personaje está escrito exactamente una vez, el algoritmo es lineal.

-...

### 4. Aplicación

##### Java (estilo LeetCode)

``java
Clase Solución {
público int mágico String(int n) {
(n == 0) retorno 0;

// Construir la cadena como un array int.
int[] s = nuevo int[n];
s[0] = 1; // los primeros tres dígitos se fijan
si (n √≥ 1) s[1] = 2;
si (n √≥ 2) s[2] = 2;

int idx = 2; // posición en s que indica la longitud de la carrera
int cur = 3; // siguiente posición gratuita para escribir
int one = 1; // ya colocamos uno '1' en s[0]

mientras (cuerdo) {
int len = s[idx]; // 1 o 2
int val = 3 - s[curo - 1]; // toggle between 1 and 2

// Write `len` copies of `val`
para (int i = 0; i) {}
s[cur++] = val;
(val == 1) uno++;
}
idx++;
}

de retorno;
}
}
`` `

#### Python

``python
Solución de clase:
def magicString(self, n: int) - int:
si n == 0:
retorno 0

s = [0]
s[0] = 1
si n √≥ 1: s[1] = 2
si n √≥ 2: s[2] = 2

idx, cur, uno = 2, 3, 1 # idx: read pos, cur: write pos, uno: count

mientras se curan
longitud = s[idx] # 1 o 2
val = 3 - s[cur - 1] # toggle between 1 and 2

para _ en rango(duración):
si cur >= n:
descanso
s[cur] = val
si vale == 1:
+= 1
cur += 1
idx += 1

de retorno
`` `

###### C++

``cpp
Clase Solución {
public:
int magic String(int n) {
(n == 0) retorno 0;
vector:
s[0] = 1;
si (n √≥ 1) s[1] = 2;
si (n √≥ 2) s[2] = 2;

int idx = 2; // índice de lectura
int cur = 3; //
int one = 1; // ya hemos colocado un 1

mientras (cuerdo) {
int len = s[idx]; // 1 o 2
int val = 3 - s[curo - 1]; // toggle

para (int i = 0; i) {}
s[cur++] = val;
(val == 1) ++ones;
}
++idx;
}
de retorno;
}
};
`` `

-...

### 5. Blog Artículo – “LeetCode 481: Magical String – Una profunda cueva para su próxima entrevista de codificación”

■ **Meta Descripción**
■ Master LeetCode 481 “Magical String” en Java, Python y C++ con una solución O(n). Entender el problema, los obstáculos y cómo llegar a esta pregunta de entrevista media.

-...

##### Introducción

Si se está preparando para entrevistas de ingeniería de software, el problema LeetCode **481. Magical String** es un ejercicio perfecto *media*–dificultad. Prueba tu habilidad para:

- Traducir una definición formal en código.
- Generar una secuencia en la mosca sin almacenar toda la cuerda en memoria.
- Optimize for time and space.

En este post caminaremos a través de la declaración del problema, ilustramos una solución O(n) limpia, examinaremos los obstáculos comunes (“malos” y patrones “muy”), y proporcionar implementaciones listas para copiar en **Java**, **Python**, y **C+**.

-...

#### Problema Recap (Lo que el entrevistador quiere)

■ A *magical string* `s` consists only of the digits `1` and `2`.
■ Si se agrupan dígitos idénticos consecutivos en `s`, el *run‐length* de cada grupo equivale al dígito correspondiente en `s` misma.

■ * Objetivo*
■ Devolver el número de `'1's en los primeros `n` caracteres de `s` (`1 ≤ n ≤ 10^5`).

■ *Examples*
" `
Ø n = 6 → s = 122112 → 3
1 → s = 1 → 1 uno
" `

-...

#### ¿Por qué es interesante este problema?

- ** Secuencia autoreferencial** – La cuerda se define, un patrón clásico visto en problemas de tipo Fibonacci.
- **Codificación de Rin‐Length** – Usted construirá una cuerda de su representación de longitud, un truco común de entrevista.
**Large Input Size** – Usted debe evitar enfoques O(n^2) como la concatenación de cuerda repetida.

-...

#### Naïve Approaches (The Bad)

1. **Concatenación Relacionada** –
``java
String s = ";
mientras (s.length()
s += (s.length() == 0 ? "1" : (s.length() % 2 == 0 ? "22" : "1"));
}
`` `
*Por qué es malo:* Cada `+=` en un `String` crea un nuevo objeto → O(n2) tiempo.

2. **Lista enlazada de caracteres** –
``java
VinculadoLista realizadoInteger ratio = nuevo LinkedList fiel();
list.add(1); list.add(2); list.add(2);
`` `
*Por qué es malo:* Linked List overhead es alto, y todavía se iteran sobre la lista muchas veces.

Estos patrones son fáciles de escribir pero hacen que la solución falle por `n = 10^5`.

-...

#### Optimal Strategy (The Good)

1. **Pre-allocate an array** of size `n` (or an `int[]` in Java, `vector fielint `` in C++, `list[int]` in Python.
2. **Uso de dos puntos**:
- `idx` - lee la longitud de ejecución del array.
- `cur` - escribe el próximo grupo en el array.
3. **Cambio entre 1 y 2** por `val = 3 - prev`, evitando las declaraciones condicionales.
4. **El punto '1' está en la mosca** - no hay necesidad de un segundo paso.

** Complejidad del tiempo:** `O(n)` - cada elemento se escribe exactamente una vez.
** Complejidad del espacio:** `O(n)` – mantenemos la gama de longitud `n` (el almacenamiento mínimo necesario).

-...

#### Walkthrough (Illustration)

`` `
Inicio: s[0] = 1, s[1] = 2, s[2] = 2
idx = 2 (punto al tercer elemento que indica la longitud de ejecución 2)
cur = 3 (la siguiente posición libre)

Loop:
lino = s[idx] = 2 // necesitamos un grupo de 2 dígitos
val = 3 - s[cur-1] = 3-2 = 1 // toggle to 1
Escriba 2 copias de 1 en las posiciones 3 y 4
+= 2
idx++ → 3
cur+++ → 5
`` `

Continuar hasta `cur == n`. El array ahora contiene los primeros 'n' dígitos de la cuerda mágica, y ya sabemos cuántos contamos.

-...

##### El Código

■ #Java #
. ``java
Solución de clase {}
# Public int magic String(int n) { ... }
.
" `

■ Python
.
Solución de clase:
√≠ def magicString(self, n: int) - confiar int: ...
" `

■ **C++**
, ``cpp
Solución de clase {}
" Public:
# Int magicString(int n) {...}
};
" `

*(Ver los bloques de código arriba para las implementaciones completas.) *

-...

#### Edge Cases & Testing

← Intromisión esperada
Silencio...
Silencio 1 Silencio 1 Silencio Únicamente el primer dígito `1`. Silencio
TENIDO 2 TENIDO 1 TENIDO `12` - todavía uno `1`. Silencio
TENIDO 3 TENIDO 1 TENIDO `122` – sólo el primer dígito es `1`. Silencio
Silencio 4 Silencio 2 Silencio `1221` – dos `1`s
TEN 100000 TENIDO *alguno número* ANTE Asegurar que el algoritmo funciona dentro del límite de tiempo. Silencio

Siempre prueba los límites inferiores, el valor exacto `n = 10^5` y los valores de rango medio aleatorio.

-...

#### Common Interview Traps

Silencio tóxico Qué ver para vivir
Silencio...
← Errores desactivados por uno TENIENDO Recordar que `idx` comienza en `2` (tercer elemento). Silencio
Silencio Integer overflow ¦ `n ≤ 10^5`, so `int` is safe. Silencio
TENIDO ANTERIOR Wrong toggle TENIDO Use `val = 3 - prev` en lugar de `prev == 1 ? 2 : 1`. Silencio
← Los bucles innecesarios ← Evite los bucles anidados que se iteran sobre partes ya generadas. Silencio

-...

#### Pensamientos Finales (El Ugly)

Algunas soluciones en el uso de Internet:

- ** Generación recursiva** con memoización – trabaja pero oculta la naturaleza lineal y aumenta el riesgo de profundidad de pila.
- **Lista enlazado o cola** para la secuencia de longitud de ejecución – añade factores constantes que importan para límites de tiempo ajustados.
- **StringBuilder with many `append` calls** – still O(n) but the constant factor is higher than array manipulation.

Adherirse al enfoque lineal basado en array para una solución limpia y rápida.

-...

##### SEO Resumen

- **Keywords**: *LeetCode 481*, *Magical String*, *Java solution*, *Python solution*, *C++ solution*, *coding interview*, *algorithm*, *job interview*, *software engineering*, *programming interview questions*.
- **Meta**: “Solve LeetCode 481 – Magical String in Java, Python & C++ con un algoritmo O(n). Aprende cómo llegar a esta pregunta de entrevista. ”

-...

### 6. Lista de verificación de la entrada

- [ ] Entender la definición de una cuerda mágica.
- [ ] Utilice un array para almacenar la secuencia – sin concatenación de cadenas.
Mantener dos punteros ( " idx " , " ) y cambiar valores con " 3 - prev " .
- [ ] Cuenta los que generan el array.
[ ] Verificar con casos de borde (1, 2, 3, 4, 10^5).
- [ ] Mantenga la solución tiempo O(n) y memoria O(n).

Buena suerte, y feliz codificación!