---
titre: LeetCode 2448. Coût minimum pour assurer l'égalité des chances -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Code Leet 2448 – Coût minimum pour rendre la représentation égale
## Une plongée profonde (bon, mauvais et laid) + Production Code prêt (Java, Python, C++)

> **Objectif** – Écrire une solution propre et prête à la production que vous pouvez déposer dans une entrevue de codage ou une soumission de LeetCode.
> **Audience** – Développeurs seniors, intervieweurs d'algorithmes et tous ceux qui cherchent à décrocher un rôle d'ingénierie logicielle.
> **SEO Boost** – Mots-clés: *LeetCode 2448*, *Coût minimum pour rendre l'array égal*, * médiane pondérée*, *fonction convexe de recherche binaire*, *questions d'entrevue d'algorithme*, *solutions hard LeetCode*.

---

- Oui. 1. Déclaration de problème (Code de bord 2448)

On vous donne deux tableaux entiers de longueur égale `nums` et `cost`.
Vous pouvez augmenter ou diminuer tout élément de "nums" par 1, et chaque opération de cette unité sur l'indice "i` coûts `cost[i]`.

> **Tâche** – Trouver le coût total minimum pour faire **tous** éléments de "nums` égaux.

Obstacles

Valeur des contraintes
C'est pas vrai.
(n = longueur des tableaux)
Coût
Autres Résultat correspond à un entier de 64 bits signé (`long`) Autres

---

- Oui. 2. Le bon – Convexité + Médiane pondéré

2.1 Pourquoi la fonction de coût est-elle Convex?

Pour une valeur cible fixe `x`, le coût d'amener chaque élément à `x` est

«» "
f(x) = < < nombres > > – < < x > > * coût < < i > >
«» "

La valeur absolue est une fonction convexe; une combinaison linéaire avec des poids positifs préserve la convexité.
Par conséquent, **f(x) est convexe** sur les entiers.

Une fonction convexe sur un intervalle discret `[L, R]` atteint son minimum en un seul point (ou un intervalle de points).
Cela signifie que nous pouvons appliquer une recherche *binaire sur la réponse* (parfois appelée *recherche ternaire sur une fonction entière convexe*).

2.2 Interprétation médiane pondérée

Si vous triez les paires `(nums[i], cost[i])` par `nums[i]`, l'optimum `x` est la médiane *pondérée* des valeurs `nums` où les poids sont `cost[i]`.
En d'autres termes, trouver le plus petit `x` de telle sorte que le poids total du coût sur le côté gauche de `x` représente au moins la moitié du poids total.

Ceci donne une solution **O(n log n)** : trier une fois puis une seule passe pour localiser la médiane pondérée.

---

- Oui. 3. La force brute pure (O(n · range)

Une approche naïve imiterait sur chaque valeur cible possible de `min(nums)` à `max(nums)` et calculerait `f(x)` à chaque fois.
Étant donné que "nums[i]" peut être jusqu'à `106', c'est beaucoup trop lent (opérations du pire cas `106 · 105').
Nous allons sauter cela pour la production.

---

- Oui. 4. Les limites de recherche binaire incorrectes

Si vous définissez par erreur les limites de recherche binaire à `[0, 106]` au lieu de `[min(nums), max(nums)]`, vous pouvez gaspiller de nombreuses itérations.
De plus, ne pas utiliser un entier 64 bits (`long` en Java/C++, `int64` en Python) débordera pour les grandes entrées.

---

- Oui. 5. Mise en œuvre de la production

Voici trois solutions propres et bien documentées :

Langue Approche Temps Espace
- C'est quoi ?
Recherche binaire + Convexité Autres
*Python * Recherche binaire + Convexité * `O(n log range) * `O(1) ` Autres
Recherche binaire + Convexité Autres

N'hésitez pas à copier l'extrait de code dans votre éditeur IDE ou LeetCode.

---

### 5.1 Java (LeetCode-ready)

"Java
***
* 2448. Coût minimum pour assurer l ' égalité de répartition
* Soumission de code Leet
*/
solution de classe {
// Helper: calcul du coût total de la cible x
privé long total Coût(int[] nombres, coût int[], long x) {
somme longue = 0L;
pour (int i = 0; i < nombres de longueur; i++) {
somme += Math.abs(nums[i] - x) * coût[i];
}
la somme de retour;
}

coût intérieur) {
// Espace de recherche entre min et max de nombres
longue gauche = longue. MAX_VALUE, à droite = Long.MIN_VALUE;
pour (int n : nombres) {
gauche = Math.min (gauche, n);
droite = Math.max (droite, n);
}

long meilleur = Long. MAX_VALEUR;
pendant que (gauche <= droite) {
long milieu = (gauche + droite) / 2;
long coût Moyenne = total Coût(nombre, coût, milieu);
long coût MidPlus = total Coût(nombre, coût, milieu + 1);

// Si le coût diminue, allez à gauche; sinon allez à droite
si (coûtMod <= coûtMidPlus) {
best = Math.min(best, costMid);
droite = milieu - 1;
} autre {
best = Math.min (best, costMidPlus);
gauche = milieu + 1;
}
}
le meilleur retour;
}
}
«» "

* Pourquoi il est sûr:*
* Utilise `long` pour tous les résultats intermédiaires – pas de débordement.
* Les limites de recherche binaire sont serrées (entre `min(nums)` et `max(nums)`).
* La condition de boucle est `left <= right` pour garantir la résiliation.

---

#### 5.2 Python (LeetCode-ready)

'`python
"""
2448. Coût minimum pour faire en sorte que la répartition soit égale à la moyenne
Soumission de LeetCode – Python 3.8
"""
Solution de classe:
@staticmethod
def _cost(nombres, coûts, cible: int) -> Int:
"""Retourner le coût total pour amener tous les éléments à `cible`."""
somme de retour (abs(n - cible) * c pour n, c en zip(nombres, coûts))

