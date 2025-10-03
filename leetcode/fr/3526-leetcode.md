---
titre: LeetCode 3526. Gamme XOR Questions avec Subarray Reversals -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3526 – Gamme XOR Questions avec Subarray Reversals
**Public=1 ≤ longueur nums.longueur des requêtes ≤ 105**

---

- Oui. 1. Aperçu du problème

On vous donne un tableau `nums` et un flux de requêtes.
Trois types de requêtes existent :

Signification des paramètres
C'est pas vrai.
Autres Mise à jour des points : "nums[index] = valeur" Autres
Autres `2`- Gamme XOR: retour `nums[left] Autres
Autres `3`-Reversement de la sous-couche: inverser la tranche `nums[gauche...droite]```[3, gauche, droite]` Autres

Retourne un tableau contenant les réponses de chaque requête de type‐2 dans l'ordre où elles ont été traitées.

La solution de force brute s'exécute en 'O(n)' par requête – beaucoup trop lent pour la 105 liée.

---

- Oui. 2. Pourquoi un arbre est le bon outil

Toutes les opérations impliquent ** segments contigus** du tableau.
Une structure de données classique pour ces problèmes est l'arborescence binaire *implicite*:

* ** Treap implicite** – une BST randomisée qui stocke les éléments par *position* au lieu de clé.
* **Splay implicite** – auto-équilibrage par rotations sur accès.
* **Implicit AVL** – équilibre déterministe, mais un peu plus chaudron.

Les propriétés clés que nous devons augmenter:

1. **Taille** – pour diviser / fusionner par index.
2. **XOR du sous-arbre** – pour répondre à la plage XOR en 'O(1)' après une scission.
3. **Lazy reverse flag** – pour inverser un segment entier dans `O(log n)` en changeant un drapeau au lieu de toucher chaque noeud.

Toutes les opérations (`split`, `merge`, `update`, `reverse`, `rangeXOR`) deviennent `O(log n)` en moyenne, donnant une solution globale `O(n+q) log n)`.

---

- Oui. 3. Algorithme de haut niveau

1. **Construire** l'arbre implicite à partir du nombre initial.
*Insérer* chaque élément à la fin (`insert(i, nums[i]")), ou construire dans `O(n)` par fusions successives.

2. Pour chaque requête :

* **Mise à jour**
* Divisé en `[0, index)`, `[index]`, `[index+1, n)`
* Changez la valeur du nœud médian, recalculez son XOR.
* Fusionne-toi.

* **Plage XOR**
* Séparer en `[0, gauche)`, `[gauche, droite]`, `[droite+1, n) "
* Le XOR de la partie centrale est la réponse.
* Fusionne-toi.

* **Réversé**
* Séparer en `[0, gauche)`, `[gauche, droite]`, `[droite+1, n) "
* Basculez le drapeau inverse de la partie centrale.
* Fusionne-toi.

Toutes les divisions/merges maintiennent l'arbre équilibré en moyenne parce que la priorité (ou la rotation) est randomisée.

---

- Oui. 4. Code

Vous trouverez ci-dessous des implémentations propres, prêtes à la copie pour **Java**, **Python** et **C++**.

> **Astuce** – Dans Python, vous aurez besoin de `sys.setrecursionlimit(1 << 25)' ou de scissions/merges itératives si votre profondeur de récursion est un problème.
> Dans C++, utilisez `std::mt19937 rng` pour les priorités.
> Dans Java, utilisez `ThreadLocalRandom.current()`.

---

#### 4.1 Java – Treap implicite

"Java
Importation de java.util.*;
importer java.util.concurrent.ThreadLocalRandom;

solution de classe publique {
- Oui. Numéro -------- */
Nœud statique privé {
valeur enregistrée
xor int; // xor du sous-arbre
taille int; // taille du sous-arbre
int prio; // priorité aléatoire
boolean rev; // drapeau inversé paresseux
Noeud gauche, droit;

Node(int v) {
ce.val = v;
ce.xor = v;
cette taille = 1;
ce.prio = ThreadLocalRandom.current().nextInt();
ce.rev = faux;
}
}

- Oui. Aides -------- */
taille d'int statique privée(Node t) { retour t == null ? 0 : t.size; }
int statique privé xor(Node t) { retour t == null ? 0 : t.xor; }

Poussoir à vide statique privé(Node t) {
si (t != null && t.rev) {
t.rev = faux;
Noeud tmp = t.left; t.left = t.right; t.right = tmp;
si (t.left != null) t.left.rev ^= true;
si (t.right != null) t.right.rev ^= true;
// XOR est symétrique, pas besoin de recalculer
}
}

vide statique privé à la hausse(Node t) {
Si (t != null) {
t.size = 1 + taille(t.left) + taille(t.right);
t.xor = t.val ^ xor(t.left) ^ xor(t.right);
}
}

- Oui. Séparer / Fusionner --------- */
// scindé par taille: gauche a les premiers éléments k
fractionnement statique de nœud privé(Node t, int k) {
si (t == null) retourne un nouveau Node[]{null, null};
Pousser(t);
si (k <= taille(t.gauche)) {
Noeud[] res = split(t.left, k);
t.gauche = res[1];
à jour(t);
retour de nouveau Node[]{res[0], t};
} autre {
Noeud[] res = split(t.right, k - size(t.left) - 1);
t.right = res[0];
à jour(t);
retourner le nouveau Node[]{t, res[1]};
}
}

statique privé Fusion de nœud(Node a, Node b) {
si a) null) retourner b;
si b == nul) retourner a;
poussant(a); poussant(b);
si (a.prio > b.prio) {
a.right = fusion (a.right, b);
Mise à jour(a);
retour a;
} autre {
b.left = fusion(a, b.left);
b);
retour b;
}
}

