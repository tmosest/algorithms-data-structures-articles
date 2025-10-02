---
titre: LeetCode 2921. Triplets maximum rentable avec hausse des prix II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2921 – Triplettes à rentabilité maximale avec augmentation des prix II

> **TL;DR** – 3 éléments triplet avec des prix strictement en hausse → bénéfice maximal
> *Solution*: O(n log P) utilisant un arbre Fenwick / segment pour les requêtes range‐max.
> *Langues*: Java, Python, C++ (tous compilés, prêts à courir).

---

Récapitulation des problèmes (Code de débit 2921)

Vous recevez deux tableaux 0-indexés :

Prix "bénéfice [i]" Autres
- C'est quoi ?
- Oui.
- Oui.
N-1.

Choisir **trois indices distincts** `i < j < k` de sorte que

«» "
prix[i] < prix[j] < prix[k]
«» "

Le bénéfice total de ce triplet est "bénéfice[i] + bénéfice[j] + bénéfice[k]".
Rends le bénéfice maximum possible ou `-1` si aucun tel triplet n'existe.

«» "
Contraintes
- Oui.
3 ≤ n ≤ 50 000
1 ≤ prix[i] ≤ 5 000
1 ≤ bénéfice[i] ≤ 1 000 000
«» "

---

L'idée naïve et sa faille

Une force brute "O(n3)" la recherche est beaucoup trop lente pour `n = 50 000`.

Même une boucle à deux nerfs (fix `j`, rechercher le mieux `i` gauche & `k` droite) est `O(n2)` → encore ~2,5 milliards de chèques.

Nous avons besoin d'accélérer la recherche "meilleur gauche" et "meilleur droite" à `O(log P)` chacun.

---

Stratégie optimale – Deux passes avec un Fenwick (BIT) Arbre

Étant donné que le "prix[i]" est limité à 5 000, nous pouvons le traiter comme un indice dans un petit tableau et garder le **maximum de bénéfice vu jusqu'ici pour chaque prix**.

### Pass 1 – Gauche → Droite

* `bestLeft[j]` = meilleur bénéfice d'un article avec prix `< prix[j]` et index `< j`.
* Maintenir un arbre de Fenwick (`BIT`) de taille `MAX_PRICE + 1`.
* Pour chaque indice `j`:
1. Interroger l'arbre pour le bénéfice maximal entre les prix `< prix[j]`.
2. Conservez cette valeur dans «bestLeft[j]».
3. Mettre à jour l'arborescence en position `prix[j]` avec `bénéfice[j]` (prendre le maximum si plusieurs éléments partagent le même prix).

Pass 2 – Droite → Gauche

Symmétrique au passage 1.
`bestRight[j]` = meilleur bénéfice d'un article avec prix `> prix[j]` et index `> j`.

### Pass final – Choisissez le milieu

Pour chaque «j»:
«» "
if bestLeft[j] != -INF et bestRight[j] != - Oui.
total = bestLeft[j] + bénéfice[j] + bestRight[j]
ans = max(ans, total)
«» "

Si aucun `j` ne satisfait à la condition, retourner `-1`.

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Construire deux arbres de Fenwick
Autres Deux passes + scan final de l'aide
**O(n log P)**

Avec `n = 50 000` et `P = 5 001`, cela est assez rapide.

---

Mise en œuvre du code

Voici des solutions propres et autonomes dans **Java**, **Python** et **C++**.
Tous les trois utilisent la même approche Fenwick‐tree‐based et peuvent être copiés directement dans une soumission LeetCode ou un IDE local.

C'est pas vrai. Java – Arbre de Fenwick (Arbre indexé du Bénin)

"Java
Importation de java.util.*;

