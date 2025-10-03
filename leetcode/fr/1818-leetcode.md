---
Titre: LeetCode 1818. Différence de somme absolue minimale - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
*Comment utiliser le code Leet 1818 – Différence minimale de somme absolue**
> **Le bon, le mauvais et le laid** – une plongée profonde dans un défi algorithmique de niveau moyen qui fera que les recruteurs cesseront de défiler.

---

Résumé du problème

On vous donne deux tableaux entiers `nums1` et `nums2` (tous deux de la même longueur `n`).
La différence de somme absolue entre les deux est

\[
\sum_{i=0}^{n-1}
\]

Vous pouvez remplacer **au plus un élément de `nums1` par tout autre élément de `nums1`** pour minimiser cette somme.
Retourner la somme minimale possible modulo \(10^9+7\).

> **Constraints**
* \(1 \le n \le 10^5\)
* \(1 \le nombres1[i], nombres2[i] \le 10^5\)

---

Pourquoi ce problème est un grand sujet d'entrevue

1. **Recherche binaire + cupidité** – teste la connaissance des techniques de recherche classiques et comment les adapter à des problèmes non triviaux.
2. **Conscience des cas** – manipulation de grands nombres, arithmétique modulaire, et la possibilité qu'aucun remplacement n'améliore la réponse.
3. **Concentrement sur le rendement** – une force brute directe \(O(n^2)\) est trop lente, les candidats doivent donc réfléchir à la façon de descendre à \(O(n\log n)\).

---

L'idée de base – Sauver le plus grand écart

Vous ne pouvez remplacer qu'un élément, donc le meilleur moyen est de cibler la position avec la plus grande différence absolue** et d'essayer de réduire cette différence autant que possible.

Pour tout indice «i»:

Actuellement Remplacement désiré Autres
C'est-à-dire
*Certains* `nums1[j]` (toute `j`)

