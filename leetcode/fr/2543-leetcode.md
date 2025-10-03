---
titre: LeetCode 2543. Vérifiez si le point est accessible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2543 – *Vérifier si le point est accessible*
**Audience cible** – toute personne se préparant à une entrevue technique ou cherchant à maîtriser les mathématiques algorithmiques.
**Langues** – Java, Python, C++
**Traitement des clés** – **Vous pouvez atteindre \((cibleX, cibleY)\) à partir de \((1,1)\) iff \(\gcd(cibleX, cibleY)\) est une puissance de 2.**

Vous trouverez ci-dessous une mise en œuvre prête à la production pour chaque langue ainsi qu'un article de style blog qui explique le raisonnement, les pièges et les idées favorables aux entrevues.

---

- Oui. 1. Code

#### 1.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public booléen isReachable(int cibleX, int cibleY) {
// gcd de java.lang. Mathématiques (Java 17+)
g = Math.gcd(cibleX, cibleY); // ou java.math. Grand entier
// Vérifiez si g est une puissance de deux: un seul bit set
retour (g & (g - 1)) 0;
}
}
«» "

> **Pourquoi `Math.gcd`?**
> Java 17+ expose `Math.gcd`. Si vous êtes sur un JDK plus vieux, il suffit d'importer `java.math. BigInteger` ou écrire une petite fonction Euclid.

#### 1.2 Python 3

'`python
d'importation de mathématiques gcd

Solution de classe:
def isReachable(self, cibleX: int, cibleY: int) -> C'est vrai.
g = gcd(cibleX, cibleY)
# Puissance de deux essais : un seul jeu de bits
retour (g & (g - 1)) 0
«» "

> **Python 3.9+** inclut déjà `math.gcd`; sinon `gcd` peut être écrit manuellement.

### 1.3 C++ (GCC/Clang)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
bool isReachable(int cibleX, int cibleY) {
int g = std::gcd(cibleX, cibleY); // C++17
retour (g & (g - 1)) == 0; // puissance de deux?
}
};
«» "

> **`std::gcd`** fait partie de `<numérique>` dans C++17; `<bits/stdc++.h>` la tire automatiquement.

> **Conseil pour les intervieweurs** – Si vous êtes invité à implémenter le GCD vous-même, laissez tomber une boucle Euclid classique :

'`cpp
int myGcd(int a, int b) {
b) { a %= b; swap(a, b); }
retour a;
}
«» "

---

- Oui. 2. Article de style blog

> *Sentez-vous libre de copier l'article dans un blog Markdown, un message LinkedIn ou un portfolio personnel. *

```markdown
# Vérifiez si le point est accessible – le bon, le mauvais, et le mauvais
Une plongée profonde en LeetCode 2543 pour Java, Python & C++

Table des matières
- [Aperçu du problème] (#problème-aperçu)
- [Le point de vue mathématique]
- [Trajet algorithmique] (#trajet algorithmique)
- [Tarifs de complexité et de bord] (#Tarifs de complexité)
- [Pièges communs (les affreux)]
- [Conseils et conseils d'entrevue] (#conseils d'entrevue)
- [Pourquoi ça compte dans un processus d'embauche]
- [Davantage de lecture et de pratique]
«» "

### Aperçu du problème

«» "
Vous êtes debout à la coordonnée (1, 1) sur une grille entière infinie.
Vous pouvez appliquer à plusieurs reprises l'un des mouvements suivants :

(x, y) → (x, y - x)
(x, y) → (x - y, y)
(x, y) → (2*x, y)
(x, y) → (x, 2*y)

Étant donné que deux entiers cibleX et cibleY (1 ≤ cibleX, cibleY ≤ 1e9), déterminer s'il est possible d'atteindre (cibleX, cibleY) à partir de (1, 1) en utilisant toute séquence de mouvements.
«» "

À première vue, cela ressemble à un problème de recherche graphique, mais c'est un puzzle classique *number-theory*. Un BFS naïf exploserait – l'espace d'état est débordé. La vraie magie vient de comprendre comment les opérations affectent le plus grand diviseur commun (GCD) des deux coordonnées.

### Le bon – Un GCD à une seule ligne Vérification

L'ensemble du problème s'effondre en une seule opération GCD** et un test *power-of-deux*. C'est pourquoi la solution GCD One‐Line est populaire sur LeetCode:
"``gcd & (gcd-1) == 0```
fonctionne dans l'espace O(log min(x, y)) et O(1). Les trois étapes clés sont les suivantes :

