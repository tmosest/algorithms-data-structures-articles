---
titre: LeetCode 3432. Compter les partitions avec même la différence de somme -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Aperçu du problème

**LeetCode 3432 – Compter les partitions avec la différence de somme égale* *
Compte tenu d'un tableau entier «nums» (longueur 2 ≤ n ≤ 100, chaque élément 1 ≤ nombres[i] ≤ 100), trouver le nombre d'indices de partition «i» «0 ≤ i < n-1»

«» "
différence = somme(nums[0 ... i]) – somme(nums[i+1 ... n-1])
«» "

est **même**.
Le tableau est divisé en deux sous-tables non vides, à gauche `[0 ... i]` et à droite `[i+1 ... n-1]`.

> **Exemple**
> `nums = [10, 10, 3, 7, 6]` → 4 partitions valides.

Le défi est de le résoudre efficacement, de comprendre l'intuition et d'écrire du code propre, prêt à la production en **Java**, **Python** et **C++**.

---

- Oui. 2. Intuition et observation clé

Un nombre est **même** s'il est divisible par 2; sinon il est **odd**.
La parité (even/odd) d'une différence ne dépend que des parités des deux sommes:

«» "
gaucheSum % 2 == droiteSum % 2 Différence égale
«» "

Il suffit donc de savoir si chaque somme partielle est égale ou étrange, et non les valeurs exactes.
Un seul balayage linéaire suffit :

1. Calculer le total **** "total".
2. Iterate une fois, garder une course à gauche Somme.
"droite Somme = total – gauche Somme.
3. Comptez les indices où `gauche Somme % 2 == droiteSomme % 2`.

Complexités:
- **Heure**: O(n) (une passe pour "total", une passe pour le scan)
- **Espace**: O(1) (seulement quelques variables entières)

---

- Oui. 3. Exécution

Voici des implémentations concises et conviviales en trois langues.
Chacun suit la même logique : préfixer la somme + vérification de parité.

#### 3.1 Java

"Java
***
* 3432. Compter les partitions avec la différence de somme égale
*/
solution de classe publique {
Nombre d'entreprises publiques
Total Somme = 0;
pour (int num : nombres) total Somme += nombre;

Int gauche Somme = 0;
nombre int = 0;

// il suffit de considérer les partitions avant le dernier élément
pour (int i = 0; i < nombres.longueur - 1; i++) {
gauche Somme += nombres[i];
Int droite Total Somme - gauche Somme;

si ((leftSum & 1) == (rightSum & 1)) { // comparaison de parité
count++;
}
}
le nombre de retours;
}
}
«» "

> **Pourquoi `& 1`?**
> C'est une petite astuce qui extrait le moins significatif, équivalent à "mod 2", mais plus rapide sur le processeur.

3.2 Python

'`python
Solution de classe:
def countPartitions(self, nombres: list[int]) -> Int:
total = somme(s)
gauche, nombre = 0, 0

# nous nous arrêtons à len(nums)-1 parce que la partie droite doit être non-vide
pour i dans la plage (len(nums) - 1):
gauche += nombres[i]
droite = total - gauche
Si (gauche & 1) == (droite & 1):
nombre += 1
Nombre de retours
«» "

### 3.3 C++

'`cpp
***
* 3432. Compter les partitions avec la différence de somme égale
*/
solution de classe {
public:
nombre int Partitions(vecteur<int>& nombres) {
long total = 0;
pour (int x : nombres) total += x;

longue gauche = 0, cnt = 0;
pour (size_t i = 0; i + 1 < nums.size(); ++i) {
à gauche += nombres[i];
longue droite = total - gauche;
Si ((à gauche et 1LL) == (à droite et 1LL))
++cnt;
}
retourner static_cast<int>(cnt);
}
};
«» "

> **Pourquoi "long"?**
> Même si les contraintes maintiennent des valeurs faibles, elles sont plus sûres pour les grands cas d'essai et reflètent les pratiques de production typiques.

---

- Oui. 4. Cas de bord et essais

Cas d'entrée prévu
- C'est quoi ?
[1,2]
[2,4,6,8]
"[5,5]" - Oui.
[100 100]
[1,1]

*Pourquoi `[5,5]` et `[100 100]` retournent-ils 1? *
Les deux sous-cours ont des sommes égales («5» et «5»; «100» et «100») → différence `0` → même.

