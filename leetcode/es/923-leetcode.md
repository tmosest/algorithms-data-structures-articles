-...
Título: LeetCode 923. 3Sum Con Multiplicidad -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 3‐Sum With Multiplicity – LeetCode 923
**Java / Python / C++ – Solución completa + SEO‐Optimized Blog Post**

-...

################################################################################################################################################################################################################################################################ Lo que aprenderás

Silencio Sección Silencioso Lo que descubrirás
Silencio...
Silencioso Problema Declaración Silencioso El desafío de LeetCode “3‐Sum With Multiplicity”
Silencio ¿Por qué importa ← Una pregunta de entrevista común que prueba conteo, combinatoria y optimización TENCIÓN
confidencialidad Good & Bad ← Cómo una solución ingenua falla, y el elegante enfoque O(1012) que gana TEN
tención Ugly " Evitado  durable Pitfalls with integer overflow and modulo arithmetic TEN
TENIDO Código TENIDO Implementaciones limpias, preparadas para la producción en **Java, Python, C+** Silencio
Silencio SEO Boost Silencio Palabras clave, meta-tags & estructura para ayudarle a clasificarse en consultas de investigación de trabajo

■ **Keywords**: 3Sum Con Multiplicidad, LeetCode 923, algoritmo de entrevista, combinatoria, contando triples, modulo 1e9+7, solución Java, solución Python, solución C+++, entrevista de trabajo, entrevista de codificación.

-...

## 1. Declaración de problemas

■ **3Sum Con Multiplicidad**
■ *Medio*

■ **Función de la firma**
. ``java
" public int threeSumMulti(int[] arr, int target)
" `

■ **Given**:
■ - `arr ' - array entero, `3 0 = arrr.length
√≥ - `0 ' = arrr[i]
" Ejercer " , "
■
■ **Retorno** el número de índices triples `i cautivo j ' significa que
[i] + arr[j] + arrr[k] == target`.
■ Como la respuesta puede ser enorme, devuélvala modulo `1_000_000_007`.

■ *Examples*

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
Silencio `[1,1,2,2,3,3,4,4,5,5]`, `target = 8` Silencio `20` Silencio 8×(1,2,5) + 8×(1,3,4) + 2×(2,2,4) + 2×(2,3,3) Silencio
TENIDO `[1,1,2,2,2,2]`, `target = 5` TENIDO `12` TENIDO 2 maneras de elegir 1 y 6 formas de elegir la vida de dos
Silencio `[2,1,3]`, `target = 6` Silencio `1` Silencio Sólo (1,2,3)

-...

## 2. Por qué es una buena pregunta de entrevista

- ** Aspectos específicos**: manipulación de arrays, combinatoria, aritmética modular, intercambios temporales.
- ** Fácil de optimizar**: un bucle anidado triple es O(n3) – demasiado lento para `n = 3000`.
- **Mostrar creatividad algoritmo**: el uso de conteos de frecuencia y fórmulas combinatorias reduce la complejidad a O(1012).

-...

## 3. Pitfalls comunes (El lado “Ugly”)

Pitfall Silencio Por qué falla
Silencio...
Silencio **Naïve O(n3) bucles** tención 27 mil millones de operaciones → límite de tiempo excedido Silencio
Silencio **No manejo modulo** Silencio Integer desbordamiento o resultado final incorrecto
Silencio **Usando entradas de 32 bits para la combinatoria** Silencio `cuenta * (cuenta-1) * (cuenta-2)` se puede desbordar antes de la división
Silencio **Missing edge cases (i == j == k)** tención Factor combinatorio incorrecto: debe usar nC3 Silencio
Silencio ** Orden de Index** ← Necesidad `i < j ' → Cuidado con las fórmulas de conteo

-...

## 4. El enfoque “bueno” – Frecuencia + Combinatoria

