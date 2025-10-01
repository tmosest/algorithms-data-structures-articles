-...
Título: LeetCode 2868. El juego de palabras -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Por cada movimiento tenemos una palabra que ya se habló.
El siguiente jugador puede hablar sólo

* una palabra que es **léxicográficamente más grande** que la última palabra y
* una palabra que empieza con la primera letra ** o con el **next**
letra en el alfabeto.

Si el jugador que tiene que hablar después no tiene tal palabra, pierde inmediatamente.

La tarea es decidir si Alice (el dueño del array 'a') puede ganar
cuando habla la primera palabra `a[0]`.

----------------------------------------------------

##### 1. Observaciones

* Ambos arrays `a` y `b` ya están ordenados.
* Todo el juego sólo depende del orden relativo de las palabras,
no en qué matriz pertenecen.
* Para una última palabra dada sólo tenemos que mirar palabras que son **strictamente
más grande**.
Si procesamos las palabras en orden léxico*
candidatos para el próximo movimiento ya son evaluados – perfecto para
programación dinámica.

----------------------------------------------------

##### 2. Estado mundial

`` `
propietario : 0 → Alice, 1 → Bob
idx : índice de la palabra dentro de la matriz de su propietario
dp[o][i] : true → el propietario `o` acaba de hablar palabra ` i `
y el *otro* jugador eventualmente perderá
(el dueño puede ganar todo el juego)
falso → el propietario perderá
`` `

El juego termina cuando el jugador que tiene que hablar siguiente no puede encontrar un
palabra válida – esta es exactamente la situación descrita por la definición
de `dp`.

----------------------------------------------------

##### 3. Estructuras de datos

Silencioso para la aplicación
Silencio--------------------------------
Silencio Todas las palabras ordenadas juntos Silencio Lista de objetos `{word, owner, idx}` Silencio
tención rápida “la próxima palabra” consultas ← Búsqueda binaria en la propia matriz del propietario ←
← Mapping word → index Silencio Hash‐map (Java `HashMap`, Python `dict`) Silencio

El número total de palabras es en la mayoría de `2·105`, por lo que todas las estructuras fácilmente
encaja en la memoria.

----------------------------------------------------

##### 4. Recidencia del DP

Por una palabra `w ' pronunciada por el propietario `o`:

`` `
op = 1 - o // oponente

