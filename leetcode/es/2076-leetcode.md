-...
Título: LeetCode 2076. Restricted Friend Solicita -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Resumen de la solución – 2076. Solicitudes de amigos restringidas del proceso

**Problema* *
Usted tiene `n` personas (0-indexed).
- `restrictions[i] = [x, y]` significa *x* y *y* nunca puede convertirse en amigos, directamente **o** indirectamente (a través de cualquier cadena de amistades).
- `requests[j] = [u, v]` es una solicitud de amigo que debe ser procesada en orden.
*Si la solicitud puede ser concedida, *u* y *v* se convierten en amigos directos para todas las solicitudes futuras. *

Regrese una matriz booleana `result[j]` decir si la petición *j*‐th tuvo éxito.

■ **Constraints**
≤ 1000
≤ 1000
≤ 1000

La solución ingenua (ver todas las restricciones para cada solicitud) sería **O(n · m)**, que está perfectamente bien para los límites, pero podemos resolver el problema elegantemente con **Desjoint Set Union (DSU)**, también conocido como **Union‐Find**.

-...

## 2. ¿Por qué Union‐Find?

*Cada persona pertenece a un “circle de amistad” (complemento conectado).
Si dos personas están en el mismo componente ya son amigos, de lo contrario no lo son. *

*La idea clave*

Cuando llegue una solicitud `[u, v]`
1. If `find(u) == find(v)` → ya amigos → * éxito*.
2. De lo contrario nosotros **hipotéticamente** fusionar los dos componentes y luego comprobar todas las restricciones.
*Si cualquier restricción `[x, y]` terminaría en el mismo componente, debemos rechazar la solicitud. *

Debido a que el número de solicitudes y restricciones es ≤ 1000, un escaneo lineal sobre las restricciones para cada solicitud es lo suficientemente rápido, mientras que todavía nos da un *O(α(n))* amortizado tiempo de hallazgo/unión.

-...

## 3. Complejidad

TEN TERRITORIO TEN TERRITORIDAD
Silencio...
TENIENDO `find` TENIDO `O(α(n)' (Inverse Ackermann)
TENIENDO `union` TENIDO `O(α(n)' Silencio
tención Proceso una solicitud Silencioso `O(α(n) + r)` donde `r` = número de restricciones (≤ 1000) Silencio
TENIDO ANTERIOR Total `O(q · r)` con `q ≤ 1000` → ≤ 1 000 000 000 operaciones ANTE

Memoria: `O(n + r)`.

-...

## 4. Aplicación

A continuación se muestran las implementaciones **commentadas** en **Java**, **Python**, y **C+**.

▪ restablecimiento Todas las soluciones suponen que los arrays de entrada son cero indexados, según la declaración del problema.

-...

### 4.1 Java (Clean & Commented)

``java
importar java.util*;

Solución de la clase pública {}
--------- Union‐Find (DSU) ---------- */
DSU de clase privada {}
int[] parent, rank;
DSU(int n) {
padre = nuevo int[n];
rango = nuevo int[n];
para (int i = 0; i)
}
int find(int x) {
si (parent[x] != x) parent[x] = encontrar(parent[x]); // path compresión
devolver padre[x];
}
unión de vacío(int a, int b) {}
a = encontrar (a); b = encontrar b);
si (a == b) regresa;
[b] {}
parent[a] = b;
} si (rank[a] } rango[b] {}
parent[b] = a;
. ♫ ... {
parent[b] = a;
rango[a]+;
}
}
}

