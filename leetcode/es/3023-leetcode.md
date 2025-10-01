-...
Título: LeetCode 3023. Encontrar patrón en flujo infinito Yo...
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código – 3 idiomas

A continuación se muestran **ready‐to-copy** implementaciones que resuelven el problema LeetCode "3023. Encontrar patrón en flujo infinito Yo” usando la estrategia **rolling-hash (Rabin–Karp)**.
El código está escrito en **Java, Python, y C++** – todo completamente comentado y listo para pruebas unitarias o una entrevista en vivo.

■ ¿Por qué Rolling-Hash? #
■ El flujo es *infinito*, pero el patrón es corto (≤ 100).
■ Un hash rodante nos permite comparar la ventana actual de la corriente con el hash patrón en **O(1)** por personaje, después de un **O(p)** pre-computación, dando una complejidad global del tiempo de **O(n)** donde *n* es el primer índice que contiene el patrón (garantizado ≤ 105).
■ Una simple ventana deslizante o comparación ingenua necesitaría **O(p × n)** operaciones, que es 107 en el peor de los casos - todavía bien, pero el rodaje-hash es más limpio y más rápido.

-...

#### 1.1 Java

``java
*
* LeetCode 3023 – Encuentra Patrón en Corriente Infinita I
*
* Autor: ChatGPT
* Date: 2025‐09‐24
*
* La solución utiliza un hash ondulado (Rabin–Karp) sobre un flujo binario.
*/
Clase Solución {

int public int findPattern(InfiniteStream infiniteStream, int[] pattern) {}
base de entrada final = 2; // Alfabeto binario
final largo mod = 1_000_000_007L; // Grande prima para evitar colisiones

--------- 1. Compute hash of the pattern ---------- */
patrón largo Hash = 0;
base largaPow = 1; // base^(p-1) modulo
para (int i = 0; i) i++) {
patrón Hash = (patternHash * base + patrón[i] % mod;
si (i) patrón. longitud - 1) basePow = (basePow * base) % mod;
}

--------- 2. Inicia la primera ventana desde el arroyo-------- */
ventana larga Hash = 0;
int[] ventana = nuevo int[pattern.length];
para (int i = 0; i) i++) {
int bit = infiniteStream.next();
ventana[i] = bit;
ventana Hash = (ventanaHash * base + bit) % mod;
}

--------- 3. Ventana deslizante ---
int idx = 0; // Índice de inicio actual de la ventana
mientras (verdad) {
si (ventanaHash == patrón Hash ' partido(ventana, patrón)) {}
devolver idx;
}

// Ventana de diapositivas por una
int oldBit = ventana[idx % pattern.length];
nuevo Bit = infiniteStream.next();

// Quitar viejo Contribución parcial
ventana Hash = (ventanaHash - (oldBit * basePow) % mod + mod) % mod;
// Apéndice nuevo Bit
ventana Hash = (ventanaHash * base + newBit) % mod;

// Mantenga el array de ventana deslizante actualizado
ventana[(idx + 1) % pattern.length] = nuevo Un poco;
idx++;
}
}

