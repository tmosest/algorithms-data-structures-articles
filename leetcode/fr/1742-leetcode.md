---
titre: LeetCode 1742. Nombre maximum de boules dans une boîte -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de maîtrise du leet 1742 – Nombre maximum de boules dans une boîte

> **SEO Mots-clés**: LeetCode 1742, Nombre maximal de boules dans une boîte, entretien de codage, solution Java, solution Python, solution C++, entretien d'algorithme, entretien d'emploi, structures de données, tableau, carte de hachage, complexité temporelle

---

TL;DR

- **Problème**: Pour chaque entier *i* dans `[lowLimit, highLimit]` mettre la balle *i* dans la boîte `sumDigits(i)`.
- **Objectif**: Retourner le plus grand nombre de balles dans n'importe quelle boîte.
- **Contraintes**: <1 ≤ faibleLimit ≤ élevéLimit ≤ 105 "
- **Meilleure solution**: temps O(n), espace O(1) (pour mémoire de taille 46).
- **Pourquoi ça compte**: Une question d'entrevue fréquente qui teste votre capacité à traduire un problème simple en un algorithme efficace.

---

Répartition des problèmes

Ce qui arrive Pourquoi ça compte
-- -- -- -- -- -- -- -- -- -- -- --
**Balls** sont numérotés de `lowLimit` à `highLimit`. Autres
Autres Les cases** sont numérotées par la somme des chiffres du numéro de la boule. Transformation de base – `box = sumDigits(ball)`. Autres
Décomptez combien de balles atterrissent dans chaque boîte. Il nous faut le maximum. Autres
Autres Retournez ce maximum. La réponse finale. Autres

> **Exemple**
> `lowLimit = 1`, `highLimit = 10`
> Balle 1 → boîte 1, Balle 2 → boîte 2, ... Balle 10 → boîte 1
> La boîte 1 obtient 2 balles → répondre `2`.

---

- Oui. Les bonnes

Description Pourquoi il est bon
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Simple Loop**=Citérer sur chaque nombre une fois.=Temps linéaire, facile à raisonner. Autres
Autres **Résumé à chiffres directs** Pas de récursion ou de conversion de chaîne – constant. Autres
**Tableau de la taille La somme maximale des chiffres pour les nombres allant jusqu'à 100 000 est "9 × 5 = 45". Autres
Autres **Simple Pass Mise à jour de Max** Un passage sur les données + un passage sur le tableau de taille fixe → toujours O(n). Autres

---

- Oui. Les mauvais

