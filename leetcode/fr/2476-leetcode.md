---
titre: LeetCode 2476. Les nœuds les plus proches se posent des questions dans un arbre de recherche binaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2476. Les noeuds les plus proches se posent des questions dans un arbre de recherche binaire
### Code Leet La solution prête (Java-Python-C++)

---

TL;DR
* **Problème** – Pour chaque requête *q* trouver:
* *mini* = plus grande valeur ≤ *q* dans la TVB (ou **‐1** si aucune).
* *maxi* = valeur la plus faible ≥ *q* dans la TVB (ou **‐1** si aucune).
* **Approach** – Convertissez la BST en un tableau ** trié** (en ordre transversal) et utilisez la recherche binaire (`bisect`/`lower_bound`) pour chaque requête.
* **Complexité** –
*Temps* : **O(n + m log n)** ( *n* = #nodes, *m* = #demandes)
*Espace*: **O(n)** (pour le tableau trié)
* **Pourquoi c'est important** – Il montre une connaissance approfondie des propriétés de la BST, de la traversée des arbres et de la recherche efficace – parfait pour toute entrevue senior en ingénierie logicielle.

---

## 1--Déclaration du problème (Code de bord 2476)

> **Input**
> * `root` – racine d'un arbre de recherche binaire (BST).
> * `queries` – liste des entiers positifs.
> ** Sortie**
> Un tableau 2-D "réponse" où
> `answer[i] = [mini, maxi]` pour la requête *i*‐e.

> **Exemples**
> ```texte
> racine = [6,2,13,1,4,9,15,null,null,null,null,null,null,null,null,14]
> requêtes = [2,5,16]
> réponse = [[2,2],[4,6],[15,-1]]
> `` "

---

Intuition et conception

C'est bien C'est mal
C'est quoi, ça ?
**La propriété BST** – chaque enfant de gauche < parent < enfant de droite. Autres
**La traversée en ordre** donne un tableau trié → recherche binaire facile. **Le stockage d'un arbre entier** à nouveau (p. ex. TreeSet) est inutile. **La recherche binaire erronée** (erreurs hors-par-un) fausse l'identification des frontières. Autres
**`lower_bound` / `bisect`** trouver le premier élément ≥ cible. **La recherche binaire récursive complexe** à l'intérieur d'une boucle est plus difficile à déboguer. Autres

---

- Oui. Algorithme

1. **Traversez la BST en ordre** → `sortedVals`.
2. Pour chaque " q " dans les " requêtes " :
* `idx = lower_bound(sorted Vals, q)»
* `maxi = (idx < n) ? triéVals[idx] : -1'
* `mini = (idx > 0) ? triésVals[idx-1] : -1'
* Si `idx < n` et `sortedVals[idx] == q` → à la fois `mini` et `maxi` = `q`.
3. Ajouter `[mini, maxi]` au résultat.

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
En ordre de passage
Chaque requête (recherche binaire)
Total **O(n + m log n)**

* `n` = nombre de nœuds d'arbres (= 105)
* `m` = nombre de requêtes (= 105)

Le temps et la mémoire s'inscrivent facilement dans les limites de LeetCode.

---

C'est pas vrai. Mise en œuvre des références

### 5.1 Java (utilisation de `ArrayList` + recherche binaire)

"Java
Importation de java.util.*;

// Définition pour un nœud binaire.
classe TreeNode {
la valeur intérieure;
TreeNode gauche, droite;
TreeNode(int x) { val = x; }
TreeNode(int x, TreeNode l, TreeNode r) { val = x; gauche = l; droite = r; }
}

solution de classe {
// Construire un tableau trié via une traversée en ordre
vide privé dans l'ordre (noeud TreeNode, liste<integer> liste) {
si (noeud == nul) retour;
inorder(node.left, liste);
liste.add(node.val);
inorder(node.right, liste);
}

Liste publique<Liste<entier>> les plus prochesNodes(racine TreeNode, requêtes List<integer>) {
Liste<entier> triée = nouvelle liste d'array<>();
inorder(root, trié);

Liste <Liste<Intégrée>> ans = nouvelle liste <>();
int n = trié.size();

pour (int q : requêtes) {
int lo = 0, hi = n; // hi est exclusif
pendant que (lo < hi) { // recherche binaire
Int milieu = lo + (h - lo) / 2;
si (sorted.get(mid) < q) lo = milieu + 1;
Autre salut = milieu;
}
// lo est le premier indice avec valeur >= q (ou n)
int maxi = (lo < n) ? trié.get(lo) : -1;
int mini = (lo > 0) ? trié.get(lo - 1) : -1;

si (lo < n& tried.get(lo) == q) { // correspond exactement
Mini = maxi = q;
}
as.add(Arrays.asList(mini, maxi));
}
le retour des an;
}
}
«» "

