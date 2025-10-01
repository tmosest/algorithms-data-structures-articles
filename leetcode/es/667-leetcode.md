-...
Título: LeetCode 667. Hermoso acuerdo II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📌 LeetCode 667 – Hermoso Arreglo II
**Medium** – `constructArray(n, k)`

■ *Problema*
■ Dados dos números enteros `n` y `k` (1 ≤ k ■ n ≤ 104), construir una permutación de los primeros `n` números naturales, de tal manera que la matriz de diferencias absolutas entre elementos consecutivos contiene **exactamente `k' valores distintos**.
■ Devuelve cualquier permutación válida.

A continuación encontrará ** tres soluciones completas, listas para funcionar** – una en **Java**, una en **Python**, y una en **C+** – más un *blog‐style* que explica el algoritmo, sus pros y contras, y por qué es un gran patrón de entrevistas.

-...

### 📐 El "Aprendimiento hermoso" Greedy Idea

1. Necesitamos diferencias distintas. * *
La mayor diferencia posible en una permutación de 1...n es `n-1`.
Si queremos exactamente `k` diferencias distintas, podemos garantizarles mediante la construcción de un patrón que produce las diferencias `k, k-1, ... , 1` - que es `k` valores distintos.

2. ** Estrategia de construcción**
* Comenzar con los primeros números 'n-k-1' en orden ascendente – producirán diferencias de 1 solo, sin nuevos valores distintos.
* Para las posiciones restantes `k+1` nos *zig‐zag* entre los dos extremos del rango restante:
* lado bajo = `n-k` (el primer número no utilizado)
* high side = `n`,
* luego decrementar el lado alto, aumentar el lado bajo, etc.
* Este zig‐zag produce diferencias: `k, k-1, ... , 1` en ese orden - exactamente `k` valores distintos.

3. *Por qué funciona*
* La primera parte no crea nuevas diferencias más allá de " 1.
* La parte zig‐zag produce una secuencia estrictamente decreciente de las diferencias, cada nueva diferencia es menor que la anterior.
* Total distinct differences = `k`.
* Todos los números de 1...n se utilizan exactamente una vez – una permutación válida.

El algoritmo funciona en **O(n)** tiempo y utiliza **O(1)** espacio adicional (además del array de salida).

-...

## 🎯 Code Snippets

## Java

``java
importar java.util*;

Clase Solución {
int[] constructArray(int n, int k) {
int[] ans = nuevo int[n];
int idx = 0;

// 1. Prefijo con 1 ... No... 1
para (int v = 1; v)
ans[idx+] = v;
}

// 2. Parte Zig‐zag que produce diferencias k
para (int i = 0; i <= k; i++) {
(i % 2 == 0) { // incluso i → tomar desde el lado bajo
ans[idx+] = n - k + i / 2;
} otra { // odd i → tomar del lado alto
ans[idx+] = n - i / 2;
}
}
devolver los ans;
}

// -... Arnés de prueba simple (opcional)...
public static void main(String[] args) {
Solución s = nueva solución ();
System.out.println(Arrays.toString(s.constructArray(3, 1))); // [1, 2, 3]
System.out.println(Arrays.toString(s.constructArray(3, 2))); // [1, 3, 2]
}
}
`` `

## Python

``python
Solución de clase:
def construct Array(self, n: int, k: int) - ratio(int):
ans = []
Prefijo: 1 ... n-k- 1
ans.extend(range(1, n - k))

