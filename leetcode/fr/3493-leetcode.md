---
titre: LeetCode 3493. Graphique des propriétés -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solutions en trois langues

Voici les solutions **ready‐to-copy** pour le LeetCode 3493 – Graphique des propriétés.
Ils utilisent tous la même idée:

1. **Construisez un jeu de bits (ou de hachage) pour chaque ligne** afin de pouvoir compter les éléments communs dans *O(1)* (ou *O(m*).
2. **Union‐Find (Disjoint‐Set Union, DSU)** suit les composants connectés.
3. Pour chaque paire `(i , j)` nous fusionnons les deux nœuds si leur intersection ≥ `k`.
4. Comptez enfin combien de racines uniques existent – c'est la réponse.

Les implémentations ci-dessous suivent les contraintes (`n , m ≤ 100`, valeurs ≤ 100) et sont fortement commentées afin que vous puissiez les coller directement dans LeetCode.

---

#### 1.1 Java – + DSU

"Java
Importer java.util. BitSet;

classe DSU {
Int[] parent, grade;

DSU(int n) {
parent = nouveau int[n];
rang = nouvelle int[n];
pour (int i = 0; i < n; i++) parent[i] = i;
}

int find(int x) {
si (parent[x] != x) parent[x] = find(parent[x]); // compression du chemin
retour du parent[x];
}

Union nulle(int a, int b) {
int ra = find(a), rb = find(b);
si (ra == rb) retour;
si (rank[ra] < rank[rb]) parent[ra] = rb;
sinon si (rank[ra] > rank[rb]) parent[rb] = ra;
Autre { parent[rb] = ra; rang[ra]++; }
}
}

solution de classe publique {
numéro d'entrée publicOfComponents(int[][] prop, int k) {
int n = longueur prop.;
// 101 suffit: les valeurs sont en [1, 100]
BitSet[] lignes = nouveau BitSet[n];

// Étape 1 – transformer chaque ligne en un BitSet
pour (int i = 0; i < n; i++) {
lignes[i] = nouveau BitSet(101);
pour (int val : prop[i]) lignes[i].set(val);
}

DSU dsu = nouveau DSU(n);

// Étape 2 – examiner chaque paire non ordonnée
pour (int i = 0; i < n; i++) {
pour (int j = i + 1; j < n; j++) {
// Comptez rapidement les intérêts communs :
BitSet tmp = (BitSet) lignes[i].clone();
tmp.and(rows[j]); //
si (tmp.cardinality() >= k) { // si ≥ k fusion
dsu.union(i, j);
}
}
}

// Étape 3 – compter les racines distinctes
Int comps = 0;
pour (int i = 0; i < n; i++)
si [dsu.find(i)] i) comps++;
les comptes de retour;
}
}
«» "

> **Pourquoi BitSet?**
> - Toutes les valeurs sont ≤ 100 → 101 bits → un Java `BitSet` correspond à un mot machine.
> - `cardinality()` est un popcount natif; l'intersection est `O(1)`.

---

#### 1.2 Python – Intersection + DSU

'`python
Classe DSU:
def __init_(self, n):
auto-parent = liste(range(n))
Self.rank = [0] * n

def find(self, x):
si soi-même. parent[x] != x:
Self.parent[x] = self.find(self.parent[x]) # compression du chemin
Revenez vous-même. parent[x]

def union(self, a, b):
ra, rb = self.find(a), self.find(b)
si rb: retour
si self.rank[ra] < self.rank[rb]:
auto-parent[ra] = rb
elif self.rank[ra] > self.rank[rb]:
auto.parent[rb] = r
Sinon:
auto.parent[rb] = r
Self.rank[ra] += 1

Solution de classe:
def numberOfComponents(self, prop: List[List[int]], k: int) -> Int:
n = len(prop)
# Convertissez chaque ligne en un *set* – l'intersection de set est O(min(-)
lignes = [set(row) pour la ligne de prop]

dsu = DSU(n)

pour i dans la plage(n):
pour j dans la plage(i + 1, n):
commun = len(rows[i] & rows[j]) # set intersection
si fréquent >= k:
dsu.union(i, j)

