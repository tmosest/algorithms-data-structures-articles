-...
Título: LeetCode 3323. Minimizar Grupos Conectados insertando Interval -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Mastering LeetCode 3323: **Minimize Connected Groups by Inserting Interval**
■ *Java ← Python ← C++ – Una Solución deslizante-Window que pasa 1 e5*

-...

## 1. Panorama general de los problemas

Se le ha dado una serie de **intervalos** (cada `[start, end]`) y una longitud máxima permitida `k` para un intervalo *nuevo* que debe insertar exactamente una vez.
Después de insertar el intervalo, desea **minimise** el número de grupos conectados* de intervalos.

Un *grupo conectado* es un conjunto máximo de intervalos que juntos cubren un rango continuo sin huecos.
Ejemplo:

¿Conectado? Silencio
Silencio...
[[1,3],[3,5],[5,6]] " TENIENDO (cubrimientos 1-6) TENIDO
Silencio `[1,2],[3,4].

**Retorno** el menor número posible de grupos conectados después de añadir el nuevo intervalo.

■ **Constraints**
* 1 ≤ `intervals.length` ≤ 105
* 1 ≤ `start` ≤ `end` ≤ 109
* 1 ≤ `k` ≤ 109

-...

## 2. Por qué este problema es difícil

* **Large Input Size** – O(n log n) es aceptable, pero cualquier cosa cuadrática será TLE.
* **La inserción debe cubrir los gaps** – No se puede simplemente “merge” intervalos; tiene que pensar en cómo el nuevo intervalo puede abarcar **multiple** vacíos a la vez.
* ** Ventana deslizante en gaps** – El truco clave es tratar las brechas entre intervalos fusionados como una secuencia y utilizar una ventana deslizante para encontrar la subsecuencia contigua más larga de vacíos que pueden ser cubiertos por un solo intervalo de longitud ≤ k.

-...

## 3. Examen básico

1. **Merge los intervalos dados** – Después de fusionarse, cada par consecutivo de intervalos fusionados está separado por un *gap* de longitud `gapStartGapEnd`.
2. # Los gaps están ordenados # Debido a que arreglamos los intervalos originales por principio, los huecos están automáticamente en orden ascendente de sus posiciones de inicio.
3. **Cover un bloque contiguo de brechas** – Si elegimos una ventana `[l ... r]` de brechas, el nuevo intervalo debe abarcar desde el *start* de la primera brecha hasta el *end* de la última brecha.
* Longitud requerida* = `gaps[r].end - gaps[l].start`.
4. **Venta deslizante** – Mover un puntero derecho, ajustar el puntero izquierdo cuando la longitud requerida exceda `k`. Realice un seguimiento del número máximo de lagunas ( " r-l+1 " ) que caben dentro del límite.
5. **Respuesta** – Cada brecha fusionada reduce el recuento del grupo por uno.
\[
\text{answer} = \text{groups} ##\text{gaps} = (\text{gaps} + 1) - \maxCovered = \text{groups} - \maxCovered
\]

-...

## 4. Pasos del algoritmo

1. **Los intervalos de reserva** comienzan a ascender; si es igual, al final descendiendo (para que podamos combinar fácilmente).
2. **Merge** intervalos superpuestos o táctiles → `merged`.
3. **Recoge las brechas** entre los intervalos consecutivos de `merged` → `gaps`.
4. **Venta flotante en vacíos**
* `l = 0`, `maxCovered = 0`
* For each `r ' in `[0 ... gaps.size-1] `
* While `requiredLength > k`, increase `l`.
* Update `maxCovered = max(maxCovered, r-l+1)`.
5. **Retorno** `merged.size() - MaxCovered`.

-...

## 5. Análisis de la complejidad

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio Ordenar Silencio **O(n log n)** Silencio O(1) auxiliar (sorting in place)
TENIDO ANTERIOR ANTERIENTE **O(n)**
*m* = merged.size() Silencio O(m) Silencio
Silencioso Ventana aguante **O(m)**
Silencio **Total** Silencio **O(n log n)** Silencio **O(n)** (el peor caso para las lagunas)

Esto satisface cómodamente las limitaciones.

-...

## 6. Implementación - Java

``java
importar java.util*;

Solución de la clase pública {}
public int minConnectedGroups(int[][] intervalos, int k) {
si (intervalos == null TENIDO intervalos.length == 0) retorno 0;

// 1. Ordenar por principio; salto de corbata por fin descendiendo
Arrays.sort(intervalos, (a, b) - título {
si (a[0] == b[0]) devuelve Integer.compare(b[1], a[1]);
integer.compare(a[0], b[0]);
});

// 2. Intervalos de fusión
Lista obtenida[]]]] fusionado con el nuevo ArrayList recomendado();
int curStart = intervalos[0][0];
int curEnd = intervalos[0][1];
para (int i = 1; i) i++) {
int[] cur = intervalos[i];
si (cur[0] <= curEnd) { // solapamiento o tacto
curEnd = Math.max(curEnd, cur[1]);
} más { // disjoint
merged.add(new int[]{curStart, curEnd});
curStart = cur[0];
curEnd = cur[1];
}
}
merged.add(new int[]{curStart, curEnd});

// 3. Reunir brechas entre intervalos fusionados
int m = merged.size();
(m == 1) retorno 1; // sólo un grupo, nada a puente
Lista obtenida[] brechas de confianza = nuevo ArrayList correctamente();
para (int i = 0; i)
int end1 = merged.get(i)[1];
int start2 = merged.get(i +1)[0];
brechas.add(new int[]{end1, start2}); // gap: (end1, start2)
}

