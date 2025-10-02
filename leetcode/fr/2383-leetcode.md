---
titre: LeetCode 2383. Heures minimum de formation pour gagner un concours -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

# Heures d'entraînement minimum pour gagner un concours – LeetCode 2383
*(Java-Health Python) Solutions C++ + billet de blog de style interview*

> **Mots clés**: Minimum Heures de formation, LeetCode 2383, interview de codage, algorithme gourmand, complexité temporelle, complexité spatiale, solution Java, solution Python, solution C++, conception d'algorithmes

---

Résumé du problème

Vous entrez dans une compétition multi-round avec:
- `initialEnergy` – la quantité d'énergie que vous commencez par
- `initialExpérience` – la quantité d'expérience que vous commencez par

Vous affronterez les adversaires `n` dans l'ordre.
L'opposant `i` a:
- `énergie[i]` – le coût de l'énergie que vous perdrez en les battant
- `expérience[i]` – l'expérience que vous gagnerez

Vous gagnez contre un adversaire si **les deux** votre énergie et votre expérience actuelles sont ** strictement plus grandes** que les adversaires.
Après chaque victoire, votre énergie diminue par `énergie[i]` et votre expérience augmente par l'expérience.

Avant la compétition, vous pouvez vous entraîner pendant quelques heures.
Chaque heure vous pouvez ** soit** augmenter votre énergie initiale de 1 ** ou** votre expérience initiale de 1.
Retournez le nombre **minimum** d'heures d'entraînement nécessaires pour vaincre tous les adversaires.

---

# # # Une perspective fondamentale

Le problème peut être résolu avec une simulation *greedy*:

1. ** Expérience**
- Tandis que l'itération à travers les adversaires, si votre expérience actuelle est **-** l'expérience de l'adversaire, vous devez entraîner suffisamment d'heures pour le faire **>** cet adversaire.
- Le montant exact requis est "opposantExp - currentExp + 1".
- Ajouter ceci à la réponse, mettre à jour `currentExp`, puis ajouter l'expérience adverse.

2. **Énergie**
- Après l'expérience de manipulation, calculer l'énergie totale** nécessaire pour survivre à toutes les batailles :
«requisEnergie = somme (énergie) + 1».
- Si votre énergie initiale est déjà plus grande, vous n'avez pas besoin de formation pour l'énergie.
- Dans le cas contraire, vous avez besoin d'heures de formation `requiredEnergy - initialEnergy`.

Cette approche est optimale car:
- Pour l'expérience, vous ne vous entraînez que lorsque vous perdez un tour, et le montant ajouté est le minimum pour gagner ce tour.
- Pour l'énergie, vous ne pouvez pas battre n'importe quel adversaire à moins que votre énergie dépasse la somme cumulative de tous les coûts énergétiques.
Ainsi, l'entraînement exactement suffisant pour satisfaire cette condition est optimal.

---

Algorithmes et complexité

Langue Algorithme Temps Espace
- C'est quoi ?
Autres Java On passe par "expérience" + la somme O(1) de "énergie" **O(n)**
Python Même que Java **O(n)**
Même que pour Java **O(n)**

Toutes les solutions fonctionnent dans le temps linéaire et l'espace auxiliaire constant, manipulant facilement la contrainte `n ≤ 100`.

---

Mise en œuvre du code

C'est pas vrai. Java

