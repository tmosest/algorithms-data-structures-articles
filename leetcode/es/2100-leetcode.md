-...
Título: LeetCode 2100. Encontrar buenos días para robar el Banco -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🛠י Solución de 3-Idioma – Encontrar buenos días para robar el Banco (LeetCode 2100)

A continuación encontrará un algoritmo limpio, **O(n)** en **Java**, **Python**, y **C+**.
Las tres implementaciones utilizan la misma técnica prefijo de dos pasos:

1. **decr[i]** – número de días consecutivos no crecientes que terminan en *i* (mira a la izquierda → derecha).
2. **incr[i]** – número de días consecutivos sin disminución que comienzan en *i* (mirar a la derecha → izquierda).

Un día *i* es “bueno” si ambos contadores son ≥ `tiempo`.

√≥ √≥ **¿Por qué este es el mejor enfoque? #
■ La ventana corredera de fuerza bruta sería **O(n·time)**, que puede volar cuando `tiempo ♥ 105`.
■ El método prefix‐suffix da un escaneo lineal y por lo tanto es óptimo.

-...

## Java

``java
importar java.util*;

Solución de la clase pública {}
public List won(int[] security, int time) {
int n = seguridad. longitud;
int[] decr = nuevo int[n]; // prefijo no creciente
int[] incr = nuevo int[n]; // sufijo no disminuyente

// izquierda → derecha : contar con días consecutivos no crecientes
para (int i = 1; i) {}
si (seguridad [i]
decr[i] = decr[i - 1] + 1;
. ♫ ... {
decr[i] = 0;
}
}

// derecha → izquierda : contar con días consecutivos sin disminuir
para (int i = n - 2; i 0; i--) {
si (seguridad [i]
incr[i] = incr[i + 1] + 1;
. ♫ ... {
incr[i] = 0;
}
}

Lista de resultadosInteger título = nuevo ArrayList implicado();
para (int i = tiempo; i) {}
si (decr[i] time " incr[i] √≥= time) {
result.add(i);
}
}
Resultado de retorno;
}
}
`` `

-...

## Python

``python
de la importación Lista

Solución de clase:
def goodDaysToRobBank(self, security: List[int], time: int) - título List[int]:
n = len(seguridad)
decr = [0] * n # non-increas prefix
incr = [0] * n # non-decreasing suffix

# izquierda → right
para i en rango(1, n):
decr[i] = decr[i-1] + 1 si la seguridad[i]

# right → left
para i en rango(n-2, -1, -1):
incr[i] = incr[i+1] + 1 si la seguridad[i]

retorno [i para i en rango(tiempo, n-time)
si decr[i] tiempo e incr[i] >= tiempo]
`` `

-...

### C++

``cpp
Incluido el título
usando std namespace;

