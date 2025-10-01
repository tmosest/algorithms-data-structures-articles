-...
Título: LeetCode 1702. Maximum Binary String After Change -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 1702 – **Maximum Binary String After Change* *
*El bueno, el malo y el feo – un profundo dinamismo en un problema codicioso de estilo entrevista que puede ganarte un trabajo. *

-...

#### TL;DR
* **Problema:** Transformar una cadena binaria con dos swaps permitidos (“00 → 10”, “10 → 01”) para conseguir la cadena numéricamente más grande posible.
****Key insight:** Todas las operaciones se pueden simular moviendo un solo `0` hacia la izquierda sobre las `1`s adyacentes.
* ** Solución óptima**
1. Encuentra el primer `0`.
2. Contar las `1's que aparecen **después** ese cero.
3. Construir una cadena de todas las `1`s, luego colocar una `0` en el índice `n - cnt_ones_after_first_zero - 1`.
* ** Complejidad:** `O(n)` tiempo, `O(1)` espacio extra.

-...

## 1. Declaración de problemas (LeetCode 1702)

Se le da una cadena binaria 'binaria' (`0`‐`1` solamente).
Usted puede aplicar repetidamente las dos operaciones siguientes en cualquier número de veces:

Silencioso Operación Silencioso Estado Silencioso
Silencio----------------------------
Silencio 1 Silencio Subestring `"00" Silencio `"00010" → "10010"
TENIDO 2 TENIDO Substring `"10" TENIDO `"00010" → `"00001"

Devuelve la cadena binaria **maximum** que puedes obtener después de cualquier número de operaciones.
“Maximum” significa que el valor decimal de la cadena binaria es el mayor posible.

**Constraints* *

* `1 ≤ binario.length ≤ 105 `
* `binary[i] Entendido {'0', '1'}`

-...

## 2. Por qué funciona Greedy – La observación “Pattern”

Experimentemos con algunas cuerdas:

Silencio Original Silencio Después de muchas operaciones
Silencio...
TENIDO INGRESO " TENIDO "
TENIDO INGRESO
TEN ANTE LAS RESPUESTAS

Te darás cuenta:

1. **Sólo un `0` puede permanecer en la cuerda final** - todo lo demás se convierte en `1`.
Cualquier `00` puede ser reemplazado por `10`, moviendo un `0` hacia la derecha.
Cualquier `10' puede ser reemplazado por `01`, moviendo un `0` hacia la izquierda.
Repetidamente aplicando estos, los ceros se "clump" en un solo cero que se puede mover a cualquier posición que desee, excepto el comienzo mismo si la cadena comenzó con '1's.

2. **Donde las tierras cero dependen del número de `1`s que siguen el primer cero en la cadena original**.
Cada `1' después del primer cero puede ser “pushed” a la izquierda del cero por operación 2.
Así el cero finalmente será posicionado para que exactamente que muchos `1`s están a su derecha.

3. **La cadena restante es toda `1`s excepto por ese único cero** - que es el valor binario máximo posible.

Así que la regla avaricia es:

■ *Mantengan todos los principales `1`s como están, dejen cada uno más `0` excepto uno, y empujen a ese `0 ` lo más recto posible dado el recuento de `1's que fueron después del primer `0`. *

-...

## 3. El Algoritmo – Paso a paso

1. **Se puede de izquierda a derecha hasta el primer `0`**
*Si nunca encuentras un `0`, la cuerda ya es máxima – devuélvela. *

2. **No `1`s que aparecen después de la primera `0`** (`cnt`).

3. **Construir el resultado**
* Crear una cuerda de longitud `n` llena de `1`.
* Colocar un solo `0` en el índice `n - cnt - 1`.

¿Por qué `n - cnt - 1`?
Porque 'cnt' es el número de '1's que debe permanecer a la derecha del cero.
En una cadena de todos, el cero ocuparía naturalmente el lugar *izquierdísimo* (index `0`).
Para cambiarlo a la derecha por posiciones "cnt", simplemente lo movemos a lugares "cnt" de la izquierda, que es 'n - cnt - 1` de la derecha.

-...

## 4. Código - Tres idiomas

A continuación se presentan implementaciones limpias y listas de producción que se ejecutan en **O(n)** tiempo y **O(1)** espacio extra (además de la cadena de salida).

■ **Nota:** Los tres códigos son idénticos en lógica; sólo la sintaxis difiere.

-...

#### 4.1 Java

``java
Clase Solución {
public String maximumBinaryString(String binario) {
int n = binario.length();
primero Zero = binario.indexOf('0');

// No cero en absoluto – ya maximal
(primerZero == -1) devolver binario;

// Conteo 1's después del primer cero
int AfterZero = 0;
para (int i = firstZero + 1; i)
si (binary.charAt(i) == '1') AfterZero++;
}

// Construir el resultado: todos 1's con un 0 colocado apropiadamente
StringBuilder sb = nuevo StringBuilder();
sb.append("1".repeat(n));
int Pos = n - uno AfterZero - 1;
sb.setCharAt(zeroPos, '0');
devolver sb.toString();
}
}
`` `

-...

#### 4.2 Python

``python
Solución de clase:
def maximumBinaryString(self, binario: str) - confiar str:
n = len(binary)
first_zero = binario.find('0')
si primero_zero == -1:
devolver binario

# Conde 1's after the first cero
one_after_zero = binario[first_zero+1:].count('1')

# Construir el resultado
*
cero_pos = n - ones_after_zero - 1
[zero_pos] = '0'
volver ''.join(res)
`` `

