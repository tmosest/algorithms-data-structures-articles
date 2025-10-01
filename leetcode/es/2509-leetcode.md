-...
Título: LeetCode 2509. Ciclo de longitud Consultas en un árbol -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 Ciclo de duración Consultas en un árbol - Una guía completa de solución optimizada SEO
■ *LeetCode 2509 – Hard – Java / Python / C++*

-...

## Tabla de contenidos

Silencio Sección Silencio Lo que aprenderás
Silencio...
← | Problema Resúmenes tóxico Entender el problema de la gráfica y por qué es duro
Silencio 📌 Key Insight ← Lowest Common Ancestor (LCA) truco Silencio
TEN | Algorithm ← Solución paso a paso en inglés TEN
← Análisis de la Complejidad TENIDO Tiempo " Cambios en el espacio
← | Code tención Java, Python & C++ implementaciones tención
Buenas, malas Donde el enfoque brilla, falla, y cómo retocar
Silencio | SEO Highlights ← Por qué este blog ayuda a tu búsqueda de trabajo ←
← | TL;DR

-...

## 1. Panorama general de los problemas

■ **Given** un árbol binario perfecto con nodos `2^n − 1` (root = 1).
■ Por cada consulta `[ai, bi]`:
■ 1. Añada un borde entre los nodos `ai ' y `bi ' .
■ 2. Encuentra la longitud del ciclo único creado.
■ 3. Quitar el borde añadido.

** Objetivo:** Devuelve una serie de longitudes de ciclo para todas las consultas.

¿Por qué Duro? *
El árbol puede tener hasta 2^30 − 1 nodos ( 5,001 mil millones), pero sólo obtenemos en la mayoría de 105 consultas. Construir el árbol explícitamente es imposible; debemos responder a cada consulta en el tiempo *logarítmico*.

-...

## 2. Key Insight – LCA es el secreto

Un árbol binario perfecto construido como un montón binario tiene una regla padre fácil:

`` `
parent(v) = v / 2 (división entero)
`` `

Cuando conectamos dos nodos `a` y `b`, el único ciclo que puede aparecer es:

`` `
a - (a a LCA) - LCA - (LCA a b)
`` `

La longitud del ciclo es igual

`` `
distancia(a, LCA) + distancia(b, LCA) + 1
`` `

Pero podemos calcularlo sin encontrar explícitamente la distancia, simplemente moviendo el nodo * más grande* hacia arriba hasta que ambos se reúnan. Cada paso ascendente cuenta como un borde, y finalmente agregamos uno más para el borde recién insertado.

-...

## 3. Algoritmo en inglés sencillo

`` `
para cada consulta (a, b):
longitud = 1 // el borde añadido
mientras que un != b:
si un mento b:
a = a / 2 / // mover un arriba
más:
b = b / 2 // movimiento b
longitud += 1
tienda longitud
`` `

¿Por qué funciona?

- Mover el nodo más grande hacia arriba mantiene el número total de movimientos mínimos: siempre reducemos el mayor de los dos valores hasta que sean iguales.
- Cada división corresponde a atravesar un borde de árbol.
- El bucle termina cuando `a == b`, que es exactamente el LCA.
- La "longitud" final es el número de bordes en el ciclo.

-...

## 4. Análisis de la complejidad

TEN TERMINAR TENIDO Computation TENIDO Explicación
Silencio----------------------------
Silencio **Tiempo por consulta** Silencioso `O(log n)` altura Árbol ≤ `log2(2n−1)` = `n`. Cada iteración de bucle reduce el nodo mayor por al menos un factor de 2. Silencio
tención **Tiempo total** Silencio `O(m · log n)` Silencio `m ≤ 105`, `n ≤ 30`. A la mayoría de 30 * 105 ♥ 3 M operaciones – fácilmente dentro de los límites. Silencio
Silencio** (aparte de la salida) Silencio No se necesitan estructuras auxiliares de datos. Silencio

-...

## 5. Código

A continuación encontrará la solución **stand-alone** para cada idioma.
Cada implementación sigue el algoritmo exacto arriba.

### 5.1 Java

``java
importar java.util*;

Solución de la clase pública {}
int[] cycleLengthQueries(int n, int[][] consultas) {
int m = consultas. longitud;
int[] ans = nuevo int[m];
para (int i = 0; i) {}
int a = consultas[i][0];
int b = consultas[i][1];
longitud int = 1; // el borde añadido
mientras (a != b) {
si (a нел b) a нель = 1; // a /= 2
b " títulos " 1; // b /= 2
+ longitud;
}
as[i] = longitud;
}
devolver los ans;
}

