---
titre: LeetCode 1973. Nombre de nœuds égaux à la somme des descendants -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 1973 – Nombre de nœuds égaux à la somme des descendants
**Objectif:** Renvoie le nombre de nœuds dans un arbre binaire dont la valeur égale la somme de toutes les valeurs dans son sous-arbre descendant.

> *Un descendant est n'importe quel noeud qui se trouve sur un chemin du noeud courant à une feuille.
> La somme des descendants pour une feuille est définie comme 0. *

La solution optimale fonctionne dans **O(n)** temps et **O(h)** espace, où *n* est le nombre de nœuds et *h* la hauteur de l'arbre (pile de récursion).

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.

---

#### 1.1 Java – DFS post-commande (récursif)

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
nombre d'int privés = 0;

int public egalToDescendants(racine de nœud d'arbre) {
dfs(racine);
le nombre de retours;
}

***
* Renvoie la somme de l'ensemble du sous-arbre enraciné au «node».
* En décompilant la récursion, nous comparons la valeur du noeud
* avec la somme de ses descendants (gauche + droite).
*/
Int privé dfs(nœud TreeNode) {
si (noeud == null) retourner 0;

Int gauche Somme = dfs (node.gauche);
Int droite Somme = dfs(node.right);
enfant Somme = gauche Somme + droite Somme;

si (node.val) nombre++;

// Somme de retour incluant ce noeud pour son parent.
retour node.val + enfantSum;
}
}
«» "

---

#### 1.2 Python – DFS post-commande (récursif)

'`python
# Définition d'un noeud d'arbre binaire.
# classe TreeNode:
# def __init_(self, val=0, gauche=Aucune, droite=Aucune):
# Self.val = val
Moi-même. gauche = gauche
Moi-même. droite = droite

Solution de classe:
def égal ToDescendants(soi, racine: TreeNode) -> Int:
total = 0

def dfs(node: TreeNode) -> Int:
si ce n'est pas le nœud:
retour 0
gauche = dfs(node.gauche)
droite = dfs(node.right)
child_sum = gauche + droite
if node.val == child_sum:
nombre d ' individus 1
retour node.val + enfant_sum

dfs(racine)
Revenez vous-même. Nombre
«» "

---

### 1.3 C++ – DFS post-commande (récursif)

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
nombre int = 0;

int egalToDescendants(racine TreeNode*) {
dfs(racine);
le nombre de retours;
}

particulier:
int dfs(nœud TreeNode*) {
si (!node) retour 0;
int gauche = dfs(node->gauche);
Int droite = dfs(node->right);
int child_sum = gauche + droite;
si (noeud->val) == child_sum) ++count;
retour du noeud->val + enfant_sum;
}
};
«» "

---

- Oui. 2. Article du blog – Le bon, le mauvais et l'acharnement de compter des nœuds égaux à la somme des descendants

Titre
**Mastering LeetCode 1973 : Les nœuds du comte sont égaux à la somme des descendants – Une plongée profonde dans les bons, mauvais et mauvais modèles* *

Description de la méta
Apprenez à résoudre le LeetCode 1973 en Java, Python et C++ avec une approche DFS propre après commande. Découvrez les meilleures pratiques, les pièges communs et les conseils prêts à l'entrevue qui impressionneront les recruteurs.

Mots clés
LeetCode 1973, Numéro de compte égal à somme des descendants, Binary Tree DFS, Post-order Traversal, Java LeetCode, Python LeetCode, C++ LeetCode, Tree Traversal, Question d'entrevue, Entretien technique, Ingénieur Backend

---

Introduction

Les problèmes d'arbre binaire sont le pain-et-beurre des entrevues de codage.
LeetCode **1973 – Compte Nodes Equal to Sum of Descendants** est un excellent exemple : il vous force à combiner un arbre classique avec un contrôle arithmétique subtil.

Dans ce billet, nous allons:
1. Briser le problème en trois parties – *Le Bon*, *Le Mauvais* et *Le Méchant*.
2. Fournir une solution prête à la production en **Java**, **Python** et **C++**.
3. Discutez des cas de bord, de la profondeur de récursion, et pourquoi ce modèle est un must-savoir pour tout ingénieur de backend.

---

C'est vrai. Le Bon – Un Elégant DFS post-commande

Aspect Pourquoi c'est bon
C'est quoi, ça ?
**Post-order traversal**= Garanties que nous connaissons les sommes descendantes *avant* évaluant le nœud actuel. Autres
**Simple pass**= O(n) temps – chaque noeud visité une fois. Autres
**Linear empile space**=O(h) space – la profondeur de récursion est égale à la hauteur de l'arbre, bien meilleure que BFS=O(n). Autres
**Readable & maintainable**=La séparation claire de la somme de calcul et de l'égalité de contrôle. Autres
Autres **Pas d'effets secondaires au niveau mondial**= L'utilisation d'un champ de classe/d'instance ('count') maintient l'aide pure. Autres

> **Insight clé**
> Si `sum(left) + sum(right) == node.val`, incrémentez le compteur.
> Retour `node.val + sum(left) + sum(right)` vers les nœuds parent.

Ce modèle est réutilisable pour de nombreux problèmes d'agrégat de sous-arbre (somme, moyenne, hauteur, etc.).

---

C'est vrai. Les mauvaises – pièges communs

