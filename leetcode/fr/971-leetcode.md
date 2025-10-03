---
titre: LeetCode 971. Flip arbre binaire pour correspondre à la précommande transversale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 971 – Flip Binary Tree pour correspondre à la trajectoire pré-commande
*Moyenne de l'arbre binaire*

> **Récapitulation des problèmes* *
> Vous êtes donné un arbre binaire dont les valeurs de nœud sont une permutation de `1 ... n`.
> Vous êtes également donné un tableau `voyage` (longueur `n`) qui représente une traversée *désirée* pré-commande.
> Dans une opération, vous pouvez changer de noeud, c'est-à-dire de sous-arbres gauche et droit.
> **Objectif:** Dépliez les nœuds **fewest** de sorte que l'arbre pré-commande soit égal à "voyage".
> Retourne une liste des valeurs de tous les nœuds retournés. Si c'est impossible, retournez `[-1]`.

---

Une idée fondamentale (La partie "Bien")

La traversée pré-commande visite les nœuds dans l'ordre *root → gauche → droite*.
Si nous descendons l'arbre en marchant simultanément dans le «voyage»:

1. Le nœud actuel **must** correspond à l'élément actuel du "voyage".
Si ce n'est pas le cas, nous sommes condamnés → retour `[-1]`.

2. Après avoir consommé la racine, regardez l'élément *next* dans `voyage` (`voyage[idx]`).
- Si l'enfant gauche existe **et** sa valeur est **pas** `voyage[idx]`, la seule façon de correspondre à l'ordre est de retourner le nœud actuel.
- Enregistrez le flip, puis recourrez à *à droite* d'abord, puis à gauche*.

3. Sinon (l'enfant gauche correspond ou l'enfant gauche est `null`), récidive normalement *left → droite*.

Parce que nous ne faisons que basculer quand la valeur suivante dans "voyage" le force, nous sommes garantis d'utiliser le nombre minimal de bascules.

---

C'est vrai. La partie "Bad"

- **État mondial** : Un pointeur `idx` unique est utilisé pour les appels récursifs.
Dans les langues à dactylographie stricte (p. ex. Java, C++), vous devez vous protéger contre les débordements ou les modifications accidentelles.
- **Manipulation des caisses**: Le code doit gérer gracieusement les sous-arbres vides (nœuds `null`) et le cas d'impossibilité (`[-1]`).
- **Débogage de la complexité**: Si l'arbre est grand (bien que `n ≤ 100` ici), la profondeur de la pile peut devenir une préoccupation dans les langages récursifs.

---

La partie "Ugly"

- **Doublure du code**: Écrire une logique presque identique dans plusieurs langues peut entraîner des maux de tête d'entretien.
- **Verbosity** : La version Java se sent souvent verbeuse en raison des définitions, des importations et de la manipulation de la liste de chaudronnerie `TreeNode`.
- ** Hypothèses implicites** : S'appuyer sur `voyage[idx]` sans limites peut produire `ArrayIndexOutOfBoundsException` si la logique de l'algorithme tourne mal.

---