---

- Oui. 5. Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Simplicité algorithmique**= Un scan linéaire – O(n) – pas de structures de données lourdes== Aucune – mais peut être surtubé si n était énorme (pas le cas)== Aucune=
**Lisibilité du code**.Loops, commentaires explicites, parité bit-wise. Une trop grande optimisation (p. ex. micro-focusing sur le sens bit vs. « % ») peut obscurcir l'intention.
En Java, oublier `& 1` et utiliser `%` est très bien mais légèrement plus lent; pas un bug
**Performance**=100 % sur LeetCode en raison d'une petite entrée=Aucune possibilité d'amélioration=L'utilisation de `int` au lieu de `long` en C++ pourrait déborder si les contraintes changent==
**Testabilité**= Tests d'unité faciles avec différents tableaux=Caisse de bord: le tableau d'élément unique n'est pas valide==0=0

> **Ligne de bottom:** La solution simple de vérification de la parité est à la fois efficace et durable. Si vous avez besoin de l'échelle à des millions d'éléments, vous pouvez envisager le streaming ou la parallélisation, mais qui est en dehors de la portée du problème actuel.

---

- Oui. 6. Article de blog optimisé par le SEO

> **Titre:** *Master LeetCode 3432: Compter les partitions avec la différence même somme – Java, Python, & C++ Solutions*
> **Méta—Description:** Apprenez à fissurer LeetCode 3432 en moins de 5 minutes. Lisez nos solutions Java, Python et C++, comprenez les maths derrière les partitions de somme et obtenez des conseils d'entrevue prêts à travailler.

---

6.1 Introduction

Si vous vous préparez à une entrevue d'ingénierie logicielle, les problèmes qui testent vos compétences de manipulation *array* et de raisonnement *parité* sont essentiels. LeetCodeS **3432 – Compter les partitions avec Even Sum Difference** est un problème classique de la méthode -easy, qui démontre une solution O(n) propre. Dans cet article, nous allons passer par:

- Oui. Exposé des problèmes et contraintes
- L'intuition sous-jacente (pourquoi la parité compte)
- Implantations pas à pas Java, Python et C++
- Manipulation des caisses
- Une revue rapide, bonne, mauvaise, moche

A la fin, vous aurez non seulement la possibilité d'écrire le code, mais aussi d'expliquer *pourquoi* il fonctionne – exactement ce que les intervieweurs recherchent.

---

6.2 Récapitulation du problème

> **Objectif:** Compter les indices `i` où la différence entre les sommes des sous-arrays de gauche et de droite est égale.
> **Contraintes:** 2 ≤ n ≤ 100, 1 ≤ nums[i] ≤ 100.

Parce que `n` est minuscule, beaucoup de gens vont droit pour une double boucle. Ça passerait encore, mais c'est inutile. Au lieu de cela, une astuce *prefix sum* donne une solution O(n) élégante.

---

6.3 Les mathématiques derrière

Une parité entière (même/odd) est tout ce qui compte.
- Même nombre : divisible par 2.
- Numéro d'ordre : non divisible par 2.

La différence de deux nombres est égale **iff** les nombres ont la même parité:

«» "
gaucheSum – droiteSum 0 (mod 2) Somme % 2 == droiteSomme % 2
«» "

Donc nous avons juste besoin de compter des indices où la parité de la somme préfixe gauche correspond à la parité de la somme suffixe droite.

---

6.4 L'algorithme linéaire

1. ** Calculer la somme totale** "total = nombres"
2. **Itérer** à travers le tableau une fois, maintenir `gauche Somme.
- `rightSum = total – gauche Somme.
- Si `leftSum % 2 == rightSum % 2`, incrémentez le compteur.
3. **Retour** le compteur.

Tout ce que nous stockons est quelques entiers: O(1) espace.

---

6.5 Passage du code

##### 6.5.1 Java

"Java
solution de classe publique {
Nombre d'entreprises publiques
= 0;
pour (int n : nombres) total += n;

Int gauche = 0, nombre = 0;
pour (int i = 0; i < nombres.longueur - 1; i++) {
à gauche += nombres[i];
int droite = total - gauche;
si ((gauche & 1) == (droite & 1) count++;
}
le nombre de retours;
}
}
«» "

