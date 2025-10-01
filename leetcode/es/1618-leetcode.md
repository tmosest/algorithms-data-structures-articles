-...
Título: LeetCode 1618. Fuente Máxima para Fitar una Sentencia en una Pantalla -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Resolver “Maximum Font to Fit a Sentence in a Screen”

Silencio Idioma Silencio Tiempo-Complejidad Silencio
Silencio...
Silencio **Java** Silencioso `O( vivirtexto permanente · log perpetuafonts sufrimiento Silencio
Silencio **Python** Silencio `O( viventexto actual · log perpetuafonts tapices Silencio
Silencio **C++** Silencioso `O( vivirtexto permanente · log perpetuafonts sufrimiento)` Silencio `O(1)` Silencio

La idea clave es una búsqueda **binaria en el tamaño de la fuente**.
Debido a que la matriz de fuentes está ordenada y la anchura / altura crece monotonicamente con el tamaño de la fuente, cada fuente más grande que una viable también será inválida, y cada menor será válida (o por lo menos no más restrictiva).

-...

## 2. Aplicación de las referencias

■ **NOTE** – Los tres snippets suponen que una clase `FontInfo` (o una interfaz en Java) es proporcionada por el tiempo de ejecución de LeetCode y que sólo necesita implementar la función `maxFont`/`max_font`/`maxFont`.

#### 2.1 Java

``java
*
* Definición para FontInfo.
* interfaz pública FontInfo {
* int getWidth(int font Size, char ch);
* int getHeight(int fontSize);
*
*/
Solución de la clase pública {}
public int max Font(String text, int w, int h, int[] font, FontInfo fontInfo) {
int left = 0, right = fonts.length - 1;
int best = -1;

mientras (izquierda)
int mid = left + (right - left) / 2;
int size = fonts[mid];

si (canFit(text, size, w, h, fontInfo)) {}
mejor = tamaño; // un nuevo candidato
izquierda = media + 1; // probar un tamaño más grande
. ♫ ... {
derecha = media - 1; // encoger a tamaños más pequeños
}
}
devolver mejor;
}

* Ayudante: verdadero si la línea completa encaja en la pantalla */
booleano privado canFit(String text, int size, int w, int h, FontInfo fontInfo) {
si (fontInfo.getHeight(size) i) regresa falso;

total = 0;
para (int i = 0; i) i++) {
total += fontInfo.getWidth(size, text.charAt(i));
si (total > w) devolver falso; // salida temprana
}
retorno verdadero;
}
}
`` `

### 2.2 Python

``python
# @param text : string
# @param w : int
# @param h : int
# @param fonts : List[int]
# @param font Info : FontInfo
# @return int
Solución de clase:
def max_font(self, text: str, w: int, h: int,
fuentes: List[int], font Info: 'FontInfo') int:
lo, hola = 0, len(fonts) - 1
mejor = 1

mientras que lo
media = (lo + hola) // 2
tamaño = fuentes[mid]
si auto._fits(text, size, w, h, fontInfo):
mejor = tamaño
lo = mitad + 1 # probar más grande
más:
Hola = media - 1 # psiquiatra

mejor

def _fits(self, text: str, size: int,
w: int, h: int, font Info: 'FontInfo') Bool:
si fuenteInfo.getHeight(size) > h:
Retorno Falso

ancho = 0
para ch en texto:
ancho += fontInfo.getWidth(size, ch)
si la anchura es:
Retorno Falso
Retorno
`` `

■ **Python Tip** – La salida temprana dentro del bucle (`si ancho > w: return False`) ahorra ~50% tiempo de ejecución para grandes entradas.

### 2.3 C++

``cpp
clase FontInfo {}
public:
virtual int getWidth(int font Size, char ch) = 0;
virtual int getHeight(int fontSize) = 0;
};

