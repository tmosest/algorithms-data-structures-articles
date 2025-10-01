-...
Título: LeetCode 1092. Supersequence Común más corto -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## Shortest Common Supersequence (LeetCode 1092) – The Good, The Bad, The Ugly
**Keywords:** *Shortest Common Supersequence, LCS, Dynamic Programming, LeetCode 1092, coding interview, Java, Python, C+*

-...

### 1. Panorama general de los problemas

TENIDO ANTERIOR ANTERIOR ANTERIOR
Silencio...
Silencio **Nombre** Silencio La supersequencia común más corta
Silencioso **LeetCode ID**
Silencio **Dificultad**
Silencio ** Entrada** tención Dos cadenas de minúsculas `str1` y `str2` (1 ≤ len ≤ 1000)
Silencio **Output** Silencio La cadena *eshortes* que contiene tanto `str1` como `str2` como subsequences. Si existen múltiples soluciones, devuelve cualquiera. Silencio
Silencio **Ejemplo** Silencio `str1 = "abac"`, `str2 = "cab" → `"cabac" Silencio

Un *subsequence* se obtiene eliminando cero o más caracteres de una cuerda sin cambiar el orden de los caracteres restantes.

-...

### 2. Why This Problem Rocks Your Interview Portfolio

*Exámenes DP mastery* – Necesitas el clásico *Longest Common Subsequence* (LCS) truco, un básico en muchas entrevistas.
*Demuestra una reconstrucción inteligente* Después de computar LCS, debe construir la supersequencia en tiempo lineal.
- **Scales agradablemente** – Maneja hasta 1000 caracteres de cuerdas cómodamente con O(m × n) tiempo > O(m × n) espacio.

-...

### 3. Intuición " The Two‐Step Strategy

1. **Compute LCS**
El LCS le dice el “core” más largo de las dos cuerdas. Los personajes de la LCS deben aparecer *una vez* en la respuesta final.

2. **Merge mientras camina hacia atrás* *
Partiendo de los extremos de ambas cuerdas, caminar hacia el comienzo utilizando la tabla DP para decidir si:
- Tomar un carácter común (si es igual).
- Tomar un personaje de una sola cadena (si es diferente y el valor DP indica una mejor opción).

Finalmente, prependió cualquier personaje restante de cualquiera de las dos cadenas. La cadena resultante es la supersequencia común más corta (SCS).

-...

### 4. Mesa de programación dinámica

Vamos.

- `m = str1.length`, `n = str2.length`.
- `dp[i][j]` = longitud de LCS de `str1[0 ... i‐1]` y `str2[0 ... j‐1]`.

Transición:

`` `
si str1[i-1] == str2[j-1]:
dp[i][j] = 1 + dp[i-1][j-1]
más:
dp[i][j] = max(dp[i-1][j], dp[i][j-1])
`` `

Inicializar `dp[0][*] = dp[*][0] = 0`.

-...

### 5. Reconstrucción del SCS

``text
i = m, j = n, result = []

mientras que yo √≥ 0 y j √≥ 0
si str1[i-1] == str2[j-1]:
result.append(str1[i-1])
Yo...
elif dp[i-1][j] √≥ dp[i][j-1]:
result.append(str1[i-1])
Yo...
más:
result.append(str2[j-1])
J...

mientras que yo 0:
result.append(str1[i-1]); i--
mientras j 0:
result.append(str2[j-1]); j--

