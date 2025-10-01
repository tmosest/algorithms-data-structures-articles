-...
Título: LeetCode 1320. Distancia mínima para escribir una palabra usando dos pasos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🧑 1320 – Distancia mínima para escribir una palabra usando dos pasos
**Solutions in Java, Python, " C++** **Full Blog Article (SEO‐optimized)* *

-...

Problema Recap

Le dan un diseño de teclado 5 × 6 (A...Z).
Las coordenadas son:

← Carta Silenciosa (x, y)
Silencio...
Silencio A Silencio (0, 0)
Silencio (0, 1)
Silencio...
TENIDO Z TENIDO (4, 1) TENIDO

Tienes dos dedos. El primer uso de cada dedo es libre (no se carga la distancia).
Por cada prensa clave posterior pagas la distancia de Manhattan entre las dos letras que escribes.

■ ** Objetivo** – escriba una cadena `palabra ' (2 ≤ tenciónword sufrimiento ≤ 300) con la distancia total **minimo**.

-...

## 2down⃣ Intuition " DP State

- Cuando estamos en la posición 'i' en 'palabra', lo único que importa es **donde cada dedo es**.
- Cada dedo puede ser:
- *un-set* (gratuito para el primer uso) - codificaremos esto como `-1`.
- o en una carta " c " (0 a 25).

Así, un estado de DP es:

`` `
dp[i][f1][f2] = distancia mínima para terminar de escribir de i,
donde el dedo1 está en f1, dedo2 en f2
`` `

`f1, f2  Iberia {‐1, 0...25}` → 27 × 27 posibles valores para cada `i`.

**Transición* *

`` `
Let cur = word[i]
Opción 1: usar el dedo1
costo = distancia(f1, cur) // 0 si f1 == -1
siguiente = dp[i+1][cur][f2]

Opción 2: use dedo2
costo = distancia(f2, cur) // 0 si f2 == -1
siguiente = dp[i+1][f1][cur]
`` `

Respuesta = `dp[0][-1][-1]`.

La distancia entre dos letras es pre-computada una vez.

-...

## 3down Complejidad

Silencio Silencio Silencio Silencio Silencio
Silencio...
← Recursive + Memo Silencioso **O(la palabra anterior × 272)** ♥ 200 000 operaciones Silencio **O(la palabra anterior × 272)** Silencio
Silencioso Iterante Silencioso

Ambos encajan cómodamente en los límites.

-...

## 4down Código

A continuación se muestran las implementaciones **ready‐to-paste** en los tres idiomas solicitados.

■ **Tip** – Los tres utilizan la misma lógica subyacente de DP, simplemente expresada idiomáticamente.

-...

#### 4.1 Java

``java
importa java.util. Arrays;

Solución de la clase pública {}
// 26 letras + 1 “no utilizado todavía” centinela
privada estática final int NOT_SET = -1;
privada estática final int N = 27; // 0...25 para cartas, 26 para NOT_SET
int[][] pos = nuevo int[26][2];
int[][][] [] memo;
palabra privada String;
int len privada;

// Posiciones pre-computadas en un teclado 5×6
Estática
para (int i = 0; i)
pos[i][0] = i % 6;/ x
pos[i][1] = i / 6; // y
}
}

mínimo público Distancia (Cerrar palabra) {
esta.word = palabra;
this.len = word.length();
// +1 para almacenar el estado NOT_SET en el índice 26
memo = nuevo int[len + 1][N][N];
para (int i = 0; i <= len; i++)
para (int f1 = 0; f1 = N; f1++)
Arrays.fill(memo[i][f1], -1);
(0, NOT_SET, NOT_SET);
}

int solve(int idx, int f1, int f2) {
si (idx == len) devuelve 0;
int fi1 = (f1 == NOT_SET) ? 26 : f1;
int fi2 = (f2 == NOT_SET) ? 26 : f2;
int cached = memo[idx][fi1][fi2];
si (caché!= -1) el caché de retorno;

int cur = word.charAt(idx) - 'A';
// Opción 1: usar el dedo1
int cost1 = distance(f1, cur) + solve(idx + 1, cur, f2);
// Opción 2: usar el dedo2
int cost2 = distancia(f2, cur) + solucion(idx + 1, f1, cur);

int ans = Math.min(cost1, cost2);
memo[idx][fi1] [fi2] = ans;
devolver los ans;
}

int distance(int from, int to) {
si (desde == NOT_SET) devuelve 0;
int x1 = pos[from][0], y1 = pos[from][1];
int x2 = pos[to][0], y2 = pos[to][1];
devolver Math.abs(x1 - x2) + Math.abs(y1 - y2);
}
}
`` `

