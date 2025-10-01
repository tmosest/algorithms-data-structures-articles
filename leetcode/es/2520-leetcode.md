-...
Título: LeetCode 2520. Cuenta los dígitos que dividen un número -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2520. Cuenta los dígitos que dividen un número
*LeetCode Easy – 100 % beat rate in Java*

#### TL;DR
- ** Objetivo**: Contar cuántos dígitos de 'num' dividen uniformemente 'num'.
- **Idea**: Extraiga dígitos uno por uno de la divisibilidad correcta y de prueba.
- ** Complejidad**: `O(log10 num)` tiempo, `O(1)` espacio (constant).
- **Idiomas**: Java, Python, C++ – todos listos para saltar.

-...

Declaración de problemas

■ **Given** un entero `num` (1 ≤ num ≤ 109) que contiene **no cero** dígitos,
■ **Retorno** el número de dígitos en `num' que divide `num` uniformemente (`num % digit == 0`).

*Examples*

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
Silencio `7` Silencio `1` Silencio 7 se divide. Silencio
Silencio `1` aparece dos veces → 2.
Silencio `4` Silencio Todos los dígitos dividen 1248. Silencio

-...

## 🔍 Why This Problem is a Gold‐Mine for Interview Prep

- **El truco de procesamiento de dígitos clásicos** - aprender a quitar dígitos con '% 10' y '/ 10'.
- **Concientización por caso edge** – no cero dígitos → ninguna división por cero preocupaciones.
- **Tiempo de intercambio espacial** – simple escaneo lineal, O(1) memoria auxiliar.
- ** Práctica de idiomas** – implementar una vez, leer en Java, Python, C++.

-...

## 🧠 Solution Overview

1. **Mantenga una copia** del número original (`original = num`).
2. **Loop** mientras que " original " 0
- 'digit = original % 10' - último dígito.
- `original /= 10` - suelte el último dígito.
- Si `num % digit == 0`, incremento `contra`.
3. Regresa a la cuenta.

Debido a que nunca construimos una cadena o un array, el algoritmo es eficiente en memoria.

-...

## 📊 Complexity Analysis

TEN TERRITOR TEN Fórmula ANTE ANTE ANTE ANTE
Silencio--------------------
Silencio **Tiempo** Silencio Cada bucle procesa un dígito decimal → `O(log10 num)` Silencio ~ 10 iteraciones para un int de 32 bits
Silencio **Espacio** Silencioso Sólo un puñado de integers Silencio

-...

## ⋅ Common Pitfalls & Gotchas

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio...
*Tratar de convertir el número a una cadena y luego iterating* tención Utilizar operaciones numéricas (`% 10`, `/ 10`) – más rápido y idiomático. Silencio
tención *Permitir cero en la lista de dígitos* Silencio Problema no garantiza ceros; si usted código para un caso genérico, guarde contra `digit == 0` para evitar división por cero. Silencio
*Usar un enfoque recursivo que puede soplar la pila* Silencio Es más seguro para grandes números. Silencio

-...

## 📦 Code Snippets

A continuación se encuentran soluciones limpias, listas para pasar en **Java, Python, y C++**. Siéntete libre de copiar, correr o adaptarlos para tu preparación de entrevistas.

## Java

``java
*
* LeetCode 2520: Cuenta los dígitos que dividen un número
* O(log num) time, O(1) space
*/
Clase Solución {
public int countDigits(int num) {}
int original = num; // mantener el número original para cheques de divisibilidad
int count = 0; // result accumulator

mientras (original!= 0) {
int digit = original % 10; // obtener el último dígito
original /= 10; // quitar el último dígito

(número dígito == 0) { // check divisibility
contar++;
}
}
recuento de retorno;
}
}
`` `

## Python

``python
# LeetCode 2520: Cuenta los dígitos que dividen un número
# O(log num) time, O(1) space

def countDigits(num: int) - título int:
original, cuenta = num, 0
original:
dígito = original % 10
original //= 10
si num % digit == 0:
Cuenta += 1
cuenta de retorno
`` `

### C++

``cpp
// LeetCode 2520: Cuenta los dígitos que dividen un número
// O(log num) time, O(1) space
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int countDigits(int num) {
int original = num;
int count = 0;
mientras (original) {
int digit = original % 10;
original /= 10;
(número dígito == 0) ++cuenta;
}
recuento de retorno;
}
};
`` `

-...

## 📚 Walk‐through of the Java Implementation

1. **Variables* *
- `original` preserva el `num original.
- "contra" almacena la respuesta final.

2. **Loop**
- `digit = original % 10` tira el dígito más correcto.
- 'original /= 10' cambia el número derecho.
- Si el dígito divide `num`, aumenta `contra`.

3. Retorno**
El bucle termina cuando `original` es cero; 'cuenta' ahora tiene el número de dígitos divisores.

-...

## 🔧 "El Bien, el Mal, el Ugly"

Silencio Silencio
Silencio------------Prince------
Silencio **Bueno** Silencio Escaneo lineal; espacio constante; sin operaciones de cadena costosas. tención Fácil de entender; perfecto para preguntas de entrevista. Silencio Ninguno – esta es una solución limpia. Silencio
Silencio **Bad** Silencio Si el número fuera muy grande ( не 64‐bit ), usted necesitaría BigInteger. El problema no garantiza ceros, así que saltamos cero. Silencio Si accidentalmente se divide por cero, el programa se estrella. Silencio
Silencio **Equipo** Silencio El estilo del código se puede mejorar con el regreso temprano para números de un dígito. Silencio N/A Silencio

-...

## 🚀 How This Blog Helps Your Job Hunt

- **SEO Palabras clave**:
`LeetCode`, `Count the Digits That Divide a Number`, `coding interview`, `algorithm`, `Java solution`, `Python solution`, `C++ solution`, `O(log n) time`, `O(1) space`, `interview prep`, `software engineer interview`.
Incluyendo estos términos en su currículum o cartera aumentará la visibilidad en los motores de búsqueda de reclutadores.

*Demonstrate Clean Code**:
Los snippets muestran un código conciso y listo para la producción: a algunos reclutadores les encanta.

*Experiencia Cross‐Language Mastery**:
Proporcionar soluciones en múltiples idiomas indica versatilidad.

- **Discuss Edge Cases & Complexity**:
Los entrevistadores valoran a los candidatos que piensan en el rendimiento y las trampas.

- **Agregar una llamada a la acción**:
Invitar a los reclutadores a probar su código en LeetCode o su repositorio GitHub.

-...

Siguientes pasos para su viaje de entrevista

1. **Ejecute el código de LeetCode** – envíe, compruebe su tiempo de ejecución y estudie la discusión para más trucos.
2. **Crear un GitHub Gist** – pegar las tres soluciones, añadir el vínculo problema y mencionar el desafío.
3. **Blog About It** – publicar un artículo corto (como éste) en Medium o dev.to, etiqueta `#LeetCode`, `#interview`, `#coding`.
4. **Aplicación para Roles** – utilice el enlace del blog en su Enlace En perfil o résumé bajo “Proyectos” o “Escritura Técnica”.

-...

####  Final Takeaway

Contando los dígitos que dividen un número es un problema engañosamente simple LeetCode que te enseña:
- **Extracción digital** vía modulo/división.
*Invariante* y complejidad espacial*
- **Clean, lenguaje de codificación agnóstica**.

Al dominarlo, y compartir su solución en un blog bien estructurado, no sólo se dará esta pregunta sino que también elevará su marca personal como un ingeniero reflexivo y listo para entrevistas. Buena suerte, y que su código siempre compila!

-..