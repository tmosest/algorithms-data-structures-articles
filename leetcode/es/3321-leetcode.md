-...
Título: LeetCode 3321. Encontrar X-Sum of All K-Long Subarrays II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 3321 – “Find X‐Sum of All K‐Long Subarrays II”
*Solución en **Java**, **Python**, y **C+** + un blog amigable con SEO que explica lo bueno, lo malo y lo feo. *

-...

## Problema Recap

■ Dado un array `nums` (length *n*), y dos enteros `k ' y `x`.
■ Por cada subarreo contiguo de longitud `k`
■ 1. Contar la frecuencia de cada elemento.
■ 2. Mantener los elementos más frecuentes **top " x " *
■ *Si dos elementos empatan en frecuencia, el valor mayor gana. *
■ 3. Invocar los elementos guardados (o todo el subarray si tiene menos de los " valores distintos " ).
■ Devuelve un array de estos "X‐Sums" para todas las ventanas correderas.

-...

## 1. La Idea Core – Dos Multisets + Ventana deslizante

TENIDO ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------------...
*Linear‐time escaparate* – sólo actualizaciones `O(n)` por movimiento Silencio *Requiere la comparación personalizada* – difícil en algunos idiomas Silencio *Lazy deletion for heaps* – puede oscurecer errores latitud
Silencio *Exacto O(1) suma de mantenimiento* – mantener una suma de funcionamiento de la parte superior `x` Silencioso *Uso de espacio* – dos multisets + mapa de hash (`O(n)` peor caso)
*Determinación de la corbata determinista* – mayor valor gana cuando las frecuencias se atan a la vida *Antes a la razón* – especialmente cuando `k == x` (todo ventana es siempre resumido) Silencio * Manejo de caso de edge* – freq va a 0, elemento desaparece ←

### Cómo funciona

Silencio Silencio Silencio Silencio Silencio
Silencio...
Mantener frecuencias** – `freq[valor]` en un mapa de hash. Silencio
Silencio **2. Dos multisets** –
TEN TENIDO `grande` - contiene en la mayoría de los elementos 'x', el actual "top x".
TENIDO TERRITORIO `pequeño' - todos los elementos restantes. Silencio
Silencio **3. Orden** – multiset se ordena **ascending** por `(frecuencia, valor)`.
*Primero* (`smallest`) en `grandecimiento` es el candidato más débil para demoler.
*Últimamente* ( " más grande " ) en `pequeña ' es el candidato más fuerte para promover. Silencio
Mantener `sumLarge`** – suma de todos los elementos en `grandecimiento ' . Silencio
tención **5. En cada cambio de ventana** – añadir nuevo elemento, eliminar el elemento viejo, luego reequilibrar `grande `` ' para satisfacer la invariable `Principal vida útil == x` (o todos los valores distintos si menos). Silencio

Debido a que cada elemento se inserta y se elimina exactamente una vez por ventana deslizarse, todo el algoritmo es `O(n log n)` (el 'log n` viene de operaciones multiset).

-...

## 2. Aplicación de las referencias

A continuación encontrarás un código limpio y listo para la producción para **Java**, **Python**, y **C+** que puedes pegar a tu editor o utilizar como referencia para tus propias soluciones.

■ **Consejo:** Todas las soluciones utilizan aritmética de 64 bits ( " largo " / " largo " ) porque la suma puede exceder `int32`.

-...

### 2.1 Java (TreeSet + HashMap)

``java
importar java.util*;

*
* LeetCode 3321 – Find X‐Sum of All K‐Long Subarrays II
*/
Solución de la clase pública {}
Clase privada estática Par implementa Comparable {
valor int final; // valor de elemento
int freq; // frecuencia actual

Pareja(valor int freq) {
esto. valor = valor;
este.freq = freq;
}

@Override
public int compare A(Pair o) {
si (este.freq != o.freq) devuelve Integer.compare(este.freq, o.freq);
integer.compare(este.valor, o.value);
}

@Override
booleano público igual(Objeto o) {
regreso o instancia de Par p '
p.value == this.value " p.freq == this.freq;
}

@Override
public int hashCode() {
devolver objetos.hash(valor, freq);
}
}

