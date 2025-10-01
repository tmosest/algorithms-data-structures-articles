-...
Título: LeetCode 1095. Encontrar en Mountain Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 1095 – “Find in Mountain Array”
**Hard** Silencio **Binary Search Silencio Mountain Array ← Entrevista Prep**

■ Si estás buscando una solución sólida para entrevistas en **Python, Java, o C++**, has llegado al lugar correcto.
■ A continuación encontrará:
* Una explicación clara, paso a paso que aborda el *bueno, el malo, y el feo*.
* Fully working code snippets in **Python, Java, and C++** that respect the 100‐`get()`‐call limit.
* Un artículo mini-blog optimizado para SEO (palabras clave, encabezados, copia de meta-estilo) que puede duplicar como un post de cartera en LinkedIn o Medium.

■ **TL;DR** – Encontrar el pico primero, luego la búsqueda binaria de la parte creciente (regresar temprano si se encuentra), de lo contrario, la búsqueda binaria de la parte decreciente.

-...

## 1. Recaptación de problemas

■ Un array *mountain* es una secuencia que aumenta estrictamente a un solo pico y luego disminuye estrictamente.
■ Sólo se le permite leer el array a través de la interfaz `MountainArray`:
" texto
> int get(int index);
()
" `
■ El objetivo: **retornar el índice más pequeño `i` tal que `get(i) == target`, o `-1` si el objetivo está desaparecido. #
■ **Importante:** Hacer **No** hacer más de **100** llamadas a `get`.

Constraints:
* `3 ≤ mountainArr.length() ≤ 104 `
* `0 ≤ target, mountainArr.get(i) ≤ 106 `

-...

## 2. El “bueno, malo,”.

Silencio **Aspecto** Silencioso ** Qué hacer**
Silencio...
Silencio **Peak‐Finding** Silencio Usar una búsqueda binaria que compara `mid` y `mid+1`. Haga un escaneo lineal o llame repetidamente `get` en un bucle sin podar. Silencio
Silencio **Increasing‐Part Search** Silencio Búsqueda binaria clásica Val → izquierda = mid+1`). Silencio Tratar la parte descendente igual que ascendente – fracasará. Silencio
Silencio **Disminución-Part Search** Silencio Retroceder los movimientos punteros (`target √≥ midVal → right = mid-1`). Silencio Olvidar que `mid` ya es `-1` o `0` y todavía mantener `izquierda ≤ derecha`. Silencio
Silencio ** Call Count** Silencio Keep `get()` a un mínimo reutilizando la longitud del array y llamando `get` sólo dos veces por comparación. Silencio Call `get` en el mismo índice muchas veces o llame a un ayudante que se bucle sobre el array. Silencio
Silencio **Edge‐Cases** Silencio Revisar que `target` puede estar en el pico. Silencio Suponga que el array siempre está aumentando o siempre disminuyendo. Silencio
Silencio **Testing** Silencio Verificar con porciones ascendentes y descendientes. ← Saltar el requerimiento del índice *smallest* – devolver el primero encontrado en lugar del más bajo. Silencio

-...

## 2. Resumen del algoritmo

1. ** Obtener la longitud de la matriz** una vez: `n = mountainArr.length()`.
2. **Encontrar el índice de pico (`p`)** – búsqueda binaria con la regla `get(mid) → mover a la derecha; otra → mover a la izquierda.
3. **Buscar la parte ascendente `[0 ... p]** con la búsqueda binaria normal.
* Si se encuentra → devolver el índice inmediatamente (garantizado más pequeño).
4. **Busca la parte descendente `[p+1 ... n-1]** con una investigación binaria inversa.
5. Devuelve el resultado (o `-1` si no se encuentra).

