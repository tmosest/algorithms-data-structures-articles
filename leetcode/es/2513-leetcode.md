-...
Título: LeetCode 2513. Minimizar el máximo de dos rayos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recap del problema – Minimizar el máximo de dos rayas

Se les da cuatro enteros:

Silencio Variable Silencio Significado
Silencio...
Silencio **divisor1** Silencio `arr1` no puede contener ningún número divisible por este valor
Silencio **divisor2** Silencio `arr2` no puede contener ningún número divisible por este valor
Silencio **uniqueCnt1** Silencio `arr1` debe contener exactamente estos muchos *distintos* enteros positivos Silencio
Silencio **uniqueCnt2** Silencio `arr2` debe contener exactamente estos muchos *distintos* enteros positivos Silencio

Los dos arrays deben ser disjoint (ningún número puede aparecer en ambos).
Su tarea: **escoge los enteros** para ambos arrays para que el entero *maximum* usado en ambos array sea lo más pequeño posible.
Devuelve ese máximo mínimo alcanzable.

Las limitaciones son enormes (`uniqueCnt1`, `uniqueCnt2` hasta 109) – una solución de fuerza bruta es imposible.

-...

## 2. Intuición

El problema es una típica * “búsqueda binaria en la respuesta”* pregunta.

* Si fijas un límite superior `M`, puedes decidir si es **posible** rellenar los dos arrays con todos los números `≤ M`.
* Si es posible, puede probar un `M` más pequeño; si es imposible, debe probar uno más grande.
* La búsqueda binaria en `M` da el máximo mínimo posible en los pasos `O(rango de registro).

Así que el subproblema clave es:

■ **Den un límite `M`, podemos seleccionar números 'uniqueCnt1' no divisibles por `divisor1`,
¿Números no divisibles por `divisor2`, todos ≤ `M`, y todos distintos? * *

La respuesta puede derivarse de la simple contabilización:

* `CntBoth` – números ≤ `M` divisible por ** ambos divisores**
* `cntOnly1` – divisible only by `divisor1` (not by `divisor2`)
* `cntOnly2` – divisible only by `divisor2` (not by `divisor1`)
* `cntother` – números divisibles por **neither** divisor

Sólo `cntOther` + `cntOnly2` son candidatos para `arr1`.
Sólo `cntOther` + `cntOnly1` son candidatos para `arr2`.

Si tratamos de dar `arr1` todos los números que puede utilizar y luego comprobar si
`arr2` todavía tiene suficiente, la decisión reduce a un puñado de aritmética
operaciones – sin necesidad de una construcción codictiva real.

-...

## 3. Algoritmo (código Pseudo)

`` `
función posible(M):
l = lcm(divisor1, divisor2)
ambos = M / l
sólo1 = M / divisor1 - ambos
sólo2 = M / divisor2 - ambos
otros = M - (tanto + sólo1 + sólo2)

Números que pueden ser utilizados por arrr1:
vale1 = otros + sólo2
Números que pueden ser usados por arrr2:
vale2 = otros + sólo1

si únicoCnt1 неле o únicoCnt2 нелентели:
devolver falso

# After giving arr1 and arr2 all exclusive candidates,
# ¿Cuántos números "otros" quedan?
utilizadoOtro = max(0, uniqueCnt1 - only2) + max(0, uniqueCnt2 - only1)
restantes Otros = otros - utilizados Otros

Regreso restante 0
`` `

Binary search around `M`:

`` `
baja = 1
alto = 2 * (uniqueCnt1 + únicoCnt2) * max(divisor1, divisor2) # seguro superior
mientras que bajo
media = (bajo + alto) // 2
si es posible (medio):
alta = media
más:
baja = media + 1
Regreso bajo
`` `

Todos los aritméticos se hacen con enteros de 64 bits ( 'long` en Java, 'long' en C++,
" tipo " en Python 3 porque autopromota.

-...

## 4. Complejidad

TEN TERRITOR TERRITOR TEN TERRITOR TEN TERRITOR TEN TERRITOR SON TERRITOR SON SON SON TEN SON SON SON 
Silencio------Prince--------
Silencioso búsqueda binaria Silencioso `O(rango de registro)` ♥ `O(log 1014)` ( י 50 iterations) Silencio `O(1)` Silencio
TENIENDO `possible` Silencio `O(1)` Silencio

Total: **`O(rango de registro)` tiempo, `O(1)` memoria** – lo suficientemente rápido para los límites.

-...

## 5. Aplicación

A continuación se presentan implementaciones limpias y listas de producción en **Java, Python y C++**.

-...

## 5.1 Java (Java 17)

``java
importa java.io.*;
importar java.util*;

