-...
Título: LeetCode 400. Nth Digit -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. El problema (Leetcode 400 – **Nth Digit**)

Dado un entero **n**, devuelve el nto dígito de la secuencia de entero infinito

`` `
1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, ...
`` `

■ *Ejemplo*
(el 11o dígito es el segundo dígito del número 10)

■ **Constraints**
≤ 231 – 1

El objetivo es hacer esto en **O(log n)** tiempo sin generar toda la secuencia.



----------------------------------------------------

## 2. Core Idea

Los números se agrupan por su número de dígitos.

Silencio Digit length Silencio Números Silencio Total dígitos
Silencio------------------------------------
Silencio 1 Silencio 1 - 9 Silencio 9
Silencio 2 Silencio 10–99 Silencio 90 × 2 = 180 Silencio
Silencio 3 Silencio 100–999 Silencio 900 × 3 = 2700 Silencio
Silencio...

1. **Encuentra el bloque** que contiene el nto dígito.
Tamaños de bloques de *n* hasta *n* encaja dentro del bloque actual.

2. Encontrar el número exacto dentro de ese bloque.
Número = inicio + (n‐1) / dígito `

3. **Extraer el dígito** de ese número.
Convertir en cadena o utilizar división/modulo.

----------------------------------------------------

## 3. Implementaciones de referencia

A continuación se encuentran soluciones limpias y de producción en **Java, Python y C++**.
Los tres utilizan el mismo enfoque basado en matemáticas.

-...

### 3.1 Java

``java
Solución de la clase pública {}
int findNthDigit(int n) {
// Números de 1 dígitos (1-9)
dígitos int = 1;
cuenta larga = 9; // cuántos números en este bloque
base larga = 1; // primer número en este bloque

mientras (n не dígitos * cuentan) {
n -= dígitos * cuenta; // saltar todo el bloque
dígitos+; // siguiente bloque
*= 10; // 10× más números
base *= 10; // primer número es 10^digits
}

// el número que contiene el nto dígito
largo número = base + (n - 1) / dígitos;
int digitIndex = (int) (n - 1) % digitos); // 0 basado

// devolver el dígito requerido
String s = Long.toString(número);
devolver s.charAt(digitIndex) - '0';
}
}
`` `

**Puntos clave* *

* `long` se utiliza para evitar el desbordamiento cuando `n` está cerca de `231 - 1`.
* El algoritmo es `O(log10 n)` porque el bucle itera en la mayoría de 10 veces.



-...

#### 3.2 Python

``python
Solución de clase:
def findNthDigit(self, n: int) - int:
dígitos = 1 # longitud del dígito del bloque actual
contar = 9 # números en este bloque
inicio = 1 # primer número en este bloque

# Paso 1 - encontrar el bloque
* cuenta:
n -= dígitos * cuenta
dígitos += 1
*= 10
inicio *= 10

# Paso 2 - localizar el número
Número = inicio + (n - 1) // dígitos
# Paso 3 - dígito dentro del número
digit_index = (n - 1) % digitos
int(str(número)[digit_index])
`` `

**Por qué funciona* *

* El bucle funciona ≤ 10 veces (para enteros de 32 bits).
* El aritmético entero es seguro en Python – sin preocupaciones de desbordamiento.



-...

### 3.3 C++

``cpp
Clase Solución {
public:
int findNthDigit(int n) {
dígitos largos = 1; // longitud del bloque actual
cuenta larga = 9; // números en bloque actual
inicio largo = 1; // primer número en bloque actual

// 1) Encontrar el bloque que contiene el nto dígito
mientras (n не dígitos * cuentan) {
n -= dígitos * cuentan;
dígitos+;
*= 10;
*= 10;
}

// 2) Localizar el número exacto
largo número = inicio + (n - 1) / dígitos;
int digitIndex = (int)(n - 1) % digitos);

// 3) Extraer el dígito requerido
cadena s = to_string(número);
devolver s[digitIndex] - '0';
}
};
`` `

