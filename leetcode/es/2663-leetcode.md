-...
Título: LeetCode 2663. Lexicographically Smallest Beautiful String -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 2663 – Lexicográficamente Más pequeña hermosa cuerda
## Un problema de LeetCode “Hard” resuelto en Java, Python y C++
■ **TL;DR**
• Greedy – escaneo de derecha a izquierda, golpea un personaje, luego reconstruye el sufijo con las letras legales más pequeñas.
• Complejidad: **O(n)** tiempo, **O(1)** espacio extra (aparte de la cadena de salida).
* Funciona para *n* hasta **100 000** y *k* de 4 a 26.

-...

## Problema Recap

* Se le da un **bello** cuerda `s` de longitud `n` (`1 ≤ n ≤ 10^5`).
* Una cuerda es hermosa * si
1. Cada carácter figura en las primeras letras " k " del alfabeto ( " a ... a+k-1 " ).
2. Ninguna subestring de longitud ≥ 2 es un palindromo.
* Encuentra el más pequeño **léxicográficomente** hermosa cuerda que es **strictamente más grande** que `s`.
* Si no existe tal cuerda, devuelve una cuerda vacía.

-...

Intuición: Greedy Idea

Piensa en la cuerda como un “bloqueo” que queremos abrir al siguiente estado válido.

1. #Move right‐to‐left**:
Partiendo de la última posición, trate de aumentar ese personaje.
*¿Por qué derecho a izquierda? *
Debido a que el sufijo que viene después de la posición cambiada debe ser reconstruido a los caracteres más pequeños posibles; no podemos darnos el lujo de aumentar un personaje más lejos izquierda si existe un incremento lexicográfico más pequeño a la derecha.

2. *Amucho legal*
Incremento `s[i]` hasta que se convierta en una letra ≤ `'a'+k-1`.
Después de cada aumento debemos comprobar que el nuevo personaje hace **no** igual
* `s[i-1]` (no dos chars iguales consecutivos) y
* `s[i-2]` (previene un palindrome de 3 longitudes).

Si ambos cheques pasan hemos encontrado la posición más izquierda donde podemos golpear la cuerda.
Si `s[i]` alcanza `'a'+k-1` y todavía falla los cheques, movemos un paso a la izquierda (`i-`) y repetir.

3. *Reconstruye el sufijo*
Una vez que tengamos un prefijo válido `s[0...i]`, el sufijo `s[i+1...n-1]` debe ser la terminación más pequeña **léxicográficamente** hermosa.
Por cada posición " j " después de " escogemos la letra más pequeña del conjunto `{a, b, ..., a+k-1} " que es diferente de `s[j-1] " y `s[j-2] " .
Debido a que siempre estamos escogiendo la carta más pequeña posible, toda la cuerda será la más pequeña lexicográficamente entre todas las cuerdas que son más grandes que el original.