- Oui. Opérations --------- */
privé racine du nœud;

// Construire l'arborescence à partir du tableau
vide build(int[] arr) {
pour (int v : arr) root = merge(root, nouveau Node(v));
}

vide update(int idx, int val) {
Noeud[]a = fraction (root, idx);
b = fractionnement(a[1], 1);
b[0].val = valeur;
à la hausse(b[0]);
racine = fusion(a[0], fusion(b[0], b[1]);
}

Int gamme Xor(int l, int r) {
Noeud[]a = fraction (racine, l);
b = fraction(a[1], r - l + 1);
int res = xor(b[0]);
racine = fusion(a[0], fusion(b[0], b[1]);
retour rés;
}

vide inverse(int l, int r) {
Noeud[]a = fraction (racine, l);
b = fraction(a[1], r - l + 1);
si (b[0] != null) b[0].rev ^= true;
racine = fusion(a[0], fusion(b[0], b[1]);
}

- Oui. API publique --------- */
public int[] getResults(int[] nums, int[][] requêtes) {
build(nums);
Liste <Integer> ans = nouvelle liste de distribution<>();
pour (int[] q : requêtes) {
interrupteur (q[0]) {
cas 1: mise à jour(q[1], q[2]); rupture;
cas 2: ans.add(rangeXor(q[1], q[2])); rupture;
cas 3: inverse(q[1], q[2]); rupture;
}
}
retourner le fichier ans.stream().mapToInt(entier::intValue).àArray();
}
}
«» "

---

#### 4.2 Python – Treap implicite

'`python
les systèmes d'importation, au hasard
sys.setrecursionlimite(1 << 25)

Numéro de classe:
__slots__ = ('val', 'xor', 'size', 'prio', 'rev', 'l', 'r')
def __init_(self, val):
autoval = val
auto.xor = valeur
taille de soi = 1
Self.prio = aléatoire.randint(0, 1 << 30)
Self.rev = Faux
Self.l = Aucune
autor = Aucune

def sz(t): retourner t.size si t autre 0
def xo(t): retourner t.xor si t autre 0

def push(t):
si t et t.rev:
t.rev = Faux
t.l, t.r = t.r, t.l
Si t.l: t.l.rev ^= Vrai
si t.r: t.r.rev ^= Vrai

d'après:
si t:
t.size = 1 + sz(t.l) + sz(t.r)
t.xor = t.val ^ xo(t.l) ^ xo(t.r)

def split(t, k):
si non t: retour (Aucun, Aucun)
Pousser(t)
si k <= sz(t.l):
l, r = fractionnement (t.l, k)
t.l = r
Mise à jour(t)
retour (l, t)
Sinon:
l, r = fractionnement(t.r, k - sz(t.l) - 1)
t.r = l
Mise à jour(t)
retour (t, r)

def fusion(a, b):
si non a: retour b
si non b: retourner a
Pousser(a); pousser(b)
si a.prio > b.prio:
a.r = fusion(a.r, b)
(a)
retour a
Sinon:
b.l = fusion(a, b.l)
(b)
retour b

Solution de classe:
def _init_(self):
auto.root = Aucune

Def build(self, arr):
pour v in arr:
self.root = fusion(self.root, Node(v))

def point_update(self, idx, val):
a, b = fraction (self.root, idx)
milieu, c = fraction (b, 1)
mi.val = val
(milieu)
self.root = fusion(a, fusion(mid, c))

def range_xor(self, l, r):
a, b = split(self.root, l)
milieu, c = fraction (b, r - l + 1)
res = xo(mid)
self.root = fusion(a, fusion(mid, c))
retour res

def inverse (self, l, r):
a, b = split(self.root, l)
milieu, c = fraction (b, r - l + 1)
si mi: mi.rev ^= Vrai
self.root = fusion(a, fusion(mid, c))

def getResults(self, nombres, requêtes):
auto.construction(nombres)
out = []
pour q dans les requêtes :
si q[0] == 1 :
Self.point_update(q[1], q[2])
élif q[0] == 2 :
out.append(self.range_xor(q[1], q[2]))
Sinon: # 3
(q[1], q[2])
retour
«» "

---

### 4.3 C++ – Treap implicite (Rope)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

Numéro de structure {
Int val, xorv, sz;
bool rev;
La présente décision entre en vigueur le jour suivant celui de sa publication au Journal officiel de l'Union européenne.
Nœuds
Node(int v) : val(v), xorv(v), sz(1), rev(false), prio(rand()), l(nullptr), r(nullptr) {}
};

int sz(Node* t) { retour t ? t->sz : 0; }
int xo(Node* t) { retour t ? t->xorv : 0; }

poussoir vide(Node* t) {
si (!t->rev) retourne;
t->rev = faux;
échange(t->l, t->r);
si (t->l) t->l->rev ^= true;
si (t->r) t->r->rev ^= true;
}

vide mis à jour(Node* t) {
si (!t) retour;
t->sz = 1 + sz(t->l) + sz(t->r);
t->xorv = t->val ^ xo(t->l) ^ xo(t->r);
}

couple <Node*, noeud*> fractionné(Node* t, int k) {
si (!t) retourne {nullptr, nullptr};
Pousser(t);
si (k <= sz(t->l)) {
auto res = split(t->l, k);
t->l = res.seconde;
à jour(t);
retour {res.first, t};
} autre {
auto res = split(t->r, k - sz(t->l) - 1);
t->r = res.first;
à jour(t);
retour {t, res.second};
}
}

Noeud* fusion (Noeud* a, Noeud* b) {
si a) retour b;
si b) retourner a;
poussant(a); poussant(b);
si (a->prio > b->prio) {
a->r = fusion(a->r, b);
Mise à jour(a);
retour a;
} autre {
b->l = fusion(a, b->l);
b);
retour b;
}
}

