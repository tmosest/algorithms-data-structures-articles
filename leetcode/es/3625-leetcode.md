-...
Título: LeetCode 3625. Número de Trapezoides II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Por cada dos puntos diferentes `A(x1 , y1)` y `B(x2 , y2)` miramos a la derecha
segmento " A " .
Todos los segmentos que tienen la misma pendiente pertenecen al mismo grupo **slope**.
Dentro de un grupo de pendiente podemos elegir dos segmentos – si los dos segmentos son

* en diferentes líneas (no collinear)
* no tienen un punto final común

entonces los cuatro puntos finales forman un trapezoide
(El parallelograma es un caso especial de una trapezoide).

----------------------------------------------------

##### 1. Representación de una línea

Para un segmento " AB "

`` `
dx = x2 – x1
dy = y2 – y1
`` `

`dx , dy` se reducen por `g = gcd( permanecedx en la vida , Silencioso
(Los signos se normalizan de modo que `dx ' 0 ' , o `dx===0 ' y el signo está en `d ' ).

`` `
pendiente : (dy , dx) – “inf” para una línea vertical
intercept : (num , den) – el valor de b en y = mx + b
(para una línea vertical: x = const)
`` `

Todas las fracciones se guardan en forma de entero reducido – ningún punto flotante aritmética es
usado.

Una clave para un *line* es la concatenación de la tecla de pendiente y la clave de interceptación.



----------------------------------------------------

##### 2. Contando todos los pares con la misma pendiente

Para una llave de pendiente

`` `
cntSlope(s) – número de segmentos con esta pendiente
cntLine(s,l) – número de segmentos acostados en la misma línea l
`` `

Todos los pares de segmentos con pendiente `s` son `C(cntSlope(s), 2).
Los pares acostados en la misma línea deben ser eliminados – no pueden construir un cuadrilátero.

`` `
trapezoids_from_slope_s = C(cntSlope(s), 2) – Governing_over_lines C(cntLine, 2)
`` `

La suma sobre todas las pistas da el número de trapezoides *y*
paralelogramas contados ** dos veces** (una vez por cada uno de sus dos laterales paralelos
pares).

----------------------------------------------------

##### 3. Contando paralelogramas

Las diagonales de un biseco paralelogramo entre sí.
Por lo tanto, dos segmentos con el mismo punto medio son las diagonales de un
Paralelograma.

Por cada par de puntos almacenamos la suma `(x1+x2 , y1+y2)` – esto es el doble de la
punto medio y se puede utilizar como clave.

`` `
cntMidpoint(m) – número de segmentos que tienen este punto medio
paralelogramas = ega_over_midpoints C(cntMidpoint, 2)
`` `

Cada paralelograma se cuenta exactamente una vez.



----------------------------------------------------

##### 4. fórmula final

`` `
respuesta =
(C(cntSlope,2) – ega_lines C(cntLine,2) ) // trapezoides + 2×parallelogramas
– paralelogramas // eliminar el doble conteo
`` `

Todos los valores intermedios encajan en enteros firmados de 64 bits
(`C(124750, 2) ♥ 7.8·10^9`).

----------------------------------------------------

##### 5. Prueba de corrección

Demostramos que el algoritmo devuelve el número de trapezoides **distintos** que
se puede formar desde los puntos dados.

-...

##### Lemma 1
Para los dos segmentos `AB` y `CD` que son

* paralelo,
* no collinear,
* share no endpoint,

el cuadrilátero formado por los cuatro puntos distintos es convexo y tiene exactamente
un par de lados paralelos.

Proof.

Los segmentos paralelos y no alineados se encuentran en dos líneas paralelas distintas.
Los cuatro puntos finales son distintos, por lo tanto las líneas se intersectan sólo en los
puntos intermedios de los segmentos, nunca dentro de un segmento.
Conexión de los puntos finales en el orden A – B – C – D` (o cualquier cambio cíclico)
produce un cuadrilátero convexo cuyos dos lados opuestos son `AB` y `CD`.



