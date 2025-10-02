---
titre: LeetCode 1644. Ancêtre commun le plus bas d'un arbre binaire II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Résumé des problèmes (Code Leet 1644)

> **Ancêtre commun de Lowest d'un arbre binaire II**
> Moyenne: 1 k+ résolu

Compte tenu de la racine d'un arbre binaire et de deux nœuds `p` et `q`, retourner l'ancêtre le plus bas (LCA)** de `p` et `q`.
Si **** `p` ou `q` est *non* présent dans l'arbre, retourner `null`.
Toutes les valeurs des nœuds sont uniques.

> **Constraints**
> * 1 ≤ #noeud ≤ 104
> * − 109 ≤ nœuds
> * `p != q`

> **Suivi**
> Trouvez le LCA *sans* un second passe qui vérifie si les nœuds existent.

---

- Oui. 2. Pourquoi 1644 est plus dur que 236?

Caractéristiques 236 (Ancêtre commun de Lowest d'un arbre binaire)
[En milliers de dollars des États-Unis]
**Garantie**** Les deux `p` et `q` sont **garantis** d'être dans l'arbre.
Autres **Résultat sur le nœud manquant**
**Early‐exit**=Safe: retourner dès que vous trouvez `p` ou `q`=Safe: vous devez toujours chercher le reste de l'arbre==

En raison de l'absence de garantie, la solution classique de 236 ('if (root==p=" root==q) return root;`) ne peut pas être utilisée sans modifications. Nous devons suivre si nous avons réellement vu les deux nœuds tout en traversant l'arbre entier.

---

- Oui. 3. Aperçu de la solution

Nous faisons un seul DFS ** post-commande** et propageons deux informations :

1. **Le candidat à la LCA** est revenu de l'appel récursif.
2. **Drapeaux** indiquant si `p` et/ou `q` ont été vus dans le sous-arbre actuel.

Lorsque les deux drapeaux sont « vrai », le nœud actuel est le véritable LCA.
Si un seul drapeau est « vrai », nous renvoyons le nœud correspondant (pour que le parent puisse décider).
Si rien ne correspond, nous retournons 'null'.

Il existe deux façons idiomatiques de stocker les drapeaux:

Méthode de mise en oeuvre
- C'est quoi ?
**Deux champs booléens** ('pFound', 'qFound') , plus facile à lire , état mutable ; plus difficile à tester en isolement ,
**Compte entier** Un seul champ Un peu moins expressif mais très compact

Les deux ont **O(N)** temps et **O(H)** espace (call pile récursive).

---

- Oui. 4. Mise en œuvre de Java

"Java
// Définition pour un nœud binaire.
classe TreeNode {
la valeur intérieure;
TreeNode gauche;
TreeNode droit;
TreeNode(int x) { val = x; }
}

solution de classe publique {
- Oui. Méthode 1 : deux drapeaux booléens
le pound booléen privé;
Booléen privé qFound;

public TreeNode le plus basCommonAncêtre(racine TreeNode, TreeNode p, TreeNode q) {
// réinitialiser les drapeaux pour chaque appel
pFound = faux;
qFound = faux;
Candidat TreeNode = dfs(root, p, q);
// retourner le candidat seulement si les deux nœuds ont été vus
retour (pFound && qFound) ? candidat : nul;
}

TreeNode dfs privé(TreeNode noeud, TreeNode p, TreeNode q) {
si (node == null) retourner null;

TreeNode gauche = dfs(node.left, p, q);
TreeNode droite = dfs(node.right, p, q);

si (noeud == p) { pFound = true; noeud de retour; }
si (noeud == q) { qFound = true; noeud de retour; }

si (gauche != null && droite != null) retourne le noeud; // les deux trouvés dans les sous-arbres
retour (à gauche != nul) ? gauche : droite; // un trouvé ou aucun trouvé
}

- Oui. Méthode 2 : compteur entier (facultatif)
// nombre d ' entrées privées = 0;
// public TreeNode le plus basCommonAncetorCounter(Rot TreeNode, TreeNode p, TreeNode q) {
// nombre = 0;
// Candidat TreeNode = dfsCounter(root, p, q);
// retour (compter) 2) ? candidat : nul;
// }
//
// TreeNode privé dfsCounter(TreeNode noeud, TreeNode p, TreeNode q) {
// si (node == null) retourner null;
// TreeNode gauche = dfsCounter(node.left, p, q);
// TreeNode droite = dfsCounter(node.right, p, q);
// si (noeud) : q) { count++; retour du noeud; }
// si (gauche != null && droite != null) retourne le noeud;
// retour (gauche != nul) ? gauche : droite;
// }
}
«» "

*Explication*
- Le DFS est post-commande : nous inspectons les enfants avant de décider du noeud actuel.
- `dfs` renvoie le noeud qui est soit `p`, `q`, ou la LCA d'entre eux dans le sous-arbre.
- Les drapeaux (`pFound`, `qFound`) ne sont définis que lorsque le nœud exact est assorti.
- Oui. Après la traversée complète, nous ne retournons le candidat que si les deux drapeaux sont "vrais".

---

- Oui. 5. Mise en œuvre de Python

'`python
# Définition d'un noeud d'arbre binaire.
classe TreeNode:
def __init__(self, val=0, gauche=Aucun, droite=Aucun):
autoval = val
auto.gauche = gauche
soi.right = droit

Solution de classe:
def le plus basAncêtre commun (soi, racine: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode Aucune:
Deux drapeaux booléens
self.p_found = Faux
Self.q_found = Faux

candidat = self._dfs(root, p, q)
retourner candidat si soi-même. p_found et moi-même. q_trouvé autre Aucune

def _dfs(self, noeud: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode Aucune:
si ce n'est pas le nœud:
retour Aucune

gauche = self._dfs(node.left, p, q)
droite = self._dfs(node.right, p, q)

si le noeud est p:
self.p_found = Vrai
noeud de retour
si le noeud est q:
self.q_found = Vrai
noeud de retour

Si gauche et droite: # les deux nœuds trouvés plus profondément
noeud de retour
retour gauche ou droite # un côté trouvé ou aucun
«» "

*Conseils pour Python*
- Utilisez `is` pour comparer les objets de noeud, pas `==`, parce que les valeurs de noeud sont uniques, mais nous devons confirmer l'identité.
- Oui. La solution fonctionne dans un seul DFS; pas de second passage de vie est nécessaire.

---

- Oui. 6. Mise en œuvre C++

'`cpp
*** Définition d'un noeud d'arbre binaire. **/
struct TreeNode {
la valeur intérieure;
TreeNode *gauche;
TreeNode *right;
TreeNode(int x) : val(x), gauche(nullptr), droite(nullptr) {}
};

solution de classe {
bool pFound, qFound; // deux drapeaux booléens

TreeNode* dfs(Nœud TreeNode*, TreeNode* p, TreeNode* q) {
si (!node) retourner nulptr;

TreeNode* gauche = dfs(node->gauche, p, q);
TreeNode* droite = dfs(node->right, p, q);

si (noeud == p) { pFound = true; noeud de retour; }
si (noeud == q) { qFound = true; noeud de retour; }

si (gauche && droite) retourne le noeud; // les deux trouvés dans les sous-arbres
Retour à gauche ? gauche : droite; // un ou aucun
}

public:
TreeNode* le plus basAncêtre commun(racine TreeNode*, TreeNode* p, TreeNode* q) {
pFound = qFound = faux;
TreeNode* candidat = dfs(root, p, q);
retour (pFound && qFound) ? candidat : nulptr;
}
};
«» "

Le code C++ est presque identique à Java – les seules différences sont la syntaxe et l'utilisation de pointeurs bruts.

---

- Oui. 6. Analyse de complexité (toutes langues confondues)

Opération Temps Espace
- C'est quoi ?
(chaque noeud visité une fois)
Autres Mises à jour du drapeau: constante par noeud: constante par noeud:
Total des dépenses

---

- Oui. 7. Cas de bord et pièges communs

Qu'est-ce qu'il faut faire attention
C'est ce que j'ai dit.
**Root est "null"**. Autres
** `p` ou `q` est le même que la racine**. Autres
**Deep skewed tree**= profondeur de récursion `H` peut atteindre `104`; dans les langues avec une pile limitée, vous pouvez avoir besoin d'une solution itérative. Autres
**Utiliser l'état global mutable**= Oublier de réinitialiser les drapeaux entre les cas de test → mauvaise réponse. Autres
Autres **Comparer par valeur au lieu de l'identité**= Dans LeetCode, les nœuds sont des objets distincts; comparer `node.val == p.val` peut donner de faux positifs si l'arbre a des valeurs dupliquées (non autorisées ici mais bonnes pratiques). Autres

---

- Oui. 8.

Aspect du bien
- C'est quoi ?
**Bon**) • Pass unique DFS avec propagation claire des drapeaux. <br>• Code minimal, temps O(N). <br>• Fonctionne pour *any* forme d'arbre binaire.
Si vous collez la solution 236 ('if(root==p="root==q)return root;`) vous manquerez la vérification d'existence. <br>• Une sortie précoce au milieu d'un DFS peut renvoyer une mauvaise ACV si un noeud manque. <br>• Utiliser `==` sur les valeurs des nœuds au lieu de l'identité des nœuds. Autres
**Ugly**) • Traitement du cas où un seul des nœuds est présent (par exemple, `p` est l'ancêtre de `q`, mais `q` est absent). Le DFS ci-dessus retourne automatiquement `null` dans ce scénario, donc aucun passage supplémentaire n'est nécessaire. <br>• Essayer d'utiliser une pile itérative tout en maintenant deux drapeaux peut devenir verbeux et sujet à erreur. Autres

---

- Oui. 9. Comment utiliser ceci pour une entrevue d'emploi

1. ** Expliquez la différence avec 236** – montrez que vous comprenez la nuance.
2. **Parcourez le DFS** – soulignez comment vous propagez les drapeaux.
3. **Afficher la manipulation des cas** – Si un noeud manque, retourner null.
4. ** Temps/espace** – les intervieweurs aiment voir O-notation.
5. **Optionnel: fournir l'implémentation contre-basée** – démontre que vous connaissez plusieurs idiomes.

---

10. Ensemble de codes complets

Ci-dessous vous trouverez les trois solutions complètes que vous pouvez coller dans l'éditeur LeetCode ou votre propre dépôt.

Langue
C'est quoi, ça ?
*Java** Autres
**Python**
*C++**

---

#### 10.1 Java (`Solution.java`)

"Java
classe TreeNode {
la valeur intérieure;
TreeNode gauche, droite;
TreeNode(int x) { val = x; }
}

solution de classe publique {
le pound booléen privé;
Booléen privé qFound;

public TreeNode le plus basCommonAncêtre(racine TreeNode, TreeNode p, TreeNode q) {
pFound = faux; qFound = faux;
Candidat TreeNode = dfs(root, p, q);
retour (pFound && qFound) ? candidat : nul;
}

TreeNode dfs privé(TreeNode noeud, TreeNode p, TreeNode q) {
si (node == null) retourner null;
TreeNode gauche = dfs(node.left, p, q);
TreeNode droite = dfs(node.right, p, q);

si (noeud == p) { pFound = true; noeud de retour; }
si (noeud == q) { qFound = true; noeud de retour; }

si (gauche != null && droite != null) retourne le noeud;
retour (à gauche != nul) ? gauche : droite;
}
}
«» "

#### 10.2 Python (`solution.py`)

'`python
classe TreeNode:
def __init__(self, val=0, gauche=Aucun, droite=Aucun):
autoval = val
auto.gauche = gauche
soi.right = droit

Solution de classe:
def le plus basAncêtre commun (soi, racine, p, q):
self.p_found = Faux
Self.q_found = Faux
candidat = self._dfs(root, p, q)
retourner candidat si soi-même. p_found et moi-même. q_trouvé autre Aucune

def _dfs(self, node, p, q):
si non noeud: retour Aucun
gauche = self._dfs(node.left, p, q)
droite = self._dfs(node.right, p, q)

si le noeud est p : soi-même. p_found = Vrai; noeud de retour
si le noeud est q: soi. q_found = Vrai; noeud de retour

si gauche et droite: noeud de retour
retour gauche ou droite
«» "

#### 10.3 C++ (`solution.cpp`)

'`cpp
*** Définition d'un noeud d'arbre binaire. **/
struct TreeNode {
la valeur intérieure;
TreeNode *gauche;
TreeNode *right;
TreeNode(int x) : val(x), gauche(nullptr), droite(nullptr) {}
};

solution de classe {
bool pound, qFound;

TreeNode* dfs(Nœud TreeNode*, TreeNode* p, TreeNode* q) {
si (!node) retourner nulptr;

TreeNode* gauche = dfs(node->gauche, p, q);
TreeNode* droite = dfs(node->right, p, q);

si (noeud == p) { pFound = true; noeud de retour; }
si (noeud == q) { qFound = true; noeud de retour; }

si (gauche & & & droite) retour noeud; // LCA trouvé
Retour à gauche ? gauche : à droite; //
}

public:
TreeNode* le plus basAncêtre commun(racine TreeNode*, TreeNode* p, TreeNode* q) {
pFound = qFound = faux;
TreeNode* cand = dfs(root, p, q);
retour (pFound && qFound) ? cand : nulptr;
}
};
«» "

---

## 11. Billet de blog – Lowest Ancêtre commun d'un arbre binaire II: bon, mauvais, laide (et pourquoi il est une grande question d'entrevue)

> ** Mots-clés du référencement**: LeetCode 1644, Ancêtre commun le plus bas, Arbre binaire, Interview de travail, Interview de codage, Structures de données, Récursion, Counter, Flag, O(N) Solution, Arbre de recherche binaire, DFS, BFS, Algorithme Thinking

---

### 11.1 Introduction

Si vous vous préparez à une interview d'ingénierie logicielle, vous rencontrerez rapidement des problèmes *=Lowest Common Ancêtre (LCA)=*. La variante classique –*trouver la LCA dans un arbre de recherche binaire* – est commune, mais *LeetCode 1644* pousse l'enveloppe en demandant la LCA **dans un arbre binaire**, et **seulement si les deux nœuds existent**. C'est le mélange parfait de la maîtrise de la structure des données, de la pensée récursive et de la manipulation des caisses.

Ce post marche à travers ce qui rend le problème, les pièges qui le font, et le scénario nuancé, qui peut vous faire monter. Nous terminerons avec une liste de contrôle pratique pour répondre à cela dans une entrevue, afin que vous puissiez entrer dans la prochaine salle d'entrevue confiant.

---

### 11.2 Le "Bien" – Pourquoi un seul passage DFS est élégant

1. **Simplicité**
Un seul DFS qui porte deux drapeaux booléens (`pFound`, `qFound`) est tout ce dont vous avez besoin.
Pas de boucles supplémentaires ou de structures de données complexes.

2. **Temps optimal**
Chaque nœud est visité une fois → **O(N)**.
Les intervieweurs aiment voir une preuve linéaire dans la section *analyse*.

3. **Uniform pour tous les arbres**
Travaille pour des arbres équilibrés, biaisés ou dégénérés.
La profondeur de récursion est la hauteur de l'arbre ('H'), donnant **O(H)** espace.

4. **Boîtes de bord Interne**
Que les nœuds cibles soient les mêmes que la racine, qu'il en manque un ou qu'il s'agisse d'un ancêtre, les drapeaux décident automatiquement si nous devons retourner `null` ou la LCA réelle.

---

### 11.3 Le "Bad" – Erreurs courantes (et comment les éviter)

Pourquoi ça arrive ?
- Oui.
En supposant que 1644 est identique à 236.
Autres Sortie anticipée à mi-DFS. Ne sortez pas tôt; propagez des drapeaux vers le haut
Autres Oublier de réinitialiser les drapeaux.
En utilisant l'égalité de valeur (`==`) au lieu de l'identité.

---

#### 11.4 Le "Ugly" – Le cas d'un nœud manquant

> ** Scénario**: `p` est l'ancêtre de `q`, mais `q` n'existe pas réellement dans l'arbre.
>
> Quoi ? **
> Si vous implémentez naïvement le flag-DFS à simple passe, vous pourriez penser qu'il retournera toujours le bon LCA. Mais il reviendra `null` parce que `qFound` reste `faux`. C'est *exactement* le comportement attendu pour ce problème. La «ugline» vient de solutions plus anciennes qui font une approche *deux-pass* : d'abord trouver la LCA, puis un BFS/DFS séparé pour confirmer l'existence des deux nœuds. Cette traversée supplémentaire peut rendre la solution plus difficile à raisonner et sujette aux bugs.

**Pourquoi le drapeau-DFS gagne* *
Les drapeaux `pFound` et `qFound` sont *propagés* jusqu'à la pile de récursion. Si un nœud n'apparaît jamais, le drapeau correspondant reste "faux". Par conséquent, le dernier `si (pFound && qFound)' vous assure de retourner `null` si le second noeud est manquant. Pas de boucles supplémentaires, pas de comptabilité désordonnée, juste une traversée propre.

---

#### 11.5 Entretien Talk-Track

1. **Commencez avec la définition du problème** – soulignez que nous traitons avec *objets*, pas seulement des valeurs entières.
2. ** Expliquez la différence avec le classique LCA (BST)** – la variante BST exploite la commande, mais 1644 nécessite une solution structurelle pure.
3. ** Dessiner l'arbre de récursion DFS** sur le tableau blanc. Marquez où se trouvent les drapeaux et comment ils se déplacent.
4. **Afficher le pseudocode** (similaire au code Java) et pointer les deux lignes clés : `if(node == p) { pFound = true; renvoyez le noeud; }`.
5. **Discuss ledge-case**: Si `root=p`, nous devons encore confirmer `q` est dans le sous-arbre. Les drapeaux résolvent ça automatiquement.
6. **Mention la solution optionnelle contre-basée** – Au lieu de booléens, j'aurais pu utiliser un compteur entier. Tous les deux sont idiomatiques; je choisirai celui que préfère l'intervieweur. (en milliers de dollars)
7. ** Temps et espace** – écrivez rapidement le grand O formules.
8. **Wrap up** – 1644 est une grande question d'entrevue parce qu'il teste la compréhension de la récursion, drapeaux, la manipulation des cas de bord, et la complexité algorithmique dans un seul problème. (en milliers de dollars)

---

11.6 Pensées finales

- *LeetCode 1644* est plus qu'un puzzle de codage ; c'est un micro-examen de la façon dont vous traitez les contraintes qui changent un problème classique.
- Maîtrisez le DFS monopass avec des drapeaux; vous serez prêt pour les juges en ligne et les entrevues en personne.
- Gardez votre code propre, annotez vos pensées, et soyez prêt à répondre à des questions de suivi comme : Ou peut-on résoudre ça de façon itérative ? (en milliers de dollars)

---

À emporter

Que vous résolviez cela sur un tableau blanc ou un ordinateur portable, rappelez-vous: ** comprendre le problème en profondeur** (le "good"), **éviter les pièges** (le "bad") et ** gérer les cas les plus délicats** (le "gugly") est ce qui distingue les meilleurs interprètes. LeetCode 1644 est un exemple quintessence de ce chemin.

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---

*Sentez libre de marquer ce message et de le partager avec votre groupe d'étude de codage. Si vous l'avez trouvé utile, déposez un commentaire ou une étoile sur le dépôt ! *

---

> **Auteur**: *Votre nom* – *Data-Structures Enthousiaste, Ingénieur Logiciel, Coach Interview*
> **Date**: *2024-07-12*
> **Commentaires**: *Ouvert pour discussion! *

---

Cette analyse complète l'explication, le code et l'entrevue pour **LeetCode 1644 – Ancêtre commun le plus bas d'un arbre binaire II**. Joyeux entretien !