---
Titre: LeetCode 1526. Nombre minimum d'augmentations sur les sous-barrages pour former un tableau cible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1526 – Nombre minimum d'augmentations sur les sous-réseaux pour former un tableau cible
> **Les bons, les mauvais et les méchants *
> *Un guide pour maîtriser un problème d'interview classique (Java, Python & C++)*

---

Aperçu du problème

On vous donne un tableau **cible** de longueur *n* (1 ≤ n ≤ 105).
Au départ, vous avez un tableau **initial** de la même longueur, mais chaque élément est **0**.

Une opération : choisir tout sous-réseau contigu et incrémenter chaque élément à l'intérieur par **1**.
Objectif : transformer **initial** en **cible** en utilisant les opérations possibles*.

> **Pourquoi ça compte** – Ce problème est un favori sur les interviews techniques (Google, Amazon, etc.) parce qu'il vous oblige à penser en termes de *préfixes* et de *choisissables* tout en gardant l'exécution linéaire.

---

C'est vrai. Aperçu clé (La pépite d'or)

Si vous regardez le tableau un élément à la fois, la seule chose qui compte pour le
*extra* opérations nécessaires est la différence ** entre la valeur courante et la valeur précédente**.

- **Augmentation**: lorsque `cible[i] > cible[i‐1]`
→ nous devons effectuer `cible[i] - cible[i‐1]` les nouvelles opérations qui affectent *seulement* l'élément i-th après les précédentes cessent d'augmenter.
- **Pas d'augmentation**: lorsque la cible [i] ≤ la cible [i‐1] "
→ rien de nouveau n'est nécessaire; les incréments antérieurs couvrent déjà l'élément i‐th.

Le premier élément est un cas particulier: nous devons commencer à partir de 0, donc nous avons besoin d'opérations `cible[0]`.

**C'est pourquoi**
«» "
réponse = cible[0] + ↓ max(0, cible[i] - cible[i‐1]) (i = 1 ... n‐1)
«» "

Cette règle simple d'ajouter les différences positives est un algorithme *greedy* qui fonctionne dans l'espace **O(n)** et **O(1)**.

---

- Oui. Pourquoi une approche de l'avidité fonctionne

1. **Localité de l'influence** – Toute opération couvrant l'indice *i* couvre également tous les indices **.
Donc le seul travail supplémentaire qui compte pour l'index *i* est combien il dépasse l'index précédent.
2. **Pas de bénéfice de la désaffectation** – La diminution d'un élément ne serait jamais utile parce que toutes les opérations sont **incrément-only**.
3. **Monotone Stack Redundancy** – Une solution basée sur la pile (utilisée dans de nombreux messages de rédaction) est inutile; chaque élément est poussé/pouplé au plus une fois, donc la cupidité linéaire est déjà optimale.

---

Faits saillants de la mise en oeuvre

Vous trouverez ci-dessous des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.
Tous suivent le même modèle d'avidité O(n) décrit ci-dessus.

