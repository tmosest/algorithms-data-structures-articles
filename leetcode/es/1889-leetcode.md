-...
Título: LeetCode 1889. Residuos mínimos del espacio de embalaje -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 Problema general
**LeetCode 1889 – Residuo mínimo del espacio del embalaje (Hard)* *

Te dan

* `paquetes` - una variedad de 'n' enteros, cada uno que representa el tamaño de un paquete.
* `boxes` – a 2-D array of size `m`. `boxes[j]` contiene los diferentes tamaños de las cajas producidas por el proveedor `j`. Cada proveedor tiene un *infinito* suministro de cada uno de sus tamaños de caja.

Usted debe elegir **un proveedor** y utilizar **sólo sus tamaños de caja** para poner cada paquete en una caja separada.
Si se coloca un paquete de tamaño " p " en una caja de tamaño " b " , el espacio perdido es " b " p " .
El objetivo es minimizar el espacio total perdido en todos los paquetes.
Si es imposible ajustar todos los paquetes con cualquier proveedor, devuelva `-1`.
Debido a que la respuesta puede ser enorme, devuélvala modulo `10^9 + 7`.

■ *Examples*
■ 1. `packages = [2,3,5]`, `boxes = [4,8],[2,8]]` → **6**
■ 2. `packages = [2,3,5]`, `boxes = [1,4],[2,3],[3,4]] ' → **-1**
■ 3. `packages = [3,5,8,10,11,12]`, `boxes = [[12],[11,9],[10,5,14]]]` → **9**

-...

Estrategia de alto nivel
1. **Ordenar los paquetes** – facilita la búsqueda binaria.
2. **Construir un array de suma prefijo** de paquetes ordenados – nos permite calcular la suma de cualquier sub-segmento contiguo en O(1).
3. Para **cada proveedor**
* Clasificar sus tamaños de caja.
* Si la caja más grande es todavía más pequeña que el paquete más grande → *skip este proveedor*.
* Camine por los tamaños de la caja en orden ascendente.
* Para una caja de tamaño " b " , utilice ** búsqueda binaria** para encontrar el índice de paquete más grande `idx ' tal que `paquetes[idx] ≤ b ' .
* Todos los paquetes del índice anterior + 1 hasta `idx` será empaquetado en cajas de tamaño `b`.
* Computa el espacio perdido para ese segmento utilizando las sumas prefijo.
* Acumular los residuos para el proveedor actual.
4. Mantenga la pérdida **minimo** en todos los proveedores.
5. Si ningún proveedor puede caber todos los paquetes → devolver `-1`.
6. Else devuelve `minWaste % MOD`.

### Por qué funciona
* La clasificación asegura que cuando procesamos tamaños de caja en orden ascendente, todos los paquetes que encajan en una caja más pequeña ya se manejan; paquetes que necesitan cajas más grandes se quedan para cajas posteriores.
* búsqueda binaria (`upper_bound`) da el último paquete que se ajusta a un tamaño de caja dado en `O(log n)`.
* Las sumas de prefijo nos permiten calcular la suma de los tamaños de paquetes en un rango en `O(1)`, que es crucial para la eficiencia.

-...

