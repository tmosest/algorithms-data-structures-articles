-...
Título: LeetCode 3609. Movimientos mínimos para alcanzar el objetivo en rejilla -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 3609 – Movimientos Mínimos a Alcance Meta en Grid
*LeetCode – Duro* Silencio **Java Silencio Python Silencio C++** Silencio **

-...

#### TL;DR
*Reverir los movimientos* es la clave.
Partiendo del objetivo `(tx, ty)`, repetidamente ** subtract** la coordenadas más pequeña del mayor.
Cuando la coordenadas más grande es *al menos dos veces* la más pequeña, debe haber sido *doubled* en la dirección delantera – así que **divide por 2**.
Si una división produciría una fracción, el objetivo es imposible.
Cuando finalmente golpeamos el punto de inicio `(sx, sy)` tenemos la respuesta.
Complejidad: **O(log max(tx, ty))** tiempo, **O(1)** espacio.

-...

Declaración de problemas

■ Dados cuatro enteros `sx, sy, tx, ty` (con `0 ≤ sx ≤ tx ≤ 109` y `0 ≤ sy ≤ ty ≤ 109`), usted comienza en `(sx, sy)` en una rejilla infinita.
■ En cualquier punto `(x, y)` vamos `m = max(x, y)`. Usted puede **add `m`** para coordinar:
* `(x + m, y)` o
* `(x, y + m)`
■
■ Encontrar el número **minimo** de movimientos requeridos para alcanzar `(tx, ty)`.
■ Regrese `-1' si es imposible.

Ejemplos
Silencio Silencio Silencio Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio 1 Silencio 2 Silencio 5 Silencio 4 Silencio 2 Silencio `+2` on y → `(1,4)` → `+4` on x → `(5,4)` Silencio
Silencio 0 Silencio 1 Silencio 2 Silencio 3 Silencio 3 Silencio `+1` on x → `(1,1)` → `+1` on x → `(2,1)` → `+2` on y → `(2,3)` Silencio
TENIDO 1 ANTERIOR 1 TENENCIA 2 ANTETENIDO 2 ANTERIED -1 ANTERIED Imposible, ver notas

-...

Intuición

Una primera búsqueda ingenua de pan (la cuadrícula es infinita).
En su lugar, piensa *hacia atrás*.

Si estamos en "(x, y)" y sabemos el último movimiento que lo produjo, podemos deducir cuál era la posición anterior:

Silencio último traslado Silencio anterior Silencioso condición
Silencio--------------------------
Silencio `x += max(prev)` Silencio `x` era la coordinación más grande, por lo que fue **doubled** → `prev = x / 2` Silencio
TENIDO `Y += max(prev)` TENIDO `Y` era la coordinación más grande, por lo que fue **doubled** → `prev = y / 2` ANTE
Silencio `x += max(prev)` Silencio `x` era la coordenadas más pequeña, por lo que fue **added** → `prev = x - y` Silencio
TENIDO `Y += max(prev)` TENIDO `Y` era la coordenadas más pequeña, por lo que fue **added** → `prev = y - x` Silencio

La operación inversa es siempre *determinista* una vez que sabemos cuál es el caso.

**¿Por qué división por 2? #
Si la coordinación más grande es al menos el doble de la más pequeña, la única manera que podría haber aumentado en un solo paso es añadiéndose (doblando).
De lo contrario el aumento vino de la coordenadas más pequeña, así que restamos.

-...

Algoritmo (BFS revisada)

`` `
movimientos = 0
tx ≥ sx y ty ≥ sy:
si tx == sx y ty == sy: movimientos de retorno
si tx .
si tx ≥ 2 * tipo:
si tx es extraño: retorno -1
tx //= 2
más:
tx -= ty
Si no es así,
si el tipo ≥ 2 * tx:
si el tipo es extraño: retorno -1
neumáticos //= 2
más:
Ty -= tx
# tx == Tipo
# no puede reducir más a menos que una de las coordenadas de inicio sea 0
si sx == tx y sy == ty: cambio de retorno
volver -1
movimientos += 1
retorno -1
`` `

*Por qué el `condado=` ¿Comprobaciones? *
Si la coordinación del objetivo se vuelve más pequeña que la correspondiente coordenadas de inicio, nunca podemos alcanzar el objetivo desde el principio porque los movimientos sólo aumentan las coordenadas.

-...

## 4down Edge‐ Lista de verificación de casos

Silencioso Escenario
Silencio...
TENIDO `(sx, sy) == (tx, ty)` TENIDO `0 `
TENIDO `sx == 0 ' ENTRE == 0 ' y objetivo no `(0,0)` Silencio `-1` (no puede crear una coordenadas no cero cuando ambos son cero) Silencio
tención más grande coordine extraño cuando necesitamos dividir por 2
TENIDO `tx == ty` pero no igual a `(sx, sy)` TENIDO `-1` (no puede reducir un par igual a menos que una coordenadas de inicio sea 0)
Silencio Cualquier coordenadas se convierte en: inicio coordinar

-...

## 5VIEWs Implementations

