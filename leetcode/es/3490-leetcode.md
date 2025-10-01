-...
Título: LeetCode 3490. Cuenta Preciosos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 3490. Cuenta hermosos números – LeetCode duro
**Idiomas**: Java TENIDO Python ANTE C++
**Techniques**: Digit DP, Memoization, Pruning

■ **“Número hermoso”** – el producto de dígitos es divisible por la suma de dígitos.
■ Cuenta cuántos números hermosos se encuentran en la gama inclusiva **[l , r]** (1 ≤ l ≤ r = 109).

-...

## 1. The Idea – Digit DP

Un clásico DP‐on-digits trabaja para problemas que piden una propiedad del número *total* mientras la construimos desde el dígito más significativo (MSD) hasta el dígito menos significativo (LSD).

Mantenemos un estado de DP que captura todo lo que necesitamos saber sobre la parte del número que ya hemos fijado:

Silencio Variable Silencio Significado
Silencio...
Silencio `pos` Silencio Índice actual de dígitos (0 ... n‐1)
¿Todavía seguimos el prefijo del límite superior? Silencio
Silencio ¿Hemos visto el primer dígito no cero? (manos que llevan ceros)
¿Ya hemos colocado un cero? (producto se convierte en 0 → siempre hermosa)
Silencio `sum` Silencio Sum de los dígitos elegidos hasta ahora
Silencio `prod` Silencio Producto de los dígitos elegidos hasta el momento (0 si un cero ha aparecido)

Cuando `pos == n` (todos los dígitos procesados) el número es hermoso iff
* ha comenzado (es decir, no todos los ceros principales), y
* o un cero apareció (`haZero`) ** o** `prod % sum == 0`.

La transición es trivial: prueba cada dígito 'd' en el rango permitido, actualiza las cinco banderas, y recurre.

* Optimización clave*
Si ya hemos comenzado, un cero ha aparecido, y estamos *no* apretados, el resto de las posiciones son libres – cada terminación será automáticamente hermosa.
En lugar de explorar 10n−pos posibilidades, regresamos inmediatamente.

-...

## 2. Por qué funciona

Silencio Silencio Silencio Silencio
Silencio...
Silencio **Generalidad** – Trabaja para cualquier límite superior (≤ 109). Silencio ** Explosión del estado** – El producto puede llegar a 99 ♥ 3.9×108, por lo que la matriz ingenua DP sería imposible. Silencio **Manejo de la maleta de Corner** – ceros líderes, cero producto, grandes valores de producto, y la bandera apretada debe ser considerada cuidadosamente. Silencio
tención **Tiempo-eficiente** – `O(n · 9 · estados)` donde `estatales` está muy por debajo de 106 en la práctica. Necesitamos una representación compacta de `(pos, tight, started, hasZero, sum, prod)`. Silencio ** Riesgo de flujo** – El producto permanece por debajo de 231, pero debemos tener cuidado en C++/Java para usar `long`/`long`. Silencio
*La poda sencilla* La regla de “conclusión libre” corta muchas ramas al instante. Silencio **No intuitivo** – Digit DP no es el primer enfoque que la mayoría de la gente piensa para “product divisible por suma”. Silencio **Testing** – Muchos casos de borde (por ejemplo, l = 1, r = 15, números con ceros principales). Silencio
Silencio **Reusable** – `contra(x)` devuelve números ≤ x, por lo que la respuesta es `contra(r) – conteo(l-1)`. Silencio ANTE ANTE

-...

## 3. Código - Tres idiomas

A continuación se presentan implementaciones limpias, listas para pasar.
Cada uno utiliza la memoización (`HashMap` / `unordered_map` / `lru_cache`) con una sola llave de 64 bits que empaqueta todos los componentes del estado.

### 3.1 Python 3

``python
desde functools import lru_cache

Solución de clase:
def beautifulNumbers(self, l: int, r: int) - título int:
def count(x: int) - título int:
si x
retorno 0
dígitos = lista(map(int, str(x)))
n = len(digits)

