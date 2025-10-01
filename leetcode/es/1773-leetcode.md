-...
Título: LeetCode 1773. Conteo artículos que coinciden con una regla -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recaptación de problemas
**LeetCode 1773 – Conteo artículos que coinciden con una regla**

Se le da una lista de artículos, donde cada artículo es un 3-tuple `[tipo, color, nombre]`.
Una regla es un par `(ruleKey, reglaValue)`.
Un artículo coincide con la regla si:

. Reglas de vida La condición clave de la vida para que coincida con
Silencio...
Silencioso `'tipo'
Silencioso `"color" Silencio `ruleValue == color`
Silencioso `'nombre' '

Devuelve cuántos elementos coinciden con la regla.

*Constraints*
- 1 ≤ artículos. longitud ≤ 104 `
- Todas las cuerdas son minúsculas y tienen longitud ≤ 10
- `ruleKey` ANTE {`'''''tipo', `'color'`, `'nombre'}

La solución es un escaneo lineal directo – O(n) tiempo y O(1) espacio extra.



----------------------------------------------------

## 2. Aplicación de Java

``java
importa java.util. Lista;

Solución de la clase pública {}

*
* Cuenta cuántos elementos coinciden con la regla dada.
*
* @param items Lista de artículos; cada artículo es una lista de contactos del tamaño 3:
* [tipo, color, nombre]
* Regla de @param Key "type", "color", o "name"
* Regla de @param Valor El valor contra el
* @retorno número de elementos que coinciden con la regla
*/
público int Partidos(Lista seleccionadaLista) ítems, Regla de cuerda Key, String ruleValue) {
int count = 0;

// Mapa de la reglaKey al índice que necesita ser comparado
int idx;
idx = 0;
si (ruleKey.equals("color") idx = 1;
*/ idx = 2;

para (Lista seleccionadaString ratio artículo : items) {
si (item.get(idx).equals(ruleValue)) {}
contar++;
}
}

recuento de retorno;
}

// Método principal opcional para la prueba manual rápida
public static void main(String[] args) {
var sol = nueva solución ();
Lista realizadaLista realizada ítems = Lista de
List.of("phone", "blue", "pixel"),
List.of("computer", "silver", "lenovo"),
List. of("phone", "gold", "iphone")
);
System.out.println(sol.countMatches(items, "color", "silver")); // 1
}
}
`` `

### ¿Por qué esto es *bueno*
- **O(n) time, O(1) space** – el más rápido posible para un solo pase.
- No se necesitan estructuras de datos adicionales ni escotillas.
- Utiliza el `equals` incorporado para la comparación de cadenas (O(length) pero trivial aquí).

#### *Bad* part that you can improve
Si el conjunto de llaves crece (por ejemplo, más atributos), la cadena `si-else` se convierte en error-prone. Un `Mapa hecha cuerda, Integer confianza` sería más limpio.

#### *Ugly* edge case
La codificación dura de los valores índices (`0`, `1`, `2`) puede hacer que el código sea frágil si el formato del elemento cambia. Una asignación de estilo conmutador mantiene la intención clara.



----------------------------------------------------

## 3. Aplicación de los pitones

``python
de la importación Lista

Solución de clase:
def countMatches(
self, items: List[List[str]], ruleKey: str, rule Valor: str
) int:
"
Cuenta artículos que coinciden con una regla dada.

Parámetros
--------
items : List[List[str]]
Cada lista interior tiene exactamente tres cuerdas: [tipo, color, nombre].
Regla Clave : str
Uno de "tipo", "color", o "nombre".
Regla Valor : str
Valor que la clave elegida debe igualar.

Devoluciones
---
int
Número de artículos iguales.
"
key_to_index = {"type": 0, "color": 1, "name": 2}
idx = key_to_index[ruleKey]
volver suma(1 para el artículo en los artículos si el artículo[idx] == reglaValue)


Prueba manual rápida
si __name_ == "__main__":
sol = Solución()
ítems =
["teléfono", "azul", "pixel"],
["computer", "silver", "lenovo"],
["teléfono", "oro", "iphone"],
]
print(sol.countMatches(items, "color", "silver")) # 1
`` `

*Highlights*

