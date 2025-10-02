---
titre: LeetCode 545. Frontière de l'arbre binaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 545 – Limite de l'arbre binaire
**Moyenne de l'arbre binaire de l'espace O(h)**

Vous trouverez ci-dessous des solutions complètes dans **Java, Python et C++**.
Après l'écriture du code, nous avons écrit un court article qui explique l'algorithme, met en évidence le bon, le mauvais et le laid, et est écrit avec des mots-clés optimisés par le SEO que les recruteurs aiment voir dans votre portfolio ou GitHub README.

---

- Oui. 1. Solution Java

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

*** Définition d'un noeud d'arbre binaire. */
classe publique TreeNode {
la valeur intérieure;
TreeNode gauche;
TreeNode droit;
TreeNode(int x) { val = x; }
}

solution de classe publique {

Liste publique<entier> limite DeBinaryTree (racine de TreeNode) {
Liste du résultat <entier> = nouvelle liste de distribution<>();
si (root) null le résultat de retour;

si (!isLeaf(root)) résultat.add(root.val);

// 1. Frontière gauche (à l ' exclusion des feuilles)
TreeNode cur = root.left;
pendant que (cur != null) {
si (!isLeaf(cur)) résultat.add(cur.val);
cur = (cour. gauche != nul) ? cur.left : cur.right;
}

// 2. Toutes les feuilles (de gauche à droite)
addLeaves(root, résultat);

// 3. Limite droite (à l'exclusion des feuilles), ajouter à l'envers
Liste<entier> droiteBoundaire = nouvelle liste de distribution<>();
cur = root.right;
pendant que (cur != null) {
si (!isLeaf(cur)) droitBoundary.add(cur.val);
cur = (cur.right != null) ? cour. droite : cour. gauche;
}
pour (int i = droiteBoundary.size() - 1; i >= 0; --i)
résultat.add(droitBoundary.get(i));

le résultat du retour;
}

vide privé addLeaves (noeud TreeNode, liste <integer> out) {
si (noeud == nul) retour;
si (estLeaf(node)) {
out.add(node.val);
retour;
}
addLeaves(node.left, out);
addLeaves(node.right, out);
}

booléen privé estLeaf (node TreeNode) {
noeud de retour. gauche == Null && noeud. droit == nul;
}
}
«» "

---

- Oui. 2. Solution Python

'`python
de taper l'importation Liste, facultative

# Définition d'un noeud d'arbre binaire.
classe TreeNode:
def __init_(self, val: int = 0, gauche: 'TreeNode' = Aucune, droite: 'TreeNode' = Aucune):
autoval = val
auto.gauche = gauche
soi.right = droit

Solution de classe:
def limite DeBinaryTree(même, racine: Facultative[TreeNode]) -> Liste[int]:
si non racine: retourner []

res = []

# Racine (si ce n'est pas une feuille)
si non self._is_leaf(root):
Res.append(root.val)

# Limite gauche (à l'exclusion des feuilles)
noeud = root.left
pendant que le nœud:
si non self._is_leaf(node):
res.append(node.val)
noeud = noeud.left si noeud. Il a quitté le nœud. droite

Feuilles
Self._add_leaves(root, res)

# Limite droite (à l'exclusion des feuilles) – collecter puis inverser
_boundary droite = []
noeud = root.right
pendant que le nœud:
si non self._is_leaf(node):
right_boundary.append(node.val)
noeud = noeud.right si noeud. C'est un nœud. gauche
res.extend(reversed(right_boundary))

retour res

def _add_leaves(self, node: Facultatif[TreeNode], out: List[int]) -> Aucun:
si ce n'est pas le nœud:
retour
si self._is_leaf(node):
out.append(node.val)
retour
Self._add_leaves(node.left, out)
Self._add_leaves(node.right, out)

@staticmethod
def _is_leaf(node: TreeNode) -> bool:
noeud de retour. gauche est Aucun et noeud. droit n'est pas
«» "

---

- Oui. 3. Solution C++

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

/* Définition d'un noeud d'arbre binaire. */
struct TreeNode {
la valeur intérieure;
TreeNode *gauche;
TreeNode *right;
TreeNode(int x) : val(x), gauche(nullptr), droite(nullptr) {}
};

