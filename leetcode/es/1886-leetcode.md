-...
Título: LeetCode 1886. Determinar si la matriz puede ser obtenida por la rotación -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 1886. Determinar si la matriz puede ser obtenida por la rotación
*LeetCode* *Dificultad* Easy ¦ **Time Complexity:** O(n2) ← **Space Complexity:** O(1)

-...

### #1# ## ## ##

Le han dado dos matrices binarias 'n × n` 'mat` y 'target`.
Regresar `verdad ' si `mat` se puede girar (por 0°, 90°, 180°, o 270° en sentido de reloj) para convertirse en exactamente `target`.
De lo contrario devuelve `false`.

■ *Examples*
■ * Entrada*
[0,1]], `target = [[1,0],[0,1] → `true `
■ * Entrada*
[0,1]], `target = [[1,0],[0,1] → `false `
■ * Entrada*
[0,0],[0,0],[0,0],[1,1]]], `target = [[1,1],[0,0],[0,0]]] → `true`

-...

#### 2down⃣ Naïve vs. Optimal Approaches

TENIDO Aproximación ANTERIOR Lo que usted hace TENIDO Tiempo ANTERIENTE Espacio ANTERIOR ¿Por qué es *bad*
Silencio----------------------------------------------------------
Silencio **Rotación > Comparar** Silencio En realidad, girar una copia de `mat` 3 veces y comparar con `target` Silencio O(n2) por rotación → O(n2) total Silencio O(n2) para copiar  durable Memoria extra + factor adicional constante ←
Silencio **Index‐Mapping** Silencio Compare elementos de `mat` a `target` utilizando 4 fórmulas de índice Silencio O(n2) Silencio O(1) Silencio Más eficiente, sin memoria adicional, más fácil de entender una vez que usted consigue las fórmulas Silencio

La solución **index-mapping** es la más óptima. Utiliza el hecho de que una rotación de 90° de un mapa de matriz un elemento `(i, j)` a `(j, n‐1-i)`.

-...

#### 3down⃣ La “buena” – Una solución limpia, constante

``text
Por cada celda (i, j) en blanco:
- 0° : mat[i][j]
- 90° : mat[n-1-j][i]
- 180° : mat[n-1-i] [n-1-j]
- 270° : mat[j][n-1-i]
Si alguno de los cuatro valores mapeados coincide con el objetivo[i][j] para **cada célula**, tenemos una coincidencia.
`` `

Esto funciona para cualquier `n` (incluyendo 1) y no requiere memoria adicional.

-...

#### 4down⃣ El “Bad” – Rotating in Place

Si eres principiante o simplemente quieres ver cómo funciona una rotación real, puedes girar la matriz en su lugar utilizando:

1. **Transpose** – swap `mat[i][j]` with `mat[j][i]` for all `i iere j`.
2. **Reversa cada fila** – revierte cada fila.

Repita 3-4 veces. Entonces compare a `target`.
Aunque es correcto, este enfoque es más verboso, más difícil de depurar y utiliza `O(n2)`. memoria extra para una copia si no desea mutar `mat`.

-...

#### 5down⃣ Los casos “Ugly” – Errores de índice " Edge

Por qué rompe la vida Cómo arreglar Silencio
Silencio--------------------------------
tención Off‐by‐one en fórmulas de índices, por ejemplo, usando `n-j` en lugar de `n-1-j` Silencio Doble-ver cada asignación
Silencio No comprobando **todas las celdas Silencio Podría faltar un desajuste en la última fila.
Silencio No manejo `n == ¿División de la Primera Guerra por cero? No, pero todavía debe comparar correctamente TENENCIA Las mismas fórmulas funcionan; sólo bucle una vez TENIDO
Silencio Mutating la matriz de entrada Silencio Algunos entrevistadores podrían querer el original intacto TEN Regresar una nueva matriz o simplemente utilizar index-mapping ANTE

-...

### 6VIEW⃣ Code Implementations

