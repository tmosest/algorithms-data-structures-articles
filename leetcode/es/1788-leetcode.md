-...
Título: LeetCode 1788. Maximizar la Belleza del Jardín -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1788. Maximizar la belleza del jardín
**Hard – LeetCode** Silencio **Java / Python / C++** Silencio ** Interview‐Ready**

-...

# Blog Title
**“Maximizar la belleza del jardín – 1788 LeetCode: Una solución de 3 idiomas (Java, Python, C++)”* *

■ **SEO Palabras clave** – LeetCode 1788, Maximizar la belleza del jardín, problema del jardín, suma prefijo, programación dinámica, entrevista de codificación, solución Java, solución Python, solución C++, desafío de codificación de entrevistas de trabajo

-...

## 1. Panorama general de los problemas

Se le da un array `flores` de longitud `n` (`2 ≤ n ≤ 105`).
Cada elemento es el valor de belleza de una flor y puede ser negativo.
Usted puede eliminar cualquier número de flores (incluyendo ninguna).
Después de las eliminaciones debe tener un jardín **válido**:

1. Al menos dos flores permanecen.
2. La primera y última flor en la secuencia restante tiene el valor de belleza ** igual**.

La belleza de un jardín es la suma de todas las flores restantes.
Devuelve el **maximum** posible belleza de cualquier jardín válido.

-...

## 2. Intuición – “La primera y última materia”

Sólo el primero y último elemento de la subsequencia elegida influyen en la viabilidad del jardín.
Todo en medio puede ser mantenido o eliminado libremente.

*Si guardamos una flor positiva entre los dos extremos iguales, obtenemos valor; si es negativa, podemos dejarla sin dañar la belleza. *

De ahí que la estrategia óptima sea:

1. Elige un valor.
2. Mantenga la ocurrencia **primero** de `v` como el extremo izquierdo.
3. Mantenga la ocurrencia **última** de `v` como el extremo derecho.
4. Mantenga todas las flores positivas estrictamente entre esas dos posiciones.

Esto produce la máxima belleza para ese valor particular `v`.
Necesitamos probar cada valor distinto y tomar el mejor resultado.

-...

## 3. Algorithm (O(n) time, O(n) space)

TEN TERRITORIO ANTERIOR ANTERIOR
Silencio...
Silencio **1** Silencioso Scan `flores` una vez para registrar por cada valor su primer y último índice. Silencio
Silencio **2** Silencio Compute a prefix array `pref[i]` = sum of **positive** flowers up to index `i` (inclusive). Silencio
Silencio **3** Silencio Por cada valor que aparece al menos dos veces ( " última palabra " ):
`Beauty = 2 * v + (pref[last-1] - pref[first])` Silencio
Silencio **4** Silencio Mantener el máximo de todas esas bellezas. Silencio

*Por qué la fórmula funciona*
`pref[last-1] - pref[first]` equivale a la suma de flores positivas estrictamente entre las dos ocurrencias.
Añadiendo `2 * v` representa las dos flores de extremo igual.
Las flores negativas en el intervalo son simplemente ignoradas.

-...

## 4. Casos de borde

Silencio Silencio Silencioso
Silencio...
Silencio **Sólo una ocurrencia de un valor** Silencio No puede formar un jardín válido → saltar. Silencio
Silencio **Todas las flores negativas** Silencio Todavía debe mantener dos negativos iguales. La fórmula maneja esto porque la suma prefijo entre ellos es 0. Silencio
Silencio **Todo positivo** Silencio El mejor jardín es toda la matriz (primero y último son el mismo valor, típicamente el máximo). Silencio

-...

## 5. Aplicación del Código

A continuación se presentan implementaciones limpias y listas de producción en **Java, Python y C++**.
Los tres utilizan la misma lógica O(n) y manejan los límites enteros de 32 bits de forma segura mediante el uso de 'long'/`long' para sumas.

### 5.1 Java

``java
importar java.util*;

Clase Solución {
int maximumBeauty(int[] flowers) {}
int n = flores. longitud;

// 1. Registro de primera y última ocurrencia de cada valor
Mapa seleccionadoInteger, Integer primero = nuevo HashMap fiel();
Mapa seleccionadoInteger, Integer confianza last = new HashMap Quería();
para (int i = 0; i)
int v = flores[i];
(!first.containsKey(v))) first.put(v, i);
último.put(v, i); // mantiene el último índice
}

// 2. Resumo prefijo de valores positivos
long[] pref = new long[n];
pref[0] = Math.max(0, flowers[0]);
para (int i = 1; i) {}
pref[i] = pref[i - 1] + Math.max(0, flowers[i]);
}

mucho mejor = Long.MIN_VALUE;

// 3. Pruebe cada valor que ocurre al menos dos veces
para (int v : first.keySet()) {
int l = first.get(v);
int r = last.get(v);
si (l == r) continuar; // necesita al menos dos flores

largo medio = pref[r - 1] - pref[l]; // positivos entre l y r
candidato largo = 2L * v + medio;
mejor = Math.max(mejor, candidato);
}

retorno (int) mejor; // resultado se ajusta en int por limitaciones de problemas
}
}
`` `

### 5.2 Python

``python
de la importación Lista
de las colecciones importadas por defecto

