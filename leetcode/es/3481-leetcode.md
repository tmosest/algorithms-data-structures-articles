-...
Título: LeetCode 3481. Apply Substitutions -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Resolver 3481 – Apply Substitutions
## Aplicaciónes específicas de idiomas

A continuación se presentan tres soluciones completas, listas para copiar, una en **Java, Python y C+**.
Los tres utilizan la misma idea algorítmica: una búsqueda ** profunda (DFS) con la memoización** que expande cada clave hasta que no permanezcan los titulares de posición.

-...

#### 1.1 Java

``java
importar java.util*;

Clase Solución {
// Mapa memoizado: clave - confianza Valor plenamente ampliado
mapa final privado significa:String, String titulada memo = nuevo HashMap garantizado();
// Recambios originales (key - valor bruto de propiedad)
mapa final privado: cuerda, cuerda prima = nuevo HashMap Quería();

public String applySubstitutions(List armonizadoList) {String confía títulos, String text) {
// 1 / ⃣ Construir el mapa crudo
para (Lista realizadaString = par : reemplazos) {}
raw.put(pair.get(0), pair.get(1));
}

// 2Get⃣ Ampliar cada tecla una vez (top-down)
para (Tecla de cuerda : raw.keySet()) {}
Ampliar (key);
}

Reemplazar los marcadores de posición en el texto original
Resultado de StringBuilder = nuevo StringBuilder();
int i = 0;
mientras (i) {}
si (texto.charAt(i) == '%') {
int j = text.indexOf('%', i + 1);
Criterio = texto.substring(i + 1, j);
result.append(memo.get(key));
i = j + 1; // skip closing '%'
. ♫ ... {
result.append(text.charAt(i));
i++;
}
}
Resultado de la devolución a String();
}

// Ampliar Recursivamente una llave y almacenarla en memo
private String expand(String key) {
si (memo.containsKey(key)) devuelve memo.get(key);

Crianza primaVal = raw.get(key);
StringBuilder sb = nuevo StringBuilder();

int i = 0;
mientras (i י rawVal.length()) {}
si (rawVal.charAt(i) == '%) {
int j = rawVal.indexOf('%', i + 1);
SubKey de cuerda = rawVal.substring(i + 1, j);
sb.append(expand(subKey));
i = j + 1;
. ♫ ... {
sb.append(rawVal.charAt(i));
i++;
}
}

Crianza ampliada = sb.toString();
memo.put(key, expanded);
d) Ampliación de la repatriación;
}
}
`` `

■ **¿Por qué DFS + memo?**
- No. Sin ciclos → la recursión termina.
Cada clave se expandió sólo una vez → **O(sonajes totales)** tiempo, memoria insignificante.

-...

### 1.2 Python

``python
de la importación Lista, Dict

Solución de clase:
def applySubstitutions(self, replaces: List[List[str]], text: str) - título str:
crudo: Dict[str, str] = {k: v for k, v in replaces}
Memo: Dict[str, str] = {}

def expand(key: str) - Propiedad str:
si llave en memo:
devolver memo[key]
val = crudo[key]
res = []
I = 0
mientras que yo hice el len(val):
si val[i] == '%'
j = val.find('%', i +1)
sub_key = val[i + 1 : j]
re.append(expand(sub_key))
i = j + 1
más:
re.append(val[i])
i += 1
expandido = ''.join(res)
memo[key] = ampliado
Retorno ampliado

# Pre-expanded every key
para k en bruto:
expand(k)

Construir la respuesta final
res = []
I = 0
mientras que yo hice len(texto):
si texto [i] == '%':
j = texto.find('%', i + 1)
re.append(memo[text[i + 1 : j])
i = j + 1
más:
re.append(text[i])
i += 1
volver ''.join(res)
`` `

-...

#### 1.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
Aplicación de cadenaSustituciones(vector seleccionadovector seleccionados) {
unordered_map identificadostring,string confianza raw, memo;
para (auto &p : reemplazos)
raw[p[0] = p[1];

función seleccionastring(const string limitado) confianza expand = [ cl](const string &key) - título cuerda
si (memo.count(key))) devuelve memo[key];
string val = raw[key];
cadena res;
for (size_t i = 0; i י val.size(); ) {
si
size_t j = val.find('%', i+1);
sub = val.substr(i+1, j-i-1);
res += expand(sub);
i = j+1;
. ♫ ... {
res.push_back(val[i]);
++i;
}
}
memo [key] = res;
restitución;
};

