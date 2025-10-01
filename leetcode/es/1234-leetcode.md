-...
Título: LeetCode 1234. Sustitúyase el Subestring for Balanced String -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recaptación de problemas

■ **Reemplazar el Subestring for Balanced String* *
■ Se le da una cadena de longitud `n` que contiene sólo los cuatro caracteres `Q`, `W`, `E`, `R`.
■ Una cadena es *equilibrada* si cada personaje aparece exactamente `n / 4` veces.
■ En una operación puede reemplazar ** cualquier subestring contiguo** de `s` con otra cadena de la misma longitud (la nueva cadena puede ser elegida arbitrariamente).
■ Regrese la longitud **minimo** de la subestring que necesita reemplazar para hacer `s` balanceado.
■ Si `s` ya está equilibrada, vuelva `0`.

■ *Constraints*
* `4 ≤ n ≤ 105`
* `n ' is a multiple of `4`
* `s` only contains `Q`, `W`, `E`, `R`

La solución clásica utiliza una técnica **sliding ventana** (dos puntos).

-...

## 2. Algoritmo – Ventana deslizante

1. **Conta la frecuencia** de cada personaje en toda la cuerda.
2. Compute `required = n / 4`.
Para cada personaje `c` sólo necesitamos *neced* `freq[c] - requerido` de ellos en el substring que reemplazaremos - si el valor es ≤ 0 el personaje ya está equilibrado o subrepresentado y no necesitamos “remove” ninguna de ellas.
3. Si cada `freq[c] == requerido`, la cuerda ya está equilibrada → retorno `0`.
4. Inicia una ventana `[l, r)` (inclusive a la izquierda, exclusiva a la derecha).
Mueva el extremo derecho un paso a la vez, *dedicando* el mostrador “necesario” para el personaje que entra en la ventana.
5. Mientras que la ventana ya contiene *al menos* el número necesario de cada personaje sobrerepresentado, trate de reducirlo de la izquierda (incremento `l` y *incremento* el contador para ese personaje).
Actualizar la respuesta con la longitud de ventana actual cada vez que la ventana es “buena”.
6. La ventana más pequeña encontrada es la respuesta.

■ **Por qué funciona* *
■ La ventana representa una subestring candidata que reemplazaremos.
■ Cuando la ventana contiene todos los caracteres de “exceso”, el resto de la cadena ya tiene el recuento adecuado, por lo que reemplazar la ventana puede fijar toda la cadena.
■ Al deslizar la ventana con codicia y encogerla siempre que sea posible garantizamos que probamos las subestrings más pequeñas posibles.

### Complexity

Silencio Silencio Silencio Silencio
Silencio----------------
Silenciosos contando frecuencias Silencio
Silencioso ventana Silencio

En general: **`O(n)` tiempo, `O(1)` espacio auxiliar**.

-...

## 3. Implementaciones de referencia

A continuación se presentan implementaciones limpias y bien agregadas en **Java**, **Python**, y **C+**.
Cada uno contiene un pequeño ayudante " de mantenimiento " , que se puede utilizar para las pruebas locales.

-...

### 3.1 Java

``java
importar java.util*;

Solución de la clase pública {}
// carácter de mapa al índice 0..3
int privado idx(char c) {}
c) {
caso 'Q' - título 0;
caso 'W' - título 1;
caso 'E' - título 2;
default - título 3; // 'R'
};
}

intento público equilibrado String(String s) {
int n = s.length();
int required = n / 4;

// 1) frecuencias totales
int[] freq = nuevo int[4];
para (int i = 0; i)
freq[idx(s.charAt(i))]++;
}

// 2) calcular cuántos de cada char que necesitamos eliminar
int[] need = new int[4];
booleano equilibrado = verdadero;
para (int i = 0; i)
si (freq[i]
necesidad[i] = freq[i] - requerida;
balanceado = falso;
}
}
si (balanceado) retorno 0; // ya equilibrado

// 3) ventana corredera
int left = 0, best = n;
para (derecho = 0; derecho) {}
int id = idx(s.charAt(right));
necesidad[id]--; // char entra ventana

// encogimiento mientras que la ventana contiene suficiente de cada char excesivamente representado
(todas las personas no positivas (necesitas)) {}
mejor = Math.min (mejor, derecha - izquierda + 1);
necesidad[idx(s.charAt(left))]++; // char leaves window
izquierda++;
}
}
devolver mejor;
}

booleano privado allNoPositive(int[] a) {
para (int v : a) si (v  título 0) devuelve falso;
retorno verdadero;
}

// ----- para las pruebas locales ---
public static void main(String[] args) {
Solución sol = nueva solución ();
System.out.println(sol.balancedString("QWER")); // 0
System.out.println(sol.balancedString("QQWE"); // 1
System.out.println(sol.balancedString("QQQW")); // 2
}
}
`` `