1. Calculer `g = gcd(cibleX, cibleY)' (algorithme euclidéen).
2. Éliminer chaque facteur de 2: `alors que (g % 2 == 0) g /= 2;` (facultatif).
3. Si le `g` restant est 1 → accessible, sinon → inaccessible.

Le «g & (g-1)» Astuce est une astuce qui vous dit si `g` a exactement un bit set - c'est-à-dire que `g` est 2^k.

### Les mauvais – Pourquoi le BFS naïf se trompe

* **Espace infini d'état** – Les mouvements double coordonnées, donc l'arbre de recherche explose exponentiellement.
* **Blow-up** – Même une recherche en largeur qui maintient un `HashSet<(x, y)>` va atteindre la limite de 256 Mo rapidement pour des valeurs proches de 1e9.
* **Time-out** – Répéter les soustractions `(x, y-x)` et `(x-y, y)` est équivalent à l'algorithme euclidien, mais vous l'écririez à la main dans la boucle BFS, gaspillant des facteurs constants.

> **À emporter :** Dans une entrevue, commencez par demander *=Comment le GCD change-t-il dans chaque opération ? Cette question guide naturellement la discussion vers l'algorithme d'Euclide et les pouvoirs de deux.

- Oui. Les mauvaises idées communes

Qu'est-ce que regarder?
Il n'y a pas de différence entre les deux.
Autres Si l'une des coordonnées est égale, divisez-la par 2 et continuez. Passer l'étape du GCD peut conduire à de mauvaises réponses lorsque les deux nombres sont étranges. Toujours calculer le GCD d'abord; il représente automatiquement toutes les puissances de deux dans les deux coordonnées. Autres
L'utilisation (x-y) (x+y) lors de l'inversion 2*x x/2. Autres
Autres Une puissance de deux moyens *tous* facteurs premiers sont 2, mais le nombre peut être étrange (c.-à-d., 1). Utiliser `bitCount` ou `x & (x-1)` Astuce à vérifier *un seul bit est réglé*, pas seulement - Autres

Pourquoi le pouvoir de 2 ?

Chaque fois que vous doublez une coordonnée, le GCD est multiplié par 2. À partir de \((1,1)\) où \(\gcd=1\), la seule façon d'obtenir un GCD cible autre que 1 est d'appliquer à plusieurs reprises les opérations *doubling*. Par conséquent, la DCM finale doit être \(2^k\). Si un facteur primaire étrange apparaît, vous ne pourrez jamais le produire à partir de \((1,1)\).

---

- Oui. 3. Discussion de préparation à l'entrevue

3.1 Pourquoi ce problème est l'entrevue Gold

* **Perspective mathématique** – Démontre comment traduire un problème en théorie des nombres (GCD, algorithme euclidien).
* **L'élégance algorithmique** – Un liner dans n'importe quel langage, mais le raisonnement n'est pas trivial.
* **Maîtrise du boîtier** – Poignée les extrêmes des contraintes proprement (1 ≤ valeur ≤ 1e9).
* ** Cohérence linguistique** – Affiche que vous pouvez le résoudre en Java, Python, C++ – un plus pour les rôles qui nécessitent plusieurs piles tech.

3.2 Exemple de conversation d'entrevue

> **Interrogateur:** Nous sommes debout à \((1,1)\). Nous pouvons doubler X, double Y, soustraire Y de X, ou soustraire X de Y. Est-il toujours possible d'atteindre un point arbitraire \(a,b)\)? (en milliers de dollars)

> **Candidate:** -Nous devrions examiner comment chaque opération change le GCD. Les soustractions maintiennent le GCD inchangé; le doublement le multiplie par 2. Ainsi, à partir de \((1,1)\), le GCD ne peut être que \(1,2,4,\dots\). Par conséquent, nous pouvons atteindre \(a,b)\) iff \(\gcd(a,b)\) est une puissance de 2. (en milliers de dollars)

> **Interrogateur :** Comment coderiez-vous ça ? (en milliers de dollars)

> **Candidate:** [Poignées au-dessus de la ligne unique ci-dessus.]

> **Interrogateur:** -Qu'en est-il de la complexité temporelle? (en milliers de dollars)

> **Candidate:** L'algorithme d'Euclid s'exécute dans \(O(\log(\min(a,b))\). La puissance de deux essais est un temps constant. Temps total \(O(\log n)\) et espace \(O(1)\).

3.3 Erreurs communes à mettre en évidence

Erreur Comment le repérer
- Oui.
Utiliser `x / 2` quand `x` est impair pendant l'inverse S'arrêtera lorsque les deux coordonnées sont impaires; cochez plutôt GCD.
Autres Vérifier seulement que `g % 2 == 0'=" Mauvaise interprétation de la puissance de deux=" comme "Even=" Utilisez bit‐count ou `g & (g-1) == Pas de problème.
Autres Oublier que les mouvements de soustraction maintiennent le GCD. Vérifier que `gcd(x±y, y) = gcd(x, y)` en utilisant Euclid=s theorem=

