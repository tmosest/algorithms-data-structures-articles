-...
Título: LeetCode 391. Rectángulo perfecto -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🏆 391. Rectángulo perfecto – Duro LeetCode
* Objetivo*
Dada una lista de rectángulos axis-alignados, determinar si se forman juntos **exactamente uno** gran rectángulo (sin huecos, sin solapas).

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio en Java**
TENIDO Python TENIDO **O(n)** ANTERIOR **O(n)**
TENIDO C++ TENIDO **O(n)** Silencio **O(n)**

-...

Artículo del Blog – “El Bien, el Mal, y el Ugly of Perfect Rectangle”

■ **Keywords: ** Perfect Rectangle LeetCode, algoritmo, Solución Java, solución Python, solución C++, pregunta de entrevista, set de hash, control de área, entrevista de trabajo.

#### 1down⃣ ¿Cuál es el problema del rectángulo perfecto?

Imagina que tienes un conjunto de rectángulos más pequeños colocados en un plano 2-D.
Se le pregunta: **¿Cubrin un solo rectángulo más grande sin agujeros ni solapas? * *

Típica pregunta de entrevista que prueba:
- **Introspección geométrica**
- **Hashing / Establecer el uso**
* Computación de la zona*

### 2 comentarios La Solución Clásica O(n)

El truco es combinar dos simples observaciones:

TENCIÓN ANTERIOR Por qué importa
Silencio...
La suma de todas las áreas de rectángulos pequeños debe igualar el área del rectángulo exterior. Silencio
Silencio **Comprobación de clientes** En una cubierta perfecta cada esquina interna aparece *un número de veces*; sólo los 4 esquinas exteriores aparecen *exactamente una vez*. Silencio

#### Pasos

1. **Track the outer bounds**
`minX`, `minY`, `maxX`, `maxY` - el rectángulo más pequeño que podría contener a todos los demás.

2. **Sum areas**
`totalArea = gia (ai - xi) * (bi - yi) `

3. **Mantenga un conjunto de esquinas**
Para cada rectángulo empuja sus 4 esquinas en un `HashSet`.
Si ya existe una esquina, retírela – esto mantiene efectivamente sólo las esquinas *odd‐frequency*.

4. **Después de procesar todos los rectángulos**
* El conjunto debe contener **exactamente cuatro esquinas**.
* Esas cuatro esquinas deben ser `(minX, minY)`, `(minX, maxY)`, `(maxX, minY)`, `(maxX, maxY)`.
* The `totalArea` must equal `(maxX - minX) * (maxY - minY)`.

Si las tres condiciones están satisfechas → **verdad**; más **falso**.

■ ¿Por qué funciona esto? #
■ Cualquier rincón interno (compartido por 2 o 4 rectángulos) se añade y elimina un número uniforme de veces → desaparece del conjunto. Sólo las esquinas del rectángulo exterior sobreviven.

#### 3down⃣ El Bien

TENIDO VALORAR LA FACTURA ANTE LAS Explicaciones
Silencio...
Silencio **Tiempo de iluminación** Silencio Cada rectángulo se procesa una vez. Silencio
Silencio **Low la memoria** Silencio Sólo un conjunto de en la mayoría de 4 esquinas al final; más unos pocos enteros. Silencio
Silencio **Determinista** Silencio No aleatoriedad o recursión – gran para la claridad de la entrevista. Silencio
Silencio **Extensible** Silencio Trabaja para cualquier rectángulos alineados por el eje. Silencio

#### 4down⃣ El malo

¿Por qué es un dolor
Silencio...
Silencio **Coordinaciones altas** tención Necesita `long`/`int64` para evitar el desbordamiento cuando la zona de computación. Silencio
Silencio **HashSet overhead** Silencio En apretadas restricciones de entrevista, es posible que necesites un hash de par personalizado. Silencio
Silencio **Asumes la entrada adecuada** Silencio No protege contra rectángulos degenerados (`xi==ai` o `yi==bi`). Silencio

