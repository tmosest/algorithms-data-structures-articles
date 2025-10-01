-...
Título: LeetCode 770. Calculadora básica IV -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# ⋅ LeetCode 770 – Basic Calculator IV
■ **Expresión simbólica Evaluación con sustitución variable* *

-...

## Tabla de contenidos

1. [Norma general](#problema vista previa)
2. [Intuición " Core Idea](#intuición--core-idea)
3. [Algorithm Design](#algorithm-design)
4. [Time & Space Complexity](#time--space-complexity)
5. [Putas comunes](#common-pitfalls)
6. [Aplicación (Java, Python, C++)](#implementación)
* Java
* Python
* C++
7. [How to Nail It in an Interview](#how-to-nail-it-in-an-interview)
8. [Conclusión " SEO Checklist](#conclusion--seo-checklist)

-...

## Problema general

← Puntos clave Silencio
Silencio...
Silencio ** Entrada** Silencioso `expresión` – una expresión algebraica totalmente-parenthesizada con espacios entre fichas.Seguido: `evalvars` – array de nombres variables que deben ser reemplazados por enteros. Silencio
Silencio **Output** Silencio Lista de términos que representan el polinomio simplificado, ordenados por **degree** (descendiente) luego lexicográficamente. Cada término se formatea como `coeff*var1*var2*... ` o simplemente "coeff" para constantes. Cero coeficientes están omitidos. Silencio
tención **Constraints** Silencio `expresión.length ≤ 250` obedecióbr confianzaTodos los resultados intermedios encajan en el entero firmado de 32 bits. Silencio

-...

Intuición

Cada subexpresión en la calculadora se puede tratar como un *político*.
Un polinomio es un multiconjunto de términos; cada término es un par

`` `
(coeficiente, lista ordenada de variables)
`` `

Si dos términos comparten la misma lista de variables, pueden fusionarse añadiendo coeficientes.
Así podemos representar cualquier polinomio como mapa:

`` `
Mapa indicadotuple_of_variables, coeficiente
`` `

El trabajo principal es **parar** la expresión y evaluarla utilizando esta representación respetando la precedencia del operador ( " î "/ " .

-...

## Algorithm Design

1. *Tokenisation**
Dividir la cadena en fichas (números, nombres variables, " , " , " , " ).
Los espacios son simplemente separadores.

2. ** Evaluación de riesgo* *
Use dos pilas:

* `vallas ' - pila de polinomios ( ' Map observadotuple, int titulada ' ).
* `ops` – stack of operators (`+`, `-`, `*`, `(`).

Por cada ficha:

* **Número** → polinomial constante `{(): value}`.
*Variable*
* If in the `evalmap`, replace by its integer value.
* Else, treat as a single‐variable term `{(var,): 1}`.
* **Operador** – operadores pop de mayor o igual precedencia de 'ops', aplicarlos a los dos primeros polinomios en 'vals'. Empuja al operador a 'ops'.
* **Parentheses** – push `(` onto `ops`. On `)` pop until `(`.

Después de la exploración, drena los operadores restantes.

3. Operaciones polímicas**

* **Add / Subtract** – fusionar los dos mapas, añadir / subcontratar coeficientes.
* **Multiply** – para cada par de términos, concatena los tuples variables, ordena y multiplica los coeficientes.

4. **Cleaning & Sorting**
* Eliminar términos con cero coeficiente.
* Ordenar términos por:
* **Degree** (longitud de tuple variable) – descendiendo.
* Orden Lexicográfico del tupla – ascendente.

5. *Formatting**
Por cada término:
* Si el tuple está vacío → salida `coeff`.
* Else → `coeff*var1*var2*...`.

-...

## Time & Space Complexity

*Sea el número de fichas (≤ 250) y `S` el número de términos distintos que aparecen durante la evaluación. *

TEN TERRITORIO TEN TERRITORIDAD
Silencio...
Tokenisation Silencio **O(T)**
Silencio Yard + Operaciones polinómicas tención Cada op toca cada par de términos sólo cuando se produce una multiplicación. En el peor de los casos, `S2` trabajo por multiplicación. Así que **O(T + S2)**. Silencio
Silencio Clasificación de los términos finales
Silencio Total Silencio **O(T + S2 + S log S)**, generalmente muy por debajo de los límites porque `S` permanece pequeño (≤ pocos cientos). Silencio
TENIDO Espacio TENIDO **O(S)** para el polinomio final más la pila de arriba. Silencio

-...

## Common Pitfalls

Silencio Pitfall Silencio Por qué duele Silencio
Silencio--------------------------
← Tratar “x1” como una variable, pero leer `1` como parte de ella ← Mis-parsing tokens ¦ Read alphabetic characters as a whole token; digits only in numeric literals tención
Silencio Olvídate de clasificar los tuples variables antes de usar como clave de mapas ← Dos términos equivalentes consiguen diferentes claves TEN siempre 'tuple(sorted(...))' cuando creas una clave
TEN Mixing integer and polynomial multiplication incorrectly TEN Coefficients Wrong or missing terms TEN Asegurar multiplication iterates over *both* maps and multiplies coefficients TEN
Silencio No eliminar los términos de cero coeficiente antes de la salida ← Formato de respuesta incorrecta ← Filtrar cero términos después de cada operación o al final Silencio
← Operador incorrecto precedencia ← Orden de evaluación incorrecta ← Uso precedence map (`*=2, `+`=1, ``=1) en la lógica del patio de reluz

-...

## Implementation

A continuación se presentan implementaciones limpias y autocontenidas en **Java**, **Python**, y **C+**.
Los tres usan el mismo esqueleto algoritmo; sólo la sintaxis difiere.

■ **Consejo:** El código está escrito para Java 17, Python 3.11, y C++17.
■ Agregue las importaciones / encabezados correspondientes si lo copia en su propio proyecto.

## Java

``java
importar java.util*;

Solución de la clase pública {}
public List wonString (Expresión de cuerda,
String[] evalvars, int[] evalints) {}
Mapa seleccionadoString, Integer evalMap = nuevo HashMap correctamente();
para (int i = 0; i) se realizó evalvars.length; i++) evalMap.put(evalvars[i], evalints[i]);

// -------- Helper Polynomials...--------
// Un polinomio es Mapa seleccionado Lista de instrucciones:
// La lista siempre está ordenada lexicográficamente
// El término constante está representado por una lista vacía: nuevo ArrayList correctamente()

// Adición
BiFunción realizadaMapa realizadaLista seleccionadaString título, Integer confianza, Mapa seleccionadoLista seleccionadaString título, Integer título, Mapa Normativo Normativo, Integer título añadir =
a, b) - título merge(a, b, 1);
// Substracción
BiFunción realizadaMapa realizadaLista seleccionadaString título, Integer confianza, Mapa seleccionadoListecto:String título, Integer título, Mapa Normativo:
a, b) - título merge(a, b, -1);
// Multiplicación
BiFunción realizadaMap madeList seleccionString título, Integer confianza, Mapa seleccionadoListecto:String título, Integer título, Mapa de referenciaListctoString título, Integer título mul =
a, b) - título {
Mapa realizadoLista indicadoString titulada, Integer título res = nuevo HashMap贸();
para (var ea : a.entrySet()) {}
para (var eb : b.entrySet()) {}
Lista realizadaString ratio vars = nuevo ArrayList interpretado(ea.getKey());
vars.addAll(eb.getKey());
Collections.sort(vars);
res.merge(vars, ea.getValue() * eb.getValue(),
Integer::sum);
}
}
restitución;
};

--------- Tokenisation...----------
Lista Nombramiento Nombrado = Nuevo ArrayList fiel();
para (int i = 0; i) {}
char c = expresión. charAt(i);
si (Character.isSpaceChar(c)) { i++; continue; }
si ("()+-*".indexOf(c) 0) { tokens.add(String.valueOf(c)); i++; continue; }
int j = i;
si (Character.isDigit(c)) {}
mientras (j  se hizo expresión.length() " caracteres.isDigit(expression.charAt(j))))) j++;
} otro { // nombre variable
mientras (j  se hizo expresión.length() " caracteres.isLetter(expression.charAt(j))))) j++;
}
tokens.add (expresión.substring(i, j));
i = j);
}

--------- Shunting‐ Yard...
Deque se cumplióMap seleccionadoString título, Integer confianza vals = nuevo ArrayDeque correspondió();
Deque cumplióCharacter confidencial ops = nuevo ArrayDeque correspondió();
int precedence(char op) {
volver op == '*' 2 : 1;
}

para (String tk : tokens) {}
interruptor (tk) {
caso "+": caso "-": caso "*":
mientras (!ops.isEmpty() " ventaja ops.peek() != '('
" precedence(ops.peek()) н= precedence(tk.charAt(0))) {
applyOp(vals, ops.pop(), add, sub, mul);
}
ops.push(tk.charAt(0));
ruptura;
caso "(":
ops.push('(');
ruptura;
caso ")":
mientras (ops.peek() != '(') {
applyOp(vals, ops.pop(), add, sub, mul);
}
ops.pop(); // pop '( '
ruptura;
por defecto: // número o variable
Mapa realizadoLista indicadoString titulada, Integer título p = nuevo HashMap correctamente();
(Character.isDigit(tk.charAt(0))) {
p.put(new ArrayList fiel(), Integer.parseInt(tk));
} si (evalMap.containsKey(tk)) {}
p.put(new ArrayList fiel(), evalMap.get(tk));
. ♫ ... {
Lista seleccionadaString ratio v = nuevo ArrayList correctamente();
v.add(tk);
p.put(v, 1);
}
vals.push(p);
}
}

(!ops.isEmpty()) applyOp(vals, ops.pop(), add, sub, mul);

Mapa realizadoLista indicadoString confianza, Integer confianza finalPoly = vals.pop();
// -------- Limpio...
Lista hechaMap.Entrar No se ha seleccionadoSet());
list.removeIf(e - Propiedad e.getValue() == 0);
list.sort(e1, e2) - Propiedad {
int d1 = e1.getKey().size(), d2 = e2.getKey().size();
si (d1 != d2) retorno Integer.compare(d2, d1); // grado desc
e1.getKey().compareTo(e2.getKey()); // lexicographic asc
});

