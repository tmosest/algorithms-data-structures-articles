-...
Título: LeetCode 2168. Subestrings únicos con frecuencia de dígito igual -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código - Tres idiomas

A continuación encontrará soluciones **ready‐to-copy** para LeetCode 2168 – * Subestrings únicos con frecuencia de dígito igual* – escrito en **Java**, **Python**, y **C+**.
Los tres siguen la misma idea O(N2 · 10):
* enumerar todas las subestrings,
* mantener una matriz de frecuencia de 10 elementos al extender la subestring,
* prueba si cada cuenta no cero es igual,
* insertar la subestring en un conjunto basado en hash para mantener sólo únicos.

``text
LeetCode 2168
Subestrings únicos Con la frecuencia de dígito igual
Hora : O(N2 · 10)
Espacio : O(N2) (conjunto de subestrings únicos)
`` `

-...

## Java – 100% Java 17

``java
importar java.util*;

Solución de la clase pública {}
// Compruebe si todos los conteos no cero son los mismos
booleano privado isValid(int[] cnt) {
int pivot = -1;
(int i = 0; i) 10; i++) {
si (cnt[i] == 0) continuar;
si (pivot == -1) pivot = cnt[i];
si (cnt[i] != pivote) devuelve falso;
}
retorno verdadero;
}

público igual DigitFrequency(String s) {
Establecer contactos únicos = nuevo HashSet correctamente();
int n = s.length();

para (int i = 0; i)
int[] cnt = nuevo int[10];
StringBuilder cur = nuevo StringBuilder();

para (int j = i; j) {}
int d = s.charAt(j) - '0';
cnt[d]+;

cur.append(s.charAt(j));

si (esValid(cnt))) único.add(cur.toString());
}
}
retorno único.size();
}
}
`` `

■ **Tip:** El `StringBuilder` se reutiliza para cada 'i', por lo que evitamos construir una nueva cuerda para cada personaje.
■ El método " isValid " escanea sólo 10 posiciones - cabezas arriba insignificantes.

-...

### Python – 3.10+

``python
de la importación Lista, Conjunto

Solución de clase:
def equal DigitFrequency(self, s: str) - int:
n = len(s)
único: Set[str] = set()

para i en rango(n):
cnt = [0] * 10
cur = []

para j en rango(i, n):
d = ord(s[j]) - 48
cnt[d] += 1
cur.append(s[j])

