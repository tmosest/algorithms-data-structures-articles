-...
Título: LeetCode 902. Números en la mayoría N Given Digit Set -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 902 - Números en la mayoría de N Given Digit Set
**Java / Python / C++ – Soluciones completas + un blog de entrevista “Good / Bad / Ugly”* *

-...

## 🎯 Problema Resumen

■ **Given** un array clasificado `digits` (cada elemento es un solo dígito `'1'...'9'') y un entero `n`,
■ **Retorno** cuántos números enteros positivos que pueden ser escritos usando sólo los dígitos en 'digits' son **≤ n**.

*Ejemplo*
`digits = ["1","3","5"], `n = 100` → **20** números: 1, 3, 5, 7, 11, 13, ..., 77.

**Constraints* *

TENIDO ANTERIOR ANTERIOR ANTERIOR
Silencio...
≥ `1 ≤ dígitos. longitud ≤ 9` Silencio
[i] es un personaje ''1'...'9'
Silencioso `1 ≤ no ≤ 109`

El problema es un problema clásico **digit‐DP / counting** que se puede resolver en *O(log n)* tiempo y *O(1)* espacio con un enfoque combinatorio simple.

-...

## 🧠 Solution Overview (la parte “buena”)

1. **Countar todos los números con menos dígitos que `n`**
Si `n` tiene 'k' dígitos, cualquier número con '1 ... k‐1 ' dígitos se puede formar de 'digits. opciones de longitud para cada lugar.
`` `
total = Governing_{i=1}^{k-1} (digits.length)^i
`` `

2. ** Números de desplazamiento con el mismo número de dígitos**
Escanear los dígitos de `n` de la más significativa a menos significativa.
Para la posición actual " i " (a partir de la izquierda):
* Cuente cuántos dígitos de `digits ' son, básicamente, menos** que `n[i] ' .
Cada dígito puede ser seguido por cualquier combinación de las posiciones restantes 'k-i-1' → añadir
A la respuesta.
* Si ** ningún dígito es igual** 'n[i]`, estamos acabados - el prefijo actual ya supera `n`.
* Si hay un dígito igual** a `n[i]`, continúe hasta la siguiente posición.

3. **Add 1 for `n` si se puede formar* *
Si nunca salimos temprano, todos los prefijos coincidían con `n`; así `n` es un número válido → añadir `1`.

El algoritmo funciona en tiempo lineal en el número de dígitos de `n` (≤ 10) y utiliza espacio extra constante.

-...

## 📚 Code – Java

``java
Clase Solución {
int public int atMostNGivenDigitSet(String[] digits, int n) {
String N = String.valueOf(n);
int k = N.length(); // número de dígitos en n
int dlen = digits.length; // número de dígitos permitidos

total largo = 0;

// 1) todos los números con menos dígitos que n
for (int len = 1; len י k; len++) {}
total += pow(dlen, len);
}

// 2) números con la misma longitud
para (int i = 0; i)
int cur = N.charAt(i) - '0';
booleano igual = falso;

para (int j = 0; j) {}
int d = digits[j].charAt(0) - '0';
si
total += pow(dlen, k - i - 1);
} si (d == cur) {
igual = verdadero;
}
}

si (!equal) { // prefijo ya supera n
(int) total de retorno;
}
}

// 3) En sí mismo es válido
retorno (int) (total + 1);
}

// poder entero rápido para pequeños exponentes
pow privada larga (en base, int exp) {
largo r = 1;
mientras (exp... 0) r *= base;
retorno r;
}
}
`` `

**Las complejidades* *
- Tiempo: `O(log n)` (≤ 10 iteraciones)
- Espacio: `O(1)`

-...

## 📚 Code – Python

``python
Solución de clase:
def enMostNGivenDigitSet(self, digits: List[str], n: int) - título int:
N = str(n)
k = len(N)
dlen = len(digits)

# helper: poder entero
def pow_int(b, e):
b ** e

total = 0

# 1) todos los números con menos dígitos
para longitud en rango(1, k):
total += pow_int(dlen, length)

# 2) la misma longitud
para i, ch in enumerate(N):
cur = int(ch)
igual = Falso
para d en dígitos:
val = int(d)
si val se hizo cur:
total += pow_int(dlen, k - i - 1)
elif val == cur:
igual = verdadero
si no es igual:
total

# 3) n itself
total de retorno + 1
`` `

-...

## 📚 Code – C++

``cpp
Clase Solución {
public:
int atMostNGivenDigitSet(vector asignadosstring curva digits, int n) {
cadena N = to_string(n);
int k = N.size(); // digitos in n
int dlen = digits.size(); // dígitos permitidos

long long total = 0;

// 1) menos dígitos
for (int len = 1; len ■ k; ++len)
total += pow_int(dlen, len);

// 2) la misma longitud
para (int i = 0; i) {}
int cur = N[i] - '0';
bool igual = falso;
para (la cadena contigua &d : dígitos) {}
int val = d[0] - '0';
si
total += pow_int(dlen, k - i - 1);
si (val == cur)
igual = verdadero;
}
si (!equal) devolver static_cast correctamenteint(total);
}

