-...
Título: LeetCode 3279. Zona Total máxima Ocupado por Pistons -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Solving ** "Maximum Total Area Ocupado por Pistons** (LeetCode 3279)

A continuación encontrará:

Silencio Idioma Silencio Código Silencioso
Silencio----------------
Silencio **Java** Silencioso Haga clic para ampliar el texto correspondiente
importar java.util*;

Solución de la clase pública {}
public long maxArea(int height, int[] positions, String directions) {}
int n = posiciones. longitud;
long[] diff = nuevo largo[2 * altura + 2]; // diferencia array (index 0 unused)
long currentSum = 0; // sum of positions at time 0
para (int i = 0; i) Sum += posiciones[i];

para (int i = 0; i) {}
int pos = positions[i];
char d = directions.charAt(i);
si (d == 'U') { //
diff[1] += 1;
diff[altura - pos + 1] += -2;
diff[2 * altura - pos + 1] += 2;
♪ otra vez { / / / bajando primero
diff[1] += -1;
diff[pos + 1] += 2;
diff[pos + 1 + altura] += -2;
}
}

long best = current Sum;
pendiente larga = 0; // derivado de la superficie total wrt tiempo
para (int t = 1; t = = 2 * altura; ++t) {
pendiente += diff[t];
corriente Sum += pendiente; // área después de t segundos
si (currentSum > best) mejor = actual Sum;
}
devolver mejor;
}
}
`` `` obedeció/detalles confianza TENIDO ** Tiempo** ``O(n + altura''] `según indica el párrafo 1 de la parte dispositiva de la parte dispositiva. Silencio
Silencio **Python** Нелилилинилинаниениханиханиханиханниханиханихананиханиенинаниеннтентениханиянанияниенниенанананиянниянинниянияния нанниениянтиенанниенних ннниханиенниеннннниенаниеннниенаниениеннниениениениениенниеннннннниениенниениениенаннннннниенниенниеннннниени
importadores
de la importación Lista

def max_area(height: int, positions: List[int], directions: str) int:
n = len(posiciones)
diff = [0] * (2 * altura + 2) # 1-based index
cur = suma(posiciones)

para pos, d en zip(posiciones, direcciones):
si d == 'U':
diff[1] += 1
diff[altura - pos + 1] += -2
diff[2 * altura - pos + 1] += 2
# 'D'
diff[1] += -1
diff[pos + 1] += 2
diff[pos + 1 + altura] += -2

mejor = curro
pendiente = 0
para t en rango(1, 2 * altura + 1):
pendiente += diff[t]
curva += pendiente
si cur > mejor:
mejor = curro
mejor

El uso de muestras...
si __name_ == "__main__":
h = 5
pos = [2, 5]
dirs = "UD"
print(max_area(h, pos, dirs)) # → 7
```` `` `` ` `` ` ` `` observado/detalles confianza ANTE ** Tiempo** ``O(n + altura) `` obedecido**Espacio** Silencio
tención **C+** Silencioso Haga clic para ampliarlo
#include יbits/stdc++.h
usando std namespace;

largo tiempo maxArea(int height, const vector implicado posiciones, const cordón curvas) {}
int n = positions.size();
vector alcanzado largo tiempo dadoff(2 * altura + 2, 0); // 1-basado índice
Cura larga larga = 0;
para (int p : posiciones) cur += p;

para (int i = 0; i) {}
int pos = positions[i];
char d = directions[i];
si (d == 'U') { //
diff[1] += 1;
diff[altura - pos + 1] += -2;
diff[2 * altura - pos + 1] += 2;
♪ otra vez { / / / bajando primero
diff[1] += -1;
diff[pos + 1] += 2;
diff[pos + 1 + altura] += -2;
}
}

long long best = cur;
pendiente larga larga = 0;
para (int t = 1; t = = 2 * altura; ++t) {
pendiente += diff[t];
cur += pendiente;
mejor = max(best, cur);
}
devolver mejor;
}

