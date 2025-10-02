---
title: LeetCode 1477. Trouver deux sous-tribus de non-overlaping avec la somme cible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1477 – Trouver deux sous-partages sans chevauchement chacun avec une somme cible
**Complexité temporelle:** `O(n)`
**Complexité spatiale:** `O(n)`

Ci-dessous vous trouverez des solutions propres et prêtes à la production dans **Java**, **Python** et **C++** qui résolvent LeetCode 1477 en temps linéaire.
Après le code, nous fournissons un article de blog complet, optimisé par le SEO, qui explique le problème, les écueils, et l'élégante astuce O(n) qui fait de cette question une question d'interview *must-know*.

---

C'est pas vrai. Solution Java

"Java
Importation de java.util.*;

solution de classe {

int public minSumOfLengths(int[] arr, int cible) {
int n = longueur de l'arrond;
// minLenFromLeft[i] – sous-réseau le plus court se terminant à ou avant i
int[] gauche = nouvelle int[n];
// minLenFromRight[i] – sous-cours le plus court à partir de i
int[] droite = nouvelle int[n];

// - Oui. Premier passage : gauche → droite ----------
int minLen = entier.MAX_VALUE;
début int = 0, somme = 0;
pour (int end = 0; fin < n; fin++) {
la somme += arr[end];
pendant que (somme > cible) {
la somme -= arr[start++];
}
si (somme == cible) {
minLen = Math.min(minLen, fin - début + 1);
}
left[end] = minLen; // stocker la meilleure longueur jusqu'à `end`
}

// - Oui. Deuxième passe : droite → gauche - Oui.
minLen = entier.MAX_VALUE;
début = n - 1;
somme = 0;
pour (int end = n - 1; fin >= 0; fin--) {
la somme += arr[end];
pendant que (somme > cible) {
-= arr[démarrage--];
}
si (somme == cible) {
minLen = Math.min(minLen, début - fin + 1);
}
right[end] = minLen; // stocker la meilleure longueur à partir de `end "
}

// - Oui. Combiner...
int best = entier.MAX_VALUE;
pour (int i = 0; i < n - 1; i++) {
si (à gauche [i] < Integer.MAX_VALUE && right[i + 1] < Integer.MAX_VALUE) {
best = Math.min(best, gauche[i] + droite[i + 1]);
}
}

Le meilleur retour == Entier. MAX_VALEUR ? -1 : meilleur;
}
}
«» "

> **Pourquoi ça marche* *
> * Fenêtre coulissante trouve chaque sous-aire dont la somme est égale à "cible" dans O(n).
> * Nous conservons la longueur la plus courte qui se termine (ou commence) à chaque indice.
> * Les deux tableaux `gauche` et `droite` encodent le sous-array de la valeur «best» pour le côté gauche et le côté droit de tout point divisé.
> * La boucle finale essaie simplement chaque point divisé – la paire optimale se trouve dans O(n).

---

Solution Python

'`python
de taper l'importation Liste

Solution de classe:
def minSumOfLengths(self, arr: List[int], cible: int) -> Int:
n = len(arr)

# gauche[i] = longueur la plus courte du sous-réseau se terminant à ou avant i
gauche = [float('inf')] * n
# droite[i] = longueur la plus courte du sous-réseau commençant à ou après i
droite = [float('inf')] * n

# ---- gauche → droite ----
s = 0
l = 0
min_len = flotteur('inf')
pour r dans la plage(n):
s += arr[r]
alors que s > cible:
-= arr[l]
l += 1
si s == cible:
min_len = min(min_len, r - l + 1)
gauche[r] = min_len

# ---- droite → gauche ----
s = 0
r = n - 1
min_len = flotteur('inf')
pour l dans la plage (n - 1, -1, -1):
s += arr[l]
alors que s > cible:
-= arr[r]
r -= 1
si s == cible:
min_len = min(min_len, r - l + 1)
droite[l] = min_len

# ---- combiner ----
ans = flotteur('inf')
pour i dans la plage (n - 1):
si gauche[i] < flotteur('inf') et droite[i + 1] < flotteur('inf'):
ans = min(ans, gauche[i] + droite[i + 1])

retour -1 si ans == flotter('inf') sinon ans
«» "

---

