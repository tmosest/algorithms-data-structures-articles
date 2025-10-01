-...
Título: LeetCode 689. Suma Máximo de 3 Subarrays No Sobresalientes -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1down El “Suma Máximo de 3 Subarrayos No Sobresalientes” – LeetCode 689
*(Hard – 73 % de las presentaciones lo golpearon – una pregunta de entrevista perfecta para un rol de ingeniería de software)*

Silencio Idioma Silencio Código Silencio
Silencio...
Silencio **Java** Silencioso Mostrar resultados/summary título ... Identificado/detalles
tención **Python** ANTERIEDO DEtalles Mostrar = ...
tención **C+** Silencioso Mostrar resultados/summary título ... Identificado/detalles

■ *¿Quieres conseguir tu próximo trabajo? Escribe la solución, explica el truco y compártelo en LinkedIn o en tu cartera. Eso es exactamente lo que se trata de este post – una inmersión profunda, una solución lista para copiar, y un artículo de blog pulido que es fácil de SEO y de entrevista. *

-...

Problema Recap

■ **Input**
" Números " : " – 1 ≤ nums.length ≤ 2 × 104
" k " : longitud de cada subarray (1 ≤ k ≤ suelo(nums.length/3))
■ **La salida*
"int[3]" – los índices de inicio de los tres *no superposición* subarros de longitud `k` que dan la suma total máxima.
■ Si varios triples dan la misma suma, devuelve la **léxicográficamente más pequeña**.

■ *Ejemplo*
■ `nums = [1,2,1,2,6,7,5,1], k = 2 → [0,3,5]`

■ Explicación: sub-arrays `[1,2]`, `[2,6]`, `[7,5]` sum to 18, the maximum possible.

-...

## 3down Estrategia de alto nivel (el “bien”)

1. ** Ventana deslizante** – computar la suma de cada sub-array de longitud `k`.
*`subSum[i]` = sum of `nums[i] .. i+k-1]`*
O(n) time, O(n) space.

2. **Pre-compute best left/right indices**
* `bestLeft[i]` – index of the *maximum* sub‐sum in the prefix `[0 .. i]`.
* `bestRight[i]` – índice del sub-sum *maximum* en el sufijo `[i .. n-k]`.
Para los lazos mantenemos el índice *earliest* (lexicográficamente más pequeño).

3. **Prueba cada sub-array medio posible*
Para el comienzo medio `m` (debe satisfacer `k ≤ m ≤ n-2k`):
`` `
izquierda = bestLeft[m - k]
derecho = mejor Derecho[m + k]
total = subSum[left] + subSum[m] + subSum[right]
`` `
Mantenga el triple con el más grande "total".
Si los lazos totales, el orden léxicográfico se maneja automáticamente mediante la construcción de `bestLeft/right`.

Todo el algoritmo es **O(n) tiempo, O(n) espacio** – lo mejor posible para este problema.

-...

## 4 pesquisas detalladas (el "Bad" " Ugly " )

¿Por qué es malo arreglar la vida
Silencio------------------------
Silencio **Naïve O(n3)** Silencio Enumerar todos los triples → demasiado lento (n hasta 20 000). Silencio Utilice la ventana deslizante + los mejores índices pre-computados. Silencio
Silencio **Double counting overlaps** Silencio Middle `m` debe dejar `k` ranuras en cada lado. Iterate `m` from `k` to `n-2k`. Silencio
Silencio **Tetas rotas incorrectamente** Silencio Escoger el índice máximo * más alto* produciría una respuesta más grande léxicográficamente. En `bestLeft`, cuando suma la corbata, mantenga el índice *smaller*; de forma similar en `mejor derecho`. Silencio
Silencio ** Errores por uno** Silenciosos `subSum` longitud es `n-k+1`. TENIENDO arrays de índice cuidadosamente: `subSum[i]` corresponde a iniciar `i`. Silencio
tención ** Casos de emergencia** Silencioso `nums.length == 3k` – sólo un triple posible. ← Los bucles manejan esto naturalmente; sólo asegúrate de que los índices estén dentro de límites. Silencio
Silencio **Large numbers** Silencio Sum of up to 2 × 104 elements, each י 216 → fits in 32‐bit signed int. peru Use `int` in Java/C++, `int` in Python (precisión arbitraria). Silencio
Silencio **Desperdicio de memoria** Silencio Mantener todo `subSum` es necesario para las búsquedas O(1). Silencio Aceptar espacio O(n); las limitaciones lo permiten. Silencio

