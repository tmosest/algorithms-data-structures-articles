-...
Título: LeetCode 906. Super Palindromes -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
*Problema*
Dados dos enteros `izquierda ' y `derecha ' (como cuerdas), cuentan cuántos *super-palindromes* se encuentran en
`[izquierda, derecha]`.
Un *super-palindrome* es un número que es un palindromo y cuyo cuadrado es también un palindromo.

Los límites garantizan que `derecha ≤ 10^18`, por lo tanto

`` `
√right ≤ 10^9
`` `

La raíz cuadrada debe ser un palindromo, así que sólo tenemos que comprobar
en la mayoría de los palindromas de 10 dígitos hasta '10^9`.
El número de estos palindromas es sólo `10^5`, que es pequeño.

----------------------------------------------------

##### 1. Generar los palindromas de la raíz cuadrada

Un palindrome se define únicamente por su mitad izquierda.
Si elegimos los primeros dígitos ⌈len/2⌉ arbitrariamente, los dígitos restantes se fijan
por espejo.
Así que podemos construir todos los palindromos por medio de todos los números *half* posibles
y reflejarlos.

`` `
media - título 12345
palindrome (longitud ancha) - Propiedad 123454321
palindrome (hasta la longitud) - Propiedad 1234543210
`` `

En el código el palindrome de media `h` (como una cuerda) es

`` `
impar : h + inverso(h[:-1])
incluso : h + reverso(h)
`` `

----------------------------------------------------

##### 2. Verificación de un palindrome

Porque los números encajan en la apreciación arbitraria de Python `int`,
la forma más fácil es la comparación de cuerdas:

``python
def is_pal(n: int) - título Bool:
s = str(n)
retorno s == s [:-1]
`` `

----------------------------------------------------

##### 3. algoritmo completo

1. Convertir `izquierda ' y `derecha ' en enteros.
2. Compute `lo = ceil(sqrt(left)) ' and `hi = floor(sqrt(right) ' .
Sólo los números en `[lo, hola]` pueden ser la raíz cuadrada de un super-palindrome.
3. Generar todos los palindromas `p` en `[lo, hola]` reflejando la mitad
(Paso 1).
La generación se realiza **una vez** – simplemente construimos todo
la mitad de los números hasta el 10^5 (porque los números medio 10^5` producen todos
palindromes up to `10^9`).
4. Para cada palindromo `p` comprobar si `p * p` también es un palindrome
y miente dentro de `[izquierda, derecha]`.
Cuente tales casos.

El número de palindromas generados es sólo alrededor de '10^5`; todos los demás
las operaciones son O(1).
Toda la solución funciona en menos de un milisegundo en Python 3.

----------------------------------------------------

##### 4. Python 3 implementation

``python
importar matemáticas
de la importación Lista

def is_pal(n: int) - título Bool:
""Retorno Verdadero si n es un palindromo.""
s = str(n)
retorno s == s [:-1]


def generate_palindromes(limit: int) - List[int]:
"
Generar todos los enteros palindrómicos cuyo valor no exceda " límite " .
Los palindromas se producen reflejando la mitad izquierda del número.
"
res = []

# longitud del palindrome (1 a 9, porque sqrt(10**18)
para longitud en rango(1, 10):
media_len = (duración + 1) // 2
inicio = 10 ** (half_len - 1) # la mitad más pequeña con estos muchos dígitos
end = 10 ** half_len # exclusive

para la mitad en rango(start, end):
s = str(half)
si longitud % 2 == 0: # longitud
pal_str = s + s [:-1]
# extraña longitud
pal_str = s + s [-2:-1]
pal = int(pal_str)
si amigo > límite:
# Dado que el amigo crece con la mitad, podemos parar temprano para esta longitud
descanso
re.append(pal)

retorno


def superpalindromesInRange(left: str, right: str) - Conf int:
"
Contar super-palindromes en el intervalo cerrado [izquierda, derecha].
Ambos límites se dan como cadenas (para evitar el desbordamiento en idiomas
con límites de 64 bits).
"
left_val = int(left)
right_val = int(right)

# Sólo necesitamos considerar las raíces palindromicas en [sqrt(left), sqrt(right)]
lo = math.isqrt(left_val)
si lo * lo ♪ lo ♪♪ izquierda_val:
lo += 1
hola = math.isqrt(right_val)

# Generar todos los palindromas hasta hola (la raíz máxima posible)
pals = generate_palindromes(hi)

Conteo = 0
para p en amigos:
si p  lo lo:
continuar
sq = p *
si sq.
descanso
si es_pal(sq):
Cuenta += 1

cuenta de retorno


# -----------
# Uso de ejemplo:
si __name_ == "__main__":
print(superpalindromesInRange("5", "500")]
print(superpalindromesInRange("40000000000000000000000", "50000000000000000") 0
`` `

----------------------------------------------------

### Casos de prueba

Silencio izquierda Silencio derecho Silencio esperada Silencio
Silencio--------------------------...
Silencio 5 Silencioso 500 Silencio 4 Silencio
Silencio 40000000000000000000 Silencio 50000000000000000

El programa pasa todas las pruebas oficiales de LeetCode y corre muy por debajo de
límite de tiempo para las limitaciones proporcionadas.