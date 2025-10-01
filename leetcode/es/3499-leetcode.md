-...
Título: LeetCode 3499. Maximizar la sección activa con el comercio Yo...
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1down El problema de estilo LeetCode “Maximise Active Sections”

■ *Problema*
■ Se le da una cadena binaria **s** (`'0'` = inactiva, `'1'` = activa).
■ Un *trade* consta de:
■ 1. Elegir un bloque contiguo de `'1's que está rodeado** por `'0'`s en *ambos* lados.
■ 2. Reemplazando ese bloque de `'1'''s con un bloque más largo de `'1'''s por "filling inflood" en los alrededores `'0'`s – el nuevo bloque se extiende hasta el siguiente `'1' bloque (o hasta que la cadena termina).
■
■ Usted puede realizar ** en la mayoría de un intercambio**.
■ Devuelve el número máximo de `'1's** que puede estar presente después del comercio (o después de no hacer nada si un comercio es imposible).

■ **Constraints**
√≥ 1 ≤ неливывый ≤ 105
* s consiste solamente en `'0'` y `'1'`

El problema aparece en LeetCode como *Secciones activas de Máximo Después de un Comercio* (ID ♥ 1690 – renombrarlo “Secciones activas de Máximo Después de un Comercio”).

■ ¿Por qué importa? * *
■ En una entrevista de calidad de producción, se pide a un candidato que optimice una operación de “trade” basada en cadenas. El truco es darse cuenta de que el único beneficio viene de convertir un bloque de ''1'''' rodeado de ceros en un bloque más largo de ''1''' que "absorbe" los ceros en ** ambos lados**.
■ Ese beneficio equivale a la suma de los dos ceros adyacentes que se sientan a cada lado del `'1'` bloque elegido.

-...

Rápido Mira el Algoritmo

1. **Nota el original `'1''s** - `ones`.
2. **Scan la cuerda** mientras mantiene:
* `curZero` - longitud de la actual racha de `'0'`.
* `prevZero` - longitud de la anterior racha de `'0' que está * redondeada* por `'1'''s.
3. Cada vez que vemos un `'1' después de algunos ceros, movemos `curZero` hacia `prevZero` y reasentamos `curZero`.
4. Si más tarde encontramos otro número de ceros seguidos por un `'1'`, podemos **trade** ese medio `'1'`` bloque y ganar `prevZero + curZero` nuevo `'1's.
5. Mantenga el máximo de todas esas ganancias ( " mejor gain " ).
*Si no hay comercio posible ( `bestGain == 0`) la respuesta es simplemente `ones`.*

El análisis completo es **O(n)** tiempo y **O(1)** espacio.

-...

## 3down Implementaciones de referencia

A continuación se presentan tres implementaciones *totalmente trabajando* – Java, Python 3 y C++– que siguen la misma lógica. Todos ellos compilan en el entorno estándar de LeetCode (`clase Solution { ... }`).

■ *Nota*
■ Los tres códigos asumen la firma de la función:

``java
Clase Solución {
public int maxActiveSections AfterTrade(String s) { ... }
}
`` `

``python
Solución de clase:
def maxActiveSections AfterTrade(self, s: str) - título int: ...
`` `

``cpp
Clase Solución {
public:
int maxActiveSectionsAfterTrade(string s) { ... }
};
`` `

-...

### 3.1 Java

``java
Clase Solución {
public int maxActiveSections AfterTrade(String s) {
// Número total de secciones activas inicialmente
int one = 0;
para (char ch : s.toCharArray()) {}
si (ch == '1') ++;
}

// Escáner para cero corres adyacentes
int bestGain = 0; // mejor suma de dos carreras cero adyacentes
int curZero = 0; // longitud de la corriente cero
int prevZero = 0; // longitud de la carrera cero anterior

(int i = 0; i) s.length(); ++i) {
char c = s.charAt(i);
si {}
curZero++; // seguir contando ceros
# Si no... # '
si (prevZero √≥ 0 " curvaZero " 0) {
bestGain = Math.max(bestGain, prevZero + curZero);
}
// La carrera de ceros que acabamos de terminar se convierte en el 'previous'
prevZero = curro Cero;
curZero = 0; // reseteo para la próxima carrera
}
}

// En caso de que la cadena termine con ceros – no pueden ser utilizados para un comercio,
// por lo que ignoramos el último curZero por no añadirlo al mejorGain.

de retorno + bestGain; // comercio es opcional
}
}
`` `

-...

#### 3.2 Python 3

``python
Solución de clase:
def maxActiveSections AfterTrade(self, s: str) - título int:
# Cuenta las secciones activas existentes
s.count('1')

best_gain = 0
cur_zero = 0
prev_zero = 0

por ch en s:
si ch == '0':
cur_zero += 1
# ch == '1'
si prev_zero 0:
best_gain = max(best_gain, prev_zero + cur_zero)
prev_zero = cur_zero
cur_zero = 0

de retorno + mejor_gain
`` `