* Helper: exacta comparación byte‐byte para proteger contra las colisiones hash. */
partidos booleanos privados(int[] ventana, int[] patrón) {}
para (int i = 0; i) i++) {
si (ventana[i]!= patrón[i]) devuelve falso;
}
retorno verdadero;
}
}
`` `

■ **Notas*
* Utilizamos un módulo (`1_000_000_007`) para evitar el flujo entero y minimizar las colisiones de hash.
* El método de 'maches' se invoca sólo cuando los hashes están de acuerdo – las colisiones son prácticamente imposibles para las limitaciones dadas, pero esto garantiza la corrección.

-...

### 1.2 Python

``python
"
LeetCode 3023 – Encuentra Patrón en Corriente Infinita I
Autor: ChatGPT
"

Solución de clase:
def findPattern(self, infiniteStream: 'InfiniteStream', patrón: List[int]) - título int:
base = 2
mod = 1_000_000_007

1. Hash del patrón
Pat_hash = 0
base_pow = 1 # base^(p-1) % mod
para i, bit in enumerate(pattern):
pat_hash = (pat_hash * base + bit) % mod
si yo hice len(pattern) - 1:
base_pow = (base_pow * base) % mod

# 2. Primera ventana
ventana = []
win_hash = 0
para _ en rango(len(pattern)):
bit = infiniteStream.next()
ventana.append(bit)
win_hash = (win_hash * base + bit) % mod

idx = 0
Mientras Verdadero:
si win_hash == pat_hash y ventana == patrón:
idx

old_bit = ventana[idx % len(pattern)]
new_bit = infiniteStream.next()

# Remove contribution of old_bit
win_hash = (win_hash - (old_bit * base_pow) % mod + mod) % mod
# Add new_bit
win_hash = (win_hash * base + new_bit) % mod

ventana[(idx + 1) % len(pattern)] = new_bit
idx += 1
`` `

■ **Python Specifics**
* El modulo se mantiene a lo largo de todo para evitar el desbordamiento en corrientes muy largas (aunque las ints Python no están abundadas).
* `ventana` es un buffer circular (lista) para mantener actualizaciones O(1).

-...

#### 1.3 C++

``cpp
*
* LeetCode 3023 – Encuentra Patrón en Corriente Infinita I
* Autor: ChatGPT
* Fecha: 2025-09-24
*
* La implementación utiliza un hash ondulado (Rabin–Karp) sobre un flujo binario.
*/

Clase Solución {
public:
int findPattern(InfiniteStream corriente, const vector identificadoint compartir patrón) {}
const long base = 2;
const long mod = 1'000'000'007LL;

int pLen = pattern.size();

--------- 1. Pattern hash & base^(pLen-1) -------- */
Pat Hash largo = 0;
base larga largoPow = 1; // base^(pLen-1) % mod
para (int i = 0; i) {}
patHash = (patHash * base + patrón[i] % mod;
b) Si (i " sec " pLen - 1) basePow = (basePow * base) % mod;
}

--------- 2. Primera ventana de la corriente...
vector de ventana(pLen);
long winHash = 0;
para (int i = 0; i) {}
int bit = stream.next();
ventana[i] = bit;
winHash = (winHash * base + bit) % mod;
}

int idx = 0; // índice de inicio de la ventana actual
mientras (verdad) {
si (winHash == patHash " igual(window.begin(), window.end(), pattern.begin()))) {}
devolver idx;
}

// ventana de diapositivas
int oldBit = ventana[idx % pLen];
nuevo Bit = stream.next();

// Eliminar la contribución del viejoBit
winHash = (winHash - (oldBit * basePow) % mod + mod) % mod;
// Apéndice nuevo Bit
winHash = (winHash * base + newBit) % mod;

ventana[(idx + 1) % pLen] = newBit;
++idx;
}
}
};
`` `

■ **C++ Específicos**
* " igual " de " efectua una comparación de byte-wise para descartar las colisiones precipitadas.
* `InfiniteStream` se supone que proporciona un método `int next()`; se puede escribir un envoltorio simple para pruebas de unidad.

-...

## 2. Blog Artículo – “El Bien, el Mal, y el Ugly of Finding Patterns in an Infinite Stream”

■ ** Palabras clave del foro* *
■ `leetcode find pattern in infinite stream`, `rolling hash`, `kmp algoritmo`, `binary stream`, `coding interview`, `job interview coding`, `Python rolling hash`, `Java KMP`, `C++ stream pattern`.

-...

#### 2.1 Introduction

■ “Voy a buscar un flujo infinito para un patrón pequeño. ”
■ Ese es el núcleo de **LeetCode 3023**. Mientras el problema se ve simple, el giro de los datos *infinitos* nos obliga a repensar estrategias típicas de subestring-search.
■ En este artículo caminaremos por el **naïve**, **rolling-hash**, y **KMP** se acerca, analizar sus pros/cons, y darle una lista de verificación para asar la entrevista.

-...

### 2.2 Declaración de problemas (reescrito)

- Se le da un patrón **binario** (arrayo de 0/1, longitud ≤ 100).
- Usted tiene acceso a un objeto `InfiniteStream` que expone `int next()`; cada llamada le da el siguiente bit de una secuencia infinita 0/1.
- Regresar el índice de inicio ** donde aparece el patrón en el flujo.
- Se garantiza que exista un partido dentro de los primeros bits `105`.

-...

### 2.3 Naïve Sliding Window

← Idea Silencioso Complejidad
Silencio------------------------
Silencio Mantenga un deque de las últimas `p` bits; después de cada `next()` comparar deque con el patrón 'O(p·n)` tiempo, `O(p)` espacio TENIDO Para `p=100` y `n=105` → 107 comparaciones – aceptable pero desperdicio; riesgo de TLE en entornos más estrictos TENIDO
Silencio No hay estructuras auxiliares de datos más allá de una pequeña cola ✔ ❌ Factor constante grande ←

