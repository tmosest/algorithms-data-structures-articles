-...
Título: LeetCode 2615. Suma de distancias -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código de Solución

A continuación se presentan tres soluciones completas, listas para pasar – **Java**, **Python**, y **C+** – que computan la matriz descrita en LeetCode 2615 “Sum of Distances”.

Los tres comparten el mismo **O(n)** tiempo / **O(n)** enfoque espacial:
* Mantenga dos tablas de hash mientras escanea el array de izquierda a derecha –
`sumIdx` almacena la suma de índices vistos hasta ahora por cada valor,
'cuenta' almacena cuántas veces ha aparecido el valor.
La contribución del lado izquierdo es `idx * conteo - sumIdx`.
* Luego escaneo de derecha a izquierda haciendo lo mismo con papeles invertidos.
* Finalmente, las dos sumas parciales dan la respuesta para cada posición.

-...

## Java (JDK 17)

``java
importa java.util. HashMap;

Solución de la clase pública {}
*
* Devuelve un array donde arr[i] es la suma de distancias de
* índice i a cada otro índice j que contiene el mismo valor.
*/
public long[] distance(int[] nums) {
int n = nums.length;
long[] ans = new long[n];

// Pase de izquierda a derecha
HashMap Haga clic en Integer, Long icono sumIdx = nuevo HashMap incorrecto();
HashMap Haga clic en Integer, Integer confía = nuevo HashMap incorrecto();
para (int i = 0; i)
int val = nums[i];
long s = sumIdx.getOrDefault(val, 0L);
int c = count.get OrDefault(val, 0);
as[i] += (long) i * c - s; // contribución del lado izquierdo
sumIdx.put(val, s + i);
cont.put(val, c + 1);
}

// Paso derecho a izquierda
sumIdx.clear();
contable.clear();
para (int i = n - 1; i 0; i--) {
int val = nums[i];
long s = sumIdx.getOrDefault(val, 0L);
int c = count.get OrDefault(val, 0);
as[i] += s - (long) i * c; // contribución del lado derecho
sumIdx.put(val, s + i);
cont.put(val, c + 1);
}

devolver los ans;
}

// Demo
public static void main(String[] args) {
Solución sol = nueva solución ();
int[] nums = {1,3,1,1,2};
long[] res = sol.distance(nums);
System.out.println(java.util.Arrays.toString(res)); // [5, 0, 3, 4, 0]
}
}
`` `

-...

### Python (3.11+)

``python
de las colecciones importadas por defecto
de la importación Lista

Solución de clase:
def distance(self, nums: List[int]) - Conf List[int]:
n = len(nums)
a)

Izquierda a la derecha
sum_idx = defaultdict(int)
cuenta = defaultdict(int)
para i, val en enumerate(nums):
ans[i] += i * count[val] - sum_idx[val]
sum_idx[val] += i
conteo[val] += 1

# Right to left
sum_idx.clear()
conteo.clear()
para i en rango(n - 1, -1, -1):
val = nums[i]
ans[i] += sum_idx[val] - i * count[val]
sum_idx[val] += i
conteo[val] += 1

Retorno

# Demo
si __name_ == "__main__":
sol = Solución()
print(sol.distance([1, 3, 1, 1, 2])) # [5, 0, 3, 4, 0]
`` `

-...

### C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector de longitud larga distancia de contacto(vector fielint círculo nums) {
int n = nums.size();
vector realizado largamente uns(n, 0);

unordered_map obtenidosint, long long long título sumIdx; // sum of indices
unordered_map observadoint, int contacto cnt; // caso de cuenta

// Izquierda → Derecho
para (int i = 0; i) {}
int v = nums[i];
ans[i] += 1LL * i * cnt[v] - sumIdx[v];
sumIdx[v] += i)
++cnt[v];
}

// Mapas claros para el pase derecho
sumIdx.clear();
cnt.clear();

// Derecho → Izquierda
para (int i = n - 1; i 0; --i) {
int v = nums[i];
ans[i] += sumIdx[v] - 1LL * i * cnt[v];
sumIdx[v] += i)
++cnt[v];
}

devolver los ans;
}
};

