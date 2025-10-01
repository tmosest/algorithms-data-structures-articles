-...
Título: LeetCode 2584. Dividir el Array para hacer productos Coprime -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. El problema (LeetCode 2584)

■ **Split the Array to Make Coprime Products* *
■ *Hard*

Se le da una matriz de enteros de 0-indexed `nums` de longitud `n`.
Una división en el índice `i' ( `0 ≤ i ≤ n‐2` ) es **válido**

`` `
producto(nums[0 ... i]) y producto(nums[i+1 ... n-1])
`` `

son coprime (`gcd == 1`).
Devuélvete el más pequeño como yo, o `-1' si no existe división.

`` `
nums = [4, 7, 8, 15, 3, 5] → respuesta = 2
`` `

`1 ≤ 104`, `1 ≤ nums[i] ≤ 106`.

-...

## 2. La visión básica

Dos productos son coprime **iff** ningún factor principal aparece en * ambas partes*.
Así que una división es imposible cuando un primo que aparece en el prefijo
también aparece más tarde en el sufijo.

*Idea*

* Por cada factor principal " p " , recuerde el índice **último** donde aparece la " p " .
* Mientras que el escaneo de izquierda a derecha siga el **más** último índice
entre todos los primos vistos hasta ahora.
Si el índice actual es igual a este índice más lejano,
no visto en el prefijo aparece más tarde → división en `i` es válida.

Esto da un algoritmo **O(n log M)** (`M = 106`) después de un tamiz lineal.



-...

## 3. Algoritmo (Código Pseudo)

`` `
construir SPF[1 ... 1_000_000] // Factor Primer más pequeño

// 1er paso: registro último índice de cada primo
lastIndex[p] = -1
para i = 0 ... n-1
para cada p de nums[i] (utilizando SPF)
lastIndex[p] = i

// 2do paso: barrido para encontrar división
más lejos = 0
para i = 0 ... n-2
para cada p de nums[i]
furthest = max(furthest, lastIndex[p])
si l == furthest // todos los primos en prefijo terminado aquí
Regreso
retorno -1
`` `

*Los primos distintos* se obtienen dividiendo repetidamente por el SPF hasta el
el factor actual desaparece.
Los bucles interiores funcionan en `O(número_de_distinct_primes)`. –
a la mayoría ~7 para cualquier número ≤ 106.

-...

## 4. Aplicación

A continuación se encuentran soluciones de trabajo, listos para pasar en **Java**, **Python**, y **C+**.

■ **Tip** – Para la programación competitiva o el uso de entrevistas, pre-computa el
Ø Sieve una vez y reutilizarlo en los casos de prueba.

-...

#### 4.1 Java

``java
importar java.util*;

Solución de la clase pública {}
int final estático privado MAX = 1_000_000;
int final estático privado[] spf = nuevo int[MAX + 1];

Estática
/ / sieve lineal para el factor primario más pequeño
para (int i = 2; i)= MAX; i++) spf[i] = i;
para (int i = 2; i * i)= MAX; i++) {
si (spf[i] == i) { // Soy el mejor.
para (int j = i * i; j)
si (spf[j] == j) spf[j] = i;
}
}
}
}

/** devolver los distintos factores principales de x utilizando la matriz de spf */
Lista estática privada realizadaInteger ratio factorize(int x) {
Lista de datos:Integer confianza res = nuevo ArrayList correctamente();
(x нель 1) {
int p = spf[x];
res.add(p);
mientras (x % p == 0) x /= p;
}
restitución;
}

int findValidSplit(int[] nums) {
int n = nums.length;
int[] lastIndex = nuevo int[MAX + 1];
Arrays.fill(lastIndex, -1);

// primer paso - última ocurrencia de cada primo
para (int i = 0; i)
para (int p : factorize(nums[i])) {}
lastIndex[p] = i;
}
}

// segundo paso – barrido
int furthest = 0;
para (int i = 0; i)
para (int p : factorize(nums[i])) {}
furthest = Math.max(furthest, lastIndex[p]);
}
si (i == más lejos) regresar i;
}
retorno -1;
}
}
`` `

-...

#### 4.2 Python

``python
importar matemáticas
de la importación Lista

MAX = 1_000_000
spf = lista(range(MAX + 1))

# linear sieve
para i en rango(2, int(MAX**0.5) + 1):
si spf[i] == i:
para j en rango(i * i, MAX + 1, i):
si spf[j] == j:
spf[j] = i

def factorize(x: int) - título List[int]:
""retorno de factores principales distintos de x usando spf""""
res = []
x √≥ 1:
p = spf[x]
res.append(p)
x % p == 0:
x //= p
retorno

def findValidSplit(nums: List[int] - int:
n = len(nums)
último = [-1] * (MAX + 1)

# 1st pass
for i, v in enumerate(nums):
para p en factorize(v):
último [p] = i

# 2nd pass
más lejos = 0
para i en rango(n - 1):
for p in factorize (nums[i]):
furthest = max(furthest, last[p])
si yo == más lejos:
Regreso
retorno -1
`` `

