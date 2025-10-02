---
titre: LeetCode 2736. Demande de somme maximale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour chaque indice ` Les "

«» "
point i = (a1[i], a2[i]) 0 ≤ i < n
somme i = a1[i] + a2[i]
«» "

Pour une requête `(x , y)` nous avons besoin

«» "
somme maximale i avec a1[i] ≥ x et a2[i] ≥ y
«» "

Si aucun indice n'existe, la réponse est `-1`.

Le problème est une question de domination bidimensionnelle:

«» "
points : (a1[i] , a2[i]) valeur : a1[i] + a2[i]
requête : (x , y) – tous les points avec x ≤ a1 et y ≤ a2
réponse : valeur maximale parmi ces points
«» "

-----------------------------------------------------------------------------------

C'est vrai. 1. Traitement hors ligne

«a1» et «a2» sont jusqu'à «2·10^5»,
Un algorithme `O(n + q) log n)` est nécessaire.

«» "
trier tous les indices par a1 (descendant)
trier toutes les requêtes par x (descendant)

lors du traitement des requêtes:
ajouter tous les points avec a1 ≥ requête courante. x
répondre à la requête avec une structure de données qui maintient
la somme maximale de tous les points déjà ajoutés
avec a2 ≥ requête courante. y
«» "

Lorsque tous les points avec `a1 ≥ x` sont insérés,
seule la restriction `a2 ≥ y` reste.
Le problème restant est un problème unidimensionnel
*range au maximum* sur les valeurs `a2`.



-----------------------------------------------------------------------------------

C'est vrai. 2. Compression de `a2`

Seules les valeurs de `a2` qui apparaissent réellement sont nécessaires.

«» "
unique_a2 = liste triée de toutes les valeurs a2 distinctes
indice[a2] = position de a2 à l'intérieur d'un_a2 unique (0 ... m-1)
«» "

`m = unique_a2.len()` – le nombre de différentes valeurs `a2`.



-----------------------------------------------------------------------------------

C'est vrai. 3. Arbre de segment pour le maximum

L'arbre segment stocke pour chaque indice comprimé `a2`
la somme maximale de tous les points insérés qui ont exactement cette «a2».
Seule la valeur *maximum* à l'intérieur d'une plage est nécessaire.

«» "
update(position , nouvelle_valeur) O(log m)
requête( gauche , droite ) O(log m)
«» "

Toutes les valeurs sont initiales avec `-1`
«-1 » est inférieur à chaque somme possible, par conséquent, il représente
Pas encore de point.

Pour une requête avec limite inférieure `y`:

«» "
lb = premier indice avec un_a2[lb] ≥ y
si lb == m → no a2 est assez grand → réponse -1
autre → réponse = requête(lb , m-1)
«» "

L'arbre ignore automatiquement tous les points dont `a2` est
plus petit que le « y » demandé.



-----------------------------------------------------------------------------------

C'est vrai. 4. Preuve d ' exactitude

Nous prouvons que l'algorithme imprime la somme maximale requise
pour chaque requête.

---

Lemma 1
Lors du traitement d'une requête `q = (x , y) "
chaque point `p = (a1 , a2)` avec `a1 ≥ x` est inséré dans le
arbre de segment, et aucun point avec `a1 < x` est inséré.

**Prof.**

Les points sont classés par ordre décroissant `a1`.
Un pointeur `pos` se déplace sur ce tableau.
Bien que `pos < n` et `points[pos].a1 ≥ x`
le point est inséré et `pos` est augmenté.
Par conséquent, après la boucle de temps

* tous les points avec `a1 ≥ x` sont insérés,
* tous les points avec `a1 < x` ne sont toujours pas insérés. *



Lemma 2
Après toutes les insertions pour une requête `q`,
la valeur de l'arborescence du segment à la position `k` est égale

«» "
max { a1[i] + a2[i]=1 i déjà inséré et a2_index[i] = k }
«» "

**Prof.**

Lorsqu'un point `i` est inséré,
`update(k , a1[i] + a2[i])` est exécuté.
La mise à jour conserve le maximum de toutes les valeurs écrites à la position `k`,
la valeur stockée est
exactement la somme maximale sur tous avec ce `a2_index`. *



