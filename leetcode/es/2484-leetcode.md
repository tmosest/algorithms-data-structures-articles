-...
Título: LeetCode 2484. Conde Palindromic Subsecuencias -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2484 – Conde Palindromic Subsequences (Length 5)

■ *Problema*
■ Dado una cadena de dígitos (0-9) de longitud hasta `104`, cuenta cuántos
Las subsecuencias de *exactamente* 5 caracteres forman un palindromo.
■ Devuelve el conteo modulo `109 + 7`.

-...

### 1. Por qué este problema es una gran pregunta de entrevista

* ** Longitud fija** – La etiqueta “hard” es un poco de un misnomer; el hecho de que
sólo necesitamos subsecuencias de la longitud 5 gira una explosión combinatoria
en un problema de alcance.
* **Requiere una buena comprensión de prefijos / matrizs de sufijo** – La mayoría
los candidatos sólo piensan en una fuerza bruta ingenua O(n5) o en una programación dinámica
enfoque que ignora la longitud fija.
* **Elegant math trick** – La solución utiliza un truco de prefijo y suffix neat que
Muchos entrevistados fallan.

■ Si puede explicar esta solución de forma limpia, impresionará cualquier contratación
√ manager que se preocupa por algoritmos, manipulación de cadenas y matemáticas
Pensando.

-...

## 2. Intuición " Derivación "

Un palindrome de 5 caracteres tiene la forma

`` `
ab
`` `

con `a == e ' y `b == d`.
Los índices deben satisfacer " a " b " c " seg.
Así podemos pensar en la subsequencia

1. Elija dos **outer** índices `a` y `e` que tienen el mismo dígito.
2. Elija dos **inner** índices `b ' y `d` que tienen el mismo dígito.
3. Escoge cualquier `c` que miente entre `b` y `d`.

The number of choice for `c` is simply `d - b - 1`.

