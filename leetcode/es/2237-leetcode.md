-...
Título: LeetCode 2237. Posiciones de cuenta en la calle con brillo requerido -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recapitulación de problemas (LeetCode 2237)

■ **Posiciones de contacto en la calle con brillo requerido* *
■ *Dificultad:* Medio

Se les da:
* an integer `n` (street is the number line `[0 ... n‐1]`);
* un array `lights` donde cada elemento `[posición, rango]` representa una lámpara de calle que ilumina el intervalo inclusivo
`[max(0, position‐range), min(n‐1, position+range)] `` ;
* un array `requirement` de longitud `n` donde `requirement[i]` es el brillo mínimo que debe tener una posición.

**Objetivo** - devolver el número de posiciones 'i' que el brillo en 'i' es por lo menos `requisito[i]`.

----------------------------------------------------

## 2. Core Idea – Line Sweep / Difference Array

Para cada lámpara podemos aumentar el contador en su frontera izquierda y decrementarlo *después* su frontera derecha.
Cuando escaneamos de izquierda a derecha y mantenemos una suma prefijo en funcionamiento obtenemos el brillo exacto en cada posición.

`` `
diff[ izquierda] += 1
diff[ right+1 ] -= 1 (if right+1 )
`` `

Por último, atraviesa el `diff`, acumula la suma de prefijo, y compártela con la correspondiente `requisición[i]`.
Esto da una solución de tiempo **O(n + m)** (`m = lights.length`) y **O(n)** memoria extra, que es óptima para los límites dados (`n, m ≤ 105`).

----------------------------------------------------

## 3. Implementaciones de referencia

### 3.1 Java 17

``java
importar java.util*;

Solución de la clase pública {}
public int meetRequirement(int n, int[][] lights, int[] requirement) {}
// Difference array
int[] diff = nuevo int[n + 1]; // n+1 para evitar controles de límites

para (int[] lámpara : luces) {}
int pos = lamp[0];
int rng = lamp[1];
int left = Math.max(0, pos - rng);
int right = Math.min(n - 1, pos + rng);

diff[left]+; // inicio de iluminación
diff[right + 1]--; // final de iluminación (inclusive)
}

int prefix = 0; // brillo actual
respuesta int = 0;

para (int i = 0; i)
prefijo += diff[i];
si (prefijo ю= requisito[i]) respuesta++;
}
respuesta de retorno;
}

Arnés de prueba rápido...
public static void main(String[] args) {
Solución s = nueva solución ();

int n1 = 5;
int[][] lights1 = {0,1},{2,1},{3,2};
int[] req1 = {0,2,1,4,1};
System.out.println(s.meetRequirement(n1, lights1, req1)); // 4

int n2 = 1;
int[][] lights2 = {0,1};
int[] req2 = {2};
System.out.println(s.meetRequirement(n2, lights2, req2)); // 0
}
}
`` `

■ **¿Por qué `int[n+1]`?**
■ Añadiendo un centinela al final ( " diff[n] " ) garantiza que el decremento " recto+1 " nunca golpee un índice fuera de límites, simplificando la lógica del lazo.

-...

#### 3.2 Python 3

``python
de la importación Lista

