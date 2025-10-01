-...
Título: LeetCode 1233. Eliminar Sub-Folders del sistema de archivos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1233. Remove Sub‐Folders del sistema de archivos
**Java • Python • C+** Silencio **LeetCode**  ** Interview‐Ready**

■ **TL;DR** – Clasifique los caminos alfabéticamente, mantenga la primera carpeta de cada “block” y suelte cualquier carpeta que comience con la carpeta guardada anterior + “/”.
■ Complejidad: **O(n log n)** tiempo, **O(n)** espacio extra.

-...

## Tabla de contenidos

1. [Problema Recap](#problema-recap)
2. [Casos de la intuición " Edge](#intuición- avec-edge-cases)
3. [Solución de escaneo ordenada de gran tamaño](solución de escaneo de gran variedad)
4. [Implementación en tres idiomas](#implementation-in-three-languages)
- [Java](#java)
- [Python](#python)
- [C++](#c++)
5. [Tiempo / Complejidad Espacial](#time--space-complexity)
6. [Aceptos alternativos] (Aprobaciones alternadas)
7. [Common Pitfalls > FAQ](#common-pitfalls--faq)
8. [Por qué esto importa para su entrevista](#why-the-matters-for-your-interview)

-...

## Problema Recap

Se le da una lista de caminos de carpetas absolutos, por ejemplo.

``text
carpeta = ["/a", "/a/b", "/c/d", "/c/d/e", "/c/f"]
`` `

Devuelve la lista después de eliminar *cualquier carpeta* que es un **sub-carpeta** de otra carpeta en la lista.
Un camino 'x' es un sub-carpeta de 'y' si:

1. `x` comienza con `y` *y*
2. el carácter inmediatamente después de `y` es un `'/'.

El orden de la lista resultante no importa.

-...

## Intuition & Edge Cases

* La longitud de la ruta más larga posible es de 100 caracteres – podemos tratar cada cadena como una cadena Java/Python simple o `std::string` en C++.
* Ordenar la matriz lexicográficamente garantiza que una carpeta padre siempre aparece *antes* cualquiera de sus subcarpetas.
* Después de ordenar, sólo necesitamos comparar el camino actual con la carpeta **última** que decidimos mantener.
Si el camino actual comienza con 'último + '/'` es un sub-carpeta y puede ser saltado; de lo contrario lo agregamos al resultado.
* Casos para vigilar:
* Una carpeta que es un prefijo de otro pero **no** un sub-carpeta (por ejemplo, `"/a" vs `"/ab').
* Senderos duplicados – el problema garantiza la singularidad, pero ten cuidado si adaptas el código.
* Entradas muy largas (`4 × 104` caminos) – la solución debe ser O(n log n) para pasar.

-...

## Greedy Sortedy Scan Solution

1. **Sorta** la matriz de caminos de carpeta.
2. **Iterate** a través de la lista ordenada.
3. Para cada carpeta `curr`:
* Si la lista de resultados está vacía → añadir `curr`.
* Else deja `última' ser la última carpeta en la lista de resultados.
* If `curr` starts with `last + '/' → skip `curr` (sub-folder).
* Else add `curr`.

Porque clasificar a todos los niños después de su padre, la comparación con sólo la carpeta *última* guardada es suficiente.

-...

## Implementación en tres idiomas

A continuación se muestran implementaciones limpias, de producción para Java, Python y C++.

## Java

``java
importar java.util*;

Clase Solución {
public List won(String[]) {
// 1 / ⃣ Sort lexicographically
Arrays.sort(folder);

Lista de resultados:String ratio result = nuevo ArrayList correctamente();

// 2Ω⃣ Escanear y guardar sólo carpetas de nivel superior
para (String curr : carpeta) {
si (result.isEmpty()) {
result.add(curr);
continuar;
}

Crianza última = result.get(result.size() - 1);
// comprobar si curr es un sub-carpeta del último
si (curr.startsCon(last + "/") {
continue; // skip sub-folder
}
result.add(curr); // mantener nueva carpeta de nivel superior
}
Resultado de retorno;
}
}
`` `

*Time*: `O(n log n) `
*Pace*: `O(n)` (para la lista de resultados)

## Python

``python
de la importación Lista

Solución de clase:
def quitar Subcarpetas(auto, carpeta: List[str]) - Propiedad Lista[str]:
# 1 Ordenar lexicografía
carpeta.sort()

res = []

# 2⃣ Escaneo saludable
para curar en carpeta:
si no res:
res.append(cur)
continuar

último = res[-1]
# sub-folder if cur starts with last + '/ '
si cur.startswith(last + "/"):
continuar
res.append(cur)

retorno
`` `

### C++

``cpp
Incluido el título
#include ■string
#include >

Clase Solución {
public:
std::vector seleccionado::string quitarSubcarpetas(std::vector seleccionados::string curva) {
// 1 / Clasificar
std::sort(folder.begin(), folder.end());

std::vector seleccionado::string res;

for (const std::string curva : carpeta) {}
si (res.empty()) {}
res.push_back(cur);
continuar;
}

const std::string ultima = res.back();
// comprobar sub-carpeta
si (cur.size()
cur.compare(0, last.size(), last) == 0 "
cur[last.size()] == '/') {
continuar; // skip
}
res.push_back(cur); // keep
}
restitución;
}
};
`` `

-...

## Time / Space Complexity

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio Ordenación Silencioso **O(n log n)** Silencio **O(1)** (en lugar)
Silencio Escanerando Silencio **O(n)** Silencio **O(n)** para la lista de salida

Total: **O(n log n)** tiempo, **O(n)** espacio auxiliar.

-...

## Alternate Approaches

Silencio Silencio Silencio Pros
Silencio...
Silencio **Trie** (árbol prefijo) Silencio Maneja alfabetos muy grandes & insertaciones dinámicas Silencio Código extra, factor constante superior tención
Silencio **Hash Set + Parent Check** Silencio Puede detenerse temprano si el padre ya es eliminado Silencio Necesita revisar todos los prefijos → O(n2) peor-case
tención **Sorting + Stack** tención Lo mismo que antes, pero utiliza una pila en lugar de una lista Silencioso esencialmente idéntica complejidad

El escaneo clasificado es el más limpio para los ajustes de entrevista.

-...

## Common Pitfalls > FAQ

Respuesta a la respuesta
Silencio...
Silencio *¿El conflicto con `'/ab'?* Silencio `"/a" es **no** una subcarpeta de `"/ab" porque el carácter después de `"/a" no es `'/'. El código usa correctamente `startsWith(last + "/")`. Silencio
*¿Qué pasa si la lista contiene sólo una carpeta?* El algoritmo todavía funciona: el resultado contendrá esa carpeta única. Silencio
*¿Es importante el orden de la lista devuelta?* No – LeetCode acepta cualquier orden. El algoritmo conserva el orden ordenado, que está bien. Silencio
*¿Podemos usar un `HashSet` para dedupe?* El problema garantiza la singularidad, por lo que un conjunto no es necesario. Silencio
¿Qué hay de los límites de memoria? espacio extra es aceptable para `n ≤ 4×104`. Silencio

-...

## Why This Matters for Your Interview

1. **Simplicidad** – Un escaneo clasificado de dos pasos es fácil de explicar e implementar, reduciendo la posibilidad de errores.
2. **Big‐O Awareness** – Demostrar que usted consideró tiempo / cambio de espacio muestra la madurez.
3. **Edge‐Case Thinking** – Handling `"/a" vs `"/ab" demuestra una cuidadosa manipulación de cuerdas.
4. ** Flexibilidad en idioma** – Conocer el mismo algoritmo en Java, Python y C++ demuestra que usted está cómodo entre las pilas, un plus para muchos administradores de contratación.

■ *Recordar*: Los entrevistadores a menudo valoran **claridad** sobre ingenio. Una solución de exploración ordenada que se ejecuta en `O(n log n)` y es sencilla de leer es a menudo la mejor opción.

-...

## SEO‐Optimized Summary

- **Keywords**: *leetcode 1233*, *remove sub folders*, *sorted scan algoritmo*, *Java/Python/C+*, *coding interview*, *software engineering interview tips*, *algorithm interview question*, *job interview coding*.
- **Descripción de los datos**: “Aprenda a resolver LeetCode 1233 – Eliminar Sub-Folders del sistema de archivos – con código Java, Python y C++. Entender el algoritmo de escaneo ordenados, la complejidad del tiempo, los casos de borde, y por qué es una opción principal para entrevistas de ingeniería de software. ”

-...

Feliz codificación, y buena suerte clavando esa próxima entrevista!