# Zig‐zag suffix
para i en rango(k + 1):
si i % 2 == 0:
ans.append(n - k + i // 2) # lado bajo
más:
as.append(n - i // 2)
Retorno

# -... Prueba...
si __name_ == "__main__":
s = Solución()
print(s.constructArray(3, 1)) # [1, 2, 3]
print(s.constructArray(3, 2)) # [1, 3, 2]
`` `

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector significado construirArray(int n, int k) {
vector significar uns
ans.reserve(n);

// Prefijo: 1 ... n-k- 1
para (int v = 1; v)
as.push_back(v);

// Zig‐zag suffix
para (int i = 0; i) = k; ++i) {}
si (i % 2 == 0) // incluso lado bajo
ans.push_back(n - k + i / 2);
más // odd - título lado alto
ans.push_back(n - i / 2);
}
devolver los ans;
}
};

int main() {}
Solución s;
vector implicado a = s.constructArray(3, 1);
para (int x : a) cout
cout se hizo 'n';
a = s.constructArray(3, 2);
para (int x : a) cout
}
`` `

-...

## 📚 Blog Artículo – “El Bien, el Mal, y el Ugly of Beautiful Arrangement II”

### 1. Título " Meta "

*Título*
*Aprendimiento hermoso II – Un paso a paso LeetCode 667 Solución (Java, Python, C++)

**Descripción de los datos**:
“¿Quieres ace LeetCode 667? Aprenda la codicioso 'zig‐zag' construcción para Hermoso Arreglo II. Soluciones completas Java, Python & C++, paso del algoritmo, casos de borde y consejos de entrevista. Perfecto para entrevistas de ingeniería de software. ”

### 2. Introducción

El problema *Beautiful Arrangement II* es un favorito entre los entrevistadores de algoritmos porque mezcla un clásico truco de permutación con un toque fresco en la diferencia-cuento. Si usted está buscando fortalecer su arsenal de entrevistas de codificación, este post le da:

* Un algoritmo codicioso (por qué funciona).
* ** Código fuente completo** en Java, Python y C++.
* Una profunda inmersión en **tiempo / complejidad espacial**.
* trampas comunes, manejo de los bordes, y consejos de entrevista en el mundo real.

¡Vamos a bucear!

### 3. Recaptación de problemas

- Entrada: " n " (tamaño de la permutación) y " k " (número deseado de diferencias distintas).
- Producto: Cualquier permutación de `1 ... n` donde el conjunto de diferencias absolutas entre elementos adyacentes contiene **exactamente `k` valores distintos**.

### 4. El Greedy Insight – “Zig‐Zag”

■ ¿Por qué zig‐zag? #
■ La mayor diferencia que podemos crear es `n-1`. Al alternar entre el menor número no utilizado y el mayor número no utilizado, podemos forzar la diferencia a reducir por 1 cada vez:
.

El patrón produce diferencias: `k, k-1, ... , 1`. Eso es 'k' números distintos - precisamente lo que el problema exige.

### 5. Construcción paso a paso

1. **Prefijo con números ascendentes**
Use los números `1` a `n-k-1`.
*¿Por qué?* Generan una única diferencia de `1`, sin introducir nuevas diferencias distintas.

2. **Zig‐zag the remaining `k+1` positions* *
``text
baja = n - k
alto = n
Resultado = []
para i = 0 ... k:
si estoy incluso: result.append(low + i/2)
más: result.append(high - i/2)
`` `
*La división de enteros " i/2 " maneja el paso alternado de “move inward”. *

3. *Combina*
El array final es la concatenación del prefijo y la parte zig‐zag.

### 6. Por qué el Algoritmo es correcto

*Todas las diferencias producidas por el prefijo son `1`. *
*La parte zig‐zag produce diferencias que disminuyen estrictamente de `k` a `1`. *
Por lo tanto, el conjunto de diferencias distintas es exactamente `{1, 2, ... , k}` – `k` valores distintos.

El algoritmo visita cada entero de `1` a `n` exactamente una vez, garantizando una permutación válida.

### 7. Análisis de la complejidad

TEN TERRITOR ANTE LAS ACTIVIDADES
...----------------------
Silencioso Prefix Silencioso `n-k-1` Silencio **O(n)**
Silencio Zig‐zag Silencioso Loop `k+1` Silencio **O(k)** (≤ O(n)) Silencio
Silencio total – Silencioso **Tiempo: O(n)** Silencio
TENIDO Espacio Extra TENIDO Conjunto de salida del tamaño `n` TEN **Espacio: O(1)** auxiliar (ignorando la salida) ANTE

La solución es óptima – no podemos vencer el tiempo lineal porque debemos tocar cada elemento al menos una vez.

### 8. Casos de borde " Errores comunes

Silencio Silencio Silencio Silencio
Silencio...
Silencio `k = n-1` (diferencias extremas) Silencio El bucle prefijo se vuelve vacío (`n-k-1` = 0). ← Código maneja esto con gracia; sólo comenzar zig‐zag desde el principio. Silencio
Silencio `n = 2`, `k = 1` Silencio El zig‐zag utiliza el patrón correctamente. Silencio Asegurar que los lazos del lazo sean `traducido= k`. Silencio
Silencio División de enteros erróneos ANTE Utilizar división flotante en lugar de división entero conduce a índices erróneos. TENIDO Use `i/2` en Java, `i // 2` en Python, `i / 2` en C++ (since `int` division truncates). Silencio
Silencio Mis-ordenamiento de los picos bajos/altos TENCIÓN Escoger ambos lados en la misma paridad puede saltar números. TENIDO A la regla “incluso → bajo, extraño → alto”. Silencio
Silencio Indices fuera de rango ← Subtracting too much from `high ' or adding too much to `low ' may exceed `[1, n]`. Silencio Verificar las fórmulas; test with random `n ' , `k`.

### 9. Consejos de entrevista

1. **Explicar la intuición primero** – a los entrevistadores les encanta ver *por qué* eliges un enfoque.
2. Cierra la permutación en papel. Escribe el prefijo y zig‐zag lado a lado; muestra las diferencias resultantes.
3. **Hablar de la complejidad** – decir “tiempo lineal, espacio extra constante”.
4. **Pregunte aclarando las preguntas** si el entrevistador es vago sobre `k` ser `0` (aunque las restricciones lo prohíben) o sobre el orden de las diferencias.
5. **Mostrar el código** en el idioma con el que estás más cómodo, pero estar listo para traducir a otro idioma en el lugar.

#### 10. Pensamientos finales

Hermoso arreglo II muestra un patrón poderoso: *utiliza un prefijo controlado para evitar trabajo extra, luego un zig‐zag deliberado para golpear exactamente los valores distintos necesarios*. Es un gran ejemplo de mezclar la construcción avaricia con el razonamiento combinatorio – perfecto para entrevistas de algoritmos.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀

-...

### 9. Conclusión

Ahora tienes:

* Tres soluciones de código de producción.
* Un algoritmo completamente documentado que es tanto **simple** como **optimal**.
* Un artículo del blog que es pulido para ** motores de búsqueda** y ** aprendizaje**.

Ya sea que se esté preparando para una entrevista de ingenieros de software senior, agudizando sus habilidades de entrevista, o simplemente buscando profundizar su comprensión de los trucos de permutación, el patrón de *Beautiful Arrangement II* es un conocimiento imprescindible. ¡Usadlo, explícamelo y mirad cómo impresionan a los entrevistadores!

-...

**P.S.** Pruebe pruebas aleatorias con `n` hasta `10^5` y confirme la diferencia distinta cuenta. Siéntete libre de extender el arnés de prueba en cualquier idioma – el algoritmo es suficientemente robusto y rápido para todas las restricciones.

Buena suerte, y feliz codificación!