-...
Título: LeetCode 588. Diseño de sistema de archivos en memoria -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 588 – Diseño de un sistema de archivos de memoria
**Hard Silencio 588 Silencio Java Silencio Python Silencio C++**

■ ¿Quieres conseguir esa entrevista de ingeniería de software?
■ Dominar este problema muestra que puede diseñar una estructura de datos, trabajar con árboles y mantener todo **léxicográficomente ordenados** – exactamente lo que los gerentes de contratación aman.

-...

## 1. Recapitulación de problemas (SEO-friendly)

■ **Diseñar un sistema de archivos en memoria** – *LeetCode 588*.
■ Cree una clase de 'FileSystem' que apoye:
* `ls(path)` – lista de contenidos del directorio o nombre de archivo.
* `mkdir(path)` – crear directorios.
* `addContentToFile(filePath, content)` – crear o anexar contenido de archivos.
* `readContentDesdeFile(filePath)` – leer contenido de archivos.

Todos los caminos son absolutos, comienzan con `/`, y no terminan con `/` (excepto la raíz).
Los nombres consisten en letras minúsculas, no duplicados en la misma carpeta.

■ **Por qué importa:**
■ Los entrevistadores piden esto para medir su capacidad de:
* Construir una estructura similar al árbol (directorios de ficheros).
* Manipulación de cuerda de mano " traversal de ruta.
* Mantenga el listado del directorio clasificado (orden léxicográfico).
* Piense en casos de borde y rendimiento.

-...

## 2. Panorama general del diseño

← Layer Silencio Lo que hace Silencio Por qué importa
Silencio...
Silencio **Node** Silencio Representa un archivo o un directorio. Silencio Mantiene los datos básicos juntos – contenido para archivos, niños para dirs. Silencio
Silencio **Tree** Silencio Root `Node` + navegación por el camino. tención Permite operaciones O(a fondo) Silencio
Silencio **Ordenar** Silencio Utilizar un mapa (`TreeMap` en Java, `std::map` en C++, `dict + ordenados()` en Python. tención Garantiza orden lexicográfico sin trabajo extra. Silencio

-...

## 3. Implementaciones de referencia

A continuación se presentan implementaciones limpias y listas de producción para **Java, Python y C++**.
Los tres siguen los mismos principios de diseño y pasan las pruebas LeetCode.

### 3.1 Java

``java
importar java.util*;

clase pública FileSystem {}

* Node representa un directorio o un archivo */
Clase privada estática Nodo {}
boolean isFile;
Contenido de StringBuilder = nuevo StringBuilder(); // sólo para archivos
TreeMap Garantizado, Node confiar niños = nuevo TreeMap Quería(); // sólo para directorios

Nodo() { esto. isFile = false; }
}

final privado Node root;

public FileSystem() {
root = nuevo Node(); // root is always a directory
}

* Listar el contenido de un directorio o el nombre de un archivo */
public List won(String) {
Nodo nodo = atravesado (vía);
si (node.isFile) { // archivo: devolver su propio nombre
Criar [] partes = camino.split("/");
devolver Collections.singletonList(parts[parts.length - 1]);
}
devolver nuevo ArrayList recomendado(node.children.keySet());
}

Crear directorios a lo largo del camino dado */
public void mkdir(String path) {
Traverse(path); // el método transversal crea automáticamente nodos perdidos
}

* Aplicar contenido a un archivo; crear archivo si falta */
public void addContentToFile(String filePath, String content) {
Nodo nodo = transversal(filePath);
Nodo. isFile = true;
node.content.append(content);
}

* Devuelve el contenido completo de un archivo */
public String readContent FromFile(String filePath) {
Nodo nodo = transversal(filePath);
retorno node.content.toString();
}

* Ayudante: caminar por el camino, creando nodos según sea necesario */
privado Node traverse(String path) {
Nodo cur = root;
si (path.equals("/") devuelve el curro;
Criar [] partes = camino.split("/");
para (int i = 1; i)
cur.children.putIfAbsent(parts[i], new Node());
cur = cur.children.get (parts[i]);
}
Volver cur;
}
}
`` `

■ **Key Java-specific options* *
* " TreeMap " → Ordenación lexicográfica integrada.
* `StringBuilder` para el gasto de cadena eficiente.
* `putIfAbsent` mantiene el código ordenado.

-...

#### 3.2 Python

``python
clase FileSystem:
Clase Nodo:
__slots__ = ('is_file', 'content', 'niños')
def __init__(self, is_file=False):
self.is_file = is_file
autor.content = [] # lista de cuerdas, eficiente concat
self.children = {} Node

def __init__(self):
self.root = self.Node()

def ls(self, path: str) - título list[str]:
nodo = yo._traverse(path)
si node.is_file:
[path.split('/')[-1]
(nodo.niños)

def mkdir(self, path: str) Ninguno.
auto._traverse(path) # crea nodos en la mosca

def addContentToFile(self, filePath: str, content: str) - Conf Ninguno.
nodo = self._traverse(filePath)
node.is_file = True
node.content.append(content)

def readContent FromFile(self, filePath: str) - título str:
nodo = self._traverse(filePath)
volver ''.join(node.content)

def _traverse(self, path: str) - título 'FileSystem. Node:
cur = self.root
si camino == '/':
Retorno
por parte en el camino.strip('/').split('/'):
si parte no en curs.niños:
cur.children[part] = self.Node()
cur = cur.children[part]
Retorno
`` `

