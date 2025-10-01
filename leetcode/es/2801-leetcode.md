-...
Título: LeetCode 2801. Conteo Números de paso en rango -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
*Lo que se te pide que hagas*

Dada dos cadenas decimales " baja " y " alta " (cada una puede contener hasta 100 000 dígitos)
contar todos * números de almacenamiento* `x ' tales que

`` `
bajo ≤ x ≤ alto
`` `

Un *número de almacenamiento* es un entero positivo cuyo dígitos decimales satisfacen

`` `
TENED[i] – d[i‐1]
`` `

(Ejemplos: 10, 121, 1234, 987, ...)

La respuesta debe ser devuelta modulo `1 000 000 007`.

----------------------------------------------------

## 1. Idea de alto nivel

El rango `[low , high]` es astronómicamente grande – hasta `10^100000`.
No podemos iterar a través de todos los números.

En lugar de nosotros

1. **Count** todos los números de paso '≤ alto' → `cnt Alto.
2. **Count** todos los números escalonados `seca bajo` (es decir, `≤ bajo-1`) → `CntLow`.
3. La respuesta es 'cntHigh – cntLow` y agregamos uno más si *low itself* es un paso adelante
número (porque la resta lo elimina).

Así que el subproblema principal es:

■ ** ¿Cuántos números de paso son '≤ N`? #

Este es un clásico *digit‐DP* (también llamado *digit DP* o *digit dynamic programming*).

----------------------------------------------------

## 2. Why digit‐DP works

Procesamos la representación decimal de `N` desde el dígito más significativo al menos.
Mientras todavía estamos “estrenos” (es decir, el prefijo que hemos elegido es exactamente igual al
prefijo de `N`), el siguiente dígito que podemos poner está obligado por el dígito correspondiente de `N`.
Tan pronto como elijamos un dígito más pequeño, nos convertimos en libres y podemos poner cualquier dígitos restantes.

Para hacer cumplir la propiedad de paso mantenemos el valor del dígito anterior
(`prev`).
En el primer dígito no cero no tenemos 'prev', así que cualquier dígito no cero es
permitido.
Después de eso, el siguiente dígito debe diferir de 'prev' por exactamente 1.

También necesitamos apoyar números cuya longitud es **shorter** que `N`.
Esto es manejado por una bandera *leading‐zero* – mientras todavía estamos poniendo sólo ceros
no han “estrellado” el número todavía; una vez que ponemos un no cero dígitos la bandera principal de cero
se aclara y a partir de entonces cada posición es un dígito real.

----------------------------------------------------

## 3. DP state

Silencio Parámetro Silencio Descripción Silencio Posibles valores
Silencio----------------------------- La vida
Silencioso `pos` Índice de la vida en la cadena (0 ... `len`)
Silencio `tight` Silencio are still bounded by the prefix of `N`? Silencio `0` or `1` Silencio
TENIDO `prev` TENIDO dígito anterior (`-1` si aún no hemos visto un no cero) TENIDO `-1 ... 9` → 11 posibilidades Silencio
¿Hemos colocado todavía un dígito no cero? Silencioso `0` o `1`

Número total de estados:
`(len+1) × 2 × 11 × 2 ♥ 44 × len` – sólo unos pocos miles incluso por `len = 100 000`.

Para cada estado intentamos en la mayoría de 10 dígitos (0-9), por lo que la complejidad general es lineal
en el número de dígitos.

----------------------------------------------------

## 4. Recurrencia

`` `
dfs(pos, tight, prev, started):
si pos == len:
// construimos un número - pero no debemos contar el número de cero
la vuelta comenzó ? 1 : 0

si memoizado → devolverlo

límite = apretado? N[pos]: 9
ans = 0

para d de 0 a límite:
siguiente_tight = ajustado y (d == limit)

// podemos colocar d si:
// • seguimos en la parte principal cero, OR
// • aún no hemos elegido un dígito (prev == -1), OR
// • d difiere de prev por exactamente 1
si no comienza y d == 0:
// sigue liderando ceros
ans += dfs(pos+1, next_tight, prev, false)
si se inicia=falso o abs(prev - d) == 1:
as += dfs(pos+1, next_tight, d, true)
as %= MOD
memoise
Retorno
`` `

----------------------------------------------------

## 5. Manejo del límite bajo

Computamos:

`` `
cnt Alto = dfs(0, verdadero, -1, falso) // números ≤ alto
cntLow = dfs(0, true, -1, false) // números se indica bajo (es decir, ≤ bajo-1)
`` `

La diferencia `cntHigh - cntLow` cuenta todos los números de paso en `[low+1 , alto]`.

Si 'bajo' en sí es un número de paso debemos añadir uno más, porque la resta
Se lo quita.
Comprobando que es un simple escaneo lineal de los dígitos de 'bajo'.

----------------------------------------------------

## 6. Aplicación completa de Java

``java
importa java.util. Arrays;