/* Opcional: Principal para la prueba manual rápida */
public static void main(String[] args) {
Solución sol = nueva solución ();
int[][] q = {5,3},{4,7},{2,3};
System.out.println(Arrays.toString(sol.cycleLengthQueries(3, q))));
// Producto: [4, 5, 3]
}
}
`` `

### 5.2 Python

``python
Solución de clase:
def cycleLengthQueries(self, n: int, queries: List[List[int]]) - No. List[int]:
ans = []
para a, b en consultas:
longitud = 1
mientras que un != b:
si un mento b:
a//= 2
más:
b/= 2
longitud += 1
ans.append(length)
Retorno

Prueba rápida
si __name_ == "__main__":
sol = Solución()
print(sol.cycleLengthQueries(3, [[5,3],[4,7],[2,3]])
# Output: [4, 5, 3]
`` `

### 5.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector cycleLengthQueries(int n, vector seleccionadovector identificadointющия queries) {}
vector significar uns
para (auto &q : consultas) {}
int a = q[0], b = q[1];
int len = 1; // borde añadido
mientras (a != b) {
si (a > b) a /= 2;
b /= 2;
++len;
}
ans.push_back(len);
}
devolver los ans;
}
};

// Opcional principal para pruebas rápidas
int main() {}
Sol de solución;
vector de vectores seleccionados {5,3},{4,7},{2,3};
vector implicado res = sol.cycleLengthQueries(3, q);
para (int x : res) cout seccionó x se hizo ";
// Producto: 4 5 3
retorno 0;
}
`` `

-...

## 6. Bien, mal

Silencio Silencio Silencio Silencio Silencio Silencio Silencio
Silencio--------------------------
Silencio **Tiempo** Silencioso rápido (`O(log n)` por consulta). Para *extremadamente* muchas consultas (` confía106`) podrías golpear el factor constante de I/O. Silencio
Silencio **Espacio** Silencio Minimal (`O(1)`). Silencio – Silencio – Silencio
Silencio **Readability** Silencio muy claro. Silencio Ninguno. Silencio Requiere la comprensión de la división entero como movimiento padre. Silencio
Silencio **Edge Cases** Silencio Handles root " hoja nodos sin costura. TEN – TEN si accidentalmente intercambias `a` y `b`, algoritmo todavía funciona debido a la simetría. Silencio
Silencio **Extensibilidad** Silencio Trabaja para *cualquier* árbol binario completo. Silencio – Silencio No** generalizar a los árboles arbitrarios – requiere la función de los padres. Silencio
Silencio **Implementation Pitfalls** Silencio – Silencio En Python, use `/` (división entero). En C++, utilice `/`. En Java, tenga cuidado con `` título `` vs `/`. peru Mis-reading the problem as "find the longest cycle" – sólo hay un ciclo por consulta. Silencio

-...

## 7. SEO Highlights – Why This Blog Helps Your Career

1. **Keyword‐Rich Title* *
*Cycle Longitud Consultas en un árbol – LeetCode 2509 Hard Solution (Java / Python / C++)* – coincide con lo que buscan los reclutadores.

2. **Problema " Language Tags " *
Usa etiquetas como `BinaryTree`, `LCA`, `LeetCodeHard`, `Interview`, `CodingInterview`, `Java`, `Python`, `C++`.
El equipo filtra a menudo a los candidatos por estas etiquetas.

3. **Código completo y estructurado**
Proporciona soluciones *copy‐paste*, reduciendo la fricción para los reclutadores que quieren ver código limpio.

4. **Discusión de la ejecución**
Muestras que puedes resolver enormes restricciones con la complejidad de `O(log n)` – un punto de freno de entrevista real.

5. ** Autocontenido* *
Incluye los arnés de `main` / test para que pueda ejecutar y verificar localmente.

6. **Explicación de casos de borde**
Muestra profundidad de comprensión – los reclutadores aman a los candidatos que piensan en las condiciones del borde.

-...

## 7. TL;DR

- **Insight:** La longitud del ciclo equivale al número de movimientos ascendentes a la LCA más uno.
*Loop* *mientras (a != b) { si (a √≥ b) a/= 2; b /= 2; longitud++; }`
- ** Resultado:** `O(m · log n)` tiempo, `O(1)` espacio extra.
- Idiomas: Java, Python, C++ – mismo algoritmo, pequeñas diferencias de sintaxis.

-...

## 8. Palabras finales

Este blog te da:

- Una solución *completa* para LeetCode 2509 en **Java, Python y C+**.
- Un algoritmo **easy‐to-implement** que se ejecuta en el tiempo *logaritmic* – un conocimiento imprescindible para cualquier entrevista algoritmo.
- Una escritura clara, *Amigable* que muestra sus habilidades de solución de problemas y codificación a los posibles empleadores.

¡Feliz codificación y buena suerte aterrizando ese papel de sueño! ▪