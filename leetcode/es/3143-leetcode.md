-...
Título: LeetCode 3143. Puntos máximos dentro de la plaza -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📌 1. Resumen del problema: “Puntos máximos dentro de la plaza”

Silencio LeetCode ID Silencio Dificultad Silencio
Silencio--------------------------...
Silencio **3143** Silencio Medio Silencioso Array, Greedy, Sorting, HashMap

# Objetivo #
Se les da `puntos [i] = [x, y]` (coordenadas distintas) y una cadena `s` donde `s[i]` es la etiqueta del punto `i`.
Una cuadra **válida** es:

* centrado en el origen `(0, 0)`
* bordes paralelos a los ejes
* **No hay dos puntos dentro de la plaza compartir la misma etiqueta* *

Devuelve el número máximo de puntos que pueden ser cubiertos por cualquier cuadrado válido.

La longitud lateral de la plaza puede ser cero.

-...

## 🎯 2. Why the Greedy “min‐vs‐second‐min” Trick Works

Silencioso de observación
Silencio...
Silencio La plaza está definida por la *máximo* coordenadas absolutas entre los puntos incluidos (por favor `R = máx(aprendida,  sometiday eterna)`. Silencio La longitud de la mitad del lado de la plaza debe ser por lo menos `R`; todo dentro de satisfies `aprevia intimidad≤R` y `apreviamente a la vida eterna≤R`. Silencio
Silencio Si una etiqueta ocurre dos veces con distancias `d1 ≤ d2`, nunca podemos incluir ambos puntos en la misma plaza porque la plaza debe ser lo suficientemente grande para el punto más lejano (`d2`). Silencio Por lo tanto, la distancia *segundo menor* para cada etiqueta determina el primer “conflicto” que invalidaría un cuadrado. Silencio
Silencio Para todas las etiquetas donde la distancia *smallest* es estrictamente más pequeña que la distancia *segundo más pequeña*, podemos incluir con seguridad el punto con la distancia más pequeña en nuestra plaza final. El radio de la plaza se puede configurar a la mayor distancia mínima – todos los puntos elegidos encajan, y ninguna etiqueta se duplica. Silencio

Así la respuesta es el número de etiquetas para las cuales
`minDistance[tag] > segundoMinDistance[tag]`.

El algoritmo es **O(n)** tiempo y **O(m)** espacio (`m` = número de etiquetas distintas).

-...

## 🧠 3. Algoritmo (Pseudo)

`` `
minDist = mapa vacío (tag → primera distancia más pequeña)
segundoMin = + mujeres
Conteo = 0

para cada punto (x, y) con la etiqueta t:
d = máx(Principalidad, Silencioso) // distancia de origen al punto
si no en minDist:
minDist[t] = d
si no, si no.
secondMin = min(secondMin, minDist[t])
minDist[t] = d
más:
secondMin = min (secondMin, d)

para cada etiqueta en minDist:
si minDist[tag]
Cuenta += 1

cuenta de retorno
`` `

-...

## 📄 4. Code

A continuación se presentan soluciones limpias y idiomáticas para **Java**, **Python**, y **C+**.

-...

### 4.1 Java (Java 17)

``java
importa java.util. HashMap;
importa java.util. Mapa;

Solución de la clase pública {}
int public maxPointsInsideSquare(int[] puntos, String s) {
Mapa seleccionadoCaracter, Integer confianza minDist = nuevo HashMap correspond();
segundo Min = Integer. MAX_VALUE;
int count = 0;

para (int i = 0; i) i++) {
int d = Math.max(Math.abs(points[i][0]), Math.abs(points[i][1]));
char tag = s.charAt(i);

si (!minDist.containsKey(tag)) {}
minDist.put(tag, d);
} si (d Identificar minDist.get(tag) {}
secondMin = Math.min(secondMin, minDist.get(tag));
minDist.put(tag, d);
. ♫ ... {
secondMin = Math.min (secondMin, d);
}
}

para (int d : minDist.values()) {}
si
contar++;
}
}
recuento de retorno;
}

public static void main(String[] args) {
int[][] pts = {2, 2}, {-1, -2};
Etiquetas de cuerda = "ab";
System.out.println(new Solution().maxPointsInsideSquare(pts, tags)); // 2
}
}
`` `

-...

### 4.2 Python (Python 3.10+)

``python
de la importación Lista, Dict

Solución de clase:
def maxPointsInsideSquare(self, points: List[List[int], s: str) - Conf int:
min_dist: Dict[str, int] = {}
segundo_min = flotador('inf')

para (x, y), etiqueta en zip(puntos, s):
d = max(abs(x), abs(y))
si la etiqueta no es min_dist:
min_dist[tag] = d
[tag]:
second_min = min(second_min, min_dist[tag])
min_dist[tag] = d
más:
second_min = min(second_min, d)

devolver la suma(1 para d en min_dist.values() si d
`` `

-...

### 4.3 C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxPointsInsideSquare(vector identificadovector fieltro pluripuntos, cadena s) {}
unordered_map determinadachar, int confianza minDist;
segundo Min = INT_MAX;
int count = 0;

para (size_t i = 0; i) ++i) {
int d = max(abs(points[i][0]), abs(points[i][1]));
char tag = s[i];

si (!minDist.count(tag)) {
minDist[tag] = d;
} si (d) minDist[tag] {}
secondMin = min(secondMin, minDist[tag]);
minDist[tag] = d;
. ♫ ... {
secondMin = min (secondMin, d);
}
}

