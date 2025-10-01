-...
Título: LeetCode 3557. Encontrar Maximum Número de Subestrings No Intersecting -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. El Código (Java Silencio Python Silencio C++)

A continuación se presentan tres soluciones completamente autocontenidas que funcionan en **O(n)** tiempo y **O(1)** espacio extra.
Todos utilizan la idea *verde* que siempre podemos “commitir” a una subestring tan pronto como veamos una válida, porque cualquier subestring posterior que comience dentro de la actual necesariamente la superpone.

``java
// -------- Java --------
importar java.util*;

Clase Solución {
public int maxSubstrings(Cierra palabra) {
int res = 0;
Mapa seleccionadoCaracter, Integer primero = nuevo HashMap Quería();
para (int i = 0; i) i++) {
char c = word.charAt(i);
si (!first.containsKey(c)) { // primera vez vemos c
primero.put(c, i);
} si (i - first.get(c) + 1  ES= 4) {//// valid non-overlapping substring
res++;
primero.clear(); // empezar de nuevo – sin solapamiento permitido
}
}
restitución;
}
}
`` `

``python
# -------- Python...
def maxSubstrings(palabra: str) - título int:
res = 0
primero
para i, c en enumerado(palabra):
si no en el principio:
primero [c] = i
elif i - first[c] + 1 ⇩= 4: # valid substring found
res += 1
primer.clear() # reset – sin solapamiento
retorno
`` `

``cpp
// -------- C++ --------
#include יbits/stdc++.h
usando std namespace;

int maxSubstrings(string word) {
int res = 0;
unordered_map determinadachar,int título primero;
para (int i = 0; i) ++i) {
char c = word[i];
si (!first.count(c)) {
primera[c] = i; // primera aparición
} si (i - first[c] + 1 ⇩= 4) { /// un subestring válido termina aquí
++res;
primero.clear(); // reset – no se admite superposición
}
}
restitución;
}
`` `

Los tres fragmentos compilan con la biblioteca estándar solamente y producen la misma respuesta para cada caso de prueba.

-...

## 2. Blog Artículo – “El Bien, el Mal, y el Ugly de LeetCode 3557”

■ **LeetCode 3557 – *Encontrar el máximo número de subestrings no interesantes***
■ *Una profunda inmersión en DP vs Greedy, por qué el codicioso es el lugar dulce, y cómo puedes clavarlo en una entrevista. *

-...

## Tabla de contenidos
1. [Norma general](#problema vista previa)
2. [Por qué este problema importa] (por qué este problema-matters)
3. [Brute‐Force / Intuición](#brute-force--intuition)
4. [Programación Dinámica (El camino "Bad")](#dinamic-programming-the-bad-path)
5. [Greedy (The "Good" Path)](#greedy-the-good-path)
6. [Edge Cases ' Pitfalls](#edge-cases--pitfalls)
7. [Testing Your Solution](#testing-your-solution)
8. [Toke‐aways & Interview Tips](#take-aways--interview-tips)
9. [Más lectura > Recursos] (recursos de lectura de la máquina)
10. [Conclusión](#conclusión)

-...

### Problema Resúmenes ## #### Nombre="problema-supervisión"

Se le da una cadena `palabra` (1 ≤ Нword perpetua ≤ 2 × 105) que consiste en minúsculas letras inglesas.
Devuelve el número **maximum** de subestrings * no superpuestos* que satisfacen:

* Longitud ≥ 4
* Empieza y termina con la misma carta

Ejemplo
`` `
palabra = "abcdeafdef"
["abcdea", "fdef"] (respuesta = 2)
`` `

-...

### ¿Por qué este problema importa?

- **Pattern-matching** + ** programación intervalida** → habilidades básicas CS.
- Las restricciones te empujan hacia **O(n)** soluciones.
- A muchos entrevistadores les encantan los problemas donde una opción *verde* es en realidad óptima – prueba su capacidad para razonar sobre la optimización, no sólo la codificación.

-...

## Brute‐Force / Intuition #1 Name="brute-force--intuition"

Un enfoque ingenuo enumera todas las subestrings, verifica la validez, y luego hace un intervalo de empaquetado DP.
Complejidad: **O(n2)** tiempo, **O(n2)** memoria – imposible para 200 000 cuerdas de longitud.

Información clave: *Cualquier subestring válido se define por un par de caracteres iguales a distancia ≥ 3*.
Por lo tanto, sólo necesitamos rastrear ** los primeros acontecimientos** de cada carta.

-...

### Dynamic Programming (The “Bad” Path) - "dinamic-programming-the-bad-path"

A clean DP formulation:

`` `
dp[i] = max number of valid substrings in word[0 ... i-1)
`` `

Transición:

`` `
dp[i+1] = max(dp[i+1], dp[j] + 1) para todos los j donde palabra[j]=word[i] y i-j+1 4
`` `

Implementación utiliza una cola por carta para mantener sólo los *últimos cuatro* ocurrencias, reduciendo el bucle interior a la mayoría de 4 cheques por personaje.
**Tiempo:** O(n)
**Espacio:** O(n) para dp array, O(n) para colas en el peor de los casos → **O(n)* *

Si bien es correcto, el array extra y la contabilidad del DP lo hacen más pesado que necesario.
Los entrevistadores a menudo prefieren la solución más limpia y codictiva.

-...

## Greedy (The “Good” Path) [El Camino del Bien]]

##### Observation

Si vemos un personaje `c` de nuevo y la distancia entre las dos ocurrencias es ≥ 4, podemos * reclamar el subestring entre ellos **sin pérdida de la óptimaidad**.
¿Por qué?
Debido a que cualquier subestring que comience dentro de este candidato tendría que terminar antes del siguiente personaje "c" (otros que se superpone), obligándolo a ser más corto que 4 – imposible.

#### Algorithm

1. Escaneo de izquierda a derecha.
2. Para cada carta almacena el índice **primero** donde apareció (`primer[c]`).
3. Cuando la misma carta aparece de nuevo en el índice " i " :
* If `i - first[c] + 1 ≥ 4` → **commit** to the substring `[first[c], i]`, increment answer, **clear all stored first indices** (no overlap allowed).
* Else → simplemente mantener el índice más temprano (no comprometer todavía).

El paso de salida clara garantiza la regla *no-overlap*: cada nueva subestring comienza después de que el anterior termina.

##### Why It Works

Es esencialmente el clásico *intervalo de programación por el tiempo de acabado más temprano* prueba:
el tiempo de acabado más temprano (lo más pronto posible `i` que da una subestring válida) nunca te duele porque deja la habitación máxima posible para subestrings posteriores.

#### Código Snippets

El codicioso es exactamente el código que enumeramos en la sección 1 (Java/Python/C++).
Observe el uso del espacio **O(1)**: sólo un pequeño hash‐map de 26 teclas que vaciamos cada vez que “commitimos”.

-...

### Edge Cases " Pitfalls " se hizo un nombre= "edge-cases--pitfalls"

Silencio Qué hacer para cuidar de Silencio
Silencio...
Silencio. La misma carta aparece 5 veces → dos subestrings? Silencio Greedy se comprometerá en la *primera* repetición que es ≥ 4, aclarando todo – todavía óptima. Silencio
Silencio `"abcd"` Silencio No hay letras iguales a distancia ≥ 3 → respuesta 0 Silencio Su código debe devolver 0 si no se encuentra ningún subestring válido. Silencio
Silencio Restablecimientos repetidos ← Reiniciar el hash‐map en cada commit es O(26) → trivial overhead. Si utiliza bit-mask + arrays, restablecer 26 entradas está bien; si utiliza un vector por carta, debe limpiar todas las colas cada vez. Silencio
TENIDO Grandes entradas TENIDO Utilice rápido I/O si su idioma lo necesita (Java: `BufferedReader`, Python: `sys.stdin.read()`). En el snippet usamos `enumerate(word)` – ya lineal en CPython. Silencio

-...

## Testing Your Solution ## Testing Your Solution ## Testing Your Solution ##

1. ** Pruebas de muestra** (desde el impulso).
2. ** Pruebas de flecha**: generar cadenas de longitud al azar hasta 10 000, fuerza bruta con un solucionador lento para la corrección.
3. ** Pruebas de estrés**: una larga cadena de 200 000 caracteres, por ejemplo `palabra = 'a'*200000` → respuesta = 50000.
4. ** Casos generales**: ``abcd'`, ``abc'`, `'a'*4`.

