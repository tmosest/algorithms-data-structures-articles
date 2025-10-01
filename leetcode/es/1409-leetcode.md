-...
Título: LeetCode 1409. Consultas sobre una permutación con llave -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🎯 LeetCode 1409 – “Preguntas sobre una permutación con llave”
■ **Emergido público:** Desarrolladores Front-end / Back-end, entusiastas de la estructura de datos, amantes de la preparación de entrevista
■ ** Objetivo:** Entregar código limpio, bien comunicado en **Java, Python, y C++** + un **SEO-friendly artículo del blog** que muestra su problema resolver picas y le ayuda a conseguir su próximo papel de ingeniería de software.

-...

## Tabla de contenidos
Silencio Sección Silencio Lo que aprenderás
Silencio...
Silencio | Problema Declaración Silencio Entender los requisitos exactos
Por qué la solución importa
← Brute‐Force Approach ← Intuitive but still efficient for LeetCode Silencio
TENIDO 🚀 Optimal (Fenwick Tree) Silencio O(n log m) solución – perfecto para entrevistas Silencio
TEN | Código Snippets ANTE Java, Python, C++ – listo para copiar " paste ANTE
Silencio 📝 Blog Artículo Silencioso “El Bien, el Mal y el Ugly” – un SEO-optimizado escritura arriba
Silencio 🎯 Take‐aways Silencio Lo que los reclutadores quieren ver

-...

Problema Recap

Dado:

* Un array `queries` – cada elemento  Iberia [1, m].
* Una permutación inicial `P = [1, 2, ..., m]`.

Por cada consulta `q = consultas[i]`:

1. Encuentre el índice 0-basado de `q` en `P`.
2. Mover `q` al frente de `P`.
3. Registre el índice antes del movimiento.

Devuelve la matriz de índices registrados.

■ **Constraints**
≤ 103
Ø • `1 ≤ consultas.length ≤ m `
≤ m `

-...

## 2down Por qué este problema es un “Gold‐Mine” para entrevistas

Silencio Lo que los reclutadores se preocupan por Silencio Cómo este problema lo demuestra
Silencio...
Silencio **Data‐structure knowledge** Silencio Usted utiliza permutaciones, indexación y opcionalmente árboles Fenwick. Silencio
Silencio ** Pensamiento algorítmico** Silencio Usted identifica una ingenua solución O(n2) vs. Silencio
Silencio **Estilo de codificación > comentarios** Silencio Código limpio y legible con manipulación de bordes. Silencio
Silencio **Tiempo-espacio-offs** Silencio Usted habla cuando un enfoque simple es aceptable. Silencio
TEN **Problema-solving under constraints** TEN m ≤ 1000 → brute‐force OK; pero todavía muestra un método escalable. Silencio

-...

## 3down Bru Brute‐Force (Intuitive) Solution

#### ## ### #######################################################################################################################################################################################################################################################
* **Tiempo:** O(n × m) (caso inferior 1 000 × 1 000 = 106 operaciones – perfectamente bien para LeetCode).
* **Espacio:** O(1) extra (además de la salida).

### 📌 Java Implementation

``java
Solución de la clase pública {}
int[] processQueries(int[] consultas, int m) {
int[] perm = nuevo int[m];
para (int i = 0; i)

int[] result = nuevo int[queries.length];

para (int idx = 0; idx) {}
int q = consultas[idx];
int pos = 0;
// encontrar índice
para (int i = 0; i)
si (perm[i] == q) {
pos = i;
ruptura;
}
}
result[idx] = pos;

// pasar al frente (los elementos de desplazamiento derecha)
int temp = perm[pos];
para (int i = pos; i > 0; i--) perm[i] = perm[i - 1];
perm[0] = temp;
}
Resultado de retorno;
}
}
`` `

### 📌 Python Implementation

``python
Solución de clase:
def process Queries(self, queries: List[int], m: int) - List[int]:
perm = list(range(1, m + 1))
res = []

para q en consultas:
pos = perm.index(q) # O(m) search
re.append(pos)
perm.pop(pos) # O(m) shift
perm.insert(0, q) # O(m) shift
retorno
`` `

### 📌 C++ Implementation

``cpp
Clase Solución {
public:
vector implicado procesoQueries(vector fieltro consultas, int m) {
vector:
iota(perm.begin(), perm.end(), 1); //

vector res;
para (int q : consultas) {
int pos = find(perm.begin(), perm.end(), q) - perm.begin();
res.push_back(pos);
int val = perm[pos];
perm.erase(perm.begin() + pos); // turno izquierda
perm.insert(perm.begin(), val); // shift right
}
restitución;
}
};
`` `

