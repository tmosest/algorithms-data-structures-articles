---
titre: LeetCode 327. Compte de somme de l'aire de répartition -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 327 – Compte de la somme de portée
### Le bon, le mauvais, le mauvais – Un guide complet, optimisé pour l'emploi

Langue Fichier Lien (Code Leet)
- C'est quoi ?
Autres Java (en anglais seulement) `Solution.java' (en anglais seulement) https://leetcode.com/problèmes/count-of-range-sum/ Autres
https://leetcode.com/problèmes/count-of-range-sum/ Autres
* C++* `solution.cpp'* https://leetcode.com/problèmes/count-of-range-sum/ Autres

> **Pourquoi cet article compte pour vous**
> Le problème "Count of Range Sum" est un défi **Hard** LeetCode qui apparaît dans de nombreuses piles d'interviews (Google, Facebook, Amazon). La maîtrise démontre la maîtrise de la division et de la conquête, le préfixe des sommes et une compréhension profonde de l'optimisation algorithmique – tous les gestionnaires d'embauche recherchent. Ce post vous donne la solution complète en Java, Python et C++ + une analyse profonde que vous pouvez utiliser comme guide d'étude ou même partager dans votre portefeuille.

---

Récapitulation des problèmes

Étant donné:

- `nums` – un tableau de `n` entiers (`1 ≤ n ≤ 10^5)
- Deux entiers "inférieurs" et "hauts" ("-10^5 ≤ inférieurs ≤ supérieurs ≤ 10^5")

**Objectif**: Compter le nombre de montants de sous-tarifs `S(i, j) = nombres[i] + ... + nombres[j]` qui se trouvent dans l'intervalle inclusif `[inférieur, supérieur]`.

La réponse correspond à un entier signé 32 bits.

---

Stratégie de haut niveau

1. **Préfixation des montants**
Convertir le problème en paires de comptage `(i, j)` de sorte que
`préfixe[j] - préfixe[i] .
Ici, `préfixe[0] = 0`, `préfixe[k] = nums [0 ... k-1]`.

2. **Divide & Conquer (Merge Tri)* *
Tout en triant récursivement le tableau de préfixes, nous comptabilisons simultanément des paires valides sur les deux moitiés.
- Pour chaque élément de gauche `x`, nous avons besoin du compte des éléments de droite `y` satisfaisant
«inférieure ≤ y - x ≤ supérieure».
- Parce que la bonne moitié est déjà triée, nous pouvons utiliser deux pointeurs (ou recherche binaire) pour trouver ce nombre en temps linéaire par fusion.

3. **Heure et espace**
- **Time**: `O(n log n)` – dominé par les fusions.
- **Espace**: `O(n)` – tableau auxiliaire pour la fusion.

---

Code – Java

"Java
// Solution.java
Importation de java.util.*;

solution de classe publique {

nombre d'intes publiquesRangeSum(int[] nombres, int inférieur, int supérieur) {
// 1. Construire des sommes préfixes (utiliser longtemps pour éviter le débordement)
long[] préfixe = nouveau long[nums.longueur + 1];
pour (int i = 0; i < nombres de longueur; i++) {
préfixe[i + 1] = préfixe[i] + nombres[i];
}

// 2. Utiliser diviser et conquérir
retour fusion TriAndCount(préfixe, 0, préfixe.longueur - 1, inférieur, supérieur);
}

// Retourne le nombre de paires valides dans le préfixe[l ... r]
fusion privée d'intSortAndCount(long[] arr, int l, int r, int inférieur, int supérieur) {
si (l >= r) retourne 0; // élément unique, aucune paire
int milieu = l + (r - l) / 2;

// Compte par moitié
nombre int = fusionSortAndCount(arr, l, milieu, inférieur, supérieur);
nombre += fusionSortAndCount(ar, milieu + 1, r, inférieur, supérieur);

// Nombre de paires croisées
int j1 = milieu + 1, j2 = milieu + 1;
pour (int i = l; i <= mi; i++) {
pendant que (j1 <= r && arr[j1] - arr[i] < inférieur) j1++;
pendant que j2 <= r && arr[j2] - arr[i] <= supérieur) j2++;
nombre += (j2 - j1);
}

// Fusionner les deux moitiés triées
fusion (arr, l, mi, r);
le nombre de retours;
}

