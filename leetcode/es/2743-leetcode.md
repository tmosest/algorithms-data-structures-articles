-...
Título: LeetCode 2743. Cuenta Subestrings Sin Personaje Repetitivo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2743. Cuenta Subestrings Sin Personajes Repetitivos – “El Bien, el Mal y el Ugly”

■ *Problema*
■ Teniendo en cuenta una cadena de minúsculas `s` (1 ≤  vidas eternas ≤ 105), cuente todos los subestrings *especial*: los que contienen **sin carácter repetido**.

■ *Examples*
Ø • `abcd` → 10
* * * * * * → 3
Ø • `abab` → 7

■ # Objetivo #
■ Proporcionar una solución **O(n)** en **Java, Python, y C++**, un post conciso **blog** con palabras clave amigables de SEO, y un vistazo rápido a las trampas (el “bad” y “muy”) que a menudo viajan a los entrevistadores.

-...

## 🚀 Why This Problem is a Golden Interview Question

Silencio **Aspecto**
Silencio--------------...
tención **Venta deslizante** Silencioso patrón de dos puntos clásico; cada subestring candidato es inspeccionado exactamente una vez. Silencio
Silencio ** Complejidad del tiempo** Silencio O(n) es óptimo; cualquier enfoque más lento es una bandera roja. Silencio
Silencio ** Complejidad del espacio** Silencio O(1) (sólo una serie de 26 ints) – demuestra el conocimiento de los intercambios espaciales a tiempo. Silencio
Silencio **Edge Cases** Silencio Personaje único, todos los mismos personajes, patrones alternantes. Silencio

■ **Keywords**: *subestrings, ventana deslizante, dos punteros, procesamiento de cuerdas, problema de entrevista, algoritmo O(n), Java, Python, C++*

-...

## 📚 The Good: A Clean Sliding‐Window Implementation

Intuición

Ampliamos una ventana `[izquierda ... derecha]`, mientras que los caracteres dentro son únicos.
Cuando aparece un duplicado, encogemos la ventana de la izquierda hasta que el duplicado desaparece.
Todas las subestrings que terminan en `derecha' y comienzan en cualquier lugar entre `izquierda ' y `derecha ' son válidas, por lo que agregamos `(derecha - izquierda + 1) a la respuesta.

#### 2down⃣ Estructuras básicas de datos

Silencio **Idioma**
Silencio----------------------------------------...
Silencio Java, C++ confidencialidad `int[26]
Silencio Python Silencioso `list[26]

■ El array indexa el recuento de cada letra de minúscula; 26 es una constante, por lo que el espacio es **O(1)**.

Pseudocode

`` `
[26] = {0}
izquierda = 0
respuesta = 0

por derecho en 0 ... n-1:
[derecho] += 1

mientras cuenta[derecha] 1: # duplicado encontrado
recuento[s] -= 1
izquierda += 1

respuesta += derecha - izquierda + 1

respuesta
`` `

El bucle corre **once** por personaje para ambos punteros – **O(n)** tiempo.

-...

Código

A continuación se presentan soluciones idiomáticas para los tres idiomas solicitados.

### #Java #

``java
Clase Solución {
público número OfSpecialSubstrings(String s) {
int[] freq = nuevo int[26];
int left = 0, ans = 0;

para (derecho = 0; derecho) {}
freq[s.charAt(right) - 'a']+;

(freq[s.charAt(right) - 'a'] 1) {
freq[s.charAt(left) - 'a'];
izquierda++;
}

ans += derecha - izquierda + 1;
}
devolver los ans;
}
}
`` `

■ *Las complejidades*
■ *Time*: **O(n)* *
■ *Espacio*: **O(1)**

-...

### Python

``python
Solución de clase:
def numberOfSpecialSubstrings(self, s: str) - int:
[0] * 26
izquierda = 0
ans = 0

por derecho, ch in enumerate(s):
idx = ord(ch) - 97
freq[idx] += 1

mientras freq[idx] 1:
freq[ord(s[left]) - 97] -= 1
izquierda += 1

ans += derecha - izquierda + 1
Retorno
`` `

■ *Las complejidades*
■ *Time*: **O(n)* *
■ *Espacio*: **O(1)**

-...

### **C++**

``cpp
Clase Solución {
public:
número int OfSpecialSubstrings(string s) {
array madeint, 26 propiedades freq{};
int left = 0, ans = 0;

para (derecho = 0; derecho) {}
freq[s[right] - 'a']++;

(freq[s [right] - 'a'] 1) {
freq[s[left] - 'a']--
++izquierda;
}

ans += derecha - izquierda + 1;
}
devolver los ans;
}
};
`` `

