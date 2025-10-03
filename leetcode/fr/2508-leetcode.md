---
titre: LeetCode 2508. Ajouter des bords pour rendre les degrés de tous les nœuds égaux -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2508 – Ajouter des bords pour rendre les degrés de tous les nœuds égaux
**LeetCode Hard.

> Si vous préparez une interview par algorithme, ce problème de LeetCode est un must‐do.
> Il teste votre capacité à penser en *parité* et *connectivité* tout en restant dans des limites strictes de temps et d'espace.
> Ci-dessous vous trouverez une solution complète dans **Java**, **Python** et **C++**, plus un parcours en profondeur de style blog que vous pouvez déposer dans un portfolio ou un lien En poste pour impressionner les recruteurs.

---

Récapitulation des problèmes

- **Graphique** : Non dirigé, jusqu ' à 105 nœuds et 105 bords.
- **Objectif**: Ajouter *au plus deux* nouveaux bords (pas de boucles d'auto, pas de duplicata) de sorte que chaque noeud ait un degré **même**.
- **Retour** : « vrai » si c'est possible, sinon « faux ».

Autres **Observation principale** – Seulement des nœuds avec un degré de matière étrange.
> La somme totale des degrés est toujours égale, donc le nombre de nœuds de degrés impairs est égal.

---

Intuition de la solution (le bon, le mauvais, le mauvais)

**Aspect**
C'est pas vrai.
Une logique simple au cas par cas (0, 2 ou 4 nœuds impairs)
**Complexité**= Temps `O(n + m)`, Mémoire `O(n + m)`= Pas de facteur de log supplémentaire; nous n'avons pas besoin de structures de données lourdes== Aucune – la logique est O(1) pour le nombre de noeuds impair==
**Codage**=Loops rectilignes + ensembles d'adjacence= Éviter d'utiliser `Vector<Set>` en Java (coûts)=Il faut protéger contre le débordement entier dans les ensembles C++ (utiliser `int` seulement)=
**Cas d'Edge**=0 noeuds impairs → déjà valides=2 noeuds impairs qui sont déjà adjacents=4 noeuds impairs qui ne peuvent pas être jumelés parce qu'un bord existe dans chaque jumelage=

---

Algorithme détaillé

1. **Ensembles d'adjacence de construction** – «O(m)»
* Permet la recherche à temps constant de «edgeExists(u, v)». *

2. **Collecter les nœuds à degrés impairs** – `O(n)`
* `odd = [v pour v dans 1..n si degré(v) % 2 == 1]`. *

3. ** Analyse de cas**
Que faire ? Pourquoi ?
- C'est quoi ?
Retour `true`. Autres
Qu'ils soient "a, b".
* Si `a` et `b` sont *not* connectés → ajouter ce bord → succès.
* À moins de rechercher un `c` qui est **non** adjacent à **tous les deux** `a` et `b`.
Si trouvé → ajouter des bords `(a, c)` & `(b, c)`. Autres
Qu'ils soient "a, b, c, d".
Essayez les 3 paires :
«(a,b)» et «(c,d)»
«(a,c)» et «(b,d)»
«(a,d)» et «(b,c)»
Si au moins une paire a **deux** bords manquant → succès. Deux bords suffisent pour fixer quatre nœuds impairs. Autres
**>4**== Retour `faux`.= Plus de deux nouveaux bords seraient nécessaires. Autres

4. **Retour** le résultat.

> **Pourquoi ça marche ? **
> Ajouter un bord retourne la parité de ses deux nœuds d'incident.
> Ainsi, toute solution doit coupler les nœuds impairs avec les nouveaux bords.
> Parce que nous pouvons ajouter au plus deux bords, le nombre maximum de nœuds impairs que nous pouvons fixer est quatre.

---

Mise en œuvre du code

Python

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def isPossible(self, n: int, bords: List[List[int]]) -> Bool:
# ensembles d'adjacence pour la recherche de bord O(1)
g = débit(set) par défaut
pour a, b dans les bords:
g[a].add(b)
g[b].add(a)

# Recueillir des nœuds de degrés impairs
impair = [v pour v dans l'intervalle(1, n + 1) si len(g[v]) % 2 == 1]

Si ce n'est pas impair : # 0 noeuds impairs
retour Vrai

si len(odd) == 2: # 2 nœuds impairs
a, b = impair
si b n'est pas en g[a]:
retour Vrai
# chercher un troisième noeud qui n'est pas adjacent à a ni b
pour c dans la plage(1, n + 1):
si c en particulier: continuer
si a n'est pas en g[c] et b n'est pas en g[c]:
retour Vrai
Retour Faux

si len(odd) == 4: # 4 nœuds impaires
a, b, c, d = impair
# trois combinaisons possibles
retour (
b) ni en g[a] ni en g[c]
c non en g[a] et d non en g[b]) ou
(d pas en g[a] et c pas en g[b])
)

