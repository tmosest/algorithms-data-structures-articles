-...
Título: LeetCode 466. Cuenta las Repeticiones -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código de Solución

A continuación se presentan tres soluciones completas, autocontenidas que compilan en los últimos JDK, Python 3.11 y GCC 14.

-...

### 1.1 Java (LeetCode 466)

``java
importa java.util. HashMap;
importa java.util. Mapa;

Solución de la clase pública {}
public int getMaxRepeticiones(String s1, int n1, String s2, int n2) {
si (n1 == 0) retorno 0;
// clave : índice en s2, valor : (indice de bloqueo, cuenta de s2 visto)
Mapa seleccionadoInteger, int[] registro = nuevo HashMap garantizado();

int index = 0; // posición dentro de s2
int count = 0; // cuántos s2 hemos completado
bloque int = 0; // cuántos bloques S1 procesados

mientras (bloqueo)
// procesar un bloque de s1
para (int i = 0; i) i++) {
si (s1.charAt(i) == s2.charAt(index)) {}
index++;
si (index == s2.length()) { // uno más s2 terminado
índice = 0;
contar++;
}
}
}

bloque++;

// detección de ciclos
Integer key = index;
si (record.containsKey(key)) {
int[] prev = record.get(key);
int prevBlock = prev[0];
int prevCount = prev[1];

// números antes del ciclo
int prefixBlocks = prevBlock;
int prefixCount = prevCount;

// números dentro del ciclo
int cycleBlocks = block - prevBlock;
ciclo int Cuenta = cuenta - prevCount;

// bloques restantes después de ciclos completos
int Bloques = n1 - bloque;
int full Ciclos = bloques restantes / cicloBlocks;
int tailBlocks = remainingBlocks % cycleBlocks;

total Cuenta = prefixCount
+ fullCycles * cicloCount
+ getTailCount(s1, s2, index, tailBlocks, count, prevCount);

total de retornoCount / n2;
}

// Recuerde el estado actual
record.put(index, new int[]{block, count});
}

// ningún ciclo detectado
recuento de retorno / n2;
}

/** cuenta cuántos más s2 podemos conseguir en la parte trasera. */
int privado getTailCount(String s1, String s2, int startIndex,
int tailBlocks, int curCount, int prevCount) {}
int index = inicio Índice;
int count = curCount;
para (int i = 0; i) {}
para (int j = 0; j) j++) {
si (s1.charAt(j) == s2.charAt(index) {
index++;
si (index == s2.length()) {}
índice = 0;
contar++;
}
}
}
}
recuento de retorno - prevCount;
}
}
`` `

*Tiempo*: **O(las vidas1 permanecen inmóviles*
*Espacio*: **O(las vidas2 sometidas)** – el mapa puede contener en la mayoría de los diferentes índices de ‘las vidas2’.

-...

### 1.2 Python (LeetCode 466)

``python
de la importación Dict, Tuple

Solución de clase:
def getMaxRepeticiones(self, s1: str, n1: int, s2: str, n2: int) - título int:
si n1 == 0:
retorno 0

# key : position in s2, value : (block_index, count_of_s2)
registro: Dict[int, Tuple[int, int] = {}

idx_s2 = 0 # posición actual en s2
cuenta = 0 # número de s2 terminado
bloque = 0 # número de bloques s1 procesados

mientras que el bloque No1
por ch en s1:
si ch == s2[idx_s2]:
idx_s2 += 1
si idx_s2 == len(s2):
idx_s2 = 0
Cuenta += 1
bloque += 1

# Detección del ciclo
si idx_s2 en disco:
prev_block, prev_count = record[idx_s2]

# Prefix
prefix_blocks = prev_block
prefix_count = prev_count

# ciclo
ciclo_blocks = bloque - prev_block
cycle_count = count - prev_count

rest_blocks = n1 - bloque
full_cycles = remaining_blocks // cycle_blocks
tail_blocks = rest_blocks % cycle_blocks

Total =
prefix_count
+ full_cycles * cycle_count
+ auto._tail_count(
s1, s2, idx_s2, tail_blocks, count, prev_count
)
)
total de retorno // n2

record[idx_s2] = (block, count)

# No hay ciclo encontrado
cuenta de retorno // n2

@staticmethod
def _tail_count(s1: str, s2: str, start: int,
sa_blocks: int, cur_count: int,
prev_count: int) - Propiedad int:
idx = start
cnt = cur_count
para _ en rango(tail_blocks):
por ch en s1:
si ch == s2[idx]:
idx += 1
si idx == len(s2):
idx = 0
cnt += 1
cnt - prev_count
`` `

