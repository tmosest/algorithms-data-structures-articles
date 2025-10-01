-...
Título: LeetCode 1601. Número máximo de solicitudes de transferencia alcanzables -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código de Solución

A continuación se presentan tres **ready‐to-copy** implementaciones de la "Maximum Number of Achievable Transfer Solicita" (Leetcode 1601) – una en **Java**, una en **Python**, y otra en **C+**.
Los tres utilizan un enfoque **backtracking + bitmask** que garantiza la óptimabilidad manteniendo el tiempo de ejecución bien por debajo de los límites (el número de solicitudes ≤ 16).

■ ¿Por qué Bitmask?
■ Porque `m ≤ 16`, podemos representar cualquier subconjunto de solicitudes como un entero de 16 bits. Enumerating all `2^m` subsets is trivial (`65536` at most) and far faster than explore a tree with pruning.
■ Para mayor `m`, retroceder con la poda (exit cuando el desequilibrio neto no puede ser corregido) sería preferible, pero para este problema el bitmask es tanto más simple como más rápido.

-...

### 1.1 Java (Java 17)

``java
importar java.util*;

Solución de la clase pública {}
*
* Código de Leet 1601 – Número máximo de solicitudes de transferencia alcanzables
* Backtracking with bitmask enumeration (O(2^m * n))
*/
int public int maximumRequests(int n, int[][ ] {
int m = peticiones. longitud;
int best = 0;

// Pre-allocate una matriz para el cambio neto de cada edificio
int[] net = new int[n];

// Enumerar todos los subconjuntos de solicitudes (0 ... (1 0)-1)
para (enmascarado = 0; mascarilla) {}
Arrays.fill(net, 0);
int count = Integer.bitCount(mask); // number of taken requests
si (cuenta <= mejor) continuar; // no puede vencer mejor

// Aplicar el subconjunto
para (int i = 0; i)
si (mask > (1 > ) 0) {
net[requests[i][0]]--; // leave building
net[requests[i] ][1]++; //
}
}

// Compruebe si todas las redes son cero
booleano ok = verdadero;
para (int val : net) {
si (val!= 0) { ok = false; break; }
}
si (ok) mejor = contar;
}
devolver mejor;
}
}
`` `

-...

### 1.2 Python 3

``python
de la importación Lista

Solución de clase:
"
Leetcode 1601 – Número máximo de solicitudes de transferencia alcanzables
enumeración de bitmask (O(2^m * n)), Python 3.11
"
def maximumRequests(self, n: int, requests: List[List[int]) - título int:
m = len(requests)
mejor = 0
para máscaras en rango(1 )
net = [0]
cnt = mask.bit_count()
si cnt = mejor:
continuar
para i en rango(m):
si mascara i
net[requests[i][0]] -= 1
net[requests[i][1]] += 1
si todo(x == 0 para x en red:
mejor = cnt
mejor
`` `

-...

### 1.3 C++ (GNU‐C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
// Leetcode 1601 – Número máximo de solicitudes de transferencia alcanzables
// enumeración de Bitmask (O(2^m * n))
int maximumRequests(int n, vector seleccionadovector identificadointюще peticiones) {
int m = requests.size();
int best = 0;

para (enmascarado = 0; mascarilla)
vector asignadoint 0);
int cnt = __ builtin_popcount(mask);
si (cnt <= best) continuar; // poda

para (int i = 0; i) {}
si (mask " (1 " ) {
net[requests[i][0]]--; // leave
net[requests[i] ][1]++; //
}
}

