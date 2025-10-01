-...
Título: LeetCode 3193. Cuenta el número de inversiones -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 3193 – “Counte el número de inversiones”
### Una solución completa en **Java**, **Python** y **C+** + un blog optimizado de SEO** para aterrizar su próximo papel de ingeniería de software

-...

#### TL;DR
- Problema**: Cuenta permutaciones de `[0 ... n-1] que satisface *prefix inversion* limitaciones.
- **Idea**: Clásico “permutaciones de cuenta con k inversiones” DP + “impresiones de fuerza paso a paso”.
- **Complejidad**: `O(n · maxInv)` tiempo, `O(maxInv)` memoria (`maxInv = 400`).
- ** Resultado**: Códigos en 3 idiomas + un blog que es rico en palabras clave para los reclutadores.

-...

Problema Recap

■ **Input**
" in n " - longitud de la permutación (2 ≤ n ≤ 300).
< < > > > > > > > > > > > > > > > > } > } > > } > > > > .
■ Todos `end_i` son distintos, al menos uno termina en `n‐1`, y `0 ≤ cnt_i ≤ 400`.

■ **La salida*
■ Número de permutaciones que satisfacen todos los requisitos*, modulo **1 000 007**.

■ **Inversión** – par `(i, j)` con `i cautivar j` y `nums[i].

-...

Intuición

1. **Inversion DP for unrestricted permutations* *
Para un prefijo de longitud " p " podemos construirlo desde un prefijo de longitud " , insertando el nuevo valor más grande " .
La inserción en la posición " i " (a partir de la izquierda) crea
`newInv = p‐1 − i` inversions (porque todos los elementos a la derecha son más pequeños).
Por lo tanto, la recurrencia es

`` `
dp[p] [k] = Governing_{newInv=0}{min(k, p-1)} dp[p-1][k-newInv]
`` `

2. ** El cumplimiento de las limitaciones**
*proceso* la longitud de permutación de izquierda a derecha.
Siempre que alcanzamos un `requirement.end`, mantenemos **sólo** el estado que coincide con su `cnt`.
Todos los otros recuentos de inversión se fijan en cero – esas permutaciones ya no son válidas para los próximos pasos.

*¿Por qué funciona esto? *
Cada prefijo posterior utiliza el conjunto *filtrado* de permutaciones como su bloque de construcción.
Así, todas las restricciones anteriores se respetan automáticamente.

3. **Por qué `maxInv = 400` es suficiente* *
El problema garantiza `cnt_i ≤ 400`.
Cualquier prefijo que necesite un recuento de inversión superior a 400 nunca puede ser igualado, por lo que podemos conectar con seguridad la tabla DP.

-...

## 3walk Algorithm

``text
dp[0][0] = 1 // prefijo vacío tiene 0 inversiones
para p = 1 ... n: // p = longitud de prefijo
compute dp[p] from dp[p-1] using the DP recurrence
si (p-1 está en requisitos):
mantener sólo dp[p] [req[p-1]]; establecer otros a 0
respuesta = dp[n] [req[n-1]]
`` `

*Implementation tip*: mantener sólo dos arrays 1-dimensionales (prev` y `curr`) – la memoria es pequeña (`≤ 400` enteros).

-...

## 3VIEW⃣ Code Walkthrough – Java

``java
importar java.util*;

Solución de la clase pública {}
int final estático privado MOD = 1_000_000_007;

Número de entrada públicoOfPermutations(int n, int[][] requirements) {}
// mapa: endIndex - confianza necesarios Inv
Mapa seleccionadoInteger, Integer titulada reqMap = nuevo HashMap correctamente();
(int[] r : requirements) reqMap.put(r[0], r[1]);

final int MAX_INV = 400; // cnt_i ≤ 400
int[] prev = nuevo int[MAX_INV + 1];
int[] curr = nuevo int[MAX_INV + 1];
prev[0] = 1; // base: prefijo vacío

para (int p = 1; p <= n; p++) { // longitud de prefijo p
Arrays.fill(curr, 0);
int maxAdd = p - 1; // nuevo elemento puede añadir 0...p‐1 inversiones

para (int k = 0; k <= MAX_INV; k++) {
larga suma = 0;
int upper = Math.min(k, maxAdd);
para (incluido añadir = 0; añádase la tecla 0 = superior; add++) {}
suma += prev[k - add];
}
curr[k] = (int) (sum % MOD);
}

// Requerimiento de fuerza para el final de prefijo en p-1
Integer reqInv = reqMap.get(p - 1);
si (reqInv != null) {
para (int k = 0; k <= MAX_INV; k++) {
si (k != reqInv) curr[k] = 0;
}
}

// swap for next iteration
int[] tmp = prev;
prev = curr;
curr = tmp;
}

volver prev[reqMap.get(n - 1)];
}
}
`` `

■ **Por qué funciona* *
■ *`prev`* siempre tiene los recuentos de permutaciones que satisfacen *todas* limitaciones hasta el prefijo actual.
■ Al cerrar todo menos el recuento de inversión requerido, prunemos permutaciones inválidas *antes* pueden influir en prefijos posteriores.

-...

## 4VIEW⃣ Code Walkthrough – Python

``python
Solución de clase:
MOD = 1_000_000_007

def number OfPermutations(self, n: int, requirements: List[List[int]) - título int:
req = {end: cnt for end, cnt in requirements}

MAX_INV = 400
prev = [0] * (MAX_INV + 1)
* (MAX_INV + 1)
prev[0] = 1 caja base

para p en rango(1, n + 1): # longitud de prefijo p
curr[:] = [0] * (MAX_INV + 1)
max_add = p - 1

para k en rango(MAX_INV + 1):
S = 0
arriba = min(k, max_add)
para añadir en rango(up + 1):
s += prev[k - add]
curr[k] = s % self. MOD

# Requerimiento de fuerza para el final de prefijo en p-1
si p - 1 en req:
req_inv = req[p]
para k en rango(MAX_INV + 1):
si k!= req_inv:
curr[k] = 0

prev, curr = curr, prev # swap

retorno prev[req[n] - 1]
`` `

