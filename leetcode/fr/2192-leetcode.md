---
titre: LeetCode 2192. Tous les ancêtres d'un nœud dans un graphique acyclique dirigé -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Tous les ancêtres d'un nœud dans un graphique acyclique dirigé
**LeetCode 2192 – Moyen**

> **Problème:**
> Avec un DAG avec des nœuds `n` (0-basé) et une liste de bords `edges`, retournez une liste où
> `answer[i]` contient *tous* ancêtres du noeud `i` dans l'ordre ascendant.
> Un noeud `u` est un ancêtre de `v` s'il y a un chemin dirigé de `u` à `v`.

---

1.1 Pourquoi ce problème est important pour les entrevues

- *Graphiques fondamentaux* – tri topologique, DFS, BFS
- *Programmation dynamique sur DAGs* – fusion des ensembles d'ancêtres
- * compromis entre l'espace temporel et l'espace temporel "
- Démonstrations **Codage propre**: listes d'adjacence, tri, fonctions d'aide modulaire

> **Référence de référence**: *LeetCode 2192 solution*, *Problème de l'ancêtre DAG*, *interview d'algorithme graphique*, *exemple Java Python C++*, *mise en œuvre du tri topologique*

---

- Oui. 2. Intuition et idée fondamentale

Le graphique est un DAG, donc nous pouvons traiter des nœuds dans l'ordre **topologique**.
Lorsque nous visitons un nœud 'v`, nous connaissons déjà les ensembles d'ancêtres de tous ses prédécesseurs.
L'ensemble des ancêtres de "v" est l'union de:

1. Tous les ancêtres prédécesseurs
2. Le prédécesseur luimême

Nous stockons l'ensemble des ancêtres de chaque noeud comme un `bitset` (ou un `Set<int>`) pour permettre une union rapide et pour garder les données petites.
Enfin, nous convertissons chaque bitset en une liste triée.

---

- Oui. 3. Algorithme (Topological-DP)

Texte
1. Créer une liste d'adjacence `adj[v] = liste d'enfants`.
2. Calculer le degré de chaque noeud.
3. Algorithme de Kahns → tableau `topo` avec un ordre topologique.
4. Pour chaque nœud `v` dans `topo`:
pour chaque enfant `c` de `v`:
les ancêtres[c] ← les ancêtres[c]
les ancêtres[c] ← les ancêtres[c]
5. Pour chaque nœud `v`: convertir `ancetstors[v]` en vecteur trié.
«» "

Complexité

Étape Temps Espace
C'est pas vrai.
Construire le graphique Autres
Type topologique Autres
L'ancêtre fusionnant l'ancêtre `O(n2)` (plus mauvais cas `n` ancêtres par noeud) Autres
Conversion finale (tri de chaque liste) Autres

Avec les limites données (`n ≤ 1000`, `m ≤ 2000`), cela fonctionne facilement en < 200 ms.

---

- Oui. 4. Mise en œuvre des références

Voici des solutions propres, commentées et prêtes à être collées dans **Java**, **Python** et **C++**.

---

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
Liste publique<Liste<Intégrée>> getAncestors(int n, int[][] bords) {
// 1. Créer une liste d'adjacence
Liste<Liste<entier>> adj = nouvelle liste de distribution<>();
pour (int i = 0; i < n; i++) adj.add(new ArrayList<>());
int[] indieg = nouvelle int[n];
pour (int[] e : bords) {
adj.get(e[0]).add(e[1]);
endeg[e[1]]++;
}

// 2. Ordre topologique via Kahn
Queue<integer> q = nouveau ArrayDeque<>();
pour (int i = 0; i < n; i++) si (indeg[i]] 0) q.offre(i);
Liste <Integer> topo = nouvelle liste de distribution<>(n);
alors que (!q.isEmpty()) {
int v = q.poll();
l'annexe II est modifiée comme suit:
pour (int nb : adj.get(v))
si (--indeg[nb]) 0) q.offre(nb);
}

// 3. Ensembles d'ancêtres
@SuppressAvertissements("non vérifié")
BitSet[] anc = nouveau BitSet[n];
pour (int i = 0; i < n; i++) anc[i] = nouveau BitSet(n);

// 4. PDD over topo order
pour (int v : topo) {
pour (int nb : adj.get(v)) {
anc[nb].or(anc[v]); // hérite de tous les ancêtres
anc[nb].set(v); // ajouter l'ancêtre direct
}
}

// 5. Convertir en Liste<Liste<entier>>
Liste <Liste<Intégrée>> res = nouvelle liste <>();
pour (int i = 0; i < n; i++) {
Liste <Integer> tmp = nouvelle liste d'array<>();
pour (int j = anc[i].nextSetBit(0); j >= 0; j = anc[i].nextSetBit(j + 1))
l'alinéa j);
res.add(tmp); // déjà trié en raison de l'ordre bit
}
retour rés;
}
}
«» "

---

4.2 Python

'`python
de collections import deque, defaultdict
de taper l'importation Liste

