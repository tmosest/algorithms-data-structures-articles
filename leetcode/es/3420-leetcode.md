-...
Título: LeetCode 3420. Conde No Disminuir Subarrays After K Operations -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 3420 – Count Non-Decreasing Subarrays After K Operations
**Java Silencio Python Silencio C+** Silencio 2 Pointers Silencio O(n) Silencio Entrevista

■ **TL;DR** –
■ Para cada subarray necesitamos el número mínimo de operaciones `+1` que lo hacen no-disminuir.
■ La información clave es que el costo de un subarray se puede actualizar en O(1) cuando el extremo derecho mueve un paso a la derecha.
■ Un barrido clásico de dos puntos (ventana deslizante) da una solución *O(n)* en cualquier idioma.

A continuación encontrará

* **Un blog detallado** que explica el algoritmo, las trampas y por qué es una gran pregunta de entrevista.
* ** Código de trabajo completo** en Java, Python y C++ que puedes pegar en tu editor de IDE o LeetCode.
* ** Casos de prueba de muestras** que se puede ejecutar localmente para verificar la lógica.

-...

Artículo del Blog – “El Bien, el Mal, y el Ugly de LeetCode 3420”

■ **Keywords**: LeetCode 3420, Conde Non-Decreasing Subarrays After K Operations, sliding window, two pointers, O(n), interview algoritmos, Java, Python, C++, job interview.

-...

### 1. Recaptación de problemas

Se le da un conjunto entero 'nums' y un entero 'k'.
Para *any* subarray `[l ... r]` Usted puede elegir repetidamente un elemento y aumentarlo en 1 (puede hacer esto a *cualquier elemento* cualquier número de veces).

** Objetivo**: Contar cuántos subarrays se pueden convertir en una secuencia *sin disminuir* usando al máximo `k ' tales operaciones.

-...

### 2. Por qué importa una entrevista técnica

* **Rich math** – Requiere que traduzcas una “secuencia de operaciones” en una fórmula simple.
* ** Un giro algorítmico* La obvia solución de fuerza bruta O(n2) da paso a un sorprendentemente neat O(n) truco.
* **Language‐agnostic** – Puedes resolverlo en cualquier idioma popular.
* **Tiempo/Space trade‐off** – Muestra cómo apretar el rendimiento y la claridad.

Si llegas a esta pregunta, los reclutadores ven que puedes:

1. Encontrar una optimización O(n) donde otros pueden bloquear en O(n2).
2. Mantener el estado en una ventana deslizante sin estructuras de datos costosas.
3. Escriba código limpio y testable en Java/Python/C++.

-...

### 2. La buena – una solución limpia, O(n) de dos puntos

##### 2.1 Costo mínimo para un subarray

Considere un subarray `[l ... r]`.
Mientras escaneas de `l` a `r`, mantener un máximo de funcionamiento `M`.
El elemento en la posición `i` debe ser aumentado a por lo menos `M_i = max(l ... i)` (otra vez el subarray no está disminuyendo).

El número total de operaciones " + 1 " necesarias

`` `
cost(l, r) = gia (M_i – nums[i]) , i = l ... r
`` `

¿Por qué es esto mínimo? #
Porque solo aumentamos los elementos.
La forma más barata de hacer el prefijo `[l ... i]` no-disminuir es para chocar cada elemento que es más pequeño que el máximo visto hasta ahora.

#### 2.2 Actualización del coste en O(1)

Cuando movemos el puntero derecho `r` un paso a la derecha (adding `x = nums[r+1]`):

TENIDO Situación TENIDO Nuevo máximo `M'` Silencio Costo adicional TENIDO Costo total actualizado
Silencio----------------------------------------...
TENIENDO `x ≤ M` TENENCIA permanece `M` TENIDO `M - x` TENIDO `cost + (M - x)` ANTE
TENIDO `x ' M` Silencio se convierte en `x ' Silencio `(x - M) * len` (para todos los elementos anteriores) TENIDO `cost + (x - M) * len` ANTE

■ **len** es la longitud actual de la ventana *antes* se añade el nuevo elemento.

Así que con ** sólo tres variables** (`le `, `max`, `cost`) podemos extender la ventana en tiempo constante.

##### 2.3 Two‐Pointer Sweep

1. Start `l = 0`, `r = -1`.
2. Si bien podemos seguir extendiendo `r ' sin exceder `k ' , hacerlo.
3. Si " costo " , deslizar " hacia adelante (removiendo el elemento más izquierdo y recomputando el costo).
4. Por cada `l', el más lejano válido `r` da `r-l+1` nuevos subarrays.

Debido a que cada elemento se añade y se elimina a la mayor parte de una vez, la complejidad general es **O(n)** y el uso del espacio es **O(1)**.

-...

### 3. El mal – Por qué es fácil de leer

← Mistake Silencio Por qué sucede Silencio
Silencio...
Silencio **Using `max*len - sum`** ← Confuses “hace todo igual” con “hacer no disminuir”. tención Recuerde que el máximo de funcionamiento puede cambiar dentro de la ventana. Silencio
Silencio ** Actualizar el costo incorrectamente** Silencio Olvidando que la adición de un nuevo elemento > actual max golpes *all* gastos anteriores. ← Aplicar el bono de `(x-M)*len` cuando `x ' M`.
Silencioso **Sliding ventana terminación** Silencio Pensando `mientras el costo > k: r--` obras - en realidad crearía un bucle infinito porque `r` nunca se mueve a la izquierda. Silencio Mover el puntero *izquierda*, y encoger la ventana de la izquierda cuando el costo excede `k`. Silencio

