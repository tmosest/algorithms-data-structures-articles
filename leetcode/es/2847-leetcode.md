-...
Título: LeetCode 2847. Número más pequeño con dado producto dígito -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Código de Solución

A continuación encontrará ** tres implementaciones completas y ejecutables** para el problema LeetCode **2847 – Número más pequeño con el producto dado dígitos**.
Las tres soluciones utilizan la misma lógica avaricia:

1. Factor de la entrada `n` sólo con los principales `2, 3, 5, 7`.
2. Si un factor permanece, la respuesta es `-1`.
3. Combine los principales factores en los dígitos más pequeños posibles (9 → 32, 8 → 23, 6 → 2·3, 4 → 22).
4. Construir la respuesta en orden ascendente de dígitos.

``text
Complejidades
-----------
Tiempo : O(log n) (caso inferior que divide en 2, 3, 5 o 7 unas pocas docenas de veces)
Espacio : O(1) (además de la cadena de salida)
`` `

■ **Tip** – Al escribir código de entrevistas, mantenga siempre la lógica en una función de ayuda independiente; esto mantiene el código legible y fácil de probar.

-...

## 1.1 Java (LeetCode signature)

``java
Clase Solución {
public String smallestNumber(long n) {
// Casos especiales
si (n == 1) retorno "1";
si (n י 10) devolver String.valueOf(n);

int[] prime = {2, 3, 5, 7};
int[] cnt = nuevo int[10]; // cnt[d] = cuántos dígitos d aparecerán

// factor n por primos 2,3,5,7
para (int p : prime) {
(n % p == 0) {
n /= p;
cnt[p]+;
}
}

si 1) retorno "-1"; / // factor sobrante 7 → imposible

// combinar en dígitos más grandes
cnt[9] = cnt[3] / 2; // 3*3 = 9
cnt[3] %= 2;

cnt[8] = cnt[2] / 3; // 2*2*2 = 8
cnt[2] %= 3;

si (cnt[3] √≥ 0 " sensible cnt[2]
cnt[3] = 0;
cnt[2] = 1; // dejar uno '2 '
cnt[6] = 1;
}

cnt[4] = cnt[2] / 2; // 2*2 = 4
cnt[2] %= 2;

// construir respuesta en orden ascendente de dígitos
StringBuilder sb = nuevo StringBuilder();
para (int d = 1; d)
para (int i = 0; i) cnt[d]; i++) sb.append(char)('0' + d));
}
devolver sb.toString();
}
}
`` `

-...

## 1.2 Python 3

``python
Solución de clase:
def más pequeño Número(self, n: int) - título str:
si n == 1: Caso especial
"1"
si no se hizo 10: # dígito único ya es la respuesta
retorno str(n)

primos = [2, 3, 5, 7]
cnt = [0] * 10 # cnt[d] = cuántas veces d dígitos aparecerán

# factor n
para p en primos:
mientras que n % p == 0:
n //= p
cnt[p] += 1

si n= # factor sobrante # 7 → imposible
"-1"

# Merge en dígitos más grandes
cnt[9] = cnt[3] // 2 # 3*3
cnt[3] %= 2

cnt[8] = cnt[2] // 3 # 2*2*2*2
cnt[2] %= 3

si cnt[3] √≥ 0 y cnt[2]
cnt[6] = 1
cnt[3] = 0
cnt[2] = 1

cnt[4] = cnt[2] // 2 # 2*2
cnt[2] %= 2

