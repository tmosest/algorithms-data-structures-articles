-...
Título: LeetCode 799. Champagne Tower -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Torre de Champagne - LeetCode 799
**Un problema DP de mediano nivel que impresiona al programa* *

■ **Keywords** – LeetCode, Champagne Tower, programación dinámica, problema de entrevista, Java, Python, C++, algoritmo, entrevista de codificación, entrevista de trabajo, desafío de codificación.

-...

Sinopsis del problema

Sobre el problema LeetCode **799 – Torre de Champagne** se le da una pirámide de gafas:

- La fila 0 tiene 1 vaso, la fila 1 tiene 2 vasos, la fila 99 tiene 100 vasos.
- Cada copa puede contener exactamente una unidad de champán.
- Pones copas en el vaso superior.
- Si un vaso se desborda, el exceso se divide ** uniformemente** entre los dos vasos directamente debajo de él.
- Cualquier cosa que se desborde de la fila inferior se gotea al suelo.

■ ** Objetivo** – Después de que se haya derramado todo el champán, devuélvase lo lleno (0–1) del vaso en `(query_row, query_glass)` Lo es.

■ **Constraints**
" `
■ 0 ≤ ≤ 10^9
■ 0 ≤ query_row
■ 0 ≤ query_glass ≤ query_row
" `

■ *Ejemplo*
> poured = 2, query_row = 1, query_glass = 1 → **0.5**

-...

## 2down Por qué el programador de amor este problema

Silencio Por qué importa
Silencio...
Silencio ** Programación Dinámica (DP)** tención Muestras que puedes modelar un problema de “flujo” del mundo real con DP. Silencio
Silencio **Simulación + Desbordamiento** Silencio Demuestra el manejo cuidadoso de los casos aritméticos y de borde de punto flotante. Silencio
Silencio **Tiempo/Espacio O(r2)** Silencio Aunque las restricciones son pequeñas, todavía muestra una solución óptima. Silencio
Silencio **Language‐agnostic** Silencio Resuelto fácilmente en Java, Python, o C++ – ideal para entrevistas. Silencio

Si puede explicar su solución y presentar códigos limpios y legibles, obtendrá una “amenaza” en cualquier entrevista técnica.

-...

## 3down La Idea Central – Row‐by-Row Simulation

Piense en la torre como ** Triángulo de Pascal** donde cada entrada es la cantidad de champán que llega a esa copa.
El proceso:

1. ** Initialize** `tower[0][0] = poured`.
2. Por cada vaso de la torre [r][c] en la fila `r ' (hasta `query_row`):
- Si `tower[r][c] > 1`, computar el **excess**:
``excess = (tower[r] [c] - 1) / 2.0```
- Añadir ese exceso a las dos copas siguientes:
```tower[r+1][c] += excess` `
```tower[r+1][c+1] += excess`` `
3. Después de la simulación, la respuesta es «min(1.0, tower[query_row][query_glass])».

■ ¿Por qué min(1.0)? #
■ Un vaso nunca puede contener más de una unidad. La simulación puede calcular un valor superior si el flujo entrante es enorme; lo sujetamos a 1.

-...

## 4VIEW⃣ Complexity Analysis

- **Hora** – Visitamos cada vaso hasta 'query_row'.
\[
T = 1 + 2 + \dots + (\text{query_row}+1) = O(\text{query_row}^2)
\]
Con `query_row ≤ 99`, esto es trivial (≤ 5 000 operaciones).

- **Espacio** - Una matriz de 2-D del tamaño `(query_row+1) × (query_row+1) → `O(query_row^2) `
Podemos reducirlo a un array de 1-D de tamaño `query_row+1` si se desea, pero la legibilidad gana aquí.

-...

## 5down Edge‐ Caso “Gotchas”

Silencio Caso Edge Silencio Por qué importa
Silencio...
Silencio **poured = 0** Silencio Todos los vasos permanecen vacíos. Silencio
TEN **query_glass = 0 o query_glass = query_row** TENIDO El vidrio primero/último recibe sólo la mitad del flujo de entrada. Silencio Manejado automáticamente por DP. Silencio
Large poured (109)** Los valores de la sobrefluencia vivieron a ser enormes; use `doble`. Silencio
Silencio **Precisión de punto flotante** Silencio Resultado de retorno con 5 lugares decimales. ← Uso `Math.min(1.0, val)` y formato en consecuencia. Silencio

-...

Implementación - Tres idiomas

### 6.1 Java

``java
Solución de la clase pública {}
champán doble públicoTower(int poured, int query_row, int query_glass) {}
si 0) retorno 0,0;

doble[][] torre = nuevo doble[query_row + 2][query_row + 2];
torre[0] [0] = derramada;