*Tiempo*: **O(las vidas1 permanecen inmóviles*
*Espacio*: **O(las vidas2 sometidas)**

-...

### 1.3 C++ (LeetCode 466)

``cpp
#include ■string
#include ■unordered_map Conf
Incluido el título

Clase Solución {
public:
int getMaxRepeticiones(std::string s1, int n1,
std::string s2, int n2) {
si (n1 == 0) retorno 0;

// mapa: índice en s2 - ratio(blockIndex, countS2)
std::unordered_map observadoint, std::pair obtenidosint, int confianza record;

int idxS2 = 0; // posición en s2
int count = 0; // número de s2 terminado
bloque int = 0; // número de bloques S1 procesados

mientras (bloqueo)
por (char ch : s1) {
si (ch == s2[idxS2]) {}
++idxS2;
si (idxS2 == (int)s2.size()) {}
idxS2 = 0;
++cuenta;
}
}
}
++bloqueo;

// detección de ciclos
auto = record.find(idxS2);
if (it != record.end()) {
int prevBlock = it- convienesecond.first;
int prevCount = it- convienesecond.second;

/ Parte de prefijo
int prefixCount = prevCount;

// Parte del ciclo
int cycleBlock = block - prevBlock;
ciclo int Cuenta = cuenta - prevCount;

int remaining = n1 - block;
int full Ciclos = restantes / cicloBlock;
int tailBlocks = restante % cycleBlock;

total de entrada =
prefixCount
+ fullCycles * cicloCount
+ saCount(s1, s2, idxS2, tailBlocks, count, prevCount);

devolver total / n2;
}
registro[idxS2] = {block, count};
}

// ningún ciclo detectado
recuento de retorno / n2;
}

privado:
/* cuántos s2 extra se pueden recoger en la parte trasera */
int tailCount(cont std::string s1, const std::string s2,
int start Idx, ent tailBlocks,
int curCount, int prevCount) const {
int idx = inicio Idx;
int cnt = curCount;
para (int i = 0; i) {}
por (char ch : s1) {
si (ch == s2[idx]) {}
++idx;
si (idx == (int)s2.size()) {}
idx = 0;
++cnt;
}
}
}
}
cnt - prevCount;
}
};
`` `

*Tiempo*: **O(las vidas1 permanecen inmóviles*
*Espacio*: **O(las vidas2 sometidas)**

■ **Las tres implementaciones utilizan la misma idea** – atravesar `s1` `n1` veces, mantener el índice actual dentro `s2`, contar cuántas 's2' completas podemos extraer, y buscar un ciclo para saltar el trabajo repetido.
■ La detección del ciclo garantiza que el algoritmo nunca exceda unas pocas cientos de iteraciones (porque sólo hay «indices distintos de las vidas2 de la vida»).

-...

## 2. Blog Artículo – “Cracking LeetCode 466: Cuenta las Repeticiones”

### 🗞י Meta Descripción
**LeetCode 466 – Cuenta Las Repeticiones** – Maestro el problema de subsecuencia de cuerdas más duro con un algoritmo basado en ciclos. Lea las soluciones Java, Python y C++, análisis de complejidad, consejos de preparación de entrevistas, y haga su próximo trabajo de ingeniería de software!

-...

###  pila 1.

TENIDO TERRITORIO TENIDO Detalles Silencio
Silencio...
Silencioso **LeetCode ID**
Silencio **Nombre** Silencio Cuenta Las Repeticiones
Silencio **Dificultad**
Silencio **Tags** Silencio String, Subsequence, Two‐Pointer, Hash, Algorithm, Interview ¦

**Declaración* *
Dados dos cuerdas `s1` y `s2`, repetir `s1` exactamente `n1 ` veces (formando `S1 = s1.repeat(n1)`) y repetir `s2 ` exactamente `n2 ` veces (formando `S2 = s2.repeat(n2)`).
`S2` es una subsecuencia ** de `S1` si podemos eliminar caracteres de `S1` para obtener `S2`.
Devolver el entero máximo `k ' tal que `S2 ` repetido `k` tiempos es una subsequencia de `S1`.
En términos formales: `k = ⌊ maxMatches / n2 ⌋`.