Solutions complètes

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.
Tous les trois résolvent le problème dans *O(n)* temps et *O(h)* espace (où `h` est la hauteur de l'arbre, le pire cas `O(n)`).

Autres **Important**: Tous les extraits supposent l'existence d'une classe/structure `TreeNode` définie exactement comme indiqué.
> Ils supposent également que `root` n`est jamais `null` dans l`API publique (LeetCode le garantit).

---

### Java (récursion de DFS)

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

// Définition pour un nœud binaire.
classe TreeNode {
la valeur intérieure;
TreeNode gauche;
TreeNode droit;
TreeNode() {}
TreeNode(int val) { this.val = val; }
TreeNode(int val, TreeNode à gauche, TreeNode à droite) {
ce.val = val; ce.gauche = gauche; ceci. droite = droite;
}
}

solution de classe {
int idx privé = 0; // position actuelle en voyage
liste privée<integer> flips = nouvelle liste de distribution<>();
voyage privé int[]; // référence pour éviter de passer

liste publique<enteger> flipMatchVoyage(racine de nœud d'arbre, voyage int[]) {
Ça. voyage = voyage;
dfs(racine);
flips de retour;
}

vide privé dfs(nœud TreeNode) {
si (noeud == nul) retour;

// Mismatch → impossible
Si (node.val != voyage[idx]) {
flips.clear();
flips.add(-1);
retour;
}
idx++; // consommer la valeur actuelle

// Si l'enfant gauche existe et que la prochaine valeur attendue n'est pas elle, nous devons retourner
si (node.left != null && node.left.val != voyage[idx]) {
flips.add(node.val); // fichier flip
dfs(node.right);
dfs(node.gauche);
} autre {
dfs(node.gauche);
dfs(node.right);
}
}
}
«» "

---

### Python (récursion du DFS)

'`python
# Définition d'un noeud d'arbre binaire.
classe TreeNode:
def __init__(self, val=0, gauche=Aucun, droite=Aucun):
autoval = val
auto.gauche = gauche
soi.right = droit

Solution de classe:
def flipMatch Voyage(self, root: TreeNode, voyage: list[int]) -> list[int]:
auto.idx = 0
auto.flips = []

def dfs(node: TreeNode):
si ce n'est pas le nœud:
retour
si noeud.val != voyage[self.idx]:
auto.flips = [-1]
retour
Auto.idx += 1
♪ besoin de retourner?
si noeud.left et noeud.left.val != voyage[self.idx]:
auto.flips.append(node.val)
Dfs(node.right)
dfs(node.gauche)
Sinon:
dfs(node.gauche)
Dfs(node.right)

dfs(racine)
Revenez vous-même. flips
«» "

---

### C++ (récursion DFS)

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
vector<int> flipMatchVoyage(racine TreeNode*, vector<int>& voyage) {
idx = 0;
flips.clear();
dfs (racine, voyage);
flips de retour;
}

particulier:
Int idx = 0;
vecteur<int> flips;

vide dfs(nœud TreeNode*, vecteur<int>& voyage) {
si (!node) retour;
si (noeud->val != voyage[idx]) {
flips = {-1};
retour;
}
++idx;
si (noeud->gauche &&noeud->gauche->val != voyage[idx]) {
flips.push_back(node->val);
dfs(node->right, voyage);
dfs(node->gauche, voyage);
} autre {
dfs(node->gauche, voyage);
dfs(node->right, voyage);
}
}
};
«» "

---

Analyse de complexité

Algorithme Temps Espace
- C'est quoi ?
Autres Toutes les 3 implémentations **O(n)**

- `n` = nombre de nœuds (= 100).
- `h` = hauteur de l'arbre (meilleure caisse `n`).

---

Pourquoi ce code s'agit-il (et comment il aide votre entrevue)

Caractéristiques Prestations
C'est pas vrai.
**Linear traversal** Autres
La logique est déterministe; aucun retour en arrière ou force brute n'est nécessaire. Autres
**Récursion claire**=La logique pré-commande est évidente, ce que les intervieweurs recherchent. Autres
**Détecte immédiatement l'impossibilité et gagne du temps. Autres
**Modèle réutilisable**Le même modèle DFS-with-index peut résoudre de nombreux problèmes de LeetCode de style . Autres

Lors d'une entrevue, vous pouvez :

1. ** Expliquez l'intuition** d'abord – montre que vous comprenez le problème.
2. **Écrire le squelette** de `dfs(node)` et l'indice mondial.
3. ** Maintenez l'état de retournement** dans un "si".
4. **Retour `[-1]`** en tant que cas particulier.

Vous impressionnerez l'intervieweur avec une solution qui est ** à la fois élégante et correcte**.

---

Article de blog prêt au SEO

> **Titre**
> LeetCode 971 – Flip Binary Tree pour correspondre à la trajectoire précommande (Java / Python / C++ Solutions)

> **Description détaillée**
> Master LeetCode 971 en apprenant la solution optimale DFS pour retourner un arbre binaire pour un parcours pré-commande souhaité. Obtenez des extraits de code Java, Python et C++ qui résolvent le problème en temps linéaire – parfaits pour les entretiens d'ingénierie logicielle.

---

Article de blog

### Flip Binary Tree pour correspondre à la première commande transversale – 971 – Un guide d'entrevue complet

