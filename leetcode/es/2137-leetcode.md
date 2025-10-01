-...
Título: LeetCode 2137. Verter agua entre cubos para hacer los niveles de agua iguales -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 Leetcode 2137 – Pour Water Between Buckets to Make Water Levels Equal
**Solución** – Búsqueda binaria (Java / Python / C++)
**Blog** – “El Bien, el Mal y el Ugly” – Guía de entrevista optimizada SEO

-...

### 1. Recaptación de problemas

Usted tiene `n` cubos con cantidades enteros de agua (`buckets[i]`).
Cuando viertes `k` galones de un cubo a otro, pierdes `pérdida' de ese vertido.

`` `
k → k * (loss/100) se derrama
k' = k * (1 - la pérdida/100) en realidad alcanza el balde objetivo
`` `

Usted puede verter *cualquier* cantidad (no necesariamente un entero) entre cualquier dos cubos.
Objetivo: **Haz que todos los cubos contengan la misma cantidad de agua y devuelve esa cantidad máxima posible. #

- 1 ≤ 10^5
- `0 ≤ cubos [i] ≤ 10^5`
- `0 ≤ pérdida ≤ 99`

Se aceptan respuestas en el apartado e 5) del valor real.



-...

## 2. Brute‐Force Intuition (Por qué es demasiado lento)

Una manera ingenua es probar cada nivel final posible (por ejemplo, enumerando todas las cantidades distintas del cubo) y simular vertederos.
Con `n = 10^5` que es imposible (`O(n^2)` en el peor de los casos.

En su lugar podemos preguntar: **Dado un nivel de destino `L`, ¿podemos alcanzarlo? #
Esto convierte el problema en un problema de decisión que puede resolverse en `O(n)`.

Entonces podemos realizar búsquedas binarias en `L` para encontrar el nivel máximo posible.
Esto da un algoritmo general `O(n log V)`, donde `V = 10^5` (el volumen máximo del cubo).

-...

## 3. Función de decisión

For a candidate level `L`:

`` `
necesidad = 0 // agua total que todavía necesita ser agregada a un cubo
dar = 0 // agua total que debe ser quitada de un cubo

por cada cantidad de cubo x:
si x ■ L: // cubo necesita agua
// para llevar x hasta L tenemos que ver (L - x) / (1 - pérdidaFraction)
necesidad += (L - x) / (1 - pérdidaFraction)
si x Ø L: // cubo tiene exceso de agua
dar += (x - L) // este agua será derramada
`` `

Si “necesitamos” = dar” (es decir, tenemos suficiente exceso para cubrir los vertederos necesarios después de contabilizar la pérdida), entonces el nivel " L " es alcanzable.
Queremos el *maximum* `L` que satisface esta condición.

-...

## 4. Búsqueda binaria

`` `
bajo = 0
alto = max(buckets) // límite superior; no puede exceder el máximo inicial
eps = 1e-6 // Requisitos de precisión

mientras alto - bajo eps
media = (bajo + alto) / 2
si es factible(medio):
baja = media // podemos ir más alto
más:
alta = media // demasiado alta, psiquiatra
Regreso bajo
`` `

La prueba de viabilidad utiliza la función de decisión anterior.

-...

## 5. Código - Java

``java
importar java.util*;

Solución de la clase pública {}
public double equalizeWater(int[] cubos, int loss) {
doble pérdidaFraction = pérdida / 100.0; // por ejemplo 80% → 0.80
eps dobles = 1e-6;

doble bajo = 0,0;
doble alto = Arrays.stream(buckets).max().getAsInt(); //

mientras (alto - bajo eps) {}
doble media = (bajo + alto) / 2.0;
si (canReach(buckets, mid, lossFraction)) {}
bajo = medio; // mediados es factible, tratar más alto
. ♫ ... {
alto = medio; // medio demasiado alto
}
}
Retorno bajo;
}

canReach(int[] cubos, doble nivel, doble pérdidaFraction) {
necesidad doble = 0,0; // agua que debe ser derramada
doble dar = 0,0; // agua que se derramará

para (int x : cubos) {}
si (x.
necesidad += (nivel - x) / (1.0 - pérdidaFraction);
} si (x > level) {
dar += (x - nivel);
}
}
// Necesitamos suficiente “dar” para cubrir la “necesidad” después de la pérdida
necesidad de retorno = dar + 1e-12; // pequeño epsilón para la seguridad numérica
}

public static void main(String[] args) {
Solución sol = nueva solución ();
System.out.println(sol.equalizeWater(new int[]{1, 2, 7}, 80)); // 2.0
System.out.println(sol.equalizeWater(new int[]{2, 4, 6}, 50)); // 3.5
System.out.println(sol.equalizeWater(new int[]{3, 3, 3, 3}, 40)); // 3.0
}
}
`` `

