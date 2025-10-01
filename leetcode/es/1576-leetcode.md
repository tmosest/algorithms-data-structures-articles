-...
Título: LeetCode 1576. Reemplazar todos ?'s para Evitar Personajes Repetitivos Consecutivos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recapitulación del problema – LeetCode 1576
**Título: ** *Reemplazar todo?'s para Evitar Personajes Repetitivos Consecutivos*
*Dificultad* Fácil

■ ** Objetivo** - Reemplazar cada `?` en la cuerda `s` (sólo letras minúsculas ' ). para que la cadena final tenga **no dos caracteres iguales adyacentes**.
■ Los caracteres no cuestionados no pueden ser cambiados.
■ Se garantiza que la cadena original no contenga repeticiones consecutivas excepto las posiciones `?`.
■ La respuesta siempre existe y se acepta cualquier cadena válida.

-...

## 2. Idea de alto nivel

Camina por la cuerda de izquierda a derecha.
Cuando golpeamos un `?`, escoge una carta que difiere de los caracteres **previous** y **next** (si existen).
Debido a que sólo necesitamos un reemplazo válido, es suficiente probar las tres primeras letras `a`, `b`, y `c`.
En la mayoría de ellos chocará con cualquiera de los vecinos, por lo que siempre encontraremos una elección adecuada.

Este enfoque codicioso es lineal en el tiempo y constante en el espacio extra.

-...

## 3. El Código

A continuación se presentan soluciones limpias y idiomáticas en **Java**, **Python**, y **C+**.
Los tres tienen un solo paso sobre la cuerda, tiempo O(n) y espacio O(1).

-...

### 3.1 Java

``java
// LeetCode 1576 – Reemplazar todo ?'s para Evitar Personajes Repetitivos Consecutivos
Clase Solución {
public String modifyString(String s) {
char[] chars = s.toCharArray(); // mutable view
int n = chars.length;

para (int i = 0; i)
si (chars[i] == '?) {}
char left = i 0 ? chars[i - 1] : '\0';
char right = i - 1? chars[i + 1] : '\0';

// probar a, b, c – el primero que no choca
para (carta c = 'a'; c
si (c != izquierda " c != derecha) {
chars[i] = c;
ruptura;
}
}
}
}
volver nuevo String(chars);
}
}
`` `

-...

#### 3.2 Python 3

``python
# LeetCode 1576 – Reemplazar todo ?'s para Evitar Personajes Repetitivos Consecutivos
Solución de clase:
def modifyString(self, s: str) - Propiedad str:
chars = list(s)
n = len(chars)

para i en rango(n):
si chars[i] == '?
izquierda = chars[i - 1] si Ninguno
derecha = chars[i + 1] si yo < n - 1 otra Ninguno

para c en 'abc':
si c!= izquierda y c!= Bien.
chars[i] = c
descanso
volver ''.join(chars)
`` `

-...

### 3.3 C++

``cpp
// LeetCode 1576 – Reemplazar todo ?'s para Evitar Personajes Repetitivos Consecutivos
Clase Solución {
public:
string modifyString(string s) {
int n = s.size();
para (int i = 0; i) {}
si (s[i] == '?) {}
char left = (i 0) ? s[i - 1] : '\0';
char right = (i ecto n - 1)? s[i + 1] : '\0';

para (carta c = 'a'; c
si (c != izquierda " c != derecha) {
s[i] = c;
ruptura;
}
}
}
}
retorno s;
}
};
`` `

Los tres snippets compilan en el entorno oficial LeetCode y se ejecutan en 1 ms para el tamaño máximo de entrada (`n <= 100`).

-...

## 4. Por qué esto funciona – Una cueva más profunda

#### 4.1 Validez Greedy
En la posición `i` conocemos al vecino izquierdo (`s[i-1]`) porque ya hemos reemplazado a cualquier anterior ``.
El vecino adecuado (`s[i+1]`) es una carta original o una ``? que reemplazaremos más tarde.
Elegir una carta que es distinta de **ambos** vecinos garantiza que, después de este paso, la subestring `[i-1.i]` ya es válida.
Debido a que procesamos de izquierda a derecha, las decisiones futuras no pueden invalidarla: el único carácter que podría igualar `s[i]` más adelante es `s[i+1]`, pero explícitamente lo evitamos.

Así, por inducción, toda la cadena permanece válida.

### 4.2 Por qué tres cartas son suficientes
Si los vecinos de izquierda y derecha son diferentes, en la mayoría de dos cartas están prohibidas ( " a " y " b " ).
Si son iguales, sólo una carta está prohibida.
Por lo tanto, al menos uno de `{a, b, c}` funcionará.
No hay necesidad de escanear todo el alfabeto.

-...

## 5. Casos de borde " Pruebas "

TENCIÓN ANTERIOR esperada salida ANTERIOR Silencio
Silencio...
¿"Vida"?"" Silencioso "ab" (o cualquier variación) TENIDO Dos consecutivos '? '; podemos elegir 'a' entonces 'b`. Silencio
¿No puede ser "a" (izquierda) o "c" (derecha). Silencio
TENIDO `'a?b?c" TENIDO `"acbcb" TENIDO Reemplazos alternativos. Silencio
¿Por qué? ¿Por qué no? Silencio
La cadena permanece inalterada. Silencio