-...

## 5VIEW⃣ Code Implementations

■ **Nota**: Las tres soluciones utilizan la idea algoritmo *same* – sólo los cambios de sintaxis.

## 5.1 Java (estilo LeetCode)

``java
// 689. Suma máxima de 3 Subarrayos no relacionados con el uso
Clase Solución {
int[] maxSumOfThreeSubarrays(int[] nums, int k) {
int n = nums.length;
si (n iere 3 * k) devuelve nuevo int[0];

// 1. Cuantía de todas las sub-arrayas de longitud k
int numSub = n - k + 1;
int[] subSum = nuevo int[numSub];
int sum = 0;
para (int i = 0; i < k; i++) sum += nums[i];
subSum[0] = sum;
para (int i = k; i) {}
suma += nums[i] - nums[i - k];
subSum[i - k + 1] = sum;
}

// 2. bestLeft[i] – índice con suma máxima en [0.i]
int[] bestLeft = new int[numSub];
bestLeft[0] = 0;
para (int i = 1; i)
si (subSum[i] Izquierda [i - 1]) {}
bestLeft[i] = i;
. ♫ ... {
bestLeft[i] = bestLeft[i - 1];
}
}

// 3. bestRight[i] – índice con suma máxima en [i.end]
int[] bestRight = new int[numSub];
lo mejor Derecho[num] Sub - 1] = num Sub - 1;
para (int i = numSub - 2; i >= 0; i--) {
si (subSum[i] >= subSum[bestRight[i + 1]) {}
bestRight[i] = i;
. ♫ ... {
bestRight[i] = bestRight[i + 1];
}
}

// 4. Pruebe cada sub-array medio
int[] best = new int[3];
t bestTotal = -1;
para (int m = k; m <= numSub - k - 1; m+) {
int left = bestLeft[m - k];
int right = best Derecho[m + k];
int total = subSum[left] + subSum[m] + subSum[right];
si (total √≥ bestTotal) {
bestTotal = total;
mejor[0] = izquierda;
mejor[1] = m;
best[2] = right;
}
}
devolver mejor;
}
}
`` `

### 5.2 Python 3

``python
# 689. Suma máxima de 3 subarrayos no superpuestos
Solución de clase:
def maxSumOfThreeSubarrays(self, nums: list[int], k: int) - ratio[int]:
n = len(nums)
si no se hizo 3 * k:
retorno []

# 1. Subarray sums
num_sub = n - k + 1
sub_sum = [0] * num_sub
curr = sum(nums[:k])
sub_sum[0] = curr
para i en rango(k, n):
curr += nums[i] - nums[i - k]
sub_sum [i - k + 1] = curr

# 2. best left
best_left = [0]
para i en rango(1, num_sub):
si sub_sum[i] - 1]]:
best_left[i] = i
más:
best_left[i] = best_left[i - 1]

# 3. best right
best_right = [0] * num_sub
best_right[-1] = num_sub - 1
para i en rango(num_sub - 2, -1, -1):
si sub_sum[i] >= sub_sum[best_right[i] + 1]]:
best_right[i] = i
más:
best_right[i] = best_right[i + 1]

3. bucle de candidato medio
mejor = [0, 0, 0]
best_total = -1
para m en rango(k, num_sub - k):
l = best_left[m - k]
r = best_right[m + k]
total = sub_sum[l] + sub_sum[m] + sub_sum[r]
si total > best_total:
best_total = total
mejor = [l, m, r]

mejor
`` `

### 5.3 C++ (17)

``cpp
// 689. Suma máxima de 3 Subarrayos no relacionados con el uso
Clase Solución {
public:
vector = máxSumOfThreeSubarrays(vector fieltro implicado nums, int k) {
int n = nums.size();
si (n  made 3 * k) regresan {};

// 1. Subarray sums
int numSub = n - k + 1;
vector empleado subSum(numSub);
int sum = 0;
para (int i = 0; i < k; ++i) sum += nums[i];
subSum[0] = sum;
para (int i = k; i) {}
suma += nums[i] - nums[i - k];
subSum[i - k + 1] = sum;
}

// 2. mejor izquierda
vector asignadoint confianza bestLeft(numSub);
bestLeft[0] = 0;
para (int i = 1; i)
bestLeft[i] = subSum[i] Izquierda[i - 1]] ? i : bestLeft[i - 1];