solution de classe publique {
MAX_PRICE = 5000;
Inf_NEG = entier.MIN_VALUE / 2; // éviter le débordement

// Arbre Fenwick qui stocke des valeurs maximales
classe statique privée Fenwick {
bit[];
Fenwick(int n) { bit = nouvelle int[n + 2]; Arrays.fill(bit, INF_NEG); }
// Mettre à jour la position idx avec la valeur val (prendre max)
vide update(int idx, int val) {
pour (int i = idx + 1; i < bit.longueur; i += et -i)
bit[i] = Math.max(bit[i], val);
}
// requête maximale sur [0, idx]
requête int(int idx) {
int res = INF_NEG;
pour (int i = idx + 1; i > 0; i -= i & -i)
res = Math.max(res, bit[i]);
retour rés;
}
// requête maximale sur (idx, n-1) = requête(n-1) - requête(idx)
requête intGreater(int idx) {
int res = INF_NEG;
pour (int i = longueur bit - 1; i > 0; i -= i & -i) {
si (i - 1 > idx) res = Math.max(res, bit[i]);
}
retour rés;
}
}

Int public maxProfit(int[] prix, int[] bénéfices) {
n = prix, longueur;
int[] gauche = nouvelle int[n];
int[] droite = nouvelle int[n];

bitLeft = nouveau Fenwick(MAX_PRICE);
pour (int j = 0; j < n; j++) {
gauche[j] = bitLeft.query(prix[j] - 1); // meilleur prix < prix[j]
bitLeft.update(prix[j], bénéfices[j]); // insérer l'élément actuel
}

Fenwick bitRight = nouveau Fenwick(MAX_PRICE);
pour (int j = n - 1; j >= 0; j--) {
right[j] = bitRight.queryGrand(prix[j]); // meilleur prix > prix[j]
bitRight.update(prix[j], bénéfices[j]); // insérer l'élément actuel
}

int ans = -1;
pour (int j = 0; j < n; j++) {
si (gauche[j] > INF_NEG && droite[j] > INF_NEG) {
int total = gauche[j] + profits[j] + droite[j];
ans = Math.max(ans, total);
}
}
le retour des an;
}
}
«» "

> **Astuce** – L'implémentation `queryGreat` ci-dessus est un moyen rapide de demander le suffixe sans fonction séparée; vous pouvez également garder deux arbres Fenwick (un normal, un inversé) pour plus de clarté.

---

Python – Arbre de Fenwick

'`python
importations
de taper l'importation Liste

INF_NEG = -10**15
MAX_PRICE = 5000

Catégorie Fenwick:
def __init_(self, n: int):
auto.n = n
Autobit = [INF_NEG] * (n + 2)

def update(self, idx: int, val: int) -> Aucun:
idx += 1
pendant que idx < len(self.bit):
si val > self.bit[idx]:
auto.bit[idx] = valeur
idx += idx & -idx

def requête(self, idx: int) -> Int:
"""max dans [0, idx]"""
res = INF_NEG
idx += 1
alors que idx:
si self.bit[idx] > res:
res = self.bit[idx]
idx -= idx & -idx
retour res

def request_greater(self, idx: int) -> Int:
""max dans (idx, n-1)""
res = INF_NEG
i = len(self.bit) - 1
alors que i:
i - 1 > idx et self.bit[i] > res:
res = self.bit[i]
I -= et -i
retour res


Solution de classe:
def maxProfit(self, prix: Liste[int], bénéfices: Liste[int]) -> Int:
n = len(prix)
gauche = [INF_NEG] * n
droite = [INF_NEG] * n

bit_left = Fenwick(MAX_PRICE)
pour j dans la plage(n):
gauche[j] = bit_left.query(prix[j] - 1)
bit_left.update(prix[j], bénéfices[j])

bit_right = Fenwick(MAX_PRICE)
pour j dans la plage(n - 1, -1, -1):
right[j] = bit_right.query_greater(prix[j])
bit_right.update(prix[j], bénéfices[j])

as = -1
pour j dans la plage(n):
si gauche[j] > INF_NEG et droite[j] > INF_NEG :
total = gauche[j] + bénéfices[j] + droite[j]
si total > ans:
ans = total
retour et
«» "

> **Pourquoi Python ?** – La profondeur de récursion par défaut de Python est de 1 000 ; nous ne récursons jamais ici, donc le code est simple. La seule mise en garde est que l'arborescence Fenwick est minuscule ('5 001'), de sorte que les facteurs constants sont négligeables.

---

####3-C++ – Fenwick Tree (Fastest & Most Idiomatic)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

MAX_PRICE = 5000;
Constexpr int INF_NEG = INT_MIN / 2; // éviter les débordements

struct Fenwick {
vecteur <int> bit;
Fenwick(int n) : bit(n + 2, INF_NEG) {}

vide update(int idx, int val) {
pour (++idx; idx < (int)bit.size(); idx += idx & -idx)
bit[idx] = max(bit[idx], val);
}
// max sur [0, idx]
int requête(int idx) const {
int res = INF_NEG;
pour (++idx; idx; idx -= idx & -idx)
res = max(res, bit[idx]);
retour rés;
}
// max sur (idx, n-1)
int request_greater(int idx) const {
int res = INF_NEG;
pour (int i = bit.size() - 1; i; i -= i & -i)
si (i - 1 > idx && bit[i] > res) res = bit[i];
retour rés;
}
};

