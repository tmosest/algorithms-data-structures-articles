-...
Título: LeetCode 1166. Sistema de Archivo de Diseño -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Resumen de problemas – 1166. Sistema de archivos de diseño

■ **LeetCode ID**: 1166
■ **Dificultad**: Medium
■ **Tag**: Diseño, Mesa de Hash, Trie

Se le pide que implemente un sistema de archivos en miniatura que soporta dos operaciones:

Silencio Silencio Silencio Silencio
Silencio--------------------------------
Silencio `createPath(pataje, valor)` Silencio `boolean` Silencio Añade un nuevo camino y adjunta un valor entero a él. Devoluciones **falso** si el camino ya existe o si su camino padre no existe. Silencio
Silencio `get(path)` Silencio `int` Silencio Devuelve el valor asociado con *path*, o **-1** si el camino no existe. Silencio

*Path format* – una cadena no vacía que comienza con `/` y contiene sólo letras en inglés minúsculas. Ejemplos: `/a`, `/leetcode/problems`. La raíz `/` en sí es **no** un camino válido.

**Constraints* *

- `2 0= path.length
- " 1 " = valor "
- 104 llamadas a `crearPath`/`get` en total

El objetivo es construir una implementación eficiente y lista para entrevistas que se pueda presentar en Java, Python o C++.

-...

## 2. Opciones de diseño de alto nivel

TENIDO ANTERIOR ANTERIOR ANTERIOR DE LA HABITACIÓN
Silencio--------------------------------------...
Silencio ** Árbol basado en Hash‐Map** Silencio Simple, rápido O(length) por operación Silencio Usos más memoria que un hash-table plano ← Elección de entrevistas comunes
tención **Flat Hash‐Table** (pat → value) Silencio O(1) promedio lookup Silencio Necesita lógica adicional para comprobar la existencia de los padres.
Silencio **Trie** Silencio Memoria-eficiente para prefijos comunes TENIDO Código ligeramente más complejo Silencioso cuando muchos caminos comparten prefijos (por ejemplo, `/a/b/c`, `/a/b/d`

La solución más amigable es un árbol basado en *hash‐map* (a veces llamada una estructura **Trie‐like**). Mantiene un nodo raíz y un mapeo de nombres de niños → nodos de niños. Cada operación sólo recorre los componentes del camino, dando `O(L)` time where `L` is the number of components (≤ 100). El uso de la memoria es `O(N)` donde `N` es el número total de nodos creados.

-...

## 3. Implementaciones de referencia

A continuación se encuentran soluciones de trabajo completo, listas para pasar en **Java**, **Python**, y **C+**. Cada uno sigue el mismo diseño basado en árboles.

### 3.1 Java – Interview‐Ready

``java
importa java.util. HashMap;
importa java.util. Mapa;

clase pública FileSystem {}

--------- Node definition ---------- */
Clase privada estática Nodo {}
Nombre de la cuerda; // nombre del componente
valor int; // valor almacenado en este nodo
Mapa seleccionadoString, Node confianza children; // children by component name

Nodo(Nombre de la cuerda) {
esto. nombre = nombre;
this.value = 0; // 0 denotes no value yet
this.children = new HashMap Quería();
}
}

--------- FileSystem API -------- */
final privado Node root;

public FileSystem() {
raíz = nuevo Nodo(")); // raíz representa "/"
}

public boolean createPath(String path, int value) {
si (página == null tención eterna path.isEmpty() tención eterna path.equals("/") devuelve falso;

Estring[] partes = path.split("/)); // split on '/', first part empty
Nodo cur = root;

/* caminar hacia el padre del nuevo camino */
para (int i = 1; i)
Parte de crianza = partes[i];
cur = cur.children.get (parte);
si (cur == null) devuelve falso; // padre no existe
}

Cierre último = partes[partes.length - 1];
si (cur.children.containsKey(last)) devuelve falso; // ya existe

Nodo nuevoNodo = nuevo Nodo(último);
newNode.value = value;
cur.children.put(last, newNode);
retorno verdadero;
}

int get (String path) {
si (pátula == null tención eterna path.isEmpty() tención eterna path.equals("/") regresan -1;

Criar [] partes = camino.split("/");
Nodo cur = root;

para (int i = 1; i) i++) {
Parte de crianza = partes[i];
cur = cur.children.get (parte);
si (cur == null) regresa -1;
}
retorno r.value;
}
}
`` `