Si nos iteramos sobre todos los pares posibles `b ' (el par interior) sólo nosotros
necesita saber:

* ¿Cuántos índices externos con dígito `x` existen dejados de `b`? → `L[x]`.
* ¿Cuántos índices externos con dígito `x` existen derecho de `d`? → `R[x]`.

Entonces la contribución de este par `(b,d)` es

`` `
(d - b - 1) * bahx L[x] * R[x]
`` `

El reto es computar esa suma para **todos**(b,d)
sin doble cuenta.

### 3. Prefijo / Cuentas de Sufijo

Por cada dígito `d` (0‐9) pre-compute:

`` `
pref[d][i] – número de d’s en s [0 ... i]
suff[d][i] – número de d’s en s[i ... n-1]
`` `

Ambos arrays se pueden construir en tiempo O(10·n).

### 4. Agrupación sobre pares interiores

Seamos el dígito del par interior ( " b " y " tendrían dígitos " ).
Recopilar todas las posiciones donde `s[pos] == y` en un array `pos[0 ... k-1]`.

Para un dígito externo fijo `x` necesitamos calcular

`` `
[i] [i]-1] * suff[x] [pos[j]+1] * (pos[j] - pos[i]
`` `

Esto parece un bucle doble, pero podemos colapsarlo a **O(k)** usando
ejecutando sumas:

`` `
sumaA = ega_{i)current} pref[x][pos[i]-1]
[x] [pos[i]-1] * pos[i]
`` `

Por el actual `j`:

`` `
contrib = (pos[j] * sumA - sumAPos - sumA) * suff[x][pos[j]+1]
`` `

Añada `contrib` a la respuesta mundial, a continuación, actualice `sumA` y `sumAPos`
con el actual `i = j`.

Hacer esto por cada dígito externo `x` (0‐9) y cada dígito interno `y `
(0‐9) produce el recuento final en **O(10·10·n)** = `O(n)` tiempo.

Todas las operaciones se realizan modulo `MOD = 1_000_000_007`.

-...

## 5. Prueba de corrección

Demostramos que el algoritmo devuelve el número exacto de palindromic
subsecuencias de la longitud 5.

-...

### Lemma 1
For any index `p` and digit `d`, `pref[d][p-1]` [p+1]
iguala el número de índices externos con dígito `d` estrictamente a la izquierda
(respectivamente a la derecha) de `p`.

Proof.
`pref[d][p-1]` cuenta todos los casos de `d` en el final del prefijo sólo
antes de " p " ; ese es exactamente el conjunto `{ i latitud 0 ≤ i ' significa p, s [i] = d }`.
Análogamente, `suff[d][p+1] ' cuenta todas las ocurrencias en el sufijo comenzando
justo después de `p`.



### Lemma 2
Para cualquier par interior " b " (dos dígitos iguales a " y " ) y cualquier dígito externo
`x`, el término

`` `
pref[x][b-1] * suff[x][d+1]
`` `

iguala el número de maneras de elegir un par exterior `(a,e)` con dígitos
`x' que satisfice `a ANTEB ' y ' d ' hecho e ' .

Proof.
Por Lemma adultnbsp;1, `pref[x][b-1] ' cuenta todos `x ' s left of `b`; cada uno
tal ocurrencia puede utilizarse como " a " .
`suff[x][d+1]` cuenta todo el derecho de `x' de `d`; cada uno puede ser utilizado como `e`.
Las opciones son independientes, por lo que el producto cuenta todo exterior admisible
pares.



### Lemma 3
Para un dígito interno fijo `y' y el dígito externo `x`, el algoritmo calcula

`` `
[i]-1] * suff[x] [pos[j]+1] * (pos[j]-pos[i]-1)
`` `

exactamente.

Proof.
Considere el paso iterativo para el índice `j`.

* `sumA` holds `eva_{i efectuaj} pref[x][pos[i]-1]`.
* `sumAPos` holds `eva_{iיj} pref[x][pos[i]-1] * pos[i]`.

Por lo tanto

`` `
pos[j] * sumA = Governing_{iَj} pref[x][pos[i]-1] * pos[j]
sumaAPos = ega_{i} pref[x][pos[i]-1] * pos[i]
`` `

Subtracting gives

`` `
pos[j] * sumA - sumAPos = ega_{i} pref[x][pos[i]-1] * (pos[j] - pos[i]
`` `

Subtracting an additional `sumA` yields

`` `
(pos[j] - pos[i] - 1)
`` `

Multiplying by `suff[x][pos[j]+1] da exactamente el término que el
usos de fórmula de contribución. Por lo tanto cada iteración añade lo correcto
cantidad para todos los pares `(i,j)` con `i cautivar j`. Summed over all `x `
(0-9) y todo `y' (0-9), cada palindrome admisible se cuenta una vez
y sólo una vez.



### Theorem
`contraPalindromicSubseq(s)` devuelto por el algoritmo equivale al número de
5-caracter palindromic subsequences of `s`, modulo `MOD`.

Proof.
De Lemma 3 sabemos que para cada elección del dígito interno `y' y exterior
dígito `x` el algoritmo suma sobre todas las posiciones externas admisibles
El producto

`` `
pref[x][i-1] * suff[x][j+1] * (pos[j]-pos[i]-1)
`` `

Por la derivación en la sección 2 esto es precisamente la contribución de todos
subsecuencias palindrómicas cuyos dígitos internos equivalen a `y ' y dígitos externos
igual `x`.
Resumiendo sobre todas las combinaciones 10×10 por lo tanto representa cada
subsequencia palindrómica exactamente una vez, demostrando el teorema. ∎



-...

## 6. Análisis de la complejidad

TEN TERRITORIO TERRITORIO ANTERIOR
Silencio...
← Prefix " suffix arrays " Silencio
Silencio Principal agregación Silencioso `O(10·10·n)` Silencio
Silencio **Total** Silencioso ** ``O(n)` tiempo, `O(10·n)` memoria**

Con `n ≤ 104`, el algoritmo funciona cómodamente bajo 1 ms en todos
idiomas.

-...

## 6. Aplicación de las referencias

A continuación se presentan implementaciones idiomáticas limpias en **Java 17**, **Python 3.11**,
y **C+17**.
Los tres usan la misma lógica, para que pueda caer uno en un arnés de prueba o
llevarlo a otro idioma sin esfuerzo.

■ **Tip** – Al someterse a un juez en línea, asegúrese de establecer
" MOD = 1_000_000_007L " (Java) o `MOD = 1000000007 ' (Python, C++).

-...

### 5.1 Java 17

``java
importa java.io.*;
importar java.util*;

clase pública Principal {}
static final long MOD = 1_000_000_007L;

conteo largo estáticoPalindromicSubseq(String s) {
int n = s.length();
int[][] pref = nuevo int[10][n];
int[][] suff = new int[10][n];

// Prefijo
para (int d = 0; d)
int cnt = 0;
para (int i = 0; i)
si (s.charAt(i) - '0' == d) cnt+;
pref[d][i] = cnt;
}
}