4. **No hay solución**
Si caminamos fuera del extremo izquierdo ( " i " 0 " ) significa que no podemos encontrar ningún incremento legal, así que regresen " .

-...

## Correctness Proof (Sketch)

Demostramos que el algoritmo devuelve la cadena deseada o reporta correctamente que no existe.

1. **Existencia de un aumento**
Si existe una cuerda hermosa más grande, debe haber una posición 'i' tal que
* `s[i]
* aumentar `s[i]` por lo menos 1 mantiene la cuerda hermosa.
El algoritmo examina todas las posiciones de derecha a izquierda y se detiene en el primero donde es posible un aumento. Así, si existe una solución, el algoritmo encontrará un 'i' válido.

2. **Minicidad lexicográfica del prefijo**
El algoritmo nunca cambia ningún personaje dejado de `i`. Cualquier otra solución que cambie un personaje dejado de 'i' sería lexicográficamente mayor porque la posición anterior cambia a una carta superior.

3. **Minicidad lexicográfica del sufijo**
Después de que el prefijo se fija, cada posición `j  título i` se fija en la letra más pequeña que mantiene la belleza con sus dos predecesores.
Cualquier otra opción en la posición `j` que es más grande haría que toda la cadena lexicográficamente más grande, y elegir una carta más pequeña rompería el límite de belleza.
Así el sufijo construido es el más pequeño posible.

Combinando 1‐3, el algoritmo devuelve la cuerda más pequeña que es estrictamente más grande que `s`. Si no existe tal ``, no se puede formar una cuerda hermosa más grande, por lo que la respuesta es ''. ∎

-...

## Edge Cases " Pitfalls

Escenario Silencioso Por qué importa Silencio Cómo lo maneja el algoritmo
Silencio--------------------------
Silencio **k = 4** (minimal allowed) Silencio Sólo letras `a‐d` existen → las limitaciones de palindromo son más estrictas. La reconstrucción del sufijo utiliza el conjunto completo `{a,b,c,d}`. Silencio
Silencio **s ya utiliza las letras más grandes** Silencio No se puede aumentar la posición. El bucle decrementará `i` pasado el extremo izquierdo → retorno `"". Silencio
Silencio ** Longitud de la cuerda = 1** Silencioso Palindrome check trivial. El algoritmo todavía funciona; no existen índices `i-1` o `i-2`. Silencio
Silencio **k = 26** Silencio Todas las letras alfabéticas permitidas. La lógica sigue siendo idéntica; el sufijo puede usar cualquiera de 26 letras. Silencio
Silencio Muy larga cuerda (10^5)** Silencio Necesita tiempo lineal. Silencio Cada personaje es examinado al máximo dos veces (una vez en la fase de choque, una vez en el edificio del sufijo). Silencio

-...

# Código #

A continuación se presentan implementaciones limpias y bien agregadas en **Java**, **Python**, y **C+**.
Todas las soluciones siguen la misma estrategia avaricia descrita anteriormente.

### 1. Java

``java
importar java.util*;

Solución de la clase pública {}
publico más pequeño BeautifulString(String s, int k) {
char[] ch = s.toCharArray();
int n = ch.length;
int i = n - 1;

// ----- encontrar posición para chocar ---
mientras (i 0) {
ch[i]+; // probar la siguiente carta
si (ch[i] - 'a' == k) { // pasó por el rango permitido
i...
continuar;
}
si ((i - 1 < 0 Silencioso ch[i] != ch[i - 1]) "
(i - 2 ■ 0 TENIDO TENIDO NUESTROS EN VIRTUD [i] ch[i - 2]) {
rotura; // golpe válido encontrado
}
}

si (i < 0) volver "; // no mayor hermosa cadena

// ----- reconstruir el sufijo con letras más pequeñas posibles ---
para (int j = i + 1; j)
// elegir la carta más pequeña que no coincida
// el anterior o el dos pasos atrás
para (int x = 0; x < k; x++) {}
char cand = (char) ('a' + x);
si (j - 1 ≤= 0 " sensibles == ch[j - 1]) continúan;
si (j - 2 ≤= 0 " sensible == ch[j - 2]) continúan;
ch[j] = cand;
ruptura;
}
}
volver nuevo String(ch);
}
}
`` `

### 2. Pitón

``python
Solución de clase:
def smallestBeautifulString(self, s: str, k: int) - confiar str:
chars = list(s)
n = len(chars)
i = n - 1

# encontrar la posición más correcta podemos aumentar
mientras que yo 0:
Prueba la siguiente carta
chars[i] = chr(ord(chars[i]) + 1)
si chars[i] > chr(ord('a') + k - 1):
I -= 1
continuar

# Check beauty
si (i - 1 < 0 or chars[i] != chars[i - 1]) and \
(i - 2 0 o chars[i] != chars[i - 2]
descanso
si lo hice 0:
"Regresa"

# Reconstruir sufijo con letras legales más pequeñas
para j en rango(i + 1, n):
para x en rango(k):
cand = chr(ord('a') + x)
si j - 1 >= 0 y cand == chars[j - 1]
continuar
si j - 2 >= 0 y cand == chars[j - 2]
continuar
chars[j] = cand
descanso

volver ".join(chars)
`` `

### 3. C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
hilo más pequeñoBeautifulString(string s, int k) {
vector asignado ch(s.begin(), s.end());
int n = ch.size();
int i = n - 1;

// encontrar la posición más correcta que se puede aumentar
mientras (i 0) {
ch[i]+; // probar la siguiente carta
si (ch[i] не char('a' + k - 1)) { // fuera de rango
i...
continuar;
}
si ((i - 1 < 0 Silencioso ch[i] != ch[i - 1]) "
(i - 2 ■ 0 TENIDO TENIDO NUESTROS EN VIRTUD [i] ch[i - 2]) {
rotura; // golpe válido
}
}

si (i < 0) devolver "; // no solución

// Reconstruir sufijo con letras más pequeñas posibles
para (int j = i + 1; j)
para (int x = 0; x < k; ++x) {
char cand = char('a' + x);
si (j - 1 ≤= 0 " sensibles == ch[j - 1]) continúan;
si (j - 2 ≤= 0 " sensible == ch[j - 2]) continúan;
ch[j] = cand;
ruptura;
}
}
cadena de retorno(ch.begin(), cap.end());
}
};
`` `

Los tres códigos se ejecutan en **tiempo lineal** (`O(n)`) y utilizan sólo algunas variables auxiliares.

-...

## Test Your Solution

``text
Entrada: s = "abcd", k = 4 → "abdc"
Entrada: s = "abdc", k = 4 → "abcd" (sin cadena más grande)
Entrada: s = "a", k = 4 → "b"
Entrada: s = "zzz", k = 26 → ""
`` `

Siéntete libre de pegar los snippets en el editor en línea de LeetCode y ejecutar las pruebas de unidad.

-...

## ¿Qué pasa si falla? – Errores comunes

← Infierno en la vida
Silencio...
Silencio Utilizando `for (char c : s)` en Java sin copiar → modifica la cadena original ← Los aumentos posteriores corrompen la entrada ← Copia en un nuevo array (`char[] = s.toCharArray()`) Silencio
tención Off‐by‐one en `chars[i] ⇩ 'a'+k-1` Silencio Puede intentar aumentar más allá de `'a'+k-1` Silencio Compare el punto *código* (`conejo`) en lugar de `=`
Silencio Rebuilding suffix with only `{a,b,c}` when `k confía3` ← Respuesta incorrecta para `k=26` Silencio Iterate `x ' (full alphabet) ←
Ignorando " i-2 " , cuando `j ' se hizo 2 ' , en caso de comprobación de palindrome incorrecta por sufijo corto, con " si (j - 2 " = 0 " , Silencio

-...

## Time & Space Complexity

TENCIÓN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio.
Silencio Java Silencio **O(n)** Silencio **O(1)** (incluido la cadena de salida)
TENIDO Python TENIDO **O(n)** ANTERIOR **O(1)**
Silencio C++ Silencio **O(n)** Silencio **O(1)**

El algoritmo nunca necesita una cola de prioridad o clasificación – simplemente intentamos la siguiente carta y realizamos cheques de tiempo constante.

-...

## ¿Por qué este problema es una “Job‐Entreview Goldmine”

1. ** Limitaciones extremas** – El límite `n ≤ 100 000` le obliga a pensar en soluciones lineales a tiempo.
2. ** Gran prueba** – Los entrevistadores aman pruebas concisas que justifican un enfoque codicioso.
3. **Manipulación de cuerdas + lógica de palindromo** – Una agradable mezcla de estructuras de datos e información algorítmica.
4. *Variantes* – El mismo patrón aparece en problemas acerca de la “permutación lexicográfica siguiente” o “contraseña válida siguiente”, por lo que el dominio le da una herramienta reutilizable para futuras preguntas.

Mostrando esta solución en una cartera (Java, Python, C++) demuestra:

* Competencia con múltiples idiomas.
* Capacidad para escribir código limpio y listo para la producción.
* Fuerte comprensión de algoritmos codiciosos y pruebas de corrección.

-...

## SEO‐Friendly Summary

- **Lexicográficamente más pequeña hermosa cuerda** - La palabra clave principal para la que quieres clasificar.
- LeetCode 2663** – Etiquetas directas el número de problema para los motores de búsqueda.
- ** Solución Java/Python/C+** – Da a los entrevistadores referencia inmediata específica del idioma.
- **Job entrevista codificación** – Destaca el valor del mundo real de este truco algorítmico.
- **Terre sin condromo** – Añade profundidad para consultas de algoritmos avanzadas.

Utilice los fragmentos de código y explicaciones anteriores en su prep de entrevista, entradas de blog, o cartera para dar una fuerte impresión en los administradores de contratación. ¡Feliz codificación!