-...
Título: LeetCode 631. Diseño Excel Sum Formula -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 1 ride⃣ Problem Recap (LeetCode 631 – Design Excel Sum Formula)

Se le pide que implemente una pequeña hoja de cálculo como Excel que soporta tres operaciones:

Silencioso método Silencioso
Silencio----------
Silencioso `Excel(intura, ancho de char)` tención Inicializar una cuadrícula de `altura × ancho' (altura 1-altura, columnas 'A'-anchura) con todos los ceros. Silencio
Silencio `void set(int row, char column, int val)` ← Escribe un valor entero en una celda. Esto aclara cualquier fórmula que pudiera haber estado allí. Silencio
Silencio `int get(int row, char column)` ← Lea el valor entero actual de una célula. Silencio
Silencio `int sum(int row, char column, List meantString confianza numbers)` ← Define una fórmula para una célula. El valor de la célula se convierte en la suma de las células/rangos en 'números'. La fórmula permanece hasta que la célula es sobrescrito por un `set` u otro `sum`. Las referencias nunca forman un ciclo. Silencio

**Constraints* *

* `1 ≤ altura ≤ 26` (máximo 26 hileras)
* `'A' ≤ ancho ≤ 'Z'` (max 26 columnas)
* `1 ≤ número de llamadas ≤ 100`
* `números ' contiene 1‐5 referencias, cada `'ColRow'` o `''ColRow1:ColRow2'` ( rectángulo incluido)
* `-100 ≤ val ≤ 100`

-...

Diseño de alto nivel

El reto clave: cuando el valor de una célula cambia (ya sea por 'set' o por redefinir su propia fórmula), cada célula que depende de ella debe ser actualizada también – *y* que la propagación puede cascada.

La forma más simple de manejar esto es:

1. **Mantenga el valor crudo de cada celda** – un array de 2-D (o un hash-map de 1-D que se clave por 'ColRow').
2. **Tome una definición de fórmula** por célula cuando se llama "sumo" – esencialmente una lista de todas las células que mira.
3. **Mantenga un gráfico de dependencia inversa**:
`dependiente[x] → { y Silencio y depende de x }`.
Cada vez que se define una fórmula, para cada célula referenciada `x` agregamos la célula actual a `dependiente[x]`.
4. **Cambios del programa**:
*Cuando el valor de una célula cambia* – ejecute una profundidad primero (o primera) caminar sobre el gráfico inverso y recomputar a cada niño. Porque el gráfico es acíclico, este paseo siempre terminará.

La propagación es *no* costosa porque la hoja de cálculo es pequeña (≤ 26×26) y tenemos en la mayoría de 100 operaciones. No hay necesidad de un tipo topológico completo; un DFS/BFS simple es suficiente.

-...

##  Settlement 3down⃣ Full Code

A continuación se ** tres implementaciones completas y autocontenidas** (Java, Python, C++).
Los tres comparten la misma idea algorítmica descrita anteriormente.

■ **Confianza para las entrevistas** – En una entrevista, usted puede explicar que utiliza una * lista de adyacencia* para dependencias inversas, y que la propagación es hecha por DFS/BFS, haciendo la solución O(N) por actualización donde N es el número de células dependientes.

#### 2.1 Java

``java
importar java.util*;

clase Excel {

filas privadas, cols;
int[][] valor final privado; // valor numérico bruto
mapa final privado significado, lista de referencias
Lista final privada efectuadaSet No se realizóString confianza dependientes; // celda → conjunto de células que dependen de ella

// Ayudante a convertir "B5" en "B5" (clave canónico)
llave privada (int r, char c) { devolver "" + c + r; }

public Excel(int height, char broad) {
esto.rows = altura;
este.cols = ancho - 'A' + 1;
this.value = new int[rows][cols];
este.formula = nuevo HashMap Quería();
esto.dependientes = nuevo ArrayList fiel(rows * cols);
para (int i = 0; i) hice filas * cols; ++i) dependientes.add(new HashSet fiel());
}

public void set(int row, char column, int val) {
Célula de cuerdas = clave(row, column);
// Quitar cualquier fórmula vieja
fórmula.remove(cell);
// Actualizar los bordes inversos
clearDependents(cell);
valor[row-1] [column-'A'] = val;
// Propagar el cambio
propagar (celular);
}

public int get (int row, char column) {}
valor de retorno[row-1] [column-'A'];
}

public int sum (int row, char column, List won) {}
Célula de cuerdas = clave(row, column);
// Eliminar la fórmula anterior y sus bordes
fórmula.remove(cell);
clearDependents(cell);

// Construir la lista de referencia (con duplicados contados)
Lista de referencias = buildRefs(números);

// Calcular el valor ahora
int sum = 0;
for (String ref : ref) {
suma += getCellValue(ref);
}
valor[row-1] [column-'A'] = suma;
fórmula.put(cell, refs);

// Registro de dependencias inversas
for (String ref : ref) {
dependientes.get(cellToIndex(ref)).add(cell);
}

// Propagar el nuevo valor
propagar (celular);
restitución;
}

Ayudantes -------

// Valor numérico de retorno para una cadena de referencia (manos celdas planas o un rango)
int privado getCellValue(String ref) {
int r1 = ref.charAt(1) - '0';
si (ref.length() == 3) { // celda simple, por ejemplo, "B5"
[r1-1][ref.charAt(0)-'A'];
} más { // rango "B1:D3"
Criar[] partes = ref.split(":");
int rStart = Integer.parseInt(parts[0].substring(1));
int rEnd = Integer.parseInt(parts[1].substring(1));
char cStart = parts[0].charAt(0);
char cEnd = parts[1].charAt(0);
int sum = 0;
para (int r = rStart; r < = rEnd; ++r) {}
para (charc = cStart; c) {}
suma += valor[r-1][c-'A'];
}
}
restitución;
}
}

// Construir una lista de referencias; se conservan duplicados (suman dos veces)
lista privada significa:Construir confianzaRefs(Listidos Números de contactos) {
Lista de referencias = nuevo ArrayList correctamente();
para (String s : números) {}
si (!s.contains(":") {
ref.add
. ♫ ... {
Criar[] partes = s.split(":");
int r1 = Integer.parseInt(parts[0].substring(1));
int r2 = Integer.parseInt(parts[1].substring(1));
char c1 = parts[0].charAt(0);
char c2 = parts[1].charAt(0);
para (int r = r1; r) {}
para (carta c = c1; c) {}
ref.add(" + c + r);
}
}
}
}
retorno ref;
}

// Quitar todos los bordes inversos que salen de esta celda
vacío privado claroDependents(Célula de cuerda) {
int idx = cellToIndex(cell);
para (Set Garantizar conjunto de confianza : dependientes) set.remove(cell);
}

// Propagar el cambio de valor a todos los dependientes
vacio privado propagar (célula de cuerda) {
Deque seleccionaString confía q = nuevo ArrayDeque corresponde();
q.add(cell);
Establecer:String titulada visitado = nuevo HashSet correctamente();
visitado.add(cell);

(!q.isEmpty()) {
Cura de cuerda = q.poll();
para (Niño de crianza : dependientes.get(cellToIndex(cur)))) {}
// Valor del niño recalculado
Lista de referencias = fórmula.get(niño);
nuevo Val = 0;
for (String ref : ref) newVal += getCellValue(ref);
[child.charAt(1)-'1'][child.charAt(0)-'A'] = newVal;
(visited.add(child)) q.add(child);
}
}
}

// Convertir cadena celular "B5" en un índice en la lista de dependientes
celda de entrada privadaToIndex(Célula de alimentación) {
(cell.charAt(1) - '1') * cols + (cell.charAt(0) - 'A');
}
}
`` `

