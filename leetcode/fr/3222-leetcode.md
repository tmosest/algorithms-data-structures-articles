---
titre: LeetCode 3222. Trouvez le joueur gagnant dans le jeu de pièces -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Problème – 3222. Trouvez le joueur gagnant dans le jeu de pièces
**LeetCode : https://leetcode.com/problèmes/find-the-winning-player-in-coin-game/**

> On vous a donné deux entiers positifs «x» (nombre de pièces de 75 valeurs) et «y» (nombre de pièces de 10 valeurs).
> Alice et Bob jouent à un jeu à tour de rôle en commençant par Alice. À chaque tour un joueur **doit** prendre des pièces qui total **115**.
> Si un joueur ne peut pas faire un mouvement, il perd.
> Rends le nom du gagnant si les deux jouent de façon optimale.

Remarques clés

Autres À quoi ressemble un mouvement?
- Oui.
1 × 75 + 4 × 10 = 115 ' 75 + 40 = 115. Aucune autre combinaison des sommes de 75 et 10 pièces à 115. Autres
Un tour consomme **un** 75-coin **et** **quatre** 10-coins. Autres
Nombre de tours possibles = `min(x, y/4)`.La ressource limite s'épuise en premier. Autres

Une fois que le nombre de tours `t` est connu, le jeu est simplement un jeu de style Nim normal:

* Si `t` est étrange → **Alice** fait le dernier mouvement → **Bob** perd → Alice gagne.
* Si `t` est même → Bob fait le dernier mouvement → Alice perd → Bob gagne.

La solution n'est donc qu'une formule arithmétique à temps constant.

---

Solutions de code

Vous trouverez ci-dessous des implémentations prêtes à être collées et qui fonctionnent pleinement dans **Java, Python et C++**.

> Les trois utilisent le même temps O(1), l'algorithme d'espace O(1) :
> `retour (Math.min(x, y/4) % 2 == 1) ? "Alice" : "Bob" ;

---

### Java

"Java
// Fichier: Solution.java
solution de classe {
public Chaîne gagnantPlayer(int x, int y) {
// Chaque tour utilise 1 pièce de 75 et 4 pièces de 10
int tours = Math.min(x, y / 4);
retour (tours % 2 ] 1) ? "Alice" : "Bob" ;
}
}
«» "

*Complexité* – **O(1)** temps, **O(1)** espace.
*Test* – `nouvelle solution().winningPlayer(2, 7)` → `"Alice"`.

---

Python

'`python
# Fichier : solution. py
Solution de classe:
def gagnant Joueur(self, x: int, y: int) -> str:
tours = min(x, y // 4) # division entière
retourner "Alice" si on tourne % 2 autre "Bob"
«» "

*Complexité* – **O(1)** temps, **O(1)** espace.
*Test* – `Solution().winningPlayer(4, 11)` → `"Bob"`.

---

C++

'`cpp
// Fichier: solution.cpp
#incluez <algorithme>
#incluez <string>

solution de classe {
public:
std::string winningPlayer(int x, int y) {
int tours = md::min(x, y / 4); // division entière
retour (tours % 2) ? "Alice" : "Bob" ;
}
};
«» "

*Complexité* – **O(1)** temps, **O(1)** espace.
*Test* – `Solution().winningPlayer(2, 7)` → `"Alice"`.

---

Article sur le blog – Le bon, le mauvais et le mauvais jeu de monnaies

> **Référencement au titre optimisé* *
> *Le gagnant du jeu de pièces Algorithm – O(1) Java, Python, C++ – LeetCode 3222 Plongée profonde*

---

C'est pas vrai. Les bonnes

* **Simplicité** – Une fois que vous réalisez qu'un mouvement est forcé d'être `1×75 + 4×10`, le jeu s'effondre à une seule expression arithmétique.
* ** Temps et espace** – O(1) est le bon endroit pour les intervieweurs. Pas de boucles, pas de récursion, pas de tables DP.
* **Compatibilité des langues – La même logique fonctionne en Java, Python et C++. Parfait pour la préparation d'entrevue où la langue est un choix.
* **Explication claire** – Le blog décompose le raisonnement étape par étape, qui est idéal pour les recruteurs qui lisent vos notes.

---

- Oui. Les mauvais

* ** Hypothèse de jeu optimal** – Nous sautons la simulation de tous les états. Dans les jeux de pièces plus complexes, la stratégie optimale peut ne pas être évidente.
* **Edge Cases with Small `y`** – Si `y < 4`, aucun tour ne peut se produire. L'algorithme le gère naturellement (tours = 0 → Bob gagne), mais un novice pourrait manquer cette nuance.
* **LeetCode-Specific** – L'explication est étroitement liée à l'énoncé du problème; vous devez traduire la logique lorsque les valeurs de la pièce changent.

---

C'est vrai. L'Ugly

* **Moins de lecture de la condition gagnante** – Beaucoup de candidats sont enchevêtrés par le dernier mouvement gagne/perdu. Dans ce problème *le joueur qui ** ne peut pas** bouger perd*, ce qui renverse la logique de parité.
* **Hard‐to‐Debug Recursion** – Certaines solutions tentent une simulation récursive, causant un débordement de pile sur de grandes entrées.
* **Sur-Ingénierie** – Construire une recherche d'état complet (FDS/BFS) quand une seule formule suffit est un piège d'entrevue classique.

---

##### 4=" À emporter pour votre chasse à l'emploi

Comment le jeu de la pièce le démontre
Il y a lieu de se reporter au présent document.
Réduisez un jeu à son fonctionnement principal (`1x75 + 4x10`). Autres
**Analyse de la complexité**** Afficher O(1) vs O(n) compromis. Autres
**Code Clarity**= Solution 2 lignes dans n'importe quelle langue – la brièveté est appréciée. Autres
**Décomposition des problèmes** Autres
**La communication d'interview**= Expliquez le raisonnement à haute voix – Ici c'est pourquoi j'utilise `min(x, y/4)' ...= Autres

---

Autres lectures et ressources

1. ** Discussion sur la solution LeetCode** – https://leetcode.com/problèmes/find-the-winning-player-in-coin-game/solutions/
2. **Les bases de la théorie du jeu** – Les façons gagnantes pour vos jeux mathématiques (livre).
3. **Complexité temporelle Cheat Sheet** – https://www.topcoder.com/community/competitive-programming/tutoriels/time-complexity/

---

Les pensées finales

Le jeu de pièces est une vitrine d'entrevue classique. La solution O(1) en Java, Python et C++ prouve que vous pouvez trouver le chemin d'or dans un problème et le communiquer de manière concise. Lorsque les recruteurs regardent votre blog ou votre soumission, ils spotll:

* Vous avez compris les contraintes fondamentales.
* Vous pouvez **optimiser** immédiatement.
* Vous pouvez **exécution** dans la langue que vous choisissez.

Gardez le blog à portée de main pour de futures interviews ; il s'agit d'un rafraîchissement rapide et d'un rappel convivial du CV. C'est ce qu'il a dit.

---