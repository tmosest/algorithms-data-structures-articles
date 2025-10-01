-...
Título: LeetCode 535. Código y código TinyURL -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 535. Codificar y Decodificar TinyURL – Código, Conceptos & SEO‐Ready Blog

■ **Target keyword package:** *Decodificar y decodificar TinyURL, TinyURL URL shortener, LeetCode 535, codificación de entrevistas de trabajo, solución Java/Python/C++, codificación URL, entrevista de ingeniería de software. *
■ **Meta‐Title (SEO):** “Encode & Decode TinyURL (LeetCode 535) – Java, Python & C++ Soluciones confidencialidad Entrevista-Ley Blog”

-...

### 1} Resumen del problema (LeetCode 535)

■ ** Objetivo:** Diseño de un pequeño servicio de URL – `encode(longUrl)` devuelve una URL acortada; `decode(shortUrl)` devuelve la URL larga original.
■ **Constraints:**
≤ 104 `
* El mismo objeto " Codec " se utiliza tanto para el código como para el código; ninguna garantía de colisiones.
* Usted puede elegir cualquier esquema de codificación – cadenas base-62, esmalte, contador, etc.

■ **Por qué importa: ** Los acortadores de URL están en todas partes (TinyURL, Bit.ly, GitHub Gists). Los entrevistadores aman este problema porque prueba:
* Uso del diccionario Hashing
* Evitación de azar y colisión
* Cambios en el espacio/tiempo
* Diseño práctico de API

-...

## ## 2down⃣ Common Design Approaches

Silencioso # Silencio Tema Silencio Pros Silencio Cons Silencio Uso Típico‐Caso Silencio
Silencio----------------------------------...
Silencio 1 Silencio **Random 6‐char base‐62 + HashMap** Silencio • Extremadamente simple <br contacto• Constant-time ops <br confianza• Fácil de reiniciar Silencio • Necesidades de comprobación de colisión (rare) = No determinista tención LeetCode " servicios de pequeña escala
Silencio 2 Silencio **Incremental counter + base‐62** Silencio • Sin colisiones, determinísticos • URLs predecibles Silencio • persistencia del Estado requeridas • URLs más largas si muchas entradas vivieron sistemas de producción reales
Silencio 3 Silencio **Hash of longUrl (e.g., MD5) + truncation** Silencio • No se necesita almacenamiento (puro apátridas) <br confianza• Rápido Silencio • Posibles colisiones <br confianza• El hash truncado puede romper Silencio CDN o próxies en caché Silencio
Silencio 4 Silencio **Codificación de átomos (base‐36, base-64 o Huffman)** Silencio • URLs muy cortas • Puede comprimir datos • Complicidad de implementación

■ **Takeaway:** Para la codificación de entrevistas, el enfoque *random 6‐char base‐62* (aproximadamente 1) es el estándar de de-facto. Equilibra la simplicidad, la corrección y el razonamiento claro.

-...

## 3down Soluciones de referencia

■ **Nota:** Todas las soluciones son autocontenidas, usan `HashMap`/`dict`/`unordered_map`, y mantienen el estado en una sola clase.

### 3.1 Java (estilo OOP)

``java
importa java.util. HashMap;
importa java.util. Random;

clase pública Codec {}
pendiente privada ALPHABET = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
privada static final int CODE_LEN = 6;

final privado Random random = nuevo Random();
final privado HashMap madeString, String ratio mapa = nuevo HashMap correctamente();

/** Generar una tecla de 6 caracteres al azar */
privada String generateKey() {}
StringBuilder sb = nuevo StringBuilder (CODE_LEN);
para (int i = 0; i)
sb.append(ALPHABET.charAt(random.nextInt(ALPHABET.length()))));
}
devolver sb.toString();
}

/** codifica una URL a una URL acortada. */
public String code(String longUrl) {
Criterios;
♪
clave = generaKey();
} mientras (map.containsKey(key)); // Evitar las colisiones
map.put(key, longUrl);
devolver "http://tinyurl.com/" + clave;
}

* Decodifica una URL abreviada a su URL original. */
public String decode(String shortUrl) {
Estring key = shortUrl.replace("http://tinyurl.com/", "));
volver mapa.get(key); // Garantizado a existir
}
}
`` `