final privado Mapa seleccionadoInteger, Integer frecuentementeq = nuevo HashMap Quería();
Árbol final privadoSet seleccionadaPair título grande = nuevo TreeSet fiel();
Árbol final privadoSet seleccionadaPair título pequeño = nuevo TreeSet fiel();
suma larga privadaLarge = 0; // suma de elementos en 'grandecimiento '

// helper para actualizar la frecuencia de un valor
cambio de vacío privadoFreq(int val, int delta) {}
int oldF = freq.getOrDefault(val, 0);
int newF = oldF + delta;
si (newF " 0 " ) lanzan nuevas ilegalStateException();

Pareja de edadPair = nuevo par(val, vejezF);
Par nuevoPair = nuevo par(val, nuevoF);

// eliminar el par viejo de cualquier conjunto que pertenece a
si (grande.contains(oldPair)) {
big.remove(oldPair);
sumLarge -= (long) oldF * val;
si 0) {
grande.add(newPair);
sumLarge += (long) newF * val;
. ♫ ... {
// freq se convierte en 0 - título gota completamente
freq.remove(val);
retorno;
}
} si (small.contains(oldPair)) {}
pequeño.remove(oldPair);
si (newF > 0) small.add(newPair);
más freq.remove(val);
} otro { // elemento no estaba presente antes
si 0) {
pequeño.add(newPair);
. ♫ ... {
retorno; // nada que hacer
}
}

si (newF > 0) freq.put(val, newF);
}

// reequilibrio grande/pequeño para mantener la vida grande x
rebalance privado vacío(int x) {
// pasar de pequeño a grande si es necesario
mientras (grande.size() Ге x " golpe !small.isEmpty()) {}
Par aMove = pequeño.últ(); // más fuerte en pequeño
pequeño.remove(toMove);
grande.add(toMove);
sumLarge += (long) toMove.freq * toMove.value;
}

// demote más débil grande a pequeño
mientras (!small.isEmpty() " grande.size()
Par aMove = grande.primer(); // más débil en grande
big.remove(toMove);
sumLarge -= (long) toMove.freq * toMove.value;
pequeño.add(toMove);
}

// swap si un elemento más fuerte está sentado en pequeño
si (!large.isEmpty() " ventaja !small.isEmpty() {)
Pareja más débilLarge = grande.
Pareja más fuerte Small = small.last(); // más fuerte entre el resto

if (strongestSmall.freq ⇩ más débilLarge.freq  durable
(más fuerteSmall.freq == más débilLarge.freq
más fuerteSmall.value не más débilLarge.value) {}

// democión más débil Grande
big.remove(weakestLarge);
sumLarge -= (long) weakestLarge.freq * weakestLarge.value;
pequeño.add(weakestLarge);

// promover más fuerte Pequeñas
pequeño.remove(strongestSmall);
big.add(strongestSmall);
sumLarge += (long) más fuerteSmall.freq * más fuerteSmall.value;
}
}
}

int[] getXSum(int[] nums, int k, int x) {
int n = nums.length;
int[] ans = nuevo int[n] - k + 1];

para (int i = 0; i < k; i++) cambioFreq(nums[i], 1);
rebalance(x);
as[0] = (int) sumLarge;

para (int i = 1; i <= n - k; i++) {
cambio Freq(nums[i - 1], -1); // remove leftmost
cambioFreq(nums[i + k - 1], 1); // añadir new rightmost
rebalance(x);
as[i] = (int) sumLarge;
}