-...

### 2. Por qué este problema es interesante

✔ Buena Нели не не не ны Bad вы ны не ны не ны не ны не ны не ны не не ны ны неле ны ны ны ны ны ны у у у ны ны у ны ны ны ны у у у ны у у у у у у у у у у у у у у ны у у у у у у у у у у у у у у у у у у у у у у у ны ны у у у у ны ны у у у у у у у у у у у у у ны у 
Silencio------------
Silencio **Bien** Silencio • Requiere una comprensión profunda de la lógica de la subsequencia. solución es demasiado lenta. Silencio • Mis-reading “repeat” como “concatenado” conduce a resultados incorrectos. Silencio
Las limitaciones (`n1, n2 ≤ 10000`) le obligan a pensar en términos de *ciclos* en lugar de fuerza bruta. Silencio • Es fácil perderse en aritmética puntero cuando `s1` y `s2` son de diferentes longitudes. Silencio • El no poder memoizar estados conduce a 'TLE' en grandes entradas. Silencio
Silencioso **Ugly** El editorial oficial es conciso pero no amigable para principiantes. Silencio • Algunos idiomas (por ejemplo, los compiladores más antiguos de C++) no soportan el `unordered_map` de pares elegantemente. Silencio • La gente a veces exagerado utilizando tablas de DP o `std::vector nombrado `` de tamaño `n1`, que consume memoria innecesaria. Silencio

-...

### 3. Visión Algorítmica

1. Traversal de paso fijo
Escaneo `s1' bloque por bloque.
Mantenga un índice `idxS2` en `s2`.
Cuando un personaje de `s1` coincide con el carácter actual de `s2`, avance `idxS2`.
Siempre que `idxS2` llega al final de `s2`, hemos extraído uno completo `s2` y reasentamos `idxS2` a `0`.
Incremento una `cuenta' que rastrea cuántos `s2's hemos extraído.

2. *Detección de ciclos*
Lo único que importa después de procesar cada bloque de `s1` es el actual `idxS2`.
Sólo existen valores posibles para `idxS2`.
Si el mismo `idxS2` aparece de nuevo, hemos entrado en un *ciclo*: el patrón de futuras terminaciones repite.
Registre el índice de bloques y la 'cuenta' cuando aparezca cada 'idxS2' único.
Una vez que se encuentra un ciclo, descomponga el trabajo restante en:

* **Prefijo** – parte antes de que comience el ciclo.
* **Cycle** – el segmento repetible.
* **Tail** – los bloques de sobra que no forman un ciclo completo.

3. **Computar el número total de s2**
`` `
total = prefixCount
+ fullCycles * cicloCount
+ saCount
`` `

