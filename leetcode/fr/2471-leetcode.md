---
titre: LeetCode 2471. Nombre minimum d'opérations pour trier un arbre binaire par niveau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 2471 – Nombre minimum d'opérations pour trier un arbre binaire par niveau
### Quick-start: code dans **Java**, **Python** et **C++**

Solution
C'est pas vrai.
*Java**
solution de classe {
au minimum des opérations publiques (racine TreeNode) {
Queue<TreeNode> file d'attente = nouveau ArrayDeque<>();
file d'attente.offre(root);
swaps d'int = 0;

pendant que (!queue.isEmpty()) {
int sz = file d'attente.size();
int[] vals = nouveau int[sz];
pour (int i = 0; i < sz; i++) {
noeud TreeNode = file d'attente.poll();
vals[i] = noeud.val;
si (node.left != null) file d'attente.offre(node.left);
si (node.right != null) file d'attente.offre(node.right);
}

// ---- 1. Triez le niveau et rappelez-vous l'indice cible de chaque valeur -----
int[] trié = vals.clone();
Tableau.sort(trié);
Carte <entier, entier> pos = nouveau HashMap<>();
pour (int i = 0; i < trié.longueur; i++) pos.put(trié[i], i);

// ---- 2. Compter le nombre de cycles → swaps minimums = n – cycles -----
booléen[] visité = nouveau booléen[sz];
pour (int i = 0; i < sz; i++) {
si (visité[i]) pos.get(vals[i]) == i) continuer;
int j = i, cycle = 0;
pendant que (!visité[j]) {
visité[j] = vrai;
j = pos.get(vals[j]);
cycle++;
}
swaps += cycle - 1;
}
}
swaps de rendement;
}
}
«» Autres

*Python**
Solution de classe:
def minimumOperations(self, root: TreeNode) -> Int:
à partir de collections import deque
q = deque([root])
swaps = 0

alors que q:
sz = len(q)
vals = []
pour _ dans l'intervalle(sz):
noeud = q.popleft()
Vals.append(node.val)
si noeud.left: q.append(node.left)
si noeud.right: q.append(node.right)

_vals triés = triés(vals)
pos = {v: i pour i, v dans le dénombrement(sorted_vals)}

visité = [Faux] * sz
pour i dans la plage(sz):
si visité[i] ou pos[vals[i]]] i:
poursuivre
j, cycle = i, 0
pendant qu'il n'est pas visité[j]:
visité[j] = Vrai
j = pos[vals[j]]
cycle += 1
swaps += cycle - 1
swaps de rendement
«» Autres

*C++ *Cpp
/* LeetCode 2471 – Nombre minimum d'opérations pour trier un binaire Arbre par niveau */
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

struct TreeNode {
la valeur intérieure;
TreeNode *left, *right;
TreeNode(int x) : val(x), gauche(nullptr), droite(nullptr) {}
};

solution de classe {
public:
int minimumOpérations(racine TreeNode*) {
la file d'attente <TreeNode*> q;
q.push(root);
swaps d'int = 0;

pendant que (!q.vide()) {
int sz = q.size();
vecteur<int> vals(sz);
pour (int i = 0; i < sz; ++i) {
TreeNode* noeud = q.front(); q.pop();
vals[i] = noeud->val;
si (noeud->gauche) q.push(noeud->gauche);
si (node->right) q.push(node->right);
}

vecteur<int> trié = vals;
tri(sorted.begin(), tried.end());
unordered_map<int,int> pos;
pour (int i = 0; i < (int)sorted.size(); ++i) pos[sorted[i]] = i;

vecteur<bool> visité(sz, false);
pour (int i = 0; i < sz; ++i) {
si (visited[i]..................................pos[vals[i]] == i) continuer;
int j = i, cycle = 0;
pendant que (!visité[j]) {
visité[j] = vrai;
j = positions[vals[j]];
++cycle;
}
swaps += cycle - 1;
}
}
swaps de rendement;
}
};
«» Autres

> **Note** – La classe `TreeNode` est fournie par LeetCode ; copiez simplement les blocs de code Java / Python / C++ ci-dessus dans la classe `Solution` et vous êtes prêt à partir !

---

