---
titre: LeetCode 2641. Cousines en Arbre Binaire II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2641 – *Cousines dans l'arbre binaire II*
**Langues:** C++
**Complexité temporelle:** O(N)
**Complexité spatiale:** O(H) (seulement la file d'attente pour le niveau actuel)

---

Récapitulation des problèmes

Étant donné la racine d'un arbre binaire, remplacer la valeur de chaque noeud par la somme de toutes ses valeurs cousines.
Deux nœuds sont *cousins* s'ils sont à la même profondeur et ont des parents différents.
La racine n'a pas de cousins, donc sa nouvelle valeur est 0.

---

No ### --Idée de la solution – Niveau par niveau

1. **Root → 0** – La racine ne change jamais.
2. Pour chaque niveau *sauf* la racine:
* Calculer **`sumchildren`** = somme de tous les enfants des nœuds dans le niveau actuel.
* Pour chaque noeud du niveau
`curChildrenSum` = somme de ce noeud ses propres enfants.
Puis chaque enfant= nouvelle valeur = `sumEnfants – curEnfantsSum` (tous les cousins au niveau suivant).
Poussez les enfants dans la file d'attente pour la prochaine itération.
3. Arrêtez quand il n'y a plus de nœuds à traiter.

L'algorithme ne garde que les nœuds du niveau courant en mémoire – O(H) espace supplémentaire.

---

## 2-

> *Les trois implémentations sont entièrement compatibles avec la définition de LeetCodes `TreeNode`. *

---

Java

"Java
***
* Définition d'un noeud d'arbre binaire.
* classe publique TreeNode {
* Int val;
* TreeNode gauche;
* TreeNode droit;
* TreeNode(int val) { this.val = val; }
* TreeNode(int val, TreeNode gauche, TreeNode droite) {
* ce.val = valeur;
* ce.gauche = gauche;
* ce droit = droit;
*}
*}
*/
solution de classe {
publique TreeNode remplacer ValeurInTree(TreeNode root) {
si (root) null retourne null;

root.val = 0; // root n'a pas de cousins
Queue<TreeNode> file d'attente = nouvelle liste liée<>();
file d'attente.offre(root);

pendant que (!queue.isEmpty()) {
taille int = file d'attente.size();
Liste <TreeNode> curLevel = nouvelle liste d'array<>(taille);
Int sumEnfants = 0;

// recueillir tous les nœuds au niveau actuel et calculer la somme de leurs enfants
pour (int i = 0; i < taille; ++i) {
noeud TreeNode = file d'attente.poll();
curLevel.add(node);
si (node.left != nul) sommeEnfants += node.left.val;
si (node.right != null) sommeEnfants += node.right.val;
}

// Mettre à jour les valeurs pour les enfants
pour (Node Tree : CurLevel) {
Int propre Enfants Somme = 0;
si (node.left != null) propreEnfantsSum += node.left.val;
si (node.right != null) propreEnfantsSum += node.right.val;

si (node.left != null) {
node.left.val = sommeEnfants - propresEnfantsSum;
file d'attente.offre(node.left);
}
si (node.right != null) {
node.right.val = sommeEnfants - propresEnfantsSum;
file d'attente.offre(node.right);
}
}
}
retour de racine;
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

Solution de classe:
def remplacer Valeur Arbre(même, racine: TreeNode) -> Numéro d'arbre:
si ce n'est pas la racine:
retour Aucune

root.val = 0 # root n'a pas de cousins
à partir de collections import deque
q = deque([root])

alors que q:
nive_size = len(q)
Nœuds de niveau = []
somme_enfants = 0

# recueillir les nœuds du niveau actuel et la somme de tous les enfants
pour _ dans l'intervalle(level_size):
noeud = q.popleft()
niveau_nodes.append(node)
en cas de nœud. gauche:
somme_enfants += noeud.left.val
en cas de nœud. à droite :
somme_enfants += noeud.right.val

# Mettre à jour les valeurs pour les enfants
pour noeud dans le_noeud de niveau:
_somme propre = 0
en cas de nœud. gauche:
own_sum += noeud.left.val
en cas de nœud. à droite :
own_sum += noeud.right.val

en cas de nœud. gauche:
noeud.left.val = somme_enfants _somme propre
q.Append(node.left)
en cas de nœud. à droite :
node.right.val = somme_enfants _somme propre
q.annexe(node.right)

retour de racine
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
* TreeNode(int x, TreeNode *l, TreeNode *r) : val(x), gauche(l), droite(r) {}
* };
*/
solution de classe {
public:
TreeNode* remplacerValueInTree(TreeNode* racine) {
si (!root) retourne nullptr;

racine->val = 0; // racine n'a pas de cousins
std::queue<TreeNode*> q;
q.push(root);

pendant que (!q.vide()) {
int sz = q.size();
md::vecteur <TreeNode*> cur;
cur.reserve(sz);
long long montantEnfants = 0; // utiliser long pour éviter le débordement

// collecter les nœuds de niveau courant et la somme de tous leurs enfants
pour (int i = 0; i < sz; ++i) {
TreeNode* noeud = q.front(); q.pop();
cur.push_back(node);
si (noeud->gauche) sommeEnfants += node->gauche->val;
si (node->right) sommeEnfants += node->right->val;
}

// Mettre à jour les valeurs pour les enfants
pour (nœud TreeNode : cur) {
longue et longue Somme = 0;
si (noeud->gauche) possèdeSum += noeud->gauche->val;
si (noeud->droit) possèdeSum += noeud->droit->val;

si (noeud->à gauche) {
node->left->val = static_cast<int>(sumEnfants - propresSum);
q.push(node->gauche);
}
si (noeud->droit) {
node->right->val = static_cast<int>(sumEnfants - propresSum);
q.push(node->right);
}
}
}
retour de racine;
}
};
«» "

---

Article du blog – *Cousins dans l'arbre binaire II : Des bogues à Brilliance (Code Leet 2641)*

> **Mots clés du référencement:**
> - *Cousines dans l'arbre binaire II*
> - *Code de débit 2641*
> - *replacer la valeur dans l'arbre*
> - * cousins d'arbres binaires*
> - *arbre binaire d'entretien d'emploi*
> - *question d'entrevue sur l'algorithme*
> - *arbre binaire BFS*

---

# Cousines in Binary Tree II – Un entretien-emploi Guide prêt

Pourquoi ce problème se pose

> LeetCode 2641 est une question qui apparaît sur de nombreux entretiens de structure de données.
> La résoudre démontre la maîtrise de :
> - traversée par ordre de niveau (BFS)
> - comptabilité des sommes à chaque profondeur
> - la manipulation des cas de bord (enfants « null », nœuds mono-enfants)

Les recruteurs diront : Nous sommes impressionnés par votre intuition transversale.

---

Le problème est redressé (avec un twist)

> Avec un arbre binaire, remplacez chaque valeur de nœuds par la somme ** de ses cousins**.
> La racine est toujours réglée à 0 car elle n'a pas de cousins.

> **Exemple**
> `` "
> Entrée: 1
/ \
> 2 3
- / / \
Autres
> Produit : 0
/ \
> 2 3
- / / \
> 0 0 0
> `` "
> (Ici, les cousins sont 5 et 6 → 5 + 6 = 11, donc la nouvelle valeur est 11.)

---

Étape par étape

1. **Root → 0**
La racine ne participe jamais aux calculs des cousins, alors nous le mettons immédiatement.

2. **BFS Loop**
Pour chaque niveau (sauf la racine), nous:
- **Collect** tous les nœuds au niveau actuel (`niveau actuel`).
- **Sum tous les enfants** de ces nœuds → `total Un enfant.
- **Pour chaque nœud**:
* `ownChildSum` = somme de ses propres enfants.
* Chaque enfant a une nouvelle valeur = `total ChildSum – propre ChildSum '.

3. **Quée pour le niveau suivant**
Nous poussons les enfants mis à jour dans la file d'attente afin que la prochaine itération fonctionne sur la prochaine profondeur.

4. **Termination**
Lorsque la file d'attente est vide, l'arbre entier a été traité.

---

Analyse de la complexité

Mesure Calcul Résultat
- C'est quoi ?
**Temps**= Chaque noeud est visité une fois; travail constant par noeud
**L'espace **La file d'attente tient au plus un niveau des nœuds (==H)

---

Pièges communs

Pourquoi ça compte ?
- Oui.
**Utilisation de «node.left.val» avant qu'il ne soit mis à jour** , Dans la conversion initiale des JS, les valeurs enfant ont été écrasées *avant* le parent , "curSum" a été calculé, corrompant la somme pour le niveau suivant. Calculer la somme des enfants **D'abord** des valeurs originales, puis mettre à jour les enfants dans un deuxième passage. Autres
**Sur les grands arbres, les valeurs du nœud peuvent être allant jusqu'à `10^5`; ajouter de nombreux enfants peut dépasser la plage de 32 bits. Utilisez `long long` (C++) ou `int` avec des contraintes minutieuses (Java/Python le manipulent bien). Autres
Autres **Vérifications nucléaires omises** quand il "null" ça fait exception. Autres Garder chaque enfant (`si (node.left != null) { ... }`). Autres
**Queue mauvais usage** Seulement enquêter sur les enfants existants. Autres

---

## -

- **Énoncer clairement l'invariant** – Tous les nœuds du niveau actuel partagent le même "totalChildSum".
- **Afficher les maths** – Nouvelle valeur = `total ChildSum – propre ChildSum '.
- ** Expliquez pourquoi root est 0** – il s'agit d'un boîtier d'angle qui élimine une branche spéciale dans la boucle.
- **Mention l'échange temps/espace** – BFS utilise O(H) espace supplémentaire par rapport à un DFS récursif qui utilise O(H) pile plus O(N) profondeur de récursion.

---

Poste de blog (optimisé par le référencement)

```markdown
# Cousines dans l'arbre binaire II (Code Leet 2641) – Remplacer la valeur dans l'arbre

Table des matières
1. Aperçu du problème
2. Résumé de la solution
3. Mise en œuvre Java
4. Mise en œuvre de Python
5. Mise en œuvre C++
6. Analyse de la complexité
7. Erreurs communes et comment éviter Eux
8. Pourquoi vous allez gâcher cela dans votre prochain entretien de codage

Aperçu du problème
Cousins en Binary Tree II est une question classique de LeetCode qui teste votre capacité à traverser un arbre binaire **niveau par niveau**, calculer des valeurs agrégées et mettre à jour les nœuds enfant sans perturber les relations parent-enfant. Le but est de remplacer chaque valeur de nœuds par la somme de toutes ses valeurs de cousins.

> ** Termes clés**
> - *Cousines* : Même profondeur, parents différents
> - *Replacer la valeur dans l'arbre* : L'opération que vous implémentez

Résumé de la solution
- Définir la valeur racine à **0** (pas de cousins).
- Pour chaque niveau, calculer la somme de ** tous les enfants**.
- Pour chaque nœud de ce niveau, soustraire la somme de ce nœud ** propres** enfants du total.
- Mettre à jour la valeur de chaque enfant à cette différence et la pousser à la file d'attente pour le niveau suivant.

Cette stratégie **BFS** fonctionne en temps linéaire **O(N)** et utilise uniquement **O(H)** espace auxiliaire.

Mise en œuvre Java
"Java
solution de classe {
publique TreeNode remplacer ValeurInTree(TreeNode root) {
si (root) null retourne null;
root.val = 0;
Demande <TreeNode> q = nouvelle liste liée<>();
q.offre(root);
alors que (!q.isEmpty()) {
taille int = q.size();
Liste du niveau <TreeNode> = nouvelle liste de répartition<>();
Int sumEnfants = 0;
pour (int i = 0; i < taille; i++) {
Node d'arbre = q.poll();
niveau.add(node);
si (node.left != nul) sommeEnfants += node.left.val;
si (node.right != null) sommeEnfants += node.right.val;
}
pour (Node Tree : niveau) {
Int propre Somme = 0;
si (node.left != null) possèdeSum += node.left.val;
si (node.right != null) possèdeSum += node.right.val;
si (node.left != null) {
node.left.val = sommeEnfants - propresSum;
q.offre(node.left);
}
si (node.right != null) {
node.right.val = sommeEnfants - propresSum;
q.offre(node.right);
}
}
}
retour de racine;
}
}
«» "

Mise en œuvre de Python
'`python
Solution de classe:
def remplacer Valeur Arbre(même, racine: TreeNode) -> Numéro d'arbre:
si ce n'est pas la racine:
retour Aucune
racine.val = 0
à partir de collections import deque
q = deque([root])
alors que q:
sz = len(q)
niveau = []
somme_enfants = 0
pour _ dans l'intervalle(sz):
noeud = q.popleft()
niveau.annexe(node)
si node.left: sum_children += node.left.val
si noeud.right: somme_enfants += noeud.right.val
pour le noeud en niveau:
propre = 0
si noeud.left: propre += noeud.left.val
si noeud.right: propre += noeud.right.val
en cas de nœud. gauche:
node.left.val = somme_enfants - propre
q.Append(node.left)
en cas de nœud. à droite :
node.right.val = somme_enfants - propre
q.annexe(node.right)
retour de racine
«» "

Mise en œuvre du C++
'`cpp
solution de classe {
public:
TreeNode* remplacerValueInTree(TreeNode* racine) {
si (!root) retourne nullptr;
racine->val = 0;
la file d'attente <TreeNode*> q;
q.push(root);
pendant que (!q.vide()) {
int sz = q.size();
vecteur <TreeNode*> niveau;
long terme Enfants = 0;
pour (int i = 0; i < sz; ++i) {
TreeNode* noeud = q.front(); q.pop();
niveau.push_back(node);
si (noeud->gauche) sommeEnfants += node->gauche->val;
si (node->right) sommeEnfants += node->right->val;
}
pour (nœud TreeNode* : niveau) {
longue et longue Somme = 0;
si (noeud->gauche) possèdeSum += noeud->gauche->val;
si (noeud->droit) possèdeSum += noeud->droit->val;
si (noeud->à gauche) {
node->left->val = static_cast<int>(sumEnfants - propresSum);
q.push(node->gauche);
}
si (noeud->droit) {
node->right->val = static_cast<int>(sumEnfants - propresSum);
q.push(node->right);
}
}
}
retour de racine;
}
};
«» "

Analyse de la complexité
**Complexité**
- Oui.
Temps **O(N)**= Chaque noeud est visité une fois. Autres
Un seul niveau de nœuds vit dans la file d'attente à la fois. Autres

Erreurs communes et comment éviter Eux
- **Mettre à jour les enfants avant de calculer le "sumchildren"** – conduit à des totaux incorrects.
- **Déréférence du pointeur-Null** – toujours vérifier `si (node.left)' avant d'accéder à `.val`.
- **Overflow sur d'énormes arbres** – utilisez des entiers 64 bits dans des langues qui le soutiennent.

Pourquoi tu vas faire ça dans ton prochain entretien de codage
- Oui. Le problème mélange **breadth‐first search** avec **numérique de raisonnement** – un bon point pour les aficionados de la structure des données.
- Démontre que vous pouvez gérer **cases-cadres** comme des nœuds mono-enfant et des pointeurs nuls gracieusement.
- Montre que vous êtes à l'aise d'écrire propre, **O(H)** code BFS qui est facilement translatable entre Java, Python, et C++.

> **Retirez-vous** : maîtrisez ceci, et les recruteurs vous verront comme un gourou *tre-traversal prêt pour les défis algorithmiques les plus difficiles.

«» "

---

**Sentez libre d'adapter, de publier et de partager votre maîtrise des cousins dans Binary Tree II!**