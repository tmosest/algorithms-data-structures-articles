---
titre: LeetCode 2578. Split avec la somme minimale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

## Se partager avec la somme minimale – le bon, le mauvais, et l'horrible
**(Code de séance 2578 – Facile)**

> *Étant donné qu'un entier positif `num`, le diviser en deux entiers non négatifs `num1` et `num2` de sorte que la concaténation de `num1` et `num2` est une permutation des chiffres en `num`. Retourner la somme minimale possible de «num1» et de «num2».

Le problème semble trompeurment simple, mais la meilleure solution est un *single* cupidy pass qui vous donne une réponse d'entrevue parfaite, une implémentation Java/Python/C++ propre, et une explication que les recruteurs aiment voir.

---

Aperçu du problème

* 2578. Split avec une somme minimale * Difficulté * Contraintes *
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * Facile "num" n'a pas de zéro de tête. Autres
**Extrait**
**Notes**="num1` et `num2` peuvent contenir des zéros de tête.

Parce que `num` est au plus un nombre de 10 chiffres, le renforcement brutal de toutes les scissions est théoriquement possible, mais l'algorithme cupide fonctionne dans *O(d log d*), où `d ≤ 10`.

---

C'est vrai. The Greedy Insight (Le bien)

- **Objectif:** Conserver les deux nombres aussi petits que possible.
- **Observation:** Plus un chiffre est petit, moins il a d'impact sur la somme finale lorsqu'il est placé dans une valeur de place plus élevée.
- ** Stratégie :**
1. **Trier tous les chiffres ascendants** – les plus petits chiffres viennent en premier.
2. **Distribuer alternativement** entre les deux nombres.
- Même indices → `num1`, indices impairs → `num2`.
3. Construisez chaque nombre en ajoutant des chiffres de gauche à droite (le plus significatif → le moins significatif).

Parce que nous choisissons toujours le plus petit chiffre disponible pour la place la plus importante dans l'un ou l'autre nombre, la somme résultante est garantie être minimale.

> **Pourquoi l'alternance fonctionne** – Il équilibre les deux nombres: si un nombre obtient un 0 à la position la plus importante, l'autre obtient également le plus petit chiffre suivant. Le report résultant de l'ajout est réduit au minimum.

---

C'est vrai. Le "Bad" – Ce qui peut mal tourner

Pourquoi il peut vous faire monter
-- -- -- -- -- -- -- -- --
La somme de deux nombres à 10 chiffres correspond à un entier de 64 bits ("long" en Java, "long" en C++). En Java, utiliser `int` est sûr parce que la somme maximale possible est inférieure à `2 147 483 647`. En C++, un `int` 32 bits suffit aussi, mais utiliser `long' est une habitude défensive. Autres
**Laisser des zéros**= Certaines solutions naïves ignorent que les chiffres peuvent être ré-ordonnés arbitrairement. En triant, nous permettons naturellement les zéros de tête (ils seront juste à l'avant de la chaîne et seront laissés tomber lors de la conversion en entier). Autres
**Piège de conversion des caractères**=La conversion d'un caractère numérique en un entier incorrectement (`'0' - '0'` vs `c - '0'`) va jeter l'arithmétique. Autres
Autres Si `num` a tous les mêmes chiffres (par exemple `1111`), l'algorithme fonctionne toujours – les deux nombres deviennent la même valeur minimale. Autres

---

C'est pas vrai. Les erreurs courantes

- **L'utilisation d'un jeu de chiffres au lieu d'un tableau trié** – l'ordre relatif des chiffres compte pour minimiser la somme.
- **Appliquer des chiffres à la droite de la chaîne** – construire des chiffres à partir du chiffre le moins significatif mène à des chiffres inversés.
- **S'appuyant sur `Integer.parse Int` sur une longue chaîne** – peut déborder pour 10 chiffres.
- **Penser le problème c'est juste deux nombres** – vous devez garder le *multiset* de chiffres intact ; vous ne pouvez pas déposer arbitrairement des chiffres.

---

C'est vrai. Mise en œuvre

Voici des solutions propres, prêtes à la production dans **Java, Python et C++** que vous pouvez déposer directement dans une soumission LeetCode.

---

##### 5.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe {
public int splitNum(int num) {
// Convertir en tableau de chiffres
char[] chiffres = Chaîne.valeurDe(num).àCharArray();
Tableau 3.

Int num1 = 0, num2 = 0;

pour (int i = 0; i < chiffres. longueur; i++) {
int d = chiffres[i] - '0';
Si (i et 1)] 0) { // même indice -> num1
num1 = num1 * 10 + d;
} autre { // indice impair -> num2
num2 = num2 * 10 + d;
}
}
retour num1 + num2;
}
}
«» "

---

5.2 Python

'`python
Solution de classe:
def splitNum(self, num: int) -> Int:
chiffres = triés(str(num)) # liste des caractères triés ascendants
num1, num2 = 0, 0
pour i, d en chiffres :
d = int(d)
i % 2 == 0 & #160;:
num1 = num1 * 10 + d
Sinon:
num2 = num2 * 10 + d
retour num1 + num2
«» "

