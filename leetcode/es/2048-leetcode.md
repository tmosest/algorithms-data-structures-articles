-...
Título: LeetCode 2048. Siguiente Mayor Número numérico equilibrado -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recaptación de problemas

**LeetCode 2048 – Next Greater Número numérico equilibrado**

■ Un integer `x` es **numerically balance** si por cada dígito `d` en `x`, el dígito `d` ocurre **exactamente `d` veces**.
■ Dado un entero `n (0 ≤ n ≤ 106)`, devolver el menor número numérico equilibrado estrictamente mayor que `n`.

Ejemplos

Silencio
Silencio...
Silencio
Silenciosos 1000 Silencio 1333
Silencio . . . Silencio Silencio

La tarea es una pregunta de estilo clásico de entrevista que prueba su capacidad de pensar combinatorialmente, prune un espacio de búsqueda, y escribir código limpio en varios idiomas.



----------------------------------------------------

## 2. Why the Backtracking / Pre-computation Approach Works

1. **Los dígitos son limitados* *
- La mayor respuesta posible para las limitaciones tiene en la mayoría de **7 dígitos** (por ejemplo, `7666666`).
- El dígito `d` puede aparecer en la mayoría de 'd' tiempos, por lo que el número máximo de dígitos diferentes que puede utilizar es `6` (1–6).
- Eso mantiene el espacio estatal pequeño.

2. **La propiedad “balanceada” es local* *
- Sólo necesitas saber cuántas veces se ha colocado cada dígito.
- Usted puede decidir si colocar un dígito 'i' basado en 'contra[i] i' y si todavía tiene suficientes "posposiciones que quedan" para terminar el número.

3. **Pre-computar una vez es más barato que comprobar un número a la vez* *
- Construir ** cada número numéricamente equilibrado hasta 7 dígitos.
- Guardarlos ordenados.
- Responde cualquier consulta por una búsqueda binaria (`O(log M)` donde `M` es el número total de números equilibrados - sólo unos pocos cientos).

La compensación es una pequeña cantidad de trabajo frontal que produce una solución limpia y reutilizable.



----------------------------------------------------

## 3. El Algoritmo (High‐Level)

`` `
1. Pre-computa todos los números numéricamente equilibrados con 1 ... 7 dígitos
a. Recursively build the number digit by digit.
b. Mantenga un array `cnt[10]` - cuántas veces se ha utilizado cada dígito.
c. Deténgase cuando el prefijo construido es √ n y todos los dígitos satisfagan `cnt[d] == d` o `cnt[d] == 0`.
d. Empuja el número válido a una lista.

2. Ordenar la lista de números válidos.

3. Para responder a una consulta n:
a. Búsqueda binaria del primer elemento > n.
b. Devuelve ese elemento.
`` `

**Por qué funciona la recursión* *
Porque cada llamada recursiva elige un solo dígito para anexar. La profundidad es a la mayoría de 7, por lo que la recursión es perfectamente segura.



----------------------------------------------------

## 4. Aplicación del Código

A continuación se encuentran soluciones limpias y de producción en **Java, Python y C++**.
Cada idioma sigue la misma lógica pero utiliza características idiomáticas.

■ **Consejo:** Si se está preparando para una entrevista de codificación, copiar el fragmento que coincida con el idioma que utilizará. Todos ellos son pre-computación de `O(M)`, `O(log M)` consultas, y funcionan bien bajo 1 ms para los límites dados.



#### 4.1 Java

``java
importar java.util*;

Solución de la clase pública {}

--------- Public API...--------
public int nextBeautiful Número(int n) {
// Iniciación perezosa – la primera llamada construye la lista
(balancedNumbers.isEmpty()) buildBalancedNumbers();
// Búsqueda binaria para el primer
int idx = Collections.binarySearch(balancedNumbers, n + 1);
idx = -idx - 1; // punto de inserción
retorno balanceadoNumbers.get(idx);
}

--------- Ayudantes privados --------
Lista final estática privada realizadaInteger confianza balanceadoNúmeros = nuevo ArrayList fiel();

construcción de vacío privadoBalancedNumbers() {}
int[] cnt = nuevo int[10];
backtrack(0, 0, cnt);
Collections.sort(balancedNumbers);
}

retroceso privado vacío (en prefijo, int len, int[] cnt) {
si (len √≥ 0 ' pc esBalanced(cnt)) {}
balanceadoNumbers.add(prefijo);
}
si 7) retorno; // máx 7 dígitos
para (int d = 1; d) = 6; d+) { // dígitos 1..6 solamente
si (cnt[d] == d) continúa; // no puede utilizar más de este dígito
// Prune: posiciones restantes se necesita para terminar este dígito
int remaining = 7 - len;
si (que se mantiene) (d - cnt[d])) continúan;
cnt[d]+;
backtrack(prefix * 10 + d, len + 1, cnt);
cnt[d]...
}
}

