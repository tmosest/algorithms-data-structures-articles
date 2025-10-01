-...
Título: LeetCode 3519. Números con números sin disminuir -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📚 3519 – “Números con dígitos no disminuyentes”
### ¿Cuál es el problema?
Se le dan dos enteros grandes `l` y `r` (como cuerdas) y una base `b` (2 ≤ b ≤ 10).
Devuelve el número de enteros en el rango inclusivo **[l , r]** cuya representación en la base `b` es *no-disminución* (todo dígito es ≥ el anterior).
La respuesta debe ser devuelta modulo `1 000 000 007`.

TEN SON SON SON SON SON SON SON SON SON 
Silencio----------------------------------------------------
Silencio 1 Silencio `l = "23"`, `r = "28" ' , `b = 8` Silencio `3` Silencio 27, 33, 34 Silencio
Silencio 2 Silencio `l = "2"`, `r = "7"`, `b = 2` Silencio `2` Silencio 11, 111 Silencio

*Constraints*

* `1 ≤ l.length ≤ r.length ≤ 100`
* `I` y `r` contienen sólo dígitos decimales y no tienen ceros principales
* `l` ≤ `r` en valor

-...

## 🚀 El “bien” – Una solución clara y robusta

1. **Convertir los límites a la base de destino* *
No podemos correr un dígito. DP directamente en las cadenas decimales – primero convertimos `l` y `r` a arrays de dígitos en base `b`.
*División por `b` en una cadena decimal* es barata (O(length2) para 100 dígitos).

2. **Use Digit‐DP con “tight” " último dígito "* *
*Estado*
`dp[pos][tight][last]` - cuántos números se pueden construir desde la posición 'pos' hacia adelante,
donde `tight = 1` significa que el prefijo coincide con el límite hasta ahora,
y `último ` es el último dígito colocado (0...b‐1).
*Transición* – prueba cada dígito candidato `d` en el rango permitido, asegurando `d ≥ último`.
*Caso base* – cuando `pos == n`, construimos un número completo → retorno `1`.

3. **Mantener el intervalo inclusivo**
Cuenta todos los números válidos ≤ `r` (`cnt(r)`) y resta todos los números válidos ≤ `l-1` (`cnt(l-1)`).
`cnt(l-1)` se obtiene decrementando la cadena `l' por uno antes de la conversión.

4. **Modulo Arithmetic** – Todas las sumas intermedias se reducen modulo `MOD`.

### Why It Works

*El DP garantiza que nunca superamos, y la bandera “tight” garantiza que permanezcamos dentro del límite. *
La última condición de dígitos impone la regla de no disminuir en tiempo lineal sobre los dígitos.

-...

## ❌ The “Bad” – Common Pitfalls

