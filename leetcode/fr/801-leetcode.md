---
titre: LeetCode 801. Swaps minimum pour faire augmenter les séquences -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# LeetCode 801 – Swaps minimum pour faire augmenter les séquences
## Un guide complet (Java) + Blog
> **Mots clés**: LeetCode 801, Swaps minimum, DP, algorithme d'entretien, solution Java, solution Python, solution C++, entretien d'emploi, entretien de codage, programmation dynamique

---

- Oui. 1. Récapitulation des problèmes

- Oui.
-- -- -- -- -- --
**Problème**
Difficulté
**Input**. Deux tableaux entiers "nums1` et "nums2` de longueur égale "n` (2 ≤ n ≤ 105) Autres
**Exploitation**= Échange de "nums1[i]` avec "nums2[i]` **une fois** par indice. Autres
**Objectif**= Nombre minimum de swaps à faire **deux** séquences augmentant strictement. Autres
**Garantie**= L'entrée admet toujours une solution. Autres

> *exemple*
> `nums1 = [1,35,4]`
> `nums2 = [1,2,3,7]`
> → swap à `i = 3` → `nums1 = [1,35,7]`, `nums2 = [1,2,3,4]` (1 swap).

---

- Oui. 2. Intuition

Pour chaque position "i", il y a deux possibilités:

1. **Ne pas échanger** à "i".
2. **Swap** à «i».

La validité d'un choix dépend uniquement du choix *précédent* :

- Si nous **n'avons pas échangé** à `i‐1`, alors les valeurs précédentes sont `nums1[i‐1]` et «nums2[i-1]».
- Si nous **wapé** à `i‐1`, les valeurs précédentes sont `nums2[i‐1]` et `nums1[i‐1]`.

Nous pouvons donc suivre deux états du PDD :

- `mainten[i]` – swaps minimums jusqu'à l'indice `i` **si nous conservons** (ne pas échanger) à `i`.
- "swap[i]" – swaps minimums jusqu'à l'indice «i» **si nous échangeons** à «i».

Parce que nous ne regardons jamais `i-1`, nous pouvons comprimer le DP à **O(1) espace**.

---

- Oui. 3. Récurrence

Let `a = nombres1[i-1]`, `b = nombres2[i-1]`, `c = nombres1[i]`, `d = nombres2[i]`.

«» "
conserver[i] = min(
garder[i-1] si < c& b < d, // continuer à augmenter
swap[i-1] si a < c && b < d + 1, // swap précédent, tenir à jour
)

swap[i] = min(
keep[i-1] + 1 si < d && b < c, // keep previous, swap current
swap[i-1] + 1 si < d && b < c, // swap précédent, swap courant
)
«» "

**Cas de base** (i = 0):

«» "
conserver[0] = 0 // aucun échange nécessaire au premier indice
swap[0] = 1 // swap au premier indice
«» "

La réponse est "min(keep[n-1], swap[n-1]")".

---

- Oui. 4. Mise en œuvre spatiale O(1) optimisée

Nous ne conservons que deux variables :

«» "
conserver = 0 // dp[0] pour conserver
swap = 1 // dp[0] pour swap

pour i = 1 .. n-1:
nouveaux Conserver = INF
nouveau Swap = INF
...
Keep = newKeep
swap = nouveau Swap
«» "

`INF` peut être `n` (swaps maximum possible).

---

- Oui. 5. Code en trois langues

#### 5.1 Java

"Java
***
* LeetCode 801. Swaps minimum pour augmenter les séquences
* Temps O(n), espace O(1)
*/
solution de classe {
int public minSwap(int[] nums1, int[] nums2) {
int n = nombres1.longueur;
maintien int = 0; // pas d'échange à la position 0
swap int = 1; // swap à la position 0

pour (int i = 1; i < n; i++) {
int newKeep = entier.MAX_VALUE;
int newSwap = entier.MAX_VALUE;

// Restez à I
si (nums1[i - 1] < nums1[i] && nums2[i - 1] < nums2[i]) {
newKeep = Math.min (newKeep, keep);
}
// Échange à i
si (nums1[i - 1] < nombres2[i] && nombres2[i - 1] < nombres1[i]) {
newSwap = Math.min (newSwap, gardez + 1);
}

// Garder à i mais échanger à i-1
si (nums1[i - 1] < nums1[i] && nums2[i - 1] < nums2[i]) {
newKeep = Math.min(newKeep, échange);
}
// Échange à i avec échange à i-1
si (nums1[i - 1] < nombres2[i] && nombres2[i - 1] < nombres1[i]) {
NewSwap = Math.min(newSwap, swap + 1);
}

keep = newKeep;
swap = nouveau swap;
}

retour Math.min(maintien, échange);
}
}
«» "

5.2 Python

'`python
"""
LeetCode 801. Swaps minimum pour faire augmenter les séquences
O(n) temps, O(1) espace
"""

