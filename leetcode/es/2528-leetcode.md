-...
Título: LeetCode 2528. Maximizar la ciudad con potencia mínima -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. LeetCode 2528 – **Maximizar la ciudad con energía mínima**

La tarea es añadir `k` nuevas etapas de poder (todos teniendo el mismo rango 'r') a una línea de ciudades para que el *mínimo* poder de cualquier ciudad sea lo más grande posible.

Las limitaciones son grandes (`n` up to `105`, `k` up to `109`) – necesitamos un algoritmo que se ejecuta en `O(n log answer)` y utiliza sólo `O(n)` memoria adicional.



----------------------------------------------------

## 2. Resumen del algoritmo

Silencio Lo que hacemos _ Por qué funciona
...------------------------
tención **1. búsqueda binaria en la respuesta** Silencio Buscar el entero `mid` que podría ser el poder mínimo. ← Si podemos lograr un poder mínimo de `medio' con las estaciones más 'k' nuevas, cualquier valor más pequeño es también alcanzable; si no podemos, ningún valor más grande es posible. Silencio
TEN **2. Colocación saludable** ANTE Durante el escaneo de las ciudades izquierda a derecha, si la ciudad `i` está perdiendo el poder, coloque las estaciones desaparecidas lo más lejos posible (`pos = min(n-1, i+r)`). Silencio Colocar lo más lejos posible a la derecha da a la estación el mayor “alcance de combustible”, por lo que puede ayudar al mayor número posible de ciudades posteriores. Silencio
Silencio **3. Reservas de ventanilla sliding** Silencio Mantener una suma de funcionamiento `cur` de centrales eléctricas que actualmente cubren la ciudad `i` (existiendo + añadido). Use un array auxiliar `add[]` donde `add[x]` es el cambio neto en `cur` que comienza en la ciudad `x`. Cuando se coloca una nueva estación en `pos`, hacemos `add[pos] += need` y `add[pos+r+1] -= need` para que la estación deje de influenciar después de que su alcance termine. Esto nos da `O(1)` actualización por ciudad y mantiene la ventana corredera en tiempo lineal. Silencio

Por lo tanto, el procedimiento de verificación es lineal, y investigamos binariamente la respuesta.



----------------------------------------------------

## 3. Prueba de corrección

Demostramos que el algoritmo devuelve el máximo poder mínimo posible.

-...

### Lemma 1
Durante la comprobación de un objetivo fijo `mid`, la regla avaricia "lugar estaciones desaparecidas en la ciudad más lejana que todavía puede cubrir la ciudad actual" nunca disminuye el conjunto de ciudades que pueden ser potenciadas en el futuro.

Proof.
Que la ciudad `i` actualmente tiene 'p' media potencia.
Cualquier ciudad que pueda ser propulsada por una nueva estación en satisfechas
`pos  marítima [i, i+r]`.
Si colocamos las nuevas estaciones en una posición de *izquierda* 'pos'' hechos pos`, las nuevas estaciones todavía cubren la ciudad `i` y también cubren todas las ciudades en `[pos', pos'+r]`.
Puesto que `pos` es la posición * más derecha* que todavía cubre `i`, el intervalo `[pos', pos'+r]`. es un subconjunto de `[pos, pos+r]`.
Por lo tanto, cualquier ciudad que pueda ser alimentada por una estación en `pos' también puede ser alimentada por una estación en `pos`.
Así, la elección de 'pos' no puede reducir el conjunto de ciudades futuras que pueden ser alimentadas. ∎



### Lemma 2
Para un `medio' fijo, la colocación codictiva utiliza el número mínimo posible de estaciones adicionales entre todas las colocaciones viables.

Proof.
Considere el momento en que la ciudad `i` es procesada.
Debido a que todas las ciudades anteriores ya están satisfechas (por inducción), cualquier colocación factible que satisfies ciudad `i` debe añadir al menos `neced = mid - cur` estaciones que cubren `i`.
El algoritmo codicioso añade exactamente estaciones "necesarias".
Debido a Lemma plaganbsp;1 esas estaciones se colocan lo más a la derecha posible, por lo que no hacen que ninguna ciudad previamente satisfecha se vuelva insatisfecha.
Por lo tanto, ninguna colocación puede usar menos estaciones que la codiciada. ∎