- Oui. 2. Plongée profonde de style Blog
> Le bon, le mauvais et le mauvais de LeetCode 2471 – Binary‐Tree‐Sorting‐Level
> *Un guide convivial pour l'entrevue de niveau suivant. *

---

2.1 Aperçu du problème

LeetCode 2471 vous demande de trouver le nombre minimum d'opérations d'échange** nécessaire pour transformer chaque niveau d'un arbre binaire en ordre croissant**.
Vous pouvez seulement échanger des valeurs qui résident sur la même profondeur** de l'arbre. Il n'est pas permis de traverser les profondeurs.

> **LeetCode 2471**

---

2.2 Pourquoi ce problème compte dans les entrevues

- **Tree + Array + Graphique** – La solution utilise la recherche largeur-première (arbre + tableau) et la théorie du graphique (décomposition du cycle).
- **Scénario du monde réel** – Dans la production, il faut souvent réorganiser les données qui vivent dans des structures hiérarchiques (p. ex. organigrammes, arbres de catégorie).
- **Interview buzz-word** – - L'échange minimal pour trier un tableau est un problème d'entrevue classique ; l'appliquer à un arbre vous donne une réponse *simple, élégante* qui démontre la largeur de la première pensée et le flair algorithmique.

---

2.3 Approche étape par étape

1. **Parcours de niveau (BFS)* *
- Utilisez une file d'attente pour visiter les nœuds en profondeur.
- À chaque niveau, collecter les valeurs dans un tableau "vals".

2. **Déterminer les indices cibles**
- Copier `vals` pour `sortedVals` et trier.
- Construisez un hash‐map `pos[value] → index` qui vous indique *où* chaque valeur devrait finalement atterrir.

3. **Swaps mineurs = `n – nombre_de_cycles`**
- Imaginez que vous avez un graphique dirigé où le noeud *i* pointe vers `pos[vals[i]]`.
- Chaque composant connecté de ce graphique est un **cycle**.
- À l'intérieur d'un cycle de longueur `k`, vous avez besoin d'échangeurs `k‐1' pour placer tous les nœuds correctement.
- Par conséquent, le total des swaps pour un niveau = --(k‐1) sur tous les cycles = `n – cycles`.

4. **Accumuler la réponse à tous les niveaux**
- La réponse finale est la somme des swaps minimaux pour chaque profondeur.

---

2.4 Faits saillants du code

