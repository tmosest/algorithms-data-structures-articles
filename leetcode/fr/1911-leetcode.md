---
titre: LeetCode 1911. Somme alternante maximale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 1911 – *Somme alternante maximale*
> **Java-Optimized Blog Post

---

TL;DR
- **Objectif:** Trouver la plus grande somme alternée possible de toute sous-séquence d'un tableau.
- ** Solution optimale :** PDD monopass avec deux variables d'exécution (`bestEven`, `bestOdd`).
- **Complexités:** **O(n)** temps, **O(1)** espace.
- **Pourquoi c'est important :** Démontre l'intuition cupide/DP, la conscience du débordement entier et le code propre – parfait pour une entrevue.

---

Récapitulation des problèmes

> La somme * alternante* d'un tableau indexé 0 est
> \[
> \sum_{\text{even }i} a_i \;-\; \sum_{\text{odd }i} a_i
> \]
>
> Avec un tableau "nums", choisissez n'importe quelle séquence (ordre conservé) et calculez sa somme alternée.
> Retournez la valeur maximale possible.

Obstacles
- "1 ≤ longueur nominale ≤ 105 "
- `1 ≤ nombres[i] ≤ 105'

---

C'est pas vrai.

**Quoi de bien**
Il y a un problème.
Une séquence comme `[1, 100, 2]` – cupides pics 100 seulement, mais `[1,100,2]` donne 101
**Formulation du PD**= 2 états capturent la parité du dernier élément choisi== Besoin de gérer les valeurs intermédiaires négatives/grandes== Très grandes sommes → débordement si l'on utilise `int`=
**Mise en oeuvre**= O(1) espace, pass simple== Indices faciles à gâcher= Oubliez qu'un subséquence peut être *vide* (mais les contraintes garantissent au moins un élément)=

Le DP propre bat l'avidité dans *tous* cas d'angle.
L'astuce est de se rappeler que la subséquence : *parité* (position uniforme/odd dans la subséquence, pas dans le tableau d'origine) décide si nous ajoutons ou soustraitons le nombre courant.

---

Le PDD optimal

Laissez

- `meilleurEven` – somme alternée maximale d'une sous-séquence qui se termine sur une position **even** (c'est-à-dire que nous *ajoutons* le dernier numéro choisi).
- `bestOdd` – somme alternée maximale d'une sous-séquence qui se termine sur une position **odd** (c'est-à-dire que nous *subtractons* le dernier numéro choisi).

Initialement "meilleur" Même = 0' (subséquence vide, somme = 0).
"meilleur" Odd` commence à `-..` parce que nous ne pouvons pas terminer sur un indice impair sans avoir pris au moins un élément.

Pour chaque nombre `x` en `nums`:

«» "
nouveaux Même = max(meilleur Même, bestOdd + x) // soit sauter x ou utiliser x à une position uniforme
newOdd = max(meilleur Odd, bestEven - x) // soit sauter x ou utiliser x à une position étrange
Même mieux, mieux vaut Odd = nouveau Même, nouveau Curieuse
«» "

À la fin `meilleurEven` est la réponse.

Pourquoi ça marche ?
La récurrence est un classique de prise ou de saut.
Nous conservons les meilleures sommes possibles pour les deux parités; la transition considère que le nouveau nombre est annexé à une séquence de la parité opposée (d'où `bestOdd + x` ou `bestEven - x`) ou simplement ignoré (`bestEven` / `bestOdd` inchangé).

---

Code (Java, Python, C++)

- Oui. 1. Java

"Java
Importation de java.util.*;

solution de classe publique {
public long maxAlternatingSum(int[] nums) {
longue meilleure Même = 0; // meilleure somme se terminant sur une position uniforme
longue meilleure Odd = Long.MIN_VALUE / 2; // -

pour (int x : nombres) {
longue nouvelle Même = Math.max (meilleurMême, meilleurOdd + x);
longue nouvelle Odd = Math.max(meilleur C'est bizarre, c'est mieux Même - x);
le meilleur Même = nouveau Même;
le meilleur Odd = nouveau Curieusement;
}
le meilleur retour Même;
}

// Pour des essais manuels rapides
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.maxAlternantSum(nouvelle int[]{4,2,5,3})); // 7
Système.out.println(s.maxAlternativeSum(nouvelle int[]{5,6,7,8}); // 8
System.out.println(s.maxAlternativeSum(nouvelle int[]{6,2,1,2,4,5})); // 10
}
}
«» "

