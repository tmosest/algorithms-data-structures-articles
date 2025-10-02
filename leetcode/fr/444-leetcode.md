---
titre: LeetCode 444. Reconstruction des séquences -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 444 – Reconstruction des séquences
**Un topologique Tri + Unicité Vérifiez que fonctionne en Java, Python & C++**

> **Mots clés**: LeetCode 444, Reconstruction de séquence, Tri topologique, Ordre topologique unique, BFS/Kahn, DFS, Théorie des graphiques, Codage Interview, Java, Python, C++.

---

- Oui. 1. Récapitulation des problèmes

> **Don**
> - `nums` – une permutation de `[1 ... n] "
> - `séquences` – une liste de subséquences qui apparaissent dans `nums`

> **Retour** **iff** `nums` est *la seule super-séquence la plus courte qui contient chaque subséquence dans `séquences`.

Il s'agit de déterminer si l'ordre en "nums" est *uniquement déterminé* par les contraintes de prépondérance due aux "séquences". Si c'est le cas, la seule super-séquence la plus courte valide est exactement «nums»; autrement, il y a au moins une autre commande valide.

---

- Oui. 2. Pourquoi un tri topologique?

Chaque subséquence `[a, b, c]` nous dit que
«» "
a → b → c
«» "
est un bord dirigé défini dans un graphique de nœuds `n` (les nombres).
Le problème est de savoir si **le graphique a un ordre topologique unique** qui équivaut à "nums".

Si l'ordre topologique du graphique est unique, il doit être le même que le nombre.
S'il n'est pas unique, il existe au moins deux super-séquences valides et `nums` ne peut pas être la seule plus courte.

---

- Oui. 3. Aperçu de l'algorithme

1. **Construire le tableau graphique et indegree* *
Pour chaque paire d'éléments consécutifs dans chaque séquence, ajoutez un bord dirigé et mettez à jour les degrés.

2. **Le tri topologique BFS avec contrôle d'unicité* *
* Maintenez une file d'attente de nœuds avec le degré 0.
* A chaque étape, si la file d'attente a **plus d'un noeud**, la commande est *pas* unique → retourner `faux`.
* Pop le nœud unique, l'ajouter à l'ordre, et diminuer les degrés de ses voisins, en faisant la demande de tout qui tombe à 0.

3. **Validité**
* Si la longueur finale de l'ordre est « n », le graphique est incomplet (certains nœuds n'apparaissent jamais dans les séquences), retourner « faux ».
* Comparez `commande` avec `nums`. Si elles correspondent, `vrai`; sinon `faux`.

---

- Oui. 4. Preuve d ' exactitude

Nous prouvons que l'algorithme renvoie `true` **iff** `nums` est la seule super-séquence la plus courte.

Lemma 1
Si l'algorithme retourne `false` parce que la file d'attente contient jamais ≥ 2 nœuds, alors l'ordre partiel défini par `sequences` admet plus d'un ordre topologique.

*Proof. *
À cette étape, deux nœuds distincts `x` et `y` ont au degré 0, ce qui signifie qu'aucune contrainte de préséance ne dicte leur ordre relatif. Par conséquent, les deux extensions `[ ..., x, y, ... ]` et `[ ..., y, x, ... ]` sont valides, donnant deux superséquences différentes. *

Lemma 2
Si l'algorithme se termine par un ordre unique `order`, alors `order` est l'ordre topologique *only* du graphique.

*Proof. *
L'algorithme de Kahns explore tous les bords. Le contrôle d'unicité garantit qu'à chaque étape, un seul nœud est admissible, de sorte que l'ordre relatif de deux nœuds est fixé par des décisions antérieures. Il n'existe donc pas d'ordre alternatif. *

Lemma 3
Si l'ordre topologique unique est égal à "nums", alors "nums" est la seule super-séquence la plus courte.

*Proof. *
Toute superséquence doit respecter les bords. Un ordre topologique est une super-séquence la plus courte du graphique car il contient chaque vertex exactement une fois. Puisqu'il n'y a qu'un seul ordre de ce genre et qu'il équivaut à des «nums», aucune autre superséquence plus courte ne peut exister. *

Lemma 4
Si `nums` est la seule super-séquence la plus courte, alors l'algorithme retournera `true`.

*Proof. *
Supposons le contraire : l'algorithme retourne « faux ».
- L'une ou l'autre des files d'attente avait des nœuds ≥ 2 par Lemma 1 plus d'une super-séquence existe une contradiction.
- Oui. Ou la longueur de l'ordre final, n'apparaissent jamais certains vertex dans les "séquences"; alors nous pourrions insérer ce vertex n'importe où sans casser les subséquences, ce qui donne une autre contradiction de superséquence.
Ainsi l'algorithme doit retourner `true`.

La combinaison de Lemmas 2-4 donne l'instruction *if et seulement si*. *

---

- Oui. 5. Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
Graphique de construction (tous bords)
BFS de Kahn **O(n + E)**
Total **O(n + E)**

Avec `n ≤ 104` et `="séquences[i]=" ≤ 105`, la solution s'adapte confortablement dans les limites.

---

- Oui. 6. Traitement des cas de bord

Autres Décision Pourquoi ça compte ?
Ce n'est pas le cas.
"nums" pas de permutation.
Autres Un nombre n'apparaît jamais dans aucun subséquence.
Aucun bord → n'importe quel ordre valide → algorithme retourne `false`
Nous utilisons un `Set` par noeud ou un contrôle avant d'ajouter `if (adj[u].add(v)) l'indeg[v]++;» Autres

---

