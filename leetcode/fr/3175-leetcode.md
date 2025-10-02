---
titre: LeetCode 3175. Trouvez le premier joueur pour gagner des jeux K dans une rangée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de la solution

Voici des implémentations propres et prêtes à la production du **LeetCode 3175 – Trouver le premier joueur à gagner des K Games dans un problème de rang** en **Java, Python et C++**.
Les trois solutions partagent le même temps O(n), stratégie spatiale O(1).

---

## 1.1 Java

"Java
***
* LeetCode 3175 – Trouvez le premier joueur à gagner des jeux K dans une rangée
*
* Complexité temporelle : O(n) – on passe par le tableau des compétences
* Complexité spatiale : O(1) – quelques variables entières seulement
*
* @auteur Votre nom
*/
solution de classe {
public int findWinningPlayer(int[] compétences, int k) {
// Leader actuel (index) et vainqueurs consécutifs
direction int = 0;
stries int = 0;

pour (int i = 1; i < compétences, durée; i++) {
// Si le nouveau joueur bat le leader actuel
si (compétences [i] > compétences [leader]) {
// Le nouveau leader commence une nouvelle série
chef = i;
sangle = 1;
} autre {
// Le leader actuel continue de gagner
stries++;
}

// Arrêter tôt quand la stries atteint k
Si (streak) k) pause;
}
chef du retour;
}
}
«» "

---

## 1.2 Python

'`python
Code Leet 3175 – Trouvez le premier joueur à gagner des jeux K dans une rangée
♪ Heure: O(n) (un passage)
♪ Espace: O(1)

Solution de classe:
def findWinning Player(self, compétences: list[int], k: int) -> Int:
leader = 0 # indice du gagnant actuel
stries = 0 # victoires consécutives du vainqueur actuel

pour i dans la plage (1, len(skills)):
si compétences[i] > compétences[leader]:
chef = i
Sangle = 1
Sinon:
Scène += 1

Si la série == k:
pause
chef du retour
«» "

---

C++

'`cpp
// Code Leet 3175 – Trouvez le premier joueur à gagner des jeux K dans une rangée
// Complexité temporelle : O(n) – passe linéaire unique
// Complexité spatiale : O(1) – espace supplémentaire constant

solution de classe {
public:
int findWinningPlayer(vecteur<int>& compétences, int k) {
leader int = 0; // indice gagnant actuel
stries int = 0; // victoires consécutives du vainqueur actuel

pour (int i = 1; i < competences.size(); ++i) {
si (compétences [i] > compétences [leader]) {
chef = i;
sangle = 1;
} autre {
++Streak;
}
Si (streak) k) pause;
}
chef du retour;
}
};
«» "

---

♪ 2. Article du blog

> **Titre:**
> *Cracking LeetCode 3175: -Découvrez le premier joueur à gagner des jeux K en ligne – One-Pass Java/Python/C++ Solutions (bonnes, mauvaises et mauvaises)*

---

2.1 Introduction

Si vous préparez une entrevue de codage, **LeetCode 3175** est un défi classique de niveau moyen qui teste votre compréhension des files d'attente, du raisonnement avide et du passage à un passage. Le problème vous demande d'identifier le premier joueur qui gagne **k matchs consécutifs** dans un tournoi où les joueurs avec une compétence supérieure gagnent toujours.

Dans ce billet, I.V. va passer par:

* L'intuition **** derrière l'algorithme optimal.
* Une mise en œuvre étape par étape** dans **Java, Python et C++**.
* Commun **gotchas** (= mauvais) et comment les éviter.
* Une plongée plus profonde dans ** cas de pointe** et des scénarios de "gugly" qui pourraient trébucher vers des solutions naïves.

Le but est de vous donner une réponse complète et prête à l'entrevue que vous pouvez vous vanter sur votre CV.

---

## 2.2 Récapitulation des problèmes

Texte
Entrée
compétences – int[] (taille n, 2 ≤ n ≤ 10^5, toutes valeurs uniques)
k – int (1 ≤ k ≤ 10^9)

Produit
index du joueur qui gagne d'abord k jeux consécutifs
«» "

> Exemple
> compétences = [4, 2, 6, 3, 9], k = 2 → sortie: 2

La mécanique du tournoi :

1. Deux joueurs avant jouent.
2. Les compétences supérieures restent à l'avant.
3. Loser déménage à l'arrière.
4. Répétez jusqu'à ce que quelqu'un gagne **k** jeux droits.

---

## 2.3 Le bien – Un laissez-passer Regard sur l'avidité

2.3.1 Pourquoi l'avidité fonctionne

À tout moment, le joueur frontal actuel (leader) est le plus fort parmi tous les joueurs qui ont *jamais* affronté l'un l'autre. Si un nouveau joueur arrive (`i`) et a une compétence supérieure, le leader actuel ne peut plus jamais gagner. Par conséquent:

* Le gagnant après `i` devient le nouveau leader.
* La série de victoires consécutives revient à **1** (le nouveau leader vient de gagner contre l'ancien).
* Si le nouveau joueur est plus faible, le leader étend simplement sa séquence.

L'observation cruciale: **Nous n'avons besoin que de suivre le leader actuel et le nombre de matchs qu'il a gagnés de suite.** Pas besoin de simuler toute la file d'attente.

### 2.3.2 Croquis d'algorithme

«» "
leader = 0 // indice du front actuel
stries = 0 // victoires consécutives du leader

pour chaque i de 1 à n-1:
si compétences[i] > compétences[leader]:
chef = i
Sangle = 1
Sinon:
Scène += 1

k: // gagnant trouvé
pause

chef du retour
«» "

L'algorithme se termine dès qu'une série atteint `k`, ce qui est garanti parce que le joueur le plus fort finira par gagner `k` fois quand `k ≤ n-1`. Pour `k > n-1`, le joueur le plus fort gagne encore le tournoi (aucun autre ne peut le battre).

---

## 2.4 Les pièges communs

Pourquoi ça arrive ?
- C'est quoi ?
**L'utilisation d'une véritable file d'attente**= Une simulation naïve pousse et pops des éléments O(n), menant à l'espace O(n) et à un facteur constant plus élevé. Utilisez le compteur gourmand; pas de file d'attente nécessaire. Autres
**En supposant que k ≤ n-1**, les contraintes de problème permettent `k` jusqu'à `10^9`. Une sortie précoce si la stries atteint `k`; sinon, la stries maximale est `n-1`. Autres
**Les erreurs hors-par-un**=Démarrer `streak` à `0` ou `1` compte incorrectement la première victoire. Commence par `0`; incrément après chaque comparaison. Autres
**Débordement entier**= Pas un problème avec des contraintes données, mais toujours attention quand `k` est énorme. Pas d'arithmétique au-delà des comparaisons; sûr. Autres
Autres Pour Java/C++/Python, `int` est suffisant; `long` n'est nécessaire que si `k` > `2^31-1`. Autres

---

## 2.5 Les cas de bord qui peuvent casser des solutions simples

1. **Deux joueurs, énorme `k`**
*compétences = [1, 2], k = 1 000 000 000*
Dans une simulation de quadrillage, la boucle tournera pour toujours parce que le gagnant continue à se diriger vers l'avant chaque tour. L'algorithme avide le résout en un seul passage : le joueur le plus fort (`index 1`) va gagner le premier jeu, stries = 1, et la boucle se termine parce que la stries maximale est `n-1 = 1`.

2. **Le joueur le plus fort à la fin**
*compétences = [1, 2, 3, 4, 5], k = 3*
Le compteur cupide fonctionne toujours parce que chaque fois qu'un nouveau joueur plus fort arrive, la série se réinitialise.

3. **Très grand `k` mais petit `n`**
*compétences = [10, 20], k = 500*
L'algorithme se termine après la première comparaison parce que le joueur le plus fort aura strie `1` et ne peut pas atteindre `k`. Selon le problème, quand `k > n-1`, le joueur avec la compétence maximale gagne. Notre code retourne automatiquement le leader à la fin de la boucle (qui est la plus forte).

4. ** Compétences non uniques (contrairement aux contraintes)* *
Si les compétences n'étaient pas uniques, vous devriez décider de l'égalité. La logique gourmande tient toujours aussi longtemps que vous rompez les liens.

---

2.6 Analyse de la complexité

Langue Heure Espace
- C'est quoi ?
Java O(n)
Python O(n)
O(n)

L'algorithme est linéaire dans le nombre de joueurs et n'utilise qu'une poignée de variables. Il s'arrête aussi dès que la série gagnante est atteinte, ce qui en fait **optimal pour les intervieweurs qui aiment le code concis et efficace. **

---

2.7 Pourquoi cela compte pour votre mémoire

* ** Pensée algorithmique** – Vous allez présenter l'optimisation avide + un seul passage.
* **Compétence multilingue** – Démontrer les implémentations Java, Python et C++ montre une polyvalence.
* **Espace et efficacité du temps** – Les intervieweurs demandent souvent la solution « best » ; O(n) time & O(1) space est un gagnant clair.
* **Balises de problèmes** – Recue, cupide, one-pass, entretien d'emploi, entretien de codage.

Si vous voulez vous démarquer, ajoutez une note dans votre CV ou portfolio :

> LeetCode 3175 – *Trouver le premier joueur pour gagner des jeux K en ligne* en utilisant un algorithme avide à un seul passage (Java/Python/C++). (en milliers de dollars)

---

## 2.8 Prise finale

Le problème LeetCode 3175 est un bon exemple de **=look‐ahead cupidy==**. En reconnaissant que le tournoi n'indique que l'importance est le leader actuel et sa série, vous évitez la simulation lourde et produisez une solution propre et constante.

Gardez la table des pièges à l'esprit lorsque vous vous attaquez à des problèmes similaires à la file d'attente : une file d'attente est souvent un hareng rouge. Si vous pouvez réduire le problème à un simple compteur, vous êtes généralement sur la bonne voie.

Bonne chance avec votre entretien de codage! C'est ce qu'il a dit.

---

2.9 Appel à l'action

Si vous souhaitez voir la solution en action, copiez les extraits de code de la section 1 dans votre éditeur en ligne IDE ou LeetCode et lancez quelques cas de test.

Codage heureux, et n'hésitez pas à **partager** cet article avec votre réseau ou laisser un commentaire si vous souhaitez discuter d'autres problèmes LeetCode !