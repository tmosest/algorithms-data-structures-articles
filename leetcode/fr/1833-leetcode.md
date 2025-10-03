---
titre: LeetCode 1833. Barres de crème glacée maximale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Vue d'ensemble de la solution (Approche de la composition et de la composition)

Pourquoi ça marche
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
*Java** * O(n + C) * O(C) * C = coût maximal * ≤ 105 *
**Python** Utiliser une `liste` de longueur `max_cost+1`
**C++**== `O(n + C)=== `O(C)=== Utilise un `vecteur<int>==de longueur `max_cost+1===

*`n`* – nombre de barres de glaces (= 105)
*`C`* – coût maximum dans le tableau (= 105)

Parce que les prix sont limités par 105 nous pouvons sauter le type `O(n log n)` habituel et simplement compter combien de barres ont chaque prix.
Puis nous marchons du prix le moins cher au plus cher, achetant autant de bars que nos pièces restantes le permettent.

---

- Oui. 2. Code

Ci-dessous se trouvent trois implémentations autonomes qui peuvent être copiées dans un bloc LeetCode.

---

### 2.1 Java

"Java
// 1833. Barres de crème glacée maximale – Tri de comptage (Java)
solution de classe {
Int public maxIceCream(coûts int[], pièces int) {
// Trouver le coût maximum pour tailler le tableau de comptage
le coût maximal = 0;
pour (int c : coûts) maxCoût = Math.max(maxCoût, c);

// 2
int[] freq = nouvelle int[maxCoût + 1];
pour (int c : coûts) freq[c]++;

Acheter des bars de moins cher à plus cher
barres int = 0;
pour (prix int = 1; prix <= maxCoût; prix++) {
int disponible = freq[prix];
si (disponible) 0) poursuivre;

int canBuy = Math.min (disponible, pièces / prix);
barres += canBuy;
pièces -= canBuy * prix;

// Sortie anticipée optionnelle: pas de pièces pour le prochain prix
si (pièces < prix) rupture;
}
barres de retour;
}
}
«» "

---

2.2 Python

'`python
# 1833. Barres de crème glacée maximale – Tri de comptage (Python 3)

Solution de classe:
def maxIceCream(self, frais: Liste[int], pièces: int) -> Int:
N° 1 Déterminer la limite supérieure du tableau de comptage
max_cost = max(coûts)

N° 2 Créer un tableau de fréquence
freq = [0] * (coût maximal + 1)
pour c en frais:
[c] += 1