-...

### 2.2 Python

``python
clase Excel:
def __init__(self, height: int, broad: str):
self.rows, self.cols = height, ord(width) - 64 # 'A' - título 1
self.val = [[0] * self.cols for _ in range(height)]
self.formula = {} # cell - Conf lista de refs
autodependientes = {} # cell - Conf conjunto de células que dependen de ella

def _cell_key(self, r: int, c: str) - confiar str:
Vuelva f

def set(self, row: int, column: str, val: int) - Conf Ninguno.
llave = auto._cell_key(row, column)
self.val[row-1][ord(column)-65] = val
auto.formula.pop(key, None)
auto._propagate(key)

def get(self, row: int, column: str) - Conf int:
retorno auto.val[row-1][ord(column)-65]

def sum(self, row: int, column: str, numbers: list[str]) - título int:
llave = auto._cell_key(row, column)
ref. = []
para ref en números:
si ':' no en ref:
ref.append(ref)
más:
a, b = ref.split(':')
c1, r1 = a[0], int(a[1:])
c2, r2 = b[0], int(b[1:])
para r en rango(r1, r2+1):
para c en rango(ord(c1), ord(c2)+1):
ref.append(f"{chr(c)}{r}")
auto.formula [key] = ref
auto._calc(key, refs)
auto._propagate(key)
retorno auto.val[row-1][ord(column)-65]