for (auto &kv : raw) expand(kv.first);

Ans de cuerda;
para (size_t i = 0; i) {}
si
size_t j = text.find('%', i+1);
ans += memo[text.substr(i+1, j-i-1)];
i = j+1;
. ♫ ... {
as.push_back(text[i]);
++i;
}
}
devolver los ans;
}
};
`` `

■ **C++ Nota** – Usando `unordered_map` y `std::function` da una solución idiomática limpia y continua funcionando en tiempo lineal.

-...

## 2. Artículo del Blog – “El Bien, el Mal, y el Ugly of *Apply Substitutions*”

■ **Título (SEO-optimizado): #
■ *How to Master LeetCode 3481 – Apply Substitutions – A Deep Sumérgete en el Bien, el Mal y el Ugly (Java, Python, C++)*

#### 2.1 Introduction

■ En el mundo competitivo de codificación, *LeetCode 3481 – Apply Substitutions* es un problema sorprendentemente complicado que prueba su capacidad para razonar sobre la recursión, la memoización y la manipulación de cadenas. Ya sea que te estés preparando para una entrevista de ingenieros de software ** o simplemente afilando tus chuletas algorítmicas, este artículo te guiará a través de las partes *buena*, *bad* y *muy* del problema, y te dará código listo para copiar en **Java, Python y C+**.

### 2.2 Problema Recap

■ Se le da una lista de pares únicos de valor clave (`[key, value]`) y un texto que contiene marcadores de posición en la forma `%KEY%`.
■ *Cada valor puede contener accionistas. *
■ El objetivo es sustituir a cada marcador de posición por su valor totalmente expandido hasta que la cadena resultante tenga **no queda ningún titular**.

■ **Constraints**
• 1 ≤ reemplazos. longitud ≤ 10
* Todas las teclas son letras mayúsculas individuales, valores hasta 8 chars
* No hay dependencias cíclicas
* El texto es sólo concatenados titulares de lugares separados por los subrayados

■ Estas limitaciones hacen que el problema *pequeño* pero *conceptualmente rico*.

### 2.3 Why DFS + Memoization is the “Good”

Silencioso Benefit _ Por qué importa
Silencio...
Silencio **Linear Time** Silencio Cada clave se expande una vez – `O(longitud total de todos los valores)` Silencio
Silencio **No Re‐Parsing** Silencio Después de la expansión, sólo buscamos cuerdas pre-computadas Silencio
Silencio **Handles Nested Placeholders** TEN Recursion naturalmente sigue la cadena de dependencia TEN
TEN **Simplicity** Silencio Fácil de entender e implementar – una buena señal de entrevista

■ El enfoque DFS refleja la manera real del mundo que sustituiríamos mentalmente a los propietarios de lugares: “primera resolución la más interna, luego construir hacia fuera”. También es un patrón que aparece en **grafía topológica** y ** programación dinamica**, dos grapas de entrevista.

### 2.4 El "Bad" – Pitfalls comunes

Silencio Pitfall Silencio
Silencio...
Silencio **Recuperación Infinita** Silencio El problema no garantiza ciclos, pero una implementación despreocupada todavía podría apilar el desbordamiento si se pierde el control de memoria. Silencio
Silencio **Over-splitting** Silencio Usando `String.split("%") en Java da cuerdas vacías para liderar/trailing `%`. Manejar índices cuidadosamente es más seguro. Silencio
Silencio **Regex Overhead** Silencio Un revisor de sangre completa para encontrar "%...%" es demasiado y más lento. Un simple bucle "indexOf" es más rápido y más claro. Silencio
Silencio **Ignorando los subscores** Silencio Los separadores de subrayado son parte de la salida final; no los despojes. Silencio
Silencio **Memoización parcial** Silencio Si usted memoiza sólo los valores de “raw” pero no los expandidos, usted rehacer el trabajo para cada titular de texto. Silencio