struct ImplicitTreap {
Noeud* racine = nullptr;
build de vide(vecteur Const<int>& a) {
pour (int v : a) root = merge(root, nouveau Node(v));
}

vide point_update(int idx, int val) {
auto a = split(root, idx);
auto b = split(a.seconde, 1);
b. premier->val = valeur;
upd(b.first);
racine = fusion(a.first, fusion(b.first, b.second));
}

int range_xor(int l, int r) {
auto a = fractionnement (root, l);
auto b = split(a.seconde, r - l + 1);
int ans = xo(b.first);
racine = fusion(a.first, fusion(b.first, b.second));
le retour des an;
}

vide inverse(int l, int r) {
auto a = fractionnement (root, l);
auto b = split(a.seconde, r - l + 1);
si (b.first) b.first->rev ^= true;
racine = fusion(a.first, fusion(b.first, b.second));
}
};

solution de classe {
public:
vector<int> getResults(vector<int>& nums, vector<vector<int>& requêtes) {
ImpliciteTreap t;
t.build(nums);
vecteur <int> ans;
pour (auto& q : requêtes) {
si (q[0]] 1) t.point_update(q[1], q[2]);
Sinon, si (q[0]] 2) ans.push_back(t.range_xor(q[1], q[2]));
autres t.revers(q[1], q[2]);
}
le retour des an;
}
};
«» "

> **Note** – La version C++ utilise `rand()` pour la simplicité; le remplacer par un PRNG rapide (`mt19937`) pour le code de production.

---

- Oui. 5. Article de blog – -**Range XOR & Reversal** – Bon, Mauvais et Ugly dans LeetCode 3526

---

5.1 Pourquoi ce problème se pose

Les problèmes de LeetCode sont rarement associés à trois opérations apparemment insignifiantes.
Ils vous obligent à **penser en termes d'opérations de segment** et à **augmenter les arbres** au-delà du manuel `sum / min`.
Les intervieweurs aiment voir :

* Capacité de **réduire la complexité** de linéaire à logarithmique.
* Compréhension de la propagation *lazy* pour les segments réversibles.
* Code clair et maintenable (même pour un treap implicite de 10 pages).

---

5.2 Bon – Ce qui fonctionne

Qu'est-ce que c'est ?
C'est quoi ?
** Clé implicite** – pas besoin de stocker des indices explicites. Autres
**Équilibre aléatoire** – très petit code, cas moyen rapide. Autres
**XOR augmentation** – trivial à maintenir avec "val ^ xor(gauche) ^ xor(droite)". Autres
**Lazy reverse** – O(1) drapeau basculement, aucun échange par noeud. Autres
** API réutilisable** – `split`, `merge` peut résoudre de nombreux problèmes de segment (élément k-th, somme de la plage, vérification du palindrome, etc.). Autres