> **Pourquoi ça marche* *
> *En ordre* donne une liste strictement ascendante parce que l'entrée est une BST.
> `lo` devient le **bound** inférieur – le plus petit indice avec `valeur ≥ q`.
> Les cas de bord (`lo==n`, `lo==0`) sont traités en vérifiant les limites.

---

#### 5.2 Python (en utilisant `bisect`)

'`python
de bisect importer bisect_left
de taper l'importation Liste, facultative

# Définition d'un noeud d'arbre binaire.
classe TreeNode:
def __init_(self, val:int=0, gauche:'TreeNode'=Aucun, droite:'TreeNode'=Aucun):
autoval = val
auto.gauche = gauche
soi.right = droit

Solution de classe:
def _inorder(self, noeud: Facultatif[TreeNode], arr: List[int]) -> Aucun:
si non noeud: retour
_inorder(node.left, arr)
Annexe(node.val)
_inorder(node.right, arr)

def le plus procheNodes(self, root: TreeNode, requêtes: List[int]) -> Liste[Liste[int]]:
_vals triés = []
Self._inorder(root, trié_vals)
n = len(vals triés)
res = []

pour q dans les requêtes :
idx = bisect_left(sorted_vals, q) # first >= q
maxi = trié_vals[idx] si idx < n autre -1
mini = trié_vals[idx-1] si idx > 0 autre -1

si idx < n et triés_vals[idx] == q: # correspond exactement
Mini = maxi = q
Annexe([mini, maxi])
retour res
«» "

> `bisect_left` implémente la même logique que la recherche binaire Java, mais dans un monoligneur.

---

C++ (En utilisant `vecteur` + `bound_lower`)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

// Définition pour un nœud binaire.
struct TreeNode {
la valeur intérieure;
TreeNode *left, *right;
TreeNode(int x) : val(x), gauche(nullptr), droite(nullptr) {}
};

solution de classe {
vide dans l'ordre (nœud TreeNode*, vecteur <int>& v) {
si (!node) retour;
order(node->left, v);
v.push_back(node->val);
order(node->right, v);
}
public:
vector<vector<int>> le plus procheNodes(racine TreeNode*, requêtes vector<int>) {
vecteur<int> trié;
inorder(root, trié);
int n = trié.size();
vecteur<vecteur<int>> ans;

pour (int q : requêtes) {
auto it = lower_bound(sorted.begin(), tried.end(), q); // first >= q
int idx = it - trié.début();

int maxi = (it != trié.end()) ? *it : -1;
int mini = (idx) 0) ? triés[idx-1] : -1;

si (it != trié.end() && *it == q) { // correspond exactement
Mini = maxi = q;
}
({mini, maxi});
}
le retour des an;
}
};
«» "

> `lower_bound` est la contrepartie STL de `bisect_left`.
> Le code est *itatif* et sûr pour les arbres très profonds.

---

C'est pas vrai. Liste de contrôle des cas

Situation Résultats attendus Erreur typique
-- -- -- -- -- -- -- -- -- --
Autres Aucun élément ≤ requête. 0' vérification. Autres
Autres Aucun élément ≥ requête : **‐1** Autres
Autres La question est égale à une valeur de nœuds. Autres
Autres Arborescence biaisée (dégénérée) : Toujours la mémoire O(n) Autres
Les valeurs dupliquées ne sont pas autorisées dans la liste BST. Autres

