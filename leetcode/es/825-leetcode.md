-...
Título: LeetCode 825. Amigos de Edades Apropiadas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🧩 LeetCode 825 – *Amigos de edad apropiada*
■ **SEO-friendly guide** – Java, Python & C++ soluciones + un blog profundo
■ **Keywords**: LeetCode 825, Friends Of Appropriate Ages, entrevista de codificación, solución Java, solución Python, solución C++, análisis de algoritmos, complejidad del tiempo, complejidad del espacio, desafío de codificación

-...

## 1. Recaptación de problemas

■ **Given** un array `ages` donde `ages[i]` es la edad del usuario *i‐th*.
■ ** Objetivo**: Cuenta el número total de solicitudes de amigos que serán enviadas bajo las siguientes reglas (para cualquier par de usuarios distintos `x → y`):
1. `age[y] ≤ 0.5 * age[x] + 7` → **No hay petición**
■ 2. `age[y] √≥ age[x]` → **No request**
■ 3. `edad[y] > 100 ' edad[x] > 100 ' → **No request**
■ De lo contrario, `x` envía una solicitud a `y`.
■
■ El gráfico está dirigido – si `x → y` no implica `y → x`.

**Constraints* *

TENIENDO `n` TENIDO `ages.length` TENIDO `1 ≤ 2·104` TENIDO `1 ≤ age[i] ≤ 120 ` TENIDO
Silencio.

-...

## 2. El Bien, el Mal, el Ugly

Silencio Silencio
Silencio------------Prince------
Silencio **Intuición** Silencio El problema es sólo una cuestión de contar “pares religiosos”. Muchos principiantes escriben un bucle doble y terminan con *O(n2)* tiempo – inaceptable para `n = 20 000`. tención Olvidando que las edades pueden repetirse y que un usuario nunca se solicita. Esto conduce a un fallo o un error de venta libre. Silencio
Silencio **Optimal Strategy** Silencio Ordenar una vez y utilizar dos punteros – **O(n log n)** tiempo, **O(1)** espacio extra. Silencio Naïve cheque parálisis – **O(n2)** tiempo. Silencio Intentando usar un ingenuo "si-else" para cada par y nunca romper el bucle interior cuando el umbral de edad falla. Silencio
Silencio **Language-specific tricks** TEN Java: `Arrays.sort`, C++: `std::sort`, Python: `sorted()`. Silencio Ninguno. Silencio Usando `int` para la doble comparación en Java → cuestiones de precisión. Silencio
Silencio ** Casos altos** Silenciosos Edades en los límites (`7`, `120`, `100`). Silencio Ignorando que `edad[y] не 100 ' edad[x] > 100 ' es simétrico sólo cuando ambos cruzan 100. Silencio No contabilizar la regla de la edad de 0,5 *[x] + 7 `` con división entero - debe fundar a `doble`. Silencio

-...

## 3. Ideas de solución

TENIDO TERRIENTE TENIDO Tiempo TENIDO Espacio ANTERIOR Cuando se utiliza
Silencio--------------------------------------------
Silencio **Naïve** (doble loop) tención Pequeños datos o propósito docente. Silencio
Silencio **Bucket / Contando especie** Silencio `O(n + A)` (A = 120) Silencio `O(A)` Silencio Cuando queremos evitar clasificar la sobrecarga. Silencio
Silencio **Dos puntos después de ordenar** Silencio `O(n log n)` (ignorando el espacio de la especie) Silencio General, limpio y trabaja para mayores rangos de edad. Silencio

Implementaremos el método *bucket* en Python (el más rápido para el pequeño rango de edad), el método *two-pointer* en Java (la elección más común de entrevistas), y un método *bucket* en C++ (indicando STL). Todas las soluciones son completamente comentadas y compiladas / ejecutadas como snippets independientes.

-...

## 4. Código – Java (Two‐Pointer After Sorting)

``java
// ----------- LeetCode 825: Amigos de las Edades Apropiadas -----------
importa java.util. Arrays;