devolver los ans;
}
}
`` `

**Por qué esta es la implementación “buena” de Java* *

- `TreeSet` garantiza *log‐n* inserción / eliminación en **O(1)** tiempo por operación.
- `Pair` tiene la frecuencia *currente*, por lo que podemos recomputar la suma en la mosca.
- El invariable ` duraciónlarge sufrimiento == x` es restaurado con un pequeño lazo, manteniendo la lógica legible.

-...

### 2.2 Python (dos montones + perezosa eliminación)

``python
importación heapq
de las colecciones importadas por defecto
de la importación Lista

# ------
# LeetCode 3321 – Python (heap + lazy deletion)
# ------
Solución de clase:
def xSum(self, nums: List[int], k: int, x: int) - título List[int]:
n = len(nums)
ans = []

freq = defaultdict(int) # elemento - título frecuencia

# Min‐heap for 'large' (top‐x)
grande = [] # (freq, value)
# Max‐heap for 'small' (todo lo demás)
pequeño = [] # (-freq, -valor)
sum_large = 0
tamaño_grande = 0

def clean(heap, invert):
"""Pop stale entries whose frequency no longer match.""
Mientras salta:
f, v = heap[0]
real_f = freq.get(v, 0)
si real_f == 0 o real_f != f:
heapq.heappop(heap) # discard stale
más:
descanso

def rebalance():
no local sum_large, size_large
# Sube de pequeño a grande si tenemos espacio
mientras que tamaño_grande Гле x y pequeño:
f, v = heapq.nlargest(1, pequeño)[0]
heapq.heappop(small)
heapq.heappush(large, (f, v))
sum_large += f * v
tamaño_grande += 1

# Demote más débil si tenemos demasiados
mientras que tamaño_grande Ø x y grande:
f, v = heapq.nsmallest(1, grande)[0]
heapq.heappop(large)
sum_large -= f * v
heapq.heappush(small, (-f, -v))
tamaño_grande -= 1

# promover más fuerte pequeño si golpea más débil grande
pequeño y grande:
# más fuerte en pequeño: más grande (-f, -v)
sf, sv = -small[-1][0], -small[-1][1]
lf, lv = large[0] # weakest large
si sf > lf o (sf == lf y sv œlv):
# Demote débil más grande
heapq.heappop(large)
sum_large -= lf * lv
heapq.heappush(small, (-lf, -lv))
# promote strongest small
heapq.heappop(small)
heapq.heappush(grande, (sf, sv))
sum_large += sf * sv
más:
descanso

# ---------- Ventana deslizante principal...--------
para i en rango(k):
v = nums[i]
freq[v] += 1
heapq.heappush(grande si len(grande)
(freq[v], v)

# After first window, build heaps properly
para v, f en freq.items():
si f > 0:
heapq.heappush(grande si len(grande)
f, v)
rebalance()
ans.append(int(sum_large))

para i en rango(k, n):
# Turn window
viejo = nums[i - k]
nuevo = nums[i]
freq[old] -= 1
freq[new] += 1

# push new entries (lazy deletion will handle stale ones)
si freq[old] == 0:
del freq[old]
heapq.heappush(grande si len(grande)
(freq.get(old, 0), old))
heapq.heappush(grande si len(grande)
(freq[new], new)

rebalance()
ans.append(int(sum_large))

Retorno
`` `

■ **Advertencia:** La versión de Python anterior es **conceptual** - la lentitud de la eliminación (`heapq` + mapa de frecuencia) funciona pero puede ser un poco lento para el gran `n`. En la práctica, puede sustituir los dos montones por " bisect.insort " en una lista ordenada ( " biblioteca de contenedores " ) para una aplicación más limpia.

-...

### 2.3 C++ (multiset + unordered_map)

``cpp
#include יbits/stdc++.h
usando std namespace;

/*
* LeetCode 3321 – Find X‐Sum of All K‐Long Subarrays II
*/
Clase Solución {
public:
struct Pair {}
int val; // elemento value
int freq; // frecuencia actual

Par(int v, int f) : val(v), freq(f) {}
// ascender por (freq, val)
bool operadores realizados(contiguos pares o) const {
si (freq != o.freq) devolver freq
retorno val
}
};

vector implicado xSum(vector fieltro nums, int k, int x) {
unordered_map madeint, int confianza freq;
multiset realizadoPair título grande, pequeño;
Large = 0;
int n = nums.size();
vector implicado un(n - k + 1);

auto update = [ cl](int val, int delta) {}
int oldF = freq.count(val) ? freq[val] : 0;
int newF = oldF + delta;
si (newF 0) lanza lógica_error(" frecuencia negativa");

Pareja de edadPair(val, vejezF), nuevoPair(val, nuevoF);

si (grande.count(oldPair)) {
big.erase(large.find(oldPair));
sumLarge -= 1LL * oldF * val;
si 0) {
big.insert(newPair);
suma Grande += 1LL * nuevoF * val;
}
} si (small.count(oldPair) {
pequeños.erase(small.find(oldPair));
si (newF > 0) small.insert(newPair);
} otro { / / / primera aparición
si (newF > 0) small.insert(newPair);
}

si (newF > 0) freq[val] = newF;
más freq.erase(val);
};

