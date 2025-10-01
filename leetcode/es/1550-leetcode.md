-...
Título: LeetCode 1550. Tres probabilidades consecutivas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Tres probabilidades consecutivas - LeetCode 1550
**Java • Python • C+** **Proyecto de reflexión (O(n), O(1))**

-...

## TL;DR

■ *“Given an integer array, return `true` if there exist three successive odd numbers; otherwise return `false`.”*

La solución más simple y eficiente es un solo escaneo lineal que mantiene un contador de números impares consecutivos.
Complejidad del tiempo: **O(n)* *
Complicidad espacial: **O(1)**

A continuación encontrará un código limpio y listo para la producción en **Java, Python, y C++**, seguido de un breve artículo del blog que explica el problema, el enfoque, y los pros/cons de varios métodos.

-...

# Código #

#### ## 1down⃣ Java

``java
Solución de la clase pública {}
public boolean threeConsecutiveOdds(int[] arr) {
int consecutivo Odds = 0; // cuenta cuántas probabilidades hemos visto en una fila

para (int num : arrr) {
(num) == 1) { / // prueba de probabilidades rápidas (num % 2 == 1 también está bien)
consecutivo consecutivo consecutivo consecutivo Odds++;
(ConsecutiveOdds == 3) {
retorno verdadero; // encontrado tres probabilidades consecutivas
}
. ♫ ... {
consecutivo consecutivo consecutivo consecutivo Odds = 0; // reseteo en número
}
}
volver falso; // nunca llegó a una racha de 3 probabilidades
}
}
`` `

-...

#### 2down⃣ Python

``python
Solución de clase:
def threeConsecutiveOdds(self, arr: list[int] - Bool:
cuenta = 0 # contador extraño consecutivo

para num en arrr:
si num
Cuenta += 1
si cuenta == 3:
Retorno
más:
Conteo = 0
Retorno Falso
`` `

-...

#### 3down⃣ C++

``cpp
Incluido el título

