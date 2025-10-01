-...
Título: LeetCode 519. Matriz Flip aleatoria -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🧩 519. Matriz de Flip aleatoria – Implementación de Full-Stack (Java Silencio Python Silencio C++)

A continuación encontrará una solución **ready‐to-copy** para cada idioma que LeetCode soporta, más un **step‐by-step blog** que recorre las partes “buenas”, “bad”, y “muy” de este problema clásico de entrevista.
Siéntete libre de meter los francotiradores en tu IDE, haz las pruebas proporcionadas, o pegarlos directamente al editor LeetCode.

-...

## 👨 💻 Code – Fast, Memory‐Efficient, and Random‐Proof

■ **Key Idea** – Map a *virtual* índice lineal al índice de matriz real.
■ Cada `flip` dibuja un número aleatorio `k ' en `[0, restante a 1] ' .
■ Si ese índice ya ha sido volteado almacenamos un *swap* en un mapa de hash.
■ Esto convierte el problema en un simple truco de “reservoir sampling” con `O(1)` tiempo y `O(#flips)` espacio.

Silencio Idioma Silencio Código Silencio
Silencio...
Silencio **Java** Silencioso Ver Java / resumen titulado ``java
importar java.util*;

Clase Solución {
privada final int m, n;
int privado restante; // células que todavía son 0
mapa final privado realizadoInteger, mapa Integer confianza; // virtual - cartografía real
final privado Random rand;

solución pública(int m, int n) {
esto.m = m;
esto.n = n;
esto. restantes = m * n;
este.map = nuevo HashMap incorrecto();
este.rand = nuevo Random();
}

* @return [row, col] of a flipped cell */
int[] flip() {}
int r = rand.next Int(remanente); // elegir una célula libre al azar
// el índice real puede haber sido cambiado antes
int real = map.getOrDefault(r, r);

// elegir la última celda gratis para llenar el agujero izquierda por r
int last = remaining - 1;
int lastReal = map.getOrDefault(última, última);

// mapa r a último Real (así que la próxima vez r dará el últimoReal)
map.put(r, lastReal);
// ya no necesitamos último en la piscina
si (r == último) map.remove(r);

restante; // una celda menos libre
volver nuevo int[]{real / n, real % n};
}

public void reset() {}
map.clear();
restantes = m * n;
}
}
`` ' escrito/detalles titulado Silencio
tención **Python** ANTERIEDO DEtalles Ver Python realizado/summary ````python
importación al azar
de la importación Lista

Solución de clase:
def __init_(self, m: int, n: int):
self.m, self.n = m, n
self.rem = m * n # rest ceros
self.mapping = {} # virtual - Conf Índice real

def flip(self) - título List[int]:
r = random.randint(0, self.rem - 1)
real = self.mapping.get(r, r)

último = auto.rem - 1
last_real = self.mapping.get(last, last)

# map the chosen index to the last free cell
self.mapping[r] = last_real
si r == último:
self.mapping.pop(r, None)