// 3. mejor derecho
vector significado mejorRight(numSub);
lo mejor Derecho[num] Sub - 1] = num Sub - 1;
para (int i = numSub - 2; i >= 0; --i)
bestRight[i] = subSum[i] >= subSum[bestRight[i + 1]] ? i : bestRight[i + 1];

// 4. bucle medio
vector implicado a(3);
t bestTotal = -1;
para (int m = k; m) = numSub - k - 1; ++m) {
int l = bestLeft[m - k];
int r = bestRight[m + k];
int total = subSum[l] + subSum[m] + subSum[r];
si (total √≥ bestTotal) {
bestTotal = total;
as = {l, m, r};
}
}
devolver los ans;
}
};
`` `

-...

## 6 comentarios⃣ Escribir un blog ganador - SEO > Entrevista lista

A continuación se muestra un artículo listo para publicar que utiliza ** títulos ricos, secciones de keyword‐denses, capturas de pantalla de código y consejos prácticos de entrevista**. Copiarlo en Medium, Dev.to, o tu propio blog de tecnología. Etiqueta con *LeetCode 689*, *entrevista de trabajo*, *ingeniería de software*, *reto de codificación* y vea crecer el tráfico.

■ **Pro-Tip**: Añadir un **“Pruébalo usted mismo”** snippet interactivo (por ejemplo, incrustado en GitHub Gist o CodePen) para que los reclutadores puedan ejecutar la solución al instante.

-...

### 6.1 Blog Esquema

Silencioso en la sección
Silencio...
Silencio **Headline** Silencio Grabar la atención " incluye el número de problema LeetCode. Silencio
Silencio **Problema Recap** Silencio Refrigerio rápido para los lectores que esquien. Silencio
Silencio **Key Take-aways** Silencio List the *why* this problem matters in interviews. Silencio
tención ** Algorithm Walk‐through** ← Paso a paso (incluye un diagrama de flujo). Silencio
Silencio **Code** Silencio Destaca la lógica central en un lenguaje de elección. Silencio
Silencio ** Análisis de la complejidad** Silencio Mostrar por qué O(n) supera todos los demás enfoques. Silencio
Silencio **Common Pitfalls** Silencio Show what interviewers love to hear you avoid. Silencio
Silencio **Edge‐Case Checklist** Silencio Reassure reclutadores usted entiende restricciones. Silencio
Silencio ** Consejos de desempeño** Silencio Discuss factores constantes, cómo optimizar los 'Arrays.fill' de Java, etc. Silencio
Silencio ** Pensamiento Final** Silencioso Alentar la práctica en LeetCode, compartiendo en LinkedIn, construyendo una cartera. Silencio
Silencio ** Call‐to‐Action** Silencioso “Descargar el código”, “Aplicar ahora”, “Comparte tus propias soluciones”. Silencio

-...

### 6.2 Full Article

■ (Copy‐paste en Medium o tu propio blog – incluso puedes añadir una imagen de héroe de un árbol binario o la animación de la ventana deslizante.)

``markdown
# 🚀 LeetCode 689: "Maximum Sum of 3 Non-Overlapping Subarrays" – Una guía completa
*Problema de entrevista, el 73 % de las soluciones lo superaron, perfecto para su próxima entrevista de ingeniería de software. *

-...

Declaración de problemas

■ ** Objetivo**: Encontrar tres sub-arrayos no superpuestos de igual longitud `k` en un array `nums` que maximice la suma total.
■ **Retorno**: Los tres índices iniciales, lexicográficamente más pequeños sobre los lazos.

■ Constraints:
* 1 ≤ nums.length ≤ 20 000
* 1 ≤ k ≤ piso(nums.length/3)
* Cada elemento

■ **Por qué importa*:
* Requiere una ventana deslizante + programación dinámica en un solo paso.
* Demuestra una comprensión profunda de las ofertas de tiempo/espacio – un conocimiento imprescindible para las entrevistas de codificación en Google, Amazon, Microsoft, Stripe, etc.

-...

## 🔍 High‐Level Insight – The “Good” Approach

1. **Venta flotante*
*Computa cada sub-array suma en tiempo lineal. *
`` `
subSum[i] = sum(nums[i ... i+k-1])
`` `
Complejidad: **O(n)**.

2. ** Índices de Max Prefijo / Sufijo**
* `bestLeft[i]` – el índice del máximo `subSum` en `[0 ... i]` (más cercano a los lazos).
* `bestRight[i]` – el índice del máximo `subSum` en `[i ... final]` (más vale en los lazos – pero escogemos el más mínimo* cuando construimos).

Estos arrays nos permiten saber instantáneamente *el mejor candidato izquierdo* y *el mejor candidato derecho* para cualquier sub-array medio.

3. *Enumerar el submarino medio*
*Middle start `m` must leave `k` slots on each side → `k ≤ m ≤ n-2k`. *
Cumplimiento total para `izquierda = mejorLeft[m-k]`, `derecha = mejor Correcto.
Mantenga el triple con el mayor total; los lazos se resuelven automáticamente porque siempre usamos los primeros índices.

