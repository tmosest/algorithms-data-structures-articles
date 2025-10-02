-...
Título: LeetCode 2728. Cuenta casas en una calle circular -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2728 – Cuenta casas en una calle circular
**LeetCode TENIDO Tiempo fácil TENIDO O(k) tiempo, espacio O(1)**

■ *“Tu tarea es contar el número de casas en una calle circular, pero solo puedes interactuar con la calle a través de un conjunto de API relacionadas con la puerta.”*

-...

### ¿Por qué este problema importa?
- **Interview staple** – el problema prueba su capacidad de diseñar un algoritmo que funcione con *limited state* y *implicit data structures* (aquí, la calle circular).
- **Estilo de codificación** – debe utilizar la interfaz dada, no un array, lo que le obliga a pensar en * pasos de procedimiento* en lugar de “sólo bucle sobre un array. ”
- **Optimization mindset** – usted está garantizado que el número de casas ≤ k, por lo que la solución debe respetar ese límite.

-...

## 1. Reposición de problemas

TENIDO TARDIS ANTERIOR ANTERIOR
Silencio...
TEN `Street` Silencioso Objeto con la siguiente API: Silencio
TENIDO TERRITORIO • `OpenDoor()` – abre la puerta delante de la casa actual. Silencio
Silencio Silencio • `closeDoor()` – cerrarlo. Silencio
Silencio Silencio • ` isDoorOpen()` – devuelve `verdad' si la puerta actual está abierta. Silencio
Silencio Silencio • `moveRight()` / `moveLeft()` – pasar a la casa adyacente en la dirección respectiva (circular). Silencio
Silencioso `k` Silencio Alto ligado al número de casas. `1 ≤ ≤ k ≤ 103`. Silencio

■ A partir de una casa arbitraria, usted tiene que regresar `n`, el número real de casas.

-...

## 2. Intuición – “Usa las puertas como un marcador”

1. **Clear cada puerta** – caminar `k` pasos (el número máximo posible de casas) y cerrar cualquier puerta abierta que vea.
Después de este bucle, *todas* puertas están cerradas.

2. **Abre la puerta actual** – esta marca la primera casa que hemos visitado.

3. **Sigue caminando en la misma dirección** – después de cada movimiento, si encontramos una puerta abierta, hemos completado un ciclo completo.
El número de movimientos que hicimos (incluyendo la primera casa) equivale al número de casas.

La observación clave: **Las puertas pueden actuar como banderas “visitadas”**. Debido a que sabemos que la calle es circular y estamos garantizados en la mayoría de las casas `k`, cerrando puertas `k` garantiza que hemos reajustado el estado de cada casa posible.

-...

## 3. Pseudocode

`` `
para mí en 0 ... k-1:
street.closeDoor()
street.moveLeft()

street.openDoor() // primera casa
= 1

Mientras Verdadero:
street.moveLeft()
si calle.isDoorOpen():
descanso
Cuenta += 1

cuenta de retorno
`` `

El algoritmo es *O(k)* en el tiempo y *O(1)* en el espacio.

-...

## 4. Código completo

## Java

``java
*
* Definición para una calle.
* class Street {}
* public Street(int[] door);
* vacío público openDoor();
* vacío público closeDoor();
* booleano público esDoorOpen();
* movimiento de vacío públicoRight();
* movimiento de vacío públicoLeft();
*
*/
Solución de la clase pública {}
int house Conde(Street street, int k) {
// Paso 1: restablecer cada puerta
para (int i = 0; i)
street.closeDoor();
street.moveLeft();
}

// Paso 2: abrir la primera casa que encontramos
street.openDoor();
int count = 1;

// Paso 3: caminar hasta que lleguemos a la puerta abierta de nuevo
mientras (verdad) {
street.moveLeft();
si (street.isDoorOpen()) {
ruptura; // un bucle completo se termina
}
contar++;
}

recuento de retorno;
}
}
`` `

## Python

``python
Definición para una calle.
# class Street:
# def __init__(self, doors: List[int]): ...
# def openDoor(self) - título Ninguno: ...
# def closeDoor(self) - título Ninguno: ...
# def isDoorOpen(self) - título bool: ...
# def moveRight(self) - título Ninguno: ...
# def moveLeft(self) - Propiedad Ninguno: ...

Solución de clase:
def house Conde(self, street: 'Street', k: int) - int:
# Paso 1: cierra cada puerta posible
para _ en rango(k):
street.closeDoor()
street.moveLeft()

# Paso 2: abre la primera casa
street.openDoor()
= 1

# Paso 3: caminar hasta que lleguemos a la puerta abierta de nuevo
Mientras Verdadero:
street.moveLeft()
si calle.isDoorOpen():
descanso
Cuenta += 1

