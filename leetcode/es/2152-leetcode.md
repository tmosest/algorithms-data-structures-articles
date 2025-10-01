-...
Título: LeetCode 2152. Número mínimo de líneas a puntos de cobertura -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 “Minimum Number of Lines to Cover Points” – LeetCode 2152
## 📚 Problema general
TENIDO ANTERIOR ANTERIOR ANTERIOR
Silencio...
Silencioso **LeetCode ID**
Silencioso **Dificultad**
Silencio **Título** Silencio Número Mínimo de Líneas a Puntos de Cubierta
Silencio **Core Idea** Silencio Encuentra el conjunto más pequeño de líneas rectas que cubren todos los puntos dados en un plan XY. Silencio
tención **Constraints** tención `1 ≤ puntos.length ≤ 10`, `puntos[i] = [xi, yi]`, todos los puntos únicos, `-100 ≤ xi, yi ≤ 100`. Silencio

■ ** Objetivo**: Devuelve el número mínimo de líneas rectas necesarias para cubrir cada punto.

-...

##  Settlement Why You should Master This Problem

* **Interview staple** – Muchas empresas tecnológicas piden esto para probar la optimización combinatoria, la recursión, el mordisco y las habilidades de DP.
* **Versatilidad lingüística** – Existen soluciones en **Java, Python y C++**. La demostración de la competencia entre los idiomas muestra flexibilidad a los administradores de contratación.
* ** Profundidad de algoritmo* Aprenderás a cambiar brute‐force vs. memoization, y cómo manejar el estado con máscaras de bit.

-...

Estrategias de alto nivel

TENIDO TERRIENTE Complejidad ANTERIOR Cuando se utiliza
Silencio----------------------------
Silencio **Recursivo + Brute‐Force** Silencio `O(n^3)` (caso peor) TENIDO Small `n` (≤ 10) – simple de código
tención **DFS + Bitmask DP** Silencioso `O(n^3 * 2^n)` ← Comercio equilibrado para `n` ≤ 10
Silencio **Recuperación Memoizada** Silencio Mismo que DP, pero a menudo más fácil de entender Silencio Cuando usted desea evitar tablas explícitas DP

■ **La mejor elección**: Para `n ≤ 10`, el DFS + bitmask DP es eficiente y fácil de implementar.
■ **El mejor lugar**: 10 puntos → 1024 estados → perfectamente bien.

-...

## 📦 Code Implementations

A continuación encontrará soluciones totalmente adaptadas en **Java, Python y C+**.
Cada fragmento de código incluye:

* Un pequeño arnés de prueba (método opcional `main` / `if __name_ == "__main__":`).
* Firmas de funciones claras que coinciden con el estilo LeetCode.
* Inline comments explaining each step.

-...

#### 1down⃣ Java (Bitmask + DFS)

``java
importar java.util*;

Clase Solución {
// Máscara de blanco: todos los puntos cubiertos
blanco privado Máscara;
// Mapa de la memoria: clave - confianza Líneas mínimas
mapa privado: Integer, Integer memo;

public int minimumLines(int[][] points) {
int n = puntos. longitud;
objetivo Máscara = (1 < > >
memo = nuevo HashMap garantizado();
dfs(0, puntos);
}

// DFS sobre estado de bitmask
int privado dfs(inmascara, int[] puntos) {
si (mask == targetMask) retorno 0; // todos los puntos cubiertos
si (memo.containsKey(mask))) devuelve memo.get(mask);

// Encontrar el primer punto descubierto
int first = 0;
(música) (música) 0) primero++;

int best = Integer.MAX_VALUE;

// Trate de dibujar una línea que pasa por 'primero' y algún otro punto
para (int i = 0; i) i++) {
si (i == primera tención involuntaria (mask > (1 > ) 0) continuar;
int newMask = mascara ¦ (1 י se hizo primero)

doble pendiente = pendiente (puntos [primer], puntos[i]);

// Incluir todos los puntos en esta línea
para (int j = 0; j)
si (j ==primer TENIDO TENIDO J == i) continúan;
si (mask " (1 " ) 0) continuar;
si (Double.compare(slope, slope(points[first], points[j])) == 0)
newMask tención= (1 iere escrito j);
}
mejor = Math.min(best, 1 + dfs(newMask, points));
}

// Caso de borde: todos los puntos restantes son collinear con 'primero '
si (mejor == entero. MAX_VALUE) best = 1;

memo.put(mask, best);
devolver mejor;
}

doble pendiente privada(int[] a, int[] b) {
// Evite la división por cero: línea vertical - título Infinity
si (a[0] == b[0]) devolver Doble. POSITIVE_INFINITY;
(doble)(b[1] - a[1]) / (b[0] - a[0]);
}

