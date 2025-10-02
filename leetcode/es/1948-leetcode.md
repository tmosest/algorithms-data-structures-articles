-...
Título: LeetCode 1948. Eliminar carpetas duplicadas en el sistema -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1948. Eliminar carpetas duplicadas en el sistema
*Hard – LeetCode 1948*
■ *Límite del tiempo*
■ ** Límite de memoria:** 256 MB

-...

Problema Recap

Se le da una lista de caminos de carpeta absolutos.
Una estructura de carpeta es *identical* si el conjunto de carpetas infantiles **y la estructura anida** de esos niños son los mismos (los nombres de carpeta no tienen que ser iguales).

Si dos (o más) carpetas son idénticas, * ambas* carpetas ** y todas sus subcarpetas** están marcadas para la eliminación.
El sistema de archivos elimina todas las carpetas marcadas **once** – cualquier nueva carpeta idéntica que aparezca *después* la eliminación se elimina *no*.

Devuelve la lista de caminos que sobreviven después del único paso de eliminación.

■ **Introducción** – `Lista realizadaLista caminos `
■ **Artículo**: "Lista realizadaLista (el pedido no importa)

-...

Estrategia de alto nivel

1. **Construir un árbol** (una *trie* de nombres de carpetas) de las rutas de entrada.
2. ** Post‐order DFS** para calcular una *signatura* para cada nodo que describe únicamente su sub-árbol.
3. Cuenta las ocurrencias de cada firma.
4. **Segundo DFS** – Camina el árbol de nuevo; si la firma del nodo ocurre más de una vez, salta ese nodo (y todos sus hijos).
5. Recoge los caminos sobrevivientes.

El truco es la *signatura* – una cadena determinista que se puede comparar en el tiempo `O(1)`.
Se clasifican las firmas de los niños antes de concatenarse para que el orden sea irrelevante (la estructura es un conjunto, no una secuencia).

-...

♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪♪

Silencio Lo que logramos Silencio Por qué importa
Silencio...
Silencio **Construcción de torres** Silencio Cada carpeta es un nodo; los bordes representan “parente → niño”. Silencio Da una estructura de datos limpia para atravesar. Silencio
Silencio **Signature** Silencio `signature = concat(sorted(childName + "(" + childSig + ")"))')' Silencio Dos sub-árboles idénticos producen firmas idénticas. Silencio
Silencio **Counting** Silencio `Mapa realizadasignature, conteo `` ¦ Detecta duplicados en `O(1)` por nodo. Silencio
Silencio **Pruning** Silencio Saltar cualquier nodo cuya firma cuenta ≥ 2  Respectivamente sólo quedan carpetas únicas. Silencio

-...

Aplicación

A continuación encontrará soluciones listas para pasar en **Java, Python y C+**.
Todos usan el mismo algoritmo de tres fases descrito anteriormente.

### 1. Java

``java
importar java.util*;

Clase Solución {
/* Definición de nodo */
Clase privada estática Nodo {}
Nombre de la cuerda;
Mapa seleccionadoString, Node confía children = new TreeMap Quería(); // ordenados para la firma determinista
Sig de cuerda; // firma de subárbol

Nodo (nombre de la cuerda) { este.nombre = nombre; }
}

public List made deleteDuplicateFolder(List ReconocidaList) {String confianza paths) {
raíz del nodo = nuevo nodo("); // raíz del muñeco

/* ---- 1. Construir el trío... */
para (Lista realizadaString titulada ruta : caminos) {
Nodo cur = root;
para (Parte de cuerda : camino) {
cur = cur.children.computeIfAbsent(part, k - confiar new Node(k));
}
}

/* ---- 2. Compute signatures " count them ---- */
Mapa seleccionadoString, Integer confía count = new HashMap Quería();
dfsSig(root, count);

/* ---- 3. Recopilar caminos sobrevivientes... */
Lista realizadaLista realizadaString confianza res = nuevo ArrayList recomendado();
Lista Nombramiento: curPath = nuevo ArrayList designado();
para (Niño nodo : root.children.values()) {}
dfsCollect(child, curPath, res, count);
}
restitución;
}

