-...
Título: LeetCode 1561. Número máximo de monedas que usted puede obtener -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1561 – * Número máximo de monedas que usted puede obtener*
**Medium tención 3 n pilas  durable O(n) time ⋅ O(max piles) space**

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

Silencio
Silencio...
Silencio**Introducción** eterna`int[] pilas` – 3 n pilas de monedas (1 ≤ montones[i] ≤ 104) tención
Silencio**Proceso** PrevenciónEn cada ronda se eligen 3 pilas.
" nbsp; tardíanbsp; Alice agarra la pila más grande.
" nbsp; tardíanbsp; Tú agarra la siguiente pila más grande.
" nbsp; limitadanbsp; Bob agarra la pila restante.
Silencio**Goal**tenciónMaximiza el número total de monedas con las que terminas.
Silencio**Output**fort`int` – máximo de monedas que puede recoger. Silencio

■ *Examples*
■ 1. `piles = [2,4,1,2,7,8]` → **9**
■ 2. `piles = [2,4,5]` → **4**
■ 3. `piles = [9,8,7,6,5,1,2,3,4]` → **18**

-...

El Bien, el Mal, y el Ugly

Silencio Silencio
Silencio------------Prince------
Silencio **Greedy Insight** Silencio Escoger el *segundo más grande* en cada triplet es óptimo – Alice siempre toma el más grande. Silencio Ninguno – la estrategia avaricia es probablemente óptima. ← Malentendido el orden puede llevar a un algoritmo *wrong* O(n). Silencio
Silencioso ** Complejidad en el tiempo** Silencioso `O(n)` (con clase) o `O(n log n)` (con `sort`). ← Ordenar es más sencillo pero más lento para grandes entradas. TEN O(n2) fuerza bruta (elegir todas las combinaciones) es *astronomicamente* lenta. Silencio
Silencio ** Complejidad del espacio** Silencioso `O(maxValue)` – pequeño porque la moneda cuenta ≤ 104. Silencio `O(1)` espacio auxiliar cuando se utiliza la indexación de `sort`. Mantener todas las permutaciones es infeasible. Silencio
Silencio **Casos Corner** Silencio Ninguno – todas las pilas son positivas. Debe manejar 3 ≤ montones. longitud ≤ 105. Silencioso Sobreflujo o índices negativos si usted mal uso arrays. Silencio
TEN **Readability** TENED código de contador directo. ← El código basado en la clasificación es más corto pero ligeramente menos intuitivo. La mezcla de ambos enfoques en una solución puede ser confusa. Silencio

-...

## 3down Two Two Classic Approaches

## 3.1 Contando-Sort Greedy (O(n) time)

1. Cuenta cuántas pilas contienen cada cantidad de monedas posible.
2. Caminar desde el valor máximo de la moneda, simulando las rondas:
* Alice toma la primera pila de ese valor (esquip).
* **Usted** toma la segunda pila (add to answer).
* Bob toma la tercera pila (esquip).
* Continúe hasta que terminen todas las rondas n/3.

Debido a que el valor máximo de la moneda es sólo 104, la matriz de frecuencia es pequeña.

-...

### 3.2 Sorting Greedy (O(n log n))

1. Ordenar `piles` en **descendiente** orden.
2. Después de ordenar, Alice consigue índices `0,3,6,...`
tienes índices de 1,4,7,...
Bob tiene índices `2,5,8,...`.
3. Sum los elementos en los índices `1,4,7,...` - que es su total.

Esto es posiblemente más limpio, pero un poco más lento.

-...

## 4VIEW⃣ Code – 3 Languages

■ **Tip** – Todos los fragmentos de abajo están listos para pegar en el editor de LeetCode o en su propio IDE.
■ **Nota** – Los métodos 'mantenimiento' son sólo para las pruebas locales rápidas, no se requieren en LeetCode.

#### 4.1 Java

``java
importa java.util. Arrays;

Solución de la clase pública {}
// Solución codictiva contable (O(n) tiempo)
public int maxCoins(int[] piles) {
int n = piles.length;
int max = 0;
para (int v : pilas) si (v > max) max = v;

int[] freq = nuevo int[max + 1];
para (int v : piles) freq[v]++;

int coins = 0; // sus monedas
int rounds = n / 3; // número de trillizos
int turn = 1; // 1 → usted, 0 → skip (Alice o Bob)
int val = max;

mientras que (redondeados ) 0) {
si (freq[val] == 0) {
val; // pasar al siguiente valor más pequeño
continuar;
}

si 1) { // Usted elige
monedas += val;
turn = 0; // siguiente turno es skip
rondas--; // redondo terminado
} { // skip (Alice o Bob)
turn = 1; // siguiente turno será tuyo
}
freq[val]--; // eliminar la pila utilizada
}
devolver monedas;
}

