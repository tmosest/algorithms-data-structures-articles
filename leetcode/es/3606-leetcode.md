-...
Título: LeetCode 3606. Validador de Código Coupon -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 3606. **Coupon Code Validator** – Full‐Stack Solution (Java, Python, C++)
■ *“Código Azul Silencio Principiante‐Amigo Silencio Personalizado”*

-...

#### TL;DR
Silencio Idioma Silencio Tiempo Complejidad Silencio
Silencio...
Silencio **Java** Silencio**
Silencio **Python** Silencio **O(n log n)** Silencio**
Silencio **C+** Silencio **O(n log n)** Silencio**

La solución es una simple rutina de filtro-then-sort.
- **Filter**: mantener sólo cupones que son activos, no vacío, tienen un código alfanum-underscore válido, y pertenecen a una de las cuatro categorías de negocios.
- **Orden**: utilice un mapa prioritario para las cuatro categorías y luego orden lexicográfico del código.

Las tres implementaciones son: 40 líneas de código limpio y listo para producción.



-...

## 1. Aplicación de Java

``java
importar java.util*;

Solución de la clase pública {}

// Orden de líneas de negocio – menor número = mayor prioridad
mapa final estático privado ORDER = Mapa de(
"electrónica", 0,
"grocery", 1,
"farmacia", 2,
"restaurante", 3
);

public List won(String) validateCoupons(String[] code,
String[] business Línea,
boolean[] isActive) {

Lista seleccionadaCoupon confía valid = nuevo ArrayList correctamente();

para (int i = 0; i) cedido código.length; i++) {
// --- 1/ Cheques básicos .
si (código[i] == null Silenciosos código(i].isEmpty()) continúan;
si (!code[i].matches("[a-zA-Z0-9_]+") continúan;
si (!ORDER.containsKey(businessLine[i])) continúan;
si (!isActive[i]) continúan;

// --- 2down⃣ Almacene un objeto de cupón ligero -----
valid.add(new Coupon(code[i], businessLine[i]));
}

// --- 3down⃣ Ordenar según prioridad del negocio entonces orden léxicográfico
valid.sort(Comparador)
.comparingInt(Coupon c) - ORDER.get(c.businessLine))
.thenComparing(c - título c.code));

// --- 4down⃣ Extraiga sólo los códigos para la respuesta final - Sí.
Lista seleccionadaString] Resultado = nuevo ArrayList correctamente(valid.size());
para (Coupon c : válido) resultado.add(c.code);
Resultado de retorno;
}

// Contenedor ligero – sin conserjes / setters para brevedad
Clase privada estática Coupon {
final Código de crianza;
último negocio de String Línea;
Coupon(String code, String businessLine) {
este.code = código;
esto.businessLine = negocio Línea;
}
}
}
`` `

-...

## 2. Aplicación de los pitones

``python
import re
de la importación Lista

Solución de clase:
# Orden de prioridad para las cuatro categorías de negocios
ORDER = "electrónica": 0, "grocery": 1,
"farmacia": 2, "restaurante": 3}

def validate Coupons(self,
código: Lista[str],
businessLine: List[str],
isActive: List[bool]) - Propiedad Lista[str]:

# Regex para alfanumérico + subrayado
patrón = re.compile(r'^[A-Za-z0-9_]+$')

# 1 Filtrar los cupones válidos
válidos
(c, bl) for c, bl, act in zip(code, businessLine, isActive)
si acto y c y patrón.match(c) y bl en uno mismo. ORDER
]

# 2⃣ Ordenar: primero por prioridad empresarial, luego lexicográficamente
valid.sort(key=lambda x: (self.ORDER[x[1]], x[0])

# 3️ Devuelve sólo los códigos
retorno [c para c, _ en valido]
`` `

-...

## 3. Aplicación C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector descritos: validateCoupons(vector identificadostring clave,
vectoriales negocios Línea,
vector asignadobool confianza isActive) {
Mapa de prioridades de negocios
unordered_map Secuencia, int
"electrónica", 0,
{\fnMicrosoft Sans Serif}
{"farmacia", 2},
{"restaurante", 3}
};

// 2Ω⃣ Helper regex: alfanumérico + subrayado
patrón de regex(R"([A-Za-z0-9_]+)");

// 3down Almacene cupones válidos como pares (código, businessLine)
vector de garantía real, cadena confianza válido;
para (size_t i = 0; i) ++i) {
si (!isActive[i]) continúan;
si (código[i].empty() Silencio!regex_match(código[i], patrón)) continúan;
si (!order.count(businessLine[i])) continúan;
valid.emplace_back(code[i], businessLine[i]);
}

// 4 Cambios en la aduana: prioridad entonces lexicografía
(valid.begin(), valid.end(),
[Continuar] (continuar auto) {
int p = order[a.second] - order[b.second];
si (p!= 0) devolución p 0;
devolver a.primero
});

