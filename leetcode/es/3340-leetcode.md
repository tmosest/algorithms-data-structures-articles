-...
Título: LeetCode 3340. Comprobación de cuerda balanceada -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 3340 – Comprobar la cuerda balanceada
■ **Bueno, malo & ugly** – Una guía práctica para escapar Esta entrevista Pregunta (y aterrizar su trabajo de sueño)

-...

### 📌 TL;DR

- **Problema**: Para una cadena de sólo dígitos `num`, compruebe si la suma de dígitos en índices iguales a la suma de dígitos en índices impares.
Un escaneo lineal, manteniendo dos totales en funcionamiento.
- *Hora*
- **Espacio**: `O(1)`
- ** Idiomas**: Java, Python, C++
- **Por qué importa**: Simple pero perfecto para demostrar el pensamiento, código limpio y fundamentales de entrevista.

-...

## 1. Declaración de problemas (LeetCode)

■ **Comprobando la cuerda balanceada**
■ *Dificultad:* Fácil
■ **Definición**
■ Una cadena de dígitos es *balanceada* si la suma de dígitos en índices iguales a la suma de dígitos en índices impares.
■ Regresar `verdad ' si `num` es equilibrado, de lo contrario `falso ' .
■ **Constraints**
√≥ - `2 י= num.length
- `num' consiste sólo en dígitos.

*Ejemplos*

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
Silencio `"1234" Silencio `false` Silencio Incluso suma = 1+3=4, Odd sum = 2+4=6
Silencio `'"24123" Silencio `true` Silencio Incluso suma = 2+1+3=6, Odd sum = 4+2=6

-...

## 2. El “bien” – Por qué Este problema es ideal para entrevistas

Por qué ayuda a su carrera a vivir
Silencio--------------------
tención **Clear, deterministic** tención No hay casos ambiguos – perfecto para las pantallas de primera ronda. Silencio
Silencio ** Algoritmo de paso** Silencio Demonstrates O(n) razonamiento, un punto básico en las entrevistas de codificación. Silencio
Silencio ** Complejidad mínima del borde** Silencio Enfoca su atención en claridad algorítmica, no codificación defensiva. Silencio
Silencio **Language‐agnostic** Silencio Puedes resolverlo en Java, Python o C++ – Elige el idioma más cómodo para ti. Silencio
Silencio **Oportunidad para una solución espacial O(1) limpia** Silencio muestra la diferencia entre el espacio algorítmico y auxiliar. Silencio

-...

## 3. El “Bad” – Pitfalls comunes

Silencio Pitfall Silencio
Silencio...
Silencio **Using `int` overflow on large strings** ← No es un problema aquí debido a la longitud máxima 100, pero siempre tenga cuidado con los límites enteros. Silencio
tención **Indices de restauración como 1-basado** tención Recuerde que los índices de array comienzan a 0 en la mayoría de los idiomas. Silencio
Silencio **Confundir “indices” con “incluso dígitos”** Silencio Incluso los índices significa la posición (0, 2, 4, ...), no la paridad del dígito. Silencio
Silencio **Uso de estructuras de datos pesadas** Silencio Ninguna necesidad de listas o mapas; un simple bucle es suficiente. Silencio
Silencio **Ignorando el espacio blanco/inválido** Silencio LeetCode garantiza cadenas de sólo dígitos; el código de producción debe validar. Silencio

-...

## 4. El “Ugly” – Variaciones avanzadas y extensiones

← Variación Silenciosa Cómo ampliar la solución
Silencio------------------
Silencio **Large string (106+)** Silencio Still O(n) with constant space, but watch for `long` vs `int` if sum can exceed `Integer. MAX_VALUE`. Silencio
Silencio **Streaming input** tención Personajes del proceso al llegar; mantener dos sumas sin almacenar toda la cuerda. Silencio
Silencio **Multiple consultas** Silencio Si se le pide muchas cadenas, pre-compute prefix sumas para responder cada consulta en O(1). Silencio
Silencio **Generalización a posiciones arbitrarias** Silencio Reemplazar “even/odd” con cualquier condición mod; mantener dos sumas en consecuencia. Silencio