#### 5down⃣ El Ugly

Silencio | Casos de borde Silencio Cómo manejar
Silencio------------------------------
Silencio **Multiple tapas desconectadas** Silencio El set de esquina tendría ≤4 esquinas – atrapadas por el cheque establecido. Silencio
Silencio **Tiny rectángulo solapa** tención La solapa causa curvas duplicadas → set size wrong. Silencio
Silencio **Coordinaciones negativas** Silencio Todavía funciona; simplemente mantenga la lógica min/max. Silencio

-...

## 🎯 Why You should Master This Problem

- Interview Gold‐mine Es una pregunta clásica “geometry + hash” en LeetCode y muchos apilamientos de entrevista de la empresa.
- **Muestre de Pensamiento** – Demuestra que puede reducir un problema de cubierta 2-D a las operaciones de álgebra.
- ** Estilo de código** – Limpio, autocontenido y fácilmente explicado en 5-10 minutos.

-...

## 📦 Code Solutions

A continuación se presentan implementaciones limpias y totalmente agregadas en **Java, Python, y C++**. Cada uno sigue el algoritmo exacto descrito.

-...

#### ## 1down⃣ Java

``java
importa java.util. HashSet;
importa java.util. Set;

*
* LeetCode 391 - Rectángulo Perfecto
* Tiempo: O(n)
* Espacio: O(n) – conjunto de esquinas
*/
Solución de la clase pública {}
// Clase de ayuda para representar un punto (x, y)
clase privada Punto {}
int x, y;
Punto(int x, int y) { this.x = x; this.y = y; }

@Override
booleano público igual(Objeto o) {
si (esto == o) regresan verdaderos;
si (! (o instancia de punto)) devolver falso;
Point p = (Point) o;
devolver x == p.x " sensible y == p.y;
}

@Override
public int hashCode() {
retorno 31 * x + y;
}
}

booleano público esRectangleCover(int[][] rectángulos) {}
// Coordenadas de rectángulo brillante
int minX = Integer.MAX_VALUE, minY = Integer.MAX_VALUE;
int maxX = Integer.MIN_VALUE, maxY = Integer.MIN_VALUE;

largo totalArea = 0; // Uso largo para evitar el desbordamiento
Establecer:Punto de contacto esquinaSet = nuevo HashSet identificado();

para (int[] rect : rectángulos) {}
int x1 = rect[0], y1 = rect[1];
int x2 = rect[2], y2 = rect[3];

// Actualización de límites
minX = Math.min(minX, x1);
minY = Math.min(minY, y1);
maxX = Math.max(maxX, x2);
maxy = Math.max(maxY, y2);

// Zona acumulada
totalArea += (long)(x2 - x1) * (y2 - y1);

// Proceso cuatro esquinas
Punto[] esquinas = {
nuevo Point(x1, y1),
nuevo punto(x1, y2),
nuevo Point(x2, y1),
nuevo Punto(x2, y2)
};

para (Punto p : esquinas) {}
si (!cornerSet.add(p)) { // ya presente - Retirar
cornerSet.remove(p);
}
}
}

// Después de procesar todos los rectángulos
si (cornerSet.size() != 4) devolver falso;

// Estas cuatro esquinas deben coincidir con las esquinas del rectángulo atado
si (!cornerSet.contains(new Point(minX, minY)))) retornan falsos;
si (!cornerSet.contains(new Point(minX, maxY)))) retornan falsos;
si (!cornerSet.contains(new Point(maxX, minY)))) retornan falsos;
si (!cornerSet.contains(new Point(maxX, maxY)))) devuelve falso;