// 3) En sí mismo
retorno estático_cast seleccionado(total + 1);
}

privado:
long long pow_int(int base, int exp) {
largo largo r = 1;
mientras (exp--) r *= base;
retorno r;
}
};
`` `

-...

## 🤕 The “Bad” " Ugly " – Common Pitfalls

¿Por qué no se puede arreglar la vida?
Silencio--------------------------
TENIDO Utilizando `Math.pow` (Java) / `pow` (C+++) que devuelve **double** Silencio Precision loss para grandes exponentes; errores de redondeo ANTE Utilizar la multiplicación entero (explicación rápida)
Silencio Olvídate del caso en el que `n` en sí es **no** constructible ← Respuesta final errada (desapareciendo `+1`) Silencio Después del lazo, añadir `1` **sólo** si el lazo nunca se rompió temprano tención
Silencio Assuming `n` tiene el mismo número de dígitos que el número más largo posible ← Cuenta incorrecta de números más cortos TENIDO Explícitamente pre-add todos los números con menos dígitos ANTE
¦ Recursión con memoización pero olvidando el uso de 'long' Silencioso cuando `digits.length` = 9 y longitud = 10  duración Use `long long` (64‐bit) para sumas intermedias
Errores en el exponente `(k-i-1)` ← Valor de potencia incorrecto tención Verificar índices cuidadosamente; prueba de unidad-prueba en muestras TEN

-...

## 🔄 Alternative: Digit‐DP (el “Uglier” pero más general)

Si necesita soportar *diferentes* dígitos conjuntos por posición o más restricciones (por ejemplo, suma de dígitos, sin ceros principales), el dígito clásico‐ DP con memoización se vuelve útil.

``java
// Java skeleton
Clase Solución {
int[] dp; // memo table
boolean[][][] vis;
Números de cadenas;
int nDigits;

int public int atMostNGivenDigitSet(String[] digits, int n) {
esto.digits = dígitos;
String s = String.valueOf(n);
nDigits = s.length();
dp = nuevo int[n] Digits + 1];
vis = nuevo booleano[nDigits + 1][1];
Arrays.fill(dp, -1);
dfs(0, true);
}

int dfs(int pos, boolean tight) {
si (pos == nDigits) regresa 1;
dp[pos];
int limit = tight ? (String.valueOf(n)).charAt(pos) - '0' : 9;
int ans = 0;
para (String d : digits) {
int val = d.charAt(0) - '0';
si (val latitud límite) romper;
ans += dfs(pos + 1, tight ' val == limit);
}
si (!tight) { vis[pos] [0] = verdadero; dp [pos] = ans; }
devolver los ans;
}
}
`` `

Esta versión es más verbosa pero muestra cómo la misma lógica generaliza.

-...

## 📈 SEO & Interview Take-aways

- **Keywords**: *LeetCode 902*, *Números en la mayoría de N dado dígitos set*, * Solución java*, * Solución pitón*, *Solución C+*, * entrevista de codificación*, *digit DP*, *ayuda de entrevista de trabajo*.
- **Meta Descripción** (para un blog):
“Master LeetCode 902 – Números En la mayoría N Given Digit Set. Ver soluciones Java, Python y C+++, explicaciones detalladas y trampas comunes para evitar. ¡Aproveche su actuación de entrevista de codificación! ”
- **Call‐to-Action**: “Como, compartir y suscribirse para más tutoriales de entrevista. ”

**Entreview Tip**:
- Comience con la idea de alto nivel (contando con menos dígitos).
- Aclarar las suposiciones acerca de la entrada (la longitud de n’).
- Muestra el conteo combinatorio antes de la codificación.
- Discuss edge cases (“¿No cuenta ella misma?”).
- Mencionar la solución *O(log n)* como una respuesta limpia y lista para la producción.

-...

##  inaceptable Final Checklist

Contando combinatorios con poderes enteros.
- [ ] Pre-add todos los números de longitud más corta.
- [ ] Maneja el desajuste prefijo correctamente.
- [ ] Add `+1` sólo cuando `n ' en sí es constructible.
- [ ] Use enteros de 64 bits para evitar el desbordamiento.
- [ ] Ejecutar pruebas unitarias sobre las entradas de muestra (`[1,3,5,7]`, `100`) y los casos de borde (`[1",'2", "3"] `1234`).

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀

-...

**Referencia**:
- Declaración del problema LeetCode: https://leetcode.com/problems/numbers-at-most-n-given-digit-set/
- Classic digit‐DP resource: https://cp-algorithms.com/algebra/digit-dp.html

-...

*Preparado por: ChatGPT – Tu entrenador de entrevista de codificación AI. *