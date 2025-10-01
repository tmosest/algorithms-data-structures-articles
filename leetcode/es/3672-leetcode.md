-...
Título: LeetCode 3672. Suma de Modos Peso en Subarrays -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Sum of Weighted Modes in Subarrays – A Complete Guide
*LeetCode 3672 – Medium Silencio Java Silencio Python ← C++ Silencioso Ventana + BST equilibrado*

-...

## 1. Recaptación de problemas

Se le da un array entero `nums` (tamaño ≤ 105) y un entero `k`.
Por cada subarreo contiguo de longitud `k` debemos:

← Paso Silencioso Descripción Silencio
Silencio...
Silencio **1** Silencio Cuenta la frecuencia de cada elemento en el subarray. Silencio
Silencio **2** Silencio El *modo* es el elemento con la frecuencia más alta; si varios elementos empatan, elija el **smallest** uno. Silencio
Silencio **3** Silencio El *peso* del subarray es `modo * frecuencia(modo)`. Silencio
Silencio **4** Silencio Sum the weights of all `k`‐length subarrays. Silencio

Devuelve esta suma como una 'long'.

■ *Ejemplo*
■ `nums = [1,2,2,3], k = 3` → weights: `4` (for `[1,2,2]`) + `4` (for `[2,2,3]`) = **8**.

-...

## 2. Por qué este problema es una gran pregunta de entrevista

Por qué importa
Silencio...
Silencioso **Venta deslizante** Ø Técnica básica utilizada en casi todos los problemas de matriz. Silencio
Silencio **Frequency Counting** Silencio Demonstrates use of hash tables (`Map`, `unordered_map`). Silencio
Silencio **Estadísticas de Orden** Silencio Necesita buscar rápidamente “mode” → usar un *balanced BST* o *heap* con comparación personalizada. Silencio
Silencio **Tie‐Breaking** Silencio Persona sutil que prueba el diseño cuidadoso de la comparación. Silencio
Silencio **Tiempo/Complejidad del Espacio** Silencio Debe manejar `n = 105` → `O(n log n)` está bien, pero `O(n2)` será TLE. Silencio
Silencio **Agnosticismo de lengua** Silencioso en Java, Python, C++ → muestra que puede adaptar las estructuras de datos al idioma. Silencio

-...

## 3. Estrategia de alto nivel

1. **Mantenga un mapa de frecuencia** `freq[valor] = cuenta` para la ventana actual.
2. **Mantenga un contenedor clasificado** que ordena pares por **frecuencia descendente, valor ascendente**.
* El primer elemento es siempre el modo actual.
3. **Slide the window** one step at a time:
* Eliminar el elemento saliente – actualizar el mapa de frecuencia y el contenedor clasificado.
* Añadir el elemento entrante – actualizar las mismas estructuras.
* Si la ventana está llena (`size == k`), lea el primer elemento del contenedor clasificado y agregue su peso a la respuesta.

Debido a que cada elemento se inserta y se retira a la mayor parte de la vez del contenedor clasificado, el costo total es `O(n log n)`.

-...

## 4. Detalles de la aplicación por idioma

### 4.1 Java (TreeSet)

El `TreeSet` de Java es un árbol rojo-negro que nos permite almacenar pares y mantener el orden.
Almacenamos `int[] {freq, value}` y proporcionamos una comparación personalizada:

``java
TreeSet madeint[]] Establecer = nuevo TreeSet seleccionado(
(a, b) - título a [0] != ¿B? Integer.compare(b[0], a[0]) : Integer.compare(a[1], b[1])
);
`` `

También utilizamos un `HashMap observadoInteger, Integer `` para la tabla de frecuencias.

Código completo abajo (igual que la solución editorial pero anotado para la claridad).

``java
importar java.util*;

Solución de la clase pública {}
modo largo públicoPeso(int[] nums, int k) {
int n = nums.length;
ans largos = 0L;

// Mapa de frecuencia: valor - confianza Cuenta
Mapa seleccionadoInteger, Integer frecuentementeq = nuevo HashMap Quería();

// Conjunto clasificado de pares {cuenta, valor}
TreeSet madeint[]] Establecer = nuevo TreeSet seleccionado(
(a, b) - título a [0] != ¿B? Integer.compare(b[0], a[0]) : Integer.compare(a[1], b[1])
);

