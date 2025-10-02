---
titre: LeetCode 3520. Seuil minimum pour le nombre de paires d'inversion -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 3520 – Seuil minimal pour le nombre de paires d'inversions
**Cible Public:** Ingénieurs, algorithmes et données de front et de back-end Les passionnés de structure, les candidats se préparant pour Java, Python ou C++.
** Pourquoi lire ça ? * *
- Maîtriser un problème *medium* LeetCode qui apparaît fréquemment dans la conception du système et les rondes d'entrevue.
- Apprenez à combiner **recherche binaire** avec un **Fenwick Tree** (BIT) pour une solution optimale.
- Prenez connaissance de *bons, mauvais, laids* compromis dont les recruteurs aiment discuter.
- Voir code propre, prêt à la production en **Java**, **Python** et **C++**.

---

Déclaration du problème (simplifiée)

Avec un tableau entier `nums` et un entier `k`, trouvez le plus petit entier `min_threshold` de telle sorte qu'il y ait ** au moins des paires d'inversion `k`** `(i, j)` satisfaisant:

Description
C'est pas vrai.
L'indice de gauche est plus petit
"nums[i] > nums[j]" Une plus grande valeur à gauche
La différence est limitée par le seuil "x" Autres

Retour `-1` si ce seuil n'existe pas.

---

Les idées fondamentales

Idées Pourquoi ça marche
C'est pas vrai.
**Binary Search on `x`**=Le nombre de paires valides est monotonique par rapport au seuil: un seuil plus grand ne peut ajouter que des paires. Autres
**Fenwick Tree (Binary Indexed Tree)** Active les requêtes de somme de la plage *log-time* sur un ensemble dynamique de nombres. Nous insérons chaque `nums[i]` en scannant de gauche à droite. Autres
**Compression coordonnée**=Les arbres de Fenwick ont besoin d'indices dans `[1, N]`. Nous comprimons les valeurs potentiellement énormes (`= 1e9`) à une plage d'indice dense. Autres

---

Solution étape par étape

1. **Pré-processus**
- Trouvez `minVal` et `maxVal`. L'espace de recherche pour `x` est `[0, maxVal - minVal]`.
- Créer une liste unique triée `uniq` de toutes les valeurs du tableau pour la compression.

2. **Recherche binaire**
Texte
pendant la période (faible < élevée):
milieu = (faible + élevé) // 2
si check(mid): // au moins paires k
haute = moyenne
Sinon:
faible = milieu + 1
retourner bas si coche(faible) sinon -1
«» "

3. **Fonction de contrôle (O(n log n))* *
- Initialiser un arbre Fenwick vide de taille `uniq.size()`.
- Numériser de gauche à droite :
* `idx` = indice de `nums[i]` dans `uniq`.
* `bound` = indice de la plus grande valeur `= nombres[i] + milieu` dans `uniq`.
* `cnt += tree.query(idx+1, lied+1)` – nombre de valeurs antérieures qui satisfont à la condition de différence.
* `tree.add(idx+1, 1)« – insérer la valeur courante.
- Arrêter tôt si `cnt ≥ k` (aide avec d'énormes `k`).
- Retourner `cnt ≥ k`.

---

Mise en œuvre du code

> Toutes les implémentations utilisent **long** (`int64` en C++) pour les nombres de paires pour éviter les débordements.

### Java

"Java
Importation de java.util.*;

solution de classe publique {
// Coordination du tableau de compression
Liste privée<entier> uniq;

public int minThreshold(int[] nums, int k) {
int minVal = entier. MAX_VALUE, maxVal = entier.MIN_VALUE;
pour (int v : nombres) {
minVal = Math.min(minVal, v);
max Val = Math.max(maxVal, v);
}

uniq = nouvelle liste d'array<>();
Définir<integer> set = nouveau HashSet<>();
pour (int v: nums) set.add(v);
uniq.addAll(set);
Collections.sort(uniq);

Int low = 0, high = max Val - minVal;
pendant que (faible < haut) {
int milieu = faible + (élevé - faible) / 2;
si (en chiffres, k, milieu) élevé = milieu;
Autre faible = milieu + 1;
}
check retour(nums, k, low) ? faible : -1;
}

contrôle booléen privé(int[] nombres, int k, int x) {
int m = uniq.size();
bit de Fenwick = nouveau Fenwick(m);
longue cnt = 0;

pour (int v : nombres) {
int idx = lowerBound(uniq, v);
int up = upperBound(uniq, v + x) - 1; // 0
si (up >= idx) {
cnt += bit.rangeSum(idx + 1, up + 1); // BIT est basé sur 1
si (cnt >= k) retourne true; // sortie anticipée
}
bit.add(idx + 1, 1); // insérer
}
retour cnt >= k;
}

/* Limite inférieure / supérieure standard sur une liste triée */
Int privé lowerBound(Liste <Integer> arr, int cible) {
int l = 0, r = arr.size();
pendant que (l < r) {
Int milieu = (l + r) >>> 1;
si (arr.get(mid) < cible) l = milieu + 1;
r = milieu;
}
retour l;
}

Int privé upperBound(Liste <Intégrer> arr, int cible) {
int l = 0, r = arr.size();
pendant que (l < r) {
Int milieu = (l + r) >>> 1;
si (arr.get(mid) <= cible) l = milieu + 1;
r = milieu;
}
retour l;
}

/* Mise en oeuvre de l'arbre Fenwick (1-basé) */
classe statique privée Fenwick {
arbre intérieur final privé;
Fenwick(int n) { arbre = nouvelle int[n + 2]; }

vide add(int idx, int delta) {
pour (int i = idx; i < arbre. longueur; i += i & -i) {
arbre[i] += delta;
}
}

Int sum(int idx) {
int res = 0;
pour (int i = idx; i > 0; i -= i & -i) {
res += arbre[i];
}
retour rés;
}

Int gamme Sum(int l, int r) { // inclusivement
somme(r) de retour - somme(l - 1);
}
}
}
«» "

> **Pourquoi c'est prêt pour la production* *
> - Les limites de recherche binaire sont serrées (`maxVal - minVal`).
> - Fin anticipée dans `check()` économise du temps pour les grands `k`.
> - "long" pour le comptage, sûr pour 104 éléments.

---

Python

'`python
de bisect importer bisect_left, bisect_right
de taper l'importation Liste