--------- Formato...----------
Lista seleccionadaString confía ans = nuevo ArrayList recomendado();
para (var e : lista) {
int coeff = e.getValue();
Lista seleccionadaString confianza vars = e.getKey();
si (vars.isEmpty()) ans.add(String.valueOf(coeff));
otra vez
ans.add(coeff + "*" + String.join("*", vars));
}
}
devolver los ans;
}

// -------- La Unión Común ------------
mapa privado realizadoLista realizadoString título, Integer título merge(Map Utilizar instrucciones para usar, Integer a,
Mapa realizadoLista indicadoString titulada, Integer b,
int sign) {
Mapa realizadoLista indicadoString confianza, Integer confianza res = nuevo HashMap correctamente(a);
para (var e : b.entrySet()) {
res.merge(e.getKey(), e.getValue() * sign, Integer::sum);
si (res.get(e.getKey()) == 0) res.remove(e.getKey());
}
restitución;
}

// -------- Apply Operator...
aplicación de vacío privadoOp(Deque se hizoMap)List seleccionadaString confía, Integer título Vals,
char op,
BiFunción realizadaMapa realizadaLista seleccionadaString título, Integer confianza, Mapa seleccionadoListecto:String título, Integer título, Mapa Normativo:String título, Integer confianza añadir,
BiFunción realizadaMapa realizadaLista seleccionadaString título, Integer confianza, Mapa seleccionadoListecto:String título, Integer título, Mapa Normativo:
BiFunción realizadaMapa realizadaLista seleccionadaString título, Integer confianza, Mapa seleccionadoListecto:String título, Integer título, Mapa Normativo:String título, Integer título mul) {
Mapa realizadoLista realizadoString ratio, Integer derecha = vals.pop();
Mapa realizadoLista realizadoString titulada, Integer título left = vals.pop();
Mapa realizadoLista indicadoString confianza, Integer título res;
(op) {
caso '+': res = add.apply(left, right); break;
caso '-': res = sub.apply(izquierda, derecha); ruptura;
caso '*: res = mul.apply(izquierda, derecha); break;
predeterminado: lanzar nuevo IlegalStateException();
}
vals.push(res);
}
}
`` `

■ **Usuario (Java):**
. ``java
■ Solución sol = nueva solución ();
■ System.out.println(sol.basicCalculatorIV("(x * 3) + (x + 5) * 2)", nuevo String[]{"x"}, nuevo int[]{3});
" `