■ ¿Por qué es aceptable? * *
■ Las limitaciones son pequeñas (`m ≤ 1000`). Incluso con un bucle anidado, el tiempo de ejecución se mantiene muy por debajo de 100 ms en LeetCode.

-...

## 4VIEW⃣ Solución Optimal – Fenwick Tree (Binary Indexed Tree)

Cuando `m` crece (por ejemplo, 105 o 106), la solución ingenua se vuelve demasiado lenta.
A **Fenwick Tree** nos permite mantener las posiciones actuales de permutación y actualizarlas en **O(log m)** tiempo.

### Cómo funciona

1. **Mapping**
* Colocar cada número en una posición “virtual” `m + i’ (para que los índices nunca se vuelvan negativos).
* Mantener un árbol de Fenwick sobre el tamaño `2m` para rastrear cuántos elementos están actualmente delante de cada índice.

2. ** Pregunta**
* El índice actual de un número `x` es la suma de prefijo hasta su posición actual - que es el número de elementos que tiene ante sí.

3. # Muévete al frente #
* Establecer el valor del árbol en la posición actual a `0`.
* Colocar el elemento en la siguiente ranura gratuita “front” (comenzando desde `m`) y establecer su valor de árbol a `1`.
* Actualizar `pos[x]` a la nueva ranura.

#### ## ### #######################################################################################################################################################################################################################################################
* **Tiempo:** O(n + m) log m)
* **Espacio*

### 📌 Java Implementation (Fenwick)

``java
clase Fenwick {}
int[] bit;
int n;
Fenwick(int n) { this.n = n; bit = new int[n + 2]; }

vacío add(int idx, int val) {
para (int i = idx; i i " i) bit[i] += val;
}
int sum(int idx) {}
int s = 0;
para (int i = idx; i 0; i -= i ' i) s += bit[i];
retorno s;
}
}

Clase Solución {
int[] processQueries(int[] consultas, int m) {
int[] res = nuevo int[queries.length];
int[] pos = nuevo int[m + 1]; // posición actual de cada valor
int size = 2 * m; // para evitar índices negativos
Fenwick ft = nuevo Fenwick(size + 2);

// inicializar: todos los elementos de la mitad derecha [m+1 .. 2m]
para (int i = 1; i) =
pos[i] = m + i;
ft.add(pos[i], 1);
}

int front = m; // next free front slot
para (int i = 0; i) hice consultas.length; i++) {
int x = consultas[i];
int curPos = pos[x];
int idx = ft.sum(curPos - 1); // elementos antes de x
res[i] = idx;

// moverse hacia delante
ft.add(curPos, -1); // quitar de la ranura vieja
ft.add(front, 1); // añadir a la nueva ranura delantera
pos[x] = frontal;
frente... // la próxima consulta irá incluso antes
}
restitución;
}
}
`` `

### 📌 Python Implementation (Fenwick)

``python
clase Fenwick:
def __init__(self, n):
self.n = n
self.bit = [0]*(n+2)
def add(self, i, delta):
mientras que yo...
auto.bit[i] += delta
i += i
def sum(self, i):
S = 0
mientras yo:
s += self.bit[i]
I -= i
retorno s

Solución de clase:
def process Queries(self, queries: List[int], m: int) - List[int]:
n = len(queries)
tamaño = 2*m
pos = [0]*(m+1)
ft = Fenwick(size+2)

para i en rango(1, m+1):
pos[i] = m + i
ft.add(pos[i], 1)