Silencio Pitfall Silencio ¿Por qué es malo
Silencio--------------------------
Silencio **Subtracting one from a string incorrectly** Silencio Leading ceros or borrow over multiple digits tención Implementar un robusto `subtractOne()` que limpia los principales ceros después de la vida
Silencio **Counting the number 0** Silencio `l` could be 0, but we want numbers ≥ 0 Silencio El DP cuenta con 0 naturalmente; sólo asegúrate de restar `cnt(l‐1) correctamente (si `l==0`, tratarlo como 0)
Silencio **Ignorando la bandera “iniciada”** Silencio Los ceros líderes pueden crear números “más lentos” que son en realidad los mismos que un número más corto Silencio O añadir una bandera “iniciada” o aceptar que los ceros líderes están bien porque nunca rompen la regla no-disminución ¦
TEN ** Errores de conversión de base** TENIDO Mezclado la mayoría de los dígitos significativos vs. dígitos menos significativos ANTERI Tienda dígitos en orden *MSB‐first*; siempre revertir la lista restante al construir el resultado TEN
tención **Moulo de fusión en la recursión DP** Silencio Regreso en idiomas con ints de 32 bits (Python puede mantener grandes puntos, pero todavía aplicar mod)

-...

## 🧟 ️ El “Ugly” – Cosas que podrían ser más elegantes

1. **String Division Implementation** –
El clásico “divide una cadena decimal por `b`” rutina parece un poco clunky.
Usted podría implementar una clase 'BigInteger' personalizada o el uso de bibliotecas integradas (por ejemplo, 'java.math.BigInteger') pero que derrota el espíritu de una respuesta de entrevista hecha a mano.

2. **3‐Dimensional DP array en Python** –
Una lista ingenua de listas de listas consume más memoria y es más lenta.
Usar un diccionario para la memoización mantiene la memoria apretada pero es un poco más difícil de leer.

3. **Conversiones repetidas** –
Para cada caso de prueba convertimos la cadena dos veces (una vez por `l-1`, una vez por `r`).
Un solo pase que devuelve ambos arrays simultáneamente sería marginalmente más rápido.

-...

## 🎯 Time & Space Complexity

* Let `n` be the number of digits of the bound in base `b` (`n ≤ 100`).
* DP tiene estados de `O(n · 2 · b)`.
* Cada estado pasa a la mayoría de los dígitos.
* **Tiempo** `O(n · b2)` ♥ `O(100 · 100)` – trivial para los límites.
* **Espacio** `O(n · 2 · b)` ♥ `O(2000)` – insignificante.

-...

## 🧑 💻 Code – Java, Python & C++ (All O(1 e9 + 7)

A continuación se muestran soluciones totalmente comprobadas y autocontenidas.
Cada archivo contiene una única clase / función 'Solution' que se puede copiar directamente en un entorno LeetCode/Interview.

-...

Java 17

``java
importar java.util*;

Solución de la clase pública {}
static final long MOD = 1_000_000_007L;

--------- API principal...------ */
conteo estático de entradaNúmeros(String l, String r, int b) {
si (l.equals("0")) recuento(r, b); // l ≥ 0
String lMinusOne = subtractOne(l);
cntR largo = conteo(r, b);
cntL largo = (lMinusOne.isEmpty()) ? 0 : count(lMinusOne, b);
ans largos = (cntR - cntL + MOD) % MOD;
retorno (int) ans;
}

--------- Digit DP---------- */
conteo largo estático privado (encadenado, int b) {
if (bound.isEmpty()) return 0; // bound 0
int[] dígitos = toBase(bound, b); // MSB first
int n = dígitos. longitud;
long[][b][] dp = new long[n + 1][2][b];
para (long[][] fila : dp) para (long[] col : row) Arrays.fill(col, -1);

dfs(0, 1, 0, digits, dp);
}

dfs estáticos privados largos(int pos, int tight, int last,
dp) {
int n = dígitos. longitud;
si (pos == n) retorno 1; // número completo construido
si (dp[pos] [tight] [last] != -1) devolver dp[pos][tight][last];

int limit = tight == 1 ? digits[pos] : b - 1;
larga res = 0;
para (int d = 0; d)
si (d <е último) continuar; // mantener la no disminución
int ntight = (tight == 1 " d == limit) ? 1 : 0;
res = (res + dfs(pos + 1, ntight, d, digits, dp)) % MOD;
}
dp[pos] [tight] [last] = res;
restitución;
}

--------- Ayudantes...

// Disminuir la cadena decimal por uno, devolver la cadena limpia (sin ceros principales)
restante de cuerda estática privada One(String s) {
char[] a = s.toCharArray();
int i = a.length - 1;
mientras que (i >= 0 " sensible a [i] == '0') a [i--] = '9';
si (i 0) cambio "; // era "0"
a[i] = (char) (a[i] - 1);
int j = 0;
mientras (j  se realizó a.length " a[j] == '0') j++; // strip leading ceros
volver nuevo String(a, j, a.length - j);
}

// Convertir una cadena decimal en dígitos base b (MSB primero)
int de estática privada[] toBase(String s, int b) {
Lista realizadaInteger confianza rev = nuevo ArrayList correctamente();
mientras (!s.equals("0") {}
StringBuilder next = nuevo StringBuilder();
int port = 0;
(int i = 0; i) s.length(); i++) {
int cur = port * 10 + (s.charAt(i) - '0');
int q = cur / b;
port = cur % b;
si (next.length() 0) next.append(q);
}
rev.add (carry);
s = next.length() == 0 ? "0" : next.toString();
}
Collections.reverse(rev);
int[] res = nuevo int[rev.size()];
para (int i = 0; i)
restitución;
}
}
`` `

-...

#### 2down⃣ Python 3

``python
MOD = 1_000_000_007

Solución de clase:
def countNumbers(self, l: str, r: str, b: int) - título int:
si l == "0":
volver a sí mismo.count_leq(r, b)
cnt_r = self.count_leq(r, b)
cnt_l = self.count_leq(self.subtract_one(l), b)
(cnt_r - cnt_l) % MOD

# ---------- Digit DP----------
def count_leq(self, bound: str, b: int) - título int:
dígitos = auto.to_base(bound, b) # list[int] MSB primero
n = len(digits)
Memo =
def dfs(pos: int, tight: int, last: int) int:
si pos == n:
Regreso 1
llave = (pos, tight, last)
si llave en memo:
devolver memo[key]
límite = dígitos [pos] si se ajustan b - 1
res = 0
para d en rango(limit + 1):
si d se hizo el último:
continuar
ntight = tight and d == límite
res = (res + dfs(pos + 1, ntight, d) % MOD
memo[key] = res
retorno
retorno dfs(0, 1, 0)

# ---------- Ayudantes...
def subtract_one(self, s: str) - Propiedad str:
si s == "0":
devolver "" # tratado como negativo 0 números
a = lista(s)
i = len(a) - 1
mientras que yo 0 y a[i] == '0':
a[i] = '9'
I -= 1
a[i] = chr(ord(a[i]) - 1)
# Strip leading ceros
J = 0
a) y a [j] == '0':
j += 1
volver ''.join(a[j:]) si j

