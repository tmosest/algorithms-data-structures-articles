-...
Título: LeetCode 1434. Número de maneras de usar diferentes sombreros para cada uno -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recapitulación del problema – LeetCode 1434
**Número de maneras de usar diferentes sombreros para cada uno**

* Hay `n` personas (`1 ≤ n ≤ 10`).
* Hay 40 tipos de sombreros (`1 ... 40`).
* `hats[i]` enumera los números de sombrero que le gusta a la persona.
* Cada persona debe usar **exactamente un sombrero** y ninguna persona puede usar el mismo sombrero.
* Devuelve el número de asignaciones válidas modulo **1 000 000 007**.

La solución clásica es un *bit-mask DP* que itera sobre los 40 sombreros en lugar de la gente, porque el número de sombreros es fijo (40) mientras que el número de personas es pequeño (`≤ 10`).

-...

## 2. La Idea – Bien, el Mal, el Ugly

Silencio Silencio Silencio Good Silencio El mal Silencio
Silencio------------------------
Silencio **Concepto** Silencio Treat hats as the *outer loop*; la gente es el *state* Silencio Sin ninguna poda usted exploraría `40 * 2n` estados - todavía diminuto, pero la profundidad de la recursión puede explotar Si olvida el modulo o el desbordamiento, la respuesta puede ser negativa/incorrecta
Silencio **Complejidad** Silencio `O(40 · 2n)` tiempo, `O(40 · 2n)` memoria Silencio Por `n = 10`, 2n = 1024 → ~40 000 células DP – perfectamente bien Silencio Si usted utiliza un array de 32 bits para la máscara DP (tamaño `1 obtenidos'), usted puede correr en problemas de memoria en máquinas muy limitadas
Silencio **Implementación** Silencioso Recursión + memoización o subida DP Ø Las personas pueden no gustar el sombrero actual – muchas afirmaciones de `continue`  sometida Un error común es olvidar convertir índices de sombreros (1-basado → 0-basado) o mal-index the DP table tención

-...

## 3. El Algoritmo (Step‐by‐Step)

1. **Proceso previo**
Construir un array `pueblo[41]` Donde 'pueblo' es la lista de personas que les gusta el sombrero.
Este es el inverso de la entrada y nos permite iterar sobre sombreros de manera eficiente.

2. ** Estado de desplazados**
`dp[hat][mask]` – number of ways to assign hats from `hat` to `40` **Dado** que las personas representadas por la mascara de bits siguen siendo **unassigned**.
*`mask`* es un poco mástil de longitud `n`.
Ejemplo: si `n = 3` y `mask = 0b101` → las personas 0 y 2 todavía están libres.

3. **Transición**
Por un `hat ' y `mask ' dado:
* **Skip** el sombrero: `ways = dp[hat+1][mask].
* Para cada persona `p` que le gusta este sombrero (`p  divisar gente [hat]`) y todavía es libre ('mask ' (1 obtenidosp)`):
* Asignar el sombrero a `p` → nueva máscara `mask ^ (1 se realizó)`.
* Recurse: `ways += dp[hat+1][mask ^ (1 obtenidos)].
Todo aritmético es modulo `MOD`.

4. **Casos de base**
* If `mask == 0` → todas las personas ya están asignadas → regreso `1`.
* If `hat Ø 40 ' and `mask != 0` → no hats left → return `0`.

5. Resultado**
Comience de `hat = 1` y máscara completa `(1 seleccionado)-1`.

La profundidad de recursión es en la mayoría de `41` (hats + 1) – seguro para todos los idiomas.

-...

## 4. Análisis de la complejidad

TENIDO MEDIO ANTERIOR Fórmula ANTERIENTE Valor para `n = 10` ANTE
Silencio------------------------- La vida...
TENIDO ANTERIOR TENIDO `O(40 · 2n) ' TENIDO ` TÉCNICA 40·1024 ♥ 40 960 ' operaciones
TENIDO Memoria TENIDO `O(40 · 2n)` TENIDO `A 40 960` enteros (~160 KB) ANTE

Ambos están bien dentro de los límites para la programación competitiva o LeetCode.

-...

## 5. Aplicación del Código

