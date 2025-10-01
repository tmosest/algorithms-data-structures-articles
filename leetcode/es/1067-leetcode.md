-...
Título: LeetCode 1067. Cuenta de dígitos en rango -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. LeetCode 1067 – **Cuento de dígitos en rango* *
**Problema** Silencioso `public int digits Conde(int d, int low, int high) `
# Dificultad**

■ ** Objetivo** – Para un solo dígito `d (0‐9)` y un rango inclusivo `[bajo, alto]`, devuelve el número total de veces `d` aparece en las representaciones decimales de cada entero en ese rango.
■ **Constraints** – `1 ≤ bajo ≤ alto ≤ 2·108` (Atención 200 millones).

Debido a que el rango de entrada puede ser enorme, un bucle ingenuo (`para (int i=low;i observado=high;i+) ...`) sería demasiado lento. La solución estándar utiliza **digit‐DP** – una técnica de programación dinámica que procesa los dígitos decimales de un número de lo más significativo a lo menos significativo, manteniendo el seguimiento de estados “tight” y “leading‐zero”.

A continuación encontrará implementaciones de trabajo, anotadas en **Java, Python, y C++** que se ejecutan en 'O(log N) ' tiempo y 'O(log N) ' memoria.

-...

## 2. Java Implementation (Digit‐DP)

``java
*
* LeetCode 1067 – Digit Count in Range
*
* Java 17, O(log N) time, O(log N) Memory
*/
Clase Solución {
// Memoization table: pos x count
int privado[][] memo;
blanco int privado; // dígito estamos contando
char privada[] dígitos; // representación de cadena del número actual

dígitos int públicos Conde(int d, int low, int high) {
esto. objetivo = d;
recuento de retornoUpTo(high) - countUpTo(low - 1);
}

* Cuenta los casos de objetivo en [0, n] */
int countUpTo(int n) {}
si (n 0) regresa 0; // guardia para bajo-1
dígitos = Integer.toString(n).toCharArray();
int len = dígitos. longitud;
memo = nuevo int[len]; // ocurrencias máximas
for (int[] row : memo) Arrays.fill(row, -1);
devolver dp(0, 0, true, false);
}

*
* @param pos current index in digits[]
* @param cnt número de dígitos de destino vistos hasta ahora
* @param apretado si los dígitos anteriores coinciden con el prefijo de n
* @param comenzó si hemos colocado un dígito cero aún
* @return total target‐digit sucesos de este estado en adelante
*/
int privado dp(int pos, int cnt, boolean tight, boolean started) {}
si (pos == dígitos.length) cnt de retorno; // extremo del número
si (!tight " empieza " memo[pos][cnt]!= -1) // Cache hit
devolver memo[pos][cnt];

límite de entrada = apretado? dígitos [pos] - '0' : 9;
total = 0;

// Opción 1: saltar esta posición (todas las ceros principales)
si (!started) total += dp(pos + 1, cnt, false, false);

int start Digit = iniciado? 0 : 1; // no plomo cero permitido después de inicio
para (int d = startDigit; d) {}
nuevo Cnt = cnt + (d == target? 1 : 0);
boolean newTight = tight " (d == limit);
total += dp(pos + 1, newCnt, newTight, true);
}

si (!tight ' iniciado) memo[pos][cnt] = total;
Total de retorno;
}
}
`` `

### Cómo funciona

Silencio ¿Qué pasa?
Silencio...
Silencio `digitsCount` ANTE Calls helper for `high` and `low-1`, then subtracts. Silencio
Silencio `countUpTo` Silencio convierte `n` a char array, prepara memo, llama `dp`. Silencio
Silencio `dp` Silencio Explora Recursivamente todos los dígitos posibles en la posición `pos`. Silencio
TENIDO Estado TENIDO `(pos, cnt, tight, started)` Silencio
← Memoization Silencio Tiendas resultados para * estados no rectos* para evitar la recomputación. Silencio

El algoritmo visita la mayoría de los estados `len * len` (`len ≤ 10` para 2·108), por lo que es prácticamente tiempo constante.

-...

## 3. Aplicación de Python (Uno-Line DP)

``python
# LeetCode 1067 – Cuenta de dígitos en rango
# Python 3.11, O(log N) time, O(1) Memory (explicitly using recursion limits)
Solución de clase:
def digits Conde(self, d: int, low: int, high: int) int:
volver a sí mismo.f(alto, d) - self.f(low - 1, d)

def f(self, n: int, target: int) - int:
si no se hizo 0: retorno 0
s = str(n)
m = len(s)
memo = [-1] * (m + 1) para _ en rango(m)]

def dp(i: int, cnt: int, tight: bool, started: bool) int:
si yo == m:
retorno cnt
si no apretado y comenzado y memo[i][cnt] != -1:
memo[i][cnt]
arriba = int(s[i]) si apretado mas 9
res = 0
si no comenzó:
res += dp(i + 1, cnt, False, False) # skip digit
para cavar en rango(0 si se inicia otro 1, arriba + 1):
res += dp(i + 1, cnt + (dig == target), ajustado y cava == arriba, True)
si no apretado y comenzado:
memo[i][cnt] = res
retorno

devolver dp(0, 0, True, False)
`` `