# Compter des racines distinctes
racines = {dsu.find(i) pour i dans l'intervalle(n)}
retour len(racines)
«» "

> **Pourquoi un "set"?**
> Les valeurs sont minuscules, de sorte que le dessus d'un `BitSet` est inutile en Python.
> L'intersection `set` est propre, facile à lire et assez rapide pour `n ≤ 100`.

---

### 1.3 C++ – ─`std::bitset` + DSU

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe DSU {
public:
vecteur <int> parent, grade;
DSU(int n) : parent(n), rang(n,0) {
(parent.begin(), parent.end(), 0);
}
int find(int x) {
si (parent[x] != x) parent[x] = find(parent[x]); // compression du chemin
retour du parent[x];
}
vide unit(int a, int b) {
int ra = find(a), rb = find(b);
si (ra == rb) retour;
si (rank[ra] < rank[rb]) parent[ra] = rb;
sinon si (rank[ra] > rank[rb]) parent[rb] = ra;
Autre { parent[rb] = ra; ++rank[ra]; }
}
};

solution de classe {
public:
nombre intOfComponents(vecteur<vecteur<int>>&prop, int k) {
int n = prop.size();
// 101 bits suffisent – les valeurs sont 1..100
vecteur<bitset<128>> lignes(n);
pour (int i = 0; i < n; ++i)
pour (int v : prop[i]) lignes[i].set(v);

DSU dsu(n);

pour (int i = 0; i < n; ++i)
pour (int j = i + 1; j < n; ++j) {
int commun = (rows[i] & rows[j]).count(); // popcount
i (commun >= k) dsu.unite(i, j);
}

// Compter les racines distinctes
Int comps = 0;
pour (int i = 0; i < n; ++i)
si [dsu.find(i)] i) ++comps;
les comptes de retour;
}
};
«» "

> **Pourquoi `bitset<128>`? **
> - 128 bits supportent confortablement les 100 valeurs possibles.
> - `operator&` et `count()` sont mis en œuvre dans le matériel (poids de hamming), donnant *O(1)* par paire.

---

- Oui. 2. Le bien, le mal et le mal

**Aspect**
C'est pas vrai.
**La clarté conceptuelle**Le syndicat-Find est une base d'entrevue classique. Il peut être difficile de compter les intersections naïvement. L'oubli de l'unité des éléments (duplicata) conduit à de mauvaises réponses. Autres
**Simplicité de la mise en oeuvre**=DSU + BitSet/Set est une logique de 5 lignes. L'intersection Python set est une seule ligne de code. L'utilisation de tableaux bruts et de popcount manuel peut être sujette à erreur. Autres
**Performance **Les opérations de bit donnent *O(n2)* avec une petite constante. "Python"s `set.intersection` est `O(m)` mais toujours < 106 opérations pour les contraintes. Les boucles manuelles de plus de 100 numéros par paire sont parfaitement fines mais plus difficiles à lire. Autres
**Readability** Les ensembles de pythons sont presque explicites. C++ `bitset<128>` peut se sentir un peu faible pour les nouveaux arrivants. Autres
Autres **Les cas d'Edge**Les valeurs en dehors de 1–100 briseraient la logique de jeu de bits – garder avec les vérifications. Les duplicata dans une rangée sont inoffensifs parce que nous utilisons `set`. Autres

> **Ligne de bottom:**
> Le *good* est un algorithme rapide et propre.
> Le *mauvais* est la tentation d'écrire une routine d'intersection lourde.
> Le *ugly* manque d'optimisations DSU (compression de chemin, union par rang), qui peut transformer une solution *O(n2 α(n)* en solution lente sur des entrées plus grandes.

---

- Oui. 3. SEO-Optimized Blog Post

> **Titre**
> ** Graphique des propriétés : Comptage des composants connectés avec le DSU – Le bon, le mauvais et le mauvais**

> **Description détaillée* *
> Master LeetCodeS de l'entreprise Graphique des propriétés avec une solution Union-Find prête à l'entrevue. Apprenez à optimiser les nombres d'intersections avec des bits, à dépanner des pièges communs et à passer votre prochaine entrevue de codage.

> ** Mots-clés principaux* *
> `LeetCode 3493`, `properties graph`, `union find`, `DSU algorithme`, `question d'entrevue`, `job interview coding`, `algorithm interview prep`, `data structure`, `graph theory`, `C++ bitset`, `Java BitSet`, `Python set intersection "

> ** Mots-clés secondaires* *
> `entretien de codage`, `entretien de génie logiciel`, `embauche de technologie`, ` résolution de problèmes algorithmiques`, ` connectivité graphique "

---

Introduction

> Dans les interviews technologiques modernes, les problèmes de LeetCode qui mélangent *graphes* et *structures de données* sont des mines d'or pour montrer la pensée algorithmique.
> LeetCode 3493 – *Propriétés Graph* – vous demande de modéliser les profils d'utilisateurs comme des nœuds, de les lier lorsqu'ils partagent suffisamment d'intérêts, et de compter combien de cercles d'amis indépendants existent.
> Ci-dessous, nous disséquons le problème, montrons une solution optimale et vous donnons une feuille de triche rapide pour la journée d'entrevue.

---

Récapitulation du problème

- **Input**
`prop` – une matrice entière `n × m` (`1 ≤ n, m ≤ 100`, valeurs ≤ 100).
`k` – le nombre minimum d'attributs *common* requis pour connecter deux lignes.
- **Bâtiment de base**
Nœuds: `0 ... n‐1`.
Le bord `(i, j)` existe sif `=prop[i]==prop[j]= ≥ k`.
- **Objectif**
Retourner le nombre de composants connectés dans ce graphique non dirigé.

