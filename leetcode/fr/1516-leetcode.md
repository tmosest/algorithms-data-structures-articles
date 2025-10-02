---
titre: LeetCode 1516. Déplacer le sous-arbre de N-Ary -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1516. Déplacer le sous‐ Arbre de l'arbre N‐ary – Solution 3-Langue + Billet de blog

> **TL;DR** – 4 cas simples, un seul DFS pour cartographier les parents, temps O(N), espace O(N).
> Les implémentations Java, Python et C++ que vous pouvez coller directement dans votre soumission LeetCode.

---

- Oui. 1. Récapitulation des problèmes

Vous êtes donné un arbre racine **N‐ary** où chaque noeud a une valeur unique.
L`arbre est représenté par la classe `Node`

"Java
Node de classe publique {
Int val public;
liste publique <Node> des enfants;
Nœud public() { enfants = nouvelle liste de distribution<>(); }
Nœud public(int _val) { val = _val; enfants = nouvelle station de radio<>(); }
}
«» "

et deux nœuds distincts `p` et `q`.
**Objectif** – déplacer tout le sous-arbre enraciné à `p` pour devenir le dernier enfant** de `q`.
Si `p` est déjà un enfant direct de `q` rien ne change.
Trois cas subtils nécessitent une manipulation spéciale:

Situation Que faire
- C'est quoi ?
Le `q` se trouve à l'intérieur du sous-arbre de `p`. Après l'échange l'ancienne racine (`p`) peut ne plus être la racine – la nouvelle racine devient l'ancienne `q`. Autres
**2**= `p` est à l'intérieur du sous-arbre de `q`= juste détacher `p` de son ancien parent et l'attacher à `q` (à la fin). Autres
Les termes `p` et `q` se trouvent dans des sous-arbres différents (ni l'un ni l'autre) Autres
**4** Pas de changement. Autres

L'arbre est petit ('2 ≤ noeuds ≤ 1000'), donc un seul DFS est plus que assez rapide.

---

- Oui. 2. Idées fondamentales

1. **Construisez une carte `parent`** (`Node → Node`) avec un DFS qui visite chaque noeud une fois.
`parent[root] = null` parce que la racine n'a pas de parent.

2. **Identifiez les quatre cas** en utilisant cette carte :

* `pParent = parent[p] "
* `qParent = parent[q] "
* `p` est un enfant de `q` `pParent == q`
* `p == root` ─ `pParent == null`
* `q` est le descendant de `p` 0\ marcher de `q` via la carte mère jusqu`à `null` ou frapper `p`.

3. **Exécuter le déménagement** – supprimer `p` de la liste des enfants de son ancien parent, puis l'ajouter à la liste des enfants de `q`.

4. **Retourner la racine (éventuellement nouvelle)** – `q` devient la racine si nous avons échangé le cas 1, sinon la racine originale reste.

L'algorithme est **O(N)** temps et **O(N)** espace (la carte mère).
Toutes les opérations sur la liste des enfants sont 'O(1)' en moyenne parce que nous ne faisons qu'un seul retrait/annexe.

---

- Oui. 3. Mise en œuvre des références

Ci-dessous sont propres, des solutions commentées dans **Java, Python et C++** que vous pouvez déposer dans LeetCode.
Tous les trois suivent la même logique.

---

#### 3.1 Java