# Construir la respuesta en orden ascendente
res = []
para d en rango(1, 10):
re.append(str(d) * cnt[d])
volver ".join(res)
`` `

-...

## 1.3 C++ (GNU C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
cuerda más pequeña Número(largo largo n) {}
si (n == 1) retorno "1";
si (n) 10) regresan a_string(n);

vector identificador principal = {2, 3, 5, 7};
vector significado cnt(10, 0); // cnt[d] = tiempos dígitos d aparecerá

para (int p : prime) {
(n % p == 0) {
n /= p;
++cnt[p];
}
}
si 1) retorno "-1";

cnt[9] = cnt[3] / 2; // 3*3
cnt[3] %= 2;

cnt[8] = cnt[2] / 3; // 2*2*2*2
cnt[2] %= 3;

si (cnt[3] " clnt[2]) { // 3*2
cnt[6] = 1;
cnt[3] = 0;
cnt[2] = 1;
}

cnt[4] = cnt[2] / 2; // 2*2
cnt[2] %= 2;

cadena res;
para (int d = 1; d)
res.append(cnt[d], char('0' + d));
}
restitución;
}
};
`` `

-...

# 2️ Blog Artículo – “El Bien, el Mal, y el Ugly of Solving LeetCode 2847”

■ **Keywords**: *LeetCode 2847*, *Smallest Number with Given Digit Product*, *Java solution*, *Python solution*, *C++ solution*, *interview coding*, *algorithm*, *greedy factorization*, *coding interview tips*, *tech hiring*

-...

## Introduction

Cada ingeniero de software tiene ese problema de LeetCode que se siente como un *mini-code-wars*: estás mirando un número, tienes que separarlo, y debes hacerlo en la cuerda más corta posible **. Eso es **2847 – Número más pequeño con el producto dado dígito**.

Es un problema de “medio” en LeetCode, pero en una entrevista puede **hacer o romper** la confianza del candidato. Vamos a diseccionar por qué este problema es un gran escaparate, qué es lo que buscan los reclutadores, y cómo puedes ** convertirlo en una estrella de entrevistas lista para portafolios**.

-...

## The Good – Why Este problema es un Gold‐Mine para los candidatos

1. ** Declaración de problemas claros** – Te han dado un solo entero. Si usted puede expresar el producto de sus dígitos como `n`, salida del número *smallest* que lo hace.
2. ** Dominio de entrada pequeña** – Todos los factores principales mayores de 7 arruinan la solución. Esa restricción le da un **finito conjunto de primos “útiles”** (`2, 3, 5, 7`) de qué preocuparse.
3. **Greedy + factorización** – La solución óptima es casi trivial una vez que vea el patrón: 9 = 32, 8 = 23, 6 = 2·3, 4 = 22. Si usted fusiona los factores principales en el orden correcto usted consigue la cadena más pequeña al instante.
4. **Language-agnostic logic** – Ya sea en Java, Python o C++, la idea central sigue siendo idéntica. Eso es genial para los candidatos que *como* un idioma pero deben responder en otro durante una entrevista.

■ **Pro tip**: En una entrevista, **explica tu plan antes de escribir código**. Programador de amor para verte pensar antes de escribir.

-...

## Los malos – saltos comunes

Silencio Pitfall Silencio Por qué es un problema
Silencio...
Silencio **Dejar `n ' < 10** – devolver `String.valueOf(n)` en Java o `str(n)` en Python. Parece trivial, pero usted también debe manejar `n = 1` que es * no* cubierto por la regla de "doble dígito". TENIENTES DE LA Terrorización `n == 1` como caso separado *antes* la lógica general. Silencio
Silencio ** Total avaricia de 9 a 2** sin comprobar los factores imposibles. Usted podría dividir por 9, 8, ..., pero si un factor sobrante > 7 permanece usted va a producir silenciosamente un número equivocado. Silencio Después de la factorización, **ver `n!= 1`**; si es verdad, salida `-1`. Silencio
Silencio **No fusionar los principales factores** Silencio Si usted acaba de producir los primos 2,3,5,7 en orden descendente, la cadena puede ser más larga que necesaria (por ejemplo, 222 → "222" vs "8"). Silencio Merge `23` → 8, `32` → 9, `2·3` → 6, `22` → 4. Este es el paso * grano de fusión*. Silencio
Silencio **Construir el resultado en el orden incorrecto** Silencio Revertir una pila de dígitos da el número equivocado: “98” vs “89”. ← Apéndice dígitos en **ascending** orden después de fusionarse. In C++/Java `append(cnt[d], digit)` or in Python `"digit"*cnt[d]`. Silencio

-...

## El Ugly – Edge‐Case Head‐aches

1. **Números de calibre** ( ' n ' hasta ' 1018 " ) – Se podría pensar que la recursión o los bucles podrían desbordarse. Use **`long`/`long'** y dividir paso a paso.
2. **Prime factorization** – Mientras que el `//=` de Python es barato, el modulo de Java en `long` puede parecer intimidante. Sólo recuerde: sólo se divide en 2, 3, 5 o 7 – que es en la mayoría ~ 60 iteraciones.
3. **Memoria fuga en Java** – Un `StringBuilder` es esencial. Evite concatenar cadenas en un bucle; es O(n2).
4. **C++ `estring::append` matices** - `res.append(cnt[d], char('0'+d));` puede ser confuso para los recién llegados. El primer argumento es el **repeat count**.

