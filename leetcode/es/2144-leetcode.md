-...
Título: LeetCode 2144. Costo mínimo de la compra de dulces con descuento -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2144. Costo mínimo de la compra de caramelos con descuento
■ - LeetCode

**Idiomas** – Java, C++, Python

■ Este post le dará tres soluciones de producción, un profundo dinamismo en el truco algorítmico, y una escritura de estilo blog optimizado SEO que puede ayudar a aterrizar su próxima entrevista de software de ingeniería.

-...

## 1. Panorama general de los problemas

■ Una tienda ejecuta una promoción de “comprar 2, obtener 1 gratis”.
■ Para cualquier dos caramelos que pague, puede elegir un tercer caramelo * cuyo costo es ≤ el más barato de los dos caramelos pagados* y obtenerlo gratis.
■
■ Dado un conjunto de `costo' de los precios de todos los caramelos, devuelve el costo total **mínimo** necesario para adquirir cada caramelo.

### Constraints

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio...
TENIDO `1 ≤ costo.length ≤ 100` ANTE
TENIDO `1 ≤ costo[i] ≤ 100

-...

## 2. Visión clave

La promoción es esencialmente un **grany "toma el dulce libre más barato posible"**.
Si clasificamos todos los caramelos en orden **sin disminuir**, entonces:

- Los dulces más caros ** siempre deben ser pagados por (nunca se puede obtener gratis porque no hay ningún caramelo más barato para satisfacer la condición “≤”.
- Los dulces **segundo más caros** también deben ser pagados (no hay ningún caramelo más barato de lo que puede ser tomado libre mientras sigue obedeciendo la regla).
- El **tercero dulce más caro** se convierte en *gratuito* – siempre será el más barato entre los tres más caros, porque se sienta exactamente en la posición “tercer-grande”.

Repitiendo este patrón desde el extremo más caro, obtenemos una estrategia óptima:
■ **Pagar por los dos caramelos restantes más caros, saltar el tercero como libre, y repetir. #

En términos de índices (después de ordenar ascendentemente), los caramelos que son *libres* son aquellos cuyo índice satisfies
n – i) % 3 == 0` donde `n` es el número total de caramelos y `i` es el índice 0-basado.
Todos los demás contribuyen al costo total.

-...

## 3. El algoritmo

1. **Sorta** el array `cost` en orden ascendente.
2. **Iterate** a través de la matriz ordenada y resumir los precios de todos los caramelos que son *no* libres.
*Los dulces libres* son los índices en los que `(n - i) % 3 == 0`.
3. **Retorno** la suma calculada.

El algoritmo es **O(n log n)** debido a la clasificación, y **O(1)** espacio auxiliar (excluyendo el espacio utilizado por la rutina de clasificación).

-...

## 4. Aplicación del Código

#### 4.1 Java

``java
importa java.util. Arrays;

Solución de la clase pública {}
mínimo público Cost(int[] cost) {
Arrays.sort(cost); // O(n log n)
total = 0;
int n = cost.length;

para (int i = 0; i)
// Si (n - i) % 3 == 0 →
si (n - i) % 3 != 0) {
total += costo[i];
}
}
Total de retorno;
}
}
`` `

### 4.2 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
mínimo Costo(vector seleccionado implicado reducido costo) {
sort(cost.begin(), cost.end()); // O(n log n)
int n = cost.size(), ans = 0;
para (int i = 0; i) {}
si (n - i) % 3 != 0) ans += cost[i];
}
devolver los ans;
}
};
`` `

#### 4.3 Python

``python
Solución de clase:
mínimo Costo(self, cost: List[int]) - título int:
cost.sort() # O(n log n)
n = len(cost)
(n - i) % 3 != 0)
`` `

■ **Tip** – Los tres francotiradores dependen de las mismas matemáticas: los caramelos libres son cada tercero desde el final. Esto mantiene el código corto, legible y rápido.

-...

## 5. Lo que funciona – Lo bueno

* **Greedy & Simple** – La solución sigue una estrategia intuitiva de “tomar el dulce libre más barato” que puede ser probada óptima por el argumento de cambio.
* **Low Complexity** – Sólo se requiere una clase, no hay DP o recursión.
* **Language‐agnostic** – El mismo patrón O(n log n) funciona en Java, C++, Python y muchos otros idiomas.
* **Readability** – Clear loop condition `(n - i) % 3 != 0` comunica instantáneamente la regla de los dulces libres.

