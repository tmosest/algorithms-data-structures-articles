-...
Título: LeetCode 862. Subarray con Sum al menos K -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**LeetCode 862 – Subarray más corto con Sum al menos K* *

*Key Idea*
La suma de un subarray \([i+1, j]\) se puede calcular rápidamente
`pref[j] – pref[i]`, donde `pref` es un array prefix-sum.
Para encontrar el *shortest* tal subarray, mantenemos un **deque monotónico** de índices de prefijo-sum:

* **Front** – da el prefijo más pequeño que podría formar un final de subarray válido en el índice actual.
* **Volver** – descartamos índices cuya suma de prefijo no es menor que la actual, porque no pueden producir un subarray más corto después.

-...

## Algorithm
`` `
1. Build prefix array pref[0...n] (pref[0] = 0).
2. minLen ←
3. Para j = 0 ... n:
• Mientras que deque no está vacío y pref[j] - pref[dq.front()] ≥ k:
minLen ← min(minLen, j - dq.front())
dq.pop_front() // frontal ya no es útil
• Mientras que no está vacío y pref[j] ≤ pref[dq.back()]:
dq.pop_back() // mantener el aumento de las sumas prefijo
• dq.push_back(j)
4. Retorno (minLen == ∞ ? -1 : minLen)
`` `

-...

### Why It Works

* `pref[j] - pref[dq.front()] ≥ k` → subarray `[dq.front()+1 ... j]` tiene suma ≥ k.
Retirarlo desde el frente sólo puede hacer futuros candidatos más largos, por lo que es seguro pop.
* Popping from the back keep only the *minimal* prefix sums at earlier indices, ensuring any later subarray will be at least as short if it starts after one of those indices.

-...

### Complexity
* **Tiempo:** `O(n)` – cada índice entra y deja el deque al máximo una vez.
****Space:* – prefijo array + deque.

-...

**Bottom line:** Utilice un array de suma prefijo junto con un deque monotónico para comprobar y actualizar codictivamente el subarray más corto, alcanzando el tiempo lineal y el espacio.