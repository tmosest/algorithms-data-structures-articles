-...
Título: LeetCode 420. Strong Password Checker -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 Mastering Leetcode 420 – Strong Password Checker
■ **“El bueno, el malo y el feo”** de resolver un problema de entrevista dura

-...

## TL;DR

- **Problema**: Pasos mínimos para hacer una contraseña fuerte (longitud 6-20, 1 inferior, 1 superior, 1 dígito, no 3-en-a-row).
- *La idea de la solución*
1. Contar tipos de caracteres desaparecidos.
2. Encontrar secuencias de repetición ( < il > 3 >) y observar cuántos reemplazos necesitan.
3. Treat **length** como la principal limitación:
- Si demasiado corto → las inserciones dominan.
- Si demasiado largo → las eliminaciones ayudan a reducir las repeticiones.
4. Combinar los tres cuenta de manera óptima.
- ** Resultado**: O(n) tiempo, O(1) espacio extra.

A continuación encontrará ** implementaciones completas** en **Java, Python, y C++**, seguido de un artículo **bug-ready** que explica la lógica, discute las trampas y muestra cómo clavar la entrevista.

-...

## 1. Aplicación de Java

``java
Clase Solución {
público fuerte PasswordChecker(Contraseña de contactos) {}
int n = password.length();
boolean hasLower = false, hasUpper = false, hasDigit = false;

// 1. Identificar tipos de caracteres desaparecidos
para (int i = 0; i)
char c = password.charAt(i);
si (Character.isLowerCase(c)) tieneLower = verdadero;
si (Character.isUpperCase(c)) tieneUpper = verdadero;
si (Character.isDigit(c)) tieneDigit = verdadero;
}
desaparecido Tipos = (haLower ? 0 : 1) + (haUpper ? 0 : 1) + (haDigit ? 0 : 1);

// 2. Encontrar secuencias de repetición y cuántos reemplazos necesitan
int replace = 0; // total de reemplazos necesarios para repeticiones
int[] len = nuevo int[n / 3 + 1]; // recuentos de repetidos mod 3 (0,1,2)
para (int i = 0, count = 1; i)
si (i + 1 < n " contraseña. charAt(i) == password.charAt(i +1) {
contar++;
. ♫ ... {
si 3) {
reemplazar += conteo / 3;
len[count % 3]++;
}
= 1;
}
}

si
// Demasiado corto – las inserciones dominan
devolver Math.max(tipos de despido, 6 - n);
} si (n <= 20) {
// Duración OK – sólo los reemplazos necesarios
devolver Math.max(tipos de despido, reemplazar);
. ♫ ... {
// Demasiado largo – las eliminaciones ayudan a reducir los reemplazos
int over = n - 20;
// Uso de borraciones en repeticiones con mod 0 primero
int del = Math.min (over, len[0]);
-= del;
-= del;
// Luego en mod 1 repite
del = Math.min(over, len[1] * 2) / 2;
-= del;
-= del * 2;
// Finalmente en mod 2 repeticiones
del = Math.min(over, len[2] * 3) / 3;
-= del;
-= del * 3;
// Después de todas las eliminaciones
volver (n - 20) + Math.max(missingTypes, reemplazar);
}
}
}
`` `

■ *Puntos clave*
* `len[0]`, `len[1], `len[2]` almacenar cuántas repeticiones dan un resto de 0, 1, 2 cuando dividido por 3.
* Eliminar un personaje de una repetición de la longitud `k` reduce el número de reemplazos requeridos por `⌊k/3⌋`.
* Eliminar sabiamente (primero aquellos con el resto 0, luego 1, luego 2) da el mayor golpe para cada eliminación.

-...

## 2. Aplicación de los pitones

``python
Solución de clase:
def strongPasswordChecker(self, password: str) - confiar int:
n = len(password)
has_lower = has_upper = has_digit = False

1. Compruebe los tipos perdidos
para ch en contraseña:
si ch.islower(): has_lower = True
elif ch.isupper(): has_upper = True
elif ch.isdigit(): has_digit = True

desaparecidos = (no has_lower) + (no has_upper) + (no has_digit)

# 2. Repeticiones de escáner
Reemplazar = 0
mod_cnt = [0, 0, 0] # cuántas repeticiones dan k%3=0,1,2
I = 0
mientras que yo no
J = i
y contraseña [j] == contraseña[i]:
j += 1
l = j) i
si l >= 3:
reemplazar += l // 3
mod_cnt[l % 3] += 1
I = j

si no se hizo 6:
máx (perdida, 6 - n)

si no se hace 20:
máx (perdida, sustitución)

# No tengo 20
más = n - 20
# Use deleciones en repeticiones óptimamente
para k en rango(3):
use = min(over, mod_cnt[k] * (k + 1))
reemplazar -= uso // (k + 1)
sobre -= uso