Solution de classe:
def minThreshold(self, nombres: List[int], k: int) -> Int:
uniq = trié(set(nums))
faible, élevée = 0, max(nums) - min(nums)

def check(x: int) -> C'est vrai.
bit = [0] * (len(uniq) + 2)
def add(idx: int, val: int) -> Aucun:
pendant que idx < len(bit):
bit[idx] += valeur
idx += idx & -idx

def prefix(idx: int) -> Int:
s = 0
alors que idx:
s += bit[idx]
idx -= idx & -idx
retour s

cnt = 0
pour v en chiffres:
l = bisect_left (uniq, v)
r = bisect_right(uniq, v + x) - 1
si r >= l:
cnt += préfixe(r + 1) - préfixe(l)
si cnt >= k:
retour Vrai # sortie précoce
ajouter(l + 1, 1)
retour cnt >= k

alors que faible < élevé:
milieu = (faible + élevé) // 2
en cas de vérification (milieu):
haute = moyenne
Sinon:
faible = milieu + 1

retourner bas si coche(faible) sinon -1
«» "

> **Fast & Clean** – Utilise la bibliothèque standard `bisect` pour la compression et un petit arbre de fenwick aligné.

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int minThreshold(vector<int>& nums, int k) {
int minV = *min_element(nums.begin(), nums.end());
int maxV = *max_element(nums.begin(), nums.end());
uniq.assign(nums.begin(), nums.end());
(uniq.begin(), uniq.end());
uniq.erase(unique(uniq.begin(), uniq.end()), uniq.end());

Int low = 0, high = maxV - minV;
pendant que (faible < haut) {
int milieu = faible + (élevé - faible) / 2;
si (en chiffres, k, milieu) élevé = milieu;
Autre faible = milieu + 1;
}
check retour(nums, k, low) ? faible : -1;
}

particulier:
vecteur<int> uniq;

Vérification de la bool(vecteur const<int>& nums, int k, int x) {
int m = uniq.size();
bit(m) de Fenwick;
long cnt = 0;

pour (int v : nombres) {
int l = lower_bound(uniq.begin(), uniq.end(), v) - uniq.begin();
int r = upper_bound(uniq.begin(), uniq.end(), v + x) - uniq.begin() - 1;
si (r >= l) {
cnt += bit.rangeSum(l + 1, r + 1); // BIT est basé sur 1
si (cnt >= k) retourne true;
}
bit.add(l + 1, 1);
}
retour cnt >= k;
}

*/
struct Fenwick {
vecteur<int> arbre;
Fenwick(int n) : arbre(n + 2, 0) {}
vide add(int idx, int val) {
pour l'arbre (; idx < (int)tree.size(); idx += idx & -idx)[idx] += val;
}
Int sum(int idx) {
int res = 0;
pour (; idx > 0; idx -= idx & -idx) res += arborescence[idx];
retour rés;
}
Int gamme Somme(int l, int r) { somme(r) de retour - somme(l - 1); } // inclusivement
};
};
«» "

> ** Faits saillants**
> - Utilise les STL.
> - La classe d'arbres Fenwick est minimaliste mais entièrement sécuritaire.
> - "longtemps" est utilisé pour "cnt".

---

Les bons, les mauvais, les affreux

