---
titre: LeetCode 2160. Somme minimum de quatre chiffres après la division des chiffres -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2160 – Somme minimale du nombre de quatre chiffres après division
- Oui. Python de Java C++

---

Déclaration du problème

On vous a donné un entier ** positif** `num` composé de **exactement quatre chiffres** («1000 ≤ num ≤ 999»).
Vous devez diviser les chiffres de `num` en deux nouveaux entiers `new1` et `new2` en utilisant **all** quatre chiffres.
Les zéros sont autorisés.

> **Objectif:**
> Retourner la valeur **minimum possible** de `new1 + new2`.

*exemple*
`num = 2932` → chiffres `[2, 9, 3, 2]`
Paires possibles: `[29, 23]`, `[223, 9]`, `[2, 329]`, ...
Montant minimum = "29 + 23 = 52".

---

Intuition

Pour garder la somme petite, nous voulons que chaque nombre soit le plus court** possible et que les nombres les plus petits** soient utilisés dans les positions **hautes**.

Si nous trions les chiffres par ordre croissant :

«» "
triés = [d0, d1, d2, d3] // d0 <= d1 <= d2 <= d3
«» "

La somme minimale est obtenue par:

«» "
new1 = d0 * 10 + d2 // premier et troisième plus petits
new2 = d1 * 10 + d3 // deuxième et plus grande
«» "

Pourquoi ?
- Chaque nombre obtient un chiffre à la place des dizaines (le plus petit est le mieux).
- Oui. Le chiffre restant va à la place des unités.
- Oui. Ce couplage donne les plus petits nombres à deux chiffres possibles, d'où la plus petite somme.

---

Analyse de complexité

Complexe métrique
C'est pas vrai.
**Heure**="O(1)" – nous trions seulement quatre éléments (constante "O(4 log 4)"=". Autres
**Espace** – mémoire supplémentaire constante. Autres

---

Mise en œuvre du code

### Java

"Java
Importer java.util. Les tableaux;

solution de classe {
Int minimum public Sum(int num) {
int[] chiffres = nouveau int[4];
pour (int i = 0; i < 4; i++) {
chiffres[i] = nombre % 10;
num /= 10;
}
Tableau 3.
int num1 = chiffres[0] * 10 + chiffres[2]; // dizaines + unités
int num2 = chiffres[1] * 10 + chiffres[3];
retour num1 + num2;
}
}
«» "

Python

'`python
Solution de classe:
def minimum Sum(self, num: int) -> Int:
chiffres = triés([int(d) pour d en str(num)]) # liste de quatre int
num1 = chiffres[0] * 10 + chiffres[2]
num2 = chiffres[1] * 10 + chiffres[3]
retour num1 + num2
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int minimumSum(int num) {
les chiffres du vecteur<int>;
pour (int i = 0; i < 4; ++i) {
chiffres. push_back(num % 10);
num /= 10;
}
tri(digits.begin(), digits.end()); // ascendant
int num1 = chiffres[0] * 10 + chiffres[2];
int num2 = chiffres[1] * 10 + chiffres[3];
retour num1 + num2;
}
};
«» "

---

Article du blog : Le bon, le mauvais, et le mauvais de résoudre le LeetCode 2160

Introduction

Si vous êtes en train de vous préparer pour les interviews de codage, la somme minimale de quatre chiffres après la division des chiffres est un parfait exemple d'un problème **concise, mais subtil**. Il vous force à penser à la manipulation numérique, à l'optimisation et aux pièges des solutions de force brute. Dans cet article, nous allons disséquer le problème, marcher à travers la solution optimale, mettre en évidence des erreurs courantes (le --bad-) et discuter comment gérer les cas de bord (le --ugly-).

- Oui. Pourquoi ce problème est important

- **La pensée algorithmique**: démontre comment le tri peut être utilisé pour minimiser les sommes.
- ** Contraintes temporelles et spatiales** : montre que des solutions à temps constant sont réalisables.
- **Interview Pertinence**: De nombreux intervieweurs posent des questions sur les variations des chiffres.

Récapitulation du problème (Quick)

Vous avez un entier à 4 chiffres "num". Divisez ses chiffres en deux nouveaux chiffres en utilisant **tous** chiffres, permettant des zéros de tête, et retournez la somme possible **minimum**.

