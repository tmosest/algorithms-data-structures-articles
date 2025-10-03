---
Titre: LeetCode 3535. Conversion d'unité II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3535. Conversion d'unité II – Un guide complet, optimisé par le SEO (Java / Python / C++)

> Lorsque vous résolvez un problème une fois, vous êtes prêt pour mille autres.

Cet article passe par le problème **Unit Conversion II** de LeetCode, donne une implémentation de travail dans **Java, Python, et C++**, puis plonge dans le *bon, le mauvais et le laid* de la solution. Le post est écrit pour la préparation des interviews **software-engineering** et est entièrement optimisé pour les mots clés **Unit Conversion II, LeetCode, entretien d'emploi, DFS, BFS, Java, Python, C++**.

---

- Oui. 1. Récapitulation des problèmes

«» "
Il y a n types d'unités (0 ... n‐1).
conversions[i] = [source, cible, facteur] → 1 unité de Source=unités de Facteur de Cible=.
requêtes[i] = [Ai, Bi] → combien de Bi-unités sont égales à 1 Ai-unité? Répondre comme (p / q) mod 1e9+7.
«» "

* `1 <= facteur <= 1e9`
* `1 <= n, q <= 1e5`
* Le graphique est un arbre (exactement les bords `n‐1`) et chaque unité est accessible à partir de l'unité 0.

La réponse requise pour chaque requête est :

«» "
réponse[i] = (facteur de Bi par rapport à Ai) mod MOD
= (numérateur * inv(dénominateur)) mod MOD
«» "

où `inv(x)` est le module inverse modulaire `MOD = 1_000_000_007`.

---

- Oui. 2. Observations

1. ** Structure de l'arbre** – il y a exactement un chemin simple entre deux unités.
2. **Chaîne multiplicative** – passer de `u` à `v` multiplie le facteur de conversion de chaque bord sur le chemin.
3. ** Direction inverse** – si le bord `u → v` a le facteur `c`, alors `v → u` a le facteur `1 / c`.
Dans l'arithmétique modulaire nous stockons `c` et son inverse modulaire `c−1`.
4. Une fois que nous connaissons le facteur cumulatif de la racine (unité 0) à *chaque noeud*, nous pouvons répondre à n'importe quelle requête dans `O(1)`:

«» "
facteur(Ai → Bi) = (facteur(0 → Bi)) * inv(facteur(0 → Ai))
«» "

Le problème se réduit donc à un seul DFS/BFS** qui propage deux valeurs pour chaque noeud :
* "à Root[u]" – produit de facteurs de bord de la racine à « u ».
* `invToRoot[u]` – produit de bord inverse de la racine à « u ».

---

- Oui. 3. Algorithme (version FDS)

«» "
créer une liste d'adjacence :
pour chaque bord (a,b,c):
ajouter b, c, c à 1) à a
ajouter (a, c−1, c) à b

DFS(0):
pour Root[0] = 1
invToRoot[0] = 1
pile/récursion:
pour chaque voisin (v, facteur, invFactor):
si elle n'est pas visitée:
toRoot[v] = toRoot[u] * facteur % MOD
invToRoot[v] = invToRoot[u] * invFactor % MOD
DFS(v)

répondre aux questions :
res = (toRoot[Bi] * invToRoot[Ai]) % MOD
«» "

**Complexité temporelle** – 'O(n + q) "
**Complexité spatiale** – «O(n)»

La seule opération lourde est une exponentiation modulaire utilisée une fois par bord pour calculer l'inverse `c−1` (`pow(c, MOD-2`), qui est `O(log MOD)` mais fait `n‐1` fois.

---

- Oui. 4. Code

### 4.1 Java (DFS)

"Java
Importation de java.util.*;

solution de classe {
finale statique privée longue MOD = 1_000_000_007L;

public int[] requêteConversions(int[][] conversions, int[] requêtes) {
int n = conversions.longueur + 1;
Liste <long[]>[] adj = nouvelle grille[n];
pour (int i = 0; i < n; i++) adj[i] = nouvelle liste de distribution<>();

// Graphique de construction
pour (int[] e : conversions) {
int a = e[0], b = e[1];
long c = e[2];
long inv = modPow(c, MOD - 2);
adj[a].add(nouveau long[]{b, c, inv}); // a -> b
adj[b].add(nouveau long[]{a, inv, c}); // b -> a
}

long[] toRoot = nouveau long[n];
long[] invToRoot = nouveau long[n];
booléen[] vis = nouveau booléen[n];
àRoot[0] = invToRoot[0] = 1;
dfs(0, adj, toRoot, invToRoot, vis);

int[] res = nouvelle int[queries.longueur];
pour (int i = 0; i < requêtes.longueur; i++) {
int a = requêtes[i][0];
int b = requêtes[i][1];
res[i] = (int) (toRoot[b] * invToRoot[a] % MOD);
}
retour rés;
}

vide privé dfs(int u, Liste<long[]>[] adj,
long[] toRoot, long[] invToRoot, booléen[] vis) {
vis[u] = vrai;
pour (long[] e : adj[u]) {
int v = (int) e[0];
si (vis[v]) continue;
long fac = e[1];
long invFac = e[2];
toRoot[v] = toRoot[u] * fac % MOD;
invToRoot[v] = invToRoot[u] * invFac % MOD;
dfs(v, adj, toRoot, invToRoot, vis);
}
}

privé long modPow(long a, long exp) {
longue rés = 1;
pendant la période (exp > 0) {
si ((exp & 1)] 1) res = res * a % MOD;
a = a * a % MOD;
Exp >>= 1;
}
retour rés;
}
}
«» "