Puesto que cada elemento está en `[0, 100]`, podemos reemplazar el array con una * tabla de frecuencia* de la longitud 101.
Entonces sólo necesitamos iterar sobre todos los pares posibles `(i, j)` con `i <= j`.
Para cada par computamos `k = target - i - j` y comprobar si `0 ' significa= k ' 100 ' .

### 4.1 3‐Caso Contando

TENIDO Condición TENIDO Cuantas triples ANTE Fórmula ANTE
Silencio--------------------------
[i], 3) = cnt[i] * (cnt[i]-1) * (cnt[i]-2) / 6 ` Silencio
TENIDO `i == j != k` ANTE Primeramente dos iguales, tercera diferente ANTE `C(cnt[i], 2) * cnt[k] = cnt[i] * (cnt[i]-1) / 2 * cnt[k] Silencio
* cnt[k] Silencio
TENIDO `i ANTERITO J == k` TENIDO Symmetric to previous, handled when loop reached `(j, j)` ANTE `cnt[i] * C(cnt[j], 2)` – esto está cubierto por el caso `i  interpretado j' observado k` cuando iteramos todas las combinaciones, pero evitamos la doble narración por sólo considerando `i <= j ' y aplicando el factor apropiado= k`. Silencio

Los bucles se ejecutan en la mayoría 101 × 101 = 10 201 iteraciones – insignificante en comparación con el tamaño de entrada original.

-...

## 5. Análisis de la complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio Construir tabla de frecuencias Silencio **O(n)** Silencio **O(101)**
Silencio Doble bucle sobre los valores de la vida **O(1012)**
Silencio **Total** Silencio **O(n + 1012) ♥ O(n)** Silencio**

`n` puede ser hasta 3000; el algoritmo es cómodamente rápido para todos los límites.

-...

## 6. Aplicación del Código

A continuación se presentan implementaciones limpias y de producción en **Java**, **Python**, y **C+**.
Todos usan la misma lógica basada en frecuencia y manejan aritmética modular de forma segura.

### 6.1 Java

``java
importar java.util*;

Clase Solución {
static final long MOD = 1_000_000_007L;

int threeSumMulti(int[] arr, int target) {}
largo[] cnt = nuevo largo[101]; // tabla de frecuencia
for (int v : arrr) cnt[v]++; // O(n)

resultado largo = 0L;

para (int i = 0; i) = 100; i++) {
si (cnt[i] == 0) continuar;
para (int j = i; j) {}
si (cnt[j] == 0) continuar;
int k = target - i - j;
si (k) 0 TENIDO TENIDO ANTE 100 TENIDO Cnt [k] == 0) continuar;

si (i == j ' t == k) { //
resultado += cnt[i] * (cnt[i] - 1) * (cnt[i] - 2) / 6;
} si (i == j) { // i=j!=k
resultado += cnt[i] * (cnt[i] - 1) / 2 * cnt[k];
} si (j == k) { // i=j=k
resultado += cnt[i] * cnt[j] * (cnt[j] - 1) / 2;
} más { / / / / toda diferencia
resultado += cnt[i] * cnt[j] * cnt[k];
}
resultado %= MOD;
}
}
Resultado de retorno (int)
}
}
`` `

### 6.2 Python

``python
Solución de clase:
MOD = 1_000_000_007

def threeSumMulti(self, arr: List[int], target: int) int:
# frecuencia de números 0.100
cnt = [0] * 101
por v en Arr:
cnt[v] += 1

res = 0
para i en rango(101):
si cnt[i] == 0:
continuar
para j en rango(i, 101):
si cnt[j] == 0:
continuar
k = target - i - j
si k > 0 o k > 100 o cnt [k] == 0:
continuar

si l == j == k:
res += cnt[i] * (cnt[i] - 1) * (cnt[i] - 2) // 6
elif i == j: i==j!=k
res += cnt[i] * (cnt[i] - 1) // 2 * cnt[k]
elif j == k: i)=j=k
res += cnt[i] * cnt[j] * (cnt[j] – 1) // 2
# Todos distintos
res += cnt[i] * cnt[j] * cnt[k]
res %= uno mismo. MOD
retorno
`` `

### 6.3 C++

``cpp
Clase Solución {
public:
const long MOD = 1'000'000'007LL;

int threeSumMulti(vector fieltro arr, int target) {}
cnt largo [101] = {0};
para (int v : arr) ++cnt[v];

ans largos = 0;
para (int i = 0; i) = 100; ++i) {}
si (!cnt[i]) continúan;
para (int j = i; j)
si (!cnt[j]) continúan;
int k = target - i - j;
si (k < 0 TENIDO TENED 100 TENIDO ANTETENIDO!cnt[k]) continúan;

si (i == j ' t == k) { //
as += cnt[i] * (cnt[i] - 1) * (cnt[i] - 2) / 6;
} si (i == j) { // i=j!=k
ans += cnt[i] * (cnt[i] - 1) / 2 * cnt[k];
} si (j == k) { // i=j=k
ans += cnt[i] * cnt[j] * (cnt[j] - 1) / 2;
} más { / / / / toda diferencia
ans += cnt[i] * cnt[j] * cnt[k];
}
as %= MOD;
}
}
volver estática_cast seleccionado(ans)
}
};
`` `

