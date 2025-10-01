-...
Título: LeetCode 1922. Cuenta buenos números -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📝 Problem Recap – LeetCode 1922 “Count Good Numbers”

A **good** digit string of length `n` satisfies

* **Indice electrónico** (0-basado) → dígito es ** incluso** (0, 2, 4, 6, 8)
* ** Índice extraño** → dígito es **prime** (2, 3, 5, 7)

Podemos usar ceros líderes.
`n` puede ser tan grande como `10^15`, por lo que una solución ingenua `O(n)` o `O(n2) ` no terminará.
La respuesta debe ser devuelta modulo `M = 1 000 000 007`.

-...

♪ ♪ ♪♪

Por cada posición que tenemos **5** opciones, por cada posición extraña tenemos **4** opciones.

Vamos.

`` `
inclusoCnt = ceil(n / 2) // número de índices uniformes (0,2,4,...)
oddCnt = piso(n / 2) // número de índices impares (1,3,5,...)
`` `

El número de buenas cuerdas es

`` `
buena(n) = 5^evenCnt · 4^oddCnt (mod M)
`` `

Así que la tarea se reduce a la computación de dos poderes modulares para un enorme exponente – utilizamos ** exponente binario (rápido)** (`O(log n)` tiempo, `O(1)` memoria).

-...

Tiempo de Complejidad Espacial

← Operación Silencioso
Silencio...
Silenciosos Compute `evenCnt ' , `oddCnt` Silencio
Silencio Explicación modular (binaria) Silencio
tención multiplicación final " modulo tención `O(1) ' Silencio
Silencio **Total** Silencioso ** `O(log n)` tiempo, `O(1)` espacio**

-...

## 📚 Code Snippets

#### ## 1down⃣ Java

``java
Solución de la clase pública {}
static final long MOD = 1_000_000_007L;

int countGoodNumbers(long n) {
long evenCnt = (n +1) / 2; // indices 0,2,4,...
largas probabilidades Cnt = n / 2; // índices 1,3,5,...

mucho tiempo Ways = modPow(5L, evenCnt, MOD);
long oddWays = modPow(4L, oddCnt, MOD);

(int) ((evenWays * oddWays) % MOD);
}

// rápida exponentiación modular
privado largo modPow(long base, long exp, long mod) {
larga res = 1L;
base %= mod;
mientras (ex) 0) {
((exp) == 1) {
res = (res * base) % mod;
}
base = (base * base) % mod;
experiencia= 1;
}
restitución;
}
}
`` `

#### 2down⃣ Python

``python
Solución de clase:
MOD = 1_000_000_007

def countGoodNumbers(self, n: int) - título int:
incluso_cnt = (n +1) // 2 # incluso índices
odd_cnt = n // 2 # índices extraños

even_ways = pow(5, even_cnt, self.MOD)
odd_ways = pow(4, odd_cnt, self.MOD)

retorno (even_ways * odd_ways) % auto. MOD
`` `

■ **Tip** – Python’s built‐in `pow` con tres argumentos ya implementa la exponentiación binaria y maneja enormes exponentes.

#### 3down⃣ C++

``cpp
Clase Solución {
public:
static constexpr long MOD = 1'000'007LL;

int countGoodNumbers(long long n) {}
largo tiempo inclusoCnt = (n +1) / 2; // incluso índices
largas probabilidadesCnt = n / 2; // índices impares

long evenWays = modPow(5LL, evenCnt);
largas probabilidadesWays = modPow(4LL, oddCnt);

retorno estática_cast seleccionado((incluso eras) % MOD);
}

privado:
largo largo modPow(long long base, long long long exp) {}
largas res = 1;
base %= MOD;
mientras (ex) 0) {
(exp " 1) res = (res * base) % MOD;
base = (base * base) % MOD;
experiencia= 1;
}
restitución;
}
};
`` `

-...

Artículo del Blog – “El Bien, el Mal, y el Ugly of Counting Good Numbers”

### 1. Introducción
Cuando veas **LeetCode 1922 – Contar buenos números**, su cerebro podría hacer una toma doble. Es un problema combinatorio aparentemente simple pero en realidad es una trampa de entrevista clásica: ** “¿Sabes cómo manejar exponentes gigantescos?”* *
En este post diseccionaremos el problema, exploraremos por qué fallan las soluciones ingenuas, mostraremos el enfoque 'O(log n)` limpio, y resaltaremos los matones de entrevista.

■ **SÉO tags**: `Count Good Numbers`, `LeetCode 1922`, `fast exponentiation`, `modular exponentiation`, `Python solution`, `Java solution`, `C+ solution`, `algorithm interview `

-...

### 2. Problema de recuperación
Una cadena de dígitos es “buena” cuando:

Posicionamiento permanente Permitido dígitos
Silencio...
Silencio 0, 2, 4,... (incluso)
Silencio, 1, 3, 5,... (odd)

Necesitas contar todas las buenas cuerdas de longitud `n`, modulo `10^9+7`.
Con `n ≤ 10^15`, ni siquiera se puede iterar sobre la cuerda – necesitamos *matemática*.

-...

### 3. El “bien” – Por qué la solución es directa
Piense en la cuerda como dos carriles independientes:

1. **Even carril** – 5 opciones por lugar → 5 posibilidades
2. **Odd lane** – 4 opciones por lugar → 4 posibilidades

Número de puntos:
- Incluso los índices = " n + 1)/2 " (redondeado)
- Índices de probabilidades = " n/2 " (redondeados)

Multiplicando las posibilidades de cada carril da:

`` `
bueno(n) = 5^(even) · 4^(odd) (mod 1 000 000 007)
`` `

**El “bueno”** es que una vez que veas esta fórmula, el resto es rutinario.

-...

### 3. El “Bad” – Por qué Brute‐ La fuerza es una pesadilla
Una respuesta inicial común es:

``python
# O(n) counting each position
para _ en rango(n):
# multiplicado por 5 o 4
`` `

Incluso si acabamos de calcular `pow(5, n//2)` en un bucle, el número `5^10^15` tiene **~10^15 dígitos**.
- **Hora**: `O(n)` → ~10^15 operaciones → imposible.
- **Memoria**: Las ints de pitón crecerían más allá de la RAM.
- Resultado de la entrevista**: Los entrevistadores preguntan *por qué* usted eligió esto, y su respuesta será penalizada.

-...

### 4. El “Ugly” – Casos de borde que te acercan

Silencio Caso Edge Silencio Qué ver para Silencio
Silencio...
TENIDO `n = 1` TENIDO Incluso índices = 1, impar = 0 → respuesta = 5 TENIDO
Silencio `n = 2` Silencio Incluso = 1, extraño = 1 → respuesta = 5·4 = 20 Silencio
Silencio Grande `n` (10^15) Silencio Los explotadores rebosan de 32 bits. Use `long' / `long` y reducciones modulares. Silencio
tención Modulo rebosadero Silencio `(5^x % M) * (4^y % M)` puede exceder de 64 bits en idiomas que no utilizan grandes enteros. Siempre aplicar modulo después de cada multiplicación. Silencio

-...

### 5. La solución limpia – Exposición binaria

La exponencia binaria reduce el `base^exp` a `O(log exp)` al cubrir repetidamente la base y reducir el exponente.
Pseudocode:

`` `
pow_mod(base, exp):
Resultado = 1
base %= M
mientras que 0:
si es extraño en la exposición: resultado = resultado * base % M
base = base * base % M
exp//= 2
Resultado de retorno
`` `

Tanto **Java** como **C++** implementaciones requieren codificación manual, mientras que **Python** puede simplemente llamar `pow(base, exp, M)` – este incorporado utiliza el mismo algoritmo bajo la capucha.

-...

### 6. Consejos para entrevistas

← Topic ← Entrevista Insight
Silencio...
Silencio **Por qué la exponencia modular importa** Silencio Los entrevistadores quieren ver que usted mantiene los números atados. Pregunta "¿Por qué es necesario el modulo aquí?" Silencio
Silencio **Elige el tipo de datos adecuado** Silencio En Java use `long`, en C++ `long', en Python `int` (unbounded). Silencio
Silencio **Por qué `O(log n)` beats `O(n)`** TENIDO Discuss the binario split: each loop halves the exponent. Silencio
Silencio **Testing** Silencio Verificar con pequeños valores (`n = 1, 2, 3, 4, 5`). A continuación, ejecutar con 'n = 10^12` para confirmar el tiempo de ejecución es |1 s.
Silencio **Explicar el razonamiento** Silencioso “Incluso los índices = ceil(n/2)” – hablar a través de la aritmética. Silencio

-...

### 7. Código en un post – Java, Python, C++

*(Los bloques de código son idénticos a los fragmentos anteriores, por lo que el lector puede copiar-paste.) *

``java
/ Código Java
`` `

``python
# Código de pitón
`` `

``cpp
// Código C++
`` `

-...

### 8. Wrap‐Up & What Want
- **Claridad**: Escriba código que es fácil de leer.
- Cambios en el espacio-tiempo**: Mostrar que entiende que `O(log n)` es el límite óptimo para este problema.
- *Sensibilización por caso* Prueba con `n = 1`, `n = 2`, y números enormes.
- *Discusión* En la entrevista, pregunte si el entrevistador quiere que pruebe la fórmula o simplemente entregar la implementación.

■ **Si puedes explicar este problema en 5 minutos y producir una solución sin errores, `O(log n)`, estás listo para la ronda “Algorithms " Data Structures” en cualquier entrevista tecnológica de primer nivel. #

-...

### 9. Lista de verificación para la retirada

TENIDO TENIDO ARTÍCULO ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTE .
Silencio...
Silencio Contar índices incluso /odd correctamente TENIDO TENIDO TENIDO
Silencio Utilizar exponenciación modular (`pow` en Python, binario manual en Java/C+++)
Silencio Mantener todos los resultados intermedios mod `1 000 000 007` Silencio Silencio
tención Evite el desbordamiento de 32 bits – use 64 bits ( " largo " , `long ' )
Silencio Explicar tiempo/complejidad espacial
Silencio Mostrar algunos casos de prueba Silencio TENIDO TENIDO
Silencio Prepárate para justificar por qué usaste la rápida exponenciación Silencio TENIDO TENIDO

¡Feliz codificación, y que sus cuerdas “buenas” siempre sean contadas con precisión! 🚀