- Un diccionario mapas claves de índices – elimina las declaraciones repetitivas.
- `sum(1 para ...)` es conciso e idiomático.
- Tiempo de ejecución: `O(n)`; memoria `O(1)`.



----------------------------------------------------

## 4. Aplicación C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int countMatches(vector seleccionadovector identificador artículos,
Regla de cadena Key, string ruleValue) {
// Regla de mapa Clave del índice de columna que debe compararse
unordered_map buscadostring, int
{"tipo", 0},
{"color", 1},
{"nombre", 2}
};
int k = idx[ruleKey];
int cnt = 0;
para (auto & item : items) {
si (tema[k] == reglaValue) ++cnt;
}
cnt de retorno;
}
};

int main() {}
Sol de solución;
vector de vectores ítems =
{"phone", "azul", "pixel"},
"computer", "silver", "lenovo"},
# El teléfono, el oro, el teléfono #
};
cout se realizó el sol.countMatches(items, "color", "silver")
retorno 0;
}
`` `

Lo que lo hace bueno
- Usa un `noordened_map` para la asignación clara de clave a índice.
- No hay asignación dinámica – todo en pila (excepto entrada vectorial).
- El bucle directo da tiempo O(n), espacio auxiliar O(1).

** Mejoras potenciales**
Si quieres permanecer 100% compatible con la biblioteca estándar, sustitúyase `unordered_map` por una simple cadena `si`; ahorra una pequeña cantidad de memoria para este pequeño mapa.



----------------------------------------------------

## 5. SEO‐Optimized Blog Artículo

■ *Título*
■ *Mastering LeetCode 1773 – Conteo artículos que coinciden con una regla (Java, Python & C++)*

■ **Meta Descripción**
■ “Aprenda a resolver LeetCode 1773 – Conteo artículos que coinciden con una regla. Guía paso a paso, Java, Python, soluciones C++, análisis de tiempo y consejos de entrevista. ¡Ponga tu entrevista de codificación hoy en día!”

-...

#### Introduction

Si te estás preparando para una entrevista de ingeniería de software, a menudo te encontrarás mirando problemas que suenan simples pero ocultan trampas sutiles. Uno de estos problemas es LeetCode 1773, *Count Items Matching a Rule*. Aunque parece trivial, la prueba real es escribir código limpio, legible y explicar la lógica en unos minutos.

En este artículo diseccionaremos el problema, caminaremos a través de tres soluciones específicas para lenguaje (Java, Python, C++), analizaremos el tiempo y la complejidad espacial, y discutiremos “el bien, el mal y el feo” de enfoques típicos. Al final se sentirá confiado en presentar esta solución en cualquier entrevista o en una plataforma de codificación.

-...

### Problema Declaración

Se le da una lista de artículos. Cada artículo es un 3-tuple: `[tipo, color, nombre]`.
A *rule* consta de dos cuerdas: `ruleKey` (que puede ser ''tipo'', `'color'`, o `'nombre'') y `ruleValue`.

**Task:** Cuenta cuántos elementos satisfacen la regla, es decir, donde el valor de la columna indicada por `ruleKey` equivale a `ruleValue`.

