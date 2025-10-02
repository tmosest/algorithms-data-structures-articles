---
titre: LeetCode 1579. Supprimer le nombre max de bords pour garder le graphique entièrement réversible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1579 – Retirez le nombre maximum de bords pour garder le graphique entièrement croisable
- Oui. C++ – Solutions de travail complètes + SEO-Optimized Blog Post

> **Mots clés**: LeetCode 1579, Union‐Find, Connectivité graphique, Problème d'entrevue, Suppression Max Edge, Solution Python, Solution Java, Solution C++, Interview de codage, Traversal complet, Alice et Bob, Conseils d'entrevue

---

TL;DR
*Utilisez Union-Find (Disjoint Set Union) pour construire un arbre de couverture pour Alice et Bob.
Premier traitement des bords de type‐3 (utilisables par les deux), puis des bords de type‐1 et de type‐2.
Comptez les bords qui sont réellement nécessaires – tout le reste peut être enlevé.
Si l'un ou l'autre graphique est déconnecté, retourner **‐1**.*

---

Récapitulation des problèmes

On vous donne un graphique non dirigé avec des nœuds `n` (1-basé).
Les bords viennent en trois saveurs:

Type Autorisé par Description
- C'est quoi ?
Alice seule Alice peut traverser
Seul Bob peut traverser
Autres Les deux peuvent traverser

Le graphique doit rester ** entièrement traversable** pour Alice * et * Bob – de n'importe quel noeud vous devez être en mesure d'atteindre tous les autres nœuds.
Votre objectif : **Supprimer autant de bords que possible** tout en conservant cette propriété.
Retourner le nombre maximal de bords amovibles ou `-1` s'il est impossible.

Contraintes: «1 ≤ n ≤ 105», «longueur des bords ≤ 105».

---

# # # , , Intuition

Un graphique connecté avec des nœuds `n` nécessite au moins des bords `n‐1` (un arbre de recouvrement).
Si nous pouvons utiliser un bord qui fonctionne pour les utilisateurs *deux*, il nous sauve deux bords -potentiels.
Par conséquent, nous ajoutons d'abord avidement tous les bords de type‐3 qui fusionnent réellement deux composants.
Après cela nous ajoutons les bords restants spécifiques à chaque utilisateur, seulement quand ils aident à connecter de nouveaux composants.

Chaque bord qui ne **pas** contribue à la connectivité de **ni** graphique est sûr à supprimer.

---

Algorithme (Union-Find / DSU)

1. **Initialiser deux structures du DSU** – une pour Alice (`dsuA`) et une pour Bob (`dsuB`).
2. **Couvercle des bords "utilisés" = 0** – bords essentiels.
3. **Arêtes de type 3 du procédé**
Texte
si dsuA.union(u, v) ou dsuB.union(u, v):
utilisé += 1
«» "
4. **Arêtes de type 1 du procédé (Alice seulement)* *
Texte
si dsuA.union(u, v):
utilisé += 1
«» "
5. **Arêtes de type 2 du procédé (Bob seulement)* *
Texte
si dsuB.union(u, v):
utilisé += 1
«» "
6. ** Vérifier la connectivité**
Texte
si dsuA.components == 1 et dsuB.components == 1 :
return edges.longueur - utilisé
Sinon:
retour -1
«» "

**Les opérations Union‐Find** fonctionnent en presque O(1) temps avec compression de trajectoire + union par taille/ rang.

---

- Oui. Code

Ci-dessous vous trouverez des implémentations propres et commentées dans **Java**, **Python** et **C++**.
Tous sont temps `O(n + m)` et espace `O(n)`.

---

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
// -------- Union‐Find ---------
classe statique privée DSU {
Int[] parent;
taille int[];
composants int;

DSU(int n) {
parent = nouveau int[n + 1];
taille = nouvelle int[n + 1];
pour (int i = 1; i <= n; i++) {
parent[i] = i;
taille[i] = 1;
}
composants = n;
}

int find(int x) {
si (parent[x] != x) parent[x] = find(parent[x]); // compression du chemin
retour du parent[x];
}

// retourne true si union a effectivement fusionné deux composants
Union booléenne(int a, int b) {
a = find(a); b = find(b);
si a) b) retourner faux;
si (taille[a] < taille[b]) { int tmp = a; a = b; b = tmp; }
parent[b] = a;
taille[a] += taille[b];
composants--;
retour vrai;
}

booléen isConnected() { composants de retour == 1; }
}
// -------- Solution...
Int public maxNumEdgesToRemove(int n, int[][] bords) {
DSU dsuA = nouveau DSU(n);
DSU dsuB = nouveau DSU(n);

int utilisé = 0; // bords essentiels

Les bords du type 3
pour (int[] e : bords) {
Si (e[0]] 3) {
// utiliser le résultat de chaque DSU – logique OU
si (dsuA.union(e[1], e[2])) utilisé++;
}
}

Type-1 (Alice)
pour (int[] e : bords) {
si (e[0] == 1 && dsuA.union(e[1], e[2])) utilisé++;
}

