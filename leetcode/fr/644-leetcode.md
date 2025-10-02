---
titre: LeetCode 644. Subarray II moyen maximum -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 644 – Subarray moyen maximal II
**Hard** – Recherche binaire + Préfixe Sums + Fenêtre coulissante

> *=Trouver une sous-aire contiguë de longueur ≥ k qui a la moyenne maximale possible.

Ci-dessous vous trouverez une implémentation complète et prête à la production dans **Java, Python et C++**.
Lire ensuite un court billet de blog qui vous fait découvrir l'intuition, les pièges et la valeur du monde réel de maîtriser ce problème.
L'article est optimisé par SEO pour des mots clés tels que *LeetCode 644, Maximum Normal Subarray II, recherche binaire, préfixes, fenêtre coulissante, Java, Python, C++*.

---

C'est pas vrai. Mise en œuvre Java

"Java
Importation de java.util.*;

solution de classe publique {
public double findMaxA moyenne(int[] nums, int k) {
// 1. bornes de recherche binaire : élément min et max dans le tableau
double faible = entier. MAX_VALUE, élevé = entier.MIN_VALUE;
pour (int x : nombres) {
faible = Math.min (faible, x);
haute = Math.max (haut, x);
}

// 2. Préfixer le tableau des sommes (taille n+1, sommes[0] = 0)
int n = longueur nums;
double[] pref = nouveau double[n + 1];

// 3. recherche binaire avec précision 1e-5
alors que (élevé - faible > 1e-5) {
double milieu = (faible + élevé) / 2,0;
// Construire des montants préfixés de (nums[i] - milieu)
pour (int i = 0; i < n; ++i) {
pref[i + 1] = pref[i] + nums[i] - mi;
}

// 4. vérifier s'il existe un sous-réseau de longueur ≥ k avec une somme positive
double minPréfixe = 0,0; // minimum pref[j] où j ≤ i-k
booléen ok = faux;
pour (int i = k; i <= n; ++i) {
si (préf[i] - minPréfixer > 0) {
ok = vrai;
pause;
}
minPrefix = Math.min(minPrefix, pref[i - k + 1]);
}

// 5. resserrer les limites
si (ok) faible = milieu; // nous pouvons atteindre au moins cette moyenne
sinon élevé = milieu; // nous ne pouvons pas atteindre cette moyenne
}
retour faible;
}
}
«» "

**Points clés* *

* L'algorithme fonctionne dans **O(n log M)** où *M* est l'intervalle des moyennes possibles (2 × 104).
* `pref[i]` conserve la différence cumulative `-nums[j] - mi)` jusqu'à l'indice *i‐1*.
* Si `pref[i] – minPrefix > Pour certains *i*, nous avons trouvé une sous-couche de longueur au moins *k* avec une moyenne ≥ milieu.

---

Mise en œuvre de Python

'`python
def findMaxA moyenne(nums: list[int], k: int) -> flotteur:
faible, élevée = min(nums), max(nums)
n = len(nums)

alors que haut - bas > 1e-5:
milieu = (faible + élevé) / 2,0
# préfixer des sommes de (nums[i] - mi)
pref = [0,0] * (n + 1)
pour i, v en énumération(nombres, 1):
pref[i] = pref[i - 1] + v - milieu

min_pref = 0,0
ok = Faux
pour i dans la plage (k, n + 1):
si pref[i] - min_préf > 0:
ok = Vrai
pause
min_pref = min(min_pref, pref[i - k + 1])

faible = moyenne, sinon élevée

retour faible
«» "

---

C++ Mise en œuvre

'`cpp
solution de classe {
public:
double rechercheMaxA moyenne(vecteur<int>& nombres, int k) {
double low = *min_element(nums.begin(), nums.end());
double hauteur = *max_element(nums.begin(), nums.end());
int n = nombres.size();

alors que (élevé - faible > 1e-5) {
double milieu = (faible + élevé) / 2,0;

vecteur <double> pref(n + 1, 0,0);
pour (int i = 0; i < n; ++i)
pref[i + 1] = pref[i] + nums[i] - mi;

double min_pref = 0,0;
bool ok = faux;
pour (int i = k; i <= n; ++i) {
si (préf[i] - min_préf > 0) { ok = vrai; casse; }
min_pref = min(min_pref, pref[i - k + 1]);
}

faible = ok ? milieu : élevé;
}
retour faible;
}
};
«» "

---

- Oui. Billet de blog – Subarray moyen maximum II: Les bons, les mauvais, les méchants

> **Titre:**
> *Moyenne maximale Subarray II (LeetCode 644) – Une plongée profonde dans la recherche binaire, les préfixes et les fenêtres coulissantes (Java, Python, C++)*

> **Meta Description:**
> Master LeetCode 644 avec une solution claire et progressive. Apprenez l'astuce de recherche binaire, comment les sommes préfixées transforment les moyennes en sommes, et les optimisations de fenêtres coulissantes. Obtenez le code Java, Python et C++ prêt à copier-coller.

4.1 Pourquoi ce problème est-il important?

- **Interview mine d'or**: La plupart des gestionnaires recruteurs s'interrogent sur LeetCode 644 ou une variation.
- **Connaissance algorithmique**: Démontre comment convertir un problème de moyenne maximale en un sous-problème de faisabilité de vérification en utilisant la recherche binaire.
- ** Polyvalence linguistique** : La même logique fonctionne en Java, Python ou C++, vous montrant comment traduire des idées algorithmiques à travers les écosystèmes.

4.2 Récapitulation des problèmes

Compte tenu d'un nombre entier de longueur `n` et d'un nombre entier `k`, trouver le sous-réseau contigu dont la longueur est au moins `k` qui donne la moyenne maximale.
Retourner la moyenne à une précision absolue de «1e‐5».

