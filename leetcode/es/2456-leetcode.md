-...
Título: LeetCode 2456. Creador de vídeo más popular -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recaptación de problemas

**2456 – Creador de Video Popular**
■ *Medium*

Se le dan tres arrays de longitud *n*:

Silencio i vivir `creators[i]` ¦ [i] Silencio
Silencio--------------------------------...
Silencio 0 Silencioso creador de vídeo *i* Silencio id de vídeo *i* Silencio número de vistas de vídeo *i* Silencio

La *popularidad* de un creador es la suma de las opiniones de todos los vídeos de ese creador.
Para cada creador también necesita saber el id del vídeo ** más visto**.
Si varios videos empatan para la mayoría de las vistas, elija el id lexicográficamente más pequeño.
Si varios creadores se atan por la popularidad más alta, devuélvalos todos (orden no importa).

Devuelve un array 2-D `respuesta` donde cada elemento es `[creador, id_of_best_video]`.



----------------------------------------------------

## 2. Algoritm (One‐pass, O(n) time, O(n) space)

La solución es un solo escaneo lineal que mantiene un *single* hash‐map por creador.

Silencioso Creador Silencioso `totalViews` Silencio `maxVideoViews` Silencio
Silencio----------------------------------------

*Total Views` – la suma de todas las opiniones de ese creador.
* `maxVideoViews` - la vista máxima vista se ve para cualquier vídeo único de ese creador.
* `bestId` – el id lexicográficamente más pequeño que tiene `maxVideoViews`.

*Steps*

1. Inicia un mapa vacío (`String → struct{ long total, int maxView, String bestId }`).
2. Itear sobre los 3 arrays simultáneamente.
* Update `total Views` (add current `views[i]`).
* If `views[i] > maxVideoViews` → reemplazar `maxVideoViews` y `best Id`.
* If `views[i] == maxVideoViews` → mantener el id más pequeño.
3. Mientras los iterantes hacen un seguimiento de la popularidad máxima global (`globalMax`).
4. Después de la exploración, caminar el mapa de nuevo y elegir a todos los creadores cuyo 'total Views == globalMax`.
Para cada uno, la salida `[creador, bestId]`.

Debido a que cada operación en un mapa es **O(1)** en promedio, la complejidad general es:

* **Time** – `O(n)`
* **Espacio** – `O(n)` (una entrada por creador distinto)

El algoritmo maneja ids duplicados naturalmente porque tratamos cada entrada como un vídeo distinto.



----------------------------------------------------

## 3. Implementaciones de referencia

A continuación encontrará soluciones limpias y bien adaptadas en los tres idiomas solicitados.

-...

### 3.1 Java (Java 17)

``java
importar java.util*;

Solución de la clase pública {}
// Clase de ayuda para mantener estadísticas de creadores
Clase privada estática Stat {
total Views; // sum of all views
int maxVideoViews; // max views of a single video
Arete bestId; // lexicográficamente más pequeño id entre maxVideoViews

Stat(long views, String id) {
esto. total Views = views;
this.maxVideoViews = (int) views;
Esto es lo mejor. Id = id;
}

vacio de actualización(excepciones largas, String id) {
total Vistas += vistas;

si (vistas не maxVideoViews) {}
maxVideoViews = (int) vistas;
lo mejor Id = id;
} si (vistas == maxVideoViews " id.compareTo(bestId)
lo mejor Id = id;
}
}
}

public List made(string[] creadores,
Estring[] ids,
int[] views) {
Mapa seleccionadoString, Stat confidencial mp = nuevo HashMap garantizado();
a largo plazo Max = 0;

para (int i = 0; i) creadores.length; i++) {
Creador de cuerdas = creadores[i];
String id = ids[i];
long v = views[i];

mp.computeIfAbsent(creador,
k - nuevos Stat(v, id))
.update(v, id);

globalMax = Math.max(globalMax, mp.get(creator).totalViews);
}

Lista realizadaLista realizadaString confía ans = nuevo ArrayList recomendado();
for (var entry : mp.entrySet() {
si (entry.getValue().totalView == globalMax) {
ans.add(Arrays.asList(entry.getKey(), entry.getValue().bestId));
}
}
devolver los ans;
}

