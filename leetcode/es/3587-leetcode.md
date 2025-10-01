-...
Título: LeetCode 3587. Cierre Adyacente Mínimo a la Paridad Suplente -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Sucursales mínimos a la paridad alternativa
**El Bien, el Mal y el Ugly – Una Guía completa para su próxima entrevista de codificación* *

■ **Keywords**: Leetcode, entrevista, algoritmo, paridad, intercambios adyacentes, entrevista de codificación, Java, Python, C++, entrevista de trabajo, ingeniería de software

-...

## 1. Por qué este problema se mete en su sueño

- **Tema de entrevista clásica**: Prueba su capacidad para razonar sobre *paridad*, * índices* y *movimiento óptimo*.
- **Hora de complejidad del tiempo**: La solución óptima es *O(n)*, pero muchos candidatos comienzan con una fuerza bruta *O(n2)*.
- Maneje por caso. El problema te obliga a pensar en *imposibilidad* (`-1`), *cuenta igual* y *objetivos válidos múltiples*.
- **Multilingual**: Puede presentar soluciones en Java, Python o C++ – perfectas para una cartera de poliglotas.

-...

## 2. Declaración de problemas (LeetCode 3587)

Se le da un array 'nums' de enteros distintos. En una operación puede cambiar **cualquier dos elementos adyacentes**.

Un arreglo es **válido** si cada par de elementos vecinos tiene una paridad diferente (uno es incluso, el otro extraño).

**Retorno** el número mínimo de swaps adyacentes requeridos para transformar `nums` en *cualquier arreglo válido.
Si es imposible, devuelve `-1`.

■ *Examples*
[2,4,6,5,7]
[2,4,5,7]
[1,2,3] " → "
[4,5,6,8]` → `-1`

-...

## 3. Intuición – El Trick de “Indice de la Odd”

1. **Colectar los índices** de todos los números y todos los números impares.
2. Una matriz *válida* debe alternar la paridad, por lo que los recuentos de los uniformes y las probabilidades pueden diferir en la mayoría de uno.
*Si ‘resistentes’ – probabilidades de vivir 1` → imposible → retorno `-1`*.
3. Hay ** en la mayoría de dos** patrones válidos:
* Comenzar con incluso → incluso ocupan índices `0,2,4,...`
* Comienza con probabilidades → las probabilidades ocupan índices `0,2,4,...`
4. Para un patrón dado, el número de swaps equivale a la suma de *distances* cada elemento debe moverse para alcanzar su índice de destino.
¿Por qué? Porque cada intercambio adyacente mueve un elemento por exactamente una posición.

■ #Key Fórmula #
■ Si tienes una lista de índices originales y los quieres en los índices de destino `0,2,4,...` (elementos ' k ' )
■ el costo es ``.

-...

## 4. Algorithm (O(n) time, O(1) extra space)

``text
1. Construir dos listas: inclusoIdx, oddIdx.
2. Si ←evenIdx sobre la vida - ←oddIdx sobre la vida
3. Inicializar los ans = INF.
4. Si inclusoIdx puede ocupar incluso posiciones → ans = min(ans, cost(evenIdx)).
5. Si oddIdx puede ocupar incluso posiciones → ans = min(ans, cost(oddIdx)).
6. Devuélvete el culo.
`` `

*`cost(list)`* implementa la fórmula de distancia.

-...

## 5. Código de referencia

## 5.1 Java (LeetCode-style)

``java
importar java.util*;

Clase Solución {
// Helper: sum of distances to target indices 0,2,4,...
costo privado largo (Lista seleccionadaInteger título) {
swaps largos = 0;
para (int i = 0; i) i++) {
swaps += Math.abs(pos.get(i) - 2L * i);
}
cambios de retorno;
}

public int minSwaps(int[] nums) {
Lista realizadaInteger aun = nuevo ArrayList implicado();
Lista realizadaInteger extraño = nuevo ArrayList implicado();

para (int i = 0; i)
(nums[i] % 2 == 0) even.add(i);
(i);
}

si (Math.abs(even.size() - odd.size()) 1) retorno -1;

Ans largos = largo. MAX_VALUE;

si (even.size() >= odd.size()) ans = Math.min(ans, cost(even));
si (odd.size() √= even.size()) ans = Math.min(ans, cost(odd));

retorno (int) ans;
}
}
`` `