para (auto &kv : minDist) {
si (kv.second < secondMin) ++cuenta;
}
recuento de retorno;
}
};
`` `

Las tres soluciones funcionan en **tiempo lineal** y usan un solo hash‐map para las etiquetas.

-...

## 🔍 5. Edge‐ Lista de verificación de casos

Silencio Caso Edge Silencio esperada Comportamiento
Silencio...
Silencio No hay puntos (`puntos.length == 0`) Silencio Regresar `0`. Silencio
Silencio Todas las etiquetas únicas  `secondMin` se mantiene ``; respuesta = número de etiquetas (`puntos.length`). Silencio
Silencio Todos los puntos tienen el *same* tag tención Sólo se puede tomar el punto más cercano; respuesta `1`. Silencio
Silencio Puntos con distancia `0` Silencio Están perfectamente dentro de un cuadrado de tamaño cero; manejado de la misma manera. Silencio

-...

♪ ♪ ♪ , 6. Pitfalls comunes (“El mal” el ugly”)

1. **Misinterpretando la longitud lateral**
*Muchos candidatos tratan la longitud lateral como el lado *full* más que el lado medio (`R`). *
**Fix:** Trabajar con `R = max(sobrevivirx, tención eterna)`; el lado cuadrado real es `2R`.

2. **Stopping at the first duplicate**
*Un simple “ surtido por R y romper duplicado” da respuestas erróneas cuando un duplicado temprano bloquea dos etiquetas únicas posteriores. *
**Fix:** Utilice el truco de min/segundo min descrito anteriormente.

3. **Overflow on distance**
*Si las coordenadas pueden ser `±10^9`, `max(abs(x),abs(y) ' se ajusta en `int`. Evite `long` a menos que sepa que el rango se extiende más allá de `2^31‐1`. *
**Fix:** Use `int` si las limitaciones son `sobrevivirx, viviry eternamente ≤ 10^9`. De lo contrario, cambiar a 'long'.

4. **Tag como cuerda en lugar de char* *
*`s[i]` es un personaje único, no una subestring. *
**Fix:** Use `s.charAt(i)` (Java) / `s[i]` (Python) / `s[i]` (C++).

-...

Test‐Driven Verification

``text
Entrada:
puntos = [2,2], [-1,-2]
s = "ab"
Producto: 2
`` `

``text
Entrada:
puntos = [-1,-2], [3,0], [0,3]]
s = "aaaB"
Producto: 1 // sólo se puede tomar la más cercana 'a'
`` `

``text
Entrada:
puntos = [0,0],[1,1],[2,2]]
s = "abc"
Salida: 3 // todas las etiquetas únicas, lado cuadrado 4 se ajusta a todos
`` `

Ejecute el código en cualquier idioma y verifique las salidas.

-...

## 📚 8. The Good, The Bad, " The Ugly of Interview Solutions

Silencio Silencio
Silencio------------Prince------
Silencio **Complejidad** Silencioso O(n) codicioso, fácil de probar  durable O(n log n) clasificación o búsqueda binaria – más pesado en la explicación Silencio O(n2) fuerza bruta, aceptado sólo en los datos de juguete
Silencio **Readability** Silencio Paso único, claros nombres de variables ← Loops anidados, confusos mapas temporales ← Duro de leer, estructuras de datos mixtas
Silencio **Robustness** tención Handles Plazas de tamaño cero, coordenadas negativas tención Fails cuando las etiquetas duplicadas aparecen temprano pero puntos posteriores podrían ser elegidos latitud Obras solamente si las restricciones garantizan no duplicar etiquetas latitud

**Takeaway:**
Para una entrevista *software-engineering*, usted quiere la solución * más clara, rápida y fácil de explicar* – el **min‐vs‐second‐min** codicioso es exactamente eso.

-...

## 🚀 9. Interview‐Ready Tips

1. ** Explique primero la distancia métrica (`R`). #
“Debido a que la plaza está alineada con el eje y centrada en el origen, cualquier punto dentro debe satisfacer `resistentes habit≤R` y `resistentesidad eterna≤R`. Así que el cuadrado está completamente determinado por el máximo de estos dos valores absolutos. ”

2. **Mostrar la lógica del conflicto con un pequeño ejemplo** (el `a(1), a(2), b(3)` contra-ejemplo).
Esto demuestra que realmente entiendes por qué una etiqueta no puede aparecer dos veces.

3. **Mención de la naturaleza de dos pasos** (min → secondMin → contar) y dar la complejidad al frente.

4. *Bono adicional*
Si el entrevistador pide una longitud *actual* cuadrada, simplemente la salida `2 * maxMinDist` donde `maxMinDist` es el `minDist más grande que satisface la condición.

-...

## ⋅ 10. Resumen

* El problema reduce a elegir un punto por etiqueta de tal manera que se minimiza la distancia **maximum** entre los puntos elegidos.
* El truco "smallest vs segundo-smallest" codicioso da el tiempo lineal óptimo.
* Existen implementaciones limpias en Java, Python y C++ – todas idénticas en lógica.
* Prepárate para explicar la intuición y el manejo de los bordes – eso es lo que *interviewers* buscan.

Buena suerte en tu próxima entrevista de codificación – ¡tienes el algoritmo *golden*! 🍀

-...

**Keywords**: Leetcode, entrevista de codificación, puntos máximos dentro de la plaza, entrevista de Java, entrevista de Python, entrevista de C++, algoritmo codicioso, complejidad del tiempo, complejidad del espacio, trabajo de ingeniería de software, preparación de entrevistas.