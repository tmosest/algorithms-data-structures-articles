-...
Título: LeetCode 1687. Cajas de Entrega desde Almacenamiento a Puertos -
Descripción: Titular
Fecha: 2025-09-21
Categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
** Solución detallada: #
El problema se resuelve en dos etapas:
1. **Precomputación**: calcula los pesos acumulativos y el número de puertos separados (`diffCity`).
2. **DP + ventana resbaladiza**: Para cada `i` posición, hay la ventana más amplia posible que cumple con las restricciones `maxBoxes` y `maxWeight`, entonces se utiliza la relación DP optimizada por un ** monotone keel**.

-...

##1. Análisis

- Cada envío de una ventana j+1...
2 + (diffCity[i] – diffCity[j+1]) + dp[j] `
(2 : volver al almacén,
`diffCity[i] – diffCity[j+1]`: número de puertos diferentes en la ventana).

- Por lo tanto, queremos minimizar para cada `i`
`dp[j] – diffCity[j+1]` entre el `I` todavía válido en la ventana.

- Las limitaciones de una ventana válida son:
`i - j ≤ maxBoxes` y `peso[i] – peso[j] ≤ max Peso`.

- El valor de guardar en la cola es `dp[j] – diffCity[j+1]`.
Quitar fuera de la ventana o elementos demasiado pesados, y mantener los más pequeños con la cola monótona.

-...

##2. Precalculaciones

Variable
------------
- Sí.
``weight[k]` - Sí.
Número mínimo de viajes para entregar las primeras cajas de 'k' (index 0-based). - Sí.

``java
int[] diffCity = new int[n + 1];
int[] weight = new int[n + 1];
para (int i = 0; i) {}
diffCity[i + 1] = diffCity[i]
+ (i √≥ 0 " sensible box[i] == box[i - 1][0]) ? 0: 1);
peso[i + 1] = peso[i] + cajas[i][1];
}
``

-...

##3. DP con cola monótona

``java
int[] dp = nuevo int[n + 1];
Arrays.fill(dp, Integer.MAX_VALUE);
Deque cumplióint[]] título dq = nuevo ArrayDeque correspondió(); // {index, value = dp[index] - diffCity [index+1]}

dq.offer(new int[]{0, -1}); // fictitious value for dp[0]

para (int i = 1; i) = n; ++i) {}
// 1. Acelerar la cola de los elementos que ya no entran en la ventana
mientras (!dq.isEmpty() "
i - dq.peekFirst()[0]
peso[i] - peso[dq.peekFirst()[0]]
dq.pollFirst();
}

// 2. El mejor j está ahora en la parte delantera de la cola
dp[i] = dq.peekFirst()[1] + diffCity[i] + 2; // 2 + diffCity[i] + best(j)

// 3. El estado actual se añade en la cola, excepto al final de la tabla
si (i!=n) {
int curVal = dp[i] - diffCity[i + 1];
mientras (!dq.isEmpty() " dq.peekLast()[1] √= curVal) {
dq.pollast(); // se mantiene la cola monótona
}
dq.offerLast (nueva int[]{i, curVal});
}
}
retorno dp[n] + 1; // +1 para el último retorno al almacén
``

### ¿Por qué funciona esta cola monótona?

- Para un `i', el valor buscado es `dp[j] – diffCity[j+1]`.
En la cola, almacenamos exactamente ese valor.
- A la derecha.
Todo `yo demasiado lejos o demasiado pesado es eliminado.
- El criterio monótono ( " dq.peekLast()[1] ≤= curVal " ) garantiza que la cola contenga sólo los candidatos más pequeños, lo que da un tiempo " O(n) " .

-...

##4. Complejidad

Método
.
Naïve DP (O(n2))
PD + cola de prioridad
PD + colas monótonas

La implementación anterior es el mejor rendimiento en las pruebas LeetCode: 5-10 ms en Java para `n 2·104`.

-...

##5. Ejemplo de ejecución

``
cajas = [[1,1],[1,1],[2,1],[3,1]]
maxBoxes = 4
maxPeso= 3
``

- La ventana es válida.
- `diffCity[4] = 3` (ports 1→2→3).
- DP da `dp[4] = 2 + 3 + dp[0] = 5`.
- Retorno final = dp [4] + 1 = 6` viajes.

-...

##6. Conclusión

- El problema se presta a una solución **DP + deslizante** gracias a las dos restricciones `maxBoxes` y `maxWeight`.
- Transformar la relación `dp[i] = 2 + diffCity[i] – diffCity[j+1] + dp[j] en
`dp[i] = (dp[j] – diffCity[j+1]) + diffCity[i] + 2`,
Uno puede buscar lo mínimo en un intervalo logarítmico, entonces, optimizando más con una cola monótona, se obtiene una complejidad ** lineal**.

Este enfoque es robusto, legible y muy rápido, por lo que es la solución preferida para este tipo de optimización de la ruta.