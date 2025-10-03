---
titre: LeetCode 2180. Compte entiers avec même chiffres -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2180 – Nombre entiers avec même la somme à chiffres
- Oui. Un parcours complet et prêt à l'interview (Java, Python, C++)

**Mots clés**: LeetCode 2180, même somme de chiffres, algorithme, question d'entrevue, solution Java, solution Python, solution C++, entretien de codage, entretien d'emploi, défi de codage

---

### TL;DR
> **Objectif** – Compter tous les entiers positifs ≤ `num` dont la somme des chiffres est égale.
> **Constraints** – «1 ≤ num ≤ 1000».
> **Brute-force** – Iterate de 1 à `num`, additionner les chiffres de chaque nombre, et vérifier si la somme est égale.
> **Complexité** – temps "O(num * log10(num)"), espace "O(1)".
> **Résultat** – Fonctionne en **0 ms** pour toutes les entrées du jeu de problèmes.

---

- Oui. 1. Compréhension des problèmes

LeetCode 2180 demande une tâche de comptage simple, mais c'est un échauffement parfait pour les intervieweurs pour voir si vous:

1. **Traduisez l'énoncé de problème en une signature de fonction. **
2. **Pensez aux contraintes** (ici "num" est petit, donc une solution naïve est bonne).
3. **Écrire le code propre et idiomatique** dans la langue de votre choix.

> Pourquoi s'embêter avec les chiffres ? Pourquoi ne pas simplement utiliser un tour?
> – Parce que les contraintes rendent la solution la plus simple à la fois suffisante et rapide, de sorte que l'intervieweur est principalement intéressé par la clarté, la justesse et le style de code.

---

- Oui. 2. La mise en œuvre propre et idiomatique

On trouvera ci-dessous trois solutions ** qui fonctionnent avec succès**.
Les trois font exactement la même chose, juste exprimée dans le style de la langue.

### 2.1 Java (style LeetCode)

"Java
solution de classe publique {
Nombre d'entrées publiquesEven(int num) {
nombre int = 0;
pour (int i = 1; i <= num; i++) {
si [est EvenDigitSum(i)] count++;
}
le nombre de retours;
}

booléen privé estEvenDigitSum(int n) {
= 0;
pendant la période (n > 0) {
somme += n % 10;
n/= 10;
}
somme de retour % 2 == 0;
}
}
«» "

> *Pourquoi une méthode d'aide? *
> Conserve la boucle en ordre et rend la logique testable en isolement.

2.2 Python 3

'`python
Solution de classe:
Dénombrement Même (self, num: int) -> Int:
retour sum(1 pour i dans l'intervalle(1, num + 1) si self._even_digit_sum(i))

def _even_digit_sum(self, n: int) -> C'est vrai.
somme de retour(int(d) pour d en str(n)) % 2 == 0
«» "

> *Tricks pyroniques:*
> * `sum(1 pour ...)` compte les éléments correspondants.
> * La conversion en `str` et l' itération sur les chiffres est très lisible pour cette petite taille d'entrée.

C++ (style LeetCode)

'`cpp
solution de classe {
public:
nombre intEven(int num) {
cnt = 0;
pour (int i = 1; i <= num; ++i)
si (même DigitSum(i)) ++cnt;
retour cnt;
}

particulier:
même DigitSum(int n) {
= 0;
pendant que (n) {
somme += n % 10;
n/= 10;
}
somme de retour % 2 == 0;
}
};
«» "

---

- Oui. 3. Traitement des cas de bord

Pourquoi c'est important Comment le code le traite
C'est-à-dire...
"num = 1" , entrée la plus petite; seulement 1 entier pour vérifier. → `false` → retour 0
"num = 1000" , relié supérieur; nombres à 4 chiffres , alors que la boucle (n) gère tous les chiffres , encore O(1) espace ,
Aucune conversion en chaîne qui ajouterait des zéros

---

- Oui. 4. Complexité temporelle et spatiale

- **Heure**:
Pour chaque entier `i` nous inspectons ses chiffres.
Nombre de chiffres "log10(num)".
Total = `num * log10(num)` → avec `num ≤ 1000`, au plus 4 000 opérations à chiffres.

- **Espace**: "O(1)" – seulement quelques variables entières.

> *Pourquoi cela est acceptable* – La limite d'exécution LeetCode est généreuse ; toute implémentation fonctionnera en < 1 ms.

---

- Oui. 5. Le mal – Sur-ingénierie

Certains intervieweurs aiment vous voir penser à DP plus avancé ou à mordre.
Par exemple, vous pouvez construire une table DP `dp[pos][parité][harse]` qui compte des nombres avec un préfixe de parité donné.
Cela serait exagéré pour "num ≤ 1000" et ne ferait qu'accroître la complexité.

- Oui. Pourquoi l'éviter :

Raison de l'impact
C'est quoi ?
Autres Ajoute le code de la plaque de chaudière
Plus difficile à lire Moins de clarté
Autres Pas d'avantage de performance

---

- Oui. 6. Les pièges communs

Erreurs dans les résultats
- C'est quoi ?
Autres Oubliant que `num` lui-même est inclusive , Erreurs hors-par-un , Utilisez `<= num` dans la boucle ,
En utilisant "somme % 2". 1` au lieu de `== 0'-- Une mauvaise logique de parité. 0
Autres Convertir en chaîne pour les grandes entrées sans optimisation.
Autres Ne pas manipuler `num = 0`- Non autorisé par les contraintes mais toujours Ajouter garde `si (num <= 0) retour 0;` Autres

---

- Oui. 7. Conseils prêts pour l'entrevue

1. ** Expliquez votre approche d'abord** – Il suffit d'itérer sur chaque nombre et de vérifier la somme. (en milliers de dollars)
2. **Afficher l'aide** – Voici une petite méthode qui nous dit si la somme des chiffres est égale. (en milliers de dollars)
3. **La complexité des discussions** – -O(num * log10(num)) est bonne pour les contraintes données. (en milliers de dollars)
4. **Vérification des cas** – Et 1 ou 1000 ? Ça marche parce que nous traitons n'importe quel nombre de chiffres. (en milliers de dollars)
5. **Échelle des peines** – Si nous avions un énorme "num", nous pourrions utiliser le chiffre DP, mais c'est inutile ici. (en milliers de dollars)

---

- Oui. 8. Dernier départ

- ** La simplicité gagne** pour ce problème.
- Une solution ** propre, bien structurée** démontre la maîtrise des constructions de programmation de base, que les intervieweurs aiment.
- Oui. Les trois implémentations en langage sont prêtes à copier-coller dans LeetCode ou votre IDE.
- Oui. L'article de blog lui-même est **SEO-optimized** (mots clés, titres, sections lisibles) pour vous aider à obtenir un emploi en montrant votre style de résolution de problèmes.

---

- Oui. 9. Extraits de code prêts à rouler

"Java
// Java
solution de classe publique {
Int public countEven(int num) { /* ... */ }
}
«» "

'`python
# Python
Solution de classe:
Dénombrement Even(self, num: int) -> int: /* ... */
«» "

'`cpp
// C++
solution de classe {
public:
Int countEven(int num) { /* ... */ }
};
«» "

N'hésitez pas à les déposer dans votre environnement local, à les exécuter contre les cas de test de LeetCode et à laisser votre CV briller. Bon codage !