-...

## 6. Qué ver – El “Bad”

tención potencial Pitfall Silencioso Cómo evitar
Silencio...
Silencio **Off‐by-one errores** Silencio Verifique que está iterando de `i = 0` a `n-1` y utilizando `(n - i) % 3`. Silencio
tención **Introducciones más altas** Silencio Aunque `n ≤ 100`, el algoritmo escala bien a millones; mantener el tipo estable. Silencio
Silencio **Modular aritmética confusión** Silencio Piensa en los dulces libres como cada tercer elemento *de la derecha*, no de la izquierda. Silencio

-...

## 7. Errores comunes

Silencioso tóxico tóxico
Silencio------------
TENIDO Utilizando `i % 3 == 0` en lugar de `(n - i) % 3` Silencioso caramelos libres (primero, cuarto, ...) ← Cambiar a `si (n - i) % 3 != 0)` Silencio
Silencio Pasar los dos últimos elementos cuando `n % 3 == 1` Silencio Perdiendo un caramelo barato ANTE Utiliza la condición general, no un bucle codificado duro. Silencio
Silencio No clasificar la matriz ← Los dulces libres aleatorios Silencio Siempre ordenar antes de aplicar la regla. Silencio

-...

## 8. Extensiones " Variantes

Silencio ¿Qué cambios? Silencio
Silencio...
Silencio **Buy `k`, get `m` free** Silencio Sort, then skip every `(k+m)`‐th candy from the end. Silencio
Silencio **Diferente regla de los candys libres (≤ vs.)** Silencio Ajustar la desigualdad, pero el patrón codicioso todavía sostiene. Silencio
Silencio **Large input (n up to 105)** Silencio Usar el tipo de contador o radio si `cost[i]` ≤ 106 para O(n) time. Silencio

-...

## 9. SEO‐Optimized Blog Artículo

■ *El Maestro LeetCode* 2144 – Mínimo Costo de compra de caramelos con descuento*
■ **Meta Descripción:** *Aprenda la solución codicioso O(n log n) para LeetCode 2144, vea las implementaciones Java, C++ y Python, y obtenga consejos de entrevista. *

#### Introduction

El problema “comprar dos, conseguir uno libre” es un clásico desafío LeetCode que prueba su capacidad de combinar la clasificación con una estrategia avaricia. A pesar de su fácil calificación de dificultad, muchos candidatos tropiezan con la condición sutil “≤ el más barato de los dos caramelos pagados”. En este post, caminaremos a través de la solución óptima, proporcionaremos fragmentos de código claro en Java, C++ y Python, y diseccionamos por qué funciona el enfoque codicioso. Al final, estarás listo para enfrentar este problema en tu próxima entrevista técnica.

### Problema Declaración

(Inscribir la descripción del problema desde el comienzo de este artículo.)

### Por qué Greedy trabaja

(Explicar el argumento de cambio: cualquier solución óptima puede ser reordenada para que el caramelo más caro se paga, el segundo más caro se paga, y el tercero es libre, etc.)

## Algorithm Walkthrough

(Detalles de los pasos: ordenar → iterate → suma excepto cada tercio del final.)

### Código Snippets

(Inserta los códigos Java, C++, Python como se muestra anteriormente).

## Time & Space Complexity

(Explain O(n log n) time, O(1) space.)

### Common Pitfalls

(Incluya la tabla mala.)

### Conclusión

(Envuélvete, menciona que dominar este patrón ayuda con muchas variantes “buy‐X-get‐Y-free”).

#### Palabras clave

*LeetCode 2144*, *mínimo costo de la compra de caramelos*, *comprar dos obtener uno gratis*, *gran algoritmo*, *Solución java*, * Solución C+*, * Solución pitón*, *preparación de interfaz*, *exposición de entrevista de ingenieros de software*.

-...

## 10. Despacho para buscadores de empleo

* **Mostrar la solución en la entrevista** – Hablar a través de la visión avaricia, escribir el código en la pizarra, y explicar por qué ordenar es el primer paso óptimo.
* **Extensiones de la mención** – Si el entrevistador pregunta sobre las variaciones, esté listo para discutir “comprar ‘k’, obtener `m` libre” o datos a gran escala.
* ** legibilidad de alta luz** – Un bucle conciso como `si (n - i) % 3 != 0)` es tanto eficiente como expresivo.

Buena suerte, y que su caramelo de entrevista sea dulce!