* `long' protege contra el desbordamiento.
* La solución sigue la misma estrategia basada en matemáticas.



----------------------------------------------------

## 4. Artículo del Blog – “El Bien, el Mal, y el Ugly de Leetcode 400”

■ **SEO Palabras clave**:
■ *Nth Digit Leetcode*, *Solución java*, *Solución Pitón*, *Solución C+*, *entrevista de codificación*, *entrevista de algoritmo*, *entrevista de trabajo*, * algoritmo *O(log n)*, *problema de extracción de dígitos*

-...

#### 4.1 Introducción

El problema **Nth Digit** (Leetcode 400) es un rompecabezas clásico de entrevistas que prueba la capacidad de un candidato para razonar sobre posiciones de dígitos, secuencias aritméticas y manejo cuidadoso de números grandes. Mientras que la declaración parece simple, los obstáculos ocultos pueden tropezar incluso programadores experimentados. En este post, diseccionamos el problema en sus aspectos *bueno* (mejores prácticas), *bad* (errores comunes), y *muy* (calentamientos de cabeza) y proporcionamos soluciones limpias en **Java, Python y C+**.

■ *¿Por qué dominar este problema te ayuda a conseguir un trabajo? *
■ Porque muestra:
■ 1. **Mathematical insight** – convirtiendo un problema aparentemente bruto-force en una fórmula de tiempo de registro.
■ 2. **Atención a desbordamiento** – crítica para entrevistas en límites de 32-bit/64-bit.
■ 3. ** portabilidad de lenguaje cruzado** – se puede explicar el mismo algoritmo en cualquier pila.

-...

### 4.2 Problema Recaptura

■ ** Objetivo:** Devolver el `n`‐th dígito de la secuencia concatenada `123456789101112...`.
■ **Constraints:** `1 ≤ n ≤ 231 - 1` (Ω 2 billion).
■ *Pocamientos físicos*
* Generar números o cadenas hasta `n` – O(n) tiempo y memoria.
* Olvídate de que `n` es 1-basado mientras que los índices de array están 0-basados.
* Desbordamiento al computar `10^digits` o `digit * count`.

-...

### 4.3 The *Good* – Elegante O(log n) Solución

##### 4.3.1 Matemáticas en el trabajo

1. *Tamaños de reloj*
* Números de 1 dígitos: 9 × 1 = 9 dígitos
* números de 2 dígitos: 90 × 2 = 180 dígitos
* Números de 3 dígitos: 900 × 3 = 2700 dígitos

2. **Encontrar el bloque** – substraer tamaños de bloque hasta que el `n` restante se ajuste.
Debido a que el tamaño de cada bloque crece por un factor de 10, necesitamos en la mayoría **10 iteraciones** para un entero de 32 bits.

3. ** Número exacto** – una vez que conocemos el bloque, el número de objetivo es
`número = inicio + (n‐1) / dígitos`.

4. **Digito de descarga** – el índice dentro de ese número es
`digitIndex = (n‐1) % digits`.
Podemos convertir a una cadena o utilizar la división/multiplicación entero para aislar el dígito.

#### 4.3.2 Por qué es rápido

El algoritmo es **O(log n)**: el bucle funciona ~10 veces, y el resto es aritmética de tiempo constante.
El uso del espacio es **O(1)**.
Esta eficiencia es lo que los entrevistadores quieren ver.

-...

### 4.4 The *Bad* – Common Mistakes

¿Por qué no se puede arreglar la vida?
Silencio--------------------------
Silencio **Brute‐force string building** (`for i in 1..n: result += i`) Silencio `n` puede ser 2 billion → Memory blow-up & time out ← Utilizar matemáticas para saltar directamente Silencio
Silencio **Usando int en lugar de largo/largo** Silencio `10^10` desborda `int` en Java/C++ Silencio Uso de 64-bits tipos
Silencio ** Errores de uno por uno** Silencio `n` es 1-basado; muchas personas usan erróneamente índices 0-basados ¦ Mantener `(n-1)` hasta el paso final
Silencio **Ignorando números de 0 dígitos** Silencio 10 tiene dos dígitos; contar dígitos de forma incorrecta conduce a un bloque incorrecto.
Silencio **Asumiendo que el primer dígito es siempre no-cero** Silencio Números como 100 contienen 0; olvidándose para convertir a cadena puede perder los principales ceros ¦ Convertirse en cuerda o mango a través de división

-...

### 4.5 The *Ugly* – Edge‐Case Quirks

1. Largest `n`**
* < n = 231 – 1  `
* El bloque de 10 dígitos (`100 000 0000`‐`9 999 999 ' ) comienza en el dígito 9 999 999 999
* Nuestro algoritmo maneja con gracia esto porque `contra` se convierte en `9 000 000` (todavía dentro de `long').

2. ** Números internos de dígito cero* *
* El primer cero aparece en la posición 10 (el número 10).
* Nuestra extracción de dígitos (n-1)%digits`) funciona porque se indexa en la representación de cadena, no en el valor numérico.

3. *No bases decimales*
* El algoritmo asume base‐10. Para entrevistas, clarifique la base; de lo contrario las matemáticas cambian.

-...

### 4.6 Código completo

■ #Java #

``java
Solución de la clase pública {}
int findNthDigit(int n) {
dígitos int = 1;
cuenta larga = 9;
base larga = 1;
mientras (n не dígitos * cuentan) {
n -= dígitos * cuentan;
dígitos+;
*= 10;
base *= 10;
}
largo número = base + (n - 1) / dígitos;
int digitIndex = (int) (n - 1) % digitos);
volver String.valueOf(number).charAt(digitIndex) - '0';
}
}
`` `

■ Python

``python
Solución de clase:
def findNthDigit(self, n: int) - int:
dígitos, cuenta, comienza = 1, 9, 1
* cuenta:
n -= dígitos * cuenta
dígitos += 1
*= 10
inicio *= 10
Número = inicio + (n - 1) // dígitos
int(str(número)[n - 1) % dígitos])
`` `

■ **C++**

``cpp
Clase Solución {
public:
int findNthDigit(int n) {
dígitos largos = 1, cuenta = 9, comienzo = 1;
mientras (n не dígitos * cuentan) {
n -= dígitos * cuentan;
dígitos+;
*= 10;
*= 10;
}
largo número = inicio + (n - 1) / dígitos;
int digitIndex = (int)(n - 1) % digitos);
volver a_string(número)[digitIndex] - '0';
}
};
`` `

