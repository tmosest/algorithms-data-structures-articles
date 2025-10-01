-...
Título: LeetCode 1814. Contar buenos pares en un Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1814. Contar buenas parejas en un Array – Una solución completa, entrevista-Ley
*(Java fort Python Silencio C++)*

-...

## TL;DR
- **Problema** - Contar el número de pares de índices *(i, j)* con `i cautivar j` tal que
`nums[i] + rev(nums[j]) == nums[j] + rev(nums[i]).
- ¿Qué? La ecuación equivale a `nums[i] – rev(nums[i]) == nums[j] – rev(nums[j]).
- **Solución** – Computar el valor `d = nums[k] – rev(nums[k])` para cada elemento, almacenar la frecuencia de cada `d` en un mapa de precipitación, y contar `freq[d] elegir 2` pares.
- ** Complejidad** – `O(n)` tiempo, `O(n)` espacio extra (donde `n = nums.length`).
- **Modulo** – Todas las respuestas se toman modulo `1 000 007`.

-...

## 1. Recapitulación de problemas (de LeetCode)

■ Se le da un array 'nums' de enteros no negativos.
(x) es el reverso del entero.
■ Un par `(i, j)` es *nice* si `i '
[i] + rev(nums[j]) == nums[j] + rev(nums[i]).
■ Devuelve el número de pares agradables modulo `1 000 000 007`.

-...

## 2. Por qué funciona el truco de la “diferencia”

`` `
nums[i] + rev(nums[j]) == nums[j] + rev(nums[i]
[i] - rev(nums[i] == nums[j] - rev(nums[j]
`` `

*Proof* – Mueva los términos que contienen el mismo índice al mismo lado:

`` `
nums[i] - rev(nums[i]) = nums[j] - rev(nums[j])
`` `

Así dos índices forman un buen par **iff** sus *diferencias* son iguales.
Así que el problema se desploma para: *cuenta cuántos valores iguales de “diferencia” existen. *

-...

## 3. Algoritm

1. **Ayudador reverso** – convertir un entero a su forma inversa.
2. Por cada elemento " x " en " años "
* `d = x - rev(x)` (store in a `long`/`long` to avoid overflow).
* Incrementar el mostrador de `d` en un mapa de hash.
3. Después del escaneo, para cada diferente `d` con frecuencia `c` añadir
c * (c – 1) / 2` a la respuesta (modulo `MOD`).
4. Devuelve la respuesta.

-...

## 4. Código

### 4.1 Java (8+)

``java
importa java.util. HashMap;
importa java.util. Mapa;

Solución de la clase pública {}
static final long MOD = 1_000_000_007L;

public int countNicePairs(int[] nums) {
Mapa seleccionadoLong, Longilo freq = nuevo HashMap especificado();

para (int x : nums) {
d = x - inverso(x);
freq.merge(d, 1L, Long::sum);
}

ans largas = 0;
para (long c : freq.values()) {}
si (c л] {
as = (ans + (c * (c - 1) / 2) % MOD) % MOD;
}
}
retorno (int) ans;
}

privado inverso(int num) {
long rev = 0;
(num √≥ 0) {
rev = rev * 10 + num % 10;
num /= 10;
}
retorno rev;
}
}
`` `

### 4.2 Python 3

``python
Solución de clase:
MOD = 1_000_000_007

def countNicePairs(self, nums: List[int] int:
freq = {}
para x en nums:
d = x - self._rev(x)
freq[d] = freq.get(d, 0) + 1

ans = 0
para c en freq.values():
ans = (ans + c * (c - 1) // 2) % yo. MOD
Retorno

def _rev(self, num: int) - título int:
rev = 0
mientras que num:
rev = rev * 10 + num % 10
num //= 10
Retorno
`` `

#### 4.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int countNicePairs(vector fielmente unidos nums) {
const long MOD = 1'000'000'007LL;
unordered_map freq;

para (int x : nums) {
largo tiempo d = (largo largo)x - reverseNum(x);
++freq[d];
}

ans largos = 0;
para (auto &p : freq) {
largo c = segundo;
(c √≥1)
as = (ans + (c * (c - 1) / 2) % MOD) % MOD;
}
retorno (int)ans;
}

