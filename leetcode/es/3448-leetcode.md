-...
Título: LeetCode 3448. Conde Substrings Divisible por Last Digit -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Cracking LeetCode 3448: Count Substrings Divisible por Last Digit
*O(n) Soluciones en Java, Python y C++ – una entrevista completa Guía lista*

-...

## TL;DR

- **Problema** - Contar todas las subestrings de una cadena de dígitos que son divisibles por su último dígito **no-cero**.
- "Hardness" en LeetCode.
- ** Solución óptima** – Un paso (`O(n)`), utilizando los restos prefijos y una pequeña tabla de frecuencia para la regla de divisibilidad de cada dígito.
- **Idiomas** - Java, Python, C++.
- **Palabras clave de SEO** – *LeetCode 3448*, *subestaciones de cuenta divisibles por último dígito*, *O(n) solución*, *Java, Python, C++*, * algoritmo de visión*, *programación dinamica*, *reglas de visibilidad*.

-...

## 1. Panorama general de los problemas

■ **Introducción**: Una cadena `s` (`1 ≤ últimas sometidas ≤ 105`) que contiene sólo dígitos decimales.
■ **Output**: The number of substrings `s[i...j]` tal que:
* `s[j]!= '0'` (el último dígito no es cero)
* el entero representado por la subestring es divisible por el valor de su último dígito.

■ *Ejemplo*
< < > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > >

La clave es que *los ceros liberados están permitidos*, así que `"01" es una subestring válida, pero se ignora una subestring que termina en `'0'.

-...

## 2. Constraints " Edge Cases

Silencio .
Silencio...
Silencioso `sobrevivir` hasta 100 000 Silencio debe ser lineal
Silenciosos dígitos Silenciosos `'0'``'9'` Silencio dígitos `0` nunca forma un último dígito válido Silencio
El resultado de la sobrefluencia permanente puede ser de hasta 5 × 109  sometida a uso de 64 bits ( " largo " ) Silencio

-...

## 3. Enfoques ingenuos

TENCIÓN ANTERIENTE Complejidad ANTERIOR Por qué falla
Silencio...
Silencio Enumerar todas las subestrings y comprobar la divisibilidad en la mosca Silencio `O(n2)` Silencio Demasiado lento para 105 Silencio
Silencio Precompute integer values of all substrings Silencio `O(n2)` la memoria ← Imposible
Silencio Programación dinámica con el estado `(endIndex, remainder)` Silencio `O(n·10·10)` Silencio Todavía demasiado grande; podemos hacer mejor Silencio

Debido a que cada último dígito tiene una regla de divisibilidad *específica* (por ejemplo, `4` depende sólo de los dos últimos dígitos, `8` de los tres últimos, `3` de la suma de dígitos), podemos aprovechar esto y evitar cualquier comportamiento cuadrático.

-...

## 4. Estrategia optimizada O n)

### 4.1 Reglas de Divisibilidad por Last Digit

Silencio para la vida
Silencio...
Silencio **1, 2, 5** Silencio Cada número que termina con estos dígitos es divisible por `d` Silencio Add `j+1` (todas las subestrings terminan en `j`) Silencio
Silencio **3, 6, 9** Silencio Un número es divisible por `3` (o `9`) si la suma de sus dígitos es. Mantenga prefijo resto modulo `3`/`9` y cuente los partidos. Silencio
Silencio **4** Silencio Divisible si el último **dos** dígitos forman un número divisible por 4 Silencio Check `(10*prevDigit + d) % 4` ←
Silencio **8** Silencio Divisible iff el último **tres** dígitos (o dos últimos para `j=1`) forman un número divisible por 8 Silencio Check `(100*d3 + 10*d2 + d) % 8` Silencio
Silencio **7** Silencio Necesita un poco más de matemáticas: < n % 7 == 0 >  pérdidas `n = 100·a + 101·b + ... > → utilizamos el modulo 7 prefijo y una pequeña mesa de 6 ciclos. Silencio Pre-compute inverses of `10^k mod 7` (`k=0,5`) and look up frequencies. Silencio
Silencio **0** Silencio *Ignorado*

### 4.2 Restauración de prefijo

Para los dígitos que confían en * toda la subestring* (`3,6,9,7`) mantenemos el resto de funcionamiento:

``text
prefijo[i] = (valor de s[0...i]) % 7
`` `