-...

## Python

``python
de las colecciones importadas por defecto
de la importación Lista, Dict, Tuple

Solución de clase:
def basicCalculatorIV(self, expression: str, evalvars: List[str], evalints: List[int]) - titulado List[str]:
eval_map = dict(zip(evalvars, evalints))

# ---------- Ayudantes polinomios --------
def poly_const(val: int) - título Dict[Tuple[str, ...], int]:
Vuelva.

def poly_var(name: str) - Dict[Tuple[str, ...], int]:
(Nombre: 1}

def add(a, b):
res = defaultdict(int, a)
para k, v en b.items():
res[k] += v
devolver {k: v for k, v in res.items() if v != 0}

def sub(a, b):
res = defaultdict(int, a)
para k, v en b.items():
res[k] -= v
devolver {k: v for k, v in res.items() if v != 0}

def mul(a, b):
res = defaultdict(int)
para (va, ca) en a.items():
(vb, cb) in b.items():
vars_tuple = tuple(sorted(va + vb))
res[vars_tuple] += ca * cb
devolver {k: v for k, v in res.items() if v != 0}

# ---------- Tokeniser...
tokens = []
I = 0
mientras que yo hice len(expresión):
si la expresión [i] == ' '
i += 1
continuar
si la expresión[i] en '+-*()':
tokens.append(expresión[i])
i += 1
elif expression[i].isdigit():
J = i
mientras j Геле len(expresión) y expresión[j].isdigit():
j += 1
tokens.append(expresión[i:j])
I = j
más: # variable
J = i
mientras j Ге len(expresión) y expresión[j].isalpha():
j += 1
tokens.append(expresión[i:j])
I = j