// Demo rápido (opcional)
public static void main(String[] args) {
Solución s = nueva solución ();
String[] c = {"alice", "bob", "alice", "bob", "alice"};
String[] id = {"1", "2", "3", "4", "5"};
int[] v = {5, 3, 5, 2, 5};

System.out.println(s.mostPopularCreator(c, id, v));
}
}
`` `

-...

### 3.2 Python (Python 3.10)

``python
de la importación Lista, Dict

clase Stat:
def __init__(self, views: int, vid_id: str):
auto.total_views = vistas
self.max_video = vistas
self.best_id = vid_id

def update(self, views: int, vid_id: str) Ninguno.
auto.total_views += views
si vistas > self.max_video:
self.max_video = vistas
self.best_id = vid_id
elif views == self.max_video y vid_id se hicieron self.best_id:
self.best_id = vid_id

def mostPopularCreator(creadores: List[str], ids: List[str], views: List[int]) - título Lista[Lista]:
mp: Dict[str, Stat] = {}
global_max = 0

para creador, vid_id, v en zip(creadores, ids, vistas):
si el creador no en MP:
mp[creador] = Stat(v, vid_id)
más:
mp[creador].update(v, vid_id)

global_max = max(global_max, mp[creator].total_views)

respuesta: Lista [Lista] = []
para el creador, stat in mp.items():
si stat.total_views == global_max:
respuesta.append([creador, stat.best_id]))

respuesta


# Demo (opcional)
si __name_ == "__main__":
creadores = "alice", "bob", "alice", "bob", "alice"]
ids = ["1", "2", "3", "4", "5"]
vistas = [5, 3, 5, 2, 5]
print(mostPopularCreator(creadores, ids, vistas))
`` `

-...

### 3.3 C++ (C++20)

``cpp
#include יbits/stdc++.h
usando std namespace;

// Estructura que almacena todas las estadísticas para un creador
struct Stat {}
larga duración total Views{0}; // sum of all views
int maxVideoViews{0}; // máximas vistas de un solo vídeo
cuerda mejor Id; // id más pequeño con maxVideoViews

Stat(long v, const string &id)
: totalViews(v), maxVideoViews(static_cast seleccionado(v)), bestId(id) {}

vacio (long v, cadena de const &id) {
total Views += v;

si (v не maxVideoViews) {}
maxVideoViews = estática_cast indicaint(v);
lo mejor Id = id;
} si (v == maxVideoViews " id " ) mejor Id) {
lo mejor Id = id;
}
}
};