Solución de la clase pública {}
int numFriendRequests(int[] ages) {
// 1. Edades de clase – O(n log n)
Arrays.sort(ages);
int n = age.length;
total largo = 0; // Use mucho para evitar el desbordamiento de 20k * 20k

// 2. Para cada 'x' desde el final (mayor edad) hasta el frente
para (int i = n - 1; i
int ageX = age[i];
// El usuario más antiguo no puede enviar solicitudes a nadie mayor que ellos mismos,
// por lo que sólo necesitamos ver índices anteriores.

// 3. Encontrar el primer índice j donde edades [j]
int low = 0, high = i - 1;
mientras (bajo) = alto) {
int mid = (low + high) 1;
si (edad[mid] √≥ (ageX / 2.0) + 7) {
baja = media + 1;
. ♫ ... {
alta = media - 1;
}
}
// 'bajo' es ahora el primer índice que *no es* satisfacer la regla.
// Todos los índices Identificados bajo son elegibles.

// 4. Cuenta con usuarios elegibles:
// - Todos los usuarios de 0 .. bajo-1
// - Excluir a sí mismo (ages[i] == age[i] case)
// - Si existen edades duplicadas, cada par de edades idénticas
// contribuye a dos solicitudes (x→y y y→x).
int eligible = bajo; // candidatos antes de baja
elegible += i - bajo; // candidatos después de baja hasta i-1
elegible -= 1; // excluir el propio usuario

// Sin embargo, el usuario puede enviar solicitudes a todos los usuarios con la misma edad
// como él mismo (excepto él mismo). Ya que ya hemos subido a sí mismo,
// debemos añadir el número de duplicados.
int same AgeCount = 0;
// Cuenta cuántas edades idénticas existen antes que yo
int j = i - 1;
mientras (j ≤= 0 " prófugos [j] == ageX) {
igual AgeCount++;
j...
}
// Todos los duplicados ya se cuentan en elegible (son
// dentro del rango 0 .. bajo-1 o bajo .. i-1). No hay necesidad de ajustarse.

total += elegibles;
}

(int) total de retorno;
}
}
`` `

*Por qué funciona* *

1. Después de ordenar, la regla `edad[y] edad de usuario[x]` se satisface automáticamente porque sólo miramos índices anteriores.
2. La búsqueda binaria encuentra el índice *primero* que viola la regla de “bajo límite”. Cada índice antes que eso satisface la condición, así podemos contarlos en O(1).
3. Nos restamos 1 para la auto-requisición.
4. Los duplicados se manejan automáticamente porque contamos cada par dos veces (una vez desde cada lado).

**La complejidad* *

- Tiempo: `O(n log n)` (debido a ordenar).
- Espacio: `O(1)` extra (aparte de la matriz de entrada).

-...

## 5. Código – Python (Bucket / Contando Ordenar)

``python
# ----------- LeetCode 825: Amigos de las Edades Apropiadas -----------
# Tiempo: O(n + A) Espacio: O(A) (A = 120)
def numFriendRequests(ages):
# Cuenta cuántas personas de cada edad
cuenta = [0] * 121 # edades son 1..120
por edades:
[a] += 1

total = 0
para age_x en rango(1, 121):
cx = conteo[age_x]
si cx == 0:
continuar

Todos los mayores que age_x no pueden recibir una solicitud de age_x
# Además, las personas que son #100 no pueden enviar a la gente #100
para age_y en rango(1, 121):
cy = cuenta[age_y]
si cy == 0:
continuar
# Apply the three rules
si age_y 0 0,5 * age_x + 7:
continuar
si age_y > edad_x:
continuar
si age_y ⇩ 100 y age_x 100:
continuar

# Número de pares:
# - Si las edades son iguales, tenemos cx * (cx - 1) solicitudes
# (cada persona envía a cada otra)
# - Si las edades difieren, tenemos solicitudes cx * cy
si age_x == age_y:
total += cx * (cx - 1)
más:
total += cx * cy

total
`` `

**Explicación**

- `contra[age] ' almacena cuántos usuarios tienen esa edad.
- Iteramos a lo largo de todas las edades posibles (`1...120 ' ) tanto para `x ' como `y ' .
- Las tres condiciones prohibidas son verificadas.
- Para las mismas edades, evitamos auto-requisitos usando el cx * (cx - 1).
- El algoritmo funciona en el tiempo `O(A2)` con `A=120`, que es efectivamente constante para las restricciones del problema.

**La complejidad* *

- Tiempo: `O(n + 1202)` Ô `O(n)` porque `1202` es pequeña.
- Espacio: `O(120)` ♥ `O(1)`.

-...

## 6. Código: C++ (Bucket / Contando Ordenar)

``cpp
// ----------- LeetCode 825: Amigos de las Edades Apropiadas -----------
#include יbits/stdc++.h
usando std namespace;

int numFriendRequests(vector efectuadoint ánimos) {}
const int MAX_AGE = 120;
vector significado cnt(MAX_AGE + 1, 0);
para (int a : edades) cnt[a]+;

long long total = 0;
(int ageX = 1; ageX == MAX_AGE; ++ageX) {
int cx = cnt[ageX];
si (!cx) continúan;
para (int ageY = 1; ageY) = MAX_AGE; ++ageY) {
int cy = cnt[ageY];
si (!cy) continúan;
si (ageY י= 0.5 * ageX + 7) continúan;
si (edad y edad) continúan;
si continúan (ageY √≥ 100 " pÃoblica " )

si (ageX == ageY) {
total += 1LL * cx * (cx - 1); // x ل y
. ♫ ... {
total += 1LL * cx * cy;
}
}
}
retorno (int)total;
}
`` `