■ *La complejidad*
■ *Time:* `O(1)` promedio para ambos " código " .
■ *Pace:* `O(N)` donde `N` es el número de URLs codificadas.

-...

#### 3.2 Python

``python
importación al azar
Importación de cadena

class Codec:
_ALPHABET = string. dígitos + string.ascii_letters
_CODE_LEN = 6

def __init__(self):
self._store = {}

def _random_code(self) - título str:
volver ''.join(random.choice(self._ALPHABET) for _ in range(self._CODE_LEN))

def encode(self, long_url: str) - Propiedad str:
Mientras Verdadero:
código = auto._random_code()
si el código no está en sí mismo._store: # Collision check
descanso
self._store[code] = long_url
volver f" http://tinyurl.com/{code}"

def decode(self, short_url: str) - Propiedad str:
code = short_url.replace("http://tinyurl.com/", "")
volver a sí mismo._store[code]
`` `

■ **Tocados pitónicos* *
* `string.digits + string.ascii_letters` da el alfabeto base‐62.
* `self._store` es el diccionario interno.

-...

### 3.3 C++

``cpp
#include ■unordered_map Conf
#include ■string
#Incluye #

Clase Codec {}
static constexpr const char* alphabet = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
static constexpr int codeLen = 6;

std::unordered_map seleccionados::string, std::string mp;
std::mt19937 rng{ std:::random_device{}() };
std::uniform_int_distribución dist{0, 61};

std::string randCode() {}
std::string s(codeLen, '\0');
para (int i = 0; i) {}
s[i] = alfabeto[dist(rng)];
}
retorno s;
}

public:
std::string encode(const std::string curva longUrl) {
std::string key;
♪
clave = randCode();
} mientras (mp.find(key) != mp.end()); // collision check
mp[key] = long Url;
devolver "http://tinyurl.com/" + clave;
}

std::string decode(const std::string cortoUrl) {
std::string key = shortUrl.substr(shortUrl.find_last_of('/') + 1);
retorno mp[key]; // garantizado para existir
}
};
`` `

■ **¿Por qué `mt19937`?**
■ Es un PRNG rápido y de alta calidad adecuado para entrevistas de codificación y servicios reales.

-...

## 4down El bueno, el malo, el ugly

Subtítulos La buena vida la mala vida
Silencio--------------------------------------------...
Silencio **Simplicidad** Silencio Las teclas Random 6-char son *tiny* y fácil de implementar. Necesidad de manejar raras colisiones. ← Sobre-ingeniería (por ejemplo, bloqueo distribuido, endurecimiento) para una simple entrevista. Silencio
Silencio **Determinismo** Silencio Las soluciones apátridas garantizan la reproducibilidad. tención Soluciones aleatorias producen diferentes URLs cada carrera → no ideal para las pruebas de unidad. ← Utilizar el estado RNG estático global puede llevar a pruebas descaradas. Silencio
tención **Scalability** tención HashMap funciona bien para millones de URLs en memoria. ← Memoria crece linealmente; no persistente. Silencio Tratando de almacenar cada par de valor clave en un archivo o DB dentro de la entrevista → overkill. Silencio
tención **Seguridad** tención Las direcciones URL cortas y no comprensibles protegen contra la enumeración. Las cuerdas aleatorias pueden ser forzadas a gran escala. ← Exponer el mapeo (por ejemplo, a través de impresiones de depuración) filtra datos. Silencio
Silencio **Thread‐Safety** Silencio El `HashMap` de Java es *no * seguro de hilo; el dict de Python también no es seguro de rosca. Silencio Ignorar la concurrencia puede causar condiciones de raza. En un servicio diminuto real es necesario bloquear o utilizar `ConcurrentHashMap`. Silencio
TEN **Real‐world concerns** TEN Incremental counter guarantees uniqueness and is easier to audit. Las colisiones aleatorias requieren lógica de regeneración. Silencio Utilizar servicios externos (Redis, S3) para la persistencia añade latencia y complejidad. Silencio

