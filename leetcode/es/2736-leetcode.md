-...
Título: LeetCode 2736. Consultas Máximas de Suma -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Por cada índice i `

`` `
punto i = (a1[i] , a2[i] 0 ≤ i
suma i = a1[i] + a2[i]
`` `

Para una consulta `(x, y)` necesitamos

`` `
suma máxima i con a1[i] ≥ x y a2[i] ≥ y
`` `

Si no existe tal índice, la respuesta es `-1`.

El problema es una pregunta de dominación bidimensional:

`` `
puntos : (a1[i] , a2[i]) valor : a1[i] + a2[i]
consultas : (x , y) – todos los puntos con x ≤ a1 y y ≤ a2
respuesta : valor máximo entre esos puntos
`` `

----------------------------------------------------

##### 1. Tratamiento sin trabas

`a1` and `a2` are up to `2·10^5`, therefore an
`O(n + q) log n)` algoritmo es requerido.

`` `
ordenar todos los índices por a1 (descendiente)
ordenar todas las consultas por x (descendiente)

mientras procesa las consultas:
añadir todos los puntos con a1 ≥ consulta actual. x
responder a la consulta con una estructura de datos que mantiene
la suma máxima de todos los puntos ya añadidos
con a2 ≥ consulta actual. Sí.
`` `

Cuando se insertan todos los puntos con `a1 ≥ x`,
sólo queda la restricción `a2 ≥ y`.
El problema restante es una dimensión
*range maximum* query over the `a2` values.



----------------------------------------------------

##### 2. Compresión de `a2`

Sólo se necesitan los valores de `a2' que realmente aparecen.

`` `
único_a2 = lista ordenada de todos los valores a2 distintos
index[a2] = posición de a2 dentro único_a2 (0 ... m-1)
`` `

`m = unique_a2.len()` - el número de diferentes valores `a2`.



----------------------------------------------------

##### 3. Árbol de segmento para máximo

Las tiendas de árboles de segmento para cada índice comprimido `a2`
suma máxima de todos los puntos insertados que tienen exactamente este `a2`.
Sólo se necesita el valor *maximum* dentro de un rango.

`` `
update(position , new_value) O(log m)
query( izquierda, derecha ) O(log m)
`` `

Todos los valores se inicializan con `-1`
(`-1` es menor que cualquier suma posible, por lo tanto representa
“no hay punto todavía”).

Para una consulta con el límite inferior 'y':

`` `
lb = primer índice con único_a2[lb] ≥ y
si lb == m → no a2 es suficientemente grande → respuesta -1
más → respuesta = query(lb , m-1)
`` `

El árbol ignora automáticamente todos los puntos cuyo `a2` es
más pequeño que el " y " solicitado.



----------------------------------------------------

##### 4. Prueba de corrección

Demostramos que el algoritmo imprime la suma máxima requerida
por cada consulta.

-...

##### Lemma 1
Durante el procesamiento de una consulta `q = (x, y) `
cada punto " p = (a1 , a2) " con " a1 ≥ x " se inserta en el
árbol de segmento, y no se inserta ningún punto con `a1  0 x`.

Proof.

Los puntos se clasifican en orden decreciente.
Un puntero se mueve sobre esta matriz.
Mientras que " se hicieron " y " puntos [pos].a1 ≥ x "
se inserta el punto y se aumenta.
En consecuencia, después del lazo

* todos los puntos con `a1 ≥ x` se insertan,
* no se han insertado todos los puntos con " a1 " . ∎



##### Lemma 2
Después de todas las inserciones para una consulta `q`,
el valor del árbol del segmento en la posición " k " equivale

`` `
max { a1[i] + a2[i] Silencio ya insertado y a2_index[i] = k }
`` `

Proof.

Cuando se inserta un punto,
`update(k , a1[i] + a2[i])` se ejecuta.
La actualización mantiene el máximo de todos los valores escritos para posicionar `k`,
por lo tanto después de procesar todos los puntos insertados el valor almacenado es
exactamente la suma máxima sobre todos ellos con ese `a2_index`. ∎



