---
titre: LeetCode 431. Encoder l'arbre N-ary à l'arbre binaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Encoder un arbre N‐ary à un arbre Binary (Code Leet431) – Code + Interview‐ Prêt Blog

> **TL;DR**
> • Convertir un arbre N‐ary → arbre binaire en utilisant l'astuce *left‐child right‐sibling*.
> • Décoder en traversant les frères et sœurs de gauche→droite.
> • temps O(N), pile de récursion O(H) (= 1000).
> • Implantation propre et apatride – parfaite pour une interview LeetCode.

---

- Oui. 1. Le problème (LeetCode 431)

Compte tenu d'un arbre naturel** (chaque noeud peut avoir n'importe quel nombre d'enfants), vous devez :

Étape Objectif
- Oui.
**Encoder**=Convertissez-le en un arbre **binaire** afin que la structure puisse être stockée ou transmise. Autres
**Décode**= Reconstruire l'arbre N-ary original à partir de la représentation binaire. Autres

> **Constraints**
> * `0 <= noeud.val <= 104`
> * `0 <= nombre de nœuds <= 104`
Hauteur ≤ 1000
> * **Pas d'état global/statique** – l'encodeur/décodeur doit être apatride.

La solution classique est la cartographie *left‐child right‐sibling* :

* L'enfant **left** d'un noeud binaire est le **premier enfant** du noeud N‐ary correspondant.
* L'enfant droit** d'un noeud binaire est le prochain frère** de cet enfant.

Cette représentation est sans perte : vous pouvez toujours revenir à l'arbre N-ary.

---

- Oui. 2. Pourquoi ce blog?
Les intervieweurs aiment les problèmes qui testent les conversions de la structure des données** et votre capacité à penser aux traversées d'arbres** de manière non triviale.
Ce post vous donne:

* ** Code de travail** dans **Java, Python et C++** – copice-paste ready.
* Une explication claire et conviviale** que vous pouvez mentionner dans une lettre d'accompagnement ou un portfolio.
* Une ventilation des aspects **good**, **bad** et **ugly** – afin de pouvoir parler de compromis lors d'une entrevue.

---

- Oui. 3. L'algorithme central

«» "
encode(root):
si root est null : retourner null
binaire = nouveau TreeNode(root.val)
Si racine. enfants non vides:
binaire.left = encode(root.children[0]) // premier enfant
cur = binaire. gauche
pour i de 1 à root.children. taille 1: // frères et sœurs
cur.right = encode(root.children[i])
cur = cur.right
retour binaire

décodage(racine):
si root est null : retourner null
nary = nouveau nœud(root.val, [])
cur = racine.gauche
alors que cur != NULL: // Traverser les frères et sœurs
nary.children.append(decode(cur))
cur = cur.right
retour
«» "

* **Heure**: Chaque noeud est visité une fois → **O(N)**.
* **Espace**: profondeur de la cheminée de récursion ≤ hauteur de l'arbre (= 1000).
* **Apatride**: Pas de variables globales; tous les états vivent dans la pile d'appel.

---

- Oui. 4. Code (Copier-Paste Ready)

#### 4.1 Java

"Java
// Définition pour un nœud d'arbre N-ary.
Numéro de classe {
Int val public;
liste publique <Node> des enfants;

Nœud public {}
Nœud public (int _val) { val = _val; }
Noeud public(int _val, liste <Noeud> _enfants) {
val = _val;
enfants = _enfants;
}
}

// Définition pour un nœud binaire.
classe TreeNode {
la valeur intérieure;
TreeNode gauche, droite;
TreeNode(int x) { val = x; }
}

