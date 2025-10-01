-...
Título: LeetCode 936. Selling The Sequence -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 936. Sellando la secuencia – Solución completa en **Java**, **Python** < **C++** + SEO-Optimised Blog Post

■ **TL;DR**
■ *Reverse‐engineer la cadena de destino, repetidamente reemplazar cualquier ventana de cierre con “*” y almacenar los índices de inicio. Una vez que todo el objetivo es “*” la respuesta es los índices registrados en orden inverso. Complejidad: `O(n·m)` tiempo, `O(n)` espacio. *

-...

### 1. Código - Tres idiomas

■ **Importante** – Las tres soluciones son algoritmos inversos **, la misma lógica utilizada en el editorial LeetCode.
■ Corren en `O(n * m)` donde `n = target.length` y `m = sello.length` (caso inferior 1 000 × 1 000 → 1 000 000 000 000 ops – fino para los límites).

-...

################################################################################################################################################################################################################################################################

``java
importar java.util*;

Solución de la clase pública {}
int[] movesToStamp(String sello, String target) {
// Caso especial – sello y objetivo son idénticos
si (estamp.equals(target)) devuelve nuevo int[]{0};

char[] s = print.toCharArray();
char[] t = target.toCharArray();
int m = s.length, n = t.length, window = n - m + 1;
Lista de cambiosInteger título = nuevo ArrayList implicado();

booleano cambiado = verdadero;
mientras (cambiado) {
cambiado = falso;
para (int i = 0; i) {}
si (canStamp(i, s, t)) { // podemos estampar aquí
selloAt(i, s, t);
moves.add(0, i); // prepend (orden reversa)
cambiado = verdadero;
}
}
}

// Verificar que cada personaje se ha convertido en '* '
para (char c : t) si (c != '*) devuelve nuevo int[0];

// Convertir lista en array
int[] ans = nuevo int[moves.size()];
para (int i = 0; i) se mueve.size(); i++) ans[i] = moves.get(i);
devolver los ans;
}

// ventana que coincida con el sello, '*'s son tratados como como como comodines
booleano privadoStamp(int i, char[] s, char[] t) {}
para (int j = 0; j) {}
char tc = t[i + j];
si (tc != '*' ' tc != s[j]) vuelve falso; // desajuste
}
// Debemos sellar al menos un personaje no estrella
para (int j = 0; j) {}
si (t[i + j] != '*) vuelven a la verdad;
}
devolver falso;
}

sello vacío privado At(int i, char[] s, char[] t) {}
para (int j = 0; j)
}
}
`` `

-...

##### 1.2 Python

``python
Solución de clase:
def moves ToStamp(self, sello: str, target: str) - confiar List[int]:
si el sello == objetivo:
Regreso [0]

s = list(stamp)
t = list(target)
m, n = len(s), len(t)
ventana = n - m + 1
movimientos = []

def can_stamp(start: int) - título Bool:
para j en rango(m):
t[start + j] != '* y t[start + j] != s[j]:
Retorno Falso
# Debe reemplazar al menos un personaje real
devolver cualquier(t[start + j] != '*' para j en rango(m)

def print_here(start: int) - título Ninguno.
para j en rango(m):
t[start + j] = '* '

cambiado = Verdadero
mientras se cambia:
cambiado = Falso
para i en rango(ventana):
si can_stamp(i):
sello_here(i)
moves.insert(0, i) # prepend
cambiado = Verdadero

si algún(c != '*' para c in t):
retorno []

Cambios de retorno
`` `

-...

##### 1.3 C++

``cpp
Incluido el título
#include ■string
#include >

Clase Solución {
public:
std:::vector asignadoint título mueveToStamp(std::string sello, std:::string target) {}
si (stamp == target) regresa {0};

const int m = sello.size();
const int n = target.size();
const int window = n - m + 1;
std::vector seleccionados movimientos de propiedad;
bool cambiado = verdadero;

auto canStamp = [ю](int i) - bool
para (int j = 0; j)
char tc = target[i + j];
si (tc != '*' ' tc != sello[j]) devuelve falso;
}
// al menos una no estrella debe ser estampada
para (int j = 0; j)
si (target[i + j] != '*) vuelven a la verdad;
devolver falso;
};

sello automático Aquí = [ ](int i) {
para (int j = 0; j );
};

mientras (cambiado) {
cambiado = falso;
para (int i = 0; i) {}
si (canStamp(i)) {}
selloHere(i);
moves.insert(moves.begin(), i); // prepend
cambiado = verdadero;
}
}
}

