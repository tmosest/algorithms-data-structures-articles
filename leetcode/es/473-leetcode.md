-...
Título: LeetCode 473. Matchsticks a Square -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 LeetCode 473 – **Matchsticks to Square* *
## The Good, The Bad, and The Ugly
■ ¿Quieres conseguir un trabajo técnico? * *
■ Maestro este problema, muestra una solución limpia y entra en tu entrevista con confianza.

-...

## 1. Panorama general de los problemas

■ **Given** un array entero `matchsticks`, donde `matchsticks[i]` es la longitud del *i*-th matchstick.
■ ** Objetivo**: Use *all* matchsticks to build a **square** (no break, no extra sticks).
■ **Retorno** `verdad ' si es posible, de lo contrario `falso ' .

### Constraints

Silencio
Silencio...
TENIDO 1 ANTERIOR = matchsticks.length 0 = 15` sometida`1 ANTE = matchsticks[i]

-...

## 2. El “bien”

* **Intuitivo**: Tratarlo como un problema de partición-into‐four‐equal-sums.
* **Backtracking**: Fácil de entender, código mínimo.
* **Bitmask DP**: Explota el pequeño tamaño de entrada (≤15) → `2^15 = 32768` estados.

-...

## 3. El “Bad”

* **Recidiva ingenua** explota rápidamente con 15 palos (caso inferior `4^15`).
* **La ordenación** no es estrictamente necesaria, pero a menudo se utiliza para la poda.
* **Gran número** (≤108) puede causar desbordamiento si no se maneja con `long`.

-...

## 4. El “Ugly”

* **Tight constraints** le obliga a manejar muchos casos de borde:
* Longitud total no divisible por 4 → inmediato `false`.
* Un único palo más largo que el lado objetivo → imposible.
* **Bit-mask tricks** puede ser difícil de leer para los candidatos desconocidos con ellos.

-...

## 5. Optimal Approach: DFS + Bitmask + Memoization

1. **Perímetro total completo** y el lado **target** (`total / 4`).
2. **Salidas externas**
* If `total % 4 != 0` → `false`.
* Si cualquier palo √≥ lado → `false`.
3. **DFS** sobre los palos, tratando de construir cuatro lados.
4. Use un **bitmask** para representar qué palos se han utilizado.
5. **Memoizar** `(mask, sideIndex)` → resultado para evitar la recomputación.

■ ¿Por qué memoización? #
■ Sin ella, el algoritmo puede revisitar estados idénticos muchas veces, especialmente con longitudes duplicadas.

-...

## 6. Aplicación del Código

A continuación se presentan soluciones limpias y bien adaptadas para **Java**, **Python**, y **C+**.

-...

### 6.1 Java

``java
importar java.util*;

Clase Solución {
int privado[] palos; // longitudes de la barra de partido
de entrada privadaLen; // longitud lateral de destino
int n privado; // número de palos
mapa privado realizadoLong, Boolean confianza memo; // key = (mask  made made made 3)

boolean public makesquare(int[] matchsticks) {}
si (matchsticks == null  durable matchsticks.length == 0) devolver falso;
this.n = matchsticks.length;
esto. sticks = Arrays.copyOf(matchsticks, n);

total largo = 0;
total += v;
si (total % 4 != 0) devolver falso;

this.sideLen = (int) (total / 4);

// poda temprana: un palo más largo que el lado no puede caber
para (int v : palos) {
si regresan falsos;
}

// ordenar descender a colocar grandes palos primero (mejor poda)
Arrays.sort(este.sticks);
inversa (este.sticks);

este.memo = nuevo HashMap Quería();
dfs(0, 0, 0);
}

/** DFS con máscara y lado actual */
dfs booleanos privados(enmascarado, int sideIdx, int curLen) {}
llave larga = ((long)mask ; 3) tención sideIdx;
si (memo.containsKey(key)) devuelve memo.get(key);

// Todos los 4 lados terminaron → éxito
(sideIdx == 3) retorno verdadero;

