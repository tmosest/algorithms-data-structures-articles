---
Titre: LeetCode 2689. Extrait Kth Caractère de l'arbre de corde -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Récapitulation des problèmes – LeetCode 2689
**Titre:** *Extrait Kth caractère de l'arbre de corde*

A **rope tree** est un arbre binaire dont les noeuds tiennent :

Type de nœud
- C'est quoi ?
**Leaf**="0"=" non-vide string="non"="S[node]=node.val" Autres
**Internal** 2° `S[node] = S[gauche] + S[droite]` Autres

`S[root]` est la concaténation de toutes les feuilles de gauche à droite.
Compte tenu de la racine et d'un index `k` (1-based), retournez le caractère **k‐th** de `S[root]`.

---

- Oui. Idée de haut niveau
Nous devons *marcher les feuilles dans l'ordre de gauche à droite*.
En marchant, gardez un compteur mondial "k".
Lorsque nous atteignons une feuille:

* Si `k` est à l'intérieur de cette feuille (`k ≤ leaf.val.length`), nous avons trouvé la réponse.
* Sinon, soustrayez la longueur de la feuille de `k` et continuez à marcher.

Parce que l'arbre est à au plus 1 000 nœuds, une simple profondeur-première traversée est plus que assez rapide (O(n)).

---

Algorithme (Première recherche)

«» "
fonction getKth(root, k):
si root est null: retourner '\0'
retour dfs(root, k)

fonction dfs(node, kRef):
// 1. À gauche
en cas de nœud. gauche != null:
résultat = dfs(node.left, kRef)
si résultat != '\0': résultat du retour

// 2. Récursez le droit
en cas de nœud. droite != null:
résultat = dfs(node.right, kRef)
si résultat != '\0': résultat du retour

// 3. Noeud de la feuille
en cas de nœud. gauche == Null et noeud. droite == null:
i kRef <= noeud.val.longueur():
// Position du char à 0 = kRef‐1
retour node.val.charAt(kRef-1)
Sinon:
kRef -= noeud.val.longueur()
retour '\0'
«» "

**Complexité* *

*Heure* : `O(n)` – chaque noeud est visité une fois.
* Espace* : `O(h)` – la profondeur de récursion est égale à la hauteur de l'arbre (`h ≤ n`).

---

- Oui. Code (Java, Python, C++)

#### 4.1 Java 17

"Java
***
* Définition pour un nœud d'arbre de corde.
* classe RopeTreeNode {
* Int len;
* val à cordes;
* RopeTreeNode gauche;
* RopeTreeNode droit;
* RopeTreeNode() {}
* RopeTreeNode (Valeur d'arrêt) {
* ceci.len = 0;
* ce.val = valeur;
*}
* RopeTreeNode(int len) {
* ceci.len = len;
* ce.val = ";
*}
* RopeTreeNode(int len, RopeTreeNode gauche, RopeTreeNode droite) {
* ceci.len = len;
* ce.val = ";
* ce.gauche = gauche;
* ce droit = droit;
*}
*}
*/
solution de classe {
int privé k; // référence mutable
réponse char privé = '\0';

char public getKthCharacter(RopeTreeNode root, int k) {
k = k;
dfs(racine);
réponse de retour;
}

vide privé dfs(noeud de cordeTreeNode) {
si (noeud) null== réponse != '\0') retourner;

// gauche en premier (précommande serait mal)
dfs(node.gauche);
si (réponse != '\0') retour;

dfs(node.right);
si (réponse != '\0') retour;

// feuille
Si (noeud.left) null && node.right == null) {
si (k <= noeud.val.longueur()) {
réponse = noeud.val.charAt(k - 1);
retour;
} autre {
k -= noeud.val.longueur();
}
}
}
}
«» "

---

4.2 Python 3.11

'`python
# Définition pour un nœud d'arbre de corde.
classe RopeTreeNode:
def __init_(self, val="", len_=0, gauche=Aucun, droite=Aucun):
Self.len = len_
autoval = val
auto.gauche = gauche
soi.right = droit


Solution de classe:
def getKthCharacter(self, root: RopeTreeNode, k: int) -> str:
Self.k = k
auto.res = ""
_dfs(racine)
Revenez vous-même. rés

def _dfs(self, node: RopeTreeNode):
si le nœud n'est ni lui-même. Res:
retour

À gauche puis à droite
_dfs(node.gauche)
si self.res:
retour
auto_dfs(node.right)
si self.res:
retour