---

- Oui. Pourquoi Union-Find?

1. **Natural  fit pour "merge" si connecté** – une fois que nous voyons un bord, nous rejoignons deux composants.
2. **Temps amorti `α(n)` (inverse Ackermann)** – pratiquement constant pour les tailles d'entrée pratiques.
3. ** Compétence d'entrevue classique** – Les recruteurs vous demandent souvent d'expliquer le DSU; avoir une solution de travail démontre la profondeur.

---

Nombre optimal d'intersections

L'approche naïve balayait les deux lignes pour chaque paire, coûtant `O(n2 m)`.
Compte tenu de la petite plage de valeurs, nous pouvons faire mieux :

**Langue******Technique****Explication**
- C'est quoi ?
**C++ / Java**="std::bitset` / `BitSet`=" Représenter chaque ligne comme une masque de 101 bits. L'intersection est un peu sage ET, la cardinalité un popcount. Autres
**Les ensembles de hachage intégrés de Python donnent un excellent comportement à temps constant pour les petits ensembles. Autres

> **Astuce**: Dans Python, si vous voulez une vitesse maximale et que vous savez que `m` est grand, vous pouvez toujours utiliser `array('I')` et bit-pack les valeurs.

---

### Une solution complète (C++)

'`cpp
vecteur<bitset<128>> lignes(n);
pour (int i=0;i<n;i++)
pour (int v: prop[i]) lignes[i].set(v); // set bit v

DSU dsu(n);
pour (int i=0;i<n;i++)
pour (int j=i+1;j<n;j++) {
si ((rows[i] & rows[j]).count() >= k)
dsu.unite(i,j);
}
«» "

- **`rows[i] & rows[j]`** – intersection accélérée du matériel.
- **'.count()'** – popcount; O(1).
- **DSU** – la compression du chemin + l'union par rang garantit un comportement presque linéaire.

---

### Pièges communs et comment les éviter

**Pitfall**
C'est pas vrai.
**Les attributs dupliqués dans une ligne**=L'intersection des comptes excédentaires=La conversion de chaque ligne en un *set* (Python) ou l'utilisation de `BitSet` (les duplicatas n'ont pas d'importance). Autres
**Zero-indexed vs one-indexed values**. Autres
**Missing DSU grade**= O(n2) pire-cas sur les mauvais intrants== Toujours mettre en œuvre l'union par rang ou taille. Autres
**Utiliser les boucles lentes**= Timeouts sur des tests plus importants= Remplacer `pour` boucles de plus de 100 valeurs par une intersection bitset ou une intersection définie. Autres

---

Entretien rapide Cheat- Feuille

- ** Structures de données à mentionner**
- "UnionFind (DSU)"
- `BitSet` (Java/C++) ou `set` (Python)
- **Complexité temporelle**
`O(n2)` bords *popcount* → ~104 opérations pour `n=100`.
- **Complexité spatiale**
`O(n)` pour le DSU + `O(n * bitset)` .
- **Note de cas**
- Une matrice vide ? Retour `0`.
- "k" 0` → chaque nœud connecté → 1 composant.

---

La pensée finale

> Maîtriser *Propriétés Graphique* signifie maîtriser la synergie entre *connectivité graphique* et *combinaison efficace*.
> Si vous pouvez expliquer cette solution en moins de 5 minutes et la coder parfaitement, vous impressionnerez les intervieweurs à travers le spectre technologique – des startups à Fortune 500.

---

FAQ

**Q1. Peut J'utilise la récursion dans DSU `find`?* *
- Oui. Dans les entrevues, une approche itérative est plus sûre – évite le débordement de la pile sur une récursion profonde.

**Q2. Pourquoi ne pas utiliser BFS/DFS? **
- BFS/DFS fonctionnerait, mais vous devriez d'abord construire tous les bords.
- DSU fusionne à la volée et utilise *O(n)* mémoire, tandis que DFS utiliserait `O(n + bords)`.

**Q3. Et si `k` est grand, disons 50? **
- Oui. L'algorithme fonctionne toujours; les nombres d'intersections réduisent naturellement le nombre de syndicats.

---

À emporter

> Le problème de graphique de propriétés est une excellente vitrine de la puissance de DSU.
> En utilisant des intersections à base de bits, vous garantissez une solution rapide qui s'écaille confortablement.
> La prochaine fois que vous aurez posé une question sur les profils de connexion, rappelez-vous : **merger si connecté → DSU**.

---

**Codage heureux, et que votre entrevue soit remplie d'algorithmes propres et de zéro bugs !* *

---

* Fin du poste*

---

> **Sentez libres de copier les extraits de code ci-dessus** – ils sont prêts à coller dans LeetCode, Codeforces, ou votre IDE local. Bonne chance pour votre prochain entretien !