// Uso del ejemplo
int main() {}
int h = 5;
vector asignadoint edad pos = {2, 5};
Dirs de cuerda = "UD";
cout se realizó maxArea(h, pos, dirs)
}
`` `` obedeció/detalles confianza TENIDO ** Tiempo** ``O(n + altura''] `según indica el párrafo 1 de la parte dispositiva de la parte dispositiva. Silencio

■ **Tip** – Las tres soluciones comparten la misma lógica:
■ 1. Transformar el movimiento de cada pistón en un array de *diferencia* de cambios de pendiente.
■ 2. Acumular pistas para obtener el área después de cada segundo.
■ 3. Seguimiento del máximo.

-...

## 🎯 Why This Problem is a Gold‐Mine for Interviews

- **Simulación + Optimización**: Muestra que puede convertir una simulación ingenua O(n · t) en O(n + h) por matemáticas inteligentes.
- **Prefix‐Sum / Difference Array**: Un clásico truco de entrevista. Enséñalo, y puedes romper muchos problemas.
- ** Análisis de la complejidad del tiempo**: Maneja `altura' hasta 106 y `n` hasta 105 - tendrá que pensar en memoria y pases lineales.
- **Edge‐Case Awareness**: Pistons at `0` or `height ' , pistón único, todo en movimiento en la misma dirección.

-...

## The Good, The Bad, and The Ugly

Silencio Silencio
Silencio------------Prince------
Silencio **Concept** Silencio física directa a la transformación de la madre podría confundir a los candidatos que no están familiarizados con los arrays de diferencia ← Mistake “área máxima en *cualquier* tiempo” para “área máxima *después* todos los pistones paran”
Silencio **Implementación** Silencio One‐pass O(n + h) algoritmo TEN Requiere enteros de 64 bits para evitar el desbordamiento TEN Off‐por‐uno en índices de array puede conducir a errores sutiles TEN
Silencio **Performance** Silencio Funciona rápido para 106 altura Silencio Todavía O(h), que puede ser grande en máquinas lentas Silencio Intentar simulación de fuerza bruta sería TLE ←

**Pro Tip**: Durante una entrevista, articular su plan *antes* código de escritura: "Usamos un array de diferencia porque la contribución de cada pistón cambia sólo dos veces por período".

-...

Paso a paso (Java Edition)

1. **Base Sum** – `cur = latitud de la Asamblea [i]` (área a la hora 0).
2. ** Diferencia Array** – `diff[1]` mantiene el cambio en * pendiente* (la tasa de cambio de área por segundo) en cada momento.
3. **Para cada pistón**:
- Si se mueve (`U`):
`` `
diff[1] += 1; // comienza a aumentar
diff[altura - pos + 1] += -2; // hit superior bound → empezar a disminuir
diff[2 * altura - pos + 1] += 2; // hit lower bound → empezar a aumentar de nuevo
`` `
- Si se mueve (D`):
`` `
diff[1] += -1; // comienza a disminuir
diff[pos + 1] += 2; // hit lower bound → start increasing
diff[pos + 1 + altura] += -2; // hit superior bound → empezar a disminuir
`` `
4. **Sweep** sobre `t = 1 ... 2*height`:
- `slope += diff[t]` – actualiza lo rápido que el área cambia en este segundo.
- `curre += pendiente' - área después de este segundo.
- Mantener `best = max(best, cur)`.
5. **Retorno** Mejor.

■ El tamaño de la matriz `2* altura+2` es suficiente porque un pistón puede cambiar la dirección dos veces en un período completo (hasta → abajo → arriba).

-...

## 📊 Complexity Analysis

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
← Construir diff Silencioso `O(n)` Silencio
TENIDO ANTERIOR TENIDO O (a la altura)
Silencio **Total** Silencioso** Silencio

Con `altura ≤ 106`, el diff array es de unos 16 MB (utilizando `long'), que encaja cómodamente en la memoria.

-...

## 📚 Blog Article – “Maximum Total Area Ocupado por Pistons”
**(SEO-optimized, interview-ready, good-bad‐ugly guide)* *

■ **Keywords**: LeetCode 3279, simulación de pistón, array de diferencia, entrevista de algoritmo, O(n + h), Java Python C++ soluciones, estrategia de entrevistas

