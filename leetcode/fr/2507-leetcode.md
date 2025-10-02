---
titre: LeetCode 2507. La valeur la plus faible après avoir remplacé la somme des facteurs principaux -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1. Le Code – 2507. La valeur la plus faible après le remplacement avec la somme des principaux facteurs

Voici trois implémentations propres et prêtes à la production (Java, Python, C++).
Chacun suit la même idée algorithmique :

1. **Fabrication primaire `n`.**
Résumez les principaux facteurs *avec multiplicité*.
2. **Replacer `n` par cette somme. **
3. **Renoncer jusqu'à ce que la somme soit égale à `n`** – cela ne se produit que lorsque `n` est premier.
4. **Retourner le premier vers lequel le processus converge. **

Toutes les solutions fonctionnent dans \(O(\sqrt{n})\) per itération et convergent dans au plus une poignée d'itérations parce que la valeur de `n` diminue monotoniquement jusqu'à ce qu'elle devienne prime.
Pour la contrainte donnée \(2 \le n \le 10^5\), l'exécution est triviale – bien en dessous de 1 ms en pratique.

---

## 1.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
***
* Renvoie la plus petite valeur accessible en remplaçant à plusieurs reprises
* n avec la somme de ses principaux facteurs.
*/
publique Valeur(int n) {
alors que (vrai) {
somme int = primeFactorSum(n);
si (somme == n) { // n est prime – stable
retour n;
}
n = somme; // continuer avec la nouvelle valeur
}
}

*** Aide : somme des facteurs principaux (avec multiplicité). */
Int prime privée FacteurSum(int x) {
= 0;
Int num = x;

// Manipulation du facteur 2 séparément pour sauter des nombres égaux
alors que (nombre % 2 == 0) {
Montant 2;
num /= 2;
}

// seuls des facteurs impairs subsistent
pour (int i = 3; i * i <= num; i += 2) {
alors que (nombre % i) 0) {
Montant i);
num /= i);
}
}

// si un premier > sqrt(x) reste
si (num > 1) somme += nombre;

la somme de retour;
}

// --------------------------------------------------
// Optionnel: une méthode principale pour les tests manuels rapides
// --------------------------------------------------
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.smallestValue(15)); // 5
Système.out.println(s.smallestValue(3)); // 3
}
}
«» "

**Points clés**

- Utilisations ** Division du procès** (optimisée par le saut de nombres).
- Fonctionne dans **espace supplémentaire constant** – seulement quelques variables entières.
- Très lisible et facile à vérifier – parfait pour une entrevue.

---

## 1.2 Python 3

'`python
Solution de classe:
def le plus petit Valeur(self, n: int) -> Int:
"""
Retourner la plus petite valeur obtenue en remplaçant à plusieurs reprises
n avec la somme de ses principaux facteurs.
"""
alors que Vrai:
s = auto._prime_factor_sum(n)
si s == n: # n est premier
retour n
n = s

def _prime_factor_sum(self, x: int) -> Int:
"""Retourne la somme des principaux facteurs de x (avec multiplicité)."""
Total = 0
num = x

Facteur 2
alors que num % 2 == 0:
Total += 2
num //= 2

# facteurs impairs
f = 3
alors que f * f <= num:
alors que num % f == 0:
Total += f
num //= f
f += 2

si num > 1 :
Total = nombre
retour total
«» "

** Faits marquants de la physique* *

- La fonction Helper maintient la logique de base lisible.
- Utilise l'arithmétique entier seulement; aucune bibliothèque externe n'est requise.
- L'algorithme est O( √n) et fonctionne en microsecondes pour `n <= 10^5`.

---

## 1,3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int plus petite Valeur(int n) {
alors que (vrai) {
somme int = primeFactorSum(n);
si (somme == n) // n est prime
retour n;
n = somme; // continuer
}
}

particulier:
Int prime FacteurSum(int x) {
= 0;
Int num = x;

// facteur 2
alors que (nombre % 2 == 0) {
Montant 2;
num /= 2;
}

// facteurs impairs
pour (int i = 3; 1LL * i * i <= num; i += 2) {
alors que (nombre % i) 0) {
Montant i);
num /= i);
}
}