/ Suffix
para (int d = 0; d)
int cnt = 0;
para (int i = n - 1; i 0; i--) {
si (s.charAt(i) - '0' == d) cnt+;
[d] [i] = cnt;
}
}

ans largas = 0;

// Por cada dígito interno y
para (int y = 0; y
// Reunir todas las posiciones del dígito y
Lista realizadaInteger confianza posList = nuevo ArrayList fiel();
para (int i = 0; i)
si (s.charAt(i) - '0' == y) posList.add(i);
}
int k = posList.size();
si (k 0 = 1) continuar; // necesita al menos dos índices internos

// Para cada dígito externo x
para (int x = 0; x < 10; x++) {
long sumA = 0;
Sumas largas = 0;
para (int idx = 0; idx = k; idx++) {}
int pos = posList.get(idx);
larga A = pos == 0 ? 0 : pref[x][pos - 1];
long B = pos = n - 1 ? 0 : suff[x][pos + 1];

largo plazo = (pos * sumA % MOD - sumAPos - sumA) % MOD + MOD) % MOD;
long contrib = term * B % MOD;
as = (ans + contrib) % MOD;

sumA = (sumA + A) % MOD;
sumAPos = (sumAPos + A * pos) % MOD;
}
}
}
devolver los ans;
}

--------- Conductor para la prueba...--------
public static void main(String[] args) tira IOException {
BufferedReader br = nuevo BufferedReader (nueva InputStreamReader(System.in));
String s = br.readLine().trim();
System.out.println(countPalindromicSubseq(s));
}
}
`` `

-...

### 5.2 Python 3.11

``python
importadores

MOD = 1_000_000_007

def count_palindromic_subseq(s: str) - int:
n = len(s)

# Prefix and suffix arrays
pref = [0] * n for _ in range(10)]
suff = [0] * n for _ in range(10)]

# Build pref
para d en rango(10):
cnt = 0
para i, ch in enumerate(s):
si ord(ch) - 48 == d:
cnt += 1
[d][i] = cnt

# Build suff
para d en rango(10):
cnt = 0
para i en rango(n - 1, -1, -1):
ord(s[i]) - 48 == d:
cnt += 1
[d] [i] = cnt

ans = 0

# Main aggregation
para y en rango(10):
posiciones = [i for i, ch in enumerate(s) if ord(ch) - 48 == y]
k = len(positions)
si k
continuar

para x en rango(10):
sumA = 0
sumAPos = 0
para posponer en posiciones:
A = pref[x][pos - 1] if pos ⇩ 0 si no 0
B = suff[x][pos + 1] si pos + 1 0

# (pos * sumA - sumAPos - sumA) mod MOD
término = (pos * sumA - sumAPos - sumA) % MOD
contrib = term * B % MOD
ans = (ans + contrib) % MOD

sumaA = (sumA + A) % MOD
sumaAPos = (sumAPos + A * pos) % MOD

Retorno

si __name_ == "__main__":
s = sys.stdin.readline().strip()
print(count_palindromic_subseq(s))
`` `

