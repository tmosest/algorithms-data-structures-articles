-...
Título: LeetCode 1564. Poner cajas en el almacén I -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 Put Boxes Into the Warehouse I – The Complete “Good, Bad, Ugly” Guide
*(LeetCode 1564 – Media – Solución de entrevistas en Java, Python & C+++)*

■ **Descripción de Meta** – ¿Quieres poner las cajas de LeetCode en el almacén I? Este post te lleva a través de la intuición, una solución codicioso O(n log n) y código completamente probado en Java, Python y C++. Aprenda los enfoques *bueno*, *bad* y *muy*, y amplíe su résumé de entrevista con palabras clave optimizadas para SEO: **LeetCode, codicioso, clasificación, almacén, cajas, algoritmo, entrevista**.

-...

### 1. Panorama general de los problemas

Se le dan dos arrays:

* `boxes` – alturas de cajas de ancho unitario.
* `centro ' - alturas de habitaciones consecutivas (izquierda a derecha).

Reglas

1. Las cajas no se pueden apilar.
2. Puede reordenar las cajas arbitrariamente.
3. Las cajas se insertan de izquierda a derecha.
4. Si una caja es más alta que una habitación, y todas las cajas * detrás* se detienen antes de esa habitación.

** Objetivo** – devolver el número máximo de cajas que se pueden colocar en el almacén.

■ *Examples*
■ 1. `boxes=[4,3,4,1]`, `warehouse=[5,3,3,4,1]` → `3`
■ 2. `boxes=[1,2,2,3,4]`, `warehouse=[3,4,1,2]` → `3`
■ 3. `boxes=[1,2,3]`, `warehouse=[1,2,3,4]` → `1`

-...

### 2. Limitaciones

* `1 ≤ cajas. longitud, almacén. longitud ≤ 105 `
* `1 ≤ box[i], warehouse[i] ≤ 109 `

Así que se requiere un algoritmo **O(n log n)**; cualquier cosa peor será TLE.

-...

### 3. El enfoque Naïve / “Bad”

Una idea de fuerza bruta: prueba cada permutación de cajas y simula la inserción.
* Complejidad en el tiempo:* `O(n! · n)` – absolutamente imposible para `n = 105`.
* Por qué falla:* El espacio estatal explota; no hay manera determinista de decidir qué caja va donde sin explorar todas las órdenes.

-...

### 4. El "bien" Greedy Insight

Piense en el almacén de **derecha a izquierda**.
Mientras se mueve hacia la izquierda, la altura de la habitación **minimum** vista hasta ahora determina lo alto que una caja puede ser en ese segmento.

* Build an array `minPref[i]` = mínimo de `cuidado[0...i]`.
* Sort `boxes` ascendiendo.
* Comenzar desde la habitación más derecha (`i = almacén.length‐1`) y desde la caja más pequeña (`j = 0`).
* Si `minPref[i] ≥ cajas[j]`, la caja se ajusta → colocarlo, contadores de aumento.
* Muévete a la habitación siguiente (i‐1) y el siguiente cuadro (j+1).
* Para cuando las cajas estén agotadas o no más habitaciones.

Esta codiciada obra porque:
* Siempre tratamos de encajar la caja más pequeña posible en la sala restante “más restrictiva” (la que tiene la altura más baja permitido).
* Si la caja más pequeña no encaja, ninguna caja más grande encajará, así que saltamos esa habitación.

-...

### 5. Algoritmo (Código Pseudo)

`` `
cajas de clase ascendiendo
construir minPref[0...m-1] // m = warehouse.length
minPref[0] = almacén[0]
para i = 1 ... m- 1
minPref[i] = min(minPref[i-1], warehouse[i]

cnt = 0 // número de cajas colocadas
i = m-1 // habitación actual (de la derecha)
j = 0 // caja actual (de izquierda)

mientras que yo 0 y j
si minPref[i] >= box[j]
cnt++
j++ // caja del lugar
i... // pasar a la habitación anterior

retorno cnt
`` `

**Las complejidades* *

*Time* – `O(n log n)` for sorting + `O(n)` for prefix + `O(n)` bi-pointer scan.
*Pace* – `O(n)` para el array prefijo (puede ser `O(1)` si usted compute en la mosca).

-...

### 6. Lista de verificación Edge‐Case

Silencio Caso confidencialidad ¿Por qué importa?
Silencio...
← Empty `boxes` Silencio No hay cajas para colocar Silencio Regresar 0 inmediatamente Silencio
Silencio Empty `warehouse` Silencio No hay habitaciones para colocar en Silencio Regresar 0 Silencio
Silencio Todas las cajas más altas que la primera habitación Silencio Ninguno puede caber Silencio Greedy se saltará todas las habitaciones
Silencio Todas las habitaciones más bajas que la caja más pequeña.

-...

### 7. Código completo – Java, Python, C++

### 7.1 Java (Compatible con Java 17)

``java
importar java.util*;

Solución de la clase pública {}
int public int maxBoxesInWarehouse(int[] boxes, int[] warehouse) {}
si (boxes == null ANTERIÓ almacén == null Silencioso cajas.length == 0 Silencioso almacén.length == 0) {
retorno 0;
}

// 1 / ️ Ordenar cajas ascendiendo
Arrays.sort(boxes);

// 2 millas  Build Construir min prefijo de alturas de almacén
int m = warehouse.length;
int[] minPref = nuevo int[m];
minPref[0] = almacén[0];
para (int i = 1; i)
minPref[i] = Math.min(minPref[i - 1], warehouse[i]);
}

2 puntos de análisis codicioso
int i = m - 1; // índice de habitación (derecha a izquierda)
int j = 0; // índice de caja (esmallest a mayor)
int count = 0;

mientras (i не= 0 ' púrpura j {}
[j] {}
contar++; // colocar la caja
j++; // siguiente caja más pequeña
}
i--; // pasar a la habitación anterior
}
recuento de retorno;
}
}
`` `

#### 7.2 Python 3

``python
de la importación Lista

Solución de clase:
def maxBoxesInWarehouse(self, boxes: List[int], warehouse: List[int]) - título int:
si no cajas o no almacén:
retorno 0

# Sort boxes (ascending)
box.sort()

# Build min prefix of warehouse
min_pref = [0] * len(warehouse)
min_pref[0] = almacén[0]
para i en rango(1, len(warehouse)):
min_pref[i] = min(min_pref[i - 1], warehouse[i]

i, j, count = len(warehouse) - 1, 0, 0
mientras que yo >= 0 y j
si min_pref[i] box[j]:
Cuenta += 1
j += 1
I -= 1

cuenta de retorno
`` `

### 7.3 C++ (C+17)

``cpp
Incluido el título
#include >

Clase Solución {
public:
int maxBoxesInWarehouse(std::vector fielint limitada box, std::vector fieltro unidad reducida almacén) {}
si (boxes.empty() TENIDO ABOGADO.empty()) devuelve 0;

std::sort(boxes.begin(), boxes.end()); // ascending

int m = warehouse.size();
std::vector obtenidosint confianza minPref(m);
minPref[0] = almacén[0];
para (int i = 1; i)
minPref[i] = std::min(minPref[i - 1], warehouse[i]);

int i = m - 1, j = 0, count = 0;
mientras (i >= 0 " sensible j " cajas seleccionadas.size()) {}
[j] {}
++cuenta;
++j;
}
-i;
}
recuento de retorno;
}
};
`` `

-...

### 8. Examen de la aplicación

``python
# Ejemplo de ejecución en Python
sol = Solución()
print(sol.maxBoxesInWarehouse([4,3,4,1], [5,3,4,1])
print(sol.maxBoxesInWarehouse([1,2,2,3,4], [3,4,1,2])
print(sol.maxBoxesInWarehouse([1,2,3], [1,2,3,4])
`` `

Las pruebas de unidad en Java/C++ siguen el mismo patrón: instantánea `Solution`, llama al método y afirma la salida esperada.

-...

### 9. Consejos para entrevistas

← Tema Silencio Lo que los entrevistadores buscan para la vida Cómo esta solución ayuda a la vida
Silencio------------------------------------
Silencio **Greedy Reasoning** Silencio Habilidad para justificar “tomar la caja más pequeña que se adapte” ← Demuestra la lógica fuerte problema–solving
Silencio ** Análisis de la complejidad** escanear ¦ Shows awareness of time/space limits tención
Silencio ** Casos de Edge** Silencio Manejando entradas vacías, alturas extremas TENIDO Evita las trampas comunes
Silencio **Estilo de codificación** Silencio limpio, legible, uso de la clasificación integrada ¦
tención **Language Adaptability** ← Aplicar en Java/Python/C+++ tención Destaca la versatilidad para múltiples pilas de tecnología

-...

### 10. Conclusión - ¿Por qué este código se mete?

* **Simplicidad** – La lógica avaricia es fácil de explicar, por lo que puede articularla en una pizarra blanca.
* **Performance** – Conoce los límites estrictos de LeetCode (`elementos 105') mientras permanece altamente legible.
* **Cross‐Language** – Funciona en Java, Python y C++ – perfecto para adaptar tu curriculum vitae a una pila de tecnología que estás apuntando.

**Takeaway:** Mastering “Put Boxes Into the Warehouse I” muestra su capacidad de pensar codicioso, ordenar datos eficientemente, y escribir código limpio y listo para la producción – todo esencial para aterrizar ese próximo papel de ingeniería de software.

¡Feliz codificación! 🚀

-...

##### 📚 Más lectura
* LeetCode Discuss – [Simple Java solution](https://leetcode.com/problems/put-boxes-into-the-warehouse-i/solutions/5789805/simple-java-solution-by-sakshikishore-cwrh/)
* Algoritmos " Estructuras de datos - *Sorting " Two‐Pointer* chapter
* Preparación de entrevistas – * patrones de Algoritmo de granedía*

-...

**Keywords** – LeetCode, Put Boxes En el Almacén, algoritmo codicioso, clasificación, dos punteros, Java, Python, C++, prep de entrevista, entrevista de algoritmos, complejidad del tiempo, complejidad del espacio.