-...

### 3.3 C++

``cpp
Clase Solución {
public:
int maxActiveSectionsAfterTrade(string s) {
int one = 0;
para (char ch : s) si (ch == '1') ++ones;

int bestGain = 0;
int curZero = 0, prevZero = 0;

para (char ch : s) {}
si
++curZero;
[ // ch == '1 '
si (prevZero √≥ 0 " curvaZero " 0)
bestGain = max(bestGain, prevZero + curZero);
prevZero = curro Cero;
curZero = 0;
}
}

de retorno + bestGain; // si mejorGain es 0, simplemente devolvemos los
}
};
`` `

Las tres soluciones se ejecutan en tiempo **O(n)**, utilizar **O(1)** espacio auxiliar, y pasar la limitación de 105 longitudes.

-...

## 4down El artículo del blog – “Masterizar el problema de las secciones activas máximas (bueno, malo y ugly)”

■ *Título*
■ **Maximise Active Sections After One Trade – A Deep Dive into a LeetCode Hard Problem* *
■ **Meta‐Description**:
■ Desbloquear los secretos del problema de las secciones activas de Maximise. Aprenda el truco inteligente O(n), entienda los casos de borde, y vea por qué es necesario resolver para entrevistas de ingeniería de software.

### 1. Introducción

El **Maximise Active Sections After One Trade** problema es un favorito en las plataformas de coding-interview como LeetCode y HackerRank. La historia suena simple: tienes una cadena binaria, se te permite realizar un único “trade”, y quieres terminar con lo más posible. En la práctica, el problema es un hermoso ejercicio en ** análisis de longitud**, ** manejo por caso entero**, y ** mentalidad de optimización**.

■ *¿Por qué aparece a menudo en entrevistas? *
■ Debido a que esconde una sutileza: la única manera de obtener un beneficio de un comercio es reemplazar un bloque de `'1's que es *redondeado* por `'0'`s con un bloque más largo que “absorbe” esos ceros. Enseña a los candidatos a convertir un problema verbal en un algoritmo concreto.

### 2. Restatement del problema (Plain English)

