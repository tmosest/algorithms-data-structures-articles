-...
Título: LeetCode 1257. Región Común más pequeña -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📚 1257 – Smallest Common Region
■ *“Encontrar el más pequeño ancestro común de dos nodos en una jerarquía”*
■ **Idiomas**: Java TENIDO Python ANTE C++
■ **SEO Palabras clave**: Región más pequeña, LeetCode 1257, LCA en un árbol, Traversal de árbol, pregunta de entrevista de Java, problema de entrevista de Python, C++ entrevista codificación

-...

Sinopsis del problema

Se nos da una jerarquía de regiones geográficas.
Cada lista de entradas `regiones[i]` es de la forma

`` `
[padre, niño1, niño2, ...]
`` `

* `parent` **directamente** contiene todo `niño*.
* La relación es transitiva – si *A* contiene *B* y *B* contiene *C*, entonces *A* contiene indirectamente *C*.

Dados dos nombres de región ( " registro1 " , " registro2 " ) debemos regresar ** la región más pequeña que contiene ambos**.
Está garantizado que tal región exista (la raíz del árbol).

■ Ejemplo
"Quebec", "región 2 = "Nueva York" → **“América del Norte”**

-...

## 2down La visión del núcleo

La jerarquía es un árbol arraigado ** donde cada nodo tiene *exactamente uno* padre.
Encontrar la región más pequeña común es equivalente a encontrar el **Ancestro Común más bajo (LCA)** de los dos nodos.

Dos formas clásicas de resolver problemas LCA:

TENIDO TERRIENTE TENIDO Tiempo TENIDO Espacio ANTERIOR Cuando se utiliza
Silencio--------------------------------------------
Silencio **Parent‐Map + Set** (nuestra solución) Silencio `O(N)` para construir mapa + `O(H)` para atravesar los antepasados de cada nodo TENIDO `O(N)` para mapa, `O(H)` para establecer la vida Simple, ninguna estructura de árbol adicional necesaria, trabaja para cualquier `H` ≤ `N` TENIDO
Silencio **Binary Lifting / Euler Tour + RMQ** Silencio `O(log N)` por consulta después de `O(N log N)` preprocesamiento Silencio `O(N log N)` Necesitado cuando muchas consultas sobre un gran árbol estático  sometida

Debido a que el problema pide una sola consulta, el primer enfoque es el más natural y fácil de implementar en cada idioma.

-...

Algoritmo (Parent‐Map + Set)

1. **Construir un niño → mapa de los padres* *
Por cada lista:
* `parent = L[0]`
* Por cada niño en `L[1 ...]`, mapa `niño → padre`.

2. *Ancestros colectivos de la `región1'*
Camine de la `región1` a la raíz, insertando cada nodo visitado en un conjunto de hash.

3. **Encontrar el primer ancestro común**
Camina de la "región 2".
El primer nodo que aparece en el conjunto es la región común más pequeña.

Debido a que la altura del árbol es en la mayoría de `N`, cada caminata toma `O(H)` tiempo.

-...

Complejidad

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio Construir mapa Silencioso `O(N)` Silencio
Silencio Walk `region1` Silencio `O(H)` Silencio `O(H)` Silencio
Silencioso `región2` Silencio `O(H)` Silencio
Silencio **Total** Silencioso `O(N)` Silencio

`N` = número total de regiones (`≤ 10^4`), `H` = altura de los árboles (`≤ N`).

-...

Aplicación

A continuación se presentan implementaciones limpias y listas de producción para **Java, Python y C++**.
Los tres siguen los mismos pasos algorítmicos y utilizan las mismas convenciones de nombres.

