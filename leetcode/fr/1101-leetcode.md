---
titre: LeetCode 1101. Le moment le plus tôt quand tout le monde devient ami -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Le moment le plus précoce où tout le monde devient ami – 1101 (LeetCode)

Langue Heure Espace
- C'est quoi ?
*Java * O(m log m)
O(m log m)
*C++ * O(m log m)

> **Key Insight** – Utilisez **Union‐Find (Disjoint‐Set Union)** pour fusionner les groupes d'amitié par ordre chronologique.
> Lorsque la taille du groupe qui contient un membre est égale à *n*, tout le monde est connecté.

> **Pourquoi l'union?**
> • Fusions rapides (temps `α(n)`)
> • Simple à maintenir le nombre de composants connectés
> • Parfait pour quand l'ensemble du réseau est-il connecté?

---

Déclaration de problème

> Il y a **n** personnes étiquetées `0 ... n‐1`.
> `logs[i] = [timestampi, xi, yi]` signifie qu'à l'époque `timestampi`, les gens `xi` et `yi` deviennent amis.
> L'amitié est transitive – si `a` est un ami de `b`, et `b` est un ami de `c`, alors `a` connaît `c`.
> **Retournez l'heure à laquelle chaque personne connaît toutes les autres personnes. **
> Si cela ne se produit jamais, retourner `-1`.

> **Constraints**
> * "2 ≤ n ≤ 100"
> * `1 ≤ longueur des billes ≤ 104 "
> * Tous les `timestampi` sont uniques et `0 ≤ timestampi ≤ 109 "
> * Chaque paire `(xi, yi)` apparaît au maximum une fois

---

Algorithme – Union-Find (Union des ensembles disjoints)

1. **Trier les journaux par horodatage** – nous devons traiter les amitiés chronologiquement.
2. **Initialiser un DSU** avec des nœuds `n`.
* `parent[i] = i "
* `size[i] = 1` (nombre de nœuds dans la composante)
3. **Processus de chaque journal** dans l'ordre trié:
* Union les deux personnes `x` et `y`.
* Après une union réussie (c.-à-d. qu'ils étaient auparavant dans différents composants), vérifiez si la taille du nouveau composant est égale à «n».
* Si oui, retournez le `timestamp' actuel.
4. Si la boucle se termine sans atteindre une taille de `n`, retourner `-1`.

---

Code Pseudo

«» "
trier(logs par horodatage)
dans le DSU(n)
pour chaque [t, x, y] dans les journaux:
si union(x, y):
si composantSize(x) == n:
retour t
retour -1
«» "

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Tri des logs **O(m log m)** (`m = logs.length`)
Les opérations de recherche de l'Union sont pratiquement constantes.
Total **O(m log m)**

Avec `n ≤ 100` et `m ≤ 104`, cela fonctionne en quelques millisecondes.

---

Cas et pièges

Numéro
C'est quoi ?
Dupliquer des amitiés ? Le problème garantit des paires uniques. Autres
Autres La paire déjà connectée?= `union` retourne `false`; pas de changement de taille. Autres
Autres Toutes les personnes déjà connectées avant n'importe quel log? Autres
Autres Très grands horodatages?= Utiliser 64 bits (`long` / `int64_t` / `int` en Python). Autres

---

Code – Java (Union-Find)

"Java
Importer java.util. Les tableaux;

solution de classe {
// -------- Le Mémorandum d'accord...
classe statique privée DSU {
Int[] parent;
taille int[];
DSU(int n) {
parent = nouveau int[n];
taille = nouvelle int[n];
pour (int i = 0; i < n; i++) {
parent[i] = i;
taille[i] = 1;
}
}
int find(int x) {
si (parent[x] != x) parent[x] = find(parent[x]); // compression du chemin
retour du parent[x];
}
// retourne true en cas de fusion
Union booléenne(int a, int b) {
int pa = find(a), pb = find(b);
si (pa == pb) retourner faux;
// union par taille
si (taille[pa] < taille[pb]) {
int tmp = pa; pa = pb; pb = tmp;
}
parent[pb] = pa;
taille[pa] += taille[pb];
retour vrai;
}
int compSize(int x) { taille de retour[find(x)]; }
}
// -------- solution...
public int leastAcq[][] grumes, int n) {
Trier par horodatage
les tableaux.sort(logs, a, b) -> Integer.compare(a[0], b[0]);
DSU dsu = nouveau DSU(n);
pour (int[] log : logs) {
t = log[0], x = log[1], y = log[2];
si (dsu.union(x, y) && dsu.compSize(x) == n) {
retour t; // tout le monde connecté
}
}
retour -1; // jamais complètement connecté
}
}
«» "

---

Code – Python (Union-Find)

'`python
de taper l'importation Liste

Classe DSU:
def __init_(self, n: int):
auto-parent = liste(range(n))
taille de soi = [1] * n

