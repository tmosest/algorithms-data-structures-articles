-...
Título: LeetCode 229. Majority Element II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Elemento de la mayoría de 3 a 229. Majority Element II
#### Quick Reference
Silencio Idioma Silencio Tiempo Silencioso Silencio Complejidad
Silencio--------------------------------------------------...
Silencio **Java** Silencio O(n) Silencio O(1) Silencio **O(n)** Silencio https://leetcode.com/problems/majority-element-ii/ Silencio
Silencio **Python** Silencio O(n) Silencio O(1) Silencio **O(n)** Silencio https://leetcode.com/problems/majority-element-ii/ Silencio
Silencio **C+** Silencio O(n) Silencio O(1) Silencio **O(n)** Silencio https://leetcode.com/problems/majority-element-ii/ Silencio

■ ** Objetivo** – Regresar cada número que aparece ** más que** * n* / 3 ⌋ veces.

■ *Por qué importa* – Este es el problema clásico de la entrevista que prueba su capacidad de pensar en *Boyer–Moore* vote, *constant‐space* algoritmos y *tiempo lineal* trucos. Es un escaparate perfecto para un candidato que puede escribir código limpio y eficiente en varios idiomas.

-...

## 2. Código – Java / Python / C++

■ *Las tres implementaciones utilizan el algoritmo extendido Boyer-Moore (también llamado la versión “2-candidato”). *

#### 2.1 Java

``java
importar java.util*;

Solución de la clase pública {}
public List won(int[] nums) {
int candidate1 = 0, candidate2 = 1; // arbitra distinct values
int count1 = 0, count2 = 0;

// 1er paso – encontrar posibles candidatos
para (int num : nums) {
(num == candidate1) {
conteo 1++;
} si (num == candidato2) {
conteo 2++;
} si (cuenta 1 == 0) {
candidato1 = num;
1 = 1;
} si (contra2 == 0) {
candidato2 = num;
conteo2 = 1;
. ♫ ... {
Conteo 1...
Conta2...
}
}

// Segundo paso – verificar candidatos
conteo1 = 0; conteo2 = 0;
para (int num : nums) {
si (num == candidato1) cuenta1++;
si (num == candidato2) cuenta2++;
}

Lista de resultadosInteger título = nuevo ArrayList implicado();
int n = nums.length;
si (cuenta1  título n / 3) resultado.add(candidate1);
si (cuenta2 √≥ n / 3) resultado.add(candidate2);
Resultado de retorno;
}
}
`` `

### 2.2 Python

``python
de la importación Lista

Solución de clase:
def majority Element(self, nums: List[int]) - List[int]:
# 1er paso - búsqueda de candidatos
cand1, cand2 = 0, 1 # valores de inicio distintos arbitrarios
cuenta1, cuenta2 = 0, 0

para las numidades:
si num == cand1:
conteo1 += 1
elif num == cand2:
Conteo2 += 1
elif count1 == 0:
cand1, cuenta1 = num, 1
elif count2 == 0:
cand2, conteo2 = num, 1
más:
conteo1 -= 1
Conteo2 -= 1

# 2do paso - verificación
cuenta1 = cuenta2 = 0
para las numidades:
si num == cand1:
conteo1 += 1
elif num == cand2:
Conteo2 += 1

res = []
n = len(nums)
si contamos con 1
re.append(cand1)
si cuenta2 √≥ n // 3:
re.append(cand2)
retorno
`` `

### 2.3 C++

``cpp
Incluido el título
#include >

