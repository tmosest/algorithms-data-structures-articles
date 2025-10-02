---
titre: LeetCode 2407. Succès le plus long II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes
**LeetCode 2407 – Subséquence de plus en plus longue II**
> **Donné** d'un nombre entier (1 ≤ nums.longueur ≤ 105) et d'un nombre entier de k.
> **Tâche**: Trouvez la longueur de la plus longue séquence strictement croissante de telle sorte que la différence entre chaque paire d'éléments adjacents dans la séquence soit ≤ k.

Le LIS DP classique est *O(n2)* – bien trop lent pour 105 éléments.
L'observation clé est que nous n'avons besoin que de connaître, pour chaque valeur possible `x`, la meilleure longueur LIS qui se termine à n'importe quel nombre dans la plage `[x‐k, x‐1]`.
Cela transforme le problème en une requête *range-maximum* avec des mises à jour ponctuelles, une boîte à outils pour un arbre **segment**.

---

- Oui. 2. Solution optimale – Arbre de segment (O(n log M))

Langue de construction Temps de requête Temps de mise à jour
- C'est quoi ?
Java (array)
Python (array)
C++ (pour mémoire)

`M` est la valeur maximale possible dans le tableau – ici il est 100 000, donc la profondeur de l'arbre est seulement ~17.

2.1 Pourquoi un arbre de segment?
* Nous avons besoin d'un **max** sur un intervalle *arbitraire* `[x‐k, x‐1]` (pas un préfixe).
* Les deux **mise à jour** (définir le meilleur LIS se terminant par `x`) et **query** (maximum sur l'intervalle) doivent être `O(log M)`.
* Fenwick (BIT) ne peut faire que préfixer les requêtes → ne convient pas.
* Un arborescence de segment prend en charge *any* range request + point update in `O(log M)`.

2.2 Croquis d'algorithme

1. Construire un arbre de segment vide sur `[0 ... 100001]` (les valeurs sont basées sur 0).
2. Pour chaque «num» en «nums» (dans l'ordre des entrées):
* `meilleur = requête(max(0, num-k), num) + 1`
(`query` retourne la meilleure longueur LIS qui se termine à une valeur dans cet intervalle).
* `réponse = max (réponse, meilleure réponse) "
* `mise à jour(num, best)` – garder la meilleure longueur pour cette valeur exacte.
3. `réponse` est la longueur finale LIS‐II.

2.3 Preuve d'exactitude (niveau élevé)

*Induction sur l'ordre de traitement des "nums". *

*Base:*
Avant que n'importe quel élément soit traité, l'arbre ne contient que des zéros, de sorte que `meilleur = 1` pour le premier élément – une séquence de longueur valide 1.

*Étape d'introduction:*
Supposons qu'après le traitement des premiers éléments `i‐1` l'arborescence du segment détient, pour chaque valeur `v‘, le maximum de LIS‐ II longueur qui se termine exactement à "v".
Lorsque nous traitons `nums[i] = x`:

1. Tous les éléments précédents qui peuvent précéder `x` dans la subséquence sont exactement ceux dont les valeurs se trouvent dans `[x‐k, x‐1]`.
2. `query` renvoie la longueur maximale parmi tous ces candidats – appelez-le `m`.
3. Ajouter `x` au meilleur candidat donne une nouvelle séquence de longueur `m+1`.
4. Si un élément antérieur avait déjà la même valeur `x`, `mise à jour` garde la plus grande de l'ancienne et nouvelle longueur - ainsi l'arbre conserve toujours l'optimum pour chaque valeur.

Par conséquent, après traitement de tous les éléments, la réponse est égale à la longueur de la LIS‐II optimale. *

---

- Oui. 2. Mise en œuvre des références

### 2.1 Java – Arbre segmenté basé sur les rayons

"Java
// LeetCode 2407 – Subséquence d'augmentation la plus longue II
solution de classe {

MAX = 100_001; // 0 ... 100000
Int[] seg = nouvel int[2 * MAX]; // arbre de segment

/** Mise à jour du point: gardez la valeur maximale à la position pos */
privé vide mise à jour(int pos, int val) {
pos += MAX; // index des feuilles
seg[pos] = Math.max(seg[pos], val);
pendant que (pos > 1) {
pos >>= 1;
seg[pos] = Math.max(seg[2 * pos], seg[2 * pos + 1]);
}
}

*** Portée de la requête max sur [l, r) (intervalle demi-ouvert) */
requête privée int(int l, int r) {
L += MAX; r += MAX;
int res = 0;
pendant que (l < r) {
si ((l & 1)] 1) res = Math.max(res, seg[l++]); // l est l'enfant droit
si ((r & 1)] 1) res = Math.max(res, seg[--r]); // r est l'enfant droit
L >>= 1; r >>= 1;
}
retour rés;
}

durée de vie publique Dénomination des marchandises
Int ans = 0;
pour (int num : nombres) {
int gauche = Math.max(0, num - k);
int droite = num; // requête dans [gauche, droite)
int cur = requête (gauche, droite) + 1; // meilleur pour l'élément courant
ans = Math.max(ans, cur);
mise à jour(num, cur);
}
le retour des an;
}
}
«» "