Type-2 (Bob)
pour (int[] e : bords) {
si (e[0] == 2 && dsuB.union(e[1], e[2])) utilisé++;
}

Contrôle final
si (dsuA.isConnected() && dsuB.isConnected()) {
les bords de retour.longueur - utilisé;
}
retour -1;
}
}
«» "

---

4.2 Python

'`python
Classe DSU:
def __init_(self, n: int):
auto-parent = list(range(n + 1))
taille de soi = [1] * (n + 1)
auto.comp = n

def find(self, x: int) -> Int:
si soi-même. parent[x] != x:
Self.parent[x] = self.find(self.parent[x])
Revenez vous-même. parent[x]

def union(self, a: int, b: int) -> C'est vrai.
a, b = self.find(a), self.find(b)
si a == b: retourner Faux
si self.size[a] < self.size[b]:
a, b = b, a
[b] = a
taille de soi[a] += taille de soi[b]
Self.comp -= 1
retour Vrai

def connecté(e) -> C'est vrai.
retour self.comp == 1

Solution de classe:
def maxNumEdgesToRemove(self, n: int, bords: List[List[int]]) -> Int:
dsu_a = DSU(n)
dsu_b = DSU(n)

utilisé = 0

# Type 3
pour t, u, v dans les bords:
Si t == 3:
si dsu_a.union(u, v) ou dsu_b.union(u, v):
utilisé += 1

# type 1 & 2
pour t, u, v dans les bords:
Si t == 1:
Si dsu_a.union(u, v):
utilisé += 1
- Oui. 2 :
si dsu_b.union(u, v):
utilisé += 1

retour (len(edges) - utilisé) si dsu_a.connected() et dsu_b.connected() sinon -1
«» "

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe DSU {
public:
vecteur<int> parent, sz;
les comptes d'entrée;
DSU(int n) : parent(n + 1), sz(n + 1, 1), comps(n) {
(parent.begin(), parent.end(), 0);
}
int find(int x) {
retourner parent[x] == x ? x : parent[x] = find(parent[x]);
}
bool unit(int a, int b) {
a = find(a), b = find(b);
si a) b) retourner faux;
si (sz[a] < sz[b]) swap(a, b);
parent[b] = a;
sz[a] += sz[b];
--comptes;
retour vrai;
}
bool connected() const { return comps == 1; }
};

solution de classe {
public:
int maxNumEdgesToRemove(int n, vector<vector<int>& bords) {
DSU dsuA(n), dsuB(n);
Int utilisé = 0;

// type 3
pour (auto &e : bords)
Si (e[0]] 3)
utilisé += (dsuA.unite(e[1], e[2]))

// type 1 et 2
pour (auto &e : bords) {
si (e[0] == 1 && dsuA.unite(e[1], e[2])) ++utilisé;
sinon si (e[0] == 2 && dsuB.unite(e[1], e[2])) ++utilisé;
}

retour dsuA.connected() && dsuB.connected() ?
static_cast<int>(edges.size() - utilisé) : -1;
}
};
«» "

---

Article de blog – SEO-Friendly Interview Guide

> *Tagué pour les ingénieurs de logiciels juniors et seniors se préparant pour les questions de Graph. *

---

### 5.1 Titre & Meta Description

«» "
LeetCode 1579: Union‐Trouver une solution en Java, Python & C++
«» "

> **Description détaillée**:
> Master LeetCode 1579 avec des solutions étape par étape Union-Find en Java, Python et C++. Apprenez la stratégie gourmande, l'analyse de complexité, les hacks d'entrevue, et comment aser ce problème de graphique dans votre prochaine entrevue de codage.

---

5.2 Table des matières

