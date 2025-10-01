-...
Título: LeetCode 1912. Sistema de alquiler de películas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

# The Good, The Bad, and The Ugly» – Solving LeetCode 1912 (Design Movie Rental System)

**Keywords**: LeetCode 1912, Design Movie Rental System, Java, Python, C++, entrevista, estructuras de datos, TreeSet, HashMap, SortedSet, entrevista de trabajo, algoritmo, ingeniero de software

-...

## 1. Recaptación de problemas

■ *Tienes una cadena de tiendas de cine. Cada tienda puede tener ** en la mayoría de una copia** de una película.
■ Para una película dada debe ser capaz de:*
* **search** – devolver las tiendas *cheapest 5* que actualmente poseen una copia *sin experiencia*
* **rent** – marcar una copia específica como alquilada
* **drop** – devolver una copia alquilada
* **informe** – devolver el *cheapest 5* copias alquiladas en todo el sistema

Todas las operaciones deben funcionar lo suficientemente rápido para hasta **100 000** llamadas.
Limitaciones típicas: `1 ≤ n ≤ 3·105`, `1 ≤ entries.length ≤ 105`, `1 ≤ price ≤ 104`.

-...

## 2. Idea de alto nivel

Silencio ** Objetivo** Silencio ** Estructura de la información**
Silencio------------------------------
Silencio Encontrar rápidamente *cheapest 5 copias no aprendidas* para una película Silencioso **`TreeSet` / `std::set` / lista clasificada** de `(precio, tienda, película)` Subtítulos Ordenar por precio → tienda → película → podemos tomar primero cinco
TENIDO Rápido encontrar *cheapest 5 copias alquiladas* en todo el sistema TENIDO Otro **`TreeSet` / `std::set`** de la * misma clave* TENIDO Mismo razonamiento – ordenados globalmente ANTE
← Búsqueda constante de la *exacto artículo* en una tienda Silencio **HashMap shop → película → Artículo** Silencio Necesitado para alquilar / soltar para encontrar el artículo en O(1) antes de moverlo entre sets Ø

Así mantenemos ** tres** estructuras de datos:

1. **`shopMap`** – `Map realizadoshop, Map mademovie, Item titulado `` – fast pointer to a particular copy.
2. ** " sin experiencia "** – " Map hechosmovie, TreeSet indicóItem confidenciales " , todas las copias actualmente no aprendidas de esa película.
3. **`rented`** – `TreeSet madeItem confidencial` – todas las copias alquiladas ordenadas por la orden del informe.

Todas las operaciones ( " investigación " , " caída " , " informe " ) se convierten en " O(log k) " , donde `k ' es el tamaño del conjunto pertinente (≤ 105).

Con estas estructuras obtenemos:

****search** – just iterate first 5 elements → `O(5 log k)` → essentially `O(1)`
* **rent / drop** – quitar de un conjunto, insertar en el otro → `O(log k)`
* **Informe** – iterate first 5 elements of the global rented set → `O(1)`

-...

## 3. Diseño detallado

### 3.1 Item

Silencio Idioma Silencio Representación Silencio
Silencio...
Silencio **Java** Silencio Clase interna `Item` con `shopId`, `movieId`, `price`. Silencio
Silencio **Python** Silencio Simple dataclass / tuple `(precio, tienda, película)` – mantenemos el `shop` adentro para ordenar el informe. Silencio
Silencio **C+** Silencio `estructura Artículo` con `int shop, movie, price;` y una comparación personalizada. Silencio

Los tres usan la orden **same**:
`price`  empleo `shop` ➜ `movie`.
Esto garantiza que el primer elemento en un `TreeSet`/`set` sea siempre la copia *mejor* para `búsqueda ' o `report ' .

#### 3.2 Constructors

Durante la construcción simplemente insertamos cada entrada en:

* el mapa local de la tienda (`shopMap`)
* the global rented set (`rented`) – *empty* at start
* el set de película no aprendiz (`unrented.get(movie)`)

Ninguna operación es `O(n log n)`; estamos haciendo 'O(entries)` inserts, cada uno cuesta a la mayoría `O(log k)` porque creamos una nueva 'TreeSet' para cada nueva película sólo una vez.

-...

## 4. Análisis de la complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio **Constructor** Silencioso `O(inscripciones de registro de entradas)` Silencio `O(entries)` Silencio
Silencio** investigación** (sólo 5 tiradas) Silencio
Silencioso **rent / drop** Silencio `O(log k)` extra para mapa look‐ups
Silencio** (primera quinta parte del conjunto mundial) Silencio

Todos los límites están cómodamente por debajo del requisito de 100 000-operación.

-...

## 5. Aplicación

A continuación encontrará una aplicación **ready‐to-copy** en **Java**, **Python**, y **C+**.
Los tres siguen la misma lógica, adaptada a los contenedores idiomáticos de cada idioma.