> **Pourquoi `Long.MIN_VALUE / 2`?**
> Empêche `bestOdd + x` de déborder quand `bestOdd Odd ' est à 'Long. MIN_VALEUR'.

---

- Oui. 2. Python

'`python
Solution de classe:
def maxAlternatingSum(self, nombres: list[int]) -> Int:
best_even = 0 # somme se terminant par un indice uniforme
best_odd = -10**18 # efficacement

pour x en nombres:
new_even = max(best_even, best_odd + x)
new_odd = max(best_odd, best_even - x)
best_even, best_odd = new_even, new_odd

retour _meilleur

# Essais manuels rapides
si __nom__ == "__main__" :
sol = Solution()
print(sol.maxAlternativeSum([4,2,5,3])) # 7
print(sol.maxAlternativeSum([5,6,7,8)]) # 8
print(sol.maxAlternatingSum([6,2,1,2,4,5])) # 10
«» "

> **Pourquoi utiliser `-10**18`? **
> Les nombres entiers de Python sont arbitraires-précision, mais l'utilisation d'une grande sentinelle négative maintient la logique claire.

---

- Oui. 3. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long long maxAlternatingSum(vecteur<int>& nums) {
longue longue meilleure Même = 0; // meilleure somme se terminant en position uniforme
longue longue meilleure Odd = LLONG_MIN / 4; // -.

pour (int x : nombres) {
long long nouveau Même = max(meilleur Même, bestOdd + x);
long long nouveau Odd = max(meilleur C'est bizarre, c'est mieux Même - x);
le meilleur Même = nouveau Même;
le meilleur Odd = nouveau Curieusement;
}
le meilleur retour Même;
}
};

// Exemple d'utilisation
Int main() {
Solution s;
vecteur<int> a1 = {4,2,5,3};
vecteur<int> a2 = {5,6,7,8};
vecteur<int> a3 = {6,2,1,2,4,5};
Cout << s.maxAlternationSum(a1) << endl; // 7
Cout << s.maxAlternationSum(a2) << endl; // 8
Cout << s.maxAlternationSum(a3) << endl; // 10
}
«» "

> **Pourquoi `LLONG_MIN / 4`?**
> Évite les débordements accidentels en ajoutant `x`. Dans la pratique, `LLONG_MIN/4` est bien inférieur à toute somme intermédiaire possible.

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Autres Un balayage au-dessus de `nums`.
Frais généraux supplémentaires Autres

`n ≤ 105`, de sorte que l'algorithme s'adapte confortablement dans les limites de temps et utilise une mémoire négligeable.

---

Article de blog optimisé par le SEO

> **Titre:**
> *LeetCode 1911: Master the Maximum Alternating Subsequence Sum in Java, Python & C++ – A Job‐Interview Essential*

---

Introduction

Lors de la préparation d'une entrevue d'ingénierie logicielle, le problème *Maximum Alternating Subsequence Sum* (LeetCode 1911) apparaît souvent sur la liste -must-know. Il teste la capacité d'un candidat à penser à **parité**, **programmation dynamique**, et **pièges agréables** – compétences que tous les gestionnaires d'embauche recherchent.

Dans ce post, nous traversons le problème, fournissons des implémentations propres dans **Java**, **Python** et **C++**, et expliquez pourquoi l'approche DP est la norme d'or. Que vous soyez un codeur junior ou un ingénieur senior qui polit vos compétences algorithmiques, ce guide vous aidera à comprendre la question et impressionnera vos intervieweurs.

---

### Énoncé de problème (court et doux)

> Compte tenu d'un tableau «nums», trouver la somme alternée maximale de toute séquence subséquente après avoir réindexé les éléments.
> *Somme alternative* = somme d'éléments à indice pair moins somme à indice impair.

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
Prendre la subséquence `[4,2,5]`: `(4+5) - 2 = 7`
La meilleure séquence est `[8]` Autres
"[6,2,1,2,4,5]"" "10"" Subséquence "[6,1,5]" : "(6+5) - 1 = 10"

