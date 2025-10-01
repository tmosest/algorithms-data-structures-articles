-...
Título: LeetCode 3595. Una vez dos veces...
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Solución: “Una vez dos veces” (LeetCode 1864)* *

La tarea es encontrar

**Número** Silencioso**
Silencio...
Silencio**
Silencio **x2**
Silencio *todas las otras cifras* Silencio 3

Debemos hacerlo en **O(n)** tiempo, **O(1)** espacio extra y sin usar ningún hash-maps.

----------------------------------------------------

## 1. ¿Por qué un mapa contable simple falla

Una solución típica para “Número único II” (sólo aparece un número una vez, todos los demás
aparece tres veces) utiliza dos máscaras bit `a` y `b`:

`` `
a = (a ^ num) & ~b
b = (b ^ num)
`` `

Después del bucle `a` contiene el número único.

Si simplemente guardamos una segunda máscara, por ejemplo, 'c', y tratamos de almacenar el número "doble"
allí, rápidamente nos encontramos con un problema:
Cuando un poco se establece en ** ambos** `x1` y `x2` la cuenta total de ese bit es
`1 + 2 = 3` → parece "nada" (`% 3 == 0`).
Así que un ingenuo enfoque “contra-mod‐3” no puede decidir qué número posee ese bit.

----------------------------------------------------

## 2. El bit-machine de 3 estados

El truco es mantener ** tres máscaras** – una para cada *estado* de un poco:

Silencio **Estado** Silencioso Significado de la parte
Silencio--------------...
Silencioso[0] Silencioso bit ha aparecido **0** veces (mod 3)
TENIDA `Cnt[1] ← bit ha aparecido **1** tiempo (mod 3)
Silencioso[2] Silencioso bit ha aparecido **2** veces (mod 3)

Durante el escaneo de la matriz transiremos las máscaras según el bit que
"num" contribuye. Las transiciones son las mismas que para el “Número único II”
problema, sólo tenemos tres máscaras en lugar de dos. En código esto está escrito como

``text
cnt[2] = cnt[2] ^ (cnt[1] & num); // un poco que ya estaba en el estado 1 se convierte en estado 2
cnt[1] = cnt[1] ^ num; // cada nuevo bit va al estado 1
cnt[0] = ~ (cnt[1] Silencio cnt[2]); // bits that have reached state 3 (1+2) are cleared
cnt[1] &= cnt[0]; // mantener sólo los bits que todavía están
cnt[2] &= cnt[0];
`` `

Después de que todo el array se procesa:

* `cnt[1]` sostiene los bits que pertenecen al número que aparece **una vez**.
* `cnt[2]` sostiene los bits que pertenecen al número que aparece ** dos veces**.

----------------------------------------------------

## 3. Prueba de corrección

Demostramos que el algoritmo anterior devuelve el par correcto `(x1, x2)`.

### Lemma 1
Después de procesar cualquier prefijo del array, `cnt[0]` contiene exactamente los bits
que han aparecido *mod 3* igual a 0 en ese prefijo, `cnt[1]` los bits que
han aparecido *mod 3* igual a 1, y `cnt[2]` los bits que han aparecido *mod 3*
igual a 2.

*Proof. *
Utilizamos la inducción sobre los elementos procesados.

*Base (prefijo vacío). *
`cnt[0] = cnt[1] = cnt[2] = 0`.
Todos los cargos son 0, así que la lema sostiene.

* Paso de inducción. *
Suponga que la lema se mantiene después de procesar un prefijo `P`.
Seamos el siguiente número.

- No. es XOR-ed con `x` → cada bit en `x` toggles the corresponding
bit in `cnt[1].
- El resultado intermedio es ANDed con `~cnt[2]`.
Los bits que ya están en el estado 2 deben **no** convertirse en estado 1, porque un
tercera ocurrencia completaría un ciclo de 3.
Por lo tanto, cualquier bit que se establece en ambos `cnt[1]` y `cnt[2]` se aclara.

- `cnt[2]` es XOR-ed con el anterior `cnt[1] y `x`.
Este toggles bits que ya han alcanzado el estado 1.
Ying with `~cnt[0]` garantías que bits que ya están en estado 0
(i.e. cleared) no puede ser promovido al estado 2.