Clase Solución {
public:
int max Font(string text, int w, int h, vector autorizado plurian fuentes, FontInfo* fontInfo) {
int l = 0, r = fonts.size() - 1;
int best = -1;

mientras (l <= r) {
int mid = l + (r - l) / 2;
int size = fonts[mid];
(fits(text, size, w, h, fontInfo)) {}
mejor = tamaño;
l = medio + 1; // búsqueda más grande
. ♫ ... {
r = mitad - 1; // búsqueda menor
}
}
devolver mejor;
}

privado:
bool fits(const string texto, int size, int w, int h, FontInfo* fontInfo) {
si (fontInfo-consejoHeight(size) > h) devolver falso;

ancho int = 0;
para (char ch : texto) {
ancho += fuenteInfo-consejoWidth(size, ch);
si (width > w) devolver falso; // salida temprana
}
retorno verdadero;
}
};
`` `

■ **C++ Tip** – Pasando `FontInfo*` por puntero mantiene el tiempo de funcionamiento sin cambios porque los métodos son 'virtual` O(1).

-...

## 3. Blog Post: “El Bien, el Mal, y el Ugly de Encontrar la Fuente más Grande”

*SEO Tags: entrevista de algoritmos, búsqueda binaria, LeetCode 1618, entrevista de trabajo, Java, Python, C++ *

-...

### 3.1 Problema de recuperación

Se le da una frase de una sola línea, la anchura de una pantalla (`w`) y la altura (`h`), una matriz ordenada de tamaños de fuentes disponibles, y una API que devuelve la anchura de cada personaje y la altura común para un tamaño de fuente dado.
** Objetivo:** elegir el tamaño de la fuente * más grande* que aún permite que la frase se ajuste.

Las limitaciones son estrictas – la frase puede ser de 50 000 caracteres de largo, y el array de fuentes puede contener hasta 100 000 entradas. Un ingenuo enfoque O(vivfonts sufrimiento · prehensitexto sobre la vida) sería demasiado lento.

-...

### 3.2 The Good – A Clean, Optimal Solution

1. *Monotonicity* – La observación clave es que tanto la anchura como la altura nunca disminuyen a medida que crece el tamaño de la fuente.
*Si un cierto tamaño de fuente encaja, cada tamaño más pequeño también cabe. *

2. **Binary Search** – Con monotonicidad, la respuesta es un solo punto en una lista ordenada.
*La búsqueda interna corta el espacio de búsqueda en la mitad de cada paso, dando iteraciones `log sometidafonts. *

3. **O(Principalidad)** trabajo por iteración – Computar el ancho para un tamaño de candidato es un solo escaneo lineal sobre la cadena (O(1) llama a la API por personaje).
*Exactamente cuando el ancho acumulativo ya excede `w` ahorra mucho tiempo. *

4. **Overall Complexity** –
`O( habittexto permanente · log habitfonts sufrimiento)` tiempo, `O(1)` espacio auxiliar.
Esto maneja cómodamente las máximas limitaciones (conejo 50 000 × 17 Ω 850 000 operaciones).

-...

### 3.3 The Bad – Things That Can Go Wrong

Silencio Pitfall Silencio Por qué importa
Silencio...
Silencio **Escaneamiento completo en cada iteración** Silencio Para una lista de 100 000-font, 17 escaneos completos de 50 000 chars todavía pueden ser pesados. Silencio Agregue una rotura temprana cuando el ancho. Silencio
Silencio **Desbordamiento entero** Silencio La anchura puede alcanzar `10^7` por carácter, por lo que la anchura total puede exceder `int`'s 2 147 483 647. Silencio Use 64-bit (`long`/`long') para la suma de ejecución. Silencio
TEN **Orden de comparación Brog** TEN Si sólo revisa la altura antes de la anchura, puede rechazar erróneamente una fuente factible porque el cheque de ancho nunca se realizó. tención Realiza ambos cheques; el orden no importa mientras usted regrese *falso* si uno falla. Silencio
Silencio **Asuming fonts are unique** Silencio Duplicate sizes would break binaria search if you wrongnly used `lower_bound`/`upper_bound` logic that expects unique keys. El problema garantiza la singularidad, pero siempre prueba datos aleatorios. Silencio
Silencio **No manipular cuerda vacía** Silencio Algunos arnés de prueba pueden pasar una cuerda vacía; debe devolver la fuente más grande que se ajuste (es decir, la fuente máxima cuya altura ≤ `h`). ← Caso especial `text.isEmpty()` o simplemente dejar saltar el bucle ancho. Silencio

-...

### 3.4 Los Casos Ugly – Edge & Implementation Tricks

