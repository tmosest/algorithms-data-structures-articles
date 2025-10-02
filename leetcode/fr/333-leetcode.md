---
titre: LeetCode 333. Sous-arbre
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Le plus grand sous-arbre BST – LeetCode 333
**A Deep‐Dive, O(n) Solution + Code en Java, Python & C++ + SEO‐Ready Blog Post**

---

Résumé du problème

Étant donné la racine d'un arbre binaire, trouver la taille (nombre de nœuds) du **plus grand sous-arbre qui est aussi un arbre de recherche binaire (BST)**.
Un sous-arbre doit contenir tous ses descendants, c'est-à-dire que vous ne pouvez pas déposer des nœuds au milieu.

Point clé Description
C'est pas vrai.
**Règle BST**=Pour chaque nœud, toutes les valeurs du sous-arbre gauche < node.val < toutes les valeurs du sous-arbre droit==
Retournez le nombre de nœuds *maximum* parmi tous ces sous-arbres de la BST
**Constraints** Autres
**Suivi**=Atteindre le temps O(n), l'espace O(n) (pile récursive)=

---

Approche optimale O(n)

Traversez l'arbre une fois (après l'ordre).
À chaque nœud calcule ** quatre informations** pour le sous-arbre enraciné dans ce nœud :

Champ
C'est quoi ?
Ce sous-arbre satisfait-il aux propriétés BST? Autres
Nombre de nœuds dans ce sous-arbre (si c'est une BST)
Valeur minimale dans ce sous-arbre
Valeur maximale dans ce sous-arbre

- Oui. Récurrence

1. **Caisse de base** – Un enfant vide est considéré comme une TVB de taille 0, min = +.
2. Pour un nœud `root`:
- Récursivement obtenir `à gauche` et `à droite`.
- `root` est une BST **iff**
`left.isBST && droite.isBST && gauche.maxVal < root.val && root.val < droite.minVal`.
- Si c'est une BST:
- `taille = gauche.taille + droite.taille + 1`
- `minVal = min(root.val, gauche.minVal) "
- `maxVal = max(root.val, droit.maxVal) "
- Sinon, marquez `isBST = false` et gardez `size = max(left.size, right.size)` (la plus grande BST trouvée plus profonde).

La réponse est la plus grande "taille" rencontrée pendant la traversée.

Cela fonctionne dans **O(n)** temps parce que chaque noeud est visité une fois, et utilise O(n) espace pour la récursion (ou O(h) si la récursion de la queue est éliminée).

---

Mise en œuvre du code

- Oui. 1. Java

"Java
***
* Définition d'un noeud d'arbre binaire.
* classe publique TreeNode {
* Int val;
* TreeNode gauche;
* TreeNode droit;
* TreeNode(int x) { val = x; }
*}
*/
solution de classe {
classe statique privée Info {
booléen estBST;
taille int; // taille de la BST si isBST == true
valeur int min; // min dans ce sous-arbre
int max; // valeur max dans ce sous-arbre
Info(boolean isBST, taille int, int min, int max) {
ce.isBST = isBST;
ce.size = taille;
ce.min = min;
ce.max = max;
}
}

Int et privé = 0;

publique BSTSubtree (racine de nœud d'arbre) {
dfs(racine);
le retour des an;
}

info privée dfs(nœud TreeNode) {
si (noeud == null) {
// Sous-arbre vide: BST valide de taille 0
retourner nouveau Info(true, 0, entier. MAX_VALUE, entier.MIN_VALUE);
}

Informations à gauche = dfs(node.left);
Info droite = dfs(node.right);

// Vérifiez l'état de la BST pour le nœud actuel
si (à gauche) && droite. estBST
&& gauche.max < node.val && node.val < droite.min) {
int sz = taille gauche + taille droite + 1;
int mn = Math.min(node.val, gauche.min);
int mx = Math.max(node.val, droit.max);
ans = Math.max(ans, sz);
retourner les nouveaux Info(true, sz, mn, mx);
}

// Pas une BST: propager la meilleure taille trouvée jusqu'à présent
ans = Math.max(ans, Math.max(gauche.size, droite.size));
retourner le nouveau Info(false, 0, 0, 0); // la taille n'est pas pertinente ici
}
}
«» "

---

- Oui. 2. Python

'`python
# Définition d'un noeud d'arbre binaire.
# classe TreeNode:
# def __init_(self, val=0, gauche=Aucune, droite=Aucune):
# Self.val = val
Moi-même. gauche = gauche
Moi-même. droite = droite

Solution de classe:
plus BSTSubtree(self, root: TreeNode) -> Int:
Self.ans = 0

def dfs(node):
si ce n'est pas le nœud:
# sous-arbre vide: BST de taille 0
retour (Vrai, 0, flotteur('inf'), flotteur('-inf'))

gauche_is_bst, gauche_size, gauche_min, gauche_max = dfs(node.left)
right_is_bst, right_size, right_min, right_max = dfs(node.right)