##### Lemma 2
Para una pendiente fija `s` el valor

`` `
C(cntSlope(s), 2) – Governing_lines C(cntLine, 2)
`` `

iguala el número de pares no ordenados de segmentos disjoint, no-collinear que
tienen pendiente.

Proof.

C(cntSlope(s), 2) " cuenta todos los pares sin orden de segmentos con pendiente `s`,
incluyendo aquellos en la misma línea.
Para cada línea `l` con pendiente `s` el valor 'C(cntLine(l), 2)` cuenta los pares
mentir en esa línea - exactamente los casos inválidos que tienen que ser excluidos.
Sutraer elimina todos los pares collinear y deja precisamente los pares que
satisfacer las condiciones de Lemma pacientenbsp;1. ∎



##### Lemma 3
La suma sobre todas las laderas de la expresión de Lemma limitadanbsp;2
iguala el número de trapezoides **plus** el número de paralelogramas
(contada dos veces).

Proof.

Cada trapezoide tiene al menos un par de lados paralelos.
*Si tiene exactamente un par de lados paralelos*
los dos segmentos de ese par pertenecen a un grupo de pendiente único y son contados
una vez en la suma.

*Si es un paralelograma*
tiene dos pares distintos de lados paralelos, por lo tanto se cuenta una vez en
cada uno de los dos grupos de pendiente correspondientes – es decir, dos veces.

Ninguna otra figura es contada por el algoritmo, porque todos los pares contados son
paralela y no colineal (Lemma limitadanbsp;2). ∎



##### Lemma 4
" parallelogramas = Governing_over_midpoints C(cntMidpoint, 2) "
cuenta cada paralelograma exactamente una vez.

Proof.

En un paralelogramo los dos diagonales se bican, de ahí su
los puntos intermedios coinciden.
Por el contrario, si dos segmentos comparten el mismo punto medio, los cuatro puntos finales
forma un paralelograma (las diagonales se bisecan entre sí).
Así cada par de segmentos sin orden con un punto medio común corresponde a un
paralelograma único, y cada paralelograma produce exactamente uno de estos pares.
Por lo tanto summing `C(cntMidpoint,2)` sobre todos los puntos intermedios cuenta cada
paralelograma una vez.



##### Lemma 5
La fórmula final

`` `
total = Governing_over_slopes ( C(cntSlope,2) – Governing_lines C(cntLine,2) ) – paraleloides
`` `

iguala el número de **distintos** trapezoides que se pueden formar.

Proof.

De Lemma adultnbsp;3 la primera suma cuenta cada trapezoide una vez,
y cada paralelograma dos veces.
Lemma plombsp;4 muestra que 'paralelogramas' es el número de diferencia
paralelogramas en la entrada.
La subcontratación elimina el segundo recuento de cada paralelograma,
dejando exactamente una ocurrencia de cada trapezoide (paralelograma incluido). ∎



################################################################################################################################################################################################################################################################ Theorem
El algoritmo descrito anteriormente devuelve el número de diferencia
trapezoides que se pueden construir desde el conjunto dado de puntos.

Proof.

El algoritmo implementa las tres etapas de conteo comprobadas correctas
Lemmas sensiblenbsp;1–5 y finalmente evalúa la fórmula de Lemma implicanbsp;5.
Por lo tanto el número producido es precisamente el deseado. ∎



----------------------------------------------------

##### 6. Análisis de la complejidad

`` `
N = número de puntos (N ≤ 500)

Número de pares de puntos: M = N·(N–1)/2 ≤ 124 750
`` `

*Building the dictionaries* – `O(M)`
*Computing the sums* – linear in the number of distinct keys
(`O(number_of_slopes + number_of_lines + number_of_midpoints)`), all of
los atados por `M`.

`` `
Hora : O(N2) ( Entendido 1.25·10^5 operaciones para el peor caso)
Memoria : O(N2) (tres tablas de hash, cada una a la mayoría de las entradas M)
`` `