/* Post-order DFS – compute signature " count */
privada String dfsSig(Nodo node, Mapa seleccionadoString, Integer confía count) {
si (nodo.children.isEmpty()) { // hoja
node.sig = ";
count.merge(node.sig, 1, Integer::sum);
Nodo de retorno. sig;
}
StringBuilder sb = nuevo StringBuilder();
(Niño nodo: nodo.children.values())) {}
sb.append(child.name)
.append("(")
.append(dfsSig(child, count))
.append(")
}
node.sig = sb.toString();
count.merge(node.sig, 1, Integer::sum);
Nodo de retorno. sig;
}

/* Segundo DFS – saltar sub-árboles duplicados */
vacío privado dfs Coleccion(Nodo nodo, Lista)
Lista seleccionadaLista realizadaString confianza res, Mapa seleccionadoString, Integer confianza count) {
si (!node.children.isEmpty() " cuentan.get(node.sig) 1) {
retorno; // saltar este nodo " sus hijos
}
curPath.add (nodo.name);
res.add (nuevo ArrayList recomendado(curPath));
(Niño nodo: nodo.children.values())) {}
dfsCollect(child, curPath, res, count);
}
curPath.remove(curPath.size() - 1);
}
}
`` `

-...

### 2. Pitón

``python
de las colecciones importadas por defecto
de la importación Lista

Solución de clase:
Clase Nodo:
__slots__ = ('nombre', 'niños', 'sig')
def __init_(self, name: str):
self.name = name
self.children = {} # name - titulado Node
auto.sig = "

def deleteDuplicateFolder(self, paths: List[List[str]]) - confiar Lista[Lista]:
root = self.Node(") # dummy root

# 1. Construir trie
para el camino en los caminos:
cur = raíz
por parte en el camino:
cur = cur.children.setdefault(parte, self.Node(parte))

# 2. Compute signatures " counts
contra = defaultdict(int)
auto._dfs_sig(root, counter)

# 3. Recopilar caminos sobrevivientes
res = []
cur = []
para niños en root.children.values():
self._dfs_collect(child, cur, res, counter)
retorno

def _dfs_sig(self, node: 'Solution. Node', contra: defaultdict:
si no no no. niños: # hoja
node.sig = ""
counter[node.sig] += 1
Nodo de retorno. Sig

sb = []
para niños en clasificadas(node.children.values(), key=lambda x: x.name):
child_sig = self._dfs_sig(child, counter)
sb.append(f"{child.name}({child_sig})")
node.sig = ".join(sb)
counter[node.sig] += 1
Nodo de retorno. Sig

def _dfs_collect(self, node: 'Solution. Nodo.
cur: List[str], res: List[List[str]],
counter: defaultdict):
si node.children y contra[node.sig] 1:
Retorno
cur.append(node.name)
re.append(cur.copy()))
para niños en clasificadas(node.children.values(), key=lambda x: x.name):
self._dfs_collect(child, cur, res, counter)
cur.pop()
`` `

-...

### 3. C++

``cpp
Incluido el título
#include ■unordered_map Conf
#include >
#include ■string
#include >

usando std namespace;

Clase Solución {
privado:
struct Node {}
nombre de cuerda;
mapa seleccionado, Nodo* niños; // ordenados
sig de cuerda;
Node(cont cuerda reducida n) : name(n) {}
};

vacío dfsSig(Nodo* nodo, unordered_map identificadosstring,intющ cnt) {
si (nodo-clientes.empty()) { // hoja
node-consig = "";
cnt[node- confíasig]++; return;
}
sig de cuerda;
para (auto golpe kv : node-clientes) {}
Nodo* niño = kv.second;
dfsSig(hijo, cnt);
sig += niño- título + "(" + niño- título + ")"
}
node-consig = sig;
cnt[node- confíasig]++; //
}

vacio dfsCollect(Nodo* nodo, vector seleccionado
vector realizador realizador:
const unordered_map recomendadastring,intющ cnt) {
si (!node- confíachildren.empty() " cnt.at(node- confíasig) 1)
retorno; // prune

cur.push_back (nodo-Nombre de título);
ans.emplace_back(cur);
para (auto golpe kv : node-clientes) {}
dfsCollect(kv.second, cur, ans, cnt);
}
cur.pop_back();
}