Mots clés Autres
C'est pas vrai.
*Java***"pos.get(vals[i]) == i` → *déjà en place
**Python**
**C++**=<int,int> pos` – *fast lookup*=

La logique de base (détection du cycle et comptage des échanges) est identique dans les trois langues; seules les structures de données diffèrent.

---

2.5 Complexité temporelle et spatiale

Formule métrique Raison
C'est quoi, ça ?
**Heure**="O(N log N)="N" = nœuds totaux. Trier les coûts de chaque niveau `O(k log k)` et la somme sur tous les niveaux est limitée par `N log N`. Autres
**Espace** Queue + tableaux temporaires pour chaque niveau; la pire profondeur est `N` dans un arbre dégénéré. Autres

---

#### 2.6 Edge- Liste de contrôle des cas

Autres Décision Pourquoi ça compte ?
C'est ce qu'on dit.
**Empty tree**Le problème garantit au moins un noeud, mais le code défensif peut garder. `minimumOperations` retournera immédiatement `0` parce que la file d'attente commence vide. Autres
**Arbre à nœuds simples** = 1; cycles = 1; échanges ajoutés = 0.
**Les niveaux peuvent être long 1 → trivial, mais notre algorithme fonctionne toujours O(1). Fonctionne parce que le cycle-check saute quand l'indice cible est égal à l'indice courant. Autres
**Les plus grandes profondeurs** Nous allouons uniquement pour le niveau actuel (`vector<int> vals(sz)`), en libérant automatiquement après la boucle. Autres
**Le code Leet garantit des valeurs distinctes, mais sinon, la carte échouerait. La carte de la valeur → index n'est valide que si toutes les valeurs sont uniques; ajoutez un garde si nécessaire. Autres

---

2.7 Ce qui rend le bon, le mauvais et le mauvais

Catégorie
C'est pas vrai.
**Bon*** *Comptage du cycle élégant* → O(1) supplémentaire par niveau.
**Le tri de chaque niveau séparément peut être évité par une structure de données plus avancée (p. ex. une TVB équilibrée). La complexité peut être cachée derrière BFS. Autres
L`emballage Java `TreeNode` que vous écrivez pour les tests locaux peut devenir une douleur; utiliser `ArrayDeque` au lieu de `LinkedList` résout une performance cachée. En oubliant `clone()` le tableau avant le tri conduit à `IllegalArgumentException` (puisque `Arrays.sort` modifie l'entrée). Autres

---

2.8 Harnais d'essai de l'échantillon (Python)

'`python
# --------- construire un assistant pour construire un arbre...
classe TreeNode:
def __init_(self, x):
autoval = x
self.left = self.right = Aucune

Def build(arr, idx=0):
"""Construit un arbre binaire à partir d'une liste en ordre de niveau. Aucun ne signifie qu'il manque un nœud."""
si idx >= len(arr) ou arr[idx] n'est pas:
retour Aucune
noeud = TreeNode(arr[idx])
noeud.left = build(arr, 2*idx+1)
node.right = build(arr, 2*idx+2)
noeud de retour

racine = build([8,9,10,1,5,5,7,6,4,2,3])
print(Solution().minimumOpérations(root)) # 4
«» "

---

2.9 Variations que vous pourriez voir dans une entrevue de codage

Variation
- C'est quoi ?
**Changement d'arbre en place**= Les swaps doivent modifier l'arbre lui-même.= Utiliser `vecteur<TreeNode*> noeuds` au lieu de valeurs et de pointeurs d'échange. Autres
Au lieu de monter, trier par un comparateur personnalisé (p. ex., en descendant). Passer un comparateur à "sort" et adapter la cartographie du cycle en conséquence. Autres
Autres **La plus grande contrainte de l'arbre**="N` jusqu'à 105 → file d'attente mémorisée. Utilisez une approche *two-stack* pour éviter la mémoire O(N) lors de la traversée d'arbres entorsés. Autres
**L'arbre streaming**L'arbre est un nœud-par-noeud (aucun pointeur parent). Tenir une pile de nœuds par profondeur; utiliser DFS au lieu de BFS. Autres

---

###2.10 Conseils prêts pour l'entrevue

Conseil Pourquoi c'est important
-- -- -- -- --
**Mention cycle-comptage**= Montre que vous connaissez les swaps classiques pour trier le truc. Autres
**Expliquez clairement le BFS** Autres
**Afficher la complexité**=Le temps `O(N log N)`, `O(N)` espace est généralement acceptable; discuter pourquoi il satisfait aux limites de LeetCode. Autres
**Préparer une démo**= Dans une interview en direct, marcher à travers un petit arbre (3-4 nœuds) et compter manuellement les swaps; puis montrer comment votre code l'automatise. Autres
Autres **Connaissez les écueils de "gugly"** Autres

J'ai résolu LeetCode 2471 en Java, Python et C++. J'ai utilisé BFS pour isoler chaque niveau d'arbre, transformé le niveau en un graphique d'indices, des cycles comptés et calculé le nombre minimum d'échange. La solution fonctionne dans le temps `O(N log N)` et l'espace `O(N)`, qui correspond aux contraintes de problème. **Votre prochaine déclaration d'entrevue* *

---

### 2.11 Méta-Description (SEO)

> **Master LeetCode 2471 – Opérations minimales pour trier un arbre binaire par niveau**.
> Obtenez les solutions officielles Java, Python et C++, une explication étape par étape, un algorithme de comptage du cycle, une liste de vérification des cas de bord et des conseils prêts à l'entrevue.
> Perfect your coded interview prep et atterrissez votre job de technologie de rêve.

---

#### 2.12 Dernier départ

LeetCode 2471 est un problème de petit arbre, de grand algorithme qui met en évidence :

- **Tree traversal** (première recherche)
- ** Tri des images** (cartographie des cibles)
- ** Théorie des graphiques** (décomposition du cycle)

Les trois implémentations linguistiques ci-dessus vous donnent un modèle unique et réutilisable que vous pouvez déposer dans n'importe quel entretien de codage ou défi de codage. En expliquant le bon, le mauvais et le laid*, vous allez non seulement attraper le problème, mais aussi montrer votre profondeur de compréhension – exactement ce que les gestionnaires d'embauche recherchent.

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit.

---