def _calc(self, key: str, refs: list[str] Ninguno.
total = 0
para r en refs:
si ':' no en r:
celda = r
total += self.val[int(cell[1:])-1] [ord(cell[0])-65]
más:
# this block is never hit because we expand ranges before
paso
self.val[int(key[1:])-1][ord(key[0]-65] = total

def _propagate(self, key: str) - Ninguno.
# build reverse dependncy graph lazily
si la llave no está en sí misma. dependientes:
autodependientes [key] = set()
for dep, refs in self.formula.items():
si clave en refs:
auto.dependientes.setdefault(dep, set()).add(key)

BFS/DFS
pila = [key]
visto
mientras que la pila:
cur = pila.pop()
cur_val = self.val[int(cur[1:])-1] [ord(cur[0])-65]
para padres, refs en auto.formula.items():
si se cura en refs:
self._calc(parent, refs)
si el padre no se ve:
visto.add(parent)
stack.append(parent)
`` `

-...

### 2.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

clase Excel {
public:
Excel(inta altura, ancho de char) {
R = altura;
C = ancho - 'A' + 1;
val.assign(R, vector autorizado(C, 0));
depende.assign(R*C, unordered_setSelección());
}

vacio set(int r, char c, int v) {}
llave de cadena = cadena(1, c) + to_string(r);
val[r-1] [c-'A'] = v;
formula.erase(key);
propagar (key);
}

int get (int r, char c) {}
devolver val[r-1][c-'A'];
}

int sum (int r, char c, const vector identificadostring ventaja nums) {
llave de cadena = cadena(1, c) + to_string(r);
formula.erase(key);
clear_dependientes(key);

vectoriales ref;
para (auto & s : nums) {
si (s.find(':') == string::npos) refs.push_back(s);
otra vez
partes automáticas = split(s, ':');
char c1 = parts[0][0], c2 = parts[1][0];
int r1 = stoi(parts[0].substr(1));
int r2 = stoi(parts[1].substr(1));
para (int rr = r1; rr) = r2; + rr)
para (char cc = c1; cc = c2; + cc)
ref.push_back(string(1, cc) + to_string(rr));
}
}

fórmula[key] = refs;
recalc(key, refs);
para (auto &ref : refs) depende[idx(ref)].insert(key);
propagar (key);
devolver val[r-1][c-'A'];
}

privado:
int R, C;
vector de vectores val;
unordered_map buscadostring, vector fórmula;
vector noordened_set seleccionadostring confianza depend;

string key(int r, char c) { return string(1,c) + to_string(r); }
int idx(const string limitado s){ return (s[1]-'1')*C + (s[0]-'A'); }

vacuno recalc(cont cordón limitante clave, const vector identificados
total = 0;
(auto &ref : refs) {
si (ref.find(':') == string::npos)
total += val[ref[1]-'1'][ref[0]-'A'];
}
val[key[1]-'1'] [key [0]-'A'] = total;
}

vacio propagar (la clave de la cuerda) {}
queue hacía referencia q;
q.push(key);
unordered_set visitada {key};

(!q.empty()){
string cur = q.front(); q.pop();
para (auto &child : depend[idx(cur)]) {}
// Recompute child
auto refs = fórmula[niño];
int tot = 0;
para (autor : refs)
si (r.find(':') == string::npos)
tot += val[r[1]-'1'][r[0]-'A'];
val[child[1]-'1' [child [0]-'A'] = tot;
(visited.insert(child).second) q.push(child);
}
}
}

vector seccionado con hilos, char delim {}
vectoriales res;
Cura de cuerda;
para(char ch : s){
if(ch===delim){ res.push_back(cur); cur.clear(); }
cur.push_back(ch);
}
res.push_back(cur);
restitución;
}
};
`` `

-...

### 2.4 C++ (moderno)

``cpp
#include יbits/stdc++.h
usando std namespace;

clase Excel {
privado:
int R, C;
vector de vectores val;
unordered_map buscadostring, vector fórmula;
vector noordened_set obtenidosstring confianza rev; // bordes inversos

string key(int r, char c) { return string(1, c) + to_string(r); }

int toIdx(const string &s) {
(s[1]-'1') * C + (s[0]-'A');
}

vacío claroEdges(contiguo cadena) {
para (auto & s : rev) s.erase(k);
}

vacio propagate(cont string &k) {
queue hacía referencia q;
unordered_set obtenidosstring confianza vis;
q.push(k); vis.insert(k);

(!q.empty()) {
string cur = q.front(); q.pop();
para (negro niño : rev[toIdx(cur)]) {}
// Recomputar el valor del niño
auto refs = fórmula[niño];
total = 0;
(auto &ref : refs) {
si (ref.find(':') == string::npos) {}
total += val[ref[1]-'1'][ref[0]-'A'];
}
}
val[child[1]-'1' [child[0]-'A'] = total;
(vis.insert(child).second) q.push(child);
}
}
}

public:
Excel(int h, char w) : R(h), C(w - 'A' + 1), val(h, vector garantizadoint(C, 0)),
rev(R*C) {}

vacio set(int r, char c, int v) {}
string k = key(r, c);
val[r-1] [c-'A'] = v;
formula.erase(k);
clearEdges(k);
propagar (k);
}

int get (int r, char c) {}
devolver val[r-1][c-'A'];
}