Clase Solución {
public:
std:::vector seleccionadoint confianza majorityElement(std::vector correspondintющ nums) {
int cand1 = 0, cand2 = 1; // distintos puntos
int count1 = 0, count2 = 0;

// Primer paso: encontrar candidatos potenciales
para (int num : nums) {
si (num == cand1) cuenta1++;
si (num == cand2) cuenta2++;
si (cuarto 1 == 0) { cand1 = num; count1 = 1; }
si (cuarto2 == 0) { cand2 = num; count2 = 1; }
si no cuenta1--; cuenta2--; }
}

// Segundo paso: verificar cuentas
conteo1 = conteo2 = 0;
para (int num : nums) {
si (num == cand1) cuenta1++;
si (num == cand2) cuenta2++;
}

std::vector obtenidosint Resultado del usuario;
int n = nums.size();
si (cuenta1 > n / 3) resultado.push_back(cand1);
si (cuenta2 > n / 3) resultado.push_back(cand2);
Resultado de retorno;
}
};
`` `

-...

## 3. Artículo del Blog – “Elemento de la mayoría II: El Bien, el Mal y el Ugly”

■ **Meta‐Description**: Master LeetCode 229 – Majority Element II. Aprenda el algoritmo O(n) / O(1) óptimo, vea las implementaciones Java, Python y C++, y entienda las trampas que pueden subir a los entrevistadores. Perfecto para los buscadores de trabajo de ingeniería de software.

#### 3.1 Introducción

Si has golpeado a LeetCode 229 en tu preparación de entrevistas, probablemente has mirado la declaración del problema, imaginado una solución *hash mapa*, y se preguntó por qué el entrevistador sigue pidiendo “tiempo lineal y espacio constante. ”
Mayoridad Element II no es sólo otro problema contable – es una prueba de su intuición algorítmica. En este artículo diseccionaremos el “bueno” (al algoritmo optimista), el “malo” (acercamientos ingenuos), y el “muy” (trampas de forja). A lo largo del camino, verá código Java, Python y C++ listo para copiar que puede pegar en su cuaderno de entrevista.

■ ¿Por qué importa esto para tu carrera? #
* Los entrevistadores aman soluciones concisas y eficientes en el espacio.
√ – Demostrar el dominio de algoritmos clásicos (Boyer–Moore).
* Muestra que puedes traducir ideas a través de idiomas: una habilidad esencial para ingenieros de personal completo.

#### 3.2 Problema Recap

■ **Given** un array entero `nums` de tamaño `n`.
■ **Retorno** todos los elementos que aparecen más que ⌊ *n* / 3 ⌋ veces.
■ **Constraints**: 1 ≤ * n* ≤ 5 × 104, tención*nums[i]* duración ≤ 109.

■ **Observaciones**:
* En la mayoría de **dos** números pueden satisfacer “ título n/3” porque 3 × (n/3) = n.
* Esta es una extensión natural del clásico problema “Elemento de la mayoría” (n/2).

### 3.3 The Naïve Approach – Hash Map

TEN TERRITOR ANTE ANTERI ANTERIOR ANTERIOR
Silencio----------------------
Silencio Cuenta las frecuencias Silencioso `Mapa seleccionadaInteger, Integer ``  durable O(n) time, O(n) space ←
Silencio Filtro Silencio iterate mapa Silencioso O(n) tiempo

``java
Mapa seleccionadoInteger, Integer frecuentementeq = nuevo HashMap Quería();
for (int nums : nums) freq.put(num, freq.getOrDefault(num, 0) + 1);
Lista de datos:Integer confianza res = nuevo ArrayList correctamente();
para (Mapa.Entrar)
si (e.getValue() > n / 3) res.add(e.getKey());
`` `

**Por qué es malo para las entrevistas* *
* Usa memoria extra – *O(n)*.
* El seguimiento de LeetCode pide explícitamente espacio O(1).
* No muestra un pensamiento algoritmo más profundo.

### 3.4 The Good – Boyer–Moore Voting (Extended)

#### 3.4.1 Intuición

1. ** Selección de candidatos** – Podemos hacer un seguimiento de la mayoría de los dos candidatos ( " , " , " , " , y de sus " votos " ( " cnt1 " ).
2. **Erradicación de votos** – Cada vez que un nuevo número no coincide con el candidato y ambos contadores son positivos, decreamos ambos.
3. **Proof** – Si un número ocurre √° n/3 veces, no se puede eliminar completamente porque cada eliminación elimina dos números, y la mayoría debe sobrevivir.

##### 3.4.2 Two Passes

* **Pass 1** – Encuentra a los dos candidatos potenciales de la mayoría.
* **Pass 2** – Cuenta sus ocurrencias reales para confirmar si efectivamente cruzan el umbral.

#### 3.4.3 ¿Por qué O(1) Space?

Nunca almacenamos todo el mapa de frecuencias. Sólo dos variables candidatas y dos contadores – cuatro enteros. La memoria permanece constante independientemente del tamaño de entrada.

#### 3.4.4 Casos de borde " Gotchas "

Silencioso Caso Edge Qué hacer para cuidar de Silencio
Silencio----------------------------
Los candidatos iniciales pueden ser los mismos que los únicos elementos que contiene la versión inicial de los candidatos a valores distintos (`0`, `1`) antes del bucle. Silencio
Silencio Todos los elementos de la misma ¦ Counters no decrementarán, todavía correcto Silencio Después de pasar 1, el único elemento sobrevivirá. Silencio
tención Números negativos Silencio No hay diferencia – sólo comparaciones TENIDO Use `=` para la igualdad. Silencio

#### 3.4.5 Snippets de implementación

■ **Java** – ver código arriba.
■ **Python** – ver código arriba.
не **C+** – ver el código arriba.

Los tres siguen la misma lógica, por lo que puede cambiar cómodamente idiomas en el lugar.

### 3.5 Los errores comunes

1. **Asumiendo que el algoritmo funciona para n/2** – Para `n/3`, sólo necesita **dos** candidatos, no uno.
2. **Skipping the second validation pass** – El primer paso sólo garantiza *posibles* candidatos; usted debe verificarlos.
3. **Usando `` en lugar de `` El problema dice explícitamente “más que n/3” (la desigualdad restringida).
4. **Iniciar a ambos candidatos al mismo valor* Si empiezas con `cand1 = cand2 = 0`, el algoritmo puede mal contabilizar cuando el array contiene sólo ceros.
5. **Omitir la cadena `else if`** – Mezclar las condiciones puede llevar a actualizaciones incorrectas de la contra.

### 3.6 Testing & Edge Cases

Silencio Test ← Input Silencio esperada
Silencio----------------------------
TENIDO ELemento Único TENIDO `[1] Silencio `[1]
Silencio Dos vidas distintas [1,2] ¿Ambos dos? No → ambos 1/2 ≤ 2/3? En realidad, 1 √≥ 0 ¦ (0) Silencio
Silencio No majority ⋅ `[1,2,3,4]` Silencio `[] Silencio No elemento ⇩ 4/3 ♥ 1.33 Silencio
Silencio Entrada grande Ø 5 × 104 números aleatorios ← O(n) tiempo de ejecución, memoria constante