*Usage* (LeetCode signature)

``python
Solución de clase:
def findValidSplit(self, nums: List[int] int:
# el cuerpo de la función es idéntico al anterior
`` `

-...

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

const int MAX = 1'000'000;
int spf[MAX + 1];

void build_sieve() {
para (int i = 2; i)= MAX; ++i) spf[i] = i;
para (int i = 2; i * i) = MAX; ++i)
si (spf[i] == i)
para (int j = i * i; j)
si (spf[j] == j) spf[j] = i;
}

vector asignadoint edad factorize(int x) {
vector res;
(x нель 1) {
int p = spf[x];
res.push_back(p);
mientras (x % p == 0) x /= p;
}
restitución;
}

Clase Solución {
public:
int findValidSplit(vector fielint &nums) {
int n = nums.size();
vector estático implicado últimoIndex(MAX + 1, -1);

// 1er paso
para (int i = 0; i)
for (int p : factorize(nums[i])) lastIndex[p] = i;

// 2do pase
int furthest = 0;
para (int i = 0; i) {}
para (int p : factorize(nums[i]))
furthest = max(furthest, lastIndex[p]);
si (i == más lejos) regresar i;
}
retorno -1;
}
};
`` `

-...

## 5. The Blog Post

■ **Título (seo-friendly)* *
■ *Cómo resolver LeetCode 2584 – Dividir el Array para hacer productos Coprime*

A continuación se muestra un artículo completo de estilo marcado que se puede pegar en un
plataforma de blogs, Medium, o su propio sitio web.
Está escrito para ** principiantes** y **interviewees** mientras todavía contiene
la profundidad técnica que los entusiastas algoritmos anhelan.

-...

### 5.1 Introduction

■ ### ¿Qué es “Splitar el Array para hacer productos Coprime”?
■
■ LeetCode 2584 es un problema *Hard* que prueba su capacidad de trabajar con
√ Factorización principal, barridos de prefijo-suffix y sieves lineales.
■ En este artículo caminamos a través de la solución **optimal O(n log log M)**,
Por qué funciona, y cómo implementarlo en Java, Python y C++.

*Keywords:* LeetCode 2584, matriz dividida, productos coprime, factorización principal, tamiz lineal, análisis de algoritmos, preparación de entrevistas, desafío de codificación.

-...

### 5.2 Problema Restatement

■ ** Objetivo: ** Encontrar el índice más pequeño `i` para que
[0 ... i]) y `product(nums[i+1 ... n-1])' son coprime.
■ Si no existe tal `i`, regrese `-1`.

`` `
Entrada: nums = [4, 7, 8, 15, 3, 5]
Producto: 2
`` `

-...

## 5.3 Why It Looks Hard at First Glance

* Los productos pueden ser astronómicos grandes (`106`^104) – no se pueden multiplicar.
* Gcd de cálculo ingenua para cada posible división sería O(n2).
* La factorización repetida por división de ensayo es demasiado lenta para el límite superior.

-...

### 5.4 La "buena" visión

1. **Los productos son coprime ♥ No hay factor principal compartido** – reduce el problema
de aritmética a combinatoria.
2. **El último truco del índice** se convierte en un “¿Este primo aparece más tarde?” prueba
en un simple barrido lineal.
3. **Linear sieve** le da el factor primario más pequeño para cada número arriba
a `106` en `O(M)` tiempo y `O(M)` memoria – un costo de una sola vez.

■ ** Resultado**
■ *Tiempo:* `O(n log M)` (Ω O(n))
■ *Memory:* `O(M)` for the sieve + `O(M)` for the `lastIndex` array
■ *Práctico:* Funciona cómodamente dentro de los límites de LeetCode para 104 elementos.

-...

### 5.5 El lado "Bad"

Silencio Por qué importa
Silencio...
Silencio **Pintura de memoria** – La matriz SPF (`1 000 001` ints) es ~4 MB. Silencio Para entornos con 16 MB límite todavía está bien, pero es notable. Silencio
TEN **Factorización sobrecabezada** – Incluso con SPF, necesitas factorizar cada elemento dos veces. Silencio Todavía trivial para 104 elementos, pero puede ser un cuello de botella si utiliza un asedio más lento o una división de prueba ingenua. Silencio
Silencio ** Requisitos de alta definición** Confiamos en *distinct* primos; los primos duplicados son ignorados, pero un error en la factorización podría doble cuenta. La implementación cuidadosa evita esto. Silencio

-...

### 5.6 Las Alternativas Naïve “Ugly”

1. ** División de Trial por elemento (O(n √M)** –
Funciona para pequeñas entradas, pero fácilmente en '106`.
2. **Pre-computando todos los sets primos a través de un mapa de primos → lista de índices** –
Usa más memoria y más pases.
3. **Computing real products** and calling `gcd` – overflow and `O(n2)` time.