-...

### 5.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;
const long MOD = 1'000'000'007LL;

largo largo conteoPalindromicSubseq(cont cordón limitado s) {
int n = s.size();
vector realizador realizado, 10001 título pref(10), suff(10); // 10 x n

// Prefijo
para (int d = 0; d) {}
int cnt = 0;
para (int i = 0; i) {}
si (s[i] - '0' == d) ++cnt;
pref[d][i] = cnt;
}
}

/ Suffix
para (int d = 0; d) {}
int cnt = 0;
para (int i = n - 1; i 0; --i) {
si (s[i] - '0' == d) ++cnt;
[d] [i] = cnt;
}
}

ans largos = 0;
vector significado pos;

para (int y = 0; y
pos.clear();
para (int i = 0; i)
si (s[i] - '0' == y) pos.push_back(i);
int k = pos.size();
si continúan (k <=1);

para (int x = 0; x < 10; ++x) {
long sumA = 0, sumAPos = 0;
para (int p : pos) {
largo largo A = (p == 0) ? 0 : pref[x][p - 1];
largo largo B = (p + 1 == n) ? 0 : suff[x][p + 1];

largo plazo = (p * sumA % MOD - sumAPos - sumA) % MOD + MOD) % MOD;
largo largo largo contrib = término * B % MOD;
as = (ans + contrib) % MOD;

sumA = (sumA + A) % MOD;
sumAPos = (sumAPos + A * p) % MOD;
}
}
}
devolver los ans;
}

int main() {}
ios::sync_with_stdio(false);
cin.tie(nullptr);
cadena s; getline(cin, s);
cout se realizó el conteoPalindromicSubseq(s)
}
`` `

-...

## 7. Preguntas frecuentes

Respuesta a la respuesta
Silencio...
Silencio **¿Por qué no la fuerza bruta? ** Por `n=104`, la fuerza bruta es `O(n^5)` → imposible. Silencio
Silencio **¿Qué pasa si la cuerda está vacía? ** Silencio Devuelve `0`. Silencio
Silencio **¿Puede el algoritmo manejar la memoria enorme? ** Silencio Utiliza sólo 'O(10·n)` ints → Silencio
Silencio **¿Por qué ignoramos 'k ≤ 1'?** Silencio Un par interior requiere al menos dos índices. Silencio

-...

## 8. ¿Qué hace este problema *Hard*?

1. **Four-nested structure** – Usted debe administrar simultáneamente dos
Dimensiones (inner vs external indices) respetando las limitaciones de orden.
2. **Cuento dinámico** – La enumeración ingenua sería exponencial.
3. **Modulo arithmetic** – Evitar el desbordamiento preservando la corrección.
4. **Edge cases** – Empty strings, all identical digits, very short
cuerdas.

Un algoritmo bien estructurado que aprovecha las sumas prefijo es la única manera
para resolverlo eficientemente.

-...

## 9. Conclusión

Hemos construido una solución óptima para contar palindromic de 5 caracteres
subsequences:

* Una cuidadosa reducción combinatorial que conduce a un algoritmo lineal.
* Una prueba rigurosa de que el método es correcto.
* Tres implementaciones de referencia que puede copiar, probar y adaptar.

■ ** Nota final** – El mismo patrón (prefix–suffix cuenta + agregación)
Puede aplicarse a muchos otros problemas de conteo de subestring (por ejemplo, contando
ocurrencias de patrones de subsequencia específicos, o palindromes de 3 caracteres
± con diferentes limitaciones). Dominar esta técnica pagará
En futuros concursos. ¡Feliz codificación! 🚀
-...



¡Feliz codificación