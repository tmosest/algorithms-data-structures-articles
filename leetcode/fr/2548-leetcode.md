---
titre: LeetCode 2548. Prix maximum pour remplir un sac -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2548 – *Prix maximum pour remplir un sac*
**Java / Python / C++** solutions + un blog SEO-friendly interview-prep

---

TL;DR

Langue Heure Espace Lien
- C'est quoi ?
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * Autres
**Python ** **O(n log n)**
**O(n log n)**

> **L'idée gourmande:** trier les articles par *prix / poids* en ordre décroissant, puis remplir le sac à partir du meilleur rapport.
> Si vous ne pouvez pas atteindre la capacité exacte, retourner **-1**.

---

Récapitulation du problème

> **Prix maximum pour remplir un sac* *
> On vous donne `items[i] = [pricei, poidsi]`.
> Chaque article peut être divisé en deux parties (fractions).
> Remplissez un sac de capacité `C` à son poids exact avec un sous-ensemble ou des fractions d'articles, maximisant le prix total.
> Retourner le prix maximum (à l'intérieur de `1e‐5`) ou `-1` si impossible.

- "1 ≤ éléments de longueur ≤ 105 "
- "1 ≤ prixi, poidsi ≤ 104 "
- "1 ≤ C ≤ 109 "

---

- Oui. Pourquoi une stratégie d'avidité fonctionne

Parce que chaque élément peut être fractionné arbitrairement, le problème se réduit à un knapsack continu.
Dans le knapsack continu, la solution optimale est de choisir les articles dont le prix par unité de poids* est le plus élevé.
Si nous choisissons un article avec un ratio inférieur avant un plus élevé, nous pouvons échanger une portion et augmenter le prix total.

Ainsi:

1. **Trier** par "prix/poids" descendant.
2. ** Prendre des articles entiers** alors que la capacité reste.
3. **Prenez une fraction** du premier élément qui ne correspond pas.
4. Si tous les éléments sont utilisés et la capacité est toujours > 0 → **impossibilité**.

---

## Pièges et causes de bord

C'est bien C'est mal
C'est quoi ?
Débordement entier dans le comparateur → utiliser la multiplication 64 bits
Les poignées se divisent automatiquement. 0 after loop → wrong `-1`=" Forgetting `reverse=True` in Python trier → wrong order="
Utiliser `int` pour le poids total → déborder

---

Code de la solution

- Oui. 1. Java – Greedy + Comparateur personnalisé

"Java
Importer java.util. Les tableaux;

solution de classe {
public double maxPrix(int[[]] articles, capacité int) {
// Trier par rapport prix/poids par ordre décroissant.
Tableaux.sort(éléments, a, b) -> {
long lhs = (long) b[0] * a[1]; // b.prix * a.poids
long rhs = (long) a[0] * b[1]; // a.prix * b.poids
retour Long.comparer(lhs, rhs);
});

total double Prix = 0,0;
long restant = capacité;

pour (int[] élément : éléments) {
si (rester) 0) pause;
long w = élément[1];
double p = élément[0];
i (rester >= w) {
// Prenez l'article entier
restant -= w;
Total général Prix += p;
} autre {
// Prendre une fraction de l'article
fraction double = (double) restant / w;
Total général Prix += p * fraction;
restant = 0;
pause;
}
}

retour restant == 0 ? totalPrix : -1,0;
}
}
«» "

**Points clés* *

- Utilisez `long` dans le comparateur pour éviter le débordement `int` (`1e4 * 1e4 = 1e8`, toujours adapté mais sûr).
- "remaining" rails poids gauche; s'arrête une fois qu'il atteint 0.
- Si `remaining` > 0 après la boucle, le sac ne peut être rempli → `-1`.

---

- Oui. 2. Python – Greedy + " trié "

'`python
de taper l'importation Liste

Solution de classe:
def maxPrix(self, items: Liste[Liste[int]], capacité: int) -> flotteur:
# Trier par le rapport prix/poids (en déclin)
items.sort(key=lambda x: x[0] / x[1], inversement=True)

_Prix total = 0,0
restant = capacité

pour le prix, le poids des articles:
s'il reste == 0:
pause
si restant >= Poids:
restant -= poids
_Prix total += prix
Sinon:
fraction = restant / poids
Total_prix += prix * fraction
restant = 0
pause

total de retour_ prix s'il reste == 0 autre -1,0
«» "