### Lemma 3
Si el cheque codicioso falla (necesita más que estaciones de 'k'), entonces ninguna colocación puede alcanzar el objetivo 'mid'.

Proof.
Supongamos que existía una colocación que lograba utilizar en las estaciones más 'k'.
Considere las ciudades en orden.
Siempre que el algoritmo codicioso decide añadir estaciones en la ciudad `i`, cualquier otra colocación debe añadir **al menos** el mismo número de estaciones en una posición que también cubre `i ' (Lemma Convennbsp;2).
Por lo tanto, la otra colocación no puede utilizar menos estaciones que la codiciada para cualquier prefijo de ciudades.
Si el codicioso supera la 'k', así debe cada otra colocación. ∎



### Theorem
La búsqueda binaria combinada con el cheque codicioso devuelve el máximo poder mínimo alcanzable.

Proof.
Dejar `opt` ser la potencia mínima óptima.
Por cada `mid ≤ opt`, el cheque codicioso tiene éxito (por Lemma 3), por lo que la búsqueda binaria moverá el límite inferior hasta 'mid'.
Por cada `mid ¢ opt`, el cheque codicioso falla, por lo que la búsqueda binaria mueve el límite superior hacia abajo.
Así la búsqueda converge a `opt`. ∎



----------------------------------------------------

## 4. Análisis de la complejidad

TEN TERRITOR TERRITOR TEN TERRITOR TEN TERRITOR TEN TERRITOR SON TERRITOR SON SON SON TEN SON SON SON 
Silencio------Prince--------
Silencioso búsqueda binaria (respuesta a la lista) Silencioso `O(respuesta a la lista) Silencio
Silencio Check per `mid` Silencio `O(n)` Silencio `O(n)` (the auxiliary array `add[]`) Silencio
Silencio total **`O(n log answer)`** Silencio** Silencio

`respuestas ' ≤ `sum(stations) + k` ≤ `105·105 + 109` ≈ `1010`, so `log answer` ≤ 34.



----------------------------------------------------

## 5. Implementaciones de referencia

Las tres implementaciones son idénticas en lógica – sólo la sintaxis difiere.

■ **NOTE** – Todos usan 'long' / 'long' para sumas y el número de estaciones agregadas para evitar el desbordamiento.
■ La función de ayuda puede implementar el cheque codicioso.

### 5.1 Java 17

``java
importar java.util*;

Solución de la clase pública {}
public long maxPower(int[] estaciones, int r, int k) {
int n = estaciones. longitud;

// límite superior: suma de todas las estaciones + k
larga suma = 0;
para (int s : estaciones) suma += s;
izquierda larga = 0, derecha = suma + k;

mientras (izquierda)
largo medio = (izquierda + derecha) 1; // (izquierda + derecha)/2 sin desbordamiento
si (puede(estaciones, r, n, mediados, k)) {}
izquierda = mediados + 1; // mediados es alcanzable → probar más grande
. ♫ ... {
derecha = media - 1; // media imposible → tratar más pequeño
}
}
derecho de retorno; // último éxito
}

booleano privado puede(int[] estaciones, int r, int n, long target, long k) {}
long[] add = new long[n + 1]; // diff array, n+1 para evitar controles de límites
larga curva = 0; // corriente de la ciudad i
largo utilizado = 0; // estaciones ya hemos añadido

para (int i = 0; i)
cur += add[i] + estaciones[i];

si
larga necesidad = objetivo - cur;
usada += necesidad;
si (utilizado > k) devolver falso; // no puede permanecer dentro del presupuesto

cur += necesidad; // añadir el poder ahora

int pos = Math.min(n - 1, i + r); // ciudad más lejana que aún cubre i
añadir[pos] += necesidad; // comenzar afectando en pos
si (pos + r + 1 ) {
añadir[pos + r + 1] -= necesidad; // dejar de afectar después del rango
}
}
}
retorno verdadero;
}
}
`` `

### 5.2 Python 3.10

``python
Solución de clase:
def maxPower(self, stations: List[int], r: int, k: int) - título int:
n = len(estaciones)

total = suma(estaciones)
lo, hola = 0, total + k # 64‐bit enteros son naturales en Python

def can(mid: int) - Propiedad Bool:
añadir = [0] * (n +1) # diff array
cur = 0 # energía que cubre esta ciudad
utilizado = 0