1. [Présentation du problème](#problème-aperçu)
2. [Pourquoi Union-Find Rocks](#Why-union-find-rocks)
3. [Bonne – Ce qui fonctionne bien] (#Bonne – Ce qui fonctionne bien)
4. [Bad – Pièges communs] (# mauvais-pièges communs)
5. [Ugly – Gotchas & Edge‐Cases](#ugly-gotchas-&-edge-Cases)
6. [Complexité temporelle et spatiale] (#temps--complexité spatiale)
7. [Conseils et astuces d'entrevue] (#conseils-d'entrevue)
8. [Renseignements complets](#Renseignements complets)
9. [Mise à jour et ressources] (#Mise à jour - ressources)

---

5.3 Aperçu du problème

LeetCode 1579 est un problème classique de connectivité *graph*.
Le scénario d'Alice et de Bob oblige les candidats à penser à **dual s'étendant sur des arbres**.
En raison de sa taille (`105`), toute solution basée sur le ‘O(n2)' ou le DFS sera épuisée.
La réponse canonique utilise **Union‐Find** – un DSU qui fusionne des composants dans un temps proche.

---

5.4 Pourquoi Union- Trouver des rochers

Raison
C'est pas vrai.
**Les opérations près de O(1)**=La compression par voie + l'union par taille garantit l'amortissement de O(α(n) par opération. Autres
**Simple API**="find`, `union` et un compteur `components`. Autres
Autres **Aucun souci de la profondeur de la récursion** Autres
**Memory friendly**. Autres

---

5.5 Bon – Ce qui fonctionne bien

Aspect Pourquoi c'est génial
-- -- -- -- -- --
**L'optimalité de la grêle**L'ajout de tous les bords utiles de type‐3 garantit d'abord le minimum de bords pour les deux utilisateurs. Autres
**Séparation claire**Deux objets DSU gardent la logique propre – aucune confusion entre les graphiques Alice et Bob. Autres
**Comptoir `utilisé` explicite** Autres
**Vérification de la connectivité à un seul passage**. Autres

---

5.6 Mauvais – Pièges communs

1. **Traitement des bords dans le mauvais ordre**
*Si vous ajoutez type‐1/2 avant type‐3, vous pouvez manquer une occasion de sauvegarder un bord. *
2. **Logique de suppression de type 3* *
*L'augmentation brutale de « utilisé » pour chaque bord de type 3, même s'il s'agissait d'une boucle de soi, donne une mauvaise réponse. *
3. **L'indexation hors-par-un**
*Les nœuds graphiques sont basés sur 1 – l'attribution de tableaux de taille `n+1` est cruciale. *
4. **Pas de vérification de la connectivité* *
*Même si `used=n‐1`, vous pourriez toujours avoir un graphique déconnecté si les bords étaient tous de type‐3 mais ne pas connecter tous les nœuds. *

---

###5.7 Ugly – Gotchas & Edge‐ Affaires

Pourquoi ça compte ? Comment manipuler ?
- C'est quoi ?
Avec `n > 1`, impossible à connecter. Retour `-1` tôt. Autres
Autres **Tous les bords sont de type‐3 mais le graphique est toujours déconnecté**. Seulement 3 nœuds connectés. Autres Après traitement, vérifiez `dsuA.components` et `dsuB.components`. Autres
**Dupliquer les bords** Union‐Find ignore naturellement les duplicatas inutiles. Autres
**Solf-loops**= L'entrée garantit `u != v`, mais le codage défensif (`union` retourne faux quand le même composant) vous protège. Autres
**La plus grande `n` mais peu de bords**. "-1". Autres

---

####5.8 Complexité temporelle et spatiale

- **Heure**:
- "O(m α(n)" où `m = bords.size()`.
- Pour `m = 105`, ceci est pratiquement linéaire.

- **Espace**:
- Deux structures DSU: `2 * (n + 1)` entiers → `O(n)` mémoire.

- **Amortissement de la fonction inverse Ackermann**:
- "α(n)" ≤ 5 pour tous les "n" réalistes. Donc nous disons souvent "O(m)".

---

### 5.9 Conseils et astuces d'entrevue

Pourquoi ça aide ?
C'est quoi ?
**Expliquez d'abord l'idée de deux DSU** Autres
Autres **Utiliser les noms de variables descriptifs** (`utilisé`, `composants`) Les intervieweurs apprécient la lisibilité. Autres
Autres **Test contre les petits bogues fabriqués à la main** Autres
**Mention edge-case handling** Autres
Autres **S'il est demandé pour la complexité, parler de α(n)** Autres
Autres **Si vous codez sur le tableau blanc, dessinez un petit graphique**. Autres

---

#### 5.10 Extraits de code complet

(voir **Section 5.5 Extraits de code complets** pour Java/Python/C++)

---

### 5.11 Enveloppe Mise à jour et ressources

- **LeetCode discussion threads** – idéal pour voir des modèles DSU alternatifs.
- **Algorithmes grégaires** – le chapitre sur le DSU donne une introduction douce.
- **La liste de lecture de YouTube : "Graph Algorithms"** – visualiser comment Union-Find construit des composants.
- **GitHub repo** – `Leetcode-1579-UnionFind` avec les trois implémentations linguistiques et les tests unitaires.

> *Prêt à l'as LeetCode 1579 ? Construisez votre bibliothèque DSU, testez attentivement et entrez dans votre entrevue avec confiance. *

---

5.12 Références

1. ** Union – Trouver la structure des données** – Wikipedia.
2. **Ackermann Function & Inverse** – "α(n)" explication.
3. **LeetCode 1579 Discussion** – plusieurs solutions acceptées.

---

> *Codage heureux et bonne chance pour votre prochaine interview! *

---

Conclusion

Nous avons livré:

- **Trois implémentations complètes, prêtes à être copiées** (Java, Python, C++) pour LeetCode 1579.
- Une explication cupide** basée sur Union-Find.
- Un guide d'entrevue **compréhensif** qui équilibre l'aperçu du problème, les avantages du DSU, les pièges, les cas de bord et les conseils pratiques.

Armé de cette connaissance, vous pouvez aborder avec confiance LeetCode 1579, impressionner les intervieweurs, et mettre en valeur votre maîtrise des algorithmes graphiques et des structures de données. Bon codage !