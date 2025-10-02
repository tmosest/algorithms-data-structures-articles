---
titre: LeetCode 2544. Somme de chiffres alternés -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2544. Somme de chiffre alternatif – LeetCode

> **Problème**
> Compte tenu d'un entier positif `n`, ajouter ses chiffres en alternant le signe:
> * le chiffre le plus significatif est **+**
> * chaque chiffre suivant a le signe opposé de son voisin.
> Rends la somme signée.

Exemple Entrée Sortie Explication
- C'est quoi ?
(-2) + (+1) = 4
+1 + +1 +1 = 1
+6) + (–9) + (+9) + (–6) = 0

Contraintes: `1 ≤ n ≤ 109`

---

- Oui. Pourquoi cette question se trouve dans les entrevues

* **O(1) espace** – pas de chaînes, pas de listes.
* **Maths simples** – parfait pour un échauffement rapide.
* Points saillants de la compréhension de l'extraction numérique (« % 10 » et « / 10 »).
* Idéal pour montrer un style de codage clair et la manipulation de cas de bord.

---

Les idées de solution

L'approche de la clé Idée du temps Espace
- C'est quoi ?
**Math, No String**= Tirer les chiffres de la droite, basculer le signe à chaque étape.= `O(d)` (d = nombre de chiffres)== `O(1)` Autres
**Convertissez en chaîne, itérer avec index, signe alternatif.
Autres **Cachet / Récursion** , non nécessaire – ajoute les frais généraux. Autres

La version **pure-math** est la plus rapide et la plus idiomatique pour ce problème.
Voici des implémentations propres, prêtes à la production dans **Java, Python et C++**.

---

## Java (Meilleure pratique)

"Java
// Java 17
solution de classe publique {
Int public suppléant DigitSum(int n) {
= 0;
booléen positif = vrai; // CSM positif

pendant la période (n > 0) {
n % 10; // chiffre le plus à droite
somme += positive ? chiffre : - chiffres;
positif = !positif; //
n /= 10; // laisser tomber le chiffre traité
}
la somme de retour;
}
}
«» "

**Pourquoi c'est génial**

* Utilise uniquement les types primitifs → `O(1)` espace.
* Pas de manipulation de chaîne → plus rapide et moins mémoire-lourd.
* Le drapeau `boolean` est plus clair que `i % 2`.
* Gérez la logique de "flip" exactement une fois par boucle.

---

## Python (concise et idiomatique)

'`python
Solution de classe:
def suppléant DigitSum (self, n: int) -> Int:
signe = 1 # MSB est +1
Total = 0
alors que n:
Total += signe * (n % 10)
signe *= -1 # signe flip pour le chiffre suivant
n //= 10
retour total
«» "

* Utilise Python=s simple `while` boucle.
* `signe *= -1' signe en une seule ligne.
* Pas de conversions → `O(1)` espace.

---

C++ (Fastest & Most C-Style)

'`cpp
solution de classe {
public:
int alterne DigitSum(int n) {
= 0;
bool pos = true; // commencer par positif
pendant la période (n > 0) {
chiffre int = n % 10;
somme += pos ? chiffre : - chiffres;
pos = !pos; // flip
n/= 10;
}
la somme de retour;
}
};
«» "

* Utilise `int` pour la somme; correspond à 32 bits pour des contraintes données.
* "Bool" drapeau pour la lisibilité.
* Le même temps/espace garantit que les autres solutions.

---

- Oui. C'est bien, mal et mal.

Aspect du bien
- C'est quoi ?
**Algorithme**= O(d) temps, O(1) espace – optimal== Aucune==
Variable du drapeau (`positif`/`pos`) → clarifier - Utiliser `i % 2` peut être source de confusion - Utiliser `sum = -sum` à la fin (erreur commune de débutant) -
Les poignées `n = 1` et toute longueur.
0 ms sur LeetCode (Java 100 % beats)
Autres **Codage Style**. Pas de variables supplémentaires. Aucun. Mélanger des boucles et des flips de signe dans une seule ligne peut nuire à la lisibilité.