// 5down Extraer los códigos ordenados
vectoriales resultado;
result.reserve(valid.size());
para (cont auto &p : válido) resultado.push_back(p.first);
Resultado de retorno;
}
};
`` `

-...

## 4. Artículo del Blog: “Coupon Code Validator – The Good, The Bad, and The Ugly”

■ **Seo Focus:** validador de código de cupón, solución LeetCode 3606, Java/Python/C+++, pregunta de entrevista, código limpio, tipo personalizado, entrevista de trabajo

-...

#### 4.1 Introducción

Cuando vi por primera vez *Coupon Code Validator* (LeetCode 3606), el problema parecía casi demasiado fácil para una entrevista de 2 minutos: “Filter and sort coupons. ”
Pero hay trampas sutiles — cuerdas vacías, caracteres raros, categorías de negocios inválidas— que pueden tropezar incluso ingenieros experimentados.

En este artículo caminaré a través del **bueno** (lo que el problema enseña), el **bad** (pocas comunes), y el **ugly** (casos de borde escondido). Terminaré con una solución limpia y lista para la producción en **Java, Python, y C++** que puedes caer en tu currículum o notas de entrevista.

-...

### 4.2 Problema Recaptura

■ **Input**
■ Tres arrays de longitud *n* (`code`, `businessLine`, `isActive`).

■ **Reglas para un cupón válido* *
■ 1. `código ' no es vacío y contiene sólo letras, dígitos o subrayado (`_`).
■ 2. `businessLine`  Iberia {“electronics”, “grocery”, “pharmacy”, “restaurant”}.
■ 3. `isActive` == `true`.

■ **La salida*
■ Lista de códigos válidos de cupones, primero por prioridad empresarial
(`electrónica → comestibles → farmacia → restaurante`), luego lexicográficamente.

■ **Constraints**
≤ 1 ≤ 100, cada longitud de cadena ≤ 100.
■ Todas las entradas son imprimibles ASCII.

-...

#### 4.3 The Good – Why Este problema es válido

1. ** Especificaciones generales** – Las reglas son inequívocas, por lo que el problema prueba *comprensión de lectura*.
2. **Simple Data Structures** – Listas/arrays y un pequeño mapa de búsqueda.
Ideal para practicar *manipulación de la recolección*.
3. **Clasificación de clientes** – presenta la idea de un * mapa de prioridad* más una * clave secundaria*.
4. **Regex Basics** – Validar un código de cupones con un único regex (`[A-Za-z0-9_]+`) es una manera rápida de mostrar el conocimiento de la coincidencia de patrones.
5. **Time‐Space Trade‐Off** – La solución ingenua O(n2) sería más lenta; la solución óptima O(n log n) es sencilla.

-...

### 4.4 Los malos – saltos comunes

Silencio Pitfall Silencio Por qué sucede 
Silencio...
Silencio **Using `==` for strings** Silencio En Java o C+++, la igualdad de cadenas se basa en referencias. TENIDO Use `.equals()` or `=` after storing in a `unordered_map`. Silencio
tención **Ignorando los valores de `null'** Silencioso `código[i]` o `businessLine[i]` puede ser `null` en pruebas de Java. Silencio Add `if (code[i] == null TENIDO código[i].isEmpty()) continue;` Silencio
Silencio **Omitiendo límites regex** Silencio `matches("[A-Za-z0-9_]+") puede coincidir con subestrings. Silencio Prepend `^` y apéndice `$` → `^[A-Za-z0-9_]+$`. Silencio
Silencio **Ordenar con la administración utilizada en la comparación** Silencio El valor del mapa de Prioridad se utiliza incorrectamente (por ejemplo, `-ORDER.get()` vs `ORDER.get()`). ORDER.get(c.businessLine)). Silencio
Silencio **Duplicar líneas de negocio** Silencio Si el mismo código aparece dos veces, el tipo podría todavía ordenarlos correctamente, pero algunas personas olvidan preservar el orden de duplicados. tención Almacene un objeto ligero (`Coupon`) en lugar de un par `String[]`.
Silencio **Over-engineering** Silencio Escribir una clase completa con getters/setters para una función tan pequeña. Use una clase interna mínima o un tuple; mantenga el código legible. Silencio

-...

### 4.5 The Ugly – Hidden Edge Cases