candidatos = palabras del propietario op que
• empezar con w[0] o
• empezar con NextLetter(w[0]
• son lexicográficamente más grandes que w
`` `

*Si hay **no** candidato*, el oponente no puede moverse →
`dp[o][idx] = true`.

*Si hay al menos un candidato*, el propietario gana
sif **un candidato** conduce a la pérdida del oponente:

`` `
dp[o][idx] = verdadero // inicialmente suponemos que podemos ganar
para cada candidato siguiente Idx:
si dp[op] [nextIdx] == falso: // oponente perderá
romper / / / / el propietario gana
más
dp[o][idx] = falso // todos los candidatos conducen a la victoria del oponente
`` `

Porque nos dedicamos a las palabras en **descendente** lexicográfico
orden, `dp[op][nextIdx]` ya es conocido.

----------------------------------------------------

##### 5. Algoritm

`` `
1. Read a[ ], b[ ] // ya ordenados
2. Construir una lista global ALL = { (palabra, propietario, indexInOwnerArray) } para
cada palabra de a y b. Más o menos lexicográficamente.
3. Crear dp[2][len(a)] y dp[2][len(b)] inicialmente todo falso
4. para cada entrada de TODOS del último al primero:
propietario = entrada. propietario
idx = entrada.idx
último Palabra = entrada.palabra
oponente = 1 - propietario
encontradoCandidato = falso
ganar = verdadero / / / ganará si el oponente no tiene movimiento

for letter in [lastWord[0], nextLetter(lastWord[0]]:
// búsqueda binaria en la matriz del oponente para primera palabra > último Palabra
siguiente Idx = primer índice en oponente Array donde
palabra " último La palabra y la palabra comienza con la letra
si sigue Idx existe:
encontradoCandidato = verdadero
si dp[opponent] [nextIdx] == falso:
ganar = verdadero // oponente perderá
descanso
más
ganar = falso // oponente ganará
si no se encuentra Candidato:
ganar = verdadero
dp[owner][idx] = win

5. La respuesta es dp[0][0] // después de que Alice habla a[0] es el turno de Bob
`` `

----------------------------------------------------

##### 6. Prueba de corrección

Demostramos que el algoritmo regresa **verdad** si Alice puede forzar una victoria.

-...

##### Lemma 1
Por cualquier palabra `w' hablada por su propietario `o`, después del algoritmo procesado
'w' we have

`` `
dp[o][idx] = verdadera latitud comenzando desde el estado
(última palabra = w, al lado de jugar = 1-o)
el dueño puede ganar.
`` `

Proof.

Procesamos palabras en un orden estrictamente léxicográfico.
Por lo tanto, cuando `w` se procesa todas las palabras lexicográficamente mayor
(y por lo tanto todos los candidatos para el próximo movimiento) ya tienen sus
Se calcularon los valores dp.

*Si el oponente no tiene candidato*:
`dp[o][idx]` se queda `verdad'.
El oponente no puede moverse, por lo que `o` gana inmediatamente - declaración sostiene.

*Si el oponente tiene al menos un candidato*:
`dp[o][idx]` está establecido en `verdad ' sólo si existe un candidato
tal que `dp[1-o][c] == false`.
`dp[1-o][c] == false` significa el propietario de `c` (el oponente)
eventualmente perderá, por lo tanto `o` gana - declaración sostiene.

*Si todos los candidatos llevan a una victoria para el oponente*:
`dp[o][idx]` se convierte en "falso".
En este caso `o` pérdida - declaración sostiene.

∎



##### Lemma 2
Después de que Alice juegue la primera palabra: el juego es ganado por Alice
iff `dp[0][0]` is `true`.

Proof.

El estado después del primer movimiento de Alice es *exactamente* el estado utilizado en el
definición de " dp[0][0] "

* La última palabra hablada es: (propiedad de Alice, índice `0`).
* Junto a jugar es Bob.

Por lo tanto, por Lemma adultnbsp;1, `dp[0][0]` dice si Alice puede forzar un
ganar de esta posición.

∎



################################################################################################################################################################################################################################################################ Theorem
El algoritmo sale **verdad** si Alice puede ganar el juego.

Proof.

Por Lemma adultnbsp;2 el algoritmo produce `dp[0][0]`.
Por Lemma adultnbsp;1 este valor es verdad exactamente cuando Alice puede forzar una victoria.
Así el algoritmo es correcto.

∎



----------------------------------------------------

##### 7. Análisis de la complejidad

Vamos.

`` `
n = a.length (1 ≤ n ≤ 105)
m = b.length (1 ≤ m ≤ 105)
`` `

*Sorting the global list*: `O(n+m) log(n+m)) `
*Procesamiento de cada palabra*: dos búsquedas binarias → `O(log n)` o `O(log m)`
*Total*: `O(n+m) log (n+m)' tiempo, `O(n+m)` memoria.

----------------------------------------------------

##### 7. Aplicación de la referencia

##### Java 17

``java
importa java.io.*;
importar java.util*;

clase pública Principal {}

--------- estructura de datos para una palabra global -------- */
Clase privada estática WordEntry {
Palabra de cuerda;
int owner; // 0 – Alice, 1 – Bob
int idx; // índice dentro de su matriz propietario

WordEntry(String w, int o, int i) {
palabra = w;
propietario = o;
i)
}
}

/* ---------- helper: siguiente letra alfabética------------
char privada estática siguienteCarta c) {
(carta) (c + 1); // 'a' - título 'b', ..., 'z' - título '{ '
}

/* ---------- búsqueda binaria: primera palabra llave y empezar con carta...
Principio de la int estática privadaGreaterConPrefix(Listecto: llave de cuerda, prefijo de char) {
int lo = 0, hola = arr.size();
mientras (lo cautivado) {
int mid = (lo + hola) 1;
Curr = arr.get(mid);
si (cur.compareTo(key)
lo = mitad + 1;
. ♫ ... {
Hola = mitad;
}
}
// lo es el primer índice con arrr[lo] clave
si (lo ecto arrr.size() " arr.get(lo).charAt(0) == prefijo) {
devolver lo;
}
retorno -1;
}

/* --------------------------
public static void main(String[] args) tira IOException {
BufferedReader br = nuevo BufferedReader (nueva InputStreamReader(System.in));

String[] a = br.readLine().trim().split("\\s+");
String[] b = br.readLine().trim().split("\s+");

int n = a.length;
int m = b.length;

/ Lista global
Lista realizadaWordEntry confía all = nuevo ArrayList fiel(n + m);
para (int i = 0; i < n; ++i) all.add(new WordEntry(a[i], 0, i));
para (int i = 0; i)

all.sort(Comparator.comparing(e - título e.word));

// dp arrays
boolean[][] dp = new boolean[2][];
dp[0] = nuevo booleano[n];
dp[1] = nuevo boolean[m];

// Proceso en orden inverso
para (int pos = all.size() - 1; pos √= 0; --pos) {
WordEntry e = all.get(pos);
int owner = e.owner;
int idx = e.idx;
Estring last = e.word;
char first = last.charAt(0);
char next = nextLetter(first);

Boolean encontrado Candidato = falso;
boolean win = true; // default: ganamos si el oponente no puede moverse

int op = 1 - propietario;
Lista No. 0) Arrays.asList(a) : Arrays.asList(b);

// probar ambas posibles primeras letras
for (char letter : new char[]{first, next}) {}
siguiente Idx = firstGreaterWithPrefix(oppArray, last, letter);
si (nextIdx!= -1) {
encontradoCandidato = verdadero;
si (!dp[op] [nextIdx]) { // oponente perderá
ganar = verdadero;
ruptura;
Si no, el oponente ganará
ganar = falso;
}
}
}
si (!foundCandidate) ganar = verdadero;
dp[owner][idx] = win;
}

System.out.println(dp[0][0] ? "verdad" : "falso");
}
}
`` `

##### Python 3

``python
importadores
importador bisect

def solve(a, b):
n, m = len(a), len(b)

# lista global de todas las palabras
all_words = []
para i, w en enumerate(a):
all_words.append(w, 0, i))
para i, w en enumerate(b):
all_words.append(w, 1, i))
all_words.sort(key=lambda x: x[0]) # lexicographic order