// 4. Ventana deslizante sobre las lagunas
int l = 0, maxCovered = 0;
para (int r = 0; r)
// longitud requerida para cubrir las lagunas[l.r]
mientras (l <= r " divide.get(r)[1] - gaps.get(l)[0] √≥ k) {}
l++;
}
maxCovered = Math.max(maxCovered, r - l + 1);
}

// 5. Resultado: grupos - maxCovered
retorno merged.size() - maxCovered;
}
}
`` `

-...

## 7. Implementación - Python

``python
de la importación Lista

Solución de clase:
def minConnectedGroups(self, intervals: List[List[int], k: int) - título int:
intervalos.sort(key=lambda x: (x[0], -x[1]))

# Merge
merged = []
cur_start, cur_end = intervalos[0]
para s, e en intervalos[1:]:
si s <= cur_end: # overlap / touch
cur_end = max(cur_end, e)
más:
merged.append(cur_start, cur_end))
cur_start, cur_end = s, e
merged.append(cur_start, cur_end))

si len(merged) == 1:
Regreso 1

# Gaps
deficiencias = []
for (s1, e1), (s2, e2) in zip(merged, merged[1:]):
(e1, s2)) # (end_of_first, start_of_second)

# Sliding window
l = 0
max_covered = 0
para r en rango(len(gaps)):
mientras que l <= r y huecos[r][1] - huecos[l][0]
l += 1
max_covered = max(max_covered, r - l + 1)

len(merged) - max_covered
`` `

-...

## 8. Implementación - C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minConnectedGroups(vector identificadovector fielint implica intervalos, int k) {
(intervalos.begin(), intervalos.end(),
[](cont vector identificadoint ánimo a, const vector identificadoint círculo b) {
si (a[0] == b[0]) devuelven un[1]  título b[1];
devolver a [0]
});

// Intervalos de fusión
vector asignado a cabo largo largo, largo tiempo fusionado;
long curStart = intervalos[0][0];
long curEnd = intervalos[0][1];
para (size_t i = 1; i) ++i) {
largo s = intervalos[i][0];
largo e = intervalos[i][1];
si (s <= curEnd) { // solapamiento
curEnd = max(curEnd, e);
. ♫ ... {
merged.emplace_back(curStart, curEnd);
curStart = s;
curEnd = e;
}
}
merged.emplace_back(curStart, curEnd);

si (merged.size() == 1) retorno 1;

// Gaps entre intervalos fusionados
vector asignado a cabo largo largo, largo tiempo deficiencias;
para (size_t i = 0; i + 1 se merged.size(); ++i) {
long end1 = merged[i].second;
long long start2 = merged[i + 1].first;
gaps.emplace_back(end1, start2); // (end, start)
}

// Ventana deslizante sobre las lagunas
size_t l = 0, maxCovered = 0;
para (size_t r = 0; r) ++r) {
mientras (l) {}
++l;
}
maxCovered = max(maxCovered, r - l + 1);
}

volver estática_cast seleccionado(merged.size() - maxCovered);
}
};
`` `

-...

## 9. Casos de borde dirigidos

Edge tóxico Cómo lo manejamos
Silencio...
Silencio No hay intervalos Silencio Regreso 0 (a diferencia debido a las limitaciones)
Silencio Todos los intervalos ya superpuestos → un grupo TEN Vuelta 1 inmediatamente TENIDO
Silencio Nuevo intervalo no puede cubrir ninguna brecha Silencio `maxCovered = 0`, respuesta = `grupos` Silencio
Silencio Gaps exactamente de longitud `k` Silencioso Ventana los incluye (≤ k)

-...

## 10. Pruebas – Prueba de unidad rápida (Java)

``java
public static void main(String[] args) {
int[] a = {1, 3}, {3, 5}, {6, 7}, {8, 9}, {10, 11}};
System.out.println(new Solution().minConnectedGroups(a, 4)); // expected 2
}
`` `

Ejecute la misma prueba en Python y C++ para confirmar la consistencia.

-...

## 11. Take-Away for Your Interview

* **Siempre piensa en fusionarse primero** – Reduce el problema a una secuencia lineal de vacíos.
* **Tratar brechas como la estructura principal de datos** – Son las únicas partes que puedes “puente”.
* **Use una ventana corredera** – La técnica clásica de dos puntos se aplica incluso cuando la limitación de la ventana depende de una diferencia computada (`gapEnd - gapStart`).
* **Cuidado con el flujo entero** – Gaps y longitudes requeridas pueden alcanzar 109, por lo que utilizar 64 bits (Java `long`, C++ `long long`, Los enteros nativos de Python).

-...

## 12. Lectura adicional " Problemas relacionados

* **“Número máximo de intervalos no superpuestos”** – ventana corredera clásica
* **“Merge Intervals”** – problema fundamental en la manipulación de intervalos
* **“Subarray más largo con suma ≤ k”** – ventana corredera analógica para sumas

-...

## 13. Veredicto final

Con la estrategia de ventanilla de fusión-gap-sliding, el problema se convierte en una cuestión de **un pase lineal** después de ordenar.
Esta solución elegante no sólo pasa los límites de tiempo, sino que también le da una base de código limpia y mantenible en Java, Python y C++.

■ ¡Feliz codificación!

-...

■ **Keywords**: intervalo de fusión, brechas, ventana deslizante, LeetCode, entrevista de algoritmo, complejidad de tiempo O(n log n).