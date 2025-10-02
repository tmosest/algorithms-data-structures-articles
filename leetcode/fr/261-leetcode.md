---
titre: LeetCode 261. Arbre graphique valide -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Code du Leet – *Arbre valide*
**Python de Java** – 3 solutions complètes, une plongée profonde dans le bon, le mauvais, et le laid, et un court post de blog **SEO-friendly** pour vous aider à atterrir cette interview d'ingénierie logicielle.

---

Aperçu du problème

> **Arbre valide** – **Code de cap 261**
> **Difficulté**: Moyenne
> **Signature**
> ``java
> booléen public valideTree(int n, int[][] bords)
> `` "
>
> **Input**
> * `n`: nombre de nœuds (`0 ... n‐1`)
> * `edges`: liste des bords non dirigés (`edges[i] = [ai, bi]`)
> **Objectif**
> Retour `true` if le graphique décrit par `edges` forme un arbre **valable** (connecté *et* acyclique).

Obstacles

Valeur des contraintes
C'est pas vrai.
1 ≤ n ≤ 2000
"0 ≤ bords.longueur ≤ 5000"
"edges[i].longueur == C'est vrai.
0 ≤ ai, bi < n ' est
"ai != bi" (pas de boucle d'auto)
Autres Pas de doublons

---

Trois approches

Pourquoi ça marche ?
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
* et* assure la connectivité via `edges.longueur == n-1`" espace
**Python**= Profondeur-Première recherche (DFS)== Traverses du noeud 0, pistes visitées nœuds, et contrôles pour les contre-côtés==="O(n + m)` time, `O(n)=" espace
La même idée que la DFS, mais itérative; vérifie également aucun cycle. espace

> **Insight clé**
> Un graphique est un arbre iff:
> 1. **Nombre de bords** = `n – 1` (nécessaire pour la connectivité).
> 2. **Aucun cycle** n ' existe.
> 3. Tous les nœuds sont accessibles depuis n'importe quel nœud de départ.

---

Détails de la mise en œuvre

C'est pas vrai. Java – Union-Find

"Java
Importation de java.util.*;

solution de classe publique {
Booléen public valideTree(int n, int[][] bords) {
si (longueur des bords != n - 1) retourner faux; // test de comptage des bords

int[] parent = nouveau int[n];
Arrays.fill(parent, -1); // chaque noeud est sa propre racine

pour (int[] e : bords) {
int root1 = find(parent, e[0]);
int root2 = find(parent, e[1]);

si (root1 == root2) retourne false; // cycle détecté

parent[root1] = root2; // union
}
retour vrai;
}

privé int find(int[] parent, int i) {
si (parent[i]] -1) retour i;
retour parent[i] = find(parent, parent[i]); // compression du chemin
}
}
«» "

**Pourquoi c'est bon* *
- Temps linéaire, pas de problèmes de profondeur de récursion.
- Compact, n'utilise qu'un seul tableau.

**Potentiel
- Oui. Si vous oubliez `edges.length == n-1` vous pouvez faussement retourner `true` sur un graphique déconnecté.

**Souple partie**
- La compression de trajectoire est un peu terre mais essentielle pour la performance.

---

Python – DFS (récursif)

'`python
de taper l'importation Liste

Solution de classe:
def valide Arbre(même, n: int, bords: Liste[Liste[int]]) -> Bool:
si len(edges) != n - 1:
Retour Faux