frente = m
res = []
para x en consultas:
cur = pos[x]
idx = ft.sum(cur-1)
re.append(idx)
ft.add(cur, -1)
ft.add(front, 1)
pos[x] = front
delantera -= 1
retorno
`` `

### 📌 C++ Implementación (Fenwick)

``cpp
struct Fenwick {}
vector significado bit;
int n;
Fenwick(int n=0){init(n);}
vacío init(int n){this- tituladan=n; bit.assign(n+2,0);}
vacío add(int idx,int val){
for(; idx obtenidos=n; idx+=idx curva-idx) bit[idx]+=val;
}
int sum(int idx){
int s=0;
for(; idx confianza0; idx-=idx cosecha-idx) s+=bit[idx];
retorno s;
}
};

Clase Solución {
public:
vector implicado procesoQueries(vector fieltro consultas, int m) {
int sz = 2*m;
Fenwick ft(sz+2);
vector implicado pos(m+1), res;
para(int i=1;i
pos[i] = m + i;
ft.add(pos[i],1);
}
int front = m;
para(int x: consultas) {}
int cur = pos[x];
int idx = ft.sum(cur-1);
res.push_back(idx);
ft.add(cur,-1);
ft.add(front,1);
pos[x] = frontal;
frente...
}
restitución;
}
};
`` `

■ ¿Cuándo deberías escoger esto? * *
√≥n • `m` √≥ 105
* Usted quiere un O(log m) garantizado por consulta (por ejemplo, para sistemas de streaming).
• Demuestra conocimiento profundo del TBI.

-...

## 5down El "Good-Enough" Trade‐off

Silencio Escenario Silencio Preferente Solución
Silencio--------------------
TENIDO `m ≤ 103` TENIDO Brute‐force Silencio Código más simple, menos líneas, más fácil de explicar. Silencio
Silencio `m` crece o quieres mostrar la escalabilidad TEN Fenwick TENED muestra profundidad algorítmica. Silencio
Silencio Usted está entrevistando para un *coding‐heavy* papel Silencio Brute‐force Silencio El entrevistador se centra en la corrección " claridad de código. Silencio
Silencio Usted está en una entrevista *sistemas* Silencio Fenwick ← Limitaciones del mundo real. Silencio

■ **Tip:**
■ Comience con la fuerza bruta, explique su complejidad, a continuación, "leche" al entrevistador si se necesita un método más eficiente. Esto muestra humildad y adaptabilidad.

-...

## 6down Ed Edge‐ Caso " robo " Checks

Silencio Caso Edge Silencio Lo que manejamos en el código
Silencio----------------
← Duplicar consultas Silencio No hay problema – simplemente movemos el mismo número de nuevo. Silencio
Silencio Consultar el elemento frontal tención Índice = 0, las operaciones de árboles eliminan y vuelven a activar la misma ranura – todavía O(log m). Silencio
tención más pequeña `m` (1) Silencio `perm.index(1)` devuelve 0; moverlo al frente no hace nada - todavía funciona. Silencio

-...

Pensamientos finales

* **Mostrar una solución simple** – demuestra que puede traducir una declaración de problema en código inmediatamente.
* **Entonces, “sabe el bar”** – presente una alternativa O(n log n), discutiendo cuando importa.
* **Explicar las compensaciones** claramente: por qué las limitaciones permiten una fuerza bruta, pero un método escalable muestra una visión más profunda.
* **Mantenga su código limpio** – use nombres variables significativos, comentar la lógica Fenwick y el formato consistentemente.

■ **Pro tip for your interview**:
■ *Pregunte al entrevistador, “Si ‘m’ fuera 105, ¿quieres todavía el mismo enfoque?”*
■ Esto inicia una conversación sobre la complejidad del tiempo y muestra su capacidad de pensar en escalar.

-...

¿Listo para escribir la siguiente solución ganadora?

Siéntase libre de copiar/pasar los fragmentos de código arriba en LeetCode.
Si desea practicar más, intente modificar el problema:
* **Variante** – en lugar de moverse hacia delante, moverse hacia el medio.
* **Siguiente** – computar la permutación después de todas las consultas.

¡Feliz codificación! 🚀

-...

*Preparado por **[Su nombre]** – Data‐Structure Enthusiast, Programador Competitivo y Entrenador de Entrevista. *
-...
"
**“Tu mejor entrevista de código no es sobre la respuesta, sino sobre el proceso de pensamiento.”* *
■/bloqueo

-...

#### 📚 Más lectura

1. Fenwick Tree – ■ https://cp-algorithms.com/data_structures/fenwick.html
2. Indización binaria Árbol sobre permutaciones – Identificado https://codeforces.com/blog/entry/79354
3. Uso de " yota " en C++ – " , " https://en.cppreference.com/w/cpp/algorithm/iota confianza "

¡Feliz aprendizaje! .
-...

End of Solution**.