/* -------------------- Prueba local opcional */
public static void main(String[] args) {
Solución s = nueva solución ();
System.out.println(s.maxCoins(new int[]{2,4,1,2,7,8})); // 9
System.out.println(s.maxCoins(new int[]{2,4,5})); // 4
System.out.println(s.maxCoins(new int[]{9,7,6,5,1,2,3,4})); // 18
}
}
`` `

-...

#### 4.2 Python

``python
Solución de clase:
# Solución codictiva contable (O(n) tiempo)
def maxCoins(self, piles: list[int]) - Conf int:
n = len(piles)
max_val = max(piles)

[0] * (max_val + 1)
para v en pilas:
freq[v] += 1

monedas = 0 # tus monedas
rondas = n // 3 # número de trillizos
turn = 1 # 1 - contigo, 0 - patron skip
val = max_val

mientras rondas 0:
si freq[val] == 0:
val -= 1
continuar

si giras == 1:
monedas += val
giro = 0
rondas -= 1
# skip
giro = 1

freq[val] -= 1

devolver monedas

# -------------------- Prueba local opcional --------------------
si __name_ == "__main__":
sol = Solución()
print(sol.maxCoins([2, 4, 1, 2, 8])
print(sol.maxCoins([2, 4, 5])) # 4
print(sol.maxCoins([9, 8, 7, 6, 5, 1, 2, 3, 4])
`` `

-...

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
// Solución codictiva contable (O(n) tiempo)
int maxCoins(vector asignadoint hombro pilas) {
int n = piles.size();
int maxVal = *max_element(piles.begin(), piles.end());

vector asignadoint confianza freq(maxVal + 1, 0);
para (int v : piles) freq[v]++;

int coins = 0; // sus monedas
int rounds = n / 3; // número de trillizos
int turn = 1; // 1 - título usted, 0 - patron skip
int val = máx Val;

mientras que (redondeados ) 0) {
si (!freq[val]) { // no pila de este valor
-val;
continuar;
}

si 1) { // Usted elige
monedas += val;
giro = 0;
rondas... // redondas
} { // skip (Alice o Bob)
turn = 1;
}
--freq[val]; // utilizar una pila
}
devolver monedas;
}
};

/* -------------------- Prueba local opcional */
int main() {}
Solución s;
cout se realizó s.maxCoins({2,4,1,2,7,8})
cout se realizó s.maxCoins({2,4,5})
cout se realizó s.maxCoins({9,8,7,6,5,1,2,3,4})
retorno 0;
}
`` `

■ Si prefieres la versión ** surtido**, simplemente remplaza el cuerpo de cada método con la siguiente línea (Python) o el truco "Arrays.sort" (Java/C++). La complejidad del tiempo caerá a `O(n log n)`, pero el uso de la memoria permanecerá `O(1)`.

-...

## 5down Por qué este problema importa para su búsqueda de empleo

1. **Entrevista clásica Pregunta** – Muchos reclutadores técnicos utilizan LeetCode 1561 como prueba de litmus para *griedy* y * surtido*.
2. ** Modelo mental claro** – Demuestra tu capacidad para *translatar un proceso del mundo real* (tres personas que recogen pilas) en un algoritmo formal.
3. **Pensamiento eficiente** – Muestras que puedes ver cuando un truco de contador golpea a un tipo ingenuo.
4. **Language‐agnostic** – Proporcionar código de trabajo en Java, Python y C++ demuestra que puedes adaptarte a la pila que usa tu futuro empleador.
5. **Blog‐Ready** – Escribir un post limpio y fácil de SEO (como éste) demuestra * habilidades de comunicación* – la segunda habilidad de entrevista más importante después de la codificación.

-...

## 6Ω⃣ SEO‐Friendly Take-away

**Keywords** (para tu blog, Linked En el artículo, o sitio web personal:
- LeetCode 1561**
- * Número máximo de monedas que puede obtener*
- *Turbio de grano*
- *Counting sort*
- *Sortingvariy*
*Preguntas de codificación revisadas*
- *Java, Python, C++*
*O(n) LeetCode solutions*
*Preparación técnica de entrevistas*
*Software engineering job interview tips*

**Descripción de los datos** (vea 155 caracteres):
■ "Solve LeetCode 1561 – Número máximo de monedas que puedes conseguir – en Java, Python y C++. Aprende el truco, la complejidad y los consejos de entrevista codiciosos. ”

-...

Lista final para su resumen / cartera

- TENIDO **Problema**: LeetCode 1561 – * Número máximo de monedas que usted puede obtener*
- Llámanos ** Idiomas**: Java, Python, C++
- ✅ **Time**: O(n) counting-sort (≤ 104 valores) o O(n log n) sorteo
- ✅ **Espacio**: O(valor máximo) (tiny) o auxiliar O(1)
- ✅ **Proof**: La selección "segundo más grande" de Greedy es óptima porque Alice siempre toma la mayor.

■ **Listo para impresionar a los reclutadores? #
■ Compartir el código y el artículo en GitHub, enlazarlo en su Enlace En perfil, y mostrarlo durante su próxima entrevista de codificación. ¡Buena suerte! 🚀