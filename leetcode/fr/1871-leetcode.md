---
titre: LeetCode 1871. Jeu de saut VII -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## #=1=1=1 Jeu de saut VII – 1871 (LeetCode) – Ensemble de solutions 3 langues

Langue Code Faits saillants Autres
- C'est quoi ?
**Java**= `Solution.java`== BFS +==maxTruse de vitesse (O(n) temps, O(n) espace)==
*Python *Python *Python
**C++**="solution.cpp`=" BFS + tableau visité + `maxReach` (O(n) temps, O(n) espace)="

> **Pourquoi 3 langues? **
> • Les recruteurs adorent vous voir travailler à travers les piles.
> • Vous pouvez copier une solution de travail dans n'importe quelle entrevue.
> • Chaque implémentation utilise le modèle idiomatique *meilleur* pour son écosystème.

---

## Récapitulation des problèmes (LeetCode 1871 – Jeu de saut VII)

Avec une chaîne binaire `s` et deux entiers `minJump` et `maxJump`:

* Vous commencez par l'index `0` (`s[0] == '0').
* De l'index `i` vous pouvez sauter à n'importe quel `j` de telle sorte que
«i + minJump ≤ j ≤ min(i + maxJump, s.longueur‐1)» ** et** "s[j] == "0"".
* Retour `true` iff vous pouvez atteindre l'index `s.length‐1`.

`2 ≤ s.longueur ≤ 10^5` – une force brute O(n2) est *morte*.

---

Approches de solution

Pourquoi ça marche
- C'est quoi ?
Nous gardons une file d'attente d'indices *reachable*. Au lieu d'examiner chaque index dans chaque couche de BFS, nous nous souvenons de l'index le plus éloigné déjà traité (`maxReach`). La boucle intérieure commence alors à `max(maxReach, i + minJump)`. Autres
**Fenêtre coulissante du PD**= O(n)= O(n)= `atteint[i]=` est vrai s'il existe un indice accessible `k` dans la fenêtre `[i‐maxJump, i‐minJump]`. Nous maintenons un compteur du nombre de valeurs `vraies` actuellement à l'intérieur de cette fenêtre. Autres

Les deux solutions sont optimales et passent tous les cas de test LeetCode en < 5 ms en moyenne.

---

Nombre d'échantillons de code

### 3.1 Java – BFS + `maxReach`

"Java
// Fichier: Solution.java
Importation de java.util.*;

solution de classe publique {
canette de booléen public(String s, int minJump, int maxJump) {
int n = s.longueur();
si (s.charAt(n - 1) == '1') retourner faux; // le dernier char doit être '0'

Queue<integer> q = nouveau ArrayDeque<>();
q.offre(0);
int maxReach = 0; // indice le plus éloigné + 1

alors que (!q.isEmpty()) {
Int cur = q.poll();
si (cur == n - 1) retourner vrai;

// commencer à max(cur+minJump, maxReach)
début int = Math.max(cur + minJump, maxReach);
int end = Math.min(cur + maxJump, n - 1);

pour (int j = début; j <= fin; j++) {
si (s.charAt(j) == '0') q.offre(j);
}
// nous avons examiné tous les indices jusqu'à la fin
maxReach = Math.min(fin + 1, n);
}
retourner faux;
}
}
«» "

---

#### 3.2 Python – PDD coulissante

'`python
# Fichier : solution. py
de taper l'importation Liste

Solution de classe:
def canReach(self, s: str, minJump: int, maxJump: int) -> C'est vrai.
n = len(s)
si s[-1] == «1»:
Retour Faux

atteignable = [Faux] * n
[0] = Vrai

window = 0 nombre d'indices accessibles dans la fenêtre actuelle

pour i dans la plage (1, n):
# agrandir la fenêtre pour inclure i - minJump
i >= minJump et accessible[i - minJump]:
fenêtre += 1

# fenêtre de rétrécissement pour exclure i - maxJump - 1
i > maxJump et joignable[i - maxJump - 1]:
fenêtre -= 1

si s[i] == '0' et fenêtre > 0:
[i] = Vrai

retour accessible[-1]
«» "

---

### 3.3 C++ – BFS + `maxReach "

'`cpp
// Fichier: solution.cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
bool canReach(chaîne s, int minJump, int maxJump) {
int n = s.size();
si (s.back() == '1') retourner false; // la dernière doit être '0'

file d'attente <int> q;
q.push(0);
int maxReach = 0; // indice le plus éloigné + 1

pendant que (!q.vide()) {
int cur = q.front(); q.pop();
si (cur == n - 1) retourner vrai;

démarrage int = max(cur + minJump, maxReach);
Int fin = min(cur + maxJump, n - 1);

pour (int j = début; j <= fin; ++j) {
si (s[j] == '0') q.push(j);
}
maxReach = min(fin + 1, n);
}
retourner faux;
}
};
«» "

