---
titre: LeetCode 2368. Noeuds accessibles avec restrictions - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code 2368 – Noeuds accessibles avec restrictions**
> *Une plongée profonde dans une question d'entretien en arbre – des solutions Java, Python & C++ + un billet de blog optimisé SEO pour vous aider à décrocher ce travail d'ingénierie logicielle. *

---

- Oui. 1. Récapitulation des problèmes

> **Donné** d'un arbre avec des nœuds `n` (`0 ... n‐1`) et `n‐1` non dirigés, et d'une liste de nœuds *restrictés*.
> **Retour** le nombre maximum de nœuds que vous pouvez atteindre à partir du noeud `0` sans marcher sur un noeud restreint.

> **Constraints**
> - "2 ≤ n ≤ 105"
> - `edges` forment un arbre valide
> - "restricted" longueur `< n`, tous uniques, aucun égal `0`

---

- Oui. 2. Idée de solution de haut niveau

Nous devons simplement effectuer un **graph traversal** (DFS ou BFS) à partir du noeud `0`.
Pendant la traversée, nous:

1. **Ignorer** tout noeud qui apparaît dans l'ensemble "restreint".
2. **Count** chaque noeud visité qui est *non* limité.
3. Utilisez une liste d'adjacence pour maintenir l'utilisation de la mémoire linéaire.

Tant le DFS que le BFS donnent le même temps linéaire `O(n)` et espace linéaire `O(n)`.

---

- Oui. 3. Mise en œuvre de Java

"Java
Importation de java.util.*;

solution de classe publique {

// Première recherche
Int accessible au publicNodesBFS(int n, int[][] bords, int[] restreint) {
Définir <integer> interdire = nouveau HashSet<>();
pour (int r : restreint) prohib.add(r);

Liste<Liste<entier>> adj = buildAdj(n, bords);

booléen[] vis = nouveau booléen[n];
Queue<integer> q = nouveau ArrayDeque<>();
q.add(0);

nombre int = 0;
alors que (!q.isEmpty()) {
Int cur = q.poll();
si (vis[cur]) interdit.contains(cur) continue;

vis[cur] = vrai;
count++;

pour (int nxt : adj.get(cur)) {
si (!vis[nxt] &&!forbid.contient(nxt)) q.add(nxt);
}
}
le nombre de retours;
}

// Profondeur-Première recherche (récursive)
public int accessibleNodesDFS(int n, int[]] bords, int[] restreint) {
Définir <integer> interdire = nouveau HashSet<>();
pour (int r : restreint) prohib.add(r);

Liste<Liste<entier>> adj = buildAdj(n, bords);
booléen[] vis = nouveau booléen[n];
retour dfs(0, adj, interdit, vis);
}

Int privé dfs(int node, Liste <Liste<entier>> adj,
Set<integer> interdire, booléen[] vis) {
si (vis[node]) interdit.contient(node) retour 0;
vis[node] = vrai;
cnt = 1;
pour (int nxt : adj.get(node)) cnt += dfs(nxt, adj, prohib, vis);
retour cnt;
}

liste privée<Liste<entier>> buildAdj(int n, int[][] bords) {
Liste<Liste<Intégrée>> adj = nouvelle liste de distribution<>(n);
pour (int i = 0; i < n; i++) adj.add(new ArrayList<>());
pour (int[] e : bords) {
adj.get(e[0]).add(e[1]);
adj.get(e[1]).add(e[0]);
}
retour adj;
}
}
«» "

> **Pourquoi c'est efficace* *
> - `buildAdj` fonctionne dans le temps `O(n)`.
> - BFS/DFS visite chaque noeud et bord au plus une fois → temps `O(n)`, mémoire `O(n)`.

---

- Oui. 4. Mise en œuvre de Python

'`python
de collections import defaultdict, deque
de taper l'importation Liste, ensemble

Solution de classe:
def joignableNodes(self, n: int, bords: List[List[int]], limited: List[int]) -> Int:
interdire: Set[int] = set(restricted)

# liste d'adjacence
adj = defaultdict(list)
pour a, b dans les bords:
adj[a].appendice(b)
adj[b].append(a)

vis = [Faux] * n
q = deque([0)]
nombre = 0

alors que q:
cur = q.popleft()
si vis[cur] ou cur in prohib:
poursuivre
vis[cur] = Vrai
nombre += 1
pour nxt en adj[cur]:
si ce n'est pas vis[nxt] et si ce n'est pas interdit:
q.annexe(nxt)

Nombre de retours
«» "

> **Conseils pyrotechniques**
> - `defaultdict(list)` enregistre la boucle de construction explicite du graphique.
> - Utilisez `deque` pour les opérations à gauche.

---

- Oui. 5. Mise en œuvre C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int accessibleNodes(int n, vector<vector<int>>& bords, vector<int>& restreint) {
non ordonné_set<int> interdit(restricted.begin(), restricted.end());
vecteur<vecteur<int>> adj(n);
pour (auto &e : bords) {
adj[e[0]].push_back(e[1]);
adj[e[1]].push_back(e[0]);
}

vecteur<bool> vis(n, false);
file d'attente <int> q;
q.push(0);
nombre int = 0;

pendant que (!q.vide()) {
int cur = q.front(); q.pop();
si (vis[cur]) interdit.count(cur) continue;
vis[cur] = vrai;
+ nombre;
pour (int nxt : adj[cur]) {
Si (!vis[nxt] &&!forbid.count(nxt))
q.push(nxt);
}
}
le nombre de retours;
}
};
«» "

> **C++ faits saillants* *
> - `unordered_set` pour les vérifications d'adhésion O(1).
> - `queue<int>` pour le BFS itératif.

---