para i en rango(n):
cur += añadir[i] + estaciones[i]
si se curan a mediados:
necesidad = media - cur
usada += necesidad
si se utiliza > k: # budget exceeded
Retorno Falso
cur +=
pos = min(n - 1, i + r)
add[pos] += necesidad
si pos + r + 1
añadir[pos + r + 1] -= necesidad
Retorno

mientras que lo
media = (lo + hola) // 2
si puede (media):
lo = mitad + 1
más:
hola = media - 1
regreso
`` `

### 5.3 C+17

``cpp
Clase Solución {
public:
largo tiempo maxPower(vector fieltro unidades limitadas, int r, long long k) {}
int n = stations.size();

larga suma = 0;
para (int s : estaciones) suma += s;
lo largo = 0, hola = suma + k; // 64‐bit

auto can = [ cl](long long target) - título bool
vector realizado largo tiempo añadir(n + 1, 0); //
curro largo = 0, utilizado = 0;

para (int i = 0; i) {}
cur += add[i] + estaciones[i];
si
larga necesidad = objetivo - cur;
usada += necesidad;
si (utilizado > k) devolver falso;
cur += necesidad;
int pos = min(n - 1, i + r);
añadir[pos] += necesidad; // comienza a influir en pos
si (pos + r + 1 )
añadir[pos + r + 1] -= necesidad; // para después de su rango
}
}
retorno verdadero;
};

mientras (lo <= hola) {
largo largo medio = (lo + hola) 1;
si (puede(medio)) lo = medio + 1;
hola = mediados - 1;
}
volver hola;
}
};
`` `

Las tres soluciones se ejecutan en el mismo tiempo `O(n log answer)` y utilizan sólo un array auxiliar 'O(n).



----------------------------------------------------

## 6. Artículo del Blog – “De LeetCode 2528 a una solución de trabajo-entrevista”

■ **Búsqueda Palabras clave**: *LeetCode 2528*, *Maximizar la Ciudad Potencial Mínima*, *una ventana corredera de búsqueda binaria*, *Entrevista de Java*, *Entrevista de Python*, *entrevista de C+*, *entrevista de trabajo*, *ingeniero de software*, *data‐estructuras*.

-...

### 6.1 Problema Recap (TL;DR)

■ Dados `n` ciudades en una línea, cada una con un número inicial de estaciones de energía `estaciones[i]`.
■ Una estación tiene un rango de cobertura " (es decir, potencia cada ciudad de `pos-r ' a `pos+r ' ).
■ Podemos construir nuevas estaciones del mismo tipo.
■ ** Objetivo:** añadir las nuevas estaciones para que el poder **minimum** entre todas las ciudades sea lo más grande posible.
■ Devuelve ese máximo poder mínimo alcanzable.

-...

### 6.2 ¿Qué hace difícil el problema?

1. **Huge `k ' (≤ 109). #
No podemos iterar sobre todas las posibilidades; debemos usar aritmética de 64 bits en todas partes.

2. **Large `n ' (≤ 105). #
Cualquier enfoque de `O(n2)` se dará tiempo atrás.
Necesitamos una solución lineal o 'n log n`.

3. **Objetivo global (min de todas las ciudades). * *
El óptimo no se logra al maximizar localmente cada ciudad; debemos pensar globalmente.



### 6.3 Insight 1 – Búsqueda binaria en la respuesta