si (num > 1) somme += nombre; // facteur primaire restant > sqrt(x)
la somme de retour;
}
};
«» "

**C++ Notes**

- Utilise `1LL * i * i` pour éviter les débordements (mais pas nécessaire pour `n ≤ 1e5`).
- Toute la logique vit dans une seule méthode – idéal pour le style d'entrevue.
- Compile avec `-std=c++17` (ou `-std=c++20` si vous préférez).

---

♪ 2. Article de blog – Le bon, le mauvais, et le mauvais de LeetCode 2507

## 2.1 Titre (optimisé par le référencement)

**LeetCode 2507 – Plus petit Valeur après le remplacement de la somme des principaux facteurs : le bon, le mauvais et le mauvais – Java, Python, C++ Solutions & Conseils d'entrevue *

## 2.2 Description des métadonnées

> Maître LeetCode 2507 en secondes. Découvrez les solutions Java, Python et C++ propres, comprenez les idées algorithmiques, et apprenez comment ace l'interview avec des astuces de factorisation.

2.3 Aperçu

1. Présentation
2. Récapitulation des problèmes
3. Intuition – Pourquoi le processus stabilise
4. Les bonnes
* Algorithme direct
* factorisation à faible complexité
* Facile à mettre en œuvre dans n'importe quelle langue
5. Les mauvais
* Division d'essai naïve contre tamis
* Risque de débordement dans d'autres contraintes
6. L'Ugly
* Erreurs de profondeur récursives
* Mauvaise mise en cache menant à un travail répété
7. Code Passage
* Version Java
* Version Python
* Version C++
8. Analyse de la complexité
9. Conseils de préparation à l'entrevue
10. A emporter et pensées finales

---

2.4 L'article (Marquage)

```markdown
# LeetCode 2507 – Plus petit Valeur après remplacement de la somme des principaux facteurs
**Le bon, le mauvais et le mauvais – Java, Python, C++ Solutions et conseils d'entrevue* *

---

Récapitulation des problèmes

Vous recevez un entier `n (2 ≤ n ≤ 105)'.
Remplacer à plusieurs reprises `n` par la somme de ses principaux facteurs (compter la multiplicité).
Retourne la valeur la plus petite que `n` ne prendra jamais.

> **Exemple**
> `n = 15 → 3 + 5 = 8 → 2 + 2 + 2 = 6 → 2 + 3 = 5`.
> La réponse est "5".

---

Intuition

- **Les numéros d'ordre restent les mêmes**:
La somme des principaux facteurs d'un "p" est "p" elle-même.
- **Les numéros composites se rétrécissent**:
Pour tout `m` composite, la somme de ses principaux facteurs est strictement inférieure à `m`.
- **Convergence**:
Par conséquent, la séquence `n, f(n), f(f(n)), ...` est strictement décroissante jusqu'à ce qu'elle atteigne un premier, qui est le point fixe.

Par conséquent, la réponse est tout simplement la première prime que vous rencontrez lorsque vous appliquez à plusieurs reprises la fonction sum.

---

Les bons

Caractéristiques Pourquoi ça compte
C'est-à-dire
Avec `n ≤ 105`, chaque factorisation prend au plus ~300 itérations. Autres
**L'espace continu**= Seulement une poignée d'entiers – parfait pour les contraintes d'entrevue. Autres
**Language-agnostique** ► Même logique en Java, Python, C++. Autres
**Code lisible** Autres

---

Les mauvais

