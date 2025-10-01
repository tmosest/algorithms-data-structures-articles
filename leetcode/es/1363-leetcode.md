-...
Título: LeetCode 1363. Múltiples de Tres -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📌 Mayor Múltiplo de Tres - LeetCode 1363
**Java  Python ← C++ ← Algorithm tención Entrevista Prep  Job‐Ready Coding**

-...

## Tabla de contenidos
1. [Norma general](#problema vista previa)
2. [Observaciones clave](Observaciones clave)
3. [Greedy + Modulo‐3 Counting](#greedy-modulo-3-counting)
4. [Detalles de implementación](Detalles de implementación)
* 4.1 Java
* 4.2 Pitón
* 4.3 C++
5. [Time & Space Complexity](#time-space-complexity)
6. [Cascos comunes & Casos de borde](#pitfalls)
7. [“Bien, Mal, Ugly” de la Solución”](#buen-bad-ugly)
8. [Por qué esto importa para su próxima entrevista de trabajo](#why-matters)
9. [Conclusión](#conclusión)

-...

## Problema de visión general ##
■ **LeetCode 1363 – Múltiples de Tres* *
■ Dado un conjunto de dígitos (`0‐9`), construir el número más grande posible ** que es un múltiplo de `3` concatenando cualquier subconjunto de los dígitos en cualquier orden.
■ Devuelve el resultado como una cadena (sin ceros líderes innecesarios). Regrese """ si no existe tal número.

Ejemplos
TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
TENIDO `[8,1,9]` TENIDO `"981" ANTE `981` es divisible por `3` y es el arreglo más grande. Silencio
TENIDO `[8,6,7,1,0]` TENIDO `"8760" TENIDO Removing the `1` da una suma divisible por `3`. Silencio
No se puede formar múltiples de `3`. Silencio

-...

## Observaciones claves: un nombre= "observaciones clave"
1. **Divisibilidad por 3**
Un número es divisible por 3 si la suma de sus dígitos es divisible por 3.
→ Sólo necesitamos la suma total** mod `3`.

2. **Sólo 10 dígitos distintos**
Podemos almacenar cuántas veces aparece cada dígito en un array de tamaño 10.
→ Memoria O(1), sin necesidad de clasificación.

3. **La eliminación de granedy**
Si la suma ≡ 1 (mod 3):
* Remove **one ** smallest digit ≡ 1 (mod 3) **or**
* Remove **two** dígitos más pequeños ≡ 2 (mod 3).

Si la suma ≡ 2 (mod 3):
* Eliminar **uno** dígito más pequeño
* Remove **two** dígitos más pequeños ≡ 1 (mod 3).

Eliminar los dígitos posibles *smallest* mantiene el número resultante lo más grande posible.

4. # Dejando Cero #
Después de la eliminación, la cadena podría comenzar con `0`.
* Si todos los dígitos restantes son `0`, devuelve `0'`.
* Si no quedan dígitos, devuélvanse `'.

-...

## Greedy + Modulo‐3 Contando un nombre = "greedy-modulo-3-counting"
1. Cuenta cada dígito (`0`‐`9`).
2. Compute `total Sum % 3`.
3. Decide cuántos dígitos de cada clase restante (`%3 == 1` o `2`) eliminar.
4. Construir la respuesta mediante iterating **de 9 a 0** y subir los dígitos restantes.
5. Casos de borde de la manija (la cadena vacía / sólo ceros).

Este enfoque funciona en **O(n)** tiempo (un paso para contar, limpieza de tiempo constante) y utiliza **O(1)** espacio extra.

-...

## Detalles de la Implementación: "implementation-details"
A continuación se presentan implementaciones limpias y bien agregadas en **Java, Python, y C++**.
Los tres comparten el mismo flujo lógico pero son idiomáticos para cada idioma.

#### 4.1 Java > = "java"
``java
importar java.util*;

Solución de la clase pública {}
public String largestMultipleOfThree(int[] digits) {
// Cuenta las ocurrencias de cada dígito.
int[] cnt = nuevo int[10];
int sum = 0;
para (int d : digitos) {
cnt[d]+;
suma += d;
}

// Determina cuántos dígitos eliminar.
int r1 = cnt[1] + cnt[4] + cnt[7]; // dígitos con restante 1
int r2 = cnt[2] + cnt[5] + cnt[8]; // dígitos con restante 2
int delete1 = 0, delete2 = 0; // eliminaciones del resto 1 / 2 dígitos

int rem = sum % 3;
si (rem == 1) {
si 1) { = 1 = }
si no (r2 >= 2) { delete2 = 2; }
de vuelta "; // imposible
} si (rem == 2) {
si 1) { delete2 = 1; }
si (r1 не= 2) { = 2 = 2}
de vuelta ";
}

// Quitar los dígitos más pequeños necesarios.
para (int d = 1; d) = 9 " cl 0; d += 3) { // 1,4,7
int take = Math.min(cnt[d], delete1);
cnt[d] -= take;
delete1 -= take;
}
para (int d = 2; d) = 9 > delete2 0; d += 3) { // 2,5,8
int take = Math.min(cnt[d], delete2);
cnt[d] -= take;
delete2 -= take;
}

// Construir el número de mayor a menor dígito.
StringBuilder sb = nuevo StringBuilder();
para (int d = 9; d 0; d--) {
(int i = 0; i) cnt[d]; i+) sb.append(d);
}

si (sb.length() == 0) devolver ";
si (sb.charAt(0) == '0') devuelve "0";
devolver sb.toString();
}

// Arnés de prueba simple
public static void main(String[] args) {
Solución s = nueva solución ();
System.out.println(s.largestMultipleOfThree(new int[]{8,1,9})); // 981
System.out.println(s.largestMultipleOfThree(new int[]{8,6,7,1,0})); // 8760
System.out.println(s.largestMultipleOfThree(new int[]{1})); // ""
}
}
`` `

■ **¿Por qué esta versión Java es eficiente? * *
* No ordenar → `O(n)` tiempo.
* Usa arrays de tamaño constante → mínimo sobrecabezamiento.
• Lógica directa con comentarios claros – excelente para entrevista pizarra blanca.

-...

### 4.2 Python #2 se hizo un nombre="python"
``python
de la importación Lista
de las importaciones de colecciones Contrato

Solución de clase:
def largestMultipleOfThree(self, digits: List[int]) - ratio str:
cnt = [0] * 10
total = 0
para d en dígitos:
cnt[d] += 1
total += d

r1 = cnt[1] + cnt[4] + cnt[7]
r2 = cnt[2] + cnt[5] + cnt[8]
delete1 = delete2 = 0
rem = total % 3

si rem == 1:
si r1 >= 1: delete1 = 1
elif r2= 2: delete2 = 2
devuelve ""
elif rem == 2:
si r2
elif r1 >= 2: delete1 = 2
devuelve ""

# Remove smallest digits of each remainder
para d in (1, 4, 7):
mientras se eliminan1 y cnt[d]:
cnt[d] -= 1
delete1 -= 1

para d in (2, 5, 8):
mientras se eliminan2 y cnt[d]:
cnt[d] -= 1
delete2 -= 1

# Resultado de construcción de 9 a 0
res = []
para d en rango(9, -1, -1):
res.extend([str(d)] * cnt[d]

si no res:
"Regresa"
si res[0] == Todos los ceros
"0"
volver ".join(res)

# ---- Ejemplo de uso...
si __name_ == "__main__":
s = Solución()
print(s.largestMultipleOfThree([8, 1, 9]) # 981
print(s.largestMultipleOfThree([8, 6, 7, 1, 0])
print(s.largestMultipleOfThree([1]) # "
`` `

■ #Python niceties #
• `cnt` es una lista de tamaño fijo → O(1) memoria.
• `Counter` es exagerado; una lista mantiene el algoritmo apretado.
* Los bucles 'mientras' hacen que el paso de eliminación sea explícito y fácil de leer en un pizarrón.

-...

#### 4.3 C++ > se hizo un nombre="cpp"
``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
cadena más grandeMultipleOfThree(vector seleccionadoint ánimos) {
array observado, 10 título cnt {}; // dígitos contados
larga suma = 0;
para (int d : digitos) {
++cnt[d];
suma += d;
}

int r1 = cnt[1] + cnt[4] + cnt[7];
int r2 = cnt[2] + cnt[5] + cnt[8];
int del1 = 0, del2 = 0;
int rem = sum % 3;

si (rem == 1) {
si 1) del1 = 1;
si no (r2 >= 2) del2 = 2;
de vuelta ";
} si (rem == 2) {
si 1) del2 = 1;
si (r1 не= 2) del1 = 2;
de vuelta ";
}

// eliminar mínimos números restantes-1 (1,4,7)
para (int d = 1; d) 0; d += 3) {
int take = min(cnt[d], del1);
cnt[d] -= take;
del1 -= tomar;
}
// eliminar mínimos restante-2 dígitos (2,5,8)
para (int d = 2; d) 0; d += 3) {
int take = min(cnt[d], del2);
cnt[d] -= take;
del2 -= take;
}

cadena res;
para (int d = 9; d 0; --d) {
res.append(cnt[d], char('0' + d));
}

si (res.empty()) regresa ";
(res[0] == '0') devolver "0";
restitución;
}
};

// prueba rápida
int main() {}
Solución s;
cout  se realizó s.largestMultipleOfThree({8,1,9})
cout se hizo s.largestMultipleOfThree({8,6,7,1,0})
cout se realizó s.largestMultipleOfThree({1})
}
`` `

■ **C+++ ventajas**
• Usa `arrayación obtenida,10 `` para memoria O(1).
• " anillo::append(count, char) " es una manera rápida de construir el resultado.
* Compacto pero completamente escrito – ideal para una entrevista coding-platform.

-...

## Time & Space Complexity ## Time > Complejidad Espacial >
Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------------------
TEN Java TENIDO **O(n)** Silencio **O(1)** (10-size array)
TENIDO Python TENIDO **O(n)** ANTERIOR **O(1)**
Silencio C++ Silencio **O(n)** Silencio **O(1)**

El algoritmo es lineal en la longitud de entrada y utiliza sólo una docena de bytes de memoria.

-...

## Common Pitfalls & Edge Cases " se hizo un nombre= "pitfalls"
¿Qué pasa?
Silencio-----------------------------Prince--
Silencio **Removiendo demasiados dígitos** – por ejemplo, eliminando todos los dígitos de `%1` cuando sólo existió TENIDO Deja una suma no visible ANTERIED Check `r1` y `r2` antes de la eliminación. Silencio
*Dejar sólo ceros* – por ejemplo, introducir `[0,0,0] ' La cadena resultante `"000" → debe ser `"0" Silencio Después de construir la cuerda, si `sb[0] == '0' `retorno `"0 ". Silencio
Silencio ** Salida vacía** – después de la eliminación no quedan dígitos Silencio Devolver `""" Silencio Si `sb.length()==0` → `"."
Silencio **Sorting** – el uso de `sort()` será `O(n log n)` Silencio más lento, no requerido Silencio Cuenta dígitos en lugar de ordenar. Silencio
Silencio **Off‐by-one en los bucles** – clases de sobrantes de mal manejo ← Deleciones incorrectas ¦ Use tuples claros `(1,4,7)` y `(2,5,8)` o paso a paso por 3. Silencio

-...

## “Bueno, malo, ugly” de la solución se hizo un nombre= "buen-bad-ugly"

Silencio Silencio
Silencio------------Prince------
Silencio **Concepto** Silencio Utiliza una propiedad matemática (sum % 3) que convierte el problema en una pregunta *removal*. El texto del problema podría engañarte para pensar que necesitas ordenar o generar permutaciones. Silencio Ninguno – la solución es limpia; la parte “muy” es sólo manejar el caso del borde “0”, que es inevitable. Silencio
Silencio ** legibilidad de cuentas** Silencio Comentarios explican *por qué* eliminamos dígitos particulares. Los bucles muy largos pueden tener una intención oscura si lo atrae todo en una línea. ← Sobre-ingeniería (por ejemplo, usando montones o recursión) es innecesario y hará que su código parezca clunky. Silencio
Silencio ** Estilo de visión** Silencio Trabaja en una pizarra – sólo una serie de 10 contadores, unos pocos cálculos enteros, y un bucle de 9→0. Silencio En Python o JavaScript puede ser tentado a utilizar 'sort()` para la simplicidad; que sería una bandera roja para los entrevistadores que esperan O(n). tención No utilizar la propiedad modulo‐3 y en lugar de intentar brute‐force todos los subconjuntos condenará su solución a tiempo exponencial. Silencio

-...

## Why This Matters for Your Next Job Interview #1 name="why-matters"
* ** Pensamiento algorítmico** – Demuestra que puedes derivar un *invariante matemático* (suma de dígitos) y convertirlo en un algoritmo codicioso.
* **Space-time trade‐offs** – Muestra que sabes cuándo ordenar es desperdicio y puedes reemplazarlo contando.
* **Cobertura por caso* Los entrevistadores aman a los candidatos que piensan en escenarios de “respuesta vacía” y “sólo ceros”.
* **Código Clean** – Soluciones bien comunicadas, lenguaje-idiomáticas indican profesionalidad y habilidades de comunicación.
* **Versatilidad** – Ser capaz de implementar la misma lógica en Java, Python, o C++ demuestra que puede adaptarse rápidamente a las pilas tecnológicas.

■ **Pro tip**: Al caminar a través de este problema en una pizarra blanca, comience con un rápido boceto de “sum % 3” → “deletrear uno o dos dígitos” → “compilar de 9 a 0”. Destaca la matriz de 10 tamaños. El entrevistador verá inmediatamente que está en la pista correcta.

-...

## Conclusión > Lectura posterior > > >
El problema **Largest Multiple of Three** es un ejemplo clásico de cómo una pregunta aparentemente combinatoria colapsa en un simple problema aritmético modulo. Al aprovechar el hecho de que sólo existen diez dígitos distintos, podemos construir un algoritmo codicioso lineal a tiempo, constante y espacial que es tanto **eficiente** como ** fácil de entender**.

Si te estás preparando para las entrevistas de codificación, este problema es un problema imprescindible porque prueba:
1. Conocimiento de la teoría de números (divisibilidad para 3).
2. Capacidad para diseñar estrategias codictivas.
3. Habilidad en el manejo de los casos de bordes (cerrar ceros, eliminaciones imposibles).
4. Aplicación limpia en varios idiomas.

-...

### 🚀 Listo para el nivel Up?
Trate de resolver el problema en LeetCode usted mismo (enlace abajo) y luego compare sus soluciones a las tres implementaciones anteriores.
🔗 **LeetCode 1363 – Múltiplo más grande de Tres**: Identificado https://leetcode.com/problems/largest-multiple-of-three/año

Buena suerte, y que su próxima entrevista sea un múltiplo perfecto de tres!