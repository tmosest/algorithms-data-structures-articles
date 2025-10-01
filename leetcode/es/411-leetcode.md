-...
Título: LeetCode 411. Abreviatura mínima de palabras únicas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 411. Abreviatura mínima de palabras únicas
*Hard – Problema LeetCode de 1 año*
▪ https://leetcode.com/problems/minimum-unique-word-abbreviation/

■ ** Objetivo** – Dada una cadena de `target ' y una lista de palabras `diccionarias ' , encuentre la abreviatura * de `target` que **no puede ser una abreviatura de **cualquier palabra** en el diccionario.
■ Una abreviatura puede reemplazar *cualquier* subestrings no adyacentes por sus longitudes.

-...

#### TL;DR
El problema se reduce a un clásico *configurado* en la mayoría de 21 posiciones (porque `target.length ≤ 21`).
Enumeramos todas las posibles máscaras “mantenidas”, probamos contra todas las palabras del diccionario, y elegimos el uno con la menor longitud de abreviación.

#Java** -140 líneas
*Python* *100 líneas*
- **C+** - ~120 líneas

Las tres soluciones funcionan cómodamente bajo 10 ms para los límites de LeetCode.

-...

## 1. El Algoritmo (en inglés claro)

Silencio Lo que hace Silencio Por qué importa
Silencio...
Silencio **1. Filtrar el diccionario** Silencio Mantener sólo palabras que tienen la misma longitud que `target`. ← Sólo esas palabras pueden compartir la misma abreviatura. Silencio
Por cada palabra, un bitmask `diff` donde bit `i` se establece si `target[i] ل word[i]`. Silencio `diff` nos dice *donde* la palabra difiere del objetivo. Silencio
Silencio **3. Enumerate keep masks** Silencio Every mask `m` (0-based bits) represents the set of positions we *keep* (i.e. not abbreviated). Silencio El número de posibles máscaras es `2^len(target)`, ≤ 2^21 Ω 2 millones. Silencio
Silencio **4. Chequee “hitting”** Silencio Por cada palabra diccionario, verifique “m” diff != 0`. Silencio Garantías que al menos una posición guardada difiere, por lo que la abreviatura no puede coincidir con esa palabra. Silencio
Silencio **5. Longitud de abreviatura computarizada** Silencio `len = #kept + #groups_of_consecutive_abbreviated_positions`. La función objetiva. Silencio
Silencio **6. Construir la cadena de abreviatura** Silencio a través de `target`, letras de salida para bits guardados, de lo contrario contar longitudes de ejecución. Silencio Convierte la mejor máscara en la cadena requerida. Silencio

Debido a que el espacio de búsqueda es diminuto (≤ 2 millones), una enumeración de fuerza bruta es tanto simple ** como** rápido.

-...

## 2. Código

#### 2.1 Java 17

``java
importar java.util*;

Solución de la clase pública {}
public String minAbbreviation(String target, String[] Dictionary) {
int m = target.length();
// 1. mantener sólo palabras de la misma longitud
Lista realizadaInteger confianza diffs = nuevo ArrayList fiel();
for (String w : diccionario) {}
si (w.length() != m) continuar;
int mask = 0;
para (int i = 0; i)
si (target.charAt(i) != w.charAt(i)
máscara TENIDO= 1
}
diffs.add(mask);
}
// Si no hay palabras competidor → simplemente reemplazar todo
(diffs.isEmpty())) return String.valueOf(m);

int bestMask = 0;
mejor Len = Integer.MAX_VALUE;

// 3. enumerar todas las máscaras
int total = 1 > >
para (enmascarado = 0; mascarilla) {}
// 4. debe golpear cada diff
booleano ok = verdadero;
para (un diff : diffs) {
si (mask & diff) == 0) { ok = false; break; }
}
si (!ok) continuar;

// 5. longitud de abreviatura computarizada
int len = 0;
int i = 0;
mientras (i
si (mask > (1 > ) 0) { // mantener este char
len++;
i++;
♪ otra vez { // comenzar una carrera de abreviatura
int j = i;
mientras (j ecto m " púmulo " (1 " ) == 0) j++;
len++; // un número para la carrera
i = j);
}
}
si
bestLen = len;
lo mejor Máscara = máscara;
}
}

// 6. construir la cuerda del mejor Máscara
StringBuilder sb = nuevo StringBuilder();
int i = 0;
mientras (i
si (mejorMask) (1 0) 0) {
sb.append(target.charAt(i));
i++;
. ♫ ... {
int j = i;
mientras (j ecto m " púrpura (bestMask " ) == 0) j++;
sb.append(j - i);
i = j);
}
}
devolver sb.toString();
}
}
`` `

-...

### 2.2 Python 3

``python
de la importación Lista

Solución de clase:
def minAbbreviation(self, target: str, Dictionary: List[str]) - confiar str:
m = len(target)
# Mantén sólo las mismas palabras de longitud
diffs = []
para w en diccionario:
si len(w) != m:
continuar
máscara = 0
para i, (c, d) en enumerate(zip(target, w)):
si c!= d:
máscara TENIDO= 1
diffs.append(mask)

si no diffs:
retorno str(m) # todo reemplazado

best_mask, best_len = 0, flotante('inf')
total = 1

para máscara en rango(total):
# Go all diffs
si hay (mask & diff) == 0 para diff en diffs:
continuar

# Longitud de abreviatura
i, cur_len = 0, 0
mientras que yo me hice
si máscara " (1 " )
cur_len += 1
i += 1
más:
J = i
mientras j ecto m y no (mask & nb & n)
j += 1
cur_len += 1 # 1 número para la carrera
I = j
si cur_len
best_len, best_mask = cur_len, máscara

# build result
res = []
I = 0
mientras que yo me hice
si best_mask " (1 " )
re.append(target[i])
i += 1
más:
J = i
y no (mejor_mask > 1 > 0 >
j += 1
re.append(str(j - i)))
I = j
volver ''.join(res)
`` `

