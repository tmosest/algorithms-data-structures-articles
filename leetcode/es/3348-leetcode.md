-...
Título: LeetCode 3348. Digit Divisible más pequeño producto II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Para un número

`` `
x = d1 d2 ... dm ( di – dígitos decimales )
`` `

su *producto* es el producto de todos sus dígitos decimales

`` `
producto(x) = d1 · d2 · ... · dm .
`` `

Para un caso de prueba se nos da

* a required product `t` ( `t ≥ 2` )
* a maximum length `n` ( `1 ≤ n` )
* a lower bound `k ' ( `k ≥ 1`)

Tenemos que encontrar un número

`` `
x ( 1 ≤ longitud(x) ≤ n , producto(x) = t )
`` `

con el menor valor decimal posible.
Si no existe tal número, la respuesta es **NO SOLUTION**.



----------------------------------------------------

##### 1. Observaciones

* El producto de un número depende sólo de sus dígitos.
* La factorización principal de un dígito decimal contiene sólo los primos
`2 , 3 , 5 , 7`.
Todos los demás factores principales no aparecen en ningún dígito decimal, por consiguiente
nunca pueden ser parte de un producto de dígitos decimales.
Por lo tanto

`` `
si t contiene un factor primario diferente a 2,3,5,7
→ ningún número con el producto t existe en absoluto
`` `

* Para los primeros `2 , 3 , 5 , 7` la tabla siguiente muestra la
* dígito más eficiente* – es decir, el dígito que utiliza la menor cantidad de
dígitos para una cantidad determinada de factores principales

Primera factor tención posible dígito Silencio número de dígitos usados
Silencio------------------------
Silencioso 23 Silencio 8 Silencio
Silencio 22 Silencio 4 Silencio
Silencio 2 · 3 Silencio 6 Silencio 1
Silencioso 32 Silencio
Silencio 2 Silencio Silencio 1 Silencio
Silencio 3 Silencio 3 Silencio 1 Silencio
Silencio 5 Silencio 5 Silencio 1 Silencio
Silencio 7 Silencio 7 Silencio

Usando los dígitos de esta tabla el número de dígitos que
son necesarios para realizar un multiconjunto dado de factores primarios
minimizado.
Después de eso, para un valor numérico mínimo los dígitos deben ser ordenados
en orden * ascendente*.

----------------------------------------------------

##### 2. Algoritm

Para cada caso de prueba

`` `
1. Read k, n, t.
2. Factorizar t en los exponentes de 2,3,5,7.
si t contiene otro factor principal → NO SOLUCIÓN
3. Producir el multiconjunto de dígitos decimales que realiza el factor
exponentes con el menor número posible de dígitos.
(verde, utilizando la tabla de la sección 1)
4. Si la cantidad de dígitos producidos
→ NO SOLUCIÓN
5. Construir el número clasificando cada vez más los dígitos producidos.
Que sea dulce.
6. Si se puede
→ NO SOLUCIÓN
7. De lo contrario, la producción se puede
`` `

----------------------------------------------------

##### 3. Prueba de corrección

Demostramos que el algoritmo produce una respuesta correcta para cada prueba
caso.

-...

##### Lemma 1
Si `t` contiene un factor primario distinto de `2,3,5,7` entonces no decimal
el número tiene el producto `t`.

Proof.
Cada dígito decimal tiene factores primarios sólo entre los `2,3,5,7`.
El producto de cualquier número de dígitos decimales es por lo tanto un producto de
estos primos sólo, nunca contiene otro factor principal. ∎



##### Lemma 2
El multiconjunto de dígitos producidos en paso limitadonbsp;3 realiza la factorización
y utiliza el menor número posible de dígitos.

Proof.
Considere una cantidad fija de factores principales de cada tipo.
La tabla de sección curvanbsp;1 listas, para cada factor principal, un dígito que
necesita el menor número de dígitos decimales para realizar ese factor.
En consecuencia, utilizando los dígitos de la tabla
elimina los factores principales de la factorización de `t`
exactamente lo más rápido posible.
Por lo tanto, después del paso de reemplazo codicioso el número de producidos
dígitos es mínimo entre todos los multisets de dígitos que realizan el factor
exponentes de `t`. ∎



##### Lemma 2
Entre todos los números decimales cuyo dígito multiset es el que se obtiene en
stepntbsp;3 el valor numérico más pequeño es el que se obtiene clasificando
los dígitos cada vez más.

Proof.
Seamos el multiconjunto de dígitos que se da cuenta de 't'.
Cualquier número decimal que utilice exactamente el multiset `S` consiste en el
dígitos de 'S' en algún orden.
Ordenar `S` en orden ascendente produce un número que es lexicográfico
no más grande que cualquier otro pedido del mismo multiset, en consecuencia
es numéricamente mínima. ∎



##### Lemma 3
Si el algoritmo produce un número de `cand` en paso cerradonbsp;7, entonces
`cand` satisface todas las limitaciones del problema.

Proof.

* Mediante la construcción de los dígitos (paso limitadonbsp;3) el producto del
dígitos equivalen a `t`, por lo tanto `product(cand)=t`.
* El número de dígitos producidos nunca exceda " ,
por lo tanto `length(cand) ≤ n`.
* En el paso inferiorbsp;6 comprobamos `cand ≥ k`.
Así, `cand` es una serie de longitud en la mayoría de `n ' y el producto `t`
que no es menor que el límite inferior requerido `k`. ∎



