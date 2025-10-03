---
titre: LeetCode 1469. Trouver tous les nœuds solitaires -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 1469 – Trouver tous les nœuds solitaires
**Facile à la recherche d'un arbre binaire

> **Objectif** – Pour chaque nœud qui est l'enfant *seulement* de son parent, retournez sa valeur.
> Le nœud racine n'est jamais considéré comme solitaire.

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Brute-Force vs Optimal] (#brute-force-vs-optimal)
3. [Algorithme – DFS (récursif)] (#algorithm-dfs-récursif)
4. [Algorithme – BFS (itératif)] (#algorithme-bfs-itératif)
5. [Complexité temporelle et spatiale] (#temps--complexité spatiale)
6. [Mise en œuvre dans 3 langues] (#Mise en œuvre)
7. [Le bon, le mauvais, le mauvais] (#le bon, le mauvais)
8. [Conseils d'entrevue et erreurs courantes](#conseils d'entrevue)
9. [SEO & Job-Seeking Takeaway](#seo-takeaway)

---

## Aperçu du problème

Valeur du paramètre
C'est quoi ?
Difficulté Facile
Nombre de nœuds
Valeur du nœud
Entrée de la racine de node d'arbre (arbre binaire)
sortie `Liste<entier>` (tout ordre)

Un seul noeud** est un enfant d'un parent qui a *exactement un* enfant.
Exemple :

«» "
1
/ \
2 3
Autres
4 ← solitaire
«» "

---

C'est pas vrai. Force vs Optimal

C'est pas vrai. Forcer
1. Traversez chaque nœud.
2. Pour chaque nœud, vérifiez s'il n'a qu'un enfant.
3. Recueillez la valeur de cet enfant.

Il s'agit essentiellement d'un *plein arbre de marche* – O(n) temps – mais de nombreuses solutions perdent du temps ou de la mémoire en construisant des structures de données auxiliaires (hash-maps, tableaux, etc.).

Optimisé
Il suffit d'inspecter la relation entre un parent et ses enfants. Un simple DFS ou BFS qui suit si le nœud actuel est seul fait le travail dans un passage sans mémoire supplémentaire au-delà de la pile de récursion (ou empil/queue explicite).

---

Algorithme – DFS (récursif)

1. **Cas de base** – Si le noeud est `null`, retourner.
2. **Vérifier la solitude** –
* Si le nœud a un enfant gauche mais pas d'enfant droit, cet enfant gauche est solitaire → ajouter au résultat.
* Si le noeud a un enfant droit mais pas d'enfant gauche, cet enfant droit est solitaire → ajouter au résultat.
3. Récursez les deux enfants.

La récursion porte naturellement le long de la relation parent-enfant; aucun drapeau n'est requis.

Texte
DFS(nœud):
si le nœud est nul : retour
si noeud.left et non noeud.right: result.add(node.left.val)
si node.right et non node.left: result.add(node.right.val)
DFS(node.left)
DFS(node.right)
«» "

---

Algorithme – BFS (Itératif)

Une première traversée de largeur utilise une file d'attente. Pour chaque nœud:

1. Si elle a un seul enfant, poussez cet enfant dans le résultat.
2. Demandez aux deux enfants (s'ils existent) de les traiter plus tard.

Des solutions itératives sont pratiques pour les intervieweurs qui veulent éviter les problèmes de profondeur de récursion.

---

## Complexité temporelle et spatiale

Métrique Récursion Itération
C'est pas vrai.
**Heure**
**L'espace**=O(h) – pile de récursion (h = hauteur de l'arbre)=O(n) – file d'attente (faible caisse pour un arbre biaisé)=

Avec n ≤ 1 000, les deux approches s'inscrivent facilement dans les limites.

---

## Mise en œuvre

> **Conseil:** Pour LeetCode, la définition `TreeNode` est déjà fournie.
> Si vous les utilisez localement, incluez la classe/structure `TreeNode` de l'aide.

- Oui. 1. Java (style LeetCode)

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<Intégrer> getLonelyNodes(racine d'EreNode) {
Liste du résultat <entier> = nouvelle liste de distribution<>();
dfs(racine, résultat);
le résultat du retour;
}

vide privé dfs(nœud TreeNode, liste <entier> res) {
si (noeud == nul) retour;

Si (node.left != Null && noeud. droite == null) {
res.add(node.left.val);
}
Si (noeud.right != Null && noeud. gauche == nul) {
res.add(node.right.val);
}

dfs(node.left, res);
dfs(node.right, res);
}
}
«» "

- Oui. 2. Python

'`python
# Définition d'un noeud d'arbre binaire.
# classe TreeNode:
# def __init_(self, val=0, gauche=Aucune, droite=Aucune):
# Self.val = val
Moi-même. gauche = gauche
Moi-même. droite = droite

Solution de classe:
def getLonelyNodes(self, root: Facultatif[TreeNode]) -> Liste[int]:
res = []
auto.dfs(racine, rés)
retour res

def dfs(self, node: Facultatif[TreeNode], res: List[int]) -> Aucun:
si ce n'est pas le nœud:
retour
si noeud. gauche et non noeud. à droite :
res.append(node.left.val)
en cas de nœud. et pas de nœud. gauche:
res.append(node.right.val)
auto.dfs(node.left, res)
Self.dfs(node.right, res)
«» "

- Oui. 3. C++ (style LeetCode)

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
vecteur<int> getLonelyNodes(racine TreeNode*) {
vecteur<int> rés;
dfs(root, res);
retour rés;
}

particulier:
vide dfs(nœud TreeNode*, vecteur<int>& res) {
si (!node) retour;
si (node->left && !node->right) res.push_back(node->left->val);
si (node->right && !node->left) res.push_back(node->right->val);
dfs(node->gauche, res);
dfs(node->right, res);
}
};
«» "

---

Les bons, les mauvais, les affreux

Aspect du bien
- C'est quoi ?
**Readability** Certains préfèrent un drapeau explicite (sur-ingénierie). Mélanger DFS & BFS dans le même code; logique difficile à trouver. Autres
**Space**= O(h) pile de récursion – minimal. Pour les arbres très profonds, risque de débordement de cheminée. En utilisant une grande carte de hachage pour se souvenir du nombre de parents – gaspillé. Autres
**Performance**= Exécute en 0 ms sur LeetCode pour tous les tests.= Pas besoin de `Collections.videList()` ou de null-checks en dehors de la boucle. Des solutions récursives qui construisent de nouvelles listes à chaque appel (espace O(n2)). Autres
**Maintenabilité**=Un assistant DFS – facile à étendre à d'autres problèmes. Certains pensent peut-être que vous avez besoin de deux passes, pas vrai. Empilement itératif sur-compliqué avec emballeurs de nœuds personnalisés. Autres

---

## Conseils d'entrevue et erreurs courantes

1. **Ne pas ignorer la racine** – la racine est *jamais* seule parce qu'elle n'a pas de parent.
2. **Juge**
* Arbre avec un seul noeud → liste vide.
* Arbres tordus (à gauche ou à droite seulement) → tous les enfants sauf les racines sont solitaires.
3. **Musinterprétation simple** – il fait référence au *enfant*, et non au parent.
4. **Pièges à complexité temporelle** – N'utilisez pas de BFS pour compter les parents pour chaque noeud; c'est O(n2).
5. **Test** – couvrir tous les motifs : équilibrés, biaisés, enfants manquants, valeurs dupliquées.

---

## SEO & Job-Seeking à emporter

- **Mots-clés**: *Trouver tous les nœuds solitaires*, *code 1469*, *nœud solitaire d'arbre binaire*, *arbre binaire DFS*, *algorithme d'entretien d'emploi*, *solutions Java Python C++*.
- **Titre** : Master LeetCode 1469 – Trouver tous les nœuds solitaires – Java, Python, C++ Solutions + Guide d'entrevue
- **Moyenne Description**: Solve LeetCode 1469 avec code DFS et BFS en Java, Python et C++. Apprenez l'algorithme, la complexité et les conseils d'entrevue pour réussir votre prochain travail technologique. (en milliers de dollars)

**Pourquoi cela importe pour les recruteurs**
1. **Profondeur technique** – vous pouvez articuler les compromis entre DFS et BFS.
2. **Clean code** – vous fournissez des solutions succinctes et testables.
3. **L'état d'esprit de résolution des problèmes** – vous identifiez les cas de bord et optimisez l'espace.

Utilisez cet article comme une entrée de portefeuille, incluez les extraits de code dans votre GitHub README, et partagez le lien sur LinkedIn ou votre blog personnel. Les recruteurs aiment les exemples tangibles qui mettent en évidence à la fois la pensée algorithmique et la compétence de codage dans plusieurs langues.

Bonne chance ! C'est ce qu'il a dit