■ **Python tricks* *
* `_______ → huella de memoria más pequeña.
* `list` para contenido → evita la concatenación de cadenas cuadráticas.
* " surtido() " en `ls ' garantiza el orden.

-...

### 3.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

clase FileSystem {
privado:
struct Node {}
bool isFile = false;
contenido de cadena; // sólo se utiliza si esFile==true
mapa realizado, Nodo* Niño; // orden lexicográfico por defecto
Nodo() = default;
};
Node* root;

// Ayudante: camina por un camino, creando nodos según sea necesario
Nodo* traverse(contiguo camino de cuerda reducida) {
Nodo* cur = raíz;
si (pátula == "/") el curro de retorno;
stringstream ss(path);
parte de cuerda;
getline(ss, part, '/'); // skip leading '/ '
mientras (obline(ss, parte, '/))) {}
si (!cur- confíachildren.count(part))
cur-iéndolos[parte] = nuevo Nodo();
cur = cur- " hijos " ;
}
Volver cur;
}

public:
FileSystem() : root(new Node() {}

vector asignados confiar ls(camino de cuerda) {
Nodo* nodo = atravesado (vía);
si (nodo- confíaisFile) {
nombre de la cadena = camino.substr(path.rfind('/') + 1);
devolver {nombre};
}
vectoriales res;
para (cont auto cosecha kv : node-clientes) res.push_back(kv.first);
restitución;
}

vacío mkdir(carril de búsqueda) { atravesado(vía); }

vacio añadirContentToFile(archivo de la cadenaPath, contenido de la cadena) {
Nodo* nodo = transversal(filePath);
node- títuloisFile = true;
node-contenido += contenido; // cadena concatenación está bien aquí
}

string readContentDesdeFile(string filePath) {
Nodo* nodo = transversal(filePath);
nodo de retorno-contenido;
}
};
`` `

■ **C++ especificos**
* `map` garantiza teclas ordenadas.
* `stringstream` → ruta limpia división.
< < > > > > > > > > > > > > > > > > > > > > > > > > > > > > .

-...

## 4. Análisis de la complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio `ls` Silencio **O( profundidad + k log k)** (`k` = número de artículos en el dir) Silencio O(k) para la lista de resultados
Silencioso `mkdir` Silencio **O(a fondo)** Silencio O(a fondo) para nuevos nodos
Silencio `addContentToFile` Silencio **O(a fondo)** Silencio O(1) para el nodo, + O(len(content)) para appending ¦
Silencio `readContentDesdeFile` Silencio **O(a fondo)** Silencio O(1) para el nodo

■ El ** profundo** está ligado por la longitud máxima del camino (≤ 10^4 caracteres) – en la práctica muy pequeña, por lo que todas las operaciones son efectivamente O(1) para fines de entrevista.

-...

## 5. Bien, Bad & Ugly – Lo que los gerentes de contratación buscan

Silencio Lo que debe destacar Silencio ¿Qué hay que ver para Silencio
Silencio--------------------------------
Silencio **Bueno** Silencio • Estructura clara del árbol realizadabr confianza• clasificación Lexicográfica vía `TreeMap`/`map` obedecbr título• Único ayudante de traversal Silencio Shows * código limpio* " reutilizabilidad*. Silencio
Silencio **Bad** Silencio • Sendero de división por `/` es **O(len(path))** – bien aquí, pero puede ser caro para árboles enormes. La optimización excesiva puede perjudicar la legibilidad. Silencio
Silencio **Ugly** Silencio • Funda de borde de `/` raíz indicadabr confianza• Cadena vacía después de la división (slash líder) Detección de directorios de archivo vs tención Los errores pequeños en estos lugares hacen que el código no prueba. Silencio

**Consejo:** Siempre agregue un arnés de prueba que imita el ejemplo LeetCode. Te obliga a pensar en casos de borde temprano.

-...

## 6. Puntos de discusión para entrevistas

1. ¿Por qué un árbol? #
* Los sistemas de archivos son naturalmente jerárquicos – un árbol es la abstracción más natural.
* El mapa de los niños de cada nodo le permite saltar de un nivel a otro en *O(1)*.

2. ** Listas de reproducción clasificadas**
* `TreeMap` / `std::map` mantener las llaves ordenadas automáticamente - no extra `sort()` Llama.
* En Python, ` surtido()` en las llaves funciona bien porque los diccionarios no son surtidos.

3. **Path Parsing**
* `split('/')` funciona pero deja una cadena vacía en el índice 0 para caminos absolutos.
* `putIfAbsent` / `children.emplace` crear directorios desaparecidos sin un cheque de existencia separado.

4. **Mimory Footprint* *
* Cada nodo del directorio almacena un `TreeMap` o `unordered_map`.
* Los archivos almacenan sólo un `StringBuilder` / `list`.
* La entrada típica de LeetCode es pequeña; el uso del mundo real requeriría persistencia o compresión.

5. *Manipulación del espejo*
* El problema oficial garantiza caminos válidos – pero en la vida real añadiría validación " lanzar excepciones descriptivas.

-...

## 7. Cómo esto te ayuda a conseguir un trabajo

← Habilidad Silencioso Ejemplo de FileSystem Silencio Cómo los reclutadores la ven
Silencio--------------------------
Silencio **Diseño de estructura de datos** Silencio Árbol de `objetos de nodo Silencio Muestras que puedes modelar sistemas de mundo real. Silencio
TEN ** Pensamiento algorítmico** TENIDO O(a fondo) traversal TENIENDO Destaca la resolución eficaz de problemas. Silencio
Silencio **Maestría en idiomas** Silencio Java `TreeMap`, Python `dict`, C++ `map` ¦ Demonstrates language-specific best practices. Silencio
Silencio **Testing " debugging** Silencio Escribe pruebas unitarias para cada método ← Proves you value correctness. Silencio

Cuando usted enumera este problema en su curriculum vitae o lo discute en una entrevista, use ** palabras clave** que los reclutadores buscan:

* **In‐memory file system* *
*LeetCode 588*
* **Design In‐Memory File System**
* **Entrevista de estructuras de datos**
* *Job Interview**
* **Coding Interview**

Menciona los idiomas con los que te sientes cómodo y destaca que puedes adaptar la lógica central a través de **Java, Python, C+**—una señal clara de * experiencia multiplataforma*.

-...

## 8. Esquema de publicación del blog de muestra (SEO‐Optimized)

### Title
**“LeetCode 588 – Design an In‐Memory File System (Java, Python, C++)

## Meta Descripción
■ Master LeetCode 588 e impresiona a los gerentes de contratación. Lea la solución completa en Java, Python y C+++ más una profunda inmersión en las decisiones de diseño y consejos de entrevista.

## Headings (H1–H4)

Palabras claves de SEO Silencio
Silencio...
* LeetCode* 588 – Design an In‐Memory File System ← `in-memory file system`, `LeetCode 588`
tención **H2:** Resumen del problema " Constraints TENIENDO `problema statement ' , `coding interview` Silencio
tención **H2:** Data‐Structure Design Silencioso `tree data structure`, `node`, `directory ' , `file`  durable
Silencio **H3:** Aplicación de Java ANTE `Java`, `TreeMap`, `StringBuilder` Silencio
Silencio **H3:** Aplicación de Python: `Python`, `dict`, `sorted()` Silencio
tención **H3:** C+++ Aplicación voca `C++`, `std::map`, `unordered_map` voca
tención **H2:** Rendimiento " Comercios " , " complejidad espacial " Silencio
tención **H2:** Common Pitfalls " Edge Cases " , `root path ' , `file vs directory ' Silencio
Silencio **H2:** Cómo se prepara este problema para las entrevistas Silencioso `entrevista de codificación ' , `ingeniero de software ' , `entrevista de trabajo `

### Ejemplo Blog Extracto

■ *“En este post descomponemos el problema de sistema de archivos más duro de LeetCode, mostramos cómo codificarlo en Java, Python y C++, y explicamos las opciones de diseño que impresionarán a tus entrevistadores. Desde la estructura del árbol que mantiene a los directorios ordenados a los sutiles quirks de la persiana del camino, cubrimos todo lo que necesitas saber para asar la entrevista y la tierra que el trabajo de ensueño.”*

-...

## 9. Script de prueba rápida (opcional)

``python
si __name_ == "__main__":
fs = FileSystem()
fs.mkdir("/a/b/c")
fs.addContentToFile("/a/b/c/d", "hello")
print(fs.ls("/")
print(fs.ls("/a/b/c")
print(fs.readContentDesdeFile("/a/b/c/d))
`` `

Siéntase libre de pegarlos en su IDE favorito o compilador en línea para probar más adelante.

-...

## 10. Final Takeaway

* ** abstracción total** (Nodo + árbol) + ** recipiente surtido** = una solución limpia y sostenible.
* La misma lógica básica funciona a través de **Java, Python, C+** – un gran punto de prueba de entrevista.
* Comprender este problema fortalece su conocimiento *data‐structure*, una habilidad imprescindible para cualquier entrevista **software-engineering**.

Pruebe esto, agréguelo a su cartera, y observe esas ofertas de trabajo enrollar! 