def minCost(self, nombres: list[int], costs: list[int]) -> Int:
gauche, droite = min(nums), max(nums)
meilleure = flotteur('inf')

alors que gauche <= droite:
milieu = (gauche + droite) // 2
cost_mid = auto._cost(nombres, coûts, milieu)
coût_next = auto._coût(nombres, coûts, milieu + 1)

# f(x) est convexe → choisir le côté avec un coût inférieur
i cost_mid <= cost_next & #160;:
best = min(best, cost_mid)
droite = milieu - 1
Sinon:
best = min(best, cost_next)
gauche = milieu + 1

retour int(meilleur)
«» "

*Le python est une précision arbitraire. *

---

### 5.3 C++ (LeetCode-ready)

'`cpp
***
* 2448. Coût minimum pour assurer l ' égalité de répartition
* Soumission de code Leet
*/
solution de classe {
// Helper: calcul du coût total de la cible x
long coût PourTarget(vecteur continu<int>& nums,
le vecteur const<int>& coût,
long x) {
somme longue = 0;
pour (size_t i = 0; i < nums.size(); ++i) {
somme += llabs(nums[i] - x) * coût[i];
}
la somme de retour;
}

public:
longue minCoût(vecteur<int>& nombres, vecteur<int>& coût) {
longue gauche = LLONG_MAX, droite = LLONG_MIN;
pour (int n : nombres) {
gauche = min(gauche, (long)n);
droite = max(droite, (long)n);
}

longue longue meilleure = LLONG_MAX;
pendant que (gauche <= droite) {
long long milieu = (gauche + droite) / 2;
longue courbure longue = coût PourTarget(nombres, coût, milieu);
long long nxt = coût PourTarget(nombres, coût, milieu + 1);

si (cur <= nxt) {
best = min (meilleur, cur);
droite = milieu - 1;
} autre {
best = min (meilleur, nxt);
gauche = milieu + 1;
}
}
le meilleur retour;
}
};
«» "

*Tout arithmétique utilise "long long" pour éviter le débordement de 32 bits. *

---

- Oui. 6. Récapitulation de complexité

Approche Complexité
C'est pas vrai.
Recherche binaire (toutes langues confondues) **O(n log 106)** **O(n · 20)** → ~2 millions d'opérations pour 105 éléments. Autres
**O(n log n)** (le tri domine). Autres
Espace **O(1)** auxiliaire (sauf pour les tableaux d'entrée). Autres

Les deux solutions respectent confortablement la limite de temps de LeetCode.

---

- Oui. 7. Liste de contrôle pour les entrevues

Liste de contrôle des besoins
- C'est quoi ?
**Utilisez des entiers 64 bits**
**Binary-search limits = [min(nums), max(nums)]
**Éviter de traiter tous les entiers comme 0–106
Fonctions d'aide au document
**Exposer la convexité dans les commentaires**

---

- Oui. 8. Pourquoi cela compte pour votre prochain rôle d'ingénieur logiciel

* ** Fluence algorithmique** – Maîtriser les fonctions de coûts convexes, les médianes pondérées et la recherche binaire est une caractéristique des meilleurs ingénieurs logiciels.
* **Interview Impact** – LeetCode 2448 est une question classique : démontrer une solution claire et propre impressionnera les gestionnaires d'embauche.
* **Production–Prêt** – Le code ci-dessus est testé, comprend la manipulation des cas de bord et utilise des types de données optimaux – exactement le type de code que vous avez envoyé dans une base de données de production.

---

- Oui. 9. SEO-Friendly à emporter

- **Titre:** *LeetCode 2448 – Coût minimum pour rendre la répartition égale – Moyenne pondérée + Recherche binaire*
- **Meta Description:** *Solve LeetCode 2448 (Hard) en Java, Python et C++ avec une solution de recherche binaire convexe prête à la production. Apprenez les astuces médianes pondérées et as votre prochaine entrevue d'ingénierie logiciel. *
- **Étiquettes d'en-tête:** `# LeetCode 2448`, `### Exposé des problèmes "### Médiane pondéré, `## Recherche binaire`, `## Complexité`, `## Code (Java)`, etc.
- **Mots clés Placement:** Chaque paragraphe contient au moins un des mots clés de la cible (`LeetCode 2448`, `coût minimum pour rendre le tableau égal`, `recherche binaire`, `convexe fonction`, `pondéré médiane`).

---

10. Pensées finales

- **Bien:** Une solution de recherche binaire concise et mathématique qui fonctionne bien sous une seconde sur le harnais de test LeetCode.
- **Bad:** Brute-force sur toute la gamme – jamais utilisé en production.
- **Gly:** Des limites mal gérées ou un débordement de 32 bits – des bugs subtils qui peuvent vaincre votre réponse.

Déposez n'importe lequel des extraits dans une soumission LeetCode ou une entrevue d'emploi. Jumeler le code avec l'explication ci-dessus, et vous aurez un *complete interview package* qui met en valeur votre profondeur algorithmique et style de codage propre.

Bon codage – et meilleure chance d'obtenir ce travail de rêve! C'est ce qu'il a dit