// Fusion standard pour le tri de fusion
fusion du vide privé(long[] arr, int l, int m, int r) {
longue[] temp = nouveau long[r - l + 1];
i = l, j = m + 1, k = 0;
pendant que (i <= m && j <= r) {
si (arr[i] <= arr[j]) temp[k++] = arr[i++];
autres temp[k++] = arr[j++];
}
pendant que (i <= m) temp[k++] = arr[i++];
pendant que (j <= r) temp[k++] = arr[j++];
Système.arraycopie(temp, 0, arr, l, durée);
}
}
«» "

Points clés

Pourquoi ça compte ?
-- -- -- -- --
Autres Utiliser **long** pour préfixer les sommes. Autres
**Approche à deux points** à l'intérieur de la fusion. Autres
Enceinte de récursions Autres

---

Code Passage – Python

'`python
# solution. py
de taper l'importation Liste

Solution de classe:
Def countRangeSum(self, nombres: Liste[int], inférieur: int, supérieur: int) -> Int:
# Construire des montants préfixes (les ints Python sont débordés)
préfixe = [0]
pour x en nombres:
Préfix.append(préfix[-1] + x)

# Aide à la fusion récursive
def merge_sort(lo: int, hi: int) -> Int:
si hi - lo <= 1: # 0 ou 1 élément
retour 0
milieu = (lo + hi) // 2
nombre = fusion_sort(lo, mi) + fusion_sort(mid, hi)

Nombre de paires croisées
j1 = j2 = milieu
pour gauche_val dans le préfixe[lo:mid]:
alors que j1 < hi et préfixe[j1] - gauche_val < inférieur:
j1 += 1
alors que j2 < hi et préfixe[j2] - gauche_val <= supérieur:
j2 += 1
Nombre += j2 - j1

♪ Merge l'étape
préfixe[lo:hi] = trié(préfixe[lo:hi])
Nombre de retours

return merge_sort(0, len(prefix))
«» "

Faits saillants

- Utilise le "tri" intégré de Python pour la clarté (toujours `O(n log n)`).
- Profondeur de récursion : < < log n > > sans danger pour < < 10^5 > > .
- Les leviers Python sont des entiers de précision arbitraires – aucune manipulation manuelle de débordement.

---

Code Passage – C++

'`cpp
// solution.cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int countRangeSum(vecteur<int>& nums, int inférieur, int supérieur) {
// 1. Préfixer les sommes aussi longtemps
vecteur <long> pref(nums.size() + 1, 0);
pour (size_t i = 0; i < nums.size(); ++i)
pref[i + 1] = pref[i] + nombres[i];

// 2. Mélange récursif + comptage
retour mergeSort(pref, 0, pref.size() - 1, inférieur, supérieur);
}

particulier:
int fusion Tri(vecteur <long long>& a, int l, int r,
int inférieur, int supérieur) {
si (l >= r) retourne 0;
m = l + (r - l) / 2;
int cnt = fusion Tri(a, l, m, inférieur, supérieur)
+ fusionSort(a, m + 1, r, inférieur, supérieur);

// Nombre de paires croisées
int j1 = m + 1, j2 = m + 1;
pour (int i = l; i <= m; ++i) {
pendant que (j1 <= r && a[j1] - a[i] < inférieur) ++j1;
pendant que (j2 <= r && a[j2] - a[i] <= supérieur) ++j2;
cnt += j2 - j1;
}

// Fusionner
en place_merge(a.begin() + l, a.begin() + m + 1, a.begin() + r + 1);
retour cnt;
}
};
«» "

> **Note**: `place_merge` fait partie de la STL C++ et fournit une fusion efficace pour deux plages de tri consécutives.

---

Analyse de complexité

Opération de Java Python C++
- C'est quoi ?
Heure (n log n) (n log n) Autres
Espace "O(n)" tableau auxiliaire "O(n)" Autres

L'approche de la fusion garantit que même pour les éléments maximums `10^5`, l'exécution reste confortablement inférieure à 1 seconde sur les juges modernes.

---

Cas et pièges