■ Resultado: **O(n)** tiempo, **O(n)** espacio – el óptimo para este problema.

-...

## 📚 Code – Java / Python / C++

■ *No dude en copiar los fragmentos de abajo en su propio IDE o el corredor de pruebas LeetCode. *

``java
// 689. Suma máxima de 3 Subarrayos no relacionados con el uso
Clase Solución {
int[] maxSumOfThreeSubarrays(int[] nums, int k) {
int n = nums.length;
si (n iere 3 * k) devuelve nuevo int[0];

int numSub = n - k + 1;
int[] subSum = nuevo int[numSub];
int sum = 0;
para (int i = 0; i < k; i++) sum += nums[i];
subSum[0] = sum;
para (int i = k; i) {}
suma += nums[i] - nums[i - k];
subSum[i - k + 1] = sum;
}

int[] bestLeft = new int[numSub];
bestLeft[0] = 0;
para (int i = 1; i)
bestLeft[i] = subSum[i] √≥ subSum[bestLeft[i-1]] ? i : bestLeft[i-1];

int[] bestRight = new int[numSub];
bestRight[numSub-1] = numSub-1;
para (int i = numSub-2; i 0; i...)
bestRight[i] = subSum[i] √= subSum[bestRight[i+1]] ? i : bestRight[i+1];

int[] ans = nuevo int[3];
t bestTotal = -1;
para (int m = k; m <= numSub - k - 1; m+) {
int l = bestLeft[m - k];
int r = bestRight[m + k];
int total = subSum[l] + subSum[m] + subSum[r];
si (total √≥ bestTotal) {
bestTotal = total;
as = nuevo int[]{l, m, r};
}
}
devolver los ans;
}
}
`` `

``python
# 689. Suma máxima de 3 subarrayos no superpuestos
Solución de clase:
def maxSumOfThreeSubarrays(self, nums: List[int], k: int) - título List[int]:
n = len(nums)
si no se hizo 3 * k: retorno []

num_sub = n - k + 1
sub_sum = [0] * num_sub
cur = sum(nums[:k])
sub_sum[0] = cur
para i en rango(k, n):
cur += nums[i] - nums[i-k]
sub_sum[i-k+1] = cur

best_left = [0]
para i en rango(1, num_sub):
best_left[i] = i if sub_sum[i] ⇩ sub_sum [best_left[i-1]]

best_right = [0] * num_sub
best_right[-1] = num_sub-1
para i en rango(num_sub-2, -1, -1):
best_right[i] = i if sub_sum[i] œ= sub_sum[best_right[i+1]) else best_right[i+1]

mejor = [0,0,0]
best_total = -1
para m en rango(k, num_sub - k):
l, r = best_left[m-k], best_right[m+k]
total = sub_sum[l] + sub_sum[m] + sub_sum[r]
si total > best_total:
best_total = total
mejor = [l, m, r]
mejor
`` `