// -------- Arnés de prueba...
public static void main(String[] args) {
Solución sol = nueva solución ();
int[][] points1 = {0,1},{2,3},{4,5},{4,3};
int[][] points2 = {0,2},{-2,-2},{1,4};
System.out.println("Ejemplo 1: " + sol.minimumLines(puntos1)); // 2
System.out.println("Ejemplo 2: " + sol.minimumLines(puntos2)); // 1
}
}
`` `

-...

Python (Bitmask + DFS)

``python
desde functools import lru_cache
de la importación Lista

Solución de clase:
mínimo Líneas(auto, puntos: List[List[int]]) - int:
n = len(puntos)
objetivo = (1  se realizó n) - 1

def slope(a, b):
si a[0] == b[0]:
# línea vertical #
(b[1] - a[1]) / (b[0] - a[0])

@lru_cache(None)
def dfs(mask: int) - título int:
si máscara == objetivo:
retorno 0
# Find first uncovered point
primero = 0
mientras que la máscara " (1
primero += 1

mejor = flotante('inf')
para i en rango(n):
si == primero o mascara " (1 " )
continuar
new_mask = mascara tención (1 iere primero)
sl = pendiente(puntos [primer], puntos[i])

para j en rango(n):
si j in (primero, i) o mascara " (1 " )
continuar
si abs(sl - pendiente(puntos [primer], puntos[j])) 1e-9:
new_mask TENIDO= (1 ANTE 10)

mejor = min(mejor, 1 + dfs(new_mask)

retorno 1 si mejor == flotante('inf') mejor

devolver dfs(0)

# -------- Arnés de prueba...
si __name_ == "__main__":
sol = Solución()
print(sol.minimumLines([0,1],[2,3],[4,5],[4,3]]) # 2
print(sol.minimumLines([0,2],[-2,-2],[1,4])) # 1
`` `

-...

### 3down⃣ C++ (Bitmask + DFS)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minimumLines(vector seleccionadovector fielint estrecho puntos) {
int n = points.size();
int target = (1 " identificados " ) - 1;
vector implicado memo(1  se realizó n, -1);
dfs(0, puntos, objetivo, memo);
}

privado:
doble pendiente(cont vector identificadoint limitada a, const vector implicado
si (a[0] == b[0]) devuelve numeric_limites obtenidosdouble título::infinity(); // vertical
retorno estático_cast observadodouble(b[1] - a[1]) / (b[0] - a[0]);
}

int dfs(int mask, const vector seleccionadovector identificadoint cuanto usa pts, int target, vector interpretadoint
si (mask == target) retorno 0;
si (memo[mask] != -1) memo de retorno;

// Encontrar el primer punto descubierto
int first = 0;
mientras que (mask " (1 " se hizo primero) " ;

int best = INT_MAX;
para (int i = 0; i) ++i) {
si (i == primera tención infligida (mask " (1  obtenidos i)))) continúan;
int newMask = mascara ¦ (1 י se hizo primero)
doble sl = pendiente(pts[first], pts[i]);

para (int j = 0; j) ++j) {
si (j == first TENIDO EN SUPERVISIÓN J == i ANTERIVADA (mask " (1 " identificados j))) continúan;
si (abs(sl - slope(pts[first], pts[j]))
newMask tención= (1 iere escrito j);
}
mejor = min(mejor, 1 + dfs(newMask, pts, target, memo));
}

si (mejor == INT_MAX) mejor = 1; // Todos los puntos restantes collinear con el primero
memo[mask] = best;
devolver mejor;
}
};

// -------- Arnés de prueba...
int main() {}
Solución s;
vector de vectores pts1 = {0,1},{2,3},{4,5},{4,3}};
vector de vectores pts2 = {0,2},{-2,-2},{1,4};
cout se realizó s.minimumLines(pts1)
cout se realizó s.minimumLines(pts2)
retorno 0;
}
`` `

-...

## 📊 Complexity Breakdown

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio **Cálculo de la pendiente**
Silencio **Las transiciones estatales de las Fuerzas de Defensa**
Silencio **Número de estados** Silencio `2^n` Silencio ≤ 1024 Silencio
tención **Total** Silencioso `O(n^3 * 2^n)` Silencio ≤ `10^5` operaciones, > 1 ms en la práctica

¿Por qué no?
■ 1. Elija el primer punto descubierto (`n`).
■ 2. Parla con cualquier otro punto descubierto (`n`).
■ 3. Escanear el resto para recoger puntos collineales (`n`).

■ **Espacio** – Memo tabla del tamaño `2^n` (≤ 1024 enteros).

-...

## 🔄 Alternative: Pure Brute‐Force (Recursive)

Si prefieres una solución ** "no-memo"** para la máxima legibilidad, el siguiente esqueleto Python funciona para 'n ≤ 10'.

``python
def brute_force(puntos):
n = len(puntos)
mejor = n

def helper(descubierto):
no local mejor
si no se descubre: # todos los puntos cubiertos
retorno 0
si len(descubierto) lo mejor: # podando
mejor

primero = descubierto[0]
por segundo en descubierto[1:]:
line_points = [p for p in uncovered if on_same_line(first, second, p)]
new_uncovered = [p for p in uncovered if p not in line_points]
mejor = min(best, 1 + helper(new_uncovered)
mejor

helper(puntos)
`` `

