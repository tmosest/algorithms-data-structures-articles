---
Titre: LeetCode 510. Successeur d'ordre dans BST II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Récapitulation du problème – LeetCode 510: Succès de l'ordre dans BST II

> **Donné d'un nœud dans un arbre de recherche binaire, retourner le successeur en ordre de ce nœud dans la TVB. **
> Un successeur de nœuds en ordre est le nœud avec la plus petite clé qui est plus grande que la valeur donnée de nœuds.
> Les noeuds de l'arbre ont un pointeur `parent` – vous êtes **not** vu la racine de l'arbre.

**Exemples**

Arbre
C'est quoi ?
[2,1,3]
[5,3,6,2,4,null,null,1]

**Contrôles* *

- `1 ≤ n ≤ 104`
- `-105 ≤ Nodeval ≤ 105 "
- Toutes les valeurs sont uniques

---

Stratégie de haut niveau

1. **Le sous-arbre existe ? **
Si le noeud a un enfant droit, le successeur est le noeud le plus gauche de ce sous-arbre droit.

2. **Pas de sous-arbre droit**
Déplacez l'arbre via le pointeur parent jusqu'à ce que vous trouviez un ancêtre qui est un enfant **gauche** de son parent.
Cet ancêtre est le successeur. Si vous atteignez la racine sans trouver un tel ancêtre, le noeud n'a pas de successeur.

Les deux étapes sont `O(h)` où `h` est la hauteur de l'arbre, et utiliser `O(1)` espace supplémentaire.

---

Mise en œuvre

Voici des solutions propres et prêtes à la production dans **Java, Python et C++**.
Les trois utilisent le même algorithme itératif et gèrent gracieusement l'affaire `null`-successeur.

---

### Java

"Java
***
* Définition pour un noeud d'arbre binaire avec pointeur parent.
*/
Numéro de classe {
la valeur intérieure;
Noeud gauche, droit, parent;
Noeud(int x) { valeur = x; }
}

solution de classe publique {

***
* Renvoie le successeur en ordre du noeud donné dans une TVB.
*
* @param noeud le noeud dont le successeur est à trouver
* @return le noeud successeur, ou nul s'il n'existe pas
*/
publique Numéro d'ordreSuccès(Node) {
si (node == null) retourner null;

/* 1. Le nœud a le sous-arbre droit – allez à son enfant le plus à gauche. */
si (node.right != null) {
Noeud succ = noeud.right;
pendant que (succ.left != null) {
succ = succ.left;
}
retour succ;
}

/* 2. Pas de sous-arbre droit – monter par les parents. */
parent nœud = parent noeud;
Noeud cur = noeud;
pendant que (parent != null && cur == parent.right) {
cur = parent;
parent = parent.parent;
}
retour du parent; // peut être nul
}
}
«» "

** Harnais d'essai**

"Java
public statique vide principal(String[] args) {
// Construire un arbre [2,1,3]
racine du nœud = nouveau nœud(2);
root.left = nouveau nœud(1);
root.right = nouveau nœud(3);
root.left.parent = racine;
root.right.parent = racine;

Solution s = nouvelle solution();
System.out.println(s.inorderSuccèsor(root.left).val); // 2
}
«» "

---

Python

'`python
Numéro de classe:
def __init_(self, val):
autoval = val
self.left = self.right = self.parent = Aucune

Solution de classe:
dans l'ordre Successeur(self, noeud: noeud) -> Numéro:
"""
Retourner le successeur en ordre de « noeud » dans une TVB.
"""
en cas de nœud. à droite :
succ = noeud.droit
tandis que succ.left:
succ = succ. gauche
retour succ

Pas de sous-arbre droit – monter par les parents
parent = noeud.parent
cur = noeud
pendant que parent et cur == parent. à droite :
cur = parent
parent = parent.parent
retour parent # peut être Aucun
«» "

**Utilisation simple* *

'`python
racine = noeud(2)
root.left = noeud(1)
root.right = noeud(3)
racine.left.parent = racine
root.right.parent = racine

sol = Solution()
print(sol.inorderSuccesseur(root.left).val) # 2
«» "

---

C++

'`cpp
#incluez <iostream>

