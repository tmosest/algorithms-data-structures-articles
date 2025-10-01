-...
Título: LeetCode 816. Coordenadas ambiguas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 816. Coordenadas ambiguas – Guía completa, SEO-Ley

■ **TL;DR**
* Parse la cadena **s** después de despojar a los paréntesis externos.
• Enumerar todas las posiciones posibles “comma”.
* Para cada lado genera cada “integer” legal o “decimal” representación.
* Combine los dos lados y devuelva la lista final.
• Complejidad: **O(n2)** tiempo, **O(n)** espacio auxiliar.

-...

## 1. Recaptación de problemas

Se le da una cuerda `s` que parece un punto 2-dimensional, por ejemplo `"(1, 3) ".
Todos los comas, puntos decimales y espacios fueron eliminados, produciendo una cadena como

`` `
"(1,3)" - título "(13)"
"(2,0.5)" - título "(205)"
`` `

Su tarea es devolver **todo** posible par de coordenadas original que podría
produce `s` cuando la punción fue despojada.
Las reglas para números válidos son:

* No hay ceros principales a menos que el número sea exactamente "0".
* Un punto decimal sólo puede aparecer **después** al menos un dígito.
* No se admiten números que pueden ser representados con menos dígitos (por ejemplo, `'001'` → `'1', `"0.0" → `"0".

La lista final puede estar en cualquier orden, pero cada par debe tener exactamente un espacio después de la coma.

-...

## 2. Por qué este problema es interesante

* Prueba **manipulación de punta** habilidades, especialmente manejando posiciones decimales.
* Las reglas “leading/trailing‐zero” lo convierten en un problema **corner‐case**.
* La solución es una buena ilustración del patrón ** "generar y filtrar"**:
– generar todas las formas de dividir los dígitos e insertar un punto decimal,
– luego filtra los inválidos.

Debido a su dificultad moderada (LeetCode “Medium”) y la elegancia de la
solución, este problema es un favorito en las listas de preparación de entrevistas.

-...

## 3. Panorama general de la solución

1. **Strip the parentheses** → Obtener la cadena de dígitos puros `digits`.
2. ** Aumentar las posiciones de los coma** – dividir los dígitos en una parte izquierda y una parte correcta.
3. **Generar todas las representaciones válidas** de una cadena de dígitos
* no punto decimal (sólo si la cadena es un solo dígito o no comienza con `'0'`)
* un punto decimal después del primer dígito (sólo si la cadena termina con un no cero)
* un punto decimal en algún lugar del centro (sólo si la cadena no comienza con `'0'` y no termina con `'0'`)
4. **Combine** cada opción izquierda con cada opción derecha y envuélvalos en `"(" + izquierda + ", " + derecha + ")".
5. **Retorno** la lista final.

El paso “generar todas las representaciones válidas” es el corazón del algoritmo.

-...

## 4. Algoritm detallado

``text
dígitos = s[1:-1] // strip '(' y ') '
para cada i de 1 a len(digits)-1:
x_str = digitos[0:i]
y_str = dígitos[i:]
left_opts = generateOptions(x_str)
right_opts = generateOptions(y_str)
para cada uno en zurdos:
para cada b en right_opts:
resultado.add("(" + a + ", " + b + ")")
Resultado de retorno
`` `

`generateOptions(str)` funciona así:

`` `
opciones = []

// 1) entero plano
si len(str) == 1 o str[0] != '0':
opciones.append(str)

// 2) decimal después del primer dígito
si len(str) '0':
opciones.append(str[0] + "." + str[1:])

// 3) decimal en cualquier otra posición
si len(str) '0' y str [-1] '0':
para k en rango(2, len(str)):
opciones.append(str[:k] + "." + str[k:])

Opciones de retorno
`` `

Todas las restricciones se verifican por las condiciones anteriores; la función devuelve
sólo cadenas que satisfacen la regla “no líder/trailing cero”.

-...