El presupuesto de llamadas es muy inferior a 100:
* `peak` needs at most `log2(104) ♥ 14` iterations → about `28` calls (`get(mid)` and `get(mid+1)` each iteration.
* Cada búsqueda binaria necesita en la mayoría de las llamadas `14` → dos búsquedas más todavía te mantienen en el límite de 100-call.

-...

## 3. Análisis de la complejidad

Silencioso ** Métrico**
Silencio...
← Tiempo Silencioso **O(log n)** – una búsqueda máxima + en la mayoría de dos investigaciones binarias. Silencio
← Espacio Silencioso **O(1)** – no hay estructuras de datos adicionales, sólo algunas variables enteros. Silencio

-...

## 4. Muestras de código completo

■ Los siguientes snippets están listos para pegar en el editor LeetCode (sólo reemplazar la 'clase Solution' existente).
■ Cada uno honra la restricción de 100’get()`‐call y utiliza la interfaz exactamente como LeetCode espera.

#### 4.1 Python 3

``python
Definición para MountainArray.
# class MountainArray:
# def get(self, index: int) - int:
# def length(self) - título int

Solución de clase:
def findInMountainArray(self, target: int, mountain_arr: 'MountainArray') - título int:
n = mountain_arr.length()

# -------- helper: binaria search --------
def binario_search(izquierda: int, right: int, target: int, ascending: bool) int:
mientras que la izquierda:
media = (izquierda + derecha) // 2
mid_val = mountain_arr.get(mid)

si mid_val == target:
retorno

si asciende: # lógica ascendente normal
si blanco Mid_val:
izquierda = media + 1
más:
derecho = mitad - 1
más: # revertido para la parte descendente
si blanco Mid_val:
derecho = mitad - 1
más:
izquierda = media + 1
retorno -1

# -------- helper: encontrar el pico--------
def find_peak() - Propiedad int:
l, r = 0, n - 1
mientras que l
media = (l + r) // 2
# Sólo necesitamos dos consigues por iteración
si mountain_arr.get(mid)
l = media + 1 # pico es a la derecha
más:
r = media * pico es a mediados o a la izquierda
Regreso

pico = find_peak()

# 1 Buscar la parte ascendente primero
idx = binario_search(0, pico, target, ascending=True)
si idx!= -1:
idx

# 2⃣ Si no se encuentra, busque la parte descendente
retorno binario_search(peak + 1, n - 1, target, ascending=False)
`` `

■ **Por qué funciona* *
■ *El pico es el punto de pivote donde el array cambia la dirección.
■ Al buscar la parte ascendente primero garantizamos el índice *smallest* si el objetivo aparece antes del pico.
■ La búsqueda binaria inversa en el lado descendente funciona porque los elementos están disminuyendo estrictamente. *

-...

### 4.2 Java

``java
*
* Esta es la interfaz que LeetCode nos da. En la actualidad
* problema que no necesita implementarlo – se proporciona.
*/
interfaz MountainArray {}
int get (int index);
longitud();
}

Clase Solución {

int findInMountainArray(int target, MountainArray mountainArr) {
int n = mountainArr.length();

// ---------- helper: búsqueda binaria --------
// ascender = verdadero → búsqueda binaria normal
// ascender = falso → invertido (parte descendente)
Java.util. BiFunción realizadaInteger, Integer, Integer
(izquierda, derecha)
int l = izquierda, r = derecha;
mientras (l <= r) {
int mid = (l + r) 1;
int midVal = mountainArr.get(mid);
si (midVal == target) regresan a mediados;
si (target > midVal) l = mid + 1;
r = mediados - 1;
}
retorno -1;
};

Java.util. BiFunción realizadaInteger, Integer, Integer descSearch =
(izquierda, derecha)
int l = izquierda, r = derecha;
mientras (l <= r) {
int mid = (l + r) 1;
int midVal = mountainArr.get(mid);
si (midVal == target) regresan a mediados;
si (target > midVal) r = mid - 1; // revertido
l = mediados + 1;
}
retorno -1;
};

