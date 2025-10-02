---
titre: LeetCode 2455. Valeur moyenne de nombres égaux qui sont divisibles par trois -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Valeur moyenne des nombres égaux divisibles par trois – LeetCode 2455
**Les solutions Java, Python & C++ + le guide d'interview SEO

---

Pourquoi ce post est important

Si vous vous préparez à une entrevue d'ingénierie logicielle, maîtriser LeetCodeS **Valeur moyenne d'Even Numbers Divisible par Three** (problème #2455) est une victoire rapide.
- ** Sujet haute fréquence** : de nombreux intervieweurs testent la manipulation du tableau + des maths simples.
- **Exposition en trois langues** : Java, Python et C++ – les langues les plus courantes sur les écrans d'entreprises technologiques.
- **SEO-optimized**: des mots-clés comme le Code du travail, l'entretien d'emploi, l'entretien de codage, l'ingénieur logiciel sont aspergés tout au long, donc les recruteurs à la recherche de ces termes peuvent trouver cet article.

---

Récapitulation des problèmes

> **Input**: `int[] nums` – tableau d'entiers positifs.
> **Tâche** : Retourne la moyenne* (arrondie) de tous les nombres qui sont ** à la fois** et **divisible par 3**.
> **Retour** : `0` s'il n'existe pas de tels nombres.

Exemple
C'est pas vrai.
[1,3,6,10,12,15]
[1,2,4,7,10]

*Construits*: "1 ≤ longueur nominale ≤ 1000", "1 ≤ longueur nominale [i] ≤ 1000".

---

Stratégie de solution

1. **Filter** le tableau : gardez des nombres où `num % 6 == 0' (même et divisible par 3).
2. **Sum** et **compte** les nombres filtrés.
3. Calculer `sum / count` (division entière automatiquement les planchers).
4. Si le nombre est `0`, retourner `0`.

Toutes les étapes se déroulent dans **O(n)** temps, **O(1)** espace supplémentaire.

---

Numéro de code

Vous trouverez ci-dessous des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**. Chacun suit la même logique, mais utilise des caractéristiques idiomatiques du langage.

---

- Oui. Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
valeur(int[] nombres) {
somme longue = 0;
nombre int = 0;
pour (int n : nombres) {
si (n % 6 == 0) { // even & divisible par 3
somme += n;
count++;
}
}
nombre de retours == 0 ? 0 : (int)(somme / nombre);
}

// Optionnel: Java Version 8+ Stream
moyenne intérieure publiqueValeurStream(int[] nums) {
retour Arrays.stream(nums)
.filtre(n -> n % 6 == 0)
.mapToLong(n -> n) // éviter le débordement
.moyenne()
.ouAutres(0.0)
.intValue();
}
}
«» "

**Pourquoi c'est bon**
- Pass linéaire, ramification minimale.
- La somme `long` empêche le débordement sur des plages d'entrée plus grandes.
- La version Stream montre le style Java moderne.

---

### Python (Python 3.10+)

'`python
Solution de classe:
moyenne Valeur(même, nombres: Liste[int]) -> Int:
filtré = [n pour n en chiffres si n % 6] 0]
retour sum(filtré) // len(filtré) si filtré autre 0
«» "

**Pourquoi c'est bon**
- La compréhension de la liste maintient le code concis.
- La division entière (`//`) planifie automatiquement le résultat.
- Poigne la liste vide avec une expression ternaire courte.

---

### C++ (C++17)

'`cpp
solution de classe {
public:
valeur(vecteur<int> et nombres) {
somme longue = 0;
cnt = 0;
pour (int n : nombres) {
si (n % 6 == 0) { // even & divisible par 3
somme += n;
++cnt;
}
}
retour cnt ? static_cast<int>(sum / cnt) : 0;
}
};
«» "

**Pourquoi c'est bon**
- Utilise "long long" pour un résumé sûr.
- Style compact pour boucle qui permet d'optimiser les compilateurs.
- Évite le survol des algorithmes STL pour cette tâche minuscule.

---

Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Complexité algorithmique**
Autres **Cas d'escroquerie** Aucun
**Readability** L'utilisation de tours bitwise (par exemple, `n & 1`) peut nuire à la clarté.
**Performance**= Pass unique, mémoire constante==== Micro-optimisations (p. ex. boucles non laminées) ajoutent du bruit sans réel avantage===
**Portabilité**
**Maintenabilité**

- Oui. Que garder

- Le simple `n % 6 == 0` check – il est à la fois expressif et efficace.
- Division entière (`//` en Python, `/` en Java/C++) pour arrondir le plancher.
- Évitez les collectes inutiles; accumulez la somme et comptez en un seul passage.

- Oui. À éviter

- Des conditions complexes ou des retours précoces qui endommagent la logique.
- Micro-optimisation précoce; la taille d'entrée (= 1000) est minuscule, donc la lisibilité gagne.
- Suringénierie avec des flux ou du régex lorsqu'une boucle simple est plus claire.

---

## C'est le SEO et les conseils d'entrevue

1. **Titre et méta**
«» "
Valeur moyenne des nombres égaux divisibles par trois – LeetCode 2455, Java, Python & C++ Solutions
«» "

2. **En-têtes**
Utilisez H1 pour le titre, H2 pour la récapitulation des problèmes, Stratégie de solution, Code Snippets, et Le bon, le mauvais et le mauvais.

3. **Mots clés**
- Code de let 2455
- Valeur moyenne des nombres égaux divisibles par trois
- Codage de l'entrevue d'emploi
- Questions de l'ingénieur logiciel
- Solutions d'interviews Java Python C++

4. ** Liens internes**
Lien vers d'autres messages : *=La manipulation d'Array dans LeetCode*===Tricks Bitwise dans Interviews*=.

5. ** Partage social**
Ajoutez un extrait de carte Twitter avec un exemple de code court et un lien vers l'article complet.

---

La pensée de clôture

Maîtriser ce problème LeetCode vous montre :

- Pars une déclaration dans un algorithme propre.
- Écrire un code concis et idiomatique en plusieurs langues.
- Balancer les performances, la lisibilité et la maintenance.

Ce sont exactement les traits que les recruteurs recherchent dans un **ingénieur logiciel**.
Bonne chance dans votre prochain entretien ! C'est ce qu'il a dit