Codec {

// Encoder un arbre N-ary à un arbre binaire.
encode public TreeNode(Node root) {
si (root) null retourne null;

TreeNode binaire = nouveau TreeNode(root.val);

si (root.children != null && !root.children.isEmpty() {
binaire.left = encode(root.children.get(0)); // premier enfant
TreeNode cur = binaire. gauche;
pour (int i = 1; i < root.children.size(); i++) { // frères et sœurs
cur.right = encode(root.children.get(i));
cur = cur.right;
}
}
retour binaire;
}

// Décoder un arbre binaire vers un arbre N-ary.
publique Décoder le nœud (racine TreeNode) {
si (root) null retourne null;

Node nary = nouveau Node(root.val, nouvelle ArrayList<>();
TreeNode cur = root.left;
pendant que (cur != null) { // traverser des frères et sœurs
nary.children.add(decode(cur));
cur = cur.right;
}
de retour;
}
}
«» "

4.2 Python

'`python
# Définition pour un nœud d'arbre N-ary.
Numéro de classe:
def __init_(self, val=None, children=None):
autoval = val
enfants = enfants ou []

# Définition d'un noeud d'arbre binaire.
classe TreeNode:
def __init__(self, val=0, gauche=Aucun, droite=Aucun):
autoval = val
auto.gauche = gauche
soi.right = droit

classe Codec:
# Encode un arbre N-ary à un arbre binaire.
def encode(self, root: 'Node') -> «TreeNode»:
si ce n'est pas la racine:
retour Aucune

noeud = TreeNode(root.val)
Si racine. enfants:
node.left = self.encode(root.children[0]) # premier enfant
cur = noeud. gauche
pour l'enfant en racine. enfants[1:]:
cur.right = self.encode(child) # frères et sœurs
cur = cur.right
noeud de retour

# Décode un arbre binaire à un arbre N-ary.
def décodage(self, root: 'TreeNode') -> 'Noeud':
si ce n'est pas la racine:
retour Aucune

nary = noeud(root.val, [])
cur = racine.gauche
alors que:
nary.children.append(self.decode(cur))
cur = cur.right
retour
«» "

### 4.3 C++

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

// Définition pour un nœud d'arbre N-ary.
Numéro de structure {
la valeur intérieure;
vecteur <Node*> les enfants;
Nœud() : val(0) {}
Node(int _val) : val(_val) {}
Noeud(int _val, vecteur <Noe*> _enfants)
: val(_val), children(_children) {}
};

// Définition pour un nœud binaire.
struct TreeNode {
la valeur intérieure;
TreeNode *left, *right;
TreeNode(int _val) : val(_val), gauche(nullptr), droite(nullptr) {}
};

Codec {
public:
// Encoder un arbre N-ary à un arbre binaire.
TreeNode* code(Node* root) {
si (!root) retourne nullptr;

TreeNode* noeud = nouveau TreeNode(root->val);
si (!root->children.vide()) {
node->left = encode(root->children[0]); // premier enfant
TreeNode* cur = noeud->gauche;
pour (size_t i = 1; i < root->children.size(); ++i) {
cur->right = encode(root->children[i]); // frères et sœurs
cur = cur->right;
}
}
noeud de retour;
}

// Décoder un arbre binaire vers un arbre N-ary.
Décoder le nœud*(racine TreeNode*) {
si (!root) retourne nullptr;

Node* nary = nouveau Node(root->val);
TreeNode* cur = racine->gauche;
pendant que (cur) {
nary->children.push_back(decode(cur));
cur = cur->right;
}
de retour;
}
};
«» "

> **Conseil** – Dans toutes les langues, n'oubliez jamais le garde `si (!root)`; sinon vous frapperez une erreur `NullPointerException`/`NoneType`.

---

- Oui. 5. Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**L'espace**= Pas de structures de données supplémentaires; seule la pile de récursion. La profondeur de récursion pourrait atteindre 1000 – sans danger en Java/Python mais veillez à ce que la pile déborde dans les arbres plus profonds. Autres
**Heure**=Linéaire, O(N). Aucun; l'algorithme est optimal.
**Simplicité**= Effacer la carte de gauche-enfant/de droite-sibling – facile à expliquer. La *liste d'enfants* est `null` ou vide → des contrôles supplémentaires `null`. Autres
Si vous changez par erreur `left`/`right` pendant le codage, le décodage échouera silencieusement. Autres
**Apatridie** Doit éviter les globals – peut être un piège pour les débutants. Aucun.
**Tests**=Tests faciles à effectuer par triage. Les harnais d'essai surcompliqués peuvent cacher des bogues. Autres

5.1 Gotchas communs

1. ** Liste nationale des enfants**
*Java* – `root.children` peut être `null`. Vérifiez `root.children != null` avant d'accéder.
*Python* – `enfants ou []` garantit qu'une liste est toujours présente.

2. **Mémoires en C++**
Chaque "nouveau" doit finalement être associé à "supprimer". Dans de vraies interviews, on vous demande habituellement de *ignorer* ceci, mais si vous construisez une bibliothèque, écrivez un destructeur ou utilisez des pointeurs intelligents.

3. ** Limites pour les piles à récursion**
*La limite de récursion par défaut est 1000. Si vous êtes malchanceux et que la hauteur de l'arbre est égale à cette limite, vous obtiendrez un `RecursionError`.
Java & C++ ont des piles plus grandes, mais il est toujours une bonne idée de tester avec une chaîne profonde d'enfants.

4. **Inversion gauche-enfant/droite-sibling**
L'échange de `gauche` et `droite` dans l'encodeur brisera le décodeur. Vérifiez toujours le diagramme de cartographie avant de le coder.

---

- Oui. 6. Comment faire fonctionner cette entrevue

1. **Cartographie**
Dessinez un petit nœud N‐ary avec 3 enfants → arbre binaire. Affichez le diagramme de gauche à droite de l'enfant.
Les aides visuelles gagnent des points.

2. **Exposer la récursion**
*Encoder* – *Premier enfant → gauche, frères et sœurs → chaîne de droits. (en milliers de dollars)
*Décoder* – à gauche, puis à droite jusqu'à "nullptr". (en milliers de dollars)

3. **Time & Space** – Mention O(N) et O(H) pile, et rassurer que H ≤ 1000.

4. **Délibérations**
* Arbre vide.
* Noeud sans enfants.
* Arbres larges contre arbres profonds.

5. Questions**
* Vous préférez une implémentation itérative pour éviter la récursion ? (en milliers de dollars)
* Comment géreriez-vous un arbre avec 105 nœuds ? (en milliers de dollars)

Montrer que vous pouvez anticiper des compromis démontre une profonde compréhension structurelle – exactement ce que les intervieweurs recherchent.

---

- Oui. 6. Bonus – Harnais d'essai rapide (Python)

'`python
def tree_to_list(root) :
si ce n'est pas root: retourner Néant
retourner [root.val] + [tree_to_list(child) pour enfant dans la racine. enfants]

Codec = Codec()

♪ Exemple d'arbre N-ary:
# 1
Numéro /
# 2 3 4
- Oui.
# 5
racine = Node(1, [Node(2), Node(3, [Node(5)]), Node(4)]
binaire = codec.encode(root)
décodé = codec.decode(binaire)

affermissez arbore_to_list(root) == arbore_to_list(décodé)
print("Round-trip réussi!")
«» "

Exécutez l'extrait ci-dessus dans un nouvel interprète Python pour voir l'algorithme en action.

---

- Oui. 7. Dernier départ

> **"La représentation de droite de l'enfant de gauche transforme un arbre de degré arbitraire en un arbre binaire sans perdre aucune structure, et c'est aussi simple qu'un seul passage récursif." * *

Vous avez maintenant :

* ** Solutions multi-langues vérifiées** que vous pouvez coller dans n'importe quelle plateforme de codage.
* Une réponse d'entrevue structurée** expliquant les compromis entre *bon*, *mauvais* et *peu*.
* **Mots clés** prêt pour votre curriculum vitæ: *Encoder N‐ary Tree à Binary Tree*, *LeetCode 431*, *tree conversion*, *data-structure interview*, *left‐child right-sibling*, *O(N) algorithme*.

Soyez confiant que vous impressionnerez votre prochain gestionnaire d'embauche avec le code et la stratégie. Bon codage ! (en milliers de dollars)