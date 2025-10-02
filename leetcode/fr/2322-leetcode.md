---
titre: LeetCode 2322. Score minimum après suppression sur un arbre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# LeetCode 2322 – Score minimum après suppressions sur un arbre
**Le bon, le mauvais et le mauvais – Un profond Plongez avec Java / Python / C++ Solutions**

> **Mots-clés du référencement**: *Code Leet 2322*, *Score minimal après élimination sur un arbre*, *Tree DP*, *XOR*, *Hard*, *Interview Prep*, *Java*, *Python*, *C++*, *Conception de l'algorithme*

---

- Oui. 1. Récapitulation des problèmes

On vous donne un arbre enraciné avec des nœuds `n` (`3 ≤ n ≤ 1000`).
- `nums[i]` – valeur du noeud `i`.
- `edges` – liste des bords non orientés `n‐1`.

Vous devez supprimer **deux bords distincts**, diviser l'arbre en **trois composants connectés**.
Pour chaque composant, calculez le XOR de toutes les valeurs de nœuds à l'intérieur.
Le **score** de cette paire de suppression est

«» "
score = max(XOR1, XOR2, XOR3) – min(XOR1, XOR2, XOR3)
«» "

Retourne le score **minimum possible** sur toutes les paires de suppressions de bord.

---

- Oui. 2. Pourquoi ce problème est grand pour les entrevues

Le bon Le mauvais Le mauvais
C'est quoi ?
**Modérer les contraintes** (`n ≤ 1000`) → vous permet de penser à la force brute + taille intelligente. **Deux suppressions** vous forcent à raisonner sur les composants *nested* – des cas faciles à manquer. Autres
**DFS classique + Euler tour** pour sous-arbre XORs – un modèle vu sur de nombreux sites. **Les boucles d'Edge-pair** ('O(n2)') pourraient sembler coûteuses; vous devez justifier pourquoi il est bon pour les contraintes. Autres
** Sous-problème clair** : calcul du sous-arbre XOR une fois, réutilisation. **Vérifications de l'ancêtre** avec temps d'entrée/sortie – une source commune de bogues hors-par-un. Autres

---

- Oui. 3. Stratégie de haut niveau

