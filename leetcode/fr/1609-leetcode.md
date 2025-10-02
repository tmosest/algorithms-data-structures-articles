---
titre: LeetCode 1609. Même l'arbre bizarre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1609. Même- Arbre étrange
**Moyenne de l'espace O(N)

> Un arbre binaire s'appelle **Even-Odd** lorsque:
> 1. Les niveaux sont numérotés à partir de 0 (racine = niveau 0).
> 2. Les niveaux indexés de façon uniforme contiennent des valeurs **odd** qui augmentent considérablement** de gauche à droite.
> 3. Les niveaux classés par ordre de grandeur contiennent des valeurs **même** qui sont ** strictement décroissantes** de gauche à droite.

Retourner `true` si l'arbre satisfait aux trois règles, sinon `faux`.

---

Pourquoi ce problème est important pour les entrevues de travail

- **La largeur de la première traversée** est un agrafe pour les questions binaires.
- Oui. Les tests de tâches **stateful traversal** (suivant la voie de la parité de niveau).
- Oui. Il nécessite une logique **de sortie précoce** – une fois qu'une violation est trouvée, l'algorithme entier s'arrête.
- Les candidats doivent réfléchir aux compromis temps/espace** et mettre en œuvre les contrôles de monotonicité proprement.

Le fait de pouvoir discuter de ce problème (et de ses variations) dans une entrevue montre que vous comprenez les traversées d'arbres, la manipulation des cas de bord et la complexité algorithmique.

---

Récapitulation du problème (version courte)

Texte
Entrée : racine TreeNode
Sortie : booléen

Règle 1 : Niveau 0, 2, 4...
Règle 2 : Niveau 1, 3, 5... -> nombres égaux, en baisse stricte
«» "

---

Idée de base – Ordre de niveau avec contrôles de parité

1. **BFS** (queue) pour visiter les nœuds niveau par niveau.
2. Gardez un drapeau `isEvenLevel` (`true` pour des niveaux égaux).
3. Pour chaque niveau:
* **Même niveau**: valeur doit être impair et `valeur > prev`.
* **Niveau idéal**: la valeur doit être égale et `valeur < prev`.
4. Mettre à jour `prev` après avoir vérifié le nœud.
5. Enquete les enfants de gauche et de droite pour le prochain niveau.
6. Dépliez le drapeau de niveau après avoir terminé un niveau.

Parce que nous pouvons retourner `false` dès qu'une règle est cassée, l'algorithme est linéaire dans le nombre de nœuds.

---

Mise en œuvre

Ci-dessous sont des solutions propres, prêtes à coller dans **Java**, **Python** et **C++**.

> **Note**: Les trois solutions utilisent la même logique BFS; les seules différences sont la syntaxe et les structures de données spécifiques au langage.

---

### Java

"Java
importer java.util.LinkedList;
Importer java.util. Demande;

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
le booléen public estEvenOddTree(racine du node d'arbre) {
si (root) null retourne true;

Demande <TreeNode> q = nouvelle liste liée<>();
q.offre(root);
booléen estEvenLevel = true; // le niveau 0 est égal
int prev = estEvenLevel ? Integer.MIN_VALUE : Integer. MAX_VALEUR;

alors que (!q.isEmpty()) {
taille int = q.size();
Niveau int Précédent = prev; // réinitialiser prev pour chaque niveau

pour (int i = 0; i < taille; i++) {
Node d'arbre = q.poll();

// Règle de parité des contrôles
si (est même niveau) {
si (node.val % 2 == 0== node.val <= levelPrev) retourner faux;
} autre {
si (node.val % 2 == 1== node.val >= levelPrev) retourner faux;
}

niveauPrev = noeud.val;

// Ajouter des enfants pour le niveau suivant
si (node.left != null) q.offre(node.left);
si (node.right != null) q.offre(node.right);
}

// Parité de niveau Flip pour le calque suivant
estEvenLevel = !isEvenLevel;
}
retour vrai;
}
}
«» "

---

Python

'`python
# Définition d'un noeud d'arbre binaire.
# classe TreeNode:
# def __init_(self, val=0, gauche=Aucune, droite=Aucune):
# Self.val = val
Moi-même. gauche = gauche
Moi-même. droite = droite

à partir de collections import deque

Solution de classe:
def isEvenOddTree(self, root: TreeNode) -> bool:
si ce n'est pas la racine:
retour Vrai

q = deque([root])
is_even_level = True # level 0 est égal
prev = float('-inf') si is_even_level autre float('inf')

alors que q:
Taille = lenq
niveau_prev = prev

pour _ dans la gamme(size) :
noeud = q.popleft()

# Contrôle de la parité et de la monotonicité
i is_even_level :
si node.val % 2 == 0 ou node.val <= level_prev:
Retour Faux
Sinon:
i node.val % 2 == 1 ou node.val >= niveau_prev :
Retour Faux

niveau_prev = noeud.val

en cas de nœud. gauche:
q.Append(node.left)
en cas de nœud. à droite :
q.annexe(node.right)

