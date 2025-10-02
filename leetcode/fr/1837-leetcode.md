---
titre: LeetCode 1837. Somme des chiffres dans la base K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1837 – Somme des chiffres de la base K
#### Easy="int sumBase(int n, int k)` – Java=" Python=" C++

Langue Heure Espace
- C'est quoi ?
*Java * O(logk n)
*Python * O(logk n)
O(logk n)

> **Pourquoi ce problème? * *
> *C'est une question classique de style interview qui teste votre compréhension de la conversion de base, de l'arithmétique modulaire et des invariants de boucle. La solution est élégante, O(log n) et utilise de l'espace constant, ce qui en fait un parfait "must-know" pour les entretiens techniques. *

---

# # # # # Description du problème (Code Leet 1837)

> **Input**
> * `n` – un entier positif dans la base‐10 (1 ≤ n ≤ 100)
> * `k` – la base cible (2 ≤ k ≤ 10)

> ** Sortie**
> Somme des chiffres de `n` exprimés en base‐`k`.
> La somme est retournée en base‐10.

> **Exemple**
> ```texte
> n = 34, k = 6 → 3410 = 546 → 5 + 4 = 9
> n = 10, k = 10 → 1010 = 1010 → 1 + 0 = 1
> `` "

---

- Oui. Les Brutes Idée de force

La façon la plus naïve est de :

1. Convertir `n` en base‐`k` et le stocker comme une chaîne de chiffres.
2. Itérer sur le tableau, convertir chaque chiffre en un entier, et les résumer.

Bien que correct, cela ajoute de l'espace supplémentaire pour la chaîne/array intermédiaire et les frais généraux inutiles.

> **Balance:**
> *Extra mémoire. *
> * Conversions renouvelables. *
> *Pas O(log n) dans le sens le plus strict – bien que toujours O(log n) temps, les facteurs constants sont plus élevés. *

---

- Oui. L'O(log n) optimal Solution

Nous pouvons calculer les chiffres à la volée en utilisant la division modulo et entière:

Texte
alors que n > 0:
chiffre = n % k // restant → chiffre courant le moins significatif dans la base k
somme += chiffre
n //= k // passer au chiffre supérieur suivant
«» "

* La boucle tourne autant de fois qu'il y a des chiffres dans la base‐`k`, qui est -logk n--
* Aucune structure de données auxiliaire n'est requise → O(1) espace.

Cas de bord

Raison
- C'est quoi ?
Un dans n'importe quelle base est 1. Autres
100 $ 100 $ 10010 = 10010 → 1 + 0 + 0 = 1.
100,1 10010 = 11001002 → 1+1+0+0+1+0+0 = 3 (pas 1) → montre l'importance du modulo correct/ division. Autres

> **Bien:**
> *Espace continu. *
> * Logique claire et lisible. *
> * Utilise directement les opérations arithmétiques. *

> **Ugly (si vous appliquez mal la division entière ou oubliez que `k` est <= 10):**
> *L'utilisation de la division en point flottant peut poser des problèmes de précision. *
> * Erreurs hors-par-un lors de l'initialisation de la « somme » ou de la condition de boucle. *

---

Mise en œuvre complète

#### 4.1 Java

"Java
// 1837. Somme des chiffres de la base K
// Heure: O(log_k n)
// Espace: O(1)

solution de classe {
public int sumBase(int n, int k) {
= 0;
pendant que (n != 0) {
somme += n % k; // chiffre le moins significatif actuel
n /= k; // décalage droit dans la base k
}
la somme de retour;
}
}
«» "

> *Pourquoi cela fonctionne:*
> `n % k` extrait le chiffre courant dans la base k. Diviser par `k` rejette ce chiffre, en préparant la prochaine itération.

---

4.2 Python

'`python
# 1837. Somme des chiffres de la base K
♪ Heure : O(log_k n)
♪ Espace: O(1)

Solution de classe:
def sumBase(self, n: int, k: int) -> Int:
Total = 0
alors que n:
Total += n % k
n //= k
retour total
«» "

> *Notes pyroniques:*
> `//` garantit la division entière. Aucune importation supplémentaire nécessaire.

---

### 4.3 C++

'`cpp
// 1837. Somme des chiffres de la base K
// Heure: O(log_k n)
// Espace: O(1)

solution de classe {
public:
int sumBase(int n, int k) {
= 0;
pendant la période (n > 0) {
somme += n % k; // reste: chiffre dans la base k
n /= k; // laisser tomber le chiffre traité
}
la somme de retour;
}
};
«» "

> *Pourquoi pas longtemps nécessaire:*
> La garantie de contraintes `n` ≤ 100, donc `int` suffit.
> Pour les entrées plus importantes, vous pouvez jeter à "long long".

---

C'est pas vrai. Exécution du code

Langue d'entrée Test d'entrée Sortie
- C'est quoi ?
Java, nouvelle solution().sumBase(34, 6)
Python: `Solution().sumBase(34, 6)`
* C++ *Solution().sumBase(34, 6) * * 9 *

---

Article de blog amical

---