---

C++

'`cpp
solution de classe {
public:
Int splitNum(int num) {
chaîne s = to_string(num);
tri(s.begin(), s.end()); // ascendant

long n1 = 0, n2 = 0;
pour (size_t i = 0; i < s.size(); ++i) {
int d = s[i] - '0';
Si (i % 2 == 0)
n1 = n1 * 10 + d;
Autre
n2 = n2 * 10 + d;
}
retourner static_cast<int>(n1 + n2); // correspond à int
}
};
«» "

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
(d ≤ 10, essentiellement constante)
Construisant deux numéros **O(d)**
Total**** Autres

Compte tenu des contraintes, cela fonctionne en *microsecondes* et passe facilement les limites de temps de LeetCode.

---

Stratégie d'essai

Autres Test d'entrée prévu Raison
C'est pas vrai.
Exemple de l'énoncé de base
Petits chiffres
Les deux chiffres deviennent 11
Diminuer le zéro après le tri. Calcul d'attente : chiffres triés = 0,79. num1=0,9 → 9; num2=7 → 7; somme=16. Autres
Nombre maximal d'entrées 9876543210 1234567890 Classé comme entrée; l'alternance donne une somme minimale. Autres

Utilisez les tests unitaires dans votre langue de choix pour valider.

---

Points communs d'entrevue

- ** Expliquer la raison de l'avidité** : Nous voulons garder les deux nombres petits, donc nous donnons les plus petits chiffres aux endroits les plus significatifs de chaque nombre. (en milliers de dollars)
- **Zéros de tête de la Mention**: Comme l'ordre des chiffres peut changer, les zéros de tête sont parfaitement légaux et n'affectent pas la valeur entière. (en milliers de dollars)
- **Complexité du temps** : le tri à 10 chiffres est trivial ; l'algorithme est effectivement O(1). (en milliers de dollars)
- **Traitement des dossiers** : Tous les chiffres identiques, ou le nombre contenant zéro – l'algorithme fonctionne toujours parce que la stratégie de tri et d'alternance est uniforme. (en milliers de dollars)

---

FAQ

Question Réponse
C'est pas vrai.
*Pourquoi ne pas essayer toutes les partitions? * * Pour jusqu'à 10 chiffres, il est possible, mais la solution gourmande est O(1) et bien plus propre. Autres
*Pouvons-nous trier en descendant? Non – cela mettrait les plus grands chiffres dans les positions les plus importantes, augmentant la somme. Autres
*Y a-t-il une solution DP? C'est trop pour ce problème; une approche avide est optimale. Autres
*La solution gère-t-elle les nombres négatifs? Le problème garantit `num` est positif, donc nous n'avons pas besoin de nous inquiéter. Autres

---

À emporter

1. **Greedy + Tri** résout ce problème en deux nombres.
2. L'algorithme est *temps constant* pour les contraintes données mais aussi balance bien à des milliers de chiffres si vous remplacez le tri par un tri de comptage.
3. Ce problème est une excellente vitrine d'entrevue : il teste votre capacité à traduire une simple observation en code propre et à communiquer efficacement le raisonnement.

---

Titres et mots clés optimisés

- **Titre**: *Split avec somme minimale – Leetcode 2578 (Java, Python, C++)*
- **Description détaillée**: Apprendre à résoudre le Leetcode 2578 – Split avec la somme minimale – en Java, Python et C++ avec un algorithme gourmand. Guide étape par étape, code complet, analyse de complexité et conseils d'entrevue. (en milliers de dollars)
- **Mots-clés**: `Leetcode 2578`, `Split With Minimum Sum`, `Java solution`, `Python solution`, `C++ solution`, `greedy algorithme`, `interview coding problem`, `minimum sum slit`, `algorithm interview tips`.

Utilisez-les dans votre blog, et vous attirerez les recruteurs à la recherche de problèmes de pratique d'entrevue.

---

La pensée finale

Maîtriser avec un minimum de somme montre que vous pouvez:

- Transformez une contrainte en algorithme propre.
- Écrire le code de production en plusieurs langues.
- Expliquer la raison d'être d'un entretien.

C'est exactement ce que veulent les recruteurs. Bon codage, et bonne chance d'obtenir votre prochain travail!