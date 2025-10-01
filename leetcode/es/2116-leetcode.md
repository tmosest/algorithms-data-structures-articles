-...
Título: LeetCode 2116. Compruebe si una crianza de los padres puede ser válida -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
*Problema*

Te dan dos cuerdas de la misma longitud

* `s` – sólo los personajes `('' y `')'
* `locked` – a string of `'0'` and `'1'`.
`bloqueado[i] == '1' significa que `s[i]` es *fixed* – no puede ser cambiado.
`bloqueado[i] == '0' significa que `s[i]` es *gratuito* – puede reemplazarlo por cualquiera
``.

¿Puede cambiar cada posición libre para que toda la cuerda se convierta en un *válido*
parentheses string (properly matched)?

----------------------------------------------------

##### 1. Observaciones

* Una cadena de paréntesis válida debe tener incluso longitud – de lo contrario es
imposible emparejar cada abertura con un soporte de cierre.

* Mientras escaneamos la cadena de izquierda a derecha podemos hacer un seguimiento de cuántos
Soportes de apertura fijos hemos visto menos los soportes de cierre fijos.
Que esto sea "balance".
Cada posición gratuita se puede utilizar como soporte de apertura (o más tarde
como uno de cierre) – en el momento sólo sabemos que puede ayudar
cubrir un déficit.

Si en algún prefijo "balance + libre" 0` ya tenemos más cierre
corchetes de los que podemos cubrir – la cadena nunca puede ser válida.

* La misma lógica debe mantenerse al escanear de derecha a izquierda,
pero ahora miramos los soportes de cierre *fijo* menos la apertura fija
Entre corchetes.
Cada vez que el déficit de los corchetes de cierre supera el número libre
posiciones en ese sufijo, un soporte de apertura fijo permanecerá sin igual.

Si **ambos ** terminan sin una contradicción, siempre podemos asignar el
corchetes libres de una manera que la cadena final es válida.

----------------------------------------------------

##### 2. Algoritm

`` `
canBeValid(s, bloqueado)
n ← longitud de s
si n es extraño → devolver falso / / / / / una cadena válida debe ser

// ----- izquierda → paso derecho ---
balance ← 0 // fijo '(' – fijo ') '
freeLeft ← 0 // posiciones libres vistos hasta ahora
para i = 0 ... n- 1
si está bloqueado [i] == '0'
gratis Izquierda ← libreIzquierda + 1
si s[i] == '(
balance ← balance + 1
// s[i] == ') '
equilibrio ← – 1

if balance + freeLeft
devolver falso // demasiados fijos ') ' ya

// ----- derecha → paso izquierdo ---
balance ← 0 // fijo ') - fijo '( '
freeRight ← 0
para i = n-1 ... 0
si está bloqueado [i] == '0'
gratis Derecho ← gratisRight + 1
si s[i] == ' '
balance ← balance + 1
// s[i] == '(
equilibrio ← – 1

si el saldo + libre
devolver falso // demasiados fijos '(' ya

retorno verdadero
`` `

----------------------------------------------------

##### 3. Prueba de corrección

Demostramos que el algoritmo devuelve `verdad ' si la cadena se puede hacer
válido.

-...

##### Lemma 1
Durante el paso izquierdo a derecha, para cada prefijo 'P' de la cuerda,
`balance(P) + freeLeft(P) ≥ 0` hold *iff* es posible reemplazar todo
free positions inside `P` so that no closing bracket in `P` is unmatched
al leer de izquierda a derecha.

Proof.