bool ok = verdadero;
para (int x : net) si (x != 0) { ok = false; break; }
si (ok) mejor = cnt;
}
devolver mejor;
}
};
`` `

■ **Tip:**
* Los tres códigos funcionan en **milliseconds** en el arnés de prueba Leetcode.
* Si prefiere una versión de retroceso pura (por ejemplo, para fines educativos), reemplace el bucle de bitmask con un DFS recursivo que mantiene una red "int[] y la actualiza en el vuelo. El truco de poda (`si (cnt = mejor) regresa;`) todavía funciona.

-...

## 2. Artículo del Blog

■ **Título:** *Leetcode 1601 – “Número máximo de solicitudes de transferencia alcanzables” – Guía completa de retroceso + Bitmask para entrevistas*
■ **Meta Descripción:** Master Leetcode 1601 con una solución de backtracking limpia, optimización de bitmask y implementaciones Java/Python/C++. Entender las trampas, las persianas, y por qué este problema importa en las entrevistas de codificación.

-...

#### 2.1 Introduction

En ** entrevistas de ingeniería de software**, *Leetcode 1601 – Maximum Number of Achievable Transfer Solicita* es un elemento básico para la prueba ** optimización web** habilidades. El problema te obliga a pensar en:

1. ** Saldo neto** por edificio (desbordamiento = entrada).
2. ** Búsqueda exhaustiva** de subconjuntos de solicitudes (≤ 16).
3. **Fabricación eficiente** o enumeración de bitmask**.

Si usted puede resolver esto de forma limpia, impresionará a los gerentes de contratación en las principales empresas tecnológicas.

-...

### 2.2 Declaración de problemas (reescrito)

Se les da `n` edificios (`0 ... n‐1`).
Cada edificio alberga inicialmente a algunos empleados, pero sólo nos importan ** cambios relativos**.
`requests[i] = [from_i, to_i]` denota el deseo de un solo empleado de pasar de construir `de_i` a construir `to_i`.

* Objetivo*
Seleccione el subconjunto más grande posible de solicitudes tales que para **todo edificio** el número de empleados que abandonan equivale al número de empleados que entran.
En otras palabras, el cambio neto por edificio es cero.

**Constraints* *

- 1 ≤ 20
- 1 ≤ m = peticiones. longitud ≤ 16
- No.

-...

### 2.3 Naïve Approach (Exhaustive DFS)

Una solución de libro de texto es probar cada combinación usando recursión:

``text
dfs(idx, net[], count)
si idx == m:
si todo(net[i] == 0): mejor = max(best, count)
Regreso
// Solicitar idx
net[de[idx]]--, net[to[idx]]+++
dfs(idx + 1, net, count + 1)
// Deshacer
net[de[idx]]++, net[to[idx]]--
// Skip request idx
dfs(idx + 1, net, count)
`` `

**Pros**

- Intuitivo, fácil de depurar.
- Modelos directos “tomar / saltar” decisiones.

**Cons**

- `O(2^m)` profundidad de recursión (caso inferior `65k` llamadas) - todavía bien, pero puede ser lento en límites de tiempo ajustados.
- No poda a menos que agregue manualmente cheques (por ejemplo, si las solicitudes restantes no pueden compensar un desequilibrio actual).

-...

### 2.4 Optimización de Bitmask (El enfoque “bueno”)

Porque `m ≤ 16`, cada subconjunto de solicitudes puede ser representado como un entero de 16 bits. Enumerating all `2^m` subsets in a single loop is both **simple** and **fast**:

1. **Arriba sobre `masca'** de `0` a `(1 ' significar m) - 1`.
2. **Computar** el cambio neto para cada edificio mediante la iteración de bits en `mask`.
3. **Verificar** que todas las redes son cero (`O(n)` por subconjunto).

La complejidad total es `O(2^m * n)`, es decir, ≤ `65k * 20 ♥ 1.3M` operaciones primitivas – bien bajo 1 segundo.

■ ¿Por qué es esto mejor? * *
* Sin apilar.
• `mask.bit_count()` le da el número de solicitudes al instante.
* Usted puede prune un subconjunto temprano (`si (cuenta <= mejor) continuar;`).
* El código es casi idéntico en todos los idiomas.

-...

### 2.5 Las Pitfallas "Bad" para evitar

Silencio Pitfall Silencioso Explicación
Silencio----------------------------
Silencio **Omitiendo la `mejor ' poda** Silencio Comprobando todos los subconjuntos independientemente del `contra` tiempo de desperdicios. Silencio `si (cnt <= best) continúan;` Silencio
Silencio **Using `int[][]` for net in DFS without resetting** TEN Net array must be freshly cleared for each mask; otherwise previous subsets pollute the result. Silencioso `Arrays.fill(net, 0); ` Silencio
Silencio **Asumiendo que `m` será grande** Silencio Si `m` fueron ⇩ 20, bitmask explotaría. Use DFS + poda entonces. TEN Switch to recursive DFS with early exit. Silencio
Silencio **Ignorando `n` hasta 20** Silencio Si utilizas una variedad de tamaño 20 para la red, estarás bien. No hay preocupaciones de desbordamiento. Silencio `vectorado net(n,0);` en C++, `int[] net = new int[n]` en Java, `net = [0]*n` en Python. Silencio

-...

### 2.6 The “Ugly” Corner Cases

1. **Todas las solicitudes son idénticas**, por ejemplo, `[0,1],[0,1],[0,1].
*Solución:* El mejor subconjunto será ** incluso** (la red de cada edificio debe ser incluso). Bitmask lo maneja automáticamente.

2. **Circular chains** – `0→1`, `1→2`, `2→0`.
Cualquier solicitud por sí sola no puede satisfacer el equilibrio; usted necesita ** los tres** juntos.
Bitmask encontrará esto sin lógica extra.

3. **Solicitudes con `de == a`** – solicitudes triviales que no hacen nada.
Siempre se pueden tomar; bitmask automáticamente los incluye en el subconjunto óptimo.

4. **Large `n` (hasta 20)** pero pequeño `m`.
El array neto puede ser de hasta 20 elementos; iterating sobre él es insignificante.

-...

### 2.7 Complexity Analysis

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
← Recursive DFS Silencioso `O(2^m)` llamadas de recursión, cada llamada hace `O(n)` actualizaciones → `O(2^m * n)` Silencio `O(n)` (red array) + pila de recursión `O(m)` Silencio
Silencioso Bitmask Silencioso `O(2^m * n)` sin recidiva Silencio `O(n)` (net array)

Con `m ≤ 16` y `n ≤ 20`, la versión bitmask funciona en **sub-millisecond** en CPUs modernas.
Si desea escalar más allá de 16 solicitudes, cambie a DFS con poda ram-and-bound.

-...

### 2.8 Best‐Practice Checklist for Interviews

Silencio TENIDO TENIDO ANTERIENTE Checkpoint ANTE
Silencio...
Silencio **Leer el aviso cuidadosamente** – sólo necesita un equilibrio relativo, no cuenta el empleado absoluto. Silencio
TEN **Confirm constraints** – guían la opción algorítmica (bitmask vs DFS). Silencio
Silencio **Mejores casos de borde** – edificio único, solicitud única, todas las solicitudes se cancelan. Silencio
Silencio ** Funciones de ayuda de la palabra** – `esBalanced(net)` mantiene la lógica básica ordenado. Silencio
Silencio **Use integrado en bit-count** (`_construidoin_popcount` / `mask.bit_count()`) para velocidad. Silencio
← **Prune temprano** – saltar máscaras cuya 'cuenta' mejor'.
Silencio **Comentar el código** – los entrevistadores aman soluciones limpias y legibles. Silencio

-...

### 2.9 Sample Test Harness

``java
public static void main(String[] args) {
int n = 3;
int[][] req = {0, 0}, {0, 1}, {1, 2}, {2, 0};
System.out.println(new Solution().maximumRequests(n, req)); // → 3
}
`` `

■ Ejecutar el mismo arnés en Python o C++ traduciendo el snippet.
■ Use **assert** declaraciones o marcos de prueba unitaria para cubrir los casos de borde enumerados anteriormente.

-...

### 2.10 Interview Takeaway

Los mejores entrevistadores preguntan *Leetcode 1601* porque comprueba:

**Perspicacia comunitaria** – reconociendo que cada subconjunto es un candidato de solución factible.
**Tiempo de intercambio espacial** – elegir entre DFS y bitmask basado en el tamaño de entrada.
- ** Estilo de codificación Clean** – un algoritmo bien estructurado con comentarios muestra profesionalidad.

Practicar este problema agudizará su capacidad de:

- codificar las restricciones como ecuaciones de equilibrio*.
- Convertir opciones recursivas en bitmasks.
- Realizar enumeraciones rápidas cuando el espacio de búsqueda es pequeño.
- Discutir los intercambios con entrevistadores, convirtiendo un simple ejemplo de código en una conversación sobre la escalabilidad.

-...

### 2.11 Conclusión > Próximos pasos

- **Clone** el código snippets para Java, Python y C++ en su IDE local.
- **Añadir pruebas de unidad** cubriendo todos los casos de borde:
- No hay solicitudes → respuesta 0.
- Todas las solicitudes cancelan → respuesta m.
- Solicitudes que no pueden ser equilibradas → respuesta 0.
- Explique su enfoque a un amigo o en una entrevista de mock.
- **Añada el problema** a su lista Leetcode “Solved” y utilícelo como punto de conversación en su próxima entrevista.

■ **Listo para aterrizar su papel de ingeniería de software de sueño? * *
■ Problemas maestros como Leetcode 1601, practicar código limpio, y presentarlos con confianza en las entrevistas. ¡Buena suerte! 🚀

-...

### 2.12 SEO Etiquetas " Palabras clave

- `Leetcode 1601 `
- Número máximo de solicitudes de transferencia alcanzables `
- algoritmo de bitmask `
- " solución de retroceso `
- Entrevista de ingenieros de software `
- Solución `Java 17 `
- " Python 3 solution `
- Solución C++ `
- Práctica de entrevistas `
- " entrevista de trabajo problemas de codificación `

Siéntete libre de copiar, adaptar y publicar este artículo en Medium, Dev.to o tu blog personal. Los encabezados estructurados y el contenido de palabras clave enriquecido deben ayudar al puesto de correo en búsquedas como “Solución de código 1601”, “problemas de entrevistas retrocedentes”, o “cómo resolver problemas de solicitud de transferencia”.