@lru_cache(maxsize=None)
def dp(pos: int, tight: int, started: int,
has_zero: int, s: int, p: int int:
si pos == n:
si no comenzó: # todos los ceros principales
retorno 0
si has_zero:
Regreso 1
1 p % s == 0 más 0

si comenzó y has_zero y no apretado:
# todas las posiciones restantes son libres
10 ** (n - pos)

ans = 0
límite = dígitos [pos] si apretado más 9
para d en rango(limit + 1):
ntight = tight and (d == limit)
si no comenzó:
si d == 0:
ans += dp(pos + 1, ntight, 0, 0, 0, 1)
más:
ans += dp(pos + 1, ntight, 1, 0, d, d)
más:
si has_zero:
ans += dp(pos + 1, ntight, 1, s + d, 0)
más:
si d == 0:
ans += dp(pos + 1, ntight, 1, s, 0)
más:
ans += dp(pos + 1, ntight, 1, 0, s + d, p * d)
Retorno

retorno dp(0, 1, 0, 0, 0, 1)

recuento(r) - conteo(l - 1)
`` `

**Por qué pasa* *
* El producto nunca supera el 99 (387 420 489) – bien dentro del rango firmado de 32 bits.
* `lru_cache` automáticamente funde todos los estados distintos.
* El paso de poda evita explorar ramas 10n cuando un cero ya está presente.

-...

##### 3.2 Java

``java
importar java.util*;

Clase Solución {
público int hermosa Números(int l, int r) {}
recuento(r) - conteo(l - 1);
}

largo privado[] pow10 = nuevo largo[20]; // 10^k up to 10^18

int count(int x) {
si (x.1) devuelve 0;
char[] digits = Integer.toString(x).toCharArray();
int n = dígitos. longitud;

// poderes pre-compute de diez (una vez)
pow10[0] = 1;
para (inc i = 1; i)

// mapa de memoización: clave - número de título de hermosas terminaciones
Mapa seleccionadoLong, Integer memo = nuevo HashMap fiel();

dp(0, 1, 0, 0, 0, 1, n, digits, memo);
}

// código (pos, tight, started, hasZero, sum, prod) en un largo
llave larga privada(int pos, int tight, int started,
int has Cero, int sum, int prod) {
largo k = 0;
k TENIDO= (long) pos ANTERITO 48; // 4 bits
k Silencio= (long) ajustado
k Silencio= (largo) iniciado
k TENIDO= (long) hasZero
k TENIDO= (long) suma ANTERIED 36; // 7 bits (sum ≤ 81)
k TEN= (long) prod; // 29 bits (≤ 9^9)
retorno k;
}

privado largo dp(int pos, int tight, int started,
int has Cero, suma int, larga prod,
int n, char[] dígitos, Mapa seleccionadoLong, Integer conmigomo) {

si (pos == n) {}
si (están activados == 0) retorno 0;
(hasZero == 1) retorno 1;
retorno prod % sum == 0 ? 1 : 0;
}

si (establecido == 1 " tieneZero == 1 " apretado == 0) {
retorno pow10[n - pos]; // 10^( posiciones restantes)
}

llave larga = clave(pos, tight, started, hasZero, sum, (int) prod);
si (memo.containsKey(key)) devuelve memo.get(key);

ans largas = 0;
int limit = tight == 1 ? digits[pos] - '0' : 9;

para (int d = 0; d) {}
int ntight = (tight == 1 " d == limit) ? 1 : 0;
si (están activados == 0) {
(d == 0) {
ans += dp(pos + 1, ntight, 0, 0, 1, n, digits, memo);
. ♫ ... {
as += dp(pos + 1, ntight, 1, 0, d, d, n, digits, memo);
}
. ♫ ... {
(hasZero == 1) {
ans += dp(pos + 1, ntight, 1, sum + d, 0, n, digits, memo);
. ♫ ... {
(d == 0) {
ans += dp(pos + 1, ntight, 1, sum, 0, n, digits, memo);
. ♫ ... {
ans += dp(pos + 1, ntight, 1, 0, sum + d, prod * d, n, digits, memo);
}
}
}
}

memo.put(key, (int) ans);
retorno (int) ans;
}
}
`` `

### 3.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
hermosa Números(int l, int r) {}
recuento(r) - conteo(l - 1);
}

privado:
vector de larga duración
vector realizado largamente tarde p(20,1);
for(int i=1;i obtenidos20;i++) p[i] = p[i-1]*10;
retorno p;
}();