dp_a = [False]
* m

# helper: primer índice en arrr que es clave y comienza con letra
def first_greater_with_prefix(arr, key, letter):
idx = bisect.bisect_right(arr, key)
mientras que idx se hizo len(arr) y arrr[idx][0] != carta:
idx += 1
volver idx si idx se hizo len(arr) otro -1

por palabra, propietario, idx in reversed(all_words):
opp = 1 - propietario
encontrado = Falso
ganar = True # ganará si el oponente no tiene movimiento

for letter in (word[0], chr(ord(word[0]) + 1)):
si opp == 0:
arrr = a
Dp_opp = dp_a
más:
arrr = b
dp_opp = dp_b

# búsqueda binaria de la primera palabra > palabra que comienza con 'letter '
# arr es una lista de cuerdas
lo = bisect.bisect_right(arr, word)
# Asegurar los primeros partidos de carácter
mientras que lo que hizo (arr) y arrr[lo][0] != carta:
lo += 1

si lo que significan
encontrado = Verdadero
si no dp_opp[lo]:
Ganancia = Verdadera
descanso
más:
Ganancia = Falso

si no se encuentra:
Ganancia = Verdadera

si el propietario == 0:
dp_a[idx] = ganar
más:
dp_b[idx] = ganar

# después de que Alice hable un [0] es el turno de Bob
retorno dp_a[0]


si __name_ == "__main__":
a = sys.stdin.readline().split()
b = sys.stdin.readline().split()
print("true" si resuelve(a, b) otro "false")
`` `

----------------------------------------------------

##### 7. Aplicación de referencia – C++ (para la integridad)

``cpp
#include יbits/stdc++.h
usando std namespace;

struct Entry{
hilo w;
int owner; // 0: Alice, 1: Bob
int idx; // índice en su propia matriz
};

int main(){
ios::sync_with_stdio(false);
cin.tie(nullptr);
línea de cuerda;
// leer línea entera, dividida por espacio blanco
vector asignado a, b;
getline(cin, line);
stringstream ss(line);
Tok de cuerda;
mientras que (ss.
getline(cin, line);
stringstream ss2(line);
b.push_back(tok);

int n = a.size(), m = b.size();

vectoriales: Entradas todas;
all.reserve(n+m);
para(int i=0;i obtenidos;i++) all.push_back({a[i],0,i});
para(int i=0;i observadom;i++) all.push_back({b[i],1,i});

sort(all.begin(), all.end(), [](const Entry plaga x, const Entry
retorno x.w
});

vector realizador autorizado dp(2);
dp[0].assign(n,0);
dp[1].assign(m,0);

auto firstGreater = [ъn](cont vector identificadostring ventaja arrr, const string pulsa key, char letter) {}
int l=0,r=arr.size();
mientras que(l) {
int mid=(l+r)/2;
si (arr[mid] <= key) l=mid+1;
más r=mid;
}
si (l)[l][0]==letter) devuelto l;
retorno -1;
};

para(int pos=(int)all.size()-1;pos confianza=0;--pos){
const auto = all[pos];
int owner=e.owner, idx=e.idx;
const string >
int opp=1-owner;
bool win=true; // ganará si el oponente no tiene movimiento
bool found=false;

char letters[2] = { last[0], (char)(last[0]+1) };

para(car carta: letras) {}
siguiente Idx;
(opp==0){
nextIdx = firstGreater(a, last, letter);
}else{
nextIdx = firstGreater(b, last, letter);
}
if(nextIdx!=-1){
found=true;
(opp==0){
si(!dp[0] [nextIdx]){ win=true; break;}
más ganar=falso;
}else{
si(!dp[1] [nextIdx]){ win=true; break;}
más ganar=falso;
}
}
}
si(!found) win=true;
si (propietario==0) dp[0][idx]=win;
dp[1][idx]=win;
}
cout se cumplió (dp [0] [0] "verdad": "false")
}
`` `

----------------------------------------------------

### 8. Conclusión

El problema reduce a comprobar si la última palabra procesada puede ser golpeada por el oponente en un juego determinista.
Al explorar el juego hacia atrás (de la palabra más grande de la lexicografía) y aplicar DP simple con búsquedas binarias, podemos determinar el ganador en el tiempo `O(n+m) log(n+m).
Todas las implementaciones de referencia anteriores se adhieren a las limitaciones del problema y son totalmente compatibles con Java 17, Python 3 y (para la integridad) C+17.