**Contrôles* *

- "1 ≤ longueur nominale ≤ 105 "
- `1 ≤ nombres[i] ≤ 105'

---

Pourquoi ça compte pour les entrevues

- **Manipulation de la rareté** – Beaucoup d'intervieweurs vérifient si vous comprenez qu'Even/odd-
- **Efficacité spatiale** – La solution optimale utilise l'espace O(1), une exigence commune pour les questions d'entrevue à haute performance.
- ** Sensibilisation à l'excès** – L'utilisation d'entiers 64 bits («long»/«long long») est essentielle; les solutions naïves «int» échouent sur de grands cas d'essai.

---

- Oui. L'erreur d'avidité

Une solution tentante est de choisir avidement les plus grands nombres alternativement.
Cependant, il échoue sur des séquences comme `[1, 100, 2]`.
Greedy choisirait `100` seul (somme = 100), mais la subséquence optimale est `[110,2]` → `(1+2)-100 = -97`? Attends, c'est plus petit. En fait, dans ce cas, cupide fonctionne. Mais considérez `[1, 2, 3]`: les pics gourmands `3` → 3; l'optimum est `[1,3]` → `(1+3) - 2 = 2`. Greedy manque l'avantage d'avoir un élément étrange entre les deux. Ceci illustre pourquoi une approche PDD qui tient compte des deux parités est nécessaire.

---

La solution de PDD élégante

C'est vrai. Idée clé

Maintenir deux variables :

- `meilleurEven`: somme alternée maximale d'une sous-séquence se terminant sur une position **even**.
- "bestOdd" : somme alternée maximale d'une sous-séquence se terminant sur une position **odd**.

À chaque étape, nous décidons d'utiliser *le nombre courant ou *skip*. Si nous l'utilisons, nous devons inverser la parité de la subséquence, d'où les transitions :

«» "
nouveaux Même = max(meilleur Même, le meilleur Moyenne + x)
newOdd = max(meilleur C'est bizarre, c'est mieux Même - x)
«» "

Enfin, Même 'est la réponse.

Pourquoi ça marche ?

Il s'agit d'une prise ou d'un saut classique.
Chaque transition considère la meilleure séquence possible de la parité opposée, ajoute le nombre actuel de façon appropriée, ou l'ignore.
Parce que nous utilisons toujours les sommes les plus connues pour chaque parité, nous ne manquons jamais une meilleure séquence plus tard.

---

Mise en œuvre complète

> **(Voir les extraits de code ci-dessus – Java, Python, C++)* *

N'hésitez pas à copier/coller dans votre IDE ou éditeur en ligne. Chaque implémentation suit le même modèle d'espace O(n) et O(1).

---

Gestion des dépassements

Lorsque nous commençons `bestOdd` avec `Long.MIN_VALUE` (ou `LLONG_MIN`), ajouter `x` peut déborder.
Une astuce sûre : utilisez une grande sentinelle négative comme `-10**18` (Python) ou `LLONG_MIN / 4` (C++/Java).
Cela maintient la logique intacte et protège contre les cas de test cachés qui poussent la somme près de 263.

---

Résumé

Pourquoi c'est une solution Go-To
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Java **= O(n) time, O(1) space== Utilise un « long » 64 bits; style propre orienté objet==
**Python**=O(n) temps, espace O(1)=Simplicité et lisibilité, sécurité de précision arbitraire=
**C++**. O(n) time, O(1) space.

La méthode DP est simple, rapide et robuste. Maîtrisez-le, et vous gérerez les problèmes de subséquence basés sur la parité avec confiance.

---

Pratique, pratique, pratique

- **Temps vous-même** sur les exemples fournis et quelques tests aléatoires.
- **Boîtiers de bords de série** : tableaux monotoniques, alternance de motifs hauts/bas et longueur maximale autorisée avec toutes les valeurs = 105.
- **Expliquez le PDD à un ami** ou même à haute voix dans une interview simulée; l'articulation est aussi importante que le code.

---

Mot final

LeetCode 1911 est plus qu'un simple exercice de codage ; c'est un test de *clairance conceptuelle* et de *robustness*.
Avec la solution DP ci-dessus, vous pouvez approcher avec confiance tout entretien d'emploi qui jette ce problème à votre façon.

Codage heureux, et que vos entretiens soient aussi lisses que notre `meilleur Même la transition !

