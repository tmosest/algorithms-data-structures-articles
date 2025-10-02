-...
Título: LeetCode 1357. Aplicar Descuento Cada n Pedidos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1 ride Lee LeetCode 1357 – * Descuento de aplicación Cada n Pedidos*
**Solución en Java, Python & C++ + una entrevista adaptada a SEO**

-...

Problema Recap

Un supermercado vende " productos " por " precios[i] " .
La factura de un cliente es dos arrays paralelos `product` & `amount`.
Cada cliente **`n``th** recibe un **`discount` %** fuera del subtotal.

Usted debe implementar:

``text
Cajero(int n, int descuento, int[] productos, int [] precios)
doble getBill(int[] producto, int[] cantidad)
`` `

`getBill` devuelve la cantidad final que un cliente debe pagar (descuento aplicado si es el
nth cliente). Se aceptan respuestas en el apartado 1e-5.

■ **Constraints**
≤ 104
* `0 ≤ descuento ≤ 100`
> > ≤ productos. longitud ≤ 200 >
* 1 ≤ producto. longitud ≤ productos. longitud `
* `product` Los ID son únicos

-...

# Idea núcleo

* **Map product IDs → precios** (`HashMap / unordered_map / dict`).
* Mantener un **contra** (`actualCustomer`).
* Después de cada llamada a `getBill`, aumentar el contador.
Si `currentCustomer % n == 0`, aplicar el descuento.
* Computar el subtotal por iterar a través del orden y summing
`amount[i] * price[product[i]]`.

El algoritmo es **O(k)** por llamada, donde *k* es el número de elementos en que
pedido, y utiliza **O(p)** espacio adicional para el mapa de precios.

-...

## ف Code

#### ## 1down⃣ Java

``java
importa java.util. HashMap;
importa java.util. Mapa;

clase pública Cashier {
int n privado final; // cada nth cliente obtiene descuento
descuento final privado; // por ciento descuento
final privado Mapa:Integer,Integer ratioMap;
privado int cliente Cnt = 0; // cuenta cuántos clientes hasta ahora

public Cashier(int n, int descuento, int[] productos, int[] precios) {
esto.n = n;
esto. descuento = descuento;
precioMap = nuevo HashMap garantizado(products.length);
para (int i = 0; i) i++) {
precioMap.put(products[i], precios[i]); // O(p)
}
}

public double getBill(int[] product, int[] amount) {
cliente Cnt++; // 1 base contando

subtotal doble = 0;
para (int i = 0; i) i++) {
subtotal += priceMap.get(product[i]) * (double) amount[i];
}

si (customer Cnt % n == 0) { // nth customer
subtotal *= (100 - descuento) / 100.0; // aplicar descuento
}
subtotal de retorno;
}
}
`` `

#### 2down⃣ Python

``python
clase Cajero:
def __init__(self, n: int, descuento: int, productos: list[int], precios: list[int]):
self.n = n
self.discount = descuento
self.price_map = {p: pr para p, pr en zip(products, prices)}
self.customer_cnt = 0