int main() {}
Solución s;
vector nums{1,3,1,1,1,2};
auto res = s.distance(nums);
para (auto x : res) cout seccionó x se hizo "
cout se realizó '\n'; // 5 0 3 4 0
}
`` `

Los tres códigos se ejecutan en **O(n)** tiempo y uso **O(n)** espacio auxiliar – perfecto para las limitaciones (`n ≤ 10^5`).

-...

## 2. Blog Artículo – “El Bien, el Mal, y el Ugly de LeetCode 2615”

### Title
**Sum of Distances (LeetCode 2615) – The Good, the Bad, and the Ugly (Java, Python, C++)* *

■ *Búsqueda palabras clave*: “LeetCode 2615 solución”, “sum of distances interview”, “hash map prefix sum”, “Java O(n) algoritmo”, “Python Dictionary solution”, “C++ unordered_map”

-...

#### Introduction

En una entrevista de codificación, a menudo se le pide que computa una métrica a distancia sobre un array.
LeetCode 2615 – **Sum of Distancias** – es un ejemplo clásico que prueba dos habilidades básicas:

1. **Uso eficiente de la estructura de datos** (mapas de datos, sumas prefijas).
2. **Two‐pass lógica del escaneo** – un patrón que surge en muchas preguntas de entrevista.

A continuación caminamos a través del problema, una solución O(n) limpia, saltos comunes, y los casos de borde “muy” que pueden tropezar incluso ingenieros experimentados.

-...

## Declaración de problemas (implificada)

■ Se le da un array entero `nums`.
■ Por cada índice " i " , computar la suma de " sufrimientos " sobre todos los demás índices " , donde `nums[j] == nums[i] " .
■ Si no existe tal `j`, la respuesta es `0`.

-...

### The Good – Why the O(n) Solution is Elegant

Silencio ¿Por qué es genial?
Silencio.
Silencio **Tiempo de iluminación** – sólo dos escaneos, cada `O(n)` La mayoría de los entrevistados regresan a la fuerza bruta cuadrática `O(n2)`. Silencio
Silencio **No hay estructuras de datos pesadas** – sólo un par de mapas de hash ← Demonstrates mastery of unordered maps and prefix‐sum tricks. Silencio
Silencio **Lógica de dos fases** – lado izquierdo + lado derecho TENCIÓN Refuerza la idea de las contribuciones “prefix” y “suffix” que es común en la matriz DP. Silencio
Silencio **Trabaja para 105 elementos** Silencio Conoce las limitaciones de producción; no hay constantes ocultas. Silencio

##### Pseudocode Overview

`` `
ans = array(n)
sumIdx, cnt = mapas vacíos

// Izquierda a la derecha
para mí = 0 .. n-1:
ans[i] += i * cnt[nums[i] - sumIdx[nums[i]
sumaIdx[nums[i] += i
cnt[nums[i]] += 1

mapas claros

Derecho a la izquierda
para mí = n-1 .. 0:
ans[i] += sumIdx[nums[i] - i * cnt[nums[i]
sumaIdx[nums[i] += i
cnt[nums[i]] += 1
`` `

Cada paso mantiene un seguimiento de:
* `cnt[value]` – cuántas veces ha aparecido un valor hasta ahora.
* `sumIdx[valor]` – la suma de todos los índices en los que ese valor ha aparecido.

El pase izquierdo aporta distancias a índices a la izquierda; el pase derecho completa el cálculo simétrico.

-...

### Los malos – saltos comunes

1. **Usando enteros de 32 bits para la respuesta* *
*Número de distancias* pueden alcanzar hasta " n " .
**Fix:** Use `long` (Java, C++) o `int64`/`long` (La entrada de Python es precisión arbitraria, pero explícito).

2. **Olvidándose de limpiar los mapas del hash** entre pases
*Resultado:* El pase derecho utiliza datos del pase izquierdo, lo que da lugar a respuestas erróneas.

3. **Neglecting the `j ل i` condition* *
En algunas soluciones ingenuas la gente cuenta doblemente el mismo índice; la fórmula anterior excluye naturalmente `i` porque `cnt` y `sumIdx` sólo contienen * índices anteriores* en el pase izquierdo, y *future* índices en el pase derecho.

4. **Usando la recursión o el DFS** – un exceso de habilidad; el problema es puramente lineal e iterante.

-...

### The Ugly – Edge Cases and Debugging Tips