---

- Oui. 4. Article de blog (optimisé par le SEO)

```markdown
# Vérifiez si le point est accessible – le bon, le mauvais, et le mauvais
**LeetCode 2543, GCD, Puissance de 2, Algorithmique Pensée, Java, Python, C++* *

> *Préparé pour la préparation d'entrevues d'ingénierie logicielle, les mathématiques algorithmiques et les amateurs de codage-challenge. *

Déclaration de problème

Vous êtes à la coordonnée **(1, 1)** sur une grille entière infinie.
Vous pouvez effectuer l'un des mouvements suivants ** n'importe quel nombre de fois**:

1. `(x, y) → (x, y – x)`
2. `(x, y) → (x – y, y)`
3. `(x, y) → (2·x, y)`
4. `(x, y) → (x, 2·y) "

Compte tenu des entiers `cibleX` et `cibleY` (1 ≤ cibleX, cibleY ≤ 109), pouvez-vous atteindre `(cibleX, cibleY)`?

> **Objectif:** Produit "Vrai" s'il est accessible, sinon "Faux".

La bonne solution – une seule ligne

Si vous pensez qu'il s'agit d'un problème graphe, vous manquez le **math caché derrière les mouvements**.
Une solution propre et unique est :

'`python
retourner math.gcd(cibleX, cibleY) et (math.gcd(cibleX, cibleY) - 1) == 0
«» "

En Java, Python et C++, cela fonctionne dans l'espace *O(log min(x, y)* et *O(1)*.
La magie réside dans la façon dont chaque opération affecte le plus grand diviseur commun (GCD)**.

Le point de vue mathématique

* Soustraction (`x±y`) ** ne changez pas** le GCD.
* Doubler une coordonnée multiplie le GCD par **2**.

À partir de `(1, 1)` le GCD commence à 1 et ne peut devenir `2, 4, 8, ...`.
Ainsi, le GCD de tout point accessible doit être une **puissance de deux**.

La preuve du GCD Invariance

`gcd(x ± y, y) = gcd(x, y)` est un corollaire de l'algorithme Euclid.
Soustraire `y` de `x` équivaut à une étape de l'algorithme Euclid=S; le GCD ne change jamais.

Puissance de 2 essais

Un nombre `n` est une puissance de 2 sif il a **exactement un set bit**.
Le truc classique :

«» "
(n & (n-1)) == 0 → vrai si n est 1, 2, 4, 8, ...
«» "

ou en C++/Java/Python moderne:

«» "
bitCount(n) == 1
«» "

Les mauvais – Pourquoi le BFS naïf se trompe

* ** explosion d'état** – Chaque double mouvement peut vous pousser deux fois plus loin.
* ** Limite mémoire** – Même avec un `HashSet`, stocker toutes les paires accessibles jusqu'à 1e9 est impossible.
* **Time‐out** – Un BFS non optimisé atteindrait facilement la limite de 1 s sur LeetCode.

> *Leçon pour les intervieweurs:* Demandez toujours *=Quel invariant pouvons-nous suivre?==* et vous arriverez rapidement au GCD.

Les pièges communs