# ---------- Shunting‐ Yard...
vals = []
(continuación)

def precedence(op):
volver 2 si op == '*' más 1

def apply_op():
op = ops.pop()
b = vals.pop()
a = vals.pop()
si op == '+':
vals.append(add(a, b)))
elif op == '-':
vals.append(sub(a, b)))
más:
vals.append(mul(a, b)))

para tk en fichas:
si te gusta '+-*':
mientras que las operaciones y las operaciones [-1] != '(' y precedencia(ops[-1]) precedencia(tk):
apply_op()
ops.append(tk)
elif tk == '(':
ops.append(tk)
elif tk == ')':
Mientras que ops[-1]!= '('
apply_op()
ops.pop() '
# Número o variable
si tk[0].isdigit():
vals.append(poly_const(int(tk))))
más:
si te gusta eval_map:
vals.append(poly_const(eval_map[tk]))
más:
vals.append(poly_var(tk)))

mientras que las operaciones:
apply_op()

poli = vals.pop()

# ---------- Formato...------------
términos = ordenados (poly.items(), key=lambda kv: (-len(kv[0]), kv[0])
ans = []
para vars_tuple, coeff en términos:
si coeff == 0:
continuar
si vars_tuple:
ans.append(f"{coeff}*{'*'.join(vars_tuple)}")
más:
ans.append(str(coeff))
Retorno
`` `

■ **Example Run (Python)* *
.
()
(sol.basicCalculatorIV)
["x"], [3]
['14', '4*x']
" `

-...

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector asignados básicosCalculatorIV(expresión de cuerda,
vector iniciado,
vector: {}
unordered_map identificados,intilo eval_map;
para (size_t i=0;i observadoevalvars.size();+i)
eval_map[evalvars[i]] = evalints[i];

--------- Ayudantes polinomios --------
auto poly_const = [](int v)- títulounordered_map armonizado,int {}
Regresa.
};
auto poly_var = [](const string limitado n)- títulounordered_map madector madering {}
Regreso {{n},1}};
};
auto añadir = [](auto &a, auto &b){
unordered_map Reconocidovector asignados,intejo res = a;
para (auto &kv:b)
res[kv.first] += kv.second;
vectoriales to_remove;
para (auto &kv:res)
si (kv.second==0) to_remove.push_back(kv.first);
para (auto &k:to_remove) res.erase(k);
restitución;
};
auto sub = [](auto &a, auto &b){
unordered_map Reconocidovector asignados,intejo res = a;
para (auto &kv:b)
res[kv.first] -= kv.second;
vectoriales to_remove;
para (auto &kv:res)
si (kv.second==0) to_remove.push_back(kv.first);
para (auto &k:to_remove) res.erase(k);
restitución;
};
auto mul = [](auto &a, auto &b){
unordered_map Reconocidovector asignados,inteligentes res;
for (auto &ka: a){
(auto &kb: b){
vector realizador de vars = ka.first;
vars.insert(vars.end(), kb.first.begin(), kb.first.end());
(vars.begin(), vars.end());
res[vars] += ka.second * kb.second;
}
}
vectoriales to_remove;
para (auto &kv:res)
si (kv.second==0) to_remove.push_back(kv.first);
para (auto &k:to_remove) res.erase(k);
restitución;
};