def getBill(self, product: list[int], amount: list[int] flotante:
auto.customer_cnt += 1
subtotal = sum(self.price_map[prod] * amt for prod, amt in zip(product, amount))
si auto.customer_cnt % self.n == 0: # cada nth client
subtotal *= (100 - self.discount) / 100.0
subtotal
`` `

#### 3down⃣ C++

``cpp
#include ■unordered_map Conf
Incluido el título

clase Cajero
int n; // frecuencia de descuento
descuento int; // por ciento
std::unordered_map seleccionada, int ratioMap; // product → precio
cliente int Cnt = 0; //

public:
Cajero(int n, int descuento, std::vector fielint productos, std::vector fielint precios)
: n(n), descuento(descuento) {
para (size_t i = 0; i) ++i)
precioMap[products[i] = precios[i];
}

doble getBill(cont std::vector seleccionadoint limitada product, const std::vector fieltro cantidad) {
++cliente Cnt;
subtotal doble = 0,0;
para (size_t i = 0; i) ++i)
subtotal += precioMap [product[i]] * static_cast seleccionadodouble(amount[i]);

si (customer Cnt % n == 0)
subtotal *= static_cast seleccionadodouble(100 - descuento) / 100.0;
subtotal de retorno;
}
};
`` `

-...

## 📐 Complexity Analysis

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------------------------------ La vida----
Silencio Precio del edificio mapa Silencioso `O(p)` (`p` = #products) Silencio `O(p)` Silencio
Silencio `getBill` call (per order) Silencio `O(k)` (`k` = #items in order) Silencio `O(1)` (beside input) ←

Con una mayoría de 1000 llamadas y `p ≤ 200`, la solución encaja fácilmente dentro de la
límites.

-...

Artículo del Blog – “El Bien, el Mal y el Ugly of *Apply Discount Every n Orders*”

### 1. Título " Meta-Descripción "

■ **Título**: *Aplicar Descuento Cada n Pedidos – Java, Python & C++ Soluciones (LeetCode 1357)*
■ **Meta‐Description**: Solve LeetCode 1357 “Promoción de aplicación Cada n Pedidos” con código Java limpio, Python y C++. Aprenda los cambios, casos de borde y consejos de entrevista para llegar a la pregunta.

### 2. Esquema

1. **Introducción** – ¿Por qué este problema es un problema básico en las entrevistas técnicas
2. **Problema declaración** – Restate constraints, goal, and expected output
3. **Observaciones clave** – ID de producto único, frecuencia de descuento fija
4. **Estrategia** – Mapa de búsqueda + contador
5. **Implementación** – Códigos para Java, Python, C++
6. ** Casos de complejidad y borde** – Rebosa, precisión de punto flotante
7. **El Bien** – Simplicidad, legibilidad, espacio O(1) por llamada
8. **El mal** – trampas alternativas (búsqueda de rayos, recursión)
9. **El Ugly** – trampas del mundo real (desbordamiento entero, reinicio de descuento perdido)
9. **Perspectiva de Interview** – ¿Qué entrevistadores están buscando realmente
10. **Testing** – Cómo escribir pruebas de unidad
11. **FAQs** – Puntos de confusión comunes
12. **Conclusión " Call‐to-Action** - Fomentar la práctica " prep

### 3. Texto completo del Blog

``markdown
# Apply Discount Every n Orders – Java, Python & C+ Solutions (LeetCode 1357)

■ **LeetCode 1357** es una pregunta de entrevista clásica que prueba
*data‐structure choice*, *contra lógica* y *floating‐point handling*.
■ A continuación se presenta una guía paso a paso con código limpio en tres idiomas principales,
más una profunda inmersión en los intercambios que cada candidato debe saber.

## 📌 Introduction

Los entrevistadores aman problemas que mezclan un sistema *establecido* (un cajero) con un
regla aritmética simple (todos los clientes nth obtienen un descuento).
Comproba:
- su comprensión de **hash mapas** para la búsqueda O(1)
**modulo arithmetic** para eventos periódicos
- manejo **materia de punto flotante** sin perder precisión

Si usted ha clavado esta pregunta, usted se sentirá confiado tackling similar
problemas estatales en cualquier ronda de contratación técnica.

-...

Declaración de problemas

■ Una tienda vende *productos* para *precios*.
■ El pedido de un cliente es dos arrays: `product[]` y `amount[]`.
■ Cada cliente de 'n' obtiene un 'descuento' % del subtotal.
■ Implementar `Cashier` con `getBill()` que devuelve la cantidad final.

Constraints:
- 1 ≤ 104
- `0 ≤ descuento ≤ 100`
- `products.length ≤ 200`
- `producto` Las identificaciones son **unique** y **positivo**.

-...

## 🔍 Observaciones clave

TENCIÓN ANTERIOR Por qué importa
Silencio...
Silencio ** IDs únicos** Silencio Permite la búsqueda directa de hash‐map. Silencio
Silencio **Fixed `n`** Silencio Simple contador con modulo. Silencio
Silencio **`discount`** ≤ 100 casos de retraso 0 % (sin descuento) > 100 % (gratuito). Silencio
Silencio **No hay cambios de orden** Silencio Mapa de precio construido una vez en constructor. Silencio

-...

## 📊 Strategy

1. ** Mapa de precios** – `producto → precio `
*O(p)* para construir, *O(1)* por lookup.
2. **Customer Counter** – `current Customer++`.
Aplicar descuento cuando `currentCustomer % n == 0`.
3. **Cálculo subtotal** – Itear sobre los artículos de pedido.

El diseño es *O(k)* por llamada, *O(p)* espacio.
Los tres idiomas (Java, Python, C++) usan la misma lógica – simplemente diferente
sintaxis.

-...

## 🧑 💻 Aspectos destacados de la implementación

Silencio Idioma Silencio Core Lines Silencio Por qué se ve bien
Silencio--------------------------------...
Silencio **Java** Silencioso `priceMap.put(products[i], prices[i]);` + `subtotal *= (100‐discount)/100.0;` peru Strong typing + explicit `double` cast.
Silencio **Python** Silencio `{p: pr for p, pr in zip(products, prices)}` + `subtotal *= (100-discount)/100.0` peru Concise comprensión, automatic big-int support. Silencio
Silencio **C++** Silencio `unordered_map observadoint,intenta precioMap;` + `subtotal *= (100-discount)/100.0` peru Compilación rápida-time Lookups, explícito casting to double. Silencio

Los bloques de código de la sección **Solución** están incrustados para copiar rápidamente.

-...

## ⏱ Complexity & Edge Cases

* **Hora** – `O(k)` por orden, lineal en número de artículos.
* **Pace** – `O(p)` para el mapa; por llamada `O(1)`.
* **Overflow** – `amount[i] * price` fits in 32‐bit signed int (`≤ 200 × 104`),
pero lanzamos a "doble" antes de multiplicarse para evitar el desbordamiento accidental.
* **Precisión** – Use `doble` y un multiplicador como `(100-discount)/100.0`.
LeetCode acepta `1e-5`, por lo que IEEE‐754 estándar es seguro.

-...

## llevándose el bien

Silencioso Benefit
Silencio...
Silencio **Claridad** Silencio Un mapa, un contador – ningún truco oculto. Silencio
Silencio **Performance** tención Mapa de tiempo constante; lineal en tamaño de orden solamente. Silencio
Silencio **Mantenibilidad** Silencioso constructor separado " método; fácil de probar. Silencio
tención **Cross‐Language** tención Mismo algoritmo, adaptación mínima para Java/Python/C++. Silencio

-...

## ⋅ The Bad

Por qué duele la vida
Silencio...
Silencio **Array‐Search Alternative** Silencio Usar una búsqueda lineal en la matriz de productos da tiempo `O(p*k)` – innecesario si `p` es 200. Silencio
tención **Recursive Counter** TEN Recursion apilaría el flujo si `n` es grande. Silencio
Silencio **Missing Reset** Silencio Failing para restablecer el contador después del descuento conduce a descuentos futuros incorrectos. Silencio

-...

## The Ugly

Problema de la vida en el escenario del mundo real
Silencio--------------...
Silencio **Desbordamiento entero** Silencioso `mont[i] * precio` podría exceder `231‐1` si usted permanece en `int`. tención Promuevan a `long` o `doble` antes de la multiplicación. Silencio
TEN **Floating‐point drift** TEN Los descuentos repetidos pueden acumular errores de redondeo. Retorno `doble` y confíe en `1e‐5` tolerancia; utilice `Decimal` en Python si se necesita la exactitud. Silencio
Silencio **Guardia de la división del espacio** Cnt % 1 == Siempre es verdad. Funciona bien; sólo asegura que el descuento se aplica a cada cliente – un caso de esquina que debe probar. Silencio

-...

## 📈 Interview Tips

1. **Preguntas aclaratorias** – “¿Se aplica el descuento al subtotal o al total final? ”
2. **Explicar la contra lógica** – “Amucho el contador primero, luego comprobar “cnt % n == 0”. ”
3. **Mostrar la construcción del mapa** – “Construiremos el mapa una vez en el constructor para espacio O(p). ”
4. ** Punto flotante de la mención** – “Usamos el doble para preservar los centavos. ”
5. ** Casos de prueba de debate** – Proporcionar ejemplos, especialmente para casos de borde: `descuento = 0`, `descuento = 100`, `n = 1`, órdenes grandes.

-...

## 📚 Testing Checklist

Silencio Test confidencialidad Qué hacer para verificar
Silencio...
tención Ejemplo básico (desde el problema) Silencio Correct descuento en 3er y 6to clientes. Silencio
Silencio `discount = 0` Silencio No hay cambio a subtotal. Silencio
Silencioso `descuento = 100` Silencio Zero factura final. Silencio
Silencio `n = 1` Silencio Cada cliente obtiene descuento. Silencio
tención Orden grande (200 ítems) Silencio Sin degradación del rendimiento. Silencio
Silencio Llamadas repetidas 104 Ø El contra modulo sigue funcionando. Silencio

-...

Conclusión

LeetCode 1357 es una pregunta *establecida* que combina el uso de la estructura de datos con
aritmética modular.
Un simple hashmap + contra enfoque da código limpio y eficiente en **Java,
Python y C+**.
Entender las trampas (sobreflujo, punto flotante) y discutir el diseño
oficios en entrevistas – demostrarás tanto la habilidad técnica como
pensativo problema - solución.

-...

## ❓ FAQ

Silencio
Silencio...
Silencio **¿Puedo usar un array en lugar de un mapa?** Silencio Sí, pero necesitarás `O(p)` búsqueda lineal para cada orden – O(k × p) tiempo. Silencio
Silencio **¿Qué pasa si los IDs de producto no son únicos?** Silencio Problema garantiza la singularidad; de lo contrario necesitará una lista de precios por ID. Silencio
Silencioso ** ¿Desbordará la multiplicación de enteros?** Silencio Use `long` o cast to `double` antes de la multiplicación. Silencio
Silencio **¿Es suficiente precisión doble?** Silencio LeetCode acepta error 1e‐5; mantissa de 53 bits doble es más que suficiente. Silencio

-...

## 🚀 Get Hired

Dominar este problema muestra que puede:

* Map data to a value efficient (`HashMap` / `dict`).
* El manejo del estado periódico cambia de forma limpia (`%` operador).
* Escriba código limpio, multiplataforma.

Agregue las soluciones anteriores a su cartera, incluya la explicación lista para la entrevista, y tendrá un punto de conversación fuerte para cualquier entrevista **software-engineering**.

¡Feliz codificación y buena suerte en tu próxima entrevista!