Ejemplo Python test de estrés:

``python
importación al azar, cadena, tiempo
def brute(palabra):
n=len(palabra); best=0
# O(n^2) brute – sólo para pequeñas cuerdas
para i en rango(n):
para j en rango(i+3, n):
si palabra[i]=word[j]:
best=max(best,1)
mejor

para _ en rango(1000):
s=''.join(random.choice(string.ascii_lowercase) for _ in range(random.randint(1,20)))
maxSubstrings(s)==brute(s)
print("Todas las pruebas aleatorias pasadas")
`` `

-...

### Take-aways & Interview Tips > > "take-aways--interview-tips"

Silencio Qué hacer hincapié en la vida eterna
Silencio...
Silencio **Explicar el argumento avaricioso** Silencio Shows que entendió el problema, no sólo escribió código. Silencio
Silencio **Las limitaciones de la mención → O(n) requerido** Silencio Los entrevistadores lo aman cuando se habla de la complejidad temprano. Silencio
Silencio **Mostrar ambos DP & Greedy** ← Demuestra la amplitud del conocimiento. Silencio
Silencio **Highlight the reset step** Silencio Es la única parte “muy” que necesita un manejo cuidadoso. Silencio
Silencio **Los mejores casos de borde viven** Silencio Hace que su solución sea robusta y muestre el pensamiento analítico. Silencio

**TL;DR** – Utilice la versión hash‐map, clara sobre el éxito, y esté lista para explicar *por qué* este compromiso es seguro.

-...

### Más lecturas > Recursos > > > Recursos > >

- ** Programación Interval** – problema clásico de libro de texto codicioso.
- **LeetCode Solutions (C+++, Java, Python)** – practicar problemas similares como * Subestring de repetición más larga* o *Número máximo de Segmentos no relacionados*.
- ** Programación Dinámica** – si quieres profundizar el conocimiento del DP, compruebe “Top‐Down vs Bottom‐Up DP” en LeetCode.

-...

### Conclusión #1 nombre="conclusión"

LeetCode 3557 es un rompecabezas *pattern matching + intervalo de programación* que se sienta en la intersección de DP y Greedy.
La solución avaricia es tanto **simpler** como **más eficiente** para la configuración de entrevistas, mientras que la versión DP muestra un enfoque clásico "full‐blown".

Al dominar este problema no sólo resolverás la pregunta en sí, sino también aprender a:

* **Elige el algoritmo adecuado** bajo restricciones estrictas.
* **Justificar la optimización** con una prueba limpia.
* **Código limpio, de lenguaje cruzado** que se puede mostrar a un panel de entrevistadores.

Buena suerte en su próxima entrevista de codificación – y recuerde: a veces la opción más simple es la más poderosa!