Si podemos lograr un poder mínimo de `medio' utilizando en la mayoría de las estaciones nuevas `k ' , entonces cualquier objetivo más pequeño es también alcanzable.
A la inversa, si no podemos lograr `mid ' , no es posible un objetivo más grande.

*¿Por qué búsqueda binaria? *
Transforma una verificación de viabilidad global en un predicado monotone:
`P(mid)` = “¿podemos alcanzar el poder mínimo ≥ mediados?”.

-...

## 6.4 Insight 2 – Greedy Placement Is Optimal

Cuando nos encontramos con una ciudad que carece de poder, debemos añadir algunas estaciones que lo cubren.
¿Qué ciudad debería albergar esas nuevas estaciones?
*Greedy Rule:* ponerlos lo más derecho posible (`pos = min(n-1, i+r)`).

¿Por qué funciona esto?

* La estación en la posición más justa posible tiene el mayor alcance *futuro* – puede ayudar al mayor número de ciudades a su derecha.
* La colocación nunca hace daño a las ciudades ya satisfechas (todos quedan de 'pos').

Matemáticamente, la estrategia avaricia es óptima (utiliza las estaciones más pequeñas) – vea la prueba de corrección arriba.



## 6.5 Insight 3 – O(1) Window Update with a Diff Array

Mientras escaneamos de izquierda a derecha mantenemos una suma de funcionamiento 'cur' de centrales eléctricas que actualmente influyen en la ciudad que se procesa.

`` `
estaciones existentes → constante
nuevas estaciones → añadido por codiciado, dejar la ventana después de pasos r
`` `

Almacenamos el * cambio de influencia* que comienza en cada ciudad en un array auxiliar `add[]`:

*Cuando ponemos nuevas estaciones en `pos`*
`add[pos] += need` (comienzan a influir en 'pos')
`add[pos+r+1] -= need` (se detienen después de su rango)

Durante la exploración realizamos `cur += add[i] + estaciones[i]`.
Todas las operaciones son `O(1)` por ciudad → general `O(n)`.



### 6.6 Complete Pseudocode

`` `
función puede (media):
Cura = 0
utilizado = 0
añadir = [0] * (n+1) // diff array

para mí en 0 ... n-1:
cur += add[i] // aplicar diff que comienza aquí
cur += estaciones[i]

si se curan a mediados:
necesidad = media - cur
usada += necesidad
si se utiliza > k: Retorno Falso

cur +=
pos = min(n-1, i+r)
add[pos] += necesidad
añadir[pos+r+1] -= necesidad // se aplicará cuando extremos de rango

Retorno
`` `

Búsqueda binaria en `mid` llamadas `can(mid)` hasta que la respuesta se estabiliza.



### 6.7 Code Snippets

Silencio Idioma Silencio Silencio
Silencio...
Silencio **Java** Silencioso `long ' por sumas, ` > 1` para el punto medio para evitar el desbordamiento. Silencio
Silencio **Python** TENIDO Use `list` of ceros; Los puntos de Python no están abundados, pero todavía usamos 'long`-like logic. Silencio
TENIDO **C+** TENIDO `long' en todas partes, `vector cumplió largo tiempo `` para `add`. Silencio

■ Vea las implementaciones de referencia en la sección anterior para código completo, copy‐paste-ready.



----------------------------------------------------

## 7. Pitfalls comunes " What Not To Do "

Silencio Pitfall Silencioso Explicación
Silencio----------------------------
Silencio **Using `int` for the answer** Silencio `k` can be `109` and each city may already have `105` stations → sum ~ `10`. TEN siempre use `long` / `long long`. Silencio
Silencio **Omitiendo el `+ r + 1` en la actualización del dif** Silencio La influencia de la estación termina después de `r` pasos. Olvidar el `+1` significa que sigue influenciando a una ciudad demasiados, lo que conduce a una supercuación. Añada la `necesidad' a `pos + r + 1`. Silencio
Silencio **Binary search bounds off by one** Silencio Si regresamos `lo' después del bucle, podemos dar un objetivo inalcanzable. Silencio Retorno `hi` (último éxito `mid`). Silencio
Silencio **Ignorando ciudades más allá de la gama de `add`** Silencio Cuando `pos + r + 1 == n`, accedemos `add[n]` que está fuera del vector. TENIDO Asignar `add` con el tamaño `n+1` o guardar con `si (pos + r + 1 ' hecho n)`.
Silencio **No añadir `estaciones[i]` Después del diff** Silencio Las estaciones existentes son siempre parte del poder en esa ciudad. tención Incluya `estaciones[i]` en la misma actualización `cur`. Silencio
Silencio **No reajustar `cur` cada prueba** Silencio La suma de ejecución persiste a través de búsquedas binarias → resultados incorrectos. Silencio Recrear `add` (o aclararlo) por cada llamada de `can`. Silencio



----------------------------------------------------

## 8. Del algoritmo a la entrevista éxito

