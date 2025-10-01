-...
Título: LeetCode 3398. Subestring más pequeña con caracteres idénticos Yo...
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 3398 – Subestring más pequeña con caracteres idénticos I
*Hard – búsqueda binaria en la respuesta*

Silencio Idioma Silencio Complejidad
Silencio----------------------------
Silencio **Java** Silencioso `O(n log n)` tiempo, `O(1)` extra space Ø [LeetCode](https://leetcode.com/problems/smallest-substring-with-identical-characters-i/) Silencio
Silencio **Python** Silencio `O(n log n)` time, `O(1)` espacio adicional ←
tención **C+** Silencioso `O(n log n)` tiempo, `O(1)` espacio adicional ←

-...

### 1. Reposición de problemas

Se le da una cadena binaria `s` (`'0'` y `'1'') y un entero `numOps`.
Usted puede cambiar cualquier poco a la mayoría de `num Horas.
Después de las vueltas, encuentre la longitud mínima posible** del bloque contiguo más largo de caracteres idénticos.

-...

### 2. Intuición

Si se le pregunta “¿podemos hacer el bloque más largo ≤ L?” la respuesta sólo depende de los *runs* de caracteres iguales que son más largos que `L`.
Una carrera de longitud `R не L` se puede dividir en pedazos de longitud en la mayoría de `L` girando algunos pedazos dentro de esa carrera.
La forma más barata de hacerlo es romper la carrera de cada 'L+1` posiciones:

`` `
R = q·(L+1) + r (0 ≤ r ≤ L)
`` `

Necesitas exactamente 'q' flips para crear los separadores requeridos.
Sum `q` sobre todas las carreras → que es el número de operaciones necesarias para el candidato `L`.
Si ese número es factible, de lo contrario no lo es.

La única sutileza es cuando `L == 1`.
Con `L == 1` queremos una cuerda perfectamente alternada.
Para eso tenemos que comprobar ambos patrones (0101...` y `1010...') y elegir el que necesita menos volteretas.

Debido a que la prueba de viabilidad es monotona (si `L` es factible entonces cualquier `L' más grande también es factible), podemos buscar binariamente el mínimo factible `L`.

-...

### 3. Algoritmo (Pseudocode)

`` `
carreras = longitudes de chars iguales consecutivos en s
maxRun = elemento máximo de las carreras

costo de la función (L):
si L == 1:
volteretas StartWith0 = número de diferencias con el patrón 0101...
volteretas StartWith1 = número de desajustes con patrón 1010...
volver min(flipsStartWith0, flipsStartWith1)

total = 0
para cada r en carreras:
total += r // (L +1)
total

búsqueda binaria sobre L en [1, maxRun]
media = (bajo + alto) // 2
si cuesta (media) Ops:
respuesta = mitad
alta = media - 1
más:
baja = media + 1

respuesta
`` `

-...

### 4. Prueba de corrección

Demostramos que el algoritmo devuelve la longitud mínima de bloque más larga posible.

-...

#### Lemma 1
Para una carrera de longitud " R " L " , el número mínimo de volteretas necesarias para reducir cada bloque dentro de esa carrera a la longitud ≤ `L ' equivale a `R / (L+1)⌋`.

Proof.
Coloque un separador (flip un poco) cada caracteres 'L+1`.
Después de los separadores de `q = ⌊R/(L+1)⌋` la carrera se divide en bloques de 'q+1`, cada una de las longitudes en la mayoría de 'L' (el último bloque puede ser más corto).
Cualquier solución que utilice menos de " giros " dejaría un bloque más largo que " L " , contradiciendo la viabilidad. ∎



#### Lemma 2
Para un `L' fijo, el número total de volteretas computadas por `cost(L)` es el número *minimal* de volteretas requeridas para obtener una cadena cuya longitud de bloque más larga es ≤ `L`.

Proof.
"cost(L) " es la suma de los valores de Lemma contaminanbsp;1 sobre todos se ejecuta más tiempo que " L " .
Todas las carreras más cortas o iguales a `L` ya están bien y no necesitan volteretas.
Los bits de deslizamiento en distintas carreras son independientes, por lo que la suma de los costes óptimos por ejecución es óptima en general. ∎



#### Lemma 3
Si `cost(L) ≤ numOps` entonces existe una secuencia de ≤ 'numOps' flips que alcanza la longitud de bloque más larga ≤ `L`.

Proof.
`cost(L)` da una manera constructiva de voltear bits en cada largo plazo como se describe en Lemma adultnbsp;1.
Aplicar estas volteretas produce una cadena con la longitud de bloque más larga ≤ `L`.
Dado que el número total de vueltas equivale a "cost(L) " y "cost(L) ≤ numOps " , el requisito queda satisfecho. ∎



#### Lemma 4
Si `cost(L) > numOps` entonces es imposible obtener una cadena con la longitud más larga del bloque ≤ `L ` utilizando sólo las vueltas `numOps`.

Proof.
Por Lemma adultnbsp;2, cualquier solución factible debe realizar al menos las volteretas "cost(L).
Si `cost(L)` excede el presupuesto, no existe ninguna solución viable. ∎



##### Theorem
El algoritmo de búsqueda binaria produce la longitud mínima de bloque más larga alcanzable.

Proof.
Definir el predicado `P(L): costo(L) ≤ numOps`.
Por Lemma adultnbsp;3, `P(L)` es cierto sif `L` es alcanzable.
Por Lemma plaganbsp;4, si `P(L)` es falso, no mayor `L` puede ser falso? En realidad monotónica: si `L` no es alcanzable, cualquier `L' más pequeño tampoco puede ser alcanzable. El conjunto de viabilidad está cerrado.
Por lo tanto, " P(L) " es la monotona que disminuye con respecto a " L " .
La búsqueda binaria en un monotone predicate siempre encuentra el más pequeño `L' con `P(L)` verdadero.
El algoritmo devuelve que `L`. ∎



-...

### 5. Análisis de la complejidad

TEN TERRITORIO TERRITORIO ANTERIOR
Silencio...
Silencio Construye corres (`O(n)`) Silencio
TENIDO `cost(L)` para un candidato TENIDO `O(m)` donde `m ≤ n` es número de carreras → `O(n)` (los resultados se procesan una vez). Silencio
Silencioso búsqueda binaria Silencioso `O(log maxRun)` iterations, `maxRun ≤ n`. Silencio
tención **Total** Silencioso `O(n log n)` tiempo, `O(1)` memoria adicional. Silencio

-...

### 5. Implementaciones de referencia

A continuación se presentan soluciones limpias y de producción en los tres idiomas solicitados.

-...

#### 5.1 Java (LeetCode-compatible)

``java
importar java.util*;

Clase Solución {
public int minLength(String s, int numOps) {
int n = s.length();
si (n ==1) retorno 1; // sólo un bloque puede existir

// Construir longitudes de ejecución
Lista de datos:Integer confianza runList = nuevo ArrayList fiel();
int count = 1;
para (int i = 1; i) {}
si (s.charAt(i) == s.charAt(i - 1)) {
contar++;
. ♫ ... {
runList.add(count);
= 1;
}
}
runList.add(count);

int maxRun = 0;
para (int r : runList) maxRun = Math.max(maxRun, r);

// Prueba de viabilidad para un candidato L
java.util.function.IntUnaryOperator cost = L - título {}
(L == 1) {
int mism0 = 0; // patrón 0101...
int mism1 = 0; // patrón 1010...
para (int i = 0; i)
carbon expected0 = (i % 2 == 0) ? '0' : '1';
carbon expected1 = (i % 2 == 0) ? '1' : '0';
(s.charAt(i) != expected0) mism0++;
(s.charAt(i) != expected1) mism1++;
}
devolver Math.min(mism0, mism1);
. ♫ ... {
int flips = 0;
para (int r : runList) {
flips += r / (L + 1);
}
volteretas de retorno;
}
};

// Búsqueda binaria
int bajo = 1, alto = maxRun, ans = maxRun;
mientras (bajo) = alto) {
int mid = (low + high) 1;
si (cost.applyAsInt(mid)
ans = medio;
alta = media - 1;
. ♫ ... {
baja = media + 1;
}
}
devolver los ans;
}
}
`` `

-...

#### 5.2 Python (3.10+)

``python
de la importación Lista

Solución de clase:
def minLength(self, s: str, numOps: int) int:
n = len(s)
si n == 1:
Regreso 1

# Build run lengths
ands: List[int] = []
cnt = 1
para i en rango(1, n):
si s[i] == s[i - 1]:
cnt += 1
más:
run.append(cnt)
cnt = 1
run.append(cnt)

max_run = max(runs)

def cost(L: int) - título int:
si L == 1:
# discordancias con dos posibles patrones alternantes
mism0 = mism1 = 0
para i, ch in enumerate(s):
esperado0 = '0' si i % 2 == 0 otra '1'
esperado1 = '1' si i % 2 == 0 más '0'
si ch!= espera0:
mism0 += 1
si ch!= esperado1:
mism1 += 1
retorno min(mism0, mism1)
flips = 0
para r en carreras:
flips += r // (L + 1)
volteretas de retorno

# Búsqueda binaria
lo, hola = 1, max_run
ans = max_run
mientras que lo
media = (lo + hola) // 2
si cuesta (media) Ops:
ans = mitad
hola = media - 1
más:
lo = mitad + 1
Retorno
`` `

-...

#### 5.3 C++ (GNU C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minLength(string s, int numOps) {}
int n = (int)s.size();
(n == 1) retorno 1;

// Construir longitudes de ejecución
vector corres;
int cnt = 1;
para (int i = 1; i) {}
si (s[i] == s[i - 1]) cnt++;
otra vez
run.push_back(cnt);
cnt = 1;
}
}
run.push_back(cnt);

int maxRun = *max_element(runs.begin(), runs.end());

auto cost = [ cl](int L)- título{
(L == 1) {
int mism0 = 0, mism1 = 0;
para (int i = 0; i) {}
char expect0 = i % 2 == 0) ? '0' : '1';
char expect1 = i % 2 == 0) ? '1' : '0';
(s[i] != expect0) mism0++;
(s[i] != expect1) mism1++;
}
retorno min(mism0, mism1);
. ♫ ... {
int flips = 0;
para (int r : carreras)
flips += r / (L + 1);
volteretas de retorno;
}
};

int bajo = 1, alto = maxRun, ans = maxRun;
mientras (bajo) = alto) {
int mid = low + (high - low) / 2;
si (costo(medio)
ans = medio;
alta = media - 1;
. ♫ ... {
baja = media + 1;
}
}
devolver los ans;
}
};
`` `

-...

### 5.4 Casos de borde accionados

Silencio Caso confidencialidad ¿Por qué importa?
Silencio...
Silencio 1` Silencio La única longitud de bloque es 1 TEN Vuelta 1 inmediatamente ANTE
Silencio 0` Silencio No se permiten flips → respuesta es la carrera más larga actual Silencio La búsqueda binaria seguirá funcionando, pero podemos saltar costosos cheques Silencio
TENIDA `L == 1` Silencio Patrón de alternancia no puede ser manejado por la fórmula de ejecución genérica ANTERIENTE Cambiadores de computación para ambos patrones (`0101...` ' 1010...`) Silencio

-...

## 6. Artículo del Blog
*(SEO-optimized copy‐paste ready for Medium, Dev.to, or a personal blog)*

■ *Título*
■ “De las cuerdas binarias a las entrevistas de trabajo – Mastering LeetCode 3398 con búsqueda binaria”

-...

### 6.1 Introduction

■ *“Hard”* es una etiqueta LeetCode que significa que no sólo estás practicando; estás * mostrando* tu pensamiento algoritmo.
Problema de usuario 3398 – * Subestring más importante con caracteres idénticos I* – prueba exactamente que: debe encontrar un bloque mínimo largo después de volteretas limitadas.
■ En este post caminaré por la intuición, la solución formal, por qué funciona, y cómo se puede explicar en una entrevista.
■ Si estás cazando un rol de ingeniería de software, este es el tipo de pregunta que verás en rondas de codificación, y dominarlo te da material digno de presunción para tu curriculum vitae.

-...

### 6.2 What Makes Este problema “Hard”

Silencio Por qué Duro Lo que significa para ti
Silencio...
Silencio **Monotone Feasibility + Binary Search** Silencio Aprenderás a “búsqueda binaria en la respuesta” – un patrón que aparece en muchas preguntas de entrevista. Silencio
Silencio **Edge Case L = 1** Silencio Los pequeños off-by‐ones pueden romper su lógica. Tendrás que pensar en ambos patrones alternos. Silencio
Silencio **Large Constraints** Silencio `n` puede ser 2 × 105. Una solución ingenua O(n2) o O(n × numOps) TLE. Silencio

-...

### 6.3 El “bueno” – La idea central

*Break every long run into blocks of length ≤ L by flipping a separator every L+1 positions. *
¿Por qué funciona esto?
Debido a que girar la parte más bella posible dentro de un largo plazo siempre le da el máximo beneficio para las más pequeñas vueltas.
La matemática funciona a las volteretas " ⌊R/(L+1) " , simples, rápidas y óptimas.

*Por qué es genial para tu currículum*

* Usted puede explicar una solución * basada en funcionamiento* en 30 segundos.
* Muestra la mentalidad *optimización*: se reduce un problema complejo a un puñado de operaciones aritméticas.
* Usted mostrará que usted puede manejar ** casos de borde no-trivial** (L = 1).

-...

### 6.4 La “Nice” – Búsqueda binaria sobre la viabilidad

No se pueden comprobar todos los posibles valores de 'L' uno por uno (hay hasta n).
En cambio, observas que si una cierta `L` es factible (puedes hacer todos los bloques ≤ L), entonces cualquier *grande* `L` también es factible, pero cualquier *smaller* `L` puede no ser.
Esta propiedad *monotone* le permite la investigación binaria `L` en `O(log n)` pasos.

**Explicación interesante* *

■ “Yo primero determinaré si es posible un `L` dado contando las volteretas requeridas; entonces realizo una búsqueda binaria sobre `L`.
■ Cada prueba de viabilidad es lineal en el número de carreras, por lo que la complejidad general es `O(n log n)` – lo suficientemente rápida para las limitaciones. ”

-...

### 6.5 The "Bad" – What could Go Wrong

1. **Mis-counting runs** – por ejemplo, olvidando empujar la última carrera.
2. **Usando la fórmula genérica para L = 1** – esto falla porque un patrón alternativo no tiene “separador” dentro de la cadena.
3. **Los límites incorrectos más bajos/upper en búsqueda binaria** – por ejemplo, utilizando `maxRun` como límite superior pero no manejando el caso donde `maxRun` es 1.

*Cómo cuidarte*

* Test with small strings (`n = 1`, `n = 2`, `numOps = 0`).
* Verificar la función de coste para un conocido `L` (por ejemplo, L = corriente max run → flips = 0).
* Camine a través de un ejemplo dibujado a mano en la entrevista; muestre que está pensando en *mismatch* cuenta para ambos patrones cuando L = 1.

-...

### 6.6 The “Bad” – Potential Interview Pitfalls

Silencio Pitfall Silencio
Silencio...
Silencio “Escribí una solución que pasa la muestra pero no las pruebas ocultas” Silencio Añadir **salidas cercanas** para casos triviales (`n = 1`, `numOps = 0`). Silencio
ANTE “Usé recursión y rebosé de pila” TEN Prefer iterative loops; en C++ evitar la recursión profunda porque el tamaño de la pila puede ser limitado en la plataforma. Silencio
Silencio “El entrevistador quiere ver la complejidad del tiempo” Silencio Estar listo para decir *O(n log n)* y explicar por qué cada parte es lineal. Silencio

-...

### 6.7 El “Nice” – Qué decirle al entrevistador

1. **Declara el problema en tus propias palabras** – “Estamos permitidos hasta las volteretas de la mordida “numOps”; queremos minimizar la longitud del bloque contiguo más largo. ”
2. **Explicar el modelo basado en la carrera** – “Podemos comprimir la cadena en longitudes de ejecución; cada carrera de longitud `R` necesitará volteretas `R/(L+1)⌋` para hacer todos los bloques ≤ L.”
3. **Mostrar la prueba de viabilidad** – “Given `L`, podemos calcular volteretas totales en tiempo lineal. ”
4. **Describir la búsqueda binaria** – “Nos binaria-búsqueda `L' de 1 a la carrera máxima actual”.
5. **Mención del caso del borde** – “Cuando L = 1, tenemos que considerar ambos patrones alternos; simplemente contamos con desajustes contra 0101... y 1010.... ”

Prepárate para escribir código en la pizarra: el esqueleto es corto; la parte difícil es manejar `L=1`.

-...

### 6.8 How This Knowledge Translate to Real‐World Coding

* **Procesamiento de lotes** – dividir una cadena en carreras es análogo al procesamiento de troncos en pedazos.
* **Greedy Selections** – Escoger el separador más temprano es una estrategia avaricia que a menudo aparece en problemas de programación.
* ** Patrones Algorítmicos** – La investigación binaria sobre la respuesta aparece en preguntas “minimo/maximo” a través de dominios (por ejemplo, “mínimo energía inicial” para problemas de trayectoria).

Si usted puede explicar cómodamente estos patrones, usted está señalando a los entrevistadores que usted puede *recognize* una clase de problemas y *apply* una técnica probada.

-...

### 6.9 Final Takeaway

LeetCode 3398 no es sólo una pregunta; es un momento de micro-teaching.
*Bien* para su currículum: una buena codicción basada en la carrera, una aplicación limpia `O(n log n)`, y una prueba sólida de corrección.
*Nice* para la preparación de entrevistas: práctica explicando *búsqueda binaria en la respuesta* y manejando casos de borde sutil.

**Siguientes pasos**
1. Envíe esta solución a su repositorio GitHub (incluya las tres variantes del lenguaje).
2. Agregue un blog con los fragmentos de código y algunos ejemplos de carreras.
3. En tu curriculum vitae, nota *“Solved LeetCode 3398 – optimización de cadenas binarias mediante descomposición de ejecución y búsqueda binaria en la respuesta.”*

Acabas de convertir un rompecabezas algorítmico en oro entrevistado. 🚀

-...

### 6.10 Cierre

¡Si disfrutas de esta profunda inmersión en LeetCode 3398, házmelo saber!
Deja un comentario o un DM en LinkedIn, y compartiré más preguntas de entrevista que se basan en los mismos conceptos.

Feliz codificación, y que sus rondas de entrevistas sean tan ajustadas como el bloque más largo mínimo que acaba de optimizar!

-...


**End of Blog Post**

*(Sin ánimo de retocar las partidas o añadir sus propias anécdotas personales. La estructura está lista para publicar y contiene todos los puntos clave que un entrevistador apreciará.) * *


-...


### 7. Observaciones finales

Hemos cubierto:

* Prueba formal algorítmica de que el avaricioso es óptimo.
* Una aplicación de referencia exhaustiva en Java, Python y C++.
* Un artículo de blog de estilo entrevistado listo para publicar que vincula la solución al crecimiento de la carrera.

Ahora estás totalmente equipado para hacer esta pregunta, escribir código limpio, y explicar el razonamiento en una entrevista de trabajo. ¡Buena suerte!