C++ Solution

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minSumOfLengths(vecteur<int>& arr, cible int) {
int n = arr.size();
vecteur<int> gauche(n, INT_MAX), droite(n, INT_MAX);

// gauche → droite
int l = 0, somme = 0, meilleure = INT_MAX;
pour (int r = 0; r < n; ++r) {
la somme += arr[r];
pendant que (somme > cible) somme -= arr[l++];
si (somme == cible) = min (meilleure, r - l + 1);
gauche[r] = meilleur;
}

// droite → gauche
int r = n - 1, best2 = INT_MAX;
somme = 0;
pour (int l2 = n - 1; l2 >= 0; --l2) {
la somme += arr[l2];
pendant que (somme > cible) somme -= arr[r--];
si (somme == cible) best2 = min(best2, r - l2 + 1);
droite[l2] = meilleur2;
}

// combiner
int ans = INT_MAX;
pour (int i = 0; i < n - 1; ++i)
si (gauche [i] != INT_MAX && droite[i + 1] != INT_MAX)
ans = min(ans, gauche[i] + droite[i + 1]);

INT_MAX ? -1 : ans;
}
};
«» "

---

Article du blog – *Les bons, les mauvais, les méchants*
**Titre**: *Maîtrise du LeetCode 1477: Trouver deux sous-groupes de non-overlaping avec la somme cible – Le bon, le mauvais, le mauvais*

---

Présentation

Lors de l'entrevue pour les rôles **logiciels-ingénierie**, LeetCode 1477 « Trouver deux sous-barrages sans chevauchement chacun avec le sum cible » est un problème classique qui teste la capacité d'un candidat à combiner **préfixer des sommes**, **des fenêtres coulissantes** et **une programmation dynamique** en un seul passage.

Dans cet article, nous allons:

1. **Énoncer le problème** en langage clair.
2. Marchez à travers **naïve** tentatives et pourquoi ils échouent.
3. Présentez la solution optimale O(n)** avec un passage clair.
4. Afficher **implémentations complètes** en Java, Python et C++.
5. Discutez de ** pièges communs** et des conseils d'entrevue.

N'hésitez pas à copier-coller les extraits de code, à les exécuter sur votre machine locale et à les ajouter à votre portfolio.

---

## Énoncé du problème (simplifié)

Vous êtes donné un tableau `arr` des entiers positifs et une somme cible `t`.
Trouvez deux sous-tribus *non-overlaping* de sorte que la somme de chaque sous-tribu soit égale à «t».
Retournez la longueur totale *minimum* de ces deux sous-groupes.
Si c'est impossible, retournez `-1`.