Usar el resto en el **end** de una subestring es suficiente porque para una subestring `s[l...r] `

`` `
valor(l,r) % d == 0 Alternativa prefix[r] % d == prefijo[l-1] * (10^(r-l+1) mod d) % d
`` `

- Por `3,6,9` el multiplicador es siempre `1` (el resto es independiente de la longitud de subestring).
- Por `7` el multiplicador cambia cada 6 posiciones porque `10^k mod 7` repite con el período 6.

#### 4.3 Tablas de Frecuencia

Para cada regla mantenemos una pequeña variedad de conteos:

``text
freq3[0..2] // conteos de restos prefijos modulo 3
freq9[0.8] // conteos de restos prefijos modulo 9
freq7[0.5][0..6] // para el ciclo 6 de 7
`` `

Durante el escaneo único nosotros:

1. **Cuente** la contribución de la posición actual utilizando la regla apropiada.
2. ** Actualizar** la tabla de frecuencia correspondiente para posiciones posteriores.

Debido a que siempre usamos los valores de prefijo ya procesados*, el algoritmo permanece lineal.

-...

## 5. Aplicación

■ **Tip** – Las tres implementaciones utilizan la misma idea fundamental.
■ Las únicas diferencias son la sintaxis, el manejo de arrays y el soporte integrado de gran entero.

## 5.1 Java (LeetCode-style)

``java
importar java.util*;

Solución de la clase pública {}
// Inversos pre-computados de 10^k mod 7 para k = 0,5
int final estático privado [] INV7 = {1, 5, 2, 3, 6, 4};

public long countSubstrings(String s) {
int n = s.length();
long[] pref3 = new long[n];
long[] pref9 = new long[n];
long[] pref7 = new long[n];
long[] prefAll = new long[n]; // prefix mod 3 (same as pref3)
largo [] freq3 = nuevo largo[3];
largo [] freq9 = nuevo largo[9];
largo[] [] freq7 = nuevo largo [6][7]; // 6 ciclo × 7 restantes

resultado largo = 0;
para (int j = 0; j)
int d = s.charAt(j) - '0';
si (d == 0) { // saltar subestrings terminando en 0
continuar;
}

--------- Regla para los dígitos 1,2,5--------
si (d == 1 Silencioso d == 2 5) {
resultado += j + 1; // todas las subestrings terminan en j
}

--------- Regla para dígitos 3,6,9--------
si no (d == 3 Silencioso 6)
long rem = pref3[j];
resultado += freq3[rem] + (rem == 0 ? 1 : 0);
} más si (d == 9) {
long rem = pref9[j];
resultado += freq9[rem] + (rem == 0 ? 1 : 0);
}

--------- Regla para el dígito 4----------
si (d == 4)
si 0) {
resultado += 1; // sólo el dígito único
. ♫ ... {
el último Dos = (s.charAt(j - 1) - '0') * 10 + d;
resultado += (último dos % 4 == 0 ? (j + 1) : 1);
}
}

--------- Regla para el dígito 8----------
si (d == 8) {
si 0) {
resultado += 1;
} si (j === 1) {
el último Dos = (s.charAt(0) - '0') * 10 + 8;
resultado += (último dos % 8 == 0 ? 2 : 1);
. ♫ ... {
int last3 = (s.charAt(j - 2) - '0') * 100
+ (s.charAt(j - 1) - '0') * 10 + 8;
int last2 = (s.charAt(j - 1) - '0') * 10 + 8;
(último 3 % 8 == 0) resultado += j - 1;
(último 2 % 8 == 0) resultado += 1;
resultado += 1; // la subestring de un dígito
}
}

--------- Regla para el dígito 7----------
si (d == 7) {
long rem = pref7[j];
resultado += (rem == 0 ? 1 : 0);
// escanear todos los 6 posibles exponentes k (0...5)
para (int k = 0; k)
int idx = (j % 6 - k + 6) % 6;
int needed = (int)(rem * INV7[k]) % 7);
result += freq7[idx][need];
}
}

// -------- Actualizar los arrays de prefijo...--------
// Computa nuevos valores de prefijo para la próxima iteración
pref3[j] = (j == 0 ? d : (pref3[j - 1] * 10 + d) % 3);
pref9[j] = (j == 0 ? d : (pref9[j - 1] * 10 + d) % 9);
pref7[j] = (j == 0 ? d : (pref7[j - 1] * 10 + d) % 7);

// Frecuencias de actualización para futuras posiciones
freq3[pref3[j]]++;
freq9[pref9[j]++;
freq7[j % 6][pref7[j]]++;
}
Resultado de retorno;
}
}
`` `

