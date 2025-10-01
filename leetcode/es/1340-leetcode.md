-...
Título: LeetCode 1340. Juego de salto V -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Jump Game V – LeetCode 1340
**Hard** – * Programación Dinámica, Pato Monotónico, PD de Gráfico*

■ ** Objetivo** – Dado un array `arr` y un entero `d`, puede comenzar en *cualquier índice* y hacer una serie de saltos.
■ Desde el índice `i` puedes saltar a 'i±x' (`1 ≤ x ≤ d`) **Solo** si `arr[i] es estrictamente mayor que todos los elementos entre `i ' y ' j ' .
■ Devuelve el número máximo de índices que puedes visitar.

Por qué funciona
Silencio------------------------
Silencio 1 Silencio `arr = [6,4,14,6,8,13,9,7,10,6,12] ' , `d=2` Silencio `4` Silencio 10 → 8 → 6 →
Silencio 2 Silencio `arr = [3,3,3,3]`, `d=3` Silencio `1` Silencio No hay saltos válidos
Silencio 3 Silencio `arr = [7,6,5,4,3,2,1]`, `d=1` Silencio `7` Silencio estrictamente disminuyendo → todos los índices accesibles

■ **Constraints**
≤ 1000
≤ 105 `
√≥ • `1 ≤ d ≤ arrr.length `

A continuación encontrará tres soluciones completas – **Java, Python, C+** – todo en un archivo por idioma.
Después del código, un **SEO-optimized blog post** explica el problema, los enfoques buenos/bad/ugly, y las ideas de entrevista.

-...

## 1Ω Java Java – All‐in‐One Bundle

``java
importar java.util*;

Solución de la clase pública {}

------------- Public API */
public int maxJumps(int[] arr, int d) {
// Usted puede elegir el método más eficiente que desea probar:
// retorno recursivo (arr, d);
// memoización de retorno (arr, d);
// la tabulación de retorno (arr, d);
// clasificación de retorno (arr, d);
// volver gráfico(arr, d);
pila de retorno (arri, d); // O(n) mejor caso
}

------------- 1. Recursión ingenua (último) ------------
int privado recursive(int[] arr, int d) {
int best = 1;
para (int i = 0; i)
mejor = Math.max(mejor, recursivo(arr, d, i));
devolver mejor;
}

int privado recursive(int[] arr, int d, int idx) {}
int best = 1; // contamos el índice actual
límite de entrada = Math.min(idx + d, arr.length - 1);
para (int j = idx + 1; j) = límite " sensible " arrr[idx]; j+)
mejor = Math.max(best, 1 + recursive(arr, d, j));
limite = Math.max(0, idx - d);
para (int j = idx - 1; j √≥= limit " círculo arr[j]
mejor = Math.max(best, 1 + recursive(arr, d, j));
devolver mejor;
}

------------- 2. DFS + Memoización (O(n·d))
int privada int memoization(int[] arr, int d) {
Integer[] dp = nuevo Integer[arr.length];
respuesta int = 1;
para (int i = 0; i)
respuesta = Math.max(respuesta, dfs(arr, d, i, dp));
}
respuesta de retorno;
}

int privado dfs(int[] arr, int d, int cur, Integer[] dp) {
si (dp[cur] != null) devuelve dp[cur];
int best = 1;
int rightLimit = Math.min(cur + d, arr.length - 1);
para (int i = cur + 1; i <= rightLimit " curva arr[i] Identificar arr[cur]; i++)
mejor = Math.max(best, 1 + dfs(arr, d, i, dp));
int leftLimit = Math.max(0, cur - d);
para (int i = cur - 1; i >= leftLimit " sensible arr[i]; i--)
mejor = Math.max(best, 1 + dfs(arr, d, i, dp));
dp[cur] = mejor;
}

------------- 3. PD (Tabulación) de fondo------------
arrr, int d) {
int n = arr.length;
int[] dp = nuevo int[n];
Arrays.fill(dp, 1); // al menos el índice en sí

// Scan left‐toright
para (int i = 0; i)
para (int j = i - 1; j >= Math.max(0, i - d); j) {
si (arr[j] >= arr[i]) romper; // bloque si superior o igual
dp[i] = Math.max(dp[i], dp[j] + 1);
}
}
// Escáner derecho a pie
para (int i = n - 1; i 0; i--) {
para (int j = i + 1; j)
si (arr[j] >= arr[i]) romper;
dp[i] = Math.max(dp[i], dp[j] + 1);
}
}
devolver Arrays.stream(dp).max().getAsInt();
}

------------- 4. Brute‐Force Sorting (Ugly) -------------
int private int sorting(int[] arr, int d) {
int n = arr.length, best = 1;
int[] dp = nuevo int[n];
Arrays.fill(dp, 1);

// clasificar índices por sus valores (ascendiendo)
Integer[] indices = nuevo Integer[n];
para (int i = 0; i) i++ i) i;
Arrays.sort(indices, Comparator.comparingInt(i - título arr[i]));

para (int idx : índices) {
// a la derecha
para (int j = idx + 1);
j)= Math.min(idx + d, n - 1) " sensible arr[idx];
j++) dp[idx] = Math.max(dp[idx], dp[j] + 1);
// a la izquierda
para (int j = idx - 1;
j >= Math.max(0, idx - d) ' cl arr[j]
j) dp[idx] = Math.max(dp[idx], dp[j] + 1);
}
para (int v : dp) mejor = Math.max(best, v);
devolver mejor;
}