##### Lemma 3
Para una consulta `q = (x , y)` vamos
`lb = primer índice con único_a2[lb] ≥ tú.
`query(lb , m-1)` returns

`` `
max { a1[i] + a2[i] Silencio i insertado para q y a2[i] ≥ y }
`` `

Proof.

Por Lemma adultnbsp;1 solo se insertan puntos con `a1 ≥ x`.
Por Lemma adultnbsp;2 cada posición de árbol contiene la suma máxima entre
puntos insertados con este exacta `a2_index`.
La consulta pide el máximo sobre el rango `lb ... m-1`,
i.e. sobre todos los índices comprimidos cuyo valor real `a2` es al menos
Sí.
Ningún punto insertado con `a2 ' y ' contribuye a esta gama, por lo tanto
el valor devuelto equivale a la suma máxima entre todos los ya
insertar puntos que satisfagan ambas restricciones de la consulta. ∎



##### Lemma 4
`query(lb , m-1)` es `-1` si no hay puntos insertados satisfies `a2 ≥ y`.

Proof.

Si ningún punto insertado tiene `a2 ≥ y`,
cada posición de los árboles en el rango queried tiene valor `-1`
(Lemma limitadanbsp;2), por lo tanto el máximo sobre este rango es `-1`.
En cambio, si al menos un punto insertado tiene `a2 ≥ y`,
la posición del árbol correspondiente contiene un valor ≥ `0`,
por lo tanto el máximo de la gama deseada no es `-1`. ∎



##### Lemma 4 (continued)
Si `lb == m` el algoritmo sale `-1`,
de lo contrario produce la suma máxima de todos los puntos insertados con
`a2 ≥ y`.

Proof.

`lb == m` significa que no hay un índice comprimido cuyo real `a2`
valor es por lo menos `y`.
En consecuencia, ningún punto insertado puede satisfacer `a2 ≥ y`, por lo tanto
definición la respuesta es `-1`, que el algoritmo imprime.

Si `lb ecto m`, por Lemma bordenbsp;3 la consulta de los árboles del segmento devuelve la
suma máxima de todos los puntos insertados con `a2 ≥ y`. ∎



##### Lemma 5
Para una consulta `q = (x, y) `
cada índice 'i' que satisface las condiciones de la consulta
(`a1[i] ≥ x` y `a2[i] ≥ y`) se inserta antes de que la respuesta sea
computado.

Proof.

Directamente desde Lemma adultnbsp;1:
cada punto con `a1 ≥ x` se inserta antes de la respuesta,
y `a2[i] ≥ y` es manejado por la consulta de árboles. ∎



##### Lemma 6
Para una consulta `q = (x , y)` el algoritmo produce el máximo
suma posible sobre *todos* índices que satisfacen la consulta.

Proof.

Seamos el conjunto de todos los índices que satisfacen la consulta.
Por Lemma adultnbsp;5 todos los índices en `S` se insertan cuando la respuesta es
computado.
Por Lemma adultnbsp;4 el algoritmo devuelve la suma máxima entre
los índices insertados.
Debido a que el conjunto de índices insertados es exactamente `S`, el devuelto
valor iguala `max { a1[i] + a2[i] ANTERIED i ANTE S}`.
Si `S` está vacío el algoritmo sale `-1`. ∎



################################################################################################################################################################################################################################################################ Theorem
Para cada consulta el programa imprime la suma máxima requerida, y
`-1` si ningún índice satisface las limitaciones de la consulta.

Proof.

Directamente desde Lemma adultnbsp;6.



----------------------------------------------------

##### 5. Análisis de la complejidad

`` `
compresión de a2 : O(n log n)
clasificación de puntos > consultas : O(n log n + q log q)
actualizaciones de los árboles del segmento / ladrido : O(n + q) log n)
consumo de memoria : O(n + m) (m ≤ n)
`` `

El programa cumple los límites requeridos.



----------------------------------------------------

##### 6. Aplicación de las referencias (artículo 1.56)

``rust
use std::cmp::max;
use std::colecciones::HashMap;
use std::io::{self, Lea};

// Punto que se insertará en el árbol
#[derive(Clone)]
struct Point {}
a1: i64,
a2: i64,
}

// Consulta almacenada con su posición original
#[derive(Clone)]
struct Query {}
x: i64,
Y: i64,
id: usize,
}