Clase Solución {
public:
bool threeConsecutiveOdds(std::vector fielmente unido arr) {
int count = 0; // contador extraño consecutivo

para (int num : arrr) {
si (num) { / / / / / prueba de probabilidades rápida
++cuenta;
(cuenta == 3) {
volver verdadero; / // racha de 3 probabilidades encontradas
}
. ♫ ... {
recuento = 0; // reajuste en número
}
}
devolver falso;
}
};
`` `

■ ¿Por qué este código? * *
■ *Single pass* – sólo un bucle sobre el array.
■ *Recuerdo constante* – sólo un contador entero.
■ *Detección rápida* – `num ' 1` es marginalmente más rápida que `% 2` y es idiomática en muchos ajustes de entrevista.

-...

## Blog Article – “Tres probabilidades consecutivas: el bien, el mal y el imprudente”

■ *Meta description:* Aprende cómo resolver LeetCode 1550 – Tres probabilidades consecutivas – en Java, Python y C++. Explore brute‐force, counting, and one-liner approaches, and get interview‐ready with a concise O(n) solution.

-...

### 1. Recaptación de problemas

- **Input:** `int[] arr ' (Java), `list[int] arr ' (Python), `vector fielint ' arr ' (C++)
- *Largo*
* Rango de valores* 1 ≤ `arr[i] ≤ 1000
- ** Objetivo:** Regresar `verdad ' si alguno de los tres elementos **consecutivos** son todos extraños; de lo contrario `falso ' .

-...

### 2. La “buena” – Estrategia Contable

La estrategia de conteo es la solución de entrevista canónica:

``text
Conteo = 0
para cada num en arrr:
si num es extraño: contar += 1
más: cuenta = 0
si cuenta == 3: volver verdadero
devolver falso
`` `

*Por qué es bueno*

Silencio Criterion Silencio Por qué puntúa alta Silencio
Silencio--------------...
Silencio **Tiempo** Silencio O(n) – un pase, lineal para el tamaño de la matriz
Silencio **Espacio** Silencio O(1) – sólo un contador
Silencio **Readability** Silencio Muy pequeña, clara intención
tención **Robustness** tención Funciona para todos los casos de borde (duración 3, alternando paridad) ←
tención **Performance** Silencio Minimal ramificación, operaciones de tiempo constante Silencio

-...

### 3. La “Bad” – Naïve Brute Force

``text
para mí de 0 a arrr.length-3:
si arr[i], arrr[i+1], arr[i+2] son todos extraños:
retorno verdadero
devolver falso
`` `

**Downsides* *

TEN TERRITORIO TERRITORIO TERRITORIO
Silencio...
← Re-checks overlapping windows ← O(3n) ♥ O(n) pero con una mayor constante ←
Silencio Less intuitiva Silencio Puede ser mal escrito en entrevistas ←
Silencio Más código ← Aumenta la posibilidad de errores Silencio

Todavía es *aceptable* para pequeñas entradas, pero innecesario cuando el método de conteo está disponible.

-...

### 4. El “Ugly” – One‐Liner con “search_n” (C+++) / “any” (Python)

■ *Ejemplo (C++): *
" Return std::search_n(arr.begin(), arr.end(), 3, 0, [](int a){ return a " 1; }) != arrr.end(); `

**Pros**

- Muy corto
- Expresa su intención en un estilo funcional

**Cons**

- Difícil de leer para los no expertos
- Depende de las utilidades específicas del idioma que muchos entrevistadores no esperan
- Malas prestaciones debido a posibles sobrecargas adicionales (comparaciones de elementos, objetos de función)

■ *Cuando se utiliza:* Cuando usted está trabajando en una base de código de producción que ya tiene tales utilidades, o cuando desea impresionar con “C++ magia” – pero estar listo para explicar los mecánicos subyacentes en una discusión.

-...

### 5. Resumen de la complejidad

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
TENIENDO TERRITORIO **O(n)** Silencio**
Silencio Brute‐Force Silencio **O(n)** (factor constante) 3) Silencio **O(1)**
TENIDO UNA VIDA **O(n)** Silencio **O(1)**

El método contable domina en *toda* métrica.

-...

### 5. Consejos para entrevistas

1. **Declara el problema en tus propias palabras. #
“Estamos buscando una carrera de tres probabilidades, por lo que sólo tenemos que hacer un seguimiento de cuántas probabilidades hemos visto en una fila. ”

2. **Explicar la contra idea antes de escribir código. #
Esto te muestra entender *por qué* estás escaneando linealmente y *cómo* el algoritmo garantiza la corrección.

3. *Mención bitwise odd check. #
`num & 1` es un truco clásico en las entrevistas de codificación y muestra que conoce trucos de rendimiento de bajo nivel.

4. **Pregunta sobre las limitaciones. #
“Tus limitaciones (≤ 1000) hacen que un paso de fuerza bruta sea factible, pero la solución contable sigue siendo mejor. ”
Esto abre una discusión sobre *operaciones de optimización*.

5. **Tiempo de intercambio espacial.**
Mostrar que puede elegir el algoritmo adecuado para la situación – *bueno vs malos* enfoques.

-...

### 6. Takeaway - Cómo hacer realidad esta pregunta

Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio **1. Comprender “consecutivo”** Silencio Clarify que las ventanas pueden superponerse; reiniciar el contador en números. Silencio
TEN **2. Usar un solo contador** TENIDO Escribe el bucle contable. Silencio
tención **3. Verificar los casos de borde** tención Duración 3 → `false`; números alternantes → `false`; triples probabilidades en cualquier posición → `true`. Silencio
tención **4. Explicar la complejidad** Silencio Los entrevistadores les encanta ver O(n) / O(1). Silencio
Silencio **5. Prepárate para explicar alternativas** Silencio Mention brute‐force y una línea para la integridad. Silencio

-...

### 7. SEO " Career Advice

Silencio SEO Keyword Silencio ¿Por qué importa
Silencio...
Silencio `Three Consecutive Odds LeetCode` ¦ Termo de búsqueda básico utilizado por los reclutadores cazan para la experiencia de LeetCode. Silencio
Silencio `Java Three Consecutive Odds` ¦ Targets Java developers. Silencio
Silencioso `Python LeetCode 1550` Silencio Pulls Python-centric interviews. Silencio
Silencio `C++ Contando Algorithm` Silencio Destaca la eficiencia algoritmo, un plus para posiciones de diseño del sistema. Silencio
Silencio `Interview algoritmo practice` Silencio Broadens llegar a cualquiera que se prepare para las entrevistas de codificación. Silencio

■ **Job‐search Sugerencia:**
■ Añadir este problema a tu cartera en GitHub, enlazarlo en tu Enlace En encabezado, y escribir un blog como este. El equipo de trabajo filtra a menudo los candidatos por el rendimiento de LeetCode, por lo que una solución clara y optimizada con una explicación adjunta puede darle un borde mensurable.

-...

### 8. Pensamientos finales

- **Counting** es la solución *de-facto* LeetCode 1550.
- La fuerza bruta es rápida pero redundante.
- Los solteros son lindos, pero la legibilidad importa más en entrevistas.

Con los tres snippets arriba y la explicación de la entrevista, usted tiene un paquete pulido que está listo para impresionar a los gerentes de contratación y pasar el control LeetCode.

¡Feliz codificación! 🚀