1. **Root l'arbre** (tout noeud, nous choisissons `0`).
2. Lancer un seul DFS pour calculer :
* `sous-Xor[u]` – XOR de toutes les valeurs dans le sous-arbre de `u`.
* `tin[u]`, `tout[u]` – temps d'entrée/sortie pour tester les relations avec l'ancêtre en O(1).
* `parent[u]` – parent de chaque noeud.
3. Pour chaque paire non ordonnée de "nœuds enfants"* `(i, j)` (le bord est `parent[i]-i`), évaluer le composant XOR résultant:
* **Arêtes disjointes** – trois sous-arbres indépendants :
`c1 = sousXor[i]`, `c2 = sousXor[j]`, `c3 = total Xor ^ subXor[i] ^ subXor[j]».
* **Les bords nestés** (l'un à l'intérieur de l'autre):
Si `j` est à l`intérieur `i` →
«c1 = sous-Xor[j]»,
`c2 = subXor[i] ^ subXor[j]` (XOR du sous-arbre `i` ** sans** `j`),
`c3 = total Xor ^ subXor[i]».
(Symmétrique si `i` est à l'intérieur `j`.)
4. Calculer `score = max(c1, c2, c3) – min(c1, c2, c3)` et conserver le minimum.

Parce que `n ≤ 1000`, la boucle de paire (`~5·105` itérations) est triviale.
L'algorithme fonctionne dans **O(n2)** temps et **O(n)** espace.

---

- Oui. 4. Cas de bord et pièges

Comment éviter
C'est quoi ?
** Erreurs d'analyse de l'ancêtre** – mélange entre `<=` et `<` incorrectement. Autres
**Différence de XOR** – oubliant que `a \ b` dans XOR est `a ^ b` si `b ́ a`= Pour les bords imbriqués, le composant XOR est `sous-Xor[ancêtre] ^ sous-Xor[descendant]`. Autres
**Exclusion du bord de la racine** – la racine n'a aucun parent. Autres
**Plus grande profondeur de récursion** en Java. Autres

---

- Oui. 5. Mise en œuvre du code

Ci-dessous sont des solutions propres, prêtes à coller dans **Java**, **Python** et **C++**.

#### 5.1 Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
liste privée <integer>[] g;
Int[] parent privé, étain, tout, sous-Xor;
minuterie interne privée;
total privé Xor;

Int minimum public Score(int[] nums, int[][] bords) {
int n = longueur nums;
g = nouvelle grille[n];
pour (int i = 0; i < n; ++i) g[i] = nouvelle liste de distribution<>();
pour (int[] e : bords) {
g[e[0]].add(e[1]);
g[e[1]].add(e[0]);
}

parent = nouveau int[n];
étain = nouvelle int[n];
tout = nouvelle int[n];
sous-Xor = nouvelle int[n];
minuteur = 0;

dfs(0, -1, nombres);

totalXor = sous-Xor[0];
int best = entier.MAX_VALUE;

// Recueillir tous les nœuds d'enfant (les bords que nous pouvons supprimer)
Liste <Integer> enfants = nouvelle liste de distribution<>();
pour (int i = 1; i < n; ++i) les enfants.add(i);

// Itérer sur les paires non ordonnées
int m = enfants.taille();
pour (int a = 0; a < m; ++a) {
i = enfants.get(a);
pour (int b = a + 1; b < m; ++b) {
int j = children.get(b);
int[] comps = compsXor(i, j);
score int = Math.max(Math.max(comps[0], comps[1]), comps[2])
- Math.min(Math.min(comps[0], comps[1]), comps[2]);
si (score < best) best = score;
}
}
le meilleur retour;
}

vide privé dfs(int u, int p, int[] nums) {
parent[u] = p;
étain[u] = ++timer;
int xr = nombres[u];
pour (int v : g[u]) si (v != p) {
dfs(v, u, nombres);
xr ^= sous-Xor[v];
}
sous-Xor[u] = xr;
tout[u] = ++timer;
}

// Retourne {c1, c2, c3} pour supprimer les bords (parent[i]-i) et (parent[j]-j)
CompsXor(int i, int j) {
// Vérifier la relation avec l'ancêtre
booléen iInsideJ = étain[j] >= étain[i] &&tout[j] <= tout[i];
booléen jInsideI = étain[i] >= étain[j] &&tout[i] <= tout[j];

c1, c2, c3;
i (iInsideJ) { // j à l'intérieur i
c1 = sous-Xor[j];
c2 = sous-Xor[i] ^ sous-Xor[j]; // i \ j
c3 = total Xor ^ sous-Xor[i];
} sinon si (jInsideI) { // I à l'intérieur
c1 = sous-Xor[i];
c2 = sous-Xor[j] ^ sous-Xor[i]; // j \ i
c3 = total Xor ^ sous-Xor[j];
} autre { // disjoint
c1 = sous-Xor[i];
c2 = sous-Xor[j];
c3 = total Xor ^ subXor[i] ^ subXor[j];
}
retourner une nouvelle int[]{c1, c2, c3};
}
}
«» "

**Points clés**
- Un DFS remplit les heures de visite `subXor` et Euler.
- "timer" garantit les contrôles de l'ancêtre "O(1)".
- Tout arithmétique est sur `int`; LeetCode garantit `nums[i]` correspond à `int`.

---

#### 5.2 Python 3

'`python
de taper l'importation Liste

Solution de classe:
def minimum Score(self, nombres: List[int], bords: List[List[int]]) -> Int:
n = len(nums)
g = [[] pour _ dans l ' intervalle n)]
pour a, b dans les bords:
Annexe b)
g[b].appendice(a)

parent = [-1] * n
étain, tout = [0] * n, [0] * n
sous = [0] * n
minuterie = 0

def dfs(u, p):
minuterie non locale
parent[u] = p
minuterie += 1
étain[u] = minuterie
xr = nombres[u]
pour v en g[u]:
Si v == p:
poursuivre
dfs(v, u)
xr ^= sous-[v]
Sous-[u] = xr
minuterie += 1
tout[u] = minuterie

dfs(0, -1)
Total = sous-[0]
meilleure = flotteur('inf')