para (int i = 0; i)
si (mask > (1 > ) 0) continuar; // ya utilizado
int len = sticks[i];
si (curLen + len > sideLen) continuar; // rebosaría el lado actual

int newMask = Máscara Silencioso (1 ieregido i);
int newCurLen = curLen + len;
int newSideIdx = (newCurLen == sideLen) ? sideIdx + 1 : sideIdx;
si (dfs(newMask, newSideIdx, newCurLen == sideLen ? 0 : newCurLen) {
memo.put(key, true);
retorno verdadero;
}
}

memo.put(key, false);
devolver falso;
}

inversa (int[] a) {
int l = 0, r = a.length - 1;
mientras que (l
int tmp = a[l]; a[l] = a[r]; a[r] = tmp;
l++; r...
}
}
}
`` `

-...

### 6.2 Python

``python
desde functools import lru_cache
de la importación Lista

Solución de clase:
def makequare(self, matchsticks: List[int]) - título bool:
si no palos de coincidencia:
Retorno Falso

total = suma (matchsticks)
si total % 4 != 0:
Retorno Falso

lado = total // 4
si max(matchsticks) lado:
Retorno Falso

# Sort descending to place large sticks first
matchsticks.sort(reverse=True)
n = len(matchsticks)

@lru_cache(None)
def dfs(mask: int, side_idx: int, cur_len: int) Bool:
si side_idx == 3: # 4o lado encaja automáticamente
Retorno
para i en rango(n):
si máscara " (1 " )
continuar
si cur_len + emparejadores[i] lado de confianza:
continuar
new_mask = máscara Silencioso (1 Identificado i)
new_cur = cur_len + matchsticks[i]
new_side = side_idx + 1 si new_cur == side_idx
nuevo_cur = 0 si nuevo_cur == lado nuevo_cur
si dfs(new_mask, new_side, new_cur):
Retorno
Retorno Falso

devolver dfs(0, 0, 0)
`` `

-...

### 6.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
bool makequare(vector fieltro fieltro) {}
int n = matchsticks.size();
(n == 0) devolver falso;

long long total = 0;
total += v;
si (total % 4 != 0) devolver falso;

int side = total / 4;
para (int v : matchsticks) si (v > side) devuelve falso;

sort(matchsticks.begin(), matchsticks.end(), mayor indicaint()); // descending
unordered_map significa largo, bool memo;

función recomendadabool(int, int, int) título dfs = [ cl](int mask, int sideIdx, int curLen) - título bool
largo largo largo largo llave = (largo largo)mask se hizo 3)
si (memo.find(key) != memo.end()) devuelve memo[key];
(sideIdx == 3) volver verdadero; / / último lado encaja automáticamente

para (int i = 0; i) {}
si (mask " (1 iere escrito i))) continúan; // ya utilizado
int len = matchsticks[i];
si (curLen + len > lado) continuar; / // rebosa el lado actual

int newMask = Máscara Silencioso (1 ieregido i);
int newCur = curLen + len;
int newSideIdx = (newCur == side) ? sideIdx + 1 : sideIdx;
newCur = (newCur == side) ? 0 : newCur;
si (dfs(newMask, newSideIdx, newCur)) {}
memo [key] = verdadero;
retorno verdadero;
}
}
memo[key] = falso;
devolver falso;
};