■ **Por qué Python funciona** – La profundidad de recursión de Python puede manejar 10 niveles (máx dígitos).
■ **Espacio** – `memo` es en la mayoría de `10 × 10`.
■ **Hora** – Todavía `O(log N)`.

-...

## 4. C+++ Implementación (Bottom‐Up Digit DP)

``cpp
// LeetCode 1067 – Cuenta de dígitos en rango
// C+17, O(log N) time, O(log N) Memory
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
dígitos int Conde(int d, int low, int high) {
objetivo = d;
recuento de retornoUpTo(high) - countUpTo(low - 1);
}

privado:
int target;
dígitos vectoriales:
vector realizador realizado en título memo; // memo[pos][cnt]

int countUpTo(int n) {}
si (n 0) retorno 0;
digits.clear();
n) { dígitos.push_back(n % 10); n /= 10; }
inverso(digits.begin(), digits.end()); // la mayoría significativa primera
int len = digits.size();
memo.assign(len, vector implicaint(len + 1, -1));
dfs(0, 0, true, false);
}

int dfs(int pos, int cnt, bool tight, bool started) {}
si (pos == digits.size()) cnt de retorno;
si (!tight " empieza " memo[pos][cnt]!= -1) memo [pos][cnt];

límite de entrada = apretado? dígitos[pos] : 9;
int res = 0;

si (!started) res += dfs(pos + 1, cnt, false, false); // skip leading cero

int start Digit = started ? 0 : 1;
para (int dig = start Digit; dign = límite; ++dig) {
res += dfs(pos + 1, cnt + (dig == target), tight " curva == limit, true);
}

si (!tight ' iniciado) memo[pos][cnt] = res;
restitución;
}
};
`` `

■ *Diferencias clave* – Utiliza un vector explícito para dígitos, recursión al fondo (sin lambdas).
■ **Complejidad** – Identical to Java/Python: `O(log N)` time, `O(log N)` Memory.

-...

## 5. Artículo del Blog – “El Bien, el Mal, el Ugly of Digit‐DP en LeetCode 1067”

■ **Keywords**: LeetCode 1067, Digit Count in Range, digit DP, preguntas de programación dinámica, entrevista de trabajo, ingeniero de software, solución Java, solución Python, solución C++, entrevista de codificación, diseño de algoritmos

### 5.1 El problema en una nuezquela

LeetCode 1067 te pide que cuentes cuántas veces aparece un solo dígito dentro de un intervalo entero enorme. La entrada puede ser tan grande como 200 millones, pero debe terminar en un milisegundo. A primera vista, un bucle de fuerza bruta parece ser la respuesta natural: simplemente iterate y convertir cada entero a una cuerda, pero que requeriría *cientos de millones de conversiones de cadena*, imposible en una entrevista o un desafío de codificación.

Este es el problema clásico “contando dígitos en un rango”. La solución elegante es *digit‐DP* – un enfoque dinámico de programación que trata el problema como traversal de los dígitos decimales de los números de límites.

### 5.2 The Good – Why Digit‐ DP es el estándar de oro

Silencio ¿Por qué brilla la Explicación Silenciosa
Silencio------------------------------
Silencio **Tiempo óptimo** Silencio Corre en `O(log N)` por consulta (≤ 10 dígitos para `2·108`). Silencio
TEN **Simplicity with recursion** TEN Cada paso de recursión maneja un solo dígito; el estado es diminuto: posición, cuenta hasta el momento, bandera ajustada, la bandera principal cero. Silencio
Silencio **Reutilizable a través de los problemas** DP, usted puede resolver una serie de problemas: “números de cuenta con una cantidad dada de dígitos”, “números divisibles por K”, “contable palindromes in range”, etc. Silencio
Silencio **Memory‐friendly** Silencioso El tamaño de la tabla de la memoización es `digits × digits` (≤ 100 enteros). Silencio

■ **Tip de Interview** – Presente el diagrama de estado primero. Mostrar que sólo hay 4 estados lógicos: `tight` (prefijo igual al límite) y `started` (si hemos colocado un dígito no cero). Esto hace que la recursión sea obvia.

### 5.3 Los malos – las caídas comunes y cómo evitarlos

1. **Cargando Cero** – Olvídate de tratar los ceros principales causa especialmente el recuento de dígitos en números como `0013`.
*Solución*: Agregue una bandera " arrancada " ; sólo cuente `target ' si `estrellado ' es verdad, de lo contrario salte.