Solución de la clase pública {}
int public int minimizeSet(int divisor1, int divisor2, int uniqueCnt1, int uniqueCnt2) {
d1 = divisor1, d2 = divisor2;
largo c1 = únicoCnt1, c2 = único Cnt2;

larga baja = 1;
alto largo = 2L * (c1 + c2) * Math.max(d1, d2); // seguro superior borde

mientras (bajo)
largo medio = bajo + (alto - bajo) / 2;
si (posible(mid, d1, d2, c1, c2)) {}
alto = medio;
. ♫ ... {
baja = media + 1;
}
}
(int) low;
}

booleano privado posible(long m, long d1, long d2, long c1, long c2) {
larga l = lcm(d1, d2);

largo ambos = m / l;
long only1 = m / d1 - both;
long only2 = m / d2 - both;
largo otro = m - (ambos + sólo1 + solamente2);

long avail1 = other + only2; // arrr1 candidates
long avail2 = other + only1; // arr2 candidates

si (c1 неленый) ненный неный c2 неленых неный неленый неный неный нененый неный неный нененый нененый ный ный неный ный ный неный неный ный ный ный ный ный ный ный ненененененый неный ный ный ный ный ный неный ный ный неный ный ный ный ный ный нененененый нен

largo usoOtras = Math.max(0, c1 - only2) + Math.max(0, c2 - only1);
quedando Otros = otros - utilizados Otros;

Regreso restanteOtros = 0;
}

lcm (long a, long b) {}
volver a / gcd(a, b) * b; // a/gcd * b nunca desborda (64 bits)
}

gcd (long a, long b) {}
mientras (b!= 0) {
t largo = un % b;
a = b);
b = t;
}
devolver a;
}

// --------
// Método principal para leer entrada para el juez en línea.
// --------
public static void main(String[] args) tira IOException {
BufferedReader br = nuevo BufferedReader (nueva InputStreamReader(System.in));
StringTokenizer st = nuevo StringTokenizer(br.readLine());
int d1 = Integer.parseInt(st.nextToken());
int d2 = Integer.parseInt(st.nextToken());
int c1 = Integer.parseInt(st.nextToken());
int c2 = Integer.parseInt(st.nextToken());
Solución s = nueva solución ();
System.out.println(s.minimizeSet(d1, d2, c1, c2));
}
}
`` `

-...

### 5.2 Python 3 (3.10+)

``python
importadores
importar matemáticas

def minimizeSet(divisor1: int, divisor2: int,
únicoCnt1: int, uniqueCnt2: int) - Conf int:
d1, d2 = divisor1, divisor2
c1, c2 = únicoCnt1, únicoCnt2

bajo, alto = 1, 2 * (c1 + c2) * max(d1, d2)

mientras que bajo
media = (bajo + alto) // 2
si es posible (medio, d1, d2, c1, c2):
alta = media
más:
baja = media + 1
Regreso bajo


def possible(m: int, d1: int, d2: int, c1: int, c2: int) - título Bool:
l = lcm(d1, d2)
ambos = m / l
sólo1 = m //d1 - ambos
sólo2 = m //d2 - ambos
otros = m - (tanto + sólo1 + sólo2)

vale1 = otros + sólo2
vale2 = otros + sólo1
si c1 √≠ cabo1 o c2 √2 }
Retorno Falso

us_other = max(0, c1 - only2) + max(0, c2 - only1)
volver otro - usado_otro не= 0


def lcm(a: int, b: int) - int:
volver a // math.gcd(a, b) * b


# --------------------------------------------------
# Standard online‐juez entry point
# --------------------------------------------------
si __name_ == "__main__":
data = list(map(int, sys.stdin.read().strip().split()))
d1, d2, c1, c2 = datos
print(minimizeSet(d1, d2, c1, c2))
`` `

-...

## 5.3 C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minimizeSet(int divisor1, int divisor2, int uniqueCnt1, int uniqueCnt2) {
d1 = divisor1, d2 = divisor2;
largo largo c1 = únicoCnt1, c2 = único Cnt2;

largo largo largo bajo = 1;
largo largo alto = 2LL * (c1 + c2) * max(d1, d2); // seguro superior borde

mientras (bajo)
largo medio = bajo + (alto - bajo) / 2;
si (posible(mid, d1, d2, c1, c2)) {}
alto = medio;
. ♫ ... {
baja = media + 1;
}
}
volver estática_cast seleccionado(bajo)
}

privado:
estática larga lcm largo(long long a, long long long b) {}
devolver un / std::gcd(a, b) * b; // no desbordamiento: 64‐bit
}

