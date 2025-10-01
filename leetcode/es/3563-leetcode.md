-...
Título: LeetCode 3563. Lexicográficamente más pequeña después de la eliminación adyacente -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 3563 – Lexicográficamente La cuerda más pequeña después de la eliminación adyacente
■ **Hard tención 250 chars tención 250 letters* *

El problema:
Dada una cadena `s` (`1 ≤  vidas eternas ≤ 250`) que consiste en letras minúsculas, podemos eliminar repetidamente *cualquier par adyacente de letras que son consecutivas en el alfabeto (incluyendo el par circular `a‐z`). Después de todas las posibles eliminaciones, queremos la cadena resultante *léxicográficamente más pequeña*.

■ Ejemplo
> `s = "abc" → eliminar `"bc" → `"a" (mejor que podemos hacer)
√≥ `s = "bcda" → delete `"cd" → `"ba" → delete `"ba" →
√≥ `s = "zdce" → borrar `"dc" → `"ze" pero `"zdce" es lexicográficamente más pequeño, por lo que conservamos el original.

La clave es que *removiendo* un par puede exponer un nuevo par que se vuelve extraíble, pero eliminar un par también puede hacer una eliminación posterior imposible. Por lo tanto debemos considerar *todas* posibles secuencias de eliminación.

-...

## 1. La Idea – Programación Dinámica en Intervalos

Vamos.

`` `
dp[l][r] = la cadena lexicográficamente más pequeña que se puede obtener
de la subestring s [l ... r] (inclusive).
`` `

La respuesta es `dp[0][n‐1]`.

### Casos de base

* < > subestring vacío → cuerda vacía.
* `l == r` – carácter único – no se puede eliminar → el carácter mismo.

### Transition

Para una subestring `s [l ... r] tenemos dos opciones:

1. # Mantener el primer personaje #
`s[l]` + `dp[l+1][r]`.

2. **Remove `s[l] ' together with some `s[k]` (`l ' ilse k ≤ r`)**
Esto sólo es posible cuando:

* `s[l]` y `s[k]` son consecutivos (circularmente) → `isConsec(s[l], s[k]).
* El segmento *entire* entre ellos puede ser aclarado.
Eso es exactamente cuando `dp[l+1] [k-1] == ".

Si ambas condiciones se mantienen, después de borrar ese par el resto del
subestring is `dp[k+1][r]`.
Elegimos la cadena más pequeña entre todos esos candidatos.

Porque `las vidas subsisten ≤ 250`, un directo `O(n3)` El DP (o la recursión memoizada) funciona bien bajo un segundo.

-...

## 2. Cómo comprobar “consecutivo”

Por dos cartas " c1 " y " c2 "

`` `
diff = (c1 - 'a' - (c2 - 'a') + 26) % 26
`` `

`diff ' igual a `1` o `25` ↔ Las letras son consecutivas
(`a‐b`, `b-c`, ... o la circular `z-a`, `a-z`).

-...

## 2. Aplicación de las referencias

A continuación se presentan tres soluciones **completos, listas para la producción** – Java, Python y C++– que siguen la estrategia DP descrita anteriormente.
Todos los códigos compilan con los compiladores estándar:

* **Java** – `javac Solution.java Solución de java `
* **Python** – Solución de pitón3. py `
* **C+** – `g++ -std=c+17 -O2 solution.cpp " sensible ./solution `

-...

#### 2.1 Java 17

``java
importar java.util*;

Solución de la clase pública {}
privada String s;
privada int n;
privada String[][] memo;

public String lexicographically más pequeño(String s) {
esto.s = s;
this.n = s.length();
memo = nuevo String[n];
dp(0, n - 1);
}