■ *Estas soluciones “muy” son grandes experimentos de aprendizaje, pero son
raramente lo que los entrevistadores o LeetCode esperan para un problema *Hard*. *

-...

### 5.7 Paso a paso con el ejemplo

`` `
nums = [4, 7, 8, 15, 3, 5]
índices: 0 1 2 3 4 5
`` `

Silencio i  tolera primes in nums[i] Silencio lastIndex[p] (updated) Silencio furthest Silencio
Silencio..
Silencio 0 Silencio {2} Silencio last[2] = 0 Silencio 0 Silencio
Silencio 1 Silencio {7} Silencio última[7] = 1 Silencio
Silencio 2 Silencio {2} Silencio last[2] = 2 Silencio 2
Silencio 3 Silencio {3,5} Silencio last[3] = 4, last[5] = 5 Silencio 5 Silencio

Mientras barre, después del índice **2** el último índice más lejano es **2**,
para que podamos dividirnos aquí.
(Primes `2` y `7` nunca aparecen de nuevo después de `i=2`.)

-...

## 5.8 Bloqueos completos de código (Ley a Pegar)

Silencio Idioma Silencio Nombre del archivo Silencio Función clave Silencio
Silencio------------------------------
TEN Java ANTE `Solution.java` ANTE `public int findValidSplit(int[] nums)` Silencio
Silencio Python Silencio `solution.py` Silencio `def findValidSplit(nums: List[int]) - confiar int:` Silencio
TENIDO C++ TENIDO `solution.cpp` TENIDO `int findValidSplit(vector interpretadointenta tener relaciones nums)`

■ Las tres versiones comparten la misma lógica lineal de sieve + barrido de dos pasos.

-...

## 6. Resumen

Silencio Lo que funcionó bien ← Qué cuidar para Silencio Dónde se pone desordenado
Silencio...
Silencio **Linear sieve** le da SPF en un solo paso. Silencio ** Memoria** – el array SPF es de 4 MB; aceptable pero no insignificante. ← Refactorizar cada número dos veces puede parecer pesado si no está usando SPF. Silencio
Silencio **El truco del último índice** convierte una limitación global en una zona local. ← **Problemas del edge** – debes parar en `n-2` porque la división necesita al menos un elemento en cada lado. ← Implementar la extracción primaria distinta incorrectamente (por ejemplo, olvidarse de saltar factores iguales) puede romper silenciosamente la lógica. Silencio
Silencio **La complejidad** – `O(n log log M)` con una pequeña constante. tención **Insectos de implementación** – errores fuera por uno, olvidando restablecer `más’ después de una división, etc. El algoritmo puede sentirse intuitivo al principio; un diagrama paso a paso ayuda. Silencio

■ **Bottom line:**
■ Si usted sabe cómo factorar los números rápidos (SPF) y hacer un seguimiento de la
■ *la última* posición de cada primo, el problema de división se colapsa a un simple
Escaneo lineal.
■ Este es el razonamiento exacto detrás del “más eficiente” oficial
■ Solución LeetCode para 2584.

-...

### 7. Lectura adicional " Recursos "

* [Esieve of Eratosthenes – Wikipedia](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)
* [Linear Sieve (Elias–Zaks algoritmo)](https://cp-algorithms.com/algebra/prime-sieve-linear.html)
* [GCD de Prefijo y Sufijo - Codeforces 1542C]
*Un problema relacionado que utiliza la misma idea de “último índice”. *

-...

## 7.1 Llamamiento final a la acción

■ ¡Pruébalo tú mismo! *
■ Escribe la solución en tu idioma favorito, ponla en contra de la
■ Leet Casos de prueba de código, y luego empujar su propio giro - por ejemplo, devolver el
Lista completa de todos los índices de división válidos.
■ Comparta su solución en GitHub y discuta sobre LinkedIn; la
La retroalimentación de la comunidad agudizará su razonamiento.

-...

■ *Feliz codificación, y buena suerte aplastando a LeetCode 2584! *

-...

**End of article. #

-...

**(Sea libre de adaptar encabezados, formato o estilo de lenguaje para que coincida con las expectativas de su audiencia.) * *