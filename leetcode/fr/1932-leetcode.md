---
titre: LeetCode 1932. Fusionner les BST pour créer une BST unique -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1932 – Fusionner les BST pour créer une BST unique
**Validation de l'ordre par Hash-Map**

---

TL;DR
- Trouvez la racine de l'arbre dont la valeur racine n'apparaît jamais comme un enfant dans un autre arbre.
- Entreposez tous les arbres dans une carte de hachage (`rootValue → TreeNode`).
- Marcher récursivement de la vraie racine et remplacer toute feuille dont la valeur correspond à une clé dans la carte avec le sous-arbre entier correspondant.
- Oui. Après la promenade, si plus d'un arbre reste dans la carte → **impossible**.
- Valider l'arbre fusionné avec une traversée en ordre – les valeurs doivent être en augmentation stricte.
- Oui. Si valide, retourner la racine fusionnée; sinon retourner `null`.

L'algorithme fonctionne dans **O(n)** temps (n = nombre d'arbres) et utilise **O(n)** espace supplémentaire pour la pile de carte et de récursion.

---

Code complet (Java, Python, C++)

> **Astuce:** La définition `TreeNode` est la même dans les trois langues – seule la syntaxe change.

### Java

"Java
***
* Définition d'un noeud d'arbre binaire.
* classe publique TreeNode {
* Int val;
* TreeNode gauche;
* TreeNode droit;
* TreeNode() {}
* TreeNode(int val) { this.val = val; }
* TreeNode(int val, TreeNode gauche, TreeNode droite) {
* ce.val = valeur;
* ce.gauche = gauche;
* ce droit = droit;
*}
*}
*/
solution de classe {
public TreeNode canMerge(Liste <TreeNode> arbres) {
si [trees.size()] 1) retourner les arbres.get(0);

// 1. Construire le hash‐map: valeur racine -> Numéro d'arbre
Carte<entier, TreeNode> carte = nouveau HashMap<>();
pour (TreeNode t : arbres) map.put(t.val, t);

// 2. Trouvez la vraie racine – celle dont la valeur n'est jamais un enfant
Définir <Integer> enfants = nouveau HashSet<>();
pour (TreeNode : arbres) {
si (t.left != null) enfants.add(t.left.val);
si (t.right != null) enfants.add(t.right.val);
}

racine TreeNode = null;
pour (TreeNode : arbres) {
si (!enfants.contient(t.val)) {
si (root != null) retourner null; // plusieurs candidats → impossible
racine = t;
}
}
si (root == null) retourne null; // aucune racine trouvée

// 3. Fusionner récursivement
fusion (root, carte);

// 4. Tous les arbres doivent être fusionnés
si (map.size() > 1) retour nul;

// 5. Valider la propriété de la TVB
Liste <integer> inorder = nouvelle liste d'array<>();
inorderTraversal(racine, inorder);
pour (int i = 1; i < inorder.size(); ++i) {
si (inorder.get(i) <= inorder.get(i - 1)) retourne null;
}

retour de racine;
}

fusion du vide privé (noeud TreeNode, carte <entier, carte TreeNode>) {
si (noeud == nul) retour;

if (node.left != null && map.contientKey(node.left.val)) {
noeud.left = map.remove(node.left.val);
fusion(node.left, carte);
}
if (node.right != null && map.contientKey(node.right.val)) {
node.right = map.remove(node.right.val);
fusion(node.right, carte);
}
}

vide privé en ordre Traversal(Node d'arbre, liste <entier> res) {
si (noeud == nul) retour;
inorderTraversal(node.left, res);
res.add(node.val);
inorderTraversal(node.right, res);
}
}
«» "

---

Python

'`python
# Définition d'un noeud d'arbre binaire.
classe TreeNode:
def __init__(self, val=0, gauche=Aucun, droite=Aucun):
autoval = val
auto.gauche = gauche
soi.right = droit

Solution de classe:
def canMerge(self, arbres: List[TreeNode]) -> Facultatif[TreeNode]:
si len(trees) == 1 :
les arbres retournés[0]

# Valeur racine de la carte -> Numéro d'arbre
arbore_map = {t.val: t pour t dans les arbres}

# Recueillir toutes les valeurs enfant
enfants = ensemble()
pour t dans les arbres:
si t. gauche:
enfants.add(t.left.val)
si t.right:
enfants.add(t.right.val)

# Trouvez la racine unique
racines = [t pour t dans les arbres si t.val pas chez les enfants]
si len(roots) != 1 :
retour Aucune
racine = racines[0]

# Fusion récursive
def merge(node: TreeNode):
si le nœud n'est pas :
retour
si noeud. gauche et noeud. gauche.val dans la_carte de l'arbre :
node.left = arbore_map.pop(node.left.val)
fusion (node.left)
si noeud. droite et noeud. droite.val dans l'arborescence_map :
node.right = arbore_map.pop(node.right.val)
fusion (node.right)

fusion(root)

Tous les arbres doivent être fusionnés
si arborescence_map :
retour Aucune