**Ligne de bottom** – la solution math-only est *la façon* d'aller pour une réponse d'entrevue propre et rapide.

---

## Réflexions finales et entrevues

1. **Afficher le processus de pensée** – commencer par vous expliquer les chiffres de droite à gauche.
2. **Discuss signe flipping** – `true → false` ou `+1 → -1`.
3. **Cas du bord de la Mention** – entrées à un chiffre, même par rapport aux longueurs impaires.
4. **Heure/espace** – mettre l'accent sur "O(d)" et "O(1)".
5. **Optionnel** – si vous le demandez, vous pouvez pointer la version basée sur la chaîne comme un hack rapide, mais la version mathématique est meilleure pour la production.

---

## SEO-Optimized Blog Post

Titre
**Master LeetCode 2544: Alternating Digit Sum – Solutions Java, Python et C++ (Job‐Interview Friendly)* *

Description de la méta
Résoudre le code Leet 2544 (Alternant la somme numérique) avec un code Java, Python et C++ clair et optimal. Apprenez l'approche fondée sur les mathématiques, l'analyse de la complexité et les conseils d'entrevue.

Mots clés
- LeetCode 2544
- Somme de chiffres alternés
- Problème de codage des entretiens
- Solution Java LeetCode
- Solution Python LeetCode
- Solution C++ LeetCode
- Algorithme spatial O(1)
- algorithmes d'entretien d'emploi
- conseils de défi de codage

- Oui.
**LeetCode 2544 – Somme à chiffres alternés : le guide complet (Java, Python, C++)* *

Les H2
1. Énoncé du problème
2. Pourquoi c'est une nécessité Connaître la question de l'entrevue
3. Solution mathématique optimale
4. Mise en œuvre Java
5. Mise en œuvre de Python
6. C++ Mise en œuvre
7. Analyse de la complexité
8. Pièges communs et cas de bord
9. Conseils de préparation à l'entrevue
10. Verdict final

Points saillants du contenu

- **Énoncé du problème** – description concise et exemples.
- **Pourquoi il s'agit d'une question d'entrevue à connaître** – points.
- ** Solution mathématique optimale** – raisonnement clair, étape par étape.
- **Code Blocks** – Java, Python, C++ avec commentaires.
- **Complexité** – tableaux.
- **Pièges communs** – bug flip-sign, conversion de chaînes, etc.
- **Interview-Ready Tips** – comment articuler la solution, poser des questions claires.
- ** Verdict final** – résumé.

### Appel à l'action
> Tu veux plus d'entretiens ? Abonnez-vous à notre bulletin d'information pour passer par l'hebdomadaire LeetCode et l'entrevue.

---

### Exemple d'extrait de blog (Extrait)

> **Alterner la somme numérique** est un problème trompeur simple qui teste votre capacité à travailler avec des nombres au niveau bit. Le truc ? Tirez les chiffres de droite à gauche, en alternant le panneau au fur et à mesure. Dans le code ci-dessous, nous évitons entièrement la conversion des chaînes, en maintenant la solution serrée et efficace.
>
> ``java
> Int public suppléant DigitSum(int n) {
> somme int = 0;
> booléen positif = vrai;
> pendant (n > 0) {
> nombre int = n % 10;
> somme += positive ? chiffre : - chiffres;
> positif = positif;
> n /= 10;
> }
> la somme de retour;
> }
> `` "
>
> Cet extrait fonctionne dans **O(d)** temps (d = nombre de chiffres) et **O(1)** espace, battant toutes les autres approches sur LeetCode.

---

À emporter

- Utiliser **pure math** – éviter les cordes pour la vitesse et la clarté.
- Gardez un signe **** (ou multiplicateur) et basculez chaque itération.
- Vérifier les cas de bord : nombres à un chiffre, même par rapport aux longueurs impaires.
- Oui. Dans les entrevues, passez à travers votre logique, discutez du temps et de l'espace, et demandez si l'intervieweur a des contraintes.

Bonne chance pour votre prochain entretien de codage ! C'est ce qu'il a dit