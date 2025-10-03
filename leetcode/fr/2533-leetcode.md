---
Titre: LeetCode 2533. Nombre de bonnes cordes binaires -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2533 – Nombre de bonnes cordes binaires
**Moyenne= 1 ≤ minDurée ≤ maxDurée ≤ 105= 1 ≤ unGroupe, zéroGroupe ≤ maxDurée* *

> Dans une chaîne binaire *good*
> 1. Longueur [minLength, maxLength]
> 2. Chaque bloc consécutif de `1`s a une longueur qui est un multiple de `un Groupe»
> 3. Chaque bloc consécutif de `0`s a une longueur qui est un multiple de `zéro Groupe»
> 4. (Zero est considéré comme un multiple de tout)

Retourne le nombre de bonnes cordes modulo 1 000 000 007.

---

Une idée de haut niveau

Les contraintes (maxLength ≤ 105) interdisent d'énumérer toutes les cordes.
Au lieu de cela, observez qu'une bonne corde peut être construite **incrémentalement**:

* À partir d'une chaîne vide (longueur = 0, qui satisfait à la règle de "multiple").
* Chaque étape s'ajoute soit
* `un groupe` consécutif `1`s, **ou* *
* `zéroGroupe` consécutif `0`s.

Donc, si nous savons combien de bonnes chaînes de longueur `i` existent (`dp[i]`), nous pouvons obtenir le nombre de longueurs plus longues en ajoutant les deux tailles de blocs possibles.

C'est une récurrence de programmation dynamique classique *bottom-up*.

«» "
dp[0] = 1 // chaîne vide
pour i = 1 ... maxLength
i ≥ unGroupe: dp[i] += Dp[i - un groupe]
i ≥ zéroGroupe: dp[i] += dp[i - zéroGroupe]
Dp[i] %= MOD
«» "

La réponse est la somme de `dp[i]` pour tous `i` dans `[minLength, maxLength]`.

La récurrence se déroule dans **O(maxLength)** temps et a besoin **O(maxLength)** mémoire – assez rapide pour 105.

---

Code Marche à travers (Java)

"Java
Importation de java.util.*;

solution de classe {
int final statique privé MOD = 1_000_000_007;

Int goodBinaryStrings(int minLength, int maxLength,
Int un Groupe, int 0 Groupe) {

// dp[i] = nombre de bonnes chaînes de longueur i
int[] dp = nouvelle int[maxLength + 1];
dp[0] = 1; // chaîne vide

résultat long = 0;

pour (int i = 1; i <= maxLength; i++) {
si (i >= un groupe) {
dp[i] = (dp[i] + dp[i - un groupe]) % MOD;
}
si (i >= zéroGroupe) {
dp[i] = (dp[i] + dp[i - zéroGroupe]) % MOD;
}
si (i >= minLength) {
résultat = (résultat + dp[i]) % MOD;
}
}

retour (int) résultat;
}
}
«» "

**Points clés* *

Explication
C'est pas vrai.
La chaîne vide compte comme un préfixe valide (zéro est un multiple de tout). Autres
"si (i >= oneGroup)""Supportez seulement quand nous avons assez de place pour un nouveau bloc. Autres
"résultat += dp[i]"" Somme seulement lorsque la longueur satisfait à la condition minimale. Autres

---

## Code Marche à travers (Python)

'`python
Solution de classe:
MOD = 1 000 000 007

def goodBinaryStrings(self, minDurée: int, maxDurée: int,
unGroupe: int, zéroGroupe: int) -> Int:

dp = [0] * (longueur maximale + 1)
dp[0] = 1 # chaîne vide
résultat = 0

pour i dans la plage (1, maxLongueur + 1):
i >= un Groupe :
dp[i] = (dp[i] + dp[i - oneGroup]) MOD
i >= zéroGroupe:
dp[i] = (dp[i] + dp[i - zéroGroupe]) % soi-même. MOD
i >= Durée minimale:
résultat = (résultat + dp[i]) MOD

résultat du retour
«» "

Même logique, juste syntaxe pythonique.

---

## Code Marcher (C++)

'`cpp
solution de classe {
public:
static const int MOD = 1'000'000'007;

Int goodBinaryStrings(int minLength, int maxLength,
Int un Groupe, int 0 Groupe) {
vecteur<int> dp(longueur max + 1, 0);
dp[0] = 1; // chaîne vide
longue rés = 0;

pour (int i = 1; i <= maxLength; ++i) {
i (i >= un groupe)
dp[i] = (dp[i] + dp[i - un groupe]) % MOD;
i (i >= zéroGroupe)
dp[i] = (dp[i] + dp[i - zéroGroupe]) % MOD;
si (i >= minLength)
res = (rés + dp[i]) % MOD;
}
retourner static_cast<int>(res);
}
};
«» "

---

Analyse de complexité

Java Python C++
C'est pas vrai.
Temps (max) Autres
* Espace * * (longueur maximale) * (longueur maximale) * (longueur maximale) * (longueur maximale) Autres

Tant le temps que l'espace sont linéaires dans la longueur maximale de la chaîne – parfait pour 105.

---

Bonne, la mauvaise et la mauvaise

Aspect du bien
C'est pas vrai.
**Désignation**
Autres **Cas d'escroquerie**
**Readability**
**Évoluabilité**
**Pièges potentiels**
**Utilisation de la mémoire**
**Supplément de l'approche**=Mémoisation du haut vers le bas (récursive)==Peut frapper la profondeur de récursion sur une grande entrée=
**Optimisation**