-...

## 5. Camión de Algoritm

1. **Initializar dos contadores**: `evenSum = 0`, `odd Sum = 0`.
2. **Tetrato sobre la cuerda** carácter por personaje.
3. **Convertir** cada personaje a su valor numérico (`ch - '0'` en C++/Java, `int(ch)` en Python.
4. **Añadir** a `evenSum` si el índice es incluso, de otra manera a `oddSum`.
5. Después del bucle, **retorno** `evenSum == oddSum`.

No se necesitan estructuras auxiliares de datos, sólo un solo bucle y dos variables enteros.

-...

## 6. Code Solutions

⇩ Las tres soluciones funcionan en el tiempo **O(n)** y **O(1)** espacio.

### 6.1 Java

``java
Clase Solución {
booleano público esBalanced(String num) {
int evenSum = 0, odd Sum = 0;
para (int i = 0; i) i++) {
int digit = num.charAt(i) - '0';
(i) == 0) inclusoSum += dígito;
más extraño Sum += dígito;
}
volver inclusoSum == oddSum;
}
}
`` `

### 6.2 Python

``python
Solución de clase:
def isBalanced(self, num: str) - Conf Bool:
even_sum, odd_sum = 0, 0
para idx, ch in enumerate(num):
dígito = int(ch)
si idx % 2 == 0:
incluso_sum += dígito
más:
odd_sum += dígito
volver incluso_sum == odd_sum
`` `

### 6.3 C++

``cpp
Clase Solución {
public:
bool isBalanced(string num) {
int evenSum = 0, odd Sum = 0;
para (int i = 0; i) ++i) {
int digit = num[i] - '0';
(i % 2 == 0) inclusoSum += dígito;
más extraño Sum += dígito;
}
volver inclusoSum == oddSum;
}
};
`` `

-...

## 7. Enfoque alternativo: uso de " mapa " / " reducir " (Python solamente)

``python
def is_balanced(num: str) - título Bool:
incluso = suma(int(num[i]) para i en rango(0, len(num), 2))
odd = sum(int(num[i]) for i in range(1, len(num), 2))
retorno incluso == raro
`` `

*Pros*: Muy conciso.
*Cons*: Sobrecarga constante ligeramente superior; no ideal para entrevistas críticas de rendimiento.

-...

## 8. Consejos de entrevista

TENIDO TENDIDO ANTERIOR Por qué ayuda a vivir
Silencio...
Silencio **Declara tu enfoque** Silencio "Usaré un solo paso O(n) escaneado" – muestra un pensamiento algorítmico claro. Silencio
Silencio **Hablar sobre el tiempo/espacio** Silencio Demuestra la comprensión de la notación de Big‐O. Silencio
Silencio **Preguntar preguntas aclaratorias** Silencio Confirme si los índices están basados en 0 o 1 base; muestre minuciosidad. Silencio
Silencio **Mention edge cases** Silencio Aunque es mínimo aquí, puede discutir lo que sucede si la longitud de la cadena es extraña/incluso. Silencio
Silencio ** Pruebas de debate** Silencio Ejecute su código en los ejemplos proporcionados, y también en casos de borde como '"00" y '"99"". Silencio
Silencio **Mostrar código limpio** Silencio Preferir readability over micro-optimizations in interviews. Silencio

-...

## 9. Conclusión optimizada

■ ¿Buscando aterrizar un rol de desarrollador de vanguardia, back-end o full-stack? Mastering **LeetCode 3340 – Check Balanced String** demuestra que puedes pensar *O(n)*, escribir código Java/Python/C++, y evitar errores de entrevista comunes. Comparte esta solución en tu GitHub, blog o portafolio y los reclutadores de relojes notan tu agudeza algorítmica.

**Keywords**: LeetCode, Check Balanced String, Balanced String, Java interview, Python interview, C++ interview, coding interview prep, algoritmo, O(n), O(1), entrevista de trabajo, ingeniero de software, reclutador técnico.

-...

**Feliz codificación, y buena suerte en su próxima entrevista! * *