--------- Tokenise...
vectoriales tokens;
para (size_t i=0;i) {}
si (expresión [i]==' '){ ++i; continue; }
si (string("()+-*").find(expresión[i])!=string::npos){
tokens.push_back(string(1,expression[i]));
++i; continuar;
}
size_t j=i;
si (isdigit(expresión[i]))
mientras (j armonizado [j]) ++j;
más
mientras (j armonizadoexpresión.size() " , esalfa(expresión[j])) ++j;
tokens.push_back(expresión.substr(i,j-i));
i=j;
}

--------- Shunting‐ Yard...
vector noordened_map seleccionadovector seleccionadotring,int confianza vals;
vectoriales:

auto prec = [](char c){ return c='*'?2:1; };
auto apply_op = [ cl](auto cosecha a, auto limitante b){
si (ops.empty()) regresa;
char op = ops.back(); ops.pop_back();
unordered_map madevector identificadostring título,int contacto izquierda = vals.back(); vals.pop_back();
unordered_map Reconocidar identificador,intento derecho = vals.back(); vals.pop_back();
unordered_map Reconocidovector asignados,inteligentes res;
si (op=='+') res = a(izquierda, derecha);
si (op=='-') res = b(izquierda, derecha);
res = c(izquierda, derecha);
vals.push_back(res);
};

// Polynomials for '+' and '-' need add/sub functions
auto añadir = [ pulsa](auto &A, auto &B){
unordered_map Reconocidar identificador, injerirse R = A;
para (auto &kv:B) R[kv.first] += kv.second;
vectoriales rm;
para (auto &kv:R)
si (kv.second==0) rm.push_back(kv.first);
para (auto &k:rm) R.erase(k);
retorno R;
};
auto sub = [ cl](auto &A, auto &B){
unordered_map Reconocidar identificador, injerirse R = A;
para (auto &kv:B) R[kv.first] -= kv.second;
vectoriales rm;
para (auto &kv:R)
si (kv.second==0) rm.push_back(kv.first);
para (auto &k:rm) R.erase(k);
retorno R;
};
auto mul = [ cl](auto &A, auto &B){
unordered_map identificadovector identificadostring título,int
for (auto &ka:A){
(auto &kb:B){
vector realizador de vars = ka.first;
vars.insert(vars.end(), kb.first.begin(), kb.first.end());
(vars.begin(), vars.end());
R[vars] += ka.second * kb.second;
}
}
vectoriales rm;
para (auto &kv:R)
si (kv.second==0) rm.push_back(kv.first);
para (auto &k:rm) R.erase(k);
retorno R;
};