▪ restablecimiento **Tip** – Siempre lee la entrada en las estructuras de datos correctas (por ejemplo, `Lista efectuadaLista realizadaLista realizadaString confianza `` en Java, `List[List[str]] ' en Python, `vector asignadovector seleccionado, indicando confianza ` en C++).
> **Edge Cases** – La raíz puede aparecer como un niño en una lista diferente? No – el problema garantiza un padre único por niño, por lo que nuestra construcción de mapas es segura.

### 5.1 Java

``java
importar java.util*;

Solución de la clase pública {}
*
* Encuentra la región más pequeña que contiene ambas regiones1 y región2.
*
* Regiones de los pares Lista de listas de regiones. El primer elemento de cada lista es el padre,
* el resto son sus hijos directos.
* @param region1 El nombre de la primera región.
* @param region2 El segundo nombre de la región.
*Retorno El nombre de la región común más pequeña.
*/
public String findSmallestRegion(ListectoListectoList madeString confianza regiones,
Región de cuerdas1, región de cuerdas2) {
// 1. Construir niño → mapa de padres
Mapa seleccionadoString, String titulada childParent = new HashMap贸();
para (Lista seleccionadaString ratio : regiones) {}
Criar padre = list.get(0);
para (int i = 1; i) i++) {
childParent.put(list.get(i), parent);
}
}

// 2. Ancestros de la región1
Establecer:Ancestros de contactos = nuevo HashSet incorrecto();
mientras (región1 != null) {
ancestros.add(región1);
region1 = childParent.get(region1);
}

// 3. Camina de la región2 para encontrar el primer antepasado común
mientras (región2 != null) {
si (ancestors.contains(region2)) {
región de retorno2;
}
region2 = childParent.get(region2);
}

// Garantizado por el problema que existe una región común.
Retorno nulo;
}

// Ejemplo de uso / prueba
public static void main(String[] args) {
Solución sol = nueva solución ();
Lista realizadaLista(s)String titulada Regiones = Arrays.asList(
Arrays.asList("Earth","North America", "South America"),
Arrays.asList("North America","Estados Unidos", "Canada"),
Arrays.asList("Estados Unidos", "Nueva York", "Boston"),
Arrays.asList("Canada","Ontario","Quebec"),
Arrays.asList("South America","Brasil")
);
System.out.println(sol.findSmallestRegion(regiones, "Quebec", "Nueva York")); / América del Norte
System.out.println(sol.findSmallestRegion(regiones, "Canadá", "South America")); / Tierra
}
}
`` `

### 5.2 Python

``python
de la importación Listo, Dict, Set

Solución de clase:
def findSmallestRegion(
auto,
regiones: Lista[Lista],
región1: str,
region2: str
.
# 1. child - titulado padre mapa
niño_parent: Dict[str, str] = {}
para lst en regiones:
padre = lst[0]
para niños en lst[1:]:
niño_parent[child] = padre

# 2. Ancestros de la región1
ancestros: Set[str] = set()
mientras que la región1 no es Ninguno:
ancestros.add(región1)
region1 = child_parent.get(region1)

# 3. Camina de la región2
mientras que la región2 no es Ninguno:
si región2 en ancestros:
región de retorno2
region2 = child_parent.get(region2)

retorno "" # Unreachable – problema garantiza una solución


# Prueba de ejemplo
si __name_ == "__main__":
sol = Solución()
regiones =
[La Tierra", América del Norte, América del Sur],
["North America","Estados Unidos", "Canadá"],
["Estados Unidos", "Nueva York", "Boston"],
["Canadá", "Ontario", "Quebec"],
["Sudamerica", "Brasil"]
]
print(sol.findSmallestRegion(regiones, "Quebec", "Nueva York") # North America
print(sol.findSmallestRegion(regiones, "Canada", "South America") # Earth
`` `

### 5.3 C++

``cpp
#include ■iostream
Incluido el título
#include ■unordered_map Conf
#include ■unordered_set
#include ■string