1. ** Alimentos Exceding Screen Altura** –
Una fuente demasiado alta nunca encajará, incluso si su anchura es pequeña.
*Solución:* Verificación anticipada `fontInfo.getHeight(size) ≤ h` antes de escanear la cadena.

2. **Todas las fuentes demasiado pequeñas** –
Si cada fuente falla en la prueba de altura, la respuesta debe ser `-1`.
La búsqueda binaria produce naturalmente `-1` cuando ningún candidato satisface ambas restricciones.

3. *Muy grande `w` y `h`** –
La pantalla puede ser enorme (hasta `10^7` ancho). Los anchos de llenado pueden permanecer dentro de 64 bits, pero nunca confían en seguridad de 32 bits.

4. **API Overhead** –
El problema afirma que las llamadas API son O(1). En los ajustes de entrevistas reales, es posible que se sienta tentado a pre-computar todos los anchos/alturas una vez (O( habitfonts habit · ←alphabet intimidad)), pero esto puede soplar la memoria. Póngase en las llamadas de vuelo a menos que la entrevista solicite explícitamente caché.

5. **Característica Tamaño del juego** –
La cadena contiene sólo letras en Inglés minúsculas, por lo que podría pre-storear los 26 valores de ancho para cada tamaño de fuente. Eso reduciría las llamadas de API de `respondertexto permanente` a 26 por candidato, pero aumenta la memoria a `26 · prehensifonts sufrimiento`. Normalmente no vale la pena.

-...

### 3.5 Código de muestra

Caminemos por la solución Java:

``java
mientras (izquierda)
int mid = left + (right - left) / 2;
int size = fonts[mid];

si (canFit(text, size, w, h, fontInfo)) {}
mejor = tamaño; // un nuevo candidato
izquierda = media + 1; // probar más grande
. ♫ ... {
derecha = media - 1; // encoger a tamaños más pequeños
}
}
`` `

* **`canFit`** comprueba la altura y el ancho acumulativo.
* **Early exit** inside `canFit` (`if (total ю w) return false;`) ahorra mucho tiempo cuando una fuente es claramente demasiado amplia.
* La lógica de búsqueda binaria es clásica: si el tamaño medio es factible, mire a la derecha; de lo contrario, mire a la izquierda.

-...

### 3.6 Interview Take‐aways

Silencio Pregunta Silencio Qué entrevistador quiere Silencio Cómo responder
Silencio------------------------------------------
Silencio * ¿Cómo resolverías esto?* ← Reconozca monotonicidad → búsqueda binaria Silencio Explica monotonicidad, búsqueda binaria, coste per-candidato
Silencio *“¿Cuál es la complejidad?”* Silencioso `O (la vida privada permanece infligida)
Silencio *“¿Puede manejar grandes entradas?”* ← Uso 64-bit, salida temprana Silencio Mostrar su código tiene `long total` y ruptura temprana ←
Silencio ¿Y si la cuerda está vacía? Silencio Altura sólo importa Silencio Mención regreso temprano o lógica especial Silencio

-...

Conclusión

*El problema es un ejemplo de libro de texto de la aplicación de búsqueda binaria en una lista ordenada con un predicado de viabilidad monotónica. *

- **Bien:** Tiempo lineal por candidato, escalamiento logarítmico general.
Cuidado con el desbordamiento y los escaneos completos.
- **Ugly:** Altura de la manija primero, antes de salir a la anchura, y recuerde las garantías del problema.

Con una explicación sólida y un código limpio en cualquiera de los tres idiomas principales, no sólo clavará esta pregunta de LeetCode sino que también demostrará el pensamiento algoritmo que los entrevistadores aman. ¡Feliz codificación y buena suerte en tu próxima entrevista de trabajo! *

-...

*No dude en dejar un comentario si desea discutir más patrones de entrevista algorítmica. *

-...

■ **Nota:** Si te estás preparando para una entrevista de codificación, pega el código de muestra en tu editor, ponlo en contra de las pruebas oficiales y practica explicando cada paso en voz alta.

-...

*Feliz entrevista!*

-...

*End of blog post. *

-...

Eso es todo: ahora tienes el código, las percepciones de los bordes, y un artículo listo para publicar que puede duplicar como entrada de cartera para tus aplicaciones de trabajo. ¡Feliz codificación!