### La bonne – Élégante et optimale

C'est vrai. 1. Trier les chiffres

En triant, nous savons immédiatement quels chiffres sont les plus petits et les plus grands.
Le tri de quatre nombres est trivial (temps "O(1)").

C'est vrai. 2. Jumeler le plus petit avec le plus petit suivant

Formulaire `new1` utilisant les chiffres les plus petits (`d0`) et les troisièmes chiffres les plus petits (`d2`),
et `new2` utilisant le deuxième plus petit (`d1`) et le plus grand (`d3`).

Pourquoi cette paire ?
- Oui. Il garantit que chaque nouveau numéro est **deux chiffres** long (sauf lorsque des zéros apparaissent).
- Oui. Il place les plus petits chiffres à la place **tens**, qui a le poids le plus élevé.

C'est vrai. 3. Retour de la somme

Ajouter les deux nombres ; c'est la réponse.

Cette solution est **rétrospective**, **readable** et **optimale**.

- Oui. Les pièges communs

Pourquoi ça va mal ?
- C'est quoi ?
** Force brute toutes permutations** Il y a 4! = 24 façons, mais toujours acceptable. Cependant, générer toutes les partitions 2^4 est surkill et augmente le temps. Utilisez le tri + appariement gourmand. Autres
** Ordre d'extraction des chiffres de Wong** La prise de chiffres de gauche à droite contre de droite à gauche peut conduire à de mauvais indices. En continu pop de la fin ou convertir en chaîne. Autres
**Ignorer les zéros de tête**=Certains pensent qu'ils doivent éviter les zéros; mais le problème les autorise explicitement. Traitez les zéros comme tout autre chiffre. Autres
**En supposant que chaque nombre doit être de 2 chiffres**. Autres L'algorithme s'en occupe naturellement, car les zéros ne contribuent à rien. Autres

- Oui. Les cas d'Edge & Entrées Tricky

En savoir plus Produit prévu Pourquoi il peut vous faire voyager
Il y a un problème.
"num = 1000"""1" (split `[1, 0]" et `[0, 0]")" Deux zéros en un seul nombre, mais l'algorithme fonctionne toujours. Autres
`num = 9999`= 99 + 99 = 198`= Tous les chiffres sont égaux – la somme est juste deux fois le nombre à deux chiffres. Autres
"num = 4009" "13" Les zéros de tête apparaissent lors de la formation "[4, 9]". Assurez-vous que votre code ne tombe pas accidentellement des zéros de l'avant. Autres

Extraits de code (toutes langues)

- **Java** – voir ci-dessus.
- **Python** – voir ci-dessus.
- **C++** – voir ci-dessus.

Ce que les recruteurs recherchent

- **Clarité**: une explication concise de l'algorithme.
- **Efficacité** : Savoir qu'il existe des solutions à temps constant.
- **Connaissance des cas** : Manipulation des entrées avec zéros ou chiffres répétés.

Dernier départ

LeetCode 2160 est trompeur mais révèle une stratégie avide classique : *sort, puis pair plus petit avec troisième plus petit, plus grand avec deuxième plus petit.* La maîtrise de ce problème démontre votre capacité de penser en algorithme, d'écrire du code propre et d'anticiper les cas de bord – toutes les compétences clés pour une entrevue d'ingénierie logicielle.

Tu en veux plus ?

- Explorer d'autres problèmes de manipulation numérique sur LeetCode (par exemple, **2164. Compter le nombre de subséquences palindromiques**).
- Pratiquer des algorithmes gourmands dans les entrevues (p. ex., **Greedy Gift Givers**, **Maximum Subarray**).
- Construisez un portefeuille personnel de solutions sur GitHub; les recruteurs aiment le code propre et bien documenté.

Bon codage, et que vos notes d'entrevue reflètent cette solution élégante! C'est ce qu'il a dit.

---

** Tags du référencement**: LeetCode 2160, Somme minimum de quatre chiffres, Algorithme Question d'entrevue, Solution Java, Solution Python, Solution C++, Greedy Algorithm, Préparation d'entrevue, Entretien de codage, Entretien d'ingénieur logiciel, Conseils d'entrevue d'emploi.