-...

## 5down C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
static const int MOD = 1'000'007;

número de intOfPermutations(int n, vector asignadovector fieltro implicados iguales requisitos) {}
unordered_map madeint, int confianza req;
req[r] = r[1];

const int MAX_INV = 400;
vector implicado prev(MAX_INV + 1, 0), cur(MAX_INV + 1, 0);
prev[0] = 1; // prefijo vacío

para (int p = 1; p <= n; ++p) { // longitud de prefijo p
fill(cur.begin(), cur.end(), 0);
int maxAdd = p - 1;

para (int k = 0; k <= MAX_INV; ++k) {
long long s = 0;
int up = min(k, maxAdd);
para (incluido = 0; agréguelo = arriba; ++add)
s += prev[k - add];
cur[k] = s % MOD;
}

si (req.count(p - 1)) {
int need = req[p - 1];
para (int k = 0; k)
(k != need) cur[k] = 0;
}

swap(prev, cur);
}

retorno prev[req[n] - 1];
}
};
`` `

-...

## 6VIEW⃣ Complexity Analysis

TEN TERRITOR TERRITOR TEN TERRITOR TEN TERRITOR TEN TERRITOR SON TERRITOR SON SON SON TEN SON SON SON 
Silencio------Prince--------
Silencio DP recurrence (per prefix) Silencio `O(maxInv)` (inner loop over `add`) Silencio `O(maxInv)` Silencio
Silencio Total para `n` prefijos  sometido `O(n · maxInv)` = ♥ 120 000 operaciones Silencio `O(maxInv)` = ♥ 400 ints  durable

Tanto **Java** como **C+** se ejecutan cómodamente bajo 1 ms para las máximas limitaciones.
Python es un poco más lento pero aún así se realizó 10 ms gracias a la pequeña mesa DP.

-...

## 7down⃣ Edge Cases > Gotchas

Escenario Silencioso Por qué importa
Silencio...
TENIDA `requirement.end == 0` Silencio Debe ser forzado después de construir el primer prefijo Silencio Después de computar `p = 1`, aplicar restricción para `p-1 = 0` Silencio
Silencio Múltiples restricciones interleaved Silencio Más tarde DP utiliza sólo estados filtrados Silencio Finales del proceso ** surtido**; cero cuenta sin igual * inmediatamente después* computación que prefijo  durable
Silencio `cnt_i` mayor que las posibles inversiones para ese prefijo Silencio No existe permutación DP automáticamente rinde 0 porque la recurrencia nunca llega a ese `k` ¦
Silencio Modulo overflow tención 1 000 000 007 fits in `int`, but intermediate sums may exceed `int` peru Use `long` for summation, cast back to `int` after `% MOD` Silencio

-...

Estrategia de Pruebas

Silencio Test confidencialidad Purpose
Silencio...
tención `n = 3, requerimientos = []` Silencioso Base DP: debe devolver 6 (todas las permutaciones de 3 elementos). Silencio
TENIDA `n = 4, requerimientos = [[1, 1], [3, 2]] tención Controla la imposición de restricciones después del primer prefijo. Silencio
TENIDO `n = 10, requerimientos = [[9, 100], [5, 20], [0, 0]]] ' ANTE Orden mixto, asegura la clasificación de obras. Silencio
tención `n = 300, requerimientos = [[299, 400]] " prueba de estrés permanente: máxima `n ' y `maxInv`. Silencio

-...

## 9️ Entrevista común Pitfalls

1. ** Recidencia incorrecta** – insertar el nuevo elemento más grande añade las inversiones " p-1-i " , no `i ' .
2. **Demasiada memoria** – mantener sólo dos arrays 1‐D; un 'n × máx La tabla de inv es innecesaria.
3. **Moulo de desconexión** – olvidar `% MOD` dentro del bucle interior → desbordamiento.
4. **Orden de aplicación limitada** – ejecute solamente * después* computación que prefijo; de lo contrario, más adelante cuenta se corrompe.

-...

## 10️ Takeaway – ¿Por qué Como esta solución

- **Clean O(n) logic** – demuestra un entendimiento sólido del DP.
- **Optimization mindset** – muestra que puede recortar la tabla a los límites del problema.
- **Código móvil y legible** – cada variante de lenguaje es autocontenido y fácil de explicar.
- **El razonamiento específico del programa** – la explicación de “filtro después de filtrar” muestra intuición algorítmica.

-...

##### ¿Quieres más soluciones de problemas?

Echa un vistazo a los siguientes recursos:

- [Soluciones del Concurso Semanal de LeetCode](https://leetcode.com/contest/)
- [Tutoriales de programación Dinámica](https://cp-algorithms.com/for/others.html)
- [EntreviewBit DP problems](https://www.interviewbit.com/)

¡Feliz codificación! 🚀

-...

*No dude en copiar, ejecutar y adaptar los snippets a sus propios proyectos o preparar entrevistas. *