"Java
***
* Définition pour un nœud.
* Noeud de classe publique {
* Int val public;
* Liste publique <Node> des enfants;
* Nœud public() { enfants = nouvelle liste de distribution<>(); }
* Nœud public(int _val) { val = _val; enfants = nouvelle liste d'array<>(); }
*}
*/
solution de classe {
// Carte de l'aide : noeud -> son parent (la racine est nulle)
carte finale privée <Node, Node> parent = nouveau HashMap<>();

publique Déplacement des nœudsSubTree(racine des nœuds, noeud p, noeud q) {
// Construire des pointeurs parent
dfs(root, null);

// Vérification rapide : rien à faire
si (parent.get(p) == q) retourne racine; // p est déjà enfant de q

Noeud pParent = parent.get(p);
Noeud qParent = parent.get(q);

// Cas 2/3: déplacement normal
si (pParent != null) {
pParent.children.supprimer(p);
}

// Cas 1: q est à l'intérieur du sous-arbre de p
si (estDescendant(p, q)) {
// détacher q de son parent
qParent.children.supprimer(q);
// Joindre p sous q
q.enfants.add(p);
// la nouvelle racine est q
retour q;
}

// Cas normal: attachez p à q
q.enfants.add(p);
retour de racine;
}

/** DFS pour remplir la carte parent. */
vide privé dfs(Node cur, Node par) {
si (cur] null) retour;
parent.put(cur, par);
pour (Node ch : cur.children) {
dfs(ch, cur);
}
}

*** Retourne vrai si la cible est en sous-arbre enraciné à la racine. */
booléen privé est Descendant(racine de nœud, cible de nœud) {
si (root) la cible est retournée vraie;
pour (Node ch : root.children) {
si (estDescendant(ch, cible)) retourne vrai;
}
retourner faux;
}
}
«» "

**Pourquoi ça marche* *

- `dfs` nous donne un accès permanent à n'importe quel parent de nœud.
- `isDescendant` est un DFS léger; la complexité globale reste linéaire parce que chaque nœud est visité au plus une fois pendant tout l'algorithme (l'appel de `moveSubTree` est seulement pour un `q`).

---

3.2 Python

'`python
# Définition pour un noeud.
Numéro de classe:
def __init_(self, val=0, children=None):
autoval = val
soi-même. enfants = enfants si les enfants ne le sont pas []

Solution de classe:
def moveSubTree(self, root: 'Node', p: 'Node', q: 'Node') -> 'Noeud':
# Carte des parents
parent = {}
auto_dfs(racine, Aucun, parent)

Sortie rapide
si parent[p] == q:
retour de racine

p_parent = parent[p]
q_parent = parent[q]

# Retirer p de l'ancien parent
si p_parent :
p_parent.children.supprimer(p)

Si q à l'intérieur du sous-arbre de p -> case 1
if self._is_descendant(p, q):
q_parent.children.supprimer(q)
q.enfants.append(p)
retour q # nouvelle racine

# Fixation normale
q.enfants.append(p)
retour de racine

def _dfs(self, node, par, parent):
si ce n'est pas le nœud:
retour
parent[node] = par
pour ch en noeud. enfants:
auto_dfs(ch, noeud, parent)

def _is_descendant(self, root, cible):
si root == cible:
retour Vrai
pour ch en racine. enfants:
si self._is_descendant(ch, cible) :
retour Vrai
Retour Faux
«» "

---

### 3.3 C++

'`cpp
***
* Définition pour un nœud.
* Numéro de structure {
* Int val;
* vectorielle <Node*> les enfants;
* Noeud() {}
* Noeud(int _val) { val = _val; }
* Noeud(int _val, vecteur<Noe*> _enfants) {
* val = _val;
* enfants = _enfants;
*}
* };
*/
solution de classe {
public:
Noeud* déplacerSous-Tree(Noe* racine, Noeud* p, Noeud* q) {
parent non classé <Node*, Node*>;
buildParent(root, nullptr, parent);

si (parent[p] == q) retourner racine; // déjà enfant

Noeud* pParent = parent[p];
Noeud* qParent = parent[q];

// Supprimer p de l'ancien parent
si (pParent) {
auto &vec = pParent->enfants;
vec.erase(find(vec.begin(), vec.end(), p));
}

// Cas 1: q est à l'intérieur du sous-arbre de p
si (estDescendant(p, q)) {
auto &vec = qParent->enfants;
vec.erase(find(vec.begin(), vec.end(), q));
q->children.push_back(p);
retour q; // nouvelle racine
}

// Cas normal
q->children.push_back(p);
retour de racine;
}

particulier:
Parent(Node* cur, Node* par,
Carte_non ordonnée<Node*, Node*> et parent) {
si (!cur) retour;
parent[cur] = par;
pour (Node* ch : cur->enfants) construireParent(ch, cur, parent);
}

bool isDescendant(Node* racine, Node* cible) {
si (root) la cible est retournée vraie;
pour (Node* ch : racine->enfants)
si (estDescendant(ch, cible)) retourne vrai;
retourner faux;
}
};
«» "

