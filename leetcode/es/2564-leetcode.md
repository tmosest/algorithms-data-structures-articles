-...
Título: LeetCode 2564. Substring XOR Queries -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## Substring XOR Queries – LeetCode 2564
*Master el truco bit-wise, escribir código limpio en Java, Python y C+++, y obtener el blog-up listo que es SEO-friendly para los reclutadores. *

-...

### 1. Recaptación de problemas

Silencio ¿Por qué?
Silencio...
Silencio ** Entrada** Silenciosa cuerda binaria `s` (≤ 104) y `preguntas[i] = [primer, segundoi] `` (≤ 105)
Silencio **Task** Silencio Para cada consulta encontrar la subestring *shortest* de `s` cuyo valor decimal `val` satisfies `val ^ firsti == secondi`. ←
Silencio ** Salida** Silencioso `[lefti, righti]` (0-basado) o `[-1,-1]` si no existe subestring. Si múltiples respuestas, escoge el que tiene el más pequeño `lefti`. Silencio

■ **¿Por qué es “difícil” para los reclutadores? #
■ Prueba álgebra bit-wise, trucos prefijo, y una buena comprensión de *hash‐map* espacio-time trade‐offs.

-...

### 2. La visión básica

1. `val ^ first == segundo → val = primer ^ segundo `
Así que cada consulta se reduce a *“encontra un subestring con valor decimal `target = primero ^ segundo.”*

2. La cadena binaria tiene al máximo **30** bits que pueden ser representados por un entero de 32 bits.
→ Para cada posición inicial sólo necesitamos examinar en la mayoría de los próximos 30 caracteres.
Esto mantiene el preprocesamiento O(n · 30).

3. Sólo necesitamos la ocurrencia *primera* (izquierda) de cada valor.
→ Guardar un solo par `[start, end]` por valor en un hash‐map.

4. **Cerrar ceros** – una subestring que comienza con `0` y es más de 1 tiene un valor de 0.
Lo tratamos como un único caso especial: almacenamos `[i,i]` por valor 0 una vez, y luego saltamos más de las subestrings "0...0".

-...

### 3. Algoritm

`` `
preproceso(s):
mapa = {}
para l en 0 ... n-1:
si s[l] == '0':
map.setdefault(0, (l,l))
continuar
val = 0
para ... min(n-1, l+29):
val = (valo se hizo 1) Silencio (s[r] - '0')
mapa.setdefault(val, (l,r))

respuesta (preguntas):
res = []
para primero, segundo en consultas:
objetivo = primer ^ segundo
if target in map:
re.append(map[target])
más:
re.append(-1,-1))
retorno
`` `

*Tiempo* = O(n · 30 + q) Silencio *Espacio* = O(n · 30) (caso inferior ♥ 3 × 105 entradas).

-...

### 4. Implementaciones de referencia

#### 4.1 Java (estilo LeetCode)

``java
importar java.util*;

Clase Solución {
int[][] substringXorQueries(String s, int[][] consultas) {
Mapa realizadoInteger, int[] Confeccionar mp = nuevo HashMap garantizado();
int n = s.length();

para (int l = 0; l ' il; n; l++) {}
si (s.charAt(l) == '0') { // sólo valor 0 es válido
mp.putIfAbsent(0, new int[]{l, l});
continuar;
}
int val = 0;
para (int r = l; r)
val = (valo se hizo 1) Silencio (s.charAt(r) - '0');
mp.putIfAbsent(val, new int[]{l, r});
}
}

int[][] ans = nuevo int[queries.length][2];
para (int i = 0; i) hice consultas.length; i++) {
int target = consultas[i][0] ^ consultas[i][1];
int[] par = mp.getOrDefault(target, new int[]{-1, -1});
ans[i][0] = par[0];
ans[i][1] = par[1];
}
devolver los ans;
}
}
`` `

##### 4.2 Python 3

``python
Solución de clase:
def substring XorQueries(self, s: str, queries: List[List[int]) - No. List[List[int]]:
mp = {}
n = len(s)

para l en rango(n):
si s[l] == '0':
mp.setdefault(0, (l, l))
continuar
val = 0
para r en rango(l, min(n, l + 30)):
val = (valo) realizado 1) tención int(s[r])
mp.setdefault(val, (l, r))

res = []
para primero, segundo en consultas:
objetivo = primer ^ segundo
re.append(list(mp.get(target, (-1, -1))))
retorno
`` `