// Árbol de segmento para rango máximo
struct SegTree {
tamaño: tamaño,
datos: Vec armonizado, //
}

impl SegTree {
fn new(n: usize) - Propiedad Yo
SegTree {}
tamaño: n,
datos: vec![-1; 4 * n + 4],
}
}

/// punto de actualización: árbol[idx] = max(tree[idx], val)
fn update(cadamut self, node: usize, l: usize, r: usize, idx: usize, val: i64) {
si l ==
si auto.data[nodo]
self.data[node] = val;
}
retorno;
}
(l + r) / 2;
si idx
self.update(node * 2, l, mid, idx, val);
. ♫ ... {
self.update(node * 2 + 1, mid + 1, r, idx, val);
}
self.data[node] = max(self.data[node * 2], self.data[node * 2 + 1]);
}

/// rango máximo en [ql, qr]
fn query( personalmente, nodo: usize, l: usize, r: usize, ql: usize, qr: usize) - título i64 {
si ql не не ный ный не не
retorno -1;
}
si ql se hizo= l ' círculo r
volver a sí mismo.data[nodo];
}
(l + r) / 2;
(nodo * 2, l, medio, ql, qr);
a la derecha = self.query(node * 2 + 1, mid + 1, r, ql, qr);
max(izquierda, derecha)
}
}

fn main() {}
/* ------------ leer todas las entradas----------
dejar que la mut ingrese = String::new();
io::stdin().read_to_string( entrada de componente).unwrap();
dejar que mut = input.split_whitespace().map( soportas sometidas s.parse:: woni64().unwrap());

n = it.next().unwrap() como usize;

dejar mut a1: Vec armonizado = Vec::with_capacity(n);
dejar mut a2: Vec armonizado = Vec::with_capacity(n);
para _ en 0. {}
a1.push(it.next().unwrap());
}
para _ en 0. {}
a2.push(it.next().unwrap());
}

q_cnt = it.next().unwrap() como usize;
Deja que las preguntas de la momia: Vec cumplióQuery confía = Vec:with_capacity(q_cnt);
para id en 0..q_cnt {}
x = it.next().unwrap();
let y = it.next().unwrap();
consultas. push(Query { x, y, id });
}

--------- compresión de a2 ---------- */
dejar mut unique_a2 = a2.clone();
unique_a2.sort_unstable();
unique_a2.dedup();
let m = unique_a2.len(); // number of different a2

dejar mut index_map: HashMap correspondientei64, usize confianza = HashMap::new();
para (i, & val) en unique_a2.iter().enumerate() {}
index_map.insert(val, i);
}

/*----------------------------
dejar los puntos de la muta: Vec Garantizado = Vec::with_capacity(n);
para mí en 0. {}
puntos. push(Point { a1: a1[i], a2: a2[i] });
}
puntos.sort_by(tenerp1, p2 vidas p2.a1.cmp( duplicap1.a1)); // descender a1

dejar que las consultas_ surtido = consultas.clone();
queries_sorted.sort_by( WordPressq1, q2 vidas q2.x.cmp( reducidaq1.x)); // descending x

--------- árbol del segmento...
dejar mut seg_tree = SegTree::new(m);

dejar que mut pos = 0usize; // siguiente punto que no se inserta
[-1i64; q_cnt];

para q en consultas_sorted.iter() {
/* insertar todos los puntos con a1 >= q.x */
mientras que se posan n " puntos cortos[pos].a1
dejar idx_a2 = *index_map.get( puntos [pos].a2).unwrap();
[pos].a1 + puntos[pos].a2;
seg_tree.update(1, 0, m - 1, idx_a2, sum);
pos += 1;
}

/* encontrar el límite inferior para y */
let lb = match unique_a2.binary_search(юq.y) {
Ok(idx) = título idx,
Err(idx) = confianza idx,
};

si Ib
let res = seg_tree.query(1, 0, m - 1, lb, m - 1);
respuesta[q.id] = res;
. ♫ ... {
respuesta[q.id] = -1;
}
}

/* ----------------------------
dejar que mut fuera = String::new();
para Val en respuesta {
out.push_str (format!("{}\n", val));
}
¡impresión!
}
`` `

El programa sigue exactamente el algoritmo probado correcto arriba
y es totalmente compatible con Rust 1.56.