# tout autre nombre de nœuds impaires est impossible
Retour Faux
«» "

---

- Oui. Java

"Java
Importation de java.util.*;

solution de classe {
booléen public estpossible(int n, Liste<Liste<entier>> bords) {
// ensembles d ' adjacence
Liste<Set<Integer>> g = nouvelle liste de distribution<>(n + 1);
pour (int i = 0; i <= n; i++) g.add(new HashSet<>());
pour (Liste <entier> e : bords) {
a = e.get(0), b = e.get(1);
g.get(a)add(b);
g.get(b).add(a);
}

// Recueillir des nœuds à degrés impairs
Liste<entier> impair = nouvelle liste de distribution<>();
pour (int i = 1; i <= n; i++) {
si (g.get(i).size() % 2 == 1) impair.add(i);
}

si (odd.isEmpty()) retourne vrai; // 0 impair

si (odd.size()) == 2) {/ 2
int a = impair.get(0), b = impair.get(1);
si (!g.get(a).contient(b)) retourner vrai;
pour (int c = 1; c <= n; c++) {
si c) continuer;
si (!g.get(a).contient(c) &&!g.get(b).contient(c) retourner true;
}
retourner faux;
}

si (odd.size()) == 4) {/ 4
int a = impair.get(0), b = impair.get(1),
c = impair.get(2), d = impair.get(3);
// Essayez les 3 paires
si (!g.get(a).contient(b) &&!g.get(c).contient(d)) retourner true;
si (!g.get(a).contient(c) &&!g.get(b).contient(d)) retourner true;
si (!g.get(a).contient(d) &&!g.get(b).contient(c)) retourner true;
retourner faux;
}

retourner faux; // >4 noeuds impairs
}
}
«» "

---

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
bool isPossible(int n, vector<vector<int>>& bords) {
vecteur <unordered_set<int>> g(n + 1);
pour (auto &e : bords) {
int a = e[0], b = e[1];
g[a].insérer(b);
g[b].insérer(a);
}

vecteur <int> étrange;
pour (int i = 1; i <= n; ++i)
si (g[i].size() % 2 == 1) impair.push_back(i);

si (odd.vide()) retourne true; // 0 impair

si (odd.size()) == 2) {/ 2
int a = impair[0], b = impair[1];
si (!g[a].count(b)) retourne vrai;
pour (int c = 1; c <= n; ++c) {
si c) continuer;
si (!g[a].count(c) &&!g[b].count(c) retourne true;
}
retourner faux;
}

si (odd.size()) == 4) {/ 4
int a = impair[0], b = impair[1],
c = impair[2], d = impair[3];
// 3 paires
si (!g[a].count(b) &&!g[c].count(d)) retourne true;
si (!g[a].count(c) &&!g[b].count(d)) retourne true;
si (!g[a].count(d) &&!g[b].count(c)) retourne true;
retourner faux;
}

retourner faux; // >4 noeuds impairs
}
};
«» "

> **Note**
> - Toutes les implémentations utilisent **`O(n + m)`** temps et mémoire.
> - Nous utilisons *hash-sets* (`unordered_set` / `HashSet`) de sorte que `edgeExists` est le temps constant même quand `n` est grand.

---

## Description du portefeuille

> **Titre**: La rareté et la connectivité – une solution O(n+m) propre à LeetCode 2508
> **Traitements clés**:
> * Parité des degrés → seuls les nœuds impairs comptent.
> * Deux nouveaux bords peuvent fixer au plus quatre nœuds impaires.
> * Les ensembles d'adjacence à temps constant maintiennent la solution linéaire.

N'hésitez pas à intégrer le code ci-dessus dans un dépôt GitHub, un PDF ou même une courte explication vidéo sur LinkedIn. Les recruteurs adorent voir une solution propre et bien commentée qui démontre *tant* un aperçu algorithmique et un codage de l'hygiène.

---

Bonus : SEO-Friendly Blog Post

> **Meta-Titre**: 2508 – Ajouter des bords pour rendre les degrés de tous les nœuds égaux (leetCode dur)
> **Méta-Description**:
> Master LeetCode 2508 avec une solution rapide et linéaire en Java, Python et C++.
> Apprenez le tour de parité, l'analyse de cas, et pourquoi vous ne pouvez pas ajouter plus de deux bords.
> Parfait pour les entrevues CS.

> **Mots-clés cibles**:
> `LeetCode 2508`, `Add Edges to Make Degrees Even`, `Hard Graph Problem`, `Interview Algorithm`, `Parity Graph`, `O(n+m) Graph`, `Java Graph Solution`, `Python Graph Solution`, `C++ Graph Solution "

---

Bon codage, et bonne chance pour cette interview ! C'est ce qu'il a dit