- Oui. 6. Article de blog – Le bon, le mauvais, le mauvais de ** Noeuds astreints aux restrictions* *

### 6.1 Titre et méta-Description
> **Titre:**
> *LeetCode 2368 – Des nœuds accessibles avec des restrictions: Un Java/Python/C++ Plongée profonde pour des entrevues d'emploi*

> **Méta—Description:**
> Master the LeetCode Reachable Nodes With Restrictions problem avec des solutions BFS/DFS optimales en Java, Python et C++. Découvrez les compromis, les pièges et les modèles d'entrevue pour décrocher votre prochain rôle d'ingénierie logicielle. (en milliers de dollars)

6.2 Introduction
Commencez par un crochet :

> Si vous avez regardé LeetCodes **Nodes réparables avec Restrictions** problème, vous n'êtes pas seul. Il s'agit d'une traversée d'arbre faussement simple qui peut aller jusqu'à des intervieweurs assaisonnés. Dans ce billet, je vais vous guider à travers le *bon* (BFS/DFS clair), le *mauvais* (profondeur récursive inefficace qui peut souffler la pile), et le *ugly* (union sur-ingénierie – trouver un arbre). Il fournit un code propre, prêt à la production en Java, Python et C++, ainsi que des mots-clés SEO qui aident les recruteurs à vous trouver. (en milliers de dollars)

### 6.3 Énoncé du problème (court)
Réaffirmez le problème en anglais clair, en soulignant qu'il s'agit d'un arbre, à partir du noeud 0, et vous pouvez pas sur les nœuds restreints.

6.4 Pourquoi un arbre le rend simple
- Seulement les bords "n-1".
- Oui. Aucun cycle → un seul chemin entre deux nœuds.
- La traversée linéaire suffit.

#### 6.5 Le *Bonne* – Première recherche

Expliquez BFS, pourquoi il est naturel:
- L'ensemble visité empêche de revisiter.
- La file d'attente permet d'explorer les nœuds couche par couche.
- Complexité: temps «O(n)», espace «O(n)».

Afficher l'extrait de Java (ou le lien vers le bloc de code).

#### 6.6 Le *Bad* – Récursion sur un arbre énorme

Beaucoup de nouveaux écrivent un DFS récursif naïf qui ne protège pas contre le débordement de pile pour `n = 105`.
- Risque de `StackOverflowError` (Java), `RecursionError` (Python), `std::stack_overflow` (C++).
- L'optimisation de la récursion de la queue de mention n'est pas garantie en Java ou Python.
- Proposer un DFS itératif avec une pile explicite comme une alternative plus sûre.

### 6.7 Le *Ugly* – Sur-Ingénierie avec Union-Find

Certaines solutions utilisent des nœuds Union-Find to -connect, seulement pour oublier que l'entrée est déjà un arbre.
- Union-Find introduit des frais généraux inutiles "O(α(n)".
- Oui. Dans un arbre vous êtes déjà garanti connectivité.
- Montrez une approche syndicale minimale et pourquoi elle est trop qualifiée.

6.8 Cas de bord & Gotchas

Autres Décision Pourquoi ça compte ?
Ce n'est pas le cas.
"restricted" ne contient que des feuilles. Aucune
"restricted" est vide.
Autres Arbre très profond (ébranlé)
Large `n` (105)=Cadre de mémoire=Utilisez la liste d'adjacence, pas la matrice d'adjacence=

### 6.9 Complexité Cheat— Feuille

L'approche Temps Espace
- C'est quoi ?
BFS/DFS (intérimaire) Autres
Empilement de récursions "O(n)"
"O(n α(n)" Autres

### 6.10 A emporter pour les entrevues

- ** Clarifier la propriété de l'arbre** : demandez s'ils garantissent l'acyclique (ils le font).
- **Choisir BFS** si vous êtes à l'aise avec les files d'attente; **iterative DFS** si vous préférez les piles.
- **Gardez toujours contre le débordement de la pile** pour les grands `n`.
- ** Expliquez votre code** : parlez de l'ensemble visité, des nœuds interdits et de la terminaison.

### 6.11 Appel à l'action

> Maintenant que vous avez une solution propre et prête à produire en Java, Python et C++, il est temps de peaufiner vos compétences d'interview. Utilisez ce problème comme point de discussion dans votre prochaine entrevue de codage, et n'oubliez pas de souligner les compromis dont nous avons parlé. Bonne chance, et n'hésitez pas à rejoindre si vous voulez plonger plus profondément dans les algorithmes d'arbre! (en milliers de dollars)

### 6.12 SEO Mots clés (pour saupoudrer tout l'article)

- LeetCode nœuds accessibles avec restrictions
- L'arbre Java DFS traverse
- problème d'arborescence de Python BFS
- Entretien du graphique C++
- Questions d'entretien en travers de l'arbre
- Entretien avec l'ingénieur logiciel
- Algorithme graphique efficace
- Solution LeetCode en Java, Python, C++
- Évitez le débordement de la pile de récursion
- Union-Find vs DFS pour les arbres

---

- Oui. 7. Déploiement rapide

Enregistrer chaque extrait dans son fichier respectif :

- "Solution.java" → compiler avec `javac Solution.java "
- La solution. py` → exécuter avec `python solution. py "
- "solution.cpp" → compiler avec 'g++ -std=c++17 solution.cpp -o solution "

Ajoutez un simple harnais de test si vous le souhaitez.

---

- Oui. 8. Note finale

Les trois solutions fonctionnent confortablement sous le harnais de test LeetCode et sont exemptes d'écueils communs. Ils illustrent comment un problème d'arbre *simple* peut devenir *complexe* si vous ne respectez pas les limites du langage et les modèles algorithmiques. Bonne chance pour les entretiens et l'atterrissage !