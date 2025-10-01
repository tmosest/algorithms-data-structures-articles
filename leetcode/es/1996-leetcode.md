-...
Título: LeetCode 1996. El número de caracteres débiles en el juego -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recapitulación del problema – LeetCode 1996
**El número de caracteres débiles en el juego**

■ Un juego contiene `n` caracteres.
"propiedades [i] = [attack_i , defense_i]` es el ataque y defensa del carácter *i‐th*.
■ Un personaje *i* es *mojo* si existe otro carácter *j* tal que
" attack_j " ataque. **y ** `defense_j  Confeder_i`.
■ Devuelve el número total de caracteres débiles.

**Constraints* *

TENIDA `n` Silencioso 2
Silencio...
Silencioso `attack_i , defense_i` Silencio 1 ... 105 Silencio

El problema es una clásica consulta de dominación de 2 dimensiones y se puede resolver en **O(n log n)** tiempo con un simple tipo + barrido.

-...

## 2. Idea de alto nivel – “Sorting + Greedy Sweep”

1. **Sorta** a todos los personajes por ataque ascendente.
*Si dos personajes tienen el mismo ataque debemos procesar primero a uno con la defensa ** más alta** – de lo contrario un personaje posterior podría considerarse erróneamente débil.
Por lo tanto la clave de clasificación es
``text
(ataque, -defensa) // ataque ascendente, defensa descendente
`` `

2. Después de ordenar, caminar el array **backwards** (desde ataque más alto a menor).
Mantenga una variable `maxDef` que almacena la máxima defensa vista hasta ahora entre los personajes con * ataque más alto*.

3. Para el carácter actual:
* si su defensa se hizo `maxDef` → es débil.
* de otra manera actualice `maxDef` con esta defensa.

4. Cuente a todos esos personajes débiles.

La intuición: un personaje sólo puede ser dominado por un personaje posterior (más alto-ataque). Debido a que procesamos en orden inverso, `maxDef` ya contiene la mejor defensa entre todos los personajes de ataque más alto. Una comparación simple nos dice si el personaje actual está dominado.

-...

## 3. Caminar del Código

A continuación encontrará **ready‐to-copy** implementaciones en:

Silencio Idioma Silencio Clase/Función Silencio Silencio
Silencio...
Silencio Java ¦ `Solution.numberOfWeakCharacters` ¦ Utiliza `Arrays.sort` con una comparación personalizada. Silencio
Silencio Python Silencioso `Solution.number_of_weak_characters` ¦ Utiliza `sort` con llave y un bucle inverso. Silencio
TENIDO C++ TENIDO `Solución::numberOfWeakCharacters` TEN Usos `estd::sort` y un solo pase. Silencio

Cada solución es **O(n log n)** tiempo, **O(1)** espacio extra (además de ordenar la sobrecarga).

-...

### 3.1 Java – `Solution.numberOfWeakCharacters `

``java
importa java.util. Arrays;

Clase Solución {
int numberOfWeakCharacters(int[][] properties) {}
// Ordenar por ataque ascendiendo; si corbata, defensa descendiendo
Arrays.sort(properties, (a, b) - Propiedad {
si (a[0] == b[0]) devolver Integer.compare(b[1], a[1]); // superior defense first
integer.compare(a[0], b[0]); //
});

int débil = 0;
int maxDef = 0; // mejor defensa vista hasta ahora entre ataque más alto
para (int i = properties.length - 1; i >= 0; i--) {
int def = properties[i][1];
si (def < maxDef) débil++;
Max Def = def; // nuevo registro
}
Retorno débil;
}
}
`` `

-...

### 3.2 Python – `Solution.number_of_weak_characters `