# Nœuds d'enfants (la bordure que nous pouvons couper)
enfants = [i pour i dans l'intervalle(1, n)]

pour une gamme(len(enfants):
i = enfants[a]
pour b dans la fourchette(a + 1, len(enfants)):
j = enfants[b]
Contrôle des ancêtres
si tin[i] <= tin[j] <= tout[j] <= tout[i]: # j à l'intérieur i
c1 = sous-[j]
c2 = sous-[i] ^ sous-[j]
c3 = total ^ sub[i]
elif tin[j] <= tin[i] <= tout[i] <= tout[j]: # i inside j
c1 = sous[i]
c2 = sous-[j] ^ sous-[i]
c3 = total ^ sub[j]
Autre: # disjoint
c1, c2, c3 = sub[i], sub[j], total ^ sub[i] ^ sub[j]

score = max(c1, c2, c3) - min(c1, c2, c3)
meilleur = min(meilleure, score)

le meilleur retour
«» "

---

Numéro 5.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
vecteur<vecteur<int>> g;
vecteur <int> parent, étain, tout, sous-Xor;
temps int, total Xor;

vide dfs(int u, int p, const vector<int>& nums) {
parent[u] = p;
étain[u] = ++timer;
int xr = nombres[u];
pour (int v : g[u]) si (v != p) {
dfs(v, u, nombres);
xr ^= sous-Xor[v];
}
sous-Xor[u] = xr;
tout[u] = ++timer;
}

public:
Int minimum Score(vecteur<int>& nums, vecteur<vecteur<int>>& bords) {
int n = nombres.size();
g. attribuer(n, {});
pour (auto &e : bords) {
g[e[0]].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

parent.resize(n);
étain.resize(n);
tout.resize(n);
sous-Xor.resize(n);
minuteur = 0;

dfs(0, -1, nombres);
totalXor = sous-Xor[0];

int best = INT_MAX;
vecteur<int> les enfants;
pour (int i = 1; i < n; ++i) children.push_back(i);

pour (size_t a = 0; a < children.size(); ++a) {
i = enfants[a];
pour (size_t b = a + 1; b < children.size(); ++b) {
int j = enfants[b];
c1, c2, c3;
si (tin[i] <= tin[j] && tout[j] <= tout[i]) { // j à l'intérieur i
c1 = sous-Xor[j];
c2 = sousXor[i] ^ sousXor[j];
c3 = total Xor ^ sous-Xor[i];
} sinon si (tin[j] <= tin[i] && tout[i] <= tout[j]) { // I à l'intérieur
c1 = sous-Xor[i];
c2 = sousXor[j] ^ sousXor[i];
c3 = total Xor ^ sous-Xor[j];
} autre { // disjoint
c1 = sous-Xor[i];
c2 = sous-Xor[j];
c3 = total Xor ^ subXor[i] ^ subXor[j];
}
int mx = max({c1, c2, c3});
Int mn = min({c1, c2, c3});
best = min(meilleur, mx - mn);
}
}
le meilleur retour;
}
};
«» "

Les trois codes partagent la même logique de base – des idiomes différents.

---

- Oui. 6. Pourquoi le `O(n2)` Brute- Travaux de force

- **Moyens d'itération**: "C(n-1, 2) = (n-1) (n-2)/2 : "5·105" pour "n = 1000".
- Chaque itération ne fait qu'une poignée d'opérations entières → < 1 ms en C++ / Python, < 5 ms en Java.
- L'utilisation de la mémoire est linéaire: `O(n)` pour la liste d'adjacence, les métadonnées DFS et quelques tableaux entiers.

**Si vous vous inquiétez de la performance**, vous pouvez prouver ce qui suit:
"5·105" boucles × ~10 opérations primitives - 5 M opérations – bien en dessous de la limite de 1 seconde sur LeetCode.
Pas besoin de tricks bit-parallels ou de structures de données avancées.

---

- Oui. 7. Pensées finales – ce qui fait ce problème *Interview-Ready*

1. **Sous-problème clair** – Calculer le sous-arbre XOR *une fois*.
2. **Euler Tour Ancestor Test** – un modèle réutilisable pour toute logique de sous-arbre par rapport au sous-arbre.
3. **Différence d'ensemble dans l'espace XOR** – une subtilité qui voyage beaucoup de candidats; la maîtriser démontre un raisonnement fort à la légère.
4. ** Analyse de complexité** – montrer que vous pouvez raisonner sur `O(n2)` par rapport à `O(n3)` et justifier vos choix de conception.

Si vous pouvez expliquer cette solution, passer à travers la boucle de paires, et montrer pourquoi le code est correct, vous allez démontrer la maîtrise des traversées d'arbres, la manipulation de bits, et la pensée algorithmique – exactement les gestionnaires d'embauche de compétences cherchent dans un problème *Hard* LeetCode.

---

- Oui. 8. Description du méta

> * Apprenez à résoudre LeetCode 2322 – Score minimum après suppression sur un arbre – avec code Java, Python et C++ étape par étape. Comprendre l'astuce de l'ancêtre-différence, les contrôles d'intervalle de temps, et pourquoi ce problème d'entrevue -Hard-Hard est une vitrine parfaite des compétences DP et XOR arbre. *

---

Bon codage, et bonne chance de tuer cette interview! C'est ce qu'il a dit