// ---------- Encontrar el pico --------
int l = 0, r = n - 1;
mientras que (l
int mid = (l + r) 1;
si (mountainArr.get(mid)
l = media + 1; // pico es a la derecha
. ♫ ... {
r = media; // pico es a mediados o a la izquierda
}
}
pico int = l;

// ---------- búsqueda parte ascendente --------
int idx = ascSearch.apply(0, pico);
si (idx!= -1) retorno idx;

// ---------- búsqueda parte descendente --------
descSearch.apply(peak + 1, n - 1);
}
}
`` `

■ *Puntos clave*
* " titulado " 1` es un turno derecho sin firmar - más rápido que `/ 2`.
* `BiFunction` se utiliza para la brevedad; también podría extraer métodos de ayuda privada si lo prefiere.
* La búsqueda de picos llama `get` twice per loop (`mid` y `mid+1`), pero las llamadas generales permanecen bien debajo de 100.

-...

#### 4.3 C++

``cpp
*
* Esta es la interfaz que LeetCode nos da. En la actualidad
* problema que no necesita implementarlo – se proporciona.
*/
Clase MountainArray {}
public:
virtual int get(int index) const = 0;
longitud de entrada virtual() const = 0;
};

Clase Solución {
public:
int findInMountainArray(int target, MountainArray &mountainArr) {
int n = mountainArr.length();

// -------- búsqueda binaria (descendiente o descendiente) --------
auto binarioSearch = [ cl](int left, int right, bool ascending) - int {
mientras (izquierda)
int mid = izquierda + (derecha - izquierda) 1);
int midVal = mountainArr.get(mid);

si (midVal == target) regresan a mediados;

si (ascendiendo) { // normal ascendente
si (target > midVal) izquierda = mediados + 1;
derecho = mediados - 1;
} otro { // revertido para la parte descendente
si (target > midVal) derecha = mid - 1;
más izquierda = mediados + 1;
}
}
retorno -1;
};

// -------- encontrar el pico (índice del elemento máximo) --------
int l = 0, r = n - 1;
mientras que (l
int mid = l + (r - l) 1);
si (mountainArr.get(mid)
l = media + 1; // pico es a la derecha
más
r = mitad; // pico a mediados o a la izquierda
}
pico int = l;

// ---------- buscar la parte ascendente primero--------
int idx = binarioSearch(0, pico, verdad);
si (idx!= -1) retorno idx;

// -------- si no se encuentra, busque la parte descendente ---
devolver binario Search(peak + 1, n - 1, false);
}
};
`` `

■ **Notas*
* La lambda captura `mountainArr` por referencia y trabaja con 'int` variables solamente.
* C+++ utiliza ` > 1` (hijo) para evitar la división.
* La búsqueda máxima utiliza `get(mid)` y `get(mid+1)` – al igual que la versión Java.

-...

## 5. Lista de verificación antes de presentar

Sustitúyase la " solución de clase " existente con el fragmento específico del idioma anterior.
- [ ] No hay funciones adicionales de ayuda que escanean toda la matriz.
- [ ] Ejecute los casos de prueba que proporciona LeetCode.
- [ ] Verifique que la respuesta es ** el índice más pequeño** (no cualquier ocurrencia).
- [ ] Asegúrese de que su código compila en el entorno dado (utilizar `#include &bits/stdc+++.h] si es necesario en C++).

-...

## 6. Conclusión

■ LeetCode **Find in Mountain Array** es un excelente ejercicio en la aplicación de la búsqueda binaria correctamente a un diseño de datos no trivial.
■ La clave es reconocer el cambio de dirección* (peak) y revertir los movimientos punteros para la parte descendente.
■ Contando cuidadosamente `get()` llamadas que te quedas cómodamente bajo el límite de 100 casillas.

¡Buena suerte y disfruta de romper la montaña! *

-...

*Si encuentras útil esta guía, por favor dale al problema LeetCode una calificación 👍 – ayuda a otros a aprender el patrón correcto. *