# Test equality of all non‐zero counts
pivote = ninguno
OK = True
para c en cnt:
si c == 0: continuar
si el pivote es Ninguno:
pivote = c
Elif c!= pivote:
ok = Falso
descanso
Si está bien:
único.add('.join(cur))

len(unique)
`` `

■ ¿Por qué una lista para 'cur'? #
 `'''.join(cur)` es O(len(cur)), pero la construcción de la lista una vez por `i` mantiene el bucle interno lineal.

-...

## C++ – Modern C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
bool isValid(cont array observadoint,10 estrecho cnt) {
int pivot = -1;
para (int c : cnt) {
(c == 0) continuar;
si (pivot == -1) pivote = c;
si (c != pivote) devuelve falso;
}
retorno verdadero;
}

int equal DigitFrequency(string s) {
unordered_set buscadostring confianza uniq;
int n = s.size();

para (int i = 0; i) {}
array observado,10 confianza cnt {}; // todos los ceros
Cura de cuerda;

para (int j = i; j)
int d = s [j] - '0';
++cnt[d];
cur.push_back(s[j]);

si (esValid(cnt)) uniq.insert(cur);
}
}
devolver estática_cast seleccionado(uniq.size());
}
};
`` `

■ **¿Por qué `noordened_set asignados'? * *
■ La trituración incorporada es lo suficientemente rápida para ≤ 1 000 subestrings.
■ Usando `std::string` mantiene el código legible; la parte superior de la copia es trivial para las limitaciones dadas.

-...

## 2. Blog Artículo – “El Bien, el Mal, y el Ugly de LeetCode 2168”

■ **Meta Title* *
√ 2168 LeetCode: Subestrings únicos con frecuencia de dígito igual – Java, Python & C++ Soluciones
■ **Meta Descripción**
■ Master LeetCode 2168 con soluciones Java, Python y C++. Aprende el algoritmo, las trampas y cómo impresionar a los gerentes de contratación con tu estilo de codificación.

-...

#### Introduction

Cuando los reclutadores le piden que resuelva * Subestrings Únicos con la frecuencia de dígito igual* (LeetCode 2168), están buscando tres cosas:

1. * Corrección** – ¿El algoritmo encuentra cada subestring clasificatoria?
2. **Eficiencia** - ¿Puede manejar la peor entrada en los límites de tiempo?
3. **Código limpio** - ¿Es la solución legible y sostenible?

En este artículo caminamos por el **bueno**, el **bad**, y las partes **enriquecidas** de las soluciones típicas, muestran una implementación lista para la producción en tres idiomas, y señalan mejoras favorables para las entrevistas.

-...

## Problema Recap

■ ** Entrada** – una cadena `s` (longitud ≤ 1000) que consiste sólo en dígitos decimales.
■ ** Objetivo** – contar subestrings ** únicos donde *todo dígito que aparece* lo hace el número de veces** **.

■ *Examples*
*“1212”* → `{"1","2","12","21","1212"} → respuesta = 5
*“12321”* → 9 subestrings únicos

La frase clave es *“todo dígito que aparece”*. Los dígitos que no aparecen en absoluto son ignorados.

-...

### The “Good” – O(N2 · 10) Brute‐Force with Early Validation

Porque `s.length ≤ 1000`, un algoritmo cuadrático es aceptable. El truco es **evitar reescanning** el subestring en cada extensión:

1. Para cada índice de inicio `i`, inicialice un array de frecuencia de 10-element `cnt` y un `StringBuilder ` (Java) / lista (Python) / cadena (C++).
2. Crece el subestring un personaje a la vez ( " j " de " a " n-1 " ), actualizando " cnt " y la cadena actual.
3. Después de cada extensión, ejecute `isValid(cnt)` – un solo paso sobre 10 elementos – para comprobar que todas las frecuencias no cero son iguales.
4. Si es válido, inserte la subestring en un conjunto de hash para mantener la singularidad.

¿Por qué es esto bueno? #

- **Linear per substring** - el bucle interior hace trabajo O(1) (10 pasos).
- **Ninguna copia de cuerda pesada** – mantenemos una cadena de funcionamiento y sólo materializamos la clave para el conjunto cuando sea necesario.
- **Código simple, idiomático** – fácil para los reclutadores para leer y razonar.

-...

### “Bad” – Rolling Hashes, Trie o Extra Data Structures

Algunas soluciones en LeetCode añaden complejidad para pequeñas ganancias:

¿Por qué? Silencio
Silencio--------------------------
Silencio Rolling hash + cola de doble duración El hash necesitaría contar 10 contadores, no sólo una subestring. Silencio
Silencio Trie of substrings Silencio Sí Silencio Construyendo un poco de hasta 1⁄2 N2 nodos es innecesario para N = 1000. Silencio
Silencio Pre-computación de todas las frecuencias del par Silencio Sí Silencio Todavía O(N2) pero desperdicia la memoria y el tiempo. Silencio

**Takeaway:** En entrevistas, una solución *clear* O(N2) golpea una optimización inteligente pero no legible. Valor del programa **comprendido** sobre *cleverness*.

-...

### La Reconstrucción de Subestring frecuente

Un error común es reconstruir la subestring en cada iteración:

``java
para (int j = i; j) {}
// ...
String sub = s.substring(i, j + 1); // O(length)
(isValid(cnt))) set.add(sub);
}
`` `

Esto añade un factor adicional `O(L)` (donde `L` es la longitud de subestring). Para una cadena de 1000 caracteres, puede empujar hacia el límite de 10 segundos en algunos jueces.

**Fix:** Mantenga una cadena mutable (`StringBuilder`, `String`, o lista) y *sólo* materialice cuando sepa que es válido.

-...

### Step‐by‐Step Code Walk-through

Vamos a ilustrar la versión Java, que es la más verbosa pero clara.

``java
público igual DigitFrequency(String s) {
Establecer contactos únicos = nuevo HashSet correctamente();
int n = s.length();

para (int i = 0; i)
int[] cnt = nuevo int[10];
StringBuilder cur = nuevo StringBuilder();

para (int j = i; j) {}
int d = s.charAt(j) - '0';
cnt[d]+;

cur.append(s.charAt(j));

si (esValid(cnt))) único.add(cur.toString());
}
}
retorno único.size();
}
`` `

* **El bucle exterior** – fija el índice de inicio `i`.
* **Loop interior** – expande la subestring a la derecha.
* **`cnt`** – actualizaciones de frecuencias en O(1).
* **`isValid`** – sólo 10 pasos, por lo que el tiempo total es `O(N2)`.

Las variantes Python y C++ siguen la misma lógica; simplemente ajustar la sintaxis y los tipos de datos.

-...

### Complexity Analysis

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencioso Subestrings enumerating Silencioso `O(n2)`
Silencio Actualización de frecuencias
Silencioso Verificación de la validez Silencio `O(10)` por paso Silencio – Silencio
Silencio Hash set  durable up to `O(n2)` única subestrings  durable – TEN
Silencio **Total** Silencioso `O(n2)` Silencio

Con " n ≤ 1000 " , las operaciones más difíciles son aproximadamente 106 " – cómodamente dentro del límite de 2 segundos en la mayoría de las plataformas.

-...

### Interview‐Friendly Tips

Silencio Silencio
Silencio...
Silencio ** Copias de cuerda innecesarias** Silencio Usar un constructor mutable / lista; sólo `join`/`toString` en subestrings válidos. Silencio
Silencio **Ignorando cero conteos** Silencio En `isValid`, omita entradas donde `cnt[i] == 0`.
Silencio **Set overhead** Silencioso Use `HashSet` (Java), `unordered_set` (C++), o `set` (Python). Silencio
Mantenga los nombres de las funciones descriptivas (`equalDigitFrequency`, `isValid`). Silencio
Silencio ** Casos de edge** ← Prueba cadenas de caracteres individuales, todos los mismos dígitos, dígitos alternos. Silencio

-...

### Qué proyector busca

1. * Corrección** – manejar todos los casos de borde, no fuera de lugar.
2. **Tiempo de intercambio espacial** – explicar por qué `O(n2)` es seguro aquí.
3. ** Estilo clásico de codificación** – evitar abstracciones innecesarias.
4. **Opcional** – mencionar las posibles mejoras (por ejemplo, usando bitmasks para 10 dígitos) pero explicar por qué son innecesarias para las limitaciones.

-...

### Closing Thoughts

LeetCode 2168 es un gran problema para mostrar un enfoque **balanceado**: un algoritmo directo que es tanto **eficiente** para los límites dados y **conociblemente**.
Al dominar las implementaciones Java, Python y C++ arriba, estarás listo para:

* Discuta el algoritmo en una pizarra blanca.
* Escriba código limpio y libre de errores en una entrevista.
* Mostrar reclutadores que priorizas **claridad sobre astucia**: un rasgo clave para desarrolladores mayores.

¡Feliz codificación, y buena suerte aterrizando ese próximo papel!

-..