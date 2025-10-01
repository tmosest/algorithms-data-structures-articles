-...
Título: LeetCode 2078. Dos casas más elegantes con diferentes colores -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

## 1. Recapitulación del problema – LeetCode 2078
**Dos casas más elegantes con diferentes colores* *
■ **Signature (Java)* *
> `public int maxDistance(int[] colors) `

Se le da un array `colors` donde `colors[i]` es el color de la pintura de la casa *i*‐th (las casas se establecen en una sola línea).
Devuelve la distancia máxima entre cualquier dos casas que son ** pintados en diferentes colores**.
La distancia entre las casas *i* y *j* es `vivi – j eterna`.

Limitaciones
* `2 ≤ n = colores. longitud ≤ 100`
* `0 ≤ colores[i] ≤ 100`
* Hay al menos dos casas con diferentes colores.

-...

## 2. El enfoque directo (O(n2))

``java
Clase Solución {
int public maxDistance(int[] colors) {}
int n = color.length;
int best = 0;
para (int i = 0; i)
para (int j = i+1; j)
si (colores[i] != colores[j]) {}
mejor = Math.max(best, j-i);
}
}
}
devolver mejor;
}
}
`` `

* El tiempo*
****Space** – `O(1)`

Con 'n ≤ 100' esto es lo suficientemente rápido para LeetCode, pero podemos hacerlo mejor.

-...

## 3. El “bueno” – Constante-Espacio, Solución de Tiempo Lineal

La observación clave:
**El par más peludo siempre implicará la primera o la última casa. #
Si tienes un par que no toque el final, siempre puedes mover un extremo del par a un borde y la distancia sólo puede aumentar.

Así que sólo necesitamos examinar dos posiciones:

Silencioso Lo que representa Silencio Por qué importa Silencio
Silencio...
Silencio `i` – casa más izquierda que es *diferente* del último color Silencio más lejos del extremo derecho Silencioso distancia a la última casa = `n-1-i` Silencio
Silencio `j` – casa más derecha que es * diferente* del primer color Silencio más lejos del extremo izquierdo Silencio distancia a la primera casa = `j-0` ←

La respuesta es simplemente `max(j, n-1-i)`.

## Java – Constant Space (O(1) Memory)

``java
Solución de la clase pública {}
int public maxDistance(int[] colors) {}
int n = color.length;
int left = 0; // primer índice de casa
int right = n - 1; // último índice de la casa

// Encuentra la casa más izquierda que difiere del último color
mientras (colores[izquierda] == colores[derecha]) {}
izquierda++;
}

// Encuentra la casa más derecha que difiere del primer color
mientras (colores [derecha] == colores[izquierda]) {}
Bien...
}

// La distancia más alejada es el máximo de dos candidatos
devolver Math.max (derecha, n - 1 - izquierda);
}
}
`` `

### Python – Constant Space (O(1) Memory)

``python
Solución de clase:
def maxDistance(self, colors: List[int]) - Conf int:
n = len(colores)
izquierda, derecha = 0, n - 1

# índice más izquierdo con un color diferente de la última casa
mientras colores[izquierda] == colores[derecha]:
izquierda += 1

# índice más correcto con un color diferente de la primera casa
mientras colores [derecha] == colores[izquierda]:
derecho -= 1

máx (derecha, n - 1 - izquierda)
`` `

### C++ – Constante espacio (O (1) memoria)

``cpp
Clase Solución {
public:
int maxDistance(vector asignadoint ánimo) {}
int n = colors.size();
int left = 0, right = n - 1;

mientras (colores [izquierda] == colores [derecha]) --derecha;
mientras (colores [derecha] == colores[izquierda]) ++izquierda;

volver max (derecha, n - 1 - izquierda);
}
};
`` `

**Las complejidades* *
* **Time** – `O(n)` (one pass for each side, worst case `O(n)` total)
****Space** – `O(1)` (sólo unos pocos índices)

