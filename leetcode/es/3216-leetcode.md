-...
Título: LeetCode 3216. Pendiente Lexicográficamente más pequeña Después de un Swap -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

## 3216 – Lexicográficamente Cuerda más pequeña después de un cigarro
*Fácil* *String*

■ *Problema*
■ Dada una cadena `s` que contiene sólo dígitos, puede realizar ** en la mayoría de un** intercambio de dígitos *adjacent* que tienen la misma paridad (tanto impares como ambos).
■ Devuelve la cadena más pequeña que se puede obtener.

-...

### Por qué este problema importa
- **Interview Signal:** Leetcode “Easy” pero requiere una comprensión clara de *parity* y *ordenaciónléxicográfica*.
- Esquía de codificación: Demuestra el razonamiento codicioso, el traversal lineal de un paso, y el diseño algoritmo de cambio mínimo.
- **Career Boost:** Resolver muestra su capacidad de leer un problema, razonar rápidamente, y ofrecer una solución O(n) óptima – un rasgo distintivo que los reclutadores aman.

-...

##  Settlement Solution Overview (Greedy)

1. **Atravesa la cuerda de izquierda a derecha. #
2. En la posición `i`, compare el dígito `s[i]` y el siguiente dígito `s[i+1]`.
3. Si:
* tienen la misma paridad* (`s[i]-'0') % 2 == (s[i+1]-'0') % 2`) **y**
* `s[i] √≥ s[i+1]` (es decir, el dígito izquierdo es mayor que el derecho)

entonces **swap** ellos y **stop** – sólo se nos permite un intercambio.
4. Si el bucle termina sin un swap, devuelve la cuerda original.

Debido a que siempre realizamos el *primer* posible intercambio beneficioso, la cadena resultante está garantizada a ser el más pequeño de la lexicografía obtenida con un solo intercambio de paridad adyacente. Esta opción avaricia es óptima: cualquier cambio posterior no mejoraría el prefijo o requeriría más de un swap.

-...

## 📦 Implementation (All Languages)

## Java

``java
// 3216. Cuerda más pequeña de Lexicografía Después de un Swap
Solución de la clase pública {}
public String getSmallestString(String s) {
int n = s.length();
char[] arr = s.toCharArray();

para (int i = 0; i)
int a = arrr[i] - '0';
int b = arr[i + 1] - '0';

si (un porcentaje 2 = == b % 2) " (a ± b)) {
// swap once and exit
char temp = arr[i];
arr[i] = arr[i + 1];
arr[i + 1] = temp;
ruptura;
}
}
volver nuevo String(arr);
}
}
`` `

-...

## Python

``python
# 3216. Lexicographically Smallest String After a Swap
Solución de clase:
def getSmallestString(self, s: str) - confiar str:
arr = lista(s)
n = len(arr)

para i en rango(n - 1):
a = int(arr[i])
b = int(arr[i + 1])

si un % 2 == b % 2 y un mento b:
arr[i], arr[i + 1] = arr[i + 1], arrr[i]
descanso

volver ''.join(arr)
`` `

-...

### C++