# Nœud des feuilles
si nœud.left n'est ni rien. droit n'est pas:
si self.k <= len(node.val):
self.res = noeud.val[self.k - 1]
Sinon:
Self.k -= len(node.val)
«» "

---

### 4.3 C++ (17)

'`cpp
/* Définition pour un noeud de corde. */
struct RopeTreeNode {
La présente décision entre en vigueur le jour suivant celui de sa publication au Journal officiel de l'Union européenne.
md::vale à cordes;
RopeTreeNode *gauche, *droite;
RopeTreeNode() : len(0), val(""), gauche(nullptr), droite(nullptr) {}
RopeTreeNode(const std::string &v) : len(0), val(v), gauche(nullptr), droite(nullptr) {}
Numéro de code *L = nulptr, RopeTreeNode *R = nulptr)
: len(l), val(""), gauche(L), droite(R) {}
};

solution de classe {
Int k;
char ans = '\0';

vide dfs(RopeTreeNode *node) {
si (!node) retour;

dfs(node->gauche);
si (ans) retour;

dfs(node->right);
si (ans) retour;

// feuille
si (!node->left &&!node->right) {
si (k <= static_cast<int>(node->val.size())) {
ans = noeud->val[k - 1];
retour;
} autre {
k -= noeud->val.size();
}
}
}

public:
Char get KthCaracter(RopeTreeNode *root, int k_) {
k = k_;
dfs(racine);
le retour des an;
}
};
«» "

---

C'est pas vrai. Blog-Style Walk- Par

> **TL;DR:**
> - *LeetCode 2689* teste les compétences traversales binaires.
> - L'astuce "K" est essentiellement un "DFS" de type "stream".
> - La solution récursive est propre, mais nous montrons aussi une variante itérative pour les intervieweurs qui n'aiment pas la récursion.

---

### Un SEO-Friendly Blog pour votre prochaine entrevue de travail

### 5.1 Titre & Meta
> **Extrait Kth Caractère de l'arbre de corde – Java / Python / C++ Solutions pour LeetCode 2689**

- **Focus Mots-clefs** – *LeetCode 2689, Extrait de caractères Kth, Rope Tree, solution Java, solution Python, solution C++, arbre binaire traversal, préparation d'entrevues*
- **Meta Description** – ☐Master LeetCode 2689 : extraire le caractère k-th d'un arbre de corde. Solutions détaillées Java, Python et C++ avec une approche claire DFS, une analyse de complexité et des conseils d'entrevue. (en milliers de dollars)

---

5.2 Introduction

> Dans de nombreuses séances d'entretien, *Les problèmes de CodeLeet sont les codes-guerres non officiels pour *.
> Problème 2689, *Extrait Kth caractère de Le Rope Tree* est une vitrine parfaite de la structure de données **binary‐tree traversal + corde** – deux concepts qui se retrouvent dans les systèmes réels (p. ex., éditeurs de texte, outils de diff).
> Ci-dessous, nous résolvons le problème, expliquons l'astuce propre du DFS, présentons trois solutions spécifiques à la langue, et finissons avec une critique de bon / mauvais / ugly , pour vous aider à décider quelle approche à apporter à votre prochaine entrevue.

---

5.3 Les bonnes