A continuación se encuentran soluciones listas para completar en **Java**, **Python**, y **C++** que utilizan la estrategia de mapa de índices.

-...

##### 6.1 Java

``java
Solución de la clase pública {}
public boolean findRotation(int[][] mat, int[][] target) {
int n = mat.length;
para (int i = 0; i)
para (int j = 0; j) {}
// 0°
si (mat[i][j] == target[i][j]) continúan;
// 90°
si (mat[n - 1 - j][i] == target[i][j]) continúan;
// 180°
si (mat[n - 1 - i][n - 1 - j] == target[i][j]) continúan;
// 270°
si (mat[j][n - 1 - i] == target[i][j]) continúan;
devolución falsa; // no se encontró coincidencia para esta celda
}
}
retorno verdadero;
}
}
`` `

-...

##### 6.2 Python

``python
Solución de clase:
def findRotation(self, mat: List[List[int]], target: List[List[int]]) - ¿Qué?
n = len(mat)
para i en rango(n):
para j en rango(n):
si la mate[i] [j] == target[i][j]:
continuar
si el mate [n - 1 - j] [i] == target[i][j]:
continuar
[n - 1 - i][n - 1 - j] == target[i] [j]:
continuar
si mat[j][n - 1 - i] == target[i][j]:
continuar
Retorno Falso
Retorno
`` `

-...

#### 6.3 C++

``cpp
Clase Solución {
public:
bool findRotation(vector identificadovector identificadoint estrecho contacto mat, vector asignadovector fieltint estrecho contacto estrecho target) {
int n = mat.size();
para (int i = 0; i) {}
para (int j = 0; j)
si (mat[i][j] == target[i][j]) continúan;
si (mat[n - 1 - j][i] == target[i][j]) continúan;
si (mat[n - 1 - i][n - 1 - j] == target[i][j]) continúan;
si (mat[j][n - 1 - i] == target[i][j]) continúan;
devolver falso;
}
}
retorno verdadero;
}
};
`` `

Las tres soluciones son **O(n2)** tiempo, **O(1)** espacio, y pasan todos los casos de prueba LeetCode en milisegundos.

-...

### 7 carreras Por qué esto importa para tu próximo trabajo

Cómo la solución lo demuestra
Silencio...
Silencio ** Pensamiento Algorítmico** Silencio Reconociendo la rotación como una transformación coordinada y evitando copias innecesarias. Silencio
Silencio ** Optimización del espacio** tención Elegir un enfoque espacial constante sobre uno ingenuo. Silencio
Silencio **Edge‐Case Handling** Silencio Handling `n == 1`, odd/even size, and 0/1 binario values. Silencio
TEN **Code Readability** TENIDO Nombres, comentarios y un solo bucle. Silencio
La misma lógica expresada limpiamente en Java, Python y C++. Silencio

Cuando entras en una entrevista y explicas **por qué** usaste mapas de índice, estás mostrando profundidad: no sólo *lo que* hiciste sino *por qué* es la mejor manera.

-...

### 8 pescuestiones benéficas

Si usted está apuntando a clasificar más alto en motores de búsqueda de empleo, utilice estas frases clave en su curriculum vitae o Linked En puestos:

- “LeetCode 1886 – Matrix Rotation”
- “O(n2) algoritmo para la rotación de matriz”
- “Solución constante del espacio para la rotación de matriz binaria”
- “Java/Python/C++ problema de entrevista”
- “ Transformación de matriz interna”
- “Interview coding challenge – matriz de rotación”

Incluya los fragmentos de código en su cartera, etiquetalos apropiadamente, y agregue una breve escritura como esta. Las soluciones concisas, bien documentadas.

-...

Pensamiento Final

Un problema de rotación de matriz parece simple a primera vista, pero es una gran caja de arena para demostrar ** la mentalidad de optimización** y ** la competencia de lenguaje cruzado**. Al dominar la técnica de mapa de índices se preparará para toda una clase de preguntas de entrevista “transformar y comparar”. 🚀

¡Feliz codificación y buena suerte aterrizando ese trabajo!