##### 4.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector de vectores subestring XorQueries(cadenamiento s, vector seleccionadovector seleccionado) {}
unordered_map buscadoint, par obtenidos,int mp;
int n = s.size();

para (incluido l = 0; l) {}
si (s[l] == '0') { // sólo se permite el valor 0
mp.emplace(0, make_pair(l, l));
continuar;
}
int val = 0;
para (int r = l; r)
val = (valo 0) 1) Silencio (s[r] - '0');
mp.emplace(val, make_pair(l, r));
}
}

vector realizador:
ans.reserve(queries.size());
para (auto &q : consultas) {}
int target = q[0] ^ q[1];
auto = mp.find(target);
si (lo != mp.end())
ans.push_back({it- valesecond.first, it- Confsec.second});
más
ans.push_back({-1, -1});
}
devolver los ans;
}
};
`` `

■ **Nota:** `emplace` with `operator[]` se comporta como 'putIfAbsent` – mantiene el par *izquierda-más*.

-...

### 5. Blog‐Ready Write‐ Arriba

■ **Descripción de los datos (conjuntos 155 chars)* *
■ “Solve LeetCode 2564 Substring XOR Consultas en Java, Python & C++. Solución hash-map de 30 bits, consejos de entrevista, truco de bitwise & guía amigable SEO para reclutadores. ”

-...

## Substring XOR Queries – The Interview‐Ready Guide
*(SEO keywords: **Substring XOR Queries**, **LeetCode 2564**, ** string binario XOR**, **hashmap solution**, **bitwise interview problem**)*

## Tabla de contenidos
1. Lo que el problema es
2. La visión ganadora
3. ¿Por qué es el favorito de un reclutador
4. Algoritm detallado & Complejidad
5. Código de referencia (Java / Python / C++)
6. “Bueno, malo” – Una crítica Toma.
7. Cómo marco este problema en un resumen/entrevista
8. FAQs & Edge Cases

-...

##### 1. Qué es el problema

LeetCode 2564 te pide que busques un valor decimal dentro de una cadena binaria** que satisface una simple ecuación XOR.
Es un clásico *bit-wise algebra* + *hash‐map* problema que a muchos entrevistadores les encanta lanzar a los candidatos.

■ *Key Take-away*
■ Convertir cada consulta en un *single integer target* (`first ^ second`) y luego preguntar: “¿Contiene una subestring con este valor? ”

-...

##### 2. La visión ganadora

insight ← Impacto Práctico
Silencio...
Silencio `val = primero ^ segundo` Silencio Cada consulta es un **lookup** – no hay necesidad de examinar la cuerda en el momento de la consulta. Silencio
Silencio Valor de cadena binaria encaja en **30 bits** Silencio Sólo examinamos en la mayoría de 30 chars por inicio → **O(n · 30)** preprocesamiento. Silencio
Silencio Sólo el **primer** (izquierda) ocurrencia importa ¦ Almacenar un solo `[start, end]` por valor → mapa pequeño y limpio. Silencio
*Los ceros* producen valor 0 ← Handle como un caso especial → evitar entradas duplicadas exponenciales. Silencio

-...

##### 3. Por qué el programador de amor este problema

Testado de Habilidad en la Vida por qué importa
Silencio...
Silencio Álgebra bit-wise tención Muchos roles de bajo nivel (embedded, sistemas) requieren una comprensión sólida de XOR, AND, OR. Silencio
← Prefix/rolling-hash ideas ← Demostra la capacidad de convertir un análisis ingenuo O(n2) en O(n). Silencio
← Hash‐map espacio-time trade‐off tención Shows se puede pensar en *O(1) amortized* lookups, un concepto básico de CS. Silencio
TEN Clean Java/Python/C++ Implementación ← Proves puede código en varios idiomas – un plus para posiciones de personal completo. Silencio

-...

##### 4. El “bien” – Lo que hace que esta solución se destaque

1. **Linear + Constant** – `O(n · 30 + q)` es esencialmente lineal en el tamaño de la entrada, que es el mejor que puede esperar en esta escala.
2. **Simplicidad** – La idea central es un solo paso que construye un mapa; la fase de consulta es sólo una búsqueda de diccionario.
3. **Respuesta definitiva** – El mapa almacena la ocurrencia más izquierda automáticamente, satisfaciendo el requisito “smallest izquierdo”.
4. **Language‐agnostic** – Funciona exactamente igual en Java, Python, C++ – ideal para mostrar versatilidad.