- Oui. 7. Exécution

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.
Les trois utilisent la même logique et courent dans le même temps asymptotique.

---

#### 7.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
séquence booléenne publiqueReconstruction(int[] nombres, Liste<Liste<entier>> séquences) {
int n = longueur nums;
Liste<Set<Integer>> adj = nouvelle liste de distribution<>(n + 1);
int[] indieg = nouvelle int[n + 1];
pour (int i = 0; i <= n; i++) adj.add(new HashSet<>());

// Graphique de construction
pour (Liste <Integer> suite : séquences) {
pour (int i = 0; i + 1 < suiv.size(); i++) {
u = suiv.get(i);
int v = suiv.get(i + 1);
si (adj.get(u).add(v)) endeg[v]++;
}
}

// Kahn avec contrôle d'unicité
Deque<integer> q = nouveau ArrayDeque<>();
pour (int i = 1; i <= n; i++) {
si (indeg[i]] 0) q.offre(i);
}

Int idx = 0;
alors que (!q.isEmpty()) {
si (q.size() > 1) retourner faux; // choix multiples -> pas unique
Int cur = q.poll();
si (cur != nums[idx]) retourner false; // ordre incorrect
idx++;
pour (int nei : adj.get(cur)) {
si (--indeg[nei]) 0) q.offre(nei);
}
}
retourner idx == n; // s'assurer que tous les nœuds sont traités
}
}
«» "

---

7.2 Python

'`python
de collections import defaultdict, deque
de taper l'importation Liste

Solution de classe:
def sequenceReconstruction(self, nombres: List[int], séquences: List[List[int]]) -> Bool:
n = len(nums)
adj = defaultdict(set)
endeg = [0] * (n + 1)

# Construire le graphique
pour les séquences suivantes:
pour u, v dans zip(seq, seq[1:]):
si v n'est pas dans adj[u]:
Adj[u].add(v)
endeg[v] += 1

Kahn avec contrôle d'unicité
q = deque([i pour i dans l'intervalle(1, n + 1) si indég[i] == 0])
idx = 0

alors que q:
si len(q) > 1 :
retour Faux # commande non unique
cur = q.popleft()
si cur != nombres[idx]:
retour fausse erreur de commande #
idx += 1
pour nei in adj[cur]:
indig[nei] -= 1
si indég[nei] == 0:
q.annexe(nei)

retourner idx == n
«» "

---

### 7.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
séquence boolReconstruction(vecteur<int>& nombres, vecteur<vecteur<int>& séquences) {
int n = nombres.size();
vecteur<unordered_set<int>> adj(n + 1);
vecteur<int> indég(n + 1, 0);

// Graphique de construction
pour (auto &seq : séquences) {
pour (size_t i = 0; i + 1 < sq.size(); ++i) {
int u = suite[i], v = suite[i + 1];
si (adj[u].insert(v).second) // inséré avec succès
++indég[v];
}
}

// Kahn avec contrôle d'unicité
file d'attente <int> q;
pour (int i = 1; i <= n; ++i)
si (indeg[i]] 0) q.push(i);

Int idx = 0;
pendant que (!q.vide()) {
si (q.size() > 1) retourner faux; // plusieurs candidats
int cur = q.front(); q.pop();
si (cur != nums[idx]) retourner false; // ordre incorrect
++idx;
pour (int nei : adj[cur]) {
si (--indeg[nei]) 0) q.poush(nei);
}
}
retour idx == n;
}
};
«» "

---

- Oui. 8. Bon, mauvais, et humble

Aspect du bien
- C'est quoi ?
**Temps**=Linéaire en `n + E`=0 Aucune=0
**Espace**
**Readability**
Autres **Edge‐Manipulation de cas**
**Piège commun**= Oublier de comparer avec `nums` pendant le BFS==Surregarder le contrôle d'unicité (`q.size() > 1`)== Utilisation de DFS sans détection de cycle → faux positifs==

---

- Oui. 9. Pourquoi cela compte dans les entrevues

- **Graphiques fondamentaux**: Comprendre les bords dirigés, les degrés, le genre topologique.
- **Vérification de l'utilité**: Une touche subtile au-delà d'une sorte de topologique.
- **Complexité** : les données du monde réel peuvent atteindre 105 bords ; vous devez rester linéaire.
- ** Compétences en codage**: Nettoyer les implémentations Java/Python/C++ montrent la maîtrise des fonctionnalités linguistiques (sets, deques, unordered_set).

Montrez cette solution sur votre portfolio ou lors d'un entretien technique pour démontrer à la fois la perspicacité algorithmique et la compétence pratique de codage.

---

10. OBJECTIFS OBLIGATOIRES En haut

Si vous préparez une entrevue de codage, la maîtrise **LeetCode 444 – Sequence Reconstruction** vous donne un avantage **unique**.
- **Amants de Java** : voir une liste d'adjacence propre basée sur "Set".
- **Python** pros: un seul liner `deque` plus `defaultdict`.
- **C++** gourous: `unordered_set` et `queue` rendent la logique croquante.

Rappelez-vous le processus **deux étapes**:
1. **Construire un graphique dirigé à partir des sous-séquences**.
2. **Appliquer l'algorithme de Kahns avec un garde unique**.

Votre réponse finale sera rapide, efficace sur le plan de la mémoire et robuste contre tous les cas de bord.
Ajoutez ceci à votre curriculum vitæ, à votre curriculum vitæ ou à vos notes d'entrevue :*séquence* votre façon de réussir !

Bon codage ! C'est ce qu'il a dit.

---

* Fin de la solution. *