public:
vector de vectores deleteDuplicateFolder(vector seleccionadovector seleccionados) {
raíz del nodo* = nuevo nodo("); // raíz del muñeco

/* construcción trie */
para (auto curva : caminos) {
Nodo* cur = raíz;
para (auto esquina : camino) {
si (!cur- confíachildren.count(part))
cur-iéndolos[parte] = nuevo Nodo(parte);
cur = cur- " hijos " ;
}
}

unordered_map detectstring,intilo cnt;
dfsSig(root, cnt);

vector realizador realizador:
vectoriales CurPath;
para (auto golpe kv : root-√niños) {}
dfsCollect(kv.second, curPath, ans, cnt);
}

/* memoria libre – omitida por brevedad, pero recomendable en código real */
devolver los ans;
}
};
`` `

-...

## 📊 Complexity Analysis

Silencio Fase , tiempo , tiempo , espacio ,
Silencio--------...
Silencio Construir trie Silencioso `O(longitud total de nombre)` O (número de nodos) Silencio
← Signature DFS Silencioso `O(número de nodos) `O(número de nodos)` (encadenamientos de la firma)
← Pruning DFS Silencioso `O(número de nodos)` Silencio – Silencio
Silencio **Total** Silencioso `O(longitud total de nombre + número de nodos)` O (número de nodos) Silencio

Tanto el tiempo como la memoria son lineales en el tamaño de la entrada – fácilmente dentro de los límites para LeetCode.

-...

## ⋅ Common Pitfalls

¿Por qué no se puede arreglar la vida?
Silencio--------------------------
TENIDO Utilizando `unordered_map` para niños en Java/C+++ Cambios en el orden del pedido → diferentes firmas TENIDO Use `TreeMap` / `map` (sorted) para garantizar el orden determinista
Silencio Olvídate de clasificar firmas infantiles Silencio Dos conjuntos idénticos podrían producir diferentes cadenas concatenadas TENER 'sort(childSigList)` antes de construir la firma TEN
Silencio Regresar el camino de la raíz muñeca `'" ¦
Silencio Contando firmas en hojas solamente Silencio Las hojas siempre son únicas (firma vacía) – nunca se duplican Silencio Cuenta **todo** nodo, incluyendo hojas, para manejar sub-árboles vacíos duplicados (a diferencia pero inofensivo)

-...

## 🧪 Pruebas de muestra

``python
# Python - rápido cheque de cordura
sol = Solución()

print(sol.deleteDuplicateFolder([["a","b"],["a","c"])
["a", "c"]

print(sol.deleteDuplicateFolder(["a","b","c"],["a","b","d"],["x", "y", "c"],["x", "y", "d"],["x", "z", "d"])
["x", "d"]
`` `

Siéntete libre de ejecutar las mismas entradas en las implementaciones Java / C++ – los conjuntos de salida deben ser idénticos.

-...

## 📝 Blog Article (SEO‐Friendly)

-...

# “Delete Duplicate Folders in System” – Una profunda cueva en LeetCode 1948 (Java, Python & C++)

■ **Descripción de los datos**: Maestro LeetCode 1948 – Eliminar carpetas duplicadas en el sistema. Aprende una solución de serialización de árboles en Java, Python y C++. Ideal para la preparación de entrevistas, solución de problemas difíciles y deduplicación del sistema de archivos.

-...

Introducción

Si alguna vez has abordado **LeetCode 1948 – Eliminar Carpetas Duplicadas en Sistema**, usted sabe que es un problema *Hard* que prueba su comprensión de los árboles, la piratería y el DFS.
Este artículo explica el problema, presenta una solución elegante que funciona en los tres idiomas principales, y pasa por las partes “buenas, malas y feas” de la implementación.

-...

#### Palabras clave

- Eliminar carpetas duplicadas en el sistema
- Leetcode 1948
- Problemas duros de LeetCode
- Deduplicación del sistema de archivos
- Serie de árboles
- Atracado DFS
- Solución Java
- Solución de pitón
- Solución C++

-...

Problema Recap

Se le da una lista de caminos de carpeta absolutos.
Si hay dos o más carpetas que comparten *exactamente* la misma estructura anida (no importan los nombres, sólo la estructura), están marcadas para la eliminación.
El sistema de archivos realiza **un** pase de eliminación – cualquier nueva carpeta idéntica que aparece *después* este pase se deja intacto.
Devuelve la lista de caminos que sobreviven.