-...

## 4. El “Bad” – ¿Por qué no tetratos con todos los pares

* Complejidad O(n2) – sobrematar para los límites pero todavía fácil de código.
* Funciona para cada escenario, pero desperdicia tiempo de la CPU si `n` crece más allá de 100.

A veces los entrevistadores piden explícitamente la mejor solución posible. Proporcionar una solución cuadrática es una respuesta *bad* porque no muestra la comprensión de la estructura del problema.

-...

## 5. El “Ugly” – Tricky Edge‐ Aplicación de casos

Una versión de buggy puede manejar incorrectamente arrays donde todas las casas tienen el mismo color excepto uno al final.
``java
mientras (colores [0] == colores[i]) i++; // para cuando i == No... 1
// podría convertirme en n, llevando a ArrayIndexOutOfBoundsException
`` `
Asegúrate de **ver los límites** o usar una condición de bucle seguro (`i י n`) y manejar el caso donde no se encuentra color diferente en un lado.

-...

## 6. Extraído para el éxito de la entrevista

1. **Lea el aviso cuidadosamente** – note que la respuesta debe implicar la primera o última casa.
2. **Piensa en invariantes** – el par más lejano siempre tocará un borde.
3. **Proporcione una solución limpia y lineal** – O(n) tiempo, O(1) espacio es óptimo aquí.
4. **Mención de la manipulación de la periferia** – si muestra conciencia de las trampas que demuestra la madurez.
5. **Explica tu razonamiento** – los entrevistadores aman a los candidatos que articulan por qué funciona una solución.

-...

## 7. SEO‐Optimized Blog Post

■ *Título*
■ “Cracking LeetCode 2078 – Two Furthest Houses With Different Colors (Java, Python, C++)”

■ **Meta Descripción**
■ Aprende a resolver LeetCode 2078 en tiempo lineal. Lea las implementaciones Java, Python y C++ constantemente en el espacio, además de consejos para crear su entrevista de codificación.

■ **Header Outline**
■ 1. Declaración de problemas
■ 2. Brute‐Force Approach (O(n2))
■ 3. Solución óptima O(n) – Por qué funciona
■ 4. Aplicación de Java
■ 5. Aplicación de los pitones
■ 6. Aplicación C++
■ 7. Manejo de Edge‐Case " Pitfalls comunes
■ 8. Tomado para entrevistas de codificación
■ 9. Preguntas frecuentes
■ 10. Call‐to‐Action – Practice on LeetCode

■ **Keywords**
■ LeetCode 2078, Two Furthest Houses With Different Colors, coding interview, algoritmo, Java, Python, C++, O(n) solution, espacio constante, consejos de entrevista, preparación de entrevistas técnicas, estructura de datos, complejidad del tiempo, complejidad espacial.

■ ** Enlaces internos**
■ *Enlace a otros blogs de problemas LeetCode en la serie (por ejemplo, 2048, 2099). *

■ ** Enlaces externos**
■ *LeetCode official problem page*, *LeetCode discussion threads*, *HackerRank, CodeSignal resources. *

■ **Ideas de imagen*
■ 1. Diagrama de flujo que muestra por qué el par debe tocar un borde.
■ 2. Código de los francotiradores lado a lado.
■ 3. Un pequeño GIF animado de dos casas que se mueven hacia el borde.

■ *CTA*
■ ¿Listo para tu próxima entrevista de codificación? Resolver más problemas de LeetCode y construir su confianza! ”

-...

## Final Code Repository

Si desea ver las tres implementaciones en un solo repo, clone el siguiente repositorio GitHub:

`` `
git clone https://github.com/yourusername/leetcode-2078-two-furthest-houses
`` `

Contiene:

* `Solution.java `
* `Solution.py `
* `Solution.cpp `
* Un `README.md` con el texto del artículo del blog.

¡Feliz codificación y buena suerte en tu próxima entrevista de trabajo!