``cpp
// 3216. Cuerda más pequeña de Lexicografía Después de un Swap
Clase Solución {
public:
string getSmallestString(string s) {
int n = s.size();

para (int i = 0; i) {}
int a = s [i] - '0';
int b = s 1] - '0';

si (un porcentaje 2 = == b % 2) " Unidos "
swap(s[i], s[i + 1]);
ruptura; // sólo se permite un intercambio
}
}
retorno s;
}
};
`` `

-...

## 🤔 Complexity Analysis

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencioso (single loop)
Silencio, conversión de String (Java) **O(n)** Silencio **O(n)** (caracter array)

'n ≤ 100', así que todas las soluciones funcionan en tiempo insignificante.

-...

## 🏆 El Bien, el Mal, y el Ugly

TENIDO Categoría ANTERIOR Lo que funciona ANTERIENTE Pitfalls potenciales
Silencio------------------------------------------------------------------
Silencio **Bien** Silencio • Un paso codicioso da tiempo lineal. No hace falta estructuras de datos adicionales. • Obras para todos los casos de borde (`s` ya mínimo, no válido swap, swap al final).
Silencio **Bad** Silencio • Mis-interpretar “adjacent” puede llevar a cambios incorrectos. • Olvidar romper después de que el primer swap viole la regla “a la mayoría de uno”. Silencio • Trápate dos dígitos de la misma disparidad no adyacente* conduce a la respuesta equivocada. • Sobre-optimizar con dos punteros puede agregar complejidad innecesaria.
Silencio **Ugly** Silencio • Usando la concatenación de cuerda dentro del bucle en Python (`s = s[:i] + s[i] + s[i] + s[i+2:]`) puede producir comportamiento O(n2). En Java, volver a crear una nueva cadena en cada iteración sería desperdicio. ← Evite la creación de cuerdas repetidas; utilice arrays de caracteres o StringBuilder. TEN TEN

-...

## 🚀 SEO‐Optimized Blog Article: "Master Leetcode 3216 – Lexicographically Cuerda más pequeña después de un súbito”

■ **Título:** "Solve Leetcode 3216 in 5 Minutes: Lexicographically Smallest String After a Swap (Java, Python, C++)"

■ **Meta Descripción:** “Aprenda a romper Leetcode 3216 en menos de 5 minutos. Coge la solución codictiva completa, fragmentos de código en Java, Python y C++, además de consejos de entrevista. ¡Consigue el trabajo que quieras!”

■ **Target Keywords:** *Leetcode 3216, Lexicographically Smallest String, intercambiar dígitos adyacentes, intercambio de paridad, problema de codificación de entrevistas, solución Java, solución Python, solución C++, consejos de entrevista de algoritmos*

### 1. Garfio - ¿Por qué Este problema se rompe

- Nota fácil, dura en entrevistas** - La gente lo pasa por alto porque parece trivial, pero los reclutadores lo aman como un rápido cheque de cordura.
- **Aplicación del mundo real** – El intercambio de paridad es similar a las optimizaciones de “bubble-sort” en sistemas integrados.

### 2. Declaración de problemas (condenada)

■ Dada una cadena de dígitos, realice *en la mayoría de un* intercambio adyacente entre dos dígitos de la misma paridad para producir la cadena más pequeña posible lexicográficamente.

### 3. Insight clave – Greedy First Good Swap

- La cadena más pequeña se determina por la posición más temprana donde un swap puede reducir el dígito izquierdo.
- Tragar el *primer* par elegible siempre es óptimo.
- Esto reduce el problema a un solo escaneo lineal.

### 4. Step‐by‐Step Code Walkthrough (Java)

``java
para (int i = 0; i)
si (sameParity(s[i], s[i+1]) " sensible s[i] {}
swap(s, i, i+1);
ruptura;
}
}
`` `

Explicar 'sameParity' y 'swap` ayudantes.

### 5. Código completo (Java, Pitón, C++)

Mostrar bloques de código (arriba) con notas breves sobre el lenguaje específico.

### 6. Lista de verificación de casos de borde

Silencio Silencio Silencio Silencio Silencio Silencio
Silencio--------Prince--------
Silencio No válido swap tención Todos los dígitos adyacentes difieren en paridad o ya mínima tención Original string tención
tención Swap en el último par de la vida Debe todavía devolver la cadena más pequeña ← cuerda cortada ←
Silencio ceros anteriores La comparación lexicográfica sigue siendo aplicable

### 7. Tiempo " Complejidad espacial "

- **O(n)** tiempo, **O(1)** espacio (además de la cadena de salida).

### 8. Consejos de entrevista

- Explique su razonamiento codicioso. Buscador *por qué* no sólo *qué*.
- **Mención de la restricción de “a la mayoría de un swap”** explícitamente al discutir su bucle.
- **Mostrar las optimizaciones específicas del idioma** (por ejemplo, utilizando `StringBuilder` en Java, `char[]` en C++).

### 9. Wrap‐Up

- Summarize la elegante solución de un paso.
- Alentar a los lectores a practicar variaciones (swaps no adyacentes, múltiples swaps).
- Enlace a los recursos adicionales y llamamiento a la acción: “Pruébalo en el código Leet, sube, comparte. ”

#### 10. Call to Action " SEO

- **Compartir** en LinkedIn con #Leetcode #CodingInterview.
- **Suscribir** a su canal de YouTube para obtener soluciones más rápidas.
- Incluir un enlace al repositorio GitHub que contiene las tres soluciones.

-...

## 🎯 Takeaway

- El problema es un ejercicio codicioso de clase**.
- La solución es **O(n)** y trivialmente implementable en cualquier idioma principal.
- Al dominar esto, usted muestra la capacidad de **read problem constraints, derivar una estrategia mínima de cambio, e implementar limpiamente**—exactamente lo que los reclutadores están cazando.

¡Feliz codificación, y que esa entrevista sea una brisa!