*Si parte. *
Suponga `balance(P) + freeLeft(P) 0`.
`balance(P)` es el número de fijos `(''' menos fijos `')' en `P`.
`freeLeft(P)` cuenta las posiciones libres, que podemos decidir más adelante.
Incluso si nos volvemos **todos** posiciones libres en `'('', el número neto de
entre corchetes de cierre en " P " ,
"- (balance(P) + freeLeft(P)) " .
Por lo tanto, habría al menos una `''' inigualable'' – imposible.

Sólo si parte. *
Asume `balance(P) + freeLeft(P) ≥ 0`.
Podemos asignar `balance(P) + freeLeft(P)` de las posiciones libres en `P`
como `'(', y el resto como `')'.
El saldo neto resultante después de este prefijo es exactamente
`balance(P) + (balance(P) + freeLeft(P) - freeLeft(P) = 0`
o positivo, así que ningún `')' puede ser inigualable. ∎



##### Lemma 2
Durante el paso derecho a izquierda, por cada sufijo de la cuerda,
`balance(S) + freeRight(S) ≥ 0` hold *iff* es posible reemplazar todo
free positions inside `S` so that no opening bracket in `S` is unmatched
al leer de derecha a izquierda.

*La prueba es simétrica a Lemma Convennbsp;1.*



################################################################################################################################################################################################################################################################ Theorem
El algoritmo devuelve `verdad` si existe una manera de reemplazar a todos
posiciones libres de `s` para que la cadena resultante sea válida
paréntesis.

Proof.

*Si el algoritmo devuelve `true`.*
Ambos pases nunca violaron las desigualdades, por lo tanto por Lemma plaganbsp;1 y
Lemma limitadanbsp;2 todo prefijo puede ser hecho libre de '') sin igual y cada uno de los
el sufijo se puede hacer libre de `'('`.
Debido a que la longitud de la cuerda es incluso, el número total de `(' iguala el
número de `''''' después de elegir los caracteres libres apropiadamente.
Por lo tanto existe una asignación completa y toda la cuerda se puede hacer
válido.

*Si el algoritmo devuelve `false`. *
El algoritmo se detiene en el primer prefijo `P` o sufijo `S` donde el
La desigualdad falla.
Por Lemma implicabsp;1 o Lemma implicanbsp;2, ninguna asignación de las posiciones libres puede
eliminar el soporte sin igual en ese prefijo/suffix.
En consecuencia, no existe una asignación válida para toda la cadena. ∎



----------------------------------------------------

##### 4. Análisis de la complejidad

TEN TERRITOR TEN SON ANTERIOR ANTERIOR TERRITORIO
Silencio----------Prince----------------
tención de la duración de la verificación Silencio O(1)
Silencio Izquierda a la derecha pasar Silencio O(n)
← Right‐to‐left pass Silencio O(n) Silencio O(1)
Silencio **Total** Silencio**

----------------------------------------------------

##### 5. Aplicación de referencia (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
bool canBeValid(string s, string locked) {}
int n = s.size();
si (n % 2 != 0) devolver falso; // debe ser incluso

// izquierda → derecha
int bal = 0; // fijo '(' - fijo ') '
int freeLeft = 0; // número de puestos libres vistos hasta ahora
para (int i = 0; i) {}
si (bloqueado[i] == '0')
++freeLeft;
si (s[i] == '(')
++bal;
// s[i] == ') '
-bal;

si (bal + freeLeft) devuelto falso;
}

// derecha → izquierda
bal = 0; // fijo ')' - fijo '( '
int freeRight = 0;
para (int i = n - 1; i 0; --i) {
si (bloqueado[i] == '0')
++libreLa derecha;
si (s[i] == ')
++bal;
// s[i] == '(
-bal;

si (bal + libreRight 0) devolver falso;
}

retorno verdadero;
}
};
`` `

----------------------------------------------------

##### 6. Prueba rápida

`` `
s = "(((())))"
bloqueado = "111111" → verdadero // ya válido

s = "(((())))"
bloqueado = "110110" → falso // a fijo ') no se puede cubrir

s = "())("
bloqueado = "0000" → verdadero // asignar "(())"

s = "(()))("
bloqueado = "000000" → falso // ninguna asignación puede balance
`` `

El programa sigue exactamente el algoritmo probado correcto arriba
y satisface el tiempo de `O(n)` / `O(1)` requisito espacial.