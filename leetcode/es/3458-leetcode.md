-...
Título: LeetCode 3458. Seleccione K Disjoint Subestrings especiales -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Para que una subestring sea *valida* cada personaje que ocurre dentro de la subestring debe tener **todo** de su
ocurrencias dentro de la misma subestring.
En otras palabras:

`` `
para cada personaje x en la subestring
primer[x] >= start_of_substring
última[x]
`` `

Toda la cadena en sí nunca se cuenta como una subestring válida.



----------------------------------------------------

##### 1. Observaciones

* El inicio de una subestring válida sólo puede ser la primera ocurrencia ** de un personaje.
(Si el comienzo fuera en otro lugar, el mismo personaje aparecería dentro del
subestring y su primera ocurrencia estaría fuera – violando la regla.)

* El final de una subestring válida es la última ocurrencia** de algún personaje que
yace dentro.
Cuando tratamos de construir una subestring desde una posición de inicio `i`, nosotros
primer vistazo a la última ocurrencia de `s[i].
Si bien la ampliación del final actual a la derecha tal vez tengamos que incluir
caracteres adicionales cuya última ocurrencia está más allá del final actual.
Si un personaje dentro del intervalo tiene una primera ocurrencia *antes* `i`,
entonces todo este intervalo es imposible – simplemente saltamos.

* Después de conocer todos los intervalos válidos `[l, r]`, el problema se convierte en
seleccionando el número máximo de intervalos no superpuestos.
Este es un problema codicioso clásico: ordenar todos los intervalos por `r`
(Termino más temprano primero) y repetidamente elegir el siguiente intervalo que comienza
después del final del último elegido.



----------------------------------------------------

##### 2. Algoritm
`` `
si k == 0 → verdadero

1. Escanear la cadena una vez y almacenar
primero[26] – primer índice de cada personaje
último[26] – último índice de cada personaje

2. Por cada posición i que es la primera ocurrencia de su carácter
(i == first[s]) :

final = último[i] // final candidato
// Ampliar el final para cubrir cada personaje dentro
para pos = i ... final:
final = max(end , last[s])

// Verificación de validez – ningún personaje dentro puede comenzar fuera [i , final]
ok = verdadero
para pos = i ... final:
si primero [s[pos]]
si !ok → continuar
si i=0 y end==n-1 → continuar // cadena entera no está permitido

intervalo de la tienda [i , final]

3. Ordenar todos los intervalos almacenados por su punto final derecho.

4. Selección graciosa de intervalos no superpuestos
último Fin = 1
elegido = 0
para cada intervalo [l , r] en orden ordenados
si yo soy el último Final
elegido++, último Fin = r
retorno (elegido >= k)
`` `

----------------------------------------------------

##### 3. Prueba de corrección

Demostramos que el algoritmo devuelve `true`
si la cadena contiene al menos 'k` subestrings válidos no superpuestos.

-...

##### Lemma 1
Por cada personaje `c` todas sus ocurrencias se encuentran en uno de los intervalos
construido por el algoritmo.

Proof.