**Pourquoi bas- C'est le gagnant**
- Évite les limites de récursion.
- Une seule passe sur la longueur.
- Oui. Pas besoin de structures de données supplémentaires au-delà du tableau `dp`.

---

Article de blog optimisé par le SEO

> **Titre**
> *Code du leet 2533 – Nombre de bonnes cordes binaires – Tutoriel Java, Python & C++ DP*

> **Description détaillée**
> Master LeetCode 2533 avec une solution de programmation dynamique claire en Java, Python et C++. Apprenez l'algorithme, la complexité et les idées prêtes à l'entrevue.

> **Mots clés**
> LeetCode 2533, Nombre de bonnes chaînes binaires, programmation dynamique, entretien de codage, solution Java, solution Python, solution C++, entretien d'ingénieur logiciel, conception d'algorithmes

---

Introduction

Quand j'ai vu la première fois **LeetCode 2533 – Nombre de bonnes cordes binaires**, je pensais que ce n'était qu'un autre problème de chaînes de compte. La torsion ? Les blocs de cordes doivent être *multiples* de tailles de groupe données.
Dans une entrevue, l'intervieweur veut généralement que vous montriez deux choses :

1. Vous comprenez les contraintes et pouvez choisir un algorithme efficace.
2. Vous pouvez traduire cet algorithme en code idiomatique propre dans la langue choisie.

Ci-dessous, je marche à travers la solution DP qui fonctionne dans **O(n)** temps, vous donner prêt-à-coller Java, Python, et C++ extraits, et expliquer pourquoi cette approche est parfaite pour une entrevue de codage.

---

Rétablissement du problème

Une chaîne binaire *good* satisfait :

- Longueur "[minLength, maxLength]".
- Chaque série consécutive de `1`s a une longueur qui est un multiple de `oneGroup`.
- Chaque course consécutive de `0`s a une longueur qui est un multiple de `zéro Groupe».

Retourne le nombre de bonnes chaînes modulo `109+7`.

Les contraintes rendent impossible une énumération naïve (chaînes '2^maxLength'). Il nous faut une solution *linéaire*.

---

### La perspective fondamentale

Une bonne chaîne peut être **grave** d'une chaîne vide en ajoutant à plusieurs reprises un bloc de longueur `oneGroup` ou `zeroGroup`.
Si nous indiquons :

«» "
dp[i] = nombre de bonnes chaînes de longueur exacte i
«» "

puis pour tout «i»:

«» "
dp[i] = (dp[i - unGroupe] si i ≥ unGroupe) +
(dp[i - zéroGroupe] si i ≥ zéroGroupe)
«» "

Comme la chaîne vide (longueur 0) satisfait à la condition multiple, nous commençons par `dp[0] = 1`.
La réponse finale est la somme de `dp[i]` pour tous `i` dans `[minLength, maxLength]`.

---

### Mise en oeuvre étape par étape

1. **Initialiser** `dp[0] = 1`.
2. **Itérer** `i` de `1` à `maxLength`.
3. **Mise à jour** `dp[i]` en utilisant la récurrence (attention avec `i - bloc` seulement si elle est non-négative).
4. **Modulo** le résultat après chaque ajout pour éviter le débordement.
5. ** Accumuler** dans la réponse lorsque «i ≥ minLength».

C'est à ça que ressemblent les trois solutions linguistiques – juste des différences de syntaxe.

---

### Java, Python, & C++ Code

* (extraits de code complets ci-dessus)*

> **Conseil pour l'intervieweur**
> Vous souvenez-vous d'appliquer le modulo après chaque ajout ? L'intervieweur va vous tester sur le débordement entier.

---

Débat sur la complexité

- **Heure**: Nous touchons chaque index une fois – "O(maxLength)".
- **Espace**: Un tableau de taille `maxLength+1` – `O(maxLength)`.

Avec `maxLength ≤ 105`, cela fonctionne en millisecondes sur les machines modernes.

---

### Interview-Ready Variations

Variation de la date d'utilisation
C'est pas vrai.
**Bottom-Up DP (celui ci-dessus)
Si vous préférez la récursion, plus facile à écrire au départ, la profondeur de récursion peut atteindre la limite de Python, légèrement plus lente en raison des appels de fonction.
**Récursif + Mémo**

---

- Oui. Pourquoi cette solution est-elle

Explication
C'est pas vrai.
*Horaires linéaires*
*Simple tableau *= Mémoire minimale au-dessus. Autres
*Arithmétique modulaire* Autres
Une boucle, deux conditions – parfait pour une réponse d'entrevue propre. Autres

---

### Envelopper

- **LeetCode 2533** est un grand problème d'entrevue pour tester *state compression* et *block-based DP*.
- Oui. La récurrence est **directement dérivé** de la description du problème.
- Le code Java, Python et C++ fourni est prêt à la production : commenté, utilise des constantes et respecte la contrainte modulo.

Si vous préparez un entretien *ingénieur logiciel*, cette solution démontre :

- Compréhension profonde des contraintes.
- Capacité de concevoir une récurrence PDD.
- La fluidité dans trois des langues d'entrevue les plus populaires.

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---

Code à emporter

Code de la langue
-- -- -- -- -- --
*Java**
*Python *Python
**C++**

---

**Sentez-vous libre de copier-coller ces solutions dans votre panneau de soumission local ou LeetCode. Bonne résolution !**