public boolean[] friendRequests(int n, int[][] restrictions, int[][ peticiones] {
int q = solicitudes. longitud;
boolean[] result = new boolean[q];
DSU dsu = nuevo DSU(n);

para (int i = 0; i)
int u = requests[i][0];
int v = requests[i][1];

// ya en el mismo componente ya amigos
si (dsu.find(u) == dsu.find(v) {
result[i] = true;
continuar;
}

// Unión temporal para probar restricciones
int pu = dsu.find(u);
int pv = dsu.find(v);
dsu.union(pu, pv);

booleano ok = verdadero;
para (int[] r : restricciones) {}
int a = dsu.find(r[0]);
int b = dsu.find(r[1]);
si (a == b) { // se violaría la restricción
ok = falso;
ruptura;
}
}

si (!ok) {
// rollback: deshacer el sindicato por re-crear DSU
// (since n ≤ 1000, podemos reconstruirlo barato)
dsu = nuevo ESD(n);
dsu.union(requests[k][0], requests[k][1]);
result[i] = false;
. ♫ ... {
result[i] = true;
}
}
Resultado de retorno;
}
}
`` `

■ **Nota** – En el código Java anterior reconstruimos el DSU en rechazo porque un verdadero rollback es complicado.
■ Para los pequeños límites del problema esto está perfectamente bien; para los límites más grandes usted mantendría una pila de historia y revertir la unión.

-...

### 4.2 Python (Clear & Idiomatic)

``python
de la importación Lista

clase DSU:
def __init__(self, n: int):
self.parent = list(range(n))
self.rank = [0] * n

def find(self, x: int) - título int:
si yo. parent[x]!= x:
self.parent[x] = self.find(self.parent[x]) # path compresión
Vuélvete. parent[x]

def union(self, a: int, b: int) - Ninguno.
a, b = self.find(a), self.find(b)
si a ==b: retorno
si auto.rank[a] se auto.rank[b]:
self.parent[a] = b
[b]:
self.parent[b] = a
más:
self.parent[b] = a
self.rank[a] += 1

Solución de clase:
def amigoRequests(
auto,
n: int,
restricciones: List[List[int],
Solicitudes: Lista[Listar]
) List[bool]:
res = [False] * len(requests)
dsu = DSU(n)

i, (u, v) in enumerate(requests):
# Ya amigos
si dsu.find(u) == dsu.find(v):
res[i] = Verdadero
continuar

# Trate de fusionar y validar restricciones
dsu.union(u, v)
OK = True
para a, b en restricciones:
si dsu.find(a) == dsu.find(b):
ok = Falso
descanso

si no está bien:
dsu = DSU(n)
para j en rango(i):
dsu.union(*requests[j])
res[i] = Falso
más:
res[i] = Verdadero

retorno
`` `

-...

#### 4.3 C++ (Fast & Modern)

``cpp
#include יbits/stdc++.h
usando std namespace;

struct DSU {}
vector:
DSU(int n = 0) { init(n); }
vacio init(int n) {}
parent.resize(n);
rnk.assign(n, 0);
iota(parent.begin(), parent.end(), 0);
}
int find(int x) {
volver padre[x] == x ? x : parent[x] = encontrar(parent[x]); // path compresión
}
vacío unite (incluido a, int b) {}
a = encontrar (a); b = encontrar b);
si (a == b) regresa;
si (rnk[a] [b]) padre [a] = b;
[b] [b] [b]] padre [b] = a;
[b] = a; ++rnk[a]; }
}
};