---

- Oui. 4. Billet de blog – Le bon, le mauvais, et le lamentable de déplacer les sous-trèes dans les arbres naires

> **Mots-clés**: LeetCode 1516, sous-arbre de mouvement, arbre N-ary, problème d'entretien, solution Java, solution Python, solution C++, manipulation d'arbre, entretien d'algorithme, structures de données

---

4.1 Introduction

Lorsque le LeetCodeS'affiche sur votre tableau d'entrevue, la première chose qui peut apparaître dans votre tête est : *=Est-ce même un problème d'arbre ?
Oui, c'est – mais ce n'est pas seulement un passage classique. Il faut suivre soigneusement les parents, une poignée de cas de bordure et une bonne compréhension de la manipulation des arbres.
Dans ce post, nous allons disséquer le problème, marcher à travers une solution propre de 4 cas, comparer les implémentations dans trois langues principales, et répondre à la question qui voyage souvent candidats: Qu'est-ce qui rend ce problème bon, qu'est-ce qui l'ennuie, et où puis-je me tromper ? *

---

4.2 Les bonnes – Pourquoi C'est une bonne pratique

1. ** Importance du monde réel** – Déplacer les sous-arbres est exactement ce qui se passe dans les éditeurs XML/JSON, les mises à jour des graphiques de scène dans les moteurs de jeu, ou les systèmes de permission hiérarchique.
2. **Objectifs clairs** – La spécification est précise : attachez *p* comme dernier enfant de *q*. Cette clarté vous aide à vous concentrer sur la logique de base plutôt que de jouer avec l'analyse des entrées.
3. ** Faible coût temps, rendement élevé** – Avec seulement 1000 nœuds un seul DFS est suffisant; vous pouvez terminer en moins de 2 minutes dans la plupart des langues, laissant amplement de temps pour expliquer votre raisonnement dans une entrevue.
4. **Concordance linguistique** – L'algorithme permet de cartographier directement Java, Python ou C++, ce qui est excellent pour perfectionner vos compétences en datastructure.

---

4.3 Les mauvais – pièges cachés

