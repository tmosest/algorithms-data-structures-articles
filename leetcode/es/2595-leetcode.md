-...
Título: LeetCode 2595. Número de bits de la noche -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Master LeetCode 2595 – “Número de Bites Incluso Y Odd”
*Aprenda a resolverlo en **Java, Python, y C++** y as a su próxima entrevista de ingeniería de software. *

-...

## Tabla de contenidos

TEN TERRITORIO TENIDO Enlace ANTE
Silencio...
Silencio 📝 Problema Declaración Silencioso Silencio
← Solución Resúmenes de la Solución
❌ Good, Bad, Ugly Silencio
Н 🔢 Bit‐Mask Approach ← #bit‐mask-approach Silencio
Silencio | Código Snippets Silencioso
← Complejidad Нели вени вени ны ный ные ных нери ный ный
Неливали Casos de borde " Pitfalls ные #pitfalls
Нени ️ Entrevista Consejos ный #interview-tips
Silencio 📚 Alternativas
Silencio 🎯 Resumen Silencio

■ **Palabras clave de SEO**: *LeetCode 2595, Número de bits, manipulación de bits, solución Java, solución Python, solución C++, codificación de entrevistas, entrevista de trabajo, ingeniero de software, bitmasking, popcount, consejos de entrevista de codificación*

-...

Declaración de problemas

■ **Given** un entero positivo `
■ **Retorno** un array `[even, odd]` Donde:
* `even` = number of **even‐indexed** bits (0‐based from the right) that are set to `1`
* `odd` = number of **odd‐indexed** bits that are set to `1`

**Los índices** se contabilizan desde el bit menos significativo (LSB) hasta el bit más significativo (MSB), comenzando por `0`.

*Examples*

TENIDO `n` ANTERITO Binario ANTERIENDO Even‐index 1s ANTE Odd‐index 1s ANTERIENDO ANTE
Silencio--------------------------------------------------------
TENIDO 50 TENIDO 110010 TENIDO 1 (Índice 4) TENIDO 2 (Índices 1,5) TENIDO `[1, 2] `` Silencio
TENIDO 2 TENIDO 10 TENIDO 0 TENIDO 1 (Índice 1) TENIDO `[0, 1]` Silencio

**Constraints* *

`` `
1 0 0 0 0 0 0
`` `

-...

## Solution Overview

TENIDO ANTERIOR ANTERIOR Idea ANTERIENTE Complejidad
Silencio----------------------------------------------------------
Silencio **Bit‐Mask > Popcount** Silencio Usar dos máscaras alternantes (`0b01010101...` < `0b101010...`) para aislar incluso y extraños bits, luego contar los bits de conjunto con una cuenta pop-count incorporada.  **O(1)** tiempo, **O(1)** espacio  durable Producción-grado, entrevista-friendly 
tención **Conversión de cuerdas** ¦ Convertir `n` a cadena binaria, iterate from LSB to MSB and increment counters based on index parity. Silencio **O(log n)** tiempo, **O(log n)** espacio
tención **Manual Bit Loop** Silencioso `n` derecha cada iteración, cheque LSB, paridad índice de cambio. Silencio **O(log n)** tiempo, **O(1)** espacio tención Educativa, si no se permite que los elementos incorporados vivieran

El método **Bit‐Mask & Popcount** es el método “bueno”: corto, eficiente y demuestra el dominio de la manipulación de bits.

-...

## ♥ Good, Bad, Ugly

TENIDO ESTADO TENIDO Qué hacer ANTERIOR Qué evitar
Silencio------------------------------------
Silencio **Bueno** Silencio Usa máscaras desgastadas + cuenta de popcon incorporada (por ejemplo, `Integer.bitCount`). Cualquier cosa que se agita sobre toda la cadena binaria a menos que tengas que hacerlo. Silencio
Silencio **Bad** Silencio Convertirse en cuerda al depurar, pero no en producción. Olvidar que los índices comienzan en `0`. Silencio
tención **Intensiblemente** Silencio Mantenga manualmente contadores y paridad de índice en un bloque 'si/else' que se enreda. tención Escribir una máscara de código duro largo como `0b010101010101010101` sin explicación. Silencio

-...

## 🔢 Bit‐Mask Approach

1. **Masks**
* Incluso índices (0, 2, 4, ...) → binario `01010101... `
* Índices extraños (1, 3, 5, ...) → binario `101010... `

En decimal:
* Incluso máscara = `0b010101010101` = `341` (para números de hasta 10 bits; puede generarlo programáticamente si quiere).
* Máscara extraña = `0b1010101010` = `682`.

2. **Aplicar al Conde**
* `even = popcount(n & evenMask)`
* `odd = popcount(n & oddMask)`

3. **Retorno** `[incluso, extraño] `

-...

## 📦 Code Snippets

## Java

``java
Clase Solución {
int[] evenOddBit(int n) {}
// Incluso índices: 0,2,4,... - titulado 0b0101010101010101 (341)
// Índices de riesgo: 1,3,5,... - título 0b101010101010 (682)
int evenMask = 0b0101010101010101010101; // 341
int oddMask = 0b1010101010101010; // 682
incluso = Integer.bitCount(n & evenMask);
int odd = Integer.bitCount(n & oddMask);
volver nuevo int[]{even, odd};
}
}
`` `

#### One‐liner (Java 17+)

``java
int[] evenOddBit(int n) {}
int[]{Integer.bitCount(n > 0b01010101010101010101), Integer.bitCount(n > 0b1010101010)};
}
`` `

