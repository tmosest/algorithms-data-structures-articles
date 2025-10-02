-...
Título: LeetCode 772. Calculadora básica III -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Solution Overview**

Evaluamos la expresión en un escaneo lineal.
Mientras escaneamos, seguimos

* `num` - el número que se está leyendo (puede contener varios dígitos)
* `pre` – el valor *último* que ya consideraba multiplicación/división
(se añadirá al resultado sólo después de ver un plus/minus o el final).
* `res` – la suma de todos los términos que ya están terminados.
* `sign` - el operador que será aplicado al siguiente `num`.

Cuando nos encontramos con un `(` repetitivamente evaluamos la sub-expresión que sigue
hasta que coincida " .
Cuando vemos un operador (o `)` o el final de la cadena) "commitimos" la corriente
`num` to `res` / `pre` according to the previous operator.
Si el personaje que causó la comisión es `)` de inmediato regresamos
`res + pre` – esto termina el nivel actual de recursión.

La profundidad recursiva está atada por el número de paréntesis anidados, por lo que la
el tamaño de la pila auxiliar es `O(#brackets)`.

----------------------------------------------------

#### Correctness Proof

Demostramos que el algoritmo devuelve el valor de la expresión `s`.

-...

##### Lemma 1
En cualquier momento durante la evaluación de un nivel (entre un par coincidente de
paréntesis o toda la cuerda) `res` equivale a la suma de todo terminado
términos y " pre " iguala el valor de la *currente* en espera de plazo (la que
se añadirá a `res` después de que el próximo operador sea procesado).

Proof.
Inicialmente `res = 0` y `pre = 0`; la lema sostiene.

Siempre que encontremos a un operador " (o al cierre " ) " o final de la cadena)
el algoritmo ejecuta:

`` `
(señal) {
caso '+': res += pre; pre = num; break;
caso '-': res += pre; pre = -num; break;
caso '*': pre *= num; break;
caso '/': pre /= num; break;
}
`` `

" La señal " es el operador que estaba pendiente antes de " año " .
- Por " + " o " el término pendiente " pre " se ha terminado y se ha añadido a " ,
y " pre " se establece en el nuevo mandato ( " año " o " año " ).
- Por `* o `/` el término pendiente es *extended* por multiplicación/división,
por lo que `pre` se actualiza pero no se añade a `res` todavía.

Así, después del interruptor, `res` contiene todos los términos terminados, y `pre` contiene
el último término inacabado (posiblemente ya multiplicado/dividido).
Si el operador es `)`, la función devuelve `res + pre`, que por el lemma
iguala el valor de la sub-expresión.
Por lo tanto el invariante mantiene inductivamente para cada paso. ∎



##### Lemma 2
Cuando una subexpresión dentro de los paréntesis se evalúa recursivamente, su retorno
valor igual al valor matemático de esa sub-expresión.

Proof.
La llamada recursiva se introduce sólo cuando se ve un `(`.
En el interior de la llamada el mismo invariante (Lemma bordenbsp;1) sostiene, porque el mismo
el mismo código es ejecutado.
Cuando el emparejado se procesa, la función devuelve `res + pre`,
que por Lemma adultnbsp;1 equivale al valor de esa sub-expresión. ∎



################################################################################################################################################################################################################################################################ Theorem
`calculado(s)` devuelve el valor de la expresión aritmética representada por
` s`.

Proof.
La llamada de nivel superior procesa toda la cadena.
Cada número se lee completamente (los números multidigit son manejados por el
`num = num*10 + digit` step).
Cuando la cadena termina, el último `num' se comete (porque `idx == n`), así que todo
se añaden términos a " res " .
Por Lemma adultnbsp;1 el valor devuelto es `res + pre`, que es el valor del
expresión entera.
Lemma plaganbsp;2 asegura que cada subexpresión paréntesisada sea evaluada
correctamente.
Así la función devuelve el resultado correcto. ∎



----------------------------------------------------

#### Complexity Analysis

Seamos la longitud de la cadena de entrada.

* **Tiempo** – Cada personaje es examinado exactamente una vez (`idx` sólo avanza hacia adelante).
Por lo tanto, el tiempo de funcionamiento es ``.

* **Espacio** – La profundidad de la pila de recursión auxiliar equivale al anidamiento máximo
de paréntesis, en la mayoría de `n/2`.
Así el espacio auxiliar es `O(#brackets)`. ≤ `O(n)`.

----------------------------------------------------

#### Referencia Implementación (Java 17)

``java
Clase Solución {
// índice compartido - la posición en la cadena que se procesa actualmente
idx privado;

public int calculate(String s) {
idx = 0; // comenzar desde el principio por cada llamada
eval (s);
}

*
* Evalua la expresión representada por la cadena
* empezando por el valor actual de `idx`. Se detiene cuando la cuerda termina
* o cuando se encuentra una coincidencia. El valor de retorno es el valor
* de la parte procesada.
*/
privada int eval (String s) {
int res = 0; // suma acumulada de términos terminados
int pre = 0; // actual término pendiente (después de *, /)
int num = 0; // número actual de lectura
char sign = '+'; // operador que se aplicará a la siguiente num

int n = s.length();
mientras (idx)
char c = s.charAt(idx++);

si (c == '(') { // inicio de una subexpresión
num = eval(s); // repetitivamente evaluarlo
} si (c не= '0' ' t = '9') { // número (posiblemente не1 dígitos)
num = num * 10 + (c - '0');
}

/* Comprobar el número actual cuando un operador, ')', o final se ve */
si (c == '+' Silencioso c == '-' {}
(señal) {
caso '+': res += pre; pre = num; break;
caso '-': res += pre; pre = -num; break;
caso '*': pre *= num; break;
caso '/': pre /= num; break;
}

si (c == ')) { // terminó un subexprador
devolver res + pre; // devolver su valor al callador
}

num = 0; // reset for the next term
señal = c; // recordar el operador pendiente
}
}
retorno res + pre; // valor final de todo el nivel
}
}
`` `

El programa sigue exactamente el algoritmo probado correcto arriba y satisfies
las limitaciones de LeetCode 227.