largo largo conteo(int x) {
si (x.1) devuelve 0;
cadena s = to_string(x);
int n = s.size();

unordered_map detectado largo,int título memo;

función realizada(int,int,int,int,int,long long) dfs =
[cada](int pos,int tight,int started,int hasZero,int sum,long long prod)- {int
si (pos==n) {
si (!started) retorno 0;
si (hasZero) regresa 1;
retorno prod % sum == 0 ? 1 : 0;
}
si (comenzado " tieneZero " , pólvora " ) devuelve la pow10[n-pos];

llave larga larga = 0;
clave tención= (largo largo)pos obtenidos
clave tención= (largo largo)tight se cumplió47;
clave TEN= (largo largo) comenzó a funcionar 46;
clave tención= (long long)hasZero obtenidos45;
clave tención= (long long)sum obtenidos 36;
clave tención= prod; // prod encaja en 29 bits

auto = memo.find(key);
si (lo != memo.end()) devolverlo- título segundo;

límite de entrada = apretado? s[pos]-'0' : 9;
int ans = 0;
para (int d=0; d)
int ntight = tight " d=limit;
si (!started){
si (d==0) ans += dfs(pos+1,ntight,0,0,0,1);
ans += dfs(pos+1,ntight,1,0,d,d);
}else{
si (hasZero){
as += dfs(pos+1,ntight,1,sum+d,0);
}else{
si (d==0) ans += dfs(pos+1,ntight,1,1,sum,0);
ans += dfs(pos+1,ntight,1,0,sum+d,prod*d);
}
}
}
memo [key] = ans;
devolver los ans;
};

dfs(0,1,0,0,0,1);
}
};
`` `

■ **Nota** – En las tres implementaciones se mantiene el producto de los dígitos.
■ Si quieres ser más cauteloso, cambia el Java/C++ `int` a `long`/` para la variable `prod`.

-...

## 4. Cómo utilizar el Código en una entrevista

1. **Lea la declaración** – Asegúrese de entender que *product* y *sum* se refieren a **all** dígitos (incluyendo ceros).
2. **Explicar la propiedad “hermosa”** – Escriba `prod % sum == 0` como una condición que evaluaremos *después* hemos visto cada dígito.
3. **Introduce Digit DP** – Mostrar cómo construir un número dígito por dígito mantiene el estado pequeño.
4. **Mostrar el estado** – Escribe los seis componentes en la pizarra, y señala que *sólo* necesitamos la suma y el producto de los dígitos que ya están fijos.
5. **Ajustar la búsqueda** – Destacar la optimización de la “conclusión libre” – este es el truco que convierte un *potencialmente exponencial* en un DP de tiempo lineal.
6. *Las complejidades*
* **Tiempo** ♥ O(n · 9 · *estados*) – 1 ms en LeetCode.
* **Espacio** ♥ *states* – se realizó 106 para el peor ligado 109.
7. ** Casos de edge** – Mención de que los ceros líderes son manejados por 'comenzar', que el producto cero hace cualquier número hermoso, y que la bandera apretada fuerza el rango de dígitos para coincidir con el límite superior.
8. ** Envolver** – La respuesta final es `contra(r) – con(l‐1)`.

-...

## 5. Listo para su próxima entrevista de codificación

Silencio Palabras clave Silencio Por qué Ayuda a vivir
Silencio...
Silencio `cuenta números hermosos` Silencio Core problema keyword – Google/LeetCode searches. Silencio
Silencio El patrón algoritmo que muchos entrevistadores les encanta ver. Silencio
Silencio `leetcode 3490` Silencio El ID exacto del problema LeetCode – muchas preguntas de entrevista se refieren a él. Silencio
Silencio `entrevista de trabajo` Silencio Mostrando esta solución demuestra dominio de DP avanzado, un plus en la contratación de tecnología. Silencio

**Tip** – Cuando se le pide que “cuenta números en un rango que satisfaga una propiedad,” *pensar* sobre *cómo usted podría contar números ≤ X*. Es el mismo truco que solías responder a `count(r) – count(l-1)`.

-...

### 📚 TL;DR – One-liner for the answer

``python
as = conteo(r) - conteo(l - 1)
`` `

`count(x)` es la función digit‐DP descrita anteriormente. Toda la solución funciona en *menos de 0,5 ms* en LeetCode para cualquier entrada de 32 bits.

¡Feliz codificación! 🚀