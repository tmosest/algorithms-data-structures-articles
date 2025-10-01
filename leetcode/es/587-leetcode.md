-...
Título: LeetCode 587. Erect the Fence -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 587. Erect the Fence – Three‐ Way Solution " a SEO‐Optimized Blog Post

■ **TL;DR**
■ *Implement a convex‐hull (Monotonic‐Chain) que mantiene puntos collineales en el límite. *
■ *Proporcionamos Java, Python, y C++ código, y un artículo de blog completo que explica el “bueno, el malo y el feo” de este problema, empaquetado con ganchos SEO amigables para entrevistas. *

-...

## 1. Recapitulación de problemas (LeetCode 587)

■ ** Objetivo** – Dado un conjunto de coordenadas de árboles, regrese * todo* árbol que se encuentra en el perímetro de la cerca de longitud mínima que encierra todos los árboles.
■ **Regla especial** – Si la valla es una línea recta (todos los árboles collinear) devuelve todos los árboles.

Constraints:
- 1 ≤ `trees.length` ≤ 3000
- 0 ≤ `xi, yi` ≤ 100
Todas las coordenadas son únicas.

-...

## 2. Idea de alto nivel

La valla que cubre todos los puntos con el perímetro más pequeño es el casco **convexo** del conjunto de puntos.
El único matiz es que *los puntos fríos que se encuentran en los bordes del casco también deben ser devueltos*.
Esta es una variación clásica del problema convex‐hull.

Utilizaremos el algoritmo **Monotonic Chain (Andrew’s)** – O(N log N) time, O(N) space – porque es corto, rápido y fácil de escribir en los tres idiomas.

-...

## 3. Detalles del algoritmo

1. **Sorta** todos los puntos lexicográficamente por x, luego por y.
2. # Construir el casco inferior #
* Camina por puntos ordenados.
* Mientras que los dos últimos puntos del casco junto con el punto actual hacen un giro **derecha** (`cross <= 0` para *keeping* puntos collinear) - pop el último punto.
* Empuja el punto actual.
3. **Construir el casco superior** de la misma manera, pero caminar a través de los puntos ordenados en reversa.
4. **Combina** cascos inferiores y superiores (correr el último punto de cada uno para evitar duplicaciones).
5. **Remove duplicados** (especialmente cuando todos los puntos son collinear – ambos cascos contendrán el mismo conjunto) – use un `HashSet` (Java), `set` de tuples (Python), o `unordered_set` con un hash personalizado (C++).

**Cross Product**
For points `A(x1,y1)`, `B(x2,y2)`, `C(x3,y3)`:
`` `
(x2-x1)*(y3-y1) – (y2-y1)*(x3-x1)
`` `
* `` 0` → giro a la izquierda
* 0` → giro derecho
* `== 0` → collinear

-...

## 4. Código

### 4.1 Java (Java 17+)

``java
importar java.util*;

Solución de la clase pública {}

// Producto cruzado de AB y AC
cruz larga privada (int[) A, int[] B, int[] C) {
(long)(B[0] - A[0]) * (C[1] - A[1]) -
(long)(B[1] - A[1]) * (C[0] - A[0]);
}

int[][][] exteriorTrees(int[][] trees) {
si (árboles == nulo ¦ 0) devolver nuevo int[0][0];
Arrays.sort(trees, (p, q) - {}
si (p[0] != q[0]) devuelve Integer.compare(p[0], q[0]);
integer.compare(p[1], q[1]);
});

Lista obtenida[] inferior = nuevo ArrayList implicado();
para (int[] pt : árboles) {}
mientras (baja.size() 2 "
cross(lower.get(lower.size() - 2),
inferior.get(lower.size() - 1), pt)
inferior.remove(lower.size() - 1);
}
inferior.add(pt);
}

Lista obtenida[]] título superior = nuevo ArrayList correctamente();
para (int i = árboles.length - 1; i >= 0; --i) {
int[] pt = trees[i];
mientras (upper.size() 2 "
cross(upper.get(upper.size() - 2),
superior.get(upper.size() - 1), pt)
superior.remove(upper.size() - 1);
}
superior.add(pt);
}