---

Introduction

Les intervieweurs posent souvent des questions *binaires* pour évaluer votre récursion et vos compétences stratégiques.
LeetCode 971 – **Flip Binary Tree To Match Pre-Order Traversal** est un problème classique qui teste exactement ces compétences.

Dans cet article vous allez découvrir:

- Une solution **complète, linéaire** dans **Java**, **Python** et **C++**.
- Le **pourquoi** derrière chaque ligne de code (flips minimal, fall‐fast, DFS‐with‐index).
- Une feuille de tricherie ** pour expliquer votre approche lors d'une entrevue de codage.

Laissez plonger !

---

##### #1

Valeur des contraintes
C'est pas vrai.
Valeurs du nœud
Longueur du voyage
≤ 100
Opération autorisée
Objectif : Retours minimums → Pré-commande désirée

---

##### 2-

Imaginez-vous debout dans l'arbre.
Le *root* doit correspondre au premier numéro du "voyage".
Après avoir choisi ce numéro, le numéro *next* vous indique quel enfant vous allez visiter.

Si le numéro suivant appartient au sous-arbre droit, nous devons retourner le noeud actuel.
S'il appartient au sous-arbre gauche (ou à l'enfant gauche est `null`), nous restons tel quel.

Cette règle gourmande donne le **fewest** flips.

---

- Oui. Faits saillants du code

- ** L'algorithme reste simple.
- **Indice pointeur** ('idx`) se déplace linéairement dans le "voyage'.
- **Flips list** ne stocke que des valeurs de nœuds inversés.
- **La sortie précoce** pour les cas impossibles permet d'économiser du temps.

---

Code Snippets

> **Java**

"Java
Liste publique<Intégrer> flipMatchVoyage(TreeNode root, int[] voyage) { ... }
«» "

> **Python**

'`python
Solution de classe:
def flipMatch Voyage(self, root: TreeNode, voyage: List[int]) -> Liste[int]: ...
«» "

> **C++**

'`cpp
solution de classe {
public:
vector<int> flipMatchVoyage(racine TreeNode*, vector<int>& voyage) { ... }
};
«» "

(Voir le code complet ci-dessus pour la mise en œuvre exacte.)

---

C'est pas vrai. Complexité

- **Heure:** O(n)
- **Espace:** O(h) – pile d'appel + tableau de résultats

---

##### 6=" Interview-Ready Conseils

Situation Comment expliquer
-- -- -- -- -- -- -- --
**DFS pattern**=Je traverse l'arbre exactement une fois, en utilisant l'index global pour synchroniser avec `voyage`. Autres
**Flips miniatures**.Le seul flip se produit lorsque l'élément suivant le force, donc nous sommes garantis des flips minimaux. Autres
**Cas impossible**=Si à un moment donné la valeur actuelle du nœud ne correspond pas à la valeur attendue, je retourne immédiatement `[-1]`. Autres
**Edge-case** Autres

---

LT;DR

- La partie **good** est un DFS linéaire et gourmand qui ne bascule que si nécessaire.
- La partie **bad** gère l'état global en toute sécurité en code récursif.
- La partie **ugly** est la duplication de code entre les langues et la plaque de chaudière.

Les trois versions linguistiques ci-dessous résolvent le problème dans le temps `O(n)` et l`espace `O(h)` tout en étant faciles à comprendre et prêts pour un entretien technique.

---

À emporter

Mastering LeetCode 971 présente :

- Connaissance de la traversée de l'arbre biologique**.
- Capacité d'écrire **code récursif propre et rapide**.
- Compréhension de **stratégies claires** pour les problèmes de changement minimal.

Si vous pouvez expliquer clairement cette solution dans une entrevue, vous démontrerez :

1. **Perspective algorithmique** – connaître le bon modèle à utiliser.
2. ** Style de codage** – concis mais lisible.
3. **L'état d'esprit de résolution des problèmes** – la manipulation précoce des cas de bord et de l'impossibilité.

Ajoutez cette solution à votre pile de prép d'entrevue et vous serez un peu plus près de l'atterrissage ce rôle d'ingénierie logicielle!

Bonne chance, et le codage heureux!