``cpp
// 689. Suma máxima de 3 Subarrayos no relacionados con el uso
Clase Solución {
public:
vector = máxSumOfThreeSubarrays(vector fieltro implicado nums, int k) {
int n = nums.size();
si (n ■ 3*k) regresan {};

int numSub = n-k+1;
vector empleado subSum(numSub);
int s=0; for(int i=0;i obtenidosk;i++) s+=nums[i];
subSum[0]=s;
para(int i=k;i observadon;i+){
s+=nums[i]-nums[i-k];
subSum[i-k+1]=s;
}

vector asignadoint confianza bestLeft(numSub);
bestLeft[0]=0;
para(int i=1;i wonnumSub;i+)
bestLeft[i]=subSum[i] confianzasubSum[bestLeft[i-1]]?i:bestLeft[i-1];

vector significado mejorRight(numSub);
bestRight[numSub-1]=numSub-1;
para(int i=numSub-2;i confianza=0;--i)
bestRight[i]=subSum[i]=subSum[bestRight[i+1]]?i:bestRight[i+1];

vector implicado a(3);
mejor Total=-1;
para(int m=k;m observado=numSub-k-1;m+){
int l=bestLeft[m-k], r=best Derecho[m+k];
int total=subSum[l]+subSum[m]+subSum[r];
si (total]
lo mejor Total=total;
as={l,m,r};
}
}
devolver los ans;
}
};
`` `

-...

Desglose de la complejidad

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencioso ventana Silencioso **O(n)** Silencio
← Prefix / Suffix max Silencio **O(n)** Silencio Dos arrays ayudantes **O(n)** Silencio
Silencio en el medio ambiente **O(n)**

Total: **Hora O(n)**, **Pace O(n)**.
Todas las demás soluciones ingenuas (ops anidados dobles o triples) serían **O(n3)**, que es *imposible* para `n = 20 000`.

-...

## ❌ Common Pitfalls > Cómo evitarlos

Silencio Pitfall Silencio ¿Por qué los reclutadores se preocupan
Silencio------------------
Silencio Utilizando dos bucles para prefijo y sufijo pero *recomputing* sub-array sums ¦ Wastes time, O(n2) ← Pre-compute `subSum` once. Silencio
← No manipular correctamente el rompimiento de corbatas.Resultados en respuesta incorrecta en pruebas sutiles TEN Tienda *principal* índice sobre los lazos al construir `bestLeft` y `bestRight`. Silencio
tención Off‐by‐one en rango medio de candidatos (`k ≤ m ≤ n-2k`) ← Fails en casos de bordes pequeños TENIDO Explicitly compute `numSub = n-k+1` y bucle `para m en rango(k, numSub - k)`. Silencio
Silencio Utilizando desbordamiento de entrada de 32 bits (en idiomas como C++) TEN Respuesta incorrecta sobre grandes insumos TENIDO Elements ANTE 216, suma ANTE 216*k*3; 32 bits es seguro, pero utiliza 'long' para la seguridad. Silencio
Silencio Neglecting `n  Ne 3k` check ← Null pointer / array index error tención Cláusula de guardia rápida al principio. Silencio

-...

## 🔧 Edge‐Case Checklist

- `nums` longitud exactamente `3k` → sólo un triple posible.
- `k = 1` → trivial, sólo tiene que elegir tres elementos max sin adjacency.
- `nums` all ceros → debe devolver `[0, 1, 2]` (léxicográficamente más pequeño).
- `k ' equals `floor(n/3)` → sólo una o dos posibles colocaciones.

Prueba estos antes de publicar.

-...

♪ ♪ ♪ ♪♪

Silencio Idioma Silencio
Silencio...
Silencio **Java** Silencio Uso `Arrays.fill` para inicializar arrays si necesita grandes predeterminados. Evite 'HashMap` lookups – utilizamos arrays simples. Silencio
Silencio **Python** Silencio Usar comprensión de la lista con moderación; los bucles son lo suficientemente rápido. Silencio
Silencio **C++** Silencio Uso `estd::vector fielint `con `reservar` para evitar reasignaciones. Use `std::max_element` si prefiere legibilidad, pero el bucle manual es marginalmente más rápido. Silencio

-...

## 🎯 Final Thought > Call‐to‐Action

*“He resuelto LeetCode 689 en Java, Python y C++ y publicado el código en GitHub. También compartí mi solución en LinkedIn y recibí llamadas de entrevista de Google y Stripe.”*