---

4.2 Python (DFS)

'`python
MOD = 1 000 000 007

Solution de classe:
def requêteConversions(self, conversions: List[List[int]],
questions : Liste[List[int]]) -> Liste[int]:
n = len(conversions) + 1
adj = [[] pour _ dans l'intervalle(n)]

pour a, b, c en conversions:
inv = pow(c, MOD - 2, MOD)
Annexe((b, c, inv)) # a -> b
(a, inv, c)) # b -> a

à_root = [0] * n
inv_root = [0] * n
visité = [Faux] * n
à_root[0] = inv_root[0] = 1
auto.dfs(0, adj, to_root, inv_root, visité)

res = []
pour a, b dans les requêtes:
res.append(to_root[b] * inv_root[a] % MOD)
retour res

def dfs(self, u, adj, to_root, inv_root, visited):
visité[u] = Vrai
pour v, fac, inv_fac dans adj[u]:
si visité[v]:
poursuivre
to_root[v] = to_root[u] * fac % MOD
inv_root[v] = inv_root[u] * inv_fac % MOD
auto.dfs(v, adj, to_root, inv_root, visité)
«» "

---

### 4.3 C++ (DFS)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;
longue MOD = 1'000'000'007LL;

solution de classe {
public:
vector<int> requestConversions(vector<vector<int>>& conversions,
vector<vector<int>&questions) {
int n = conversions.size() + 1;
vecteur<vector<array<long long,3>>> adj(n);
pour (auto &e : conversions) {
int a = e[0], b = e[1];
long c = e[2];
long inv = modpow(c, MOD-2);
adj[a].push_back({b, c, inv});
adj[b].push_back({a, inv, c});
}

vecteur <long long> àRoot(n), invRoot(n);
vecteur <int> vis(n,0);
àRoot[0] = invRoot[0] = 1;
dfs(0, adj, toRoot, invRoot, vis);

vecteur <int> ans;
pour (auto &q : requêtes) {
int a = q[0], b = q[1];
les données relatives à l'état de l'aéronef, y compris les données relatives à l'état de l'aéronef;
}
le retour des an;
}

particulier:
vide dfs(int u,
vecteur<vector<array<long long,3>>> &adj,
vecteur <long> &toRoot,
vecteur <long> &invRoot,
vecteur<int> &vis) {
vis[u] = 1;
pour (auto &e : adj[u]) {
int v = e[0];
si (vis[v]) continue;
long fac = e[1], invFac = e[2];
toRoot[v] = toRoot[u] * fac % MOD;
invRoot[v] = invRoot[u] * invFac % MOD;
dfs(v, adj, toRoot, invRoot, vis);
}
}

long long modpow(long long a, long e) {
long r = 1;
pendant que e) {
si (e & 1) r = r * a % MOD;
a = a * a % MOD;
e >>= 1;
}
retour r;
}
};
«» "

Les trois solutions sont **'O(n + q)'** et s'adaptent confortablement aux contraintes (`n, q ≤ 10^5').

---

- Oui. 5. Article du blog – L'unité de conversion II: le bon, le mauvais, et le mauvais

5.1 Introduction

La conversion d'unité est un problème d'interview classique qui cache une subtile torsion algébrique. **LeetCode 3535 – Conversion d'unité II** vous demande de convertir entre unités arbitraires quand seulement un arbre de facteurs de conversion par paires est donné. Dans un contexte de recherche d'emploi, la maîtrise de ce problème démontre votre compréhension du graphe traversal, de l'arithmétique modulaire et de l'optimisation dans des délais serrés.

**Mots clés**: *Unit Conversion II, LeetCode, DFS, BFS, entretien d'emploi, inverse modulaire, Java, Python, C++ *

5.2 Le bon – Pourquoi la solution DFS/BFS est élégante

Résistance Explication
C'est pas vrai.
**Temps linéaire** Autres
Autres **Efficacité de l'espace**. Autres
**Simple pass**= Après DFS, chaque requête est répondue en temps constant. Autres
**Modulaire-friendly**=Le facteur de bord de stockage et son inverse; évite les erreurs de point flottant. Autres
**Language-agnostic**Le même algorithme fonctionne en Java, Python ou C++ avec des changements minimes. Autres