■ **Consejo**: En C++, utilice 'long' para cálculos intermedios para evitar el desbordamiento.

-...

## 7. Step‐by‐Step Walk‐through (Java)

``java
resultado largo = 0L;
para (int i = 0; i) = 100; i++) {
si (cnt[i] == 0) continuar; // saltar números no utilizados
para (int j = i; j) {}
si (cnt[j] == 0) continuar;
int k = target - i - j;
si (k) 0 TENIDO TENIDO ANTE 100 TENIDO Cnt [k] == 0) continuar;

si (i == j ' t == k) {
// Los tres índices apuntan al mismo número
resultado += cnt[i] * (cnt[i] - 1) * (cnt[i] - 2) / 6;
} si (i == j) {
// i y j son los mismos, k es diferente
resultado += cnt[i] * (cnt[i] - 1) / 2 * cnt[k];
} si (j == k) {
// j y k son los mismos, yo es diferente
resultado += cnt[i] * cnt[j] * (cnt[j] - 1) / 2;
. ♫ ... {
// i, j, k son todos distintos
resultado += cnt[i] * cnt[j] * cnt[k];
}
resultado %= MOD; // mantener el valor pequeño
}
}
`` `

Cada rama utiliza el factor combinatorio correcto:

- `C(n, 3)` cuando todo igual,
- `C(n, 2) * m` cuando dos son iguales,
- `n * m * p` cuando todo distinto.

-...

## 8. Validación de Edge‐Case

[0, 0, 0]`, `target = 0`
■ ** Resultado**: `C(3, 3) = 1` – sólo un triple `(0, 0, 0)`.

[50, 50, 50, 50] `target = 150`
■ ** Resultado**: `C(4, 3) = 4` – cuatro triples `(50,50,50)`.

-...

## 8.1 ¿Y si los números eran más grandes?

Si el dominio era más grande (por ejemplo, «int» valores hasta 105), el enfoque basado en la frecuencia todavía funciona pero requiere un *hash mapa* en lugar de un array de tamaño fijo.
La complejidad se convertiría en O(unique2).
Para las limitaciones de LeetCode, el dominio fijo 0–100 está garantizado, por lo que un array 101-length basta.

-...

## 8.2 ¿Y si quisiéramos todos los pedidos?

Si el requisito era triples * no ordenados* (cualquier orden de índices permitidos), las fórmulas contables cambian ligeramente (sin necesidad de `i <= j` restricción).
La solución presentada respeta naturalmente " i " J " , coincidiendo con la afirmación del problema.

-...

## 8.3 Real‐World Analogies

**Product inventory**: `cnt` is like stock levels; `(i, j, k)` are three items that sum to a target price.
- Paradoja de cumpleaños**: Contar combinaciones de valores idénticos es análogo a los cumpleaños de agrupación.

-...

## 8.4 Manejo de números muy grandes