(n - 20) + max(missing, replace)
`` `

■ ¿Por qué la misma lógica? #
■ La versión de Python refleja el Java: contamos tipos perdidos, repeticiones de escaneo, luego ajustamos para la longitud.
■ La brevedad de Python esconde los mismos pasos algorítmicos.

-...

## 3. Aplicación C++

``cpp
Clase Solución {
public:
fuerte PasswordChecker (contraseña de inicio) {}
int n = password.size();
bool hasLower = false, hasUpper = false, hasDigit = false;

// 1. Tipos de caracteres perdidos
para (char c : contraseña) {
si (islower(c)) tieneLower = verdadero;
si (isupper(c)) hasUpper = true;
si (isdigit(c)) hasDigit = true;
}
int missing = (hasLower ? 0 : 1) + (hasUpper ? 0 : 1) + (hasDigit ? 0 : 1);

// 2. Repeticiones
int replace = 0;
int modCnt[3] = {0, 0, 0};
para (int i = 0; i) {
int j = i;
[j] == contraseña[i] ++j;
int len = j - i;
si 3) {
reemplazar += lino / 3;
modCnt[len % 3]++;
}
i = j);
}

si (n. 6) devolver max(missing, 6 - n);
si (n י= 20) devuelve máx(perder, reemplazar);

// n
int over = n - 20;
para (int k = 0; k)
int use = min(over, modCnt[k] * (k + 1));
-= uso / (k + 1);
sobre -= uso;
}
(n - 20) + max(missing, replace);
}
};
`` `

-...

## 4. Artículo del Blog – “El Bien, el Mal, y el Ugly de Leetcode 420”

■ *Keywords*: Strong Password Checker, Leetcode 420, entrevista de codificación, fuerza de contraseña, entrevista de algoritmos, entrevista de trabajo

-...

#### 📌 Introducción

Cuando los entrevistadores preguntan **“¿Cuántos pasos para hacer una contraseña fuerte?”**, no sólo están probando su comprensión de la manipulación de cuerdas sino también su capacidad de **optimizar** bajo múltiples restricciones. Leetcode 420 (“Strong Password Checker”) es notorio por ser *hard* pero *esencial* para muchos roles de ingeniería de software. A continuación se muestra una profunda inmersión en el problema, una solución O(n) robusta y problemas comunes que debe evitar.

-...

#### ## 1down⃣ El problema en una nuezquela

Requisitos para la vida
Silencio...
Ø Largo Ø 6 ≤ `len(palabra)` ≤ 20 Silencio
tención Tipos de caracteres Silencioso al menos 1 minúscula, 1 minúscula, 1 dígito
← Repetición Silencio No hay tres charcos idénticos en una fila

** Objetivo:** Devolver el número *mínimo* de **inserto**, **delete**, o **reemplaza** operaciones para satisfacer a los tres.

-...

#### 2down⃣ The Core Insight – * “Tres piezas de movimiento”*

Silencio Parte privada Lo que hace ← Cómo afecta a la respuesta
Silencio------------------------------
Silencio **Missing types** Silencio Cuenta de las categorías de char desaparecidos Silencio Cada tipo de fuerzas desaparecidas al menos una operación Silencio
Silencio **Repeats** Silencio Secuencias como `'aaa'` o `'bbbbbb'`` Silencio Cada grupo de `k` chars idénticos necesita `⌊k/3⌋` reemplazos Silencio
Silencio **Largo** Silencioso `len  ` 6` → inserciones; `len ⇩ 20` → supresiones Silencio La inserción puede resolver los tipos desaparecidos " repetidos; la eliminación reduce las repeticiones

Equilibrar estas tres partes produce los mínimos pasos totales.

-...

#### 3down⃣ La elegante solución O(n)