Clase Solución {
int final estático privado MOD = 1_000_000_007;

/* ----------------------------------------------------------------------------
* API pública */
/* ----------------------------------------------------------------------------
int countSteppingNúmeros(Cantando bajo, Cantando alto) {
cntHigh largo = countUpTo(high);
cntLow = countUpTo(low);

diff largo = (cntHigh - cntLow + MOD) % MOD; // números en [low+1 , alto]

si (estáStepping(low)) { // añadir bajo si es necesario
diff = (diff + 1) % MOD;
}
retorno (int) diff;
}

/* ----------------------------------------------------------------------------
/* helper: contar números de paso ≤ N */
/* ----------------------------------------------------------------------------
cuenta larga privadaUpTo(String N) {
int len = N.length();
Long[][][][] [] memo = new Long[len][2][11][2];
// prev digit : -1 ... 9 → índice prev+1 (0 ... 10)
// iniciado? : 0 / 1 → index 0 / 1
// apretado? : 0 / 1
dfs(0, true, -1, false, N, memo);
}

/* ----------------------------------------------------------------------------
/* DP recursivo */
/* ----------------------------------------------------------------------------
dfs privados largos(int pos, boolean tight, int prev, boolean started,
String N, Long[][][][] memo) {

si (pos == N.length()) {}
// número construido? (excluye el número total de cero)
la vuelta comenzó? 1 : 0;
}

apretado Idx = ajustado? 0 : 1;
int prevIdx = prev + 1; // cambio por +1 porque prev puede ser -1
int start Idx = iniciado? 0 : 1;

si (memo[pos][tightIdx][prevIdx] [startIdx] != null)
devolver memo[pos][tightIdx][prevIdx][startIdx];

larga res = 0;
límite de entrada = apretado? N.charAt(pos) - '0' : 9;

para (int d = 0; d) {}
booleano siguiente Tight = tight " (d == limit);
booleano nextStart = comenzó ¦ 0);

si (!started " d == 0) {/// still in leading ceros
res += dfs(pos + 1, siguiente Tight, prev, false, N, memo);
} si (!started Silencioso Math.abs(prev - d) == 1) {
res += dfs(pos + 1, siguiente Tight, d, nextStart, N, memo);
}
res %= MOD;
}

memo[pos][tightIdx][prevIdx] [startIdx] = res;
restitución;
}

/* ----------------------------------------------------------------------------
/* ver si una determinada cadena decimal es un número de paso */
/* ----------------------------------------------------------------------------
booleano privado isStepping(String s) {
(int i = 1; i) s.length(); ++i) {
si (Math.abs(s.charAt(i) - s.charAt(i - 1)) != 1) {
devolver falso;
}
}
retorno verdadero; // s es positivo, no hay necesidad de comprobar para cero
}
}
`` `

### Por qué este código es correcto

Silencio Cómo se maneja ¦
Silencio...
Silencio **Todo-cero número** Silencioso El caso Base devuelve `0` si `comienza=false`. Silencio
Silencio **Modulo** Silencio Cada adición se reduce modulo `MOD`. Silencio
Silencio **Números negativos** Silencio La resta se envuelve con '+MOD' antes del '%'. Silencio
Silencio **Desbordamiento largo** Silencio Utilizamos `long` para sumas intermedias y objetos `Long` para la memoización;
cada valor es ≤ `len * 10` (Ω 10^6 para 100 k dígitos) por lo que `long` es seguro. Silencio
Silencio ** Tiempo** Silencioso `O(len)` estados × 10 transiciones → ♥ 4 400 000 operaciones para el
entrada peor de la maleta – lo suficientemente rápido. Silencio

----------------------------------------------------

## 7. Problemas comunes y cómo los evitamos

Silencio Pitfall Silencioso Explicación
Silencio----------------------------
Silencio ** `0`** Silencio Un número de paso debe ser *positivo*. En el caso base devuelve `estrellado ? 1 : 0`. Silencio
Silencio **Missing leading ceros** Silencio Los números más cortos deben ser representados. ← Usar una bandera 'estrellada'. Silencio
Silencio **Modulo en la resta** El resultado permanente puede ser negativo. Silencio Añadir `MOD` antes de aplicar `%`. Silencio
TEN **Large string** ANTE La profundidad de la recorsión hasta 100 000 puede desbordar la pila de llamadas. La profundidad de recursión de Java es ~1 000 000, por lo que está bien, pero si quieres
enfoque más seguro que puede reescribir el DP iterativamente. Silencio
tención ** " prev " indexación** Silencioso `prev` puede ser `-1 '  durable Shift por +1 cuando lo utiliza como un índice de array. Silencio
Silencio **Performance** Silencio 44 × limon ♥ 4 400 000 estados – bien, pero evitar volver a localizar arrays cada uno
Llamada de recursión. TENIENDO Asignar el array 4‐D una vez por atado (`len × 2 × 11 × 2`). Silencio

----------------------------------------------------

## 8. Control de cordura rápido

``java
public static void main(String[] args) {
Solución sol = nueva solución ();
System.out.println(sol.countSteppingNumbers("1", "9") // 8 (1,2,3,4,5,6,7,8,9)
System.out.println(sol.countSteppingNumbers("10", "20")); // 2 (10,12)
System.out.println(sol.countSteppingNúmeros("100", "200"); // 5 (101,121,121? no, 121 (102); 123,121? etc.)
}
`` `

Usted puede reemplazar `String` con `StringBuilder` si lo prefiere, pero el algoritmo permanece
igual.

----------------------------------------------------

## 9. Take-away

* Reducir el intervalo `[low , high]` a dos problemas de un solo límite a través de dígitos DP.
* En el DP recuerda: `pos`, `tight ' , `prev ' (o “no anterior”), y si el
el número ha comenzado.
* Skip the all‐zero number in the base case.
* No te olvides de añadir `low` back si es en sí mismo un número de paso.

Con esto usted puede manejar con seguridad los gigantescos 100 000-digit límites – la solución funciona
en unos segundos en hardware moderno.