Dans une interview, vous pouvez présenter ceci comme -construire une carte des facteurs de conversion de racine à chaque noeud, puis calculer `root→ B* inv(root→Ai)» L'intervieweur apprécie l'idée d'enraciner l'arbre et de propager des produits cumulatifs.

5.3 Les mauvaises – Pièges communs

Comment éviter
C'est quoi ?
**Modification des inverses modulaires** dans un champ principal; l'utilisation de `c` seul donne de mauvais résultats lors de l'inversion des bords. Autres
Autres **Débordement de la pile (Java)**=La profondeur de la DFS récursive peut atteindre `10^5`; passer à la pile itérative ou augmenter la limite de récursion. Autres
** Grandes valeurs intermédiaires** Exclure plusieurs fois avant le module; utiliser `long`/`int64` pour rester dans les 64 bits. Autres
**Exposition répétée**= Calculer inversement une seule fois par bord; pré-calculer tous les inverses via `pow` peut coûter `n log MOD`. Autres
**Débordement entier en Python**= Utiliser `pow(c, MOD-2, MOD)` pour conserver le résultat dans le module. Autres

Ces écueils sont typiques de l'amour des intervieweurs : ils testent si vous pouvez repérer des erreurs cachées.

5.4 L'horrible – Ce qui fait Ce problème Tricky

Pourquoi c'est Ugly
C'est quoi ?
**Inversions implicites**=La conversion de `Bi` en `Ai` nécessite des facteurs inverses; si vous ignorez cela, vous obtiendrez la division par zéro ou des erreurs de flottement. Autres
**La division modulaire**La division n'est pas simple en modulo arithmétique; vous devez vous rappeler Fermats petit théorème ou pré-calcul inverses. Autres
**Grande taille du graphique**. Un DFS naïf pour chaque requête serait `O(q * n)` – impossible. Autres
**L'utilisation de doubles peut conduire à des erreurs d'arrondi; modulo garantit l'exactitude, mais vous devez l'appliquer correctement. Autres

Dans l'entrevue, un candidat pourrait d'abord écrire une approche naïve: pour chaque requête effectuer un DFS à la volée. Cela serait temps sur de grandes entrées et montrer un manque de prévoyance. La partie *ugly* apprend à reconnaître que **une fois que vous enracinez l'arbre, le reste du travail est une simple multiplication et inversion**.

5.5 Comment parler du problème dans une entrevue

1. ** Clarifier le modèle**
On nous donne un arbre de facteurs de conversion par paires; aller de l'avant multiplies par `c`, aller de l'arrière multiplies par `1/c`. (en milliers de dollars)

2. **Exposer l ' arithmétique modulaire**
Comme la réponse doit être modulo `10^9+7`, nous remplaçons la division par la multiplication par des inverses modulaires (`pow(c, MOD-2'), car le module est primordial. (en milliers de dollars)

3. **Exemple du prétraitement* *
Faites un DFS/BFS du nœud 0. Pour chaque noeud, conserver `facteurRoot[u]` (produit de la racine à `u`) et `invRoot[u]` (produit des inverses). (en milliers de dollars)

4. **Afficher la formule de requête**
Toute requête `Ai → Bi` = `factorRoot[Bi] * invRoot[Ai] (mod MOD)`. Nous n'avons donc besoin que des deux tableaux précalculés. (en milliers de dollars)

5. **Juge**
* Vérifier que tous les nœuds sont visités; gérer les indices 1-basés versus 0-basés.
* Pour chaque bord calculer inversement une seule fois.

6. **Budget-temps**
Le DFS est linéaire; chaque requête est "O(1)". Nous pouvons facilement résoudre 10^5 requêtes dans moins de 100 ms dans Java/Python/C++ sur l'environnement LeetCode. (en milliers de dollars)

#### 5.6 À emporter pour les demandeurs d'emploi

* Conversion unitaire II* est un petit problème qui touche à de nombreux concepts importants. En implémentant un seul DFS et en répondant aux questions en temps constant, vous montrez :
* **Profondeur algorithmique** – transformer une chaîne multiplicative en une simple multiplication basée sur la racine.
* ** Compétence linguistique** – le code fonctionne de façon identique en Java, Python et C++.
* **Gestion du temps** – votre solution fonctionne dans les 1 s pour le pire cas (nœuds `10^5`, requêtes `10^5`).

Lorsque vous expliquez votre solution dans une interview, passez d'abord par l'intuition, puis détaillez la pré-computation inverse modulaire et la résolution de la requête. Soulignez que c'est la solution *canonique* – pas de tricks DP intelligents ou de bibliothèques lourdes nécessaires.

---

- Oui. 6. Pensées finales

Le problème **Unit Conversion II** est une mine d'or pour les candidats se préparant à des entrevues techniques. Il mélange un simple graphe traversant avec arithmétique modulaire, exigeant une manipulation soigneuse des inverses. La solution DFS ci-dessus est simple, efficace et peut être mise en œuvre dans toutes les langues principales. Maîtrisez-le, et vous impressionnerez les intervieweurs avec à la fois correcte et propre, code performant. Bonne chance pour ta chasse au travail !