-...

## Cómo brillar en una entrevista

1. **Declara tu enfoque* *
“Preferiré el número usando los primos 2, 3, 5, 7. Si queda algo, es imposible. Entonces combinaré avariciosamente pares de 3 en 9’s, triples de 2’s en 8’s, y así sucesivamente. ”

2. **Explicar la fusión avariciosa*
“Porque 9 es el dígito único más grande, y 9=32, usando 9 reduce el conteo de dígitos. Del mismo modo 8=23 y 6=2·3, 4=22. Esto garantiza el resultado más pequeño de la lexicografía. ”

3. **Mostrar el código paso a paso**
*No sólo desperdiciar el snippet final.* Camine por el bucle de factorización, la sección de fusión, y la construcción de cuerdas. A los clientes les encanta la explicación.

4. ** Casos de esquina hundidos**
* `n == 1` → “1”.
* " n " 10 " → `str(n)` o `to_string(n)`.
* Factor de sobra > 7 → `-1`.

5. # Lo más a fondo #
Correr los siguientes casos:
``text
1 → "1"
10 → "-1" (10 = 2·5 → OK, pero 10 realizados es un solo dígito)
20 → "45" (20 = 22·5 → 4·5)
256 → "288" (256 = 28 → 8·8)
1000000000000000000 → "-1"
`` `
En entrevistas, los candidatos a menudo saltan la prueba número grande; asegúrese de que no.

-...

## Conclusión – Convertir 2847 en un Ganador Contratando

*LeetCode 2847* es un estudio **micro-case** de la factorización codictiva, manipulación óptima y manipulación de cuerdas. Es lo suficientemente pequeño para ser resuelto en menos de 5 minutos, pero prueba su:

* **Intuición matemática** – Reconociendo que 9 = 32, 8 = 23, etc.
* ** Claridad algorítmica** – Escribir código limpio, lingüístico-agnóstico.
* ** Sensibilización por caso** – Manejo de `1`, dígitos únicos e insumos imposibles.

Cuando entras en una entrevista tecnológica, *menciona la estrategia codictiva* primero. Mostrar que puede razonar sobre por qué fusionar los factores principales da la cuerda lexicográfica más pequeña. A continuación, escriba su código en el estilo amigable de la entrevista arriba.

■ **Recuerde**: El *bueno* es la elegante lógica avaricia; el *bad* es la tentación de pensar o olvidar el caso `-1`; el *muy* es los pequeños errores de implementación que aparecen sólo en casos de borde. Enséñales, y pasarás de “medio” a “must‐hire” en poco tiempo.

¡Feliz codificación y buena suerte en tu próxima entrevista técnica! 🚀

-...

■ **¿Hay más soluciones para entrevistas? * *
> [My GitHub LeetCode Repository](https://github.com/your‐github) – Java, Python, C++ – listo para copy‐paste.
¡Suscríbete a mi newsletter para desglosamientos semanales de algoritmos y consejos de entrevista-prep!