■ **Tip for interviewers**:
■ *Explicar el *por qué* detrás de cada opción de estructura de datos – quieren ver que entiende “recolectas surgidas” y “hash-lookup” trade‐offs. *

-...

## 5.1 Java (TreeSet + HashMap)

``java
importar java.util*;

clase pública MovieRentingSystem {
* Una copia de una película en una tienda */
clase privada estática Artículo {
última tienda de entrada Id;
última película de int Id;
precio int final;

Artículo(int shopId, int movieId, int price) {
esto. shopId = shopId;
esto. película Id = película Id;
esto. precio = precio;
}
}

// Comparador utilizado para conjuntos intrínsecos y alquilados
Comparador final estático privado
a, b) - título a.price!= ¿B.price? Integer.compare(a.price, b.price)
: a.shopId!= b.shop Id ? Integer.compare(a.shop Id, b.shopId)
: Integer.compare(a.movie Id, b.movieId);

final privado Mapa seleccionadoInteger, Mapa seleccionadoInteger, Itemilo tiendaMap = nuevo HashMap Contraseña();
mapa final privado realizadoInteger, TreeSet Garantizado = nuevo HashMap garantizado();
Árbol final privadoSet realizadaItem confidencial alquilado = nuevo TreeSet fiel(COMPARATOR);

public MovieRentingSystem(int n, int[][] entries) {
para (int[] e : entradas) {
int shop = e[0], movie = e[1], price = e[2];
Artículo = nuevo Artículo(tienda, película, precio);

// 1. Map shop→movie→ Tema
shopMap.computeIfAbsent(shop, k - título nuevo HashMap correctamente()).put(movie, item);

// 2. Unrented set for this movie
unrented.computeIfAbsent(movie, k - título new TreeSet correctamente(COMPARATOR)).add(item);
}
}

* Devuelve los IDs de la tienda de las más baratas 5 copias no aprendidas de la película dada. */
public List made integer confianza search(int movie) {}
TreeSet hizoItem confidencial set = unrented.getOrDefault(movie, new TreeSet quiso decir(COMPARATOR));
Lista realizadaInteger confía ans = nuevo ArrayList designado(5);
int i = 0;
para (Teemas : set) {
(i+ == 5) ruptura;
ans.add(it.shopId);
}
devolver los ans;
}

* Alquila una copia de una tienda específica. */
public void rent(int shop, int movie) {
Artículo = shopMap.get(shop).get(movie);
unrented.get(movie).remove(it);
alquilado.add(it);
}

Devuelve una copia alquilada. */
public void drop(int shop, int movie) {
Artículo = shopMap.get(shop).get(movie);
rented.remove(it);
unrented.get(movie).add(it);
}

* Devuelve las 5 copias alquiladas más baratas (tienda, película). */
public List made() {) {
Lista realizadaLista realizadaInteger confianza res = nuevo ArrayList recomendado(5);
int i = 0;
para (Loem : alquilado) {
(i+ == 5) ruptura;
res.add(Arrays.asList(it.shop Id, it.movieId));
}
restitución;
}
}
`` `

■ *Por qué es rápido* – Todas las operaciones mutantes tocan sólo dos contenedores ordenados, cada inserción o eliminación es `O(log k)`.

-...

### 5.2 Python (Sorted List + `bisect`)

Python no tiene un "TreeSet" incorporado, pero la biblioteca estándar "bisect" nos permite mantener una * lista surtida* que se comporta como un árbol equilibrado para nuestras limitaciones.

``python
importador bisect
de la importación Lista

Artículo:
__slots__ = ("shop", "movie", "price")

def __init__(self, shop: int, movie: int, price: int):
self.shop = shop
automoción = película
precio = precio

# Key for sorting: (price, shop, movie)
def key(self):
regreso (auto.precio, auto.shop, auto.movie)

def __lt_(self, other: 'Item'):
volver a sí mismo.key()


class MovieRentingSystem:
def __init_(self, n: int, entries: List[List[int]):
# shop → movie → Tema
self.shop_map = {}

# película → lista ordenada de elementos no aprendices
sin experiencia

# lista global de artículos alquilados
self.rented = []

para tienda, película, precio en entradas:
it = Item(shop, movie, price)

self.shop_map.setdefault(shop, {})[movie] = it

si la película no está en sí misma. inquilinos:
self.unrented[movie] = []
# Insertar mientras mantiene la lista ordenada
bisect.insort_left(self.unrented[movie], it)

def search(self, movie: int) - título List[int]:
lst = self.unrented.get(movie, [])
volver [it.shop for it in lst[:5]]

def _remove_from_set(self, lst: List[Item], it: Item):
idx = bisect.bisect_left(lst, it)
# Confiamos en el problema garantiza que el artículo existe
lst.pop(idx)

def _add_to_set(self, lst: List[Item], it: Item):
bisect.insort_left(lst, it)

def rent(self, shop: int, movie: int) - Propiedad Ninguno.
it = self.shop_map[shop][movie]
auto._remove_from_set(self.unrented[movie], it)
auto._add_to_set(self.rented, it)

def drop(self, shop: int, movie: int) - Ninguno.
it = self.shop_map[shop][movie]
auto._remove_from_set(self.rented, it)
auto._add_to_set(self.unrented[movie], it)

def report(self) - título List[List[int]]:
volver [[it.shop, it.movie] para él en auto.rented[:5]]
`` `

