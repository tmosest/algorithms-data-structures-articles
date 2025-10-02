-...
Título: LeetCode 1447. Fracciones simplificadas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
1. LeetCode 1447 – Fracciones simplificadas
** Solución agnóstica de programación** (Java / Python / C++)
** Complejidad del tiempo**: \(O(n^2)\)
** Complejidad del espacio** : \(O(n^2)\) (tamaño de salida del peor de cada caso)

-...

## 1.1 The Idea

Por cada denominador `d` de **2** a `n `
" Nbsp; , por cada numerador `num' de **1** a `d-1 '

* If* `gcd(num, d) == 1 `la fracción `num/d` es **irreducible** (simplificada).
Guárdalo como una cadena `"num/d"`.

La prueba " gcd " garantiza que nunca añadamos una fracción reducible como " 2/4 " .
No se requieren estructuras de datos adicionales (hash-maps, sets) más allá de la lista de salida.

-...

## 1.2 Code

Silencio Idioma Silencio Código Silencio
Silencio...
Silencio**
importa java.util. ArrayList;
importa java.util. Lista;

Solución de la clase pública {}
public List Garantizado(int n) {
Lista de resultados:String ratio result = nuevo ArrayList correctamente();
para (int denom = 2; denom = n; denom++) {}
for (int num = 1; num י denom; num++) {}
si (gcd(num, denom) == 1) {
result.add(num + "/" + denom);
}
}
}
Resultado de retorno;
}

// algoritmo euclidiano – O(log min(a,b))
int gcd privado (int a, int b) {}
mientras (b!= 0) {
int tmp = un % b;
a = b);
b = tmp;
}
devolver a;
}
}
`` Silencio
Silencio **Python**
de la importación Lista

Solución de clase:
def simplified Fracciones (self, n: int) - Lista de títulos [str]:
def gcd(a: int, b: int) - título int:
mientras b:
a, b = b, porcentaje b
retorno a

res = []
para denom en rango(2, n + 1):
para num en rango(1, denom):
si gcd(num, denom) == 1:
re.append(f"{num}/{denom}")
retorno
`` Silencio
Silencioso **C+**
Incluido el título
#include ■string
#include ■numeric confianza // std:gcd en C+17

Clase Solución {
public:
std::vector seleccionado::string confianza simplifiedFractions(int n) {
std::vector seleccionado::string res;
para (int denom = 2; denom <= n; ++denom) {}
para (int num = 1; num < denom; ++num) {
si (std::gcd(num, denom) == 1) {
res.push_back(std::to_string(num) + "/" + std::to_string(denom));
}
}
}
restitución;
}
};
`` Silencio

-...

## 1.3 Why This Works

✔ Cambios en la Explicación
Silencio...
TENIDO TENIDO Silencio **Correcto** – El algoritmo de Euclidean identifica correctamente pares de coprime. Silencio
TENIDO ANTERIOR **Completeness** – Cada fracción reducida con denominador ≤ n se genera. Silencio
TENIDO TENIENDO TENIDO **Performance** – `O(n^2)` es óptimo porque hay cerca de \(\frac{n(n-1)}{2}\) fracciones posibles. Silencio
TENIDO TENIDO ANTERIOR **Simplicity** – Sin puntos flotantes aritmética, sin mapas de hash. Silencio

-...

# 2. Artículo del Blog
**Título:** Fracciones simplificadas (LeetCode 1447) – El Bien, el Mal y el Ugly*

## 2.1 Introducción (SEO Meta-Descripción)

■ Master LeetCode 1447 “Fraciones simplificadas” en Java, Python y C++. Aprenda la solución GCD óptima, las trampas de trucos de punto flotante, y cómo impresionar a los gerentes de contratación con código limpio y listo para entrevistas. Ideal para los candidatos de algoritmos de estructuración de datos.

**Keywords:** LeetCode 1447, fracciones simplificadas, pregunta de entrevista, algoritmo GCD, solución Java, solución Python, solución C++, codificación de entrevistas de trabajo, pensamiento algoritmo.

-...

## 2.2 El problema en un glance

■ Dado un entero **n** (1 ≤ n ≤ 100), volver *todo* fracciones irreducibles entre 0 y 1 (exclusiva) cuyo denominador no excede **n**. El orden es irrelevante.

Ejemplo
'n = 4 → ["1/2","1/3","1/4","2/3","3/4"] `
(Notice **2/4** se omite porque simplifica **1/2**.)

-...

## 2.3 La “buena” – Una solución limpia y basada en GCD