Code de la langue
C'est quoi, ça ?
NombreOpérations(int[] cible) {<br> int ops = cible[0];<br> pour (int i = 1; i < cible.longueur; i++) {<br> si (cible[i] > cible[i-1]) {<br> ops += cible[i] - cible[i-1];<br> }<br> }<br> retour des opérations;<br>}<br>` Autres
**Python**="python<br>class Solution:<br> def minNumberOperations(self, cible: List[int]) -> int:<br> ops = cible[0]<br> pour i dans l'intervalle(1, len(cible)):<br> si cible[i] > cible[i-1]:<br> ops += cible[i] - cible[i-1]<br> retour ops<br>`` Autres
**C++**="cpp<br>#include <vector><br>using namespace std;<br>int minNumberOperations(vector<int>& cible) {<br> int ops = cible[0];<br> pour (size_t i = 1; i < cible.size(); ++i) {<br> si (cible[i] > cible[i-1])<br> ops += cible[i] - cible[i-1];<br> }<br> retour des opérations;<br>}<br>`` Autres

> **Astuce** – Le code est intentionnellement minimal; vous pouvez ajouter des tests de logage ou d'unité autour pour la production ou la pratique d'entrevue.

---

Analyse de complexité

Aspect Complexité
C'est pas vrai.
Temps **O(n)** – un passage sur le tableau
Espace **O(1)** – seulement quelques variables entières

Parce que *n* peut être jusqu'à 105, la solution linéaire est la seule qui correspond confortablement aux limites de temps sur le LeetCode et les plates-formes d'entretien typiques.

---

C'est vrai. Edge Cases & Gotchas

Scénario Pourquoi il est difficile Comment le gérer
-- -- -- -- -- -- -- --
**Tous les éléments sont égaux**= Vous pouvez penser que vous avez besoin d'opérations `n`, mais vous avez seulement besoin du premier élément. La somme gourmande des différences ajoutera `0` pour chaque paire, de sorte que vous obtenez `cible[0]`. Autres
**L'algorithme ne doit pas être soustrait; seul le premier élément compte. Le garde `si (cible[i] > cible[i-1])` empêche les ajouts négatifs. Autres
**Zeros au milieu**=Certains posts éditoriales ajoutent par erreur des différences absolues, conduisant à de mauvais comptes. * S'en tenir aux différences positives seulement** ; les zéros n'ajouteront jamais d'ops supplémentaires. Autres
**Les plus grands nombres**=Le risque de dépassement dans les langues avec des ints signés 32 bits.=Utilisez 64 bits (`long` en Java/Python="s int est débordé, `long` en C++). Autres

---

- Oui. Le Bon – Pourquoi C'est un problème de Nice

- **Linéaire, O(n)** – Pas de récursion cachée ou de tables DP.
- **Pas de gymnastique de la structure de données** – Juste quelques comparaisons.
- **Intuitive** – Une fois que vous réalisez que les pas ne font qu'augmenter la matière, la réponse est évidente.

---

- Oui. Les mauvaises – pièges communs

- **Penser à chaque élément a besoin de son propre fonctionnement** – mène à des solutions naïves O(n2).
- **Utiliser une pile inutilement** – beaucoup de blogs éditorial montrent des preuves basées sur pile, mais ils ajoutent O(n) espace au-dessus qui est évitable.
- **Mixation vers le haut de la différence de l'équation par rapport à la valeur absolue de l'équation** – certaines solutions prennent incorrectement l'équation « a-b » lorsqu'un ≤ b, qui gonfle le nombre.

---

- Oui. L'horrible – Pourquoi les gens luttent avec celui-ci

1. **Mise en échec de l'opération**
- Vous pouvez incrémenter *any* sub-array, pas seulement le tableau entier.
- Une erreur courante est de penser que vous pouvez --stop--- un incrément au milieu d'un sous-array; mais vous pouvez simplement choisir un sous-array plus court.

2. **Suringénierie**
- Une pile ou une technique à deux points est souvent surqualifiée.
- La logique avide est plus simple et plus durable; les intervieweurs apprécient cela.

3. **Bogues de mise en œuvre**
- Off‐by‐one dans le premier élément.
- Oublier que le premier élément contribue toujours à la réponse, indépendamment de sa comparaison avec un élément précédent (il n'y en a pas).

---

#### 9.

- ** Expliquer l'intuition d'abord** – Nous n'avons besoin d'ajouter que lorsque la valeur actuelle dépasse la valeur précédente. (en milliers de dollars)
- **Afficher la formule** – "réponse = cible[0] + "max(0, cible[i] - cible[i‐1]"
- ** Temps et espace** – mention O(n) temps, O(1) espace.
- **Cas d'Edge** – Qu'en est-il si le tableau commence par 0 ? – toujours couvert par «cible[0]».
- **Optionnel** – présenter la preuve de la pile pour plus de profondeur, mais transition rapide au noyau avide pour gagner du temps.

---

#### 10.

- **Greedy** est la bonne stratégie car chaque exigence d'indice dépend uniquement de l'indice *précédent*.
- Oui. La solution est **O(n)** temps, **O(1)** espace – parfait pour les grands *n* jusqu'à 105.
- Éviter la pile ; il est élégant mais inutile pour ce problème.
- Oui. Dans une entrevue, soulignez d'abord les principaux points de vue, puis donnez le code succinct.

---

Code final (Complète, prête pour copier-coller)

**Java**

"Java
// LeetCode 1526: Nombre minimum d'augmentations sur les sous-barrages pour former un tableau cible
solution de classe {
public int minNumberOperations(int[] cible) {
// Le premier élément exige toujours que de nombreuses opérations
int ops = cible[0];
pour (int i = 1; i < longueur cible; i++) {
// Ajouter seulement lorsque la valeur actuelle est supérieure à la valeur précédente
si (cible[i] > cible[i - 1]) {
Opérations += cible[i] - cible[i - 1];
}
}
les opérations de retour;
}
}
«» "

**Python**

'`python
# LeetCode 1526: Nombre minimum d'augmentations sur les sous-barrages pour former un tableau cible
Solution de classe:
def minNumberOperations(self, cible: List[int]) -> Int:
ops = cible[0] # premier élément
pour i dans la plage (1, len(cible)):
si cible[i] > cible[i - 1]: # seulement en augmentant
Opérations += cible[i] - cible [i - 1]
retour ops
«» "

**C++**

'`cpp
// LeetCode 1526: Nombre minimum d'augmentations sur les sous-barrages pour former un tableau cible
#incluez <vecteur>
utilisant l'espace de noms std;

int minNumberOpérations(vecteur<int> et cible) {
int ops = cible[0]; // premier élément
pour (int i = 1; i < (int)target.size(); ++i) {
si (cible[i] > cible[i - 1]) { // augmentation nécessaire
Opérations += cible[i] - cible[i - 1];
}
}
les opérations de retour;
}
«» "

---

### ♫ SEO & Tags pour votre billet de blog

- '#LeetCode1526 '
-#GreedyAlgorithmes "
- #CodageInterview "
- `#LinearTime "
- #StackProof "
- #PythonJavaCPP "

Utilisez ces balises pour atteindre un public plus large à la recherche de prép d'entrevue ou de modèles algorithmiques.

---

Bonne chance pour régler ce problème, et rappelez-vous: la règle d'or* est de ** compter seulement les hausses positives**!