*Pourquoi `& 1`? *
`x & 1` est un moyen rapide d'obtenir `x % 2`. C'est un tour classique que beaucoup d'intervieweurs aiment.

6.5.2 Python

'`python
Solution de classe:
def countPartitions(self, nombres: list[int]) -> Int:
total = somme(s)
gauche, nombre = 0, 0
pour i dans la plage (len(nums) - 1):
gauche += nombres[i]
droite = total - gauche
Si (gauche & 1) == (droite & 1):
nombre += 1
Nombre de retours
«» "

La lisibilité de Python brille : une seule boucle "pour" et une comparaison de parité.

*### 6.5.3 C++

'`cpp
solution de classe {
public:
nombre int Partitions(vecteur<int>& nombres) {
long total = 0;
pour (int n : nombres) total += n;

longue gauche = 0, nombre = 0;
pour (size_t i = 0; i + 1 < nums.size(); ++i) {
à gauche += nombres[i];
longue droite = total - gauche;
Si ((à gauche et 1LL) == (à droite et 1LL))
+ nombre;
}
retourner static_cast<int>(compte);
}
};
«» "

Remarquez l'utilisation longue - sûre pour les entrées plus grandes si les contraintes augmentent jamais.

---

6.6 Cas de bord et essais

Pourquoi ?
- C'est quoi ?
Autres Paire unique égale : `[2,4]` Les deux sommes même → différence
Autres Tous les nombres impairs `[1,3,5]`=0=0 Les parités gauche/droite diffèrent pour chaque coupe
Parités mixtes Une seule coupe garde des parités égales.

L'essai est simple : il suffit d'alimenter des tableaux de longueurs variables et de s'assurer que le compteur correspond au calcul manuel.

---

#### 6.7 Bonne, mauvaise, mauvaise analyse

- **Bien:** O(n) temps, espace constant, logique de parité claire.
- **Bad:** Aucune, sauf si vous êtes sur-optimisation pour la micro-performance.
- **Ugly:** Utiliser des astuces fantaisistes bit-wise quand un "%" clair serait plus clair peut cacher l'intention.

Les intervieweurs apprécient *explication*. Gardez le code assez simple pour en discuter en quelques minutes.

---

6.8 Conseils d'entrevue

1. ** Expliquez le tour de parité** – il montre que vous comprenez l'arithmétique modulaire.
2. **Afficher la logique O(n)** – indiquez que vous ne faites pas de boucles imbriquées.
3. **Essais sur le bord de la Mention** – demandez des entrées de coin potentielles.

> **Départ rapide:** Parce qu'une différence égale implique des parités égales, je compte juste les coupes préfixes où `gauche Somme % 2 ' correspond 'à droite Somme % 2 %. (en milliers de dollars)

---

6.9 Réflexions finales

LeetCode 3432 est un fruit à faible hauteur qui teste les fondamentaux du tableau et l'intuition arithmétique. La solution de parité préfixe est propre, efficace et conviviale. Qu'il s'agisse du codage **Java**, **Python** ou **C++**, la logique de base reste la même : *un passage, un contrôle de parité et un compteur. *

> ** Prêt pour votre prochaine entrevue de codage? * *
> Pratiquez ce problème, et vous gagnerez de la confiance dans la gestion des préfixes de tableau, des suffixes et de la parité – tous les concepts clés qui se répètent sur de nombreuses questions d'entrevue.

Bon codage et bonne chance pour votre prochaine interview!

---

### 6.10 Appel à l'action

> **Vous souhaitez plus de solutions LeetCode?** Abonnez-vous à notre bulletin d'information pour obtenir des renseignements hebdomadaires sur les problèmes, des interviews et des ressources sur l'avancement professionnel.

---

- Oui. 7. Pensées de clôture

Vous avez maintenant :

- Un algorithme de production éprouvé pour LeetCode 3432
- Trois implémentations en langage propre
- Une compréhension claire de la raison pour laquelle la parité est le facteur décisif

Déposez cette solution dans votre éditeur de code, exécutez les tests d'échantillon, et vous serez prêt pour l'entrevue. Rappelez-vous: la clé pour exceller dans le codage des entrevues n'est pas seulement obtenir la bonne réponse, mais être en mesure de *articuler* le raisonnement derrière votre solution. Joyeux entretien !

---

* Fin de l'article. *