Solución de clase:
def maximumBeauty(self, flowers: List[int] - int:
n = len(flores)

# First and last indices
primero
último = {}
para i, v en enumerado(flores):
si no en el primero:
primero [v] = i
último [v] = i

# prefijo suma de positivos
* n
pref[0] = max(0, flowers[0]
para i en rango(1, n):
pref[i] = pref[i - 1] + max(0, flowers[i]

mejor = flotante('-inf')

para v en el primero:
l, r = first[v], last[v]
si l == r:
continuar
media = pref[r] - pref[l]
candidato = 2 * v + medio
mejor = max(best, candidate)

mejor
`` `

### 5.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maximumBeauty(vector fieltro flores) {}
int n = flowers.size();

unordered_map observadoint, int título primero, último;
para (int i = 0; i) {}
int v = flores[i];
if (!first.count(v))) first[v] = i; // first occurrence
última [v] = i; // última (última) ocurrencia
}

vector realizado largo tiempo pref(n);
pref[0] = max(0LL, flowers[0]);
para (int i = 1; i) {}
pref[i] = pref[i-1] + max(0LL, flowers[i]);
}

largo tiempo mejor = LLONG_MIN;

para (const auto &kv : primero) {
int v = kv.first;
int l = kv.second;
int r = last[v];
si (l == r) continuar; // necesita dos flores

long long long middle = pref[r-1] - pref[l];
caño largo = 2LL * v + medio;
mejor = max(best, cand);
}

volver estática_cast seleccionado(best);
}
};
`` `

Los tres códigos se ejecutan en **tiempo lineal** (`O(n)`) y utilizan ** espacio auxiliar lineal** (`O(n)`).

-...

## 6. Análisis de la complejidad

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
Silencio ** Tiempo** Silencioso `O(n)` Silencio `O(n)` Silencio `O(n)` Silencio
Silencio **Espacio** Silencioso `O(n)` (dos mapas + array prefijo) Silencio `O(n)` Silencio `O(n)` Silencio
Silencio **Por qué es aceptable** Silencio `n ≤ 105`, `duranteflores[i] sueño ≤ 104` → sumas ≤ 109, encajado de forma segura en el entero firmado de 32 bits. Silencio

-...

## 7. “Bueno, malo, “muy” de la solución

Silencio Silencio
Silencio------------Prince------
Silencio **Bien** Silencio • Paso único, sin recidiva. • Maneja los valores negativos elegantemente. • Usa sólo contenedores incorporados → rápido & de memoria. Silencio
Silencio **Bad** Silencio • Requiere escanear el array dos veces (una vez para índices, una vez para prefijo). • Necesita dos mapas de hash – un poco más de memoria de lo estrictamente necesario. Silencio
Silencio **Ugly** Silencio • Algunas soluciones ingenuas (por ejemplo, “pick any two equal end and sum everything”) accidentalmente añadir números negativos en el medio, dando resultados sub-optimal. Se acerca el DP Recursive que intenta evaluar cada subsequencia explota a tiempo exponencial en esta escala. Silencio

-...

## 8. Enfoques alternativos " Por qué los evitamos

1. **Brute Force (O(n2))** – Enumerar cada par de valores iguales y sumar los positivos entre. Demasiado lento para 'n = 105'.
2. ** Programación Dinámica (DP)** – El problema es *no* un DP clásico (no hay estructura de subproblema superpuesta) – el uso de DP sólo agregaría complejidad innecesaria.
3. ** Árbol de segmento / Árbol de Indización binaria** – Sobrekill; sumas prefijo ya dan consultas de rango de tiempo constante.

Por lo tanto, el prefijo-sum + el primer/último truco es el lugar dulce.

-...

## 9. Cómo explicar Esto a los entrevistadores

■ **Cuando se le preguntó "¿Cómo resolvería LeetCode 1788?", se puede decir:**
■
*“Me di cuenta de que sólo importan los primeros y últimos elementos. Grabé para cada valor de belleza el primer y último índice. Luego construí una suma prefijo de sólo flores positivas, que me permite calcular la mejor suma entre dos extremos iguales en O(1). Por último, me entero de todos los valores que ocurren al menos dos veces y mantener el máximo. El algoritmo es O(n) y utiliza espacio extra O(n) – perfecto para 105 elementos.”*

Esta explicación concisa muestra que usted puede **abstractar el problema**, detectar un **pattern**, y aplicar una técnica **claro O(n)** – exactamente lo que los entrevistadores buscan.

-...

## 10. Pensamientos finales – Tu próxima entrevista

- **Práctica**: Implementar esta solución en tu idioma favorito desde cero.
- **Timing**: Ejecute contra 105 casos aleatorios para convencerse de su linealidad.
- **Explicar**: Prepárate para discutir el truco “positivo sólo prefijo” – esa es la visión clave.

Dominar este problema te da un patrón poderoso: *“Cuando sólo las condiciones fronterizas importan, mantengan los extremos e incluyan los positivos dentro.”*
Aplíquelo a problemas de subsequencia similares que encontrará en entrevistas reales.

-...

#### 🚀 Takeaway

- **LeetCode 1788** es solvable en * tiempo lineal* con *refix sums*.
- La misma lógica se traduce en **Java, Python y C+** con un mínimo esfuerzo.
- Comprender la intuición detrás de “primero” le permite explicar la solución con fluidez en una entrevista de codificación, aumentando su confianza y puntuación.

Feliz codificación, y que su trabajo entrevista jardín siempre sea *bello*!