Solution de classe:
def getAncestors(self, n: int, bords: List[List[int]]) -> Liste[Liste[int]]:
1. Adjacence + degré
adj = [[] pour _ dans l'intervalle(n)]
endeg = [0] * n
pour u, v dans les bords:
adj[u].appendice(v)
endeg[v] += 1

2. Ordre des topo
q = deque([i pour i dans l'intervalle(n) si indég[i] == 0])
topo = []
alors que q:
v = q.popleft()
topo.append(v)
pour nb dans adj[v]:
endeg[nb] -= 1
si indég[nb] 0:
q.annexe(nb)

# 3. Ensembles d'ancêtres – utilisez Python ensemble pour la clarté
anc = [set() pour _ dans la plage(n)]

# 4. PDD
pour v in topo:
pour nb dans adj[v]:
ANC[nb].update(anc[v]) # hérite
anc[nb].add(v) # ancêtre direct

# 5. Trier chaque liste
retour [trié(liste(s)) pour s in anc]
«» "

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<vector<int>> getAncestors(int n, vector<vector<int>>& bords) {
// 1. Graphique + degré
vecteur<vecteur<int>> adj(n);
vecteur<int> indég(n, 0);
pour (auto &e : bords) {
adj[e[0]].push_back(e[1]);
endeg[e[1]]++;
}

// 2. Kahn
file d'attente <int> q;
pour (int i = 0; i < n; ++i) si (indeg[i]) 0) q.push(i);
vecteur<int> - le droit d'auteur;
pendant que (!q.vide()) {
l'entrée v = q.front(); q.pop();
topo.push_back(v);
pour (int nb : adj[v]) {
si (--indeg[nb]) 0) q.push(nb);
}
}

// 3. Les bits de l'ancêtre
vector<bitset<1000>> anc(n); // 1000 est le maximum n

// 4. PDD
pour (int v : topo) {
pour (int nb : adj[v]) {
anc[nb]= anc[v];
le nom de l'autorité compétente de l'État membre d'origine;
}
}

// 5. Convertir en vecteurs triés
vecteur<vecteur<int>> ans(n);
pour (int i = 0; i < n; ++i) {
pour (int j = anc[i]._Find_first(); j < n; j = anc[i]._Find_next(j))
le nom de l'autorité compétente;
}
le retour des an;
}
};
«» "

> **Note :**
> *C++* utilise une constante de compilation `1000` pour la taille des bits. Si vous préférez le calibrage dynamique, passez à `vector<unordered_set<int>>` ou `vector<set<int>>`, mais soyez conscient des frais généraux plus élevés.

---

- Oui. 5. Suppléant Brute-Force DFS (O(n·m))

Si vous préférez un DFS direct qui suit l'idée originale d'atteindre tous les descendants, voici une version compacte qui correspond toujours aux limites.

### 5.1 Java (version DFS)

