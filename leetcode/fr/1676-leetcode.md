---
titre: LeetCode 1676. Ancêtre commun le plus bas d'un arbre binaire IV -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – Trois langues

Vous trouverez ci-dessous une solution **pass simple, O(N) temps / O(H) espace**
Code du leet 1676 – *Lowest Common Ancêtre d'un arbre binaire IV*.
Le code est écrit en **Java, Python et C++** afin que vous puissiez le coller dans le
les juges en ligne correspondants ou vos propres projets.

> **Pourquoi cette version? * *
> * Utilise un `HashSet` (ou `unordered_set`) pour les tests d'adhésion O(1).
> * Compte récursivement combien de nœuds cibles apparaissent dans chaque sous-arbre.
> * Le premier noeud qui contient tous les nœuds cibles dans son sous-arbre est le LCA.
> * Pas de structures de données supplémentaires (en dehors de l'ensemble) – frais généraux minimes.

---

### Java (style LeetCode)

"Java
// Définition pour un nœud binaire.
classe TreeNode {
la valeur intérieure;
TreeNode gauche;
TreeNode droit;
TreeNode(int x) { val = x; }
}

solution de classe {
TreeNode privé ans = nul;
Ensemble privé <TreeNode> cible Jeu;

public TreeNode le plus basCommonAncêtre(racine TreeNode, noeuds TreeNode[]) {
si (root) null retourne null;

cible Set = nouveau HashSet<>(Arrays.asList(nodes));
dfs(racine);
le retour des an;
}

// Renvoie le nombre de nœuds cibles trouvés dans ce sous-arbre
Int privé dfs(nœud TreeNode) {
si (noeud == null) retourner 0;

nombre int = 0;
si (cibleSet.contient(node)) count++;

nombre += dfs(node.left);
nombre += dfs(node.right);

// Si ce sous-arbre contient tous les nœuds cibles et que nous n'avons pas encore défini la réponse
si (compter) cibleSet.size() && ans == null) {
ans = noeud;
}
le nombre de retours;
}
}
«» "

---

Python 3

'`python
# Définition d'un noeud d'arbre binaire.
classe TreeNode:
def __init_(self, x):
autoval = x
auto.gauche = Aucune
soi.right = Aucune

Solution de classe:
def le plus basCommonAncêtre(même, racine: 'TreeNode', noeuds: list['TreeNode']) -> «TreeNode»:
si ce n'est pas la racine:
retour Aucune

cible_set = set(noeuds)
Self.ans = Aucune

def dfs(node: TreeNode) -> Int:
si ce n'est pas le nœud:
retour 0
count = 1 si le noeud est dans le_set cible 0
nombre += dfs(node.left)
nombre += dfs(node.right)

if count == len(target_set) et self. n'est pas:
self.ans = noeud
Nombre de retours

dfs(racine)
Revenez vous-même. ans
«» "

---

### C++ (GNU‐C++17)

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
TreeNode* le plus basAncêtre commun(racine TreeNode*, vecteur<TreeNode*>et noeuds) {
si (!root) retourne nullptr;
unordered_set<TreeNode*> cible(nodes.begin(), nodes.end());
as = nullptr;
dfs(root, cible);
le retour des an;
}

particulier:
TreeNode* ans = nulptr;

// renvoie le nombre de nœuds cibles trouvés dans ce sous-arbre
int dfs(nœud TreeNode*, ensemble_non classé<nœud Treenode*> et cible) {
si (!node) retour 0;

int cnt = cible.count(node) ? 1 : 0;
cnt += dfs(node->gauche, cible);
cnt += dfs(node->right, cible);

si (cnt == cible.size() && !ans) ans = noeud;
retour cnt;
}
};
«» "

---

- Oui. 2. Article du blog – *Les bons, les mauvais, et les odieux de la LCA (Nœuds multiples)*

Titre
**Lowest Ancêtre commun de plusieurs nœuds dans un arbre binaire – Une plongée profonde pour les entrevues* *