1. # Puede ser una vez #
- Rastrear tipos perdidos.
- Detectar secuencias de caracteres repetidos; grabar `len / 3` y `len % 3`.
2. **Caso 1 - contraseña corta ( ' Reconocida ' 6 ' )* *
- La inserción domina.
- `pasos = max(missing, 6 - len)`.
3. **Caso 2 - Longitud aceptable (`6 ≤ len ≤ 20`)* *
- Sólo los reemplazos necesarios.
- `pasos = max(missing, totalReplacements)`.
4. **Caso 3 - Larga contraseña ( < il > 20 > )**
En primer lugar para reducir la longitud.
- Utilizar eliminaciones en repeticiones donde reducen el número de reemplazos necesarios con mayor eficiencia:
* Eliminar 1 char de un grupo donde `len % 3 == 0` → reducir un reemplazo.
* Eliminar 2 chars de un grupo donde `len % 3 == 1` → reducir un reemplazo.
* Eliminar 3 chars de un grupo donde `len % 3 == 2` → reducir un reemplazo.
- Después de todas las supresiones: `pasos = supresiones + máx(miso, remplazamientos restantes)`.

La lógica anterior es **exactamente** lo que implementa el código Java/Python/C+++.

-...

#### 4down⃣ Bien – Lo que hace que esta solución sea grande

Silencio TENIDO ANTERIOR ANTERIOR
Silencio...
Silencio **Tiempo de iluminación** Silencio Uno pasa por encima de la cuerda → O(n) (n ≤ 50)
Silencio **Espacio constante** Silencio Sólo unos pocos contadores (tipos de despido, reemplazar, modCnt[3]) Silencio
Silencio **Determinista** Silencio No retroceder ni recidivar – no hay tiempo oculto-fuerzos
tención **Lógica azul** Silencio Cada caso maneja un régimen de longitud distinto, haciendo que el algoritmo sea fácil de razonar sobre tención

-...

#### 5down⃣ Mala – Mis pasos comunes para evitar

Ø ❌ ¦ Mistake Silencio
Silencio...
*Counción de reemplazos incorrectamente* Silencio `reemplazar += longitud / 3` pero olvidando restar después de las supresiones ¦ Seguir `len % 3` grupos y ajustar `reemplaza` después de cada eliminación ANTE
*Restablecer contraseñas cortas insertando* peru Perdiendo el hecho de que una inserción puede satisfacer simultáneamente un tipo faltante y romper una repetición Silencio `max(missing, 6 - len)` mangos ambos
*Ignorando el orden de las supresiones* Silencio Eliminar de una repetición de la longitud 5 antes de una longitud 4 puede desperdiciar las operaciones TENIDO Suprímase en orden de `len % 3` (0 → 1 → 2)
Silencio *Using recursion or backtracking* ← Soplamiento exponencial en las cadenas de peor de los casos.

-...

### 6 Cambios - Casos de bordes que se acercan hasta códigos inteligentes

← Edge Silencio Por qué Es Tricky
Silencio...
Silencio **Todas las repeticiones " demasiado largas** ( " aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
Silencio **Mising type but no repeats** (`"aaaaaa"`) Silencio Eliminar no ayudará; usted necesita reemplazos Silencio Garantizar `max(missing, replace)` se aplica ←
Silencio **Largo exactamente 20 pero con muchas repeticiones** Silencio La eliminación no está permitida, sólo reemplazos Silencio Reemplazar cada tercer personaje en repeticiones Silencio
TEN **Largo exactamente 6 pero todavía faltando tipos** TEN No se permiten inserciones, pero los reemplazos pueden crear tipos desaparecidos TEN Uso reemplazos que cambian el tipo de personaje TEN

-...

### 7 comentarios Cómo esto ayuda a su juego de entrevistas

- *Mostrar el pensamiento algorítmico* Estás equilibrando tres restricciones simultáneamente.
- ** Optimización de demostraciones**: Las sustituciones de Greedy muestran que puede reducir las operaciones.
- **Highlights edge‐case awareness**: Discutir casos malos/grandes muestra minuciosidad.

■ **Pro tip**: En una entrevista, comience explicando la estrategia de alto nivel antes de bucear en código. Esto indica claridad de pensamiento y mantiene al entrevistador comprometido.

-...

### 8 comentarios SE SEO Boost – Hacer que su blog sea encontrado

- **Título**: *Comprobador de contraseñas sólido – Código 420 explicado (Java, Python, C++)*
- **Meta Descripción**: *Master Leetcode 420 con soluciones paso a paso en Java, Python y C++. Aprende el algoritmo O(n), trampas comunes y consejos de entrevista. *
- **Keywords**: “Strong Password Checker”, “Leetcode 420”, “Java password strength checker”, “Python password checker solution”, “C++ Leetcode 420”, “Coding interview password”, “job interview algoritmo”.

-...

#### 9down W Wrap‐Up

Leetcode 420 puede parecer intimidante, pero con una clara estrategia codictiva se puede resolver de manera eficiente y segura. Recuerde: **balance tipos desaparecidos, repeticiones y longitud**. El código es directo – simplemente traducir la lógica en su idioma de elección.

Si usted clavó este problema, usted está listo para ** mostrar en cualquier entrevista de ingeniería de software** con confianza. ¡Feliz codificación y buena suerte aterrizando ese trabajo de sueño! 🚀

-...

*No dude en marcar este post, compartirlo en su Enlace En perfil, y dejar un comentario con cualquier otro desafío de Leetcode que te gustaría explicar. *


-...



Eso completa la respuesta **full**: código en tres idiomas y un artículo completo del blog.