`tailCount` se computed por simular los `tailBlocks ' restantes (a la mayor parte de un ciclo de longitud).

4. **Respuesta** – división por `n2` (división de enteros).

El algoritmo funciona en tiempo lineal con respecto a las longitudes de `s1` y `s2` más una pequeña constante para la búsqueda del ciclo. El consumo de memoria se ve obligado por " las vidas2 eternas " .

-...

### 4. Código Snippets

Silencio Idioma Silencio Archivo clave Silencio Complejidad
Silencio--------------------------
Silencio **Java** Silencioso `Solution.java` Silencioso ** Tiempo** O(sobrevividos1 sobre la vida eterna) **Espacio** O(sobrevivientes2) Silencio
tención **Python** Silencioso `solution.py` Silencio ** Tiempo** O( las vidas1 sometidas+ las vidas2 sometidas) **Espacio** O(las vidas2 sometidas) Silencio
Silencio **C+** Silencioso `Solution.cpp` Silencioso ** Tiempo** O(sobrevivientes1 sobreviviente+ sobre la vida) **Espacio** O(las vidas2 vivas) Silencio

*Los bloques de código completo se muestran arriba. *

-...

### 5. Consejos de entrevista

Tema de la vida _ Por qué importa
Silencio...
Silencio **Two‐pointer technique** Silencio Mantiene seguimiento de posiciones en `s2` mientras escanea `s1`. Silencio Piensa en `s1` como el bucle "outer" y `s2 ` como el puntero "inner". Silencio
Silencio **Detección de ciclos** Silencio nos permite saltar grandes repeticiones (`n1` hasta 10 000). tención Almacene el *state* (index in `s2`) en un mapa; una vez visto de nuevo usted sabe que está bucleando. Silencio
Silencio **Análisis de la complejidad** ¦ Los entrevistadores amor limpio Big‐O discusión. Silencio Destacar el tiempo lineal y el espacio constante (O(las vidas2 vivas)). Silencio
Silencioso ** Casos de evacuación** Silenciosos cuerdas vacías, `n1==0`, `s2 `más largo que `s1`. Prueba estos antes de codificación. Silencio

■ **Pro tip** – Al explicar su solución, mencione que este es un problema clásico *“encuentre el período”* que aparece en muchas preguntas de entrevista de subsecuencia de cadena. Muestra una profunda comprensión de cómo optimizar más allá de la fuerza bruta.

-...

### 6. ¿Por qué esta solución te trae el trabajo

1. **Clear, código idiomático** – Sin arrays innecesarios, cada variable tiene un solo propósito.
2. ** algoritmo escalable** – Funciona cómodamente para los peores límites de los casos (`n1, n2 ≤ 10 000`).
3. **Preparado para seguimientos** – Si el entrevistador pregunta “¿Qué pasa si ‘s1’ o `s2’ es extremadamente largo?”, usted puede explicar con confianza el enfoque basado en el ciclo.
4. **Versatil** – Demuestra tu capacidad de traducir la misma lógica a través de Java, Python y C++ – un disco rojo para empresas que utilizan múltiples pilas de tecnología.

-...

## 2. SEO‐Optimized Blog Post

■ **Título**: *Maestro LeetCode 466 – Conde Las Repeticiones: Java, Python, C+++ Prep*

■ **Meta Descripción**: Aprende la solución óptima para LeetCode 466 – Contar las Repeticiones. Sumérgete en el problema de subsecuencia de cadenas duras, explora la detección de ciclos y ve las implementaciones Java, Python y C++ que te ayudan a mejorar tu próxima entrevista tecnológica.

``markdown
# Master LeetCode 466 – Cuenta las Repeticiones (Hard)

**LeetCode 466** es un favorito entre ingenieros de software y entusiastas de la estructura de datos.
Este post te lleva a través de una solución rápida basada en ciclos en **Java**, **Python**, y **C+**.
Diseccionaremos por qué el problema es desafiante, resaltar los conceptos clave de entrevista, y le daremos la ventaja de aterrizar su papel de sueño.

-...

## 🚀 Problemática instantánea

