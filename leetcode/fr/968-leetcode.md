---
titre: LeetCode 968. Caméras à arbre binaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Caméras d'arbre binaire – LeetCode 968
> *Hard – Après l'ordre Greedy DFS*

Résolvez le problème en **Java, Python et C++** et lisez un court billet de blog SEO qui explique l'idée, le bon, le mauvais, et le laid, et pourquoi maîtriser ce problème vous aide à trouver un emploi technologique.

---

- Oui. 1. Code

> **Conseil:** La solution est la même idée dans les trois langues:
> *Post-order* traversal qui retourne un des trois états
> – **-1** : le noeud est **non surveillé* *
> – **0** : noeud est **monitored** (pas de caméra ici)
> – **1** : noeud **a une caméra**

> Le parent utilise ces valeurs pour décider s'il a besoin d'une caméra.

---

#### 1.1 Java

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
caméras internes privées = 0;

Int public minCameraCover(racine d'arbre) {
// Si root n'est pas surveillé après le DFS nous avons besoin d'un appareil photo de plus.
retour dfs(root) == -1 ? caméras + 1 : caméras;
}

***
* @return -1 : le noeud n'est PAS surveillé
* 0 : le noeud est surveillé (pas de caméra)
* 1 : noeud A une caméra
*/
Int privé dfs(nœud TreeNode) {
si (node == null) retourner 0; // null est considéré comme surveillé

int gauche = dfs(node.gauche);
int droite = dfs(node.right);

// Si aucun enfant n'est surveillé, placez la caméra ici.
Si (à gauche) -1) {
caméras++;
retour 1; // ce nœud a maintenant une caméra
}

// Si un enfant a une caméra, ce nœud est surveillé.
Si (à gauche) 1) {
retour 0; // surveillé, pas de caméra
}

// Aucun des enfants n'a de caméra et tous sont surveillés.
retour -1; // non surveillé, le parent doit surveiller
}
}
«» "

---

#### 1.2 Python

'`python
# Définition d'un noeud d'arbre binaire.
# classe TreeNode:
# def __init_(self, val=0, gauche=Aucune, droite=Aucune):
# Self.val = val
Moi-même. gauche = gauche
Moi-même. droite = droite

Solution de classe:
def minCameraCover(même, racine: TreeNode) -> Int:
auto.caméras = 0

si self.dfs(root) == -1: # la racine n'est toujours pas surveillée
Revenez vous-même. caméras + 1
retour self.cameras

def dfs(self, noeud: TreeNode) -> Int:
"""
Retour :
-1 : le noeud n'est PAS surveillé
0 : le noeud est surveillé
1 : noeud A une caméra
"""
si ce n'est pas le nœud:
retour 0 # nul est considéré comme surveillé

gauche = auto.dfs(node.gauche)
droite = self.dfs(node.right)

s'il reste == -1 ou à droite == - 1 :
soi-même. caméras += 1
retour 1

s'il reste == 1 ou à droite == 1 :
retour 0

retour -1
«» "

---

*## 1.3 C++

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
int minCameraCover(racine TreeNode*) {
caméras = 0;
si [dfs(root)] -1) caméras de retour + 1; // racine non couverte
les caméras de retour;
}

particulier:
caméras int = 0;

// -1: NON surveillé, 0: surveillé, 1: a une caméra
int dfs(nœud TreeNode*) {
si (!node) retourne 0; // null est surveillé

int gauche = dfs(node->gauche);
Int droite = dfs(node->right);

Si (à gauche) -1) { // enfant non surveillé
++caméras;
retour 1; // placer la caméra ici
}

Si (à gauche) 1) { // enfant a une caméra
retour 0; // surveillé
}

retour -1; // toujours pas surveillé
}
};
«» "

---

- Oui. 2. Article du blog

> **Titre:** *Binary Tree Cameras – LeetCode 968 Résolue en Java, Python et C++ *
> **Mots clés:** caméras d'arbre binaire, LeetCode 968, problème dur, algorithme d'entrevue, post-commande DFS, cupidité, entretien d'emploi, recruteur de technologie

---

2.1 Introduction

Si vous êtes en train de vous préparer à une interview d'ingénierie **logiciel**, vous vous trouverez à résoudre des problèmes difficiles qui poussent votre compréhension des arbres, la programmation dynamique, et des stratégies gourmandes.
LeetCode 968 – **Binary Tree Cameras** – est l'un de ces problèmes de signature.

> **Pourquoi ça compte**
> • Teste votre capacité à raisonner avec les états des arbres.
> • Nécessite une solution DP propre et ascendante.
> • Affiche les recruteurs vous pouvez écrire un code efficace et lisible en plusieurs langues.

Dans cet article, nous traversons le **good**, le **bad**, et le **ugly** de ce problème, partageons une solution **greedy post-order**, et montrons comment vous pouvez l'implémenter dans **Java, Python et C++**.

---

