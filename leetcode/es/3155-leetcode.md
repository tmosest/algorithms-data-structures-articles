-...
Título: LeetCode 3155. Número máximo de servidores de pregrado -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Conseguir 3155. Número máximo de servidores de alta calidad – Solución Full-Stack
■ ** Tipo de problema:** Media – búsqueda binaria
■ **Idiomas: Java 17 Silencio Python 3 Silencio C+17
■ **LeetCode Link:** https://leetcode.com/problems/maximum-number-of-upgradable-servers/

-...

### 1. Recaptación de problemas

Tienes centros de datos.
Para el centro de datos `i` usted sabe:

TENCIÓN TERRITORIO TENIDO Significado ANTE
Silencio...
Silencio `contra[i]` Silencioso # de los servidores que posees
TENIDA `agradable[i] ' TENIDO dinero necesario para actualizar **un servidor**
Silencio. dinero que recibes cuando vendes **un servidor**
Silencioso `dinero[i]` Silencioso dinero que ya tienes

Usted puede vender cualquier número de servidores (`0 ... cuenta[i]`) **en el centro de datos sólo**.
Después de vender, puede actualizar tantos de los servidores restantes como su dinero lo permita.

** Objetivo** – Para cada centro de datos, el número *maximum* de servidores que se pueden actualizar.



-...

### 2. Observaciones " Intuición

* Si decidimos actualizar los servidores "x", debemos mantener al menos los servidores "x".
De ahí `x ≤ conteo[i] - s`, donde `s` = # vendido.

* El dinero total después de vender `s` servidores es `dinero[i] + s * vender[i]`.
Para actualizar `x` servidores necesitamos `x * actualizaciones[i]` dinero.

* Debemos encontrar el más grande `x' de tal manera que exista un `s` satisfacer ** ambos**
`x ≤ count[i] - s` **and** `money[i] + s * sell[i] ≥ x * upgrade[i]`.

La clave es que para un *fijo* `x` el `s más pequeño que satisface la restricción de dinero es

`` `
s_min = ceil(x * upgrade[i] - money[i]) / sell[i]
`` `

Si `s_min` es negativo podemos ponerlo en `0`.
La restricción `x ≤ conteo[i] - s` se convierte en `s ≤ conteo[i] - x`.

Así que para un `x' dado sólo necesitamos comprobar:

`` `
max(0, ceil(x*upgrade - money)/sell))
`` `

Si la desigualdad sostiene, los servidores x son actualizables.
De lo contrario, no lo son.

Puesto que la respuesta es un entero entre `0` y `count[i]`, podemos buscar binario sobre `x`.
Cada cheque es O(1). La complejidad general por centro de datos es `O(log count[i])`,
y para todos los centros de datos `O(n log maxCount)` – lo suficientemente rápido para `n, contar ≤ 105`.

-...

### 3. Algoritmo (Pseudo)

`` `
para cada centro de datos i
Lo siento. 0
[i]
mientras que lo
media = (lo + hola + 1) / 2 // media superior para evitar el bucle infinito
/ / / Cálculo requerido de la cantidad de venta
requerido = max(0, ceil(mid * upgrade[i] - dinero[i]) / vender[i])
si es necesario
lo = media / / media es alcanzable
más
hola = media - 1
respuesta[i] = lo
`` `

`ceil(a / b)` in integer arithmetic: `(a + b - 1) // b` (with `a ≥ 0`).
Todos los productos intermedios son hasta " 1010 " , así que " largo " (Java / C++) o Python `int` es seguro.

-...

### 4. Prueba de corrección

Demostramos que el algoritmo devuelve los servidores optimizables máximas para cada centro de datos.

**Lemma 1**
Para cualquier entero `x` (0 ≤ x ≤ conteo),
`x` servidores se pueden actualizar sif

`` `
max(0, ceil(x*upgrade - money)/sell))
`` `

*Proof. *
- Necesidad:
Seamos el número real de servidores vendidos.
`x` actualización requiere `x ≤ conteo - s` ⇒ `s ≤ conteo - x`.
Dinero después de la venta: `dinero + s*sell ≥ x*upgrade` ⇒
`s ≥ ceil(x*upgrade - money)/sell)`.
Así el más pequeño posible `s` que satisface la condición de dinero es
`s_min = max(0, ceil((x*upgrade - money)/sell)).
Para una solución factible debemos tener `s_min ≤ s ≤ conteo - x`.
Por lo tanto `s_min ≤ contar - x`.

- Suficiencia:
Si `s_min ≤ contar - x` elegir `s = s_min`.
Entonces `s ≤ cuenta - x` ⇒ conservamos al menos `x` servidores.
Y por definición de 's_min' tenemos suficiente dinero:
`dinero + s_min*sell ≥ x*upgrade`.
Así se pueden actualizar los servidores x. ∎



*Lemma 2*
Para cada centro de datos la búsqueda binaria en el algoritmo devuelve el mayor `x`
Lemma 1.

*Proof. *
El predicado `P(x)` definido como "`x` es actualizable" es monotónico:
si los servidores 'x` son actualizables entonces cualquier 'y' identificado x` son actualizables también
( vendiendo los mismos o más servidores).
Búsqueda binaria en un predicado monotono siempre devuelve el máximo `x `
con "P(x)" verdadero.
El algoritmo utiliza la fórmula media superior `(lo+hi+1)/2`, por lo que converge a la
más factible



**Teorema* *
Para cada centro de datos el algoritmo produce el número máximo posible de
servidores actualizados.

*Proof. *
Por Lemma 1 el predicado utilizado en la búsqueda binaria es exactamente la viabilidad
condición.
Por Lemma 2 la búsqueda binaria produce el mayor `x` que satisface esto
condición, que por definición son los servidores máximos actualizables. ∎



-...

### 5. Análisis de la complejidad

Silencio Silencio
Silencio...
Silencio Por centro de datos búsqueda binaria Silencio `O(log count[i])` Silencio
Silencio Todos los centros de datos soportan `O(n log maxCount)` Silencio
Silenciosos en memoria extra por centro de datos, `O(n)` para el array de respuesta

Con `n, contar ≤ 105`, esto encaja fácilmente dentro de los límites.

-...

### 6. Aplicación de las referencias

■ **Consejo:** Use `long` (Java / C++) o `int` (Python) para productos intermedios para evitar el desbordamiento.

-...

#### 6.1 Java 17

``java
importar java.util*;

Solución de la clase pública {}
int[] maxUpgrades(int[] count, int[] upgrade, int[] sell, int[] money) {
int n = count.length;
int[] ans = nuevo int[n];
para (int i = 0; i)
int lo = 0, hola = count[i];
mientras (lo cautivado) {
int mid = (lo + hola + 1)  1; // media superior
long need = (long) mid * upgrade[i] - dinero[i];
tiempo necesario Vender = 0;
si necesita 0) {
requeridoSell = (necesidad + venta[i] - 1) / vender[i];
}
si (requeridoSell <= (long) cuenta[i] - A mediados de) {
lo = medio;
. ♫ ... {
hola = mediados - 1;
}
}
ans[i] = lo;
}
devolver los ans;
}
}
`` `