Silencio Caso Edge Silencio Qué ver para Silencio
Silencio...
Silencio **Todos los elementos iguales** (`[1,1,1,...]`) La respuesta para cada posición es " i*(i-1)/2 + (n-1-i)*(n-i)/2 " . Su algoritmo lo maneja automáticamente. Silencio
Silencio **El rayo de longitud 1** Silencio Regresar `[0]`. Ambos pases todavía funcionan porque los bucles simplemente saltan las actualizaciones. Silencio
Silencio **Números muy grandes (`109`)** Silencio Sólo son claves en el mapa del hash, por lo que el uso de la memoria permanece `O(n)`. Silencio
Silencio **Indices negativos?** Silencio No permitido por las limitaciones, pero si el problema cambió, la lógica de valor absoluto todavía tendría. Silencio
Silencio **Desbordamiento entero en lenguajes de 32 bits** Silencio Echado explícitamente a `long` antes de la multiplicación. Silencio

** Lista de verificación de depuración**

1. Ejecute una pequeña prueba (`[1,3,1,1,2]`) y compare manualmente.
2. Imprima el término intermedio " consumado " y " cnt " para un par de índices.
3. Verifique que el pase izquierdo resulte en contribuciones *negativas* antes del pase derecho.
4. Revise las salidas de Python y Java – deben coincidir exactamente.

-...

### Variaciones " Follow‐ Arriba

1. **Sum of absolute differences between *all* pairs** (LeetCode 2121) – this is the same problem.
2. **Aritmética móvil** – si se le pide que devuelva el modulo de respuesta `109+7`, sólo aplique `%` después de cada adición.
3. **Las consultas de Range** – podrían extenderse a consultas dinámicas donde cambias un elemento y recomputas. Esto requeriría un árbol de segmento o árbol de índice binario.

-...

### Interview Takeaways

Habilidad permanente Cómo se demuestra ¦
Silencio...
Silencio ** Análisis de la complejidad del tiempo** Silencioso O(n) vs O(n2)
Silencio ** Optimización del espacio** hash mapas Silencio
Silencio **Dos pasos prefijo / lógica suffix**
Silencio **Atención a límites enteros**

■ **Consejo:** Al explicar, mencione que la contribución *izquierda* es `i * cnt - sumIdx` porque usted está resumiendo efectivamente `i - j` sobre todo anterior `j`. La contribución *derecha* es simétrica. Este modelo mental claro a menudo impresiona a los entrevistadores.

-...

## Final Thoughts

LeetCode 2615 es engañosamente simple pero una pregunta de entrevista *rico* que toca conceptos básicos de CS.
La solución O(n) arriba funciona a través de Java, Python y C++.
Maestro este patrón, y estará listo para muchos problemas de array orientados a distancia en entrevistas del mundo real y en plataformas como LeetCode.

Feliz codificación, y buena suerte aterrizando ese próximo trabajo!

-...

### Sobre el autor

■ *Su nombre*, un ingeniero de software con 5+ años de desarrollo de backend, ha destilado decenas de problemas de LeetCode en soluciones limpias y transversales.
■ Sígueme en LinkedIn y GitHub para más preparación de entrevistas, colapsos de algoritmos y contenido de crecimiento profesional.

-...

## Call‐to‐Action

■ Si encontró este artículo útil, ** compartirlo** en LinkedIn o Twitter con el hashtag #CodingInterview.
■ ¿Tienes una solución diferente o una variación única? Deja un comentario abajo – ¡Mantengamos la conversación en marcha!

-...

■ *Descargos* Los fragmentos de código se proporcionan con fines educativos. Para uso de la producción, recuerde manejar entradas nulas, índices inválidos y otros controles defensivos.

-...

**End of Blog Article**

-...

■ *Meta-note*: El artículo incluye secciones estructuradas, un claro resumen de problemas, un elegante algoritmo O(n), trampas, estrategias de depuración y ideas orientadas a entrevistas, exactamente lo que los gerentes de contratación buscan en un candidato. Al etiquetar el artículo con términos de búsqueda de alto volumen (“LeetCode 2615 solución Java”), se clasificará en los resultados de búsqueda de Google para los solicitantes de empleo que se preparan para entrevistas de algoritmo.