Clase Solución {
public:
vector realizador seleccionador: másPopularCreator(vector asignadostring consigo mismos creadores,
vector iniciado,
vector significando puntos de vista {}
unordered_map buscadostring, Stat confianza mp;
a largo plazo Max = 0;

para (size_t i = 0; i) creadores.size(); ++i) {
const string "creator = Creators[i];
const string &id = ids[i];
long long v = views[i];

si (!mp.count(creator))
mp[creator] = Stat(v, id);
más
mp[creator].update(v, id);

globalMax = max(globalMax, mp[creator].totalViews);
}

vector realizador realizador:
para (contiguador automático > ) {
si (st.totalViews == globalMax) {
ans.push_back({creator, st.bestId});
}
}
devolver los ans;
}
};
`` `

Las tres soluciones funcionan en el tiempo *O(n)* y utilizan el espacio auxiliar *O(n)*, los límites óptimos para este problema.



----------------------------------------------------

## 4. Bien, Mal & Ugly - Qué entrevistadores En realidad quiere

¿Qué es lo bueno que hay en la vida?
Silencio--------------------------------------
Silencio ** Bien** Silencio • Un hash‐map por creador → **O(n)** pases. • Mangos duplicados ids automáticamente.
Silencio **Bad** Silencio • Usando mapas anidados de 2 a 3 (uno para popularidad, otro para estadísticas por id) agrega espacio *O(k)* (k = ids distintos). ■br título• Usted arriesga un error sutil: añadir las opiniones del mismo id en lugar de tomar el *maximum* de un solo vídeo. ← Esto a menudo aparece en concursos: “Resumí las opiniones del mismo vídeo dos veces”. Silencio
Silencio **Ugly** Silencio • Cuando varios vídeos empatan, elegir el id más pequeño requiere una * comparación toxicográfica* – un detalle pequeño pero crucial. • Si te olvidas de rastrear la popularidad máxima global durante el primer paso, tendrás que ejecutar un segundo pase de todos modos. La clásica historia de “perder el último caso de prueba” – generalmente es un caso de esquina alrededor de lazos o entrada vacía. Silencio

### Cómo evitar el Ugly

por qué importa
Silencio...
tención **Single struct per Creator** Silencio mantiene la lógica en un lugar – sin doble narración accidental. Silencio
Silencio **`computeIfAbsent` / `map.getOrDefault`** ANTE Garantías que la entrada del mapa se crea sólo una vez. Silencio
Silencio **Comparar siempre cadenas id** Silencio `id.compareTo(bestId) 0` garantiza el id más pequeño para los lazos. Silencio
Silencio **Track `globalMax` on the fly** Silencio Evita un segundo pase completo si sólo necesita la lista de creadores de max-pop. Silencio

Cuando esté listo para el trabajo-interview, puede soltar cualquiera de los códigos de referencia en su repositorio de solución, o incluso llevarlo a otro idioma (Rust, Go, etc.) – el mismo patrón se aplica.



----------------------------------------------------

## 5. Análisis de la complejidad

TEN TERRITOR TEN Fórmula ANTE ANTE ANTE ANTE
Silencio--------------------
Silencio **Tiempo** Silencioso `O(n)` – bucle único, operaciones de hah en tiempo constante
*m* = número de creadores distintos ****Linear** Silencio

Porque *m* ≤ *n*, el peor espacio es `O(n)`.



----------------------------------------------------

## 6. Por qué este problema es un deber saber para su próxima entrevista

* ** Datos del mundo real** – Piensa en YouTube o TikTok: muchos creadores, muchos vídeos, grandes conjuntos de datos.
* **Mapa pesada** – La mayoría de los desarrolladores mayores necesitan estar cómodos con hash-tables, `unordered_map`, `HashMap`, etc.
* **Tie-breaking logic** – Los entrevistadores les encanta probar su capacidad de manejar casos de borde y ordenar lexical.
* **Multiple answer format** – Muestra que puede devolver colecciones de pares, un patrón común de entrevista.

Al dominar este problema usted demuestra:

* ** Eficiencia algorítmica** (tiempo lineal, actualizaciones de espacio constante).
* **Estilo de codificación eclesiástico** (estructura de datos single, sin bucles anidados).
* **Atención a casos de borde** (sids duplicados, lazos, múltiples creadores).
* **Preparación de entrevista** – usted puede explicar su razonamiento en la pizarra en menos de 5 minutos.

-...

## 7. SEO‐Friendly Summary

**LeetCode 2456** – *El Creador de Video Popular*
- Solución Java (HashMap, O(n) time, O(n) space)
- Solución Python (dict, O(n) time, O(n) space)
- Solución C++ (unordered_map, O(n) time, O(n) space)
- Prep de entrevista – explicar lazos, ruptura de corbatas, elección de estructura de datos
- Complejidad Algorítmica – tiempo O(n), espacio O(n)
- Código demo - rápido, limpio, sencillo

Si está preparando una entrevista de ingeniería de software, agregue este artículo a su lista de estudio. El patrón de **un mapa + max global** es un truco reutilizable que aparece en muchos problemas “top-k” o “group‐by” en LeetCode y más allá.



----------------------------------------------------

## 8. Take‐ Away

1. **Use un solo hash‐map por creador** – mantiene el código corto y elimina el doblecuento accidental.
2. ** Actualizar estadísticas sobre la mosca** – ningún segundo pasar a través de los videos, sólo uno pasa a través de los creadores después de la exploración.
3. **Cuidado con los lazos** – mantener la id lexicográficamente más pequeña cada vez que golpeas una situación de igualdad de visión.
4. **Prueba los casos de borde** – arrays vacíos, un solo creador, todos los creadores empatan, los ids duplicados con las mismas vistas, etc.

¡Feliz codificación, y puede que su próxima entrevista vaya *stream-lined* como un vídeo viral de éxito! 🚀