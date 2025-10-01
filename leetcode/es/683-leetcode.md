-...
Título: LeetCode 683. K Ranuras vacías -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 LeetCode 683 – **K Empty Slots**
■ **Hard** – 2 × 104 ≤ n, k ≤ 2 × 104

■ * Objetivo*
■ Encuentra el día más temprano** en el que dos bulbos que son **k + 1** posiciones separadas son ambos ON y todas las bombillas entre ellos son OFF.

-...

## 1. Idea de solución rápida
1. **Mantén la pista de las bombillas que ya están ON** en un árbol de búsqueda binaria balanceado* (TreeSet` / `set` / `SortedSet`).
2. Cuando una nueva bombilla en la posición 'p' se enciende:
* Mira la bombilla más cercana a la izquierda** (`abajo(p)`).
* Mira la bombilla más cercana a la derecha* (`superior(p)`).
3. Si alguno de los dos vecinos está exactamente `k + 1` posiciones de distancia → devolver el día actual.
4. Si el bucle termina → devolver `-1`.

■ ¿Por qué funciona? * *
■ La única manera de que un par de bombillas ON pueda tener *exactamente* `k` bulbos OFF entre ellos es si no hay otra bombilla ON en ese intervalo.
■ La bombilla más cercana en cada lado es el candidato *sólo* para satisfacer la condición.

■ *Las complejidades*
■ *Time*: **O(n log n)** – cada inserción " lookup es `log n ' .
■ *Espacio*: **O(n)** – almacenamos cada bombilla una vez.

-...

## 2. Aplicación del Código

#### 2.1 Java 17
``java
importa java.util. TreeSet;

Solución de la clase pública {}
int kEmptySlots(int[] bulbs, int k) {
TreeSet wonInteger confiar en = nuevo TreeSet identificado();
para (un día = 1; día == bulbs.length; day+) {
int pos = bulbos[día - 1];
on.add(pos);

Integer left = on.lower(pos);
Integer right = on.higher(pos);

si (izquierda!= null ' pos - izquierda - 1 == k) día de regreso;
si (derecha!= null ' derecha - pos - 1 == k) día de regreso;
}
retorno -1; // nunca encontrado
}
}
`` `

### 2.2 Python 3 (bisecto)
``python
de la importación de bisect_left

Solución de clase:
def kEmptySlots(self, bulbs: list[int], k: int) - confiar int:
on = [] # lista ordenada de posiciones ON
por día, pos in enumerate(bulbs, 1):
i = bisect_left(on, pos)
on.insert(i, pos)

# Left neighbour
si yo 0 y pos - on[i-1] - 1 == k:
Día de regreso
vecino derecho
si i+1 0 se hizo len(on) y on[i+1] - pos - 1 == k:
Día de regreso
retorno -1
`` `

### 2.3 C+17 (`std::set`)
``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int kEmptySlots(vector identificadoint ánimos, int k) {
establecidos:
para (un día = 1; día = = bulbs.size(); ++día) {
int pos = bulbos [día-1];
on.insert(pos);

auto = on.lower_bound(pos);

// vecino izquierdo
si (lo != on.begin()) {}
int left = *prev(it);
si (pos - izquierda - 1 == k) día de regreso;
}

// vecino derecho
auto nxt = siguiente(it);
si (nxt != on.end()) {}
int right = *nxt;
si (derecha - pos - 1 == k) día de regreso;
}
}
retorno -1;
}
};
`` `

-...

## 3. Artículo del Blog – “El Bien, el Mal, y el Ugly de LeetCode 683”

■ **Keywords**: *LeetCode 683*, *K Empty Slots*, *hard interview problem*, *Java TreeSet*, *Python bisect*, *C++ set*, *binary search tree*, *tratificador de entrevista de trabajo*

-...

#### 3.1 Introducción
En cada entrevista de ingeniería de software, el entrevistador le gusta mezclar un problema de *array clásico* con un giro *data‐structure*. LeetCode 683 “K Empty Slots” es un problema de este tipo. Te obliga a pensar en *reformaciones dinamicas* y *querías de vecinos* – habilidades que aparecen en sistemas reales como el desalojo de caché, la programación y la analítica de series temporales.

■ **Por qué este problema importa* *
• Demuestra tu comprensión de conjuntos ordenados** y ** reducción del espacio de investigación**.
* Prueba su capacidad para **optimizar** una fuerza bruta O(n2) en O(n log n).
* Te expone a la sutileza de las condiciones **bundantes** (k = 0, n = 1, etc.).

-...

### 3.2 The Naïve (Bad) Approach
Una solución de libro de texto O(n2) es, para cada día, comprobar cada par de bombillas ON y contar bombillas OFF entre ellas.
``text
por día en 1..n:
para mí en 1..day:
para j en i+1..día:
si las bombillas[i] y las bombillas [j] están en:
si la cuenta_off_between(i, j) == k:
Día de regreso
`` `
- **Tiempo**: O(n3) - demasiado lento para n = 20 000.
- **Espacio**: O(1).

