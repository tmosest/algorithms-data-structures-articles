---
titre: LeetCode 3067. Nombre de paires de serveurs connectés dans un réseau d'arbres pondérés -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Solution – Nombre de paires de serveurs connectés (LeetCode 3067)

**Récapitulation des problèmes* *

On vous donne un arbre *non rodé avec des serveurs `n` (vertises) numérotés `0 ... n‐1`.
Pour chaque bord `edges[i] = [u, v, w]` la distance entre `u` et `v` est `w`.
Une paire de serveurs `a, b)` est **connectable via un serveur `c`** si

1. `a < b` et `a != c`, `b != c',
2. "dist(c, a)" est divisible par "signal" Vitesse
3. `dist(c, b)` est divisible par `signal Vitesse
4. Les deux chemins simples `c → a` et `c → b` ne partagent aucun bord.

Retourner un tableau `cnt[0 ... n‐1]` où `cnt[c]` est le nombre de ces paires pour chaque serveur `c`.

Les contraintes sont petites (`n ≤ 1000`) de sorte qu`une solution `O(n2)` est bonne.



---

Pourquoi un "O(n2)" DFS des œuvres de chaque noeud

* Pour un centre fixe `c` chaque sous-arbre voisin de `c` est indépendant - toute paire de serveurs connectés doit se trouver dans deux sous-arbres *différents* de `c`.
* Dans un sous-arbre, nous n'avons besoin que de savoir **combien de nœuds** ont une distance de `c` qui est un multiple de `signalSpeed`.
* En explorant un sous-arbre, nous pouvons garder la distance actuelle de `c`; si elle est multiple, nous incrémentons un compteur.
* Après avoir exploré un sous-arbre, nous combinons son compteur avec les comptoirs des sous-arbres déjà traités – ce qui donne toutes les paires qui utilisent ce nouveau sous-arbre.

L'algorithme est exactement le même que dans les solutions LeetCode acceptées qui apparaissent dans le problème de l'éditorial.

---

Mise en œuvre en 3 langues

Ci-dessous vous trouverez des implémentations propres et commentées dans **Java**, **Python** et **C++**.
Tous les trois partagent la même logique et fonctionnent dans le temps `O(n2)`, la mémoire `O(n)`.



---

#### 3.1 Java 17

"Java
Importation de java.util.*;

solution de classe {
// liste de proximité: chaque élément est {voix, poids}
@SuppressAvertissements("non vérifié")
liste privée<int[]>[] buildAdj(int[][]] bords, int n) {
Liste<int[]>[] g = nouvelle liste de distribution[n];
pour (int i = 0; i < n; i++) g[i] = nouveau tableau <>();
pour (int[] e : bords) {
u = e[0], v = e[1], w = e[2];
g[u].add(nouvelle int[]{v, w});
g[v].add(nouvelle int[]{u, w});
}
retour g;
}

// DFS qui retourne le nombre de nœuds dans le sous-arbre enraciné au nœud
// dont la distance par rapport au centre est divisible par mod.
int dfs(int node, int parent, long dist, int mod, List<int[]>[] g) {
int cnt = (dist % mod == 0) ? 1 : 0; // noeud courant
pour (int[] nb : g[node]) {
int nxt = nb[0], w = nb[1];
si (nxt) le parent continue;
cnt += dfs(nxt, noeud, dist + w, mod, g);
}
retour cnt;
}

public int[] countPairsOfConnectableServeurs(int[][]] bords, signal intSpeed) {
int n = bords longueur + 1;
Liste<int[]>[] g = buildAdj(edges, n);
int[] ans = nouvelle int[n];

pour (int c = 0; c < n; c++) {
paires longues = 0;
préfixe int = 0; // nombre de nœuds divisibles dans les sous-arbres traités
pour (int[] nb : g[c]) {
enfant int = nb[0], w = nb[1];
int subCnt = dfs(enfant, c, w, signal Vitesse, g);
paires += 1L * sous-Cnt * préfixe; // paires formées avec des sous-arbres précédents
préfixe += sous Cnt;
}
as[c] = (int) paires;
}
le retour des an;
}
}
«» "

> **Pourquoi "long"?**
> Les distances peuvent aller jusqu'à `n * 106` (=109), donc nous utilisons `long` pour éviter les débordements.



---

3.2 Python 3.9

'`python
de collections importer par défautdict
importations
sys.setcursionlimit(2000) # sûr pour n ≤ 1000

