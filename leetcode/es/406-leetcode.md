-...
Título: LeetCode 406. Reconstrucción por la altura -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Queue Reconstruction by Height – LeetCode 406
*El Bien, el Mal, y el Ugly – A Deep‐ Buceo + Java/Python/C++ Soluciones*

-...

### 📌 TL;DR
■ **Problema:** Reconstruir una cola dada `[altura, k]` pares donde `k` es el número de personas en frente que son **taller o igual**.
■ **Solución:** Ordenar a la gente **Crecer la altura** (ties → aumentar `k') e insertar a cada persona en el índice `k`.
■ **La complejidad:** `O(n2)` tiempo, `O(n)` espacio (simple codicia).
■ **Variantes:** `O(n log n)` utilizando un Árbol de Indización / Árbol de Segmento binario.

-...

## 1. Introducción

Al buscar un trabajo de primera línea, los reclutadores les encantan los problemas “LeetCode-style” que muestran soluciones *clever*.
“Queue Reconstruction by Height” es un problema medio clásico que a menudo se pregunta en entrevistas.

En este artículo, vamos a:

1. Comprender el problema y sus limitaciones.
2. Camine a través del algoritmo codicioso “sort-and‐insert” (la parte *buena*).
3. Discuss trampas, casos de borde, y por qué algunas personas piensan que es la parte *bad*.
4. Explore el *ugly* – el cuello de botella de complejidad y las estructuras de datos más avanzadas.
5. Proporcione códigos listos para copiar en **Java**, **Python**, y **C+**.
6. Ofrece consejos sobre hacer el post SEO-friendly (palabras clave, meta-descripción, títulos, etc.) para atraer administradores de contratación.

-...

## 2. Declaración de problemas

Given an array ` people` of `n` pairs `[hi, ki]`:

- 'hi' - altura de la persona i-th.
- `ki` - número de personas frente a la persona i, cuya altura es **≥** `hi`.

Reconstruir la cola que satisface a todos los pares.
Regrese la cola como un array 2-D `queue[j] = [hj, kj]` donde `queue[0]` es el frente.

**Constraints* *

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio...
Ø ≤ 2000
Ø ≤ ≤ ≤ 106
Silencioso
Una reconstrucción válida siempre existe.

-...

## 3. Intuición – ¿Por qué funciona “Sort & Insertar”

1. **Pon a la gente más alta primero. #
Para la persona más alta, la única manera de satisfacer `k` es ponerlo en posición `k`.
Ya que nadie es más alto, `k` sólo cuenta a sí mismo.

2. **Insertar gente más corta después. #
Al insertar una persona más corta, las personas ya colocadas más altas no afectarán a 'k' porque son más altas o iguales.
Al insertarse en el índice exacto " k " , garantizamos que las personas más altas o iguales estén por delante.

3. *La regla de la orden*
*Ordenar por la altura descendente* → más alto primero.
*Ties*: ordenar ascendiendo `k` para que las personas con la misma altura pero más pequeñas `k` se coloquen antes, asegurando la corrección.

-...

## 4. Algoritm (Greedy)

``text
ordenar gente por:
1. altura descendente
2. k ascendente (para alturas iguales)

cola = lista vacía
para cada persona (h, k) en lista clasificada:
insertar persona en el índice k en la cola

de retorno
`` `

¿Por qué no?
La inserción en un array a un índice aleatorio cuesta `O(n)` debido a la transferencia.
Hacer esto `n` veces produce `O(n2)`.

**Espacio:**
Utilizamos una lista adicional para la salida – `O(n)`.

-...

## 5. Código - 3 idiomas

## 5.1 Java (Inserción LinkedList)

``java
importar java.util*;

Solución de la clase pública {}
int[][] reconstructQueue(int[][] people) {
// 1. Ordenar por altura descendiendo, k ascendiendo
Arrays.sort(personas, nuevo Comparador) {}
int compare(int[] a, int[] b) {
si (a[0] != b[0]) retorno b[0] - a[0]; // altura descendiendo
volver a[1] - b[1]; // k ascender
}
});

// 2. Insertar en el índice k utilizando LinkedList (O(1) por inserción)
Lista obtenida[] Resultado del título = nuevo LinkedList correctamente();
(int[] p : people) {
result.add(p[1], p);
}

// 3. Convertirse en int[][]
int[][] ans = nuevo int[ people.length][2];
para (int i = 0; i) i++) {
as[i] = result.get(i);
}
devolver los ans;
}
}
`` `

■ ¿Por qué LinkedList?
■ La inserción en un `LinkedList` en un índice conocido es `O(1)` una vez que tengas el nodo.
■ Pero porque usamos 'List.add(index, element)', Java sigue caminando hasta el índice (`O(n)`) - el mismo costo asintotico.
■ El código es conciso y refleja la solución típica de LeetCode.

-...

### 5.2 Python (list insertion)

``python
Solución de clase:
def reconstruct Queue(self, people: List[List[int]) - No. List[List[int]]:
# Sort: altura descendente, k ascendente
people.sort(key=lambda x: (-x[0], x[1]))

res = []
para h, k en la gente:
[h, k]) # O(n) por inserción
retorno
`` `