self.rem -= 1
volver [real // self.n, real % self.n]

def reset(self) - título Ninguno.
self.mapping.clear()
self.rem = self.m * self.n
`` ' escrito/detalles titulado Silencio
tención **C+** Silencioso Ver C+++Se realizó/summary titulada```cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
int m, n, remaining;
unordered_map madeint,int confianza mp; // virtual cartografía real
mt19937 rng; // motor aleatorio moderno

public:
Solución(int m, int n) : m(m), n(n), remaining(m*n) {}
rng.seed(random_device{}());
}

vector asignador() {}
uniform_int_distribución efectuadaint título dist(0, remaining - 1);
int r = dist(rng); // elegir una célula virtual gratuita
int real = mp.count(r) ? mp[r] : r; // traducir a índice real

int last = remaining - 1;
int lastReal = mp.count(last) ? mp[last] : último;

// llenar el agujero dejado por r con la última célula libre
mp[r] = lastReal;
si (r == último) mp.erase(r);

- seguir existiendo;
devolver { real / n, real % n };
}

vaciado() {}
mp.clear();
restantes = m * n;
}
};
`` ' escrito/detalles titulado Silencio

■ *Por qué funciona* *
■ 1. Cada llamada dibuja un número aleatorio de la piscina *current* de células libres.
■ 2. Mantenemos una bijeción entre los índices virtuales `[0, restantes-1]` y los índices reales `[0, m*n-1]`.
■ 3. Después de voltear, reemplazamos el índice usado por el último libre, asegurando que los sorteos futuros nunca vuelvan a ver el mismo índice.
■ 4. `reset()` simplemente aclara el mapa y restaura el tamaño original de la piscina.

-...

## 📚 Blog Article – “The Good, The Bad, and The Ugly of LeetCode 519”

■ **Audiencia de emergencia:** Ingenieros de avanzada / back-end, entusiastas de la estructura de datos, y cualquiera que se prepare para entrevistas de algoritmos.
■ **SEO Palabras clave: *LeetCode 519*, *Random Flip Matrix*, *Preguntas de entrevista de Java*, *Problemas de entrevista de Python*, *C+++ algoritmos de entrevista*, *O(1) flip matriz*, *diseño de algoritmo*, *consejos de entrevista de codificación*.

-...

### Title
**El Bien, el Mal, y el Ugly de LeetCode 519: Mastering Random Flip Matrix en Java, Pitón, C++* *

#### TL;DR
- **Bueno**: Tiempo lineal, memoria O(#flips), sin rejilla extra, acceso aleatorio a tiempo constante.
- **Bad**: Los enfoques ingenuos son el espacio *(m*n)* y *(m*n)* por voltereta – inescalable.
- **Ugly**: El mal manejo de la semilla al azar o el intercambio de lógica conduce a errores sutiles y sesgo en el azar.

-...

##### 1. Panorama general de los problemas

■ *Se le da una matriz binaria `m × n` inicialmente llena de ceros.
■ Cada llamada a `flip()` debe devolver un índice uniformemente aleatorio `(i, j)` donde la célula es `0`, voltear esa célula a `1`, y garantizar que cada `0` restante tiene la misma posibilidad de ser seleccionado.
■ La operación "reset()` restaura la matriz a todos los ceros. *

Las restricciones son generosas (`m, n ≤ 104`), pero sólo hasta **1000** operaciones `flip`/`reset`. Por lo tanto necesitamos un algoritmo que funciona bien incluso para matrices masivas.

-...

##### 2. The Naive (Bad) Approach

Silencio Silencio Silencio Silencio Silencio Silencio
Silencio--------------------
tención 2‐D array + lista de celdas libres tención Almacena toda la matriz – imposible para 108 células. Silencio
Silencio El escaneo aleatorio hasta que se encuentre una célula libre Silencioso `O(m*n)` por flip Silencio `O(m*n)` Silencio Incluso con pequeño `k`, cada voltereta puede bucle miles de veces. Silencio

La ingenua solución **fails** porque viola las limitaciones de la entrevista:
- Necesitarías mantener una matriz o lista de *todo* célula para garantizar la uniformidad, soplando la memoria.
- Reescanear la matriz para cada voltereta se convierte en un cuello de botella de rendimiento.

■ **¿Por qué es malo? #
■ La complejidad del algoritmo es una función del tamaño de la rejilla *entire*, no el trabajo real* que estás haciendo.
■ Para una matriz 104 × 104 que significaría almacenar 108 ints – simplemente imposible en la mayoría de las máquinas de entrevista.

-...

##### 3. El elegante (bueno) Mapa‐Swap Trick

1. *Flatten the Matrix*
Trate de la matriz 2-D como una matriz 1-D de longitud `N = m * n`.
Un índice lineal `x` mapas a `(x / n, x % n)`.

2. **Mantenga un mostrador “Remanente”**
`mantener = N` inicialmente.
Cada voltereta reduce `mantenerse' por uno.

3. **Use un mapa de Hash para intercambiar*
``text
virtual_index ↔ real_index
`` `
*Cuando se utiliza un índice virtual, lo mapeamos a la última célula gratuita, luego “remove” esa célula de la piscina. *

4. **La elección del brazo**
Pick `k` uniformly in `[0, remaining-1]`.
Traducir `k` a un índice real usando el mapa (`k` puede haber sido cambiado antes).
Swap `k` with `remaining-1` (the last free cell).

5. **Regresar las coordenadas 2-D* *
`row = real / n`, `col = real % n`.

*Por qué es bueno*
- **O(1)** per `flip`/`reset`.
- **O(k)** memoria donde `k` es el número de volteretas (≤ 1000).
- No hay necesidad de almacenar toda la matriz.
- El azar es *sin prejuicio* porque cada sorteo es de un subconjunto uniformemente aleatorio de las células libres actuales.

■ **Pseudocode (estilo pitón)* *
.
> r = random.randint(0, remaining-1)
> real = mapping.get(r, r)
Ø último = restante 1
(último, último)
cartografía[r] = últimoReal
Ø restantes -= 1
[real // n, real % n]
" `

-...

#### 3.1. Sutil Pitfalls “Ugly”

← Infierno en la vida
Silencio...
Silencio **Incorrect swap when `r == last`** Silencio El mapa todavía contiene una clave que ya no existe en la piscina, rompiendo futuros sorteos. tención Retire la llave (`mapping.pop(r, None)`) cuando `r == last`.
Silencio **Using `randint` with inclusive bounds** Silencio Off‐por-one error: `randint(0, remaining)` elige un índice fuera de la piscina. TENIDO Utilizar `randint(0, remaining-1)` o `nextInt(remanente)`. Silencio
tención **Seed mis-management** Silencio Diferentes carreras producen la misma secuencia, haciendo que la solución parezca determinista. Use una semilla *fresh* (`mt19937` + `random_device` en C++, `Random()` en Java, RNG predeterminado en Python. Silencio
TEN ** Collisions hash in high-level languages** TENS Rare, but can degrade performance. TEN Use `unordered_map` (C++), `HashMap` (Java), o Python’s dict – all are amortized O(1). Silencio

-...

##### 3. 3. Aplicación práctica

Los fragmentos de código en la sección anterior ya encarnan la solución **buena**.
A continuación se **completo, comentado** snippets para cada idioma – dejarlos directamente en LeetCode.

■ **Consejo:** En Python, evite `numpy` o cualquier biblioteca pesada.
■ En C++ use `mt19937` en lugar de la `rand() deprecatada para una mejor uniformidad.

-...

##### 4. Análisis de la complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio `flip()` Silencio **O(1)** (expected)
TENIENDO `reset()` Silencio **O(1)** – despeja el mapa
Silencio total para `k` flips Silencio **O(k)** Silencio **O(k)** (k ≤ 1000)

■ **Mimory Footprint* *
■ A la mayoría de los 1000 enteros en el mapa de hash → 0 10 KB incluso en Java (32-bit int).
■ Más ligero que almacenar toda la matriz (hasta 400 MB para 108 células).

-...

##### 5. Why Randomness Matters in Interviews

- **Uniformity**: Los entrevistadores esperan que usted proporcione una selección aleatoria verdaderamente uniforme.
- **Bias**: Incluso una sola asignación errónea puede hacer perder probabilidades.
- **Reproducibilidad**: Algunas plataformas de entrevista ejecutarán su solución en la misma entrada varias veces. Asegúrese de que su generador aleatorio no use una semilla fija a menos que se requiera explícitamente.

-...

##### 6. Consejos de práctica

1. *Desactiva tus propias pruebas*
``python
s = Solución(10000, 10000)
para _ en rango(1000):
r = s.flip()
s.reset()
`` `
Verifique que `reset()` restaura el tamaño de la piscina.

2. *Ver la uniformidad*
Simular 1 000 000 volteretas en una pequeña matriz (`m=2, n=2`) y contar la distribución de salidas. El histograma debe ser plano.

3. ** Casos de emergencia**
- `flip()` llamado cuando la matriz está llena ( ' permanecer == 0`) - debe lanzar una excepción o manejar con gracia.
- `reset()` llamado repetidamente - siempre debe limpiar el mapa.

4. **Entrevista de puntos**
- Explicar la idea de mapeo “virtual → real”.
- Mención ** muestreo de reserva** como analogía conceptual.
- Destacar los cambios entre el espacio/tiempo y el método ingenuo.

-...

##### 7. Conclusión – Usted está listo para As the Interview

- **Bueno**: O(1) por operación, memoria mínima, uso elegante de un mapa de hash.
- **Bad**: Tocar toda la cuadrícula es un error *deadly* en una matriz grande.
- **Ugly**: Omitir casos de borde clave (como cambiar el mismo índice) producirá resultados parciales o incorrectos, a menudo sin darse cuenta hasta que un caso de prueba falle.

Deje este código en su repositorio, agregue una breve descripción del algoritmo en su README, y tendrá una referencia **job‐ready** para futuras entrevistas.

¡Feliz codificación! 🚀

-...

################################################################################################################################################################################################################################################################ ¿Quieres más código de entrevista?
Suscríbete a nuestro boletín para pasarelas semanales de problemas de LeetCode, explicaciones de vídeo y desafíos de preparación de entrevistas.

-...

■ **Author: ** *[Su nombre]* – *Ingeniero Algorithm TENIDO Datos–Evangelista de la Estructura*
■ **Contacto:** `your.email@example.com` Silencio `LinkedIn / Twitter` Silencio `GitHub: yourgithub `

-...

**End of Blog* *

-...

### 🔗 Quick Links

Silencioso en la sección Silencio
Silencio...
Silencioso Código Silencio
Silencio Blog Artículo Silencioso
TENIDA TL;DR ANTE `#tldr` Silencio

-...

Happy interviewing, and remember: **The right data‐structure trick is half the battle. #