# Valider la TVB par ordre
dans l ' ordre = []
def dfs(node: TreeNode):
si le nœud n'est pas :
retour
dfs(node.gauche)
inorder.append(node.val)
Dfs(node.right)

dfs(racine)
if any(inorder[i] <= inorder[i-1] pour i in range(1, len(inorder))):
retour Aucune

retour de racine
«» "

---

C++

'`cpp
***
* Définition d'un noeud d'arbre binaire.
* struct TreeNode {
* Int val;
* TreeNode * gauche;
* TreeNode *right;
* TreeNode(int x) : val(x), gauche(nullptr), droite(nullptr) {}
* };
*/
solution de classe {
public:
TreeNode* canMerge(vecteur<TreeNode*>& arbres) {
si [trees.size()] 1) les arbres de retour[0];

// Valeur racine de la carte -> Numéro d'arbre
unordered_map<int, TreeNode*> mp;
pour (autot : arbres) mp[t->val] = t;

// Recueillir les valeurs de l'enfant
un_set_non ordonné<int> enfant;
pour (auto t : arbres) {
si (t->left) child.insert(t->left->val);
si (t->right) child.insert(t->right->val);
}

// Trouvez la racine unique
racine TreeNode* = nullptr;
pour (auto t : arbres) {
si (child.find(t->val) == child.end() {
si (root) retourne nullptr; // plus d'un candidat
racine = t;
}
}
si (!root) retourne nullptr;

// Fusion récursive
fonction<very(TreeNode*)> fusion = [&](TreeNode* noeud) {
si (!node) retour;
si (node->left && mp.count(node->left->val) {
node->left = mp[node->left->val];
mp.erase(node->left->val);
fusion (node->gauche);
}
si (node->right && mp.count(node->right->val) {
node->right = mp[node->right->val];
mp.erase(node->right->val);
fusion (node->right);
}
};
fusion(root);

// Tous les arbres doivent être fusionnés
si (!mp.vide()) retourne nullptr;

// Valider la TVB par ordre
vecteur<int> dans l'ordre;
fonction<very(TreeNode*)> dfs = [&](TreeNode* noeud) {
si (!node) retour;
dfs(node->gauche);
inorder.push_back(node->val);
dfs(node->right);
};
dfs(racine);

pour (size_t i = 1; i < inorder.size(); ++i)
si (inorder[i] <= inorder[i-1]) retourne nullptr;

retour de racine;
}
};
«» "

---

## Blog Post (optimisé par le référencement)

> **Titre:** *De Merge à Master – Résoudre le LeetCode 1932 (Merge BST) et renforcer vos compétences en matière de structure de données*

---

- Oui. 1. Présentation

Lorsque vous préparez une entrevue de software-engineering senior, il est rare qu'on vous demande de résoudre un problème qui combine *hash-maps*, *tree recursion* et *BST validation* tout à la fois. LeetCodeS **1932 – Fusionner les BST pour créer une seule BST** est l'un de ces joyaux cachés. C'est marqué "Hard" pour une raison: les contraintes (5 × 104 arbres, chacun avec ≤ 3 nœuds) exigent une solution linéaire qui est également facile à raisonner.

Dans ce post, nous allons marcher à travers:

Mot-clé Pourquoi ça compte
-- -- -- -- -- --
< < Fusionner bst > > Concept du problème de base
"Hash map"
"dfs" : profondeur – premier passage pour coller des arbres
" validation de l'ordre "" Voie rapide pour tester la propriété BST
Les intervieweurs aiment les solutions linéaires

---

- Oui. 2. Aperçu du problème

> **Objectif**: Combiner une liste de petits arbres binaires en **un** arbre de recherche binaire (BST), ou déterminer qu'il est impossible.

**Input**
- `arbres`: liste des pointeurs TreeNode.
- Oui. Chaque valeur racine d'arbre est unique.
- Chaque arbre a au plus 3 nœuds (racine + 0/1/2 enfants).

**Opérations autorisées* *
- Choisissez un arbre comme la vraie racine** (celui qui n'apparaît jamais comme un enfant).
- Oui. Si une valeur de feuille correspond à une autre valeur de racine d'arbre, remplacez cette feuille par le sous-arbre *entire*.
- Chaque arbre peut être utilisé au plus vite.

**Retour**
- Oui. La racine fusionnée si une seule BST valide peut être formée, sinon `null` (ou `Aucun` / `nullptr`).

---

- Oui. 3. Principaux défis

Pourquoi c'est difficile
- Oui.
Autres Identifier la racine *réelle* Une approche naïve pourrait mal saisir un sous-arbre comme la racine. Autres
Éviter les doubles-mères Une feuille pourrait correspondre à plusieurs sous-arbres si l'entrée est mal formée. Autres
Une recherche efficace est O(n2). Autres
Autres Validation de la propriété BST après fusion.Un arbre peut sembler fin structurellement mais violer la règle de l'ordre. Autres

---

- Oui. 4. Approche (étape par étape)

1. **Hash-Map Construction**
Carte chaque valeur racine à son TreeNode (`rootValue → node`).
*Pourquoi?* Permet le temps constant ─ est-ce un sous-arbre?

2. **Trouver la vraie racine**
- Rassemblez toutes les valeurs de l'enfant dans un ensemble.
- Scanner tous les arbres ; celui dont la valeur racine est *pas* dans l'ensemble enfant est la vraie racine.
- S'il y a plus d'un candidat ou aucun, la fusion est impossible.

3. ** Fusion récursive* *
En partant de la vraie racine, traversez l'arbre.
Chaque fois que vous rencontrez une feuille dont la valeur existe dans la carte, remplacez cette feuille par le sous-arbre cartographié et retirez l'entrée de la carte.
Récupérer dans le sous-arbre nouvellement inséré.

4. **Vérifier l'intégralité**
Après la traversée, la carte doit contenir seulement la vraie racine. Si un arbre reste → impossible.

5. **Validation de la TVB**
Effectuer une traversée en ordre pour recueillir des valeurs de nœuds.
Si la liste n'augmente pas strictement → l'arbre fusionné viole les règles BST → retourner `null`.

---

- Oui. 5. Faits saillants de la mise en œuvre

Langue Remarques spéciales
- C'est pas vrai.
**Java**=Utilisez `List<TreeNode>= du LeetCode; la profondeur de récursion est sûre (=3 × 5 000). Autres
**Python**Utilisez le dictionnaire (`{}`) et définissez (`set()`) – ops rapide O(1). Autres
**C++**= Utilise `unordered_map` et `unordered_set`; lambda recursion avec `std::fonction`. Autres

---

- Oui. 6. Complexité temporelle et spatiale

Formule métrique Explication
- C'est quoi ?
**Temps** **O(n)**= Chaque arbre est traité un nombre constant de fois (construction, détection de racine, fusion, validation). Autres
**L'espace **=O(n)**=La carte de hachage enregistre une entrée par arbre; profondeur de la cheminée de récursion ≤ 3. Autres

---

- Oui. 7. Cas de bord couverts

- ** Multiples racines réelles** → impossible.
- **Aucune vraie racine** → impossible.
- **Les arbres non fusionnés gauche** → impossible.
- **En ordre ne augmentant pas strictement** → BST invalide.
- **Input d'arbre unique** → trivialement retourné.

---

- Oui. 8. Bonne, mauvaise et mauvaise – Pièges communs

Autres La phase est bonne
- C'est quoi ?
**Bâtiment de carte**=1______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
**Détection de la racine**=L'ensemble d'enfants à passe unique=Plusieurs candidats → silencieux acceptent (bug)=La racine peut être *feuille* seulement (arbre vide)=
**Modifier la structure de l'arbre d'entrée en place (effets secondaires)
**Validation** Oublier de traverser *tous* noeuds (supporter un enfant nul)

---

- Oui. 9. Stratégie d ' essai

1. ** Cas de réussite fondamentale**
- Deux arbres où l'un est un enfant direct.
- Trois arbres formant une BST parfaite.

2. **Manquement dû à plusieurs racines**
- Deux arbres indépendants (sans lien enfant).

3. ** Échec dû aux arbres restants**
- Une feuille qui ne correspond à aucune autre racine.

4. ** Échec de la violation de la TVB* *
- Merge produit un arbre où l'enfant gauche > parent.

5. ** Grande entrée**
- 5 × 104 arbres, chacun avec 3 nœuds – vérifier l'exécution < 1 s.

---

10. SEO et conseils professionnels

Mot-clé
C'est quoi, ça ?
Titre, 1er paragraphe, intitulés H2
Description de la méta, première ligne
Sujets H3
Remarques:
Java/Python/C++ solution

**Pourquoi cela compte pour votre carrière:**
- La maîtrise des cartes de hachage et de la récursion des arbres démontre une connaissance profonde de la structure des données – une caractéristique des rôles de niveau supérieur.
- Les problèmes de LeetCode sont le pain-and-butter des interviews technologiques chez Google, Amazon et FAANG.
- Une solution propre et bien commentée montre le professionnalisme et la lisibilité du code – la valeur des qualités d'embauche des gestionnaires.

---

Conclusion

Résoudre **LeetCode 1932 – Fusionner les BST pour créer une BST unique** est un excellent moyen d'affiner votre intuition de plan de hachage, de pratiquer les DFS et de renforcer les techniques de validation de la BST. L'algorithme linéaire ci-dessus est à la fois élégant et efficace, ce qui en fait un point de discussion solide dans votre prochaine interview.

Si vous avez déjà cloué ce problème, envisagez de pratiquer des problèmes connexes:
- **2105. Remplacer tous les chiffres par la somme des sous-ensembles de chiffres** (combinaison d'arbres similaires).
- **1307. Puzzle arithmétique verbal** (hash-map + backtracking).

Bon codage et bonne chance pour votre voyage d'entrevue!