---

> *Pour plus d'articles prêts à l'entrevue, abonnez-vous à notre newsletter et recevez des défis d'algorithme hebdomadaires directement dans votre boîte de réception. *

---

À emporter

- ** Pensez toujours à la parité subséquemment**, pas aux indices originaux.
- Gardez deux *meilleures sommes* : même → ajouter, impair → soustraire.
- Mettre à jour les transitions `max(skip, take)`.
- Utilisez des entiers 64 bits pour éviter les débordements.

Implémentez le DP une fois en Java, Python et C++ ; maintenant vous êtes prêt à résoudre LeetCode 1911 dans n'importe quelle langue que vos intervieweurs choisissent. Bonne chance !

---

Étiquettes

`algorithmes`, `dynamique-programmation`, `leetcode`, `Java`, `Python`, `C++`, `entrevue-préparation`, `entrevue-emploi`, `parité`, `greedy "

---

**Auteur:** *Votre nom – Ingénieur principal du logiciel et de l'algorithme
**Suivez sur Twitter:** @Votre poignée
**Newsletter:** Abonnez-vous aux défis algorithmiques hebdomadaires.

---

Clôture

Le *Maximum Alternating Subsequence Sum* est un micro-leçon parfait sur **comment concevoir un DP qui suit brièvement**.
Lorsque vous pouvez expliquer clairement cette approche dans une entrevue, vous ne répondez pas seulement à un seul problème – vous montrez les intervieweurs *mindset* : propres, efficaces et conscients des cas de bord.

Bonne chance ! C'est ce qu'il a dit.

---

Bonus : Liste de contrôle rapide pour l'entrevue

1. **Lire le problème** – confirmer la compréhension de *parité subséquemment*.
2. **Planifier le PDD** – deux variables pour les sommes paires/imprimées.
3. **Utilisez 64 bits entiers** – `long` / `long` / Python int.
4. ** Pass unique** – itérer une fois au-dessus des "nums".
5. **Retour** `meilleurEven` (séquence se terminant par une position uniforme).
6. ** Expliquez à l'intervieweur votre récurrence.

---

* Fin de poste*

---

**Mots clés**: LeetCode 1911, somme alternée maximale, programmation dynamique, problème d'entrevue, implémentation Java, implémentation Python, implémentation C++, entretien d'emploi, algorithme, parité, espace O(1).

---

> *Restez à l'écoute pour notre prochain post: Haut 10 LeetCode Problèmes Chaque ingénieur senior devrait maîtriser.

---

*Bon code ! *

---

(Fin de l'article du blog)

---

Bonus: Exécutez le code localement

Si vous voulez tester la solution Java localement, copiez simplement la classe ci-dessus dans un fichier nommé `Solution.java`, compilez avec `javac Solution.java`, et exécutez `java Solution`.

Pour Python, lancez `python3 solution.py`.
Pour C++, compiler avec `g++ -std=c++17 solution.cpp -O2 -Wall &&./a.out'.

Tous les produits correspondent aux résultats escomptés.

---

Pensée de clôture

L'élégance algorithmique n'est pas seulement une question de vitesse, il s'agit aussi de *clarité* et de *robustness*.
La solution DP de LeetCode 1911 démontre que : une seule ligne de récurrence, deux variables « longues » et une boucle.
Avec cela dans votre boîte à outils, vous êtes un pas plus près d'avoir cette prochaine interview.

Bonne chance, et que vos emplois soient aussi bons que les sommes que vous calculez! C'est ce qu'il a dit.

---

* Fin de l'article. *

---

** Fait!**

---

> Si vous avez aimé ce contenu, partagez-le avec des amis ou laissez un commentaire ci-dessous avec vos propres astuces d'implémentation!

---