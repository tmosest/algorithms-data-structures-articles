-...
Título: LeetCode 464. ¿Puedo ganar?
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🧩 LeetCode 464 – “Puedo ganar”
**Problema** Silencio**
-... Silencio...
[LeetCode 464 – Can I Win](https://leetcode.com/problems/can-i-win/) ¦ Medium Silencio `Dynamic Programming`, `Bitmask`, `Game Theory`, `Backtracking `

-...

Problema Recap

Dos jugadores toman turnos eligiendo un número de `1 ... maxChoosableInteger`.
Números **No se puede reutilizar** – una vez que se elige un número se ha ido.
Añaden el número elegido a un total de funcionamiento.
El jugador que primero gana el total **≥Total**.

Regrese 'verdad' si el primer jugador puede forzar una victoria, de lo contrario 'false'.
Ambos jugadores juegan de forma óptima.

**Constraints* *

`` `
1 ≤ maxChoosableInteger ≤ 20
0 ≤ total ≤ 300
`` `

Debido a que `maxChoosableInteger ≤ 20` podemos codificar el estado de “qué números todavía están disponibles” con una máscara de 20 bits – perfecto para una solución DP-memoization.

-...

## 🔍 High‐Level Idea

1. *Salida total*
* Si `desiredTotal' = 0` → el primer jugador gana inmediatamente.
* Si la suma de todos los números se hizo `desiredTotal` → imposible alcanzar el objetivo → volver `false`.

2. **Recursive Backtracking + Memoization**
* Representar el conjunto de números disponibles con un bitmask `mask`.
* Por cada número `i' que sigue libre (bit `i` is 0):
* If picking `i` wins immediately ( ' i ' il restTotal ' ), return `true`.
* De lo contrario, simular elegir `i`, restar del total restante, y **recursivamente** preguntar si el jugador *next* puede ganar con la nueva máscara.
* Si el jugador *next* **no puede** ganar, el jugador actual puede ganar – devolver `true`.
* Si ninguna opción conduce a una victoria, memoizar y devolver `false`.

3. *La complejidad*
* **Espacio estatal**: en la mayoría de `2^maxChoosableInteger` máscaras (`≤ 1,048,576`).
* **Tiempo**: `O(2^n * n)` en el peor caso (cada máscara explora todos los números restantes).
* **Espacio**: `O(2^n)` para la tabla de memo + la pila de recursión (`≤ 20` profundidad).

-...

## 📄 Code Implementations

A continuación se presentan soluciones limpias de autodocumentación en **Java**, **Python**, y **C+**.
Cada uno utiliza el mismo patrón recursivo + memoización.

-...

## Java

``java
importa java.util. HashMap;
importa java.util. Mapa;

Solución de la clase pública {}
// Mapa de la Memoización: máscara - confianza canFirstPlayerWin
mapa privado realizadoInteger, Boolean ratio memo = nuevo HashMap garantizado();

canIWin(int maxChoosableInteger, int wishTotal) {
// Cheques de cordura rápido
si (desiredTotal 0 = 0) retornan verdaderos;
int maxSum = (maxChoosableInteger * (maxChoosableInteger + 1)) / 2;
si (máximo 0 = total) devuelve falso;

retorno canWin(0, deseadoTotal, maxChoosableInteger);
}

*
* @param máscara Bitmask de números ya elegidos.
* @param remaining Cuánto falta para llegar a desearTotal.
* @param maxChoosable El entero máximo que se puede elegir.
* @return true si el jugador actual puede forzar una victoria.
*/
booleano privadoWin(enmascarado, int restante, int maxChoosable) {}
// Memo lookup
si (memo.containsKey(mask))) devuelve memo.get(mask);

para (int num = 1; num <= maxChoosable; num++) {}
int bit = 1 " 0 " (num - 1);
si (mask) != 0) continuar; // ya utilizado

// Si podemos ganar inmediatamente eligiendo este número
si (num не= restante) {
memo.put(mask, true);
retorno verdadero;
}

// Intenta elegir este número y deja que el oponente juegue
int newMask = máscara ¦
oponente booleano Gana = canWin(newMask, remaining - num, maxChoosable);

// Si el adversario pierde, el jugador actual gana
si (!opponentWins) {}
memo.put(mask, true);
retorno verdadero;
}
}

// No hay movimiento ganador encontrado
memo.put(mask, false);
devolver falso;
}
}
`` `

-...

## Python

``python
Solución de clase:
def __init__(self):
automemo = {}

def canIWin(self, maxChoosableInteger: int, wantedTotal: int) - título Bool:
# Casos de borde
si desea Total 0 0
Retorno
si (maxChoosableInteger * (maxChoosableInteger + 1)) // 2 se ha buscadoTotal:
Retorno Falso

volver a sí mismo._dfs(0, deseadoTotal, maxChoosableInteger)

def _dfs(self, mask: int, remaining: int, max_num: int) - título Bool:
# Memo lookup
si máscara en sí mismo. Memo:
Vuélvete. memo[mask]

para num en rango(1, max_num + 1):
bit = 1 > > (num - 1)
si mascara >
continuar # ya elegido #

# Win immediately
si num >= restante:
self.memo[mask] = True
Retorno

Deja que el oponente juegue
si no auto._dfs(mask tención bit, remaining - num, max_num):
self.memo[mask] = True
Retorno

# Sin movimiento ganador #
self.memo[mask] = False
Retorno Falso
`` `

-...

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
unordered_map madeint, bool contactos memo;

bool canIWin(int maxChoosableInteger, int wishTotal) {
// Salidas tempranas
si (desiredTotal 0 = 0) retornan verdaderos;
int maxSum = (maxChoosableInteger * (maxChoosableInteger + 1)) / 2;
si (máximo 0 = total) devuelve falso;

dfs(0, deseadoTotal, maxChoosableInteger);
}

privado:
bool dfs(mascarada, int restante, int maxNum) {
si (memo.count(mask)) devuelve memo[mask];

para (int num = 1; num 0 = maxNum; ++num) {}
int bit = 1 " 0 " (num - 1);
si (mask > bit) continuar; // ya utilizado

si (num >= restante) { // ganar inmediatamente
memo[mask] = verdadero;
retorno verdadero;
}

// El turno del Opponent
si (!dfs(mask peru bit, remaining - num, maxNum)) {}
memo[mask] = verdadero;
retorno verdadero;
}
}

memo[mask] = falso;
devolver falso;
}
};
`` `

-...

## 📚 Blog Artículo – ¿Puedo ganar? Dominar LeetCode 464 con DP & Bitmask

■ **SEO Palabras clave**: LeetCode 464, ¿Puedo ganar, programación dinámica, bitmask, teoría del juego, entrevista de codificación, entrevista de algoritmo, Java, Python, C+++.

-...

#### ## 1down⃣ El problema en una nuezquela

■ *“Puedo ganar”* es un problema clásico de juego imparcial. Dos jugadores eligen un número único cada turno, añadiéndolo a un total de funcionamiento. El primero en alcanzar o superar las ganancias totales deseadas. ¿El desafío? Determinar si el primer jugador puede forzar una victoria dado ambos jugar de forma óptima.

Es un ejemplo perfecto de *teoría del juego* combinado con *programación dinamica* y *bitmask* técnicas—skills a los entrevistadores les encanta.

-...

#### 2down⃣ ¿Por qué este problema choca (bueno)

- **Tamaño de entrada pequeña** – `maxChoosableInteger ≤ 20` nos permite explorar todos los estados del juego con una máscara de 20 bits.
- **Determinista** – Sin azar; podemos razonar sobre el camino óptimo.
- **Línea DP** – Cada estado puede ser memoizado: “¿El jugador actual gana de este conjunto de números restantes? ”
- **Extensible** – El mismo patrón se aplica a otros juegos “tomadas” (por ejemplo, variantes de Nim).

-...

#### 3down⃣ Los Pitfalls (Bad)

1. **Recuperación Infinita** – Sin la memoización se soplará la pila.
2. ** Explosión Estatal** – La enumeración ingenua (por ejemplo, lista todas las permutaciones) es exponencial e imposible para `maxChoosableInteger = 20`.
3. **Off‐by‐One Errores** – Off‐by-one en posiciones de bits (`1 se indica (num-1)`) es un error común.
4. ** Casos de Edge** – Olvidando los Total 0` atajo o la suma de comprobación conduce a respuestas incorrectas en pruebas triviales.

-...

#### 4down⃣ El “Ugly” – Una lista de verificación de depuración rápida

← Temas Silenciosos Silenciosos
Silencio--------...
Silencio Wrong memo key tención La misma máscara se reutiliza incorrectamente ← Utilizar `unordered_map wonint, bool confía` o `Map Haga clic enInteger, Boolean prenda` Silencio
TENIDO TLE en el peor de los casos TENENCIA Demasiados llamadas recursivas Silencio Añadir salida anticipada: si `num >= remaining` return `true` immediately TEN
Silencio Cambio de bits equivocados ← Off‐by-one bit TENCIÓN Verificar con pequeños ejemplos (por ejemplo, max=3, pick=1 - título=1) TEN
← Sobreflujo de Stack 1000 TENCIÓN La profundidad es ≤ 20, pero la seguridad con el DP iterativo si es necesario

-...

### 5down⃣ Step‐by‐Step Walkthrough (El Algoritmo)

1. ** Condiciones de base**
* `desiredTotal 0` → El primer jugador gana al instante.
* Sum of `1 ... maxChoosableInteger IdentificadoTotal` → impossible, return `false`.

2. **Ayudante recursivo**
* Números de parámetro `mask` usados*.
* Encima sobre todo el `num` de `1` a `maxChoosableInteger`.
* Skip if already used (`mask ' bit`).
* ** Inmediata Ganancia**: si `num √= rest` → el jugador actual gana.
* **Grupo de los participantes**: `si !canWin(newMask, remaining - num)` → ganamos.

3. **Memoizar " Return** – Guardar el resultado de cada máscara para evitar la recomputación.

-...

#### 6VIEW⃣ Complexity Analysis

- **Hora**: `O(2^n * n)` (caso peor), donde `n = maxChoosableInteger`.
*Reason*: Hay máscaras de 2^n; para cada una podemos intentar hasta 'n' números.
- **Espacio**: `O(2^n)` para la mesa de memo + `O(n)` profundidad de recursión.

Con 'n ≤ 20', esto es cómodamente rápido para todas las pruebas de LeetCode.

-...

### 7 carreras “¿Y si quiero una solución más rápida? ”

Para este problema específico, la solución DP + bitmask ya es óptima en la práctica.
Si te encuentras más grande `maxChoosableInteger`, necesitarás un enfoque diferente (por ejemplo, Sprague-Grundy números o análisis combinatorio), pero los que exceden las restricciones de LeetCode 464.

-...

### 8 Cambios en la entrevista—Ley Tips

TENIDO TENDIDO ANTERIOR Por qué importa
Silencio...
Silencio **Explicar salidas tempranas** Silencio Muestra que te preocupan los casos de rendimiento y de borde. Silencio
Silencio **Derrame la máscara** ← Visualizar el estado de 20 bits ayuda a los entrevistadores a ver su proceso de pensamiento. Silencio
Silencio **Hablar sobre la recursión vs iteración** Silencio Entrevistas les encanta ver que consideran la seguridad de la pila. Silencio
Silencio **Mention memoization map** Silencio Destaca su conocimiento de caché para prevenir el trabajo repetido. Silencio
Silencio **Mejor con números pequeños** Silencio Demuestra la habilidad y la comprensión del algoritmo. Silencio

-...

Pensamientos finales

“Puedo ganar” es un problema de libro de texto que combina la teoría del juego** con ** programación dinamica** y ** manipulación de bits**. Dominar no sólo te da una solución ganadora para LeetCode, sino que también te equipa con un patrón que verás en muchos puzzles de entrevista.

- **Bien**: Pequeño espacio estatal, determinista, limpio DP.
- **Bad**: Fácil de deslizar en el índice de bits, casos de base perdidos.
- **Ugly**: Recursive TLE si olvidas la memoización.

Utilice los fragmentos de código arriba (Java, Python, C++) como una referencia lista a paso. Luego, la práctica explicando el algoritmo en voz alta: su capacidad de articular el razonamiento es tan valiosa como el código mismo.

¡Feliz codificación, y que tu primer jugador siempre gane! 🚀

-...

**Listo para asar su próxima entrevista? * *
Siga practicando, lea soluciones editoriales y comparta su propio análisis “Puedo ganar” en su blog o GitHub. A los clientes les encanta ver soluciones limpias y explicables, especialmente cuando usted demuestra tanto el *why* como el *how* detrás de su código.