### 2.2 Énoncé du problème

> **Don** arbre binaire, vous pouvez placer une caméra sur n'importe quel noeud.
> Une caméra peut surveiller son parent, lui-même, et ses enfants immédiats.
> **Retourner le nombre minimum de caméras nécessaires pour surveiller chaque noeud** de l'arbre.

*Contre: *
- 1 ≤ nombre de nœuds ≤ 1000
- Les valeurs de nœuds sont toutes 0 (la valeur n'est pas pertinente).

---

2.3 La bonne – Pourquoi l'idée de l'avidité fonctionne

- **Résumé :** Un état de nœud est entièrement déterminé par les états de ses enfants.
- ** Seulement 3 états nécessaires** (non surveillé, surveillé, caméra) – maintient le DP petit.
- ** Temps linéaire** (O(n)) et **O(h)** cheminée auxiliaire (profondeur de récursion).
- **Code élégant** : une seule fonction "dfs" et un compteur.

** Diagramme d'état**

Gauche Droite Actuelle
- C'est quoi ?
-1 (non surveillé)
1 (caméra)
0 (surveillant)

---

2.4 Les mauvaises – Pièges communs

Pourquoi ça fait mal ?
- C'est quoi ?
**Traitez nul comme non surveillé**
**Return value maluse** . Confusant `-1` avec `0` dans les ints primitifs de Java .
**Profondeur récursive**=Débordement de la pile pour l'arbre de 1000 noeuds en forme d'équerre. Autres
**Ne pas vérifier la racine après le DFS** -1) caméras

---

#### 2.5 Lamentable – Quand les choses tournent mal

- **Désignement des conditions**: Placer la caméra avant de vérifier les enfants conduit à des comptes sous-optimaux.
- **PDD trop compliqué**: Essayer de stocker une liste des positions de la caméra ou utiliser BFS au lieu de DFS transforme la solution élégante en désordre.
- **Profondeur de l'arbre-codage dur**: Certaines solutions précalculent la profondeur, puis lancent une autre boucle – inutile.

---

### 2.6 Solution complète – SSD après l'ordonnance

1. **DFS** retourne **état** du nœud.
2. Si un enfant est **non surveillé** (`-1`), placer la caméra sur le noeud courant (`cameras++`) et retourner **camera** (`1`).
3. Si un enfant a une **caméra** (`1`), le noeud est **monitored** (`0`).
4. Autrement, le noeud est **non surveillé** (`-1`).
5. Après DFS, si le **root** n'est pas surveillé, ajoutez une autre caméra.

> **Heure**: O(n) – chaque noeud visité une fois.
> **Espace**: O(h) – pile de récursion, où `h` est la hauteur des arbres.

---

2.7 Échantillons de codes

*(Voir la section de code ci-dessus pour les implémentations Java, Python, C++.) *

---

2.8 Comment cela vous aide à trouver un emploi

1. **Démonstration de l'arbre DP** – Beaucoup d'intervieweurs demandent quoi ? (en milliers de dollars)
2. **Shows Coding Propreté** – Trois langues, logique identique → grand extrait de portfolio.
3. **Faits saillants Problème-Solving Mindset** – Reconnaître la propriété gourmande réduit considérablement la complexité.
4. **Préparatifs pour les Variations** – S'ils demandent Qu'en est-il si les caméras coûtent différemment?

Ajoutez ce problème à votre liste **LeetCode Top 100 Hard**, postez les solutions sur GitHub et discutez des compromis dans votre entrevue.

---

###2.9 Cheat de référence rapide Feuille

La langue contre la signature du DFS Autres
C'est pas vrai.
Java "int cameras" "int dfs (noeud TreeNode)" Autres
Def dfs(self, noeud) Autres
C++="int cameras`="int dfs(nœud TreeNode*)" Autres

---

2.10 A emporter

> *Binary Tree Cameras* vous enseigne comment ** modéliser un problème avec une petite machine d'état** et le résoudre avec un **pass unique DFS**.
> Maîtrisez ceci, et vous serez prêt à affronter tout problème difficile lié aux arbres sur le plancher de l'entrevue.

Bonne chance ! C'est ce qu'il a dit.

---

> **Ressources :**
> • LeetCode 968: https://leetcode.com/problèmes/binary-tree-cameras/
> • Discuter sur les questions Reddit /r/cscareer.
> • Dépôt GitHub pour solutions multi-lang.

---

> **Disclaimer:** Le code est écrit avec Java 17, Python 3.10 et C++17 en tête.
> Des adaptations peuvent être nécessaires pour votre environnement de compilateur ou d'exécution.

---


> **Fin de l'article**



---

> **Note aux lecteurs:**
> Si vous souhaitez plonger plus profondément dans l'arbre DP ou avez besoin d'aide avec un autre problème dur LeetCode, laissez un commentaire ou envoyez-nous un courriel à `interviewguru@exemple.com`. Bon codage !