cuenta de retorno
`` `

### C++

``cpp
*
* Definición para una calle.
* class Street {}
* public:
* Street(vector realizadasint propietarios puertas);
* vacío openDoor();
* vacío closeDoor();
* bool isDoorOpen();
* movimiento por vacíoRight();
* movimiento vacíoLeft();
* };
*/
Clase Solución {
public:
int house Conde(Street* street, int k) {
// Paso 1: restablecer todas las puertas
para (int i = 0; i) {}
street- tituladacloseDoor();
street- tituladamoveLeft();
}

// Paso 2: marca la primera casa
street- iconopenDoor();
int count = 1;

// Paso 3: caminar hasta encontrar la puerta abierta de nuevo
mientras (verdad) {
street- tituladamoveLeft();
si (street- confíaisDoorOpen())
ruptura;
++cuenta;
}

recuento de retorno;
}
};
`` `

-...

## 5. Análisis de la complejidad

TENCIÓN TERRITOR TENIDA Cálculo
Silencio----------
Silencio **Hora** Silencioso `2k` operaciones en la mayoría (cerrar + fase de apertura). ################################################################################################################################################################################################################################################################
tención **Espacio** Silencioso Sólo un puñado de variables enteros. → **O(1)**

Con k ≤ 103, la solución funciona cómodamente en 1 ms de hardware moderno.

-...

## 6. Lista de verificación Edge‐Case

Silencio Caso confidencialidad ¿Por qué es seguro ← Cómo se comporta el algoritmo
Silencio----------------------------------
Silencio Todas las puertas inicialmente cerradas Silencio Ninguna puerta se deja abierta después del primer lazo. Silencio Primera `openDoor()` todavía marca la primera casa. Silencio
Silencio Todas las puertas se abren inicialmente.Primero bucle cierra cada una. Lo mismo que antes. Silencio
Silencio `n = k` (maximum) Silencio Caminamos exactamente `k` pasos; no hay movimientos adicionales. El conde será `k`. Silencio
TENIDO `n ANTERIENTE TENIDO Alguna posición que nunca visitamos durante el primer lazo. Las puertas de Closing aún cubren toda casa real. Silencio
Silencio La puerta de inicio está abierta Silencio Está cerrada en el primer lazo, y luego se abre de nuevo más tarde. Silencio Contado correctamente. Silencio

-...

## 7. Bueno, malo de una perspectiva de entrevista

Lo que es bueno para la vida Lo que es malo Qué es Ugly
Silencio--------------------------------------------------------------
• Espacio constante; no hay estructura de datos extra. • Usa sólo la API proporcionada. • Trabaja para *cualquier* casa de inicio. TEN ANTE TENIDO
La suposición “moveLeft” puede parecer arbitraria, pero la dirección puede ser “derecha” o “izquierda” siempre y cuando usted siga siendo consistente. Si mezclas direcciones en la primera o segunda fase, nunca volverás a golpear la puerta abierta.
Silencio **Ugly** Silencio • Una solución ingenua que itera sobre un array sería *O(n)* pero no satisfaría la restricción “API‐únicamente”. • Olvídate de abrir la primera puerta antes de comenzar el bucle volverá 0 en lugar de `n`.

**Tip de Interview:**
■ Siempre **explica tu elección de dirección** (izquierda vs. derecha) y por qué lo mantienes consistente. Te muestra entender la naturaleza circular del problema.

-...

## 8. Entrevista Take-aways

Previamente Testado de Habilidad Silencio Por qué Es Valioso
Silencio...
Silencio * Iteración completa* Silencio Sólo se puede leer/escribir a través de efectos secundarios. Silencio
Silencio *Extremidad abundada* Silencio Usted utiliza `k` a trabajo atado en lugar de iterar ciegamente sobre una matriz desconocida. Silencio
Silencio *Problema de-composición* Silencio Limpiar todas las puertas primero, luego utilizarlas como marcadores es un patrón clásico. Silencio
tención *Coding contra una interfaz* ← Un escenario común del mundo real: tienes una biblioteca o una API de caja negra y debes construir lógica alrededor de ella. Silencio

Si te estás preparando para las entrevistas de codificación, este problema es un **must‐solve**. Combina el pensamiento algoritmo con restricciones prácticas.

-...

## 9. SEO‐Friendly Summary

- **Keywords**: `Casas en una calle circular ' , `LeetCode 2728 solution ' , `Java Python C++`, `circular street problem`, `interview algoritmo`, `time complejidad O(k)`, `space complexity O(1)`
- **Título**: “LeetCode 2728 – Conde Houses in a Circular Street (Java / Python / C++ Solution)”
- **Meta Descripción**: “Solve LeetCode 2728 – Count Houses in a Circular Street – con Java limpio, Python y C++. Aprenda el algoritmo O(k), explicación detallada y consejos de entrevista. ”

-...

## Palabras finales

El truco de “door‐as-marker” es un truco limpio y de entrevista que mantiene el estado mínimo mientras todavía permite un traversal completo. Aplicarlo en **Java, Python, o C++** es directo una vez que comprenda la API y la naturaleza circular de la calle.

¡Feliz codificación y buena suerte en tu próxima entrevista!