para (carc : target) si (c != '*) regresar {};

// resultado ya está revertido, no hay necesidad de revertir de nuevo
movidas de retorno;
}
};
`` `

■ **Cómo correr** – Los tres snippets están listos para caer en una clase LeetCode `Solution` (Java), una clase `Solution` con el método `movesToStamp ' (Python), o una clase `Solution ' con el miembro `movesToStamp ' (C++).
■ Usted puede probarlos en su IDE o ejecutar un método de `principal' rápido para imprimir la salida.

-...

### 2. SEO‐Optimised Blog Post

■ **Título** – “LeetCode 936: Stamping The Sequence – Greedy Reverse Solution en Java / Python / C++”
■ **Meta Descripción** – “Aprenda la solución algoritmo completa para el problema LeetCode 936 ‘Stamping The Sequence’. Paso a paso la lógica inversa ambiciosa, el manejo de los bordes y el código limpio en Java, Python, C++ ace su entrevista de codificación. ”

-...

################################################################################################################################################################################################################################################################

■ ** Declaración sobre el proyecto** Se nos da una cadena *stamp* (por ejemplo, “abc”) y una cadena *target* (por ejemplo, “ababc”).
■ En un movimiento podemos colocar el sello sobre cualquier ventana contigua del objetivo; cada personaje en esa ventana se convierte en “*”.
■ El sello se puede colocar sobre “*” porque esas posiciones serán posteriormente sobrescritos.
■ El objetivo: convertir todo el objetivo en “*” utilizando ** en la mayoría de los movimientos de `10 × target.length** y producir la secuencia de índices de inicio (orden reversa de estampación).

■ Este problema es un clásico rompecabezas de entrevistas de “ingeniería reversa” que prueba ** estrategia de grano** y ** manipulación de cuerdas**. Es uno de los desafíos más esperados de LeetCode en entrevistas técnicas para los roles de software más altos.

-...

##### 2.2 Intuición - Trabajo *Backward*

■ En lugar de construir el objetivo del sello, *destruimos* el objetivo hasta que todo sea “*”.
■ ¿Por qué? Porque la estampación sobrescribe caracteres – una vez que una posición es “*”, cualquier sello posterior lo sobreescribirá.
■ Si empezamos desde el final (target) y retrocedemos, podemos reemplazar con seguridad una ventana de cierre de sellos con “*” sin preocuparse por futuras dependencias.

■ **Core Idea** – Repetidamente encontrar una ventana `[i, i+m)` que coincida con el sello (tratar “*” como un comodín), reemplazarlo con “*”, y recordar `i.
■ Después de no más reemplazos son posibles, compruebe si todo el objetivo es “*”. Si es así, revierta los índices registrados → es la lista de movimientos de estampación.

-...

#### 2.3 El Algoritmo Inverso Greedy (Pseudocode)

`` `
1. Convertir sello y blanco en arrays mutables.
2. movimientos = lista vacía
3. cambiado = verdadero
4. mientras se cambia:
cambiado = falso
para mí en 0 ... n-m:
si target[i...i+m) coincide con el sello (t[i+j] == '*' o t[i+j] == sello[j] para todos j):
reemplazar el objetivo[i...i+m) por '* '
prepend i to moves // reverse order
cambiado = verdadero
5. si algún personaje en blanco != '*': retorno []
6. movimientos de retorno // ya revertidos
`` `

*El paso “prependiente” garantiza que finalmente devolvamos los índices en el orden correcto de estampación sin un pase de reversión adicional. *

-...

#### 2.4 Manejo del objetivo del 10 ×. longitud Mover constraint

■ La condición de terminación natural del algoritmo es que cada personaje se convierte en “*”.
■ En el peor de los casos podríamos marcar una ventana muchas veces; el editorial LeetCode muestra que el número de movimientos es siempre ≤ `10 × n`.
■ Por lo tanto, no necesitamos hacer cumplir explícitamente el límite – el algoritmo terminará antes o devolverá `[]` si es imposible.

-...