-...

##### 5. El “Bad” – Donde la Solución puede Strain

Silencio Silencio Silencio Silencio
Silencio----------
Silencio **Tamaño máximo** – Hasta ~3 × 105 entradas Silencio Usos ~12 MB en Java, 8 MB en Python, 8 MB en C++ (cena 30 % del límite de memoria en LeetCode) Silencio Aceptable para las limitaciones; si usted golpea los límites de memoria, usted puede dejar caer el mapa para los valores. Silencio
tención **30-char limit** – Hard-coded for 32‐bit ints Silencio Si la plataforma cambia a 64‐bit, usted necesita extender a 60 caracteres Silencio Mantener el límite como una constante (`MAX_LEN = 30`). Silencio
Silencio **Cargando cero manipulación** Silencio Requiere una pequeña pero esencial rama tención Document it clearly to avoid confusion during a code‐review. Silencio

-...

##### 6. El “Ugly” – cosas que se sienten difíciles

1. ** Subestrings valor 0 vs. "0...0"** – Se siente contra-intuitivo que cualquier cadena más larga de ceros todavía igual a 0.
2. ** Valores duplicados** – Dos subestrings diferentes pueden producir el mismo valor entero; usted debe garantizar el *izquierda más* uno gana.
3. **Off‐por-uno en la ventana 30-char** – El bucle utiliza `r - l < 30`, que es sutil pero crucial para permanecer dentro de los límites de 32 bits.
4. ** Collision hash‐map** – In C++ `unordered_map` puede ser sensible a golpes; reserve un gran recuento de cubos ( ' reserve(n*30)`) para mantener amortizado O(1).

-...

##### 7. Cómo presentar Esto en un resumen / entrevista

TENCIÓN FORMULADA EN VIRTUD
Silencio...
Silencio **Problema Declaración** 2564 – Subestring XOR Consultas – cadena binaria + 100k consultas.” Silencio
"Reducir cada consulta a una única búsqueda de entero a través de 'target = first ^ second`. Pre-computado el subestring más corto para cada valor posible utilizando un hash-map y sólo examinó los próximos 30 caracteres por inicio.” Silencio
Silencio **La complejidad** Silencioso “O(n·30 + q) tiempo, espacio O(n·30) – escalas a 104 longitud de cadena y 105 consultas.” Silencio
tención **Language Proficiency** ← “Implemente soluciones limpias en Java, Python 3 y C+17”. Silencio
Silencio ** Resultado** Silencioso "Aceptado en LeetCode en 0,2 s para todos los casos de prueba; perfecto para roles críticos de desempeño." Silencio

-...

##### 8. Preguntas frecuentes

Silencio
Silencio...
Silencio *¿Por qué 30, no 32?* Silencio Porque un int de 32 bits firmado puede representar valores hasta 231-1. El problema garantiza el `primer ^ segundo ≤ 109  realizado 230`. Silencio
¿Qué hay de los ceros principales?* Silencio Una subestring que comienza con `0` y tiene longitud 1 sigue siendo 0. Sólo almacenamos el único personaje cero una vez. Silencio
Silencio *¿Podemos usar un array prefix‐sum en su lugar?* Silencio Sí, pero todavía requeriría un mapa de todos los valores posibles de 30 bits. El rodillo directo es más sencillo y más rápido. Silencio
Silencio *¿Qué pasa si `s` es más largo que 104?* Silencio El algoritmo todavía funciona pero superaría los límites de tiempo/espacio. En ese caso necesitarás un bit-set más sofisticado / trie. Silencio

-...

### 9. Pensamientos finales

- **Bueno** – O(1) lookups amortizados, matemáticas claras, preprocesamiento de tiempo constante.
- **Bad** – Roughly 3 × 105 entradas del mapa; memoria pesada para cadenas muy grandes.
- **Ugly** – El quirk “leading‐zero” obliga a una rama especial que es fácil de perder.

Al dominar este problema, impresionará a los reclutadores que se preocupan por las operaciones de ** bit-wise**, **hash-map tricks**, y **clean code** en varios idiomas.

¡Feliz codificación y buena suerte aterrizando esa entrevista!