TENIDO Caso TENIDO TENIDO Impacto ANTERIOR Cómo cuidar
Silencio------------------
Silencio `código` = "_" Silencio Válido por regex pero semánticamente extraño. El regex todavía lo acepta – la especie dice sólo alfanum o subrayar, por lo que está bien. Silencio
← Duplicar códigos válidos Silencio Ordenar todavía funciona; no se eliminan los duplicados. Si quieres una singularidad, puedes añadir una 'Set' antes de la extracción final. Silencio
Silencio Muy largo `código ' (100 chars) Silencio Podría llegar a la profundidad de recursión o a límites de amortiguación en idiomas con pequeñas pilas. No hay ningún efecto aquí porque n ≤ 100; pero todavía use `StringBuilder`/`vector` pre-allocation in Java/C++. Silencio
← Mixing `True`/`true` in input ← Algunos entrevistadores dan una serie booleana de cuerdas (“True”). Silencio Convertir `isActive[i]` a Boolean (`isActive[i] == "true"`). Silencio
← Leading/trailing whitespace Silencio Regex `[A-Za-z0-9_]+` rechazará los espacios, pero la gente a veces se recorta primero. Sin recortar requerido por la especificaciones. Silencio

-...

### 4.6 Clean‐Code Solution – Why It Looks Good

1. **Single Responsibility** – `validateCoupons` hace *exactamente* lo que su nombre dice.
2. ** Mapa de Orden Inmutable** – `Map. of(...)` o `static constexpr` mantiene la prioridad constante y segura de los hilos.
3. **Expresión regional** – Una sola línea (`^[A-Za-z0-9_]+$`) encapsula toda la lógica de validación del código.
4. ** Comparador Moderno** – Lambda de Java + `entoncesComparing` lee como un requisito de negocio.
5. **Contenedor MInimal** – La clase interna de `Coupon` sólo contiene los datos necesarios para ordenar.
6. **Pre-alubicación** – `result.reserve(valid.size()))` evita reasignaciones innecesarias en C++/Java.

■ **Entreview Tip** – Cuando se le preguntó sobre este problema, diga: *“Usé un pequeño mapa de búsqueda para la prioridad empresarial y un reex para el código. Eso me permite filtrar en tiempo lineal y luego ordenar en O(n log n), lo cual es óptimo para las limitaciones.”*

-...

### 4.7 Código de Full-Stack – Copiar & Pegar

■ Cada fragmento de abajo compila en el último JDK 17 / CPython 3.10 / GCC 12.

Silencio Idioma Silencio Código Silencio
Silencio...
Silencio **Java** vocablos [Continúe] [Continúe]] ORDER.get(c.businessLine))\n .thenComparing(c - título c.code));\n Lista seleccionadaString Resultado = nuevo ArrayList recomendado(valid.size());\n para (Coupon c : valid) resultado.add(c.code); \n resultado de retorno;\n }\n\n privado clase estática Coupon {\n final String code;\n final String businessLine;\n Coupon(String code, String businessLine) {\n this.code = code;\n this.businessLine = businessLine;\n }\n\n}\n`\n``\n`\n `` ``''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''' Silencio
Silencio **Python** Нателенилиниханиенниханихинанихинаниениниенининанинининанининанининанинининия \": \"restaurante\": 3\n\" válido\n" Coupons(self, code: List[str], businessLine: List[str], isActive: List[bool]) - Wishlist[str]:\n pattern = re.compile(r'^[A-Za-z0-9_]+$')\n valid = [\n (c, bl) for c, bl, act in zip(code, businessLine) ORDER\n ]\n valid.sort(key=lambda x: (self.ORDER[x[1]], x[0]))\n return [c for c, _ in valid]\n``\n `` ``\n interpretado/detalles confianza Silencio
tención **C+** Silencioso {\nMicrosoft Sans Serif} {\nMicrosoft Sans Serif}\nMicrosoft Sans Serif} valido;\n para (size_t i = 0; i Identifica code.size(); ++i) {\n si (!isActive[i]) continuar;\n si (código[i].empty() tención!regex_match(código[i], patrón)) continuar;\n if (order.count(businessLine[i])) 0) devolver p < 0;\n devolver a.first Identificado b.first;\n });\n vector asignadostring confianza res;\n res.reserve(valid.size());\n for (auto &p : valid) res.push_back(p.first);\n return res;\n }\n};\n`\n ``\n `\n `\n `contrados/details] Silencio

-...

### 4.8 Take‐ Lista de verificación para entrevistadores

- ✅ **Lea la especificaciones cuidadosamente** - cada regla importa.
- ✅ **Use a priority map** – mantiene la lógica de clasificación legible.
- ✅ **Validar con un único reex** – evitar sobre-ingenierar el patrón.
- ✅ **Sorta con una comparación estable** – primera clave primero, luego segundo.
- ✅ **Retorno sólo los datos que se le pide** – no filtre objetos internos.

Siéntase libre de pegar los fragmentos de idioma específico en su currículum o en la sección "Mis Soluciones" de su perfil GitHub. Cuando el entrevistador pregunta “¿Cómo lo harías en otro idioma?” ya tendrás una respuesta lista para copiar.

-...

### 4.9 Pensamientos de clausura

*Coupon Code Validator* puede sentirse trivial en papel, pero es un excelente **micro‐test** de las prácticas de código limpio:

- **Parsing & Validation** – muestra que puedes escribir y razonar sobre regex.
- **Mapping & Sorting** - demuestra familiaridad con las tablas de búsqueda y comparadores personalizados.
- **Edge‐Case Awareness** – demuestra que tienes cuidado con `null`, cadenas vacías, y datos inválidos.

Así que la próxima vez que estés en una entrevista de codificación, dale a este problema un pulgar hacia arriba, y cuando lo codifica, mantenerlo tan limpio como el snippet arriba. Impresionará a los gerentes de contratación, marcará puntos en la entrevista, y se verá muy bien en su currículum. ¡Feliz codificación!