Erreurs Pourquoi il casse Comment corriger
- C'est quoi ?
Autres Diviser un nombre impair par 2 lors d'une recherche inversée
Contrôle "g % 2" 0 ' , interprète la puissance de 2 , en utilisant `bitCount` ou `n & (n-1) == Pas de problème.
Ignorer que la soustraction préserve GCD.

Conseils d'entrevue

1. ** Expliquez d'abord l'intuition du GCD. **
2. **Afficher la puissance de deux états** en utilisant des tours de bits.
3. **Discuse la complexité du temps**: L'algorithme EuclidS fonctionne dans le temps *logarithmique*.
4. **Cas de bord de Mention**: `targetX` ou `targetY` égale 1; les deux coordonnées impair mais GCD 1 → joignable.

Pourquoi ça compte dans l'embauche

* **Démontre la profondeur** – La théorie des nombres montre que vous pouvez penser au-delà de la force brute.
* **Language-agnostic** – Solvable en Java, Python et C++.
* **Efficace** – LeetCode répond à des limites strictes de temps et de mémoire.
* **Savoir-faire** – Un candidat qui explique cette élégamment gagne des points de brownie supplémentaires.

Autres pratiques

- LeetCode: [Nombre de façons de réorganiser une chaîne] (https://leetcode.com/problèmes/nombre de voies-à-réorganiser-a-string/)
- HackerRank: [GCC LCM Challenge] (https://www.hackerrank.com/challenges/gcdlcm)
- Codeforces: [Soustractions et multiplications] (https://codeforces.com/problemset/problem/1472/C)

«» "

Pourquoi ça compte dans un processus d'embauche

* ** Capacité quantitative** – Rôles qui impliquent des structures de données, une cryptographie ou un code critique de performance pour les candidats qui peuvent identifier des invariants.
* **Code propre** – Le monoligneur démontre la maîtrise des fonctions intégrées comme `math.gcd`, `std::gcd`, ou Javas `BigInteger`.
* **Gestion du temps** – Vous passez des minutes à prouver le code du théorème et des secondes, ce qui montre l'efficacité sous pression d'entrevue.

> **Conseil pro :** Joignez l'article à une session de codage en direct sur un site Web de portfolio. Afficher le test d'exécution contre les valeurs aléatoires 1e9 pour convaincre les recruteurs de votre confiance.

---

- Oui. 5. Lecture supplémentaire

1. La théorie du nombre pour les programmeurs** – Une série d'articles expliquant GCD, LCM et arithmétique modulaire dans un contexte de programmation.
2. **=Euclid==Algorithme dans O(log n)==** – Algorithme classique avec pseudocode.
3. **LeetCode discut** – Rechercher dans 2543 GCD pour voir les discussions communautaires sur les variations.

---

> ** Fin de l'article. **
«» "

---

- Oui. 5. Résumé

* ** Trois langues, le même algorithme** – la vérification GCD d'un liner.
* **Éviter les BFS naïfs** – l'espace d'état est infini ; le calcul vous donne une solution à temps constant.
* **Réussite d'entrevue** – montre le raisonnement mathématique, l'élégance algorithmique et la compétence croisée.
* **L'impact d'une crise** – Démontre la capacité d'un candidat à transformer un problème de force brute en une solution propre et théorique – exactement ce que veulent les recruteurs technologiques.

---

Mot final

- *Si vous construisez un site Web personnel ou un blog, copiez le Markdown ci-dessus. *
- *Sentez libre de modifier la description du problème pour correspondre au style de votre portfolio. *
- *Rappelez-vous d'inclure les trois extraits de code et le dialogue d'entrevue; recruteurs aiment voir à la fois le code et le processus de pensée. *

Bon codage, et bonne chance sur votre interview prep!
«» "

---

N'hésitez pas à ajuster les en-têtes, à ajouter des images (p. ex., un diagramme des déplacements de la grille) ou à intégrer les extraits de solution dans les blocs de code. L'objectif est de faire preuve de compréhension, tout en gardant l'explication concise et conviviale.
«» "

---

Avec l'article et les trois solutions, vous êtes entièrement équipé pour présenter **LeetCode 2543** comme un témoignage de vos compétences algorithmiques et mathématiques. Bon codage et bonne chance pour votre prochaine interview!