■ **¿Por qué esto es amigable? * *
■ *Separación completa de las preocupaciones*: una clase ligera de `nodo ' , directo `createPath` y `get`. La lógica es fácil de rastrear en una entrevista de codificación en vivo.

-...

### 3.2 Python – Concise & Readable

``python
clase FileSystem:
clase _Nodo:
__slots__ = ("nombre", "valor", "niños")

def __init_(self, name: str):
self.name = name
autovalor = 0 # 0 significa "no valor todavía"
self.children = {}

def __init__(self):
auto.root = self._Node(") # root representa "/"

def createPath(self, path: str, value: int) Bool:
si no camino o camino == "/":
Retorno Falso

partes = path.split("/")[1:]
cur = self.root

por parte en partes [:-1]: # caminar a los padres
si parte no en curs.niños:
Retorno Falso
cur = cur.children[part]

último = partes [-1]
si último en cur.children: # ya existe
Retorno Falso

cur.children[last] = self._Node(last)
cur.children[last]. valor = valor
Retorno

def get(self, path: str) - int:
si no camino o camino == "/":
retorno -1

partes = path.split("/")[1:]
cur = self.root

por parte en partes:
cur = cur.children.get(parte)
si el cura es Ninguno:
retorno -1
retorno cur.value
`` `

■ **Tocados pitónicos* *
■ *`______`* mantiene los objetos nodos inclinados.
■ *Splitting on `/`* ofrece una forma fácil de combinar componentes.

-...

### 3.3 C++ – Fast & Modern

``cpp
#include ■unordered_map Conf
#include ■string
Incluido el título

clase FileSystem {
privado:
struct Node {}
int value{0}; // 0 = sin valor todavía
std::unordered_map buscado::string, Nodo* niños;
};

Nodo* root = nuevo Nodo(); // root represents "/"

// Utilidad: dividir un camino en componentes, saltando los vacíos
std estático:::vector seleccionado::string confianza split(cont std::string curva) {
std::vector seleccionado::string partes;
size_t start = 1; // skip leading '/ '
para (size_t i = 1; i)= path.size(); ++i) {
si (i == path.size()
si (i > start) partes.emplace_back(path.substr(start, i - start));
inicio = i + 1;
}
}
partes de retorno;
}

public:
FileSystem() = default;
-FileSystem() { clear(root); }

bool createPath(cont std::string curva, int value) {
si (path.empty() TENIDO Sendero Vidal == "/") devuelve falso;

partes automáticas = split(path);
Nodo* cur = raíz;

para (size_t i = 0; i + 1 0 partes.size(); ++i) { // vaya a los padres
const auto cosecha comp = parts[i];
aut it = cur- títulochildren.find(comp);
si (es == cur-¢children.end()) devuelve falso;
cur = it- tituladasecond;
}

const std::string ultima = parts.back();
si (cur-jeron.count(last)) devuelve falso;

Node* child = new Node();
niño-convalor = valor;
" cur- "children [last] = niño;
retorno verdadero;
}

int get (cont std::string curva) const {
si (path.empty() tención eterna path == "/") retorno -1;

partes automáticas = split(path);
Nodo* cur = raíz;

para (continuar auto-comp : partes) {
aut it = cur- títulochildren.find(comp);
si (lo == cur- títulonimen.end()) devuelve -1;
cur = it- tituladasecond;
}
retorno cur-convalor;
}

privado:
vacío claro (nodo*) {
para (auto cosecha [_, niño] : node- títuloniños)
clara(niño);
eliminar el nodo;
}
};
`` `

■ **¿Por qué C++?**
■ *La gestión de la memoria flexible* (con `clarar') muestra conciencia de la propiedad.
* " unordered_map "* da las apariencias esperadas.

-...

## 4. Análisis de la complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio `createPath` Silencio `O(L)` – donde `L` es el número de componentes en el camino Silencio Adds one node → `O(1)` additional TEN
Silencioso `get` Silencio `O(L)` Silencio Ninguno (sólo lee los nodos existentes)

- " L " ≤ 100 (disposiciones dadas).
- Memoria total `O(N)` donde `N` = nodos totales jamás creados (≤ número de llamadas exitosas 'createPath').