**Por qué falla en entrevistas** – Los entrevistadores esperan que pienses en soluciones *time-optimal*. Un linar-scan está bien para algunos problemas, pero con la garantía 'n≤105` esperarán *O(n)* con un trabajo mínimo periteration.

-...

### 2.4 Rolling Hash (Rabin–Karp) – The Good

TENCIÓN ANTERIOR ANTERIOR Explicación
Silencio------------------------------
Silencio Treat bits as digits in base 2, compute hash over a sliding window  durable `O(n)` time, `O(p)` espacio Silencio Cada iteración hace **constant** operaciones aritméticas
Silencio Modulus `1 000 000 007` (o `2^63-1` con unsigned long long) para evitar el desbordamiento ✔ ✔ ✔ Prevents integer overflows ←
← Verificar el partido exacto cuando los hashes coinciden ✔ ✔ Garantías corrección incluso si una rara colisión ocurre ←
Silencio **El amortiguador clásico** para la ventana Silencio Actualizaciones `O(1)`

*Takeaway* – El hash rodante es *la respuesta esperada* para un flujo binario con `p` hasta 100. Es elegante, rápido y escaparate conocimiento de *estring hashing*.

-...

### 2.5 KMP – La alternativa

Silencio Idea Silencioso Complejidad
Silencio------------------------
Silencio Construir la “función de fracaso” del patrón; mientras que la lectura de la secuencia avance el estado TENIDO `O(n)` tiempo, `O(p)` espacio Silencio No modulus, así que no hash; la sobrecabeza aritmética es pequeña (just 2 × p). Silencio
Silencio Obras para cualquier alfabeto ✔ ❌ Más código para explicar (failure function construction)

**Cuando elegir KMP**
- Si usted está codificando en **Java** o **C+** y prefiere permanecer en el reino de “ algoritmo clásico”.
- En una *entrevista de trabajo*, los entrevistadores pueden preguntar explícitamente “¿Podría resolver esto con KMP?” para probar su amplitud algorítmica.

**Por qué normalmente elegimos el hachón rodante sobre KMP** –
- Rolling hash coincide con la naturaleza *stream*: nunca tienes la cuerda completa en memoria; solo guardas la ventana actual.
- Modulus arithmetic es barato en binario y escalas a cualquier tamaño del alfabeto (sólo cambio `base`).
- KMP requiere un array *adicional* (`pi`) pero todavía necesita el mismo `next()` llamadas – ambos son lineales.

-...

### 2.6 The “Ugly” – Hash Collisions

A pesar de que el alfabeto es binario, ** colisiones de hash** son teóricamente posibles (las ventanas diferentes producen el mismo hash).
**Mitigación* *
- Usar un módulo *prime* (`1 000 000 007` o `2^61-1`).
- Realizar una comparación *exacta* cuando el hash coincida.
- En entrevistas, explícitamente declaramos “nos protegemos contra las colisiones con un cheque; las colisiones son astrónomos poco probables. ”

-...

### 2.7 Implementation Checklist