A continuación se muestran ** soluciones limpias, listas para la producción** para **Java**, **Python**, y **C+**.
Todos comparten la misma idea algoritmo; las únicas diferencias son sintaxis y estructuras de datos.

### 5.1 Java

``java
importar java.util*;

Clase Solución {
int final estático privado MOD = 1_000_000_007;
// dp[hat][mask] where hat  Iberia [1, 40] (index 1‐based)
int privado[] dp;
int n privado; // número de personas
privada Lista realizadaInteger confianza[] personas; // personas que gustan de cada sombrero

público número Ways(ListectoList) {Integer títulos) {
n = sombreros.size();
// personas[1..40] – lista de índices de persona que gusta el sombrero h
personas = nuevo ArrayList[41];
para (int i = 0; i <= 40; i++) personas[i] = nuevo ArrayList fiel();
para (int p = 0; p < n; p++) {}
para (int h : hats.get(p)) personas[h].add(p);
}

// dimensiones dp: 41 sombreros + 1 (1-basado), 1
dp = nuevo int[41][1] [1]
for (int[] row : dp) Arrays.fill(row, -1);

dfs(1, (1 , 3)
}

int privado dfs(int hat, int mask) {
si (mask == 0) retorno 1; // todas las personas asignadas
si (hat 40) devuelve 0; // no se quedan sombreros

int &res = dp[hat][mask];
si (res!= -1) restitución;

int ways = dfs(hat + 1, máscara); // skip this hat
for (int person : people[hat]) {}
si (mask > (1 > ) 0) {
maneras += dfs(hat + 1, máscara ^ (1 <) persona obtenida);
-= MOD;
}
}
retorno res = maneras;
}
}
`` `

### 5.2 Python

``python
Solución de clase:
MOD = 10**9 + 7

def number Ways(self, hats: List[List[int]]) - int:
self.n = len(hats)
gente [hat] lista de personas que les gusta este sombrero
personas = [[] for _ in range(41)]
para p, h_list in enumerate(hats):
para h_list:
personas[h].append(p)

# dp[hat][mask] with hat 1‐based
autor.dp = [1] * (1 < > > > > >
full_mask = (1 Гленнанная auto.n) - 1
volver a sí mismo._dfs(1, full_mask)

def _dfs(self, hat: int, mask: int) - título int:
si máscara == 0:
Regreso 1
si hat > 40:
retorno 0

si auto.dp [hat] [mask] != -1:
volver a sí mismo.dp[hat][mask]

maneras = self._dfs(hat + 1, máscara) # skip current hat
por persona en personas [hat]:
si la máscara " (1 " )
maneras += uno mismo._dfs(hat + 1, máscara ^ (1 iere persona)
maneras %= uno mismo. MOD

autodp [hat] [mask] = ways
Retorno
`` `

■ **Tip** – En Python se puede utilizar 'lru_cache` para una implementación ligeramente más limpia, pero la tabla manual mostrada anteriormente le da control sobre el diseño de memoria.

### 5.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
static const int MOD = 1'000'007;
int n;
vector realizador designado injerto; // dp[hat][mask], sombrero 1-basado
vector realizador implicado personas; // personas [hat] - lista de índices de persona

int numberWays(vector seleccionadovector identificadoint
n = sombreros.size();
people.assign(41, {});
para (int p = 0; p < n; ++p) {
para (int h : sombreros[p]) personas[h].push_back(p);
}

dp.assign(41, vector asignadoint título(1)
dfs(1, (1 , 3)
}

privado:
int dfs(int hat, int mask) {
si (!mask) retorno 1; // todas las personas asignadas
si (hat 40) devuelve 0; // no se quedan sombreros

int pulmonar res = dp[hat][mask];
si (res!= -1) restitución;

largos largos caminos = dfs(hat + 1, máscara); // patrón sombrero
for (int person : people[hat]) {}
si (mask " (1 " ) {}
maneras += dfs(hat + 1, máscara ^ (1 <) persona obtenida);
maneras %= MOD;
}
}
retorno res = (int)ways;
}
};
`` `

-...

## 6. Arnés de prueba rápida (Todos los idiomas)

``text
Entrada: sombreros = [3,4], [4,5], [5,6]
Producto : 6
Explicación : 3 personas, 3 sombreros – cada persona le gusta un sombrero diferente, todos 3! = 6 maneras.

Entrada: sombreros = [3,5], [3,5], [3,5]]
Producto : 0
Explicación : 3 personas todos quieren sombreros 3 o 5 – sólo dos sombreros disponibles, imposible.

Entrada: sombreros = [[2], [1, 2], [1, 3]
Producto: 2
Explicación : Person0 → 2; Person1 → 1; Person2 → 3 OR Person1 → 2, Person2 → 1.
`` `

