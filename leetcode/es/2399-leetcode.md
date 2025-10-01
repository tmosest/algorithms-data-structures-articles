-...
Título: LeetCode 2399. Distancias de control Entre las mismas letras -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 2399 – Check Distances Entre las mismas cartas
■ ** “El Bien, el Mal y el Ugly” – Una guía práctica para los candidatos listos para la entrevista* *

-...

#### TL;DR

- **Problema**: Cada letra de la minúscula aparece *exactamente dos veces* en una cuerda `s`.
Por cada carta `i` (`'a' → 0`, ..., `'z' → 25`) el array `distance[i]` dice cuántos **otros** letras deben mentir entre sus dos ocurrencias.
Regresar `verdad' si `s` satisface todas las distancias dadas.

- **Solución**:
1. **Track‐First** – Almacene el primer índice de cada letra, luego valide en la segunda apariencia.
2. **Check‐Second** – Cuando veas una carta, mira de inmediato hacia adelante `distancia + 1` pasos y compara; establece la entrada a `-1` para evitar la doble comprobación.

- *La complejidad*
- Tiempo: `O(las vidas eternas)` (≤ 52)
- Espacio: `O(26)` (constant)

- ¿Por qué importa?
El patrón es común en preguntas de entrevista de cadena y radio. Dominar muestra que puede manejar *two-pass* lógica, uso de mapas y seguridad de bordes.

-...

Problema Recap

``text
Input
---
s – cuerda (longitud 2-52, todas minúsculas)
distancia – int[26] (0 basado en 'a'...'z')

Producto
---
booleano – verdadero sif s es una cadena “bien espaciada”
`` `

*Ejemplo*

`` `
s = "abaccb"
distancia = [1,3,0,5,0,...] // sólo a,b,c materia
Resultado: verdadero
`` `

-...

Dos enfoques ganadores

Silencio Silencio
Silencio--------------...
tención **Track‐First** Silencio Recordar el primer índice; en el segundo índice compute `i - firstIndex - 1`. Silencio Simple, claro. ← Requiere una bandera “primera vista”; utiliza una matriz de 26 ints. Silencio
Silencio **Ver-Second** En primer lugar, mire directamente `i + distancia + 1`. Marca procesada (`-1`). tención One‐pass; no hay necesidad de un array de bandera separado. TENIDO Slightly trickier to understand; utiliza 'distance` array mutably. Silencio

A continuación encontrará **Java, Python, y C+** implementaciones para *ambos* métodos para que pueda elegir el que se ajuste a su estilo.

-...

## 3VIEW⃣ Code Snippets

■ **Consejo:** Todas las soluciones suponen que las restricciones garantizan que cada letra aparece *exactamente dos veces*, por lo que no se requiere validación adicional más allá de los controles de límites.

### 3.1 Java

``java
// --------
// Java – Track‐First (HashMap basado)
// --------
Solución de la clase pública {}
public boolean check Distancias(Cantidad s, int[] distancia) {
Mapa seleccionadoCaracter, Integer primeroPos = nuevo HashMap garantizado();
(int i = 0; i) s.length(); i++) {
char ch = s.charAt(i);
si (primerPos.containsKey(ch)) {
int diff = i - firstPos.get(ch) - 1;
si (diff != distancia[ch - 'a') devolver falso;
. ♫ ... {
firstPos.put(ch, i);
}
}
retorno verdadero;
}
}

// --------
// Java – Check‐Second (en lugar)
// --------
Solución de la clase pública {}
public boolean check Distancias(Cantidad s, int[] distancia) {
(int i = 0; i) s.length(); i++) {
int d = distance[s.charAt(i) - 'a'];
// si segunda ocurrencia o fuera de los límites → fallar
si (i + d + 1 √≥= s.length() ANTETENIDO S.charAt(i + d + 1) != s.charAt(i)
devolver falso;
distancia[s.charAt(i) - 'a'] = -1; // marca procesada
}
retorno verdadero;
}
}
`` `

#### 3.2 Python

``python
# --------
Python – Track‐First
# --------
Def check Distancias(s: str, distance: list[int]) - Conf Bool:
primero
para i, ch in enumerate(s):
si ch en primer lugar:
si yo - primero[ch] - 1 != distancia[ord(ch) - 97]:
Retorno Falso
más:
primero [ch] = i
Retorno

# --------
Python – Check‐Second
# --------
Def check Distancias(s: str, distance: list[int]) - Conf Bool:
para i, ch in enumerate(s):
d = distancia[ord(ch) - 97]
si i + d + 1 √≥= len(s) o s[i + d + 1] != ch:
Retorno Falso
distancia[ord(ch) - 97] = -1 # marca procesada
Retorno
`` `

### 3.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

// --------
// C++ – Track‐First
// --------
Bool check Distancias (cadenamiento s, vector implicados iguales distancia) {}
vector asignadoint primero(26, -1);
para (int i = 0; i) ++i) {
int idx = s[i] - 'a';
si (primero[idx]!= -1) {
si (i - first[idx] - 1 != distance[idx]) devuelve falso;
. ♫ ... {
primero [idx] = i;
}
}
retorno verdadero;
}