Conséquences
- C'est quoi ?
**Utiliser des variables globales** . Essai difficile à unit-test, risque d'état d'impasse sur les appels. Enregistrer l'état dans un champ de classe ou retourner un tuple. Autres
**Brute-force BFS/DFS**. Recalculer les sommes de zéro pour chaque nœud → O(n2). Calculez une fois dans un laissez-passer post-commande. Autres
** Pile itérative avec suivi manuel de la somme** Préférez la récursion à moins que la hauteur de l'arbre n'excède 105 (risque de débordement de la pile). Autres
**Ignorer la définition du nœud foliaire** Traiter la somme descendante de la feuille comme 0. Autres
**Débordement entier**= Valeurs allant jusqu'à 105, mais la somme de nombreux nœuds pourrait dépasser `int`.= Utiliser `long` en Java/C++ ou Python=s entiers illimités. Autres

---

C'est pas vrai. L'Ugly – Solutions inefficaces ou incorrectes

1. **Récursion naïve (O(n2))* *
"Java
nombre int = 0;
(nœud TreeNode) { ... } // O(n)
(nœud TreeNode) {
si (noeud == nul) retour;
somme int = sommeDescendants(noeud);
si (node.val == somme) count++;
traversée (node.gauche);
la traversée (node.right);
}
«» "
- Pourquoi ? Chaque noeud déclenche une somme entière du sous-arbre, conduisant au temps quadratique.

2. ** Utilisant une `HashMap` pour stocker des sommes de sous-arbre* *
"Java
Carte<TreeNode, Integer> mémo = nouveau HashMap<>();
Int getSum (noeud TreeNode) {
si (noeud == null) retourner 0;
retour memo.computeIfAbsent(node, n -> n.val + getSum(n.left) + getSum(n.right));
}
«» "
- Pourquoi ? Ajoute de l'espace et de la complexité; pas nécessaire pour ce problème.

3. **DFS itérative avec une pile et deux passes* *
- Première passe pour pousser les nœuds.
- Deuxième passe à pop et calcul des sommes.
- Pourquoi ? Double travail et code fragile.

Évitez ces tendances à moins que l'entrevue ne demande une solution de rechange (p. ex., PDD ascendant, arbres segmentés).

---

C'est vrai. Cas de bord et robustesse

Scénario Quoi faire ?
C'est ce que j'ai dit.
**Empty tree (`root == null`)** Autres
**Arbre fortement déséquilibré**=Hauteur n → la récursion peut déborder. Utilisez une pile explicite ou `recursion de la queue` (rarement autorisée). Autres
**Grandes sommes descendantes**= Débordement potentiel en int 32 bits.= Utiliser `long` (Java/C++) ou Python's int.==
Autres **Tous les nœuds sont égaux à 0**. Chaque correspondance non-feuille parce que la somme descendante est 0. Autres

L'essai avec ces boîtiers de bord garantit une présentation à l'épreuve des balles.

---

#### 6=1 Interview-Ready Points de discussion

1. **Déclarer l'approche d'abord** – -Il fera un DFS post-commande parce que j'ai besoin des sommes descendantes avant de pouvoir vérifier l'égalité. (en milliers de dollars)
2. **Exposer la complexité** – Une passe, O(n) temps, O(h) pile. (en milliers de dollars)
3. **Mention Overflow** – Toutes les valeurs d'entrée sont ≤ 105, mais la somme peut dépasser 32-bit; je vais utiliser "long".
4. **Afficher le code** – Fournir un extrait propre dans la langue de votre choix.
5. **Facultatif – Discuter d'une base de données Brute-Force** – Si nous devions forcer, nous finirions avec O(n2), ce qui est peu pratique. (en milliers de dollars)
6. **Demander des Variations** – Et si nous voulions retourner les nœuds réels au lieu d'un compte ? – mène à un petit refacteur.

---

Conclusion

LeetCode 1973 n'est pas seulement un test de récursion ; c'est un micro-cours sur l'agrégation efficace des arbres**.
La solution DFS de post-commande est la norme or:
* espace simple, linéaire, logique claire. *

Évitez les mauvais et laids modèles, parce que les recruteurs sont à la recherche d'un code propre, *ami-interview* qui balance.

---

Liste de contrôle à emporter

- [ ] Utilisez **post-order DFS** pour les agrégats de sous-arbres.
- [ ] Conserver les compteurs dans un champ de classe/d'instance; éviter les statiques globales.
- [ ] Traiter les feuilles comme ayant une somme de 0 descendant.
- [ ] Garder contre le débordement (`long` / `Biginteger`).
- [ ] Poignez l'arbre vide comme un boîtier de base.
- [ ] Soyez prêt à expliquer la profondeur de récursion et l'utilisation de la pile.

Maîtriser ces principes vous donnera une base solide pour **entretiens d'ingénierie backend** où la logique arborescente est commune.

---

- Oui. Réflexions finales

Les arbres binaires sont partout – de l'analyse des arbres d'expression dans les compilateurs à l'organisation d'une structure de répertoire dans les systèmes de fichiers.
Le modèle que nous avons démontré aujourd'hui va faire surface dans beaucoup d'autres problèmes: Sum de sous-arbre gauche, Sum de chemin maximal, Sum de plus grande taille dans un arbre binaire, etc.

Donc la prochaine fois que vous voyez un problème d'arbre LeetCode, pensez :

> *Computer une fois → stocker une fois → se propager vers le haut. *

Bonne codification et bonne chance pour impressionner votre prochain recruteur!