---

## 7-

Thème Qu'est-ce que l'intervieweur se soucie de :
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**BST fondamentaux** Savez-vous comment une traversée en ordre donne une liste triée? Dessinez une petite BST sur du papier, marchez dans l'ordre. Autres
**Binary search** Mettre en œuvre `bisect_left` ou `low_bound` à partir de zéro, puis optimiser. Autres
Autres **Optimisation de l'espace**=Vous réalisez que le stockage de l'arbre à nouveau (par exemple, avec `TreeSet`) est un gaspillage? Explication du compromis entre un `TreeSet` (log-time insert/search) et un seul tableau trié. Autres
**Manipulation d'un cas d'Edge** Afficher les cas de test où la requête est plus petite que tous les nœuds ou plus grande que tous les nœuds. Autres
**Iterative vs recursive**= Votre solution gère-t-elle des arbres biaisés?=Utilisez une pile ou un passage itératif si vous prévoyez une hauteur de 105. Autres

> **Rappelez-vous**: Les tests LeetCode génèrent généralement un arbre aléatoire asymétrique, de sorte que la profondeur de récursion peut atteindre la limite de pile par défaut en Java/Python. Un en-ordre non récursif (en utilisant une pile explicite) garantit la stabilité.

---

## 8-- FAQ (dépliant rapide)

C'est ce qu'il a dit.
-- -- -- -- -- --
**Puis-je utiliser `TreeSet` au lieu d'un tableau trié?**= Oui, mais vous aviez encore besoin d'appeler `lowerBound`/`ceil` pour chaque requête – le temps est le même, mais la mémoire est plus haute. Autres
**Est-ce que `upper_bound` est nécessaire?**. Non, `lower_bound` + `idx-1` suffit pour prédécesseur et successeur. Autres
Autres **Que faire si l'arbre contient des valeurs dupliquées?**Le problème garantit un arbre de recherche *binaire*, qui par définition a des valeurs distinctes; sinon la réponse serait ambiguë. Autres
**Puis-je le faire dans le temps O(n + m)?**= Seulement si vous effectuez une seule traversée *parallèle* de l'arbre et des requêtes (ligne de balayage avancée). Pas nécessaire pour 105 contraintes. Autres
Autres **Comment construire l'arborescence à partir d'un tableau?**=Utilisez l'aide habituelle LeetCode qui insère les nœuds niveau par niveau. Cela ne fait pas partie de la logique fondamentale. Autres

---

## 9.

1. ** Montrez votre compréhension de la structure des données** – expliquez pourquoi en ordre donne une liste triée.
2. **Parler de la complexité** – Nous faisons une seule traversée (O(n)), puis chaque requête utilise la recherche binaire (O(log n)). (en milliers de dollars)
3. **Boîtes de bord de mention** – Si la limite inférieure est au début ou à la fin, nous retournons
4. **Si vous avez demandé une solution plus dynamique** – suggérez d'utiliser `TreeSet` ou une BST équilibrée qui supporte `floor()` et `plafond()` dans O(log n).

> **Pourquoi ça te distingue**
> Il démontre *la capacité de réduire une solution O(n ·m) naïve à une solution rapide O(n + m log n)* – une caractéristique d'un ingénieur assaisonné.

---

## Code final Snapshot

"""
♪ Java
Java - leetcode de jardin. pot
# Python
solution python3. py
Numéro C++
g++ -std=c++17 solution.cpp && ./a.out
«» "

Les trois extraits ci-dessus sont prêts à copier-coller dans l'éditeur de LeetCode.

---

Joyeux Codage !
Si vous avez apprécié cette promenade, appuyez sur ** , **** et **subscribe** pour plus de LeetCode de plongée profonde – parfait pour votre prochaine interview prep. C'est ce qu'il a dit