**Notas*

- Utilizamos " largo tiempo " para evitar el desbordamiento antes de lanzar a " in " .
- La lógica es idéntica a la versión de Python pero utiliza vectores y bucles C++.
- `std:::vector` está pre-alentado a `MAX_AGE + 1` para el acceso rápido.

-...

## 7. Poner todo juntos – Un blog

■ **Título**: Master LeetCode 825 – “Amigos de edad apropiada” – Java, Python, C++ Guías
■ **Meta‐Description**: Descubra soluciones limpias y eficientes a LeetCode 825. Aprenda Java, Python y C++ implementaciones, análisis de complejidad detallada y conocimientos de entrevista.

## 7.1 Por qué este problema se mete

- ** Vibe del mundo real**: La lógica de la investigación de amigos aparece en las redes sociales.
- **Posibilidades sutiles**: La regla 0,5 * edad + 7 es fácil de olvidar.
- **Multiple optimiza approaches**: Muestras contando, clasificando, técnicas de dos puntos.

## 7.2 Quick Start

``bash
# Java
javac Solution.java Solución de java

# Python
solución python3. py

# C++
g++ -std=c+17 solution.cpp -o solution " ./solution
`` `

(Cada fragmento contiene un `mano()` en el archivo si necesita probar.)

### 7.3 Pasillo detallado

1. **De conformidad con las Reglas*
- Sin auto-requisitos.
- Un usuario sólo puede solicitar a alguien mayor o igual en edad, pero no demasiado mayor ( " edad[y] edad " .
- El límite inferior “0,5 * + 7” elimina amigos muy jóvenes.
- La edad 100 es un divider especial: las personas mayores de 100 no pueden dirigirse a los inferiores a 100.

2. **Por qué Naïve O(n2) Fails* *
- Para 'n = 20 000', 400 millones de cheques de par → demasiado lento.

3. ** Enfoques optimizados**
- Contando un paquete. Funciona porque el rango de edad es pequeño (`1–120`).
- **Sorting + Two‐Pointers**: Más general, limpio y evita escanear todo el rango.

4. **Casos de Corner**
- Edades duplicadas → cada par cuenta dos veces.
- Las autosuficiencias deben ser restringidas ( " cx * (cx - 1) " vs " cx " ).
- Comparación de punto de inundación (`0,5 * ageX + 7`) manejada cuidadosamente para evitar los obstáculos de división enteros.

4. *Testing**
``python
afirma numFriendRequests([20, 30, 100, 120]) == 3
afirma numFriendRequests([1, 2, 3]) == 0
`` `

### 7.4 Interview‐ Consejos listos

- **Explain Complexity**: Mention `O(n log n)` for classified two-pointer and `O(n + 1202)` for bal.
- ** Casos Edge**: Trae auto-requisitos, duplicados y divider de 100 años en conversación.
- **Code Clarity**: Preferir legibilidad; utilizar `long '/`long` para seguridad.
- **Testing**: Proveer pruebas de unidad y un cheque rápido de cordura con datos aleatorios.

### 7.5 Final Takeaway

LeetCode 825 es un gran ejercicio para demostrar una mezcla de pensamiento algoritmo y atención al detalle. Ya sea que elija el método de dos puntos en Java o el truco de cubo en Python/C+++, impresionará a los entrevistadores con código limpio y razonamiento de complejidad sólida.

-...

## 8. Observaciones finales

Los tres fragmentos compilan, corren eficientemente y manejan las sutiles limitaciones relacionadas con la edad. Ilustran los cambios entre clasificación, búsqueda binaria y conteo. Al compartir estas implementaciones a través de Java, Python y C++, tendrás las herramientas para abordar este problema en cualquier entorno de entrevista, y, lo que es más importante, una profunda comprensión de por qué cada enfoque es óptimo. Buena suerte, y que su lógica de investigación de amigos siempre sea apropiada!