Solution de classe:
def minSwap(self, nums1: list[int], nums2: list[int]) -> Int:
n = len(nums1)
conserver, échanger = 0, 1 # dp[0]

pour i dans la plage (1, n):
new_keep = float('inf')
nouveau_swap = flotteur('inf')

Garder le courant, garder le précédent
si nombres1[i-1] < nombres1[i] et nombres2[i-1] < nombres2[i]:
new_keep = min(new_keep, gardez)

# Gardez le courant, échangez précédent
si nombres1[i-1] < nombres1[i] et nombres2[i-1] < nombres2[i]:
new_keep = min(new_keep, swap)

# Swap courant, garder précédent
si nombres1[i-1] < nombres2[i] et nombres2[i-1] < nombres1[i]:
new_swap = min(new_swap, conserver + 1)

# Échanger courant, échanger précédent
si nombres1[i-1] < nombres2[i] et nombres2[i-1] < nombres1[i]:
new_swap = min(new_swap, échange + 1)

garder, échanger = new_keep, new_swap

retour min(entretien, échange)
«» "

C++

'`cpp
***
* LeetCode 801. Swaps minimum pour augmenter les séquences
* Temps O(n), espace O(1)
*/
solution de classe {
public:
int minSwap(vector<int>& nums1, vector<int>& nums2) {
int n = nombres1.size();
int keep = 0; // dp[0] lorsque nous conservons le premier élément
swap int = 1; // dp[0] lorsque nous échangeons le premier élément

pour (int i = 1; i < n; ++i) {
Int newKeep = INT_MAX, newSwap = INT_MAX;

// garder le courant, garder le précédent
si (nums1[i-1] < nombres1[i] && nombres2[i-1] < nombres2[i]) {
newKeep = min (newKeep, keep);
newKeep = min(newKeep, échange);
}
// Swap courant, garder ou swap précédent
si (nums1[i-1] < nums2[i] && nums2[i-1] < nums1[i]) {
NewSwap = min(newSwap, conserver + 1);
NewSwap = min (newSwap, swap + 1);
}

keep = newKeep;
swap = nouveau swap;
}
retour min(entretien, échange);
}
};
«» "

> **Pourquoi avons-nous deux contrôles séparés pour l'état de Keep. * *
> Parce que la condition `nums1[i-1] < nums1[i] && nums2[i-1] < nums2[i]` est la même que l'indice précédent ait été échangé ou non. La seule différence est de savoir si nous ajoutons un coût d'échange (`swap + 0` ou `swap + 0`). La même logique s'applique à l'état d'Eswap.

---

- Oui. 6. Article de blog – Le bon, le mauvais, le mauvais de LeetCode 801

6.1 Titre et méta

**Titre:**
*Mastering LeetCode 801: Swaps minimum pour faire augmenter les séquences – Java, Python, & C++ Solutions*

**Meta Description:**
Découvrez la solution la plus rapide O(n) DP pour LeetCode 801, avec les implémentations Java, Python et C++. Découvrez les pièges, les compromis et les explications prêtes à l'entrevue.

---

6.2 Introduction

> Quelle est la façon la plus efficace de faire deux séquences en augmentation stricte lorsque vous ne pouvez échanger des éléments qu'au même index ? (en milliers de dollars)
> C'est la question derrière LeetCode 801. Le défi semble simple mais se transforme rapidement en un exercice de manuel DP si vous le décomposez correctement.
> Dans cet article, nous allons parcourir le problème, le truc de programmation dynamique qui le réduit à O(n) temps et O(1) espace, et le code en trois langues populaires. Nous discuterons également des aspects *bon*, *mauvais* et *doucement* de la solution pour vous aider à éviter les pièges d'entrevue communs.

---

6.3 Le problème en anglais clair

1. Vous avez deux tableaux entiers `nums1` et `nums2` de longueur égale `n`.
2. Dans une opération, vous pouvez échanger les deux nombres au même indice: `nums1[i] ↓ nums2[i]`.
3. Votre objectif : ** les deux tableaux deviennent en pleine augmentation** (`a[i] < a[i+1]` pour chaque `i`).
4. Trouvez le nombre minimum de swaps nécessaires.

