-...
Título: LeetCode 2531. Hacer Número de caracteres distintos igual -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Respuesta corta** - Sí.
Usted puede decidir la respuesta en *O(Principal involuntario)* tiempo sólo examinando
frecuencia de cada letra (hay sólo 26 de ellos).
La idea clave es seguir el *número de letras únicas* en cada cadena
(`c1` y `c2`) y ver qué sucede con esos números cuando cambias dos
letras.

-...

## ¿Por qué la fuerza bruta es innecesaria

Si literalmente probamos todos los pares de posiciones en `w1` y `w2` lo haríamos
necesidad

`` `
O( vivenw1 sufrimiento · Silenciow2 intimidad)
`` `

operaciones.
Porque un intercambio sólo puede afectar el *tipo* de las dos letras involucradas
(`a` from `w1` and `b` from `w2`), the effect depends only on the
*frecuencia* de `a` en ambas cuerdas y de `b` en ambas cuerdas.
Sólo hay 26 cartas posibles, así que podemos probar todos los pares del `26 × 26`.
y computar el efecto en tiempo constante.

-...

## ¿Qué cambios cuando cambiamos a " (de `w1 ' ) con `b ' (de `w2 ' )

← Situación Silencioso Efecto en el *unique‐letter* conteo de la cuerda que deja
Silencio...------------
Silencio `a` aparece **una vez** en `w1` → se hace único después de sacarlo → **c1=1**
Silencio `a` hace **no** aparecen en `w2` → se convierte en una nueva carta única en `w2` → **c2+=1**
Silencio `b` aparece ** una vez** en `w2` → se hace único después de sacarlo → **c2-=1**
Silencio `b` hace **no** aparecen en `w1` → se convierte en una nueva carta única en `w1` → **c1+=1** Silencio

Si `a` y `b` son el carácter *same* los dos primeros cambios cancelan
unos a otros – terminamos con el mismo 'c1' y 'c2' que nosotros
comenzó con, por lo que este intercambio sólo puede tener éxito cuando `c1 == c2` ya.

Con estas reglas podemos calcular el *nuevo* número de cartas únicas
sin tocar las cuerdas reales.

-...

## Java implementation (O (O( turbulencias) tiempo, O(1) space)

``java
importar java.util*;

Solución de la clase pública {}

booleano público isItPosible(String w1, String w2) {
// Frecuencia de cada carta
int[] f1 = nuevo int[26];
int[] f2 = nuevo int[26];

// Cuenta cartas únicas en cada cadena
int uniq1 = 0, uniq2 = 0;
para (cara c : w1.toCharArray()) {}
(f1[c - 'a']+ == 0) uniq1++;
}
para (cara c : w2.toCharArray()) {}
(f2[c - 'a']+ == 0) uniq2++;
}

/* Salida temprana: si la diferencia es > 2, un intercambio puede cambiar
el conteo a la mayoría de 2 (remove un char único y/o añadir un
nuevo char único). Si es imposible traer las dos cuentas
dentro de 2, la respuesta es definitivamente falsa. */
(Math.abs(uniq1 - uniq2) 2) volver falso;

/* Pruebe cada par (a desde w1, b desde w2) */
para (int a = 0; a) {}
si (f1[a] == 0) continuar; // a debe existir en w1

// copia de cuenta únicas actuales para esto a
int newUniq1 = uniq1;
int newUniq2 = uniq2;

// La eliminación de un w1
si (f1[a] == 1) nuevoUniq1--; // a era único
si (f2[a] == 0) nuevoUniq2++; // a es nuevo en w2

para (int b = 0; b)
si (f2[b] == 0) continuar; // b debe existir en w2

int curUniq1 = newUniq1;
int curUniq2 = newUniq2;

// Si a == b cambiamos la misma carta
si (a ==b) {
// En este caso ya manejamos el efecto de
// eliminación de la w1, añadirla a w2. No hay cambio
// a los conteos únicos – sólo necesitamos comprobar
// si los conteos actuales ya son iguales.
si (curUniq1 == curUniq2) regresan verdaderos;
continuar;
}

// Añadiendo b a w1
si (f1[b] == 0) curUniq1++; // b es nuevo en w1

// Removing b de w2
si (f2[b] == 1) curUniq2--; // b era único

/* Ahora curUniq1 / curUniq2 son los conteos únicos después
intercambiando una con b. Si coinciden, hemos encontrado un
un intercambio válido. */
si (curUniq1 == curUniq2) regresan verdaderos;
}
}
devolución falsa; // ningún par tuvo éxito
}
}
`` `

### Cómo funciona – paso a paso

1. ** Tablas de frecuencias de construcción** – O(Princew1 sobrevivir+ sobrevivir)
`f1[i]` es el número de veces que aparece la letra `'a'+i` en `w1`;
`f2[i]` hace lo mismo por `w2`.

2. **Countar las letras únicas** – una carta es única si su frecuencia
es exactamente 1.
Esto nos da `uniq1` y `uniq2`.

3. **Early pruning** – if `responderuniq1 – uniq2 confidencial ≤ 2`, we can return `false `
inmediatamente.

4. **Enumerar todos los 26×26 pares** – por cada `a' que aparece en `w1`
y cada `b' que aparece en `w2' computamos el efecto sobre los dos
singular-letter cuenta usando la tabla anterior.
Todas las operaciones dentro de los bucles son tiempo constante, por lo que el total
tiempo es `26 × 26 = 676`, es decir **O(1)** con respecto a la cadena
longitudes.

5. **Retorno** – el primer par que rinde cuentas iguales es un éxito;
si agotamos todos los pares regresamos 'falso'.

-...

## Complexity

- **Tiempo** – `O( habitw1 vidas + tenciónw2 vidas)` para construir las tablas de frecuencia, más
el bucle constante 26×26 (Aplauso 676 pasos).
Así que el tiempo de funcionamiento general es lineal en el tamaño de entrada.

- **Espacio** - utilizamos dos arrays de longitud 26, es decir, `O(1)` adicional
memoria.

-...

## Takeaway

Usted no necesita probar cada posición en las cuerdas.
Porque sólo los tipos de letras* importan para las cuentas de letras únicas,
puede analizar el efecto de un solo intercambio en tiempo constante y
probar todos los '26 × 26` posibles pares de cartas. El resultado es un
algoritmo O(Principal) que es simple de implementar y fácil de implementar
Entiendo.