// Combinar inferior y superior, evitar puntos finales duplicados
Conjunto de instrucciones:
(int[] p : lower) set.add(Arrays.asList(p[0], p[1]));
para (int[] p : superior) set.add(Arrays.asList(p[0], p[1]));

int[][] res = nuevo int[set.size()][2];
int i = 0;
para (Lista realizadaInteger título : set) {
[i] [0] = lst.get(0);
res[i][1] = lst.get(1);
i++;
}
restitución;
}
}
`` `

■ **¿Por qué usar 'Listecto'Integer `` en el set? #
■ Los arrays primitivos no pueden ser cortados correctamente en Java; envolvernos en un `List` nos da un `equals`/`hashCode` estable.

-...

### 4.2 Python 3

``python
de la importación Lista

Solución de clase:
def en el exterior Árboles (yo, árboles: Lista [Lista [int]]) - No. List[List[int]]:
si no los árboles:
retorno []

árboles.sort() # lexicographic: x then y

def cross(o, a, b):
(a[0]-o[0]) * (b[1]-o[1]) – (a[1]-o[1]) * (b[0]-o[0])

inferior = []
para p en los árboles:
len(lower) √≥= 2 y cruz(lower[-2], inferior[-1], p)
inferior.pop()
inferior.append(p)

superior = []
for p in reversed(trees):
mientras len(upper) √≥= 2 y cruz(upper[-2], superior[-1], p)
superior.pop()
superior.append(p)

# Combine and dedupe
hull = set(tuple(pt) for pt in lower[:-1] + upper[:-1])
[lista(pt) para pt en hull]
`` `

■ **Nota** – Dejamos caer el último punto de cada media hora para evitar la duplicación de los puntos finales ( " más bajo [-1] == superior[-1] " ).

-...

### 4.3 C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
larga cruz (cont array observado,2 A,
const array madeint,2 B,
const array madeint,2⁄4
1LL*(B[0]-A[0])*(C[1]-A[1]) -
1LL* (B[1]-A[1])*(C[0]-A[0]);
}

vector realizador identificadoint títulos externosTrees(vector identificadovector fielint implica árboles) {}
(trees.empty()) return {};

especie(trees.begin(), árboles.end(),
[](cont vector identificadoint ánimo p, const vector implicado
si (p[0] != q[0]) devuelve p[0]
retorno p[1] q[1]
});

vector realizador realizado, 2 título inferior, superior;
para (autor : árboles) {}
array madeint,2 caracteres pt{p[0], p[1];
mientras (baja.size() 2 "
cross(lower[lower.size()-2], lower.back(), pt)
inferior.pop_back();
inferior.push_back(pt);
}

para (auto it = árboles.rbegin(); it != árboles.rend(); ++it) {
(*it)[1];
mientras (upper.size() 2 "
cross(upper[upper.size()-2], upper.back(), pt)
superior.pop_back();
superior.push_back(pt);
}

// Eliminar el último elemento de cada uno para evitar duplicados
inferior.pop_back();
superior.pop_back();

unordered_set obtenidos largo visto;
vector de vectores res;

auto añadir = [ cl](cont array observadoint,2⁄4 pt){
llave de largo largo = 1LL*pt[0]*101 + pt[1]; // 0 se realizó=x,y se realizó=100 - único
si (ver.insert(key).second) {
res.push_back({pt[0], pt[1]});
}
};

para (autor: inferior) add(pt);
para (auto &pt : superior) add(pt);

restitución;
}
};
`` `

■ **Key trick** – Compresa cada punto en una sola llave de largo (`x*101 + y`) porque `x` y `y` son ≤ 100. Esto nos permite utilizar `noordered_set obtenidoslong tiempo `` para la deduplicación O(1).

-...

## 5. Blog Post – “El Bien, el Mal y el Ugly” de LeetCode 587

### Title
■ **Erect the Fence (LeetCode 587) – The Complete Guide (Java / Python / C++)**
■ *Por qué el casco convex es un conocimiento imprescindible para entrevistas de estructura de datos, además de un tutorial paso a paso. *

*(Agregue una imagen atractiva ofrecida de un casco convex en 2-D, el logotipo de LeetCode, y los fragmentos de código resaltados.) *