-...

## 5down Optimizaciones " Variantes "

confidencialidad Idea Silencioso Aplicación Silencioso
Silencio...
Silencio **Base‐62 contador** Silencio Convertir un contador entero a la cadena base‐62. ← URLs deterministas, más fácil depuración. Silencio
Silencio ** Collision‐resistant hash** Silencio Uso `hashlib.sha256(longUrl)` → tomar primero 6 bytes. servicio ininterrumpido; almacenamiento mínimo. Silencio
Silencio **Prefix with domain** tención Store domain in a config file, e.g., `http://tinyurl.com`. TEN Flexible for multiple tenants. Silencio
Silencio **Claves de caballo** Silencio Usar teclas de 4 caracteres → 624 ♥ 14 millones de combos únicos. ← Si conoce su cuenta de URL se realizó 14M. Silencio
Silencio **Apátridas** Silencioso Retorno `https://tinyurl.com/` + base62(sha256(longUrl)). Silencio Sin almacenamiento, sin mapa de decodificación (pero perder búsqueda inversa). Silencio

-...

## 6down⃣ Interview Tips

1. **Aclarar los requisitos primero* *
* Pregunte si es necesaria la persistencia.
* ¿Se le permite utilizar bibliotecas externas?
* ¿Y la seguridad de los hilos?

2. **Explicar el cambio de diseño**
* Random vs counter vs hash.
* Estrategia de manejo de colisión.

3. # Código limpio #
* Preocupaciones separadas: generación clave, gestión de mapas.
* Use constantes para dominio, alfabeto, longitud de tecla.

4. ** Casos del borde de los debates**
* URLs muy largas (10 kB).
* Re-encoding la misma URL varias veces.

5. #Mostrar complejidad #
* `O(1)` time, `O(N)` space.
* Potential Memory bottleneck for huge N.

6. **Offer a production extension**
* Persiste el mapa en un DB.
* Use un contador distribuido.
* Agregue el límite de velocidad y análisis.

-...

Pensamientos finales

- La solución *random 6‐char base‐62* es la respuesta del libro de texto para LeetCode 535 – equilibra brevedad, corrección y rendimiento.
- En un servicio real, usted se inclina hacia un enfoque basado en **contra-basado** con almacenamiento persistente (por ejemplo, Redis) para garantizar la singularidad y permitir el análisis.
- Tenga siempre en cuenta el alcance de la entrevista: muestre que entiende los cambios, puede escribir código limpio, y puede discutir posibles extensiones del mundo real.

■ **Pro tip for job hunting** – post these solutions on your GitHub repo, tag them with `tinyurl`, and mention them in your résumé’s “Coding Projects” section. A los clientes les encanta ver la implementación exacta que utilizó para un problema de entrevista clásico.

-...

¿Quieres más práctica?

- **Top Interview Coding Problems** – 30+ preguntas que abarcan estructuras de datos, algoritmos y diseño de sistemas.
- **Repositorio GitHub** – `tinyurl-leetcode-535` con todas las variantes de lenguaje y pruebas unitarias.
- **Live Coding Session** – programar una entrevista de mock de 1 hora en GMeet o Zoom; te guiaré a través de estas soluciones.

■ **Prepárate**: Acabas de dominar una de las preguntas de entrevista *más comunes*. ¡Usa las ideas arriba para llegar a la próxima entrevista tecnológica!

-...

 **SEO Palabras clave**: Diseño TinyURL, solución LeetCode 535, mapeo aleatorio base-62, acortamiento de URL, entrevista de mapas de hash, acortador de URL basado en contador, evitación de colisión, servicio minúsculo del mundo real, patrones de entrevista de codificación.

-...

¡Buena suerte