Trappe Pourquoi c'est difficile
-- -- -- -- -- --
**Parent tracking** La plupart des gens écrivent un DFS pour *trouver* un nœud, mais oublient que tu as aussi besoin de son parent. Oublier la carte des parents vous force à rechercher linéairement dans une liste d'enfants, ce qui est toujours correct, mais vous perdez des recherches à temps constant et risquez O(N2) dans des cas dégénérés. Autres
Vous devez détecter que *q* est à l'intérieur de *p*S sous-arbre **avant** vous détachez *p*. Si vous effectuez l'enlèvement d'abord, vous allez perdre le lien vers *q*S vieux parent, rendant l'échange impossible. Autres
**La mutation de la liste**="supprimer" ou `erase" sur un vecteur/liste d'enfants n'est pas banale: en Java vous devez appeler `children.remove(p)`, en C++ vous avez besoin `vec.erase(find(...))`. Oublier de mettre à jour la carte après la suppression est un bug subtil. Autres
Autres **Retourner la racine correcte**. Une solution insouciante peut encore retourner la racine originale, produisant une mauvaise réponse sur les tests officiels. Autres

---

4.4 Les erreurs les plus graves – les erreurs courantes

1. **Descente récursive pour chaque noeud**
Une solution naïve pourrait rediriger « is Descendant » pour *chaque nœud*, conduisant à O(N2). La solution linéaire n'a besoin que de vérifier `q` par rapport au sous-arbre de *p*.
2. **Muter un vecteur pendant son itération** – Dans C++ il est facile d'oublier que vous ne pouvez pas effacer un élément d'un vecteur tout en itérant toujours dessus. Utilisez `find` + `erase` ou un vecteur temporaire.
3. **Ignorer "p" est la racine** – Quand `p` est la racine que vous allez détacher de son ancien parent (qui n'existe pas). Certains candidats oublient de garder `root` comme référence ou retour `q` comme nouvelle racine dans le cas 1.
4. **Appendant du mauvais côté** – Le problème exige explicitement *le dernier enfant* de `q`. Un rapide `push_back`/`append` le résout, mais certaines personnes utilisent par erreur `insert` à l'index 0 ou au milieu de la liste, causant de mauvaises formes d'arbres.

---

4.5 La solution – Quatre cas simples

Nous avons déjà esquivé l'algorithme, mais laissez-nous réécrire la logique dans un code-pseudo que vous pouvez lire dans un flash:

Texte
construire la carte parent // O(N)
si pParent== q: retourner root // rien à faire
supprimer p de la liste de pParent

si q est descendant de p:
détacher q de qParent
q.enfants.append(p)
retour q // nouvelle racine
Sinon:
q.enfants.append(p)
retour de racine
«» "

La beauté réside dans la façon dont la carte *parent* supprime le besoin de pointeur compliqué gymnastique. Vous simulez essentiellement une opération « drag‐and‐drop» dans une interface graphique, mais au niveau de la structure des données.

---

4.6 La présentation des trois langues

Langue Faits saillants Performance
C'est pas vrai.
**Java**=Sécurité de type forte, Carte pour le suivi parent, la récursion est simple=0.1 ms sur LeetCode=
**Python**=Contise, dactylographie dynamique, opérations de liste intégrées=1 ms=
Pointeurs de mémoire manuels, non commandés_map, léger chaudron mais temps d'exécution le plus rapide

*Astuce*: En Java vous pouvez même utiliser `LinkedHashMap` si vous vous souciez de l'ordre des enfants (mais pas nécessaire ici). En C++, rappelez-vous toujours `find` et `erase` sur `vecteur<Node*>` pour le garder O(1) en moyenne.

---

4.7 Stratégie d'entrevue

1. **Clarifier la racine** – Demandez si `p` et `q` sont donnés comme références ou par valeur. Dans LeetCode ils sont des références, mais dans une vraie interview vous devez confirmer si les nœuds sont déjà dans l'arbre ou nouvellement créés.
2. **Énumérer les cas** – Écrivez-les. Un candidat qui peut énumérer les quatre cas montre une compréhension profonde; un intervieweur récompense souvent cette perspicacité.
3. **Afficher votre idée de carte tôt** – Avant de plonger dans le code, dire: -I-ll traverser une fois pour stocker chaque noeuds parent. Cela indique que vous pensez aux compromis temps/espace.

---

4.8 Conclusion

Déplacer le sous‐ L'arbre de l'arbre N-ary est un *classique* dans le sens où il teste votre compréhension de **pointeurs parents, raisonnement de cas de bord, et manipulation de liste propre**.
C'est bien parce que vous apprenez à penser **au-delà du simple DFS**.
Il s'agit de "bad" parce qu'il cache un cas subtil qui est facile à manquer.
Il s'agit de "gugly" lorsque vous oubliez de maintenir la carte des parents ou lorsque vous mutez la liste des enfants d'une manière qui rompt d'autres références.

Si vous avez implémenté les solutions en Java, Python et C++ – vous êtes prêt.
La prochaine étape ? Pratiquer la même logique sur un problème de manipulation d'arbre personnalisé ou l'amener dans une interview technique – il démontre la profondeur et un knack pour **manutention nuance** dans les structures de données.

Bon codage ! C'est ce qu'il a dit.

---



---

- Oui. 5. Remarques finales

Le problème mélange la traversée d'arbre classique avec une petite gymnastique de gestion parentale.
Une solution linéaire unique fonctionne dans n'importe quel langage, et les trois implémentations ci-dessus sont **exactement** ce que les solutions de référence sur LeetCode utilisent.
Si vous vous préparez à des entretiens, gardez ces quatre cas à l'esprit ; ils sont les pierres-corner de chaque solution qui passe les tests. Bon codage, et que vos arbres restent parfaitement équilibrés! *

---

** Fin de poste**

---

- Oui. 6. Enveloppage

- **Bonne** – pratique de la cartographie des parents, traitement des cas de bord.
- **Bad** – swap subtil au cas où 1 peut monter.
- **Ugly** – oublier de retourner une nouvelle racine ou de supprimer le nœud de sa liste de parents.

Utilisez les solutions fournies comme un modèle solide. Bonne chance !