-...
Título: LeetCode 247. Strobogrammatic Number II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 247. Strobogrammatic Number II
**Java / Python / C++ – Soluciones completas + entrevista- Lista de Blog**

■ *LeetCode 247 – Strobogrammatic Number II*
■ *Dificultad: Medium*
■ *Time‐Limit: 1 s (Ω 5 × 105 llamadas recursivas max)*
■ *Pace‐Limit: 256 MB*

-...

## Tabla de contenidos
1. [Declaración sobre el proyecto] (declaración sobre el problema)
2. [¿Qué es un número estrobogramamático?](#qué es-un-estrobograma-número)
3. [Estrategia de Alto Nivel] (Estrategia de alto nivel)
4. [Bien - El enfoque de recuperación simple](#bueno)
5. [Bad – Edge Cases " Leading Zeros](#bad)
6. [Ugly - Handling Extremely Large `n`](#ugly)
7. [Java Implementation](#java-implementation)
8. [Python Implementation](#python-implementation)
9. [C+++](#c+++-implementation)
10. [Análisis de complejidad](#complexidad-análisis)
11. [Aproximaciones alternativas] (Aprobaciones alternativas)
12. [Entrevista Consejos " Errores comunes "](#interview-tips)
13. [SEO-Optimized Summary](#seo-summary)
14. [Conclusión](#conclusión)

-...

## 1. Declaración de Problema: Nombre= "problema-estado"

■ **Given an integer `n`, return *all* strobogrammatic numbers of length `n`.**
■ Un número estrobogramamático es un número que aparece igual después de girarlo 180° (al revés).

*Examples*

Silencio
Silencio...
TENIDO 2 TENIDO "[11", "69", "88", "96"] Silencio
Silencio 1 Silencioso `["0","1","8"] Silencio

**Constraints* *

* `1 ≤ n ≤ 14`

-...

## 2. ¿Qué es un número estrobogramamático?

Silencio Digit Silencio Rotated (180°)
Silencio...
Silencio 0 Silencio 0 Silencio
Silencio 1 Silencio 1 Silencio
Silencio 6 Silencio 9
Silencio 8 Silencio 8
Silencio 9 Silencio

Un número es estrobogrammático si el *i*‐th digit de la izquierda equivale al *i*‐th digit de la derecha después de aplicar la asignación anterior.

-...

## 3. Estrategia de alto nivel

* **Recursive Backtracking** – Construya el número desde el exterior.
* **Casos de base** –
* `n == 0` → cuerda vacía (utilizada para construir números de longitud).
* `n == 1` → ``0,'1','8'. (el dígito medio de números de longitud extraña).
* **Recursive Step** – Por cada cadena `inner` de `ayuda(n-2, m)` prepend/append cada par válido.
* **Evitar Cero de Liderazgo** – Saltar `"0" + interior + "0" cuando `n == m` (capa exterior).

Esto produce todas las combinaciones en el tiempo y el espacio `O(5^(n/2)).

-...

## 4. Bien - El enfoque de recuperación simple - seleccionó un nombre= "bueno"

* **Readability** – Una función, un bucle claro.
* **Natural Fit** – El problema es literalmente “compilado de los bordes en. ”
* **Extensibilidad** – Fácil añadir nuevos pares de dígitos si la definición cambia.
* **No hay estructuras de datos adicionales** – Usa sólo listas/vectores de cadenas.

-...

## 5. Malos – Casos de bordes " Cero principales " se hizo un nombre= "bad "

* Olvidando excluir `'0...0'` en el nivel más exterior genera números como ''00', `'000', que son **inválidos** porque tienen ceros líderes.
* Una implementación ingenua que siempre añade el par cero producirá `4` cadenas adicionales para cada capa externa, inflando el conjunto de resultados.
* Cuando `n` es extraño, la capa media sólo debe contener `'0'`, `'1'`, `'8'`. Añadiendo `'0'` en los lados crearía números de longitud `n+2` - un clásico off-by-one bug.

-...

## 6. Ugly – Handling Extremely Large `n` se hizo un nombre= "ugly"

* **Desbordamiento de la tensión** – La profundidad de la recuperación crece con `n`. Para `n = 14` la profundidad es sólo `7`, por lo que es seguro, pero para la generalización (por ejemplo, `n = 104`) usted había alcanzado los límites de la pila.
* ** Pieza de memoria** – El número de resultados es " 5^(n/2) " ; para " n = 14 " es " 5^7 = 78 125 " .
* Cada cadena es longitud 14 → ~1 KB por resultado → ~78 MB total.
* Si el entrevistador pide *cuenta* solamente, puede evitar materializar todas las cadenas.

-...

## 7. Aplicación de Java se realizó un nombre="java-implementation"

``java
importar java.util*;

Solución de la clase pública {}
public List meantString confianza findStrobogrammatic(int n) {
helper(n, n);
}

privada Lista hecha pública(int n, int m) {
// Casos de base
(n == 0) devolver nuevo ArrayList recomendado(Collections.singletonList("");
si (n == 1) devolver nuevo ArrayList correctamente(Arrays.asList("0", "1", "8"));

Lista seleccionadaString titulada res = nuevo ArrayList correctamente();
// Recurse para la parte interna
Lista realizadaString confianza interior = helper(n - 2, m);

para (String s : interior) {
si (n != m) res.add("0" + s + "0"); // skip leading cero at outermost level
res.add("1" + s + "1");
res.add("6" + s + "9");
res.add("8" + s + "8");
res.add("9" + s + "6");
}
restitución;
}
}
`` `

■ *Por qué está limpio* – El ayudante recibe el *original* `m` para saber cuándo evitar `"0" par.
■ **Hora** – O(5^(n/2)
■ **Espacio** – O(5^(n/2)

-...

## 8. Aplicación de Python se hizo un nombre="pion-implementation"

``python
de la importación Lista

Solución de clase:
def findStrobogrammatic(self, n: int) - titulada List[str]:
volver a sí mismo.

def _helper(self, n: int, m: int) - Propiedad Lista[str]:
si n == 0:
["""]
si n == 1:
["0", "1", "8"]

res = []
para interior en sí mismo._helper(n - 2, m):
si n != m: # Evitar los ceros principales
res.append("0" + interior + "0")
res.append("1" + interior + "1")
res.append("6" + interior + "9")
res.append("8" + interior + "8")
res.append("9" + "6")
retorno
`` `

■ ** Nota pitónica** – Usar la recursión mantiene el código corto; si prefieres un BFS iterativo, simplemente reemplaza al ayudante con un bucle de cola.

-...

## 9. C+++ Implementación realizada un nombre="c+++-implementation"

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector de la búsqueda de confianzaStrobogrammatic(int n) {
helper(n, n);
}
privado:
vector iniciado(int n, int m) {
si (n == 0) regresa {"};
si (n == 1) retorno {"0", "1", "8"};

vectoriales res;
vector realizador interno = helper(n - 2, m);

para (la cuerda contigua : interior) {
si (n != m) res.push_back("0" + s + "0"); // evitar ceros líderes
res.push_back("1" + s + "1");
res.push_back("6" + s + "9");
res.push_back("8" + s + "8");
res.push_back("9" + s + "6");
}
restitución;
}
};
`` `

■ ¿Por qué C++? La misma lógica de recursión; la única diferencia es la gestión manual de memoria a través de `std::vector`.

-...

## 10. Análisis de Complejidad > > > > >

Silencio Silencio Silencio Silencio
Silencio----------------
Silencioso de la profundidad de los árboles de la recuperación (Apilación de llamadas)
Silencio Número de cadenas generadas Silencio `5^(n/2)` Silencio `5^(n/2)` (lista de salida)
Silencio Total Silencioso `O(5^(n/2)' Silencio

*Reason*: En cada nivel generamos 5 veces más cadenas que el nivel interior anterior (excepto el nivel más externo donde saltamos el par “00”, dando 4 * 5^(k-1) para incluso `n’).

-...

## 11. Enfoques alternativos > > > >

Silencioso tóxico Pros
Silencio----------
TEN **Iterative BFS (queue)** TEN No recursion, easier to understand for startners TEN Slightly more calderaplate, same asinptotic complexity TEN
Silencio **DP / Memoization** Silencio Reuse sub-problemas para mayor `n` sufrimiento Memoria extra para memo memorias, overkill for `n ≤ 14` Silencio
Silencio **Apoyo sólo** Silencio O(1) espacio si sólo se necesita el número de soluciones.

■ ¿Cuándo elegir BFS? Si tu panel de entrevistas prefiere soluciones iterativas o si temes apilar desbordamiento para mayor `n`.

-...

## 12. Consejos de entrevista > Errores comunes > Nombre= "interview-tips"

1. **Clarificar la definición** – Confirmar que los dígitos "6" y "9" están permitidos y "0" puede aparecer en el medio sólo por longitudes extrañas.
2. **Pregunte sobre los ceros principales** – Mención de que los números como "00" son inválidos a menos que `n == 1`.
3. **Declarar la complejidad** – Mención `O(5^(n/2))` tiempo/espacio; si `n` fuera enorme, discuta cómo modificar el algoritmo.
4. **Primero los casos de edge** – Discutir los casos de base explícitamente antes de bucear a la recursión.
5. **Testing** – Después de escribir código, prueba para `n=1,2,3,4,5` para asegurar el correcto manejo de longitudes extrañas/inclusas.
6. **Evitar la codificación dura 4 o 5** – Utilice una estructura de datos de pares para mantener el código flexible.

-...

## 13. SEO‐Optimized Summary > seo-summary >

■ Esta guía ofrece la solución **LeetCode "Strobogrammatic Number II"** en **Java**, **Python**, y **C+**.
■ El algoritmo conciso recursivo construye todos los números estrobogrammáticos de longitud `n` (1 ≤ n ≤ 14) en el tiempo `O(5^(n/2)).
■ Puntos clave: casos de base (`n==0` → `"', `n=1` → `["0","1","8"]`), evitar ceros líderes en el nivel más exterior, y evitar la repetición innecesaria.
■ Complejidad: exponencial `5^(n/2)`.
■ Las versiones alternativas BFS/iterative tienen un rendimiento idéntico.
■ Los entrevistadores a menudo buscan la capacidad de manejar casos de borde y discutir la complejidad; evitar salidas de "0...0" y apilar desbordamientos.

-...

## 13. Conclusión: Nombre=conclusión

La solución de retroceso recursivo es la forma más **natural** y ** legible** para generar todos los números estrobomáticos. Maneja limpiamente longitudes extrañas/incluso, salta ceros líderes, y funciona cómodamente dentro de las limitaciones del problema. Para los entrevistadores que prefieren lógica iterativa, un BFS basado en cola produce el mismo resultado sin recidiva.

■ **Pro tip** – Siempre pregunte si el entrevistador quiere la *cuenta* o la *lista*; si sólo el conteo importa, puede devolver `4 * 5^(n/2-1)` para incluso `n` y `4 * 5^(n-1)/2)` para extraña `n`, guardar memoria.

Buena suerte rompiendo “Strobogrammatic Number II” en su próxima entrevista de codificación! 🚀

-...

### Referencias

* Problema de LeetCode: https://leetcode.com/problems/strobogrammatic-number-ii/
* Soluciones discussed en GitHub (Java, Python, C++)

-...

**Keywords para SEO**: Strobogrammatic Number II, Solución LeetCode, retroceso recurrente, solución Java, solución Python, solución C++, consejos de entrevista, complejidad del tiempo, complejidad del espacio, alternativa BFS.