> **Pourquoi la division est bonne**: `prix` et `poids` sont ≤ 104, donc le rapport est un double précis; aucune perte de précision pour le tri.

---

- Oui. 3. C++ – Greedy + Comparateur personnalisé

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
double maxPrix(vecteur<vecteur<int>>& items, capacité int) {
// Trier par prix / rapport poids descendant
tri(items.begin(), items.end(),
[](const vector<int>& a, const vector<int>& b) {
retour 1LL * a[0] * b[1] > 1LL * b[0] * a[1];
});

total double Prix = 0,0;
longue durée restante = capacité;

pour (auto &it : items) {
si (rester) 0) pause;
long w = it[1];
double p = it[0];
i (rester >= w) {
restant -= w;
Total général Prix += p;
} autre {
fraction double = static_cast<double>(remaining) / w;
Total général Prix += p * fraction;
restant = 0;
pause;
}
}
retour restant == 0 ? totalPrix : -1,0;
}
};
«» "

> **1LL** garantit la multiplication 64 bits pour le comparateur.

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Tri (`n log n`)
Scan linéaire
Total des dépenses

---

## Résumé de l'entrevue

- **Key Insight**: Knapsack continu → gourmand par rapport.
- **Mise en œuvre**: Tri par "prix/poids"; prendre des articles entiers jusqu'à ce qu'il reste de la capacité; prendre une partie fractionnelle du premier article impropre.
- **Manipulation d'Edge**: Si après avoir consommé tous les articles reste la capacité > 0 → retourner `-1`.
- **Langue-spécifique Conseils**:
- **Java**: Utiliser `long` dans le comparateur, éviter `int` débordement.
- **Python**: Le tri par rapport de flotteur est sûr; garder la trace avec "remaining".
- **C++**: multiplication 64-bits (`1LL * a[0] * b[1]`) dans le comparateur.

---

## SEO-Optimized Blog Post

Titre
**Master LeetCode 2548 – Prix maximum pour remplir un sac: Solutions Java, Python & C++ + Conseils d'entrevue**

Description de la méta
Apprenez à cracher LeetCode 2548 avec tri avide. Des solutions détaillées Java, Python et C++ ainsi qu'un guide d'entrevue prêt à travailler. Parfait pour les ingénieurs logiciels qui se préparent pour les entrevues de codage.

Rubriques

1. **Aperçu du problème**
2. **Pourquoi Greedy fonctionne** – Knapsack continu expliqué
3. **Mise en œuvre
- Solution Java
- Solution Python
- Solution C++
4. **Cas de complexité et de bord* *
5. ** Pièges communs (bons, mauvais et odieux)* *
6. **Cocher la liste de vérification de la préparation de l'entrevue* *
7. **À emporter et conseils professionnels**

Exemple d'introduction

> *Éver regardait un défi de codage apparemment impossible et se demandait comment l'aborder? Code du leet 2548 – *Prix maximum pour remplir un sac* – est un parfait exemple. Ci-dessous vous trouverez des solutions propres et prêtes à la production en Java, Python et C++, une plongée profonde dans la raison pour laquelle le tri avide est optimal, et une feuille de tri rapide pour impressionner les recruteurs lors de votre prochaine interview.

Mots clés

- LeetCode 2548
- Prix maximum pour remplir un sac
- sac à dos continu
- algorithme gourmand
- Java solution gourmande
- Python knapsack
- C++ trier le comparateur
- la préparation de l'entretien
- entretien de codage
- trading algorithmique
- structures de données et algorithmes

### Appel à l'action

> ** Prêt à accepter votre prochain entretien? * *
> Téléchargez notre PDF gratuit de la préparation de l'algorithme 30-Day ou abonnez-vous à notre newsletter pour relever des défis hebdomadaires de codage et d'entretien.

Pied de page

> © 2025 VotreNom — Tous droits réservés.
> *Cet article est destiné uniquement à des fins éducatives. *

---

Les pensées finales

- La stratégie **greedy** est à la fois *intuitive* et *efficace* pour ce problème de knapsack continu.
- Faites attention à *data type limits* – en particulier dans Java et C++ où le débordement `int` peut briser silencieusement votre solution.
- Oui. Dans les entrevues, énoncez la *preuve d'optimalité* (argumentation d'écart) pour montrer une compréhension profonde.

Utilisez ce guide pour peaufiner vos compétences de codage, impressionner les intervieweurs, et atterrir votre rôle d'ingénierie logicielle de rêve!