2. **Off‐by‐One on Ranges** – Muchas soluciones substraen `count(low-1)` pero olvidan que `low-1` podría ser `0`.
*Solución*: Agregue la guardia `si (n 0) devuelve 0;` en el ayudante.

3. ** Condiciones de memoización** – Llevar resultados para estados * rectos* es incorrecto porque el límite superior cambia por llamada.
*Solution*: Memo only for `!tight ' comenzó`.

4. **Depth de la recursión** – En idiomas con límites de recidiva poco profundos (p. ej., Python 2), puede ser necesario `sys.setrecursionlimit`.
*Solución*: En Python, la profundidad de recursión es sólo 10 para este problema, pero establecer límite de todos modos si se generaliza.

5. **Wrong Digit Order** – Convertir un número en una cadena frente a la construcción de una serie de dígitos de lo menos a más puede cambiar el significado de 'pos'.
*Solution*: Standardize on ** most-significant first**; it simplifies the `tight` flag logic.

### 5.4 Los Casos Ugly - Edge que Trip Up Even Expertos

← Caso Edge Silencio Por qué es desagradable
Silencio...
Silencio **d = 0** Silencio Los ceros líderes nunca contaron, así que 0 aparece sólo en números como 10, 20... pero *no* como el dígito principal de 100. Silencio Mantenga la bandera `estrellada ' ; cuente `target` sólo cuando `estrellado `. Silencio
Silencio **Range incluye 1** Silencio `low = 1` da `alta-bajo+1 = 1` entero, pero el ayudante todavía funciona porque `contraUpTo(0)` es 0. Silencio No hay cambio - el `contraUpTo(low-1)` guardia lo maneja. Silencio
tención **alta = 2·108** Silencio números de 9 dígitos, pero algunos idiomas tratan 200 000 000 como 9 dígitos; garantizar la longitud de los dígitos es correcta. tención Convertir en hilo o utilizar el bucle de división; ambos dan la longitud correcta. Silencio
tención **target = 0 y número = 0** Silencio 0 contiene un cero. Algunas soluciones saltan erróneamente a la cuenta debido a la bandera de " arrancada " . 0`, regreso 1. Silencio

### 5.5 SEO‐ Resumen optimizado para los buscadores de empleo

■ **Si te estás preparando para una entrevista de ingeniería de software, masterización digital DP no sólo resuelve LeetCode 1067 en milisegundos sino que también demuestra un pensamiento algoritmo profundo. #
■ **Showcasing a clean Java, Python, or C++ implementation of digit‐ DP** impresionará a los entrevistadores que esperan que se ocupen eficientemente de los problemas de entrada grande.
■ **Más allá de LeetCode, los conceptos de digitación aparecen en escenarios del mundo real** — privilegiando algoritmos, contando combinatorios en analítica, e incluso en la construcción de índices de búsqueda eficientes.

**Key Takeaways for the curriculum vitae:**

*Programación Dinámica:* Experiencia demostrada en patrones de DP.
* Optimización de la complejidad del tiempo:* Soluciones entregadas en `O(log N)`.
- *Cross‐Language Competencia* Java, Python, soluciones C++ con la misma lógica.
- *Resolver el problema:* Haga preguntas de entrevista dura como “Conteo de dígitos en rango” rápidamente.

Use la frase ** "Digit‐DP algoritmo design"** en la sección de habilidades; los reclutadores a menudo la utilizan como filtro de palabras clave.

-...

## 6. Clausura

Las soluciones anteriores están listas para copiar-pasar en su IDE o plataforma de codificación. Cuando los presente en una entrevista, pasee por la máquina del estado, explique el manejo de los ceros principales, y haga hincapié en la bandera 'tight'. Esa narrativa, junto con el código recursivo elegante, dejará a los entrevistadores convencidos de que es un candidato fuerte para cualquier papel de ingeniería de software. 🚀

-...

¡Feliz codificación! *