Silencio Silencio ↑ ❌
Silencio...
Silencio **Explicar el problema claramente** – restar restricciones ❌ Jump straight to code ←
Silencio **Describir el modelo de flujo infinito** – no se puede almacenar toda la cadena Н ❌ Assume que se puede vivir
Silencio **Elija el tiempo O(n)** – el hash o KMP ❌ Naïve O(p·n) Silencio
Silencio **Mostrar tiempo-tiempo constante por-iteración** – algunas operaciones enteros, sin bucles ❌ O(p) per-iteration loops ←
Silencio **Guard contra las colisiones de hash** – verifique el patrón cuando hash coincida con ❌ Skip check ¦
tención **Explicar módulos y manejo de desbordamiento** – crucial para Java & C++ ❌ Ignore integer limits ←
Silencio **Mención del límite garantizado (≤ 105)** – esto justifica O(n) pero también insinúa posibles optimistas ❌ Ignore bound Silencio

-...

### 2.8 Entrevista de muestra Pseudo‐Code

``text
1. Patrón de cálculo Hash = patrón de la Asamblea [i] * base^(p-1-i) (mod M)
2. Construye primera ventana de tamaño p desde el arroyo.
3. Para cada nuevo bit:
a. Hachón de turno: eliminar la contribución más izquierda.
b. Añada un poco nuevo.
c. Si los fósforos coinciden, compare bits para la seguridad de colisión.
d. Índice de retorno cuando coincida.
`` `

-...

## 2.9 Por qué Rolling Hash gana en escenarios de entrevista

- **Minimal per-iteration work** – sólo dos operaciones aritméticas modulares y una asignación de matriz.
- **Separación absoluta de las preocupaciones** – la piratería es un componente autónomo que puede probar de forma independiente.
- **Language‐agnostic** - la misma idea funciona en Python, Java, o C++.
- **Dispone de flujos infinitos naturalmente** – nunca necesitas rebobinar; simplemente sigues deslizando.

-...

### 2.10 Pensamientos de clausura

- **LeetCode 3023** es un *substring-search* disfrazado como un problema de streaming.
- El **bueno** es la claridad y eficiencia de la solución Roll-hash.
- El **bad** es el enfoque ingenuo que ignora el requisito de tiempo constante.
- El **encarecidamente** es el riesgo de colisiones precipitadas o de desbordamiento si no utiliza un módulo o un paso de verificación.

■ **Tu Takeaway** – Mostrar el entrevistador que conoces *ambos* las técnicas de rodaje-hash y KMP, explicar por qué elegiste el primero para un flujo infinito binario, y confirmar la corrección por una comparación rápida byte‐byte. Ese nivel de rigor convierte una “simple búsqueda de subestring” en una respuesta * entrevista estelar*.

-...

### 2.11 TL;DR (One‐Line Summary)

■ “Para LeetCode 3023, utilice un hash binario **rolling** con un módulo y un buffer circular; el algoritmo funciona en el tiempo O(n) y garantiza la corrección incluso con un flujo infinito. ”

-...

### 2.12 Final Note

■ Mantenga este artículo marcado y vuelva a referirse cuando le pidan que busque patrones en la transmisión de datos – ya sea registros binarios, paquetes de red o datos de sensores.
■ Buena suerte, y recuerde: *La entrevista es sólo otra corriente; encontrar el patrón y caminar lejos. *

-...

■ **END OF ARTICLE**
■ (Cuento de palabras: ~1,350 palabras, a medida para un blog de LinkedIn/Coding-Interview.)

-...

## 3. Pensamientos finales

■ Ya sea que usted está codificación en Java, Python, o C++, el enfoque ondulado es una fuente de verdad ** single** para LeetCode 3023.
■ Pásalo con un cheque de colisión y tendrás una solución antibalas que funciona cómodamente bajo el límite de bits de `105`.
■ Y si estás preparando entrevistas de codificación, ten en cuenta el marco **bueno, malo, feo** – te ayudará a presentar una solución concisa y optimizada cada vez.