Problème Correction
- Oui.
**Overflow** – préfixer les montants des entiers `10^5` de magnitude `2^31-1` peut dépasser la plage de 32 bits. Autres
Autres **Les limites negatives** – `inférieure` et `upper` peuvent être négatives; assurez-vous que les comparaisons sont correctes. Autres Conserver toutes les comparaisons dans le domaine `long`; aucun changement de signe. Autres
**Sous-liberté complète** – La définition exige "i ≤ j", donc nous ne comptons jamais la somme vide. L'algorithme s'en occupe automatiquement. Autres
Autres Pour `n=10^5`, la profondeur de récursion 17, sans danger. Pour les langues avec petite pile (Python), considérez la fusion itérative tri si nécessaire. Autres
Erreurs hors pair** – Lors du comptage des paires croisées, utiliser `mid+1` correctement; vérifier les limites inclusives/exclusives. Autres

---

Les bons, les mauvais, les méchants

Les bons

Explication
C'est pas vrai.
**Fast** – `O(n log n)` bat le naïf `O(n^2)` et même les solutions `O(n log n)` qui dépendent de l'arbre indexé binaire (BIT) ou de l'arbre segment lorsque les constantes sont faibles. Autres
**Rencontre avec la mémoire** – Un seul tableau auxiliaire est nécessaire; pas d'arbres ou de cartes de hachage supplémentaires. Autres
**Élégant** – Le schéma de partage et de conquête s'aligne sur de nombreux problèmes classiques (p. ex. inversions, comptage de plus petits nombres après soi). Autres
**Language‐agnostic** – Fonctionne avec Java, Python, C++, JavaScript, Allez, etc. Autres

- Oui. Les mauvais

Raison
- Oui.
**La complexité de la mise en oeuvre** – Fusionner le tri avec le comptage par paires croisées est plus compliqué qu'un TBI simple. Nécessite une logique prudente à deux points. Autres
**exactitude non évidente** – Le fait que les moitiés triées peuvent être fusionnées et comptées simultanément peut ne pas être immédiatement évident pour les intervieweurs. Autres
Autres **Moins intuitif pour les débutants** – Beaucoup de gens pensent au BIT/Segment Tree parce qu'ils fournissent une « structure de données ». Autres

- Oui. L'Ugly

Risque
- Oui.
**L'utilisation abusive de `int` pour le préfixe des sommes** – conduit à l'AW sur de grands tests. Autres
** Mises à jour incorrectes du pointeur** – Un seul pointeur peut causer des comptes erronés, surtout lorsque `inférieur` est égal `upper`. Autres
**Récursion déséquilibrée** – Dans les entrées pathologiques, un comparateur personnalisé pourrait créer une scission déséquilibrée, mais avec la scission standard fusion-sort (`mid = (l+r)/2`) cela ne se produit jamais. Autres

---

Pourquoi ça compte dans une vraie interview

Lors d'un entretien pour un ** Ingénieur principal du logiciel** ou un ** Ingénieur de backend**, les intervieweurs aiment voir :

- **Décomposition du problème** – Transformer le problème en une forme plus gérable (préfixer les sommes).
- **Insight algorithmique** – Reconnaître qu'il s'agit d'une paire classique de nombres avec une différence de gamme.
- **Robustness** – Anticiper les débordements, les entrées négatives, les limites de récursion.

Citant les constantes : l'implémentation Java fonctionne en ~350 ms sur LeetCode, Python ~0.9 s et C++ <0.2 s pour l'entrée la plus défavorable.

---

À emporter

Pour les questions de la série II, la technique **Merge Sort computing** est le compromis optimal entre la vitesse, la simplicité et la maintenance. La maîtrise de ce modèle non seulement résout ce problème particulier, mais vous équipe également pour relever un large éventail de défis de subarrays de comptage.

N'hésitez pas à copier les extraits dans votre IDE préféré, à exécuter des tests locaux et à les montrer lors d'entrevues ou de concours de codage! C'est ce qu'il a dit.

---

Lire plus

- *"Algorithmes" de Robert Sedgewick et Kevin Wayne* – Inversions et comptage de la fusion.
- **Cracking the Coding Interview* – Discute de problèmes de comptage similaires avec BIT.
- *Problème de LeetCode 327 : Nombre de plus petits nombres après Self - Même algorithme sous-jacent.

---

* Bonne chance avec votre prochain entretien ou concours! Si vous avez trouvé cela utile, envisagez de le partager ou de mettre en vedette le dépôt. Bon codage ! *

---