-...

#### 6.2 Python 3

``python
Solución de clase:
def maxUpgrades(self, count, upgrade, sell, money) - titulada list[int]:
ans = []
para cnt, up, sl, mo in zip(count, upgrade, sell, money):
Lo, hola = 0, cnt
mientras que lo hizo hola:
media = (lo + hola + 1) // 2
necesidad = media * arriba - mo
required_sell = 0 si es necesario 0 0 (necesidad + sl - 1) // sl
si es necesario_sell
Lo siento.
más:
hola = media - 1
ans.append(lo)
Retorno
`` `

-...

#### 6.3 C+17

``cpp
Clase Solución {
public:
vector identificador principal maxUpgrades(vector correspondint
vector asignadoint
vector significado vender,
vector significando dinero
int n = count.size();
vector:
para (int i = 0; i) {}
int lo = 0, hola = count[i];
mientras (lo cautivado) {
int mid = (lo + hola + 1) / 2; // superior mid
larga necesidad = 1LL * media * actualización[i] - dinero[i];
largo tiempo requerido Vender = 0;
si necesita 0) {
requeridoSell = (necesidad + venta[i] - 1) / vender[i];
}
si (requeridoSell <= 1LL * cuenta[i] - A mediados de) {
lo = medio;
. ♫ ... {
hola = mediados - 1;
}
}
ans[i] = lo;
}
devolver los ans;
}
};
`` `

-...

### 7. Casos de borde " Pitfalls

Silencio Caso Edge Silencio Qué ver para Silencio
Silencio----------------------
Silencioso `sell[i]` muy pequeño, pero `dinero[i]` ¿Ya es suficiente para la División de Vida por cero? Silencio. 1` por restricciones, pero guarde con `si (necesitado 0= 0)` Silencio
Silencio Productos muy grandes (hasta 1010) Silencio 32-bit desbordamiento Silencio Uso 64-bit (`long` / `long long`) Silencio
Silencio `contra[i]` = 0 Silencio La búsqueda binaria todavía funciona (0.0) Silencio No se necesita un manejo especial
Silencio Todos los servidores ya son asequibles para actualizar ¦Debería devolver `count[i]` La búsqueda binaria termina en `hi` = `count[i]` Silencio

-...

### 8. Estrategia de examen

1. ** Pruebas de muestra** – Provista en la declaración del problema.
2. **Edge tests**
- `contra = [0]` → respuesta `[0]
- `dinero' lo suficientemente grande para actualizar todo → respuesta `cuenta `
- `sell` = 1, `upgrade` = 1, `dinero` = 0, `contra` = 10 → respuesta `0` (necesita vender por lo menos `10` para actualizar `0`?)
3. ** Pruebas desarmizadas** – Generar valores aleatorios (dentro de limitaciones) y verificar con fuerza bruta (pequeña `contra`).
4. ** Pruebas de tensión** – Tamaño máximo de entrada (`n = 105`, cada `cuenta = 105`) para garantizar que se respeten los límites de tiempo y memoria.

-...

### Resumen

* **Problema:** Maximizar servidores actualizados por centro de datos vendiendo algunos servidores.
* **Idea clave:** Búsqueda binaria sobre el número de servidores actualizados y un simple cheque de viabilidad utilizando aritmética entero.
* ** Complejidad: ** `O(n log maxCount)` tiempo, `O(1)` espacio extra.
* ** Resultado:** Soluciones listas para copiar en Java, Python y C++.

-...

### 10. SEO‐Optimized Takeaway

Si te estás preparando para una entrevista de ingenieros de software ** y quieres mostrar tu dominio de **búsqueda binaria** y ** razonamiento algoritmico**, este problema es un escaparate perfecto. Utilice los fragmentos de código arriba en su cartera, resaltar el análisis **time/space**, y estar listo para explicar la prueba **mathematical**—todo lo cual demuestra su profundidad de comprensión.

¡Buena suerte aterrizando ese trabajo de ensueño! 🚀

-...

■ **Keywords**: Maximum Number of Upgradable Servers, LeetCode 3155, Binary Search, Java solution, Python solution, C++ solution, interview question, algoritmo analysis, coding interview, software engineer, job interview, programming challenge, data center optimization.