para (int r = 0; r) {}
para (int c = 0; c) {}
doble exceso = (tower[c] - 1.0) / 2.0;
si (excesos 0) {
torre[r + 1][c] += exceso;
torre[r + 1][c + 1] += exceso;
}
}
}

devolver Math.min(1.0, torre[query_row][query_glass]);
}
}
`` `

¿Por qué 2-D? Mantiene el código legible. La matriz es pequeña (≤ 102 × 102).

-...

### 6.2 Python

``python
Solución de clase:
def champagne Tower(self, poured: int, query_row: int, query_glass: int) - título flotante:
si se derrama == 0:
retorno 0,0

# inicializar (query_row+2) filas para facilitar el manejo de índice
torre = [0.0] * (query_row + 2) for _ in range(query_row + 2)]
torre[0][0] = derramada

para r en rango(query_row):
para c en rango(r + 1):
[c] - 1.0) / 2.0
si el exceso 0:
torre[r + 1][c] += exceso
torre[r + 1][c + 1] += exceso

volver min(1.0, torre[query_row][query_glass])
`` `

■ **Python tip** – La comprensión de la lista construye una matriz 2-D limpia.

-...

### 6.3 C++

``cpp
Clase Solución {
public:
champán doble Torre(int poured, int query_row, int query_glass) {}
si 0) retorno 0,0;

vector de vectores torre(query_row + 2,
vector alcanzadodouble(query_row + 2, 0,0));
torre[0] [0] = derramada;

para (int r = 0; r) {}
para (int c = 0; c) {}
doble exceso = (tower[c] - 1.0) / 2.0;
si (excesos 0) {
torre[r + 1][c] += exceso;
torre[r + 1][c + 1] += exceso;
}
}
}

volver min(1.0, torre[query_row][query_glass]);
}
};
`` `

■ **¿Por qué `vector asignadovector hizo doble título ``? #
■ El C++ STL hace una asignación dinámica directa, y el tamaño sigue siendo de 200 × 200.

-...

## 7Ω A Una Variante Unidimensional (Opcional)

Si quieres impresionar a los reclutadores que puedes *optimizar* la memoria, aquí está el truco 1-D (estilo java):

``java
dp = nuevo doble [query_row + 2];
dp[0] = poured;
para (int r = 0; r) {}
para (int c = r; c >= 0; c--) { // iterate back!
doble exceso = (dp[c] - 1.0) / 2.0;
si (excesos 0) {
dp[c] += exceso;
dp[c + 1] += exceso;
}
}
}
devolver Math.min(1.0, dp [query_glass]);
`` `

*Backwards iteration* garantiza que los valores de la fila actual no están sobrescritos antes de ser utilizados.

-...

## 7 carreras Cómo presentar Esto en una entrevista

1. **Declarar las suposiciones** – por ejemplo, “ simularemos fila por fila, sujetando cualquier vidrio a un máximo de 1. ”
2. ** Dibujar un diagrama rápido** – Mostrar una pequeña torre de 3 acres y cómo fluye el desbordamiento.
3. **Explicar la recurrencia del DP** – Reflujo = `(actualmente - Cantidad - 1) / 2`.
4. *Espera una muestra* Utilice el array 2-D para ilustrar los cálculos.
5. ** Complejidad de la mención** – O(r2) tiempo, espacio O(r2); trivial para r = 100.
6. **Hablar sobre los casos de borde** – salida temprana para `poured == 0`, precisión de punto flotante, aferrarse a 1.

■ **Tip** – Mantenga la respuesta a 5 decimales: `System.out.printf("%.5f\n", ans); ` (Java) o `format(ans, '.5f')` (Python).

-...

## 8️ Takeaway for Your Next Technical Interview

*Baja el flujo* No es sólo “add 1”; es *cuánta desbordamiento*.
- **DP + Simulación** – Una mezcla perfecta de pensamiento algoritmo y aplicación cuidadosa.
- **Language‐agnostic proof** – Mostrar la misma lógica en Java, Python y C++ para demostrar versatilidad.
- **Claridad > Micro-optimización** – Atención al cliente más sobre lógica limpia que apretar un byte.

■ **Pro-tip:** Cuando escriba su propia solución LeetCode, agregue un comentario en la parte superior con el enlace de problema y una descripción corta. Señala que estás organizado y preparado.

-...

## 🎯 SEO‐Ready Summary

■ *“Champagne Tower”* es un reto común de entrevista de LeetCode que prueba la programación dinámica, la simulación y el manejo de los bordes. El problema es solvable en Java, Python, o C++ con una simple fila-por-row DP. Este artículo te lleva a través de la lógica, analiza la complejidad, enumera las trampas, y proporciona fragmentos de código limpio. Usa esto como punto de conversación en tu próxima entrevista de codificación, y demostrarás fuertes cortes algorítmicos que los reclutadores aman.

-..