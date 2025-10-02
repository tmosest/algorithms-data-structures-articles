---
titre: LeetCode 1028. Récupérer un arbre de la route de précommande -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1. Récupérer un arbre binaire à partir de la route de précommande
> **LeetCode 1028 – Hard**
> **Mots clés:** *Binary Tree, Précommande Traversal, Encodage de profondeur, Stack, Récursion, LeetCode 1028, Interview Prep, Algorithme Design*

---

Récapitulation du problème

On vous donne une chaîne qui représente un **précommande** traversant un arbre binaire.
Chaque noeud est imprimé comme suit:

«» "
D tirets + valeur
«» "

* `D` – profondeur du noeud (profondeur de la racine = 0).
* `-` – caractère de tiret.
* "valeur" – entier positif (1 ≤ valeur ≤ 109).

Si un nœud n'a qu'un seul enfant, cet enfant est garanti être l'enfant **left**.
Reconstruisez l'arbre original et retournez sa racine.

> Exemple
> Entrée: "1-2-3-4-5-6-7"
> Produit: `[1,2,5,3,4,6,7]` (représentation au niveau de l'ordre)

---

- Oui. 2. Choisir la bonne approche

Démarche Temps Espace Complexité
- C'est quoi ?
**Descente récursive** (DFS)** **O(n)** – une passe au-dessus de la corde** **O(h)** – pile de récursion, `h` = hauteur**
**O(n)**

Les deux méthodes sont O(n) et correspondent aux contraintes (n ≤ 1000).
La méthode *stack* est souvent préférée pour les intervieweurs car elle évite les problèmes de profondeur de récursion et est très intuitive.

Ci-dessous nous présentons l'implémentation **stack** en trois langues (Java, Python, C++).
Le code est prêt à être copié et comprend les définitions `TreeNode` requises par LeetCode.

---

- Oui. 3. Mise en œuvre des références – Méthode de la pile

#### 3.1 Java

"Java
***
* Définition d'un noeud d'arbre binaire.
* classe publique TreeNode {
* Int val;
* TreeNode gauche;
* TreeNode droit;
* TreeNode(int val) { this.val = val; }
*}
*/
solution de classe {
public TreeNode récupérerTree(String S) {
si (S) null, S.isEmpty() retourne null;

// Chaque élément de la pile correspond à un nœud à sa profondeur.
// stack.peek() est le parent du noeud suivant à créer.
Deque<NodeWithDepth> pile = nouvelle ArrayDeque<>();

int i = 0; // index courant dans la chaîne
pendant que (i < S.longueur()) {
// 1=1 nombre de tirets → profondeur du noeud à venir
profondeur int = 0;
alors que (i < S.leng() && S.charAt(i) == '-') {
profondeur++;
i++;
}

// 2.
Int val = 0;
alors que (i < S.length() && Character.isDigit(S.charAt(i))) {
valeur = valeur * 10 + (S.charAt(i) - '0');
i++;
}

TreeNode noeud = nouveau TreeNode(val);

// 3-- Réduisez la pile jusqu'à ce qu'elle ne contienne que les ancêtres du nœud actuel
pendant que (stack.size() > profondeur) {
pile.pop();
}

// 4.
si (!stack.isEmpty()) {
Parent TreeNode = pile.peek();
si (parent. gauche == null) parent. gauche = noeud;
autre parent. droite = noeud;
}

// 5.- Poussez le nouveau noeud – il devient le nœud de profondeur actuel
empil.push(noeud);
}

// Le premier élément poussé est la racine
retour pile.isEmpty() ? null : pile.peekLast();
}

*** Classe d'aide pour garder la profondeur avec le noeud */
classe statique privée NodeWithDepth {
Noeud arbre;
profondeur int;
NodeWithDepth(NodeTreeNode, profondeur int) {
ce.node = noeud;
Ça. profondeur = profondeur;
}
}
}
«» "

> **Pourquoi `stack.peekLast()`? **
> Après la boucle, la pile contient le chemin entier de la racine au noeud le plus profond.
> La racine est l'élément *bottom* – `peekLast()` le donne en O(1).

---

3.2 Python

'`python
# Définition d'un noeud d'arbre binaire.
# classe TreeNode:
# def __init_(self, val=0, gauche=Aucune, droite=Aucune):
# Self.val = val
Moi-même. gauche = gauche
Moi-même. droite = droite
Solution de classe:
def récupérer Tree(self, S: str) -> 'Facultative[TreeNode]':
si ce n'est pas S:
retour Aucune

pile = [] # pile de (profondeur, TreeNode)
i = 0

alors que i < len(S):
profondeur
profondeur = 0
alors que i < len(S) et S[i] == '-':
profondeur += 1
i += 1

Valeur
Valeur = 0
alors que i < len(S) et S[i].isdigit():
Valeur = valeur * 10 + int(S[i])
i += 1

noeud = TreeNode(val)

# 3-
pendant que len(stack) > profondeur:
Pile.pop()

# 4--Attache le nœud
si pile:
parent = pile[-1]
si parent. gauche est None:
parent. gauche = noeud
Sinon:
parent. droite = noeud

# 5.
pile.append(node)

La racine est le bas de la pile
retourner la pile[0] si la pile n'est pas
«» "

---

### 3.3 C++

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
TreeNode* récupérerTree(string S) {
si (S.vide()) retourne nullptr;

struct NodeDepth {
Noeud arbre*;
profondeur int;
NodeDepth(TreeNode* n, int d) : node(n), profondeur(d) {}
};

vector<NodeDepth> pile; // vector utilisé comme pile
i = 0; // indice courant en S

pendant que (i < S.size()) {
// profondeur
profondeur int = 0;
alors que (i < S.size() && S[i] == '-') {
profondeur++;
i++;
}

Valeur
Int val = 0;
alors que (i < S.size() && isdigit(S[i]) {
val = valeur * 10 + (S[i] - '0');
i++;
}

TreeNode* noeud = nouveau TreeNode(val);

// 3-
pendant que (!stack.vide() && pile. back().profondeur >= profondeur)
pile.pop_back();

// 4.
si (!stack.vide()) {
TreeNode* parent = pile.back().node;
si (parent->left == nulptr)
parent->gauche = noeud;
Autre
parent->droit = noeud;
}

// 5.
emple.emplace_back(node, profondeur);
}

La racine est le premier élément poussé
retour pile.vide() ? nullptr : pile.front().node;
}
};
«» "

> Les trois extraits analysent la chaîne **once**, maintiennent une pile d'ancêtres et fixent correctement les enfants de gauche/droite en fonction de la disponibilité.

---

- Oui. 4. Article de blog – Code de Leet 1028: Récupérer un arbre binaire de la précommande Traversal

> *Écrit pour le développeur-candidat moderne qui veut une plongée profonde dans une interview-classique tout en gardant SEO à l'esprit. *

---

### 4.1 Titre & Meta Description

**Titre:** *Recover Binary Tree from Preorder Traversal – LeetCode 1028 expliqué*
**Meta Description:** *Guide étape par étape pour résoudre le LeetCode 1028. Solutions d'embouteillage et de récursion en Java, Python, C++. Explication prête à l'entrevue, analyse de la complexité, cas de pointe et perspectives de recherche d'emploi dans le monde réel. *

---

4.2 Table des matières

1. [Énoncé du problème] (#Énoncé du problème)
2. [Pourquoi la reconstruction de l'arbre Binary-Tree est importante] (#Why-binary-tree-reconstruction-matières)
3. [Constraints & Edge Cases](# Contraintes-&-edge-cases)
4. [Approches – Stack vs Récursion] (#Approaches-stack vs Récursion)
5. [Applications de référence](#applications de référence)
6. [Analyse du temps et de l'espace] (#analyse de l'espace-temps)
7. [Pros & Cons de la méthode de la pile](#pros--cons de la méthode de la pile)
8. [Pièges communs d'entrevue] (#pièges communs d'entrevue)
9. [Comment utiliser ces connaissances dans une entrevue technique] (#comment utiliser ces connaissances dans une entrevue technique)
10. [Pensées finales et lecture supplémentaire] (#pensées finales -- lecture supplémentaire)

---

### 4.3 Énoncé du problème

LeetCode 1028 vous demande de reconstruire un arbre binaire vu son **précommande** traversant avec profondeur codée comme des tirets. La longueur de chaîne d'entrée ne dépasse jamais 1 000, et les valeurs des nœuds sont dans la plage 1...109.

**Objectif:** Retourner la racine de l'arbre reconstruit.

---

4.4 Pourquoi Binary- Questions relatives à la reconstruction des arbres

- **Données du monde réel**: De nombreux systèmes sérialisent des arbres (p. ex. arbres de systèmes de fichiers, hiérarchies des composants de l'interface utilisateur) à l'aide de marqueurs de profondeur.
- **Entretien classique**: Ce problème teste l'analyse des cordes, les compétences en récursion/pierre, et une prise ferme de l'ordre de traversée des arbres.
* Fondement algorithmique** : La résolution de ce problème démontre la maîtrise du DFS, de la manipulation de la pile et de la rétro-tracking, ce qui fait surface dans de nombreux rôles de niveau supérieur.

---

4.5 Contraintes et causes de bord

Contraintes Implications
C'est pas vrai.
"n ≤ 1000" Les solutions monopass sont très bien; profondeur de récursion ≤ 1000 (sûr en Java/Python)
Le nœud a au plus un enfant → l'enfant gauche Pas d'ambiguïté lors de l'attachement des nœuds; la règle de gauche-première tient.
Le nombre d'hyphènes est égal à la profondeur

* Cas à tester :*
- Arbre asymétrique (`"1-2-3-4-5"`) → tous les nœuds sont laissés enfants.
- Noeud simple (`"42"`) → profondeur 0, pas de tirets.
- Nombres importants ("1000000000-2") → assurer la manipulation de 64 bits entier.

---

4.6 Approches – Stack vs Récursion

Récursion
C'est quoi ?
**Readability**
Autres **Sécurité de la profondeur de l'emplacement** Autres
**Mémoires en haut de la page**
**Complexité**= Heure `O(n)`, espace `O(h)`= Heure `O(n)`, `O(h)` espace

La méthode *stack* est adaptée à l'entrevue : elle vous donne un aperçu clair de la chaîne d'ancêtres.
La méthode *recursive* est plus concise en code, mais risque de déborder une pile si la profondeur de l'arbre approche de la longueur de la chaîne.

---

4.7 Mise en œuvre des références

Ci-dessous se trouve la solution **iterative stack** (Java, Python, C++), suivie d'un bref résumé de la variante *recursive* pour être complète.

- **Java** – utilise `ArrayDeque` et un `NodeWithDepth` sur mesure.
- **Python** – exploite une liste comme une pile, `isdigit()` pour l'analyse.
- **C++** – vecteur agissant comme pile; structure pour la profondeur.

(Voir la section 4.2 pour le code complet.)

---

4.8 Analyse du temps et de l'espace

Que `h` soit la profondeur maximale de l`arbre (`- n`).

**Heure**
- C'est quoi ?
"O(n)" – chaque char visité une fois "O(h)" – nombre de nœuds dans la pile
"O(n)" – même que la pile

Les deux atteignent un temps linéaire. L'utilisation de l'espace est limitée par la profondeur de l'arbre; dans le pire des cas `h = n`.

---

#### 4.9 Avantages et inconvénients de la méthode Stack

**Pour**

- **Deterministic** – parent est toujours sur le dessus de la pile.
- **Pas besoin de rétro-tracking** – nous créons la pile une fois que la profondeur correspond.
- ** Localité mémoire** – les éléments de la pile vivent dans la mémoire contiguë.

**Cons**

- Nécessite une structure de données auxiliaire (pistolet) qui peut se sentir lourd si vous êtes utilisé pour la récursion pure.
- Un peu plus de plaque de chaudière pour manipuler la taille et la fixation.

Dans l'ensemble, l'approche de la pile gagne sur *l'ergonomie d'entrevue*.

---

###4.10 Pièges communs d'entrevue

1. **En supposant que la chaîne soit délimitée par l'espace blanc** → oublier de gérer le comptage des tirets.
2. **Attacher des enfants en mauvais ordre** → doit vérifier si la gauche est libre avant d'attribuer le droit.
3. **Débordement d'index** → La lecture des chiffres doit s'arrêter à l'extrémité non numérique ou chaîne.
4. **Utiliser la mauvaise méthode de pile** → par exemple, sauter trop agressivement (profondeur > `stack.size()`) conduit à `NullPointerException`/segfault.
5. **Ignorer la règle de gauche de l'enfant** → ne peut pas déduire si un noeud est gauche ou l'enfant droit sans la règle.

---

### 4.11 Comment utiliser ces connaissances dans une entrevue technique

1. ** Expliquez clairement le problème** : mentionnez la précommande, la profondeur des tirets et la règle de gauche.
2. **Discussion des solutions potentielles**: Faire preuve de sensibilisation aux compromis itératifs et récursifs.
3. **Choisir la pile pour la clarté**: Il utilise une pile pour maintenir les ancêtres car elle donne une cartographie naturelle entre la profondeur et la taille de la pile. (en milliers de dollars)
4. **Parcourir un exemple**: Afficher comment `profondeur=2` conduit à faire apparaître deux nœuds.
5. **Complexité**: Citer "O(n)" temps, "O(h)" espace.
6. **Essais d'urgence**: Demandez si l'intervieweur veut que vous couvriez des arbres biaisés ou de grandes valeurs.
7. **Essais de concentration**: Fournissez des tests unitaires dans votre éditeur de code pour assurer l'exactitude.

---

### 4.12 Pensées finales et lecture supplémentaire

*LeetCode 1028* est plus qu'un puzzle à cordes; c'est une fenêtre dans la façon dont **données structurées** peuvent être sérialisées et désérialisées efficacement. La maîtrise se traduit ici par :

- pipelines de traitement des billes efficaces
- Cadres hiérarchiques de l'interface utilisateur
- Systèmes de fichiers distribués (HDFS)

**Prochaines étapes:**
- Pratique *Sérialisation d'arbre* (LeetCode sérialise et désérialise l'arbre binaire).
- Explorer *prefix/postfix notation* parsing pour les expressions arithmétiques.
- Etude *Visites d'Euler* et *décomposition de lumière lourde* pour les requêtes d'arbres avancées.

---

### 4.13 Appel à l'action

> Vous voulez voir cet algorithme en action ? Découvrez les extraits de code en Java, Python et C++ ci-dessus. Implémentez-les, exécutez des tests unitaires, et partagez vos résultats sur GitHub ou un blog personnel – excellent pour le portfolio et la préparation d'entrevue.

---

- Oui. 5. Résumé

- **Trois solutions robustes** (arrêt, récursion) à LeetCode 1028 sont maintenant disponibles.
- **Le code de référence** en Java, Python, C++ montre une analyse de chaîne propre et une manipulation de pile.
- **Blog article** fournit le contexte, les pièges, et la stratégie d'entrevue tout en renforçant la visibilité SEO pour les développeurs ciblant les entretiens techniques.

Autres Bon codage et bonne chance dans votre prochaine interview! C'est ce qu'il a dit.

---

* Fin de la réponse. *