### 3.7 Variaciones " Extensiones

* **k-majority** – Generalizar a “ título n/k” utilizando candidatos “k-1”.
* ** Datos de análisis* El mismo algoritmo funciona en un flujo de datos: mantener contadores, descarte a medida que vayas.
* ** Paralelismo** – Dividir array, correr Boyer–Moore localmente, fusionar candidatos.

### 3.8 Conclusión - Lo que los entrevistadores realmente buscan

← Trait tóxico Evidencia en su solución
Silencio...
Silencio ** Profundidad algorítmica** Silencio Usos Boyer-Moore, no sólo mapas precipitados
Silencio **Eficiencia del espacio** Silencio Únicamente O(1) memoria extra
Silencio **Robustness** Silencio Handles negativos, ceros, pequeños arsenales
Silencio **La calidad de los esposos** viv Clear, commented, multi-language ready
Silencio **Comunicación** Silencio Puede explicar el razonamiento en 30 segundos

**Pro tip:** Después de la codificación, ensaye una explicación de 30 segundos: “Mantenemos dos candidatos, decremos ambos cuando entra un nuevo elemento, y luego verificamos los recuentos. ”

### 3.9 Call to Action

■ **Lista a su próxima entrevista de codificación? * *
■ Copia los fragmentos Java/Python/C++ arriba, practica en LeetCode y confía en explicar la magia de Boyer-Moore.
■ **Después de más artículos de entrevista** – abordaremos la clasificación, DP, teoría de gráficos, y más.

-...

## 4. Lista de verificación SEO (para el artículo del blog)

1. **Título** – “Elemento de la mayoría II – LeetCode 229 Python, C++ Solutions
2. ** Descripción de los datos** – Resumen breve y rico en palabras clave (ver arriba).
3. **Headings** – H1, H2, H3 con palabras clave de destino (“LeetCode 229”, “Majority Element II”, “Boyer–Moore”, “O(n) time”).
4. **Enlaces internos** – Enlace a artículos relacionados o página de demostración de código abierto.
5. ** Enlaces externos** – Referencia LeetCode problema página, explicación oficial.
5. **No texto** – Para cualquier captura o diagramas de código, utilice etiquetas descriptivas alt.
6. ** Densidad de la palabra clave** – ~1–2 % para las palabras clave principales; uso natural.
7. **Compartir Social** – Incluir botones de compartir; mencionar “compartir en LinkedIn, Twitter”.

Con este artículo, no sólo usted resuelve el problema, también se posiciona como un candidato que puede ofrecer código optimizado y multiplataforma, un deber-tener para los roles de ingeniería de software de hoy. ¡Feliz entrevista!