adj = [[] pour _ dans l'intervalle(n)]
pour u, v dans les bords:
adj[u].appendice(v)
Annexe(u)

visité = set()

def dfs(node: int, parent: int) -> C'est vrai.
pour proche en adj[node]:
Si proche == parent: # sauter le bord que nous venons de
poursuivre
si près en visite:
retour Faux cycle # back‐edge →
visit.add(voix)
si ce n'est pas dfs(voix, nœud):
Retour Faux
retour Vrai

visité.add(0)
si ce n'est pas dfs(0, -1):
Retour Faux
retour len (visité) == n
«» "

**Pourquoi c'est bon* *
- Clair, facile à lire.
- Poigne de petits graphiques confortablement.

Les pièges *
- Profondeur de récursion (`n` peut être 2000) – Limite de récursion par défaut de Python ~1000, vous pouvez donc frapper `RecursionError`.
- Utilisez `sys.setrecursionlimit` si vous restez récursif.

**
- Construire la liste d'adjacence prend une mémoire supplémentaire ('O(n + m)'), mais inévitable pour le DFS/BFS.

---

C++ – BFS (Itératif)

'`cpp
#incluez <vecteur>
#incluez <queue>
utilisant l'espace de noms std;

solution de classe {
public:
bool validTree(int n, vector<vector<int>>& bords) {
si (edges.size() != n - 1) retourner false; // contrôle du nombre de bords

vecteur<vecteur<int>> adj(n);
pour (auto &e : bords) {
adj[e[0]].push_back(e[1]);
adj[e[1]].push_back(e[0]);
}

vecteur<int> visité(n, 0);
file d'attente <int> q;
q.push(0);
visité[0] = 1;

pendant que (!q.vide()) {
noeud int = q.front(); q.pop();
pour (int nei : adj[node]) {
si (visité[nei]) {
si (nei != noeud) retourner faux; // cycle trouvé
poursuivre;
}
visité[nei] = 1;
q.push(nei);
}
}
pour (int v : visité) si (!v) retourner faux; // déconnecté
retour vrai;
}
};
«» "

**Pourquoi c'est bon* *
- Itératif → aucune limite de récursion.
- Détection explicite du cycle ('visited[nei]').

**Bad**
- Un peu plus de verbe que Union-Find ; mais la clarté gagne.

**Désormais**
- Dupliquer les entrées d'adjacence peut gaspiller quelques octets; pas un gros problème.

---

Analyse de complexité

L'approche Temps Espace
- C'est quoi ?
Autres L'Union Java – Finition **O(n + m)**
Python DFS **O(n + m)**
C++ BFS **O(n + m)**

Tous répondent aux contraintes confortablement.

---

Les bons, les mauvais et les affreux

Aspect du bien
- C'est quoi ?
**Sobriété algorithmique**= Union‐Find est un contrôle du nombre de bords après un liner. DFS/BFS nécessitent une liste d'adjacence; plus de plaque de chaudière. Autres
**Échelle**= Temps linéaire; aucun problème de profondeur de récursion. Récursif DFS peut frapper la limite de récursion dans Python.
**Le code Java est concis. Python DFS est extrêmement lisible. C++ BFS est verbeux mais clair. Autres
**Sécurité des caisses**Le test de comptage des bords empêche les graphiques déconnectés. Impossible de vérifier la connectivité → faux positifs. Même chose.
**Utilisation de la mémoire** O(n + m) pour la dépendance. Même chose.

---

Les derniers départs

- **Le nombre d'Edge** est le premier garde.
- **Détection des cycles**: Union-Find ou DFS/BFS.
- **Connectivité**: vérifier tous les nœuds visités (ou `m == n-1` + vérification du cycle le garantit).

---

Article sur le blog optimisé du SEO

> **Titre**: *LeetCode 261 – Arbre graphique valide: Union-Find, DFS et BFS en Java, Python & C++ *
> **Meta Description**: Découvrez comment résoudre le LeetCode 261 avec trois implémentations propres en Java, Python et C++. Comprendre les compromis et les stratégies prêtes à l'entrevue.

---

Aperçu de l'article

1. **Intro** – Qu'est-ce qu'un arbre valide? Pourquoi LeetCode 261 compte pour les entrevues.
2. **Récapitulation des problèmes** – Contraintes, format d'entrée, exemples.
3. **Stratégie** – Détection des bords et des cycles.
4. **Solution 1 – Java Union‐Find** – Code + explication.
5. **Solution 2 – Python DFS** – Code + notes de récursion.
6. **Solution 3 – C++ BFS** – Code + approche itérative.
7. ** Analyse de complexité** – Tableaux et discussion.
8. **Bien, mal, mal** – Feuille de triche rapide.
9. **Conseils pour les entrevues** – Parlez par algorithme, discutez des cas de bord, écrivez un code propre.
10. **Conclusion** – Résumé et prochaines étapes (pratique plus de problèmes graphiques).

- Oui. Extrait de blog

> **Comprendre le LeetCode 261**
> Un arbre *valide* est un graphique à la fois *connecté* et *acyclique*. Pour les nœuds `n`, un arbre doit avoir exactement les bords `n-1`. Ce simple fait se transforme en un puissant raccourci: si le nombre de bords diffère, nous pouvons retourner `faux` immédiatement. Il reste à faire en sorte qu'il n'y ait pas de cycles.
>
> **Pourquoi l'union?**
> La structure de données Disjoint Set Union (DSU) nous permet de fusionner des composants en un temps presque constant. En ajoutant chaque bord, nous vérifions si les deux paramètres partagent déjà une racine. Si elles le font, ajouter le bord créerait un cycle → retourner `false`. Après avoir traité tous les bords, un arbre est garanti sif `m == n-1` et aucun cycle n'a été trouvé.

*(Continuer avec des extraits de code, des explications et des conseils d'entrevue.) *

---

Dépôt de code final

Les trois solutions sont prêtes à copier-coller:

Langue Fichier Lien
C'est quoi ?
Autres Java (https://gist.github.com/) Autres
[GitHub Gist] (https://gist.github.com/) Autres
[GitHub Gist] (https://gist.github.com/) Autres

> Remplacer le nom de classe `Solution` par celui que votre plateforme attend (LeetCode utilise habituellement `Solution`).

Bon codage et bonne chance d'atterrissage ce travail de rêve! C'est ce qu'il a dit