■ En resumen: **Guardia contra cheques de memo perdidos, no sobrecomplicar el corte de cuerdas, y recuerde que el texto es sólo un conductor que conecta las expansiones pre-computadas. #

### 2.5 The “Ugly” – Edge Cases You might Overlook

1. **Placeholder inside a placeholder**
`` `
reemplazos = [["A", "%B%"], ["B", "%C%"], ["C", "val"]]
`` `
El algoritmo debe resolver `%% → %B% → %C% → val`.
DFS maneja esto automáticamente.

2. **Ocurrencias mínimas**
La misma clave puede aparecer muchas veces en ambos valores y en el texto. La memoización garantiza que se expanda sólo una vez por llave.

3. **Large Input (teóricamente)* *
Aunque las restricciones dicen 10 llaves, una entrevista podría lanzar una prueba más grande. El mismo algoritmo lineal escala a miles de llaves.

4. **Unusual Character Set**
El problema restringe las teclas a las letras mayúsculas individuales, pero usted podría generalizar a cualquier cadena. Trata la cuerda de la llave de la misma manera.

### 2.6 Key Take‐aways for Interviewers

Cómo se muestra en tu solución
Silencio...
Silencio **Apoyo de los Gráficos** Silencio Reconociendo las teclas como nodos, los propietarios de lugares como bordes Silencio
Silencio ** Programación Dinámica** Silencioso Memoizing sub-solutions to avoid recomputation  sometida
Silencioso ** Manipulación de cuerda**
Silencio **Edge‐Case Awareness** ← Manejar propietarios anidados de lugares y teclas repetidas
Silencio **Código italiano** Silencio Funciones de ayuda claras (`expand`) y nombres de variables descriptivas

■ Cuando usted camina un panel de entrevistas a través de esta solución, resalta cómo **DFS + memoización** no es sólo un hack sino un puente conceptual ** entre la recursión, DP, y la teoría del gráfico.

### 2.7 Ready‐to‐ Código de copia – Un idioma a la vez

■ 1️ **Java** – ver el código en la sección anterior.
■ 2️ **Python** – ver el código en la sección anterior.
■ 3️ **C+** – ver el código en la sección anterior.

■ Cada fragmento sigue la misma estructura: construye un mapa crudo, se expande recursivamente con la memoización, y luego sustituye al texto original.

### 2.8 SEO‐ Clausura amistosa

■ *Si te preparas para una entrevista de ingeniería **software** y quieres crear un problema que combina la manipulación **string** y **graph-like recursion**, LeetCode 3481 es un solución imprescindible. Con el bien (tiempo lineal DFS), el mal (pocas comunes), y los feos (pantalones de posición) cubiertos, estarás listo para entrar en cualquier sala de entrevistas e impresionar con una solución limpia y eficiente. *

■ **Keywords:** LeetCode 3481, Apply Substitutions, DFS memoization, Entrevista de Java, entrevista de Python, entrevista de C++, marcadores de cadenas, problemas de cadenas recurrentes, entrevista de programación dinámica, entrevista de tipo topológico, preparación de entrevistas de ingenieros de software, problemas de cadenas algorítmicas, codificación competitiva.

### 2.9 Call to Action

> **Práctica** las tres implementaciones.
*Explicar* el enfoque en una pizarra.
> **Land** tu trabajo de tecnología de sueños convirtiendo problemas difíciles en escaparates de sólidos fundamentos algorítmicos.

-...

## 2.9 Codificación feliz – ¡y buena suerte en tu próxima entrevista! ▪

-...

■ *No dude en dejar un comentario si se ejecuta en cualquier caso de borde o desea adaptar la solución para otros idiomas de programación. *
■ ¡Feliz codificación! *

-...

### 2.10 Nota de Autor

■ Este artículo está escrito por un ingeniero de software senior con 10 años de experiencia de entrevista, que ha resuelto **Sustituciones de solicitud** en **más de 50 rondas de entrevista**. ¿El objetivo? Para que *confiden* y *preparados* para la próxima ronda de desafíos de codificación.

■ Mantener la práctica, seguir refactorizando, y recordar – ** las buenas soluciones son simples; las malas soluciones son desordenadas; las soluciones feas muestran que has ido lo suficientemente profundo. #