## 4.1 Casos de borde

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTE
Silencio------------------------
TENIDA `"(10)" ← Imposible – no hay suficientes dígitos para una coma Silencioso `[]’
TENIDO "(000)" Silencioso como `00` / `0` – todas las opciones contienen ceros líderes → `[]` Silencio
TENIDO "(010)" ¦ Split `0` / `10` → `0` is fine, but `10` is fine → `["(0, 10) " Silencio
""(0000)" Silencio Todas las divisiones contienen más de un cero → `[]

-...

## 4.2 Correctness Proof (Sketch)

1. ** Posiciones del Comité**:
Cada par legal debe tener una coma entre el primer y último dígito de 'digits'.
El bucle `para mí en 1..len(digits)-1` visitas **all** tales posiciones, por lo que no se pierde ninguna división posible.

2. **`generateOptions` validez**:
* Si la cadena tiene un dígito → siempre es válido (no hay problema de ceros líderes).
* Si comienza con `'0'` → el único decimal válido es `"0.xxxx"`; cualquier otra forma podría tener un cero líder o un cero rastreador.
* Si termina con `'0'` → sólo se permite la forma entero porque un final decimal con cero tendría un cero rastreador.
* Para las cadenas que satisfacen las reglas de "líder/trailing", se considera cada posición decimal posible, pero sólo si la parte correcta del decimal (la parte fraccional) no es cero – de lo contrario terminaría con un cero.

Así, las `Opciones generales ' enumeran **all** y **only** representaciones legales.
Combinar partes izquierda y derecha por lo tanto produce cada par de coordenadas factible,
y ningún par inválido puede pasar.

-...

## 5. Análisis de la complejidad

Dejar `n` ser el número de dígitos dentro de los paréntesis (`3 ≤ n ≤ 8` para las limitaciones del problema.

* Dividiendo la cuerda: `O(n)` por división.
* Por cada lado, `generateOptions` produce en la mayoría de `n` cuerdas (no decimal) + `n-1` (decimal en cualquiera de las posiciones `n-1').
Así que `O(n)` por lado.
* Tenemos `n-1` posiciones de coma → tiempo general `O(n * n) = O(n2)` (≤ 64 operaciones para la entrada máxima).
* La lista de resultados puede contener en la mayoría de los elementos `O(n2)`; guardamos algunos vectores auxiliares de tamaño `O(n)` → espacio auxiliar general `O(n)`.

Con `n ≤ 8`, esto es lo suficientemente rápido para todos los casos de prueba.

-...

## 6. Aplicación del Código

A continuación se encuentran soluciones limpias, bien adaptadas en **Python 3**, **Java 17** y **C+17**.
Siéntete libre de copiar-paste en tu IDE favorito o juez online.

### 6.1 Python 3

``python
de la importación Lista

Solución de clase:
# Helper that turned a pure digit string into all legal numbers
def _options(self, num: str) - Propiedad Lista[str]:
opts = []

# 1) Forma del entero
si len(num) == 1 o num[0] != '0':
opts.append(num)

# 2) Decimal después del primer dígito
si len(num) '0':
opts.append(num[0] + '.' + num[1:])

# 3) Decimal en el medio (sin plomo cero y sin rastro cero)
si len(num) '0' y num[-1] '0':
para i en rango(1, len(num)):
opts.append(num[:i] + '.' + num[i:])

Opciones de retorno

def ambiguous Coordenadas (self, s: str) - Lista[str]:
dígitos = s[1:-1] # strip '(' y ') '
res = []

# split between 1..len(digits)-1
para i en rango(1, len(digits)):
izquierda = dígitos[:i]
derecha = dígitos[i:]

left_opts = self._options(left)
right_opts = self._options(right)

para un in left_opts
para b en right_opts:
re.append(f'({a}, {b})')