# Réduire la parité de niveau
is_even_level = pas is_even_level

retour Vrai
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
#incluez <queue>
utilisant l'espace de noms std;

solution de classe {
public:
bool isEvenOddTree(racine TreeNode*) {
si (!root) retourne vrai;

la file d'attente <TreeNode*> q;
q.push(root);
bool isEvenLevel = true; // le niveau 0 est égal
int prev = estEvenLevel ? INT_MIN : INT_MAX;

pendant que (!q.vide()) {
int sz = q.size();
Niveau int Précédent = prev; // réinitialiser pour ce niveau

pour (int i = 0; i < sz; ++i) {
TreeNode* cur = q.front(); q.pop();

if (isEvenLevel) { // even Level: valeurs impaires, augmentation
si (cur->val % 2 == 0.->val <= levelPrev) retourner faux;
} autre { // niveau impair: valeurs égales, diminution
si (cur->val % 2 == 1=" cur->val >= levelPrev) retourner faux;
}

niveauPrev = cur->val;

si (cur->left) q.push(cur->left);
si (cur->right) q.push(cur->right);
}

isEvenLevel = !isEvenLevel; // flip pour le niveau suivant
}
retour vrai;
}
};
«» "

---

Étape par étape (exemple de Java)

1. ** Initialisation du temps** – commencer par la racine.
2. **Taille du niveau** – "taille = q.size()" indique combien de nœuds appartiennent au niveau actuel.
3. **Prev Value** – `prev` est initialisé à `INT_MIN` sur des niveaux égaux (toute valeur impair sera plus grande) et à `INT_MAX` sur des niveaux impairs (toute valeur pair sera plus petite).
4. **Contrôle des nœuds** –
* Même niveau : `node.val % 2 == 1` ET `node.val > prev`.
* Niveau bizarre : `node.val % 2 == 0` ET `node.val < prev`.
5. **Défaut précoce** – retour `faux` immédiatement si une règle est violée.
6. **Encouler les enfants** – à gauche puis à droite, en préservant l'ordre de gauche à droite.
7. **Niveau Flip** – «estEvenLevel = !estEvenLevel».

---

Pièges communs

Piège
- Oui.
Autres **Utiliser `prev = Integer.MIN_VALUE` sur les deux niveaux**= Réinitialiser `prev` par niveau; utiliser `INT_MIN` uniquement sur des niveaux égaux, `INT_MAX` sur des niveaux impairs. Autres
**Mixation de l'ordre de gauche/droite** Le BFS garantit un ordre de niveau correct. Autres
**Ignorer les enfants "null"** . Ne pas enquerrer "null" ; sinon la file d'attente va augmenter inutilement. Autres
**Ne pas retourner le drapeau après chaque niveau**.Si vous oubliez de basculer `isEvenLevel`, tous les niveaux seront traités comme pair. Autres

---

Analyse de complexité

Complexe métrique
C'est pas vrai.
**Heure**="O(N)" – chaque noeud est visité exactement une fois. Autres
**L'espace**='O(N)' – la file d'attente la plus défavorable tient tous les nœuds au niveau le plus profond (= la moitié de l'arbre). Autres

---

Autres approches

1. **Recursive DFS with Level Tracking** – passe le numéro de niveau à chaque appel récursif, mais vous devez garder une trace de la valeur précédente par niveau.
2. **DFS itérative avec Stack** – complexité similaire mais plus lourde pour maintenir l'ordre.
3. **Divide‐et‐Conquer** – traiter les sous-arbres gauche et droit, puis fusionner les résultats; frais généraux inutiles.

BFS reste la solution la plus simple et la plus lisible pour ce problème.

---

Faits saillants du SEO

- **Titre** : Solution de LeetCode d'arbre d'Even-Odd – Java, Python, C++ expliqué
- **Mots clés**: *Même l'arbre bizarre, LeetCode 1646, Binary Tree BFS, ordre de niveau Traversal, préparation d'entrevues, Structures de données, complexité temporelle, complexité spatiale, Algorithme de sortie précoce, vérification de la parité des arbres*
- **Description détaillée**: Maîtrisez le problème Even-Odd Tree sur LeetCode avec des solutions BFS étape par étape en Java, Python et C++. Comprendre les règles de parité, la complexité et les stratégies d'entrevue. (en milliers de dollars)

---

À emporter

L'Even-Odd Le problème des arbres est une vitrine concise de :

1. **La première traversée** avec une file d'attente.
2. **Traitement de la parité de niveau.
3. **Monotonicité et contrôles de parité** avec sortie anticipée.
4. **Heure linéaire** et **espace optimal**.

N'hésitez pas à modifier les solutions pour les variations (p. ex., commande stricte ou non stricte) ou à manipuler de grands arbres dans des contextes d'entrevue. Bonne chance – montrez à ces intervieweurs que vous avez des traversées d'arbres sous votre ceinture ! C'est ce qu'il a dit.

---