Tanto las implementaciones Java/Python como C++ satisfacen fácilmente las restricciones LeetCode.

-...

## 5. Entrevista-Comercio Específico Offs

← Tema Silencio Lo que los entrevistadores buscan para vivir Pitfalls para evitar la vida
Silencio---------------------------------------- La vida--
Silencio ** Casos de edge** Silencioso `/`, cadena vacía, componente duplicado tención Olvídase de saltar el primer componente vacío después de la división
Silencio ** Existencia de Padre** Silencio La Traversal debe alcanzar el nodo *parente* primero Silencio Actualizando el nodo equivocado o añadiendo un niño cuando el padre está desaparecido
TEN **Value 0 vs. No Value** Silencio 0 es un valor almacenado válido? TEN En los valores de las especificaciones son ≥ 1, por lo que 0 puede significar con seguridad “no valor todavía”. Silencio
Silencio **Memoria** Silencio Cada nodo tiene un mapa de niños Silencio Sobre localización mapas (por ejemplo, la creación de un nuevo mapa para cada nodo) puede ser despilfarrador
Silencio **Garbage Collection** Silencio Java/Python: automatic; C++: manual tención El fracaso para eliminar los nodos conduce a las fugas

-...

## 5. Pitfalls comunes " Cómo fijar Ellos

1. **Splitting `/` incorrectly* *
*Fix*: ignora las cuerdas vacías o salta el líder `/`.
2. **Asumiendo que el padre existe automáticamente**
*Fix*: caminar por el camino *hasta que el padre* y regresar `falso ' si algún componente falta.
3. **Retorno del valor equivocado para “no valor todavía”* *
*Fix*: almacenar valores sólo en nodos que se crean explícitamente, dejar otros valores de nodos en un centinela (por ejemplo, 0 o `None`).
4. **Raíz de apoyo
*Fix*: la declaración del problema dice que root no es un camino válido – tratarlo especialmente o rechazarlo de forma directa.

-...

## 5. Variedades “Qué si”

- **Flat Hash-Table* *
``cpp
unordered_map detectstring,int confianza val;
unordered_map Secuenciar,string confianza parent; // parent[path] = "/a/b"
`` `
- `createPath` debe comprobar que existe 'padre [pata].
- `get` es `O(1)` promedio.

- ** Árbol del segmento** (sobremata para este problema) – bueno para las consultas del lote en rangos numéricos.

-...

## 5. Resumen – Mensajes para su próxima entrevista

1. **El mapa de hash basado en los pies es el estándar oro**: limpio, rápido y fácil de explicar.
2. **Siempre valida al padre** antes de insertar.
3. **Mantenga el peso ligero de almacenamiento de nodos** – utilice un solo mapa por nodo, un campo de valor y, opcionalmente, un centinela para “sin valor todavía. ”
4. **La complejidad del tiempo** es lineal en el número de componentes del camino (≤ 100), que está muy por debajo del límite LeetCode.
5. **El uso del espacio** es lineal en el número de nodos – fino para ≤ 104 nodos.

■ **Sugerencia de estilo entrevistador**: “¿Puede describir cómo almacenaría la estructura de datos? ”
■ Respuesta: “Un nodo raíz, cada nodo tiene un diccionario de los niños que se clave por el siguiente componente de ruta. ”
■ Luego escribe los dos métodos – el resto sigue naturalmente.

-...

## 6. Final Take‐ Away – “Design File System” en 3 idiomas

- **Java**: Usar `HashMap escritoString, Node confianza` dentro de cada nodo; dividir caminos con `split('/).
- **Python**: La misma idea, pero usa '______ para mantener los nodos inclinados.
- **C++**: `unordered_map` + manual `new`/`delete` le da la velocidad y la claridad de la propiedad.

Las tres soluciones satisfacen las limitaciones de LeetCode y pueden ser demostradas en cualquier entrevista de codificación o evaluación técnica. Elige el idioma con el que estés más cómodo, o presenta los tres para mostrar la amplitud del conocimiento.

■ **Recuerde** – el valor real de la entrevista no es sólo el código final, sino la capacidad de discutir *por qué* usted eligió este diseño, qué cambios considerados, y cómo usted probar casos de borde. ¡Buena suerte!