■ * Objetivo*
⇩ - Repita `s1` `n1` veces → `S1`.
■ - Repita `s2` `n2` veces → `S2`.
- Encontrar el máximo `k ' tal que `S2 ` repetido `k` tiempos es una subsequencia de `S1`.

### Why It's Hard

- No se trata sólo de concatenación; usted debe **delete** caracteres de `S1` para coincidir con `S2`.
- Brute‐force `O(n1· las vidas1· las vidas2 sometidas)` es inaceptable para `n1, n2 ≤ 10,000`.
- El malentendido “repeat” versus “concatenado” conduce a errores.

-...

## 📈 Algoritmic Breakthrough

1. **Escaneo luminoso de la técnica de dos puntos.
2. **Concluciones de tráfico de `s2`** - Use un índice `idxS2` y un contador `contra`.
3. ** Ciclos de insectos** – Sólo los estados de `responders2 inquietos ' posibles `idxS2`; use un mapa.
4. **Skip repeticiones** – Compute prefijo, ciclo y cola para conseguir 'total Matches`.
5. Resultado** – División entero por n2.

El algoritmo se ejecuta en **O(las vidas1 sobrevivir + Silencios2 sobrevivir)** tiempo y **O(las vidas2 sobrevivir)** espacio.

-...

Código de tres idiomas

Silencio Idioma Silencio Complejidad
Silencio...
Silencio **Java** Silencio ** Tiempo** O(las vidas1 sobre la vida eterna) **Espacio** O(las vidas2 vivas) Silencio
Silencio **Python** Silencio **Tiempo** O(sobrevividos1 sobre la vida eterna) **Espacio** O (sobrevivir) Silencio
tención **C++** Silencio **Hora** O(las vidas1 sobre la vida eterna) **Espacio** O(las vidas) Silencio

■ *El código fuente completo se proporciona en el artículo anterior. *

-...

## 🧠 Interview Prep Checklist

- Estrategia de dos puntos para que coincida la subsecuencia.
- Detección del ciclo estatal para evitar TLE.
- Manejo de caso de borde (`n1==0`, cuerdas vacías).
- Discusión de complejidad: tiempo lineal, espacio extra constante.

-...

## 🎯 Get Hired

Mostrar reclutadores que puedes resolver un problema difícil de LeetCode con código limpio y eficiente en varios idiomas.
Esto demuestra:

1. ** Profundidad algorítmica** – la detección del ciclo es una técnica probada.
2. **Versatilidad lingüística** – habilidad para escribir Java idiomático, Python y C++.
3. **Mente de solución de problemas** – se centra en la optimización, no en la fuerza bruta.

-...

¡Feliz codificación!
`` `

-...

#### 📌 Key SEO Palabras clave

- LeetCode 466
- Cuenta las Repeticiones
- Problema de subsecuencia de cuerda dura
- algoritmo de cadena Java
- Python técnica de dos puntos
- Detección de ciclo C++ sin orden
- Preparación de entrevista para problemas de cuerda
- Estructuras de datos y algoritmos
- Soluciones de entrevistas de ingeniería de software

-...

### 3. Pensamiento final

LeetCode 466 te enseña cómo transformar un desafío de cuerda aparentemente intráctil en una solución elegante y eficiente.
Ya sea que codificas en **Java**, **Python**, o **C++**, la idea central sigue siendo la misma: escanear una vez, recordar tu estado, encontrar el ciclo y saltar el resto.

Utilice los fragmentos de código y las ideas de entrevistas anteriores para **confidentalmente explicar** el problema en su próxima entrevista y **Mostrar su dominio** de técnicas avanzadas de manipulación de cadenas. ¡Buena suerte! 🚀

-...

*End of blog post. *

-...

Esta guía integral, combinando códigos de producción y explicaciones de entrevistas, debería facultarle para dominar a LeetCode 466 e impresionar a los reclutadores en cualquier empresa de alta tecnología. ¡Feliz solución!