Usted puede pegar cualquiera de los anteriores en el editor de LeetCode y ejecutar las pruebas de muestra. El tiempo de ejecución suele ser de 100 ms en todos los idiomas.

-...

## 7. Qué decirle al entrevistador

1. ¿Por qué los sombreros como el bucle exterior? * *
* “Porque el conjunto de sombreros está fijo (40) mientras que el número de personas es diminuto, la iteración sobre sombreros mantiene el estado pequeño (`2n`) y garantiza que nunca retrocedamos sobre las personas.”*

2. **Definición del Estado**: `mask` = " personas no firmadas " .
Mostrar un diagrama simple: `mask = 0b101` → personas 0 & 2 todavía necesitan sombreros.

3. **Transición** – “O saltar el sombrero o asignarlo a una de las personas libres que les gusta. ”
Mencione la operación modulo para mantener la respuesta positiva.

4. ** Casos de Edge** – “Si todas las personas ya están asignadas hemos terminado; si nos quedamos sin sombreros antes de volver 0. ”

5. **La complejidad** – "O(40·2n) tiempo y memoria; con 'n=10' que es ~4 × 104 celdas – trivial para las máquinas actuales. ”

6. ¿Por qué no un simple retroceso? * *
“Backtracking todavía sería `40 · 2n`, pero sin memoización volvería a computar subproblemas muchas veces. DP lo reduce a un computation por `(hat, máscara)` par.

-...

## 8. Pitfalls comunes " Cómo evitarlos

Silencio Pitfall Silencio
Silencio...
tención **Missing modulo** – resultados envolver alrededor de números negativos ← Siempre realizar `% MOD` después de cada adición, y utilizar 'si (ways √≥= MOD) maneras -= MOD;` Silencio
tención **1-basada / 0-basada confusión** tención Tienda sombreros exactamente como aparecen (1-basada) en `pueblo[1...40]`. No hace falta restar 1 a ninguna parte. Silencio
Silencio **Large DP table** ← `n ≤ 10` ⇒ `1 obtenidos ` = 1024. 41 × 1024 ♥ 40 000 ints ♥ 160 KB. Seguro. Silencio
Silencio **Profundidad de la recursión** Silencio Max profundidad 41 – seguro en Java, Python, C++. Silencio
Silencio ** Listas ininicializadas** Silencio En Java, recuerden inicializar `pueblo[0]` (no usado) o índices de guardia. Silencio

-...

## 9. Tomado para su próxima entrevista

* **Explicar claramente el estado** – muchos candidatos saltan directamente a retroceder y se atascan.
* **Mostrar el diseño de mesa DP** – dibujar una pequeña matriz (`hat` vs `mask`).
* ** Demostrar un caso base** – “mask == 0 → 1”.
* **Mención del modulo temprano** – a los entrevistadores les gusta ver que usted está consciente de flujo entero.
* **Time/Space** – un rápido “40·2n = 40 960” es un buen cheque de cordura.

Con esto, impresionará a los administradores de contratación que valoran el pensamiento algoritmo limpio y la capacidad de codificar en varios idiomas.

-...

## 10. Palabras finales

La parte **buena**: un DP conciso que funciona en unos pocos milisegundos.
La parte **bad**: muchos candidatos olvidan el truco hat-as‐outer-loop o el modulo.
The **ugly** part: a single mis-indexed array cell can break the whole solution.

Al dominar este patrón, usted estará listo para as no sólo LeetCode 1434 sino también **cualquier pregunta de entrevista** que implica asignar un pequeño número de entidades a un grupo más grande de categorías.

Buena suerte en tu entrevista de codificación, y feliz piratería!