### --Sum of Digits in Base K – The Interview‐Ready LeetCode 1837 Tutoriel

> **Meta Title**: Somme des chiffres dans Base K – Java, Python, C++ Solutions (LeetCode 1837)
> **Description de Meta**: Master LeetCode 1837 – Somme des chiffres dans la base K. Apprendre O(log n) Solutions Java, Python et C++, explications détaillées, cas de bord, et conseils de préparation d'entrevue.

---

Introduction

Quand vous voyez **=Sum of Digits in Base K==** dans une interview technique, la première question qui surgit est : *=Pouvez-vous convertir un nombre à une base différente et résumer ses chiffres ?==* Cette tâche apparemment simple met en évidence une compréhension candidate de la théorie des nombres, des boucles et de l'optimisation algorithmique.

Dans cet article, nous traversons l'énoncé du problème, donnons une solution O(log n) propre dans **Java, Python et C++**, disséquons la logique, cachez les cas de bord, et saupoudrez quelques idées favorables à l'entrevue. À la fin, vous serez prêt à impressionner les gestionnaires d'embauche avec vos cliquets de résolution de problèmes.

---

C'est vrai. 1. Récapitulation des problèmes

Paramètre Contraintes
- C'est quoi ?
Nombre dans la base
2 ≤ k ≤ 10

**Objectif**: Retourner la somme des chiffres de `n` après conversion `n` de base‐10 en base‐k`.

*Exemple*: `n = 34`, `k = 6` → `3410 = 546` → somme = `5 + 4 = 9`.

---

C'est vrai. 2. L'O(log n) optimal Stratégie

Pourquoi O(log n) ?

Le nombre de chiffres de `n` dans la base `k` est approximativement `logk n`. Chaque itération de l'algorithme traite un chiffre, de sorte que le nombre de boucles est proportionnel à ce logarithme.

2.2 Étape par étape

1. **Initialiser** "somme = 0".
2. **Alors que** `n > 0`:
* « chiffre = n % k » (extraire le chiffre le moins significatif actuel).
* "somme += chiffre".
* `n /= k` (division entière → supprimer le chiffre traité).
3. **Retour** "somme".

Cette boucle s'arrête lorsque tous les chiffres ont été traités (`n` devient 0). Aucun tableau ou chaîne auxiliaire n'est nécessaire, garantissant **O(1)** espace.

---

C'est vrai. 3. Échantillons de codes

*Voir la section « Mises en œuvre complètes » ci-dessus pour le code Java, Python et C++. *

---

C'est vrai. 4. Cas de bord et pièges communs

Autres Décision Pourquoi il importe d'éviter les erreurs
Il y a un problème.
"n = 1" (entrée minimale) Fonctionne naturellement; la boucle tourne une fois. Autres
"k = 2" "La conversion binaire" fonctionne toujours; modulo par 2 est rapide. Autres
`n` divisible par `k`= Les zéros de piste dans la base `k`= Modulo donne 0, mais la somme reste correcte. Autres
Division entière par rapport à la division flottante. Autres

---

C'est vrai. 5. Conseils d'entrevue

1. **Exposer l'invariant**: Chaque itération traite le chiffre le moins significatif.
2. **Temps de mention et complexité de l'espace**: temps O(log n), espace O(1). (en milliers de dollars)
3. **Afficher une vérification mentale rapide**: Pour `n=34`, `k=6`, marcher à travers deux itérations.
4. **Conclusions** : Pas besoin d'une manipulation en gros-int avec des limites données, mais notez que pour plus grand `n`, vous pouvez utiliser `long` en C++ ou `long` en Java.

---

C'est vrai. 6. Pourquoi ce problème est un savoir-faire

* **La conversion des bases** est un concept fondamental qui apparaît dans de nombreuses interviews (p. ex., convertir la décimale en binaire).
* **Modulo & division** opérations test de connaissance de l'arithmétique entier.
* La solution est *concise*, *optimal*, et démontre un bon style de codage – exactement ce que les recruteurs recherchent.

---

C'est vrai. 7. Pensées finales

Mastering LeetCode 1837 est plus qu'écrire une boucle ; il s'agit de comprendre la relation entre les bases numériques et l'efficacité algorithmique. En implémentant la même logique à travers **Java, Python et C++**, vous montrez la polyvalence et la profondeur – qualités hautement valorisées dans les rôles d'ingénierie logicielle.

---

Prochaines étapes

1. **Pratique**: Exécutez la solution avec différentes valeurs `n` et `k`.
2. **Optimiser**: Essayez d'exprimer la même idée dans le style fonctionnel (par exemple, en utilisant la récursion).
3. **Partager**: Ajoutez ce problème à votre portfolio GitHub avec des commentaires clairs et un README.

Bon codage, et bonne chance dans votre prochaine interview! Les

---

> **Mots clés**: LeetCode 1837, Somme des chiffres dans la base K, Solution Java, solution Python, solution C++, question d'entretien, interview algorithmique, complexité temporelle, complexité spatiale, entretien d'emploi, entretien technique, entretien de codage, conversion de base de nombres, opération modulo.

---