"Java
***
* Heures d'entraînement minimum pour gagner un concours - LeetCode 2383
*
* Complexité temporelle: O(n)
* Complexité spatiale: O(1)
*/
solution de classe {
public int minNumberOfHours(int initialEnergy, int initial Expérience, int[] énergie, int[] expérience {
// 1. Calculer l'énergie supplémentaire requise
Total Énergienécessaire = 0;
pour (int e : énergie) total Énergienécessaire += e;
énergie int Heures = Math.max(0, totalÉnergieBesoin - initialÉnergie + 1);

// 2. Simuler l'expérience en comptant les heures d'entraînement nécessaires
expérience Heures = 0;
Int courant Exp = initiale Expérience;
pour (int exp : expérience) {
if (currentExp <= exp) {
int diff = exp - courantExp + 1;
expérience Heures += diff;
actuel Exp += diff; // Train avant de faire face à cet adversaire
}
actuel Exp += exp; // Acquérir de l'expérience après la victoire
}

énergie de retour Heures + expérience Heures;
}
}
«» "

> **Conseil** – Utilisez `Math.max` pour éviter les heures d'entraînement négatives pour l'énergie.

---

# # # # # #

'`python
"""
Heures minimum de formation pour gagner un concours - LeetCode 2383
"""

Solution de classe:
def minNumberOfHours(self, initialEnergy: int, initial Expérience: int,
énergie: liste[int], expérience: liste[int]) -> Int:
1. Énergie: somme de tous les coûts + 1
total_énergie_nécessaire = somme(énergie) + 1
énergie_heures = max(0, total_énergie_nécessaire - initialÉnergie)

2. Simulation d'expérience
_heures d'expérience = 0
curr_exp = expérience initiale
pour exp en expérience:
si curr_exp <= exp:
diff = exp - curr_exp + 1
expérience_heures += diff
curr_exp += diff # Train avant ce tour
curr_exp += exp # Gain après la victoire

return energy_heures + experience_heures
«» "

> **Pourquoi `+1` pour l'énergie? **
> Pour gagner l'adversaire **dernier**, votre énergie doit être strictement plus grande que le *sum* de toute `énergie[i]`.
> Ajouter 1 garantit une stricte inégalité.

---

C'est vrai. C++

'`cpp
***
* Heures d'entraînement minimum pour gagner un concours - LeetCode 2383
*
* Heure: O(n)
* Espace: O(1)
*/
solution de classe {
public:
int minNombre d'heures(int initialÉnergie, int initial Expérience,
vectorielle<int>&énergie, vectorielle<int>&expérience) {
// Énergie supplémentaire requise
Total Énergie = 0;
pour (int e : énergie) total Énergie += e;
énergie int Heures = max(0, totalÉnergie - initialeÉnergie + 1);

// Simulation d'expérience
expérience Heures = 0;
pour Exp = initiale Expérience;
pour (int exp : expérience) {
si (currExp <= exp) {
int diff = exp - currExp + 1;
expérience Heures += diff;
currExp += diff; // Train devant cet adversaire
}
currExp += exp; // Gain après la victoire
}

énergie de retour Heures + expérience Heures;
}
};
«» "

> **C++11+** – `vector<int>` et `max` de `<algorithme>` suffisent.

---

Pièges communs

Pourquoi ça arrive
- Oui.
*Missing the `+1` for energy** - Pensons à la somme de l'énergie est suffisant. Toujours ajouter 1 pour garantir une inégalité stricte. Autres
**L'expérience de formation après avoir ajouté l'expérience de l'adversaire** Check et train **avant** ajouter l'expérience adverse. Autres
**Utiliser `<=` au lieu de `<` dans la comparaison d'expérience**. * Vérifiez `<=` parce que nous avons besoin de plus. Autres
**Débordement entier (pas un problème avec des contraintes)**** Avec des contraintes plus grandes, le cumul de 100 * 100 pourrait déborder de 32 bits. Autres

---

Variations et extensions

1. ** Ordre aléatoire des opposants** – Si l'ordre peut changer, une solution de programmation dynamique peut être nécessaire.
2. **Options de formation multiples** – Au lieu d'augmentations de 1 point, permettre différents avantages de formation; utiliser avide ou DP en conséquence.
3. **Récupération d'énergie** – Supposons que vous récupériez une quantité fixe après chaque ronde; modifiez la simulation pour l'incorporer.

---

Conseils d'entrevue

1. ** Clarifier la règle plus importante** – Il change la condition de `>=` à `>`.
2. **Expliquer les deux sous-problèmes distincts** – Expérience et énergie.
3. **Afficher la preuve gourmande** – Nous ne nous entraîneons que lorsque nous ne pouvons pas gagner ; le montant ajouté est minime. (en milliers de dollars)
4. **Écrire un code propre** – Utiliser des noms de variables descriptives (`totalEnergyNeeded`, `experienceHours`).
5. **Discuse la complexité** – Mention du temps linéaire et de l'espace constant.

---

À emporter

Le problème des heures minimales de formation pour gagner un concours est une simulation classique *greedy* qui équilibre deux ressources indépendantes.
En traitant l'expérience et l'énergie séparément, vous pouvez dériver un algorithme propre et optimal qui fonctionne dans le temps O(n).
Maîtriser ce modèle vous aidera à répondre à de nombreuses questions d'entrevue où les contraintes de ressources et de la matière de commande.

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit.

---