``python
Solución de clase:
def number OfWeakCharacters(self, properties: List[List[int]) - título int:
# Sort by attack ascending, defense descending
propiedades.sort(key=lambda x: (x[0], -x[1]))

débil = 0
max_def = 0
for _, def_val in reversed(properties):
si def_val
débil += 1
más:
max_def = def_val
Retorno débil
`` `

-...

### 3.3 C++ – `Solution::numberOfWeakCharacters `

``cpp
Clase Solución {
public:
número de intOfWeakCharacters(vector seleccionadovector asignadoint implica propiedades iguales) {}
(propiedades.begin(), properties.end(),
[](cont vector identificadoint ánimo a, const vector identificadoint círculo b) {
si (a[0] == b[0]) devuelve un[1] √≥n b[1]; // superior defense first
retorno a[0] ANTEB[0]; // menor ataque primero
});

int débil = 0;
int maxDef = 0;
para (int i = properties.size() - 1; i ±= 0; --i) {
int def = properties[i][1];
si (def < maxDef) ++weak;
Max Def = def;
}
Retorno débil;
}
};
`` `

-...

## 4. Análisis de la complejidad

Silencioso ** Métrico**
Silencio...
tención Tiempo Silencioso **O(n log n)** – dominado por el paso de clasificación. Silencio
TENIDO Espacio Extra TENIDO **O(1)** – sólo algunas variables entero. (El tipo en sí puede utilizar el espacio de pila O(log n). Silencio

-...

## 5. Casos de borde " Pitfalls

Problema de la vida Ø Lo que fue incorrecto
Silencio...
Silencio Dos personajes tienen el mismo ataque Silencio Ordenar sólo por ataque puede marcar el segundo débil incorrectamente Silencio Ordenar por defensa descender cuando ataque lazos ¦
Silencio Muy grande `n` (105) tóxico Usar un bucle anidado O(n2) causa TLE tóxico Usa el barrido codicioso organizado
Silencio Valores defensivos en los límites Silencio No se necesita un manejo especial – algoritmo funciona para todos los valores
tención Empty input ¦ Constraints guarantee `n ≥ 2`, pero el código defensivo puede manejar `n=0` Silencio

-...

## 6. El Bien, el Mal, y el Ugly

Silencio Silencio
Silencio...
tención ** Algorithm** TENSIÓN Solución simple O(n log n) – fácil de razonar e implementar TEN O(n2) fuerza bruta es demasiado lenta para 105 ANTE Una solución “magia” O(n) que se basa en una gran matriz fija (tamaño 105+2) puede desperdiciar la memoria y ser confuso ANTE
Silencio **Sorting Key** Silencio `(atack, -defense)` es un patrón bien conocido para dominancia 2-D ¦ Olvidar el salto de corbata de defensa → respuesta incorrecta Silencio Ordenar por ataque sólo entonces escanear hacia atrás conduce a errores sutiles ←
Silencio **Espacio** Silencio Espacio auxiliar constante Silencio Ninguno Silencio Usar arrays adicionales de tamaño 105+2 es innecesario Silencio
Silencio **Readability** Silencio Limpiar comparador o función clave Silencioso bucles anidados, demasiadas variables Silencio Principalmente terse un código de línea que sacrifica claridad Silencio

-...

## 7. SEO‐Optimized Blog Post Draft

■ *Título*
■ LeetCode 1996 – El número de caracteres débiles: Java, Python & C++ Soluciones + consejos de entrevista
■ **Meta‐Description:**
■ Master LeetCode 1996 en menos de 15 minutos. Aprenda el O(n log n) clasificación + solución de barrido codicioso en Java, Python y C++. Obtenga entrevistas preparadas con trampas, periferias y consejos de búsqueda de empleo.

-...

### 7.1 Introduction

Si estás preparando una entrevista de ingeniería de software, seguramente te encontrarás con **LeetCode 1996 – "El número de caracteres débiles"**. Este problema de media-dificultad prueba su comprensión de dominancia 2-D y clasificar trucos. A continuación se muestra una profunda inmersión en la solución más eficiente, además de las implementaciones listas a paso en Java, Python y C++. También caminaré a través de las trampas comunes, por qué el barrido codicioso funciona, y cómo este conocimiento puede aumentar su curriculum vitae.

-...

### 7.2 Declaración de problemas (Re-phrased)

Se le da un array 2-D `properties`, cada elemento `[ataque, defensa]`. Un personaje *i* es **weak** si otro personaje *j* tiene ** ataque estrictamente superior y defensa estrictamente superior**. Cuenta cuántos personajes son débiles.

-...

## 7.3 Why the O(n log n) Greedy Sweep Works

1. **Dominance in 2‐D** – Un personaje sólo puede ser dominado por un personaje que es a su derecha cuando se clasifica por ataque.
2. **Sorting Key** – Cuando los ataques se atan, el personaje con * más alto* defensa domina el que con *más bajo* defensa. Ordenar por `(ataque, -defensa)` asegura que el "bueno" aparece primero.
3. **Sweep Backwards** – Caminando desde el personaje más adecuado hasta el más izquierdo, mantenemos `maxDef`, la mejor defensa entre los personajes ya vistos (más alto-ataque).
4. ** Comparación de silencio** – Si la defensa actual se hizo `maxDef`, el carácter actual es débil; de lo contrario, actualice `maxDef`.

No se requieren estructuras de datos adicionales, haciendo que el algoritmo sea limpio y rápido.

-...

## 7.4 Code Implementations

■ **Consejo:** Pruebe estos fragmentos directamente en su editor de soluciones LeetCode.

##### Java

``java
importa java.util. Arrays;

Clase Solución {
int numberOfWeakCharacters(int[][] properties) {}
Arrays.sort(properties, (a, b) - Propiedad {
si (a[0] == b[0]) devuelve Integer.compare(b[1], a[1]);
integer.compare(a[0], b[0]);
});

int débil = 0;
int maxDef = 0;
para (int i = properties.length - 1; i >= 0; i--) {
int def = properties[i][1];
si (def < maxDef) débil++;
Max Def = def;
}
Retorno débil;
}
}
`` `

#### Python

``python
Solución de clase:
def number OfWeakCharacters(self, properties: List[List[int]) - título int:
propiedades.sort(key=lambda x: (x[0], -x[1]))
débil, max_def = 0, 0
for _, def_val in reversed(properties):
si def_val
débil += 1
más:
max_def = def_val
Retorno débil
`` `

###### C++

``cpp
Clase Solución {
public:
número de intOfWeakCharacters(vector seleccionadovector asignadoint implica propiedades iguales) {}
(propiedades.begin(), properties.end(),
[](cont vector identificadoint ánimo a, const vector identificadoint círculo b) {
si (a[0] == b[0]) devuelven un[1]  título b[1];
devolver a [0]
});

int débil = 0, maxDef = 0;
para (int i = properties.size() - 1; i ±= 0; --i) {
int def = properties[i][1];
si (def < maxDef) ++weak;
Max Def = def;
}
Retorno débil;
}
};
`` `

-...

### 7.5 Edge‐ Casos que debe cubrir

Por qué importa su código
Silencio...
Silencioso `properties = [[2,1],[2,1]]
Silencio Ataduras de ataque con la reducción de la defensa ← Mis-order → dominancia errónea  durable Use `-defense` en key/comparator Silencio
Silencio Grande `n` Silencio Brute force O(n2) times out ← Usar el barrido codicioso sólo ←

