-...
Título: LeetCode 2470. Número de Subarrays With LCM Equal to K -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 LeetCode 2470 – “Número de Subarrayos con LCM = K”
**Java ⋅ Python ← C++ – Full Working Solutions + Blog Guide**
*(SEO optimizado, “el bueno, el malo y el feo” para tu próxima entrevista)*

-...

## 1. Panorama general de los problemas

■ **Given** un array entero `nums` (1 ≤ `nums.length` ≤ 1000) y un entero `k` (1 ≤ `k` ≤ 1000).
■ **Retorno** el número de subarrays contiguos** cuyos múltiples (LCM)** son iguales a `k ' .

Un subarray es una rodaja sin vacío contigua de `nums`.
El LCM de un array es el número entero positivo más pequeño divisible por **todo** elemento.

■ *Ejemplo*
[3, 6, 2, 7, 1]`, `k = 6` → respuesta: **4** (los cuatro subarrays enumerados en la declaración del problema).

-...

## 2. Observaciones clave

TENCIÓN ANTERIOR Por qué importa
Silencio...
Silencio `LCM(a, b)` sólo puede ** crecer** o permanecer el mismo cuando anexamos más números Si alguna vez supera `k`, ninguna extensión posterior lo traerá de vuelta → podemos **break** temprano. Silencio
tención `nums[i] ≤ 1000` y `k ≤ 1000` tención Limita el máximo útil LCM que necesitamos considerar. Silencio
Silencio `LCM` se puede computar usando `LCM(a, b) = a / gcd(a, b) * b` Silencio `gcd` es barato (altitmo euclidiano) y mantiene los valores intermedios pequeños. Silencio
tención **La complejidad del tiempo**: `O(n2)` está bien para `n ≤ 1000` tención 1 000 000 iteraciones son triviales para las CPU modernas. Silencio

-...

## 3. El “bien” – El algoritmo básico

``text
ans = 0
para i = 0 ... n-1:
Cur = 1
para j = i ... n-1:
cur = lcm(cur, nums[j])
if cur == k: ans++
si cur > k: romper // no es necesario extender este subarray más
Retorno
`` `

* `cur` sostiene el LCM de `nums[i...j]`.
* Tan pronto como `cur не k` dejamos de extender ese subarray porque LCM no puede reducir.
* `lcm` se computed via `gcd` para evitar el desbordamiento y mantenerlo rápido.

-...

## 4. “El mal” – Pitfallas comunes

Silencio Pitfall Silencio
Silencio...
Silencio Usando un ingenuo `lcm` que se multiplica antes de dividir → overflow TENIDO Use `cur / gcd(cur, x) * x` (o `std::gcd` en C+17). Silencio
Silencio Olvídalo para romper cuando "cur " k " → O(n3) en el peor de los casos  durable Añadir `romper ' después de la comparación. Silencio
Silencio Usando `doble` o punto flotante para LCM → errores de precisión Silencio Stick to integer arithmetic only. Silencio
Silencio No manejar el caso `k == 1` adecuadamente Silencio El algoritmo cuenta naturalmente subarrays cuyo LCM es exactamente 1. Silencio

-...

## 5. “El Ugly” – Pruebas de Casos de Edge

Silencioso Caso Edge Qué hacer para probar
Silencio--------------
Silencio `k` no presente en array Silencio Resultado debe ser 0. Silencio
Silencio Todos los elementos son 1 Silencio Cada subarray tiene LCM = 1.
Silencio `k` iguala el producto de varios elementos Silencio Asegurar que el algoritmo no se pierda los subarrays de varios elementos. Silencio
Silencio Grande `k` cerca de 1000 Silencio Verificar que la lógica 'romper' funciona correctamente. Silencio

Siempre ejecute el siguiente arnés de prueba:

``python
def brute(nums, k):
importar matemáticas
ans = 0
para i en rango(len(nums)):
para j en rango(i, len(nums)):
Cur = 1
para x en nums[i:j+1]:
cur = cur * x // math.gcd(cur, x)
si cur == k:
ans += 1
Retorno
`` `

Revise la salida de su implementación contra esta fuerza bruta para insumos aleatorios.

-...

## 6. Aplicación del Código Completo

## 6.1 Java (LeetCode Style)

``java
Clase Solución {
public int subarrayLCM(int[] nums, int k) {
int count = 0;
para (int i = 0; i)
int curLcm = 1;
para (int j = i; j) {}
curLcm = lcm(curLcm, nums[j]);
si (curLcm == k) cuenta++;
si (curLcm > k) romper; // importante optimización
}
}
recuento de retorno;
}

int privado lcm(int a, int b) {}
devolver a / gcd(a, b) * b;
}

int gcd privado (int a, int b) {}
mientras (b!= 0) {
t = un % b;
a = b);
b = t;
}
devolver a;
}
}
`` `

### 6.2 Python 3

``python
de la importación de matemáticas gcd

Solución de clase:
def subarrayLCM(self, nums: list[int], k: int) - título int:
Conteo = 0
n = len(nums)
para i en rango(n):
Cur = 1
para j en rango(i, n):
cur = cur * nums[j] // gcd(cur, nums[j])
si cur == k:
Cuenta += 1
si cur > k:
descanso
cuenta de retorno
`` `

### 6.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int subarrayLCM(vector fielmente unido nums, int k) {
int count = 0;
para (int i = 0; i) ++i) {
Cura larga larga = 1;
para (int j = i; j) ++j) {
cur = cur / std::gcd(cur, (long long)nums[j]) * nums[j];
si (cur == k) + cuenta;
si (cuerdo > k) romper; // prune la búsqueda
}
}
recuento de retorno;
}
};
`` `

■ **Nota**: 'long long' mantiene el producto intermedio seguro, a pesar de que rompemos cuando `cur не k`.

-...

## 7. Análisis de la complejidad

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
Silencio fuerza bruta (lazos inclinados + " lcm " ) Silencio **O(n2)** (conceder 1 000 000 000 ops for `n=1000 ' ) Silencio **O(1)**
Silencio Usando `romper' en `cur > k Mismo peor caso, a menudo más rápido en la práctica

Con `n = 1000`, esto se ejecuta bajo un milisegundo en todos los idiomas.

-...

## 8. Por qué este blog ayuda a su carrera

1. **Entreview Mastery** – El problema de subarray LCM es un medio *clásico* LeetCode que demuestra su comprensión de la teoría del número, el razonamiento de dos puntos / deslizante de estilo ventana, y trucos de optimización.
2. **Multilingual Show‐case** – Tener soluciones listas para copiar en Java, Python y C++ demuestra que eres un ingeniero versátil cómodo en toda la pila.
3. **SEO‐Friendly Content** – Al esparcir palabras clave como “LeetCode 2470”, “Número de Subarrays Con LCM Equal to K”, “Problema de subarray LCM”, y “entrevista de codificación”, los reclutadores que se arrastran por la experiencia de solución de problemas detectarán su puesto.
4. **Structured Insight** – Explicar “bueno, malo, feo” demuestra habilidades de codificación reflexiva, algo que los entrevistadores valoran al evaluar la antigüedad.

-...

## 9. Lista de verificación final antes de presentar

- [ ] **Reúne todos los casos de prueba** (proporción, borde y aleatorio).
- [ ] **Comentario** las partes clave (`lcm`, `break`).
- [ ] **Comprobar el desbordamiento**: usar `long'/`int64_t` en C++, `long` en Java si desea ser extra seguro.
- [ ] **Hora tu solución** en una máquina local - debe ser de 5 ms para `n=1000`.
- [ ] **Push to GitHub** y añadir un README claro con una breve explicación - los reclutadores aman las muestras de código abierto.

-...

## 10. TL;DR

■ **Algorithm**: Doble bucle, compute running LCM, romper cuando excede `k`.
■ ** La complejidad**: `O(n2) ` tiempo, `O(1)` espacio.
■ ** Resultado**: Conde de subarrays cuya MCM es exactamente 'k'.
■ **Idiomas**: Java, Python, C++ listo para copiar.

¡Feliz codificación, y que esos entrevistadores amen sus soluciones de seguridad LCM! 🚀

-..