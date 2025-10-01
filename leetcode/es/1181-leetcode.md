-...
Título: LeetCode 1181. Antes y Después de Puzzle -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1181 – Antes y después del rompecabezas
### 3‐Way Code & a "How‐To" Blog Post for the Next Interview

-...

### 1. Recaptación de problemas

Dada una lista de frases, construya cada posible *Antes > Después de* puzzle:

* Un rompecabezas se forma mediante la fusión de dos frases diferentes.
* Sólo se fusionan la palabra **última** de la primera frase y la palabra **primera** de la segunda frase (la palabra en sí aparece sólo una vez).
* El orden de las dos frases importa – tanto `i → j` como `j → i` debe ser considerado.
* La salida es una lista ** surtida** de cadenas de rompecabezas **unique**.

■ *Ejemplo*
"Código de escritura", "Código de rocas"] → "Código de escritura rocas"

-...

### 2. Estrategia de alto nivel

1. **Pre-proceso** cada frase para almacenar su primera y última palabra.
2. **Mapa**:
* `primer ord → Lista de frases que comienzan con esa palabra titulada `
* `lastWord → Lista de las frases que terminan con esa palabra titulada `
3. Por cada frase " p " (como la frase *primera*)
* buscar todas las frases que comienzan con 'p.last Word`.
* Por cada partido `q`, fusionarse:
`p + " + q.substring(q.firstWord.length()+1)`
(debajo de la palabra duplicada de `q`).
4. Insertar cada resultado en un tipo de `TreeSet` (automáticamente dedupes).
5. Convertir el conjunto en una lista y volver.

Esto es **O(n2)** en el peor caso, pero con 'n ≤ 100' es trivial.
El uso de la memoria es `O(n)`.

-...

### 3. Aplicación del Código

A continuación encontrará soluciones listas para pasar en **Java, Python y C+**.
Todos siguen la misma idea algoritmo y compilan con la biblioteca estándar solamente.

-...

##### 3.1 Java

``java
importar java.util*;

Solución de la clase pública {}
public List won(String[] frases) {}
// Mapas para búsqueda rápida
Mapa:String, Listo:String confianza primeroWordMap = nuevo HashMap garantizado();
Mapa:String, Listo:String confianza últimoWordMap = nuevo HashMap garantizado();

// Pre-proceso cada frase
para (Cantar p : frases) {}
Criar[] partes = p.split(");
Criar primero = partes [0];
Cierre último = partes[partes.length - 1];

firstWordMap.computeIfAbsent(primer, k - título nuevo ArrayList fiel()).add(p);
lastWordMap.computeIfAbsent(last, k - título nuevo ArrayList recomendado()).add(p);
}

// Árbol Set da deduplicación + clasificación
Establecer contacto Resultado estándar = nuevo TreeSet correspond();

para (Primera frase: frases) {}
Primeras partes = primerPhrase.split(");
Estring lastWord = firstParts[firstParts.length - 1];

Lista Nombramiento:String titulada candidates = firstWordMap.getOrDefault(lastWord, Collections.emptyList());
para (String secondPhrase : candidates) {}
si (primeroPhrase.equals(segundoPhrase)) continúan; // i != j

String[] secondParts = secondPhrase.split(");
// Eliminar la palabra duplicada
Criatura fusionada = primera Frase + " +
String.join(" ", Arrays.copyOfRange(secondParts, 1, secondParts.length));
result.add(merged);
}
}

devolver nuevo ArrayList garantizado(resultar);
}
}
`` `

-...

###### 3.2 Python

``python
de las colecciones importadas por defecto
de la importación Lista

Solución de clase:
def before YDespuésPuzzles(self, frases: List[str]) - Lista[str]:
first_map = defaultdict(list) # first word - título frases
last_map = defaultdict(list) # last word - título frases

# Pre-procesamiento
para p en frases:
palabras = p.split()
first_map[words[0].append(p)
last_map[words[-1].append(p)

res = set()

para p en frases:
last_word = p.split() [-1]
para q en first_map.get(last_word, []):
si p == q: j
continuar
merged = p + " + ".join(q.split()[1:])
res.add(merged)

de vuelta ordenados (res)
`` `

-...

##### 3.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vectoriales antesY despuésPuzzles(vector asignados frases iguales) {}
unordered_map identificadostring, vector identificadostring confianza primero, último;
unordered_set obtenidosstring Resultado de confianza;

// Ayudante a dividir
auto split = [](la cadena restante) {
vectoriales palabras;
Cura de cuerda;
istringstream iss(s);
mientras (es нелине cur) palabras.push_back(cur);
devolver palabras;
};

// Pre-proceso
for (const string &p : frases) {}
auto palabras = split(p);
primero[words.front()].push_back(p);
último[words.back()].push_back(p);
}

// Construir rompecabezas
for (const string &p : frases) {}
auto w = split(p);
const string > Word = w.back();
aut it = first.find(lastWord);
si (it == first.end())) continúan;

for (const string &q : it- título) {}
si (p == q) continúan; // i != j
auto wq = split(q);
string merged = p;
para (size_t i = 1; i) ++i) {
merged += " + wq[i];
}
result.insert(merged);
}
}

