---
titre: LeetCode 1192. Connexions critiques dans un réseau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Connexions critiques dans un réseau – LeetCode 1192
**Une plongée profonde dans les ponts, l'algorithme de Tarjan, et comment aser cette question d'entrevue* *

> **Mots clés:** *Critical Connections in a Network, LeetCode 1192, bridge finding, Tarjan algorithme, fiabilité du réseau, solution Java, solution Python, solution C++, entretien d'ingénieur logiciel, préparation d'entretien d'emploi*

---

- Oui. 1. Aperçu du problème

> **LeetCode 1192 – Connexions critiques dans un réseau**
> **Difficulté:** Dur

Vous recevez un graphique connecté non dirigé avec des nœuds (serveurs) **`n`** numérotés de **0** à **n‐1** et une liste de **`connections`** où chaque connexion est un tableau de 2 éléments `[a, b]`.
Une connexion **critique** (ou **bridge**) est un bord qui, s'il est enlevé, augmente le nombre de composants connectés.
Retournez toutes les connexions critiques dans n'importe quel ordre.

> **Constraints**
2 ≤ n ≤ 105
> * n - 1 ≤ connexions longueur ≤ 105
0 ≤ ai, bi < n
> * ai
> * Pas de rebords dupliqués

---

- Oui. 2. Pourquoi ce problème est-il difficile?

C'est bien, c'est mal.
C'est pas vrai.
**Il faut comprendre la théorie des graphes** – pas un simple DFS ou BFS. **La complexité du temps** doit être **O(V + E)** – l'élimination de la force brute de chaque bord est O(V·E)
**L'algorithme de Tarjan est un classique**Les grandes tailles d'entrée** – la profondeur de récursion peut atteindre 105** **Cas d'Edge** – noeuds isolés, composants multiples, auto-boucles (pas permis ici mais mérite d'être gardé)
**Les interviews l'adorent** – présente la résolution de problèmes, les structures de données. **Besoin de liste d'adjacence** – l'abus peut conduire à un coup de mémoire.

---

- Oui. 3. Idée de base – Algorithme de recherche du pont de Tarjan

1. **DFS traversant** avec horodatage (`tin`) quand un nœud est visité pour la première fois.
2. ** Valeur de liaison faible** (`low[u]`) = plus petit timestamp accessible depuis `u` en utilisant **au plus un bord arrière**.
3. Lorsque vous explorez un bord `u → v` (bord de l'arbre), après être revenu de `v`, si `low[v] > tin[u]`, le bord `(u, v)` est un pont.
4. Pour les bords arrière, mettre à jour `low[u]` avec `tin[v]`.

Cela fonctionne dans le temps **O(V + E)** et la mémoire **O(V + E)** (liste d'adjacence + pile de récursion).

---

- Oui. 4. Mise en œuvre du code

Ci-dessous vous trouverez des solutions propres et prêtes à la production dans **Java, Python et C++**.
Tous les trois utilisent la même logique de Tarjan, sont commentés pour la clarté, et traitent les contraintes maximales en toute sécurité.

---

#### 4.1 Java 17

"Java
Importation de java.util.*;

***
* Code Leet 1192 – Connexions critiques dans un réseau
*
* Heure : O(V + E)
* Espace : O(V + E) (liste des dépendances + pile de récursion)
*/
solution de classe {
Liste privée <Liste<entier>> résultat; // liste des ponts
liste privée<enteger>[] graphique; // liste d'adjacence
Int[] étain privé; // temps d'entrée
valeur d'int privé faible; // lowlink
minuterie interne privée;

Liste publique<Liste<entier>> critiquesConnexions(int n, Liste<Liste<entier>> connexions) {
// Créer une liste d'adjacence
graphe = nouvelle liste de répartition[n];
pour (int i = 0; i < n; i++) graphe[i] = nouvelle liste de distribution<>();
pour (Liste <Integer> conn : connexions) {
u = conn.get(0), v = conn.get(1);
graphic[u].add(v);
graphic[v].add(u);
}

étain = nouvelle int[n];
faible = nouvelle int[n];
Tableau.fill(tin, -1); // -1 = non visité
minuteur = 0;
résultat = nouvelle liste de distribution<>();

// Le graphique est garanti pour être connecté, mais nous effectuons DFS à partir de 0
dfs(0, -1);

le résultat du retour;
}

vide privé dfs(int u, int parent) {
tin[u] = low[u] = timer++; //
pour (int v : graph[u]) {
si (v == parent) continue; // ne retourne pas à parent
si (tin[v]] -1) { // bord de l'arbre
dfs(v, u);
low[u] = Math.min(low[u], low[v]);
si (faible[v] > étain[u]) {
result.add(Arrays.asList(u, v)); // (u, v) est un pont
}
} autre { // bord arrière
faible[u] = Math.min(faible[u], étain[v]);
}
}
}
}
«» "

---

#### 4.2 Python 3.10+

'`python
de taper l'importation Liste

Solution de classe:
"""
Code du leet 1192 – Connexions critiques dans un réseau
Heure : O(V + E)
Espace : O(V + E)
"""
def criticalConnexions(self, n: int, connexions: Liste[Liste[int]]) -> Liste[Liste[int]]:
# Créer une liste d'adjacence
graphique = [[] pour _ dans l'intervalle(n)]
pour u, v dans les connexions:
graphic[u].append(v)
graphic[v].append(u)

étain = [-1] * n
faible = [0] * n
minuterie = 0
ponts = []

def dfs(u: int, parent: int) -> Aucun:
minuterie non locale
étain[u] = faible[u] = minuteur
minuterie += 1
pour v dans le graphique[u]:
si v == parent:
poursuivre
si tin[v]] # bord de l'arbre
dfs(v, u)
faible[u] = min(faible[u], faible[v])
si faible[v] > étain[u]:
bridges.append([u, v])
Autre: # bord arrière
faible[u] = min(faible[u], étain[v])

dfs(0, -1)
ponts de retour
«» "

> **Astuce:** Sur LeetCode, définissez une limite de récursion plus élevée (`sys.setrecursionlimit(200000)`) si vous touchez une erreur de profondeur de récursion.

---

### 4.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

***
* Code Leet 1192 – Connexions critiques dans un réseau
* Heure : O(V + E)
* Espace : O(V + E)
*/
solution de classe {
public:
vector<vector<int>> criticalConnexions(int n, vector<vector<int>>& connections) {
// Créer une liste d'adjacence
vecteur<vector<int>> graphique(n);
pour (auto &e : connexions) {
u = e[0], v = e[1];
graphic[u].push_back(v);
graphic[v].push_back(u);
}

vecteur<int> étain(n, -1), faible(n, 0);
la minuterie int = 0;
les ponts vecteurs<vector<int>>;

fonction<vit(int,int)> dfs = [&](int u, parent int) {
tin[u] = low[u] = timer++;
pour (int v : graph[u]) {
si (v) le parent continue;
si (tin[v]] -1) { // bord de l'arbre
dfs(v, u);
faible[u] = min(faible[u], faible[v]);
si (faible[v] > étain[u])
bridges.push_back({u, v});
} autre { // bord arrière
faible[u] = min(faible[u], étain[v]);
}
}
};

dfs(0, -1); // graphique est connecté
les ponts de retour;
}
};
«» "