* Why `bisect` works*:
La lista siempre está clasificada por `(precio, tienda, película)`. La inserción o eliminación de un solo elemento cuesta `O(log k)` más un cambio de lista (`O(k)`) - pero con 105 elementos todavía está muy por debajo del límite de 100 000-operación.

-...

## 5.3 C++ (std::set + unordered_map)

``cpp
#include יbits/stdc++.h
usando std namespace;

struct Item {}
int shop, película, precio;
Artículo(int s, int m, int p) : shop(s), movie(m), price(p) {}
// clave para clasificar: precio → tienda → película
bool operator made(const Item otro) const {
si (price != other.price) precio de devolución se hizo otro.precio;
si (shop != other.shop) la tienda de vuelta
la película de retorno se hizo otra.
}
};

clase MovieRentingSystem {
// tienda - título (movie - título de propiedad a artículo)
unordered_map seleccionadaint, unordered_map seleccionadaint, Item* shopMap;
// película - título set of unrented items
unordered_map detectint, set madeItem* Norented;
// conjunto global de artículos alquilados
establecido:

public:
MovieRentingSystem(int n, vector seleccionadovector fielint implicados iguales entradas) {
vector:
allItems.reserve(entries.size());

para (autofr e : entradas) {}
int shop = e[0], movie = e[1], price = e[2];
allItems.push_back(news Tema (taller, película, precio));
Artículo* = allItems.back();

shopMap[shop] [movie] = it;
unrented[movie].insert(it);
}
}

vector identificador de confianza(int movie) {}
vector res;
aut it = unrented.find(movie);
si (it == unrented.end()) devuelve res;
int cnt = 0;
para (Item* ip : it- título) {}
si (cnt++ == 5) ruptura;
res.push_back(ip-propios);
}
restitución;
}

alquiler de vacío(int shop, int movie) {
Artículo* ip = shopMap[shop][movie];
unrented[movie].erase(ip);
alquilado.insert(ip);
}

vacio gota (int shop, int movie) {
Artículo* ip = shopMap[shop][movie];
alquilado.erase(ip);
unrented[movie].insert(ip);
}

vector realizado() {
vector de vectores res;
int cnt = 0;
para (Item* ip : alquilado) {
si (cnt++ == 5) ruptura;
res.push_back({ip- títuloshop, ip- títulomovie});
}
restitución;
}
};
`` `

■ ** Limpieza de memoria** – Para brevedad el destructor no libera `Item*`. En una entrevista real lo mencionaría o usaría `unique_ptr`.

-...

## 6. ¿Qué fue el mal? – Pitfalls comunes

1. **Eligiendo el contenedor clasificado equivocado**
*Solución*: Use `TreeSet`/`set` para seguir ordenando; evite soluciones sencillas porque pierde la recuperación del elemento “mejor”.

2. **No compartir la comparación**
* Resultado*: " La investigación " y " el informe " darían diferentes elementos " más adecuados " .
*Fix*: Mantenga una sola comparación para todos los conjuntos ordenados.

3. **Al almacenar sólo el precio en el conjunto global alquilado**
*Problema*: El informe también requiere el ID de la tienda.
*Fix*: Incluya la " tienda " en el artículo o el tuple clave.

4. **Copiar objetos en lugar de almacenar punteros**
*Efecto*: Cada operación mutante crearía nuevos objetos → memoria innecesaria y búsquedas más lentas.
*Solución*: Puntos de venta o referencias a la misma instancia `Item` en todos los conjuntos.

-...

## 7. Takeaway

- ** Colecciones ordenadas** (TreeSet/TreeSet/Set) le dan *constant‐time* la mejor recuperación del elemento.
- ** Hash maps** te dan *O(1)* tienda → película → copy lookup.
- La combinación resuelve tanto *search* como *report* en O(1), manteniendo las actualizaciones baratas.

■ **Recuerde**: La entrevista no es sólo sobre el código de escritura; se trata de demostrar *por qué* sus opciones de estructura de datos hacen que la solución sea eficiente.

¡Feliz codificación y buena suerte en tu próxima entrevista!

-..