N° 3 Acheter avec plaisir du moins cher au plus cher
barres = 0
pour le prix dans l'intervalle(1, max_cost + 1):
si freq[prix] 0:
poursuivre
can_buy = min(freq[prix], pièces // prix)
barres += can_buy
pièces -= can_buy * prix
si pièces < prix:
pause
barres de retour
«» "

---

C++

'`cpp
// 1833. Barres de crème glacée maximale – Tri de comptage (C++17)
solution de classe {
public:
Int maxIceCream(vecteur<int>& coûts, pièces int) {
// Trouvez le coût maximum
int maxCost = *max_element(costs.begin(), costs.end());

Tableau de fréquences
vecteur<int> freq(maxCoût + 1, 0);
pour (int c : coûts) + freq[c];

L'achat de graisse
barres int = 0;
pour (prix int = 1; prix <= maxCoût ++prix) {
si (!freq[prix]) continue;
int canBuy = min(freq[prix], pièces / prix);
barres += canBuy;
pièces -= canBuy * prix;
si (pièces < prix) rupture;
}
barres de retour;
}
};
«» "

---

- Oui. 3. Article de blog – Le bon, le mauvais, et le mal de compter trier sur LeetCode

### Titre (friendly SEO)
**Contribution–Trier sur LeetCode: Le Bon, le Mauvais et le Ugly – Guide de préparation au travail de 1833. Barres maximales de crème glacée* *

---

Description de la méta
Apprenez à résoudre le LeetCode 1833 en utilisant le tri de la crème glacée maximale. Guide étape par étape, code Java/Python/C++, analyse des performances, pièges et conseils d'entrevue.

---

Introduction

La chaleur estivale, un enfant affamé, et un portefeuille plein de pièces – c'est l'histoire derrière LeetCode 1833. Cela ressemble à un simple problème d'avidité, mais la touche est la plage de prix *bounded* (1 ≤ coût ≤ 105).
Cette contrainte invite à une solution de comptage-sort qui bat l'approche habituelle `O(n log n)`. Dans ce poste, nous disséquons le **bon**, le **mauvais** et les aspects **ugly** de cette méthode, nous vous donnons le code prêt à la production en trois langues, et nous montrons comment il peut impressionner les gestionnaires d'embauche.

---

Récapitulation des problèmes

> On vous donne un tableau `coûts` de la taille `n` (1 ≤ n ≤ 105) et un entier `pièces` (1 ≤ pièces ≤ 108).
> Chaque élément `coûts[i]` (1 ≤ coûts[i] ≤ 105) est le prix de la barre de glaces *i*.
> Le garçon peut acheter des bars dans n'importe quel ordre et veut en acheter le plus possible.
> Retournez le nombre maximum de barres qui peuvent être achetées avec les pièces disponibles.

---

C'est vrai. Les bons – Pourquoi compter les rochers

Caractéristiques Prestations
C'est pas vrai.
Avec `C = 105`, l'exécution est essentiellement linéaire, aucun facteur logarithmique. Autres
**Mémoire Prévisible** – 'O(C)'. Autres
**Complexité déterministe** Autres
**Intuition claire**=Enregistrez les fréquences, puis balayez du moins cher au plus cher. Autres
** Facile à vérifier** Le débogage est trivial : vous pouvez imprimer le tableau de fréquence pour confirmer les nombres. Autres

---

C'est pas vrai. Le mauvais – quand compter trier pourrait échouer

Pourquoi ça compte ?
- Oui.
Autres **Grande plage de coûts**= Si le coût maximum était, par exemple, 109, le tableau de fréquences serait impossible à attribuer. Autres
Autres **Données d'analyse**= Lorsque les coûts sont répartis mincement sur une vaste gamme, compter le tri se transforme en un gaspillage de mémoire. Autres
**Cache Unfriendly**Le tableau de fréquences peut être plus grand que les lignes de cache, ce qui peut causer plus de manques qu'un tri `O(n log n)` sur les petites entrées. Autres
Autres **Code Boilerplate**= Vous devez trouver manuellement `maxCost` et construire le tableau de fréquence, en ajoutant quelques lignes de code. Autres

> Dans LeetCode 1833, les contraintes garantissent le scénario de "bien", donc le tri est l'approche recommandée.

---

C'est vrai. Les pièges communs et comment les éviter

1. **Échec‐par‐un**
*Solution:* Tailler toujours le tableau de fréquences comme `maxCoût + 1` et itérer de `1` à `maxCoût` inclus.

2. **Excédent total dans la soustraction des pièces* *
*Solution:* Utilisez `long` ou `int64_t` pour le produit intermédiaire ` canBuy * price` lorsque la valeur des pièces peut atteindre 108. En Java, `int` est sûr parce que `maxCoût ≤ 105` et `coins ≤ 108` → produit ≤ 1013, qui convient à `long`.

3. **Skipping Zero Fréquences**
*Solution:* Ajouter un garde `si (freq[prix] == 0) poursuivre;» pour éviter les divisions inutiles.

4. **Conditions de sortie précoce**
*Solution:* Après chaque achat, si `coins < price` puis casser. Cela évite les boucles inutiles quand vous êtes hors de l'argent.

5. **Test des cas de bord* *
- Tous les coûts sont égaux au maximum ("105").
- Des pièces moins chères.
- Des pièces suffisantes pour un sous-ensemble de barres.

---

#### 6=" Mise en oeuvre (Java)

1. **Trouver le coût maximum** – nécessaire pour connaître la taille du tableau.
2. **Création d'un tableau de fréquences** – une passe sur les "coûts".
3. **Greedy balay** – pour chaque prix de 1 à `maxCoût`, acheter autant que possible jusqu'à ce que les pièces s'épuisent.

Le code Java dans la section **2.1** suit ce plan exact et peut être déposé directement dans LeetCode.

---

Python et C++ Versions

La même logique s'applique ; seule la syntaxe diffère :

- **Python**: `freq = [0] * (max_cost + 1)`
- **C++**: `vecteur<int> freq(maxCoût + 1, 0)`

Les deux versions reflètent l'implémentation Java et respectent les mêmes garanties de complexité temps/espace.

---

- Oui. Comment utiliser ces connaissances dans les entrevues

1. **Exposer les contraintes**
Souligner que `costs[i]` ≤ 105 → un tableau de comptage est possible.

2. **Énoncer la complexité**
Temps O(n + C), espace O(C). Pour ce problème C = 105, il est donc linéaire. (en milliers de dollars)

3. **Afficher le flux d'algorithmes**
Utilisez un diagramme de tableau blanc: -compte → acheter → répéter.

4. **Discuses sur les cas de bord* *
Demandez à l'intervieweur s'il veut que vous preniez en charge les coûts négatifs ou zéro pièce, puis adaptez-vous.

5. **Échanges de salaires**
Si les coûts n'étaient pas limités, nous reviendrons au tri ou à une file d'attente prioritaire. (en milliers de dollars)

---

C'est pas vrai. Bonus: Mini-Checklist pour votre prochain travail LeetCode

Objet
- Oui.
Maîtrisez à la fois les paradigmes gourmands et les modèles de tri. Autres
Pratiquez l'écriture propre, commenté code dans au moins 2 langues. Autres
Préparez-vous à discuter des compromis temps/espace dans les entrevues. Autres
Conserver un dépôt de solutions LeetCode avec des explications claires. Autres
Utilisez le framework "Good, Bad, Ugly" pour expliquer les algorithmes lors des écrans techniques. Autres

---

Conclusion

Le comptage est une technique simple, rapide et fiable lorsque les valeurs clés sont limitées – exactement le cas pour LeetCode 1833. En comprenant le **good** (vitesse, simplicité), **bad** (limites de mémoire, contraintes de portée) et **ugly** (bogues communes), vous serez en mesure de résoudre ce problème sans faille et impressionner les intervieweurs avec votre perspicacité algorithmique.

Bon codage, et que vos barres de glaces soient toujours les plus abordables! (en milliers de dollars)

---

Référence Mots clés

- Compter Tri LeetCode
- 1833 Solution de barres de crème glacée maximale
- Java Python C++ algorithme gourmand
- Conseils d'entretien LeetCode
- Algorithme du temps linéaire
- Explication de l'algorithme d'entretien d'emploi

---

*Soyez libre de partager cet article sur LinkedIn, Reddit ou votre blog personnel – il est rempli de contenu prêt à l'entrevue et vous aidera à grimper l'échelle de recherche d'emploi. *