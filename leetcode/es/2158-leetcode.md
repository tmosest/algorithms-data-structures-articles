-...
Título: LeetCode 2158. Cantidad de Nueva Zona Pintada Cada Día -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 2158 – * Cantidad de Nueva Zona Pintada Cada Día*
**LeetCode Hard tención Entrevista-Ley Solución en Java, Python & C++**

■ ¿Quieres mostrar a los reclutadores que puedes resolver un problema *hard* LeetCode en **O(n log n)** tiempo?
■ Aquí hay una implementación limpia y lista para la producción, un paso a paso del algoritmo, y un artículo listo para el blog que puede copiar para pasar a Medium, Dev.to, o su cartera personal.

-...

## Tabla de contenidos

Silencio Sección Silencio Lo que aprenderás
Silencio...
Silencio 📌 Problema Declaración Silencio El desafío exacto de LeetCode
TENIDO TENIDO Ejemplos TENIDO 3 muestras de insumos / salidas
Silencio | Limitaciones de tamaño y implicaciones
Silencio 🔧 Solution Resúmenes ¿Por qué un `TreeMap` / `map` funciona
TEN 📚 Algorithm Walk‐through TENCIÓN Intervalos de fusión + computación nueva área Silencio
TENIDO Código en tres idiomas ANTE Java, Python, C++ TENIDO
← Tiempo > Complejidad del Espacio O analysis confidencialidad
Silencio ❓ Pitfalls comunes 
Н 🚀 SEO > Consejos de carrera ← Palabras clave, cómo mostrar esto en un currículum
← Llamada a la acción

-...

Declaración de problemas

■ **LeetCode 2158** – * Cantidad de Nueva Zona Dorada cada día*
■ Se le da una lista de pintura donde `paint[i] = [start_i, end_i]`.
■ El día `i` usted pinta el segmento `[start_i, end_i)` de un lienzo 1-dimensional.
■ Pintar el mismo área varias veces es desperdicio; sólo quieres contar el *nuevo* área pintada en cada día.
■ Devuelva un array 'worklog' donde `worklog[i]` es la cantidad de nuevo área pintada el día `i`.

### Input

TENIDO Variable TENRIENTE Tipo TENIDO Constraints
Silencio--------------------------
TENIENDO `Pintura' TENIDO `int[][]` TENIDO `1 ≤ 105`, `0 ≤ start_i Silencio

#### Output

Silencio Variable Silencio Tipo Silencio
Silencio--------------
Silencio `worklog` Silencio `int[]` Silencio Nueva zona pintada cada día

-...

##  Allow Sample Cases

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
Silencio `[1,4],[4,7],[5,8]]` Silencio `[3,3,1]` Silencio Día 0 pinturas 1‐4 → 3 unidades. Día 1 pinta 4‐7 → 3 unidades. Día 2 pinturas 5‐8, pero 5‐7 ya fue pintado → sólo 1 unidad es nueva. Silencio
Silencio `[1,4],[5,8],[4,7]]` Silencio `[3,3,1]` Silencio La misma lógica, el orden importa. Silencio
Silencio `[1,5],[2,4]] ' Silencio `[4,0] ` Silencio Día 0 pinturas 1‐5 → 4 unidades. Día 1's intervalo es completamente dentro del día 0 ́s región pintada → 0 nuevas unidades. Silencio

-...

## Constraints

* `paint.length` puede ser tan grande como `105`.
* `end_i` nunca excede `5·104`, pero no podemos confiar en un pequeño rango de coordenadas porque el algoritmo necesita manejar *cualquier* grandes valores eficientemente.
* Un análisis ingenuo *(n2)* es demasiado lento.

-...

## 🔧 Solution Overview

La visión clave:
**Mantenga un BST equilibrado de intervalos pintados *disjoint*. #
Cuando llegue un nuevo intervalo, nosotros:

1. Encontrar todos los intervalos superpuestos en el BST.
2. **Sutracto** las longitudes superpuestas de la longitud del nuevo intervalo para obtener el área *nuevo*.
3. **Merge** todos los intervalos superpuestos (más el nuevo) en un solo intervalo e insertarlo de nuevo.

A `TreeMap` (`Java`), `std::map` (`C++`), o una `mapa' de inicio → final (`Python`) nos da *(log m)* búsqueda/información donde `m` es el número actual de intervalos pintados.
Puesto que cada intervalo se fusiona a la mayor parte de la vez, la complejidad total es `O(n log n)`.

-...

## 📚 Algorithm Walk-through

`` `
pintado = mapa ordenado vacío (key=start, value=end)
res = array de longitud n

por cada día yo:
l, r = pintura[i]
newLen = r - l

// 1) Combina todos los intervalos que intersectan [l, r)
mientras que hay un intervalo [s, e) en pintado con s ≤ r y e ≥ l:
// superposición: restar la superposición
newLen -= min(r, e) - max(l, s)
// extender el nuevo intervalo para cubrir el sindicato
l = min(l, s)
r = max(r, e)
// eliminar el intervalo antiguo; será reemplazado
borra [s, e) de pintado

// 2) Registro de nuevo área
res[i] = newLen

// 3) Insertar el intervalo de fusión de nuevo
[l] = r
`` `