retorno inverso(resultado)
`` `

El paso "reverso" es necesario porque construimos la respuesta desde el final hacia atrás.

-...

### 6. Análisis de la complejidad

TENCIÓN TERRITOR TENIDA Cálculo
Silencio----------
Silencio **Tiempo** Silencio O(m × n) – DP table + linear back-tracking Silencio
Silencio **Espacio** Silencio O(m × n) – Mesa DP (puede reducirse a O(n) si sólo mantiene dos filas, pero la reconstrucción entonces necesita la mesa completa)

Con `m, n ≤ 1000`, esto es cómodamente rápido.

-...

### 7. Lista de verificación Edge‐Case

Silencioso Caso Edge Qué ver para Silencio
Silencio...
Las cuerdas Identical TENIDO Resultado es la cuerda misma (la más corta posible). Silencio
Silencio Ningún personaje común Silencio Resultado es `str1 + str2`. Silencio
Silencio Una cuerda vacía ANTE Result es la otra cadena. Silencio
Silencio Todos los caracteres idénticos pero las cuerdas difieren en la longitud ANTE Result length = max(len1, len2). Silencio

-...

### 8. Implementación – Java, Python, " C++

■ **Consejo:** Mantenga su código limpio y agregue comentarios en línea para la legibilidad – entrevistadores apreciar la lógica clara.

-...

##### 8.1 Java

``java
*
* LeetCode 1092 – La supersequencia común más corta
*/
Clase Solución {
public String shortestCommonSupersequence(String str1, String str2) {
int m = str1.length(), n = str2.length();
int[][] dp = nuevo int[m + 1][n + 1];

// Build LCS DP table
para (int i = 1; i) =
para (int j = 1; j <= n; j+) {}
si (str1.charAt(i - 1) == str2.charAt(j - 1))
dp[i][j] = 1 + dp[i - 1][j - 1];
más
dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
}
}

/ Reconstruct SCS
StringBuilder sb = nuevo StringBuilder();
int i = m, j = n;
mientras que (i √≥ 0 " 0) {
si (str1.charAt(i - 1) == str2.charAt(j - 1) {)
sb.append(str1.charAt(i - 1));
i... j...
} si (dp[i - 1] [j]
sb.append(str1.charAt(i - 1));
i...
. ♫ ... {
sb.append(str2.charAt(j - 1));
j...
}
}

mientras (i > 0) { sb.append(str1.charAt(--i)); }
}

devolver sb.reverse().toString();
}
}
`` `

-...

#### 8.2 Python

``python
LeetCode 1092 – La supersequencia común más corta
Solución de clase:
def shortestCommonSupersequence(self, str1: str, str2: str) - confiar str:
m, n = len(str1), len(str2)
# DP table
dp = [0] * (n + 1) para _ en rango(m + 1)]

para i en rango(1, m + 1):
para j en rango(1, n + 1):
si str1[i-1] == str2[j-1]:
dp[i][j] = dp[i-1][j-1] + 1
más:
dp[i][j] = max(dp[i-1][j], dp[i][j-1])

# Backtrack to build SCS
i, j = m, n
res = []
mientras yo y J:
si str1[i-1] == str2[j-1]:
re.append(str1[i-1])
i -= 1; j -= 1
elif dp[i-1][j] √≥ dp[i][j-1]:
res.append(str1[i-1]); i -= 1
más:
res.append(str2[j-1]); j -= 1

res.extend(reversed(str1[:i]))
res.extend(reversed(str2[:j]))
volver ''.join(reversed(res))
`` `

-...

#### 8.3 C++

``cpp
// LeetCode 1092 – La supersequencia común más corta
Clase Solución {
public:
string shortestCommonSupersequence(string str1, string str2) {
int m = str1.size(), n = str2.size();
vector seleccionado(n + 1, 0)

// Construir la mesa LCS
para (int i = 1; i)
para (int j = 1; j)
dp[i][j] = (str1[i-1] == str2[j-1]) ?
dp[i-1][j-1] + 1 :
max(dp[i-1][j], dp[i][j-1]);

/ Reconstruct SCS
cadena res;
int i = m, j = n;
mientras (i ' t
(str1[i-1] == str2[j-1]) {
res.push_back(str1[i-1]);
--i; --j;
} si (dp[i-1][j] не dp[i][j-1]) {}
res.push_back(str1[i-1]);
-i;
. ♫ ... {
res.push_back(str2[j-1]);
-j;
}
}
(i) res.push_back(str1[--i));
j) Res.push_back (str2[--j]);

inversa (res.begin(), res.end());
restitución;
}
};
`` `

-...

### 9. El bien