-...

### 1. Introducción

Probablemente has visto problemas de simulación antes: “Dado un conjunto de objetos que se mueven en una línea, computa algo con el tiempo. ”
LeetCode 3279, **Maximum Total Area Ocupado por Pistons**, lleva esto al siguiente nivel: cada pistón rebota de ida y vuelta entre las paredes de un cilindro, y necesita encontrar el área total máxima bajo todos los pistones en cualquier momento.

■ **¿Por qué es una gran pregunta de entrevista? #
* Prueba habilidades de simulación, pero te obliga a pensar en **periodicidad** y **estructuras de datos eficientes**.
* La solución óptima es sorprendentemente simple una vez que reconoces las matemáticas subyacentes.

-...

### 2. Recaptación de problemas

- ** Entrada*
- `Altura' - límite superior de la moción de los pistones.
- `posposiciones[i]` - altura actual del pistón `i` (también la zona debajo de ella).
- `directions[i]` – 'U' (upwards) o 'D' (downwards).

*El objetivo* – Devolver el máximo*
\[
\text{total area}(t) = \sum_{i=0}^{n-1} \text{height of pistón }i\text{ after }t\text{ seconds}
\]
para *cualquier* entero `t ≥ 0`.
Los pistones nunca paran; siguen reflexionando para siempre.

- Constraints**
- 1 ≤ 105
- `1 ≤ altura ≤ 106`
- `0 ≤ posiciones[i] ≤ altura

-...

### 3. Naïve Approach ( Why It Fails)

Usted podría simular segundo por segundo, actualizar la posición de cada pistón y comprobar la suma.
Pero:

- Cada pistón necesita pasos `O(altura)` para un ciclo completo.
- Con 105 pistones y una altura de 106, es decir, 1011 operaciones** – mucho más allá de los plazos.

-...

### 3. Insight clave – Periodicidad + Cambios de pendiente

La altura de cada pistón con el tiempo es una onda triangular*:

- Si comienza a " p " y se mueve hacia arriba, la zona aumenta a velocidad " +1 " por segundo hasta que alcanza la parte superior ( " altura " ).
- En la parte superior se invierte inmediatamente la dirección → la pendiente cambia a `-1`.
- Después de otro `altura - p` segundos que golpea el fondo, la pendiente vuelve a girar hacia '+1'.
- El patrón repite cada 2* altura.

** Observación**:
El *slope* de un pistón (valor de cambio de área) sólo cambia en ** tres momentos distintos** en un período completo.
Podemos codificar todos estos cambios en un array **difference** – una técnica clásica para actualizaciones de rango y consultas de puntos en el tiempo O(1) cada uno.

-...

### 4. Difference Array Construction

TENCIÓN TERRITORIO FORMACIONES (índices basados en el principio) TENCIÓN
Silencio----------------------------------
Silencio `U` Silencio `diff[1] += 1 " 0 " - p + 1] += -2 " - " , - p + 1] += 2` Silencio Inicio arriba, golpe arriba, golpe abajo
Silencio `D` Silencio `diff[1] += -1` Identificar `diff[p + 1] += 2` <br título `diff[p + 1 + altura] += -2` Silencio Comienza abajo, abajo abajo, arriba

El **primera entrada `diff[1]`** establece el cambio de pendiente inicial para todos los pistones simultáneamente.
Añadiendo o restando `2` en los índices posteriores refleja la inversión instantánea del movimiento.

■ **¿Por qué 2 × altura? * *
■ Un pistón puede cambiar la dirección al máximo dos veces por ciclo (up → down → up).
■ Así que necesitamos un array lo suficientemente largo como para capturar ambos eventos, por lo tanto `2*altura + 2`.

-...

### 5. Sweeping Through Time

Una vez que se construye la matriz de diferencia:

1. `cur = latitud de la Asamblea [i] ' – área a la hora 0.
2. `slope = 0`
3. Por cada segundo `t = 1 ... 2*height`:
- `slope += diff[t]` (actualiza cómo el área rápida cambia en este instante).
- `curre += pendiente` (nuevo área total después de `t` segundos).
- `best = max(best, cur)`.

Debido a que la pendiente es una función *a la vez constante*, nunca tenemos que simular los pistones mismos – solo actualizamos las cantidades agregadas.

-...

### 6. Aplicación en una línea (Java, Python, C++)

Los fragmentos de código de arriba ilustran cómo compacto puede ser la solución final una vez que se entienda la matemática.
Todos los idiomas siguen el mismo patrón:
- **Construir un diff array en O(n)* *
- **Sweep in O(height)* *

-...

### 7. Estrategia de entrevistas

1. **Clarificar la cuestión**: “Se nos pide el área total máxima * en cualquier momento*, no después de que todos los pistones se detengan. ”
2. **Sketch the approach**:
- *Explicar* que la moción de cada pistón es periódica con el período `2*Altura`.
- *Mención* que un pistón sólo cambia su tasa de cambio de área dos veces por período.
- *Introduce* un array de diferencia para captar cambios de pendiente.
3. **Write clean code** – mantener índices 1-basados para evitar confusión.
4. **Los mejores casos de borde** en papel:
- Pistons ya a 0 o altura.
- Un pistón en movimiento en una dirección.
- Todos los pistones se mueven juntos.
5. **Explicar complejidad** – mostrar que la solución escala con 'altura' y 'n'.

■ **Por qué esto importa*: Demostrando un plan claro y explicando el dominio de las señales lógicas a los entrevistadores, incluso si no estás 100% seguro en el código.

-...

### 8. Pitfalls comunes (y cómo evitarlos)

Silencio Pitfall Silencio
Silencio...
Silencio **Desbordamiento entero** – la suma puede exceder de 32 bits  durable Use `long`/`int64_t`. Silencio
Silencio **Off‐by-one indices** tención Stick to 1-based indices in the diff array. Silencio
Silencio **Misinterpreting “maximum”** Silencio Clarify usted está tomando el máximo sobre todo el tiempo `t ≥ 0`. Silencio
Silencio **No considerando el período completo** Silencio Sumérjase hasta `2*Altura` para capturar todos los cambios de dirección. Silencio

-...

### 9. Takeaway

LeetCode 3279 es un ejemplo brillante de cómo *math* y *data‐structures* pueden convertir una pesadilla de simulación en una solución slick O(n + h).
Ya sea que estés en codificación en Java, Python o C++, la idea central sigue siendo la misma: transformar el movimiento en cambios de pendiente y barrer una vez.

■ **Recuerda** – Cuando los entrevistadores presentan un problema de “simulación” con grandes limitaciones, piensa: * ¿Hay una periodicidad oculta? ¿Puedo usar sumas prefijas o arrays de diferencia?* Esa es generalmente la clave para romperla.

-...

#### 10. Call to Action

- **Práctica** – Probar variaciones: pistones en un círculo, diferentes condiciones de límites, o “máximo después de k segundos”.
- **Compartir** – Deja tu propio código en GitHub o en un blog; otros pueden aprender de tu estilo.
- **Entrevista** – Traiga este problema a su próxima entrevista de codificación – es un ganador para usted y el entrevistador.

-...

### 11. Pensamiento de clausura

En el mundo de las entrevistas de codificación, ** los problemas de simulación no son el cuello de botella** – a menudo son la * puerta* para el pensamiento algoritmo más profundo.
LeetCode 3279 muestra que una estructura de datos bien escogida (el array de diferencia) puede ahorrarle **millones de operaciones** e impresionar a cualquier gestor de contratación.

■ ¡Buena suerte en tu próxima entrevista! * *
■ Utilice las soluciones anteriores, explique su proceso de pensamiento claramente, y usted saldrá de esa habitación sintiéndose como un verdadero algoritmoista.

-...

Feliz codificación, y que su pila de entrevistas siempre contenga la *diferencia* correcta! 🚀

-...

■ *Este artículo está adaptado para desarrolladores de entrevista y gerentes de contratación de tecnología. No dude en adaptar el código y explicaciones a su estilo de enseñanza o contratación. *