Lemma 3
Pour une requête `q = (x , y)`
`lb = premier indice avec unique_a2[lb] ≥ y'.
retour `query(lb , m-1)`

«» "
max { a1[i] + a2[i]- i inséré pour q et a2[i] ≥ y }
«» "

**Prof.**

Par Lemma 1 seuls les points avec `a1 ≥ x` sont insérés.
Par Lemma 2 chaque position d'arbre contient la somme maximale entre
des points insérés avec cette `a2_index` exacte.
La requête demande le maximum sur la plage `lb ... m-1`,
i.e. sur tous les indices compressés dont la valeur réelle `a2` est au moins
'y'.
Aucun point inséré avec `a2 < y` ne contribue à cette plage, donc
la valeur retournée est égale à la somme maximale entre tous déjà
inséré des points satisfaisant aux deux restrictions de la requête. *



Lemma 4
`query(lb , m-1)` est `-1` si aucun point inséré ne satisfait `a2 ≥ y`.

**Prof.**

Si aucun point inséré n'a «a2 ≥ y»,
chaque position de l'arbre dans la plage demandée a une valeur `-1`
(Lemma 2), donc le maximum sur cette plage est `-1`.
Inversement, si au moins un point inséré a «a2 ≥ y»,
la position de l'arbre correspondant contient une valeur ≥ `0`,
Par conséquent, le maximum de l'intervalle demandé n'est pas "-1". *



Lemma 4 (suite)
Si `lb == m` l`algorithme produit «-1»,
sinon, il produit la somme maximale de tous les points insérés avec
«a2 ≥ y».

**Prof.**

"lb" m` signifie qu`il n`y a pas d`indice compressé dont le vrai `a2`
valeur est au moins "y".
Par conséquent, aucun point inséré ne peut satisfaire «a2 ≥ y», d'où
définition la réponse est `-1`, que l'algorithme imprime.

Si `lb < m`, par Lemma 3, l'arborescence du segment retourne la requête
somme maximale de tous les points insérés avec `a2 ≥ y`.



Lemma 5
Pour une requête `q = (x , y) "
chaque index `i` qui satisfait aux conditions de requête
(«a1[i] ≥ x» et «a2[i] ≥ y») est inséré avant que la réponse soit
calculé.

**Prof.**

Directement de Lemma 1:
chaque point avec `a1 ≥ x` est inséré avant la réponse,
et `a2[i] ≥ y` est géré par la requête arborescente. *



Lemma 6
Pour une requête `q = (x , y)` l'algorithme produit le maximum
somme possible sur *tous* indices qui satisfont à la requête.

**Prof.**

Laissez `S` être l'ensemble de tous les indices satisfaisant la requête.
Par Lemma 5 tous les indices dans `S` sont insérés lorsque la réponse est
calculé.
Par Lemma 4 l'algorithme renvoie la somme maximale entre
les indices insérés.
Parce que l'ensemble des indices insérés est exactement `S`, le retour
la valeur est égale à `max { a1[i] + a2[i]=" i S }`.
Si `S` est vide, les sorties de l'algorithme `-1`.



C'est vrai. Théorème
Pour chaque requête, le programme imprime la somme maximale requise, et
`-1` si aucun index ne satisfait aux contraintes de la requête.

**Prof.**

Directement de Lemma 6.



-----------------------------------------------------------------------------------

C'est vrai. 5. Analyse de la complexité

«» "
compression de a2 : O(n log n)
points de tri & requêtes : O(n log n + q log q)
Mises à jour/requête du segment arborescent : O(n + q) log n)
Consommation de mémoire : O(n + m) (m ≤ n)
«» "

Le programme remplit les limites requises.



-----------------------------------------------------------------------------------

C'est vrai. 6. Mise en œuvre des références (Rust 1.56)

"``rouille
utiliser md::cmp::max;
utiliser std::collections::HashMap;
utiliser std::io::{self, Lire};

/// Point qui sera inséré dans l'arbre
#[derive(Clone)]
struct Point {
a1: i64,
a2: i64,
}

/// Demande stockée avec sa position d'origine
#[derive(Clone)]
struct Query {
x: i64,
Y: i64,
id: usize,
}

