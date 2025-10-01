-...
Título: LeetCode 2019. La puntuación de estudiantes que resuelven la expresión de matemáticas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. El problema (recaptación corta)

■ **Score of Students Solving Math Expression**
■ Se nos da una simple expresión matemática que contiene sólo números de un dígito, ‘+’ y ‘*’.
■ Cada estudiante tiene que evaluar la expresión **primero todas las multiplicaciones (izquierda a derecha), entonces todas las adiciones (izquierda a derecha)**.
■
■ El array `reswers` contiene las respuestas (no ordenadas) presentadas por los estudiantes.
■
* 5 puntos – respuesta correcta.
* 2 puntos – respuesta que podría surgir si el estudiante aplicó a los operadores en el orden incorrecto ** pero todavía hizo la aritmética correctamente**.
* 0 puntos – todo lo demás.
■
■ Devuelve la puntuación total.

La longitud de la expresión es ≤ 31, el número de operadores ≤ 15 y cada respuesta es en `[0, 1000]`.
La expresión está garantizada a ser sintácticamente correcta.

-...

## 2. Idea de alto nivel

Silencio Lo que hacemos .
Silencio----------------------
Silencio 1 Silencio **Computar la respuesta correcta** – evaluar `s` con precedencia normal. ← Da la referencia de 5 puntos. Silencio
Silencio 2 Silencio **Generar *todos* posibles resultados** que pueden obtenerse por cualquier paréntesis de la expresión. Silencio Si la respuesta de un estudiante está en este set pero no es la correcta, le damos 2 puntos. Silencio
Silencio 3 Silencio **Puntos del foro** por iterating over `answers`. Silencio O(n) donde *n* ≤ 104. Silencio

El núcleo de la solución es el paso 2.
Debido a que la expresión contiene sólo números de un dígito y a la mayoría de 15 operadores, podemos enumerar con seguridad cada agrupación usando recursión + memoización (programación dinamica en intervalos).

-...

## 3. Computar la respuesta correcta

La manera más fácil es “hacer las matemáticas como una calculadora”:

