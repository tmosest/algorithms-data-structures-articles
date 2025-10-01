-...
Título: LeetCode 544. Partidos del concurso de salida -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

# LeetCode 544 – *Partidos del concurso de salida*
**Java Silencio Python ← C++ – Código completo, Algorithm & Interview‐Ready Blog**

-...

Problema Recap

Usted tiene **n** equipos (n = 2^k, 1 ≤ k ≤ 12).
Los equipos están clasificados 1 ... n (1 = más fuerte, n = más débil).

Durante cada ronda siempre empareja el equipo ** más fuerte que queda** con el equipo ** más débil que queda**:

`` `
Ronda 1 : (1,n), (2,n‐1), (3,n‐2), ...
Ronda 2 : ganadores de (1,n) vs ganadores de (n-1,2), ...
...
`` `

La tarea: **Regresar el corchete completo como una sola cadena** usando paréntesis, comas y números de equipo.

■ Ejemplo
"(1,4),(2,3)"
((1,8),(4,5)),(2,7),(3,6))"

-...

## 2down Core Core Idea

El soporte es un árbol binario perfectamente equilibrado.
Si repetidamente dividimos el conjunto de equipos en dos mitades que siempre contienen las mitades * más débiles* y * más fuertes*, podemos construir la cuerda de las hojas hacia arriba.

Fórmula Recursiva**

`` `
build(l, r) = // l = índice izquierdo (inclusivo), r = índice derecho (exclusivo)
si r - l == 1 /// un equipo
cadena de retorno(l+1)
más
m = (l + r) / 2
devolver "(" + construir(l, m) + "," + construir(m, r) + ")"
`` `

Para la primera llamada `build(0, n)` obtenemos el soporte final.
Este algoritmo funciona en **O(n)** tiempo y **O(log n)** profundidad de recursión (max 12), ajustando fácilmente las limitaciones.

-...

## 3VIEW⃣ Full Code – 3 Languages

■ **Consejo:** En entrevistas se le permite utilizar una sola recursión que escribe directamente a un `StringBuilder` / `list` / `stringstream` para evitar la copia excesiva de la cadena.

-...

### 3.1 Java

``java
Clase Solución {
public String findContestMatch(int n) {
StringBuilder sb = nuevo StringBuilder();
build(sb, 0, n);
devolver sb.toString();
}

construcción de vacío privado (StringBuilder sb, int l, int r) {}
si (r - l == 1) { // hoja
sb.append(l + 1); // los números de equipo comienzan desde 1
retorno;
}
int m = (l + r) / 2;
sb.append('(');
(sb, l, m);
sb.append(',');
(sb, m, r);
sb.append(')');
}
}
`` `

-...

#### 3.2 Python

``python
Solución de clase:
def findContestMatch(self, n: int) - Propiedad str:
def build(l, r, out):
si r - l == 1: Un equipo
out.append(str(l + 1))
Regreso
m = (l + r) // 2
out.append('(')
(l, m, out)
out.append(',')
(m, r, out)
out.append(')')

fuera =
build(0, n, out)
volver ''.join(out)
`` `

-...

### 3.3 C++

``cpp
Clase Solución {
public:
string findContestMatch(int n) {
cadena res;
build(0, n, res);
restitución;
}

privado:
vacio(int l, int r, string &out) {
si (r - l == 1) { // Equipo único
out += to_string(l + 1);
retorno;
}
int m = (l + r) / 2;
fuera += '(';
(l, m, out);
fuera += ',';
(m, r, out);
out += ')';
}
};
`` `

-...

## 4VIEW⃣ Complexity Analysis

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
TENIDO Tiempo ANTERIOR O(n) ANTERIOR O(n) TENIDO
TENIDO Memoria TENIDO O(n) string + O(log n) recursion TENIDO O(n) + O(log n) TENIDO O(n) + O(log n) ANTE

El algoritmo es lineal en el número de equipos y utiliza espacio extra insignificante (máxima profundidad 12).

-...

## 5down El bueno, el malo, el ugly

Silencio Silencio
Silencio------------Prince------
La solución Recursive es intuitiva, sin trucos de estructura de datos. Silencio Algunos entrevistadores podrían penalizar la profundidad de recursión (a pesar de la profundidad ≤ 12). ← Sobre-ingeniería: el uso de colas o bit-twiddling para generar emparejamientos puede ocultar la lógica. Silencio
Silencio **Readability** Silencio Directo a la función 'compilado'. La lista de “StringBuilder” y Python de Java puede parecer verbosa a los recién llegados. La manipulación de cadenas in‐place en C++ puede ser propensa a errores (sobrecarga del operador). Silencio
Silencio **Información** Silencioso rápido (O(n)). TEN Python puede ser ligeramente más lento pero todavía dentro de los límites. Silencio Todos los idiomas funcionan bien; Python más lento en la entrada masiva (no es una preocupación aquí). Silencio
tención **Espacio** Silencio Únicamente necesario para la cuerda final y la pila. Ninguno.

**Qué evitar (el Ugly)* *
- **Bitwise hacks** (como la solución del editorial LeetCode) que funcionan pero son crípticos.
- ** simulación alternativa** que escanea repetidamente el array para encontrar pares – O(n2) e innecesario.
- **Lógica básica codificada por miedo** que no generaliza para no poder de dos entradas (aunque el problema garantiza 2^k).

-...

## 6down⃣ Interview Tips

1. **Explicar el árbol recursivo** antes de la codificación. Mostrar que cada nodo representa un partido, y los niños son los dos sub-matches que se alimentan en él.
2. ** Caso básico de mención**: equipo único.
3. **Hablar sobre la complejidad**: O(n) tiempo, O(log n) profundidad de recursión.
4. **Mostrar versión iterativa** si se pregunta (utiliza una cola o apilar para simular rondas).
5. ** Casos de borde hundido**: `n = 2` → `(1,2)`; `n = 4096` se ajusta a la pila de recursión.

-...

Conclusión

El problema LeetCode 544 es un ejemplo de libro de texto de una construcción binaria perfectamente equilibrada.
Un simple algoritmo recursivo que anexa a un constructor de cadenas / lista / secuencia da una solución limpia, legible y altamente eficiente.

■ *Key Takeaway*
■ *Siempre piensa en el soporte como un árbol binario; la regla “fuerte-vs‐weakest” simplemente significa que dividir el rango en la mitad de cada ronda. *

-...

## 8VIEW⃣ SEO Tags > Palabras clave

- LeetCode 544
- Partidos del concurso de salida
- Solución Java LeetCode
- Solución pitón LeetCode
- Solución C++ LeetCode
- Problemas de codificación de entrevistas
- Repetición del árbol binario
- Complejidad de tiempo O(n)
- Prepa de entrevista de Algorithm
- Entrevista de ingeniería de software

-...

#### 🔧 Quick Test

``python
# Python
print(Solution().findContestMatch(4)) # ((1,4),(2,3))
print(Solution().findContestMatch(8)) # ((1,8),(4,5)),(2,7),(3,6)))
`` `

Ejecutar lo mismo para Java y C++ – las salidas coinciden con los resultados esperados.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