Clase Solución {
public:
vector asignadobool amigoRequests(int n,
const vector armonizado:
const vector llevado a cabo
vector asignadobool confía ans(requests.size(), false);
DSU dsu(n);

para (int i = 0; i) ++i) {
int u = requests[i][0];
int v = requests[i][1];

si (dsu.find(u) == dsu.find(v) { // ya friends
as[i] = verdadero;
continuar;
}

dsu.unite(u, v); // tentative merge
bool ok = verdadero;
para (auto &p : restricciones) {}
(dsu.find(p[0]) == dsu.find(p[1]) {/// restriction violated
ok = falso;
ruptura;
}
}

if (!ok) { // rollback by rebuilding DSU
dsu.init(n);
para (int j = 0; j)
dsu.unite(requests[j][0], requests[j][1]);
as[i] = falso;
} más
as[i] = verdadero;
}
devolver los ans;
}
};
`` `

> ¿Por qué reconstruirse en la vuelta? * *
■ Para la reconstrucción de las restricciones dadas es barato (`O(n)`), pero si quieres un rollback real, mantendrías una pila de pares que se fusionaron y revertían la operación.

-...

## 5. “Bien – malo – ugly” de la aproximación del ESD

¿Qué es lo que está diciendo?
Silencio...
TEN **Simplicity** Silencio Clear mapping of friend‐circles to DSU components Silencio Todavía debe escanear restricciones para cada petición Silencio Reconstruir el ESD en rechazo siente “hacky” – usted pierde verdadera semántica deshacer
TEN **Scalability** Silencio Obras para `n, q, r ≤ 106` si usted reemplaza el escaneo de restricción lineal con un hash-set de pares prohibidos TEN El escaneo de restricción lineal se convierte en un cuello de botella en 106 latitud Path-compression por sí solo no previene la violación de la restricción - usted todavía necesita el escaneo
Silencio **Edge-cases** Silencio Manejar "ya amigos" temprano evita el trabajo extra Si un par de restricción ya se viola antes de cualquier solicitud (introducción contradictoria) – el algoritmo simplemente rechaza todas las solicitudes relevantes Silencio Reconstruir el DSU en cada fallo puede llevar a errores sutiles si olvida volver a aplicar todas las fusiones exitosas anteriores TEN

-...

## 6. Lista de verificación para entrevistas

Por qué importa en una entrevista tecnológica
Silencio.
Silencio ✅ **Use DSU** – muestra que conoce una estructura de datos clásica y puede aplicarla a un problema de conectividad. Silencio
TENIDO TENIDO **Explicar el truco de la fusión hipotética** – muchos candidatos se atascan en cómo probar restricciones. Silencio
Silencio ✅ **Discuss rollback** – demostrar la conciencia de que Union‐find no soporta naturalmente el deshacer, y explicar la estrategia de reconstrucción-como-fallback (o deshacer basado en pilas para datos más grandes). Silencio
TENIDO ✅ **Analyze complejidad** – mostrar que puede razonar sobre amortised `α(n)` y por qué la solución es lo suficientemente rápida. Silencio
TENIDO TENIDO ** Optimizaciones potenciales de la mención** – por ejemplo, mapeando cada restricción a un conjunto de vecinos, o almacenando los “pares olvidados” en un conjunto de precipitaciones para la búsqueda O(1) después de una fusión. Silencio

-...

## 7. Pensamientos finales " Pasos siguientes

- **Bien** – El ESD ofrece una solución clara y casi lineal que escala bien.
- **Bad** – La técnica de reconstrucción-en-reject es una solución; un sistema del mundo real necesitaría una pila de deshacer adecuada.
- **Evidentemente** – Escanear todas las restricciones para cada solicitud es simple, pero puede convertirse en un hotspot si las restricciones crecen a 105.
→ * Consejo de optimización:* mantener para cada componente el conjunto de “compañeros restringidos”; cuando se fusiona, prueba rápidamente si la intersección es no vacía.

-...

## 8. 🎯 SEO‐Optimised Blog Post

A continuación se muestra un artículo pulido que puede caer en su GitHub README, blog, o LinkedIn para mostrar sus cortes algorítmicos.

-...

# Procesamiento Restricted Friend Solicita – Leetcode 2076
*Una solución de búsqueda sindical que es perfecta para su próxima tecnología-interview. *

-...

## Tabla de contenidos
1. [Lo que aprenderás] (#¿qué-learn-)
2. [The Problem at a Glance] (#the-problem-at-a-glance)
3. [Por qué Union‐Find Rocks](#why-union‐find-rocks)
4. [De Pseudocode a Production‐Ready Code](#de-pseudocode-to-producción-ready-code)
5. [Complejo & Performance](#complexity‐performance)
6. [Corner‐Case Handling](#corner-case-handling)
7. [Optimisations for Larger Inputs](#optimisations-for-larger-inputs)
8. [Job‐Entreview Nuggets](#job‐interview-nuggets)
9. [Wrap‐Up](#wrap‐up)

-...

## 1. Lo que aprenderás

- **Union‐Find (Disjoint Set Union)** – la estructura de datos para problemas de conectividad.
- Cómo manejar ** restricciones de par restringidas** mientras se fusionan componentes.
- Código en **Java, Python y C+** - listo para una presentación de Leetcode o una entrevista técnica.
- Una explicación de trabajo-interview que resalta su pensamiento algoritmico** y **calidad de código**.

-...

## 2. El problema en un glance

`` `
n = 5
[0, 1], [2, 3]]
[0, 2], [1, 3], [0, 4]]
`` `

*Procesar cada solicitud en orden, pero nunca permitir que un par restringido comparta un componente. *

Producto: `[verdad, falso, verdadero]`.

-...

## 3. Por qué Union‐Find Rocks

**Preguntas de componentes anteriores**: `find(x)` le dice si dos personas ya están conectadas.
- **Amortizado O(α(n)** tiempo para 'unión' y 'find`.
- ¿Qué? En rechazo se puede reconstruir el ESD desde cero (los límites son pequeños).