*El bucle “mientras” siempre termina porque cada iteración elimina un intervalo existente y nunca añade más. *

-...

Código de tres idiomas

A continuación se **completo, listo para pasar** soluciones en **Java**, **Python**, y **C+**.
Los tres usan la misma idea algoritmo pero se adaptan a sus estructuras de datos nativas.

■ **Tip:**
* En Java necesitarás `java.util. TreeMap`.
* En C++ use `std::map observadoint,int contacto`.
* En Python, la biblioteca estándar tiene 'bisecto', pero para la claridad usamos 'sortedcontainers' 'SortedDict`.
■ Si no tienes ese paquete, puedes volver a una lista + bisecto.

-...

## Java

``java
importar java.util*;

Clase Solución {
// O(n log n) time, O(m) space
int[] amountPainted(int[][] paint) {
int n = paint.length;
int[] res = nuevo int[n];
TreeMap Haga clic enInteger, Integer titulada = nuevo TreeMap Quería();

para (int i = 0; i) {}
int l = paint[i][0];
int r = pintura[i][1];
int newLen = r - l;

// Encontrar el primer intervalo con inicio
Integer key = pintado.floorKey(l);
(key!= null) {
int s = clave;
int e = pintado.get(s);

si (e <= l) { // no solap
llave = pintada.lowerKey(key);
continuar;
}

// Existe superposición
newLen -= Math.min(r, e) - Math.max(l, s);
l = Math.min(l, s);
r = Math.max(r, e);

// Retire el intervalo de fusión
pintado.remove(s);
llave = pintada.floorKey(l);
}

// Después de fundir todas las superposiciones
res[i] = newLen;
pintado.put(l, r);
}
restitución;
}
}
`` `

-...

## Python

``python
de la importación de bisect_left, bisect_right

Solución de clase:
# O(n log n) time, O(m) space
def amountPainted(self, paint: list[list[int]) - título [int]:
n = len(paint)
[0]
# Use dos listas paralelas: comienza y termina
comienza, termina = [], []

i, (l, r) in enumerate(paint):
new_len = r - l

# Encontrar el primer intervalo que puede superponerse
idx = bisect_right(starts, l) - 1
mientras que idx >= 0 y termina[idx]
s, e = comienza[idx], termina[idx]
# Overlap
new_len -= min(r, e) - max(l, s)
l = min(l, s)
r = max(r, e)
# Quitar este intervalo
comienza.pop(idx)
fines.pop(idx)
idx -= 1

# Merge cualquier intervalo que comience dentro [l, r)
idx = bisect_left(starts, l)
mientras que idx se hizo len(starts) y comienza[idx]
s, e = comienza[idx], termina[idx]
new_len -= min(r, e) - max(l, s)
l = min(l, s)
r = max(r, e)
comienza.pop(idx)
fines.pop(idx)

res[i] = new_len
# Insertar el intervalo fusionado
idx = bisect_left(starts, l)
start.insert(idx, l)
end.insert(idx, r)

retorno
`` `

-...

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector significado(vector seleccionado) {
int n = paint.size();
vector asignadoint título res(n);
mapa seleccionado,int título pintado; // start - título

para (int i = 0; i) {}
int l = paint[i][0];
int r = pintura[i][1];
int newLen = r - l;

// Encontrar el intervalo con el mayor inicio
auto = pintado.upper_bound(l);
si (lo != pintado.begin()) -it;

mientras que (lo != pintado.end() " aplique it- inicialmente " ) {}
int s = it- tituladafirst, e = it- títulosecond;
newLen -= min(r, e) - max(l, s);
l = min(l, s);
r = max(r, e);
auto aErase = it+;
pintado.erase(toErase);
}

res[i] = newLen;
pintado[l] = r; // Introdúzcase intervalo
}
restitución;
}
};
`` `

■ **Nota:**
■ Si está utilizando Python en una plataforma sin soluciones basadas en `bisect`‐, simplemente puede instalar `sortedcontainers`:

``bash
pip instalacion clasificadocontainers
`` `

Luego, reemplace el enfoque de dos listas con una versión "SortedDict" (start → end) – funciona exactamente como la versión Java "TreeMap".

-...

