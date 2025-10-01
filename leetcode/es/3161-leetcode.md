-...
Título: LeetCode 3161. Búsquedas de colocación de bloques -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Para la escalera conocemos los límites

`` `
1 , 2 , ... , MAX
`` `

Durante el juego algunas de esas posiciones se convierten en *obstacles*.
Si usted está de pie en un paso `a` usted puede caminar sólo a la derecha.
Tan pronto como pisara un obstáculo el paseo se detiene.
La consulta `P a` pide el número máximo de pasos que se pueden tomar
empezando desde el paso `a`.

----------------------------------------------------

##### 1. Observación

Un obstáculo nunca desaparece – sólo se añade.
Todos los obstáculos juntos dividen toda la gama en descomunión
intervalos

`` `
,
(primerObstáculo, segundoObstáculo)
(segundoObstáculo, tercerObstáculo)
(últimoObstáculo, +∞)
`` `

El paseo que comienza en `a` sólo puede utilizar el intervalo que contiene `a`
y debe detenerse antes del siguiente obstáculo a la derecha.
Por lo tanto, la respuesta para una consulta `P a` es

`` `
siguienteObstacleOnRight – a – 1
`` `

El siguienteObstacleOnRight es el primer obstáculo cuya posición es mayor
que `a`.
Si `a` en sí es un obstáculo el paseo ya está bloqueado - la respuesta
es `0`.

----------------------------------------------------

##### 2. Estructura de datos

El conjunto de posiciones de obstáculos debe apoyar

* insertar un nuevo obstáculo,
* preguntar si una posición es un obstáculo,
* encontrar el primer obstáculo más grande que una posición dada.

Todas las operaciones son necesarias en tiempo logarítmico.
Un árbol de búsqueda binaria equilibrado (`TreeSet` en Java) es perfecto para eso.
Dos obstáculos ficticios se insertan una vez por caso de prueba:

`` `
-1 – justo antes del primer paso real
MAX + 1 – justo después del último paso real
`` `

Con esos dos centinelas `más alto(a)` (el primer elemento más grande que
" a " ) siempre se define por cada `a ' entre `1 ' y `MAX`.

----------------------------------------------------

##### 3. Algoritm

Para cada caso de prueba

`` `
leer MAX y Q
obs ← TreeSet que contiene -1 y MAX+ 1

repetir Q veces
read type (C or P) and value v
si tipo = 'C' // crear un obstáculo
obs.add(v)
más // tipo = 'P', consulta
si obs.contains(v)
producción 0
más
siguiente ← obs.higher(v)
(next - v - 1)
`` `

----------------------------------------------------

##### 4. Prueba de corrección

Demostramos que el algoritmo imprime la respuesta correcta para cada consulta.

-...

##### Lemma 1
Que `O` sea el primer obstáculo estrictamente mayor que `a`.
Cualquier caminata que comience a paso `a' y no pise un obstáculo
contiene exactamente `O - a - 1` pasos.

Proof.

Todos los pasos entre `a` y `O-1` están libres de obstáculos, porque
`O` es el primer obstáculo a la derecha.
El paseo puede moverse a `O-1`, que es el último paso libre.
Después de eso el siguiente paso sería en `O`, un obstáculo, que es
No está permitido.
Así el paseo consta de los pasos

`` `
a, a+1 , ... , O-1
`` `

cuya longitud es `O-1 - a + 1 = O - a - 1`. ∎



##### Lemma 2
Si el paso `a' en sí es un obstáculo, el número máximo de pasos que
puede ser tomado de `a` igual a `0`.

Proof.

Usted comienza en un obstáculo, por lo tanto ya está bloqueado y
no puede dar ningún paso. ∎



##### Lemma 3
Por cada paso `a` entre `1` y `MAX` el algoritmo devuelve
`0` si `a` es un obstáculo y de otra manera vuelve `O - a - 1`,
Donde `O` es el primer obstáculo en el derecho de `a`.