/// Arbre de segment pour la portée maximale
struct SegTree {
taille: usize,
données: Vec<i64>, //
}

pour SegTree {
fn nouveau(n: usize) -> Moi-même {
Légèreté {
taille: n,
données: vec![-1; 4 * n + 4],
}
}

/// mise à jour point: arborescence[idx] = max(tree[idx], val)
fn update(&mut self, node: usize, l: usize, r: usize, idx: usize, val: i64) {
si l == r {
si self.data[node] < val {
auto.données[node] = valeur;
}
retour;
}
laisser mi = (l + r) / 2;
si idx <= milieu {
self.update(node * 2, l, mi, idx, val);
} autre {
auto.mise à jour(noeud * 2 + 1, milieu + 1, r, idx, val);
}
auto.data[node] = max(self.data[node * 2], auto.data[node * 2 + 1]);
}

/// plage maximale sur [ql, qr]
fn requête(&self, noeud: usize, l: usize, r: usize, ql: usize, qr: usize) -> i64 {
si ql > r.
retour -1;
}
si ql <= l && r <= qr {
retourner self.data[node];
}
laisser mi = (l + r) / 2;
gauche = auto.query(node * 2, l, milieu, ql, qr);
let right = auto.query(node * 2 + 1, milieu + 1, r, ql, qr);
max (gauche, droite)
}
}

fn principal() {
/* --------- lire toutes les entrées --------- */
que mut input = chaîne::new();
io::stdin().read_to_string(&mut input).unwrap();
laisser mut it = input.split_whitespace().map(=s= s.parse::<i64>(=).unwrap());

let n = it.next().unwrap() comme usize;

Let mut a1: Vec<i64> = Vec::with_acability(n);
let mut a2: Vec<i64> = Vec::with_acability(n);
pour _ dans 0..n {
a1.push(it.next().unwrap());
}
pour _ dans 0..n {
a2.push(it.next().unwrap());
}

q_cnt = it.next().unwrap() comme usize;
laissez les requêtes mut : Vec<Query> = Vec::avec_capacité(q_cnt);
pour id dans 0..q_cnt {
x = it.next().unwrap();
laisser y = it.next().unwrap();
questions. Pousser (Query { x, y, id });
}

- Oui. compression de a2 --------- */
laissez mut unique_a2 = a2.clone();
unique_a2.sort_unstable();
unique_a2.dedup();
let m = unique_a2.len(); // nombre de différents a2

let mut index_map: HashMap<i64, usize> = HashMap::new();
pour (i, &val) dans unique_a2.iter().énumérer() {
index_map.insert(val, i);
}

/* ---------- trier les points et les questions -------- */
Let mut points: Vec<Point> = Vec::with_acability(n);
pour i en 0..n {
des points. Pousser(Point { a1: a1[i], a2: a2[i]});
}
points.sort_by(-), p2.a1.cmp(&p1.a1)); // descendant a1

laissez mut requests_sorted = requests.clone();
requête_sorted.sort_by(-), q2.x.cmp(--q1.x)); // descendant x

- Oui. arbre de segment -------- */
que mut seg_tree = SegTree::new(m);

laisser mut pos = 0usize; // point suivant qui n'est pas inséré
que mut reponse = vec![-1i64; q_cnt];

pour q dans requêtes_sorted.iter() {
/* insérer tous les points avec a1 >= q.x */
alors que pos < n& points[pos].a1 >= q.x {
idx_a2 = *index_map.get(&points[pos].a2).unwrap();
la somme = points[pos].a1 + points[pos].a2;
seg_tree.update(1, 0, m - 1, idx_a2, somme);
pos += 1;
}

/* trouver la limite inférieure pour y */
let lb = match unique_a2.binary_search(&q.y) {
Ok(idx) => idx,
Err(idx) => idx,
};

si lb < m {
let res = seg_tree.query(1, 0, m - 1, lb, m - 1);
réponse[q.id] = res;
} autre {
réponse[q.id] = -1;
}
}

Produit
laisser mut out = Chaîne::new();
pour la valeur en réponse {
out.push_str(&format!("{}\n", val));
}
imprimer!
}
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus
et est entièrement compatible avec Rust 1.56.