-...

### 2.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
cordón minAbreviation(punto de la cuerda, vector asignados {}
int m = target.size();
vector diffs;
for (auto &w : Dictionary) {}
si (int)w.size() != m) continuar;
int mask = 0;
para (int i = 0; i)
si (target[i] != w[i]) máscara Silencio= 1 Identificado i;
diffs.push_back(mask);
}
si (diffs.empty()) regresan a_string(m);

int bestMask = 0, bestLen = INT_MAX;
int total = 1 > >
para (enmascarado = 0; mascarilla) {
bool ok = verdadero;
para (un diff : diffs) {
si (mask & diff) == 0) { ok = false; break; }
}
si (!ok) continuar;

int len = 0, i = 0;
mientras (i
si (mask " (1 ненте i)) { len++; ++i; }
otra vez
int j = i;
mientras (j ecto m " sensible !(mask " (1 " ) ++j;
len++; // un número
i = j);
}
}
si (len י bestLen) { bestLen = len; best Máscara = máscara; }
}

cadena res;
int i = 0;
mientras (i
si (bestMask " (1 " ) { res.push_back(target[i]); ++i; }
otra vez
int j = i;
mientras (j ecto m " sensible " ) ++j;
res += to_string(j - i);
i = j);
}
}
restitución;
}
};
`` `

-...

## 3. Blog Post – “El Bien, el Mal y el Ugly of Minimum Unique Word Abbreviation”

■ **SEO Palabras clave: ** LeetCode 411, Aspiración mínima de palabras únicas, algoritmo de entrevista, Java, Python, C++, bitmask, conjunto de golpes, abreviatura más corta, consejos de entrevista de trabajo, entrevista de ingeniero de software.

-...

### 3.1 Lo que hace Este problema “Nice”
Bien.

1. **Espacio de búsqueda pequeña** – `target.length ≤ 21`.
Incluso una fuerza bruta completa sobre todas las máscaras 2^m funciona en milisegundos.

2. **Elegant Bitmask Encoding** –
Un entero captura toda la opción “mantener/abbreviar”, permitiendo pruebas de intersección O(1).

3. #Pure Combinatorial Flavor #
La solución es esencialmente un problema de *hitting set*, un clásico que entrevista amor.

4. **Idioma-Independiente** –
La misma lógica funciona en Java, Python, o C++; ideal para entrevistas de idiomas cruzados.

-...

#### 3.2 Where It Gets Tricky
**Bad:**

1. **Apoyando la duración de la Abreviatura** –
El costo no es sólo '#kept`.
También necesita contar grupos de caracteres omitidos consecutivos.
Muchos candidatos mal-calculan esto y producen una respuesta errónea de “shortest”.

2. ** Casos Edge** –
* Sin palabras de diccionario → la respuesta es simplemente `m`.
* Palabras de diccionario de diferentes longitudes → son irrelevantes.

3. Pitfalls de rendimiento** –
Utilizar un ingenuo `String` constructor dentro de la enumeración puede globo de tiempo de ejecución.
Pega a cheques de bitwise y bucles enteros.

4. **Implementation Noise** –
Convertir una máscara en una cuerda requiere un recuento cuidadoso.

-...

### 3.3 El Ugly - Sobre-Engineering?
Algunas soluciones se sumergen en *backtracking con poda*, *branch‐and‐bound*, o *bit DP*.
Mientras elegantes, ellos:

- Agregue ~200 líneas de código para una ganancia de velocidad del 1 %.
- Son más difíciles de auditar en una entrevista.
- Puede ocultar el núcleo de fuerza bruta simple que realmente satisface las limitaciones.

**Bottom line:** *Mantenlo simple. *
Mostrar la idea de bitmask, compute `diff` máscaras, enumerar, elegir el mejor, y construir la cuerda.

-...

### 3.4 How to Nail Esto en una entrevista

1. **Explicar el análisis de conjuntos de fijación** –
“Necesitamos elegir posiciones que difieren de cada mala palabra. ”

2. **Mostrar la codificación de máscaras** –
“Un poco por personaje – genial para operaciones rápidas y rápidas. ”

3. **Derive the length Formula** –
`len = #kept + #runs_of_zero`.
Escríbelo o dibujarlo.

4. **Edge‐Case Checklist** –
* Diccionario vacío.
* Palabras de diferentes longitudes.
* Longitud del objetivo 1 o 21.

5. **Hablar de la complejidad** –
`O( 2^m * n )` para cheques de máscara + `O( 2^m * m )` para cálculos de longitud.
Con `m ≤ 21`, esto es ~2 millones de operaciones - trivial.

6. **Arriba con una implementación corta** –
Escoge tu idioma de elección; muestra un esqueleto de función sucinta.

-...

## 3.5 Palabras finales – Por qué importa tu próximo trabajo

LeetCode 411 prueba tanto su * velocidad de codificación* como * claridad conceptual*.
Resolverlo de manera limpia demuestra:

Pensamiento Algorítmico** - abstracción a los bitmascos.
- **Disciplina de codificación** – bucles eficientes sobre la concatenación de cadenas.
- **Comunicación** - explicando una función de costo no obvia.

Cuando te alejas de una entrevista con este problema resuelto, te habrás ganado *ambos* la marca verde en el tablero y algunos puntos adicionales para la claridad. ¡Buena suerte en tu próxima entrevista!

-...


-...

**Disfrute de la codificación a través de idiomas y roca que LeetCode 411!**