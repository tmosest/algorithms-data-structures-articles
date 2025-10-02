---
titre: LeetCode 2333. Somme minimale de la différence carrée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Le code du leet 2333 – minimum Somme de la différence carrée
C++** – Les trois solutions utilisent la même idée optimale.
Lisez aussi le **blog post** qui plonge dans le *bon, le mauvais, et le laid* de ce problème, plus l'interview-ready SEO-friendly copie.

---

Récapitulation des problèmes

Paramètre Type Contraintes
C'est quoi ?
"nums1, nums2"""int[]"""1 ≤ n ≤ 105", "0 ≤ nums[i] ≤ 105"
"k1, k2"" "int"" "0 ≤ k1, k2 ≤ 109" Autres

Vous pouvez ajouter ou soustraire `1` à tout élément de `nums1` **au plus** `k1` fois et à tout élément de `nums2` **au plus** `k2` fois.
Après toutes les modifications, retourner le **minimum possible* *

\[
\sum_{i=0}^{n-1}\bigl(\text{nums1}[i]-\text{nums2}[i]\bigr)^2
\]

Remarque : les éléments peuvent devenir négatifs.

---

Idée de base

1. **Les différences sont importantes, pas les valeurs** –
Seule la différence absolue `d =="nums1[i] - nums2[i]=" influence la différence carrée.
Chaque opération réduit une différence de `1` (en se déplaçant d'un côté vers l'autre).

2. **Greedy sur les plus grandes différences** –
Chaque diminution sur une différence `d` réduit la somme carrée de

\[
d^2 - (d-1)^2 = 2d-1
\]

Donc nous devrions toujours dépenser une opération sur la **la plus grande** différence actuelle.

3. **Traitement au lieu d'un tas** –
La différence ne peut jamais dépasser "100 000".
Conservez la fréquence de chaque différence dans un tableau de taille `100 001`.
Cela donne **O(n + maxDiff)** temps et **O(maxDiff)** espace, bien mieux qu'une file d'attente prioritaire.

4. ** Appliquer toutes les opérations** –
Il faut passer de la différence maximale vers le bas, à la différence inférieure suivante jusqu'à ce que nous manquions d'opérations ou atteignions « 0 ».

5. ** Calculer la réponse** –
Somme `freq[d] * d2` pour toutes les différences restantes.

---

Mise en œuvre

Vous trouverez ci-dessous le code prêt à la copie dans **Java**, **Python** et **C++**.

---

Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
public long minSumSquareDiff(int[] nums1, int[] nums2, int k1, int k2) {
MAX = 100_000;
int[] freq = nouveau int[MAX + 1];
longues opérations = (long) k1 + k2; // total des opérations autorisées
longue sommeDiff = 0; // somme totale des différences

// Différences de comptage
pour (int i = 0; i < nums1.longueur; i++) {
int d = Math.abs(nums1[i] - nombres2[i]);
si (d > 0) {
freq[d]++;
b) SumDiff += d;
}
}

// Si nous avons assez d'ops pour réduire tous les diffs à zéro
si (sumDiff <= ops) retourne 0L;

// Réduction de la graisse du plus gros au plus petit diff
pour (int d = MAX; d > 0 && ops > 0; d--) {
int cnt = freq[d];
Si (cnt) 0) poursuivre;
long canMove = Math.min(cnt, ops);
freq[d] -= (int) canMove;
freq[d - 1] += (int) canMove;
ops -= can Déplacer;
}

// Calculer la somme finale des carrés
résultat long = 0;
pour (int d = 0; d <= MAX; d++) {
si (freq[d] > 0) {
résultat += (long) d * d * freq[d];
}
}
le résultat du retour;
}
}
«» "

**Complexités* *

- Heure: `O(n + 100000)` → ~`O(n)`
- Espace: `O(100000)` → `O(1)` (taille constante de l'entrée)

---

Python 3

'`python
de taper l'importation Liste

Solution de classe:
def minSumSquareDiff(self, nombres1: List[int], nombres2: List[int],
k1: int, k2: int) -> Int:
MAX = 100_000
freq = [0] * (MAX + 1)
ops = k1 + k2
_diff total = 0

# Compter les différences
pour a, b en zip(nums1, nums2):
d = abs(a - b)
si d:
freq[d] += 1
total_diff += d

Si tous les diffs peuvent être éliminés
si total_diff <= ops:
retour 0

# Réduction de l'avidité
pour d dans la plage (MAX, 0, -1):
en cas d'opérations == 0:
pause
cnt = freq[d]
si cnt == 0:
poursuivre
prise = min(cnt, ops)
-= prise
freq[d - 1] += prise
ops -= prise

# Somme des carrés restants
ans = 0
pour d, cnt dans l'énumération:
si cnt:
ans += d * d * cnt
retour et
«» "

**Complexités* *

- Heure: `O(n + 100000)` → `O(n)`
- Espace: `O(100000)` → `O(1)`

---

C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long long minSumSquareDiff(vecteur<int>& nums1, vecteur<int>& nums2,
long long k1, long long k2) {
const int MAX = 100000;
vecteur<int> freq(MAX + 1, 0);
longues opérations longues = k1 + k2;
long total long Diff = 0;

// Différences de comptage
pour (size_t i = 0; i < nums1.size(); ++i) {
Int d = abs(nums1[i] - nombres2[i]);
si d) {
++freq[d];
Total général Diff += d;
}
}

si (totalDiff <= ops) retourne 0LL;

// Réduction de l'avidité par rapport aux plus grands diff vers le bas
pour (int d = MAX; d > 0 && ops > 0; --d) {
int cnt = freq[d];
si (!cnt) continue;
long mouvement = min<long long>(cnt, ops);
freq[d] -= mouvement;
freq[d - 1] += mouvement;
ops -= déménagement;
}

// Somme finale des carrés
long an = 0;
pour (int d = 0; d <= MAX; ++d) {
si (freq[d])
as += 1LL * d * freq[d];
}
le retour des an;
}
};
«» "

**Complexités* *

- Heure: `O(n + 100000)` → `O(n)`
- Espace: `O(100000)` → `O(1)`

---

Pourquoi ces solutions passent tous les tests

- **Les grandes valeurs `k`** sont traitées avec `long long`/`long`.
- **La différence maximale** est limitée par `105`, de sorte que le tableau de comptage ne déborde jamais.
- **Pas de tas** → pas de frais généraux `O(n log n)`.
- Oui. La boucle gourmande garantit que nous dépensons chaque opération sur la différence la plus précieuse.

---

Billet de blog – Les bons, les mauvais et les méchants

> **Titre**:
> **=LeetCode 2333: Maîtriser la somme minimale de la différence carrée – Une feuille de châtaigne d'entrevue**

> **Description détaillée** (SEO):
> Découvrez comment cracker LeetCode 2333 en Java, Python et C++. Comprendre le comptage avide, les cas de bord et les techniques d'entrevue pour les rôles d'ingénierie logicielle. (en milliers de dollars)

---

Introduction

LeetCodeS **Somme minimum de la différence carrée** (problème 2333) est un puzzle classique *greedy + compter*.
Les intervieweurs aiment ce problème parce qu'il teste:

- **Perspective algorithmique** (reconnaissant que seules les différences comptent).
- ** compromis entre l'espace et le temps** (tableau de comptage et file d'attente prioritaire).
- **Attention aux détails** (grandes valeurs `k`, débordement d'entier long, nombres négatifs).

- Oui. Les bonnes

Autres Ce qui est grand Pourquoi ça compte
C'est pas vrai.
**Temps linéaire** – `O(n)` – évolutive aux éléments `105`. Démontrer la capacité d'optimiser au-delà de O (n log n). Autres
**Simple structure de données** – tableau de fréquences – pas de tas, pas de bibliothèques supplémentaires. Autres Montre l'utilisation intelligente des contraintes de problème. Autres
**Cupide déterministe** – toujours optimal. Évite le retour en arrière ou DP. Autres
**Handles énorme `k`** via `long long`. Autres

C'est vrai. Les mauvais

Des pièges communs
- Oui.
Autres Oublier que `d` peut être `0` – conduit à la division par zéro dans `pow`. Passer `d==0` lors du comptage. Autres
Utiliser `int` pour `k1 + k2` lorsque `k` peut être `109`. Utiliser `long`/`long`. Autres
Relying on a priority file → `O(n log n)` and higher constant. Utiliser un tableau de comptage (taille 100 001). Autres
Autres Ne pas vérifier si les différences totales ≤ opérations → boucle gaspillée. Retour précoce `0`. Autres

C'est pas vrai. L'Ugly

Traitement des bords
- Oui.
**Toutes les différences zéro** – la réponse est `0`. Sautez le comptage et revenez tôt. Autres
**La différence maximale est de 100 000** – sécurité de l'indice de tableau. Utiliser `MAX + 1` tableau. Autres
**Les opérations dépassent la somme de la différence totale** – doivent régler tous les diffs à `0`. Sortie anticipée. Autres
** Nombres négatifs après les opérations** – non pertinents parce que seules les différences comptent. Pas besoin de manipulation spéciale. Autres

C'est vrai. Conseils de préparation à l'entrevue

Conseil Pourquoi ça impressionne
-- -- -- -- -- --
** Expliquez les économies `2d-1`** – quantifiez pourquoi le choix avide est optimal. Autres Montre une profonde perspicacité mathématique. Autres
** Contraintes de concentration** – l'utilisation d'un tableau de fréquences exploite «d ≤ 100 000». Démontre une conception efficace spécifique à un problème. Autres
Autres **Parler de la complexité** – temps `O(n)`, espace auxiliaire `O(1)`. Autres
**Montrer la couverture du cas de bord** – retour anticipé pour "total Diff <= ops`, manier `0` diffs. Autres
Autres **Offre une solution de repli** – dans les langues où le comptage des tableaux est peu pratique. Montre la polyvalence. Autres

Référence Mots clés

- Solution LeetCode 2333
- Somme minimale de la différence carrée
- entretien d'algorithme gourmand
- compter le tri par rapport à la file d'attente prioritaire
- C++ O(n) Solution LeetCode
- Java 17 LeetCode 2333
- Python LeetCode 2333
- conseils d'entretien en génie logiciel
- résolution de problèmes algorithmiques

> En tissant ces mots-clés naturellement dans le post, les recruteurs qui sont Googling -LeetCode 2333 solution ou --la somme minimale de la différence carrée - verront votre contenu élevé dans les résultats de recherche.

---

Enveloppe

*Les trois implémentations atteignent le même algorithme linéaire optimal. *
Choisissez celui qui correspond à votre langue de choix et impressionnez vos intervieweurs avec une solution propre et bien commentée.

Bon codage ! C'est ce qu'il a dit