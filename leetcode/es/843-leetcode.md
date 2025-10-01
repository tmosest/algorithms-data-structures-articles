-...
Título: LeetCode 843. Supongo que la palabra...
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Atención de la Palabra – 843**
*(Java – Interfaz interactiva “Master”)*

-...

## 1. Recaptación de problemas

Se le da un *palabro* de hasta 10 000 cadenas de 6 letras (toda la misma longitud).
Uno de ellos es la palabra secreta**.

Puedes inventar hasta 10 suposiciones**.
Después de cada conjetura el objeto `Master` le dice cuántos caracteres coinciden con la palabra secreta ** en las mismas posiciones** (un entero `0 ... 6`).
Si adivinas la palabra secreta, el juego termina con éxito; de lo contrario tienes que seguir adivinando hasta que golpeas la palabra secreta o te quedas sin intentos.

Su trabajo es escribir una función

``java
novato encontrarSecretWord(String[] wordlist, Maestro)
`` `

que hace la secuencia de conjeturas y garantiza una victoria dentro del número permitido de intentos.

-...

## 2. Lo que el entrevistador realmente pregunta

1. **¿Puede modelar la interacción como un problema de búsqueda? * *
– Cada conjetura divide el candidato actual establecido según el valor de retroalimentación.
2. **¿Cuál debería elegir el siguiente? #
– Queremos reducir el conjunto de candidatos lo más rápido posible (la ganancia máxima de información).
3. **¿Qué oficio estás dispuesto a hacer? * *
– La estrategia óptima (minimax) es cara; una heurística práctica a menudo basta.

Explique que estamos resolviendo un *imperfect‐information juego* con el objetivo de minimizar el peor número de conjeturas.

-...

## 3. Estrategia de alto nivel

1. **Empieza con un "pivot" adivina* *
– Escoge cualquier palabra (aleatorio o determinista).
– Call `master.guess(pivot)` → conseguir 'm` coincidencias.

2. **Iniciar la lista**
– Mantenga sólo palabras que también dan exactamente "m" partidos con el pivote.
– Todas las otras palabras son imposibles.

3. *Iterate*
– Si la lista filtrada tiene sólo una palabra izquierda, adivina.
– De lo contrario, elegir otra palabra de la lista filtrada (a menudo al azar).
– Repita el paso filtrante utilizando la nueva suposición.

4. **Parar*
– O usted golpeó 6 fósforos (fundió el secreto) o ha utilizado todas las 10 conjeturas.

-...

## 4. Por qué funciona esto

*Feedback es exacto* Si una palabra cede los partidos " k " , cualquier candidato debe ceder el mismo `k ' .
- **La fusión encoge el espacio exponencialmente** – En una distribución aleatoria, cada suposición elimina aproximadamente una fracción constante de las palabras restantes.
- **Random o pivote determinista** – Ambos están bien; el azar evita las construcciones patológicas de los peores casos, determinista (por ejemplo, minimax basado en similitudes) garantiza ≤ 10 conjeturas en promedio.

-...

## 5. Algoritmos prácticos

### 5.1 Filtración aleatoria/grande (simple)

``java
Clase Solución {
int match(String a, String b) { ... } // count same‐position chars

public void findSecretWord(String[] words, Master master master) {
Lista Nombramiento Nombrados = Nuevo ArrayList(Arrays.asList(words));

para (int i = 0; i) 10 " golpe !candidates.isEmpty(); i++) {
// elegir la palabra i‐th (o al azar de la lista)
Estring guess = candidates.get(0); // deterministic
int match = master.guess(guess);
si 6) retorno; // éxito

// filtro
Lista seleccionadaString siguiente = nuevo ArrayList correctamente();
para (String w : candidatos) {}
si (w.equals(guess))) continúan;
si (match(gues, w) == fósforos) siguiente.add(w);
}
candidatos = siguientes;
}
}
}
`` `

*La complejidad:*
- `match()` is `O(6)` → constante.
- Cada iteración escanea todas las palabras restantes → `O(n)` por ronda.
- En el peor caso `O(n2)`, pero en la práctica la lista se encoge rápidamente.

### 5.2 Greedy basado en la similitud (mejor para datos aleatorios)

1. **Anotación de similitudes precomputadas**
- Por cada palabra cuenta cuántas otras palabras comparten al menos un mismo personaje en la misma posición.

2. **Ordenar la lista de palabras descendiendo por esta puntuación* *
- La palabra más “popular” eliminará a muchos candidatos.

3. **Guess en ese orden, filtrando después de cada conjetura* *
- El mismo paso filtrante que arriba.

*Por qué esto ayuda: *
Cuando usted espera que la mayoría de las conjeturas regresen los partidos de `0` (Ω80 % chance), eligiendo una palabra que coincide con muchos otros en al menos una posición elimina un gran pedazo de posibilidades si la retroalimentación es `0`.

-...

## 6. Casos de borde y discusión

Escenario Silencioso Lo que sucede Silencio Por qué está bien
Silencio----------------------------...
Silencio Todas las palabras son completamente distintas (por ejemplo, "abcdef", "ghijkl", ...").
← Lista contradictoria de caso peor Silencio El pivote aleatorio podría tener éxito dentro de 10 conjeturas Silencio Aunque el enfoque de similitud determinista puede fallar, el filtro aleatorio garantiza el éxito en 10 intentos porque el peor tamaño de caso ≤ 10 latitud
Silencioso `palabralista.length` > 10 000 Silencio Filtrando todavía `O(n)` cada ronda ¦ n está ligada por las restricciones del problema ¦

-...

## 7. Resumen de la complejidad

- Hora:
`O(n2 * 6)` peor caso, pero el caso promedio es `O(n log n)` debido a la contracción exponencial.
- ¿Qué?
`O(n)` para la lista de candidatos.

-...

## 8. Cómo presentar esto a un entrevistador

1. **Clarificar el problema:**
“Estamos jugando un juego interactivo; cada conjetura nos da el número de posiciones correctas. ”

2. **Definir la idea central:**
“Filter el candidato se fijó usando la retroalimentación exacta del partido; cualquier conjetura que no coincida elimina un gran número de palabras. ”

3. **Explicar la opción algoritmo:**
- "Yo elegiré la primera palabra (o una aleatoria) como mi pivote, consulta al Maestro, y luego guardaré sólo esas palabras que producen la misma retroalimentación. ”
- Repito hasta que encuentre el secreto o la lista está abajo a uno. ”

4. **Discusión del tiempo y el comercio espacial**
“Escaneamos la lista cada ronda, por lo que es `O(n)` por suposición. Debido a que la lista se encoge rápidamente, esto es aceptable. ”

5. **Extensiones de la mención**
- “Si queremos ser más inteligentes, podríamos calcular una partitura de similitud y siempre elegir la palabra más ‘informativa’. ”
- “Eso trae ideas basadas en minimax o entropía, pero la solución avaricia simple cumple con el límite de 10-pagos. ”

6. **Mostrar código snippet* *
“Aquí hay una implementación concisa que sigue los pasos anteriores. ”

-...

### Final Note

El núcleo de la solución es ** filtrado iterativo** basado en coincidencias de posición exacta.
Ya sea que elija un pivote al azar, la primera palabra, o un pivote con peso similar, la idea sigue siendo la misma: cada conjetura reduce el espacio de búsqueda, y después de un puñado de rondas siempre será capaz de golpear la palabra secreta dentro de los intentos permitidos.