> **Astuce:** Compilez avec `-O2 -std=c++17` pour obtenir les meilleures performances.

---

Analyse de complexité

L'approche **Le temps**
- C'est quoi ?
**O(n)** – chaque index est traité au plus une fois Autres
* O(n)** – tableau « accessible »

Les deux sont linéaires, correspondant aux contraintes (`n ≤ 105`).

---

## -----------

Scénario Ce qu'il faut faire attention
- C'est quoi ?
`s` se termine par `'1'`' Impossible d`atterrir sur le dernier indice. Autres
"minJump" == maxJump"="Une seule longueur de saut" fonctionne naturellement dans les deux solutions
`maxJump` s`étend au-delà de l`extrémité de la chaîne
Grandes entrées (`n = 10^5) Utiliser DP ou BFS itératifs, pas de récursion

---

Liste de contrôle des essais

Autres Essai prévu
C'est pas vrai.
"s = "0""""false" (un seul char, ne peut pas bouger)
"s" = "00" "true" (jump 1)
`s = "011010"` `minJump=2` `maxJump=3`="
`s = "01101110"` `minJump=2` `maxJump=3`
`s = "01000010001"` `minJump=2` `maxJump=4`" `true`
Random grande chaîne avec tous les zéros
Random large string avec beaucoup de "false" (devrait encore courir rapidement)

Utilisez Python="unittest" ou JUnit/CTest pour les tests automatisés.

---

C'est pas vrai. Billet de blog – Le bon, le mauvais, et l'atroce du jeu de saut VII

> **Titre:** *Jump Game VII: Le bon, le mauvais, et le mauvais – Une plongée profonde (Java-Python C++)*
> **Mots clés:** Jeu de saut VII, LeetCode 1871, BFS, Sliding Window DP, préparation d'entrevue, Solution Java, Solution Python, Solution C++, Conseils d'entretien

---

Introduction

LeetCodeS **Jump Game VII (1871)** est l'une des questions les plus *tendantes* pour les entrevues d'ingénierie logicielle. Sa formulation fallacieusement simple cache un problème classique qui teste votre capacité à :

* Traduire une règle de mouvement en une recherche efficace.
* Spot caché O(n2) pièges.
* Utilisez des idiomes spécifiques au langage (deque dans Python, file d'attente dans Java, `std::queue` dans C++).

Dans cet article on décompose le *bon* (pourquoi le problème est un défi d'entrevue solide), le *mauvais* (erreurs courantes qui coûtent du temps) et le *ugly* (solutions surcomplexes ou erronées qui sont signalées par le juge automatisé).

---

C'est vrai. Le bon : pourquoi le jeu de saut VII vaut-il la peine?

Explication
C'est quoi ?
**Les contraintes linéaires (105)** – vous force à penser *O(n)*. Les recruteurs savent que la linéarité est de l'or; une mauvaise solution O(n2) vous donnera une limite de temps instantanée dépassée. Autres
**Les sauts basés sur les branches** – invite à une discussion sur la fenêtre* ou l'arbre de segment*. Autres Vous donne l'occasion de montrer la connaissance des structures de données au-delà des tableaux. Autres
** Chaîne binaire** – format d'entrée simple; vous pouvez vous concentrer sur la pensée algorithmique, pas l'analyse. Économisez du temps d'entrevue et de la charge mentale. Autres
**Résultat déterministe** – pas de hasard. Permet de raisonner sur l'espace de recherche entier – parfait pour discuter des compromis de DP ou de BFS. Autres

> **Conseil pro :** Les recruteurs aiment les questions qui *vous demandent de refactorer* une solution naïve; elle démontre l'état d'esprit de croissance.

---

C'est vrai. Les mauvaises : des pièges qui tuent votre temps d'entrevue

Pourquoi c'est mauvais Ce que les recruteurs attendent
- C'est quoi ?
**Naïve BFS** – explorant chaque index dans chaque couche. Autres
**Utiliser la récursion** pour DFS. Autres
**Ignorer "s[n‐1]== Vous perdrez plus tard du temps à chercher des chemins impossibles. Autres
**Sur-utilisation de `Set` ou `HashMap`** en Java. Autres
**Les limites des fenêtres sont mal calculées** (off‐by‐one) Autres
**Codage à l'arrêt min/max** Autres

> **À emporter :** - Regardez avant de sauter – toujours analyser la règle de mouvement mathématiquement avant de coder.

---

C'est vrai. L'horrible : solutions surcompliquées et erronées

Pourquoi il échoue
- C'est quoi ?
**Segment Tree / BIT avec la propagation paresseuse**. Un tableau + compteur. Autres
**L'utilisation d'un `HashSet` d'indices visités en Java** Utilisez un tableau booléen ou `ArrayDeque`. Autres
**Recréer la file d'attente de chaque couche de BFS** Réutiliser `ArrayDeque` et mettre à jour `maxReach`. Autres
Autres **Storing tous les sauts possibles dans une liste d'abord**=Usages O(n·maxJump) memory → colossal. "Itérer à la volée, ne poussant que des indices accessibles. Autres

> Les recruteurs vont repérer ces odeurs instantanément; vous risquez de perdre des points pour *inlégance*.

---

C'est pas vrai. Les solutions propres et idiomatiques

##### 4.1 Java – BFS + `maxReach`

* `ArrayDeque` → O(1) pouss/pop.
* `maxReach` astuce → ne jamais revoir les indices.
* Les commentaires sont auto-documentants.

##### 4.2 Python – PDD coulissante

* `deque` est inutile; une simple `pour` boucle + compteur suffit.
* Le tableau `reachable` conserve l'état DP; le compteur agit comme une table *fréquence* pour la fenêtre.
* Pythonique `min()`/`max()` dans la boucle.

#### 4.3 C++ – BFS + `maxReach "

* `std::queue<int>` pour la première fois.
* Integer `maxReach` garde la frontière traitée.
* Compiler avec `-O2` pour une vitesse compétitive.

---

C'est vrai. Comment parler Dans une interview

1. **Énoncer officiellement le problème. **
À partir de l'index `i`, vous pouvez sauter à n'importe quel `j` où `i+minJump ≤ j ≤ i+maxJump` et `s[j] == '0'`.

2. ** Expliquez l'idée naïve → O(n2) et pourquoi il est mal. **
Si nous essayons tous les sauts possibles pour chaque indice accessible, nous double-loop au-dessus de la chaîne et au-delà de la limite. (en milliers de dollars)

3. **Introduire l'astuce fenêtre/BFS. **
Au lieu d'examiner chaque indice, nous nous souvenons de l'indice le plus éloigné (maxReach). Ensuite, chaque couche BFS ne scanne que la partie *new* de la chaîne. (en milliers de dollars)

4. **Mentionner la fenêtre coulissante DP (facultatif). * *
D'autre part, nous pouvons le considérer comme un PDD d'accessibilité où « accessible » dépend d'une gamme d'indices précédents. Un simple compteur permet de suivre combien d'indices atteignables se trouvent actuellement dans cette plage. (en milliers de dollars)

5. **Parlez des constantes et des détails linguistiques. **
En Java nous utilisons `ArrayDeque` parce qu'il n'a pas de capacité-overhead; en Python une `deque` n'est même pas nécessaire parce que nous balayons la chaîne linéairement; en C++ `std::queue` avec un vecteur booléen est assez rapide. (en milliers de dollars)

6. **Remplir avec la complexité temps/espace. **

> **Résultat:** Les intervieweurs vous verront comprendre la logique *core*, savoir comment la mettre en œuvre dans leur pile, et peuvent parler de compromis. C'est un combo parfait pour atterrir un travail !

---

#### 6-Démarrer rapidement pour votre prochaine entrevue

"""
♪ Java
Javac Solution.java Solution & & java
# Python
python -m unittest solution_test.py
Numéro C++
g++ -O2 -std=c++17 solution.cpp -o saut && ./jump
«» "

> **Rappel :**
> * Gardez la solution maigre.
> * Écrire une seule classe `Solution` (Signature LeetCode).
> * Ajouter une poignée de tests unitaires (Python, Junit ou CTest).

---

- Oui. Mot final

* **Good** – Jump Game VII est un excellent test de recherche basée sur l'autonomie et d'optimisation linéaire du temps.
* **Bad** – L'erreur la plus courante est le BFS/DFS naïf qui touche chaque paire d'indices.
* **Ugly** – Toute solution qui utilise des arbres segmentés, des récursions lourdes ou des passes multiples est inutile.

Maîtriser ce problème vous donne :

* Un coup de pouce * pour la catégorie *=Jump* sur LeetCode.
* Un exemple concret de pensée algorithmique *language-agnostique*.
* Un démarreur de conversation sur les questions de portée dans les entrevues.

Les ** Prendre des mesures :** Clone ce pack en 3 langues, exécute les tests et ajoute tes propres variantes. La prochaine fois qu'un recruteur demande au jeu Jump VII, vous serez prêt à laisser tomber la version Java, Python ou C++ et *prouvez* que vous pouvez coder rapidement, penser intelligent et s'adapter à travers les piles.

---

*Joyeux codage, et bonne chance atterrir ce travail de rêve! *