# Le nœud actuel forme une BST?
si gauche_is_bst et droite_is_bst et gauche_max < noeud.val < droite_min:
sz = taille gauche + taille droite + 1
mn = min(node.val, gauche_min)
mx = max(node.val, droite_max)
Self.ans = max (self.ans, sz)
retour (Vrai, sz, mn, mx)
Sinon:
self.ans = max(self.ans, gauche_size, droite_size)
retour (Faux, 0, 0, 0)

dfs(racine)
Revenez vous-même. ans
«» "

---

- Oui. 3. C++

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
struct Info {
bool isBST;
taille int; // taille si isBST==true
Int minV;
à l'intérieur maxV;
Info(bool b, int s, int mn, int mx) : isBST(b), taille(s), minV(mn), maxV(mx) {}
};

la plus grande BSTSubtree(racine TreeNode*) {
Int ans = 0;
dfs(racine, ans);
le retour des an;
}

particulier:
Info dfs(nœud TreeNode*, int& ans) {
Si (!noeud)
retourner Info(true, 0, INT_MAX, INT_MIN); // arbre vide

Info gauche = dfs(node->gauche, ans);
Info droite = dfs(node->right, ans);

Si (gauche.isBST && droite.isBST &&
gauche.maxV < noeud->val && noeud->val < droit.minV) {

int sz = taille gauche + taille droite + 1;
ans = max(ans, sz);
int mn = min(node->val, gauche.minV);
int mx = max(node->val, droit.maxV);
retour Info(true, sz, mn, mx);
}

ans = max(ans, max(left.size, right.size));
retourner Info(false, 0, 0, 0); // la taille n'est pas pertinente lorsqu'elle n'est pas une TVB
}
};
«» "

---

Qu'est-ce qui fait cette solution ?

Aspect du bien
- C'est quoi ?
Autres **Complexité du temps**
Autres **Complexité de l'espace**= O(n) pile de récursion (O(h) si la queue est optimisée)== S/O Aucune=
**Readability**= Utiliser un retour clair `Info`/tuple; commentaires en ligne== Légèrement verbeux en Java en raison de la classe d'aide== Aucune Autres
Autres **Cas d'esquive**=Poigne l'arbre vide, valeurs négatives, valeurs dupliquées, arbres profonds
**Pitfall**= Oublier d'initialiser `min`/`max` pour les enfants nuls → mauvaise comparaison== Complication excessive avec des structures de données supplémentaires=== Aucune==

C'est pas vrai.

1. **Valeurs sentinelles incorrectes** – Utiliser `+---- pour max. En Java: `Integer.MAX_VALUE / Integer.MIN_VALUE`.
2. **Mise à jour min/max** – Pour un nœud BST, `min` est le plus petit de sa propre valeur et le sous-arbre de gauche min; `max` est le plus grand de sa propre valeur et le sous-arbre de droite max.
3. **Négligence pour propager la meilleure taille** – Même lorsqu'un sous-arbre n'est pas une BST, ses enfants pourraient contenir la plus grande BST ; garder la meilleure taille vue jusqu'ici.

---

Ressources et variations supplémentaires

- **Contrôle de passage dans l'ordre** – La séquence des BST dans l'ordre doit être en pleine augmentation.
- **Programmation dynamique sur arbres** – Modèle similaire utilisé pour le diamètre du sous-arbre, plus grande BST en arbre binaire, problèmes de somme du sous-arbre.
- **A posteriori – Utilisez une pile explicite pour éviter le débordement de la pile de récursion pour les arbres extrêmement profonds.

---

## -Traitement de l'entrevue- Loin

> *« Expliquez comment vous trouveriez le plus grand sous-arbre BST d'un arbre binaire, et pourquoi vous auriez utilisé une traversée post-commande. » *

Principaux points abordés:
- La post-commande assure la disponibilité des informations sur les enfants avant le traitement du parent.
- Le modèle `Info` réduit le nombre de passages à travers l'arbre.
- Discutez des valeurs sentinelles et des raisons pour lesquelles les `+=" / `=" sont sûrs indépendamment des valeurs des nœuds.

---

Appel à l'action

C'est vrai. **Vous souhaitez maîtriser plus de questions d'entrevue LeetCode? * *
- **S'abonner** pour les solutions hebdomadaires Java/Python/C++.
- **Téléchargez** la feuille complète de "LeetCode 333", la plus grande feuille de triche de la BST.
- **Partager** ce post sur LinkedIn ou Twitter avec #LeetCode333, #BST, #CodingInterview.

---

Résumé

- Le plus grand problème BST Subtree est un problème de DP d'arbre classique.
- Un DP propre post-commande qui retourne `isBST, size, min, max` donne une solution **O(n)**.
- Oui. Nous avons fourni **code prêt à la production** pour **Java, Python et C++** – copier-coller, courir et impressionner le gestionnaire d'embauche.

Bonne chance avec votre interview de codage, et continuez à résoudre!