## 📊 Complexity Analysis
*Let* `N = package.length` (≤ 105) y `M = número total de tamaños de caja en todos los proveedores ' (≤ 105).

*Sorting* `packages`: `O(N log N)`
*Sorting* lista de caja de cada proveedor: `O(M log M)` general
*Procesamiento* cada caja: una búsqueda binaria → `O(log N)`
Tiempo total: **O(N + M) log N)* *
Espacio: **O(N)** (para paquetes, sumas prefijas; más arrays temporales para cada proveedor).

-...

## 🛠ح Code Implementations

A continuación se encuentran soluciones limpias y de producción en **Java**, **Python**, y **C+**.
Cada uno sigue el algoritmo descrito anteriormente, maneja los casos de borde y utiliza el módulo 1 000 000 007.

-...

## Java

``java
importa java.util. Arrays;

Solución de la clase pública {}
int final estático privado MOD = 1_000_000_007;

public int minWastedSpace(int[] paquetes, int[][ cajas] {
int n = paquetes.length;
Arrays.sort(paquetes);

// Suma prefijo de tamaños de paquetes
largo[] prefijo = nuevo largo[n + 1];
para (int i = 1; i) = n; i++) {
prefijo[i] = prefijo[i] + paquetes[i] - 1);
}

mucho mejor = largo. MAX_VALUE;
booleano posible = falso;
más grande Paquete = paquetes[n] - 1);

para (int[] proveedor : cajas) {
Arrays.sort(supplier);
más grande Recuadro = proveedor[supplier.length - 1];
si (el más grandeBox) {
continuar; // este proveedor no puede adaptarse al paquete más grande
}
posible = verdadero;

desechos largos = 0;
int prev = -1; // último índice de paquete ya empaquetado

for (int boxSize : provider) {
[0] {}
continuar; // esta caja es demasiado pequeña para cualquier paquete
}
int idx = upperBound(paquetes, boxSize); // último paquete que se ajusta
suma largaPaquetes = prefijo[idx + 1] - prefijo[prev + 1];
numPackages largos = idx - prev;
desecho += numPackages * boxSize - sumPackages;
prev = idx;
}

mejor = Math.min(best, waste);
}

(int) (mejor % MOD) : -1;
}

// último índice donde los paquetes [i]
estática privada int upperBound(int[] arr, int target) {
int lo = 0, hola = arr.length - 1, ans = -1;
mientras (lo <= hola) {
int mid = lo + (hi - lo) / 2;
si (arr[mid]
ans = medio;
lo = mitad + 1;
. ♫ ... {
hola = mediados - 1;
}
}
devolver los ans;
}
}
`` `

-...

## Python 3

``python
importador bisect
de la importación Lista

MOD = 10**9 + 7

Solución de clase:
def minWastedSpace(self, packages: List[int], boxes: List[List[int]]) - título int:
n = len(paquetes)
paquetes.sort()

# Prefix sums
pref = [0]
para p en paquetes:
pref.append(pref[-1] + p)

más grande_pkg = paquetes [-1]
mejor = flotante('inf')
posible = Falso

para proveedor en cajas:
proveedor.sort()
si el proveedor [-1] se realizó mayor_pkg:
continuar # no puede caber el paquete más grande
posible = verdadero

desechos = 0
prev = 1

para caja en proveedor:
si la caja se ajusta a paquetes [0]:
continuar
idx = bisect.bisect_right(paquetes, caja) - 1
si idx 0 = prev:
continuar
sum_pkg = pref[idx + 1] - pref[prev + 1]
num_pkg = idx - prev
residuos += num_pkg * caja - sum_pkg
prev = idx

mejor = min (mejor, residuos)

int(mejor % MOD) si es posible más -1
`` `

-...

### C++ (17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
static constexpr long MOD = 1'000'007LL;

int minWastedSpace(vector seleccionadoint limitada paquetes, vector asignadovector seleccionadoint círculos {)
int n = package.size();
sort(packages.begin(), package.end());

// sumas prefijas
vector realizado largo tiempo anterior(n + 1, 0);
para (int i = 1; i) = n; ++i)
pref[i] = pref[i] + paquetes[i] - 1);

long long best = LLONG_MAX;
bool possible = false;
más grande Pkg = paquetes.back();

para (auto comprador : cajas) {
sort(supplier.begin(), provider.end());
si (supplier.back() < mayorPkg) continúan; // no cabe
posible = verdadero;

desechos largos = 0;
int prev = -1;

for (int box : provider) {
si (caja de paquetes.front()) se siguen; // demasiado pequeño para cualquier paquete
int idx = upperBound(paquetes, caja); // último paquete de fijación
larga suma Pkg = pref[idx + 1] - pref[prev + 1];
cnt largo largo = idx - prev;
residuos += cnt * caja - suma Pkg;
prev = idx;
}

best = min(best, waste);
}

volver posible ? static_cast seleccionado(mejor % MOD) : -1;
}

privado:
// último índice donde los paquetes [i]
int upperBound(cont vector identificadoint círculo arr, int target) {}
int lo = 0, hi = (int)arr.size() - 1, ans = -1;
mientras (lo <= hola) {
int mid = lo + (hi - lo) / 2;
si (arr[mid]
ans = medio;
lo = mitad + 1;
. ♫ ... {
hola = mediados - 1;
}
}
devolver los ans;
}
};
`` `