1. **Explicar la monotónica**: por qué la búsqueda binaria funciona para la viabilidad.
2. **Describa el invariante avaricioso**: más lejos colocación → más largo alcance, nunca hace daño a la izquierda.
3. **Mostrar el truco de ventana O(1)**: diff array → actualización de la ventana deslizante.
4. **Emphasise 64 bit arithmetic**: point out that `k` is huge, `n` large → all sums must be `long`.
5. **Demuestra tu código**: corre a través de un pequeño caso de prueba mental, pasando por `cur`, `add`, `used`.
6. ** Casos de discusión**:
* `r` = 0 → cada ciudad sólo puede ser alimentada por su propia estación.
* `k` = 0 → La respuesta es simplemente `min(estaciones)`.
* Todas las ciudades ya tienen un enorme poder → la respuesta es enorme, pero aún limitada por el presupuesto.

Ser capaz de articular estas ideas muestra al entrevistador que usted puede manejar tanto *algoritmic* como *practical* limitaciones.



----------------------------------------------------

### 7.1 Final Thought

LeetCode 2528 es un ejemplo de libro de texto de cómo un problema aparentemente simple "add-up‐to‐k" esconde ideas algoritmos profundos.
Al convertir el objetivo global en un predicado de búsqueda binaria, demostrando la óptimaidad codictiva, y utilizando un array de diff para actualizaciones lineales, llegamos a una solución que es tanto **eficiente** como **limpio**.

Comparte este enfoque en tu próxima entrevista, ¡y mira a los entrevistadores anotados en aprobación!

-...



### 6.8 Artículo – ¿Me perdí algo? ”

■ Si saltas el artículo y ves las lagunas, aquí tienes una lista de verificación rápida:

1. ¿Mencionaste aritmética de 64 bits? * *
2. ** ¿Explicaste por qué el codicioso es óptimo? #
3. ** ¿Has mostrado cómo el array de diff mantiene la ventana O(1)? * *
4. ** ¿Enumeró los errores más comunes? * *
5. ** ¿Usaste las palabras clave en el título? #

■ Si no, siéntete libre de ajustar el artículo en consecuencia.



-...

¡Felicitaciones!
Usted ahora entiende LeetCode 2528 a un nivel profundo, tiene código de producción listo en tres idiomas, y puede explicarlo como un ingeniero de temporada. ¡Buena suerte en tu próxima entrevista!



----------------------------------------------------

### 7. Sobre este escrito

■ Si te ha parecido útil, compártelo en GitHub, Stack Overflow, o en un blog personal.
■ Etiqueta con **software-engineering**, **interview‐prep**, **algorithms**, y **data‐estructuras**.

-...



-...

### 8. Resumen de lo que usted aprende

* La búsqueda binaria convierte un cheque de viabilidad global en un predicado monotone simple.
* La regla codicioso “lugar lo más justo posible” es probablemente óptima para este problema.
* Un array de diff (diferencia) da una actualización de la ventana deslizante de `O(1)`, convirtiendo un proceso potencial `O(n2)` en `O(n)`.
* Todas las implementaciones utilizan aritmética de 64 bits para permanecer dentro de las limitaciones presupuestarias.
* El mismo algoritmo funciona en Java, Python y C++, demostrando la elegancia agnóstica del lenguaje.



----------------------------------------------------

¡Feliz codificación!



----------------------------------------------------

### 9. Preguntas frecuentes

**Q:** ¿Por qué la respuesta es siempre 'hi' después del bucle de búsqueda binaria?
**A:** Porque `lo' supera el último éxito 'mid'. El bucle termina cuando " lo " hi " ; `hi ' entonces tiene el mayor valor factible.

**Q:** ¿Y si 'k = 0'?
**A:** La función " puede " comprobar inmediatamente si cada ciudad ya satisface `mid ' ; si `mid ' es mayor que el mínimo mundial, falla.

**Q:** ¿Realmente necesitamos el 'add` array size `n+1`?
**A:** Es un pequeño margen de seguridad; podríamos usar el tamaño `n` con controles de límites, pero la ranura extra elimina un condicional por iteración.



----------------------------------------------------

#### 10. Take-away

■ *LeetCode 2528* muestra que una combinación inteligente de ** búsqueda binaria**, ** colocación inteligente**, y ** actualizaciones de la matriz diff** pueden convertir una optimización global abrumadora en un algoritmo elegante y lineal.
■ Dominar estos patrones te servirá bien en entrevistas y proyectos del mundo real por igual.