■ **Introducción clave** – *Se viola una restricción si sus dos puntos finales terminan en el mismo ESD establecido después de una fusión. *

-...

## 4. De Pseudocode a Código de Producción-Ley

#### 4.1 Java

``java
Solución de la clase pública {}
--------- DSU...
DSU de clase privada {}
int[] p, r;
DSU(int n){ p=new int[n]; r=new int[n]; for(int i=0;i obtenidosn;i++) p[i]=i;}
int find(int x){ return p[x]=x?x:p[x]=find(p[x]);}
unión de vacío(int a,int b){
a=find(a); b=find(b);
si (a==b) regresa;
(r[a]cantar[b]) p[a]=b;
si (r[a] confíar[b]) p[b]=a;
[b]=a; r[a]++; }
}
}

public boolean[] friendRequests(int n, int[][] restrictions, int[][ peticiones]{
Int q=requests. longitud;
boolean[] ans=new boolean[q];
DSU dsu=new DSU(n);

para(int i=0;i observadoq;i+){
int u=requests[i][0], v=requests[i ][1]

if(dsu.find(u)==dsu.find(v)){ ans[i]=true; continue; }

// Se fusiona provisionalmente
dsu.union(u,v);
boolean ok=true;
para(int[] r:restrictions) {}
if(dsu.find(r[0])==dsu.find(r[1]){ ok=false; break; }
}

if(!ok){ // rollback: reconstruction DSU
dsu=new DSU(n);
for(int j=0;j obtenidosi;j++) dsu.union(requests[j][0],requests[j][1]);
as[i]=false;
} ans[i]=true;
}
devolver los ans;
}
}
`` `

#### 4.2 Python

``python
clase DSU:
def __init__(self,n): self.p=list(range(n)); self.r=[0]*n
def find(self,x): return x if self.p[x]=x otro auto._set(x,self.find(self.p[x]))
def _set(self,x,val): self.p[x]=val; return val
def union(self,a,b):
a,b=self.find(a),self.find(b)
si a==b: retorno
si auto.r[a] se auto.r[b]: self.p[a]= b
elif self.r[a] convieneself.r[b]: self.p[b]=a
más: auto.p[b]=a; self.r[a]+=1

Solución de clase:
def amigoRequests(self,n,restrictions,requests):
ans=[False]*len(requests)
dsu=DSU(n)
i,(u,v) en enumerado(requestas):
si dsu.find(u)=dsu.find(v):
as[i]=True; continue
dsu.union(u,v)
Ok=True
para a,b en restricciones:
si dsu.find(a)==dsu.find(b): ok=False; break
si no está bien:
dsu=DSU(n)
para j in range(i): dsu.union(*requests[j])
ans[i]=False
más: ans[i]=True
Retorno
`` `

#### 4.3 C++

``cpp
clase DSU{
vector significado p,r;
public:
DSU(int n){ p.resize(n); r.assign(n,0); iota(p.begin(),p.end(),0);}
int find(int x){ return p[x]=x?x:p[x]=find(p[x]);}
unite de vacío(int a,int b){
a=find(a); b=find(b);
si (a==b) cambio;
(r[a]cantar[b]) p[a]=b;
si (r[a] confíar[b]) p[b]=a;
[b]=a; r[a]++; }
}
};