-...

## Python

``python
Solución de clase:
def evenOddBit(self, n: int) - List[int]:
even_mask = 0b010101010101 # 341
odd_mask = 0b10101010 # 682
incluso = (n & even_mask).bit_count()
extraño = (n & odd_mask).bit_count()
Volver [even, odd]
`` `

#### One‐liner (Python 3.10+)

``python
Solución de clase:
def evenOddBit(self, n: int) - List[int]:
[n " 0b10101010101).bit_count(), (n " 0b010101010).bit_count()]
`` `

-...

### C++

``cpp
Clase Solución {
public:
vector significado inclusoOddBit(int n) {}
// Incluso indices máscara: 0b010101010101 (341)
// Indices extraños máscara: 0b1010101010 (682)
int evenMask = 0b01010101010101010101;
int oddMask = 0b101010101010;
int even = __constructionin_popcount(n & evenMask);
int odd = __ builtin_popcount(n & oddMask);
Regresar {incluso, impar}
}
};
`` `

#### One‐liner (C++14+)

``cpp
vector significado inclusoOddBit(int n) {}
retorno {__construido_popcount(n < 0b0101010101010101010101), __construidoin_popcount(n > 0b101010101010)};
}
`` `

-...

Complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
TENIDO Bit‐Mask + Popcount ANTE **O(1)** (continuado, independiente de `n`) Silencio **O(1)**
Silencio Conversión de cuerdas Silencioso **O(log n)** Silencio **O(log n)**
TENIDO ANTERIOR manual TENIDO **O(log n)** TEN **O(1)** TENIDO

Para " n " = 1000 " las diferencias son insignificantes, pero el enfoque bit-mask es *universalmente* óptimo.

-...

## ѕливали Casos de bordes " Pitfalls

Silencio Pitfall Silencio
Silencio...
tención Off‐por-uno índice cuando iterating a string ¦ Use `i % 2 == 0` para incluso, `i % 2 == 1` para extraño, contando desde LSB (índice reverso). Silencio
Silencio El tamaño de la máscara incorrecta Silencio Las máscaras deben cubrir todos los bits que pueden aparecer en `n`. Para los enteros de 32 bits, utilice `0x55555555 ' (even) & `0xAAAAAAA` (odd). Silencio
Silencio No utilizar el popcount integrado TEN Manual popcount es más lento y incorrecto. Silencio
TENIDO Asumiendo que `n` es cero ANTERIOR El problema garantiza `n не= 1`, pero si permite `0`, máscaras todavía funcionan (ambas cuentas serán `0`). Silencio

-...

Consejos de entrevista

1. **Explicar la lógica de bit-mask**: Mostrar que los índices incluso y extraños alternan; por lo tanto podemos crear una máscara que coincida con esas posiciones.
2. **Mostrar por qué la cuenta pop es eficiente**: Es tiempo acelerado y constante para tamaños de palabras fijos.
3. **Discuten las alternativas brevemente**: Conversión de cadenas de mención y bucle manual para demostrar minuciosidad, pero argumentan rápidamente por qué son suboptimales.
4. **Hablar sobre la escalabilidad**: Para `int` vs `long`, simplemente cambiar las constantes de la máscara (`0x5555555555`, `0xAAAAAAAAAA`).
5. **Tiempo de intercambio espacial**: Emphasize constant time & space, which is a hallmark of a good interview answer.

-...

## 📚 Alternativas (Si usted debe evitar incorporados)

### Manual Bit Counting

``java
int[] evenOddBit(int n) {}
int even = 0, odd = 0, idx = 0;
mientras (n!= 0) {
(n) == 1) {
(idx % 2 == 0) incluso++;
más extraño++;
}
n > 1;
idx++;
}
volver nuevo int[]{even, odd};
}
`` `

### String Conversion

``python
Def evenOddBit(n):
bits = bin(n)[2:][:-1] # LSB first
incluso = suma(1 para i, b en enumerado(bits) si i % 2 == 0 y b == '1')
odd = sum(1 for i, b in enumerate(bits) if i % 2 == 1 and b == '1')
Volver [even, odd]
`` `

Estos son excelentes para fines *educativos* o idiomas que carecen de cuenta pop.

-...

## 🎯 Summary

- El método **Bit‐Mask + Popcount** es el método más rápido, más conciso y muestra una profunda comprensión de las operaciones de bits.
- Para 'n י= 1000', cualquier solución pasa, pero los entrevistadores esperan el enfoque de tiempo constante.
- Máscaras como `0b010101010101` (`341`) para incluso y `0b101010101010` (`682`) para índices impares aisla los bits en una sola vez.
- Construidos ( " Integer.bitCount " , `_construidoin_popcount ' , `.bit_count() ' ) hacen del código una sola línea, ideal para entrevistas de codificación.

■ **Recuerda**: “Mostrar la máscara → aplicar → popcount → retorno.” Es todo lo que necesitas impresionar.

-...

## ⋅ Final Thought

Los problemas de manipulación de bits son un elemento básico de las entrevistas técnicas. Dominar esto no sólo le aterriza la matriz '[incluso, extraño]` en tiempo constante, sino que también le da un patrón reutilizable para una amplia gama de preguntas relacionadas con bits. ¡Feliz codificación!

-...

■ **¿Quieres más preparación para la entrevista?** Echa un vistazo a mis otros guías en *two-sum*, * bits reversos* y *cuenta bits*, todo optimizado para el éxito de la entrevista.