// --------
// C++ – Check‐Second
// --------
Bool check Distancias (cadenamiento s, vector implicados iguales distancia) {}
para (int i = 0; i) ++i) {
int d = distancia[i] - 'a';
si (i + d + 1 ≤= (int)s.size() prehensivo s[i + d + 1] != s[i]) devuelve falso;
distancia[i] - 'a'] = -1; // procesada
}
retorno verdadero;
}
`` `

■ **Elige el estilo que se siente más natural para ti. #
■ *Track‐First* es ideal para entrevistas que valoren **explicit state tracking**.
*Check‐Second* demuestra **optimised one‐pass logic** y una comprensión más profunda de los índices de array.

-...

## 4VIEW⃣ Complexity Analysis

TEN ANTERI ANTERIOR ANTERIOR ANTERIOR QUÉ
Silencio----------------------------------------
TENIDO Tiempo TENIDO `O(n)` – un escaneo, búsquedas de mapas de tiempo constante Silencio `O(n)` – un escaneo, acceso constante a los arrays
TENIDO EL ESPACIO TENIDO `O(26)` (Mapa de los primeros índices) – reutiliza el array de entrada Silencio

Ambos cumplen con las restricciones de LeetCode cómodamente (max `n = 52`).

-...

## 5VIEW⃣ Common Pitfalls (The Ugly)

¿Por qué no se puede arreglar la vida?
Silencio--------------------------
Silencio **Using `i - firstIndex` en lugar de 'i - firstIndex - 1`** Silencio Mis-counts the letters *between* occurrences. tención Subtract 1 para excluir los puntos finales. Silencio
Silencio **Los límites de verificación incorrectos (`i + d  observado n` en lugar de `i + d + 1  interpretado n`)** Silencio Off‐por-uno error al mirar hacia adelante. Silencio Recordar el `+1` para la propia carta. Silencio
Silencio **Asumiendo que todas las 26 letras aparecen** Silencio Ignorar la regla “ignore if absent” puede llevar a falsos positivos/negativos. Utilice un mapa o marca de entradas procesadas; ignore distancias cuando la carta nunca se ve. Silencio
*Mutating `distance` in Check‐ En segundo lugar sin una copia** ← Los efectos secundarios pueden filtrarse en código de llamadas o pruebas. ← Copiar el array primero ( < [] copiar = distancia.clone()`) o documentar explícitamente que el método lo muta. Silencio

-...

## 6down Verificación del Test-Driven

``text
Prueba 1
---
s = "abaccb"
distancia = [1,3,0,5,0,...]
Resultado: verdadero

Prueba 2
---
s = "aaa"
distancia = [1,0,0,...]
Resultado: falso

Prueba 3 (edge)
-----------
s = "zzxyyzxxzz" // 10 letras, cada dos veces
distancia = [0]*26; distancia[25] = 8; distancia[23] = 2; distancia[24] = 1
Resultado: verdadero
`` `

Ejecutar ambas implementaciones en la misma suite de pruebas garantiza que usted captura errores sutiles fuera de cada uno.

-...

SEO‐Optimized Blog Wrap‐ Arriba

*Título*
■ *Ver distancias entre las mismas letras – Java, Python, C++ Soluciones & Entrevista Consejos*

*Descripción*
■ Master LeetCode 2399 con aplicaciones Java, Python y C++. Aprender el Track‐First vs. Check‐ Segundos enfoques, complejidad y obstáculos comunes. ¡Pon tu entrevista de codificación hoy!

**Header Palabras clave**
- LeetCode 2399
- Distancias de control Entre las mismas cartas
- Algoritmos de cuerda
- Biss String Matching
- Preparación de entrevistas

**Cerrar la llamada a la acción**
■ “Si estás preparando tu próxima entrevista de ingeniería de software, practica este problema hasta que la solución sienta la segunda naturaleza. Los conceptos, mapas desh, cheques de dos puntos y seguridad fuera de uno, son reutilizables en innumerables desafíos de codificación. ”

-...

## Final Thought

*El bueno* – Un algoritmo directo y eficiente en el tiempo que convierte una regla potencialmente confusa de la “distancia” en un pase limpio y lineal.
*El malo* – La tentación de codificar índices o ignorar la regla de la “carta de consentimiento” puede tropezar incluso codificadores experimentados.
*El feo* – errores fuera por uno que rompen sutilmente las soluciones; evitelas comprobando los límites y usando el truco de `-1`.

Ahora que posees las tres implementaciones del lenguaje y entiendes el *por qué* detrás de cada línea, estás listo para golpear LeetCode 2399, impresionar entrevistadores, y aterrizar esa oferta de trabajo. 🚀

¡Feliz codificación!

-...

* Tu amistoso mentor de codificación*
■https://www.codemaster.io instrucciones
-...

**Feliz resolución, y que su código de entrevista siempre sea fuera-por-cero correcto! * *