■ Si te estás preparando para una entrevista de codificación, practica este problema *daily*. Agregue la solución a su cartera, escriba un post del blog, o cree un breve vídeo explicando el algoritmo. Aviso de trabajo cuando los candidatos *probar* sus habilidades de solución de problemas, no sólo *hablar* sobre ellos.

-...

### 📥 Download the full solution (all languages) → [GitHub Gist](https://gist.github.com/your-username/leetcode-689)

¿Quieres discutir otros desafíos de LeetCode? Deja un comentario o envíame DM en LinkedIn.

■ *Listo para romper su próxima entrevista? ¡Código, compartir y contratar! 🚀*
`` `

-...

### 6.3 Mejoras visuales

← Recurso Silencioso Cómo añadir
Silencio...
TEN **Diagrama de ventana deslizante** ANTE Utiliza un SVG o PNG que muestra la ventana móvil a través de la matriz. Silencio
Silencio **Code syntax highlight** ← Utilizar bloques de código marcado; Medium automáticamente resalta. Silencio
Silencio **Edge‐Case Table** tención Utilice tabla de marcado para referencia rápida. Silencio
Silencio **Enlace a GitHub repo** Silencio Proporcionar un enlace a un repo con las tres implementaciones del lenguaje. Silencio

-...

Siguientes pasos para ti

1. **Den el código** - pegar los fragmentos en su IDE favorito.
2. **Test edge cases** – por ejemplo, `nums=[1,2,3,4,5,6,7,8,9], k=3`.
3. **Publicar** – copiar el artículo en Medium/Dev.to con etiquetas relevantes.
4. **Share** – post on Linked En con un comentario: “Solved LeetCode 689 en Java, ¡listo para la próxima entrevista de codificación!”
5. **Apply** – use la conversación como punto de conversación en su próxima entrevista.

-...

■ **Feliz codificación " buena suerte en su próxima entrevista!
`` `

-...

*Eso es todo* Usted ahora tiene la solución *full*, *time‐space analysis*, *common pitfalls*, y un *ready‐to‐publish SEO‐rich article*. Deja esto en tu cartera, sigue practicando, y aterrizarás ese papel de ingeniería de software más rápido de lo que puedes decir “LeetCode 689”.

¡Feliz codificación! 🧩
`` `

-...

■ **Meta‐Note**: Si estás usando el artículo en Medium, establece el ** "Leer tiempo"** a unos 7-8 minutos para que coincida con los posts típicos de la solución LeetCode, y agrega una sección ** "Leer más"** para el próximo desafío de LeetCode.

-...

## 8down Cómo Compartir en LinkedIn

``text
Entendido Problema: LeetCode 689 – Suma Máximo de 3 Subarrayos que no funcionan
✅ Solución: O(n) pase lineal + prefijo/suffix índices max
Entendido Idiomas: Java, Python, C++
Entendido Echa un vistazo al código completo: https://github.com/username/leetcode-689
💬 Vamos a discutir cómo esto demuestra la ventana deslizante + dominio DP! #leetcode #interviewprep #softwareengineering
`` `

Deja el enlace a tu GitHub o al blog. A los clientes les encanta ver el código real, y el hashtag de discusión subirá su perfil a los gerentes de contratación.

-...

### 📅 Practica semanal Rutina

1. #Day 1** – Lea el problema " escriba el algoritmo en papel.
2. **Día 2** – Aplicar en un idioma, ejecutar en casos de muestra.
3. **Día 3** – Agregue las pruebas del borde (`n = 3k`, todos los ceros, grandes `k`).
4. **Día 4** – Escribe un blog o un video explicando la solución.
5. #Day 5** – Compartir en redes sociales, participar con comentarios.
6. **Día 6** – Revisar las soluciones de otros o someterse al juez en línea.
7. **Día 7** – Refleja los errores " refina tu código.

Repita con un nuevo problema de LeetCode.

-...

**Y esa es una guía completa** del algoritmo a la publicación, asegurando que obtenga el beneficio completo de la solución y la exposición a los reclutadores.

¡Buena suerte y disfrute de su preparación de entrevistas! 🚀

-...

*No dude en adaptar el artículo, el código y las redes sociales para adaptarse a su propio estilo y marca. *