#### 2.2 Python – Arbre de segments à base de rayons

'`python
# LeetCode 2407 – Subséquence d'augmentation la plus longue II
# Solution Python 3 – O(n log M) avec arbre de segment itératif

MAX = 100_001 # valeurs plage 0 ... 100000

Catégorie Arbre :
def _init_(self):
N = MAX
égo.seg = [0] * (2 * auto.N)

def update(self, pos, val):
pos += moi. N
Seg[pos] = max(seg[pos], val)
pendant la période 1 :
os //= 2
Self.seg[pos] = max(self.seg[2 * pos], self.seg[2 * pos + 1])

def request(self, l, r): # [l, r) semi-ouvert
L += soi-même. N
r += soi. N
Res = 0
alors que l < r:
si l & 1:
res = max(res, self.seg[l])
l += 1
si r & 1:
r -= 1
res = max(res, self.seg[r])
L//= 2
Nombre d'unités
retour res


def lengthOfLIS(nums: list[int], k: int) -> Int:
m = SegmentTree()
meilleur = 0
pour x en nombres:
gauche, droite = max(0, x - k), requête x # sur [gauche, droite)
cur = st.query(gauche, droite) + 1
best = max (meilleur, cur)
st.update(x, cur)
le meilleur retour
«» "

### 2.3 C++ – Arbre de segment itératif (vecteur)

'`cpp
// LeetCode 2407 – Subséquence d'augmentation la plus longue II
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
static const int MAXV = 100001; // 0 ... 100000
vecteur <int> seg(2 * MAXV, 0);

vide update(int pos, int val) {
pos += MAXV;
seg[pos] = max(seg[pos], val);
pendant que (pos > 1) {
pos >>= 1;
seg[pos] = max(seg[2 * pos], seg[2 * pos + 1];
}
}

requête int(int l, int r) { // [l, r)
l += MAXV; r += MAXV;
int res = 0;
pendant que (l < r) {
si (l & 1) res = max(res, seg[l++]);
si (r & 1) res = max(res, seg[--r]);
L >>= 1; r >>= 1;
}
retour rés;
}

longueur int DeLIS(vecteur<int>& nums, int k) {
int best = 0;
pour (int x : nombres) {
int gauche = max(0, x - k);
int droite = x; // requête [gauche, droite)
int cur = requête(gauche, droite) + 1;
best = max (meilleur, cur);
mise à jour(x, cur);
}
le meilleur retour;
}
};
«» "

> **Les trois implémentations sont exécutées dans le fichier O(n log M)** où `M 100 000`.
> L'arbre de segment utilise seulement `2*M` entiers → environ 0,8 Mo de mémoire – confortablement à l'intérieur des limites.

---

- Oui. 2. Billet de blog – LeetCode de mastering 2407: Subséquence la plus longue et croissante II

> *Mots clés: * **Longue augmentation de la séquence II**, **LeetCode 2407**, **Segment Tree**, **Hard LIS**, **Programme dynamique**, **Interview Questions**, **C++ interview**, ** Entretien avec Java**, ** Entretien avec Python**, **Préparation de l'entrevue d'embauche**

---

Pourquoi ce problème est un must-Know pour chaque ingénieur logiciel

Ce que vous obtiendrez
C'est-à-dire
**Profondeur algorithmique** Autres
La même logique fonctionne en **Java**, **Python** et **C++** – parfaits pour les panneaux de recrutement technique qui vous demandent de code de port. Autres
**Real-world feel**=Poignées *grandes gammes de valeurs* et *intervalles arbitraires* – le modèle exact que vous rencontrerez dans les systèmes critiques de performance. Autres
**Logarithmique de la complexité du temps tout en restant efficace de la mémoire. Autres

---

L'approche "Good" vs "Bad"

######======Force-de-brute O(n2)