Proof.

El conjunto `obs` siempre contiene todos los obstáculos actuales.
Si `a` está en `obs` los productos del algoritmo " 0 " , por Lemma contaminanbsp;2
esta es la respuesta correcta.

De lo contrario el algoritmo obtiene `next = obs.higher(a)`.
Debido a que el conjunto también contiene los centinelas `-1` y `MAX+1`,
" El siguiente " es precisamente el primer obstáculo estrictamente mayor que " .
El algoritmo produce `next - a - 1`.
Por Lemma adultnbsp;1 esto equivale a la longitud de la caminata admisible más larga
empezando desde `a`. ∎



################################################################################################################################################################################################################################################################ Theorem
Para cada consulta de tipo `P a` el algoritmo imprime el máximo
posible número de pasos que se pueden caminar desde el paso `a`.

Proof.

Por Lemma limitadanbsp;3 el valor impreso por el algoritmo equivale a la longitud
de la caminata más larga que no atraviesa un obstáculo.
Cualquier caminata admisible debe terminar antes del primer obstáculo a la derecha,
por lo tanto ya no existe caminar.
Por lo tanto el valor impreso es exactamente el máximo requerido. ∎



----------------------------------------------------

##### 5. Análisis de la complejidad

Dejar `N` ser el número de obstáculos que se han añadido
(incluyendo los dos centinelas).

*Cada inserción* o *lookup* en `TreeSet` cuesta `O(log N)` tiempo.
Todas las consultas se procesan en
`O(Q · log N)` tiempo.
El conjunto almacena en la mayoría de los valores 'N', por lo que el consumo de memoria es
`O(N)`.

----------------------------------------------------

##### 6. Aplicación de las referencias (Java 17)

``java
importa java.io.*;
importar java.util*;

clase pública Principal {}

Escáner rápido...
Clase privada estática FastScanner {}
final privado BufferedInputStream in;
byte final privado[] buffer = nuevo byte[1]
int ptr privado = 0, len = 0;

FastScanner(InputStream is) { in = new BufferedInputStream(es); }

int readByte() lanza IOException {
si
len = in.read(buffer);
ptr = 0;
si (len len= 0) retorno -1;
}
búfer de retorno[ptr+];
}

Privada cuerda siguiente() lanza IOException {
StringBuilder sb = nuevo StringBuilder();
int c;
♪
c = readByte();
(c == -1) Retorno nulo;
} mientras (Character.isWhitespace(c));

♪
sb.append(char) c);
c = readByte();
} mientras (c != -1 " sensible !Character.isWhitespace(c));

devolver sb.toString();
}

largo siguienteLong() lanza IOException {
String s = next();
si (s == null) lanzar nuevo IOException("EOF");
devolver Long.parseLong(s);
}
}
/* *

el vacío estático público principal (String[] args) lanza Excepción {
FastScanner fs = nuevo FastScanner (System.in);
StringBuilder out = nuevo StringBuilder();

Token String;
(token = fs.next()) != null) { // read MAX
largo MAX = Long.parseLong(token);
larga Q = fs.nextLong(); // número de consultas

TreeSet se realizóLong ratio obs = nuevo TreeSet correspondió();
obs.add(-1L); // centinela ante la escalera
obs.add(MAX + 1); // centinela después de la escalera

para (long i = 0; i)
Tipo de cuerda = fs.next(); // "C" o "P"
long v = fs.nextLong();

si (tipo.charAt(0) == 'C') { // añadir obstáculo
obs.add(v);
} más { / / consultas
si (obs.contains(v)) {}
out.append('0').append('\n');
. ♫ ... {
largo siguiente = obs.higher(v); // primer obstáculo v
out.append(next - v - 1).append('\n');
}
}
}
}

System.out.print(out.toString());
}
}
`` `

El programa sigue exactamente el algoritmo probado correcto arriba y
se ajusta al estándar Java 17.