solution de classe {
public:
vectorielle<int> limite De l'arbre de lapin (racine de l'arbre node*) {
vecteur <int> ans;
si (!root) retournent des ans;

si (!isLeaf(root)) ans.push_back(root->val);

// Limite gauche (à l'exclusion des feuilles)
TreeNode* cur = racine->gauche;
pendant que (cur) {
si (!isLeaf(cur)) ans.push_back(cur->val);
cur = (cur->gauche) ? cur->gauche : cur->gauche;
}

// Feuilles
addLeaves(root, ans);

// Limite droite (à l'exclusion des feuilles) – collecter puis inverser
vecteur<int> droitB;
cur = root->right;
pendant que (cur) {
si (!isLeaf(cur)) droiteB.push_back(cur->val);
cur = (cur-> droite) ? cur-> droite : cur-> gauche;
}
pour (auto it = rightB.rbegin(); it != rightB.rend(); ++it)
le nom de l'entité ou de l'entité;

le retour des an;
}

particulier:
(nœud TreeNode*) {
retour noeud->gauche == nullptr && node->right == nullptr;
}

vide addLeaves(nœud TreeNode*, vecteur<int>&out) {
si (!node) retour;
si (estLeaf(node)) {
out.push_back(node->val);
retour;
}
addLeaves(node->left, out);
addLeaves(node->right, out);
}
};
«» "

> **Astuce:** Dans les trois langues, l'idée centrale est la même – *DFS avec trois passes* :
> 1. Limite gauche (de haut en bas, sautez les feuilles)
> 2. Toutes les feuilles (de gauche à droite)
> 3. Limite droite (du haut au bas, sautez les feuilles) mais ajouté dans l'ordre inverse

---

## ♫ Blog-Style Writing-up: Boundary of Binary Tree – Good, Bad & Ugly

> **Mots-clés**: *Codeleet 545, Frontière du binaire Arbre, arbre binaire traversant, DFS, algorithme d'entrevue, entretien d'ingénieur logiciel, entretien de codage, complexité temporelle, complexité spatiale, conseils d'entrevue d'emploi. *

---

C'est pas vrai. Les bonnes

Autres Pourquoi cet algorithme brille-t-il ?
C'est-à-dire
**Simplicité** – La solution n'est que quelques boucles et un collecteur récursif. Pas de machine d'état supplémentaire ou de logique de drapeau. *Clear, code lisible*
**Temps linéaire** – Chaque noeud est visité au plus une fois → **O(n)**. Parfait pour les grands arbres.
** Low Auxiliary Space** – Seulement la profondeur de récursion ('O(h)') et quelques listes auxiliaires ('O(h)'). *Optimisé par l'espace
**Extensible** – Vous pouvez brancher cette routine dans n'importe quel système d'entretien ou de production qui nécessite une vue périphérique d'arbre. *Modèle de code réutilisable*
**Pas de double calcul** – Les feuilles ne sont ajoutées qu'une seule fois, qu'elles apparaissent sur une frontière ou non. *Garantie sans caution

> **Recruter-friendly takeaway**: *=Je peux produire un code propre, O(n) arbre-traversal qui évite les pièges communs tels que les feuilles à double comptage.

---

- Oui. Les mauvais

Réparez / évitez
- C'est pas vrai.
**Roule naturelle** – L'énoncé de problème garantit une racine, mais le codage défensif est toujours sage. Rechercher la "root== null` tôt. Autres
**Nœuds frontières mono-enfant** – Un nœud avec un seul enfant doit encore être considéré comme faisant partie de la limite. Utilisez le --si la gauche existe à droite (et vice versa pour la limite droite). Autres
**Root étant une feuille** – Dans ce cas, la limite est juste `[root.val]`. Passer en ajoutant `root` quand c'est une feuille. Autres
**Quirks de langue** – Dans Python la limite de récursion peut frapper `sys.setrecursionlimit`, dans C++ les pointeurs-checks doivent être prudents. Gardez la profondeur de récursion à l'esprit, ou passez à une pile itérative si `h` pourrait être énorme. Autres

---

C'est vrai. L'Ugly

