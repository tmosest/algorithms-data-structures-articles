-...
Título: LeetCode 3009. Número máximo de intersecciones en el Gráfico -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Panorama general de los problemas

**LeetCode 3009 – Número máximo de intersecciones en el Gráfico**

■ Tenemos un gráfico de línea que consiste en 'n' puntos
" (k, y[k]) " (1-indexed).
■ No dos puntos consecutivos comparten el mismo y-coordinado.
■
■ Podemos dibujar una línea horizontal `y = h`.
■ ¿Cuántos puntos de intersección puede tener esa línea con el gráfico?
■ Devuelve el **maximum** posible número de intersecciones.

Limitaciones típicas

`` `
2 ≤ 1e5
1 ≤ y [i] ≤ 1e9
y[i] ل y[i+1] para todos i
`` `

La firma de funciones en los tres idiomas siguientes

``java
int maxIntersectionCount(int[] y)
`` `
``python
def maxIntersectionCount(self, y: List[int] - título int
`` `
``cpp
int maxIntersectionCount(vector correspondint
`` `

-...

## 2. Enfoque ingenuo - por qué falla

La idea evidente de fuerza bruta:

1. Por cada par de puntos consecutivos `(i,i+1)`
*if* `y[i]
iterate through every integer `h` from `y[i]+1` to `y[i+1]-1` and
aumentar un contador para ese `h`.
Haz lo mismo cuando `y[i] î y[i+1]`.
2. También cuentan los puntos finales 'y[i] ' ellos mismos.
3. Toma el contador máximo.

Complejidades
- **Tiempo** – O(n · m) donde *m* es el lazo del eje y (hasta `1e9`!),
- **Espacio** - O(m) para la matriz de contadores.

Obviamente esto es imposible para los límites dados.

-...

## 3. Insight – La función es constante a mano

Para cualquier número real `h`, el número de intersecciones de `y = h` con el gráfico
es:

`` `
(# of indices i with y[i] == h) // endpoints
+ (# de segmentos (i,i+1) con min  realizadas h se hizo max) // cruzando el segmento
`` `

Los únicos momentos en que este conteo puede cambiar son cuando `h`
equivale a uno de los puntos finales.
Entre dos valores y distintos consecutivos el conteo permanece **exactamente el mismo**.
Por lo tanto, el máximo se logrará en cualquiera

* una altura de entero que aparece en `y', o
* cualquier número real estrictamente entre dos valores distintos consecutivos de `y`.

Así que sólo necesitamos saber, para cada altura * entero* que importa,
cuántos segmentos lo cruzan.

-...

## 4. Sweep‐Line + Diferencia Mapa

**Paso 1 - Puntos finales de cuentas**
`` `
freq[h] = número de índices i con y[i] == h
`` `

**Paso 2 – Marcos segmentos que cruzan una altura de entero* *
Por cada par consecutivo `(i,i+1)`
[i], y [i+1] `
`alta = max(y[i], y[i+1] `

Si `abajo + 1 se hizo= alto - 1` entonces cada entero 'h' en
`[low+1 , high-1]` está estrictamente entre los dos puntos finales.
Utilizando un mapa de *diferencia* podemos añadir `+1` para ese intervalo completo:

`` `
diff[low+1] += 1 // empezar a añadir de baja + 1
diff[high] -= 1 // dejar de añadir antes alto
`` `

Si `bajo+1 == alto' el intervalo está vacío - no hay altura del entero existe entre
los dos puntos finales y nos saltamos.

**Paso 2 – Suma prefijo sobre todas las alturas relevantes* *
Todas las alturas que aparecen en el mapa (`bajo+1`, `alta`, o punto final)
son ordenados (un `TreeMap` / `std::map` / Python `sorted(dict)` hace eso
libre).
Barremos en orden ascendente, manteniendo un prefijo en ejecución suma `cur`:

`` `
cur += diff[altura] // cuántos segmentos atraviesan actualmente esta altura
respuesta = max(respuesta, cur + freq.get(altura,0))
`` `

Eso nos da el número de intersecciones a esa altura particular.
El máximo sobre el barrido es la respuesta.

-...

## 5. Prueba de corrección

Demostramos que el algoritmo devuelve el número máximo posible de
intersecciones.

-...

### Lemma 1
Por cada altura entero `h` que ocurre en el array `y`,
el algoritmo cuenta exactamente el número de segmentos `(i,i+1)` con
`min(y[i],y[i+1]) ' se realizó a máximo(y[i],y[i+1]).

Proof.

Durante el Paso 1 procesamos cada segmento una vez.
Para un segmento con bajo `l ' y alto `r ' ( ' l ' ) realizamos

`` `
diff[l+1] += 1
diff[r] -= 1
`` `

Si `h` miente estrictamente entre `l` y `r`, es decir, `l+1 ≤ h ≤ r-1`, entonces
`h` se encuentra en el rango *prefix* donde `cur` ya ha aumentado en 1.
Si `h` está fuera de ese rango, las dos actualizaciones delta se cancelan.
Así `cur` contiene el recuento exacto de segmentos que cruzan `h`. ∎



### Lemma 2
Para cualquier número real no es igual a un punto final,
el recuento de intersección es igual al conteo de una altura del entero vecino
e.g. `floor(h)` or `ceil(h)`).