Por qué es buena vida
Silencio----------
Silencio **Correcto** Silencio Utiliza el algoritmo de Euclidea para probar `gcd(num, denom) == 1`. No hay posibilidad de falsos positivos. Silencio
TEN **Simplicidad** ANTE Únicamente dos lazos anidados; no hay contenedores adicionales o conversiones de punto flotante. Silencio
tención **Performance** Silencioso `O(n2)` tiempo, que es óptimo dado el tamaño de la salida; `O(1)` espacio auxiliar además de la lista de resultados. Silencio
Silencio **Readability** Silencio Nombres variables claros (`num`, `denom`) y un pequeño ayudante `gcd`. Silencio
Silencio **Portabilidad** Silencio Funciona de forma idéntica en Java, Python, C++ – perfecto para la preparación de entrevistas a través de idiomas. Silencio

## Code Snippet (Java)

``java
para (int denom = 2; denom = n; denom++) {}
for (int num = 1; num י denom; num++) {}
si (gcd(num, denom) == 1) {
result.add(num + "/" + denom);
}
}
}
`` `

-...

## 2.4 El “Bad” – Mapas de Hash Floating‐Point

Algunas soluciones utilizan un mapa de valores 'float' para detectar duplicados:

``cpp
flotante val = estática_cast 0,242(j) / i;
si (!mp.count(val)) { /* añadir fracciones */ }
`` `

## Problemas

TEN TERRITORIO TERRITORIO TERRITORIO
Silencio...
Silencio **Pérdida de precisión** Silencio `0.3333333333` y `0.33333334` pueden ser tratados como iguales o distintos incorrectamente. Silencio
Silencio **Espacio extra** Silencioso El mapa añade \(O(n2)\) arriba; innecesario. Silencio
Silencio **La complejidad** Silencio Mismo `O(n2)` lazos, pero las operaciones del mapa agregan la sobrecarga de bitácora. Silencio

En la práctica, este enfoque funciona para 'n ≤ 100' pero falla en entradas más grandes o ajustes de entrevista estrictos donde la exactitud importa.

-...

## 2.5 El “Ugly” – Brute‐Force sin GCD

Un acercamiento ingenuo sobre todos los pares numerador/denominador y *re-reduce* cada fracción:

``python
para d en rango(2, n+1):
para num en rango(1, d):
simplified = reduce_fraction(num, d) # caro
si no se simplifica en la vista:
visto.add(simplificado)
`` `

### Why It's Ugly

Silencioso
Silencio...
Silencio **Trabajo repetido** Silencio Cada fracción se reduce incluso si ya se sabe. Silencio
Silencio **Complejidad más alta** La reducción de las vidas puede ser `O(log min(a,b))) ' ; repetido por cada par conduce a una desaceleración notable. Silencio
Silencio **Less Readable** Silencio Funciones de ayudantes adicionales, estructuras de datos adicionales, más difícil de auditar durante una entrevista. Silencio

-...

## 2.6 Quick Checklist for Interviewers

✔ Cambios en la lista de verificación
Silencio...
TENIDO TENIENDO TENIDO Utilizar Euclidean GCD (construido o personalizado). Silencio
TENIDO ANTERIOR Dos lazos anidados; denominadores de 2 a `n`. Silencio
TENIDO TENIDO Silencio No hay matemáticas de punto flotante. Silencio
TENIDO TENIENDO TENIDO Vuelta `Lista seleccionadaString `` (Java), `vector asignadostring confianza` (C++), `List[str]` (Python). Silencio
TENIDO TENIDO TENIDO Mantenga el código compacto (≤ 20 líneas). Silencio
TENIDO TENIDO ANTERIOR Añadir comentarios para la claridad. Silencio

-...

## 2.7 Pensamientos finales

- La solución GCD es el estándar **oro** para LeetCode 1447.
- Evite trucos de punto flotante a menos que se permita explícitamente.
- Mantenga su código * legible*, *correcto* y *eficiente*, los entrevistadores se preocupan por *cómo* usted resuelve, no sólo *lo que* usted resuelve.

Buena suerte aterrizando esa entrevista de codificación! 🚀

-...

**Referencias**
- Problema LeetCode 1447: " : " https://leetcode.com/problems/simplified-fractions/ "
- Euclidean Algorithm Wikipedia: " https://en.wikipedia.org/wiki/Euclidean_algorithm titulado "

No dude en adaptar los snippets para su propia preparación de entrevistas o contribuciones de código abierto.