---

5.3 Mauvais – Ce qui rend le code désagréable

Points de douleur
C'est pas vrai.
** Récursion profonde** – La "split/merge" est récursive; la pile Python peut déborder. Autres
**Mémoires** – chaque nœud stocke 7 pointeurs/int/flags → ~80 octets par élément → ~8 Mo pour 105 nœuds – encore bien mais pas trivial. Autres
**Difficile de déboguer** – les erreurs hors-par-un dans les indices fractionnés sont fréquentes. Autres
**Randomness** – les cas de test déterministe peuvent exposer des arbres déséquilibrés dans de rares cas de bordure. Autres

---

#### 5.4 Ugly – Les choses Vous voulez vraiment éviter

Éviter si possible
Il s'agit d'un projet pilote.
**Équilibrage manuel (AVL)** – code supplémentaire pour maintenir les hauteurs; ne vaut pas le gain de vitesse marginal. Autres
**Inversements non paresseux** – l'échange d'enfants à l'intérieur d'une boucle de longueur `O(r-l+1)' va à l'encontre du but. Autres
**L'attribution de priorité de Wong** – en utilisant `rand()` sans semis (`srand`) peut produire la même priorité pour tous les nœuds → dégénérescence. Autres
**Pointer fuites** – oublier les nœuds `delete` (C++), vous allez manquer de tas après de nombreux cas de test. Autres

---

- Oui. 6. Pensées finales

*LeetCode 3526* est un problème classique**.
Les trois opérations se plantent naturellement sur le squelette `split/merge`; l'astuce est le drapeau **XOR + inverse**.
Si vous pouvez expliquer la conception et la mettre en œuvre dans n'importe quelle langue avec un code propre, vous aurez non seulement ce problème mais toute une série de questions d'entrevue orientées segment.

---

6.1 À emporter pour les candidats

1. **Démarrer simple** – un filet implicite (randomisé) est le bon endroit.
2. **Tester les cas de bord** – pousser vers les éléments `n` avec toutes les opérations sur l'ensemble du tableau pour assurer l'équilibre.
3. **Utilisez `__slots__` / `struct` emballage** pour la mémoire.
4. **Ajouter des assertions** (Python) ou des vérifications de santé (C++) pour attraper les bogues index tôt.

---

5.5 Appel à l'action

Essayez les implémentations ci-dessus dans votre sandbox LeetCode.
Ajouter un mode **debug** qui imprime les nombres de nœuds, leur profondeur et leur statut.
Poussez la solution sur **Codeforces 1226D** (le -D. Reversing Substrings) pour voir comment la même structure résout différents problèmes de segment.

---

Note finale

Lorsque vous maîtrisez le modèle =rope=, la prochaine fois que vous verrez un problème qui demande l'élément =k‐th, la somme de la plage, le sous-réseau inverse=, vous aurez un outil *prêt à réutiliser* dans votre boîte à outils.
LeetCode 3526 n'est pas qu'un défi, c'est une classe de master en structures de données avancées**.

Bon codage ! C'est ce qu'il a dit.

---

## 6.7 Annexe – Récapitulation de la complexité rapide

Opération (défaut)
- C'est quoi ?
Point mis à jour \(O(\log n)\)=" Deux divisions + fusion, les mises à jour du drapeau se propagent paresseusement. Autres
Gamme XOR (O(\log n)\) (Deux scissions + fusion, temps de constante XOR). Autres
Inverser \(O(\log n)\)=Deux scissions + fusion + basculement du drapeau, sans balayage. Autres

Mémoire: ~80 octets × 105 8 Mo.
Tous dans les limites typiques de LeetCode.

---

- Oui. 7. Enveloppage

Vous avez maintenant :

* ** Implémentations complètes** dans **Python, C++** et **Java**.
* **Une explication détaillée** de la raison pour laquelle le code fonctionne, où il falte, et comment **refactor** pour la production.
* A **blog article** qui cadre le problème d'une interview-perspective, vous guidant à travers les **bons, mauvais, laid** aspects de ces solutions avancées segment-tree.

Allez-y, soumettez votre solution sur LeetCode 3526, et laissez le treap implicite faire sa magie! Les

---

**Mots clés:**
`LeetCode 3526 `=" `range XOR`=" `revers subarray`=" `implicite treap`=" `rope`=" `lazy propagation`=" `logarithmic complexity`=" `segment treegraration`=" `interview data structure`=" `avancé algorithmic problem` "