> **Constraints**
> 1 ≤ longueur ≤ 105 "
> • `1 ≤ arr[i] ≤ 103'
> 1 ≤ t ≤ 108 '

---

C'est pas vrai. Les bonnes – idées intuitives

Démarche Complexité
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Brute-Force** (deux boucles imbriquées + une autre boucle imbriquée) Simple à mettre en œuvre Trop lent pour `n=105` Autres
**Deux points (fenêtre coulissante)** Poignées de nombres positifs agréablement
**Préfixe Sum + HashMap**

La partie *bonne* est qu'avec **entiers positifs** nous pouvons exploiter la propriété *monotonique* des sommes: l'expansion d'une fenêtre augmente seulement la somme, la rétrécissant seulement diminue. C'est la clé d'une solution linéaire ** à deux points**.

---

- Oui. Les mauvaises – pièges communs

Pourquoi il échoue
C'est quoi ?
**Traiter la meilleure sous-tribu à gauche comme une seule variable mondiale** Nous avons besoin de la sous-tribu la plus courte* qui se termine *n'importe où* sur la gauche d'un point de fractionnement, pas seulement le dernier. Autres
**Ne pas propager les meilleures longueurs**= Après avoir trouvé un sous-réseau se terminant à `i`, vous devez vous rappeler que le meilleur jusqu'à `i` pourrait être encore plus court à un index précédent. Autres
**L'utilisation de deux scans indépendants sans fusion**. Autres
**Sur-complication avec les états de programmation dynamiques**= L'espace d'état explose; une approche simple de deux-pass préfixe/suffixe suffit. Autres

---

- Oui. Les solutions Ugly – Over-Engineered

Certains candidats ajoutent des recherches binaires, des arbres de segments ou même `unordered_map` sur des montants préfixés pour chaque index final possible.
Alors que ceux-ci sont *techniquement corrects*, ils sont:

* Lire comme suit :
- **Hard au débogage**
- **Hard à expliquer dans une interview* *

Lorsqu'une question d'entrevue permet une solution linéaire et propre, les approches *ugly* ne feront que nuire à votre score.

---

Solution O(n) optimale – Fenêtre coulissante + Préfixe/Suffixe

4.1 Aperçu

1. **À gauche → Pass droit**
* Pour chaque indice `i`, trouvez la sous-tribu la plus courte qui se termine au `i` ou avant et les sommes à `t`.
* Entreposez cette meilleure longueur dans le tableau `left[i]`.

2. **Droite → Pass gauche**
* De même, pour chaque indice `i`, calculer la sous-tribu la plus courte qui commence à `i` ou après.
* Stocker dans le tableau `right[i]`.

3. **Merge**
* Pour chaque point de division possible `i` (`0 ≤ i < n‐1`), combiner `left[i]` et `right[i+1]`.
* Le minimum de `gauche[i] + droite[i+1]` est la réponse.

4.2 Pourquoi ça marche

- La fenêtre de glissement **** garantit que nous vérifions *chaque sous-aire* dont la somme est exactement "cible".
- Le tableau "gauche" *propage* la longueur la plus courte vue jusqu'à présent, rendant chaque point de partage conscient de la meilleure sous-tribution gauche.
- Le tableau `droit` fait la même chose pour le côté droit.
- Puisque chaque sous-cours est découvert dans *O(n*), et que l'étape de fusion est un autre *O(n*), le temps d'exécution total est *linéaire*.

### 4.3 Pseudocode

«» "
n = longueur(arr)
gauche = tableau d'INF[n]
droite = tableau d'INF[n]

♪ Passe gauche
somme = 0; début = 0; meilleur = INF
pour la fin dans 0..n-1:
somme += arr[end]
en général cible:
sum -= arr[start]; start++
si somme == cible:
best = min (meilleur, fin - début + 1)
gauche[fin] = meilleur

♪ Pass droit
somme = 0; fin = n-1; meilleur = INF
pour commencer par n-1..0:
somme += arr[démarrer]
en général cible:
somme -= arr[end]; fin--
si somme == cible:
best = min (meilleur, fin - début + 1)
right[start] = meilleur

♪ Fusionner
réponse = INF
pour i en 0..n-2:
si gauche[i] < INF et droite[ i+1] < INF:
réponse = min(réponse, gauche[i] + droite[i+1])

réponse au retour == INF ? -1 : réponse
«» "

---

Mise en œuvre complète

Nous avons déjà présenté le code complet dans les sections précédentes.
N'hésitez pas à les déposer dans votre dépôt; nous vous recommandons d'ajouter **tests unitaires** pour les cas suivants:

1. `arr = [1,2,2,1,2,1,1,1]`, `t=3` → `réponse = 3` (par exemple, `[1,2]` et `[2,1]`).
2. `arr = [1,1,1,1,1,1]`, `t=7` → `réponse = -1` (pas de sous-tribus disjoints).
3. Cas de bord: longueur `arr` 1 → toujours `-1`.

---

## 6-

Conseil Comment l'utiliser
C'est quoi ?
**Expliquez votre plan d'abord** Autres
Autres **Utilisez une valeur factice** (`INF`) pour indiquer qu'il n'y a pas encore de sous-réseau. Évite les erreurs hors-par-un. Autres
**Demander des éclaircissements** Autres
**Vérification de la complexité du temps** fonctionnera dans environ 0,01 s pour `n=105` sur un ordinateur portable typique. Autres
**Discuss edge cases**= Montrez que vous considérez les scissions vides et les conditions de chevauchement. Autres

---

# # # 7--

LeetCode 1477 illustre parfaitement comment une structure de données *simple* (deux tableaux) et un algorithme *simple* (fenêtre coulissante) peuvent résoudre un problème apparemment complexe dans le temps linéaire.

**Traitements clés**:

- Rappelez-vous à **propagate** la meilleure longueur sub-array à tous les indices.
- Une approche **deux-pass** (préfixe + suffixe) est souvent la plus propre.
- Gardez le code **readable** et **bien commenté** – c'est ce que recherchent les intervieweurs.

Bon codage, et bonne chance avec votre prochaine interview! C'est ce qu'il a dit.

---

Références

- Problème officiel de LeetCode: https://leetcode.com/problèmes/find-two-non-overlapping-sub-arrays-each-with-target-sum/
- Solutions et discussion sur LeetCode discuter forum.
- Didacticiel de fenêtre coulissante: https://leetcode.com/articles/two-sum-ii/
- Technique de préfixe sum : https://leetcode.com/articles/shortest-subarray-with-sum-at-least-k/

---

**Bon entretien!**

---

*Auteur: [Votre nom]* – * Ingénieur logiciel
*Suivez-moi sur GitHub / Linked Pour plus de contenu algorithmique. *


---

*Word comte: ~1300*
* Temps de lecture : ~8 minutes*
*Mots clés: LeetCode, algorithme, interview, fenêtre coulissante, préfixe sum, Java, Python, C++ *


---

Bon appétit !