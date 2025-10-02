---
titre: LeetCode 2231. Le plus grand nombre après les swaps de chiffres par Parité -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2231. Le plus grand nombre après les swaps de chiffres par parité – Code + Interview‐ Prêt Blog

**Numéro de code:** 2231
**Difficulté:** Facile
**Tags:** Array, Greedy, Tri, Priority Queue, String, Interview Question, Java, Python, C++

---

Résumé du problème

On vous donne un entier positif `num`.
Vous pouvez échanger deux chiffres qui ont la même parité* (même ou les deux impairs).
Après n'importe quel nombre de swaps, retourner le **le plus grand entier possible** vous pouvez former.

> **Exemple**
> `num = 1234 → 3412`
> `num = 65875 → 87655`

> **Constraints**
> `1 <= num <= 10^9` (s'adapte en "int" 32 bits)

---

## -Le point de vue clé

L'ordre relatif des chiffres *odd* et *even* ne change jamais – vous ne pouvez réordonner que les chiffres ** dans chaque classe de parité**.
La stratégie optimale est donc :

1. **Extrait** les chiffres impairs et même séparément.
2. **Trier** chaque liste dans l'ordre **descendant** (les plus grands chiffres sont donc les premiers).
3. **Reconstruire** le nombre en remplaçant chaque chiffre original par le chiffre suivant le plus grand de la même parité.

Le résultat est garanti être le maximum possible entier.

---

Complexité

Opération Temps Espace
- C'est quoi ?
Extrait + tri "O(d log d)" (d = nombre de chiffres, ≤ 10) "O(d)" Autres
Reconstruction Autres

Avec `d ≤ 10` la solution est triviale dans le temps et la mémoire.

---

Mise en œuvre du code

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.

> **Astuce** – Les trois solutions convertissent le nombre en une chaîne pour fonctionner avec des chiffres, ce qui maintient le code lisible et évite les boucles manuelles modulo/division.

---

Java (Java 17)

"Java
Importation de java.util.*;

solution de classe {
publique Entier(int num) {
// Convertir en tableau char pour un échange facile
char[] chiffres = Chaîne.valeurDe(num).àCharArray();

// Greedy: pour chaque position trouver le plus grand chiffre de même parité à droite
pour (int i = 0; i < chiffres. longueur; i++) {
pour (int j = i + 1; j < chiffres.longueur; J++) {
si (chiffres[j] > chiffres[i] &&
(chiffres[j] -chiffres[i]) % 2 == 0) {
// échange
char tmp = chiffres[i];
chiffres[i] = chiffres[j];
chiffres[j] = tmp;
}
}
}
retourner Integer.parseInt(nouvelle chaîne(chiffres));
}
}
«» "

> **Pourquoi cela fonctionne:**
> La double boucle garantit que chaque fois que nous regardons à droite, nous plaçons le plus grand chiffre possible de la même parité à la position actuelle. Il en va de même pour le tri de chaque groupe de parité par ordre décroissant.

---

Python (Python 3,11)

'`python
Solution de classe:
plus Total (soi-même, nombre: int) -> Int:
s = liste(str(num))
n = len(s)

pour i dans la plage(n):
pour j dans la plage(i + 1, n):
si s[j] > s[i] et (int(s[j]) - int(s[i]) % 2 == 0:
s[i], s[j] = s[j], s[i]

retour int("".join(s))
«» "

> **Note pyrotechnique:**
> L'approche cupide à deux boucles est très lisible. Pour les entrées plus grandes, vous pouvez utiliser la méthode *sort‐by‐parity*, mais avec au plus 10 chiffres, la solution simple est parfaite.

---

C++ (C++17)

'`cpp
solution de classe {
public:
la plus grande Entier(int num) {
chaîne s = to_string(num);
int n = s.size();

pour (int i = 0; i < n; ++i) {
pour (int j = i + 1; j < n; ++j) {
si (s[j] > s[i] && (s[j] - s[i]) % 2 == 0) {
swap(s)[i], s[j];
}
}
}
retour des stoi(s);
}
};
«» "

> **C++ 17** – Utilisations `std::to_string`, `std::stoi` et `std::swap`.
> Le truc modulo `(s[j] - s[i]) % 2` fonctionne parce que les caractères `'0'`–`'9'` diffèrent du même montant que leurs valeurs numériques.

---

Article du blog – Le plus grand nombre après les swaps de chiffres par la parité : le bon, le mauvais, et le mauvais

Titre

> ** Le plus grand nombre après les swaps de chiffres par Parity – Master the Interview Problem (Java, Python, C++)* *

Description de la méta

> Solve LeetCode 2231 – Le plus grand nombre après les swaps de chiffres par Parity – avec des solutions Java, Python et C++ propres. Comprendre la stratégie avide, les pièges et les conseils d'entrevue. Augmentez votre score d'entrevue de codage!

---

Introduction

Si vous chassez pour un problème d'interview *réel* qui teste à la fois vos compétences de manipulation **array** et votre intuition **algorithmique**, ne cherchez pas plus loin que LeetCode 2231: **Plus grand nombre après swaps de chiffres par Parity**. Il s'agit d'un problème facile sur la plate-forme, mais il cache des nuances subtiles qui peuvent aller jusqu'à des programmeurs assaisonnés.

Dans cet article, nous plongerons profondément dans:

- Oui. La stratégie d'avidité qui garantit le nombre maximum.
- Erreurs courantes (le .
- Trois solutions prêtes à la production (Java, Python, C++).
- Comment expliquer la solution dans un cadre d'entrevue.

Laisse tomber !

---

### Le bon – Pourquoi il est élégant

Aspects Pourquoi ça marche
C'est pas vrai.
Chaque swap est local : nous mettons toujours le plus grand chiffre possible (de la même parité) à l'endroit le plus à gauche. Autres
**Préservation de la rareté**La contrainte de parité maintient le problème solvable avec une approche simple par groupe. Autres
**O(d log d)**= Avec les chiffres `d ≤ 10`, l'algorithme est essentiellement à temps constant. Autres
**Aucun grand entier n'a besoin d'être ajouté**. Le résultat final se situe dans un entier signé 32 bits (‘=10^9'). Autres

L'élégance consiste à reconnaître que l'échange de chiffres de même parité équivaut à trier indépendamment les chiffres impairs et même en ordre décroissant, puis à les assembler selon le modèle de parité original.

---

### Les mauvaises – Pièges que vous devriez éviter

1. **En supposant que vous pouvez échanger deux chiffres**
L'échange d'un `1` (odd) avec un `4' (même) est illégal – de nombreuses solutions pour les débutants le font par erreur.

2. **Utiliser entier arithmétique au lieu de chaîne**
Le fait de travailler directement avec des chiffres entiers (`num % 10`) peut conduire à des bogues lorsque vous essayez d'échanger des chiffres en place.

3. **Ignorer les principaux zéros**
Alors que le problème garantit `num >= 1`, vous pourriez penser à des nombres qui commencent par `0`. Un algorithme gourmand qui réordonne simplement les chiffres peut par inadvertance créer un zéro de tête si vous n'êtes pas prudent.

4. **Optimisation excessive pour les grands nombres**
Parce que `num` est plafonné à `10^9`, il n'y a pas besoin d'un tas ou de compter tri. La suringénierie peut rendre votre solution plus difficile à comprendre.

---

- Oui. Les pièges de complexité

- **Récursifs/retraits**
Certaines approches naïves tentent d'explorer chaque permutation de swaps impairs/même, conduisant à un temps exponentiel («O(d!)»). C'est *terrible* pour même `d = 10`.

- **En utilisant BigInteger**
Une erreur courante est d'analyser la chaîne finale dans `BigInteger` pour éviter le débordement, mais les contraintes la rendent inutile – et `BigInteger` est plus lent.

- **Vérification de la parité par défaut* *
En utilisant `(digit1 + digit2) % 2 == 0` est *incorrect* pour la comparaison de parité. Le bon test est "(numérique 1 -numérique 2) % 2 == 0" ou "numérique 1 % 2 ==numérique 2 % 2".

---

### Entrevue–Préparation Explication

> **=J'ai d'abord séparé les chiffres en deux listes – odds et evens. Puis je trie chaque liste descendante de sorte que les plus grands chiffres sont à l'avant. Enfin, je passe à travers le numéro original, remplaçant chaque chiffre par le prochain plus grand chiffre de la même parité de la liste correspondante. Le résultat est le plus grand entier possible. *

Expliquez que l'algorithme est *greedy* parce qu'à chaque étape nous choisissons le choix local optimal (le plus grand chiffre de même parité à gauche), et grâce aux groupes de parité indépendants, cet optimum local est aussi global.

---

Code Passage

C'est vrai. Java

"Java
char[] chiffres = Chaîne.valeurDe(num).àCharArray();
pour (int i = 0; i < chiffres. longueur; i++)
pour (int j = i + 1; j < chiffres.longueur; j++)
si (chiffres[j] > chiffres[i] &&
(chiffres[j] -chiffres[i]) % 2 == 0) {
char t = chiffres[i];
chiffres[i] = chiffres[j];
chiffres[j] = t;
}
retourner Integer.parseInt(nouvelle chaîne(chiffres));
«» "

* Pourquoi il est propre:* Deux boucles imbriquées, un simple contrôle de parité et un swap en place.

Python

'`python
s = liste(str(num))
pour i dans la plage(len(s)):
pour j dans la plage(i+1, len(s)):
si s[j] > s[i] et (int(s[j]) - int(s[i]) % 2 == 0:
s[i], s[j] = s[j], s[i]
retour int("".join(s))
«» "

*Twist pyronique:* Utilisation de la syntaxe `swap` `s[i], s[j] = s[j], s[i]`.

C++

'`cpp
chaîne s = to_string(num);
pour (int i = 0; i < s.size(); ++i)
pour (int j = i+1; j < s.size(); ++j)
Si (s[j] > s[i] && (s[j] - s[i]) % 2 == 0)
swap(s)[i], s[j];
retour des stoi(s);
«» "

*Points saillants:* `std::swap` maintient le code concis.

---

- Oui. Bonus : Approche triée par priorité (alternative)

Si vous voulez mettre l'accent sur *le tri* plutôt que sur les deux boucles gourmandes, vous pouvez faire :

"Java
Liste <Caractéristiques> cotes = nouvelle liste de distribution<>();
Liste <Caractéristiques> evens = nouvelle ArrayList<>();

pour (charc : chiffres) {
si (c - '0') % 2 == 0) evens.add(c);
autres cotes.add(c);
}
cotes.sort(Collections.reverseOrdonnance());
evens.sort(Collections.reverseOrder());

o = 0, e = 0;
pour (int i = 0; i < chiffres. longueur; i++) {
si [(chiffres[i] - '0') % 2 == 0) chiffres[i] = evens.get(e++);
autres chiffres[i] = cotes.get(o++);
}
«» "

> **Pourquoi il s'agit encore de Il est légèrement plus long mais rend l'indépendance des groupes de parité* claire. Dans une interview, il pourrait effectivement impressionner l'intervieweur en vous montrant que vous avez considéré plusieurs chemins de solution.

---

Dernier départ

LeetCode 2231 est un problème d'entrevue *golden*. La maîtrise vous donne :

- Les contraintes de gestion de la confiance et les cas d'angle.
- Expérience expliquant clairement la logique avide.
- Un motif réutilisable (groupe → trier → reconstruire) qui apparaît dans de nombreux problèmes de tableau.

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit.

---

### Ressources & Lecture supplémentaire

- [LeetCode 2231 – Problem Statement](https://leetcode.com/problèmes/plus grand nombre-après-numérique-swaps-by-parity/)
- [Greedy Algorithms – Coursera] (https://www.coursera.org/learn/greedy-algorithms)
- [Parité dans la programmation – Questions et réponses sur les dépassements de capacité] (https://stackoverflow.com/questions/what-is-parity)

---

SEO Boost

- **Mots-clés**: LeetCode 2231, Le plus grand nombre après les swaps de digitation par Parity, la solution de Java, la solution de Python, la solution de C++, l'algorithme d'algorithme, le codage des conseils d'entretien, la manipulation de l'array, la contrainte de la parité, l'intuition algorithmique.
- **En-têtes**: Utiliser `<h1>`, `<h2>`, `<h3>` et `<h4>` pour structurer le contenu des moteurs de lecture et de recherche.
- **Images**: Inclure un petit diagramme de -odd / même groupes et un diagramme de flux de l'algorithme.
- **Backlinks** : Dépôts officiels de référence LeetCode, Medium et GitHub pour une exploration plus approfondie.

Avec le code et le guide d'entrevue ci-dessus, vous êtes prêt à ace LeetCode 2231 et présentez vos côtelettes de résolution de problèmes dans toute entrevue technique. Bon codage !