■ **Drawback** – Sin memoización, pero aún así se hicieron permutaciones.

-...

## 🎯 Take‐Away Checklist (Entreview)

1. ** Representación del Estado* *
* Use una máscara de bits (`int mask`) – cada bit representa si un punto ya está cubierto.
2. **Recursivo DFS**
* Escoge el primer punto descubierto, empareja con otro punto, construye una línea, y recurre a la nueva máscara.
3. **Memoización / DP**
* Resultados de caché para cada máscara (`lru_cache` en Python, `unordered_map` o vector en Java/C++).
4. **Manejo de pendiente**
* Líneas verticales con `Infinity ' o `numeric_limits realizadasdouble::infinity()`.
* Use una tolerancia (`1e‐9`) al comparar las pendientes de punto flotante.

5. ** Casos de emergencia**
* Todos los puntos restantes collinear con el primer punto descubierto → utilizar una línea.

-...

## 📈 Big‐O Summary (DFS + Bitmask)

TEN TERRITOR TEN TEN ANTE
Silencio...
Silencio ** Tiempo** Silencioso `O(n^3 * 2^n)` Silencio
tención **Espacio** Silencioso `O(2^n)` para la memoización + pila de recursión (`≤ 10` niveles). Silencio
Silencio **Práctico** Silencio Para `n = 10` → 1024 estados, ♥ 5 × 105 operaciones - se ejecuta en

-...

## 🛠 Qué mostrar en su resumen

Esquía en la vida útil Silencio
Silencio...
Silencio ** Algorithm Design** ← “Solved LeetCode 2152 usando DFS con bit-mask DP para minimizar las líneas que cubren hasta 10 puntos”. Silencio
Silencio ** Análisis de la complejidad** Silencioso “Conseguido `O(n3·2n) ` tiempo y `O(2n) ` espacio; demostró la memoización completa.” Silencio
Silencio **Multilingual** Silencioso “Soluciones ampliadas en **Java, Python y C+**, mostrando fluidez en el lenguaje cruzado”. Silencio
"Usó este problema para conseguir un papel en XYZ Tech – entrevista comentarios elogió mi clara estrategia de codificación estatal". Silencio

■ **Tip**: Al responder preguntas de entrevista, comience con la traducción **problema-transformación** (bitmask, DP, recursion), luego explique el **state** y **transiciones**. Muestra tu análisis de complejidad para probar que entendiste las operaciones.

-...

##  inaceptable Bonus – Quick‐Start Playground

Si desea experimentar localmente, simplemente copiar el fragmento de idioma elegido en un archivo y ejecutarlo. La sección incluida `main`/`if __name_ == "__main__":` imprimirá las salidas esperadas:

``bash
Solución de javac. java " java Solution
Ejemplo 1: 2
Ejemplo 2: 1

Solución de $ pitón3. py
2
1

$ ./a.out
2
1
`` `

-...

## 🎯 Final Take‐ Away

* Para LeetCode 2152, **DFS + Bitmask DP** es el lugar dulce: elegante, rápido y lingüístico-agnóstico.
* Master the **state‐encoding** (caras bit) y **memoization** patrones – son útiles para una amplia variedad de problemas de entrevista (por ejemplo, “Set Cover”, “Maximum Subsequence”, “Stickers to Spell Word”).
* Práctica que explica el algoritmo, la complejidad y los casos de borde – comunicación clara es la mitad de la entrevista gana!

Buena suerte, y feliz codificación! 🚀

-...

■ **Meta Descripción** – “Solve LeetCode 2152: Número mínimo de líneas a puntos de cubierta. Obtenga las soluciones óptimas Java, Python y C+++, análisis algorítmico y consejos de entrevista para llegar a su próxima entrevista de trabajo. ”