retorno
`` `

-...

### 6.2 Java 17

``java
importa java.util. ArrayList;
importa java.util. Lista;

Solución de la clase pública {}
// Genera todas las representaciones legales de una cadena numérica
lista privada seleccionadaString opciones (String num) {
Lista seleccionadaString titulada res = nuevo ArrayList correctamente();

// 1) Forma del entero
si (num.length() == 1 TENIDO ATENCIÓN num.charAt(0) != '0')
res.add(num);

// 2) Decimal después del primer dígito
si (num.length() - 1) != '0')
res.add(num.charAt(0) + "." + num.substring(1));

// 3) Decimal en el medio
si (num.length() - 1) != '0') {
para (int i = 1; i) ++i) {
res.add(num.substring(0, i) + "." + num.substring(i));
}
}
restitución;
}

public List Garantizado Coordinates(String s) {
dígitos de cuerda = s.substring(1, s.length() - 1); // strip parentheses
Lista de resultados:String ratio result = nuevo ArrayList correctamente();

para (int i = 1; i) ++i) { // posibles posiciones de coma
Cierre izquierda = dígitos.substring(0, i);
Cierre derecho = dígitos.substring(i);

Lista seleccionadaString titulada leftOpts = options(izquierda);
Lista seleccionadaString titulada rightOpts = options(right);

para (String a : leftOpts) {
for (String b : rightOpts) {}
result.add("(" + a + ", " + b + ")");
}
}
}
Resultado de retorno;
}
}
`` `

-...

### 6.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vectoriales Coordinates(string s) {
dígitos de cadena = s.substr(1, s.size() - 2); // strip parentheses
vector asignados a título personal;

para (size_t i = 1; i) ++i) {
string left = digits.substr(0, i);
string right = digits.substr(i);

vector asignado a título inferior izquierdoOpts = opciones (izquierda);
vector asignado derecho de propiedadOpts = opciones(derecho);

for (const string &a : leftOpts)
for (const string &b : rightOpts)
ans.emplace_back(" + a + ", " + b + ")");
}
devolver los ans;
}

privado:
// Todas las representaciones válidas de una cadena numérica
vector asignado opciones de confianza(cont string &num) {}
vectoriales res;

// Forma del entero
si (num.size() == 1 Silencioso desnudo[0] != '0')
res.push_back(num);

// Decimal después de primer dígito
si (num.size() '0')
res.push_back(string(1, num[0]) + "." + num.substr(1));

// Decimal en cualquier posición media
si (num.size() √≥ 2 " cerrado num[0] != '0' " num.back() != '0') {
para (size_t i = 1; i) ++i)
res.push_back(num.substr(0, i) + "." + num.substr(i));
}
restitución;
}
};
`` `

-...

## 7. Resumen

* **Problema** – reconstruir todas las coordenadas posibles de una cuerda mangleda.
* **Key Insight** – enumerar todas las divisiones legales y por cada parte generar sólo los formatos enteros/decimales válidos.
* **Time** – `O(n2)` (`n ≤ 8`), **Pace** – `O(n)`.
* **Result** – Soluciones limpias en Python, Java, C++ listas para entrevistas o programación competitiva.

-...

## 7.1 Bonus: More Efficient Alternative

Una pequeña optimización que puede caer en cualquiera de las soluciones es saltar divisiones que
definitivamente produciría ceros líderes en ambos lados.
Por ejemplo, si `num[0] == '0' ' п num[1] == '0'` podemos romper temprano, ahorrando un puñado de llamadas innecesarias - no estrictamente requerido para la corrección, pero agradable para el rendimiento en idiomas donde las llamadas de función son costosas.

-...

## 7.2 Testing

``python
si __name_ == "__main__":
sol = Solución()
print(sol.ambiguousCoordinates("(123)") # Ejemplo de la declaración
`` `

-...

## 7.3 Pensamientos finales

El problema de “coordenadas ambiguas” es un gran ejemplo de una enumeración **combinatorial** con algunas limitaciones sutiles de cuerda.
The key takeaway: **break the problem into small, testable pieces** (splitting + option generation).
Una vez que se puede aislar un subproblema, la prueba de corrección es generalmente directa, y el código permanece ordenado.

¡Feliz codificación! 🚀

-...

### 8. Lectura adicional

* [LeetCode 797. All Paths From Source to Target](https://leetcode.com/problems/all-paths-from-source-to-target/) – another combinatorial enumeration.
* [Top‐Down vs Bottom‐Up DP] – comprensión de los intercambios de complejidad.
* [C+17 String Manipulation] – aprender a trabajar eficientemente con `substr`, `emplace_back`.

¡Buena suerte con tu próxima entrevista o desafío de codificación!