Tiempo de Complejidad Espacial

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio Java Silencio **O(n log n)** (balanced BST lookup " erase) Silencio **O(m)** – `m` es el número de intervalos *disjoint* pintados (≤ n). Silencio
Silencio Python Silencio **O(n log n)** (bisect + list erase)
TENIDO C++ TENIDO **O(n log n)** (map lookup " erase)

*¿Por qué `m` ≤ n? *
Cada día puede añadir a la mayoría de un intervalo nuevo, y cada fusión elimina al menos un intervalo viejo.
Por lo tanto, en cualquier momento nunca tenemos más de intervalos almacenados.

-...

## ❓ Common Pitfalls

Por qué rompe la vida Fijar
Silencio-----------------------------Prince--
Silencio **Usar una 'lista' y escanear todos los intervalos** Silencio `O(n2)` – demasiado lento. Silencio Usar una estructura *ordenada* (`TreeMap` / `map`). Silencio
Silencio **Sustraer sólo de `r-l` una vez** ANTERIOR Ignores *partial* superpone. ANTE Substraer la solapa exacta para *todo* intervalo de superposición. Silencio
Silencio **No quitar intervalos fusionados** Silencio Terminas con intervalos superpuestos de nuevo. ← Eliminar cada intervalo superpuesto dentro del bucle. Silencio
* Caso Edge* intervalo vacío → area 0. Silencio El algoritmo lo maneja naturalmente (`newLen = 0`). Silencio
Silencio **Python `bisect` off‐by‐one** ← Wrong fusiona límites. Silencio Prueba con `bisect_left`/`bisect_right` cuidadosamente; el código anterior muestra ambos extremos. Silencio

-...

## 🚀 SEO & Career Tips

Silencio Palabras clave Silencio Cómo utilizarlo
Silencio...
Silencio *hard LeetCode problem* Silencio En su currículum: “Solved LeetCode 2158 (Hard) – 100% correcto”. Silencio
Silencio *interval merging* Silencio En un blog o entrevista: “Implemented a disjoint-interval BST for excellent time”. Silencio
Silencio *TreeMap / std::map* ← Demuestra el conocimiento de árboles equilibrados. Silencio
Silencio *O(n log n) algoritmo* Muestra que puedes razonar sobre asintotica. Silencio

*Muéstralo en tu currículum*

``text
- Ejecutó un problema duro de LeetCode (2158 – “Montad de Nueva Zona Pintada Cada Día”) en el tiempo de usuario.
- Usaba un BST equilibrado (TreeMap / std::map) para mantener intervalos pintados descomunales.
- Demostrar fuertes habilidades de solución de problemas y estructura de datos.
`` `

**Post it on Medium / Dev.to**

- Copiar la sección *blog artículo* a continuación.
- Etiqueta con `#LeetCode`, ``Algorithm`, `#Java`, `#Python`, `#C++`.
- Agregue un vídeo corto (o GIF) que pase por los primeros 3 casos de prueba.

-...

Llamado a Acción

1. *Denle el código a LeetCode*
Verifique que la implementación de `O(n log n)` pasa todas las pruebas ocultas.

2. **Agregue la solución a su cartera.**
``text
- Solved LeetCode 2158 – Cantidad de Nueva Zona Pintada Cada Día (Hard)
- Idiomas: Java, Pitón, C++
- Algoritmo: BST equilibrado de intervalos de unión
- Complejidad: O(n log n) tiempo, O(m) espacio
`` `

3. **Publicar un blog. #
Use el artículo abajo (o adapte) e incluya un enlace a su GitHub repo.

4. ** Práctica de entrevista.**
Pregunte a un amigo o mentor para simular una entrevista de pizarra blanca donde explica el algoritmo *sin* mirando el código.

-...

##  gradualmente Blog‐Ready Article (copy‐paste into Medium / Dev.to)

■ **Título**: *LeetCode 2158 – “Monta de Nueva Zona Pintada Cada Día” – O(n log n) Solución en Java, Python & C++ *
■ **Tags**: #LeetCode #Hard #Interview #Algorithms #Java #Python #C++

``markdown
# 2158 – * Cantidad de Nueva Zona Pintada Cada Día*
**LeetCode Hard – O(n log n) Solución en Java, Python & C+**

■ ¿Quieres impresionar a los reclutadores con un problema difícil de LeetCode?
■ Aquí hay una implementación limpia y lista para la producción en tres idiomas, además de una profunda inmersión en el algoritmo.

## Problema Declaración
■ (Recopiar la declaración completa de la sección “Declaración de problemas”)

## Casos de muestra
■ (copiar la tabla de la muestra)

## Algorithm Overview
■ (copiar el párrafo “Solution Overview”)

## Step‐by‐Step Walk‐through
(copiar el diagrama “Algorithm Walk‐through”)

# Código #

## Java
■ (pasar el bloque de código Java)

## Python
■ (pasar el bloque de código Python)

### C++
■ (pasar el bloque C++)

## Complexity Analysis
■ (copiar la sección de complejidad)

## Common Pitfalls
■ (copiar la sección de trampas)

## SEO & Career Boost
■ (copiar la sección de consejos de carrera de SEO)

-...

`` `

Siéntase libre de ajustar el tono, agregue sus propias anécdotas o inserte un corto **video demo**.

-...

Llamado a Acción

1. **Enviar** la solución en LeetCode y ver la placa "Hard" aparece.
2. **Añádelo a tu GitHub** con un README que refleja este artículo.
3. **Tweet** un corto “#LeetCodeHard #Java #Python #C++” post y etiqueta LeetCode.
4. **Preparación para entrevistas** – ahora tienes un ejemplo sólido y listo para la prueba que puedes explicar en menos de 5 minutos.

Buena suerte, y feliz codificación! 🚀