def find(self, x: int) -> Int:
si soi-même. parent[x] != x:
Self.parent[x] = self.find(self.parent[x]) # compression du chemin
Revenez vous-même. parent[x]

def union(self, a: int, b: int) -> C'est vrai.
p, pb = self.find(a), self.find(b)
si pa == pb: # déjà dans le même ensemble
Retour Faux
si self.size[pa] < self.size[pb]: # union par taille
pb = pb, pb
auto.parent[pb] = pa
Self.size[pa] += self.size[pb]
retour Vrai

def comp_size(self, x: int) -> Int:
retourner self.size[self.find(x)]

Solution de classe:
dès que Acq(self, logs: List[List[int]], n: int) -> Int:
logs.sort(key=lambda x: x[0]) # 1
dsu = DSU(n)
pour t, x, y dans les journaux:
si dsu.union(x, y) et dsu.comp_size(x) == n:
retour t
retour -1
«» "

---

Code – C++ (Union-Find)

'`cpp
#incluez <vecteur>
#incluez <algorithme>

classe DSU {
public:
DSU(int n) : parent(n), sz(n, 1) {
pour (int i = 0; i < n; ++i) parent[i] = i;
}
int find(int x) {
si (parent[x] != x) parent[x] = find(parent[x]); // compression du chemin
retour du parent[x];
}
bool unit(int a, int b) {
int pa = find(a), pb = find(b);
si (pa == pb) retourne false; // déjà connecté
si (sz[pa] < sz[pb]) md::swap(pa, pb); // union par taille
parent[pb] = pa;
sz[pa] += sz[pb];
retour vrai;
}
int compSize(int x) const { retour sz[find(x)]; }

particulier:
std::vector<int> parent, sz;
};

solution de classe {
public:
int le plus tôt Acq(std::vector<std::vector<int>>& Registres, int n) {
std::sort(logs.begin(), logs.end(),
[](suite::vector<int>& a,
(En milliers de dollars des États-Unis)
retourner a[0] < b[0];
}) ; //
DSU dsu(n);
pour (const auto& e : logs) {
t = e[0], x = e[1], y = e[2];
si (dsu.unite(x, y) && dsu.compSize(x) == n)
retour t; // tous connectés
}
retour -1; // jamais complètement connecté
}
};
«» "

---

Alternative – Profondeur – Première recherche (DFS)

Si vous préférez une approche plus «brute‐force» :

1. **Construisez une liste d'adjacence** à partir des journaux au fur et à mesure.
2. Après chaque union, ** lancez un DFS** de n'importe quel membre pour compter le nombre de nœuds accessibles.
3. Lorsque ce nombre est égal à `n`, retournez l'horodatage.

> **Pourquoi ne pas utiliser le DFS? **
> * Plus facile à comprendre pour les débutants
> * Complexité temporelle: O(m·n) dans le pire des cas – encore bon pour les contraintes données
> * La version DSU est plus propre pour les intervieweurs et les échelles à plus grande `n`

---

Point d'entrevue

- ** Expliquez la transition** tôt – beaucoup de candidats l'oublient.
- **Afficher clairement l'aide du DSU**: `find`, `unite`, `size`.
- ** Tri de mentions** – un getcha commun qui fait la solution O(m log m) au lieu de O(m).
- **Parler de la compression du chemin et de l'union par taille** – les intervieweurs apprécient la nuance.
- ** Expliquez pourquoi vous retournez après une union réussie** – pas toutes les «union» ne changent la taille de la composante.

> **Tip STAR** – *En fusionnant des groupes d'amitié, j'ai utilisé Union-Find pour que chaque syndicat prenne un temps presque constant. Dès que la taille du composant atteint n, je sais que tout le monde est connecté. J'ai trié les logs par horodatage pour garder l'invariant chronologique.

---

## -Offre d'entrevue

1. **DSU est une balle magique** pour les problèmes de connectivité dans le temps.
2. ** Conserver la taille du composant** à l'intérieur du DSU; sinon vous auriez besoin d'un compteur séparé.
3. **Éviter O(n2) DFS après chaque log** – le DSU est des ordres de grandeur plus rapides.
4. **Show clean code** – noms de variables comme `parent`, `size`, `union`/`unite`, `find`.
5. **Manipulation des bords de mention** (paires dupliquées, paires déjà connectées) – fait preuve de robustesse.

> **Si vous réussissez ce problème, vous acquerrez le segment "connectivity" dans presque n'importe quel entretien de conception de systèmes ou de structures de données.**

---

La pensée finale

> Le moment le plus précoce où tout le monde devient ami est un problème de manuel Union-Trouver.
> Maître le modèle DSU et vous serez prêt pour toute entrevue qui demande *=quand ce graphique est-il devenu connecté?
> Et la meilleure partie ? La solution n'est que quelques lignes de code – parfait pour votre portefeuille LeetCode et votre prochaine recherche d'emploi! C'est ce qu'il a dit.

Bon codage, et bonne chance d'atterrissage ce rôle de technologie de rêve!