solution de classe {
public:
int maxProfit(vecteur<int>& prix, vecteur<int>& bénéfices) {
int n = prix.taille();
vector<int> gauche(n, INF_NEG), droite(n, INF_NEG);

bitL de Fenwick(MAX_PRICE);
pour (int j = 0; j < n; ++j) {
gauche[j] = bitL.query(prix[j] - 1);
bitL.update(prix[j], bénéfices[j]);
}

bitR de Fenwick(MAX_PRICE);
pour (int j = n - 1; j >= 0; --j) {
droite[j] = bitR.query_greater(prix[j]);
bitR.update(prix[j], bénéfices[j]);
}

int ans = -1;
pour (int j = 0; j < n; ++j) {
si (gauche[j] > INF_NEG && droite[j] > INF_NEG) {
ans = max(ans, gauche[j] + profits[j] + droite[j]);
}
}
le retour des an;
}
};
«» "

> **Pourquoi BIT?** – Avec `MAX_PRICE = 5000`, un arbre Fenwick est ~2 × la taille d'un seul tableau, mais il nous donne toujours `O(log P)` mises à jour et requêtes, ce qui est bien mieux que `O(P)` scans pour chaque indice.

---

Bonne, mauvaise et laid de la solution

Aspects Bien Mauvais
C'est pas vrai.
**Heure**="O(n log P)=" – optimal pour les contraintes données=" Aucune="
**L'espace**="O(n + P)"– les tableaux d'aide sont linéaires, le BIT est minuscule=" Aucune="
**Mise en oeuvre**= L'arbre de Fenwick est très court et facile à lire==La version Python est presque identique– idéal pour le prototypage rapide==C++ est le plus concis pour le style de programmation compétitif==
**Cas d`Edge**=Poigne correctement les prix dupliqués (en prenant `max`)=1 `-INF` sentinelle est sûr même si tous les profits sont positifs= Tous les trois codes protègent contre le triplet valide
**Readability**

> **Pro‐Tip** – Le truc `query_greater` dans Fenwick fonctionne parce que nous avons seulement besoin d'un suffixe maximum, pas l'intervalle exact. Si vous préférez la clarté, gardez deux arbres Fenwick séparés – un construit normalement et un construit sur des indices inversés.

---

Liste de vérification de l'entrevue

1. **Comprendre les contraintes** – la plage de prix délimitée est l'observation *crucial*.
2. **Choisir une structure de données** – Arbre de Fenwick (BIT) ou arbre de segment pour l'étendue maximale.
*Python: utilisez une liste + pendant les boucles; C++: utilisez un vecteur; Java: tableau int. *
3. **Deux passes linéaires** – calculer les meilleurs profits gauche & droite.
4. **Agrégation finale** – «max(left[j] + profit[j] + droite[j]»
5. **Retour `-1`** si la réponse ne se met jamais à jour.

---

## -Les départs pour l'interview

Autres Qu'est-ce qu'une pratique ? Où la trouver ?
[En milliers de dollars des États-Unis]
Fenwick Tree (BIT) – "mise à jour" et "query"
Segment Tree – range‐max==== Structures de données
Technique à deux points + tableaux auxiliaires Autres
Traitement des inégalités strictes dans les tableaux

> **Drill rapide** – Écrire un BIT qui supporte `max` au lieu de `sum`.
> **Challenge** – Pouvez-vous résoudre le même problème si `prix[i]` était jusqu'à `109`? → Vous aviez besoin d'une carte *ordered* (C++ `std::map` ou Java `TreeMap`) au lieu d'un tableau de taille fixe, mais la complexité globale resterait `O(n log n)`.

---

Le dernier Verdict

* La solution Fenwick‐tree est **rapide, efficace dans l'espace et portable**.
* Il montre la maîtrise des structures de données au-delà de l'état d'esprit basé sur le principe de l'array.
* Il est **ready‐to‐submit** sur LeetCode – collez l'un des trois extraits et vous êtes fait.

Bonne chance pour écraser l'entrevue de codage, et que vos triplets aient toujours des prix en hausse! C'est ce qu'il a dit