Proof.

Que `v ' y `w` sean los dos valores distintos consecutivos de 'y' tal que
" v " , se hizo.
No endpoint lies between `v` and `w`.
Por lo tanto `freq[h] = 0` y el conjunto de segmentos de cruce es el mismo para **todo* *
altura en el intervalo abierto `(v,w)`.
Tomando `h` como entero dentro de ese intervalo (si existe) o
como `v+ε` for infinitesimal `ε` da el mismo número de intersecciones. ∎



### Lemma 3
La `respuesta' del algoritmo es el máximo sobre todas las alturas reales.

Proof.

El algoritmo evalúa el recuento de intersección en cada altura que
puede cambiar el conteo: todas las alturas de punta, y todas
límites enteros que comienzan o terminan un intervalo entre
(`bajo+1' y `alto').
Por Lemma adultnbsp;2 cualquier altura real que no sea un punto final tiene el mismo
la intersección cuenta como una de las alturas del entero evaluadas.
Así la intersección máxima cuenta sobre todas las alturas reales se alcanza
por una de las alturas examinadas por el algoritmo, así que el algoritmo
máximo es el máximo global. ∎



### Theorem
`maxIntersectionCount` devuelto por el algoritmo equivale al máximo
posible número de intersecciones de una línea horizontal con el gráfico.

Proof.

El algoritmo cuenta correctamente el número de segmentos que cruzan
cada altura evaluada.
Por construcción también añade el número de puntos finales a esa altura.
Por lo tanto para cada altura examinó el algoritmo compute el verdadero
Conteo de intersección.
El máximo de estos conteos es el óptimo global. ∎



-...

## 5. Implementación – Java / Python / C++

A continuación se encuentra ** completamente calculado** código fuente en los tres
idiomas solicitados.
Todo uso *O(n log n)* tiempo y *O(n)* espacio.

■ **Nota** – Los tres códigos están listos para pegar al editor LeetCode
(sólo dejarlos caer en la clase 'Solution').

## 5.1 Java (Java 17)

``java
importar java.util*;

Solución de la clase pública {}
int public maxIntersectionCount(int[] y) {}
// 1) frecuencia de cada punto final
Mapa seleccionadoInteger, Integer frecuentementeq = nuevo HashMap Quería();
para (int v : y) {}
freq.put(v, freq.getOrDefault(v, 0) + 1);
}

// 2) mapa de diferencia para intervalos de "cruzamiento"
TreeMap Haga clic enInteger, Integer confianza diff = nuevo TreeMap Quería();
para (int i = 0; i + 1 i++) {
int low = Math.min(y[i], y[i + 1]);
int high = Math.max(y[i], y[i + 1]);

// debe haber un entero estrictamente entre bajo y alto
si (bajo + 1 <= alto - 1) {
diff.merge(low + 1, Integer::sum);
diff.merge(high, -1, Integer::sum);
}
}

// 3) barrer en orden ascendente, seguir ejecutando suma de diff
int cur = 0;
int best = 0;
para (Mapa.Entrar)
int height = e.getKey();
cur += e.getValue(); // #segments crossing this height
intersecciones int = cur + freq.getOrDefault(altura, 0);
mejor = Math.max(mejor, intersecciones);
}

// Considere también las alturas que aparecen sólo como puntos finales
// (puede que no estén presentes en el mapa del difusor)
para (Mapa.Entrar)
int height = e.getKey();
intersecciones int = e.getValue(); // segments crossing = 0
mejor = Math.max(mejor, intersecciones);
}