**Clear DP foundation** – LCS es una pregunta de entrevista clásica; reutilizarla aquí demuestra un profundo entendimiento.
Reconstrucción limpia** – Caminar hacia atrás mantiene el código conciso y lineal.
- **Scalable** – O(106) operaciones para el peor caso, muy por debajo de los límites temporales típicos.

-...

#### 10. El “Ugly” – Lo que podría subir

Silencio Pitfall Silencio
Silencio...
Silencio Olvídate de revertir al final de la vida La respuesta se construye desde la cola; invertir es esencial. Silencio
← Errores desactivados por uno en los índices de DP siempre prueban en pequeñas cadenas ( " a " , " b " ), " i-1 " vs " es una fuente frecuente de errores. Silencio
Silencio No manipular los lazos correctamente Silencio Si `dp[i-1][j] == dp[i][j-1]`, eligiendo cualquiera de los trabajos de cuerda; su código maneja esto eligiendo `str2[j-1]`. Silencio
← Espacio Excesivo Silencio Usar una tabla completa de DP está bien, pero puede reducirla a O(n) si tiene cuidado con la reconstrucción. Silencio

-...

### 11. Los malos (common Mistakes)

1. *Usando sólo una fila DP*
- Trabaja para la longitud LCS pero pierdes la tabla completa necesaria para retroceder → conduce al SCS equivocado o la complejidad extra.

2. **Aprobando antes de invertir**
- Muchas soluciones anexan erróneamente a los personajes en orden inverso sin invertir al final → la respuesta será reflejada.

3. **Ignorando la rama común* *
- Algunas fusiones ingenuas olvidan *remove* duplicados de la LCS, produciendo una supersequencia más larga.

-...

### 11.1 Qué evitar en las entrevistas

- **Verbose code** – Mantener funciones cortas; evitar bucles anidados dentro de bucles a menos que sea necesario.
- ** Números de magia no comprometidos** – Siempre explican el significado de `dp[i][j].
- **Igualdad de consumo** – Casos de borde donde una cuerda está vacía deben ser manejados explícitamente para la integridad.

-...

### 11. El Ugly

- **O(m × n) espacio** – Aunque son aceptables, algunos candidatos apuntan al espacio O(n) descartando la tabla antes de tiempo. Esta es una *buena* optimización para mostrar pero complica la reconstrucción.
- **Pocamientos de rastreo de nuevo** – Obtener la dirección equivocada produce una respuesta *sub-optimal*; comprobar doblemente las transiciones de DP contra casos de prueba.

-...

### 11. El Ugly – Cuando Es un problema

- **Large input** – Si el juez impone límites estrictos de memoria, una mesa de 1000×1000 (Equipo 4 MB en Java) todavía puede estar bien, pero para 104 podría explotar.
- **Multiple pasa** – Re-computing DP o reconstruir dos veces derrota la etiqueta “hard”.

-...

### 11. Quick Fix for Space‐Constrained Environments

Si debe caber en 1 MB, mantenga dos filas de `dp` mientras se construye, pero *store* toda la mesa *sólo* si necesita reconstrucción. De lo contrario, se puede reconstruir sobre la mosca con un enfoque codicioso de dos puntos que podría producir una respuesta más larga pero todavía válida para las duras limitaciones.

-...

#### 10. Pensamientos finales

Usted acaba de caminar a través de un *hard* problema que hermosamente re-packages un *fácil* DP truco (LCS). Entregar cualquiera de las tres implementaciones anteriores en una entrevista impresionará a los gerentes de contratación y demostrará que está listo para **Hard‐DP** preguntas.

■ **Pro-Tip:** Pare esta solución con una explicación sucinta de la lógica subyacente del DP – esa es la combinación que convierte a un buen candidato en uno grande.

¡Feliz codificación y feliz entrevista! 🚀

-...

■ *No dude en copiar-pasar los fragmentos de código en su IDE favorito, ejecutarlos contra los ejemplos proporcionados, y compartirlos en su cartera o LinkedIn para mostrar sus chuletas de solución de problemas. *