■ *Por qué funciona*
* Cada `d` se maneja en tiempo constante.
* Las tablas de frecuencia ( "freq3 " , `freq9 ' , `freq7 ' ) contiene sólo ** pocas entradas**, así que el uso de la memoria es pequeño.
* El pase único garantiza tiempo.

-...

### 5.2 Python

``python
Solución de clase:
INV7 = [1, 5, 2, 3, 6, 4] # (10^k)^-1 mod 7 for k = 0,5.

def countSubstrings(self, s: str) - Conf int:
n = len(s)
* n
* n
* n

[0] * 3
[0] * 9
freq7 = [[0] * 7 for _ in range(6)]

ans = 0
para j en rango(n):
d = int(s[j])

si # Nunca un último dígito válido
continuar

# 1, 2, 5 – siempre divisible
si d en (1, 2, 5):
ans += j + 1

# 3, 6, 9 - regla de la suma de dígitos
elif d in (3, 6, 9):
rem = pref3[j] if d in (3, 6) else pref9[j]
si d en (3, 6):
ans += freq3[rem] + (1 if rem == 0 más 0)
# d == 9
ans += freq9[rem] + (1 if rem == 0 más 0)

# 4 – dos últimos dígitos
Elif d == 4:
si 0:
ans += 1
más:
last_two = int(s[j-1:]) # dos dígitos que terminan en j
si el último_2 % 4 == 0:
ans += j + 1
más:
ans += 1

# 8 – últimos tres dígitos (o dos para j == 1)
elif d == 8:
si 0:
ans += 1
elif j == 1:
last_two = int(s[0:2])
ans += 2 si el último_2 % 8 == 0 más 1
más:
último_tres = int(s[j-2:j+1])
last_two = int(s[j-1:j+1])
si el último_3% 8 == 0:
ans += j - 1
si el último_2 % 8 == 0:
ans += 1
ans += 1

# 7 – necesita el multiplicador de 6 ciclos
elif d == 7:
rem = pref7[j]
ans += 1 si rem == 0 más 0
para k en rango(6):
idx = (j % 6 - k + 6) % 6
necesario = (rem * self.INV7[k]) % 7
ans += freq7[idx][need]

# Compute new prefix remainders
si 0:
pref3[j] = d % 3
pref9[j] = d % 9
pref7[j] = d % 7
más:
pref3[j] = (pref3[j-1] * 10 + d) % 3
pref9[j] = (pref9[j-1] * 10 + d) % 9
pref7[j] = (pref7[j-1] * 10 + d) % 7

# frecuencias de actualización
freq3[pref3[j] += 1
freq9[pref9[j] += 1
freq7[j % 6][pref7[j]] += 1

Retorno
`` `

■ **Python specifics** –
* Usa `int(s[a:b])' para la extracción rápida de los últimos 2 o 3 dígitos.
* `INV7` es una lista global, evitando la re-creación dentro del bucle.

-...

### 5.3 C++ (GCC 17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
static constexpr int INV7[6] = {1, 5, 2, 3, 6, 4};

public:
int countSubstrings(string s) {
int n = s.size();
vector significado pref3(n), pref9(n), pref7(n);
vector realizado largamente frecuenciaq3(3), freq9(9);
vector realizadora realizada largamente,7 confianza freq7(6); // 6-ciclo × 7

ans largos = 0;
para (int j = 0; j)
int d = s[j]-'0';
si (d == 0) continúan;

/ 1, 2, 5
si (d == 1 Silencioso d == 2 5) {
ans += j + 1;
}
// 3, 6, 9
si no (d == 3 Silencioso 6)
int rem = pref3[j];
ans += freq3[rem] + (rem==0);
} más si (d == 9) {
int rem = pref9[j];
ans += freq9[rem] + (rem==0);
}
// 4
si (d == 4)
si (j == 0) ans += 1;
otra vez
el último Dos = (s[j-1]-'0')*10 + d;
ans += (último dos % 4 == 0 ? j+1 : 1);
}
}
// 8
si (d == 8) {
si (j == 0) ans += 1;
si 1) {
el último Dos = (s[0]-'0')*10 + 8;
ans += (último dos % 8 == 0 ? 2 : 1);
. ♫ ... {
int last3 = (s[j-2]-'0')*100 + (s[j-1]-'0')*10 + 8;
int last2 = (s[j-1]-'0')*10 + 8;
(último 3 % 8 == 0) ans += j-1;
(último 2 % 8 == 0) ans += 1;
ans += 1;
}
}
/ 7
si (d == 7) {
int rem = pref7[j];
ans +=(rem==0);
para (int k=0;k obtenidos6;k+) {}
int idx = (j%6 - k + 6)%6;
int need = (rem * INV7[k]) % 7;
ans += freq7[idx][need];
}
}