Durante el paso 1 computamos `primer[c]` y `último[c]`.
Cuando nos encontramos con una posición " que equivale a " primera[c] " ,
el algoritmo expande el final del candidato hasta que contiene cada
carácter cuya última ocurrencia está dentro del intervalo actual.
Así el intervalo final `[i , final]` contiene todos los casos de cada
carácter apareciendo dentro.
En particular, contiene todos los casos de " c " .
Por lo tanto, toda la gama [primer[c] , último[c] `
está completamente cubierto por un intervalo construido (posiblemente junto con otros
caracteres). ∎



##### Lemma 2
Cada intervalo producido por el algoritmo es una subestring válida
según la definición del problema.

Proof.

Tome cualquier intervalo producido `[i , final]`.
Durante su construcción realizamos dos cheques:

1. *Expansion* – después del primer lazo ampliamos `end` hasta cada uno
carácter interior `[i , end]` tiene su última ocurrencia ≤ `end`.
Así por cada personaje `x` dentro del intervalo
`primer[x] ≥ i` y `último[x] ≤ final`.

2. *Validez* – en el segundo lazo comprobamos que ningún personaje
dentro tiene una primera ocurrencia ``.
Combinado con la propiedad anterior, para cada personaje `x`
en la subestring
`primer[x]` y `último[x] `` mienten dentro de `[i , final]`.

Por lo tanto la subestring satisface la definición de una subestring válida.
∎



##### Lemma 3
El procedimiento codicioso en el paso 4 selecciona el número máximo posible de
intervalos no superpuestos entre todos los intervalos construidos.

Proof.

Los intervalos se clasifican al terminar el tiempo.
La prueba estándar del algoritmo codicioso de programación del intervalo
muestra que para un conjunto de intervalos ordenados por tiempo de acabado,
elegir el primer intervalo de acabado que no se superpone con el
previamente elegido uno produce una solución óptima.
El algoritmo en el paso 4 es exactamente ese algoritmo codicioso. ∎



##### Lemma 4
Si el algoritmo devuelve `true`, la cadena contiene al menos `k`
subestrings válidos no superpuestos.

Proof.

`verdad ' se devuelve sólo cuando la selección codiciada en el paso 4 eligió al menos
intervalos.
Por Lemma 2 cada intervalo elegido es una subestring válida, y por
Lemma 3 estos intervalos son pares sin superposición.
Por lo tanto existen al menos 'k' subestrings válidos y no superpuestos. ∎



##### Lemma 5
Si la cadena contiene al menos 'k' no superposición de subestrings válidos,
el algoritmo devuelve `true`.

Proof.

Que las subestrings " k " sean `T1 , T2 , ... , T_k`
y ordenarlos por sus posiciones de inicio.
Por Lemma 1 cada ocurrencia de cada personaje se encuentra en uno de los
intervalos producidos por el algoritmo, por lo tanto cada 'T_i' aparece
en la lista de intervalos.
Por Lemma 2 cada intervalo listado es una subestring válida.
Puesto que el T_i no está superpuesto,
el conjunto de intervalos que los contiene es un calendario factible.
Por Lemma 3 el algoritmo codicioso seleccionará **al menos** tantos
intervalos como cualquier calendario factible, por lo tanto, seleccionará por lo menos `k `
intervalos y el algoritmo devuelve `true`. ∎



################################################################################################################################################################################################################################################################ Theorem
El algoritmo devuelve `true`
si la cadena de entrada contiene al menos 'k' no superposición válida
subestrings.

Proof.

*Si la parte*:
`true` ⇒ by Lemma 4 la selección codiciada eligió por lo menos 'k'
intervalos no superpuestos, cada uno de ellos es una subestring válida
(Lema 2).
Así la cuerda contiene al menos 'k' tales subestrings.

*Sólo si parte*:
Supongamos que la cadena contiene al menos 'k' subestrings válidos no superpuestos.
Todos ellos están entre los intervalos construidos
(Lema 1 y Lemma 2).
El algoritmo codicioso (Lemma 3) encuentra el número máximo de
intervalos no superpuestos entre ellos,
≥ " k " .
En consecuencia, el algoritmo devuelve `true`. ∎



----------------------------------------------------

##### 4. Análisis de la complejidad

`` `
Paso 1 : O(n)
Paso 2 : cada posición se visita al máximo una vez al ampliar el final
→ O(n) (total en todos los inicios)
Paso 3 : ordenar O(m log m) (m - número de intervalos, m ≤ n)
Paso 4 : O(m)
`` `

`m` nunca excede `n`, por lo que el tiempo de funcionamiento general es **O(n)* *
y el consumo de memoria es **O(n)**.



----------------------------------------------------

##### 5. Aplicación de referencia (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
// Regresar verdadero si por lo menos k no superposición subestrings válidos existen
bool maxSubstringLength(string s, int k) {
si (k <= 0) retornar verdadero; // caso de borde

int n = (int)s.size();
vector implicado primero(26, n), último(26, -1);

--------- 1. primera / última posición -------- */
para (int i = 0; i) {}
int c = s [i] - 'a';
si (primero[c] == n) primero[c] = i;
[c] = i;
}

--------- 2. construir todos los intervalos válidos -------- */
vectores obtenidospair realizados,intenta intervalos de confianza; // [l , r]
para (int i = 0; i) {}
int ch = s [i] - 'a';
si (primero [ch]!= i) continuar; // sólo comenzar en el primer occ.

int end = last[ch]; // final candidato
para (int pos = i; pos <= end; ++pos)
final = max(end, last[s] - 'a')); // expander para cubrir todos

/ / / validez de verificación - ningún char dentro comienza antes de que yo
bool ok = verdadero;
para (int pos = i; pos <= end; ++pos) {
int c = s[pos] - 'a';
si (primero[c] i) { ok = falso; romper; }
}
si (!ok) continuar;
si (i == 0 " punto final == n - 1) continuar; // cadena entera no se permite

intervalos.emplace_back(i, end);
}

--------- 3. ordenar al terminar el tiempo...
(intervalos.begin(), intervalos.end(),
[](cont auto simultáneamente a, const auto simultáneamente b){ devolver a.second iere b.second; });

--------- 4. programación de intervalos codiciosos...
int chosen = 0;
el último Fin = -1;
para (auto &iv : intervalos) {}
si (iv.first  Conf LastEnd) {
++elegido;
último Fin = iv.segundo;
si (elegidos >= k) regresan verdadero; // salida temprana
}
}
devolver falso;
}
};
`` `

El código sigue exactamente el algoritmo probado correcto arriba y
se ajusta a la norma C+17.