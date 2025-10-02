---
titre: LeetCode 3004. Sous-arbre maximal de la même couleur -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 3004 – Sous-arbre maximal de la même couleur
**Solution en Java
**+ Un billet de blog plein-blown SEO-friendly qui raconte l'histoire de la bonne, de la mauvaise et de l'hugly *

---

### TL;DR

* **Objectif** – Trouvez le plus grand sous-arbre (raciné à n'importe quel noeud) où ** chaque noeud a la même couleur**.
* **Idée** – DFS + rétro-suivi.
* **Complexité** – temps « O(n) », espace « O(n) » (pile de récursion).
* **Code** – 3 implémentations prêtes à coller (Java, Python, C++).

---

- Oui. 1. Récapitulation des problèmes

> **LeetCode 3004 – Sous-arbre maximal de la même couleur**
> On vous donne un arbre (le nœud 0 est la racine).
> `edges[i] = [u, v]` indique un bord non dirigé.
> `colors[i]` est la couleur du noeud i.
> Retourne la taille du plus grand sous-arbre dont les nœuds sont tous de la même couleur.

Exemple
C'est pas vrai.
= [[0,1],[0,2],[0,3], couleurs = [1,1,2,3]
"edges = [[0,1],[0,2],[0,3], couleurs = [1,1,1,1]"
= [[0,1],[0,2],[2,3],[2,4], couleurs = [1,2,3,3]

---

- Oui. 2. Intuition et pourquoi le DFS fonctionne

Un sous-arbre est *homogène* seulement si chaque sous-arbre enfant est également homogène ** et** partage la même couleur que la racine.
Pendant la DFS, nous pouvons **retourner deux informations** pour chaque nœud :

1. **Le sous-arbre est-il enraciné ici homogène? * *
* Si oui → taille du sous-arbre (pour une réponse potentielle).
* Si pas → `-1` (moyennant :
2. ** Sous-arbre homogène maximal vu jusqu'à présent dans l'appel récursif**.

Lorsqu'un parent traite un enfant:

* Si le sous-arbre de l'enfant est homogène *et* la couleur de l'enfant équivaut au parent, nous pouvons fusionner en toute sécurité leurs tailles.
* Dans le cas contraire, le sous-arbre parent devient « mélangé » (`-1`).

Ce **back-tracking** garantit que nous n'inspectons chaque nœud qu'une seule fois → `O(n)`.

---

- Oui. 3. Le bon, le mauvais et le mauvais

**Aspect**
C'est pas vrai.
**Algorithme**: Simple DFS, intuitif, linéaire.
**Liste d'adjacence O(n) + empilement de récursion O(n)
**Lisibilité du code**. Très compact, retour du tableau à deux valeurs.
**Cas d'Edge**= Fonctionne pour un seul noeud, toutes les mêmes couleurs, toutes les différentes=_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________

---

- Oui. 4. Mise en œuvre des références

Ci-dessous vous trouverez trois implémentations polies.
Tous partagent la même idée de base mais sont idiomatiques dans leur langue.

> **Astuce**: La liste d'adjacence est construite en "O(n)".
> DFS est implémenté de façon récursive (se sentir libre de convertir en itératif si la profondeur de la pile est une préoccupation).
> La paire retournée `[subtreeSize, maxSize]` est emballée en tableau / tuple / struct.

#### 4.1 Java (17)

"Java
Importation de java.util.*;

solution de classe publique {
// méthode publique comme LeetCode s'attend
public int maximumSubtreeSize(int[][] bords, int[] couleurs) {
int n = bords longueur + 1;
Liste <entier>[] graphique = buildGraphique(n, bords);
retour dfs(0, -1, graphique, couleurs)[1];
}

// DFS retourne {subtreeSize, bestSize}
Int[] dfs(int u, int parent, Liste<entier>[] graphique, couleurs int[] {
courant int = 1; // taille si jusqu ' à présent homogène
int best = 0; // best vu chez l'enfant

pour (int v : graph[u]) {
si (v) le parent continue;

int[] res = dfs(v, u, graphique, couleurs);
int childSize = res[0];
best = Math.max(best, res[1]);

si (childSize != -1 && couleurs[v] == couleurs[u]) {
current += childSize; // fusion enfant
} autre {
courant = -1; // sous-arbre devient mélangé
}
}
retourner le nouveau int[]{current, Math.max(current, best)};
}

liste privée<integer>[] buildGraph(int n, int[][] bords) {
Liste <entier>[] g = nouvelle liste de distribution[n];
pour (int i = 0; i < n; i++) g[i] = nouveau tableau <>();
pour (int[] e : bords) {
g[e[0]].add(e[1]);
g[e[1]].add(e[0]);
}
retour g;
}
}
«» "

#### 4.2 Python (Python 3.8+)

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def maximumSubtreeSize(self, bords: List[List[int]]], couleurs: List[int] -> Int:
n = len(couleurs)
g = defaultdict(list)
pour u, v dans les bords:
g[u].appendice(v)
g[v].append(u)

def dfs(u: int, parent: int):
cur = 1 # taille si homogène
meilleure = 0 # meilleure vue dans les sous-arbres
pour v en g[u]:
si v == parent: continuer
child_size, child_best = dfs(v, u)
best = max (meilleur, meilleur enfant)

si enfant_size != -1 et couleurs[v] == couleurs[u]:
pour taille d'enfant
Sinon:
pour = -1
retour cur, max(cur, meilleur)

_, ans = dfs(0, -1)
retour et
«» "

### 4.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maximumSubtreeSize(vecteur<vecteur<int>>& bords, vecteur<int>& couleurs) {
int n = colors.size();
vecteur<vector<int>> g(n);
pour (auto &e : bords) {
g[e[0]].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

fonction<pair<int,int>(int,int)> dfs = [&](int u, int p) {
Int cur = 1; // taille si homogène
int best = 0; // best in children
pour (int v : g[u]) {
si v == p) se poursuit;
auto [childSize, childBest] = dfs(v, u);
best = max (meilleur, meilleur enfant);

si (childSize != -1 && couleurs[v] == couleurs[u])
pour taille enfant;
Autre
cur = -1;
}
retour make_pair(cur, max(cur, best));
};

retour dfs(0, -1).seconde;
}
};
«» "

---

- Oui. 5. Analyse de la complexité

Métrique
- C'est quoi ?
**Heure** Autres
**Space** + récursion

> **Note** : La profondeur de récursion est égale à la hauteur de l'arbre. Dans le pire des cas (liste liée) profondeur = `n`. Pour `n ≤ 5·104` il convient dans la plupart des environnements d'exécution, mais si vous touchez empile limite basculer vers une pile itérative.

---

- Oui. 6. Variations et extensions

Variation de la taille
C'est quoi ?
**Fruits multiples**=Construisez une forêt; exécutez le DFS de chaque composante. Autres
* Couleurs pondérées * Gardez une trace des couleurs comme des cordes ou des objets. Autres
**Requêtes dynamiques** Autres
**Itérative DFS**=Utilisez la pile et la paire explicites (noeud, état itérateur). Autres
**Parallel DFS**=Pour les arbres énormes, diviser les sous-arbres entre les fils. Autres

---

- Oui. 7. SEO–Friendly Takeaway

- **Mots clés**: `LeetCode 3004`, `Maximum Subtree of the Same Color`, `Tree DFS`, `Tree DP`, `Java solution`, `Python solution`, `C++ solution`, `Algorithmes d'entretien d'emploi`, `Thème du graphique`, `Structures de données`, `Programmation compétitive'.
- **Meta Description** (pour les moteurs de recherche de blog):
> LeetCode 3004 – Sous-arbre maximal de la même couleur. Lisez notre solution complète en Java, Python & C++ avec une explication étape par étape, une analyse de complexité et des idées prêtes à l'entrevue. Parfait pour les recruteurs et les auto-études. (en milliers de dollars)

- **La structure de la tête** (H1‐H3) permet aux moteurs de recherche de voir le débit:
«» "
Code Leet 3004 – Maximum Sous-arbre de la même couleur
## Déclaration du problème
## Intuition & DFS
Bien, mal et mal
## Java/Python/C++ Code
Analyse de complexité
«» "

- **Backlinks & Social**: Partager l'article sur LinkedIn, Reddit r/cscareerquestions, et les forums de programmation pertinents. Mention « Prêt à utiliser le code d'entrevue » pour attraper l'intérêt du recruteur.

---

- Oui. 8. Conclusion

Le crux de **LeetCode 3004** est un DFS *simple* qui retourne une paire de valeurs.
L'algorithme est optimal (« O(n) ») et facile à comprendre, ce qui en fait un excellent point de discussion dans une interview technique.

> **Conseil pro**: Si vous vous préparez à une entrevue, n'oubliez pas de **expliquer le suivi arrière** et pourquoi un sous-arbre homogène est brisé dès qu'une inadéquation est trouvée. Les recruteurs adorent vous voir penser en termes de *état* et de *mémorisation* même dans un problème de *O(n).

Bon codage et bonne chance pour votre prochain entretien! C'est ce qu'il a dit.

---