privada String dp(int l, int r) {
si regresan ";
(l == r) return String.valueOf(s.charAt(l));

// Si guardamos el primer personaje
Criar mejor = s.charAt(l) + dp(l + 1, r);

// Trate de eliminar s[l] junto con algunos s[k]
para (int k = l + 1; k)
(isConsecutive(s.charAt(l), s.charAt(k)))) "
dp(l + 1, k - 1).isEmpty() {

candidato a la cadena = dp(k + 1, r);
si (candidato.compareTo(best) 0) mejor = candidato;
}
}
memo[l][r] = best;
devolver mejor;
}

booleano privado isConsecutive(char a, char b) {}
int diff = (a - 'a' - (b - 'a') + 26) % 26;
retorno diff == 1 TENIDO TENIDO TENIDO ENTRE LA FERENCIA == 25;
}

// --------------------------------------------------
// Arnés de prueba – se puede eliminar en la producción
// --------------------------------------------------
public static void main(String[] args) {
Solución sol = nueva solución ();
System.out.println(sol.lexicographicallySmallestString("abc")); // a
System.out.println(sol.lexicographicallySmallestString("bcda")); // (empty)
System.out.println(sol.lexicographicallySmallestString("zdce"); // zdce
System.out.println(sol.lexicographicallySmallestString("aab")); // a
System.out.println(sol.lexicographicallySmallestString("za")); // (empty)
}
}
`` `

-...

### 2.2 Python 3

``python
importa functools

Solución de clase:
def lexicographicallySmallestString(self, s: str) - Propiedad str:
n = len(s)

@functools.lru_cache(maxsize=None)
def dp(l: int, r: int) - Propiedad str:
si me iere r:
"Regresa"
si l == r:
retorno s[l]

1. Mantener el primer personaje
mejor = s[l] + dp(l + 1, r)

# 2. Trate de quitar s[l] con algunos s[k]
para k en rango(l + 1, r + 1):
si auto._consecutive(s[l], s[k]) y dp(l + 1, k - 1) == "":
cand = dp(k + 1, r)
si se puede hacer mejor:
mejor = cand
mejor

retorno dp(0, n - 1)

@staticmethod
def _consecutive(a: str, b: str) - confiar Bool:
diff = (ord(a) - ord(b) % 26
Retorno diff == 1 o diff == 25

# ----
# Uso del ejemplo
# ----
si __name_ == "__main__":
sol = Solución()
print(sol.lexicographicallySmallestString("abc")
print(sol.lexicographicallySmallestString("bcda") #
print(sol.lexicographicallySmallestString("zdce") # zdce
print(sol.lexicographicallySmallestString("aab") # a
`` `

-...

### 2.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
string lexicographically más pequeña (cadena s) {
int n = s.size();
vector realizador seleccionado(n));
para (int i = 0; i) no; ++i) memo[i] = string(1, s[i]);

for (int len = 2; len י= n; ++len) {}
para (int l = 0; l + len - 1  won n; ++l) {
int r = l + len - 1;
string best = s[l] + memo[l + 1][r];

para (int k = l + 1; k)
si (consec(s[l], s[k])) " memo[l + 1][k - 1].empty() {
cand = (k == r) ? " : memo[k + 1][r];
si (candúa) mejor = cand;
}
}
memo[l][r] = best;
}
}
memo [0][n - 1];
}

privado:
bool consec(char a, char b) const {
int diff = (a - 'a' - (b - 'a') + 26) % 26;
retorno diff == 1 TENIDO TENIDO TENIDO ENTRE LA FERENCIA == 25;
}
};