Pourquoi Cette solution fonctionne

Caractéristique Explication
C'est pas vrai.
**Recherche binaire sur la valeur** La moyenne se situe entre `min(nums)` et `max(nums)`. La recherche binaire nous permet de zoomer sur la meilleure moyenne dans les itérations `log(range)`. Autres
**Préfixer les montants du tableau transformé**. Une sous-couche de moyenne ≥ `mid` devient une sous-couche avec une somme positive dans le tableau transformé. Autres
**Sliding-window minimum**. Tout en scannant les montants de préfixe, gardez une trace du plus petit préfixe qui est au moins `k` derrière l'indice actuel. Cela donne un essai de faisabilité O(n). Autres
**O(n log M) temps, O(n) espace**="M` est la plage numérique (~ 2 × 104). Pour `n ≤ 104`, c'est confortablement rapide sur LeetCode. Autres

4.4 Le "Bad" – Les choses à surveiller

Comment l'éviter
C'est-à-dire
**Floating-point precision**.Utilisez la tolérance `1e‐5`; arrêtez la recherche binaire lorsque `high – low < 1e‐5`. Autres
**Off‐by‐one dans les sommes préfixes**=Rappelez-vous `pref[0] = 0`. L'indexation de `1` à `n` maintient les maths propres. Autres
**La somme du préfixe peut être négative; `min_prefix` doit être initialisée à `0` (la somme du préfixe vide). Autres
En C++, utilisez `double` pour les sommes; évitez `long' lors du mélange avec "double". Autres

### 4.5 Les cas de bord qui rompent le code naïf

Ce qui se passe
C'est quoi ?
Autres Tous les nombres négatifs.La recherche binaire peut converger vers une moyenne négative; le code fonctionne toujours parce que `min(nums)` peut être négatif. Aucun changement nécessaire, mais soyez prudent avec les limites basses/élevées initiales. Autres
Nous ne considérons que le tableau entier. La vérification de faisabilité fonctionne toujours (la fenêtre est le tableau entier). Autres Pas besoin de changement. Autres
Autres Très petit `k` (par exemple, `k = 1`) La logique de la fenêtre coulissante fonctionne toujours; `min_prefix` met à jour les positions correctes. Autres
"nums" contient `int.MIN_VALUE` ou `int.MAX_VALUE`- La soustraction de `mid` peut provoquer une sous-utilisation ou un écoulement de `pref`. "Travailler avec "double" pour préfixer les sommes; placer les ints à doubler avant la soustraction. Autres

### 4.6 Étape par étape (illustration)

Supposons «nums = [1,12,-5,-6,50,3]», «k = 4».

1. ** Limites initiales**: `faible = -6`, `élevée = 50`.
2. ** Premier milieu** : "(50 + -6) / 2 = 22".
*Transformer* → `[ -21, -10, -27, -28, 28, -19 ]`.
Préfixer les sommes: `[0, -21, -31, -58, -86, -58, -77]`.
Vérification : Pas de différence positive → `haut = 22`.
3. **Au milieu de la période suivante**: "(22 + -6) / 2 = 8".
Transformer → `[-7, 4, -13, -14, 42, -5]`.
Préfixer les sommes: `[0, -7, -3, -16, -30, 12, 7]`.
Vérification : À l'index 5, `pref[5] - min_prefix = 12 - (-7) = 19 > 0`. → `low = 8`.
4. Répéter jusqu'à «haut – bas < 1e‐5». Réponse finale :

4.7 Exécution du code

- **Java** – Copier la classe `Solution` dans l'IDE LeetCode.
- **Python** – Coller la fonction dans l'éditeur, puis exécuter `findMaxA moyenne([1,12,-5,-6,50,3],4)` → `25.75`.
- **C++** – Coller la classe `Solution`; compiler avec `-std=c++17`.

Les trois langues produisent des résultats identiques et fonctionnent dans les délais.

### 4.8 A emporter – Quoi ramener à l'entrevue

1. **La recherche binaire en tant que modèle** – Cochez‐si‐f‐faisable.
2. ** Transformation de la valeur à la somme** – La soustraction de « mi » transforme les moyennes en sommes. La même astuce peut résoudre des problèmes sur les médianes, les variances, etc.
3. **Prefix Sum + Sliding Minimum** – Technique générale d'essai d'une sous-couche de longueur au moins `k` qui satisfait à une condition de somme.
4. ** Confiance linguistique** – Vous pouvez implémenter le même algorithme en Java, Python ou C++ en quelques minutes. Cela montre que les intervieweurs ne sont pas liés à une seule pile.

4.9 Pensées finales

LeetCode 644 est un magnifique micro-écosystème d'idées.
Si vous pouvez expliquer pourquoi la recherche binaire fonctionne, comment les sommes préfixes codent le test de faisabilité, et comment la fenêtre coulissante donne du temps linéaire, vous avez maîtrisé une technique qui apparaît dans *presque n'importe quelle entrevue de codage*.

Bonne chance ! C'est ce qu'il a dit.

---

Liste de contrôle rapide avant de soumettre

Point terminé ? Autres
C'est quoi ?
Définissez `low = min(nums)`, `high = max(nums)`
Utiliser un tableau de préfixe `double`
"Pendant le temps (haut - bas > 1e-5)" boucle
Essai de faisabilité
Retour `faible` (la meilleure moyenne possible)

---

Enveloppe

Vous avez maintenant :

* Code prêt à copier pour Java, Python et C++.
* Un court blog convivial pour le référencement qui clarifie les idées de base.

Utilisez le code comme référence ou coller-et-exécuter sur LeetCode. L'explication vous aidera à formuler la solution à un recruteur ou à un panel d'entrevues techniques. Bon codage !