Aspect du bien
- C'est quoi ?
**Complexité du temps**= `O(log(maxVal - minVal) * n log n)` – fonctionne rapidement pour `n ≤ 104`.= Le facteur constant peut être élevé si vous reconstruisez naïvement l'arbre à chaque fois. Erreurs hors-par-un dans les indices BIT ou dans la condition de fin de recherche binaire. Autres
Autres **Complexité spatiale**="O(n)` pour l'arbre Fenwick + `O(unique)` pour la compression. La compression peut gâcher la mémoire pour très petite `n` (mais c'est très bien). Le traitement des indices 1-basés versus 0-basés dans les trois langues est sujet à erreur. Autres
**Readability**=La division de la logique en fonctions de recherche binaire `check()` + helper est propre. Certaines personnes interrogées écrivent tout en une seule boucle, ce qui rend la lecture difficile. La logique de compression de coordonnées est souvent cachée derrière une ligne (`vector<int> uniq = trié(set(nums))`) – elle peut être mal comprise par les nouveaux arrivants. Autres
**Robustness**. Sortie précoce lorsque `cnt ≥ k` protège contre le travail inutile. Dans le cas des bords, lorsque `maxVal=minVal`, la réponse est toujours `0`. Autres

---

Liste de contrôle des points d'entrevue

Sujet Ce que le recruteur veut
C'est ce qui s'est passé.
**Monotonicité**= Comprendre pourquoi la recherche binaire est sûre. Si j'augmente `x`, l'ensemble de paires valides ne peut que croître, jamais rétrécir. Autres
**L'arbre de Fenwick**L'arbre de Fenwick permet de démontrer la connaissance des requêtes de somme de plage. Autres
**Compression** Nous maçons chaque nombre distinct à un index dense; cela maintient l'arbre Fenwick petit. Autres
**Cas d'Edge**"k" plus grand que le total des paires, "nums" avec toutes les valeurs égales, très petit `n`. Autres
**Complexité** Dans l'ensemble : O(n log n log(max‐min)) 2.4 × 106 opérations pour le pire des cas 104. Autres

> **Astuce:** Dans une interview, dessinez toujours la solution sur papier d'abord, puis traduisez en code. Cela démontre *la discipline de résolution de problèmes* que les gestionnaires embauchent aiment.

---

## TL;DR (Liste de contrôle des déplacements)

1. **Recherche binaire** sur le seuil `[0, max‐min]`.
2. **Scan** `nums` gauche → droite, **insérer** chaque valeur dans un arbre de Fenwick.
3. **Query** la plage des valeurs antérieures qui sont ≤ `nums[i] + x` et > `nums[i]`.
4. **Départ précoce** si le nombre atteint `k`.
5. **Retour** le minimum "x" qui satisfait à la condition, sinon "-1".

---

Comment résoudre ce problème dans une entrevue de codage

Étape Ce que l'intervieweur vérifie
- C'est quoi ?
**Compréhension des problèmes**= Êtes-vous clair sur la définition de la paire d'inversion* et du seuil? Autres
**Esquisse de solution**= Pouvez-vous expliquer pourquoi le nombre de paires est monotonique? Autres
**Choix de la structure des données** Quelles autres structures de données pourraient être utilisées? Autres
**Manipulation d'un cas d'urgence** Avez-vous protégé contre le débordement ? Autres
**Analyse de la complexité** Autres
**Qualité du code** Autres

---

Mots-clés prêts à l'emploi

- **LeetCode 3520**
- ** paires minimales de seuils d'inversion**
- **algorithme de recherche binaire**
- **Fenwick (BIT)* *
- ** Entretien avec un ingénieur logiciel* *
- Défi de codage de Java/Python/C++**
- **optimisation de la structure des données**

N'hésitez pas à ajouter ces balises à votre lecture GitHub ou à votre blog personnel pour attirer les recruteurs à la recherche de solutions de problèmes LeetCode.

---

Bonus: Cas de test que vous devriez exécuter

"nums"" "k"" Prévu "min_threshold" Autres
- C'est quoi ?
[5, 3, 2, 4]
[10, 5, 3, 1]
[1, 1, 1, 1]
"[10, 9, 8, 7]"" "6"" "0" (toutes les inversions adjacentes satisfont déjà)"
"[2, 100000000]" "1" "9999998"

> Exécutez-les dans chaque langue pour être confiants.

---

Enveloppe

- **Bien** – Solution propre et bien structurée qui utilise seulement deux concepts classiques.
- **Bad** – Nécessite une gestion soigneuse des erreurs hors-par-un et des grandes plages de valeurs.
- **Ugly** – La subtilité des conventions de compression de coordonnées et d'indice BIT peut aller jusqu'à des développeurs aguerris.

Avec les extraits de code ci-dessus, vous êtes prêt à montrer à la fois *profondeur conceptuelle* et *codage artisanat* dans toute entrevue de codage qui inclut LeetCode 3520. Bon codage !

---