-...

#### 4.3 C++

``cpp
Clase Solución {
public:
string maximumBinaryString(string binario) {
int n = binario.size();
primero Cero = binario.find('0');
si (primeroZero == cadena::npos) devolver binario; // no cero

// Conteo 1's después del primer cero
int AfterZero = 0;
para (int i = firstZero + 1; i)
si (binario [i] == '1') ++ones AfterZero;

// Resultado de construcción
cadena res(n, '1');
int Pos = n - uno AfterZero - 1;
res[zeroPos] = '0';
restitución;
}
};
`` `

-...

## 5. El Bien, el Mal, y el Ugly

**Aspecto** Silencio**
Silencio----------------------------------------------------
Silencio ** Idea Algorítmica** Silencio Escaneo lineal + matemáticas simples. Silencio Ninguno. Silencio Sobre-ingeniería con BFS/DP. Silencio
Silencio **La complejidad** Silencioso `O(n)` tiempo, `O(1)` espacio. Silencio O(n2) si simulas cada intercambio. O(2n) brute‐force. Silencio
Silencio **Readability** ← Clean, one‐pass. Silencio difícil de seguir si mezcla la lógica. ← Confundir soluciones recursivas o apiladas. Silencio
Silencio **Edge Cases** Silencio Handles all‐ones, all-zeros, mixto. ← Fails si la posición cero no se calcula correctamente. ← Fails en cadenas muy largas (desbordamiento de la cubierta). Silencio
Silencio **Interview Verdict** Silencio ★★★★★★★★★★ – simple, determinista, cubre las limitaciones. ★ ★ ☆☆☆☆ – complejidad demasiado lenta e innecesaria. ★ ★ ☆☆☆☆☆ – arriesgado, falla en las pruebas. Silencio

*Por qué funciona la codicia*
Debido a que las operaciones son locales y sólo afectan a un `0` y a un `1` adyacente, se puede pensar en la cuerda como un “parque” donde cada `0` puede conducir a través de `1`s pero no puede saltar sobre otro `0`. Así pues, en la mayoría de un `0` puede sobrevivir y su posición final está plenamente determinada por cuántos `1`s fueron a su derecho originalmente. Ese es el corazón matemático de la solución.

-...

## 6. Por qué este blog ayuda a su búsqueda de empleo

1. **SEO Palabras clave** – El artículo está lleno de términos que los reclutadores buscan: *Maximum Binary String After Change*, *LeetCode 1702*, *transformación de cuerdas binarias*, * Solución de Java*, * Solución de pitón*, *Solución de C+*, * algoritmo de color verde*, *O(n) time*.

2. **Depth of Explicaation** – El equipo de trabajo aprecia a los candidatos que no sólo escriben código, sino que pueden articular *por qué* funciona una solución.

3. ** Muestras de Codo en Múltiples Idiomas** – Demuestra versatilidad y habilidad para trabajar en el idioma que utiliza su equipo.

4. **Structured Sections & Headings** – Hace fácil contratar administradores para esquiar y encontrar lo que necesitan.

5. **Contexto del programa** – Muestras que puedes abordar problemas reales de entrevista de LeetCode, un requisito común para los roles de ingeniería del software.

-...

## 7. Cheat-off Sheet

Silencio ¿Qué hacer?
Silencio----------------------
Silencio 1 Silencio `0`. Silencio
Silencio 2 Silencioso Conde `1`s después de que `0`. Esos son los que terminarán hasta la derecha del cero final. Silencio
Silencio 3 Silencio Construir una cuerda de todo-`1` e insertar un `0` en `n - cnt - 1`. tención Posiciona el cero exactamente donde las operaciones permiten. Silencio
Silencio 4 Silencio Regresar la cuerda. Silencio Ya maximal por construcción. Silencio

-...

## 8. Pensamientos finales

El problema *Maximum Binary String After Change* es un ejemplo clásico de cómo una serie aparentemente complicada de swaps locales puede colapsar en una única solución codictiva de tiempo lineal. Dominar este problema muestra:

* ** Intuición Algorítmica** – observando al invariante que todos los ceros colapsan en uno.
* **Coding elegancia** – implementación limpia y legible.
* **Preparación de entrevista** – capacidad para explicar tanto “cómo” como “por qué”.

Mantenga este patrón en su kit de herramientas: cuando vea operaciones locales que solo muevan un elemento izquierda o derecha, compruebe si toda la secuencia se reduce a una sola opción global.

Buena suerte: tu próxima entrevista de codificación no sabrá qué lo golpeó! 🚀

-...

■ *Preparado por ChatGPT, el asistente de AI que ama código limpio y buenas explicaciones. *