-...

## 6. Código - Python

``python
def equalizeWater(buckets: list[int], loss: int) flotante:
loss_frac = pérdida / 100.0
eps = 1e-6
bajo, alto = 0,0, max(buckets)

def factible(nivel: flotante) Bool:
necesidad = 0,0
dar = 0,0
para x en cubos:
si x < nivel:
necesidad += (nivel - x) / (1.0 - loss_frac)
elif x √nivel:
dar += (x - nivel)
necesidad de devolución

mientras alto - bajo eps
media = (bajo + alto) / 2.0
si es factible(medio):
baja = media
más:
alta = media
Regreso bajo


si __name_ == "__main__":
print(equalizeWater([1, 2, 7], 80)) # 2.0
print(equalizeWater([2, 4, 6], 50)) # 3.5
print(equalizeWater([3, 3, 3, 3], 40) # 3.0
`` `

-...

## 7. Código: C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
doble ecualizarWater(vector asignadoint círculos, int loss) {
doble pérdidaFrac = pérdida / 100.0;
eps dobles = 1e-6;
doble bajo = 0,0;
doble alto = *max_element(buckets.begin(), cucharas.end());

auto factible = [ cl](nivel doble) - bool
necesidad doble = 0,0, dar = 0,0;
para (int x : cubos) {}
si (x)
necesidad += (nivel - x) / (1.0 - lossFrac);
si (x √nivel)
dar += (x - nivel);
}
la necesidad de retorno = dar + 1e-12;
};

mientras (alto - bajo eps) {}
doble media = (bajo + alto) / 2.0;
si (feasible(mid))
baja = media;
más
alto = medio;
}
Retorno bajo;
}
};

int main() {}
Sol de solución;
cout ' se hizo fijo " se realizó la determinación(5);
cout se realizó el sol.equalizeWater({1,2,7}, 80)
cout se realizó el sol.equalizeWater({2,4,6}, 50)
cout se realizó el sol.equalizeWater({3,3,3,3}, 40)
}
`` `

-...

## 8. Artículo del Blog – “El Bien, el Mal y el Ugly”

■ *Título*
■ **Leetcode 2137 – Pour Water Between Buckets to Make Water Levels Equal**
*Una profunda inmersión en la búsqueda binaria, Edge‐Case Mastery, y éxito de la entrevista*

-...

### 8.1 ¿Por qué este problema se mete para las entrevistas

Por qué importa
Silencio...
Silencioso ** razonamiento cuantitativo** Silencio Se le pide razonar sobre la pérdida y transferencia, un rompecabezas de matemáticas sutil. Silencio
Silencio **Binary search** Silencio Una técnica algorítmica básica; los empleadores quieren verlo utilizar en espacios continuos. Silencio
Silencio **Precisión de punto flotante** Silencioso codificación del mundo real requiere un manejo cuidadoso de `doble`/`float`. Silencio
Silencio **Edge-case hunting** Silencio Las restricciones (perder 0‐99, grandes arrays) prueban robustez. Silencio
Silencio **Optimization** Silencio O(n log V) es el lugar dulce para los puntos de datos 10^5. Silencio

■ **Palabras clave de SEO**: Leetcode 2137, problema de cubo de agua, entrevista de búsqueda binaria, soluciones de entrevista de Java, codificación de entrevistas de Python, algoritmo de entrevista de C++, prep de entrevista de ingeniero de software, solución de problemas algorítmicos, transferencia de pérdida de porcentaje, codificación de entrevistas de trabajo, preguntas de entrevista de algoritmo.

-...

### 8.2 Problema de ruptura

1. **Understand the pour rule**
Al verter `k` galones, sólo `(1 - pérdida%) * k` llega.
*Pérdida 80% → Usted obtiene efectivamente 20% del volumen derramado. *

2. ** Objetivo**
Encontrar el nivel de agua corriente ** máximo** alcanzable por vertidos repetidos.

3. **Observaciones**
- El nivel final nunca puede superar el cubo inicial máximo.
- Para cualquier nivel de candidatos `L`, el total “necesario” para llenar cubos cortos puede ser calculado.
- El total “dar” de los cubos desbordados es sólo la suma de `(x - L)` para `x  Conf L`.
- Después de la pérdida, la cantidad *eficaz* derramada de los cubos desbordadores debe cubrir la necesidad.

-...

### 8.3 La función de la decisión – El bien

**Por qué funciona* *
- Reduce un problema continuo a un simple cheque lineal.
- O(n) tiempo por cheque, no hay estructuras de datos adicionales.
- Manijas punto flotante con un pequeño epsilón para evitar errores de redondeo.

**Implementation Highlights* *
- `neced` utiliza la división por `(1 - la pérdidaFraction)` porque esa es la inversa de la eficiencia de transferencia.
- 'Give' es una sutracción directa.
- La prueba de viabilidad `necesitar <= dar` captura directamente la condición de viabilidad.

-...

### 8.4 Búsqueda binaria – El "Bad"

Silencio potencial Pitfall Silencio
Silencio...
Silencio **Pérdida de precisión** Silencio Usar un pequeño `eps` (1e-6 o 1e-7) y `doble`/`long double`. Silencio
Silencio **Overflow of sum** Silencio Todas las sumas caben en `doble` porque suma máxima ♥ 10^5 * 10^5 = 10^10, seguro dentro de la mantissa de 53 bits de doble. Silencio
Silencio **El bucle infinito** Silencio Asegurar `mid` es recalculado cada iteración y parar cuando `alta - bajo ♪ = eps`.

*Por qué es “malo”*
La búsqueda binaria en números flotantes puede ser mentalmente confusa. En entrevistas, usted necesita justificar claramente los límites y el criterio de parada; de lo contrario el entrevistador podría sospechar un error sutil.

-...

### 8.5 The “Ugly” – Numerical Stability & Edge Cases

1. **Zero loss (loss = 0)* *
La cantidad efectiva derramada equivale a la cantidad derramada.
La función de decisión sigue funcionando: `1 - lossFraction = 1.0`.

2. Pérdida: 99%**
La eficiencia es " 0,01 " , dividiendo por " (1 - 0.99) " → " 100 " .
La precisión sigue siendo segura, pero ten cuidado de que la `1 - pérdidaFraction` sea extremadamente pequeña. Un cheque por `pérdida == 100' causaría división por cero, pero las restricciones se detienen en el 99%.

3. *Todos los cubos son iguales*
La viabilidad siempre sostiene; la búsqueda binaria convergerá rápidamente.

4. **Large arrays**
El algoritmo sigue siendo rápido; no hay bucles anidados.

-...

### 8.6 Cómo hacerlo en una entrevista en vivo

1. **Leer la pregunta cuidadosamente** – confirmar que usted entiende “sólo X% llega”.
2. **Explicar el algoritmo** antes de codificación.
3. **Mostrar la función de decisión** – caminar a través de un pequeño ejemplo manualmente.
4. **Precisión de la mención** – discutir por qué usas `eps`.
5. **Code con claridad** – evitar sobre-complicar; escribir bucles legibles.
6. **Test edge cases**:
- `[0, 100000]`, loss=0 → final=100000.
- `[1, 2, 3]`, loss=99 → final de la cúpula0.01 * ¿algo? (Mostrar resultado).
- Gran matriz aleatoria con pérdida=50.

-...

### 8.7 Takeaway for Your Coding Journey

- **La búsqueda interna no es sólo para los arrays** – funciona para los rangos continuos también.
- ** Las funciones de decisión son oro** – te permiten convertir “encontrar lo mejor” a “es esto factible?”.
- Cuidados de punto flotante** - Siempre anticipar el redondeo.
- **Siempre explica** – Un claro avance verbal impresiona a los gerentes de contratación mucho más que un perfecto pero poco legible.

-...

### 8.8 Veredicto Final

- **Bueno**: La comprobación de viabilidad lineal – simple, rápido, matemáticamente elegante.
- **Bad**: El bucle de búsqueda binaria - precisión, pero manejable.
- **Ugly**: Gestionar el punto flotante y asegurar la terminación – el “gotcha” habitual en la codificación de entrevistas.

■ Resultado**
■ Dominar este problema demuestra un pensamiento algoritmo fuerte, un obstáculo para la precisión numérica, y la confianza para enfrentar desafíos continuos en el espacio – todas las habilidades que las empresas de tecnología buscan activamente.

¡Feliz codificación y buena suerte en la próxima entrevista!

-...

## 9. Observaciones finales

Este problema es un **tour de force**: una mezcla de matemáticas inspiradas por la física, búsqueda binaria continua, y manejo cuidadoso de punto flotante.
Las soluciones proporcionadas Java, Python y C++ funcionan cómodamente bajo el límite de datos 105 mientras cumplen con el requisito de precisión 1 e-6.

Para la próxima entrevista, la práctica explicando la función **decisión** paso a paso, mostrar la lógica de búsqueda binaria en papel, y estar listo para discutir el manejo del borde por caso.
Su capacidad para convertir una regla del mundo real aparentemente desordenada en un algoritmo elegante es exactamente lo que buscan los reclutadores.

Buena suerte aterrizando ese papel de ingeniero de software! 🚀

-..