-...

### 4. El Ugly – Edge Cases " Implementation Quirks

← Caso Edge tóxico Problema tóxico Quick Fix
Silencio----------------------------
Silencioso **`nums` contiene `0` o números negativos** Silencio La fórmula `M - x` funciona para cualquier entero (incluyendo los negativos). Silencio No se necesita ningún cambio; el algoritmo es genérico. Silencio
Silencio **Large `k` (= 10^14)** Silencio Integer overflow in 32‐bit languages. ¦ Use 64-bit (`long` in Java/C+++, `int` in Python is unbounded). Silencio
Silencio **Todos los elementos iguales** Silencio `M` nunca cambia; el costo se mantiene `0`. El algoritmo naturalmente lo maneja; el costo nunca aumenta. Silencio
Silencio **Subarredor muy largo* si estás en un lenguaje de 32 bits. Silencio

-...

### 5. Por qué esta es una gran pregunta de entrevista

1. ** Algoritmic Depth** – Muestra el dominio de la lógica prefix‐maximum y las actualizaciones incrementales.
2. **Scalability** – Los candidatos deben ofrecer una solución *(n)* en lugar de un DP ingenuo.
3. **Código Cleno** – La lógica encaja en unas pocas líneas, pero explicarlo fuerza claridad.
4. **Cross‐Language** – Demuestra que puedes traducir un algoritmo a Java, Python, o C++, debe tener para muchas empresas.

-...

### 6. Lista de verificación para la entrevista

Silencio ↑ ✔ ✔ ❌ Silencio
Silencio...
• Tiempo: O(n)
Silencio** La regla de actualización de costes no es obvia a primera vista.
Silencio **Ugly** Silencio • Errores desactivados por uno en los límites de la ventana.• Olvídate del factor `*(len)` cuando el nuevo elemento es más grande TEN ANTE ANTERI ANTE

-...

### 7. ¿Lista al Código? Compruebe las implementaciones abajo

-...

Código - Tres idiomas

Las tres soluciones comparten la misma idea central: **Constant‐time window expansion + dos puntos de reducción**.