A continuación se presentan implementaciones limpias y listas de producción para **Java**, **Python**, y **C+**.
Todos funcionan en el tiempo `O(log max(tx, ty)' y utilizan sólo espacio extra constante.

### 5.1 Java

``java
Clase Solución {
public int minMoves(int sx, int sy, int tx, int ty) {
si (sx == tx ' sensible == ty) devuelve 0;
si (sx не tx не нывывывый sy нека) regreso -1;

int moves = 0;
mientras (tx >= sx " sensible= sy) {
si (tx == sx " sensible == sy) movimientos de retorno;

si (tx > ty) {
si
(tx) == 1) retorno -1; // extraño
tx √Ī= 1; // divide por 2
. ♫ ... {
tx -= ty; // subtract smaller
}
} si (y > tx) {
si (y >= 2 * tx) {
(y) == 1) retorno -1;
titubeante 1;
. ♫ ... {
-= tx;
}
} más { // tx == ty
retorno -1; // par igual no se puede reducir
}
moves+;
}
retorno -1;
}
}
`` `

### 5.2 Python

``python
Solución de clase:
def minMoves(self, sx: int, sy: int, tx: int, ty: int int:
si sx == tx y sy == ty:
retorno 0
si sx > tx o sy > ty:
retorno -1

movimientos = 0
mientras que tx. Sí.
si tx == sx y ty == sy:
Cambios de retorno

si tx .
si tx.
si tx % 2: # extraño
retorno -1
tx //= 2
más:
tx -= ty
elif ty > tx:
si el tipo >= 2 * tx:
si el tipo es el siguiente:
retorno -1
neumáticos //= 2
más:
Ty -= tx
# tx == Tipo
retorno -1
movimientos += 1
retorno -1
`` `

### 5.3 C++

``cpp
Clase Solución {
public:
int minMoves(int sx, int sy, int tx, int ty) {
si (sx == tx ' sensible == ty) devuelve 0;
si (sx не tx не нывывывый sy нека) regreso -1;

int moves = 0;
mientras (tx >= sx " sensible= sy) {
si (tx == sx " sensible == sy) movimientos de retorno;

si (tx > ty) {
si
si (tx " 1) retorno -1; // odd
tx √Ī= 1; // divide por 2
. ♫ ... {
tx -= ty;
}
} si (y > tx) {
si (y >= 2 * tx) {
si (y " 1) retorno -1;
titubeante 1;
. ♫ ... {
-= tx;
}
} más { // tx == ty
retorno -1;
}
++moves;
}
retorno -1;
}
};
`` `

-...

## 6VIEW⃣ Complexity Analysis

TEN TERRITOR TEN TEN ANTE
Silencio...
Silencio **Tiempo** Silencioso `O(log max(tx, ty))` – cada bucle corta la coordenadas más grande en la mitad o la resta, ambas reducciones logarítmicas
Silencio** – sólo un puñado de variables enteros

Para el peor caso `(0,0) → (109,109)`, el bucle corre a la mayoría ~30 veces.

-...

## 7 carreras Bueno / malo / Ugly

Silencio Categoría Silencio Qué hacer hincapié / Evitar
Silencio------------------
Silencio **Bueno** Silencio • La lógica determinista inversa elimina la necesidad de BFS. <br confianza• Trabaja para 109 límites sin desbordamiento (utiliza los enteros de 64 bits si desea seguridad adicional). Silencio
Silencio **Bad** Silencio • Olvídate de la ` 2 * min` condición puede permitir que el algoritmo elija la operación incorrecta, devolviendo una respuesta incorrecta. • Ignorar el “odd al dividir” cheque produce resultados incorrectos para objetivos como “(3,4)”. Silencio
Silencio **Ugly** Silencio • Implementar un BFS adelante o DFS es una receta para errores de tiempo y memoria. (por ejemplo, `tx / 2.0`) introduce errores de redondeo; quédate con aritmética entero. Silencio

-...

Preguntas frecuentes

Respuesta a la respuesta
Silencio...
*¿Por qué la división siempre es segura cuando ‘más grande ≥ 2 * más pequeña’?* La única manera en que la coordinación más grande podría haber crecido a su valor actual en un paso adelante es añadiéndose (doblando). Si fuera la coordenadas más pequeña, el crecimiento habría sido menos del doble del valor más pequeño. Silencio
*¿Qué pasa si ambas coordenadas son iguales en algún momento?* La única manera de alcanzar un par igual desde el principio es si una de las coordenadas de inicio era cero. De lo contrario no podemos reducir el par más allá, por lo que el camino es imposible. Silencio
Silencio *¿Puedo seguir utilizando BFS en este problema?* Usted puede, pero usted necesita almacenar el conjunto visitado hasta 109 pasos - infeasible. El algoritmo inverso es el enfoque fácil de entrevista. Silencio
*¿Este algoritmo va a funcionar para coordenadas negativas?* El problema garantiza coordenadas no negativas, pero si deseas una solución genérica necesitas manejar los signos cuidadosamente. Silencio

-...

Conclusión

*Reverir el movimiento* transforma un problema infinito en un algoritmo codicioso de tiempo logarítmico.
La idea central —** "divide cuando ves un gran salto; de otro modo resta"**— trabaja en los tres idiomas y es lo suficientemente simple como para explicar en 5 minutos durante una entrevista.

Utilice esta solución como un **código-review graple** o déjela caer en su biblioteca personal de LeetCode.

-...

### 📌 SEO Tags > Palabras clave

- Movimientos mínimos para alcanzar el objetivo en la rejilla
- LeetCode 3609 - Duro
- algoritmo de movimiento de presión
- Solución BFS inversa
- Java, Python, C++ implementaciones
- Preparación de entrevistas, entrevista de codificación, estructuras de datos

-...

Feliz codificación, y que sus futuros entrevistadores sean deslumbrados por su pensamiento reverso ****