-...

## 5.3 C++ (inserción de actor)

``cpp
Clase Solución {
public:
vector de vectores reconstructQueue(vector identificadovector fielint implica personas) {
// 1. Ordenar por altura descendiendo, k ascendiendo
(personas.begin(), people.end(),
[](cont vector identificadoint ánimo a, const vector identificadoint círculo b) {
si (a[0] != b[0]) devuelve a[0]
volver a[1]  b b[1]; // k ascender
});

// 2. Insertar en el índice k
vector de vectores res;
para (auto &p : personas) {
res.insert(res.begin() + p[1], p); // O(n) por insert
}
restitución;
}
};
`` `

-...

## 6. El Bien, el Mal, el Ugly

Silencio Silencio
Silencio------------Prince------
Silencio ** Complejidad del tiempo** Silencio Simple `O(n2)` – aceptable para `n ≤ 2000`. Silencio No es óptimo para muy grande `n`. Silencio Para `n` hasta 105, `O(n2) ` iría a tiempo. Silencio
Silencioso **Espacio** Silencioso `O(n)` – trivial.
Silencioso **Implementación Simplicidad** tención Una especie + bucle único. ← Requiere una clasificación cuidadosa comparador. ← Necesidad de implementar árbol de segmentos / TBI para `O(n log n)`. Silencio
Silencio **Readability** Silencio Natural claro, "verde". La regla de clasificación puede confundir a los principiantes. El código del árbol de Segment es verbose. Silencio
Silencio ** Casos de Edge** Silencio Handles lazos correctamente (a la derecha). Ninguno.
TEN **Real‐world Applicability** TEN Good for interview demos. TEN No escalable para conjuntos de datos enormes. ← Requiere conocimientos de estructuración de datos. Silencio

-...

## 7. Optimización a O(n log n) – Variante “Árbol de segmento”

Cuando `n` es grande, podemos mantener un **Árbol de Indización Indical (Fenwick)** o ** Árbol de Segmento** para encontrar la `k`‐th posición vacía en `O(log n)`.
La idea:

1. Ordenar como antes (altura descendente, k ascendente).
2. Inicialmente, todas las posiciones son libres (`1`).
3. Para cada persona, encuentre el índice de la ranura libre '(k+1).
4. Marca esa ranura como ocupada.

Esto reduce la complejidad general a `O(n log n)`.

■ *¿Por qué el artículo? *
■ Muestra un conjunto de habilidades de estructuración de datos más profundo – a menudo buscado por los gerentes de contratación.

-...

## 8. SEO " Interview‐ Consejos de Blog listos

TENIDO ELement TENIDO Recomendación
Silencio...
Silencio **Título** Silencioso “Reconstrucción profunda por Altura (LeetCode 406) – Java / Python / C++ Solution”
Silencio **Meta Descripción** Silencioso “Aprenda el enfoque codicioso de LeetCode 406 – Reconstrucción de colas por altura. Código completo en Java, Python y C++. Comprender la complejidad del tiempo, los casos de borde y las optimizaciones avanzadas”. Silencio
Silencio **Headings** Silencio H1 para título, H2 para secciones, H3 para sub-secciones. Silencio
Silencio **Keywords** Silencioso `Reconstrucción profunda por Altura`, `LeetCode 406`, `Solución de Java ' , `Solución de pitón ' , `solución de C++ ' , ` algoritmo grave ' , `árbol de segmento ' , ' árbol indizado binario ' . Silencio
Silencio **Code Formatting** Silencio Triple backticks with language identifiers. Silencio
Silencio ** Call‐to‐Action** Silencio “Si te estás preparando para entrevistas de codificación, agrega este problema a tu lista de práctica”. Silencio
Silencio **Imágenes** Silencio Esquema opcional que muestra el proceso de clasificación e inserción. Silencio
Silencio ** Enlaces internos** tención Enlace a otros blogs de algoritmos (“Trucos de ordenación”, “Árbol de Indización Indignaria”). Silencio
Silencio ** Enlaces externos** Silencio Página de problemas oficial LeetCode y soluciones principales (como en el aviso). Silencio

-...

## 9. Conclusión

- **Greedy Sort > Insert** es la solución canónica para *Reconstrucción por Altura*.
- Funciona en `O(n2)` - fino para las restricciones de entrevista.
- Para conjuntos de datos grandes, actualice a una solución `O(n log n)` utilizando BIT/Segment Tree.
- Los fragmentos proporcionados Java, Python y C++ cubren la versión amigable de la entrevista y se pueden copiar en su espacio de trabajo IDE o LeetCode.

¡Feliz codificación! 🚀
*(Si encontró este artículo útil, considere compartir o dejar un comentario. ¡Feliz entrevista!) *

-..