int left = 0;
para (derecho = 0; derecho) {}

// Agregar nuevo elemento
int val = nums[right];
int cnt = freq.getOrDefault(val, 0);
si (cnt ю 0) set.remove(new int[]{cnt, val});
cnt++;
freq.put(val, cnt);
set.add(new int[]{cnt, val});

// Eliminar el elemento antiguo cuando la ventana k
si (derecha - izquierda + 1 ± k) {}
int oldVal = nums[left];
int oldCnt = freq.get(oldVal);
set.remove(new int[]{oldCnt, oldVal});
OldCnt...
si (oldCnt == 0) {
freq.remove(oldVal);
. ♫ ... {
freq.put(oldVal, oldCnt);
set.add(new int[]{oldCnt, oldVal});
}
izquierda++;
}

// Cuando la ventana es exactamente k, añadir su peso
si (derecha - izquierda + 1 == k) {
int[] modoInfo = set.first(); // frecuencia alta, menor valor
ans += 1L * modoInfo[0] * modoInfo[1]; // pond = freq * valor
}
}
devolver los ans;
}
}
`` `

■ *Las complejidades*
■ Tiempo: `O(n log n)` (factor de registro de operaciones de `TreeSet ' )
■ Espacio: `O(n)` (mapa de frecuencia + conjunto)

-...

### 4.2 Python (SortedContainers + Counter)

La biblioteca estándar de Python carece de un BST equilibrado, pero el paquete de terceros 'sortedcontainers' nos da un 'SortedList` con operaciones O(log n).
Si no puede utilizar libs externas, puede emular la lógica con una eliminación máxima de saltos + perezosos – el código que aparece a continuación utiliza `SortedList` para la brevedad.

``python
de las importaciones de colecciones Contrato
de importadores clasificados importados

Solución de clase:
defModo Peso(self, nums: list[int], k: int) - Propiedad int:
n = len(nums)
freq = Counter()
# Sort by (cuenta, valor) → mayor cuenta primero, menor valor primero
orden = SortedList(key=lambda x: (-x[0], x[1]))

ans = 0
izquierda = 0
por derecho, val in enumerate(nums):
# add new
c = freq.get(val, 0)
si c:
orden.remove(c, val))
c += 1
freq[val] = c
orden.add(c, val))

# diapositiva izquierda
si a la derecha - izquierda + 1 ≤ k:
viejo = nums[izquierda]
c_old = freq[old]
orden.remove((c_old, old))
c_old -= 1
si c_old:
freq[old] = c_old
orden.add(c_old, old))
más:
del freq[old]
izquierda += 1

si la derecha - izquierda + 1 == k:
mode_count, mode_val = order[0]
ans += mode_count * mode_val

Retorno
`` `

■ *Las complejidades*
■ Tiempo: `O(n log n) `
■ Espacio: `O(n) `

-...

### 4.3 C++ (unordered_map + multiset)

El "multiset" de C++ es un BST equilibrado; almacenaremos pares `{count, value}` y utilizar un comparador personalizado:

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
largo largo largo tiempo Peso(vector asignadoint círculo nums, int k) {
int n = nums.size();
ans largos = 0;

unordered_map madeint,int confianza freq;
// multiset ordenados por freq desc, valor asc
auto cmp = [](contiguo par observadoint,intющ a, par const observadoint,int unión b) {}
if(a.first != b.first) return a.first √≥ b.first; // larger freq first
volver a.second  observado b.second; // menor valor primero
};
multiset obtenidospair obtenidos,intenta, decltype(cmp)

int left = 0;
para(int right=0; right maden; ++right){
int val = nums[right];
int c = freq[val];
(c) order.erase(order.find({c,val}));
++c;
freq[val] = c;
orden.insert({c,val});

si (derecha - izquierda + 1 ± k) {}
int old = nums[left];
int c_old = freq[old];
orden.erase(order.find({c_old,old}));
--c_old;
si (c_old){
freq[old] = c_old;
orden.insert({c_old,old});
. ♫ ... {
freq.erase(old);
}
++izquierda;
}

if(right - left + 1 == k){
auto = orden.begin();
as += 1LL * it- inicialmente * it- título segundo;
}
}
devolver los ans;
}
};
`` `