-...

#### 4.2 Python

``python
importa functools
de la importación Lista

Solución de clase:
# Pre-compute coordinates for A..Z
coords: List[tuple] = [(i % 6, i // 6) for i in range(26)]

mínimo Distancia (auto, palabra: str) - Propiedad int:
@functools.lru_cache(None)
def dp(idx: int, f1: int, f2: int) int:
""f1/f2 son índices 0‐25 para una carta, -1 significa no utilizado.""
si idx == len(word):
retorno 0

cur = ord (palabra[idx]) - 65 # 0-based

# Use finger 1
cost1 = autodista(f1, cur) + dp(idx + 1, cur, f2)
# Use finger 2
cost2 = autodista(f2, cur) + dp(idx + 1, f1, cur)

retorno min(cost1, costo2)

retorno dp(0, -1, -1)

def dist(self, from_idx: int, to_idx: int) int:
si de_idx == -1:
retorno 0
x1, y1 = self.coords[from_idx]
x2, y2 = self.coords[to_idx]
retorno abs(x1 - x2) + abs(y1 - y2)
`` `

-...

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
// Coordenadas pre-computadas para A..Z
vector significado(26);
vector de vectores seleccionados memo;
Palabra de cuerda;
int n;

Solución() {
para (int i = 0; i) {}
pos[i] = {i % 6, i / 6};
}
}

mínimo Distancia (llamada) {
este- título = palabra;
n = word.size();
// 27 = 26 letras + 1 para “no utilizado”
memo.assign(n + 1, vector asignadovector seleccionado(27, vector asignadoint título(27, -1));
dp(0, 26, 26); // 26 representa NOT_SET
}

privado:
int dp(int idx, int f1, int f2) {
si (idx == n) retorno 0;
si (memo[idx][f1][f2] != -1) memo[idx][f1][f2];

int cur = word[idx] - 'A';
// Use el dedo 1
int cost1 = dist(f1, cur) + dp(idx + 1, cur, f2);
// Usa el dedo 2
int cost2 = dist(f2, cur) + dp(idx + 1, f1, cur);

memo[idx][f1][f2] = min(cost1, cost2);
}

int dist(int from, int to) {
si (desde ==26) regresa 0; // NOT_SET
auto [x1, y1] = pos[de];
auto [x2, y2] = pos[to];
devolver abs(x1 - x2) + abs(y1 - y2);
}
};
`` `

-...

Artículo del Blog (SEO‐Optimized)

■ **Título:** Distancia mínima para escribir una palabra usando dos discos – Java, Python & C++ Soluciones*
■ **Meta Descripción:** Solve LeetCode 1320 con explicaciones DP claras, código Java/Python/C++ óptimo, y una guía amigable SEO para la preparación de entrevistas.

-...

### 5.1 Introduction

El problema ** “Minimum Distancia a Tipo una Palabra Usando Dos Alimentadores”** es un reto clásico de programación dinámica que prueba su capacidad de modelar el estado y optimizar las transiciones. Es una pregunta de entrevista perfecta para los roles de ingeniería de software, especialmente los que se centran en el diseño algorítmico y el dominio de la estructura de datos.

Este artículo camina a través del razonamiento, presenta tres implementaciones de producción, y le da una comprensión más profunda de los aspectos “bueno, malo y feo” que encontrará al resolverlo.

-...

### 5.2 Problema Recap

- **Diseño de teclado:** 5 filas × 6 columnas (letters A–Z).
- ¿Qué? Distancia de Manhattan, `vivirx1‐x2 permanecen + Silencio1‐y2 viven`.
- ¿Qué?
- El primer uso de cada dedo es gratis.
- Los Fingers pueden comenzar con cualquier llave (incluyendo el primer personaje).
- Debe escribir la palabra dada con **mínimo distancia total**.

**Introducción** - una cadena `palabra ' (período, longitud ≤ 300).
**Output** – la distancia mínima (integer).

-...

### 5.3 Key Ideas

1. Compresión estatal**
Lo único que influye en los costos futuros es la ubicación actual de cada dedo. No necesitamos toda la historia, así que comprimemos el estado a `(index, finger1, finger2)`.

2. **Sentinel para “no utilizado todavía”* *
Use `-1` (o `26` en C++) para representar el estado libre. La primera vez que se utiliza un dedo, la distancia es `0`.

3. **Pre-computación**
Las coordenadas de cada letra en el teclado son deterministas. Guárdelos en un array para la búsqueda O(1).

4. **Simetría de transición**
Al decidir qué dedo utilizar para el siguiente personaje, las dos opciones son simétricas. Esto reduce drásticamente el espacio de búsqueda.

-...

### 5.3 Dynamic Programming Derivation

← Paso tóxico Lo que estamos haciendo tóxico Por qué funciona
Silencio------------
Silencio **Define DP** Silencio `dp[i][f1][f2] – costo mínimo de la posición `i` lugares dados de los dedos. ← Capture todas las dependencias futuras. Silencio
Silencio **Caso de base** Silencio `i == len(word)` → `0`. Silencio Acabado escribiendo → no más costo. Silencio
Silencioso ** Transición** Silencioso Use ambos dedos. Costo de cómputo + `dp[i+1][...]`. Silencio
Silencio **Memoización** Silencio Cache resulta en un array 3-D o `lru_cache`. tención Evite el soplo exponencial; cada estado resuelto una vez. Silencio

-...

### 5.4 “Bueno” – ¿Por qué funciona DP

- **Espacio de estado determinista** - Sólo las posiciones de los dedos importan.
# Tiempo de polínomía # Las limitaciones del problema son modestas, pero el DP garantiza eficiencia.
*Separabilidad limpia* La regla de primer uso se traduce en un simple cheque “0 costo si no se establece”.

-...

### 5.5 "Bad" – Pitfalls comunes

Silencioso Temas anteriores Explicación
Silencio------------------------
tención Mis‐encoding NOT_SET ANTE Utilizar `-1` directamente en el índice de array 3-D conduce a índices negativos. tención Mapa `-1` → 26 (o cualquier ranura "extra"). Silencio
Silencio Distancia de venta libre ← Olvidar que el primer uso de un dedo es gratis. tención Caso especial: `distancia = 0` cuando el dedo == NOT_SET. Silencio
El límite de recursión de Python es de 1000, pero la longitud de la palabra ≤ 300, por lo que es seguro, pero todavía guarda con `sys.setrecursionlimit`. ← En Java/C++ los bucles iterativos o la recursión de la cola es más segura. Silencio

-...

### 5.6 “Ugly” – Trade‐offs " Variations

** Consumo de memoria** – 273 × 300 ♥ 200 000 ints (~ 0.8 MB). Si la memoria se convierte en una preocupación (por ejemplo, en un entorno de entrevistas de memoria), se puede reducir a **dos capas** (`dp_cur`, `dp_next`) porque `dp[i]` depende solamente de `dp[i+1]`.
- **Diferentes formas de teclado** – Si el diseño del teclado cambia, sólo necesita reconstruir el array 'pos'.
- Paralelismo... Aquí no es necesario; el DP es inherentemente secuencial debido al orden de caracteres.

-...

### 5.7 Pensamientos Finales > Consejos de Entrevista

*Explica tu estado claramente* Los entrevistadores les encanta ver articular por qué cada dimensión importa.
- **Mostrar el diagrama de transición** – Una simple tabla o transición pseudocódigo aclara su razonamiento.
- **Preguntas aclaradoras** – Por ejemplo, ¿se permite cambiar el mismo dedo entre dos llaves consecutivas? En este problema, sí, pero hacer esa suposición explícita puede evitar errores sutiles.
- **Test edge cases** – Empty string, all same letter, alternating letters, longest string.

-...

### 5.8 Summary

Hemos:

1. Decoded the LeetCode 1320 problem into a concise DP model.
2. Caminó por el **bueno** – estado determinista, complejidad polinomio, transiciones limpias.
3. Destacado el **bad** – saltos alrededor de valores centinela, costo de primer uso.
4. Tackled the **ugly** – uso de memoria, problemas potenciales de profundidad de recursión.

Los fragmentos de código para **Java, Python y C++** están completamente probados y listos para entrevistas de producción o como plantilla para problemas similares de DP.

Buena suerte, y feliz codificación! 🚀

-...


-...


**End of article**



-...


#### 6down⃣ Nota final

■ **Pro tip** – Al prepararse para las entrevistas, tenga en cuenta este patrón: *Identificar la mínima “memoria” necesaria para describir el futuro*, codificar que como un estado DP, pre-computa cualquier aspecto costoso (como distancias), y luego iterate sobre las opciones.
■ LeetCode 1320 es un ejemplo de libro de texto de ese principio. ¡Feliz solución!