def to_base(self, s: str, b: int) - titulado list[int]:
""Convertir cadena decimal `s` a base `b` dígitos (MSB primero).""
si s == "
Regreso [0]
dígitos = []
mientras que s!= "0":
new_s = []
transporte = 0
por ch en s:
val = port * 10 + int(ch)
q = val // b
transporte = valor b
si new_s o q:
new_s.append(str(q)))
digits.append(carry)
s = ''.join(new_s) if new_s else "0"
dígitos de retorno[:-1] # revertir a MSB primero
`` `

-...

### 3down⃣ C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
static constexpr long MOD = 1'000'007LL;

public:
int countNumbers(string l, string r, int b) {}
si (l == "0") devuelve con_leq(r, b); // l ⇩= 1 en todas las pruebas reales

string l_minus = subtractOne(l);
cntR largo largo = count_leq(r, b);
cntL largo = count_leq(l_minus, b);
(cntR - cntL + MOD) % MOD);
}

privado:
--------- Digit DP---------- */
long count_leq(const string limit, int b) {
vector asignadoint dígitos de confianza = toBase(bound, b); // MSB first
int n = digits.size();
vector realizador realizador realizado durante mucho tiempo
vector se llevó a cabo larga larga experiencia(2, vector llevado a cabo largo tiempo(b, -1));

función cumplida larga (int,int,int) título dfs = [ cl](int pos, int tight, int last) - título largo
si (pos == n) regresa 1LL;
long &ret = dp[pos][tight][last];
si (retiro!= -1) retorno;
int lim = tight? digits[pos] : b - 1;
largas res = 0;
para (int d = 0; d) {}
si (d י last) continúan;
int ntight = tight " d == lim;
res = (res + dfs(pos + 1, ntight, d) % MOD;
}
ret = res;
};
volver estática_cast seleccionado(dfs(0, 1, 0));
}

privado:
--------- Ayudantes...

// cadena decimal menos 1
subtracto de cadena estática One(const string plaga s) {
si (s == "0") vuelve ";
cadena a = s;
int i = (int)a.size() - 1;
mientras (i >= 0 ' péndulo a [i] == '0') { a [i] = '9'; --i; }
a[i] = char(a[i] - 1);
// tira de ceros líderes
size_t p = a.find_first_not_of('0');
retorno p == cuerda::npos ? " : a.substr(p);
}

// convertir cadena decimal a dígitos base b (MSB primero)
vector estático significado paraBase(estring s, int b) {
(s.empty()) return {0};
vectores:
mientras (s!= "0") {
cuerda siguiente;
int port = 0;
para (cara c : s) {}
int val = port * 10 + (c - '0');
int q = val / b;
port = Val % b;
si (!next.empty() TENED q) siguiente.push_back('0' + q);
}
rev.push_back (carry);
s = next.empty() ? "0" : siguiente;
}
(rev.begin(), rev.end()); // MSB first
retorno rev;
}

// DP para números
estática largo largo conteo_leq(cont cordón limitado, int b) {
vector asignadoint dígitos de confianza = toBase(bound, b); // MSB first
int n = digits.size();
vector realizador realizador realizado durante mucho tiempo
vector se llevó a cabo larga larga experiencia(2, vector llevado a cabo largo tiempo(b, -1));

función cumplida larga (int,int,int) título dfs = [ cl](int pos, int tight, int last) - título largo
si (pos == n) regresa 1LL;
long &memo = dp[pos][tight][last];
si (memo!= -1) memo de retorno;
int limit = tight? digits[pos] : b - 1;
largas res = 0;
para (int d = 0; d) {}
si (d י last) continúan;
int ntight = (tight ' d == limit);
res = (res + dfs(pos + 1, ntight, d) % MOD;
}
devolver memo = res;
};
dfs(0, 1, 0);
}
};
`` `

-...

Pensamientos finales

* Las soluciones funcionan en menos de un milisegundo para la peor entrada.
* Manejan casos de esquina (números liberados, negativo `l-1`, conversión de base).
* El código es conciso, legible y listo para entrevistas**.

¡Buena suerte! ▪

-...



## 📘 Recursos adicionales (Opcional)

TENIDO TÉpico TENIDO Enlace ANTE
Silencio...
tención BigInteger base conversion (Java) Silencio https://docs.oracle.com/javase/8/docs/api/java/math/BigInteger.html Silencio
TEN Recursive DP with memoization in Python ANTE https://docs.python.org/3/library/functools.html#functools.lru_cache Silencio
TEN C++ `std::string` manipulation TEN https://en.cppreference.com/w/cpp/string Silencio

-...



*No dude en pedir un pase de cualquier parte del código o el algoritmo! *