-...

#### 3.2 Python

``python
importadores

Solución de clase:
def balanceado String(self, s: str) - Propiedad int:
n = len(s)
req = n // 4

# Contando frecuencias
freq = {c: 0 para c en 'QWER'}
por ch en s:
freq[ch] += 1

# Cuantas de cada char deben ser removidas de la ventana
necesidad = {c: max(0, freq[c] - req) for c in 'QWER'}
if all(v == 0 for v in need.values()):
retorno 0

# ventana corredera
izquierda = 0
mejor = n
por derecho, ch in enumerate(s):
necesidad[ch] -= 1 # char entra ventana

mientras que todos (v <= 0 para v en necesidad.values()):
mejor = min (mejor, derecha - izquierda + 1)
necesidad[izquierda] += # char leaves window
izquierda += 1

mejor


Pruebas locales...
si __name_ == "__main__":
sol = Solución()
print(sol.balancedString("QWER") # 0
print(sol.balancedString("QWE") # 1
print(sol.balancedString("QQW") # 2
`` `

-...

### 3.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
Intento equilibrado String(string s) {
int n = s.size();
int req = n / 4;
array obtenidos, 4 caracteres = {0, 0, 0, 0};
auto id = [](char c) {
c) {
caso 'Q': retorno 0;
caso 'W': retorno 1;
caso E: retorno 2;
por defecto : retorno 3; // 'R'
}
};

for (char c : s) cnt[id(c)]++;

array 4 necesidad;
bool balanceado = verdadero;
para (int i = 0; i) {}
si
necesidad[i] = cnt[i] - req
balanceado = falso;
[i] = 0;
}
si (equilibrado) retorno 0;

int left = 0, best = n;
para (derecho = 0; derecho)
necesidad[id(s[right])]--; // ventana se expande

(all_of(neced.begin(), need.end(),
[](int v){ return vs= 0; }) {
mejor = min (mejor, derecha - izquierda + 1);
necesidad[id(s[left])]++;/
++izquierda;
}
}
devolver mejor;
}
};

// ----- pruebas locales ---
int main() {}
Sol de solución;
cout se hizo sol.balancedString("QWER")
cout se hizo sol.balancedString("QWE")
cout se realizó el sol.balancedString("QQQW")
retorno 0;
}
`` `

-...

## 4. Artículo del Blog – *El Bien, el Mal, y el Ugly de “Reemplazar el Subestring for Balanced String”*

*Publicado 2025‐09‐26 Silencio Etiquetas: #LeetCode #CodingEntrevista #Algorithms #SlidingWindow #JobSearch*

-...

### 4.1 Por qué este problema importa para los reclutadores

Programador de amor LeetCode problemas que prueba **data‐structure mastery + inteligente algoritmo diseño**.
Este problema se encuentra en el cubo *media*, pero su solución requiere:

1. **Observando la sobrerepresentación** – un pequeño truco lógico que muestra que puedes pensar *más allá* el obvio “cuenta cada personaje”.
2. **Ventana deslizante** – una técnica clásica de dos puntos que aparece en muchas entrevistas (subestrings de palindrome, dos series de 2-d suma, etc.).
3. **Movimiento por caso directo** – la cadena ya puede ser equilibrada, o la ventana puede necesitar reducirse varias veces. Una implementación limpia evita errores sutiles.

Si puedes explicar este problema en 5–10 minutos y escribir a mano el algoritmo en una sola dirección, ya estás a mitad de camino a la categoría de candidato de nivel superior*.

-...

### 4.2 The **Good** – Simple pero poderoso

No hay bucles anidados, sólo escaneo lineal.
- **O(1) space** – sólo 4 contadores, incluso para 100 000 caracteres.
- **Tecnica reutilizable** – el esqueleto de ventana corredera se puede adaptar para *cualquier problema* que pide un segmento contiguo con una propiedad dada.

Usted puede mostrar esto en su cartera o en una pizarra:

`` `
Conteo √≥ requerido - exceso de confianza
Ventana contiene todo el exceso - sustitución de la ventana
`` `

Es un gran ejemplo de ** “reducir el problema”**: de “encontrar una subestring” a “encontrar una subestring que contiene todo el exceso”.
Los reclutas preguntarán: *“¿Por qué restamos ‘requerido’?”* y puedes decir inmediatamente: *“Porque sólo necesitamos eliminar el excedente, el resto de la cadena permanece intacto.”*

-...

### 4.3 The **Bad** – Common pitfalls

Silencio Pitfall Silencio Cómo evitarlo
Silencio...
Silencio **Cálculo incorrecto de la necesidad** (sutracting when you should add) Silencio
Silencio **Asumiendo que la ventana debe crecer antes de encoger** Silencio Mantener el cheque de la “buena” ** después de la ampliación de la ventana; sólo entonces intentar reducir. Silencio
Silencio **Missing the already balanced case** Silencio Un rápido `if all(freq[i] == req)` guard saves 0‐time edge cases. Silencio
Silencio **Usando un mapa en Java/Python** (O(1) vs O(4)) Silencio Prefer arrays (`int[4]`) para la velocidad; los mapas dan legibilidad pero una ligera sobrecarga. Silencio

Destacando estos obstáculos durante una entrevista muestra que *sabe cómo depurar* y puede pensar defensivamente en casos de borde – una habilidad muy apreciada.

-...

### 4.4 The **Ugly** – Why people struggle

1. **Misreading “reemplace any substring”** – Algunos candidatos piensan que debe eliminar todos los caracteres sobrantes, sin darse cuenta también puede *insertar* nuevos en el reemplazo.
2. ** Ampliación de la ventana optimista* Dejan que el puntero derecho se mueva hasta el final antes de reducirse, causando `O(n2)' en la práctica debido a cheques repetidos.
3. ** Obsesión de complejidad** – Tratando de evitar cheques “todos los positivos” de dos puntos y en lugar de utilizar una cola de prioridad o árbol de segmento – un *horrendous over-engineering* de una simple solución O(n).

Un candidato superior reconocerá que la solución *superada* es sólo **en términos generales**. Ellos dirán: “No hay necesidad de un montón; sólo un pase de dos puntos. ”

-...

### 4.5 Quick interview tramp‐sheet

TEN TERRITOR ANTERIOR Código snippet
...------------------------------
Silencio Cuenta las frecuencias ← para ch en s: freq[ch] += 1` Silencio Un pase, O(n). Silencio
Silencio Excess array Silencio `neced[ch] = max(0, freq[ch] - req)` Silencio Sólo eliminar lo que realmente necesita. Silencio
TENIDO VENTA ANTERITORIO ANTERITORIO 1` Silencio Los valores negativos significan “la ventana ya tiene suficiente de este char”. Silencio
Silencio Prueba de bondad TENIDO `mientras todo(v <= 0 para v en necesidad)` TENIDO `O(1)` cheque por iteración. Silencio
TENIDO TERRITORIO TENIDO `necesidad[left_char] += 1; izquierda+` Silencio Mover a la izquierda sólo cuando la ventana es buena. Silencio

Recuerde: la longitud de la ventana **bebidas** sólo cuando * todo* carácter sobrerepresentado ya está satisfecho.

-...

### 4.6 Cómo hablar de esto en una entrevista

1. **Declara el problema en inglés claro** – asegúrate de que el entrevistador sepa que entiendes la operación de reemplazo.
2. **Explicar la observación** – “¿Por qué nos importa “freq[c] – req`?”
→ Esto te muestra que la cadena ya tiene la cantidad correcta de caracteres *bajo representado*.
3. **Coge la ventana de deslizamiento** – dibuja un simple diagrama en la pizarra.
*Agrega puntero derecho, saca puntero izquierdo, encoge mientras que bueno*.
4. **Edge-case check** – señala la respuesta `0` para cadenas ya equilibradas.
5. **La complejidad** – mencionar el tiempo y la memoria constante de `O(n)`, y opcionalmente comentar sobre por qué esto golpea una ingenua búsqueda de subestring `O(n2)`.

Si terminas con un *clean, snippet de código ejecutable*, habrás convencido al entrevistador de que puedes escribir ** código correcto, eficiente y listo para la producción**.

-...

### 4.7 Palabras finales

El problema ** "Reemplazar el Subestring for Balanced String"** es un *gateway* a temas más avanzados (resumiendo sumas prefijos, mapas de frecuencia, colas monotonales).

- **Bueno** – Un clásico ejercicio de ventanilla deslizante que demuestra el pensamiento lineal.
- **Bad** – A menudo tropezado por aquellos que olvidan restar la cantidad requerida primero.
- **Ugly** – Las soluciones “sobre-ingenieradas” que explotan la memoria o el tiempo añadiendo estructuras de datos innecesarias.

Si usted asea este problema, usted está demostrando que puede ver patrones, diseñar algoritmos eficientes, y escribir código limpio - exactamente lo que los reclutadores están buscando.

¡Feliz codificación y buena suerte con tu próxima entrevista! 🚀

-...

### 5. Cómo utilizar este artículo para obtener su resumen

- **Agregar una sección** titulada “Problema de LeetCode resuelto” y enumerar este problema con un enlace a su solución.
- **Utilice los puntos de bala** del párrafo “Por qué importa este problema” como puntos de conversación en su preparación de entrevista.
- **Compartir el código snippets** en su GitHub README (por ejemplo, `BalancedString.java`) – los reclutadores a menudo esquiman sus repositorios para código limpio.

-...

### 6. Lista de verificación para el retiro

- [ ] Comprender el truco **exceso-representación**.
- [ ] Domine la plantilla **Sliding ventana**.
- [ ] Sea capaz de escribir la solución en **Java/Python/C+** en 5 minutos.
- [ ] Preparar una explicación oral de 5 minutos que cubre el *why* y *how*.
- [ ] Agregue la implementación a su cartera para una revisión rápida del reclutador.

¡Feliz entrevista!

-...

### 7. Referencias

1. [LeetCode 1694 – Reemplazar la Subestring for Balanced String](https://leetcode.com/problems/replace-the-substring-for-balanced-string/)
2. *Two‐Pointer (Sliding Window) Pattern*, CS 101 textbook
3. *HackerRank – “Frequency Counter” patrón*

-...

### 8. SEO " Job‐Search Hooks

- Palabrasclave: " cadena balanceada " , " sustitución subestring " , `LeetCode medium " , " entrevista de codificación " , " algoritmos de entrevista de trabajo " .
- Meta descripción: *Aprenda la solución O(n) más rápida a LeetCode 1694 – Reemplazar el Subestring for Balanced String, con código de referencia en Java, Python y C++. Maestro la técnica de la ventana deslizante para impresionar a los reclutadores. *

-...

**End of article. #