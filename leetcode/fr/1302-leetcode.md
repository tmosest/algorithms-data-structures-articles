---
titre: LeetCode 1302. Feuilles les plus profondes Somme -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Feuilles les plus profondes Somme – LeetCode 1302
### 3-Way Mise en œuvre
*Java *=Python *=C++*

---

### Java (O(n) temps, O(n) espace)

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
Importation de java.util.*;

solution de classe {

Int public le plus profond FeuillesSum(racine de nœud d'arbre) {
si (root) null retourne 0;

Demande<TreeNode> q = nouveau tableau<>();
q.offre(root);
= 0;

alors que (!q.isEmpty()) {
niveau intTaille = q.size();
somme = 0; // somme de remise pour le nouveau niveau

pour (int i = 0; i < levelSize; i++) {
TreeNode cur = q.poll();
somme += cur.val;

si (cur.left != null) q.offre(cur.left);
si (cur.right != null) q.offre(cur.right);
}
}
somme de retour; // somme du dernier niveau traité (feuilles les plus profondes)
}
}
«» "

---

Python (O(n) temps, O(n) espace)

'`python
# Définition d'un noeud d'arbre binaire.
# classe TreeNode:
# def __init_(self, val=0, gauche=Aucune, droite=Aucune):
# Self.val = val
Moi-même. gauche = gauche
Moi-même. droite = droite

à partir de collections import deque
de taper l'importation Facultatif

Solution de classe:
plus profond FeuillesSum(self, root: Facultatif[TreeNode]) -> Int:
si ce n'est pas la racine:
retour 0

q = deque([root])
alors que q:
niveau_somme = 0
pour _ dans la plage(len(q)):
noeud = q.popleft()
niveau_sum += noeud.val
en cas de nœud. gauche:
q.Append(node.left)
en cas de nœud. à droite :
q.annexe(node.right)
_somme du niveau de retour
«» "

---

### C++ (O(n) temps, O(n) espace)

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
#incluez <queue>
utilisant l'espace de noms std;

solution de classe {
public:
int les plus profonds FeuillesSum(racine TreeNode*) {
si (!root) retourne 0;
la file d'attente <TreeNode*> q;
q.push(root);
= 0;
pendant que (!q.vide()) {
int sz = q.size();
somme = 0; // réinitialiser pour le nouveau niveau
pour (int i = 0; i < sz; ++i) {
TreeNode* cur = q.front(); q.pop();
somme += cur->val;
si (cur->left) q.push(cur->left);
si (cur->right) q.push(cur->right);
}
}
somme de retour; // somme du niveau le plus profond
}
};
«» "

---

- Oui. 2. Article de blog – Le bon, le mauvais, et le lamentable de résoudre *Les feuilles les plus profondes Somme*

Titre
**Les feuilles les plus profondes sum – Le bon, le mauvais et le mauvais (Binary Tree, BFS, DFS & Interview-Ready)* *

> *Mots clés:* Feuilles les plus profondes Somme, binaire Arbre, Leetcode 1302, BFS, DFS, arbre récursif, codage d'entrevue, algorithme, complexité temporelle, complexité spatiale, entretien d'emploi, ingénieur logiciel

---

Introduction

Lorsque vous faites défiler les problèmes de LeetCodes, **1302. Deepest Leaves Sum** apparaît souvent comme une question que beaucoup d'intervieweurs aiment. Le but est simple : *retourner la somme des valeurs des feuilles les plus profondes d'un arbre binaire*. Pourtant, sous la simplicité se trouvent des choix de conception subtils, des pièges cachés, et des astuces d'optimisation qui font de ce problème un micro-test pour une proue de l'arbre candidat.

Dans ce poste nous disséquons les parties **good**, **bad** et **ugly** pour résoudre le problème. Nous allons passer par la solution classique de recherche en largeur (BFS), la comparer avec les alternatives de recherche en profondeur (FDS) et expliquer pourquoi l'approche BFS est habituellement préférée dans le code de production et les entrevues.

---

- Oui. Le bon – Pourquoi le problème est un Gold‐Mine

1. ** Clarté conceptuelle**
Le problème est un énoncé propre: *=somme les noeuds les plus profonds de la feuille. Il teste la compréhension de la profondeur de l'arbre, de la traversée de niveau et de l'agrégation dynamique.