■ ¿Por qué tanto? #
■ Cada costo de intercambio puede ser hasta `n`, y resumir hasta `n` swaps da `O(n2)` en el peor de los casos. `long` protege contra el desbordamiento por `n = 105`.

-...

### 5.2 Python 3

``python
de la importación Lista

Solución de clase:
def minSwaps(self, nums: List[int] int:
# Posiciones de los (odds) y ceros (evens)
odd_pos = [i for i, v in enumerate(nums) if v ' 1]
n = len(nums)

# Helper: costo cuando el patrón de inicio es 'start' (0 o 1)
def count_swaps(start: int) - int:
devolver suma(abs(p - (start + 2 * i))) para i, p en enumerate(odd_pos))

Prueba de imposibilidad rápida
m = 2 * len(odd_pos)
si m < n o m > n:
retorno -1

si m == n: # igual cuenta - probar ambos comienza
retorno min(count_swaps(0), count_swaps(1))
si m == n + 1: # probabilidades > evens – debe comenzar con extraño
recuento_swaps(0)
si m == n - 1: # pares de probabilidades - debe comenzar con
recuento_swaps(1)

retorno -1
`` `

■ **Nota**: Los enteros de Python están sin límites, así que no nos preocupamos por el desbordamiento.

-...

### 5.3 C++ (Fast & Clean)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
largo costo(contre vector consignaint confianza &pos) {
cinturones largos = 0;
para (size_t i = 0; i) ++i) {
swaps += llabs(pos[i] - 2LL * i);
}
cambios de retorno;
}
public:
int minSwaps(vector fielint círculo nums) {
vector implicado incluso, extraño;
para (int i = 0; i) ++i) {
(nums[i] % 2 == 0 ? even : odd).push_back(i);
}

si (abs(int)even.size() - (int)odd.size())) 1) retorno -1;

ans largos = LLONG_MAX;

si (even.size()  Conf= odd.size()) as = min(ans, cost(even));
si (odd.size() √= even.size()) ans = min(ans, cost(odd));

volver estática_cast seleccionado(ans)
}
};
`` `

-...

## 6. Análisis de la complejidad

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio.
Silencio **Hora** Silencio O(n) Silencio O(n) Silencioso
TEN **Auxiliary** ANTERI O(1) (excepto las listas de entrada)
tención **Espacio** Silencio O(1) Silencio O(1) Silencio

■ **¿Por qué es O(1)? * *
■ Sólo conservamos los índices originales en dos *listas* – igual que el tamaño de entrada. Una vez calculamos el costo que descartamos las listas, por lo que el espacio *extra* es constante.

-...

## 7. Las partes “Bad” – Pitfalls comunes

Silencio Pitfall Silencio Por qué Sucede
Silencio...
Silencio **Pensando en `-1` como un índice especial** Silencio Algunos candidatos tratan `-1` como un centinela y lo utilizan accidentalmente en cálculos de distancia. tención Realizar el cheque imposible **antes** costos de cálculo. Silencio
Silencio **Uso de índices basados en 1** Silencio La fórmula de costo se basa en índices basados en 0 (`0,2,4,...`). Los errores fuera de lugar por uno rompen todo. Pruebe ambos patrones explícitamente ( " arranque = 0 " o " arranque = 1 " ). Silencio
Silencio **Asumiendo que ambos patrones son siempre válidos** Silencio Si los recuentos difieren por uno, sólo un patrón es legal. TENCIÓN UTILIZACIÓN " = " cheques al decidir qué costo calcular. Silencio
Silencio ** Desbordamiento de distancias** Silencio Summing `n` distancias pueden llegar a 105 × 105 = 1010, que supera la int de 32 bits. ¦ Utilizar enteros de 64 bits (`long` en Java, `long' en C+++, predeterminado `int' en Python). Silencio

-...

## 8. Lista de verificación Edge‐Case

Escenario tóxico Qué hacer para probar
Silencio------------
Silencioso **Todavías** Silencioso `[2,4,6] → `-1`
Silencioso **Todas las probabilidades** Silencioso `[1,3,5]` → `-1`
Silencio **Cuenta igual** Silencio `[2,1,4,3]` - debe devolver `0` (ya válida). Silencio
Silencio *Un extra extraño* – debe comenzar con extraño → costo `0`. Silencio
Silencio **Un extra incluso** Silencioso `[2,1,3]` - debe comenzar con incluso → costo `0`. Silencio
Silencio **Large alternancia** Silencioso `[2,4,6,8,9,11,13,15]` - rendimiento de prueba para 105 elementos. Silencio

-...

## 9. Consejos de entrevista – Cómo hacer realidad esta pregunta

1. **Explicar la imposibilidad pronto**.
“Si la diferencia en las cuentas es mayor que una, no existe un arreglo válido. ”
Esto te muestra leer la declaración del problema a fondo.

2. ** Dibuja un diagrama** de índices.
Incluso índices → `0,2,4,...` e índices Odd → `1,3,5,...`.
Las ayudas visuales convencer a los entrevistadores de que puede razonar en papel.

3. **Hablar sobre el costo como distancia**.
“Cada intercambio adyacente mueve un elemento un paso. Así, el número mínimo de swaps equivale a la distancia total que los elementos tienen que viajar. ”

4. **Edge-case walk-through**.
Demostrar que el algoritmo funciona para ambos patrones y por qué necesitamos la 'min' sobre ellos.

5. **Tiempo & espacio**.
“O(n) tiempo porque sólo cruzamos la matriz un número constante de veces, y espacio O(1) porque sólo guardamos algunos contadores. ”

6. **Bonus** – Hablar sobre * swaps inestables vs.*.
Dado que todos los elementos son distintos, el orden relativo de elementos de la misma paridad no importa.

-...

## 10. Resumen – Lo que debe recordar

- ** Índices de color** → `evens` ' `odds`.
- **Comprobar viabilidad** → `vivinevens - odds habits = 1`.
- **Computa dos costes posibles** → ``Vista a la vida[i] - 2*i.
- **Tome el mínimo** → esa es la respuesta.
- Retorno `-1' si es imposible.

■ **Practice**: Intente modificar el problema:
■ *¿Y si pudiera cambiar dos elementos (no sólo adyacentes)? *
■ *¿Y si el array tenía duplicados? *
■ Esto profundizará su comprensión del concepto de paridad-índice.

-...

## 11. Pensamiento Final - Girar Esto en una habilidad de seguridad de trabajo

Problemas de LeetCode como 3587 son *micro-proyectos* que muestran a un candidato:

- Agudización algorítmica
- Fluencia de codificación en varios idiomas
- Atención a casos de borde
- Capacidad para comunicar ideas claramente

Añadir los fragmentos de código (Java, Python, C++) a tu cartera, blog sobre los aspectos “bueno, malo, feo” y práctica explicando el problema en voz alta. Los entrevistadores aman a los candidatos que *no sólo resuelven el problema sino que también articulan su proceso de pensamiento. *

■ **Siguientes pasos**
■ 1. Cierre este repo y añadir pruebas de unidad para todos los casos de borde.
■ 2. Poner la solución en GitHub con un README claro.
■ 3. Compartir el blog en LinkedIn/Medium con la etiqueta #CodingInterview.
■ 4. Siga refinando: pida a los pares que revisen su código y critican las explicaciones.

Buena suerte en tu próxima entrevista – ¡tienes esto!