privado:
largo reversoNum(int n) {}
long long rev = 0;
y n) {
rev = rev * 10 + n % 10;
n /= 10;
}
retorno rev;
}
};
`` `

-...

## 5. Blog-Estilo Artículo: *El Bien, el Mal, y el Ugly of Counting Nice Pairs*

■ **Descripción (SEO)** - ¿Quieres aterrizar esa entrevista de codificación?
■ Master LeetCode 1814 “Count Nice Pairs” en Java, Python y C++!
■ Aprende el truco hash‐map, trampas y consejos de entrevista en el mundo real.

-...

## 5.1 El Bien - Lo que hace que este problema sea un Gold‐Mine

1. **La simplicidad de las matemáticas** – Una vez que note el truco de cancelación (`x - rev(x)`), todo el problema se colapsa a un recuento de frecuencia.
2. ** Alto rendimiento** – La solución O(n) funciona cómodamente para las máximas limitaciones (`10^5` números).
3. **Language‐agnostic** – La misma idea encaja en Java, Python, C++, Vaya, etc., para que pueda responder en cualquier idioma que prefiera el entrevistador.
4. **Great entrevista showcase** – Demonstrates:
- Capacidad para detectar simplificación algebraica.
- Uso adecuado de mapas de hash para contar.
- Manejo de grandes números con aritmética modular.

-...

### 5.2 Los malos – los saltos comunes y cómo evitarlos

Silencio Pitfall Silencio Por qué importa
Silencio...
Silencio **Using `int` for reversed values** tención Reversing 1 000 000 000 produces 1, which is fine, but intermediate multiplications (e.g., `rev * 10`) can overflow `int`. Silencio
Silencio **Neglecting the modulo** Silencio Aunque la respuesta está tapada, las sumas intermedias como `c * (c-1) / 2` pueden rebosar 64-bit si `c` es enorme (teóricamente hasta 10^5). tención Modulo Compute después de cada adición y elenco a `long'. Silencio
Silencio **No manipular ceros** Silencio `rev(0)` debe ser `0`, pero el bucle `mientras (num) `` saltará, por lo que debe manejar `num == 0` explícitamente. Silencio O inicialice `rev = 0` y utilice `mientras (num ≤ 0)` (que funciona), o caso especial cero. Silencio
tención **Using a plain array for frequencies** tención El valor de la diferencia puede ser negativo, por lo que un array indexado por `d` no es factible. Use un mapa/diccionario de hash keyed por `d`. Silencio
Silencio **Off‐by-one errors** Silencio Recuerde que los pares son *noordenados*: `(i, j)` y `(j, i)` son los mismos. La fórmula " c * (c-1)/2 " explica esto. tención Verifica con pequeños ejemplos. Silencio

-...

## 5.3 Los escenarios de Edge‐Case y los exámenes de “Tricky”

Silencio Test Silencio Esperado Respuesta Silencio ¿Por qué es complicado
Silencio...
Silencio `nums = [0, 0, 0]` Silencio 3 Silencio Todas las diferencias son cero; usted debe contar 3 pares. Silencio
TENIDO `nums = [100, 1]` TENIDO 0 ANTE `rev(100) = 1`, `rev(1) = 1`; diferencias: `99` y `0` → ningún partido. Silencio
Silencio `nums = [123456789, 987654321]` Silencio 1 Silencio Ambos tienen diferencias diferentes pero `rev` voltea el orden. Silencio
Silencio Valores muy grandes (cerca a `10^9`) Silencio Obras Silencio Garantizar que el reverso no se desborde. Silencio
Silencio Aleatoriamente sacudió la larga matriz Silencio Pase Silencio Rendimiento debe ser lineal. Silencio

-...

### 5.4 Interview‐ Friendly Talk‐ Pista

1. **Explicar la observación**: `nums[i] + rev(nums[j]) == nums[j] + rev(nums[i])` → `nums[i] - rev(nums[i]) == nums[j] - rev(nums[j])`.
2. **Declarar el enfoque**: calcular la “diferencia” para cada número, utilizar un mapa de hash para contar diferencias idénticas, luego utilizar la fórmula combinatoria.
3. **La complejidad de la luz**: O(n) time, O(n) space, factor constante minúscula.
4. ** Manejo del borde de fusión**: aritmética de 64 bits, modulo, ceros.
5. **Mostrar código**: Una aplicación concisa en el idioma de elección.
6. **Optional**: Discuss why we use `long` for `rev` and `difference`.

-...

### 5.5 Take-away

*La belleza de “Count Nice Pairs” reside en convertir una igualdad aparentemente compleja en un simple problema contable. Al dominar este truco no sólo resolver LeetCode 1814 de manera eficiente, sino también demostrar una poderosa mentalidad que los entrevistadores aman: ver el patrón subyacente, reducir a los básicos, e implementar limpiamente. *

-...

## 6. Lista de verificación final antes de su próxima entrevista

- [ ] **Explicar la simplificación de matemáticas** claramente.
- [ ] **Escribe un ayudante inverso** que trabaja para 0 y evita el desbordamiento.
- [ ] **Utilice un mapa de hash** ( < < > > > en Java, > > > > , > en Python.
- [ ] **Count pairs** con `c * (c-1) / 2` y aplicar modulo `1 000 000 007`.
- [ ] **Prueba con los casos de borde** (todos los ceros, números grandes, datos aleatorios).
- [ ] **Práctica la pista de hablar** para que puedas responder con confianza en 2-3 minutos.

¡Feliz codificación y buena suerte con esa entrevista! 🚀