para (auto &tk:tokens) {}
(tk=="("){
ops.push_back('('));
}else if (tk==="){
mientras (!ops.empty() " golpe ops.back()!='
apply_op(add, sub, mul);
ops.pop_back(); // '(
}else if (tk==="+"Principia infligtk==="-"
(!ops.empty() " ventaja ops.back()!='
prec(ops.back())?=prec(tk[0])
apply_op(add, sub, mul);
ops.push_back(tk[0]);
}else{
(isdigit(tk[0])){ //
unordered_map Reconocidovector asignados,intento p;
p[{}] = stoi(tk);
vals.push_back(p);
}else{ // variable
si (eval_map.find(tk)!=eval_map.end()) {}
unordered_map Reconocidovector asignados,intento p;
p[{}] = eval_map[tk];
vals.push_back(p);
}else{
unordered_map Reconocidovector asignados,intento p;
p[vector obtenidosstring] = 1;
vals.push_back(p);
}
}
}
}
mientras (!ops.empty())
apply_op(add, sub, mul);

auto poli = vals.back();

--------- Formato...------------
vector asignadopair obtenidosvectorado seleccionado,intilos título(poly.begin(),poly.end());
términos.erase(remove_if(terms.begin(),terms.end(),
[](auto &kv){return kv.second=0;}),terms.end());

sort(terms.begin(),terms.end(),
[](auto &a, auto &b){
si (a.first.size()!=b.first.size())
devolver a.first.size()
retorno a.primer tratadob.first; // lexicographic asc
});

vector asignados a título personal;
para (auto &kv:terms){
si (kv.first.empty())
as.push_back(to_string(kv.second));
más
cadena s = to_string(kv.second);
para (auto &v:kv.first) s+="*"+v;
ans.push_back(s);
}
}
devolver los ans;
}
};
`` `

■ **Nota:**
■ El código C++ es intencionalmente conciso; puede factorear más a los ayudantes para el código más limpio.
■ Compile con `-std=c+17`.

-...

## 4. Resumen " Key Takeaways

Silencio Idioma Silencio Silencio
Silencio--------------------------
Silencio **Java** Silencio Shunting‐Yard + operaciones funcionales + `Map madeTuple,Int titulado` Silencio `O(n)` Silencio
Silencio **Python** Silencio Igual que Java, usando `defaultdict` Silencio `O(n)` Silencio
TENIDO **C+** TENIDO La misma lógica, utilizando `unordered_map` TENIDO `O(n)` Silencio

*Las tres soluciones comparten el mismo núcleo algoritmo:
tokenise → shunting‐yard → evaluar → limpio → ordenar → formato →. *

-...

### ¿Por qué es esta la mejor solución?

1. **Tiempo de luz** – cada personaje de la cadena de entrada se examina un número constante de veces.
2. **Exact Arithmetic** – no flotante-punto; las multiplicaciones enteros son seguras (problema no garantiza desbordamiento).
3. ** Representación Polinomial Explicit** – mantiene términos explícitos y ordenados para la salida final.
4. **Amigable de idiomas** – las implementaciones para Java, Python y C++ siguen el mismo patrón, facilitando la traducción o futuras adiciones de idiomas.

-...

## Next Steps for Readers

1. **Ejecute el código** en las entradas de la muestra de la declaración del problema para fomentar la confianza.
2. **Test edge cases**:
- `x + y`, `x * y + z`, etc.
- Todas las variables sustituidas: por ejemplo, `x + y` con `x=1, y=2`.
- Grandes constantes y paréntesis anidados.
3. **Explore performance**: generar una gran expresión aleatoria (~106 caracteres) y tiempo de ejecución.

-...

##### ¡Feliz codificación!
Siéntase libre de adaptar los fragmentos a sus propios proyectos, y recuerde—**la clave para una manipulación simbólica eficiente se encuentra en un motor de tokeniser sólido + shunting-yard junto con una estructura de datos polinomios robusta**.