-...

### 1. Introducción

■ “Estoy entrevistando para una posición de ingeniero de software, pero no puedo superar las preguntas de geometría. ”
■ Esta frase es tan común como un lápiz roto en un panel de contratación.
■ El problema Erect the Fence es un *golden ticket* – prueba dos conceptos simultáneamente:
* Nota: * Nota** (para linearizar los datos)
* Invariantes geométricos** (producción cruzada, orientación).

Le mostraremos la solución ** más rápida, limpia y más fácil de entrevista** en tres idiomas.

-...

### 2. ¿Por qué Convex Hull? (El Bien)

- ** Concepto universitario** – Aparece en gráficos de ordenador, robótica, GIS, incluso juego AI.
- **Linear‐time or near-linear** – El algoritmo de Andrew funciona en O(N log N), golpeando el cheque perímetro de fuerza bruta O(N2).
- **Cobertura de test de Rich** – Maneja todos los casos de esquina (todos los puntos collinear, punto único, arreglos de convex vs. concave).

■ **Interview hook** – “Describa una situación en la que tuvo que optimizar el camino de un vacío robot que tenía que cubrir todas las habitaciones de una casa. ”
■ El reclutador espera que usted mencione “convex hull” casi inmediatamente.

-...

### 3. Caminata de implementación (El Bien)

1. **Ordenar los puntos** – El primer paso O(N log N)
2. **Use una pila (o vector)** para mantener el casco mientras se iteran.
3. **Prueba de producto de escoria** – Una sola línea de código determina si un punto debe permanecer o ser eliminado.
4. **Keep collinear points** – Sólo cambia `cruzâ 0` a `cruz == 0`.
5. **Deduplicado** – En Java, utilice un `Set observadoLista realizadoInteger confianza ``; en Python, `set(tuple(pt)) '; en C++, una clave de entero hashed.

*¿Por qué este algoritmo golpea el clásico Graham Scan? *
- Menos código, menos fallos, más fácil de explicar verbalmente.

-...

### 4. Pitfalls comunes (The Bad)

Silencio Pitfall Silencio ¿Por qué es malo
Silencio--------------------------
TENIDO Utilizando ` 0` para la condición pop ANTE Elimina los puntos collinear en los bordes del casco. TENIDO UTILIZACIÓN `Seguido= 0` sólo si usted *necesita* para mantenerlos, de lo contrario ` 0`. Silencio
Silencio Olvídate de dedupe cuando todos los puntos son collinear Silencio Devuelve árboles duplicados o falta algunos. Silencio Usar un `Set` o `unordered_set` después de fundir los cascos superiores inferiores. Silencio
Silencio Usando el desbordamiento entero en el producto cruzado ← Coordinas ≤ 100, pero en problemas genéricos podrían ser 109. TENIDO A "longitud larga" / "long" antes de la multiplicación. Silencio
tención Mezclando la lógica izquierda/derecha vuelta Silencio Flips la orientación del casco, que conduce a una forma incorrecta. TENIDO ATENCIÓN A LA CONVENCIÓN: " Cruzando " 0 " = izquierda, " 0 " = derecha. Silencio

**Tip** – Escribe un pequeño ayudante del cruce con comentarios claros; un solo tipo romperá toda la solución.

-...

### 5. El “Ugly” – Cuando los entrevistadores te empujan más

1. **Todos los puntos Collinear** – Su algoritmo debe manejar este caso de borde con gracia.
*Solución:* Después de construir ambos cascos, conviértete a un conjunto; no hay necesidad de lógica separada.