#### 2.5 Time & Space Complexity

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
TEN Java TENIDO `O(n·m)` (caso inferior ♥ 1 M operaciones) Silencio `O(n)` (mutable target array + lista de índices)
TENIDO Python TENIDO `O(n·m)` Silencio
TENIDO C++ TENIDO `O(n·m)` TENIDO `O(n)` Silencio

■ **¿Por qué?
■ Para cada escaneo de todas las ventanas (en la mayoría de las ventanas 'n-m+1`) comparamos con 'm` caracteres.
■ En el peor de los casos es posible que necesitemos escanear `n` veces, dando `n·m`.
■ Desde `n,m ≤ 1000`, la solución es lo suficientemente rápida.

-...

#### 2.6 Common Pitfalls & Edge‐ Lista de verificación de casos

Silencio Pitfall Silencio Qué hacer para mirar hacia fuera Para Silencio
Silencio------------------------
tención **El bucle infinito** – olvidando poner `cambiado` de nuevo a `falso' antes de cada bucle exterior. ← El algoritmo nunca terminaría. tención Inicializar `cambiado = falso` al comienzo de la `mientra'. Silencio
Silencio **Missing a sello** – not treat “*” as a wildcard during matching. El algoritmo no informará incorrectamente ninguna solución. Silencio En `canStamp`, permita `target[i+j] == '*' para que coincida con cualquier personaje de sello. Silencio
Silencio **Orden de movimiento incorrecto** – reiniciar índices en orden inverso. Los entrevistadores esperan que los movimientos se apliquen *para adelante*. Ya sea prependiendo cada índice encontrado o revertir la lista final. Silencio
Silencio **Posiciones inalcanzables** – algunas posiciones pueden nunca convertirse en “*” a pesar de que el sello puede ser colocado allí más tarde. El algoritmo puede devolver prematuramente un array vacío. Mantenga una matriz 'visitada' para evitar volver a iniciar la misma posición una vez que haya sido estampada. Silencio
← **Large input** – naïvely re-scanning every time may degrade performance. No es un gran problema para las limitaciones, pero buenas prácticas para romper temprano si no hay cambios. Utilice la bandera `cambiada' para salir temprano si no se encontró ninguna ventana de estampación. Silencio

-...

#### 2.7 Ejecutando el Código (Ejemplo)

``bash
# Java (LeetCode environment)
Solución s = nueva solución ();
int[] res = s.movesToStamp("abc", "ababc");
System.out.println (Arrays.toString(res)); // [0, 1]

# Python
s = Solución()
print(s.movesToStamp("abc", "ababc") # [0, 1]

# C++
Solución s;
auto res = s.movesToStamp("abc", "ababc");
para (int x : res) std::cout se realizó x  se hizo ";
`` `

■ ** Salida** – `[0, 1]` significado: sello en el índice `1` primero (volver “ababc” → “a***c”), luego marcar el índice `0` (volver “a***c” → “*****”).

-...

##### 2.8 Conclusiones

"Stamping The Sequence" es un ejercicio valioso para dominar algoritmos codiciosos en cuerdas.
■ La solución inversa codicioso es concisa, fácil de entender y funciona uniformemente a través de Java, Python y C++.
■ Maestro este patrón – usted será capaz de abordar rompecabezas similares *string overwriting* en entrevistas de codificación del mundo real.

-...

### 3. Pensamientos finales

■ **Por qué importa** – Conocer tanto el algoritmo como cómo articular sus razonamientos muestra que puede *solver problemas complejos de cuerda* y *explicar su proceso de pensamiento* claramente.
■ Estos son rasgos esenciales para los ingenieros de software senior en las principales empresas tecnológicas, especialmente aquellos enfocados en la solución de problemas algorítmicos, diseño de sistemas y código de alto rendimiento.

■ **Siguiente Pasos** – Variaciones de práctica:
* ¿Y si el sello contiene caracteres repetidos?
* ¿Cómo adaptarías el algoritmo para cadenas Unicode?
* ¿Y si se le pidió que emitiera el número de movimientos *mínimo*?

■ ¡Pruébalos! Y no te olvides de compartir tu solución en GitHub o una cartera personal para impresionar a los reclutadores. ¡Feliz codificación!

-...

■ **Author** – (Su nombre) – Senior Software Engineer at XYZ Corp.
■ **Contacto** – email@example.com, LinkedIn: /in/yourprofile.

-...

**End of Blog Post**.