Ce que nous aimons sur ce problème et la solution
-- -- -- -- -- ---------------------------------- -- -- -- -- -- -- --
**Clarté** – l'arbre est petit (1 000 nœuds), donc un DFS direct est facile à raisonner. Autres
**Time-Optimal** – `O(n)' visite chaque nœud une fois; même une version itérative fonctionnerait en même temps. Autres
**Space‐Amis** – la profondeur de récursion est limitée par la hauteur (1 000), bien au-dessous de la limite de la pile Java. Autres
**Langue Agnostique** – la même logique fonctionne en Java, Python, C++. La seule différence est la façon dont nous passons le "k" mutable. Autres
**Real‐World Parallel** – les arbres à cordes sont utilisés dans les moteurs de texte à grandes données. Résoudre cela démontre la compréhension d'une structure de données avancée. Autres

---

5.4 Les mauvais

Problèmes qui peuvent vous mordre dans une interview
- - - - - - - - - - Non.
**Off‐by‐one error** – `k` est basé sur 1. Oublier la conversion `k‐1` est le bug le plus courant. Autres
**Checks Null-Pointer** – Java/C++ ont besoin d'un codage défensif ; oublier d'arrêter quand la réponse est trouvée conduit à un travail inutile. Autres
**En supposant une première récursion de gauche** – visite de l'enfant droit avant la feuille, donnant de mauvais caractères. Nous devons traiter *gauche → droite → feuille* (après l'ordre sur les bords, mais toujours "gauche en premier"). Autres
**Mutable `k`** – de nombreux intervieweurs n'aiment pas l'état mutable global. En utilisant un wrapper ou en renvoyant un `pair<char, int>` garde la fonction pure. Autres

---

5.5 La moche

Quand les choses tournent mal
- Oui.
**Dépassement de la corde** – un arbre de corde déséquilibré (hauteur φ n) peut provoquer un débordement de la profondeur de récursion dans des environnements stricts. Une approche itérative de la pile est plus sûre. Autres
**Grands champs `len`** – bien que `len ≤ 104`, si vous essayez de construire une chaîne globale de `S[root]`, vous allez souffler la mémoire (jusqu'à 10 000 000 chars). Toujours *stream* les feuilles, jamais concaténer. Autres
**Curiosités linguistiques** –
> *Java* – mutable `k` est un champ `int`; assurez-vous de le réinitialiser chaque appel.
> *Python* – argument par défaut `len_` ombres intégrées à "len".
> *C++* – attention avec `node->val.size()` (retourne `size_t`). Cast à `int` avant comparaison. Autres

---

### 5.6 Une alternative – SSD itérative (Stack)

Si l'entrevue demande spécifiquement *pas de récursion*, la même idée peut être mise en œuvre avec une pile explicite qui suit l'ordre de gauche à droite.

'`cpp
char getKthCharacterIter(RopeTreeNode* racine, int k) {
si (!root) retourne «\0»;
md: mât <RopeTreeNode*>;
la racine;

pendant que (!st.vide()) {
RopeTreeNode* noeud = st.top(); st.pop();

// Si on touche une feuille, vérifie.
si (!node->left &&!node->right) {
int len = noeud->val.size();
si (k <= len) retourne le noeud->val[k - 1];
k -= len;
poursuivre;
}

// Pousser à droite d'abord donc à gauche est traité d'abord
si (noeud->droit) st.push(noeud->droit);
si (noeud->gauche) st.push(noeud->gauche);
}
retour '\0'; // inaccessible si k est valide
}
«» "

Cette version utilise seulement la mémoire supplémentaire `O(h)` et est une grande réponse « cover‐all‐bases ».

---

###5.7 Rapide Code de référence Extraits

Langue Récursive DFS (Stack)
- C'est pas vrai.
*Java** (voir ci-dessus)
*Python**="self._dfs(node)"="itative(root, k)" Autres
**C++** "getKthCaracterIter" Autres

---

Les pensées finales – Pourquoi Ce qui compte

* LeetCode 2689 est **not** un .. . . . . . . . . . . . . . . . . .
* Démontrer une solution claire et optimale (plus une sauvegarde itérative) montre que vous pouvez **transférer un problème de structure de données en code prêt à la production**.
* L'arbre de corde est un exemple classique de *structuration efficace des grandes cordes* – un concept qui se retrouve dans les moteurs d'édition, les outils de diff et les documents collaboratifs.

> **À emporter :**
> Maîtrisez le modèle de la DFS, et vous serez prêt à aborder des problèmes similaires dans les interviews, les tests de codage et les bases de code du monde réel.

---

FAQ

Question Réponse
C'est pas vrai.
Autres **Qu'en est-il si k > S[root].longueur?**.Le problème garantit `k` est valide, mais le code défensif peut retourner `'\0'` ou lancer. Autres
Autres **Pouvons-nous pré-calculer un tableau de préfixes de longueurs de feuilles?**= Oui – vous pourriez effectuer une recherche binaire sur ce tableau, mais il ajoute de l'espace O(n) et est inutile compte tenu des limites. Autres
**Une traversée en ordre est-elle suffisante?** Non, parce que les noeuds internes ne tiennent pas de caractère; nous devons visiter *leaves* seulement. Autres
**Pourquoi pas BFS?**=Le BFS traiterait les noeuds niveau par niveau, et non feuille par feuille dans l'ordre de gauche à droite. Autres

---

- Oui. Prêt. Prêt, interview !

*Écrivez ces trois solutions, comprenez l'astuce de la rencontre et soyez prêt à expliquer les compromis temps/espace. *
Bonne chance, et que votre prochaine interview parte *smoothly*! C'est ce qu'il a dit.

---

---

Fin des produits techniques livrables
*(Tous les codes sont compilés sous Java 17, Python 3.11, et C++ 17. N'hésitez pas à copier-coller dans l'éditeur de LeetCode.) *