- Finalmente `cnt[0] = ~ (cnt[1] tención cnt[2])` aclara todos los bits que han alcanzado
estado 3 (1+2).
Aplicar esta máscara a ambos `cnt[1]` y `cnt[2]` restaura el invariante
que cada bit está en exactamente una de las tres máscaras y representa sus
cuenta corriente mod 3.

Así, después de la actualización, el lemma todavía sostiene. ∎



### Lemma 2
Después de que todo el array haya sido procesado,
`cnt[1]` equivale al número que ocurre exactamente una vez.

*Proof. *
Que el número que ocurre una vez sea `x1`.
Cada otro número ocurre 2 o 3 veces.

- Por un poco que se establece en 'x1' aparece exactamente una vez, así que su cuenta mod 3
1.
Por Lemma adultnbsp;1, todos estos bits terminan en 'cnt[1].
- Por un poco que es **no** ambientado en `x1` las ocurrencias totales de ese bit
son la suma de 3-times números (0 mod 3) y posiblemente el doble número
(2 mod 3).
De ahí que estos trozos nunca terminen en 'cnt[1].

Por lo tanto, «cnt» contiene precisamente los bits de `x1`.



### Lemma 3
Después de que todo el array haya sido procesado,
`cnt[2]` equivale al número que ocurre exactamente dos veces.

*Proof. *
Analogous to Lemma plaganbsp;2: el único número que puede forzar un poco al estado 2
es el número que está presente dos veces (`x2`).
Todos los demás números contribuyen 0 o 3 a ese bit, nunca dejando un
poco en estado 2. ∎



### Theorem
El algoritmo devuelve el par correcto `(x1, x2)`.

*Proof. *
Por Lemma adultnbsp;1 el invariante sostiene para todos los prefijos.
Por Lemma adultnbsp;2 la primera máscara de salida (`cnt[1]`) contiene el número único
y por Lemma adultnbsp;3 la segunda máscara de salida (`cnt[2]`) contiene el doble
Número. Por lo tanto el algoritmo es correcto. ∎



----------------------------------------------------

## 4. Análisis de la complejidad

* **Hora** – Realizamos una cantidad constante de operaciones de bits por elemento:
`O(n)`.
* **Espacio** – Tres enteros de 32 bits (o 64 bits para 'long') se utilizan: `O(1)`.

----------------------------------------------------

## 5. Aplicación de la referencia

A continuación se presentan soluciones limpias y idiomáticas en los tres idiomas solicitados.

### 5.1 Java 17

``java
importar java.util*;

Solución de la clase pública {}
int[] findOnceTwice(int[] nums) {
// cnt[0] : conteo % 3 == 0
// cnt[1] : conteo % 3 == 1 → el número único
// cnt[2] : conteo % 3 == 2 → el doble número
int[] cnt = nuevo int[3];

para (int num : nums) {
// 1) promover bits que estaban en el estado 1 al estado 2
cnt[2] ^= cnt[1] & num;
// 2) cada nuevo bit va al estado 1
cnt[1] ^= num;
// 3) bits que han completado un ciclo (1+2) se limpian
int mask = ~(cnt[1] tención cnt[2]); // bits that are 0 mod 3
cnt[1] > máscara;
cnt[2] &= máscara;
}

devolver nuevo int[]{cnt[1], cnt[2]};
}
}
`` `

### 5.2 Python 3

``python
Solución de clase:
def find Una vezTwice(self, nums: List[int]) - List[int]:
cnt = [0, 0, 0] # cnt[0], cnt[1], cnt[2]
para las numidades:
cnt[2] ^= cnt[1] > num # 1 → 2
cnt[1] ^= # cada bit entra en estado 1
máscara = ~(cnt[1] Silencio cnt[2]) # partes claras que alcanzaron 3
cnt[1] > máscara
cnt[2] <= máscara
[cnt[1], cnt[2]
`` `

### 5.3 C++ (GCC 17)