### Méta-Description
Débloquez la solution LeetCode 1676 : découvrez le meilleur algorithme, comparez les implémentations Java/Python/C++, et maîtrisez l'interview. Parfait pour les ingénieurs logiciels qui préparent des questions sur la structure des données.

---

- Oui. 1. Présentation

Lorsque vous pensez à *Lowest Common Ancêtre* (LCA) dans les arbres binaires, le problème d'interview classique est *deux* nœuds. LeetCode 1676 lance une torsion : **avec un tableau de nœuds, trouvez la LCA de tous**.
Cela semble trivial, mais les solutions naïves que vous voyez sur Internet ignorent souvent les cas de coin, font exploser la mémoire, ou manquent la garantie *O(N)*.

Dans cet article, nous allons passer par:

**Ce que vous allez apprendre**
- Oui.
Autres Bon Le O(N) algorithme qui fonctionne pour n'importe quel nombre de nœuds
Mauvais Pourquoi l'approche de recherche de chaque paire échoue
Des pièges cachés : profondeur de récursion, identité contre valeur, et fuites de mémoire

---

- Oui. 2. Rétablissement des problèmes

> **Input** –
> * `root` – pointeur/référence à la racine d'un arbre binaire (les valeurs sont uniques).
> * `nodes[]` – un tableau d'objets **TreeNode** qui existent tous dans l'arbre.
>
> **Output** – le TreeNode qui est l'ancêtre commun le plus bas de *chaque* noeud dans `nodes[]`.

> **Constraints**
> * 1 ≤ N ≤ 104 (nombre de nœuds dans l'arbre).
> * Toutes les valeurs des nœuds sont uniques.
> * Tous les nœuds dans `nodes[]` sont distincts et présents dans l'arbre.

---

- Oui. 3. Approches naïves (les mauvais)

La complexité Pourquoi ça pose problème
- C'est quoi ?
**Pairwise LCA** – Calculer LCA pour chaque paire, puis fusionner. Autres
**Mark & Sweep** – DFS chaque noeud cible, stocker les ancêtres, intersecter. Autres
**Brute DFS avec Set à chaque nœud** – Pour chaque nœud, collectez toutes les cibles dans son sous-arbre. Autres

Ces modèles sont courants dans les solutions de premier projet que vous verrez dans les blogs ou les forums de discussion. Ils travaillent pour de petites données mais échouent sur les contraintes.

---

- Oui. 4. Stratégie optimale (le bien)

4.1 Idées fondamentales

Lors d'une seule traversée en profondeur, nous gardons une trace de **Combien de nœuds cibles** apparaissent dans le sous-arbre actuel.
* Si un sous-arbre contient des cibles *all*, alors le noeud actuel est le LCA.
* Nous renvoyons le compte au parent pour que l'ancêtre sache si son sous-arbre est un candidat.

Cela nous donne :

* **Heure** – Chaque nœud est visité une fois → **O(N)**
* **Espace** – Profondeur de la cheminée de récursion → **O(H)** où H est la hauteur de l'arbre

4.2 Détails de la mise en œuvre

Langue Remarques spéciales
C'est pas vrai.
Utiliser un `HashSet<TreeNode>` pour les vérifications O(1) `contient()`. Gardez un champ mutable `ans` qui stocke le premier noeud qui satisfait à la condition de comptage. Autres
**Python**= Utiliser un `set(nodes)`; la récursion renvoie un nombre entier. Utilisez `nonlocal ans` ou un attribut de classe. Autres
**C++**="unordered_set<TreeNode*> target(nodes.begin(), nodes.end());` Recursion retourne le nombre. Magasinez `ans` en tant que membre privé. Autres

Pourquoi ça marche ?

Laisser `k = noeuds.longueur`.
Lorsque nous visitons un noeud `x`, nous comptons combien de cibles `k` sont dans ses sous-arbres gauche et droit, puis ajouter 1 si `x` elle-même est une cible.
* Si la somme est égale à `k`, alors chaque cible se trouve dans le sous-arbre enraciné à `x`.
* Parce que nous traversons des feuilles vers le haut, le **premier** tel nœud rencontré est le *plus bas*.
* Une fois que `ans` est réglé, nous propagons simplement le compte vers le haut; nous n'écraserons jamais `ans'.

---

- Oui. 5. Passage en code (exemple de Java)

"Java
privé TreeNode ans = null; // stocke le LCA une fois trouvé
set privé<TreeNode> cibleSet; // test d'adhésion rapide

public TreeNode le plus basCommonAncêtre(racine TreeNode, noeuds TreeNode[]) {
si (root) null retourne null;
cible Set = nouveau HashSet<>(Arrays.asList(nodes));
dfs(root); // pass unique DFS
le retour des an;
}

Int privé dfs(nœud TreeNode) {
si (noeud == null) retourner 0;
int count = cibleSet.contient(node) ? 1 : 0;
nombre += dfs(node.left);
nombre += dfs(node.right);

si (compter) cibleSet.size() && ans == null) {
ans = noeud; // premier noeud couvrant toutes les cibles
}
le nombre de retours;
}
«» "