Clase Solución {
public:
std::string findSmallestRegion(
const std::vector seleccionado::vector seleccionado:::string regiones,
std::string region1, std::string region2) {

// 1. niño → mapa de padres
std::unordered_map seleccionados::string, std::string ChildParent;
para (continuidad autocorpora lst : regiones) {}
const std::string paciente = lst[0];
para (size_t i = 1; i) ++i) {
ChildParent[lst] = parent;
}
}

// 2. antepasados de la región1
std::unordered_set obtenidosstd::string ancestros;
mientras (!region1.empty()) {}
ancestros.insert(región1);
aut it = childParent.find(region1);
region1 = (it == childParent.end()) ? "" : it- título segundo;
}

// 3. subir de la región2
mientras (!region2.empty())) {}
si (ancestors.count(region2)) región de retorno2;
auto = niñoParent.find(región2);
region2 = (it == childParent.end()) ? "" : it- título segundo;
}

devolver "; // Nunca deberías golpear aquí.
}
};

int main() {}
Sol de solución;
std:::vector seleccionados::vector seleccionados::string regiones =
"La Tierra", "América del Norte", "América del Sur"
"Estados Unidos", "Canadá"
"Estados Unidos", "Nueva York", "Boston"},
"Canada", "Ontario", "Quebec"
América del Sur, Brasil
};

std:::cout ■ sol.findSmallestRegion(regiones, "Quebec", "Nueva York")
std:::cout ■ sol.findSmallestRegion(regiones, "Canada", "South America")
}
`` `

-...

## 6down “El Bien, el Mal, el Ugly”

Silencio Silencio
Silencio------------Prince------
Silencio **Bien** Silencio • Construcción de un mapa – O(N) tiempo & espacio. • Trabaja para cualquier forma de árbol, sin supuestos especiales. • El código es corto, fácil de auditar.
Requiere `O(N)` memoria extra para el mapa – no ideal para árboles gigantescos. • Para muchas consultas repetidas, pagamos la construcción del mapa de `O(N) cada vez.
Silencioso **Ugly** Si las listas de entrada no son surgidas o contienen duplicados, el mapa puede sobreescribir a los padres. El algoritmo *no* detecta ciclos – asume un árbol válido según las limitaciones. En idiomas como Python, la profundidad de recursión es irrelevante aquí, pero un traversal basado en pilas es más sencillo.

*Lo que los entrevistadores realmente quieren*
- Corrección para todos los casos de borde (sólo raíz, jerarquías profundas).
- Razonamiento claro sobre por qué el algoritmo encuentra la región común *smallest* (el primer ancestro común caminando hacia arriba).
- Discusión de tiempo/espacio - mencionar que una solución de elevación binaria reduciría el tiempo de consulta a costa de más memoria y preprocesamiento.

-...

Consejos de entrevista

1. **Clarificar el recuento de consultas** – preguntar si se pueden necesitar múltiples consultas.
2. **Declarar las limitaciones** – confirmar que cada niño tiene sólo un padre y ningún ciclo.
3. **Mostrar el “primer antepasado común” intuición** – muchos candidatos pasan por alto que el paseo debe comenzar desde la “región1” y utilizar un conjunto.
4. **Explicar la complejidad** – destacar el preprocesamiento lineal y el ancestro lineal traversal.
5. **Pregunte sobre el preprocesamiento** – un buen seguimiento: “Si tuviéramos 105 consultas, ¿qué cambiarías?” – respuesta con levantamiento binario / RMQ.

-...

## 8down Pensamiento final

La solución “parent‐map + set” es un ejemplo de libro de texto de **Map-based ancestor tracking**.
Combina legibilidad, sencillez y rendimiento sólido para una sola consulta – exactamente lo que este problema LeetCode requiere.
Con las tres implementaciones de idiomas anteriores, usted está listo para abordar el problema en cualquier entorno de entrevista o producción.

¡Feliz codificación! 🚀

-...

*Si te ha parecido útil esta guía, no dudes en compartirla con tus amigos, o comenta a continuación si tienes preguntas sobre los casos de borde “muy”. *