"Java
solution de classe publique {
Liste publique<Liste<Intégrée>> getAncestors(int n, int[][] bords) {
Liste<Liste<entier>> adj = nouvelle liste de distribution<>();
pour (int i = 0; i < n; i++) adj.add(new ArrayList<>());
pour (int[] e : bords) adj.get(e[0]).add(e[1]);

Liste <Liste<Intégrée>> res = nouvelle liste <>();
pour (int i = 0; i < n; i++) res.add(new ArrayList<>());

pour (int src = 0; src < n; src++) {
booléen[] vis = nouveau booléen[n];
dfs(src, src, adj, res, vis);
}

pour (Liste<Intégre> liste : res) Collections.sort(liste);
retour rés;
}

vide privé dfs(int src, int cur, Liste<Liste<entier>> adj,
Liste<Liste<entier>> res, booléen[] vis) {
vis[cur] = vrai;
pour (int nxt : adj.get(cur)) {
Si (!vis[nxt]) {
res.get(nxt).add(src); // src est un ancêtre de nxt
dfs(src, nxt, adj, res, vis);
}
}
}
}
«» "

5.2 Python

'`python
Solution de classe:
def getAncestors(self, n: int, bords: List[List[int]]) -> Liste[Liste[int]]:
adj = [[] pour _ dans l'intervalle(n)]
pour u, v dans les bords:
adj[u].appendice(v)

res = [[] pour _ dans l'intervalle(n)]

def dfs(src, cur, visité):
visité[cur] = Vrai
pour nb en adj[cur]:
si elle n'est pas visitée[nb]:
res[nb].annexe(src)
dfs(src, nb, visité)

pour src dans la plage(n):
Dfs(src, src, [Faux] * n)

retour [trié(lst) pour lst in res]
«» "

C++

'`cpp
vector<vector<int>> getAncestors(int n, vector<vector<int>>& bords) {
vecteur<vecteur<int>> adj(n);
pour (auto &e : bords) adj[e[0]].push_back(e[1]);

vecteur<vecteur<int>> ans(n);
pour (int src = 0; src < n; ++src) {
vecteur<bool> vis(n, false);
fonction<vit(int)> dfs = [&](int cur) {
vis[cur] = vrai;
pour (int nb : adj[cur]) {
si (!vis[nb]) {
le nom de l'utilisateur,
dfs(nb);
}
}
};
dfs(src);
}
pour (auto &vec : ans) tri(vec.begin(), vec.end());
le retour des an;
}
«» "

> **Performance** – Ces solutions basées sur le DFS sont `O(n2)` dans le pire des cas, mais elles sont souvent plus rapides en pratique lorsque le graphique est clairsemé (`m`). Ils sont formidables à montrer *simple logique* et *récursion* aux intervieweurs.

---

- Oui. 6. Bonne, mauvaise et laid – Ce que les intervieweurs À propos

Aspect du bien
- C'est quoi ?
Autres **L'utilisation de listes d'adjacence**=Keeps memory low and operations `O(1)` per edge=Keep.
**Topological trie**= Garantit que les données antérieures sont prêtes===== Oublier les degrés → boucle infinie====Profondeur de la récursion > 1000 → débordement de la pile
**Bitset / Set fusion**= Union rapide, faible frais généraux==== Utiliser `vector<int>` pour fusionner → `O(n3)`===== Gestion manuelle de la mémoire en C++ (manquant `std::unique`) Autres
**Désorption du résultat** → Mauvaise réponse

> **À emporter :**
> La solution DP-on-DAG (topologique + bitset) est *la plus propre* et *la plus rapide* pour les contraintes.
> La version DFS‐from‐each‐node est plus simple à comprendre, mais peut être plus lente sur les DAG denses.
> **Souvenez-vous toujours**: dans le codage d'entrevue, une solution *simple* correcte bat souvent une solution intelligente mais buggy.

---

- Oui. 7. Et si... – Cas de bord & Extensions

Traitement des bords Autres
- Oui.
Autres **Pas de bords** (`m=0`)=" L'ordre topo est `[0,1...,n‐1]`; chaque liste d'ancêtres reste vide. Autres
** Graphique de la chaîne** («0→1→2→...») Chaque noeud accumule les ancêtres `O(n)`; bitset gère l'union dans `O(n)` chacun. Autres
**Les plus grands ensembles d'ancêtres** Autres
**Plusieurs cas d'essai**. Autres

---

- Oui. 8. Comment utiliser ces solutions pour *Entretien d'emploi* Prép

1. **Lisez attentivement le problème** – Comprendre la définition d'un ancêtre.
2. ** Tirez un ordre topologique** – Écrivez-le sur papier; cela vous aidera à vérifier l'étape DP.
3. **Écrire le code dans la langue de votre choix** – Utilisez les extraits ci-dessus comme modèle.
4. **Vérifier localement** – Utilisez le diagramme de chaîne d'échantillonnage et les cas sans ancrage.
5. ** Expliquez votre logique** – Dans une interview, passez à travers l'algorithme, pas seulement le code.
5. ** Mettre en avant l'efficacité** – Montrez comment l'utilisation de listes de bits ou d'adjacence permet d'économiser du temps et de l'espace.

* *Pratique:* Essayez d'implémenter une variation où vous devez également afficher le chemin le plus long* qui n'utilise que les bords de l'ancêtre.
Autres *Entretien de masse:* Paire le programme avec un ami et explique chaque étape en anglais simple.

---

- Oui. 9. Lecture et ressources supplémentaires

Pourquoi ça aide ?
C'est pas vrai.
[Code Leet 1736 – 1736. Trouver dans Mountain Array](https://leetcode.com/problemset/problem/1736) Pratiquer la recherche binaire + DP sur les tableaux. Autres
(https://www.geeksforgeeks.org/topological-sorting/) Explication classique de l'algorithme de Kahn. Autres
[cppreference – `std::bitset`](https://en.cppreference.com/w/cpp/utility/bitset) (en anglais seulement) Autres
(https://stackoverflow.com/questions/1045924/graph-representation-in-c) Discute des listes d'adjacence par rapport aux matrices. Autres
(https://www.youtube.com/watch?v=YzZgZt9qGvA) (en anglais seulement). Autres

---

- Oui. 9. TL;DR – Résumé d'une condamnation

*La solution la plus rapide et efficace pour LeetCode 1736 est d'effectuer un tri topologique, d'utiliser un bitset/`std::bitset` pour fusionner les ensembles d'ancêtres dans le temps linéaire, puis de sortir des listes triées; la variante DFS‐from‐each‐node est plus simple mais peut être plus lente sur des graphiques denses. *

---

- Oui. 10. Mot final

*Vous êtes maintenant équipé à la fois des *optimal* et *simple* façons de résoudre LeetCode 1736.
Rappelez-vous : la clé des entrevues de codage d'acing est un algorithme **clair et correct** et *explain‐vos-pensées* qui vous montrent vraiment comprendre le domaine de problème. *

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit.

---



---

11 ans. FAQ

**Q1: Pourquoi ne pas utiliser une structure de données de recherche syndicale? * *
R1: Union‐find est idéal pour les composants *connectés*, pas pour les relations avec les ancêtres dirigés. L'approche DP-on-DAG est l'ajustement naturel pour les graphiques acycliques dirigés.

**Q2: Le code bitset C++ sera-t-il compilé avec `-std=c++17`?**
A2: Oui, mais vous devez définir la taille au moment de la compilation (par exemple, `bitset<1000>`). Pour la dynamique `n`, considérez `vector<bitset<1000>>` ou `vector<unordered_set<int>>`.

**Q3: Que faire si l'entrée utilise des indices basés sur 1? **
A3: Convertissez tous les sommets en 0 avant de construire le graphique, ou ajustez le résultat en conséquence (p. ex., ajoutez 1 à chaque indice de la sortie).

**Q4: Y a-t-il un algorithme gourmand? * *
A4: Aucun algorithme avide ne produira les ensembles d'ancêtres corrects car vous devez considérer tous les chemins. L'approche PDD est la solution avide dans le sens de prendre tous les ancêtres qui ont déjà été pris. (en milliers de dollars)

---

12. Pensée de clôture

> Dans les algorithmes graphiques, pensez toujours à un ordre topologique. Une fois que vous avez cela, beaucoup de problèmes deviennent embarrassants simple. *

Codage heureux et profiter de casser le puzzle des ancêtres DAG! (en milliers de dollars)

---