##### Lemma 4
Si el algoritmo sale **NO SOLUTION** entonces no existe ningún número válido.

Proof.
El algoritmo puede producir **NO SOLUTION** en cuatro diferentes
situaciones:

1. Se encontró un factor primario distinto a los 2,3,5,7`.
Por Lemma plaganbsp;1 no hay número con el producto `t` existe.
2. La cantidad de dígitos producidos excede " n " .
Cualquier número con el producto `t` debe contener al menos los dígitos de los
multiset producido en el paso limitadobsp;3, por lo tanto contiene al menos
que muchos dígitos, por lo tanto más largo que `n`.
3. El candidato construido `cand` es más pequeño que `k`.
Todos los números que se dan cuenta del mismo multiconjunto de dígitos son
permutaciones de `cand`; la permutación más pequeña es `cand `
(Lemma limitadanbsp;2).
Por lo tanto, cada número con el producto `t` y a la mayoría de 'n' dígitos
es más pequeño que 'k'.
4. The multiset contains a prime factor other than `2,3,5,7`.
Como en 1. el producto no se puede lograr.

En cada caso ningún número puede cumplir las limitaciones. ∎



##### Lemma 5
Si el algoritmo produce un número de `cand` en paso cerradonbsp;7, entonces
`cand` es el menor número decimal con el producto `t` y la longitud
a most `n` that is not smaller than `k`.

Proof.
Todos los números decimales con el producto `t` y a la mayoría de 'n' dígitos deben usar
un multiconjunto de dígitos que realiza la factorización de `t`.
Por Lemma adultnbsp;2 el número mínimo de dígitos que cualquier multiset puede
contener es el producido en el paso 3).
En consecuencia, cada otro número admisible tiene al menos tantos dígitos
como `cand`.
Si tiene más dígitos, es más grande que cualquier número con el mismo
número de dígitos porque su dígito principal es por lo menos `1` y el
dígitos adicionales añaden valor.
Si tiene el mismo número de dígitos, entonces debe ser diferente
permutación del mismo multiset.
Entre todas las permutaciones de un multiset fijo el más pequeño numéricamente
se obtiene clasificando los dígitos cada vez más (Lemma implicanbsp;2).
Así, el `cand` no es mayor que cualquier otro número admisible.

Finalmente, en el paso fronterizonbsp;6 descartamos todos los números más pequeños que `k`.
Por lo tanto, el número restante `cand` es el menor número admisible
que es al menos `k ' ∎



################################################################################################################################################################################################################################################################ Theorem
Para cada caso de prueba el algoritmo imprime el número requerido si es
existe, de lo contrario se imprime **NO SOLUTION**.

Proof.
Si el algoritmo imprime un número, Lemma implicanbsp;5 garantiza que esto
el número satisface todas las limitaciones y es el más pequeño posible.
Si se imprime **NO SOLUTION**, Lemma plaganbsp;4 muestra que no es admisible
el número existe. Por lo tanto el algoritmo es correcto. ∎



----------------------------------------------------

##### 4. Análisis de la complejidad

Dejar `P = sqrt(t)`.

*Factorización* – en la mayoría de las divisiones de `O(P).
Todas las demás operaciones son lineales en la cantidad de dígitos que son
producido, es decir, en la mayoría de `O(n)`.

`` `
Hora : O( √t + n ) por caso de prueba
Memoria : O( n )
`` `

----------------------------------------------------

##### 4. Aplicación de la referencia (Python 3)

``python
importadores
importar matemáticas

# --------
# helper: factorise t en exponentes de 2,3,5,7
# --------
def factorize(t):
cnt = {2:0, 3:0, 5:0, 7:0}
for p in (2,3,5,7):
mientras que t % p == 0:
cnt[p] += 1
t //= p
# if something is left → a prime factor outside 2,3,5,7
vuelta cnt, t

# --------
# produce el multiset digital con el menor número de dígitos
# --------
def produce_digits(cnt):
res = []
# use the efficient digits first
# 2^3
cnt[2] 3:
res.append('8')
cnt[2] -= 3
# 3^2
cnt[3] 2:
res.append('9')
cnt[3] -= 2
# 2 * 3
cnt[2] не= 1 y cnt[3] 1:
res.append('6')
cnt[2] -= 1
cnt[3] -= 1
# 2^2
cnt[2] 2:
res.append('4')
cnt[2] -= 2
# restante 2 y 3
cnt[2] 1:
res.append('2')
cnt[2] -= 1
cnt[3] 1:
res.append('3')
cnt[3] -= 1
# 5 and 7
cnt[5] >= 1:
res.append('5')
cnt[5] -= 1
cnt[7] >= 1:
re.append('7')
cnt[7] -= 1
retorno

# --------
# principal solucionador
# --------
def solve():
it = iter(sys.stdin.read().strip())
out_lines = []
Prueba:
Mientras Verdadero:
k = int(next(it)))
n = int(next(it)))
t = int(next(it)))

# factorise t
cnt, rest = factorize(t)
si descansas!= 1:
out_lines.append("NO SOLUTION")
continuar

dígitos = produce_digits(cnt)
si len(digits)
out_lines.append("NO SOLUTION")
continuar

cand = ''.join(sorted(digits))
si int(cand)
out_lines.append("NO SOLUTION")
más:
out_lines.append(cand)
excepto StopIteration:
paso

sys.stdout.write("\n"join(out_lines))

si __name_ == "__main__":
solve()
`` `

El programa sigue exactamente el algoritmo probado correcto arriba.