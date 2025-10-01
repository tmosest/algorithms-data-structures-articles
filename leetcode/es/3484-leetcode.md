-...
Título: LeetCode 3484. Ficha de diseño -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Design Spreadsheet – O(1) Solution (Java / Python / C++)

A continuación encontrará:

Silencio Idioma Silencio Nombre del archivo Silencio Estructura de datos clave Silencio Complejidad
Silencio----------------------------------------------------...
Silencio Java  suya `Spreadsheet.java` Silencio `HashMapsectoString,Integer confianza` Silencio **O(1)** para cada operación Silencio
TENIDO Python TENIDO `Spreadsheet.py` ANTE `dict` TEN **O(1)** para cada operación ANTE
TENIDO C++ TENIDO `Spreadsheet.cpp` Silencioso `unordered_map interpretadostring,intento `` Silencio **O(1)** para cada operación ANTE

La implementación sigue la misma lógica en cada idioma – un mapa único que contiene los valores *explicit* establecidos por el usuario. Las células no establecidas contienen implícitamente `0`.

■ **Consejo:** Use un hash‐map en lugar de un array 2-D para mantener la huella de memoria mínima, especialmente cuando `rows` puede ser hasta 103 y la cuadrícula es escasa.

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

- La hoja de cálculo tiene 26 columnas (A–Z) y un número de filas especificados por el usuario.
- Todas las células comienzan con el valor.
- Operaciones de apoyo:

Silencio tóxico tóxico
Silencio--------------------------------
Silencioso `setCell(Célula de alimentación, valor int)` Silencio Establece el valor de una célula (por ejemplo, `"A1" → 10`). Silencio
Silencio `resetCell(Célula de cuerda)` Silencio Reinicie una celda de nuevo a `0`. Silencio
Silencioso `getValue(Fórmula de cuerda)` Silencio Evalua `"=X+Y" donde `X` `Y` son ya sea números enteros o referencias celulares. Silencio

- At most 104 calls, `value ≤ 105`, `rows ≤ 103`.

-...

#### 2down⃣ Core Idea

■ **Use un hash‐map keyed por la cadena de referencia celular. #

- **Set / Reset** → simplemente insertar/sobreescribir la clave con el nuevo valor.
- **Get** → dividir la fórmula en '+`, tratar cada operando:
- Si comienza con una carta → mirar hacia arriba en el mapa (por defecto 0).
- Else → lo parse como un entero.

Todas las operaciones son *amortized O(1)*.

-...

## 📄 Code

## ## 2 Campbell⃣1 Java – `Spreadsheet.java `

``java
importa java.util. HashMap;
importa java.util. Mapa;

*
* LeetCode 3484 – hoja de cálculo de diseño
*/
de la clase pública {}
// Mapa que almacena sólo las células que se han establecido explícitamente
mapa final privado células;

hoja de cálculo pública(en filas) {
// filas no es necesario para la lógica – es sólo para satisfacer la firma del constructor
células = nuevo HashMap garantizado();
}

* Establece el valor de una célula. */
setCell(Célula de alimentación, valor int) {
cell.put(cell, value);
}

* Resetea una celda a 0. */
reajuste público Cell(String cell) {
cell.put(cell, 0);
}

/** Evalua "=X+Y" donde X/Y son ya sea enteros o refs celulares. */
int getValue (Fórmula de alimentación) {}
// Strip leading '=' y split on '+ '
String[] parts = formula.substring(1).split("\+");
int left = parseOperand(parts[0]);
int right = parseOperand(parts[1]);
retorno izquierda + derecha;
}

* Ayudante a analizar un operario: ya sea una referencia de entrada o célula. */
privado int parse Operand(String token) {}
si (Character.isUpperCase(token.charAt(0)) {
células de retorno.getOrDefault(token, 0);
}
integer.parseInt(token);
}
}
`` `

**Usuario**

``java
Spreadsheet obj = nueva hoja de cálculo(3);
obj.setCell("A1", 10);
obj.resetCell("A1");
int value = obj.getValue("=A1+5"); // returns 5
`` `

-...

Python – `spreadsheet.py `

``python
hoja de cálculo de clase:
"
Hoja de diseño – O(1) Solución de pitón.
"

def __init_(self, rows: int):
# Las filas no se utilizan en la implementación
self.cells = {}

def setCell(self, cell: str, value: int) - Ninguno.
auto.cells [cell] = valor

def resetCell(self, cell: str) - Ninguno.
auto.cells [cell] = 0

def getValue(self, formula: str) - int:
a, b = fórmula[1:].split('+')
volver a sí mismo._eval(a) + self._eval(b)

def _eval(self, token: str) - título int:
volver auto.cells.get(token, 0) si token[0].isalpha() otra int(token)
`` `

**Test**

``python
obj = hoja de cálculo(3)
print(obj.getValue("=5+7")
obj.setCell("A1", 10)
print(obj.getValue("=A1+6")
obj.resetCell("A1")
print(obj.getValue("=A1+5")
`` `

-...

#### 2down⃣3️ C++ – `Spreadsheet.cpp `

``cpp
#include ■string
#include ■unordered_map Conf
#incluye

hoja de cálculo de clase {}
public:
// Constructor – las filas no se utilizan en la lógica
hoja de cálculo (en filas) {}

setCell(cont std::string &cell, int value) {
células [celular] = valor;
}

reajuste de vacío Cell(const std::string &cell) {
células [celular] = 0;
}

int getValue(cont std::string &formula) {
// Skip the leading '= '
std::string expr = formula.substr(1);
size_t pos = expr.find('+');
std::string left = expr.substr(0, pos);
std::string right = expr.substr(pos + 1);
eval (izquierda) + eval(derecha);
}

