-...
Título: LeetCode 3337. Personajes totales en cuerda después de las transformaciones II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Objetivo #

Después de `t` transformaciones la cuerda puede ser astronómicamente larga (hasta 25n).
Sólo necesitamos su longitud – que es el número total de caracteres presentes después de todo
transformaciones.
La observación clave es que el arreglo *exacto* de los personajes es irrelevante,
sólo cuántos de cada una de las 26 letras existen.
Si podemos calcular la frecuencia final de cada carta, sumarlas da la
respuesta.

----------------------------------------------------

### 1. Cuenta las letras en la cadena de inicio

`` `
cnt[i] = número de ocurrencias de la letra i‐th (a → 0, ... , z → 25)
`` `

Esto necesita `O(las vidas eternas)` tiempo y es el único lugar donde la cuerda original es
inspeccionado.

----------------------------------------------------

### 2. ¿Cómo cambia una carta?

Para una carta " c " (0...25) se nos da `nums[c] = k ' .
Durante una transformación `c` es reemplazada por las siguientes 'k' letras de la
alfabeto (envolver alrededor).
Así que en un solo paso:

`` `
c → (c+1) mod 26
c → (c+2) mod 26
...
c → (c+k) mod 26
`` `

----------------------------------------------------

### 3. Matriz de transición

Construimos una matriz 26 × 26 **T** donde

`` `
T[i][j] = número de letras j producidas a partir de una sola letra i en un paso
`` `

Por cada `i' (letter) y cada `x = 1 ... nums[i] `

`` `
siguiente = (i + x) mod 26
T[i][next] += 1
`` `

La matriz ya contiene el efecto del envoltorio, y cada entrada
es 0 o 1 (porque cada carta producida es única en un paso).

----------------------------------------------------

### 4. Muchos pasos – rápida exponentiación

Después de " pasos " una sola letra " produce una distribución dada por
`I`‐th row of **T(t)** (la matriz T elevada al poder `t`).
Toda la transformación de toda la cuerda es

`` `
final_counts = cnt · T(t)
`` `

(`cnt` se trata como vector de filas).

Para calcular `T(t)` utilizamos la exponencia binaria:

`` `
resultado = I // matriz de identidad
potencia = t
mientras poder 0
si el poder es un resultado extraño = resultado · T
T = T · T
potencia = poder / 2
`` `

El tamaño de la matriz es sólo 26, por lo que una multiplicación toma
`263 Ω 17 576` operaciones de escalar – trivial para un ordenador.
Lo realizamos `O(log t)` tiempos, que es a la mayoría de 30 multiplicaciones para
No ≤ 109.

Toda aritmética se realiza modulo `MOD = 1 000 000 007` para evitar el desbordamiento.

----------------------------------------------------

### 5. Aplicar la matriz potenciada a las frecuencias iniciales

`` `
para mí en 0...25
para J en 0...25
final_counts[j] += cnt[i] * T(t)[i][j] (mod MOD)
`` `

Sólo se necesitan 262 operaciones.

----------------------------------------------------

### 6. Resultado

La respuesta es el número total de cartas después de todas las transformaciones:

`` `
respuesta = suma(final_counts) mod MOD
`` `

----------------------------------------------------

### 7. Complejidad

TEN TERRITOR TERRITOR TEN TERRITOR TEN TERRITOR TEN TERRITOR SON TERRITOR SON SON SON TEN SON SON SON 
Silencio... . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 
TENIDO " Cnt " TENIDO `O(las vidas eternas) ' TENIDO `O(26) ' Silencio
Silencioso edificio **T** Silencioso `O(262)`
Silencioso Matrix exponentiation habit `O(263 log t) ' (Ω 1.7 k × log t)
Silencioso Vector × matriz Silencioso `O(262)` Silencio
Silencio Sumario final Silencioso `O(26)`

El término dominante es la exponencia de la matriz; todo lo demás es insignificante.

----------------------------------------------------

### 8. Por qué funciona esto

*Linearidad* – El número de cada carta después de un paso es lineal
combinación de los números antes del paso; matrices codifican exactamente que
transformación lineal.
- **Poder de una matriz** - Repetir el mismo paso lineal 't' tiempos es el
igual que aplicar la matriz `t` veces, es decir, multiplicando por 'T(t)`.
Fast exponentiation computes `T(t)` in logarithmic time.
- Modulo... Los conteos crecen exponencialmente; el uso del módulo mantiene todo
resultados intermedios ligados.
- **No hay construcción de cuerdas** – Nunca construimos la cuerda gigantesca; sólo nosotros
guarda 26 contadores.

----------------------------------------------------

** Resultado**
Contando las letras iniciales, construyendo la matriz de transición,
el poder 't', aplicarlo a los recuentos iniciales, y resumir el resultado
frecuencias, obtenemos la longitud de la cuerda después de transformaciones 't',
modulo `1 000 000 007`.