booleano privado esBalanced(int[] cnt) {
para (int d = 1; d)
si (cnt[d]!= 0 " clnt[d] != d) devolver false;
}
retorno verdadero;
}
}
`` `

■ *La complejidad*
*Pre-computación*: `O(1)` (la lista tiene 300 elementos).
■ * Pregunta*: `O(log M)` (búsqueda obligatoria).
■ * Memoria*: `O(M)`.



#### 4.2 Python

``python
de la importación de bisect_right
desde functools import lru_cache
de la importación Lista

Solución de clase:
# Pre-compute once
_balanced: List[int] = []

def __init__(self):
si no Solución._balanced:
Solución._balanced = self._build_balanced()

def nextBeautifulNumber(self, n: int) - int:
idx = bisect_right(Solution._balanced, n)
Solución de retorno._balanced[idx]

def _build_balanced(self) - título List[int]:
res = []
cnt = [0] * 10

def dfs(prefix: int, length: int):
si longitud 0 y auto._is_balanced(cnt):
re.append(prefijo)
si la longitud == 7: # max 7 digitos
Regreso
para d en rango(1, 7):
si cnt[d] == d: # no puede usar más dígitos d
continuar
# restante ranuras
rem = 7 - longitud
si rem se hizo (d - cnt[d]):
continuar
cnt[d] += 1
dfs(prefijo * 10 + d, longitud + 1)
cnt[d] -= 1

dfs(0, 0)
res.sort()
retorno

@staticmethod
def _is_balanced(cnt: List[int]) - confianza bool:
devolver todo(cnt[d] == 0 o cnt[d] == d para d en rango(1, 7)
`` `

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
ent nextBeautiful Número(int n) {
(balanced.empty()) build();
auto = superior_bound(balanced.begin(), balance.end(), n);
Regresar *it;
}

privado:
vector estático significante equilibrado;

construcción estática de vacío() {}
int cnt[10] = {0};
función recomendadavoid(int,int) título dfs = [ cl](int prefix, int len) {
si (len √≥ 0 ' pc esBalanced(cnt))
balanceado.push_back(prefijo);
si 7) retorno; // 7 dígitos max
para (int d = 1; d)
si (cnt[d] == d) continúan;
int rem = 7 - len;
si (rem " Sec " (d - cnt[d])) continúan;
++cnt[d];
dfs(prefix * 10 + d, len + 1);
- cnt[d];
}
};
dfs(0, 0);
(balanced.begin(), balanced.end());
}

bool estático esBalanced(const int cnt[]) {}
para (int d = 1; d)
si (cnt[d] " clnt[d]!= d) devolver falso;
retorno verdadero;
}
};

vector Solución::balanced; // definición del miembro estático
`` `

----------------------------------------------------

## 5. La desintegración “buena – mala”

¿Qué es lo bueno que puede sentirse mal?
Silencio----------------------------------------...
Silencio **La complejidad del tiempo** Silencioso `O(log M)` por consulta (prácticamente instantánea). Silencio *None* – el algoritmo es óptimo para las limitaciones.
Silencio **Memory‐footprint** Silencio Muy bajo – sólo unos cientos de enteros almacenados. *None* – la misma razón.
Silencio **Readability** Silencio Limpieza de preocupaciones, búsqueda binaria, recursión. Silencio Algunos entrevistadores no les gusta el estado estático global. La lista estática es un truco común de entrevista (init perezoso). Silencio
Silencio **Edge-cases** Silencio Handles `n = 106` → `7666666`. Silencio Ninguno - la lista pre-computada cubre todos los casos. ← Pre-computación garantiza la corrección. Silencio
Silencio **Mantenibilidad** Silencio Un lugar (`compild()`) para cambiar la lógica si los límites del dígito cambian. ← Requiere que recuerdes la lista estática debe ser reconstruida si las restricciones crecen. La profundidad de recursión es pequeña, por lo que es segura. Silencio
Silencio **Testing** Silencio Fácil de probar imprimiendo la lista `balanced`. Silencio Mismo. Silencio La lista contiene todos los números equilibrados de 1 a 7 dígitos – usted puede afirmar en su contra. Silencio

■ **Bottom line:** El algoritmo es **fast, robusto y muy fácil de entrevista**. No hay una complejidad oculta “muy”, sólo un puñado de optimizaciones que mantienen la recursión trivial.



----------------------------------------------------

## 6. Pruebas de la unidad de muestra (Java)

``java
TestSolution de la clase pública {}
public static void main(String[] args) {
Solución s = nueva solución ();
asever s.nextBeautifulNumber(1) == 22;
afirma s.nextBeautifulNumber(1000) == 1333;
s.nextBeautifulNumber(3000) == 3133;
asever s.nextBeautifulNumber(10) == 22;
asever s.nextBeautifulNumber(0) == 22;
afirma s.nextBeautifulNumber(76665) == 76666;
System.out.println("Todas las pruebas pasaron!");
}
}
`` `

Siéntase libre de copiar la prueba en su IDE – las afirmaciones fallarán en voz alta si algo sale mal.



----------------------------------------------------

## 7. Pensamientos Finales – Cómo utilizar esto en su próxima entrevista

* **Conoce las limitaciones** – límite de 7 dígitos es la observación clave.
* **Explicar las reglas de poda** – 'cnt[d]  SegÃ3 d` y "remanente de las tragamonedas нереннных necesitados".
* **Mostrar su pre-computación** – demuestra que puede optimizar en múltiples casos de prueba.
* ** Periferias de mención** – cero, el límite superior `106`, y el menor número equilibrado (`22`).
* **Bring the code in the language of choice** – copy‐paste the snippet, run, and be ready to discuss the logic on a whiteboard.

Impresionará a los entrevistadores con una solución que no sólo es correcta sino también eficiente, escalable y fácil de mantener.



----------------------------------------------------

## 8. Tome el siguiente paso

Si usted está buscando un **Ingeniero de software** papel que valora algoritmos limpios, retroceder y resolver problemas, las técnicas anteriores son exactamente lo que los gerentes de contratación buscan.

- Máster en el patrón del siguiente número numérico mayor**.
- 🚀 Use los fragmentos proporcionados en **Java, Python, o C++**.
- 🧪 Prueba contra casos de borde antes de tu próxima entrevista.

■ ¿Listo para conseguir tu trabajo de ensueño? * *
■ Alcanzar, aplicar y traer estas soluciones de entrevista a la mesa. ¡Tu equipo futuro te lo agradecerá!

¡Feliz codificación!