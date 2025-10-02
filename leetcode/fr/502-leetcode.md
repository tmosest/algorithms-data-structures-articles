---
titre: LeetCode 502.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – LeetCode 502 – *IPO*

Point de détail
- C'est quoi ?
**ID**
Titre
Difficulté
Avec `k` (nombre maximum de projets que vous pouvez terminer), un capital initial `w`, des tableaux `profits[]` et `capital[]` (les deux longueur `n`). Vous pouvez choisir au maximum `k` *distinct* projets. Un projet ne peut être lancé que si vous disposez actuellement au moins de son «capital[i]». Lorsque vous la terminez, vous gagnez des «bénéfices[i]», qui sont ajoutés à votre capital. Autres
**Return the maximum capital you can have aftering at most `k` projects. Autres
**Constances**=1 ≤ k ≤ 105 `<br>=0 ≤ w ≤ 109`<br>=1 ≤ n ≤ 105`<br>=0 ≤ bénéfices[i] ≤ 104`<br>=0 ≤ capital[i] ≤ 109`=

La solution classique utilise une stratégie *greedy* avec deux files d'attente prioritaires (ou un tableau trié + un max-heap).

---

- Oui. 2. Regard sur l'avidité

1. **À chaque étape, nous voulons le projet le plus rentable qui est actuellement abordable. * *
2. **Pourquoi est-ce optimal? * *
* La seule chose qui peut changer l'ensemble de projets qui deviennent abordables est le montant du capital que vous avez.
* Si vous sautez un projet rentable qui est déjà abordable en faveur d'un projet moins rentable, vous *ne récupérerez jamais * le profit perdu, tandis que le capital que vous avez après le prochain tour sera strictement plus petit ou égal.
* Par conséquent, prendre le projet le plus rentable est toujours sûr et ne peut pas nuire aux choix futurs.

Donc l'algorithme devient :

*Trier les projets par les capitaux nécessaires. *
*Alors que nous avons encore des "rounds" (projets "k" à gauche): *
C'est la raison pour laquelle la Commission s'est prononcée en faveur de l'adoption d'une directive relative à l'étiquetage des denrées alimentaires. Ajouter chaque projet dont le "capital" ≤ capital actuel dans un **max-heap** clé par le "bénéfice".
C'est la raison pour laquelle la Commission s'est prononcée en faveur de l'adoption d'une directive relative à l'étiquetage des denrées alimentaires. Pop le plus grand profit du tas et l'ajouter à notre capitale.
C'est la raison pour laquelle la Commission s'est prononcée en faveur de l'adoption d'une directive relative à l'étiquetage des denrées alimentaires. Si le tas est vide, nous ne pouvons pas nous permettre tout autre projet → arrêter.

complexité du temps: `O(n + k) log n)` (triage + opérations de tas).
complexité spatiale: `O(n)` (pour le tas et le tableau trié).

---

- Oui. 3. Mise en œuvre – Java, Python & C++

Voici des implémentations claires et bien commentées dans les trois langues demandées.
Tous suivent la même logique que celle décrite ci-dessus.

---

### 3.1 Java (LeetCode friendly)

"Java
Importation de java.util.*;

***
* LeetCode 502 – IPO
* Solution Greedy + Max-Heap.
*/
solution de classe publique {

*** Représentation des projets – nous avons seulement besoin de capital et de profit */
classe statique privée Mise en œuvre du projet Comparable<Projet> {
capital int;
le bénéfice net;

Projet(int capital, profit int) {
Ça. capital = capital;
Ça. bénéfice = bénéfice;
}

*** Tri par capital requis (croissant) */
@Override
comparaison publique À(Projet autre) {
retour Integer.comparer(ce.capital, autre.capital);
}
}

capital(int k, int w, int[] bénéfices, int[] capital) {
n = bénéfices. longueur;
Projet[] projets = nouveau projet[n];

// Construire des objets de projet
pour (int i = 0; i < n; ++i) {
projets[i] = nouveau projet[i], bénéfices[i];
}

Trier les projets selon les besoins en capital
les tableaux.sort(projets);

// 2-Lheap max pour les bénéfices (Javas PriorityQueue est min-Lheap par défaut)
Priorité Queue<enteger> maxProfitHeap =
nouveau PriorityQueue<>(Collections.reverseOrder());

int idx = 0; // pointeur dans les projets triés
courant intCapital = w;

pour (int round = 0; round < k; ++ round) {
// Poussez tous les projets que nous pouvons nous permettre maintenant
alors que (idx < n && projets[idx]. capital <= courantCapital) {
maxProfitHeap.offre(projets[idx].profit);
idx++;
}

// Si aucun projet abordable, nous sommes coincés
si (maxProfitHeap.isEmpty()) pause;

// Prenez le plus rentable
currentCapital += maxProfitHeap.poll();
}

retour courantCapital;
}
}
«» "

---

### 3.2 Python (Code Leet 3.10.1 – Python 3.10)

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def findCapital Maximisé(
auto, k: int, w: int, profits: Liste[int], capital: Liste[int]
-> Int:
"""
Solution Greedy + max-heap.
"""
# Combiner les deux tableaux en une liste de tuples (capital, bénéfice)
projets = triés(zip(capital, bénéfices)) # tri par capital asc

max_profit_heap: Liste[int] = [] # stockera les bénéfices négatifs (minimum-heap)
idx = 0
n = len(projets)

pour _ dans la plage(k):
# Poussez chaque projet abordable dans le tas
pendant que idx < n et projets[idx][0] <= w:
# Python n'a qu'un peu de gain; stocker le bénéfice négatif pour max-heap
heapq.heappush(max_profit_heap, -projets[idx][1])
idx += 1

si non max_profit_heap:
pause

# Prenez le projet le plus rentable
(max_profit_heap)

retour w
«» "

---

*## 3.3 C++ (Codeet 3.10.1 – C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int find Maximisé Capital(int k, int w,
vectorielle <int>& profits,
vecteur<int>&capital) {
int n = profits.size();
// Paire capital et bénéfice
le vecteur<pair<int,int>>projets(n);
pour (int i = 0; i < n; ++i)
projets[i] = {capital[i], bénéfices[i]};

Classer par le capital requis
tri(projets.begin(), projets.end(),
[](const auto& a, const auto& b) { retourner a.first < b.first; });

// 2-Levure maximale pour les bénéfices (plus grande <> transforme priority_queue en max-heap)
priority_queue<int> maxProfitPQ;

int idx = 0; // index dans les projets triés
pour (int round = 0; round < k; ++ round) {
// Ajouter tous les projets que nous pouvons nous permettre en ce moment
alors que (idx < n && projets[idx]. premier <= w) {
maxProfitPQ.push(projets[idx].seconde);
++idx;
}

Si (maxProfitPQ.vide())
pause; // ne peut se permettre aucun autre projet

w += maxProfitPQ.top(); // prendre le plus rentable
maxProfitPQ.pop();
}

retour w;
}
};
«» "

---

- Oui. 4. Article de blog – *Le Bon, le Mauvais, et l'Ugly of Solving LeetCode 502 (IPO)*

> **Titre:**
> **IPO (LeetCode 502) – De la confusion à la clarté : le bon, le mauvais et le mauvais**

> **Désignation de la méta (=160 caractères):**
> Master LeetCode 502 avec une solution gourmande + prioritaire. Apprenez les écueils, l'approche optimale et comment aser l'entrevue. Boostez votre CV de codage aujourd'hui!

> **Mots clés:** LeetCode 502, problème d'IPO, algorithme gourmand, file d'attente prioritaire, codage d'entretien, interview d'algorithme, optimisation du capital, solutions Java Python C++

---

- Oui. 1. Pourquoi ce problème (le bon)

- **Saveur du monde réel:** Vous jouez essentiellement à un *jeu d'investissement* – pensez au capital-risque, à la sélection des projets et à l'allocation des ressources. Cela résonne avec de nombreux ingénieurs logiciels qui travaillent sur des cartes routières de produits.
- **Profondeur conceptuelle:** Il combine la stratégie **greedy** avec les structures de données **heap**. La maîtrise de ces sujets est un must pour les rôles supérieurs.
- **Échelle:** Les contraintes (`n, k ≤ 105`) vous poussent à penser à *la complexité du temps* et *l'empreinte de mémoire*, exactement ce que les gestionnaires d'embauche tiennent à.
- ** Support linguistique multiple :** Résoudre en Java, Python et C++ démontre la polyvalence – un avantage dans les interviews technologiques.

---

- Oui. 2. Pièges communs (les mauvais)

Pourquoi ça fait mal ?
- C'est quoi ?
**L'approche O(n2)** (largage sur tous les projets à chaque tour) Autres
Vous choisiriez le projet le moins rentable.
*Ignorer la contrainte de capital * Ajouter aveuglément tous les profits conduit à une mauvaise réponse * Filtrer les projets par `capital ≤ courantCapital` avant de pousser au tas *
Vous pourriez prendre plus de projets que permis.
Le tri par profit au lieu du capital mélange la logique d'abordabilité

---

- Oui. 3. La solution Elegant Greedy (L'Ugly... en fait le meilleur!)

> La laideur se réfère ici au fait qu'une fois que vous le voyez, vous ne regarderez jamais le problème à nouveau. *

3.1 Croquis d'algorithme

«» "
trier les projets par capital
heap = heap maximal vide
idx = 0
pour round dans 1 ... k:
alors que idx < n et projets[idx]. capital <= capital:
heap.push(projets[idx].profit)
idx++
si le tas est vide: casser
capital += heap.pop_max()
«» "

##### 3.2 Pourquoi c'est bizarre dans un sens positif

- ** Pas besoin de retour en arrière.** Le choix avide garantit l'optimalité, donc vous n'avez pas à écrire des tables complexes de récursion ou DP.
- ** Séparation claire des préoccupations :**
- *Trier* gère la dimension **faisabilité** (capital).
- *Le lourd* gère la dimension **optimize** (profit).
- **Codage rapide dans n'importe quelle langue.** L'idée principale est langagière-agnostique; vous n'avez qu'à échanger des structures de données (Javas `PriorityQueue`, Python=s `heapq`, C++=s `priority_queue`).

---

- Oui. 4. Passer par un exemple

On prend le cas classique :

«» "
k = 2, w = 0
bénéfices = [1, 2, 3]
capital = [0, 1, 1]
«» "

1. **Création 1**
*Projets abordables:* indices 0,12 (tous capitaux 0/1 ≤ 0).
*Temps après avoir poussé:* `[3, 2, 1]` (Temps maximum).
*Take 3 → capital devient 3. *

2. **Durée 2**
*Tous les projets restants sont déjà dans le tas. *
*Take 2 → capital devient 5. *

**Réponse:** `5`, qui est le meilleur.

Vous pouvez vérifier que chaque capital intermédiaire est le *meilleur* possible compte tenu des contraintes.

---

- Oui. 5. Stratégie d'essai (Le vrai laid)

Autres Cas d'essai: Que vérifier?
- C'est quoi ?
**Tous les projets sont abordables**
Autres **Pas de projet abordable au début**
Vous pouvez terminer *tous* projets si abordable.
**Grands déficits de capital** , les projets ne deviennent abordables qu'après plusieurs tours , vous assurer de pousser les projets ** seulement quand ils sont abordables** Autres
**Randomisé petit n**. Calcul manuel possible.

---

- Oui. 6. Take‐away: Comment utiliser ceci sur votre CV

1. **Afficher le code de solution** (cochez votre langue) et expliquer l'algorithme dans les commentaires.
2. **Ajouter une brève analyse de complexité** à côté du code ou dans un bloc de commentaires.
3. **Mention de l'expérience d'entrevue** – p. ex., le texte du LeetCode 502 en trois langues; expliqué le raisonnement avide en entrevue de codage de 30 minutes. (en milliers de dollars)
4. ** Mettre en évidence le résultat de l'apprentissage :** Il a mis en œuvre un algorithme cupide basé sur la file de priorité, améliorant le temps d'exécution de O(n2) à O(n+k) log n. (en milliers de dollars)

Ces points prouvent que vous êtes non seulement un codeur, mais un architecte *solution* qui comprend les implications de performance – exactement ce que les recruteurs recherchent.

---

- Oui. 5. Conclusion

LeetCode 502 IPO= peut sembler intimidant à première vue, mais avec un principe clair et gourmand et une file d'attente prioritaire, vous pouvez le transformer en une solution concise et optimale.
Les implémentations Java, Python et C++ ci-dessus sont testées et prêtes pour des entretiens de production.

Bon codage, et que votre capital (et votre CV) grandissent!

---

**Partager cet article** sur Linked Dans ou GitHub pour aider d'autres à transformer leur expérience d'entrevue – parce que la meilleure préparation d'entrevue est la connaissance *partagée* qui transforme le "bad" en "good". (en milliers de dollars)