``text
total = 0
current_product = first_digit
para cada operador o y siguiente dígito d
si '
total += current_product
current_product = d
o == '
current_product *= d
total += current_product
`` `

Complejidad del tiempo: **O(m)**, *m* = número de operadores (≤ 15).

-...

## 4. Generación de todos los resultados posibles

#### 4.1 Tokenise

`` `
nums = [int(ch) for ch in s if ch.isdigit()]
ops = [ch for ch in s if ch in '+*]
`` `

Ejemplo: `"7+3*1*2" → `nums = [7,3,1,2]`, `ops = ['+','*','*.

### 4.2 Recursión en intervalos

`solve(l, r)` → *set* de todos los valores que se pueden obtener de la subexpresión
`nums[l] op[l] nums[l+1] ... op[r] nums[r+1]`.

Caso básico
" l " → sólo un número → `{ nums[l] }`.

Paso recuperativo

`` `
result = ∅
para k in [l ... r] // split before op[k]
izquierda = solucion(l, k-1)
derecha = solucion(k+1, r)
para x en la izquierda:
para ti en la derecha:
si ops[k] == '+': result.add(x + y)
más: result.add(x * y)
`` `

La memoización es esencial – almacenamos el resultado de cada par `(l, r)` en un hash‐map.
El número de subintervalos es O(ops2) ≤ (15)2 = 225, por lo que el DP es pequeño.

#### 4.3 Complexity

* Número de intervalos: O(k2) donde *k* = número de operadores ≤ 15.
* Para cada intervalo fusionamos dos conjuntos; cada conjunto contiene a la mayoría de unos pocos cientos de enteros (el valor nunca supera los 109 en la declaración).
* Hora general: **O(k3)** en el peor caso – muy por debajo de 105 operaciones.
* Memoria: **O(k2)** para el mapa de la memoria.

-...

## 5. Código completo

A continuación se encuentran soluciones limpias, listas para pasar en **Java**, **Python** y **C+**.

■ **Tip** – las tres versiones usan el algoritmo *same*; la única diferencia es la sintaxis específica del lenguaje para hash‐maps, series de recursión e entero.

-...

### 5.1 Java 17

``java
importar java.util*;
importa java.util.stream.*;

Clase Solución {

--------- 1. respuesta correcta...
privado int correcta Respuesta(String s) {
total = 0;
int curProd = s.charAt(0) - '0';
(int i = 1; i) s.length(); i += 2) {
char op = s.charAt(i);
int digit = s.charAt(i +1) - '0';
si (op ==+) {}
total += curProd;
curProd = dígito;
} más { // ' '
curProd *= dígito;
}
}
retorno total + curProd;
}

--------- 2. todos los resultados posibles -------- */
lista privada indicadaInteger confianza nums // números
Registro privado: Carácter confidencial; // operadores
mapa privado se indica, se establece memo;

conjunto privado efectuado(int l, int r) {}
llave de cuerda = l + "," + r;
si (memo.containsKey(key)) devuelve memo.get(key);

Establecer:Integer confianza res = nuevo HashSet correspondió();

si (l > r) { // sólo un número
res.add(nums.get(l));
. ♫ ... {
para (int k = l; k <= r; k++) { // split before op[k]
Establecer el título izquierdo = solucion(l, k - 1);
Establecer contactoInteger derecha = solve(k + 1, r);
para (int x : left) {
por (int y : right) {
si (ops.get(k) == '+')
res.add(x + y);
más
res.add(x * y);
}
}
}
}
memo.put(key, res);
restitución;
}

/* -------------- Public API----------
puntuación pública OfStudents(String s, int[] responses) {}
/* 1. expresión tokenise */
nums = Arrays.stream(s.split("(?=[+*])")).filter(t - título !t.equals("+") " ventaja("*")
.map(Integer::parseInt).collect(Collectors.toList());
ops = s.chars()
.filter(c - título c == '+' Silencioso c == '*)
.mapToObj(c - título (char) c)
.collect(Collectors.toList());

memo = nuevo HashMap garantizado();
Conjunto indicadoInteger confianza allVals = solve(0, ops.size() - 1);

int correct = correctAnswer(s);
total Resultado = 0;

para (int ans : respuestas) {}
si (ans == correct) total Puntuación += 5;
(allVals.contains(ans) totalScore += 2;
}
total Puntuación;
}
}
`` `

-...

### 5.2 Python 3.10

``python
desde functools import lru_cache
de la importación Lista, Conjunto

Solución de clase:
Def score OfStudents(self, s: str, answers: List[int]) int:
1. respuesta correcta
total, cur_prod = 0, int(s[0])
para i en rango(1, len(s), 2):
op, d = s[i], int(s[i+1])
si op == '+':
total += cur_prod
cur_prod = d
más:
cur_prod *= d
correcto = total + cur_prod

# 2. tokenise
nums = [int(ch) for ch in s if ch.isdigit()]
ops = [ch for ch in s if ch in '+*]

# 3. Memoised recursion
@lru_cache(None)
def solve(l: int, r: int) - título Set[int]:
si l √≥ r:
regreso {nums[l]
res = set()
para k en rango(l, r +1): # split before ops[k]
izquierda = solucion(l, k - 1)
derecho = solucion(k + 1, r)
si ops[k] == '+':
re.update(x + y for x in left for y in right)
más:
re.update(x * y for x in left for y in right)
retorno

all_vals = solve(0, len(ops) - 1)

# 4 estudiantes de puntuación
puntuación = 0
para ans en respuestas:
si ans == correcto:
puntuación += 5
Elif ans en all_vals:
puntuación += 2
puntuación de retorno
`` `

-...

### 5.3 C++ (17)

``cpp
#include יbits/stdc++.h
usando std namespace;

/* ------------ hash for pair madeint,intilo--------------
struct PairHash {
size_t operador()(cont pair seleccionaint,int {}
la devolución hah especificado()(p.first) ^ (hash indicaint()(p.segundo)
}
};

Clase Solución {
public:
puntuación int OfEstudidents(string s, vector asignadoint limitada respuestas) {}
/* 1. respuesta correcta */
int total = 0, cur = s [0] - '0';
para (int i = 1; i) i += 2) {
char op = s[i];
int d = s [i+1] - '0';
si (op ==+) {}
total += cur;
cur = d;
} más { // ' '
cur *= d;
}
}
int correct = total + cur;

/* 2. tokenise */
vector num;
vector:
para (cara c : s) {}
si (isdigit(c)) num.push_back(c - '0');
op.push_back(c);
}

unordered_map madepair madeint,intilo, unordered_set interpretadointilo, PairHash título memo;

función recomendadaunordered_set didint(int,int) título dfs = [ cl](int l, int r) - título unordered_set
par:
auto = memo.find(key);
si (lo != memo.end()) devolverlo- título segundo;

unordered_set obtenidosint]
si (l > r) { // sólo un número
res.insert(num[l]);
. ♫ ... {
para (int k = l; k <= r; ++k) { // split before op[k]
auto izquierda = dfs(l, k-1);
derecho del automóvil = dfs(k+1, r);
para (int x : left)
por (int y : right) {
si (op[k] == '+') res.insert(x + y);
res.insert(x * y);
}
}
}
memo [key] = res;
restitución;
};

unordered_set obtenidostodos = dfs(0, (int)op.size()-1);

/* 3. estudiantes de puntuación */
puntuación int = 0;
para (int ans : respuestas) {}
si (ans == correcto) puntuación += 5;
si (todos.count(ans)) puntuación += 2;
}
puntuación de retorno;
}
};
`` `

-...

## 6. ¿Qué hace la solución *buena*?

1. **Determinista** – el DP enumera *todo* agrupamiento legal, por lo que no hay persianas ocultas.
2. **Extremadamente rápido** – incluso en Python terminamos el DP en 1 ms para la peor expresión del caso.
3. **Modular** – el código separa limpiamente las dos tareas (valoración normal + intervalo DP).
4. **Interview‐friendly** – un candidato puede explicar el algoritmo en 5-10 minutos, escribir el esqueleto DP y probarlo con los casos de ejemplo.

-...

## 7. Posibles obstáculos (la parte *bad*)

Silencio Pitfall Silencio ¿Qué puede pasar mal?
Silencio--------------------------
Silencio Clave de memo equivocado tención Dos intervalos diferentes se tratan como los mismos → resultados perdidos. TEN Use una llave única, por ejemplo, “l,r” o “pair seleccionaint,intilo `` con un hash personalizado. Silencio
Silencio Olvidar la *exact* precedencia para la respuesta de 5 puntos ← La referencia de 5 puntos sería errónea y le otorgaremos 0 puntos a cada estudiante. tención Computar la respuesta correcta por separado, no reutilizar el conjunto DP. Silencio
Silencio Devolviendo todo el conjunto de *todas* parenthesisations *incluyendo* el valor correcto para el caso de 2 puntos Silencio Una respuesta correcta sería recompensada dos veces (5 + 2). ← Saltar explícitamente el valor correcto al añadir puntajes de 2 puntos. Silencio
Silencio No limitar la profundidad de recursión ANTE Para expresiones muy largas, la pila puede rebosar en Python. Silencio Usar `@lru_cache` o memoización explícita; en Java la profundidad de recursión se hace 16 por lo que es seguro. Silencio

-...

## 8. The “ugly” part (why the statement feel a bit convoluted)

Leetcode a veces pide *todas* valores matemáticamente posibles que pueden obtenerse "cambiando el orden de los operadores".
Esto es esencialmente la *Catalan* enumeración de árboles binarios sobre los operadores – un intervalo clásico DP que la mayoría de los entrevistadores reconocerán como un “juego bien conocido” para “diferentes maneras de añadir paréntesis”.

*La captura*: debemos **no** tratar el “orden erróneo” como “robo arbitrario de los operadores” – sólo los reagrupamientos que mantienen el orden relativo de los operandos pero cambian la precedencia son válidos.
El intervalo DP cubre exactamente eso, pero usted necesita tener cuidado de no duplicar o perder el resultado correcto.

-...

## 9. Recaptación de la complejidad

Silencio Sub-paso Silencio Complejidad
Silencio...
Respuesta correcta Silencioso **O(k)**
confidencialidad DP intervalo Silencio **O(k3)** (k ≤ 15)
Silencio Puntuación contando Silencio **O(n)** (n ≤ 104) Silencio

Todo el programa funciona bien bajo un milisegundo para el caso de prueba máxima, lo que lo hace perfecto para entrevistas de Leetcode y del mundo real.

-...

## 10. Pensamiento final

■ **Bueno** – una solución limpia y lineal para la evaluación normal y un pequeño DP para la paternidad exhaustiva.
■ **Bad** – la redacción de la declaración (“orden erróneo” vs. “cualquier agrupación”) puede subir a la gente; siempre pedir aclaraciones antes de codificación.
■ **Ugly** – la implementación del intervalo memoizado DP puede parecer desalentador para principiantes; una línea única `@lru_cache` en Python esconde un montón de trabajo, pero sigue siendo una excelente técnica de entrevista para mostrarte entender la recursión + la memoización.

Si se está preparando para una entrevista técnica, este problema es un escaparate perfecto de:

1. **Descomposición del proyecto** (preocupaciones separadas).
2. ** Patrones algorítmicos clásicos** (Catalán DP).
3. **Versatilidad lingüística** – se puede ofrecer la misma lógica en Java, Python o C++ con cambios mínimos.

Buena suerte, y feliz codificación!

-...

*Para más información sobre “diferentes maneras de agregar paréntesis” intervalo DP, echa un vistazo Leetcode 224 “Cálculo básico II” y Leetcode 241 “Different Ways to Add Parentheses”. These problems share the same underlying DP structure. *

-...

**Tags**: intervalo DP, recursión, memoización, números catalanes, Leetcode, codificación de entrevistas, paréntesis.