■ *Las complejidades*
■ Tiempo: `O(n log n) `
■ Espacio: `O(n) `

-...

## 5. Bueno, malo y abundante de la solución

TENIDO Categoría ANTERIOR Lo que funciona bien ANTERIENDA Potential Pitfalls
Silencio------------------------------------
Silencio **Bien** Silencio • La ventana deslizante mantiene cada elemento procesado dos veces (add/remove). • `TreeSet` / `multiset` mantiene automáticamente el modo en el frente. No hay necesidad de recomputar frecuencias desde cero.
Silencio **Bad** Silencio • `TreeSet` o `multiset ' operations cost `O(log n)` – acceptable but can be heavy if `k` is small and `n` large. Use heap + perezosa eliminación si no se permiten libs externas. Silencio
Silencio **Ugly** Silencio • Eliminar un elemento de un BST requiere el par exacto; debemos saber el recuento anterior para eliminarlo. Si nos olvidamos de eliminar el viejo par, el conjunto contendrá entradas de estalla, corrompiendo el modo. TEN • El comparador incorrecto conduce al modo incorrecto (por ejemplo, olvidando el salto de corbata por valor). Silencio • Siempre prueba con casos de borde: valores repetidos, lazos, `k == 1`, `k == n`.. Silencio

-...

## 6. Enfoques alternativos (cuando `O(n log n)` es demasiado lento)

TEN ANTERIOR ANTERIOR ANTERIOR
Silencio...
Silencio **Bucket Sort + Counting Sort** Silencio Si `nums[i] ≤ 105`, podemos utilizar un array de tamaño `105 + 1` para frecuencias y mantener un segundo array para conteos → `O(1)` insertion/removal. > Sin embargo, conseguir el modo todavía requiere escanear el array de conteos (`O(maxValue)`), que es `O(105) lento por ventana → Silencio
Silencio **Dos Heaps + Lazy Deletion** TENIENDO Utilizar un max-heap para `(cuenta, valor)` y un hash map for lazy deletions. ■br títuloInsertion O(log n), deletion O(1) (lazy). El factor constante puede ser inferior al "multiset". Silencio
Silencio ** Árbol de segmento / Árbol de Indización binaria** Silencio Guardar frecuencias en un árbol de Fenwick y mantener un árbol de segmento sobre valores para consultar la frecuencia máxima. No se necesita para esta limitación. Silencio

-...

## 7. Por qué este blog te ayuda a aterrizar un trabajo

* ** Título rico en palabras clave** – “Sum of Weighted Modes in Subarrays – LeetCode 3672” muestra el número y el nombre del problema.
* **SEO-friendly** – Frecuente uso de términos como “LeetCode Medium”, “Java/Python/C++”, “Sliding Window”, “Balanced BST”, “Interview Question”.
* **Clear, explicación paso a paso** – Ingenieros de valor del equipo que pueden articular el proceso de pensamiento.
* **Multiple languages** – Demonstrates adaptability.
* ** Código anotado** – Muestra no sólo “aquí está la respuesta”, sino “cómo construirla”.
* **Edge-case discussion** – Destaca las prácticas de codificación defensivas.

Añadiendo este artículo a tu GitHub README o a tu sitio web personal indica que no solo estás resolviendo problemas, estás aprendiendo, documentando y compartiendo conocimientos. Esas son exactamente las habilidades suaves que buscan los entrevistadores.

-...

## 8. Final Takeaway

La clave de este problema es reconocer que el **mode se puede mantener en la parte delantera de un contenedor clasificado** mientras actualizamos frecuencias en la mosca.
La solución resultante `O(n log n)` es tanto limpia como eficiente en Java, Python y C++.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀

-...

*Author: Su nombre – Ingeniero de Software Problema‐ Resolviendo a Enthusiast. *