bool estático posible(largo largo m,
largo tiempo d1, largo largo d2,
largo c1, largo largo c2) {
largo l = lcm(d1, d2);
largo ambos = m / l;
largo sólo1 = m / d1 - ambos;
largo sólo2 = m / d2 - ambos;
largo otro = m - (ambos + sólo1 + solamente2);

long long avail1 = other + only2;
long long avail2 = other + only1;
si (c1 неленый) ненный неный c2 неленых неный неленый неный неный нененый неный неный нененый нененый ный ный неный ный ный неный неный ный ный ный ный ный ный ный ненененененый неный ный ный ный ный ный неный ный ный неный ный ный ный ный ный нененененый нен

largo uso Otros = max(0LL, c1 - only2) + max(0LL, c2 - only1);
mucho tiempo restante Otros = otros - utilizados Otros;
Regreso restanteOtros = 0;
}
};
`` `

-...

## 6. “Bueno, malo, ugly” – ¿Qué hay que ver

TENIDO Aspecto TENIDO Qué hacer ANTERIOR Qué *no* hacer ANTERIOR
Silencio------------------------- La vida...
Silencio **Bien** Silencio Usar aritmética de 64 bits en todas partes – la respuesta puede ser ~1014. tención Stick to 32‐bit `int` – obtendrá respuestas incorrectas para grandes insumos. Silencio
Silencio **Bien** Silencio Binaria búsqueda del *abajo* conservadoramente (`alta = 2*(c1+c2)*max(d1,d2)`); nunca llegarás al caso “busca demasiado alto”. Silencio Elija un `alto' demasiado pequeño (por ejemplo, `c1+c2`) – la búsqueda binaria se abrirá para siempre o devolverá un resultado incorrecto. Silencio
Silencio **Bien** Silencio Prueba al ayudante con un pequeño script de ayuda primero (`M=10,20,30' etc.). Silencio Supongamos que el cheque “disponible solamente-exclusivo” es suficiente – todavía necesita tener en cuenta la “otra” piscina compartida. Silencio
Silencio **Bad** Silencio Olvídate de que 'cnt Other' cuenta *neither* divisor. Piensa que 'cntOther' cuenta "ambos" – entonces podrás llenar `arr1` pero no `arr2`. Silencio
Silencio **Ugly** Silencio Una implementación de “gran selección” que realmente construye dos arrays rápidamente explotará en las limitaciones de `109` y es innecesaria. ← Implementar un ingenuo retroceder o dos puntos codiciosos – que va a tiempo fuera. Silencio

-...

## 7. Why This Problem Rocks for a Coding Interview

1. ** Muestra tu dominio de “búsqueda binaria en respuesta”** – un patrón de entrevista recurrente.
2. **Prueba su capacidad de contar con cuidado** en lugar de construir soluciones explícitas.
3. **Requiere una comprensión sólida de la teoría de números** ( " lcm " , " gcd " ) en un contexto de programación.
4. **Demuestra tu habilidad con aritmética de 64 bits** – la mayoría de los entrevistadores te pedirán que expliques por qué 32 bits es inseguro.
5. ** Destaca cómo diseñar un límite superior seguro** para el rango de búsqueda binaria – un pequeño detalle que puede viajar a muchos candidatos.

■ *Si puedes explicar el algoritmo anterior en menos de 5 minutos, impresionarás a casi todos los gerentes de contratación. *

-...

## 8. Key Take‐aways for Your Next Interview

Silencio Take‐away Silencio Por qué importa
Silencio...
Silencio **Explicar el cheque “posible(M)” en palabras** (no sólo código). Silencio Muestra comprensión profunda, no sólo memorización. Silencio
Silencio **Mostrar la intuición en el límite superior** (por qué `2*(c1+c2)*max(d1,d2) ` funciona). ← Evita una pregunta de entrevista sobre “¿por qué termina la búsqueda binaria?”. Silencio
Silencio **Discuss time‐complexity** – log-scale even for `1014`. ← Demonstrates usted puede razonar sobre asintotica bajo restricciones estrictas. Silencio
tención **Posencias potenciales de la mención**: desbordamiento, indexación basada en 1, manejo de 'otros' números correctamente. Muchos candidatos bajan la “otra” piscina; obtendrás marcas completas. Silencio

-...

## 9. Conclusión

*El problema es engañosamente simple una vez que te das cuenta de que es un problema contable oculto detrás de una pregunta “elegir el máximo más pequeño”. *
La búsqueda binaria en el máximo junto con una prueba de viabilidad `O(1)` ofrece una solución limpia, rápida y matemáticamente rigurosa que escala a las entradas más grandes que el problema permite.

¡Feliz codificación y buena suerte clavando esa entrevista!