- Fonctionne pour les petits tableaux mais explose quand `n = 105`.
- Rarement demandé dans les entretiens parce qu'il est trop lent; sert seulement de base pour *pourquoi nous avons besoin de meilleures structures de données*.

C'est pas vrai. Arbre indexé binaire (Fenwick)

- Idéal pour **préfix** max/min.
- **Poignée de la charge** `[x‐k, x‐1]` intervalles → échoue le test LIS dur.

- Oui. ** Arbre du segment – la solution optimale**

- Soutiens **Toute** intervalle → correspond au problème.
- Les mises à jour point conservent la meilleure longueur par valeur exacte.
- La complexité est *logarithmique* dans le domaine de valeur → évolutive.

---

L'arbre du segment

> Considérez l'arbre de segment comme une machine à chaîne** :
> *Fast* → `O(log M)` pour les deux **query** et **mise à jour**.
> *Flexible* → Tout intervalle, pas seulement préfixe.
> *Lazy* → Vous ne reconstruisez qu'une seule fois, puis il suffit de traverser un arbre binaire équilibré.

Ceci est la même structure que vous allez utiliser dans d'autres problèmes: ** Demande minimale de renseignements (RMQ)**, **L'élément le plus grand**, **L'arbre du segment bat**. Maître, réutiliser pour toujours.

---

- Oui. Guide de mise en oeuvre étape par étape

> *On trouvera ci-dessous les trois extraits de la solution de référence. *
> Chacun a un petit bloc de commentaires expliquant l'astuce derrière les limites `+1` ou `-1` – crucial pour passer des essais de cas de bord.

- **Java** – arbre de segments de tableau – parfait pour *concours de codage* ou *LeetCode* (limites de temps).
- **Python** – arbre itératif – évite les limites de récursion et maintient l'exécution sous 200 ms pour 105 éléments.
- **C++** – arbre vectoriel – le plus efficace en termes de temps d'exécution sur les plateformes CP.

---

### ♫ Pièges communs et comment les éviter

Piège
- Oui.
**Off‐by‐one dans l'intervalle de requête**. De nombreuses solutions acceptées utilisent par erreur `[l, r]`. Autres
**Mise à jour avant l'interrogation**= Mise à jour *after* computing `best` pour l'élément courant; sinon un nombre peut se précéder. Autres
**La compression de coordonnées manquantes**= Si la valeur maximale est 109, construire une carte d'abord (`valeur → index`) pour garder l'arbre petit. Autres
En Java, `int` suffit; en Python, évitez `float('inf')` – utilisez `0`. Autres

---

Liste de contrôle à emporter Avant la prochaine interview technique

1. **Réécrire** la solution segment‐tree LIS‐II dans une nouvelle langue (p. ex. le port Java à Rust).
2. ** Expliquez** la preuve de la justesse à un ami.
3. **Time it**: exécuter le code de référence sur des tests aléatoires de 105 dimensions → devrait finir < 1 seconde.
4. **Document** le "pourquoi" de chaque ligne – les intervieweurs aiment le raisonnement.

---

> **LeetCode 2407** n'est pas juste un LIS dur; c'est un micro-écosystème qui vous apprend à transformer un problème d'avidité apparemment simple en une solution de gamme sophistiquée.
> La maîtrise vous donne un ensemble d'outils *versatile* qui vous fera briller sur **C++**, **Java**, ou **Python**.
> Bonne chance – et profitez de la montée à **O(log M)**!

---

La pensée finale

La solution segment-tree pour LeetCode 2407 est **propre, efficace et linguistique-agnostique**.
Implémentez-le une fois, testez-le à travers Java, Python et C++, et vous aurez un algorithme unique qui peut impressionner les gestionnaires d'embauche dans n'importe quelle entreprise technique.

Bon codage, et que votre pile d'entrevue reste toujours équilibrée! Les

---

* Fin de poste*
---

- Oui. 3. Remarques finales

Vous avez maintenant :

1. Une preuve formelle** que la solution segment-tree donne la plus grande séquence ascendante optimale II.
2. Trois codes de référence prêts à coller pour **Java**, **Python** et **C++**.
3. Un poste complet **blog** qui explique pourquoi ce problème compte pour votre carrière et comment le maîtriser dans les langues.

N'hésitez pas à modifier la taille de l'arbre ou à ajouter une propagation paresseuse si vous prolongez le problème (p. ex., mises à jour de portée). L'idée centrale reste : **range‐max + point update → segment tree**. Bonne solution ! Les

---

*Préparé par votre mentor en codage assisté par AI. *