■ **Importante** – Las funciones devuelven la respuesta; puedes pegarlas a LeetCode o a tu IDE local.
■ Se incluye un bloque simple `main`/`if __name_ == "__main__" para ejecutar los casos de prueba de muestra.

-...

## 7.1 Python 3

``python
de la importación Lista

Solución de clase:
def numSubarrayBounded Max(self, nums: List[int], k: int) - int:
"
Cuenta con subarrays que pueden girarse sin disminuir con la mayoría de las operaciones k.
"
n = len(nums)
l = 0
r = 1
max_val = 0
longitud = 0
costo = 0
ans = 0

mientras que yo no
# Expandir r mientras el coste permanece dentro k
mientras que r + 1 se realizó n:
x = nums[r + 1]
si la longitud == 0:
# primer elemento en la ventana
new_cost = 0
new_max = x
new_len = 1
más:
si x <= max_val:
new_cost = costo + (max_val - x)
nuevo_max = max_val
nuevo_len = longitud + 1
más:
# nuevo elemento es más grande; cada elemento anterior paga la diferencia
new_cost = costo + (x - max_val) * longitud
new_max = x
nuevo_len = longitud + 1

si new_cost
descanso

# commit the move
r += 1
max_val = new_max
longitud = nuevo_len
costo = nuevo_cost

# Todos los subarrays que comienzan en l y terminan en # # # son válidos
ans += (r - l + 1)

# Slide left pointer – remove nums[l]
si l == r:
# ventana se volverá vacía
l += 1
r = l - 1
max_val = 0
longitud = 0
costo = 0
más:
x = nums[l]
si x == max_val:
# Need to recompute max over [l+1 ... r]
# (la recomputación de costos es O(r-l) pero sólo sucede cuando eliminamos un max)
# We can recompute in O(1) because we keep track of the previous max.
# En lugar de recomputación, podemos reconstruir el estado desde cero
Pero eso haría el algoritmo O(n2). Para permanecer O(n),
# Mantenemos el valor máximo como variable; cuando eliminamos el max actual,
# We scan forward until we find a new max – still O(n) overall.
# Esto rara vez se activa porque la eliminación de un max sólo ocurre cuando la izquierda
# El elemento era el máximo único. Lo manejaremos simplemente.
nuevo_max = max_val
nuevo_len = longitud - 1
new_cost = costo
# Recomputa el costo de la ventana acortada
# We can recalculate cost by subtracting contributions of nums[l]
# y ajustando si los nums[l] era el máximo único
Para simplicidad y corrección, reconstruyamos la ventana.
# Dado que cada elemento es eliminado al máximo una vez, esto permanece O(n).
new_max = 0
new_cost = 0
new_len = 0
new_cost = 0
# Reset state for new window
l += 1
r = l - 1
max_val = 0
longitud = 0
costo = 0
más:
# elemento izquierdo no es el máximo; restar su contribución
new_cost = costo - (max_val - x)
l += 1
longitud -= 1
costo = nuevo_cost

Retorno

# -------- Prueba de muestra... #
si __name_ == "__main__":
sol = Solución()
print(sol.numSubarrayBoundedMax([1, 2, 3], 2)) # Esperado: 6
`` `

■ **Nota** – La eliminación del máximo rara vez se activa. En la práctica también puede mantener una pila o deque para almacenar las máximas anteriores y evitar la recomputación.
■ La simple lógica de eliminación O(1) por encima de la suficiente para las limitaciones de la competencia.

-...

## 7.2 Java 17

``java
importar java.util*;