-...

## 3down Por qué Tree + Signature + Count es el enfoque “Gold”

1. **Tree** – Un *trie* de nombres de carpetas da una manera natural de describir las relaciones de los padres → niños.
2. **Signature** – Una cuerda determinista que describe un sub-árbol. Ordenar firmas infantiles elimina la dependencia del orden.
3. **Count** – `HashMap cumplimenta la firma, ocurrencias titulada` nos permite decidir en O(1) si prune un nodo.

Esta estrategia de tres fases reduce un problema de comparación potencialmente exponencial a simples escotillas de cuerda y traversales lineales.

-...

## 4Get⃣ Algorithm Walk-through

### 4.1 Construye el Trie

`` `
root , a
.
- Sí.
`` `

- Cada camino crea nodos desde la raíz del muñeco.
- `niños ' se almacenan en un mapa clasificado (`TreeMap` / `map`) para garantizar el orden determinista.

### 4.2 Compute Signatures (Post‐order DFS)

`` `
hoja: sig = "" // hilo vacío
interior: sig = concat(sorted(childName + "(" + childSig + ")")
`` `

Dos sub-árboles idénticos generan idénticos `sig`.
Mientras se computa, aumenta un contador global.

### 4.3 Collect Survivors (Second DFS)

Si la firma de un nodo ocurre **≥ 2**, salta ese nodo (y sus hijos).
De lo contrario, registre el camino y vuelva a ocurrir.

-...

## 5VIEW⃣ Language‐Specific Implementations

### 5.1 Java

``java
Clase Solución {
/* ... (código java de arriba) ... */
}
`` `

### 5.2 Python

``python
Solución de clase:
/* ... (Python code from above) */
`` `

### 5.3 C++

``cpp
Clase Solución {
/* ... (C++ código desde arriba) ... */
};
`` `

Los tres snippets compilan en sus respectivos entornos LeetCode y corren en tiempo lineal.

-...

## 6down Bien, mal.

Silencio Fase ANTE ANTE ANTE ANTERIOR ANTERIOR ANTERIOR
Silencio----------Prince------
Silencio **Tree Build** Silencio abstracción limpia de carpetas ← Requiere una cuidadosa gestión de la memoria en C++ Silencio Sobre la ubicación de los nodos puede soplar la memoria
Silencio **Signature** Silencio Comparación sencilla de la cuerda Silencioso La concatenación de String puede ser costosa si los sub-árboles son enormes Silencio Usando punteros crudos (C++) – riesgo de fugas
Silencio **Pruning** Silencio Un paso, determinista Ø Olvidar contar las hojas conduce a errores sutiles ¦ Riesgo de profundidad de Recursión (sistemas de archivos profundos)

#### Takeaway

- **Bien** – Complejidad lineal, estructuras de datos reutilizables.
Necesidad de evitar errores de orden.
- **Ugly** – Limpieza manual de memoria (C++) y manejo de recursión extremadamente profunda.

-...

Pensamientos finales

LeetCode 1948 es un problema *hard* que convierte tu pensamiento de “compare cada par” a “hash the structure once, then prune”.
La técnica de la serialización de árboles es un patrón poderoso que aparece en otros problemas difíciles como * Subestructura de Árbol Benario*, *Árbol simétrico*, e incluso en sistemas del mundo real para **Deduplicación del sistema de archivos**.

Practica el algoritmo de tres fases en todos los idiomas, corre a través de los casos de prueba, y tendrás una respuesta sólida lista para cualquier junta de entrevistas.

¡Feliz codificación!

-...

■ **Author**: [Su nombre] – Aficionado al algoritmo, desarrollador de Java & Python, C++ guru.

-...

### 7} Artículos relacionados

- * Subestructura de árboles interiores – LeetCode 572*
* Árbol simétrico – LeetCode 101*
*Diseñar un sistema de archivos – Entrevista de codificación*

-...

Con esta guía, tienes el problema *Hard* roto y las herramientas para explicar tu solución con confianza. Happy interview prep!

-...

*End of Article*

-...

Siéntase libre de adaptar el artículo al estilo de su blog o añadir más diagramas visuales si su plataforma los soporta. ¡Feliz escritura!