Problème Piège commun Correction
- Oui.
**HashMap Overhead**= L'utilisation d'une `Map<Integer, Integer>= ajoute le coût d'attribution et de hachage. Remplacer par un tableau de taille fixe. Autres
**Conversion de la chaîne**=Le terme `String.valueOf(i.chars().sum()` est plus lent que l'extraction numérique.= Utilisez des opérations arithmétiques. Autres
**Bound de somme incorrecte**= En utilisant un tableau de taille de 100 000 (ou une grande constante) déchets mémoire. La taille doit être < 45 + 1 > . Autres
**Erreurs hors-par-un** Vérifier les limites des boucles (`i <= highLimit`). Autres

---

- Oui. L'Ugly

Pourquoi il s'agit d'un remède ?
- C'est quoi ?
**Récursions inutiles**=Le cumul récursif des chiffres peut atteindre les limites de la pile et est plus difficile à déboguer. Utilisez une approche itérative. Autres
**Sur-ingénierie**= Implémentation d'une solution DP ou combinatoire sophistiquée lorsqu'une simple boucle suffit. Stick à l'algorithme le plus direct. Autres
**Limites codées à la main**= Le codage dur `45` comme somme maximale sans explication rend l'entretien risqué. Calculer dynamiquement `maxSumDigits(highLimit)` ou documenter la dérivation. Autres
Autres **Poor Variable Naming**= Utiliser des noms vagues comme `arr`, `cnt`, `boxNo` masque l'intention. Utiliser des noms expressifs: `digitSum`, `boxCount`. Autres

---

C'est pas vrai. Le code

Voici des solutions idiomatiques et propres dans **Java**, **Python** et **C++** qui suivent l'approche *Good* décrite ci-dessus.

#### 5.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
compte int publicBalls(int lowLimit, int highLimit) {
// La somme maximale pour les chiffres jusqu'à 100000 est de 45
int[] boxCount = nouveau int[46];
Int maxBalls = 0;

pour (int i = lowLimit; i <= highLimit; i++) {
boîte int = chiffreSum(i);
boxCount[box]++;
si (boxCount[box] > maxBalls) {
maxBalls = boîteCount[box];
}
}
retour maxBalls;
}

chiffre int privé Somme(int n) {
= 0;
pendant la période (n > 0) {
somme += n % 10;
n/= 10;
}
la somme de retour;
}
}
«» "

Pourquoi c'est rapide

- **Time**: `O(n)` – une boucle sur la plage, somme à chiffres à temps constant.
- **Espace**: "O(1)" – tableau de 46 entiers indépendamment de la taille d'entrée.

5.2 Python

'`python
Solution de classe:
def countBalls(self, lowLimit: int, highLimit: int) -> Int:
# 9 * 5 = 45 est la somme maximale possible de chiffres pour 100000
box_count = [0] * 46
max_balles = 0

pour num dans la gamme (lowLimit, highLimit + 1):
box = auto._digit_sum(num)
box_count[box] += 1
si box_count[box] > max_balls:
max_balls = box_count[box]
_Return maxballs

@staticmethod
def _digit_sum(n: int) -> Int:
s = 0
alors que n:
s += n % 10
n //= 10
retour s
«» "

C++

'`cpp
solution de classe {
public:
compte intBalls(int lowLimit, int highLimit) {
// 9 * 5 = 45 pour des nombres allant jusqu'à 100000
vecteur<int> boîteCount(46, 0);
Int maxBalls = 0;

pour (int num = lowLimit; num <= highLimit; ++num) {
boîte int = chiffreSum(num);
++boxCount[box];
si (boxCount[box] > maxBalls) {
maxBalls = boîteCount[box];
}
}
retour maxBalls;
}

particulier:
digitaux intSum(int n) {
= 0;
pendant que (n) {
somme += n % 10;
n/= 10;
}
la somme de retour;
}
};
«» "

> **Astuce**: En C++ vous pouvez également utiliser `std::array<int, 46> boxCount{}` pour l'allocation statique.

---

L'espace et la complexité du temps

Langue Heure Espace
- C'est quoi ?
**O(n)** où `n = highLimit - lowLimit + 1'" **O(1)** (pour 46 int)
Python **O(n)**
* * * * * * * * *

> Même avec le cas le plus défavorable `n = 100 000`, la solution fonctionne en quelques millisecondes.

---

## 7.

1. **Lire les contraintes** – 105 est assez petit pour une simple boucle.
2. **Éviter la suringénierie** – un plan de hachage est inutile ici.
3. **Connais la limite supérieure des montants de chiffres** – aide à choisir la taille du tableau.
4. **Parlez de votre logique** – expliquez pourquoi un tableau de taille 46 suffit.
5. **Cas de bord de Mention** – par exemple, quand `lowLimit == highLimit`, ou lorsque tous les chiffres partagent la même somme de chiffres.

---

- Oui. Bonus : une comparaison Brute-Force contre une comparaison optimisée

Démarche Complexité
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Force-brute (HashMap)** (log m de l'extraction des chiffres)
**Optimisé (Array de 46)** Une mémoire minimale, plus rapide

> Si votre intervieweur insiste pour utiliser une carte, expliquez au moins le compromis.

---

## 9.

( ) **Vous avez maintenant une implémentation propre et prête à la production** dans votre langue préférée.
( ) **Vous comprenez bien le spectre de « Good-Bad-Ugly »** – idéal pour expliquer les compromis à la volée.
( ) **Vous pouvez répondre avec confiance à la question de "pourquoi"** – une compétence clé dans le codage des entrevues.

---

- Oui. Tu veux plus d'entretiens ?

- **S'abonner** à notre newsletter hebdomadaire pour des plongées plus profondes dans des problèmes LeetCode.
- **Télécharger** le livre électronique gratuit d'entrevue de 30 jours (lien en bio).
- **Demandez-nous une question sur Stack Overflow ou GitHub Discussions – nous sommes toujours heureux d'aider!

Bonne chance dans vos interviews ! *

---