-...

### 4.7 Testing Your Implementation

Silencio en la entrada esperada
Silencio----------
Silencio 3 Silencio 3 Silencio Primero 3 dígitos son 1,2,3 Silencio
Silencio 11 Silencio 0 Silencio 10 contiene 0 Silencio
Silencio 100 Silencio 1 Silencio 100to dígito es el primer '1' del número 10
Silencio 190 Silencio 9 Silencio Último dígito de bloque de números de 2 dígitos
Silencio 1900 Silencio 1 Silencio Primer dígito de bloque de números de 3 dígitos tención
TEN 2147483647 TENIDO 7 TENIDO Caso Edge, mayor 32 bit int TEN

Use pruebas de unidad o scripts rápidos para validar cada caso.

-...

### 4.8 Take‐ Puntos para su búsqueda de trabajo

1. **Mostrar pensamiento matemático** – los entrevistadores aman algoritmos que saltan la ingenua ruta O(n).
2. ** Casos de borde hundido con confianza** – demostrar la conciencia de desbordamiento y el pensamiento basado en 1 vs 0.
3. **Deliver limpio, código de idiomas** – estar preparado para explicar su solución en Java, Python, o C++ dependiendo de la pila de entrevistas.
4. **Explicar tiempo " complejidad espacial** – *(log n)* tiempo, *O(1)* espacio.
5. **De vuelta a los patrones de entrevista** – este problema es una variante de preguntas “Digit DP” y “sequence position” que aparecen en muchas pistas de entrevista.

-...

### 4.9 Pensamientos Finales

El problema Nth Digit es engañosamente simple pero empaquetado con conceptos relevantes para entrevista: secuencias aritméticas, búsqueda logarítmica, manejo de desbordamiento y código limpio. Dominar no solo te gana un “solver” de 6 meses en Leetcode sino que también muestra a los reclutadores que puedes transformar un desafío aparentemente bruto en una elegante solución O(log n).

Feliz codificación, y que su próxima entrevista sea *a la mejor!