* `dfs` renvoie le nombre de cibles trouvées dans le sous-arbre de `noeud`.
* Dès que `ans` est réglé, nous arrêtons de chercher un candidat plus profond.

---

- Oui. 6. Cas et pièges de bord

Problème Comment le repérer
- Oui.
Autres **Un seul noeud cible est le nœud lui-même. L'algorithme s'en occupe naturellement: `compte == 1`. Autres
**Identification du nœud par rapport à la valeur**= Deux nœuds peuvent avoir la même "val` mais sont des objets différents==Utilisez toujours l`identité de l`objet* (référence `TreeNode`) dans le jeu, et non la valeur entière. Autres
**Recursion profonde**= Hauteur de l'arbre près de N (104) → débordement de la pile sur Java/Python== Utiliser le DFS itératif ou augmenter la limite de récursion (`sys.setrecursionlimit`). Autres
**Fausse mémoire en C++**= Oublier de supprimer `unordered_set` local si vous l'attribuez à l'intérieur d'un helper==Allotissez-le une fois dans la méthode publique; l'helper le reçoit par référence. Autres
Autres **Le code Leet garantit `root != null`, mais les `dfs` locaux doivent toujours se protéger contre les enfants `null`. Autres

---

- Oui. 7. Prise d'entrevues Toujours

Question Réponse
C'est pas vrai.
*Quelle est la complexité temporelle de votre solution? * **O(N)** – une visite DFS par nœud. Autres
*Pourquoi avons-nous besoin d'un HashSet? *** **O(1)** tests d'adhésion; sans elle nous devrions faire O(N2). Autres
*Comment vous garantir de retourner l'ancêtre le plus bas? Le premier noeud dont le nombre de sous-arbres est égal à `k` est le plus bas parce que nous passons de feuilles en racines. Autres
*Et l'utilisation de l'espace? Seulement la pile de récursion – **O(H)**, pas O(N) sauf si l'arbre est dégénéré. Autres

---

- Oui. 7. Résumé

**Beau**
C'est quoi ?
Autres Un pass DFS, O(N) time, O(H) space.
Autres Utilise un `HashSet` pour l'adhésion à temps constant.

Avec les trois implémentations prêtes à être copiées ci-dessus, vous pouvez en toute confiance frapper le code de bord 1676 – Ancêtre commun le plus bas d'un arbre binaire IV.

---

- Oui. 8. Pensée finale

> ** Pratique, pratique, pratique. **
> Essayez d'écrire le DFS vous-même à partir de zéro dans chaque langue.
> Puis, changez l'arbre (ébranlé, équilibré, aléatoire) et exécutez les mêmes tests – vous verrez l'échelle linéaire qui compte.

Bon codage – et bonne chance pour votre prochaine entrevue!