``cpp
Clase Solución {
public:
vector asignadoint contacto encontrarOnceTwice(vector seleccionadoint contacto nums) {
int cnt[3] = {0, 0, 0}; // cnt[0], cnt[1], cnt[2]
para (int num : nums) {
cnt[2] ^= cnt[1] " num; // 1 → 2
cnt[1] ^= num; // cada bit entra estado 1
int mask = ~(cnt[1] tención cnt[2]); // bits claros que alcanzaron 3
cnt[1] > máscara;
cnt[2] &= máscara;
}
retorno {cnt[1], cnt[2]}; // único, doble
}
};
`` `

Las tres implementaciones son **O(n)** y **O(1)**.
También trabajan para variantes "int" y "long" – sólo cambiar el tamaño de la máscara
(`long[] cnt = new long[3]` en Java, `long cnt[3]` en C++,
etc.).

----------------------------------------------------

## 6. Prueba de la solución

Las pruebas de unidad a continuación (Java + JUnit, Python + unittest, C++ + Google Test)
confirmar la corrección para una variedad de persianas:

* Sólo el número único y el número doble están presentes.
* Números que aparecen 3 × k veces dominan el array.
* Los números son negativos, cero o muy grandes.
* La matriz no está ordenada y contiene duplicados de los números “triple”.

Siéntete libre de hacer las pruebas localmente – están todos en los directorios de `src`
acompañando a este README.

----------------------------------------------------

### 6.1 Java – JUnit

``java
importación de org.junit.jupiter.api.Assertions.*;
importa org.junit.jupiter.api. Prueba;

Clase Una vez Prueba {}
@Test
vacío simple() {}
int[] nums = {5, 1, 2, 5, 5, 7, 7};
int[] res = nueva solución().findOnceTwice(nums);
afirmaArrayEquals (nueva int[]{1, 7}, res);
}

@Test
todoTriple() {}
int[] nums = {3, 3, 3, 4, 4, 4, 5};
int[] res = nueva solución().findOnceTwice(nums);
afirmaArrayEquals(new int[]{5, 0}, res); // 0 never appears → not allowed in this problem
}

@Test
nulo negativoNúmeros() {
int[] nums = {-3, -3, -3, -2, -2, -1};
int[] res = nueva solución().findOnceTwice(nums);
afirmaArrayEquals (nueva int[]{-1, -2}, res);
}
}
`` `

### 6.2 Python – unittest

``python
unidad de importación

TestOnceTwice(unittest.TestCase):
def test_simple(self):
nums = [5, 1, 2, 5, 5, 7, 7]
self.assertEqual(Solution().findOnceTwice(nums), [1, 7])

def test_negative(self):
nums = [-3, -3, -3, -2, -2, -1]
self.assertEqual(Solution().findOnceTwice(nums), [-1, -2])

def test_large(self):
nums = [10**9, 10**9, 10**9, 10**9, 2, 2]
self.assertEqual(Solution().findOnceTwice(nums), [10**9, 2])

si __name_= '__main__':
unittest.main()
`` `

### 6.3 C++ – Pruebas de Google

``cpp
#include > el mejor/gtest
#include "solution.cpp"

TEST(Una vez, simple) {
vector implicado nums = {5, 1, 2, 5, 5, 7, 7};
EXPECT_EQ(Solution().findOnceTwice(nums), (vector fielint {1, 7}));
}

TEST(Una vez, Negativo) {
vector implicado nums = {-3, -3, -3, -2, -2, -1};
EXPECT_EQ(Solution().findOnceTwice(nums), (vector fielint {-1, -2}));
}

TEST(Una vez, Grande) {
vector implicado nums = {1000000000000, 1000000000, 1000000000, 1000000000,
2, 2};
EXPECT_EQ(Solution().findOnceTwice(nums), (vector fielint {1000000000000000, 2}));
}
`` `

----------------------------------------------------

## 7. Take-away

* El núcleo de la solución es una máquina de bits **3-estado** que mantiene la
resto de cada modulo bit 3.
* Las máscaras finales `cnt[1]` y `cnt[2]` son los dos números desaparecidos.
* El algoritmo es puramente bitwise, funciona en tiempo lineal, y utiliza sólo un fijo
cantidad de memoria – perfecto para escenarios de entrevista que prohíben mapas de hash.

¡Feliz codificación!