/* Définition de nœud pour une TVB avec pointeur parent */
Numéro de structure {
la valeur intérieure;
Nœud gauche, droite, parent;
Node(int x) : val(x), gauche(nullptr), droite(nullptr), parent(nullptr) {}
};

solution de classe {
public:
Noeud* dans l'ordreSuccèseur(noeud*) {
si (!node) retourner nulptr;

/* Cas 1 : le sous-arbre droit existe */
si (noeud->droit) {
Noeud* succ = noeud->droit;
pendant que (succ->à gauche)
succ = succ->gauche;
retour succ;
}

/* Cas 2: pas de sous-arbre droit – monter jusqu'à ce que le nœud soit un enfant gauche */
Noeud* parent = noeud->parent;
Noeud* cur = noeud;
pendant que (parent && cur == parent->right) {
cur = parent;
parent = parent->parent;
}
retour du parent; // peut être nulptr
}
};
«» "

**Démarrage**

'`cpp
Int main() {
Noeud* racine = nouveau Noeud(2);
root->left = nouveau nœud(1);
root->right = nouveau nœud(3);
racine->gauche->parent = racine;
root->right->parent = root;

Solution s;
Noeud* succ = s.inorderSuccèseur(root->left);
si (succ) std::tout << succ->val << '\n'; // estampes 2
autre point::tout << "Pas de successeur\n";
}
«» "

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Sous-arbre droit traversant Autres
Escalade par les parents Autres
**Total**** Autres

`h` est la hauteur de la TVB.

---

Les bons, les mauvais et les affreux

Aspect du bien
- C'est quoi ?
**Simplicité de l'algorithme**
Autres **Utilisation de l'espace Toujours besoin de liens parent.
**Utilisation du temps**=Linéaire en hauteur=Le pire cas `O(n)` pour l'arbre biaisé== Aucune=
**Causes d ' évasion** Aucun
**Défi de suivi**= Résolvé par parent traversant== Impossible d'utiliser les valeurs== Aucune Autres

**A emporter**: Le pointeur parent est l'arme secrète; il transforme une autre recherche "O(n)" en marche "O(h)".

---

Conseils pour l'entrevue

1. ** Expliquez les deux cas** – le sous-arbre droit vs grimper.
2. **Mentionner le pointeur parent** – c'est pourquoi le suivi (pas de recherche de valeur) est trivial.
3. **Time/Space** – mettre en évidence le temps "O(h)", espace "O(1)".
4. **Manipulation d'Edge** – si le nœud est l'élément maximum, retourner `null`.
5. **Testez votre solution** avec des arbres équilibrés et biaisés.

---

Bonus – Suivi : sans regarder n'importe quel nœud

Lorsque vous êtes seulement autorisé à inspecter les pointeurs de nœuds (pas leurs valeurs), le même algorithme fonctionne parce que:

- Oui. Vous ne comparez jamais les valeurs – vous naviguez seulement `gauche`, `droite` et `parent`.
- Le successeur est toujours le **premier ancêtre** qui est un **enfant gauche** de son parent (ou le nœud le plus gauche du sous-arbre droit).

Ainsi, la solution itérative ci-dessus est déjà optimale pour le suivi.

---

Référencement et emploi

- **Titre**: Mastering LeetCode 510: Successeur en ordre dans BST II – Java, Python, C++ Solutions & Interview Insights
- **Description détaillée**: Obtenez la réponse pour LeetCode 510. Apprenez l'algorithme successeur en ordre, voyez le code Java, Python et C++ propre, et asez votre interview de structures de données.
- **Mots clés**: LeetCode 510, Successeur d'ordre dans BST II, successeur de BST, arbre de recherche binaire, pointeur parent, question d'entrevue, solution Java, solution Python, solution C++, O(h) temps, O(1) espace, interview d'algorithme, prép. d'entrevue technique.

> ** Prêt à impressionner les recruteurs?** Déposez cet article dans vos messages portfolio ou LinkedIn, et regardez les intervieweurs remarquer votre compréhension profonde des BST et de la logique des pointeurs.

Bon codage et bonne chance pour la prochaine interview! C'est ce qu'il a dit