■ *Las complejidades*
■ *Time*: **O(n)* *
■ *Espacio*: **O(1)**

-...

## ⋅d The Bad: Common Pitfalls

Silencio **Issue** Silencio **Por qué Fails**
Silencio--------------------------
TENIDO Utilizando `String.contains()` o regex para comprobar duplicados TEN O(n2) por cheque TENIDO Utilice el array de frecuencia de la ventana deslizante ANTE
Silencio Olvídate de reajustar `freq` cuando se encogía la ventana ¦ Duplicate todavía cuenta ¦ Decrement `freq[s[left]]` antes de mover `izquierda'
Silencio Usando `HashSet` para cada puntero derecho (re-inserting all chars) Silencio O(n2) tiempo ← Mantener un solo set y eliminar sólo el char tóxico más izquierdo

#### Ejemplo

``java
para (derecho = 0; derecho) {}
Establecer contactoCaracter confidencial visto = nuevo HashSet correspondió();
para (int i = right; i 0; i--) {
si (!seen.add(s.charAt(i)))) romper;
ans++;
}
}
`` `

■ **La complejidad**: O(n2) – inaceptable para n = 105.

-...

## 🤡 The Ugly: Edge‐ Case Traps

1. **Todos los personajes idénticos** (`aaaaa').
*Expecado*: cuenta igual de longitud de la cadena (sólo longitud-1 subestrings).
*Insecto común*: La falta de encogimiento de la ventana conduce correctamente a una enorme sobreventa.

2. ** cuerda de longitud máxima** (`n = 105`).
* Limite de memoria*: Una matriz de 2-D o lista de listas es demasiado pesada.
*Solución*: Mantenga la matriz de frecuencia de tamaño constante.

3. **Mix de maletín superior e inferior** (aunque el problema garantiza una minúscula).
*Bug*: El cálculo del índice `s[i] - 'a' se vuelve negativo.
*Check*: Validar entrada o utilizar `Character.toLowerCase`.

4. **No-ASCII input** (rare).
*Fix*: Use puntos de código Unicode o limite a `a`‐`z`.

-...

## 📈 SEO‐Optimized Summary

- **Título**: “2743 Contar Subestaciones Sin Personajes Repetitivos – O(n) Guía de Ventana Sliding (Java, Python, C++)”
- **Meta description**: “Master LeetCode 2743 con una solución de ventanilla deslizante O(n) limpia. Aprende las trampas, los casos de borde, y cómo ace problemas de entrevista de cadena en Java, Python y C++. ”
- **Palabras clave principales**: *LeetCode 2743, contar subestrings, ventana deslizante, cadena sin duplicados, algoritmo de entrevista, solución Java, solución Python, solución C+*
- **Palabras clave de segundo orden**: *dos punteros, mapa de hah, tiempo de O(n), espacio constante, casos de borde, consejos de entrevista*

-...

## 📅 Quick Study Plan (30 Minutes)

TEN TERRITORIO TERRITORIO TERRITORIO TERRITORIO TERRITORIO TERRITORIO TEN TERRITORIO TERRENO
Silencio...
Silencio 1. Lea el problema (5 min) Silencio
Silencio 2. Piense en la ventana deslizante, proyecto de pseudocódigo (5 min)
Silencio 3. Escribe código Java, prueba de ejecución (10 min)
Silencio 4. Traducir a Python & C++ (5 min)
Silencio 5. Problemas de revisión, periferias (5 min)

■ ** Resultado**: Una solución pulida y lista para entrevistas + un post de blog que puede copiar-paste en LinkedIn, Medium o un sitio personal.

-...

## 🎯 Final Takeaway

- **Bueno**: Una ventana corredera, espacio constante, matemáticas claras.
- **Bad**: Enfoques cuadráticos, mantenimiento incorrecto de ventanas.
- *Ingenuamente*: Mal manejo de casos enteros, exageración.

■ **Si puede explicar las tres columnas anteriores y pegar cualquiera de los fragmentos de código, impresionará a cualquier gerente de contratación. * *

¡Feliz codificación y buena suerte con tu próxima entrevista! 🚀