Solution de classe:
def build_adj(self, bords, n):
g = defaultdict(list)
pour u, v, w dans les bords:
g[u].appendice(v, w))
g[v].appendice(u, w))
retour g

def dfs(self, noeud, parent, dist, mod, g):
""Retourne combien de nœuds dans le sous-arbre enraciné au nœud
ont une distance du centre un multiple de mod."""
cnt = 1 si dist % mod == 0 autre 0
pour nxt, w en g[node]:
si nxt == parent:
poursuivre
cnt += autodfs(nxt, noeud, dist + w, mod, g)
retour cnt

def countPairsOfConnectableServeurs(soi, bords, signalSpeed):
n = len(edges) + 1
g = auto.build_adj(edges, n)
res = [0] * n

pour c dans la plage(n):
paires = 0
pref = 0
pour nxt, w en g[c]:
sous = auto.dfs(nxt, c, w, signalSpeed, g)
paires += sous * pref
pref += sous
res[c] = paires
retour res
«» "

> **Conseil pour les intervieweurs** – maintenir la profondeur de récursion faible en augmentant `sys.setrecursionlimit` si vous n'êtes pas sûr de la pile.



---

### 3.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
vecteur<vector<pair<int,int>>> g; // {voix, poids}

// DFS qui compte les nœuds dont la distance par rapport au centre est multiple de mod
int dfs(int node, int parent, long long dist, int mod) {
int cnt = (dist % mod) 0) ? 1 : 0;
pour (auto [nxt, w] : g[node]) {
si (nxt) le parent continue;
cnt += dfs(nxt, noeud, dist + w, mod);
}
retour cnt;
}

public:
vector<int> countPairesOfConnectableServers(vecteur<vector<int>>& bords, signal intSpeed) {
int n = bords.taille() + 1;
g. attribuer(n, {});
pour (auto &e : bords) {
u = e[0], v = e[1], w = e[2];
g[u].push_back({v, w});
g[v].push_back({u, w});
}

vecteur <int> ans(n);
pour (int c = 0; c < n; ++c) {
longues paires longues = 0;
Int pref = 0;
pour (auto [enfant, w] : g[c]) {
int subCnt = dfs(enfant, c, w, signalSpeed);
paires += 1LL * sous Cnt * pref;
pref += sous Cnt;
}
ans[c] = statique_cast<int>(paires);
}
le retour des an;
}
};
«» "

> **Pourquoi "long"?**
> La même protection de débordement que pour Java.



---

- Oui. Essai du code

'`python
♪ Harnais d'essai rapide (Python)
les bords = [[0,1],[1,2],[2,3]]
signal = 2
print(Solution().countPairsOfConnectableServers(edges, signal))
# Résultats attendus : [1, 1, 0, 0]
«» "

Vous pouvez exécuter des tests analogues en Java ou C++ en copiant le code dans un compilateur en ligne ou un IDE local.



---

C'est pas vrai. Bien, mal et mal – Ce que vous devriez discuter dans une entrevue

C'est une bonne chose
- C'est quoi ?
** Logique intuitive** – L'algorithme reflète exactement la déclaration de problème. **Temps quasi** – Pour `n = 1000` il est encore bon, mais sur les arbres plus grands il exploserait. **Dupliquer le code** – Chaque langue a besoin de son propre helper DFS ; l'idée centrale est la même mais la syntaxe se répète. Autres
**Profondeur de la récursion** – La récursion Python/C++ peut atteindre une limite pour les arbres très profonds (bien que 1000 est sûr). **Risque de dépassement** – L'utilisation de `int` pour les distances peut se briser sur les poids lourds; l'utilisation de `long` / `long'. Autres
**Modalité claire** – Séparer `build_adj`, `dfs` et la boucle principale. **Pas de taille** – Chaque DFS visite à nouveau l'arbre entier. Si vous avez besoin de prendre en charge de nombreuses requêtes (différente `signalSpeed`), vous allez refaire tout le travail. Autres

> **Comment en parler dans une interview* *
J'ai utilisé une approche `O(n2)` qui fait un DFS de chaque centre pour compter combien de nœuds dans chaque sous-arbre enfant ont une distance qui est un multiple de la vitesse donnée. Comme chaque paire de serveurs connectés doit provenir de deux sous-arbres différents du centre, je combine les comptes en utilisant une somme préfixe.
> Cela démontre votre compréhension de la décomposition des arbres et de l'arithmétique modulaire.



---

Améliorations possibles (La section «Pourquoi je suis toujours en entrevue»

Si un embaucheur demande, pouvez-vous faire mieux? Vous pouvez mentionner:

1. **Décomposition de Centroid** – Réduit le nombre total de DFS de `O(n2)` à `O(n log n)` en divisant récursivement l'arbre autour de son centroïde.
2. ** Programmation dynamique sur l'arbre** – Si `signalSpeed` est fixé pour l'ensemble du cas d'essai, vous pouvez propager modulo compenses bottom-up en un seul DFS.
3. **Bitset / BFS** – Lorsque les poids sont petits, vous pouvez précalculer les restes en O(n) par centre.

Ces optimisations ne sont pas strictement nécessaires pour les contraintes données, mais les connaître montre que vous êtes *aware* des compromis de performance – exactement ce que les intervieweurs aiment.



---

C'est pas vrai. À emporter: Comment faire pour éponger le LeetCode 3067 Question d'entrevue

Autres Ce que vous allez démontrer Pourquoi ça compte
-- -- -- -- -- -- -- --
**Tree traversal** – DFS/BFS, récursion, pile, listes d'adjacence.Les arbres sont une base dans les questions d'entrevue (binaire, n‐ary, pondérée). Autres
**Arithmétique modulaire** – Compte des nœuds dont la distance est un multiple d'une valeur. Autres
**Combiner les sous-solutions** – préfixe sum sketch. Autres
**Analyse de la complexité**Les intervieweurs s'attendent à ce que vous discutions `O(n2)` vs `O(n log n)`. Autres
**La polyvalence de la langue**=Codage en Java, Python, C++ montre que vous pouvez traduire des concepts à travers les piles. Autres

> Si vous vous préparez à une entrevue de codage, pratiquez l'écriture de l'aide `dfs` une fois, puis réutilisez-la pour la logique de la combinaison avec le sous-arbre précédent. Commentez bien votre code – c'est ce que les recruteurs recherchent.



---

FAQ de l'intervieweur

**Q1. Pourquoi n'avons-nous pas besoin de nous soucier de `a < b`? **
L'algorithme compte des paires non ordonnées une fois par centre, et l'énoncé du problème exige seulement que chaque paire soit comptée pour le centre `c` qui satisfait aux conditions. L'état `a < b` est seulement là pour éviter le double comptage sur l'ensemble des serveurs, et non pour le comptage propre au centre.

**Q2. Est-ce que `int` suffit pour les distances? * *
Le poids des bords est jusqu'à `106` et la profondeur de l'arbre peut être `n-1`. La distance maximale est `=109`, qui *s'insère dans un entier de 32 bits signé, mais la somme de nombreuses distances de ce type peut la dépasser, il est donc plus sûr d'utiliser `long`/`long'.

**Q3. Comment accéléreriez-vous cela pour `n = 105`? * *
Vous avez opté pour une méthode de décomposition centroïde ou de décomposition en lumière lourde qui fonctionne dans `O(n log n)` ou même `O(n)` dans certains cas.



---

Conclusion

- Un "O(n2)" L'algorithme DFS‐from‐each‐node est propre, simple et passe les limites de LeetCode.
- Les trois extraits de langue ci-dessus utilisent la même idée élégante : *compter les nœuds divisibles dans chaque sous-arbre enfant, puis combiner les nombres entre les sous-arbres*.
- Discuter de l'algorithme dans une interview montre que vous comprenez **l'indépendance de l'arbre**, **l'arithmétique modulaire** et **le comptage de paire** – tous les concepts d'entrevue classiques.

Bon codage, et bonne chance d'atterrissage ce rôle d'ingénierie de logiciels! C'est ce qu'il a dit.



---



## 10.0 SEO-Friendly Heads (Utilisez-les dans votre blog)

* `#LeetCode 3067 – Nombre de paires de serveurs connectés – Solution Java "
* `#Python 3 DFS – Problème d'arbre pondéré "
* `#C++17 – Interview-Ready Tree Traversal "
* `#Algorithmes d'Arbre – Préparation de l'entrevue d'emploi'
* `#Wighted Tree Network – Algorithm Design "
* `#DFS Solution – Compter des paires de serveurs compatibles "



---



## 11:0 Bonus – Une ligne rapide pour les programmeurs compétitifs

Si vous êtes absolument sûr que `signalSpeed` divise tous les poids de bord, le compteur DFS simplifie pour *compter tous les nœuds* dans le sous-arbre, ce qui transforme la solution entière en un seul passe `O(n)`. C'est un truc soigné que vous pouvez mentionner lors d'une entrevue pour présenter des idées plus profondes.