Ambos límites están fácilmente dentro de los límites de la tarea.



----------------------------------------------------

##### 7. Aplicación de la referencia (Python 3)

``python
importar matemáticas
de la importación Lista, Tuple

# -----------

def comb2(x: int) - título int:
""Retorno C(x,2) = x*(x-1)/2, pero para x 102 el resultado es 0.""
retorno x * (x - 1) // 2 si x 2 más 0

# -----------
# Resolucionador principal

def count_trapezoids(puntos: List[Tuple[int, int]]) - título int:
slope_cnt = {}
line_cnt = {}
Mid_cnt = {}

para i en rango(len(puntos)):
x1, y1 = puntos[i]
para j en rango(i + 1, len(puntos)):
x2, y2 = puntos[j]

dx = x2 - x1
dy = y2 - y1

# -------- .
si dx == 0: # vertical
g = abs(dy)
slope_key = ("inf", dy // g)
intercept_key = (x1, 0) # x = const
más:
g = math.gcd(dx, dy)
dx //= g
dy //= g
si dx 0
Dx, dy = -dx, -di
slope_key = (dy, dx)

# slope m = dy/dx
num = y1 * dx - x1 * dy * b * dx
den = dx
g2 = math.gcd(num, den)
num //= g2
den/= g2
intercept_key = (num, den)

# ---------- line key -...
line_key = (slope_key, intercept_key)

# ---------- actualización de diccionarios - Sí.
slope_cnt[slope_key] = slope_cnt.get(slope_key, 0) + 1
line_cnt[line_key] = line_cnt.get(line_key, 0) + 1

# ---------- -----
mid_key = (x1 + x2, y1 + y2) # 2 * punto medio
mid_cnt[mid_key] = mid_cnt.get(mid_key, 0) + 1

# ---------- trapezoids + 2×parallelogramas -----------
total = 0
para s, c en slope_cnt.items():
total += comb2(c)

para c en line_cnt.values():
total -= comb2(c)

# ---------- paraleogramas ----------
par = 0
para c en mid_cnt.values():
par += comb2(c)

int(total - par)

# -----------
# Uso del ejemplo

si __name_ == "__main__":
Ejemplo 1
puntos = [(0, 0), (1, 1), (1, 2), (2, 1), (2, 2), (3, 3)]
print(count_trapezoids(puntos)) # → 4
`` `

El programa sigue exactamente el algoritmo probado correcto arriba
y se ajusta a la firma de funciones requerida `count_trapezoids`.

----------------------------------------------------

##### 8. Aplicación de la referencia (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

usando ll = largo;

ll comb2(ll x){ return x > 2 ? 0 : x*(x-1)/2; }
ll gcdll(ll a, ll b){ return std:gcd(a,b); }

int main(){
ios::sync_with_stdio(false);
cin.tie(nullptr);
int n; // número de puntos
si (!(cin нелины n)) retorno 0;
vector efectuadopair realizadoll,ll confianza p(n);
for(int i=0;i armonizan;i++) cin > título p[i].first  título p[i].second;

unordered_map buscadostring,ll pendiente Cnt, lineCnt, midCnt;

para(int i=0;i obtenidos;i++){
ll x1=p[i].first, y1=p[i].second;
para(int j=i+1;j obtenidos;j++){
ll x2=p[j].first, y2=p[j].second;
ll dx=x2-x1, dy=y2-y1;

// -------------- pendiente--------------
pendiente de cuerda Clave;
(dx==0){
ll g=gcdll(abs(dy),1);
dy/=g; // mantener el signo en dy
slopeKey="inf"+to_string(dy);
}else{
ll g=gcdll(abs(dx),abs(dy));
dx/=g; dy/=g;
si (dx obtenidos0){ dx=-dx; dy=-dy; }
slopeKey=to_string(dy)+"_"+to_string(dx);
}

--------- interceptación --------
interceptación de cadenas Clave;
(dx==0){
interceptKey=to_string(x1)+"_0"; // x = const
}else{
// pendiente m = dy/dx, so b = y1 - m*x1 = (y1*dx - x1*dy)/dx
ll num=y1*dx - x1*dy;
ll den=dx;
ll g2=gcdll(abs(num),den);
num/=g2; den/=g2;
interceptKey=to_string(num)+"_"+to_string(den);
}

//---------------- La llave de línea----------------
línea de cuerdaKey = pendienteKey+" Clave;

slopeCnt[slopeKey]++;
línea Cnt[line] Key]++;

//------------ punto medio --------
ll midKeyX=x1+x2, midKeyY=y1+y2;
string midKey = to_string(midKeyX)+"_"+to_string(midKeyY);
midCnt[mid Key]++;
}
}

total = 0;
para (auto &kv : slopeCnt) total += comb2(kv.second);
total -= comb2(kv.second);

ll par = 0;
para (auto &kv : midCnt) par += comb2(kv.second);

ll answer = total - par;
cout se hizo la respuesta
retorno 0;
}
`` `

----------------------------------------------------

##### 9. Aplicación de la referencia (Java 17)

``java
importa java.io.*;
importar java.util*;

clase pública TrapezoidCounter {}

/* ---
estática larga comb2(long x){ return x2?0L:x*(x-1)/2L; }

/* ---
pendiente de cuerda estáticaKey(long dx, long dy){
if(dx==0) return "inf"+dy; // vertical
g largo = Math.abs(gcd(dx,dy));
dx/=g; dy/=g;
si (dx obtenidos0){ dx=-dx; dy=-dy; }
dy+"_"+dx;
}

Intercepto estático de cuerda Key(long x1,long y1,long x2,long y2,long dx,long dy) {}
si(dx==0){ // vertical
retorno x1+"_"+0; // x = const
}else{
largo num = y1*dx - x1*dy; // 2*b
den largo = dx;
g largo = Math.abs(gcd(num,den));
num/=g; den/=g;
volver num+"_"+den;
}
}

/* ---
gcd largo estático (long a, long b) {}
si(b==0) devolver Math.abs(a);
gcd(b, a%b);
}

/* ---
el vacío estático público principal (String[] args) lanza Excepción{
BufferedReader br = nuevo BufferedReader (nueva InputStreamReader(System.in));
int n = Integer.parseInt(br.readLine().trim());
long[][] p = new long[n][2];
para(int i=0;i obtenidos;i++){
StringTokenizer st = nuevo StringTokenizer(br.readLine());
p[i][0] = Long.parseLong(st.nextToken());
p[i][1] = Long.parseLong(st.nextToken());
}

Mapa seleccionadoString,Integer confianza slopeCnt = nuevo HashMap correctamente();
Mapa seleccionadoString,Integer confianza lineCnt = nuevo HashMap garantizado();
Mapa seleccionadoString,Integer confianza midCnt = nuevo HashMap correspond();

para(int i=0;i obtenidos;i++){
x1=p[i][0], y1=p[i][1];
para(int j=i+1;j obtenidos;j++){
x2=p[j][0], y2=p[j][1];
dx=x2-x1, dy=y2-y1;

String sKey = slopeKey(dx,dy);
String iKey = interceptKey(x1,y1,x2,y2,dx,dy);
Cuerda lKey = sKey+" eterna"+iKey;

slopeCnt.merge(sKey,1,Integer::sum);
lineCnt.merge(lKey,1,Integer::sum);

largo mx=x1+x2, mi=y1+y2;
MKey de cuerda = mx+"_"+my;
midCnt.merge(mKey,1,Integer::sum);
}
}

total largo = 0;
para(int c : slopeCnt.values() total += comb2(c);
for(int c : lineCnt.values() total -= comb2(c);

long par = 0;
para(int c : midCnt.values()) par += comb2(c);

respuesta larga = total - par;
System.out.println(answer);
}
}
`` `

Los tres programas de referencia implementan la misma lógica, son completamente
compatible con las versiones de idiomas especificadas, y
resolver el problema dentro de las limitaciones dadas.