// ----
// Demo en principal – eliminar en producción
// ----
int main() {}
Sol de solución;
cout se realizó el sol.lexicographicallySmallestString("abc")
cout se realizó el sol.lexicographicallySmallestString("bcda")
cout se realizó el sol.lexicographicallySmallestString("zdce")
retorno 0;
}
`` `

Las tres implementaciones se ejecutan en la memoria `O(n3)` tiempo y `O(n2)`.
Con 'n ≤ 250' el peor número de operaciones es inferior a 16 millones – lo suficientemente rápido para el segundo límite.

-...

## 2. Lo que funciona bien – lo bueno

✔ ✔ Aspect Silencio
Silencio...
TENIDO TENIDO Silencio ** Corrección** – el DP explora cada camino de eliminación, garantizando el verdadero mínimo. Silencio
TENIDO TENIDO TENIDO **Simplicidad** – el código es una pequeña función recursiva más un pequeño ayudante, sin instrucciones de datos exóticas. Silencio
TENIDO ANTERIOR **Scalability** – `O(n3)` con `n = 250` es trivial para las CPU modernas. Silencio
TENIDO TENIDO ANTERIOR **Extensibilidad** – la misma plantilla DP se puede adaptar a muchos problemas de “removal-intervalo”. Silencio

-...

## 3. Donde Puede Fuego de Fuego – El "Bad"

Silencio ❌ ❌ Silencio
Silencio...
TENIDO ANTERIENTE TENIDO **Hora** – un ingenuo retroceso volaría (factorial) – el DP corta eso. Silencio
ANTE NOVEDAD ANTERIOR **Espacio** – una tabla de cuerdas memoizadas puede usar mucha memoria; guardamos las cuerdas de `O(n2)`, pero cada cuerda puede ser hasta 'n ' caracteres largos - todavía 0 × 250 Ω 60 kB. Silencio
TEN NOVEDAD TENED **Readability** – intervalo DP es un patrón clásico que puede no ser obvio para los recién llegados. Silencio

-...

## 4. Lo que no hicimos – El “Ugly”

* Un algoritmo codicioso de la pila-removal (pop cuando la corriente superior es consecutiva) hace *no* siempre dar la cuerda lexicográficamente más pequeña.
Funciona para el problema *clásico* “delete pares consecutivos adyacentes hasta que no haya pares”, pero el requisito aquí es *minimise* la cadena final, no para minimizar el número de eliminaciones.

* Una enumeración bruta-fuerza de todas las órdenes de eliminación es **exponencial** – completamente impráctico incluso para `las vidas eternas = 20`.

Así el intervalo DP es la solución más limpia y fiable.

-...

## 5. Pruebas del Código

← Intromisión esperada
Silencio...
Silencio
Silencioso `bcda` Silencio `''' Silencio `cd` → `ba` → `a` → `z` → nada
Silencio `zdce` Silencio `zdce` Silencio sin eliminación da una cuerda más pequeña
TENIENDO `Aab` TENIDO `A` Silencio mantener primero `a`, eliminar `ab` Silencio
Silencioso `za` Silencioso `'' Silencio
Silencio `az` Silencio `az` Silencio pareja no es consecutiva; nada puede ser borrado

Ejecute los arnés de prueba en cada archivo o utilice el corredor LeetCode en línea.

-...

## 6. Requisitos para entrevistas

1. ** Identificar la “interval”** – si la operación depende de un segmento contiguo, DP de longitudes es un ir-a.
2. ** El código “puede ser eliminado?”** como una función booleana (`esConsecutive`).
3. **Memoise** – evite la recomputación; en Java o Python use un array 2-D o `lru_cache`.
4. **Comparar cadenas léxicográficamente** – `` se realiza en todos los idiomas.

-...

## 6. SEO " Learning Notes

Este artículo está escrito para:

* **Programadores competitivos** buscando una solución DP limpia.
* ** Ingenieros software** preparándose para entrevistas de codificación (LeetCode, HackerRank).
* **Estudiantes** aprendiendo acerca del intervalo DP y la memoización recursiva.

No dude en adaptar el código de referencia a sus propios proyectos o materiales educativos.

¡Feliz codificación! 🚀

-...

**Keywords:** Java DP, eliminación de intervalos Python, recursión C++, cadena lexicográficamente más pequeña, letras consecutivas, entrevista de algoritmo, problema LeetCode, solución O(n3), intervalo DP tutorial.