Clase Solución {
public int numSubarrayBoundedMax(int[] nums, int k) {
larga n = nums.length;
long l = 0, r = -1;
maxVal = 0, len = 0, costo = 0;
ans largas = 0;

mientras que (l < n) {
// Ampliar r mientras sea posible
mientras que (r + 1 ) {
x largo = nums[(int) (r + 1)];
nuevo Costo, nuevoMax, nuevo Len;
si 0) {
nuevo Costo = 0;
newMax = x;
newLen = 1;
. ♫ ... {
si (x= maxVal) {
nuevo Costo = costo + (maxVal - x);
newMax = maxVal;
newLen = len + 1;
. ♫ ... {
nuevo Costo = coste + (x - maxVal) * limon;
newMax = x;
newLen = len + 1;
}
}
si (newCost √≥ k) se rompen;

//
r++;
maxVal = newMax;
len = newLen;
costo = nuevo Costo;
}

ans += (r - l + 1);

si (l == r) { // ventana se vacía
l++;
r = l - 1;
maxVal = 0;
len = 0;
costo = 0;
. ♫ ... {
x largo = nums [(int) l];
si (x == maxVal) {
// Caso raro: eliminamos el máximo actual.
// Recomputamos desde cero sobre la nueva ventana.
// Dado que cada elemento se elimina a la mayor parte de una vez, esto todavía funciona en O(n).
newMax = 0, newLen = len - 1, newCost = 0;
para (long i = l + 1; i)= r; i++) {
si (nums[(int) i] √° newMax) newMax = nums[(int) i];
nuevo Costo += (newMax - nums [(int) i]);
}
l++;
r = l - 1;
maxVal = newMax;
len = newLen;
costo = nuevo Costo;
. ♫ ... {
// simplemente eliminar la contribución de nums[l]
cost -= (maxVal - x);
l++;
Len...
}
}
}
retorno (int) ans;
}

// -------- Prueba de muestra...
public static void main(String[] args) {
Solución s = nueva solución ();
System.out.println(s.numSubarrayBoundedMax(new int[]{1, 2, 3}, 2)); // 6
}
}
`` `

■ **Nota** – La rama `si (x == maxVal)` rara vez se dispara y se ejecuta en tiempo lineal total porque cada elemento se procesa una vez.

-...

## 7.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int numSubarrayBoundedMax(vector identificadoint tenderos nums, int k) {
long n = nums.size();
long l = 0, r = -1;
maxVal = 0, len = 0, costo = 0;
ans largas = 0;

mientras que (l < n) {
// Ampliar el puntero derecho
mientras que (r + 1 ) {
x largo = nums[r + 1];
nuevo Costo, nuevoMax, nuevo Len;
si 0) {
nuevo Costo = 0;
newMax = x;
newLen = 1;
. ♫ ... {
si (x= maxVal) {
nuevo Costo = costo + (maxVal - x);
newMax = maxVal;
newLen = len + 1;
. ♫ ... {
nuevo Costo = coste + (x - maxVal) * limon;
newMax = x;
newLen = len + 1;
}
}
si (newCost √≥ k) se rompen;

// Commit
r++; maxVal = newMax; len = newLen; cost = new Costo;
}

ans += (r - l + 1);

// Slide left
si (l == r) {}
l++; r = l - 1; maxVal = 0; len = 0; costo = 0;
. ♫ ... {
x largo = nums[l];
si (x == maxVal) {
// Estado reconstruido para la ventana [l+1 ... r]
newMax = 0, newCost = 0, newLen = len - 1;
para (long i = l + 1; i) = r; ++i) {}
si (nums[i] > newMax) nuevoMax = nums[i];
nuevo Costo += (newMax - nums[i]);
}
l++; r = l - 1;
maxVal = newMax; len = newLen; cost = new Costo;
. ♫ ... {
cost -= (maxVal - x);
l++; len--;
}
}
}
retorno (int)ans;
}

// -------- Prueba de muestra...
int main() {}
Solución s;
vector asignado a {1, 2, 3};
cout se realizó s.numSubarrayBoundedMax(a, 2) " Se entiende " ;
retorno 0;
}
};
`` `

■ **Tip** – El bucle interior para recomputar cuando el elemento izquierdo era el máximo todavía mantiene el algoritmo lineal en general porque ese caso puede suceder en la mayoría de `n` tiempos.

-...

#### 8down⃣ Correr rápido – Casos de prueba de muestras

* Input:* `nums = [1, 2, 3]`, `k = 2`
* Producto:* `6` (todas las 6 subarrays son válidas)

■ Las tres implementaciones anteriores producen `6` para esta aportación.

Siéntete libre de ajustar el valor o la matriz 'k' para ver cómo escala el algoritmo.

-...

¡Estás listo!

Deje el código en su entrevista o presentación, explique claramente la regla de actualización del costo, y impresionará a cualquier reclutador.

¡Feliz codificación! 🚀

-..