auto-rebalance = [ Pulido](int x) {
// llenar grande si es posible
mientras (grande.size() se hacía (size_t)x " sensible !small.empty()) {}
auto = prev(small.end()); // más fuerte en pequeño
sumLarge += 1LL * it- Conffreq * it- títuloval;
big.insert(*it);
pequeña.erase(it);
}
// demote más débil grande si tenemos demasiados
mientras (!small.empty() " grandes.size() {}
auto = pequeño.end(); // más fuerte pequeño (no necesario aquí)
/ // en realidad sólo demoteamos cuando grande
auto itLow = grande.begin(); // más débil grande
sumLarge -= 1LL * itLow- Conffreq * itLow- Confval;
Small.insert(*itLow);
big.erase(itLow);
}
// promover si un pequeño ritmo más fuerte un grande más débil
mientras (!small.empty() " ventaja !) {}
auto débilLarge = grande.begin();
auto fuerte Small = prev(small.end());
si (strongSmall-propfreq weakLarge-Lofreq
(strongSmall-propfreq == weakLarge-nciafreq "
strongSmall- confíaval îbleLarge- títuloval) {
sumLarge -= 1LL * weakLarge- Conffreq * weakLarge-Convalida;
big.erase(weakLarge);
suma Grande += 1LL * fuerteSmall- Conffreq * fuerte Small-conval;
big.insert(*strongSmall);
pequeña.erase(strongSmall);
} más romper;
}
};

// ventana inicial
para (int i = 0; i) 1);
rebalance(x);
ans[0] = static_cast fielint(sumLarge);

para (int i = 1; i) = n - k; ++i) {}
update(nums[i - 1], -1); // remove leftmost
actualización(nums[i + k - 1], 1); // añadir new rightmost
rebalance(x);
ans[i] = static_cast fielint(sumLarge);
}
devolver los ans;
}
};
`` `

■ La versión C++ refleja la lógica Java, pero se beneficia de los iteradores *bidirectionales* de 'multiset', haciendo el swap / promover lógica succinct.

-...

## 3. Key Takeaways for a Production‐ Solución lista

Silencio Idioma Silencio Data‐structure Silencio Complejidad
Silencio------------------------------...
Silencio **Java** Silencio `TreeSet No se hizo realidadPair confianza `` Silencio O(n log k) Silencio Mantenimiento invariable simple, pedido incorporado. Silencio
Silencio **Python** Silencio `heapq` + `defaultdict` (lazy deletion) Silencio O(n log k) Silencio Obras pero pueden ser lentas; use lista ordenada si la velocidad importa. Silencio
Silencio **C++** Silencio `multiset madePair ``  durable O(n log k) Silencio Control completo sobre los iteradores, baja sobrecarga. Silencio

**Qué hace la solución “buena”* *
- **Actividades de troncos predecibles** a través del árbol equilibrado o el montón.
- **Mantenimiento de sumas flexibles** - evitar recomputar desde cero por cada ventana.
- **Rehabilitación invariable total** - Mantener `vivienda grande == x` con lazos mínimos.
- **Evitar objetos temporales excesivos** – actualizar las estructuras de datos existentes.

-...

#### TL;DR

- **Use un árbol equilibrado (TreeSet` / `multiset`)** en Java, C++, o C++ para hacer un seguimiento de los elementos 'k' y mantener el sub-set top‐x.
- ** Actualizar frecuencias en cada diapositiva**, ajustando la suma en la mosca.
- **Reequilibrio** cuando el número de elementos en los cambios de configuración superior o cuando aparece un elemento más fuerte en el resto.

Esto produce una solución elegante, rápida y sostenible para el problema ** "X‐sum de una ventana deslizante"**.