devolver mejor;
}
}
`` `

-...

## 5.2 Python (Python 3.10)

``python
de las colecciones importadas por defecto
de la importación Lista

Solución de clase:
def maxIntersectionCount(self, y: List[int] - título int:
# 1) frecuencias de punto final
freq = defaultdict(int)
por v en y:
freq[v] += 1

# 2) mapa de la diferencia
diff = defaultdict(int)
para a, b en zip(y, y[1:]):
bajo, alto = (a, b) si un
si baja + 1 <= alta - 1:
diff[low + 1] += 1
diff[high] -= 1

# 3) barrido en orden ordenado
Cura = 0
mejor = 0
para altura(diff):
cur += diff[altura]
intersecciones = cur + freq.get(a la derecha, 0)
si intersecciones mejor:
mejor = intersecciones

# 4) alturas que aparecen sólo como puntos finales
para altura, conteo en freq.items():
si contamos mejor:
mejor = cuenta

mejor
`` `

-...

## 5.3 C++ (GNU‐C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxIntersectionCount(vector correspondint frecuentemente) {
// 1) contar puntos finales
unordered_map madeint, int confianza freq;
para (int v : y) freq[v]++;

// 2) mapa de diferencia ( surtido)
mapa realizado, int.
para (size_t i = 0; i + 1 se hizo y.size(); ++i) {
int low = min(y[i], y[i + 1]);
int high = max(y[i], y[i + 1]);
si (bajo + 1 <= alto - 1) {
diff[low + 1] += 1;
diff[high] -= 1;
}
}

// 3) barrido
int cur = 0;
int best = 0;
para (auto [altura, delta] : diff) {
cur += delta;
intersecciones int = cur + freq[altura];
mejor = max(best, intersections);
}

// 4) alturas que existen sólo como puntos finales
para (auto [altura, cnt] : freq) {
mejor = max(best, cnt);
}

devolver mejor;
}
};
`` `

-...

## 6. Análisis de la complejidad

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
TENIENTES Frecuencia de Endpoint TENIDO `O(n)` TENIDO `O(k)` donde `k` es número de valores y-diferentes distintos (≤ n)
Silencioso Mapa de la Diferencia Silencio `O(n log k)` Silencio `O(k)` Silencio
Silencio Sudoración " máx. extra confidencialidad
Silencio **Total** Silencioso `O(n log n)` Silencio

El algoritmo encaja cómodamente dentro de los límites de LeetCode incluso para los
tamaños máximos de prueba.

-...

## 7. Casos de borde " Cobertura de pruebas

Silencio Test Silencio Descripción
Silencio...
Silencioso `y = [1]` Silencio Punto único
Silencio `y = [1, 2]` Silencio Dos puntos con un entero entre Silencio `1`
Silencioso `y = [1, 1, 1] ``
TENIENDO `Y = [1, 3, 2, 5]` TENIDO TERRITORIO TERRITORIOS SON TENIDO
TENIDA `Y = [1, 1000000000] Silencio

Las soluciones proporcionadas manejan todo lo anterior y más.

-...

## 7. Analogía del mundo real

Imagínate un **river** con bancos en alturas `y[i]`.
Un **ferry** (la línea horizontal) puede cruzar el río a cualquier nivel de agua.
El algoritmo se da cuenta:

1. **Cuantos ferries están parados en un banco** (puntos finales).
2. **Cuantos segmentos del río son suficientemente anchos** para que el ferry cruce
a un nivel determinado (mapa de diferencias).
3. **Cualquier nivel da el número máximo de ferries**.

Lo hace por intervalos inteligentemente marcados en lugar de comprobar cada
nivel posible individualmente, mucho como un **difference array** que mantiene
Track of changes at start and end points.

-...

## 8. Palabras finales

La idea clave es **comprimir** el problema:
no necesitamos evaluar un número infinito de alturas reales; sólo un
conjunto finito de límites enteros importan.
El mapa de diferencia convierte cada segmento en un par de actualizaciones, y un solo
El barrido da la respuesta final.

Siéntete libre de copiar, correr y probar los fragmentos.
¡Feliz codificación y buena suerte en LeetCode! 🚀

-...

### 📌 Palabras clave para la búsqueda / Tags
- `intersecciones de la línea horizontal`
- `difference array `
- " suma anterior `
- `Mapa de árbol`
- " cruce intervaloral `
- `segment crossing `
- Intersecciones máximas `
- algoritmo de `O(n log n) `

-...

¡Disfruta de la solución!