Parce que les données de test garantissent une solution, vous n'avez besoin que de minimiser les swaps, ne vous inquiétez pas des cas impossibles.

---

### 6.4 Le bon – Pourquoi ce PDD est élégant

- **Heure linéaire:** Nous n'avons besoin que d'un seul passage sur les tableaux («O(n)»).
- ** Espace supplémentaire permanent :** Seules deux variables entières (`maintenance`, `swap`) sont nécessaires.
- **Répétition simple :** L'état à l'index `i` dépend uniquement de `i-1`.
C'est la marque d'un problème de DP propre.

---

6.5 Les mauvaises – Erreurs communes

Pourquoi ça arrive ?
- Oui.
Autres Les gens pensent parfois que la condition pour échanger à "i" est la même que pour garder, mais ce n'est pas. Gardez les quatre contrôles séparément : garde, garde, garde, garde, garde. Autres
**Utiliser des tableaux pour DP inutilement** Utilisez deux variables et mettez-les à jour. Autres
**Ignorer l'effet "Swap" à l'effet i-1. Toujours ajouter `+1` pour le swap courant dans `newSwap`. Autres
**Si l'on suppose que les tableaux indexés à 1 sont basés sur 0, Java, Python et C++; le mélange d'indices conduit à des valeurs hors frontières. Démarrer la boucle à `i = 1`. Autres

---

#### 6.6 Le mauvais – Cas de bord et conseils de débogage

- **Égalité aux frontières** ('nums1[i] == nums2[i]' ou "nums2[i] == nums1[i]`).
Rappelez-vous le problème demande *strictement* augmenter, de sorte que vous ne pouvez pas autoriser `=`. Le DP vérifie (`<`) la gestion automatique.
- **Grands nombres** (1e9e).
Il n'y a pas de débordement parce que nous ne stockons que les nombres (`. n`), mais vous devriez toujours garder contre `. MAX_VALUE` en Java/C++.
- **Arrays de longueur 1** (`n = 1`).
La réponse est toujours `0` parce que les tableaux augmentent de façon insignifiante; le boîtier de base DP le gère automatiquement.

** Liste de contrôle pour le débogage : **

1. Imprimer `mainten' et `wap` à chaque étape.
2. Vérifiez que les quatre branches sont correctement touchées.
3. Recoupez-vous avec une solution de force brute pour le petit `n` pour assurer la justesse.

---

### 6.7 Explication de l'entrevue

> * Nous utilisons un DP à deux états : conserver ou échanger à chaque indice. * *
> *Connaissance clé:* Swapping à l'indice `i` ne **pas** influence la possibilité d'un futur swap; il ne change que les valeurs actuelles. Par conséquent, il suffit de se rappeler si l'indice précédent a été échangé ou non, et non la séquence exacte des swaps.

> **Pourquoi deux états suffisent? **
> Parce qu'il n'y a que deux possibilités par indice (ou pas). Pour chacun d'eux, nous évaluons si la condition strictement croissante est maintenue avec l'état de l'indice précédent. Cela donne exactement quatre cas, qui sont capturés dans la récurrence.

> ** Optimisation de l'espace:**
> Puisque `dp[i]` dépend uniquement de `dp[i-1]`, nous pouvons écraser les valeurs précédentes. Cela nous donne la variante de l'espace constant que les intervieweurs aiment.

---

6.7 Réflexions finales

LeetCode 801 est un problème *parfait* d'entrevue à présenter:

Maîtrise de la programmation dynamique.
- Capacité d'écrire un code propre, langue-agnostique.
- L'attention aux cas bord et l'étiquette d'entrevue.

Utilisez les solutions ci-dessus comme point de départ. Ajoutez des commentaires qui expliquent chaque branche dans vos propres mots – c'est ce que les intervieweurs recherchent.

Bonne chance, et que vos tableaux restent strictement en augmentation!

---

### 6.8 Appel à l'action

> Avez-vous déjà abordé LeetCode 801 ? Partagez votre expérience dans les commentaires, ou essayez le prochain problème DP: **[LeetCode 725 – Split Array with Same Sum](https://leetcode.com/problèmes/split-array-with-sum/)**. Bon codage !

---

- Oui. 7. Résumé

Nous avons dérivé une solution DP propre pour LeetCode 801 qui fonctionne dans le temps linéaire et l'espace constant. Nous l'avons implémenté en Java, Python et C++. L'article explique le problème des forces, des pièges et des stratégies de débogage, ce qui en fait une référence utile pour la préparation des entrevues et la reprise de la construction.