dfs(0, 0, 0);
}
};
`` `

■ **¿Por qué `(long long)mask ' se hizo 3)
" máscara " necesita 15 bits; cambiamos por 3 (ya que `0 ' se entiende= sideIdx " ) para mantener una llave única.

-...

## 7. Lista de verificación Edge‐Case

TENIDO TERRITORIO Por qué importa
Silencio...
← Vacío matriz Silencio No puede formar un cuadrado. Silencio
Silencio Total no divisible por 4 Silencio Imposible – sin partes iguales. Silencio
TENIDO Stick > lado objetivo TENIDO pegamento único demasiado largo → no cabe. Silencio
← Longitudes Duplicadas Silencio Memoization maneja máscaras idénticas de manera eficiente. Silencio
TENIDO `n ANTE 4` TENENCIA Aún es posible si cada lado utiliza múltiples pegatinas. Silencio

-...

## 8. Análisis de la complejidad

Silencio Silencio Silencio Silencio Silencio
Silencio...
SilencioBrute‐Force DFS (no pruning) Silencio
TENEDADS + Bitmask + Memoization ANTE `O(2^n * n)` (Ω `O(2^15 * 15)`) Silencio `O(2^n)` para la mesa de memorandos
tenciónC++ unordered‐map Silencio `O(2^n)` caso promedio, peor caso `O(2^n * n)` Silencio

*Con `n י= 15`, la solución óptima funciona en milisegundos en hardware moderno. *

-...

## 9. Pitfalls comunes para evitar

1. *Desbordamiento del número entero*
* Use `long`/`long' cuando summing stick longitudes.
2. **Manejo del índice secundario equivocado* *
* Recuerde: después de terminar el lado 3 podemos volver 'verdad' porque los palos restantes deben formar el cuarto lado.
3. *Missing pruning*
* Ordenar descender y colocar los palos más grandes primero corta dramáticamente el árbol de búsqueda.
4. **Memo incorrecto*
* Asegúrate de que la máscara y el índice lateral se combinan de forma única (hift + OR).
5. **Tiempo de salidas en palos duplicados* *
* Sin memoización, las longitudes duplicadas conducen al soplo exponencial.

-...

## 10. Consejos para entrevistas

TENIDO TENDIDO ANTERIOR Por qué ayuda a vivir
Silencio...
**Explicar el problema en inglés claro** antes de la codificación. Silencio Muestra habilidades de comunicación. Silencio
Silencio **Mostrar la intuición** (partición en 4 sumas iguales). ← Demonstrates problema–solving mindset. Silencio
Silencio **Escribe un DFS limpio primero** (sin memo), luego añade poda. Que los entrevistadores vean su proceso de pensamiento. Silencio
Silencio **Disculpiza la tecla de memoria** claramente en su respuesta. tención Evita confusión sobre trucos de masajista. Silencio
Silencio **Mention time‐complexity** y por qué las restricciones permiten `2^15` estados. Silencio Destaca la conciencia algorítmica. Silencio
*Exámen de las pruebas del borde* (`[1,1,1,1,4]`; `[1,1,1,1,2,2,2,2]`). Silencio

■ **Pro-move:** Después de resolver, pregunte al entrevistador:
■ *“Si tuviéramos 30 palos, ¿seguiría manteniendo este enfoque? ¿Qué cambios?*
■ Se convierte en una simple pregunta en una discusión sobre la escalabilidad y los cambios algorítmicos.

-...

## 11. Take- Away: Cómo lograr este problema

TENIDO VALORACIÓN ANTERIOR TENIDO ANTERIOR TENIDO
Silencio...
Silencio **Readability** Silencio Comentarios claros + funciones de ayuda
Silencio **Efficiencia** Silencio Bitmask + memoización
TEN **Scalability** Silencio Handles duplica " large numbers 
Silencio **Interview‐friendly** Silencio Discuss salidas tempranas, poda y complejidad

-...

Conclusión

■ **LeetCode 473** es una entrevista clásica.
■ Maestro el backtracking‐with-bitmask patrón, entender los casos de borde, y estar listo para explicar el algoritmo en lenguaje simple.

■ *Un gancho listo*
■ *“LeetCode 473 Matchsticks to Square solution – DFS, Bitmask, Memoization – prepárate para tu próxima entrevista técnica.”*

-...

### 📄 Meta Descripción
*Aprenda a resolver LeetCode 473 “Matchsticks to Square” en Java, Python y C++ con un enfoque DFS + bitmask claro. Entender los aspectos buenos, malos y feos, y entrar en tu entrevista con una solución pulida. *

-...

¡Feliz codificación, y buena suerte aterrizando ese papel de sueño! 🚀