---
titre: LeetCode 2979. Article le plus cher qui ne peut pas être acheté -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Description du problème – ♫ Élément le plus cher qui ne peut pas être acheté

Code du leet
C'est pas vrai.
Difficulté Moyenne
Tags Maths, Théorie des nombres

**État* *
Vous êtes donné deux nombres primaires distincts `primeOne` et `prime Deux.
Vous avez une quantité infinie de pièces dans ces deux dénominations.
Pour chaque entier positif `x` il y a un article qui coûte `x`.
Retourner le prix le plus élevé d'un article qui ** ne peut** être payé exactement avec n'importe quel
combinaison des deux pièces.

**Exemples**

* 'primeOne '* `primeDeux '* Produit*
- C'est quoi ?
Prix non achetables: {1,3}. Tous >3 sont achetables. Autres
Prix non achetables: {1,2,3,4,6,9,11,13,16,18,23}. Tous >23 sont achetables. Autres

**Contrôles* *

* 1 < `primeOne`, `primeDeux` < 104
* "primeOne" et "prime" Deux sont premier
* "primeOne" × `primeDeux` < 105

---

## ♫ Insight – Poulet McNugget Théorème

Lorsque vous avez deux entiers positifs de coprime `a` et `b`, le plus grand entier qui ne peut être exprimé comme
`a * x + b * y` avec des entiers non négatifs `x, y` est

«» "
maxNotReprésentable = a * b - a - b
«» "

Les deux premiers sont distincts, donc ils sont automatiquement coprimes.
La réponse est donc simple.

«» "
début Un * prime Deux - prime Un - premier Deux
«» "

Aucune boucle ou DP n'est nécessaire – la solution fonctionne dans **O(1)** temps et **O(1)** espace.

---

Mise en œuvre – trois langues

C'est pas vrai. Java

"Java
2979. Article le plus cher qui ne peut pas être acheté
solution de classe {
public int mostExpensive Item(int primeOne, int primeDeux) {
// Théorème du poulet McNugget pour les primeurs de coprime
retour prime Un * prime Deux - prime Un - premier Deux;
}
}
«» "

# # # # # #

'`python
# 2979. Article le plus cher qui ne peut pas être acheté
Solution de classe:
Coût Item(self, primeOne: int, primeDeux: int) -> Int:
Formule O(1): a*b - a - b
retour prime Un * prime Deux - prime Un - premier Deux
«» "

C'est vrai. C++

'`cpp
2979. Article le plus cher qui ne peut pas être acheté
solution de classe {
public:
Dans la plupart des cas Item(int primeOne, int primeDeux) {
// Théorème du poulet McNugget pour les primeurs de coprime
retour prime Un * prime Deux - prime Un - premier Deux;
}
};
«» "

Les trois extraits sont prêts à tomber dans le bouton LeetCodeSubmit et passer chaque cas de test instantanément.

---

Article du blog – Le bon, le mauvais, et l'atroce problème du poulet McNugget

> **Titre**:
> Comment cracker le leetCode 2979 en 10 secondes : le théorème de McNugget de poulet expliqué

> **Description détaillée**:
> Découvrez comment résoudre le LeetCode 2979 en O(1) avec le Chicken McNugget Theorem. Obtenez des solutions Java, Python et C++, ainsi qu'un blog détaillé sur les maths derrière elle. (en milliers de dollars)

> **Mots clés**:
> LeetCode 2979, article le plus cher qui ne peut pas être acheté, poulet mcnugget théorème, problème de pièce, théorie des nombres, interview de codage, solution Java, solution Python, solution C++, algorithme O(1), DP vs maths.

---

Introduction

Quand j'ai vu pour la première fois *LeetCode 2979 – Point le plus cher qui ne peut pas être acheté*, j'ai supposé qu'une approche de programmation dynamique (DP) était inévitable : Nous avons deux dénominations de pièces, pouvons-nous calculer tous les montants représentatifs? (en milliers de dollars)
Mais les contraintes étaient minuscules ('primeOne * primeDeux < 105') et les cas de test étaient simples.
Le vrai secret ? Un résultat classique de théorie des nombres appelé le **Chicken McNugget Theorem**.

---

### Le bon – Pourquoi la formule fonctionne

1. **Coprime Primes** – Deux premières distinctes sont coprime, c'est-à-dire "gcd(primeOne, primeDeux) == 1`.
C'est la condition exacte que le théorème exige.

2. **La plus grande somme inaccessible** – Le théorème nous dit le plus grand entier que ** ne peut pas** être écrit comme
'prime Un * x + prime Deux (x, y ≥ 0) sont
'prime Un * prime Deux – prime Un – premier Deux.

3. **Réponse à temps constant** – Une fois que vous connaissez la formule, la réponse est une seule opération arithmétique.
C'est pourquoi les trois solutions fonctionnent dans le temps *O(1)*.

---

- Oui. Les mauvaises – pièges communs

Pourquoi ça arrive ?
- Oui.
**Off‐by‐One Erreurs**= Oublier que le théorème s'applique à *positif* entiers > Utiliser le "prime" Un * prime Deux - prime Un - primeDeux.
**Overflow (Java)**= La multiplication `int` pourrait déborder pour les premiers plus grands (mais les contraintes le maintiennent en sécurité). Toujours sûr parce que `prime Un * primeDeux < 105`. Autres
**Missinterpréter *Distinct * Certains supposent que les premiers peuvent être égaux, ce qui briserait la condition de coprime. Le problème garantit qu'ils sont distincts. Autres

---

### Les affreux – Quand vous ne connaissez pas le théorème

Si vous êtes coincé et n'avez pas entendu parler du théorème, vous pourriez:

1. **Écrire un DP** qui explore toutes les sommes jusqu'à "prime" Un * primeDeux'.
Temps: `O(n2)` dans le pire des cas (n ~ 105) → ~109 opérations → trop lent.

2. **Mise en œuvre d ' un formulaire BFS/DP avec une requête** qui continue d ' ajouter < < primeOne > > et < < prime > > Deux.
Il finit toujours par explorer ~105 états, mais il est inutile.

3. **Énumération de l'essai et de l'erreur** jusqu'à ce que vous remarquez le modèle.
Cela gaspille du temps et conduit à des solutions floues qui peuvent échouer à des essais cachés.

---

Dernier départ

Le problème LeetCode 2979 est un exemple de manuel de la façon dont un petit maths peut transformer un problème DP apparemment dur en un seul-liner.
Rappelez-vous :

«» "
réponse = prime Un * prime Deux - prime Un - premier Deux
«» "

Ajoutez ceci à votre boîte à outils d'entrevue, et vous impressionnerez les intervieweurs avec votre codage et les côtelettes mathématiques!

---

Liste de contrôle du référencement

- **Titre** & **Meta** contient le mot-clé principal (-)
- **Intro** accroche les lecteurs avec une histoire (première rencontre).
- **Les têtes** (`#`, `#`, `###`) séparent le contenu pour la lisibilité et le référencement.
- **Les blocs de code** sont spécifiques à la langue et prêts à être collés.
- **Les listes de bulletins** pour les pièges rendent l'article écrémable.
- **Mots clés** parsemés naturellement.

---

**Codage heureux, et peut-être votre entrevue sera-t-elle aussi lisse que celle-ci!* *