// actualización de los restos prefijo para la siguiente ronda
pref3[j] = (j==0? d : (pref3[j-1]*10 + d)%3);
pref9[j] = (j==0? d : (pref9[j-1]*10 + d)%9);
pref7[j] = (j==0? d : (pref7[j-1]*10 + d)%7);

/ / actualizaciones de freq
freq3[pref3[j]]++;
freq9[pref9[j]++;
freq7[j%6][pref7[j]]++;
}
devolver los ans;
}
};
`` `

■ **C++ Notas** –
* Usa `vector` para arrays dinámicos.
* `arrayo realizado largo,7 `` para tabla interior fija, que es ligeramente más rápido que el `vector`.

-...

## 6. Resumen de la complejidad

Silencio Idioma Silencio Tiempo Silencioso
Silencio----------------------------
Silencio Java Silencio O(n) Silencio ~50 bytes
Silencio Python Silencio O(n) Silencio ~70 bytes
Silencio C++ Silencio O(n) Silencio ~50 bytes

* Por qué `O(1)` por posición** –
■ Cada " d " activa a la mayoría de un puñado de accesos a la matriz y operaciones aritméticas.

-...

## 7. Pruebas " validación "

- **Pruebas de unidad** – Revisar las pequeñas cadenas manualmente (`"12345"`, `"9876543210"`, `"1111111111"`).
- ** Pruebas de tensión** – Random strings up to `10^5` digits; compare contra un algoritmo de fuerza bruta en un conjunto de datos reducido (`n ≤ 2000`) para validar la corrección.
* Casos de emergencia*
- Todos los dígitos iguales ( " 1111 " , " 2222 " , " 4444 " , " 7777 " ).
- Cuerdas que terminan con "0" (saltos de seguridad).
- Cadena aleatoria de longitud máxima (`1e5' dígitos).

-...

## 8. Conclusión

■ **Takeaway** – Un problema aparentemente “heavy” contando sobre todas las subestrings de un número decimal puede ser resuelto en tiempo lineal por:
■
■ 1. Digitos de agrupación por * propiedades de divisibilidad matemática*.
■ 2. Utilizando **prefijo de los restos** y tablas de frecuencia cortas.
■ 3. Escaneando una vez, computando cada contribución en tiempo constante.
■
■ Este enfoque se aplica igualmente bien a otros controles de divisibilidad (por ejemplo, " n % 11 " , " n % 13 " ) - sólo el período de ciclo y el cambio de tabla inversa.

■ ¿Por qué deberías recordar esto?
■ El mismo patrón aparece en muchos problemas de entrevista:
■ *Reducir el problema a un pequeño espacio estatal (prefijo restante + posición) y utilizar un mapa de frecuencia para acumular cuenta. *

-...

■ ¡Feliz codificación!
■ Si te gustó esta solución, dale un 👍 en GitHub o deja caer un ⭐ en el repositorio.
■ *Feliz codificación – y que sus números siempre sean divisibles! *