-...

## 📚 Blog Article – “Minimum Space Wasted from Packaging: Good, Bad & Ugly”

■ **Target Audience**: desarrolladores de software, entusiastas de entrevistas, reclutadores.
■ **Keywords**: Residuos mínimos del espacio de embalaje, LeetCode Hard, Binary Search, Prefix Sum, Java, Python, C++, entrevista de codificación, algoritmos, consejos de entrevista de trabajo, estructuras de datos, solución de problemas de entrevista.

-...

### ⋅ The Story (Good, Bad & Ugly)

Silencio Fase ANTERIOR Lo que sucedió ANTERIOR Por qué importa ANTETENIDO ANTERIENTE
Silencio----------------------------- La vida es...
Silencio **Bien** Silencio **Paquetes ordenados + sumas prefijo** nos dan un *simple* pero poderoso fundamento. tención permite consultas de rango O(1), que mantiene el algoritmo rápido. *Siempre* ordenar y procesar los datos antes de la iteración. Silencio
Silencio **Bad** Silencio **Large inputs** (105) nos obligan a considerar el *caso inferior* de tiempo de ejecución. Un enfoque ingenuo O(n2) no tendría tiempo. Muchos candidatos subestiman la necesidad de operaciones logarítmicas. tención Nunca asumir O(n2) es aceptable en 105 elementos. Silencio
Silencio **Ugly** Silencio **Skipping proveedores inutilizables** puede ser un error-prone si se olvida el cheque de “paquete más grande” ← Una sola supervisión puede llevar a un valor de desperdicios incorrecto `-1' o más grande. Prueba tu código en los casos de borde: sólo un paquete, todas las cajas del mismo tamaño, etc. Silencio

-...

### ♥ Why Interviewers Love This Problem
* **Te obliga a pensar en cómo *diferentes estructuras de datos* (arrayos, sumas prefijo, árboles de búsqueda binaria) interactúan.
* Muestra que puedes **balance pre-procesamiento y trabajo por proveedor** – un tema de entrevista común.
* Prueba **atención al detalle** (modulo aritmético, seguridad de 64 bits, manejo de bordes).

### 🌱 Cómo hacerlo en una entrevista técnica
1. **Explicar la intuición primero** (por qué clasificar las sumas de prefijo).
2. **Pasa por un simple ejemplo** sobre papel o pizarra.
3. **Declara tu complejidad** y por qué cumple con las limitaciones.
4. **Implement cleanly** – funciones modulares, nombres de variables adecuados y comentarios.
5. **Preguntar preguntas aclaratorias**: "¿Tenemos que usar exactamente las cajas que el proveedor ofrece?" “¿Se permite mezclar diferentes tamaños de caja del mismo proveedor?” (Se les permite explícitamente, pero sólo del proveedor elegido).

-...

### 🚀 SEO‐Friendly Summary

■ *Minimum Space Wasted From Packaging* – a **LeetCode Hard** problema que prueba la búsqueda binaria y prefijo suma mastery.
■ Este blog recorre la estrategia algorítmica, muestra el código Java, Python y C++, y explica por qué este enfoque es lo suficientemente eficiente para 105 puntos de datos.
■ Ya sea que se esté preparando para una entrevista de ingeniería **software**, un reto ** de codificación** o simplemente quiere profundizar su comprensión de *data‐structure-based optimization*, las soluciones aquí le darán un camino claro al éxito.

**Keywords**: Residuos mínimos del espacio de embalaje, LeetCode 1889, búsqueda binaria, Prefix Sum, Java, Python, C++, Problema de entrevista dura, Coding Interview Prep, Algorithms, Job Interview Tips, Software Engineering.

Codificación feliz – y que los residuos mínimos (y la llamada de entrevista) vengan a su manera! 🚀