■ *Por qué falla*: El doble bucle ya explota el tiempo de ejecución. Los entrevistadores modernos esperan que mejoren esto.

-...

### 3.3 El enfoque eficiente (bueno)
Usando un BST **balanced** (Java `TreeSet`, C++ `std::set`, Python `bisect`) nos permite:

1. Inserte cada posición de la bombilla en **O(log n)**.
2. Encontrar el *conservador* en la bombilla izquierda/derecha en **O(log n)**.
3. Compare distancias.

■ * Resultado*: **O(n log n)** tiempo, **O(n)** espacio.
■ Esta es la solución simple más rápida que puedes escribir sin recurrir a estructuras de datos más exóticas (árbol de segmento, árbol indizado binario, o unión con actualizaciones perezosas).

-...

### 3.4 Edge Cases " Pitfalls (The Ugly)

Silencio Escenario Silencioso Qué ver para Silencio
Silencio------------------
TENIDA `k == 0` Silencio Estás buscando bombillas adyacentes ON. El código todavía funciona porque `pos - left - 1` será `0`. Silencio
Silencio 1` Silencio No hay pareja → siempre `-1`. Silencio El bucle sale con `-1`. Silencio
El problema garantiza una permutación, por lo que esto no sucederá, pero en un sistema real que necesita para protegerse contra él. Silencio Use un `Set` para detectar duplicados pronto. Silencio
Silencio Muy grande `k ' (p. ej., ' k ' n ' ) tención Opcional pre-check `si k >= n: return -1`. Silencio
← Errores desactivados por uno ANTERIOR Recuerde que las posiciones en los `bulbos` son **1-indexed**, pero nuestros índices de bucle son **0-basados**. ← Utilizar `int pos = bulbs[día - 1];` y `para (un día = 1; día == bulbs.length; day++)`. Silencio

-...

### 3.5 What Interviewers En realidad buscamos

1. **Correcto**: Regrese el día más temprano*, no sólo cualquier día.
2. **La complejidad**: Explicar por qué O(n log n) es aceptable para n = 20 000.
3. ** Elección de la estructura de datos**: Justifique por qué un BST es un ajuste natural (solicitudes vecinas).
4. ** readability del proyecto**: Use nombres variables significativos ( " en " , " derecho " ) y comentarios.

-...

### 3.6 Takeaway for Your Next Interview

- Dominar la idea de *“vecino mejor en una colección ordenada”*; aparece en programación, networking e incluso desarrollo del juego.
- Práctica implementando la misma lógica en **Java, Python, y C++** – estarás listo para preguntas agnósticas de lenguaje.
- Recuerde discutir **edge cases**; a los entrevistadores les encanta ver que piensan en ellos.

-...

## 4. Pensamientos finales

LeetCode 683 es más que un rompecabezas de "golb-turning". Es un microcosmos de problemas algorítmicos del mundo real: tienes un conjunto dinámico de elementos y necesitas responder a las preguntas del rango rápidamente. Al dominar este problema, usted demostrará tanto el entendimiento teórico como los recortes prácticos de codificación —exactamente lo que los gerentes de contratación buscan.

¡Buena suerte en tu búsqueda de trabajo! 🚀