Autres Quand le code ressemble à un monstre spaghetti
-- -- -- -- -- -- ----------------------------------
La sur-ingénierie avec les entiers de "flag" (1 = gauche, 2 = droite, 3 = autre) et plusieurs méthodes d'aide juste pour garder une trace de "où nous sommes" est ** inutile** pour ce problème. Cela rend le code plus difficile à lire et plus sensible aux erreurs. Autres
Autres Utiliser un `vecteur<int>` global et le muter de la récursion profonde peut être difficile à déboguer, surtout en C++ où la gestion manuelle de la mémoire est impliquée. Autres
Autres Oublier de sauter les feuilles lors de l'ajout de la limite gauche/droite conduit souvent à des valeurs dupliquées dans la liste finale. Une approche « simple » qui ajoute la racine, la limite gauche, les feuilles, la limite droite – puis dédouble – est plus propre. Autres

> **Take‐away**: *Écrire le DFS le plus simple qui satisfait aux règles de limites. Évitez les drapeaux cachés ou les machines d'état à moins que l'entrevue ne les exige explicitement. *

---

####4-SEO–Résumé optimisé

Si vous construisez un README GitHub, une page de portfolio ou préparez un jeu de solutions **LeetCode** pour impressionner les gestionnaires d'embauche, utilisez les méta-tags, les en-têtes et les phrases de mots clés suivantes:

- `#LeetCode545`, `#BoundaryOfBinaryTree`, `#BinaryTreeTraversal`, `#DFS`, `#Recursion`, `#InterviewAlgorithm`, `#SoftwareEngineer`, `#CodingInterview`, `#JobInterview`, `#AlgorithmDesign`, `#TimeComplexity`, #Complexité spatiale "

**Exemple de l'extrait de lisière**

```markdown
# Limite de l'arbre binaire – LeetCode 545

- **Problème**: Calculer la limite d'un arbre binaire (limite gauche, feuilles, limite droite) en temps O(n).
- **Langues**: Java, Python, C++.
- **Complexités**: temps «O(n)», espace auxiliaire «O(h)» (h' = hauteur de l'arbre).
- **Pourquoi c'est important**: Démontre la première recherche en profondeur, la manipulation des caisses et le code propre – compétences clés pour une entrevue avec un ingénieur logiciel.
«» "

> **Pourquoi cela compte pour votre recherche d'emploi* *
> Les recruteurs cherchent des candidats qui peuvent ** résoudre des problèmes d'arbres classiques** rapidement et avec un code propre. En ajoutant ce problème (LeetCode 545) à votre demande publique et en écrivant un billet de blog qui explique *bonnes, mauvaises, laides* idées, vous présentez :
> * Compétences en résolution de problèmes
> * Lisibilité et maintien du code
> * Compréhension des compromis entre le temps et l'espace
> * Capacité de communiquer des idées complexes dans un format digestible

---

C'est vrai. Harnais d'essai rapide (facultatif)

"Java
public statique vide principal(String[] args) {
/* Construire l'arbre suivant
1
/ \
2 3
/ \ \
4 5 7
*/
racine TreeNode = nouveau TreeNode(1);
root.left = nouveau TreeNode(2);
root.right = nouveau TreeNode(3);
root.left.left = nouveau TreeNode(4);
root.left.right = nouveau TreeNode(5);
root.right.right = nouveau TreeNode(7);

Solution sol = nouvelle solution();
Système.out.println(sol.boundaryOfBinaryTree(root)); // -> [1, 2, 4, 5, 7, 3]
}
«» "

---

Comment utiliser ces solutions dans votre portefeuille d'entrevues

1. **Téléchargez les trois fichiers sources** (`Solution.java`, `solution.py`, `solution.cpp`) dans une repo publique GitHub.
2. Ajouter l'article **blog** en tant que fichier `README.md` ou un fichier `blog.md` séparé.
3. Dans votre page LinkedIn ou portfolio, link to the repo and mention *=Solved LeetCode 545 – Limite de l'arbre binaire avec O(n) DFS.
4. Lorsque vous présentez une demande, ajoutez l'extrait suivant à votre lettre de motivation ou à votre LinkedIn :

> Lors de ma récente préparation d'entrevue, j'ai abordé LeetCode 545 – Boundary of Binary Tree, implémentant une solution propre et linéaire en Java, Python et C++. L'algorithme met en évidence ma capacité à effectuer des DFS sur des arbres binaires, à gérer la logique des cas de bord et à produire du code prêt à la production.

---

**Codage heureux & meilleure de chance atterrir que prochain rôle d'ingénierie de logiciel!**