---

- Oui. 5. Exécution des solutions sur les essais d ' échantillons

Test de langue Résultat
- C'est quoi ?
Java, `n = 4`, `connections = [[0,1],[1,2],[2,0],[1,3]``[[1,3]` Autres
"[[1,3]]" Autres
C++ Autres

Tous les trois produisent le(s) pont(s) attendu(s) indépendamment de l'ordre.

---

- Oui. 6. Liste de contrôle des cas de bord

1. **Arête unique** (`n = 2`, `[0,1]]`) → toujours un pont.
2. ** Graphique entièrement connecté** (graphique complet) → aucun pont.
3. **Graphique avec plusieurs composants** (bien que le problème garantisse la connectivité).
4. **Recursion profonde** (graphique en chaîne) → définir la limite de récursion / taille de la pile.
5. **Large `n`** (105) → itérative BFS n'est pas nécessaire; la profondeur de récursion est égale `n` dans le pire des cas; la taille de la pile typique (~1 MB) est suffisante pour 105 sur la plupart des plateformes.

---

- Oui. 7. Pourquoi cet algorithme se trouve-t-il dans les entrevues

- **Cadre algorithmique classique** (DFS + lowlink) qui met en valeur les connaissances en graphes profondes.
- **Explication claire**: vous pouvez marcher un recruteur à travers `tin`, `low`, et l'état du pont.
- **Scalable**: s'adapte aux contraintes du LeetCode et aux systèmes de production.
- **Réutilisable**: le même noyau fonctionne pour *points d'articulation*, *composants fortement connectés*, etc.

---

- Oui. 8. Paragraphe à emporter optimisé SEO

Si vous préparez une entrevue d'ingénierie logicielle, maîtrisez **Critical Connections in a Network (LeetCode 1192)** est un must. Ce problème difficile teste votre compréhension de l'algorithme de recherche de ponts**, **DFS traversal** et **lowlink valeurs**. En implémentant des solutions propres dans **Java, Python et C++**, vous démontrez la polyvalence et la profondeur que recherchent les recruteurs de caractères clés. Assurez-vous de mettre en évidence votre capacité à gérer de grandes entrées, éviter les débordements de pile, et expliquer l'intuition de l'algorithme. Ces points vous sépareront et vous aideront à décrocher ce travail.

---

### TL;DR

- Utilisez l'algorithme ** de Tarjan pour trouver des ponts en O(V + E).
- Implémenter dans **Java, Python ou C++** avec des listes d'adjacence.
- Poignez soigneusement la profondeur de récursion et les grandes entrées.
- Montrez la solution dans votre interview pour impressionner les gestionnaires d'embauche.

Bon codage – et bonne chance pour votre prochaine entrevue!