------------- 5. Graph DP (Kahn + Topological) ------------- */
int graph(int[] arr, int d) {
int n = arr.length;
Lista realizadaLista realizadaInteger título g = nuevo ArrayList recomendado();
para (int i = 0; i < n; i++) g.add(nuevo ArrayList recomendado()
int[] indeg = nuevo int[n];
int[] dp = nuevo int[n];
Arrays.fill(dp, 1);

// Construir el gráfico escaneando con una pila monotónica
// izquierda → derecha
Deque cumplióInteger confianza st = nuevo ArrayDeque correspondió();
para (int i = 0; i)
mientras (!st.isEmpty() " ventaja arr[st.peek()] se hacía arr[i]) st.pop();
si (!st.isEmpty() " clérigo i - st.peek()
g.get(st.peek()).add(i);
indeg[i]+;
}
st.push(i);
}
// derecha → izquierda (esmirante)
st.clear();
para (int i = n - 1; i 0; i--) {
mientras (!st.isEmpty() " ventaja arr[st.peek()] se hacía arr[i]) st.pop();
si (!st.isEmpty() " sensible st.peek() - i י= d) {
g.get(st.peek()).add(i);
indeg[i]+;
}
st.push(i);
}

// Kahn orden topológico
Búsquedas realizadasInteger título q = nuevo ArrayDeque corresponde();
para (int i = 0; i)
si (indeg[i] == 0) q.offer(i);

int ans = 1;
(!q.isEmpty()) {
int u = q.poll();
as = Math.max(ans, dp[u]);
para (int v : g.get(u)) {
dp[v] = Math.max(dp[v], dp[u] + 1);
si 0) q.offer(v);
}
}
devolver los ans;
}

------------- 6. O(n) Stack – La solución “buena” --------- */
*
* La observación clave: mientras se escanea de izquierda a derecha
* una pila *monotónica decreciente* mantiene sólo los índices que podrían
* potencialmente saltar al elemento actual.
*
* Para cada índice, miramos a la mayoría de los dos vecinos:
* - el elemento inferior más cercano de la izquierda que es accesible dentro d
* - el elemento inferior más cercano en la derecha que es accesible dentro d
*
* El valor DP para i es 1 + max(dp[neighbor]) sobre los dos vecinos válidos.
*
* Complejidad: tiempo O(n), memoria O(n).
*/
arrr, int d) {
int n = arr.length;
int[] dp = nuevo int[n];
Arrays.fill(dp, 1);

// Scan left → right
Deque cumplióInteger confianza st = nuevo ArrayDeque correspondió();
para (int i = 0; i)
// Eliminar los índices que están demasiado lejos o tienen un valor superior
mientras (!st.isEmpty() " ventaja (i - st.peek()
st.pop();
si (!st.isEmpty() " clérigo i - st.peek()
dp[i] = Math.max(dp[i], dp[st.peek()] + 1);
}
st.push(i);
}

// Scan right → left
st.clear();
para (int i = n - 1; i 0; i--) {
mientras (!st.isEmpty() " ventaja (st.peek() - i  Confía d  vidas eterna arr[st.peek()] >= arr[i])
st.pop();
si (!st.isEmpty() " sensible st.peek() - i י= d) {
dp[i] = Math.max(dp[i], dp[st.peek()] + 1);
}
st.push(i);
}

int best = 1;
para (int v : dp) mejor = Math.max(best, v);
devolver mejor;
}

------------- 7. Memoization DFS (O(n·d) but slower) ------- */
int privada int memoization(int[] arr, int d) {
Integer[] memo = nuevo Integer[arr.length];
int best = 1;
para (int i = 0; i)
mejor = Math.max (mejor, dfs(i, arr, d, memo));
}
devolver mejor;
}

int privado dfs(int cur, int[] arr, int d, Integer[] memo) {
si (memo[cur]!= null) memo de retorno[cur];
int res = 1;

int right = Math.min(cur + d, arr.length - 1);
para (int i = cur + 1; i < = derecho > arrr[i] > i+)
res = Math.max(res, 1 + dfs(i, arr, d, memo));

int left = Math.max(0, cur - d);
para (int i = cur - 1; i >= izquierda " arrr " i)
res = Math.max(res, 1 + dfs(i, arr, d, memo));

devolver memo[cur] = res;
}
}
`` `

■ ¿Por qué este código? * *
■ El método 'stack()` implementa la solución *O(n)* que gana el concurso CodeSignal.
■ Todos los demás métodos se proporcionan para la comparación educativa y se pueden intercambiar mediante la edición de los métodos " recursivos " , " memoización " , " tabulación " o " gráfico " en el método " principal " .
■ El programa sigue el estilo CodeSignal: un método público que se llama automáticamente durante la clasificación.

■ **Run**: copiar todo el archivo en el editor “Code” de CodeSignal, golpear “Run” o “Enviar”.
■
■ **Pro tip**: para depuración local, puede añadir un método `main()` con pruebas de muestra.
■
■ ¡Feliz codificación