Piège
- Oui.
** Division d'essais naïfs** Autres
**Excédent**= Pas de problème pour `n ≤ 105`; mais si elle est prolongée, utiliser `long'. Autres
**Limites codées à l'aide d'un code à l'aide d'une barre**. Autres

---

Les affreux

Qu'éviter
C'est quoi ?
**Mise en œuvre récursive** Autres
**La factorisation répétée**=Cacher les montants des facteurs pour les nombres vus serait exagéré ici, mais pourrait aider pour des intrants plus importants. Autres
**Inefficient I/O**. Pour la pratique de l'entrevue, la console I/O est bonne; mais dans la production utiliser des flux tamponnés. Autres

---

Code Passage

Voici les trois implémentations que vous pouvez copier dans votre IDE.

### Java

"Java
solution de classe publique {
publique Valeur(int n) {
alors que (vrai) {
somme int = primeFactorSum(n);
si (somme == n) retourner n; // prime trouvé
n = somme;
}
}
Int privé primeFactorSum(int x) { ... } // voir code ci-dessus
}
«» "

Python

'`python
Solution de classe:
def le plus petit Valeur(self, n: int) -> Int:
alors que Vrai:
s = auto._prime_factor_sum(n)
si s == n: retour n
n = s
def _prime_factor_sum(self, x: int) -> int: ... # voir le code ci-dessus
«» "

C++

'`cpp
solution de classe {
public:
int plus petite Valeur(int n) {
alors que (vrai) {
somme int = primeFactorSum(n);
si (somme == n) retour n;
n = somme;
}
}
particulier:
Int primeFactorSum(int x) { ... } // voir code ci-dessus
};
«» "

Tous les trois partagent le même assistant `primeFactorSum`, qui fonctionne dans `O( √x)`.

---

Analyse de complexité

- **Heure**: `O( √n * k)` où `k` est le nombre d'itérations (=6 pour `n ≤ 105').
- **Espace**: "O(1)" – seulement quelques variables locales.

---

Conseils pour l'entrevue

1. **Exposer la convergence**: Parlez de la raison pour laquelle la séquence frappe une prime et reste là.
2. ** Optimisation des peines**: Nous sautons même les nombres après le facteur de manipulation 2.
3. **Afficher la lisibilité**: Gardez des méthodes d'aide petites et bien nommées.
4. **Préparer pour les extensions**: Si les contraintes changent (`n ≤ 1012`), utilisez `long' et considérez un tamis simple pour les premiers contrôles primaires.

---

À emporter

LeetCode 2507 est un exemple parfait de la façon dont **la théorie des nombres simples** peut conduire à un algorithme propre qui est facile à mettre en œuvre, à tester et à expliquer.
Maître celui-ci et vous aurez une astuce d'interview pratique pour tout problème impliquant la factorisation primaire.

Bon codage, et bonne chance pour votre prochaine interview!
«» "

---

Les pensées finales

- La clé de *LeetCode 2507* est de reconnaître que le processus se termine toujours à un niveau de priorité.
- S'en tenir à une approche interactive, trial-division**.
- Showcase **code propre** et ** raisonnement clair** – c'est ce que les intervieweurs aiment.

Bonne solution ! C'est ce qu'il a dit.

«» "

2.5 Pourquoi cela aide votre carrière

- **Lisibilité de style Google**: Le code propre et sans bug est prisé par les géants de la technologie.
- **Couverture linguistique**: Les intervieweurs testent souvent en plusieurs langues; les trois se montrent polyvalents.
- **Connaissance algorithmique**: Expliquer la convergence et la complexité montre une compréhension plus profonde que juste je l'ai codé. (en milliers de dollars)

---

♪ 3. Résumé de clôture

Nous avons livré:

- **Trois solutions prêtes à la production** (Java, Python, C++).
- **Article détaillé** avec des mots-clés SEO, des conseils d'entrevue et une analyse de complexité.
- ** Explications claires** du comportement de l'algorithme – le bon, le mauvais, et le laid.

Avec ces ressources dans votre boîte à outils, vous êtes entièrement prêt à clouer LeetCode 2507 et toute question d'interview qui touche la factorisation principale. Bon codage !

«» "

---

*Sentez libre de modifier l'article pour votre plateforme de blog personnelle (WordPress, Medium, Dev.to). La structure, les titres et les mots-clés sont conçus pour se classer en haut sur les requêtes de recherche comme les problèmes d'interview de LeetCode 2507 ou de factorisation.
«» "

---

**Bonne entrevue!**