Solución de clase:
def meetRequirement(self, n: int, lights: List[List[int],
requisito: List[int]) - título int:
diff = [0] * (n +1) # n+1 para el centinela

para pos, rng en luces:
izquierda = max(0, pos - rng)
derecho = min(n - 1, pos + rng)
diff[left] += 1
diff[right + 1] -= 1

brillo = 0
respuesta = 0
para i en rango(n):
brillo += diff[i]
si el brillo >= requisito[i]:
respuesta += 1

respuesta


# ----------- rapid tests -----------
si __name_ == "__main__":
sol = Solución()
print(sol.meetRequirement(5, [[0,1],[2,1],[3,2]], [0,2,1,4,1])) # 4
print(sol.meetRequirement(1, [[0,1]], [2]) # 0
`` `

■ **Nota** – Las listas dinámicas de Python están perfectamente bien para `n ≤ 105`.
■ Evitar cualquier pase adicional `O(m)` mantiene la solución inclinada.

-...

### 3.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int meetRequirement(int n, vector asignadovector identificadoint
vectores requeridos {}
vector asignadoint título diff(n + 1, 0); // n+1 sentinel

para (auto & lamp; luces) {}
int pos = lamp[0];
int rng = lamp[1];
int left = max(0, pos - rng);
int right = min(n - 1, pos + rng);

diff[left]+; // start
diff[right + 1]--; // end + 1
}

int prefix = 0;
int ans = 0;
para (int i = 0; i) {}
prefijo += diff[i];
si (prefijo ю= requisito[i]) ++ans;
}
devolver los ans;
}
};

// ------------- arnés de prueba----------------
int main() {}
Solución s;
cout se hizo s.meetRequirement(5, {0,1},{2,1},{3,2}, {0,2,1,4,1})
cout se realizó s.meetRequirement(1, {0,1}, {2})
}
`` `

■ **¿Por qué `vector seleccionado injerto diff(n+1)? * *
■ El centinela garantiza `right+1` nunca sale de límites, dejándonos saltar un condicional dentro del bucle y mantener el código ordenado.

----------------------------------------------------

## 4. Artículo del Blog – “El Bien, el Mal, y el Ugly de LeetCode 2237”

■ *Título*
■ *LeetCode 2237 – Posiciones contables en la calle con brillo requerido: El bueno, el malo, el imprudente – una profunda cueva para entrevistas de trabajo-Ley*

#### 4.1 TL;DR

* **Solución** – Un barrido de rayos de diferencia de tiempo lineal ( barrido de línea).
* ** Complejidad del tiempo** – `O(n + m)` (`n = longitud de la calle`, `m = #lamps`).
* ** Complejidad del espacio** – auxiliar.
* **Por qué importa** – Dominar este patrón muestra que puede convertir un problema aparentemente cuadrático en un elegante `O(n)` uno, una habilidad apreciada para entrevistas de diseño de sistema y algoritmo.

-...

### 4.2 El problema, re-framed

Imagínese un camino recto con `n` intersecciones (0-basadas).
Cada faro ilumina un segmento contiguo de intersecciones.
Se le da un requisito de brillo mínimo** en cada intersección y debe contar cuántas intersecciones lo satisfacen.

■ ¿Por qué la dificultad? * *
■ Un enfoque ingenuo itera sobre cada lámpara para cada intersección → `O(n·m)` → demasiado lento para `105`.
■ La clave es tratar cada lámpara como una contribución *intervalo* y combinarlos inteligentemente.

-...

### 4.3 The Good – Line Sweep + Difference Array

1. **Intervalos → Actualizaciones Prefix**
*Por cada lámpara*
``text
diff[l] += 1 // inicio de iluminación
diff[r+1] -= 1 // una pasada el final
`` `
Porque la lámpara cubre `[l, r]` inclusivamente.

2. **Paso sencillo para completar brillo* *
Correr la suma de prefijo sobre `diff` da el brillo exacto en cada posición.
Mientras se escanea, compare con el requisito y cuente la respuesta.

3. *Por qué funciona*
El array *difference* almacena el cambio *net* en cada índice.
La suma acumulativa reconstruye la matriz original de recuentos de brillo.

4. Resultado**
*Tiempo de iluminación, trabajo adicional constante por lámpara y por intersección. *
Funciona para los peores límites de casos fácilmente.

-...

### 4.4 The Bad – Pitfalls & Edge Cases

Silencio Pitfall Silencio Por qué duele Silencio
Silencio--------------------------
Silencio **Off‐by-one en el límite derecho** Silenciosos Lamps cover *inclusive* ranges; olvidándose de las roturas de decremento `derecha+1` cuenta al final. Silencio Explicitly decrement at `right+1` (or use `n` sentinel). Silencio
Silencio ** Index out of bounds** Silencio `right+1` puede ser `n`; si el tamaño de la matriz es `n`, `diff[n]` es inválido. ← Allocate `diff[n+1]` o añadir un guardia antes de decrementar. Silencio
No en las limitaciones, pero si 'range' fuera negativo, las matemáticas estarían equivocadas. TENCIÓN DE LA CAMPAÑA A LA PROPAGACION con `max/min`. Silencio
Silencio **Large values overflow** TEN `range` up to `105`; using `int` is safe, but if extended, use `long`. TEN Use `long` or careful casting if necessary. Silencio

-...

### 4.5 The Ugly – When Simpler No es suficiente

- **Memory‐Bounded Systems** – La matriz de `O(n)` puede ser todavía pesada si `n` Ω `109 ` (fuentes fuera de LeetCode).
*Alternativa:* comprime coordenadas o usa un BST equilibrado de eventos.
Aquí no es necesario, pero vale la pena saberlo.

- Preguntas frecuentes Si tuviera que responder a muchos arrays de requisitos en el mismo conjunto de lámparas, recomputar el barrido cada vez sería desperdicio.
*Optimización:* Precomputar la matriz de brillo una vez; cada consulta es la comparación de `O(n).

- ** Cuestiones de Precisión en Otros Idiomas** – En JavaScript o Python, el uso accidental de 'float' puede causar errores sutiles con grandes enteros.
*Fix:* Pegue a la aritmética entero y evite conversiones de tipo implícito.

-...

### 4.6 SEO‐ Resumen amistoso

■ *Buscando una **Java**, **Python**, o **C++** solución a LeetCode 2237 – “Posiciones de la Casa en la calle con brillo requerido”?
■ Maestro el barrido **line** y **Diferencia array** técnica para resolver este problema en **O(n + m)** tiempo y **O(n)** espacio.
■ Aprenda a evitar errores comunes como errores fuera por uno e índice fuera de límites, y vea por qué este patrón es un conocimiento imprescindible para las entrevistas de diseño del sistema y algoritmo. *

-...

### 4.7 Final Word

LeetCode 2237 es más que un rompecabezas de la carretera; es un microcosmos de problemas de agregación de intervalos que encontrarás en sistemas de producción (por ejemplo, actualizaciones de rango en bases de datos, modelado de tráfico).
Ser capaz de identificar e implementar el barrido **Diferencia-array** demuestra:

* ** Flexibilidad algorítmica** – convirtiendo un problema cuadrático aparente en tiempo lineal.
* **Disciplina de codificación** – manejo minucioso de límites y bucles concisos.
* **Preparación para la contratación técnica** – a los entrevistadores de patrones les encanta ver.

Practique las implementaciones anteriores, casos de borde de prueba, y estará listo para discutir este patrón con confianza durante su próxima entrevista de codificación o conversación de diseño de sistema.

-...

**End of Article**

-...

### 5. Pensamientos finales

El barrido de línea *difference‐array* es un patrón clásico que aparece en muchas preguntas de entrevista (por ejemplo, “Número de pasantes superpuestos”, “Personas en un parque”, “Maximal Rectangle”, etc.).
Al dominarlo ahora, usted estará equipado para abordar retos de agregación de intervalos similares en los sistemas del mundo real, lo que le hace un candidato más fuerte para los roles de ingeniería de software.

Buena suerte en sus entrevistas de codificación – y recuerde: una solución limpia `O(n)` es siempre una victoria!