2. **Large Input Range** – Algunos entrevistadores preguntan “¿Y si ‘xi, yi’ podría ser hasta 109? ”
*Solución:* Use `long’ para el producto cruzado, evite el flujo entero y cambie la clave de deduplicación a un par de hash.

3. **Constraints de memoria** – Cuando la memoria es limitada, puede construir el casco en su lugar y reutilizar el array de entrada.
*Python/C++:* Apéndices de casco a una nueva lista, luego vuelve a mapa.
*Java:* Usar un resultado " un [][] " y llenarlo mientras se iteraba.

4. ** Límites de tiempo** – El algoritmo O(N log N) pasa fácilmente con N = 3000.
Si necesita optimizar más, puede pre-ordenar por valores enteros y utilizar el tipo de conteo (O(N)) porque las coordenadas son pequeñas.

-...

### 6. Cómo explicar En un Whiteboard

1. **Draw** la lista ordenada de puntos horizontalmente.
2. **Mostrar** el casco inferior que se construye – cada pop representa un “corner” que se suaviza.
3. Espejo** para el casco superior.
4. **Combina** – Visualizar el “upper” como una versión volteada de la parte inferior.
5. **Point out** por qué los puntos collinear en los bordes permanecen – enfatizar la condición de cross-product.

*Practice*: Trate de explicar esto en 3 minutos – encontrará que puede hacerlo naturalmente después de haber escrito el código algunas veces.

-...

### 7. Hoja de Cheat despejada

Silencio Idioma Silencio Ordenar por Silencio Cross Producto ◾ Hull Building
Silencio----------------------------------------------------------------...
TEN Java TENIDO `Arrays.sort(trees, cmp)` Silencio `ArrayList madeint[] confía` Silencio `HashSet madeList madeInteger confianza `` Silencio
TENIENDO Python TENIDO `trees.sort()` Silencio `def cross(o,a,b)` Silencio
Silencio C++ Silencioso `sort(begin,end,cmp)` Silencio `vector observadoarray madeint,2 título` Silencio `unordered_set obtenidoslong `` (key = x*101+y) Silencio

■ **Key:** Utilice la fórmula de producción cruzada * igual* a través de idiomas. Mantenga la condición `cruz . 0` para el giro derecho y mantenga puntos collinear.

-...

### 8. Palabras finales

■ Cuestiones de geometría Erect the Fence son *no* sobre ser un matemático; se trata de probar que puede manejar ** conjuntos de datos en dos dimensiones**, aplicar un algoritmo robusto, y escribir código limpio y libre de errores.
■ Maestro el casco convexo una vez y ganarás no sólo este problema, sino una * clase completa* de preguntas de entrevista.

*Agregar un “¿Quieres más? Echa un vistazo a mi repositorio completo de soluciones de entrevistas de instrucciones de datos” enlace y un formulario de correo electrónico o de contacto. *

-...

### 9. SEO Meta‐Data (para Recruiter Robots)

TEN TERRITORIO TERRITORIO TERRITORIO TERRITORIO
Silencio...
“LeetCode 587”, “Erect the Fence solution”, “convex hull interview”, “Java convex hull”, “Python geometry problem”, “C+++ convex hull”, “Data structure interview questions”, “algorithm interview preparation”
tención Descripción Silenciosa “Descubre la solución Java/Python/C++ más rápida para LeetCode 587 – Erect the Fence. Aprenda los fundamentos del casco convexo y consiga un avance completo con código.” Silencio
Tag Silencio “Erecte la Fence LeetCode 587 – Completa Java/Python/C++ Guide”
TEN OG Image TEN `https://example.com/assets/convex-hull.png` Silencio
Silencio Twitter Card Silencioso `summary_large_image` Silencio

-...

## 6. Cómo utilizar este blog en su cartera

- **Pin it on LinkedIn** con el titular “Solved Erect the Fence en 4 idiomas – Convex Hull 101”.
- Subió el código de tu GitHub README.
- **Crear un video corto** (3 minutos) de usted que resuelve el problema en vivo, luego subir a YouTube con el mismo título – El algoritmo de YouTube ama “cómo resolver” videos.
- **Añada una prueba** al final del artículo (“Given points X, Y, Z, que está en el casco?”) – fomenta el compromiso.

-...

## 7. Pensamiento de clausura

■ La geometría puede sentirse intimidante, pero los patrones subyacentes son simples.
■ Al dominar el algoritmo de la cadena monotónica una vez, usted puede resolver con confianza Ejecutar la Fence, sus variaciones, y una multitud de otros rompecabezas de geometría entrevista.

Feliz codificación, y que sus cercas siempre sean *tight* y *eficiente*! 🚀

-...

**End of Post**