2. **Balance temps et espace**
La solution optimale fonctionne dans **O(n)** temps et utilise **O(n)** espace auxiliaire (faible file d'attente/poche). Cela correspond à la limite inférieure pour les problèmes liés aux arbres – il n'y a aucun moyen de sauter l'inspection de chaque noeud.

3. ** Réutilisabilité des connaissances* *
La maîtrise de ce problème renforce les compétences avec :
- BFS basé sur les files d'attente
- Récursion DFS & pile itérative
- Manipulation des pointeurs "null"
- Modèles de traversée de niveau

Ceux-ci sont transférables à d'autres problèmes de LeetCode tels que *Binary Tree Order Traversal*, *Profondeur maximale de l'arbre binaire*, *Sum of Left Leaves*, etc.

4. **Entretien-Amis**
Les intervieweurs apprécient les problèmes qui sont courts à dire mais exigent que le candidat montre de la profondeur dans la pensée algorithmique. Il ouvre des portes à la discussion sur - Pourquoi BFS ? - Pourquoi DFS ? - et sur l'optimisation de la récursion de queue.

---

- Oui. Les mauvais – les erreurs courantes et les cas de bord

Pourquoi ça se casse
C'est pas vrai.
**Utiliser le DFS pour accumuler la profondeur et la somme en un seul passage**= Sans une comptabilité soignée, vous pourriez ajouter des sommes intermédiaires qui appartiennent à des niveaux non profonds. Tenir une trace de la profondeur maximale vue jusqu'à présent et de la somme de course. Réinitialisez la somme lorsqu'un niveau plus profond est trouvé. Autres
** Supposons que l'arbre soit équilibré**. Un DFS naïf empilé seul peut frapper les limites de récursion ou empiler le débordement dans des langages comme Python. Utilisez une pile explicite ou itérative BFS pour éviter une récursion profonde. Autres
**Niveau de comptage**= Erreurs hors-par-un lorsque vous commencez à compter la profondeur de `0` ou `1`. Décider une convention (profondeur de la racine = 0) et la maintenir cohérente à travers l'algorithme. Autres
**Ignorer les enfants `null`**= Ne pas vérifier pour `null` avant de pousser sur une file d'attente conduit à `NullPointerException` en Java ou des défauts de segmentation en C++. * Garde avec `si (node.left) q.push (node.left);` etc. Autres
**Utilisation de `sum += node.val` avant de vérifier si le noeud est une feuille**.Si vous ajoutez prématurément des valeurs non-feuilles, la somme finale sera erronée. Autres Soit ajouter seulement quand `noeud. gauche == Null && noeud. right == null` ou utilisez le niveau-order et ajoutez tous les nœuds du dernier niveau (simpler). Autres

---

### L'horrible – Pourquoi les gens écrivent

1. **Suringénierie**
Certains candidats essaient de calculer la hauteur d'abord, puis lancent un second DFS pour résumer les nœuds à la hauteur-1. Cette approche à deux passages, tout en étant correcte, ajoute une récursion supplémentaire et une complexité de code.

2. **Mixation du BFS & DFS en une seule fonction**
L'écriture d'un assistant récursif qui retourne à la fois la profondeur et la somme partielle conduit à un code convolué qui est difficile à déboguer.

3. **Ignorer les facteurs constants**
Pour les intervieweurs, le *big-O* compte, mais dans la pratique, un "O(n)" BFS qui stocke l'ensemble du niveau peut être plus lent en raison de cache manquants qu'un DFS soigneusement codé qui utilise la récursion de queue.

4. **Optimisation de l'espace
L'utilisation d'une variable globale pour accumuler des sommes tout en récursant peut causer des conditions de race dans des environnements concomitants (moins pertinents pour LeetCode mais un bon point de conversation dans les entrevues).

---

### Solution Walk‐Trough – La façon BFS

**Idée:**
Procéder au niveau de l'arbre par niveau. Une fois le niveau final traité, le `level_sum` contiendra la somme des feuilles les plus profondes.

1. **Initialiser une file d'attente** avec le nœud racine.
2. **Bien que la file d'attente ne soit pas vide :**
- Déterminer la taille du niveau actuel (`sz = q.size()`).
- Réinitialiser `level_sum = 0`.
- Déterminez les temps "sz" :
* Faites un nœud.
* Ajouter sa valeur à `level_sum`.
* Faites connaître ses enfants non null.
3. **Retour `level_sum`.**
À la sortie de boucle, le dernier `level_sum` correspond au niveau le plus profond.

**Pourquoi BFS? **
- Garantie que lorsque nous terminons le traitement d'un niveau, nous avons traité *tous* noeuds à cette profondeur.
- Plus simple à coder et plus facile à raisonner que DFS avec le suivi de profondeur.
- Manipulation naturelle des arbres biaisés sans risque de débordement de cheminée.

**Complexité temporelle :**
Chaque noeud est enquêté et dépouillé une fois.

**Complexité spatiale:**
La taille maximale de la file d'attente correspond à la largeur maximale de l'arbre. Dans le pire des cas (arbre parfaitement équilibré), il s'agit de **O(n)**, mais pour les arbres biaisés il se dégrade à **O(1)**.

---

Option alternative – Récursion du SSD (basée sur la hauteur)

"Java
Int public le plus profond FeuillesSum(racine de nœud d'arbre) {
retour dfs(root, 0, nouvelle int[]{-1, 0});
}

vide privé dfs(nœud TreeNode, profondeur int, données int[]) {
si (noeud == nul) retour;
si (profondeur > données[0]) {
données[0] = profondeur; // nouvelle profondeur la plus profonde
données[1] = noeud.val; // somme de remise
} sinon si (profondeur == données[0]) {
données[1] += noeud.val; // même profondeur
}
dfs(node.left, profondeur + 1, données);
dfs(node.right, profondeur + 1, données);
}
«» "

**Pour :**
- Oui. Pas de file d'attente.
- Oui. Utilise uniquement la pile d'appel (auxiliaire **O(h)**).

**Cons:**
- La récursion profonde peut déborder si la hauteur de l'arbre ~ n.
- Un peu plus difficile à mettre en œuvre et à tester.

---

### Conseils d'entrevue – Points de discussion

1. **Demandez à l'intervieweur d'abord**
Vous voulez une solution itérative ou récursive ? (en milliers de dollars)
Certains intervieweurs préfèrent explicitement le DFS au test de récursion.

2. **Discussion de la fuite**
Expliquez comment des langages comme Java ou C++ pourraient interligner les appels de queue, mais la plupart ne le font pas.

3. **Précipitations* *
Et un arbre vide ? → retourner 0.
Et si l'arbre n'a qu'un seul nœud ? → profondeur = 0, somme = valeur du noeud.

4. ** Contraintes réelles et mondiales* *
En production, vous devrez peut-être gérer des traversées simultanées en lecture seule. BFS avec une file d'attente locale est sûr de thread, alors qu'une variable globale ne serait pas.

---

### Conclusion – Transformer les congés les plus profonds en une compétence gagnante

Mastering *Deepest Leaves Sum* vous donne:

- Une preuve concise de concept pour les traversées binaires d'arbres.
- Un début de conversation solide sur les compromis entre BFS et DFS.
- Un modèle démontrable qui apparaît dans de nombreux systèmes plus grands (par exemple, le calcul de mesures agrégées à travers des données hiérarchiques).

**Rappel :**
La solution "good" n'est pas celle qui utilise la récursion pour calculer la hauteur d'abord. C'est le BFS propre et monopass que vous pouvez écrire en 10 lignes de code, expliquer à un gestionnaire d'embauche, puis réutiliser dans d'autres problèmes. Les erreurs d'apprentissage sont de grands moments d'apprentissage, et la sur-ingénierie d'apprentissage révèle votre croissance en tant qu'ingénieur logiciel.

Bonne chance – continuez à faire un somme de ces feuilles les plus profondes, et que votre prochaine entrevue soit aussi simple et enrichissante que celle-ci!

---

- Oui. À propos de l'auteur

*Alexei *Alec* Torres
Ingénieur logiciel senior chez **TechNova**, passionné de LeetCode et mentor à temps partiel sur *CodeSignal* et *Educatif. io*. Passionné de structures de données, de code propre et de faire de la préparation d'entrevue un puzzle amusant plutôt qu'une corvée.

Suivez-moi sur **Linked En** pour plus de contenu de prép d'entrevue: [linkedin.com/in/alexei-torres](https://linkedin.com/in/alexei-torres)

---

Bon codage ! C'est ce qu'il a dit.

---

> *Si vous avez trouvé cet article utile, partagez-le avec vos collègues développeurs et déposez un commentaire ci-dessous avec les astuces que vous avez utilisé pour clouer le problème de Leaves Sum le plus profond. *