int sum (int r, char c, const vector obtenidos >
string k = key(r, c);
formula.erase(k);
clearEdges(k);

vectoriales ref;
para (auto & s : nums) {
si (s.find(':') == string::npos) refs.push_back(s);
otra vez
auto p = split(s, ':');
int r1 = stoi(p[0].substr(1));
int r2 = stoi(p[1].substr(1));
char c1 = p[0][0];
char c2 = p[1][0];
para (int r=r1; rr observado=r2; ++rr)
para (char cc=c1; cc observado=c2; ++cc)
ref.push_back(string(1, cc) + to_string(rr));
}
}

fórmula[k] = refs;
int tot = 0;
for (auto &ref : refs) tot += val[ref[1]-'1'][ref[0]-'A'];
val[r-1] [c-'A'] = tot;
// Actualización gráfico inverso
for (auto &ref : refs) rev[toIdx(ref)].insert(k);

propagar (k);
retorno tot;
}

privado:
vector seccionado con hilos, char delim {}
vectoriales res;
Cura de cuerda;
para (char ch : s) {}
(ch == delim) { res.push_back(cur); cur.clear(); }
cur.push_back(ch);
}
res.push_back(cur);
restitución;
}
};
`` `

-...

-...

## 🧩 4down Por qué funciona

- ** Lista de adyacencia** – 'dependientes' almacena los bordes *reversos*, por lo que podemos caminar desde una célula cambiada hacia fuera sin problemas de profundidad de recursión.
- **Acíclica** – Porque sólo `sum` puede añadir bordes, y nunca agregamos un borde que crea un ciclo (la especificaciones garantiza referencia acíclica). DFS/BFS es seguro.
- **La complejidad** – Cada actualización visita cada niño una vez, por lo que el costo es proporcional al número de células afectadas, muy por debajo del tamaño de la cuadrícula.

-...

## 📌 5️ Interview Talking Points

1. **Explicar estructuras de datos** – matriz 2-D para valores, hash‐map para fórmulas, lista de adyacencia de independencia inversa.
2. **Mostrar el algoritmo de propagación** – DFS/BFS que recomputa a los niños.
3. **Discuss edge-cases** – Referencias duplicadas (cuentas dos veces), ampliación de rango antes de la evaluación.
4. **La complejidad** – O(N) por actualización, N = número de células afectadas; para ≤ 26×26 esto es trivial.

¡Buena suerte en tu entrevista! 🚀

-...

### Гленый 🎉 Final Note

Las soluciones anteriores son compactas y fáciles de probar.
Si quieres extender la hoja de cálculo más tarde (más filas/cols, datos más grandes), simplemente cambiar de arrays a diccionarios – la lógica de propagación permanece igual.
¡Feliz codificación!