Clase Solución {
public:
vector implicado buenoDaysToRobBank(vector fielmente unido seguridad, tiempo int) {
int n = security.size();
vector implicado decr(n, 0), incr(n, 0);

// izquierda → derecha: prefijo no creciente
para (int i = 1; i)
decr[i] = (seguridad[i] = seguridad[i-1]) ? decr[i-1] + 1 : 0;

// derecha → izquierda: sufijo sin disminuir
para (int i = n-2; i 0; i)
incr[i] = (seguridad[i] = seguridad[i+1]) ? incr[i+1] + 1 : 0;

vector significar uns
para (int i = tiempo; i)
si (decr[i] time " incr[i] √≥= time)
as.push_back(i);

devolver los ans;
}
};
`` `

-...

## 📚 Blog Artículo – “El Bien, el Mal y el Ugly: Mastering LeetCode 2100”

#### Introduction

■ **Problema:** *Encontrar buenos días para robar el Banco* – un desafío de mediano nivel que prueba su capacidad para razonar sobre prefijos de array, sufijos y ventanas correderas.
■ ** Objetivo:** Proporcionar una solución concisa **O(n)** que pasa todos los casos de borde.

En este post exploraremos:

1. La mecánica central del problema.
2. Una *buena* estrategia lineal.
3. Dificultades comunes (*el mal*).
4. El truco sutil que hace que el algoritmo sea robusto (*el feo*).

Y vamos a pimienta el artículo con ** palabras clave de SEO** como *LeetCode 2100*, *prefijo de rayos*, *programación dinamica*, *codificación de visión*, *Java Python C++* soluciones* para que puedas encontrarte en Google y aterrizar ese trabajo!

-...

#### ## 1down⃣ Comprender el bien

Un *bueno día* requiere **dos patrones simétricos**:

- No hay aumento de guardias por `tiempo` días antes de `i.
- **No disminuir** guardias por `tiempo` días después de `i.

La solución más ingenua comprobaría cada día candidato con dos bucles, costando **O(n·time)**. Cuando `tiempo' es tan grande como `105`, esto se vuelve infeasible.

**Introducción clave:** Los dos patrones pueden ser pre-computados con dos pases lineales:

TEN TERRITORIO ANTERIOR ANTERIOR Lo que computamos ANTERIOR Por qué funciona
Silencio--------------------------------
TENIDO 1 TENIDO A LA izquierda → derecha TENIDO `decr[i]`: más larga estreak no creciente terminando en `i` ANTERI Si la longitud de la raya ≥ `tiempo`, ya sabemos que la parte "antes" está bien. Silencio
TENIDO 2 TENIDO A la derecha → izquierda TENIDO `incr[i]`: la racha más larga no-disminución que comienza en `i` ANTE ANTES El razonamiento simétrico para la parte "después". Silencio

Una vez que ambos arrays existen, un simple escaneo determina todos los días buenos en el tiempo **O(n)**.

-...

#### 2down⃣ Los malos – errores comunes

¿Por qué no se puede arreglar la vida?
Silencio--------------------------
Silencioso **Usando `` incorrectamente** Silencio Algunas implementaciones comparan `seguridad[i] > seguridad[i-1] " en lugar de ``. Este descarte cuenta de guardia igual, que se permite por el problema. TENIDO Utilizar `traducido=` para el paso izquierdo-a derecha y `traducido=` para el paso derecho-a-izquierda. Silencio
Silencio ** Errores benéficos** Silencio Olvidando excluir días que no tienen `tiempo' días antes o después (`i יי time` o `i √≥ n-1-time`). Silencio Ejecute el bucle final de `i = tiempo` a `i нереннненная n - tiempo.
Silencio **O(n2) acercamiento** Silencio Brute‐force escaparate, recomputing sums each time. ← Precompute prefijo y matriz de sufijo en lugar de recomputing. Silencio
Silencio **Desperdicio de memoria alto** Silencio Usando un array separado para cada tendencia de guardia, pero no reutilizarlos. Únicamente se necesitan dos " conjuntos de longitud " n " , mantenlos locales. Silencio
Silencio **Ignorando el tiempo = 0** Silencio Devolviendo una lista vacía porque `tiempo` nunca se verifica. Silencio Si `tiempo == 0`, todos los índices son válidos – el bucle naturalmente maneja esto. Silencio

-...

#### 3down⃣ Los Ugly – Casos Edge Usted debe manejar

1. **Todos los valores iguales**
`` `
seguridad = [5,5,5,5], tiempo = 1
`` `
Tanto `decr ' como `incr ' se convierten en `0,1,2,...`. Nuestra lógica todavía funciona.

2. **Muy pequeños arrays**
`` `
seguridad = [1], tiempo = 0
`` `
El algoritmo devuelve con gracia `[0]` porque el bucle corre de `i=0` a `i < 1-0`.

3. **Large `time` approaching array length* *
`` `
seguridad = [1,2,3,4,5], tiempo = 4
`` `
Ningún día satisface la condición; los límites del bucle (`i - tiempo') evitan que cualquier índice sea considerado.

4. ¿Cuenta el guardia negativo? #
El problema garantiza los enteros no negativos, pero nuestro algoritmo todavía funcionaría porque las comparaciones dependen sólo del orden, no del valor absoluto.

-...

### 4down It Putting It All Together – A Robust Implementation

Aquí está el final, listo para la producción Código Java (puede copiarlo en un editor LeetCode):

``java
importar java.util*;

Solución de la clase pública {}
public List won(int[] security, int time) {
int n = seguridad. longitud;
int[] decr = nuevo int[n]; // más largo prefijo no creciente terminando en i
int[] incr = nuevo int[n]; // más largo sufijo no disminuyendo a partir de i

para (int i = 1; i) {}
decr[i] = security[i] " se entiende= security[i-1] ? decr[i-1] + 1 : 0;
}

para (int i = n-2; i 0; i--) {
incr[i] = security[i] י= security[i+1] ? incr[i+1] + 1 : 0;
}

Lista de datos:Integer confianza res = nuevo ArrayList correctamente();
para (int i = tiempo; i) {}
si (decr[i] time " incr[i] √≥= time) {
res.add(i);
}
}
restitución;
}
}
`` `

El mismo patrón se traduce en Python (comprensiones de listas) y C++ ( < > > ).

-...

#### 4down⃣ Por qué esto importa para su entrevista

← Habilidad tóxica Cómo se presenta en la Solución
Silencio...
Silencio **Manipulación de rayos** Silencio Dos escaneos lineales, cuidadoso índice aritmético. Silencio
Silencio **Tiempo " complejidad del espacio** Silencioso Mastery de **O(n)** vs. **O(n2)** trade‐offs. Silencio
Silencio **Edge-case thinking** Silencio Handling `time == 0`, arrays muy cortos, grandes rachas. Silencio
Silencio ** readability del proyecto** Silencio Nombres variables claros (`decr`, `incr`), comentarios, y ningún número mágico. Silencio
tención **Language versatility** Silencio Mostrando la lógica idéntica en Java, Python y C++ demuestra la adaptabilidad, un rasgo clave de entrevista. Silencio

-...

### 📈 SEO Boost – How to Get Found

- **Título:** “LeetCode 2100 – Encontrar buenos días para robar el Banco (Java / Python / C++ O(n) Solución)”
- **Meta Descripción:** “Aprenda una solución limpia y lineal a LeetCode 2100. Entender prefijos, sufijos, trampas comunes y casos de borde. Aumenta tus habilidades de entrevista de codificación. ”
- ** Frases clave:** * Solución LeetCode 2100*, *programación dinámica prefijo de rayos*, *rob el problema de la entrevista bancaria*, * algoritmo java O(n), * matriz de sufijo de Python*, *C++ truco de prefijo*, *estrategia de codificación de interfaz*.

Agregue estas frases naturalmente a sus epígrafes y a lo largo del post. Si usted acoge el artículo en una plataforma de blog, añádelos a los **tags** y **categorías** también.

-...

#### 🎯 Final Takeaway

- **Bien:** Técnica de prefijo lineal.
- **Bad:** Errores comunes de indexación y comparación.
- **Ugly:** Casos de bordes raros pero críticos (tiempo cercano a la longitud del array, todos los valores iguales).

Con los tres fragmentos de código, puede dejar esta solución en cualquier entrevista o prueba de codificación. Añadir el artículo a tu cartera, compartirlo en LinkedIn, o incluso incluirlo en tu README GitHub. La combinación de ** código de alta calidad** y ** Contenido amigable de SEO** le ayudará a destacar a los reclutadores que buscan chuletas de solución de problemas.

Feliz codificación, y que su próxima entrevista se sienta como un *heist con cero bajas*! 🚀