La implementación maneja cadenas de longitud 1 y aquellas que terminan/están con `?` agraciadamente porque el vecino verifica el uso de valores centinela.

-...

## 6. Complejidad del tiempo y el espacio

← Algorithm Silencio Silencio
Silencio----------------
Silencio Greedy scan Silencio **O(n)** Silencio **O(1)** (conversión en el lugar)

Con `n 0 = 100', esto es trivial, pero la solución escala a cadenas muy largas sin modificación.

-...

## 7. Lo que hace que este problema sea “bueno, malo, ugly”

## 7.1 Bien - Las fortalezas del problema
- **Claridad** – Las limitaciones son simples: letras minúsculas + `?`.
*Determinista* – Siempre hay una solución; solo necesitamos encontrarla.
- ¿Qué? La estrategia avaricia funciona para cualquier longitud de cuerda.
- ** Buenas Prácticas** - Demostrar el manejo de vecinos, valores centinelas y edición en el lugar.

## 7.2 Bad – Potential Pitfalls
- **Misreading Constraints** – Olvidando que la cadena original nunca contiene duplicados adyacentes.
- **Off‐by-One Errores** – Índices de vecinos equivocados (especialmente en extremos).
- ** Complejidad innecesaria** – Algunos pueden over-engineer con bucles de alfabeto completo o regex.

## 7.3 Ugly – Common “Ugly” Code Patterns
- Replacing `?` escaneando el alfabeto cada vez (`para c en 'abcdefghijklmnopqrstuvwxyz'').
- Usando cadenas o listas adicionales para rastrear a los vecinos (recuerdo sabroso O(n)).
- Loops anidados que revisitan el mismo personaje varias veces.

La solución limpia anterior evita todos estos obstáculos centrándose en la propiedad esencial: **Sólo se requieren tres letras**.

-...

## 8. Enfoques alternativos (Bonus)

Silencio Silencio Silencio Pros
Silencio...
Silencio ** Programación Dinámica** – rastrea el carácter anterior y prueba todas las posibilidades. tención Maneja variantes más complejas. ← Sobrematar para este simple problema; O(n·26) tiempo. Silencio
Silencio **Volver arriba** – probar cada letra para cada `?` hasta el éxito. Silencio Funciona para cualquier variante. Tiempo exponencial para grandes cuerdas. Silencio
Silencio ** Reemplazo deRegex** – `s.replaceAll("\?"",a")` luego post-proceso. tención Rápido para pequeñas cuerdas. ← No es eficiente y difícil de garantizar la corrección. Silencio

Sigue el método codicioso para LeetCode 1576.

-...

## 9. Cómo esto te ayuda a conseguir un trabajo

**Showcase**: La solución demuestra su capacidad de leer limitaciones, oportunidades de optimización de puntos e implementar un algoritmo O(n).
- **Interview Readiness**: Muchos gerentes de contratación hacen preguntas similares “reemplazar – el propietario”. Su código es corto, legible y cubre los casos de borde.
- Portafolio. Incluya la implementación de tres idiomas en GitHub con comentarios y un README que explica la lógica.
- **SEO‐Friendly Portfolio**: Añadir etiquetas como *Leetcode 1576*, *Replace All ?'s*, *Evitar Personajes de Repetición Consecutiva*, *Java/Python/C++ Pregunta de entrevista*, *previsión de entrevistas de codificación*, * algoritmo fácil*.

-...

## 10. Wrap‐Up

- *Key Insight* – En cada uno de los `?`, sólo evite a los dos vecinos; `a`, `b`, o `c` siempre funcionará.
- **Complejidad** – O(n) tiempo, O(1) espacio extra.
- **Robustness** - Maneja todos los casos de borde, incluyendo cadenas que comienzan o terminan con '?'.
- **Job‐Ready** – Código limpio y conciso en tres idiomas populares, perfecto para tu kit de herramientas de entrevista técnica.

¡Feliz codificación, y buena suerte haciendo su próxima entrevista! 🚀