■ *Ejemplo*
" texto
ítems = [["phone", "blue", "pixel"],
["computer", "silver", "lenovo"],
["phone", "gold", "iphone"]
▪ Clave = "color", reglaValue = "plata"
■ → respuesta = 1
" `

-...

### El enfoque directo

A simple vista, el problema es simplemente “atrapar a través de cada artículo y comparar el campo relevante”. Eso nos da un algoritmo **O(n)** con **O(1)** espacio auxiliar, donde `n` es el número de elementos.

**¿Por qué es esta la solución óptima? #
- Debemos inspeccionar cada artículo al menos una vez – no puede hacer mejor que el tiempo lineal.
- Necesitamos sólo un contador, por lo que no se requiere memoria adicional más allá de la entrada.

La verdadera pregunta es cómo implementar esto limpiamente a través de los idiomas y cómo evitar errores comunes.

-...

### Good, Bad, and Ugly – A Language‐by-Language Breakdown

Silencio Idioma Silencio bueno (Lo que funciona bien) ← Bad (Lo que se puede mejorar) ← Ugly (Hard‐to-maintain code)
Silencio------------------------------------------------------------
TEN **Java** TENIDO Cartografía del índice recto; líneas mínimas TENIDO Repetir la cadena `si-else`; índices de codificación dura ANTERIED operadores ternarios o el estilo de conmutación que no es legible ANTE
Silencio **Python** Silencio Dictionary for key‐to‐index; `sum` generador ¦ Usando una lista de tuples; no explicit index mapping TEN cadenas de lambda largas o complejas comprehensiones de lista
Silencio **C++** Silencio `unordered_map` para la cartografía; basado en rango para TEN-Usar `map` en lugar de simple `si` cuando sólo tres claves ANTERIENTE Comparación de cadena manual con `strcmp ' y manejo manual de índices

##### 1. El bien
- **Escaneo de línea** – visitamos cada artículo una vez; este es el más rápido posible.
- ** Índice de expansión Mapping** – cada solución mapas `"tipo" → 0`, `"color" → 1`, `"nombre" → 2` – haciendo la intención cristalina.

##### 2. El mal
- **Codificación de riesgo** – si el problema cambia para añadir un atributo cuarto, tendría que parchear cada lugar que utiliza los índices numéricos.
- **Verbose `if-elseâ** – cuando tienes muchas llaves, la cadena crece y se convierte en un peligro de mantenimiento.

##### 3. El Ugly
- **Switch‐like patterns** que usan terneros anidados o "switch" en cadenas (en Java 14+).
- ** Optimización Prematura** – tratando de micro-optimizar la comparación de cadena cuando el tamaño de entrada es modesto.

-...

### Code Walk-through

A continuación mostramos la lógica básica una vez, luego proporcionar implementaciones específicas para el lenguaje.

*Core Idea*
``text
1. Regla de mapa Índice de columna → (0, 1, 2)
2. Para cada artículo:
si el artículo [index] == Regla Valor: contra++
3. Retorno
`` `

##### Java

``java
int idx = ruleKey.equals("type") ? 0
: ruleKey.equals("color") ? 1
: 2; // nombre

para (Lista seleccionadaString ratio artículo : items) {
si (item.get(idx).equals(ruleValue)) contra++;
}
`` `

#### Python

``python
key_to_index = {"type": 0, "color": 1, "name": 2}
idx = key_to_index[rule Clave]
volver suma(1 para el artículo en los artículos si el artículo[idx] == reglaValue)
`` `

###### C++

``cpp
unordered_map buscadostring,intilo idx{"type",0},{"color",1},{"name",2};
int k = idx[ruleKey];
para (auto > items) si (item[k] == ruleValue) ++cnt;
`` `

Los tres francotiradores alcanzan el tiempo **O(n)**, **O(1)** espacio.

-...

## Time & Space Complexity Analysis

TEN TERRI TEN ANTERIOR ANTERIOR ANTERIOR
Silencio------------------------------
Silencioso** tención Single pasar a través de la lista de entrada. Silencio
Silencio **Auxiliary Space** Silencio `O(1)` Silencio Sólo un contador y un pequeño mapa/diccionario. Silencio
Silencio ** Espacio de entrada** Silencioso `O(n * 3 * avgLen)` Silencio Determinado por el problema; nuestra solución no añade a él. Silencio

**¿Por qué no podemos hacerlo mejor? #
Necesitas leer cada artículo para saber si coincide con la regla. Sin un índice preprocesado, usted no puede saltar los elementos. Así, `O(n)` es asintotically óptimo.

-...

### Interview Tips

1. **Explicar la asignación claramente** – “Uso un diccionario/HashMap para traducir la clave de cadena en un índice entero. ”
2. **Declarar la complejidad frente a frente** – “Este es tiempo lineal, espacio constante. ”
3. ** Periferias de la mención** – por ejemplo, ¿qué pasa si 'ruleKey' es 'nombre'? Muestra que tu código lo maneja a través de la asignación.
4. **Discuten las extensiones posibles** – “Si se añadieran más atributos, podríamos mantener la asignación genérica. ”

-...

### Conclusión

LeetCode 1773 es un ejemplo de libro de texto de un problema que recompensa **claridad** sobre la astucia.
- **Java** – utilizar un mapa o una cadena de 'si' para el mapeo de índices; mantener el bucle simple.
- **Python** – un diccionario mantiene el código DRY; `sum` o una comprensión de la lista es idiomática.
- **C++** – un pequeño `unordered_map` (o incluso un simple `si') hace el trabajo; los bucles basados en rangos lo mantienen legible.

Recuerde siempre:
Mantenga el algoritmo lineal y legible.
- **Bad**: Evite índices de codificación dura que se romperán si el problema evoluciona.
- **Ugly**: Mantener la distancia de las declaraciones convocadas de conmutador/ternario que tienen una intención oscura.

Armado con estas soluciones y una explicación sólida, estará listo para asar este problema en cualquier entrevista de codificación o juez en línea. Buena suerte, feliz codificación, y que sus entrevistadores estén impresionados!

-...

### Further Reading

- [LeetCode 1773 – Count Items Matching a Rule](https://leetcode.com/problems/count-items-matching-a-rule/)
- [Teoría de la complejidad de los entrevistadores](https://medium.com/@alexjohnson/compstanding-complexity-in-interview-questions)
- [C++] Based For Loops – Modern Best Practices](https://cppreference.com/w/cpp/language/range-for)

-...

**Author Bio**
*Jane Doe* es un ingeniero de software senior que ha ayudado a miles de candidatos a romper entrevistas técnicas en Google, Amazon y Microsoft. Escribe sobre diseño de algoritmos, legibilidad de códigos y estrategias de entrevista.

-...

¡Feliz codificación! *



-...

## Final Thoughts

Solving LeetCode 1773 es más que solo producir la respuesta correcta. Se trata de demostrar que usted entiende los fundamentos algorítmicos, puede escribir código limpio en varios idiomas, y puede anticipar preocupaciones futuras de mantenimiento. Utilice los fragmentos de código arriba como plantillas, tweak ellos para adaptarse a su estilo personal, y practicar explicando la lógica en voz alta. Estarás listo para este problema —y muchos más— en tu próxima entrevista.

-...

**End of Article**



-...

### Closing

Hemos abarcado las estrategias *core*, *implementaciones*, *análisis* e incluso *interview communication*. El problema es simple, la solución elegante, y los aprendizajes universales. Tome una taza de café, ejecute estos francotiradores en su máquina, y practique la explicación hasta que se sienta natural. ¡Buena suerte!

-...



----------------------------------------------------

### Quick recap of resources

TEN TERRITOR SON SON SON SON SON
Silencio...
Silencio LeetCode 1773 Silencio https://leetcode.com/problems/count-items-matching-a-rule/ Silencio
Silencio Java `equals` docs ANTE https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#equals-java.lang. Objeto... Silencio
Silencio Python `sum` generador ANTE https://docs.python.org/3/library/functions.html#sum Silencio
TEN C++ `unordered_map` TEN https://en.cppreference.com/w/cpp/container/unordered_map Silencio


■ ¡Feliz codificación! *



-...



**[End of Blog]**



-...



¿Listo para empezar tu entrevista? #
- **Java** – copiar el snippet, ejecutarlo y explicar el mapeo del índice.
- **Python** - mostrar el diccionario, luego la expresión del generador.
- **C++** – señala el mapa y el rango de base para el bucle.

Tienes todo el arsenal trilingüístico. ¡Buena suerte!



-...



**Consejo:** Mantenga una copia *limpia* de cada solución útil; puede pegarla en cualquier IDE rápidamente. La clave es hablar con confianza sobre el algoritmo, no perderse en sintaxis.



-...



¡Feliz entrevista!



-...



**P.S.** Si encontró útil este artículo, compartalo en LinkedIn, Twitter o tu comunidad de desarrolladores favorita. ¡Buena suerte en tu viaje de codificación!



-...



**Keywords**: LeetCode 1773, Contando artículos que coinciden con una regla, Solución Java, solución Python, solución C++, codificación de entrevistas, complejidad del tiempo, complejidad del espacio, análisis de algoritmos, consejos de entrevista de ingeniería de software, entrevista de codificación.



-...



¡Feliz codificación!



-...



**



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-..