vector asignado(result.begin(), result.end());
(ans.begin(), ans.end());
devolver los ans;
}
};
`` `

-...

### 4. Blog Post: “Antes y después del rompecabezas – LeetCode 1181: El Bien, El Mal El Mal

-...

#### Title (SEO‐Friendly)

*Cracking LeetCode* 1181 – Antes > Después de Puzzle: Java/Python/C++ Soluciones + consejos de entrevista”**

*Keywords: LeetCode, Antes y Después de Puzzle, entrevista prep, solución Java, solución Python, solución C++, algoritmo, manipulación de cuerdas, entrevista de codificación, entrevista de programación, problema algorítmico. *

-...

##### Introducción

■ **“En entrevistas de codificación, LeetCode’s *Antes de > Después de Puzzle* (Problema 1181) es un desafío engañosamente simple de manipulación de cuerdas que prueba su capacidad de pensar en *marcales*, *hash-mapping*, y *deduplicación*. En este artículo, caminaremos por el problema, mostraremos soluciones limpias en Java, Python y C++, y discutiremos los obstáculos que pueden tropezar incluso entrevistados experimentados.”* *

-...

#### Problema Resumen

- **Introducción** - Array of `phrases ' (cada una cadena de letras inglesas de un solo espacio).
- ** Objetivo** - Por cada par ordenado `(i, j)` donde `i ل j`, si la última palabra de `frases[i]` equivale a la primera palabra de `frases[j]`, fusionarlos en una sola frase:
`` `
"frase[i] frase[j]" // pero deja caer la palabra duplicada
`` `
Todas las distintas frases fusionadas, ordenadas lexicográficamente.

-...

#### ¿Por qué es “bueno” para las entrevistas?

1. **Clear Constraints** – `n ≤ 100`, `len ≤ 100`. Perfecto para enseñar *fuerza bruta* vs *optimizada* pensamiento.
2. # Encourages Hashing # La idea central es combinar palabras rápidamente usando mapas de hash.
3. **String Handling** – Una buena prueba de cómo te separas, te unes y evitas errores por uno.

-...

##### El “Bad” – Pitfalls comunes

← Mistake Silencio Por qué sucede Silencio
Silencio...
Silencio **El uso de bucles anidados ingenuamente** Silencio O(n2) está bien aquí, pero muchos candidatos añaden complejidad innecesaria. Mantener O(n2) pero pre-compute mapas de palabras primero/último para evitar la repetición. Silencio
Silencio **Incluyendo auto-puzzle** (`i == j`) Silencio Muchas soluciones accidentalmente fusionan una frase consigo misma. Silencio Explicablemente saltar cuando los índices o cadenas coinciden. Silencio
Silencio **Duplicado palabras en fusión** Silencio Olvidando despojar la primera palabra de la segunda frase. Silencioso Quitarla vía `substring` o `split[1:]`. Silencio
Silencio **No deduplicar** Silencio Los pares diferentes pueden producir la misma cuerda fusionada. Silencio Usar una `Set` o `TreeSet` antes de convertir a la lista. Silencio
Silencio ** Ordenación incorrecta** Silencio Devolviendo la lista sin surtido. Use built‐in kind or `TreeSet`. Silencio

-...

##### Los “Ugly” – Edge Cases

1. ** Frases de palabras individuales** – “a” es primera y última palabra.
2. ** Frases duplicadas en la entrada** – por ejemplo, `["ab ba", "ab ba"].
3. **Gran número de duplicados** – “a a a” → muchos emparejamientos pero un resultado único.
4. ** Frases muy largas** – hasta 100 caracteres; evitar operaciones de cadena O(length2).

-...

#### Step‐by‐Step Solution

1. **Split cada frase en palabras** – `split(")`.
2. **Record**:
* `firstWordMap[first] → lista de frases que comienzan con esa palabra `
* `lastWordMap[last] → lista de frases que terminan con esa palabra `
(Ambos pueden ser `HashMap observadoString, List No se hace referencia aString confianza `` en Java, `defaultdict(list)` en Python, o `unordered_map detectstring, vector asignadostring confianza `` en C++.)
3. **Por cada frase `p` como primera parte**:
* `last = p.last Palabra `
* Para cada candidato " q " , en `primera palabra " . (donde `q != p`):
* Merge: `p + " + q.substring(q.firstWord.length() + 1)` (Java) o similar en otros idiomas.
4. **Insértese en un `Set`** para garantizar la unicidad y el orden (un `TreeSet` o conjunto ordenado).
5. **Regresar** la lista clasificada.

-...

#### Complexity Analysis

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio Pre-procesamiento Silencioso `O(n * w)` (`w` = término medio por frase) Silencio `O(n)` Silencio
Silencioso pareado " merging  durable `O(n2 * w)` (worst case, but `n ≤ 100`) Silencio `O(n2)` para el conjunto de resultados
Silencio Ordenación Silencioso `O(k log k)` donde `k` = número de resultados únicos Silencio `O(k)` Silencio

Con las limitaciones dadas esto es cómodamente rápido.

-...

#### Código Snippets (Ready for Interview)

*Java* – se muestra antes.
*Python* – se muestra antes.
*C+* – mostrado anteriormente.

■ **Consejo:** En entrevistas, primero se puede mostrar el bucle doble de fuerza bruta (claro y correcto), y luego optimizar por la piratería. Esto demuestra tanto la corrección como la eficiencia.

-...

#### Final Thoughts

*Antes > Después de Puzzle* es un **gold‐mine** para los entrevistadores: es corto, cubre conceptos esenciales, y deja espacio para que un candidato hable de estructuras de datos, manejo de los bordes y estilo de código.

**Practice Tips:**

1. Implemente las tres soluciones usted mismo; ser fluido en Java, Python y C++ muestra versatilidad.
2. Ejecute su código en las entradas de la muestra (y algunos casos de borde que crea).
3. Explicar la lógica en voz alta mientras escribes el código—los interlocutores aman la claridad del pensamiento.

Buena suerte, y que sus puzzles siempre se “merge” agradablemente!

-...

##### Sobre el autor

*[Su nombre]* es un ingeniero de software experimentado que ha ayudado a los equipos a ganar entrevistas de codificación en LeetCode. Sígueme para más avances de algoritmos, guías de preparación de entrevistas y perspectivas de carrera.

-...

¡Feliz codificación y feliz entrevista!