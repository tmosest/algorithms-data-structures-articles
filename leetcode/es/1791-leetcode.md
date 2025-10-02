-...
Título: LeetCode 1791. Busca Centro de Gráfico Estelar -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1791 – Find Center of a Star Graph
**Guía optimizada SEO, fragmentos de código y explicación para entrevistas* *

-...

### 🎯 ¿Cuál es el problema?

Se le da un gráfico *estrella* – un gráfico no dirigido con un único nodo “centro” que está conectado a cada otro nodo.
El gráfico es descrito por un array `edges`, donde cada entrada `[u, v]` representa un borde entre los nodos `u` y `v`.

**Retorna la etiqueta del nodo central. #

■ **Constraints**
* `3 ≤ n ≤ 105`
* `edges.length == n‐1`
* Cada entrada es un par de enteros distintos entre `1` y `n`.
* La entrada siempre representa un gráfico de estrellas válido.

-...

## ♥ Intuition – El truco de una línea

En un gráfico estrella, **todo borde contiene el centro**.
Elija dos bordes – el centro debe aparecer en *ambos* de ellos.

- Si `edges[0] [0] es el centro, también aparecerá en `edges[1]`.
- De lo contrario el otro punto final del primer borde debe ser el centro.

Eso da una solución *constant-time* (O(1)), sin bucles, sin memoria adicional.

-...

## ف Code – 3 Languages

### 1. Java

``java
*
* Leetcode 1791 – Find Center of Star Graph
* O(1) time ← O(1) space
*/
Solución de la clase pública {}
int findCenter(int[] edges) {
// El centro es el nodo común en los dos primeros bordes
retorno (edges[0][0] == edges[1] [0] tención de los bordes de la vida [0] == edges[1]
? edges[0][0] : edges[0][1];
}

// Arnés de prueba simple
public static void main(String[] args) {
Solución s = nueva solución ();
int[][] edges1 = {1, 2}, {2, 3}, {4, 2}};
System.out.println(s.findCenter(edges1)); // 2

int[][] edges2 = {1, 2}, {5, 1}, {1, 3}, {1, 4};
System.out.println(s.findCenter(edges2)); // 1
}
}
`` `

### 2. Python 3

``python
Solución de clase:
def findCenter(self, edges: List[List[int]]) int:
# O(1) - la misma lógica que Java
los bordes de retorno[0][0] si (edges[0][0] == los bordes[1][0] o
bordes[0][0] == bordes[1]) otros bordes[0][1]


# Demo
si __name_ == "__main__":
s = Solución()
print(s.findCenter([1, 2], [2, 3], [4, 2]])
print(s.findCenter([1, 2], [5, 1], [1, 3], [1, 4])) # 1
`` `

### 3. C++

``cpp
Incluido el título
usando std namespace;

*
* Leetcode 1791 – Find Center of Star Graph
* O(1) time ← O(1) space
*/
Clase Solución {
public:
int findCenter(vector seleccionadovector fielint estrechos bordes) {}
retorno (edges[0][0] == edges[1] [0] tención de los bordes de la vida [0] == edges[1]
? edges[0][0] : edges[0][1];
}
};

int main() {}
Solución s;
vector de vectores e1{1,2},{2,3},{4,2}};
vector de vectores e2{1,2},{5,1},{1,3},{1,4};
cout se realizó s.findCenter(e1)
cout se realizó s.findCenter(e2)
}
`` `

-...

## 🕵ר️ El Bien, el Mal, el Ugly

Silencio Silencio
Silencio------------Prince------
Silencio **La complejidad del tiempo** Silencio O(1) – perfecto para entrevistas Silencio – ←
Silencio **Complejidad del espacio** Silencio O(1) – ninguna estructura adicional Silencio – Silencio
Silencio **Implementación** Silencio One-liner – limpio, legible Silencio Ninguno ← Sobre-ingeniería con bucles o mapas desperdicia tiempo
Silencio **Robustness** Silencio Trabaja para cualquier gráfico estrella válido Silencio depende de las `edges[1] existentes - pero `n≥3` lo garantiza Silencio Si la entrada viola las suposiciones, lanza `ArrayIndexOutOfBounds` Silencio
Silencio **Readability** Silencio Fácil de explicar: “mirar primero dos bordes” Silencio Podría parecer “mágico” a algunos Silencioso
Silencio ** Casos de emergencia** Silencio Maneja cualquier `n ' (≥3)

■ **Consejo:** Mención de la propiedad *observational* (centro aparece en todos los bordes) durante la entrevista; demuestra que usted lee la declaración a fondo.

-...

## 📊 Complexity Analysis

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
Silencio ** Tiempo** Silencio O(1) Silencio O(1) Silencio
tención **Espacio** Silencio O(1) Silencio O(1) Silencio
Silencio **Big‐O** Silencio ✔

Todas las soluciones son *amortizadas* O(1) porque inspeccionan en la mayoría de dos bordes.

-...

## 🔧 Alternatives > When to Use Them

TENIDO APARTAMENTO ANTERIOR Cuando hace Sentido ANTERIENTE
Silencio------------------------------
Silencio **Full scan** (`for edge in edges`) Silencio Si usted no notó la propiedad estrella, todavía O(n) pero aceptable para el pequeño `n` tiempo lineal, innecesario para `n=105` Silencio
Silencio **Hash map counting** Silencio Gráficos generales en los que el centro puede ser identificado por frecuencia TEN O(n) tiempo & espacio, overkill TEN
Silencio **Set intersection** Silencio Si usted quiere ilustrar las operaciones del set Silencio Still O(n) pero más claro para gráficos no estrellas Silencio

-...

## ⋅ How This Helps You Land a Job

* **Interview Prep** – Demostrar un cuchillo para *quick observation* y *constant‐time* trucos.
* **Code Quality** – One-liner, no hay números mágicos, comentarios claros.
* ** Pensamiento Algorítmico** – Mostrar que puedes identificar propiedades gráficas (el centro aparece en cada borde).
* **Performance** – Emphasize O(1) solution; interviewers love space‐time trade‐offs.

Añadir esto a tu cartera, compartir en GitHub, o publicar una entrada de blog. Mencione el ID de Leetcode, las etiquetas (`Easy`, `Graph`, `Arrays`), y resaltar el tiempo **O(1)** en el título – oro SEO para los reclutadores que buscan la solución "Leetcode 1791".

-...

## 📝 SEO‐Friendly Summary (para tu blog)

- **Título**: “Leetcode 1791 – Find Center of Star Graph in O(1): Java, Python, C++ One‐Liner
- **Meta Descripción**: “Solve Leetcode 1791 – Find Center of Star Graph utilizando una línea única de tiempo constante en Java, Python y C++. Aprende el truco, la complejidad del tiempo/espacio y las ideas de entrevista. ”
- **Keywords**: *Leetcode 1791, Find Center of Star Graph, O(1) solution, Java, Python, C++, algoritmo de gráfico, interrogante de ingeniero de software, entrevista prep*

-...

## 🚀 Takeaway

La función de definición del gráfico estrella – cada borde contiene el centro – te permite resolver Leetcode 1791 en *una línea* con **O(1)** tiempo y espacio.
Escriba el código limpio, explique la intuición, y impresionará a los entrevistadores y reclutadores por igual. ¡Feliz codificación!