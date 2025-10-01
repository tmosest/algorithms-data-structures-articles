-...
Título: LeetCode 2575. Encontrar la Divisibilidad Array de una cuerda -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2575. Encontrar el rayo de divisibilidad de una cuerda
*Dificultad* Medium tención **Time:** O(n) Silencio **Espacio:** O(n)

-...

### ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## #

Dada una cadena decimal `palabra ' (longitud `n` hasta `105`) y un entero `m ' (`1 ≤ m ≤ 109`), devuelve una matriz `div` de longitud `n`, donde

`` `
div[i] = 1 si el entero representado por palabra [0 ... i] es divisible por m
div[i] = 0 de otro modo
`` `

Probar directamente el prefijo en un entero de 64 bits puede rebosar, por lo que debemos confiar en la aritmética modular.

-...

## Solution Idea – “Keep the Remainder”

* Procesar la cadena de izquierda a derecha.
* Mantener un resto de funcionamiento `rem` del modulo prefijo actual `m`.
* `rem = (rem * 10 + dígitos) % m `
* If `rem == El prefijo actual es divisible por `m`.
* Almacene `1` o `0` en el array de respuesta.

Debido a que `rem' se observó m` en todo momento, nunca desbordamos, incluso si el número real es astronómico grande.

-...

# Código #

A continuación se encuentran soluciones limpias y de producción para **Java**, **Python**, y **C+**.

-...

## Java

``java
Solución de la clase pública {}
int[] divisibilidad Array(Tipo de cuerda, int m) {
char[] ch = word.toCharArray();
int[] ans = nuevo int[ch.length];
largo rem = 0; // largo para evitar el desbordamiento accidental
para (int i = 0; i)
int digit = ch[i] - '0'; // faster than Character.getNumericValue()
rem = (rem * 10 + dígitos) % m; // mantener sólo el resto
ans[i] = (rem == 0) ? 1 : 0; // prefijo divisible?
}
devolver los ans;
}
}
`` `

-...

## Python 3

``python
Solución de clase:
def divisibility Array(self, word: str, m: int) - ratio[int]:
ans = []
rem = 0
para ch en palabra:
rem = (rem * 10 + int(ch) % m
ans.append(1 if rem == 0 else 0)
Retorno
`` `

-...

### C++ (C+17)

``cpp
Clase Solución {
public:
vectorialidad Array(palabra de cuerda, int m) {
vector significar uns
ans.reserve(word.size());
long rem = 0;
por (char ch : word) {
int digit = ch - '0';
rem = (rem * 10 + dígitos) % m;
ans.push_back(rem == 0 ? 1 : 0);
}
devolver los ans;
}
};
`` `

-...

## Performance

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio Java Silencio O(n) Silencio O(n)
Silencio Python Silencio O(n) Silencio O(n)
TENIDO C++ TENIDO O(n) Silencio O(n)

La única operación pesada por iteración es una multiplicación/addición modular, que es tiempo constante.

-...

## The Good, The Bad, and The Ugly

Silencio Silencio
Silencio------------Prince------
Silencio **Overflow** Silencio Usa sólo restos → safe Silencio Ninguno Silencio
Silencio **Complejidad** Silencio Tiempo lineal " la memoria "n " puede ser 100 000, todavía bien TENIDO Ninguno TENIDO
Silencio **Readability** Silencio Corto, código idiomático Silencio Requiere comprensión de aritmética modular Silencio Algunas personas pueden pensar que 'long' es demasiado caro
Silencio **Edge Cases** Silencio Handles leading ceros, `m = 1`, `m = 109` Silencio Ninguno Silencio Ninguno
Silencio **Memory Footprint** Silencio O(n) result array  durable `ans` size `n` unavoidable Silencio
Silencio **Testing** Silencio Fácil de probar prefijos para una unidad Silencio

### Why It's “Great” for Interviews

1. **Mostrar que usted entiende aritmética modular** – una trampa de entrevista común.
2. **Demonstrates O(n) efficiency** – meets the LeetCode constraints.
3. **Código simple** – menos espacio para errores, más fácil de explicar.

### Potential Pitfalls

- Olvidar cambiar después de cada multiplicación puede causar desbordamiento.
- Convertir caracteres incorrectamente (por ejemplo, `int digit = ch - 48;` está bien, pero `int digit = Character.getNumericValue(ch);` es más lento).
- Devolviendo un tipo equivocado ( " Listifique:Integer " vs `int[] ' en Java).

-...

## Tips for Turning This Into a Job‐Winning Portfolio Piece

1. **Añada una suite de prueba**
``python
def test():
sol = Solución()
afirmar sol.divisibilidadArray("998244353", 3) == [1,1,0,0,0,1,0,0]
afirmar sol.divisibilidadArray("1010", 10) == [0,1,0,1]
`` `
2. **Documentar su código** – añadir breves comentarios explicando pasos modulares.
3. **Explicar el Algoritmo en su Resumen** – “Usado aritmético modular para resolver divisibilidad de gran número en el tiempo O(n). ”
4. ** Entrevista de Mención Context** – “Aprobada esta solución para LeetCode 2575; lista para discutir casos de borde y optimización. ”

-...

## SEO‐Optimized Blog Title & Meta Descripción

*Título*
*LeetCode 2575: Divisibilidad Array – El Bien, el Mal y el Ugly (Java, Python, C++)*

**Meta Descripción:**
"Master LeetCode 2575 con soluciones Java, Python y C++. Aprenda el truco aritmético modular, el análisis del tiempo y consejos de entrevista para aterrizar su próximo trabajo".

-...

## Pensamientos finales

El patrón “Mantenga el Restante” es un elemento básico para los problemas de cadena a entero donde el número puede superar los tipos incorporados.
- *Bueno*: O(n) tiempo, sin desbordamiento, fácil de razonar.
- **Bad**: Ninguno si recuerdas cambiar cada paso.
- **Ugly**: Ninguno – la solución es elegante.

Muestra esto en tu cartera, y tendrás un fuerte punto de conversación para entrevistas técnicas. ¡Buena suerte! 🚀