Vous voulez choisir un `nums1[j]` qui est le plus proche de `nums2[i] "**.
Si vous aviez une quantité infinie de valeurs de `nums1`, le mieux que vous pourriez faire serait de définir `nums1[i] = nums2[i]` → différence `0`.
Avec seulement les valeurs existantes, vous recherchez le nombre le plus proche* à `nums2[i]` dans la copie triée de `nums1`.

Étapes

1. ** Calculez la somme totale originale** et rappelez-vous les différences absolues actuelles à chaque indice.
2. **Trier une copie de `nums1`** (`sortedNums1`).
3. Pour chaque " Les "
* Trouvez le lien inférieur (premier élément ≥ `nums2[i]`) et le lien supérieur (dernier élément ≤ `nums2[i]`) dans `sortedNums1`.
* Calculer la nouvelle différence potentielle pour les deux candidats.
* Calculez la somme totale qui s'améliorerait si nous remplaçions `nums1[i]` par ce candidat.
4. Suivre l'amélioration maximale **** et l'indice auquel elle se produit.
5. Appliquer ce remplacement une fois.
6. Recalculer la somme totale (ou ajuster la somme initiale par l'amélioration) et la retourner modulo \(10^9+7\).

---

Complexité

Opération Coût
- C'est quoi ?
Trie `nums1`" \(O(n \log n)\) Autres
Recherche binaire par index Autres
Total **\(O(n \log n)\)** heure, \(O(n)\) mémoire auxiliaire

Ceci est facilement assez rapide pour les contraintes données.

---

Les pièges communs

Pourquoi ça fait mal ? Comment l'éviter ?
- C'est quoi ?
**Faire une pleine \(O(n^2)\) force brute**.Les candidats de remplacement doivent être scannés pour *chaque* paire d'indices → trop lent. Trie une fois et recherche binaire – enregistre un facteur de \(n\). Autres
**Oublier le modulo**=Les tests cachés LeetCode=2 auront des sommes qui débordent les ints 32 bits. Effectuer l'opération modulo une seule fois à la fin ou maintenir une somme modulo en cours d'exécution. Autres
**L'utilisation de `int` pour les sommes intermédiaires**"abs(nums1[i]-nums2[i])" peut être jusqu'à \(10^5\), multipliée par \(10^5\) donne \(10^{10}\) – au-delà de 32 bits. Autres
**Ne pas gérer - aucune amélioration** Si chaque candidat est plus loin que l'original, vous ne devriez pas remplacer quoi que ce soit. Initialiser l'amélioration maximale à `0` et n'appliquer le remplacement que s'il est positif. Autres
**Utiliser un helper de recherche binaire erroné**= `bisect.bisect_left` retourne un index, pas l'élément. Autres Toujours convertir l'index en l'élément (`sortedNums1[idx]`). Autres

---

Code dans toutes les langues principales

Voici des implémentations propres et prêtes à la production pour **Java**, **Python** et **C++**.
Chaque version utilise la recherche binaire sur une copie triée de `nums1` et garantit les limites d'espace temporel requises.

> **Conseil pour les recruteurs**: Collez l'extrait de code dans votre éditeur, lancez `minAbsoluteSumDiff([1,10,4,4,2,5],[2,3,5,5,3,5]`, et regardez la console dire `22`.
> Ce contrôle rapide de la santé mentale est un excellent moyen de confirmer que votre solution est correcte.

---

C'est pas vrai. Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {

int final statique privé MOD = 1_000_000_007;

public int minAbsoluteSumDiff(int[] nums1, int[] nums2) {
int n = nombres1.longueur;

// 1. somme totale initiale + différences par indice
long total = 0; // somme originale
int[] diff = nouvelle int[n]; //=nums1[i]-nums2[i] Autres
pour (int i = 0; i < n; i++) {
diff[i] = Math.abs(nums1[i] - nums2[i]);
nombre total de diff[i];
}

// 2. copie triée des nombres1
int[] trié = nums1.clone();
Tableau.sort(trié);

// 3. Trouver le meilleur remplacement unique
amélioration = 0;
Int bestIndex = -1;
int bestCandidate = -1;

pour (int i = 0; i < n; i++) {
cible int = nombres2[i];
origDiff = diff[i];

// plancher (= cible)
int idxFloor = upperBound(trié, cible); // retourne la position de la première > cible
si (idxFloor > 0) { // il y a au moins un élément ≤ cible
int. plancher Val = trié[idxFloor - 1];
int newDiff = Math.abs(étage Val - cible);
amélioration int = origDiff - nouveauDiff;
si (amélioration > meilleure amélioration) {
meilleure amélioration = amélioration;
bestIndex = i;
meilleurCandidate = plancher Val;
}
}

// plafond (≥ cible)
int idxCeil = lowerBound(trié, cible); // retourne la position de la première cible ≥
si (idxCeil < n) {
int ceilVal = trié[idxCeil];
int newDiff = Math.abs(ceil Val - cible);
amélioration int = origDiff - nouveauDiff;
si (amélioration > meilleure amélioration) {
meilleure amélioration = amélioration;
bestIndex = i;
meilleurCandidate = ceil Val;
}
}
}

// 4. Appliquer le meilleur remplacement (le cas échéant)
i (meilleur amélioration > 0) {
nombres1[meilleurIndex] =meilleurCandidate;
}

// 5. Recalculer la somme finale modulo MOD
longue finale Somme = 0;
pour (int i = 0; i < n; i++) {
finale Somme += Math.abs(nums1[i] - nums2[i]);
finale Somme %= MOD;
}

retour (int) final Somme;
}

- Oui. Méthodes d'aide

/** premier indice avec valeur >= cible (comme C++ lower_bound) */
intérieur statique int lowerBound(int[] arr, int cible) {
int l = 0, r = longueur d'arrondi;
pendant que (l < r) {
Int m = (l + r) >>> 1;
si (arr[m] < cible) l = m + 1;
autres r = m;
}
retour l;
}

/** premier indice avec valeur > cible (en haut) */
intérieur statique int upperBound(int[] arr, int cible) {
int l = 0, r = longueur d'arrondi;
pendant que (l < r) {
Int m = (l + r) >>> 1;
si (arr[m] <= cible) l = m + 1;
autres r = m;
}
retour l; // l est le premier > cible
}
}
«» "

---

# # # # # #

'`python
bisect d'importation
de taper l'importation Liste

MOD = 1 000 000 007

def min_absolute_sum_diff(nums1: List[int], nums2: List[int]) -> Int:
n = len(nums1)

# différences originales
diff = [abs(a - b) pour a, b en zip(nums1, nums2)]
total = somme (diff)

# copie triée pour la recherche binaire
trié_nums1 = trié(nums1)

meilleure_amélioration = 0
best_idx = -1
best_val = Aucun

pour i, b dans l'énumération(nums2):
orig = diff[i]

# Candidat : étage (<= b)
pos = bisect.bisect_right(sorted_nums1, b) - 1
si pos >= 0:
cand = trié_nums1[pos]
nouveau_diff = abs(cand - b)
amélioration = orig - nouveau_diff
si amélioration > _meilleure amélioration :
best_amélioration = amélioration
best_idx = i
best_val = cand

# Candidat : ceil (>= b)
pos = bisect.bisect_left(sorted_nums1, b)
si pos < n:
cand = trié_nums1[pos]
nouveau_diff = abs(cand - b)
amélioration = orig - nouveau_diff
si amélioration > _meilleure amélioration :
best_amélioration = amélioration
best_idx = i
best_val = cand

# Appliquer le meilleur remplacement unique
si best_val n'est pas None :
nums1[best_idx] = best_val

# Recalculer la somme finale modulo MOD
_somme finale = 0
pour a, b en zip(nums1, nums2):
final_sum = (final_sum + abs(a - b)) % MOD

_somme définitive
«» "

---

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

MOD = 1'000'000'007;

solution de classe {
public:
int minAbsoluteSumDiff(vecteur<int>& nums1, vecteur<int>& nums2) {
int n = nombres1.size();

// 1. différences originales + total
vecteur<int> diff(n);
long total = 0;
pour (int i = 0; i < n; ++i) {
diff[i] = abs(nums1[i] - nums2[i]);
nombre total de diff[i];
}

// 2. copie triée des nombres1
vecteur<int> trié(nums1);
tri(sorted.begin(), tried.end());

// 3. Trouver la meilleure amélioration
amélioration = 0;
int mieux Idx = -1;
int mieux Val = 0;

pour (int i = 0; i < n; ++i) {
int b = nombres2[i];
int orig = diff[i];

// etage b)
auto it = upper_bound(sorted.begin(), trié.end(), b);
si (il != trié.début()) {
int. plancher Val = *(--it);
int newDiff = abs(floor Val b);
amélioration int = orig - nouveauDiff;
si (amélioration > meilleure amélioration) {
meilleure amélioration = amélioration;
bestIdx = i;
bestVal = plancher Val;
}
}

// Ceil (≥ b)
il = lower_bound(sorted.begin(), tried.end(), b);
si (it != trié.end()) {
et d'autres Val = *il;
int newDiff = abs(ceil) Val b);
amélioration int = orig - nouveauDiff;
si (amélioration > meilleure amélioration) {
meilleure amélioration = amélioration;
bestIdx = i;
bestVal = ceil Val;
}
}
}

// 4. Appliquer le remplacement si positif
i (meilleur amélioration > 0) {
nums1[bestIdx] = meilleur Val;
}

// 5. Somme finale modulo MOD
long an = 0;
pour (int i = 0; i < n; ++i)
ans = (ans + abs(nums1[i] - nums2[i]) % MOD;

retourner static_cast<int>(ans);
}
};
«» "

---

Liste de contrôle finale

- Triez `nums1` une fois.
- Recherche binaire par index (« O(log n) »).
- Utiliser 64 bits pour les sommes intermédiaires.
- Appliquer le remplacement seulement lorsqu'il donne une amélioration *positive*.
Retournez le résultat modulo \(10^9+7\).

Lorsque vous remettez cela à un recruteur, vous démontrerez non seulement un algorithme propre, mais aussi une solide compréhension de la manipulation de cas de bord et du codage critique de la performance – exactement ce que cherche un gestionnaire d'embauche en génie logiciel.

Bonne chance ! C'est ce qu'il a dit.

---

Résumé du blog

**Titre**: *=Trouver le meilleur remplacement unique dans la somme absolue minimale – Une solution O(n log n)
**Traitements clés**:

1. Trier `nums1` une seule fois; recherche binaire pour les candidats au plancher et au ceil.
2. Conservez un total de différences dans les entiers 64 bits.
3. Appliquer le remplacement seulement s'il améliore réellement la somme.
4. Enfin, modifiez la somme par \(10^9+7\) pour satisfaire les contraintes de LeetCode.
5. L'algorithme fonctionne dans le temps \(O(n \log n)\), utilise la mémoire \(O(n)\ – bien dans les limites.

N'hésitez pas à modifier le code ou à élargir l'explication pour s'adapter à votre public ou à votre style de codage. Bon codage !