-...

### 7.6 Interview‐Level Questions to Ask

Durante una entrevista real, el entrevistador podría probar:

* “¿Y si necesitas contar * caracteres no débiles* en su lugar? ”
* “¿Puedes alcanzar el tiempo O(n) usando un árbol Fenwick? ”
* ¿Y si el tamaño de entrada es 106? Soluciones de memoria amigables? ”

Estas preguntas determinan su profundidad de comprensión y adaptabilidad.

-...

### 7.7 Añadiendo la Solución a Tu Resumen

■ **Por qué importa:** Los entrevistadores aman soluciones concisas y óptimas.
■ **Resume wording example:**
• Aplicación de una solución **O(n log n)** para el problema LeetCode “El número de caracteres débiles” mediante la clasificación + barrido codicioso en Java, Python y C++.
• Experiencia demostrada en dominancia de 2-D, diseño de algoritmos y intercambios de tiempo-espacio.

Incluya el enlace GitHub o el fragmento de código en una cartera o como referencia de proyecto.

-...

## 7.8 Pensamientos de clausura

LeetCode 1996 es un pequeño problema con una gran lección: *ordenar asuntos.* Recuerde el truco de `(ataque, -defensa)`, barrer de derecha a izquierda, y pasará este problema en un flash. Aplicar el mismo patrón a cualquier problema de “dominio” que vea en entrevistas. Buena suerte, ¡y sigue codificando!

-...

## 8. Palabras finales

Ahora posees:

* Una solución **robust, óptima**.
* **Three language‐specific snippets** que correrá rápido en LeetCode.
* * *Common pitfalls** para protegerse contra.
* Una historia** se puede tejer en la narrativa de la entrevista.

¡Feliz entrevista!

-...

*No dude en adaptar el borrador del blog a su propia voz o plataforma. *