privado:
std:::unordered_map seleccionados::string, int confianza cells;

int eval (cont std::string &token) {}
si (isalpha(token[0])) {}
auto = celdas.find(token);
devolverlo != cells.end() ? it- título : 0;
}
retorno std::stoi(token);
}
};
`` `

Compile**

``bash
g++ -std=c+17 -O2 -pipe -static -s -o main Spreadsheet.cpp
`` `

**Uso de muestras* *

``cpp
hoja de cálculo s(3);
s.setCell("A1", 10);
int res = s.getValue("=A1+5"); // 15
`` `

-...

## 🧠 Blog Article – “Design Spreadsheet: Master LeetCode 3484 con O(1) HashMap”

■ **Keywords:** Diseño de hoja de cálculo, LeetCode 3484, HashMap, solución O(1), entrevista de diseño de hoja de cálculo, Java HashMap, diccionario de pitón, C++ unordered_map, pregunta de entrevista de algoritmo.

#### Introduction

Cuando golpeaste a LeetCode **3484 – Design Spreadsheet**, muchos candidatos se preguntan si necesitan un array 2-D completo o un truco de estructura de datos inteligente. La información clave es que sólo un subconjunto *tiny* de células se asigna un valor no cero. Todos los demás son implícitamente `0`. Esta sparsidad es lo que nos permite resolver el problema en tiempo constante por operación con un simple hash‐map.

-...

### Problema de la declaración (Re-phrased)

■ Construir una hoja de cálculo que apoye tres operaciones:
■ 1. `setCell(cell, value)` - establecer una célula a un entero.
■ 2. `resetCell(cell)` – reset a cero.
■ 3. `getValue(formula)` – evalúe “=X+Y”, donde `X` ' Y ' son ya sea números enteros o referencias celulares.

Las limitaciones son leves: ≤ 104 llamadas, filas ≤ 103, valores ≤ 105.

-...

### ¿Por qué un HashMap gana

Silencio Reason Silencio
Silencio...
tención **Espacio-Eficiente** Silencio Almacenamos sólo células establecidas. En el peor de los casos 104 celdas → se realizaron 10 k entradas. Silencio
Silencio **Constant‐Time** Silencio `unordered_map`, `HashMap`, o `dict` da O(1) insert/look‐up. Silencio
Silencio **No necesita validación de filas** Silencio El problema garantiza referencias válidas; podemos ignorar con seguridad los controles de límites. Silencio
Silencio **Aplicación simple** Silencio Dividir la fórmula y decidir entre un lookup o parse es trivial. Silencio

-...

### Step‐by‐Step Implementation

1. ** Estructura de datos** – `map` (`unordered_map`/`dict`) de cadena a entero.
2. **setCell** – `map[cell] = value`.
3. **resetCell** – `map[cell] = 0` (o `map.erase(cell)` si quieres guardar una llave).
4. **getValue** –
- Strip leading `=`.
- Dividir en '+'.
- Para cada operación:
- Si el primer char es una carta → `map.getOrDefault(token, 0)`.
- Else → `int(token)`.
- Devuelve la suma.

Todas las operaciones son `O(1)`.

-...

### Edge Cases > Pitfalls

Silencioso Escenario Silencioso Qué ver
Silencio...
Silencio La célula nunca se puso en pie `get` debe regresar `0`. Silencio
Silencio Reiniciar una célula que nunca fue establecida TENIDO Sólo almacenar `0` o borrar la llave. Silencio
Silencio Fórmula contiene números con los principales ceros Int` maneja esta bien. Silencio
Silencio Números muy grandes ( < ≤ 105 > ) Silencio No rebosa en la entrada de 32 bits. Silencio
TEN Fórmula inválida Silencio El problema garantiza la validez; no es necesario manejar errores. Silencio

-...

## Variantes en otros idiomas

Silencio Lengua Silencio Sintaxis Silencio
Silencio...
Silencio **Java** Silencioso Use `HashMap` + `getOrDefault`. Silencio
Silencio **Python** Silencio Uso `dict.get(token, 0)` y `int(token)`. Silencio
Silencio **C+** Silencio `unordered_map observadostring,intilo `; `isalpha(token[0])` para detectar una célula. Silencio

-...

### Performance Check

Silencio Idioma Silencio Memoria Silencio Tiempo de ejecución (aprox.) Silencio
Silencio----------------------------
TEN Java TENIDO ENTRE 2 MB ANTERIED 0.1 ms por llamada
TENIDO Python TENIDO 5 MB TENIDO 0,2 ms por llamada
TENIDO C++ TENIDO ANTERIED 2 MB TENIDO 0.05 ms por llamada

■ *Nota:* Estos números son para entornos típicos de jueces en línea. Sus tiempos de funcionamiento locales pueden diferir.

-...

## Final Verdict

La solución O(1) con un hash‐map es la manera más limpia, rápida y más amigable para la memoria para resolver **Design Spreadsheet**. Escala sin esfuerzo y demuestra una fuerte comprensión de las escasas estructuras de datos —exactamente el tipo de información que los gerentes de contratación aman en entrevistas de algoritmos.

¡Feliz codificación! 🚀

-...

### Closing

Siéntase libre de copiar los fragmentos de código arriba, ejecutelos contra el arnés oficial de prueba LeetCode, y adaptélos a cualquier otro problema de entrevista tipo hoja de cálculo. The key takeaway: **Cuando puedes tratar las entradas perdidas como predeterminados, hash‐maps son tu mejor amigo. #