// Verificación de área
long expectedArea = (long)(maxX - minX) * (maxY - minY);
total Zona == esperada;
}
}
`` `

-...

#### 2down⃣ Python

``python
de la lista de importación de escritura, Tuple, Set

Solución de clase:
Def isRectangle Cover(self, rectángulos: List[List[int]]) - conveniente bool:
# Bounding box
min_x, min_y = flotador('inf'), flotante('inf')
max_x, max_y = flotador('-inf'), flotante('-inf')

área = 0
esquinas: Set[Tuple[int, int] = set()

para x1, y1, x2, y2 en rectángulos:
min_x, min_y = min(min_x, x1), min(min_y, y1)
max_x, max_y = max(max_x, x2), max(max_y, y2)
área += (x2 - x1) * (y2 - y1)

# Cuatro esquinas del rectángulo
para esquina en (x1, y1), (x1, y2), (x2, y1), (x2, y2)):
si esquina en esquinas:
esquinas.remove(corner)
más:
esquinas.add(corner)

Después de todos los rectángulos procesados
si len(corners) != 4:
Retorno Falso

esperado_corners = {(min_x, min_y), (min_x, max_y),
(max_x, min_y), (max_x, max_y)}

si esquinas != espera_corners:
Retorno Falso

área de retorno == (max_x - min_x) * (max_y - min_y)
`` `

-...

#### 3down⃣ C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
bool isRectangleCover(vector seleccionadovector seleccionado) {}
área larga = 0;
long long minX = LLONG_MAX, minY = LLONG_MAX;
maxX largo largo = LLONG_MIN, maxY = LLONG_MIN;

// Conjunto de puntos de esquina representados como par =
unordered_set obtenidos largo largos esquinas de confianza; // utilizar truco de la piratería

codificador automático = [](int x, int y) - título largo
// Embalaje de 32 bits (trabajos para coordenadas dentro +/-1e5)
retorno ((largo)(x + 100000)
};

para (autor : rectángulos) {}
int x1 = r[0], y1 = r[1];
int x2 = r[2], y2 = r[3];

minX = min(minX, (long long)x1);
minY = min(minY, (long long)y1);
maxX = max(maxX, (long long)x2);
maxy = max(maxY, (long long)y2);

área += (long long)(x2 - x1) * (y2 - y1);

vector asignadopair obtenidosint,intenta confiar pts = {{x1,y1},{x1,y2},{x2,y1},{x2,y2};
para (auto &p : pts) {}
llave larga larga = código(p.first, p.second);
si (!corners.insert(key).second) { // ya presente - título Retirar
corners.erase(key);
}
}
}

si (corners.size() != 4) devolver falso;

vector de garantía realizable largo, largo tiempo espera =
{minX, minY}, {minX, maxy},
{maxX, minY}, {maxX, maxY}
};
para (auto &e : esperado) {
si (!corners.count(encode(int)e.first, (int)e.second)))) devolver falso;
}

largo tiempo esperadoArea = (maxX - minX) * (maxY - minY);
área de retorno == espera Zona;
}
};
`` `

■ **Nota en el truco de codificación C++** –
■ Usando un entero de 64 bits para empacar dos coordenadas de 32 bits evita la necesidad de una estructura de hash personalizado.
■ Para las limitaciones del problema ( " perpetuacoordinate duradera ≤ 1e5 " ) el cambio de 32 bits es seguro.

-...

Pensamientos finales

- **Tiempo & Espacio** – Linear y baja cabeza; perfecto para una entrevista de codificación.
- **Key Insight** – Reducir el problema de la cubierta 2-D a la paridad de bellotas* + *igualdad de la zona*.
¿Qué hay que destacar en una entrevista?
- ¿Por qué la esquina termina con exactamente cuatro esquinas?
- ¿Por qué el control de área atrapa escenarios “gap” y “overlap”.
- Manejo de caso de borde (coordenadas negativas, gran entrada).

> Dominar esta pregunta le da un sólido pie en problemas de corte geométrico, un tema de entrevista común en las empresas de tecnología superior.

¡Feliz codificación, y que su cubierta sea perfecta! 