- ** Entrada**: Una cadena binaria `s` (`'0'` = inactiva, `'1' = activa).
- Reglas de comercio**:
1. Elija un bloque contiguo de `'1's **flanked** por `'0'`s en los lados * ambos*.
2. Reemplazar ese bloque con un nuevo bloque de `'1' que se extiende hasta el siguiente `'1' bloque (o el cordón termina).
- ** Objetivo**: Después de realizar en la mayoría de un oficio, devuelve el número máximo de `'1's** que puede aparecer en la cuerda.

La longitud de la cadena puede ser hasta 100 000, por lo que una simulación ingenua está fuera de la cuestión.

### 3. “Bien” – El Clever O(n) Insight

La observación clave:
■ **El beneficio del comercio equivale a la longitud de los dos cero-runs en cada lado de la `'1''` bloque elegido. #
■ En otras palabras, estamos buscando un patrón `0...0 1...1 0...0` y podemos "squeeze" el medio `'1''' bloque en los ceros izquierdo y derecho.
■ El beneficio es `leftZeroRun + rightZeroRun`.

Desde este punto de vista el problema se reduce a:

1. Cuenta ya existente `'1's – ese es el valor base.
2. Encontrar la suma **maximum de dos consecutivos cero-runs** que son *sandwiched* entre `'1's.
3. Añadir esa suma máxima al valor base.
4. Si no existe tal par, la respuesta es sólo el valor base (hacer nada siempre está permitido).

### 3.1 Manejo de los casos de borde

Silencio ¿Por qué es complicado ← Cómo nuestro algoritmo se enfrenta a ¦
Silencio------
Silencio Zero-runs al principio o al final de la cuerda Silencio No están *redondeados* por `'1'`s, por lo que no pueden ser parte de un comercio. El escaneo nunca añade el primer o último cero-run a `bestGain`. Silencio
Silencio bloques consecutivos `'1'` sin ceros entre ellos Silencio No es posible el comercio, porque el medio `'1'` bloque no está rodeado de ceros. El algoritmo simplemente nunca actualiza `bestGain` – se mantiene `0`. Silencio
Silencio Muy largo cero-run que puentea toda la cadena El comercio sería un no-op, ya que no hay nada en el otro lado para reemplazar. El primer cero-run nunca se convierte en 'prevZero' (su anterior char no es ''1''). Silencio

### 4. “Bad” – Por qué el enfoque ingenuo es una mala idea

Un primer intento podría ser:

1. Enumerar todos los bloques medios posibles.
2. Para cada uno, simula el comercio escaneando hacia adelante y hacia atrás hasta el siguiente `'1'.
3. Cuenta las nuevas ''1'''s, mantén las mejores.

Esa es una solución **O(n2)**: para una cadena de 105 caracteres que sería timeout. Es “malo” porque:

- ignora la naturaleza *corriente* del problema.
- Utiliza el trabajo cuadrático cuando el trabajo lineal es suficiente.
- Forza al candidato a pensar en una simulación cara en lugar de un simple escaneo.

### 5. “Ugly” – La implementación de Ugly de larga duración

Muchos entrevistados o estudiantes escriben una solución *muy* brute‐force que:

``python
para i en rango(len(s)):
para j en rango(i, len(s)):
si s[i:j+1] == '1'*k y s[i-1] == '0' y s[j+1] == '0':
# ... la simulación de relleno de inundación ...
`` `

El bucle interior re-reads partes de la cuerda repetidamente, lo que conduce a una complejidad **time que explota**. También es *muy* porque:

- El código es difícil de leer – bucles anidados, muchos cheques de índice.
- Es frágil – errores de índice pequeños causan `IndexError` o resultados incorrectos.
- Es exagerado – el problema no requiere una simulación de relleno de inundación.

El editorial de LeetCode, sin embargo, destaca la elegante solución de dos puntos de duración, convirtiendo al feo en un algoritmo limpio, legible y eficiente de un paso.

### 6. The Linear‐Time Trick Explained

En el corazón de la solución O(n) es la técnica **2 puntos de ejecución**:

1. **Current Zero Run (`curZero`)** – mientras vemos ''0' 's simplemente los contamos.
2. ** Previous Zero Run (`prevZero`)** – cuando golpeamos un `'1'`, tratamos la carrera de ceros que acabamos de terminar como el "alquien izquierdo" para el próximo comercio potencial.
3. Cada vez que la siguiente carrera de ceros sigue que `'1'` bloque, podemos **trade** y ganar `prevZero + curZero`.
4. Nunca necesitamos mirar más allá del próximo cero inmediato - que es toda la información necesaria.

Este enfoque es similar al problema clásico “maximum sub-array”: mantiene una ventana de rodadura, actualiza un mejor valor, y nunca revisita partes procesadas.

### 7. Real‐World Takeaway

■ *Si usted puede reducir una operación aparentemente complicada “trade” a un simple “pick dos ceros vecinos y reemplazar los medios”, estará listo para preguntas en*:
* Codificación Run‐length (común en algoritmos de compresión).
* Manipulación de cuerdas en problemas de entrevista.
* Optimización de operaciones en estructuras de datos (por ejemplo, árboles de segmentos, árboles Fenwick).
* Sensibilización por caso de Edge – especialmente cuando se trata de condiciones “redondeadas”.

### 8. TL;DR – La Solución 3-Lina

``text
uno = cuenta('1')
prevZero = curZero = 0
para c en s:
si c == '0': curZero += 1
más:
mejor = max(best, prevZero + curZero)
prevZero, curZero = curZero, 0
de retorno + mejor
`` `

Ese es el corazón de cada solución aceptada. Una vez que lo entiendes, el problema es una brisa.

### 9. Ejercicios de práctica

Silencio ¿Por qué es útil
Silencio...
Silencio 1 ← Implementar la solución en **Rust** – practicar la vida útil > cotejo prestado. ← Construye habilidades de manejo de cuerdas de bajo nivel. Silencio
Silencio 2 tención Modifique la función para devolver los *indices* del bloque de comercio óptimo. tención Teaches mapear de nuevo del algoritmo al problema original. Silencio
Silencio 3 Silencio Generalizar a una versión **k-trade** – usted puede realizar hasta 'k' comercios. tención te reta a pensar en las soluciones DP o segment‐tree. Silencio

#### 10. Pensamientos finales

El problema **Maximise Active Sections** es un reto pequeño y autónomo que enseña las lecciones *grandes*:

- **Traducir palabras a correr** – buscar siempre grupos contiguos.
- **Las maletas de Edge son la prueba real** – recuerden que las primeras y últimas carreras de ceros no se pueden utilizar para un comercio.
- **Optimise early** – una simulación O(n2) siempre te dejará atascado; piensa en pases lineales.

Maestro este problema, y encontrará que muchas otras preguntas de entrevista se vuelven mucho más fáciles. ¡Feliz codificación!



■ **Keywords** – *LeetCode, entrevista, desafío de codificación, cadena binaria, codificación de longitud, algoritmo de O(n), un comercio, secciones activas, relleno de inundación, análisis de ejecución, entrevista de ingeniería de software*
■ **Tags** – *LeetCode, Interview, Algorithms, String, Sliding Window, Dynamic Programming*



-...

Feliz solución, y que su ''1' siempre esté en la mayoría!