Clase Solución{
public:
vector asignadobool amigoRequests(int n,
const vector armonizado:
const vector llevado a cabo
vector asignadobool confía ans(requests.size());
DSU dsu(n);
para(int i=0;i observado(int)requests.size();+i) {}
int u=requests[i][0],v=requests[i][1];
if(dsu.find(u)==dsu.find(v)){ ans[i]=true; continue; }
dsu.unite(u,v);
bool ok=true;
para(auto &p:restrictions)
if(dsu.find(p[0])==dsu.find(p[1]){ ok=false; break; }
si(!ok){ dsu=DSU(n);
for(int j=0;j obtenidosi;j++) dsu.unite(requests[j][0],requests[j][1]);
as[i]=false; }
ans[i]=true;
}
devolver los ans;
}
};
`` `

-...

## 5. Complejidad y rendimiento

Silencio Silencio Silencio Silencio
Silencio----------------
TENIDO `find` TENIDO O(α(n))
TENIDO `unión` TENIDO O(α(n))
Silencioso Escaneo de Restricción Silencioso O(r) por merge Silencioso O(r)
tención algoritmo completo Silencio O(q + r) · α(n)

Con **α(n) ≤ 4** incluso para `n = 106`, el algoritmo funciona en unos pocos milisegundos en hardware moderno.

-...

## 6. Corner‐Case Handling

← Intromisión esperada Comportamiento
Silencio...
Silencio Pareja restringida ya conectada ( " restricciones = [[0,1]] " , " solicitudes = [[0,1]] " Rechazo permanente: salida `false`. Silencio
← Duplicar peticiones Silencio Cada manejado independientemente; cheque ya conectado garantiza no trabajo extra. Silencio
Silencio No hay restricciones.Todas las solicitudes tienen éxito – DSU reduce al clásico gráfico de amigos. Silencio

-...

## 7. Optimizaciones para insumos más grandes

1. ** Hach-set de socios prohibidos** por componente.
2. En fusión, computar `intersección = partnersA ∩ partnersB`; si no vacía → rechazar.
3. Uso **Unión por Rank** + **Path Compression** para mantener la profundidad del árbol poco profunda.

-...

## 8. Trabajo-Entrevista Nuggets

- ** Explique el “por qué” antes del “cómo”**: Comience describiendo el gráfico de conectividad, luego traiga el DSU.
- **Retroceder**: Reconocer que la unión no es fácil de hacer; discutir las opciones de reconstrucción o nómada.
- Cambios en el espacio-tiempo**: Mostrar que puede cambiar de un escaneo de restricción lineal a un hash-set si aumentan las restricciones.
- **Testing**: Proveer pruebas de unidad para escenarios “ya conectados” y “violación de restricción”.

-...

## 9. Wrap‐Up

Ahora tienes:

- Una solución de ESD concisa y legible en tres idiomas principales**.
- Una explicación clara de cómo **respetar restricciones** mientras fusionan componentes.
- Puntos de conversación listos para la entrevista que demuestran **data‐structure mastery** y ** análisis de complejidad**.

¡Suelta este artículo en su cartera, utilízalo para impresionar a los gerentes de contratación, o simplemente por diversión – tus amigos te agradecerán por desmitificar un problema difícil de Leetcode!

-...

> **¡Feliz codificación y buena suerte en su próxima entrevista técnica!**

-...

*No dude en comentar a continuación o abrir una PR si observa mejoras. ¡Mantengamos la conversación algorítmica! *

-...

*Tags: #Leetcode #2076 #UnionFind #DisjointSetUnion #AlgorithmDesign #Java #Python #C++ #TechnicalInterview*

-...

¡Y eso es todo! Usted está listo para demostrar que puede **solve** y **explicar** el problema *Proceso Restricted Friend Solicita* como un profesional. ¡Feliz entrevista