Para idiomas con números enteros arbitrarios de precisión (por ejemplo, Python’s `int’), la división antes del modulo es segura.
En lenguajes de ancho fijo, siempre realizar la división *después* multiplicando para mantener los números pequeños.

-...

## 8.5 Preguntas de la entrevista común

1. **¿Puede explicar las fórmulas combinatorias? * *
*Respuesta*: `C(n,3) = n(n-1)(n-2)/6`, `C(n,2) = n(n-1)/2`.

2. ** ¿Por qué iteramos `j` de `i` a 100 en lugar de 0? #
*Respuesta*: Asegura que no tengamos parejas de doble cuenta y mantengamos `i > j ' .

3. **¿Cómo modificaría esto si los números pudieran ser negativos? * *
*Respuesta*: Cambie la tabla de frecuencias o utilice un `HashMap observadoInteger, Longilo`; todavía O(unique2).

4. **¿Qué pasa si `target` es enorme ( > 300 )? #
*Respuesta*: `k` se vuelve negativo → saltado; algoritmo naturalmente regresa 0.

-...

## 8.6 Pensamientos finales

- **Elegancia**: Reemplazar los valores con frecuencias convierte un problema aparentemente intratable O(n3) en un pequeño bucle O(10 k).
- **Scalable**: Funciona para cualquier 'n' ≤ 3000 sin afinación.
- Aritmética moderna Mantenga un modulo de funcionamiento para evitar el desbordamiento y coincida con la salida esperada de LeetCode.

Siéntase libre de copiar—pasar el código en su IDE favorito y ejecutar los casos de prueba proporcionados.

-...

## 8.7 Summary

← Pieza Silencioso Silencio
Silencio...
Silencioso ** Tabla de frecuencia** Silencio Comprende el array en 101 conteos
Silencio **Doble loop** Silencio Enumera todos los pares de valor `(i, j)` Silencio
Silencio **k computation** Silencio `k = target - i - j` peru
tención **Caso de manejo** tención 3 fórmulas combinatorias, sin doble conteo
Silencio **Modulo** Silencio Aplicado después de cada adición

Este es un ejemplo de libro de texto de convertir una idea de fuerza bruta en una solución *optimal*.

-...

## 8.8 “¿Qué-Si” Preguntas para la Exploración

1. ¿Qué pasa si "target" puede ser hasta 300? #
El algoritmo todavía funciona porque `k` puede ser negativo; simplemente saltamos esos casos.

2. **¿Podemos reducir aún más la complejidad? * *
No realmente – el doble bucle sobre los 101 valores ya es *O(1)* relativo a la entrada.

3. **Si los números eran de hasta 105, ¿podríamos seguir utilizando un array de frecuencia? * *
Sí, pero la tabla sería grande; un mapa de hash (`unordered_map`) y iterating sobre las teclas únicas todavía sería rápido.

4. **¿Podríamos usar técnica de dos puntos después de ordenar? * *
Dos puntos funciona para *distinct* sumas, pero el manejo de números iguales combinatorialmente es más simple con la tabla de frecuencias.

-...

## 8.9 Problemas de práctica

- LeetCode 1512** – *Agregar al borde del rayo de entero* (utilizar dos puntos).
- LeetCode 1675** – *Minimum Operations to Reduce X to Zero* (dos puntos + ventana deslizante).
- LeetCode 436** – *Encontrar Intervalo derecho* (búsqueda binaria + clasificación).

-...

## 8.10 Consejo de clausura

- **Understand the domain**: Constraints like `0 <= val ' = 100 ' open the door to frequency‐based optimizations.
- **Master combinatorial formulas**: `nC2`, `nC3` son tus amigos.
- **Aritmética modular de alta calidad** cuidadosamente: Use `long `/`long` y aplique `% MOD` después de cada adición.

¡Buena suerte sacudiendo esa entrevista! 🚀

-...

### FAQ

**Q**: *¿Y si el array de entrada contiene números negativos? *
**A**: La solución actual se basa en el dominio `[0,100]`. Para los negativos, utilice un `HashMap observadoInteger, Longilo` para almacenar frecuencias e iterar sobre todos los pares clave. La complejidad se convierte en O(unique2).

**Q**: *¿Podemos pre-computar factoriales para combinaciones? *
**A**: Con pequeñas cuentas fijas, las fórmulas directas son más simples y evitan los arrays factoriales.

**Q**: *¿Por qué no usar ints de 32 bits en Python? *
**A**: Las ints de Python son de apreciación arbitraria, por lo que el desbordamiento no es un problema, pero todavía echamos a "int" para el retorno final.

-...

**Disfruta de la codificación y la mejor suerte en tu próxima entrevista! * *