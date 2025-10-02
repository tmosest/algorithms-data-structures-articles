---
titre: LeetCode 1675. Réduire au minimum les écarts dans le tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1675. ** Minimiser la déviation dans le tableau** – Ensemble de solutions complètes (Java, Python, C++)
Le bon, le mauvais, et le mauvais de LeetCode 1675 – Comment le faire dans votre prochaine interview

---

Récapitulation des problèmes

> **Objectif** – Compte tenu d'un tableau de nombres d'entiers positifs, vous pouvez :
> 1. **Diviser** un nombre pair par "2".
> 2. ** Multiplier** un nombre impair par «2».
> Trouver l'écart possible *minimum* (max – min) après un certain nombre de ces opérations.

**Contrôles* *

- Oui.
-- -- -- -- -- --
≤ 10 %

---

Le bien – Ce que nous faisons

1. **Normalisez tous les nombres pour être uniformes** –
Chaque élément étrange doit d'abord être doublé. Après cette opération, l'élément est uniforme et peut être réduit de moitié n'importe quel nombre de fois.
2. **Utiliser un poids maximal** –
L'élément le plus important dicte l'écart actuel. En réduisant à plusieurs reprises ce plus grand élément, nous *gredily* réduisons l'écart.
3. **Tirer le minimum actuel** –
Chaque fois que nous poussons une nouvelle valeur dans le tas, gardez un minimum de fonctionnement afin que nous puissions calculer `max – min` en O(1).

---

Les pièges communs

Pièges
- Oui.
Autres 1= Oublier de doubler les nombres impairs d'abord=si (num % 2=) 1) nombre *= 2;
Autres 2. Arrêter la boucle trop tôt.
Utiliser un min‐heap et pop le mauvais élément Utiliser un **max‐heap** (ou des valeurs inversées)
Autres Sans mise à jour `minVal` après avoir poussé le nombre de moitiés de `minVal = min(minVal, newVal);` Autres
Utiliser `int` pour le débordement 32 bits Tous les résultats intermédiaires s'inscrivent dans la version 32-bit, mais utilisent la version longue pour la sécurité en Java/Python

---

C'est pas vrai. Les cas de bord et l'optimisation

Qu'est-ce qui arrive ? Pourquoi ça compte ?
-- -- -- -- -- -- -- -- -- -- -- --
"nums" a déjà tous les nombres égaux.
Le plus grand élément est une puissance de deux.
`nums` contient 1s=1 → 2 → 1? Non, 1 est étrange, double à 2; après avoir réduit de moitié à 1 de nouveau, mais nous nous arrêtons quand impair.
Autres Très grandes valeurs (`109`)

> ** Rendement :**
> * Temps*: `O(n log n)` – construire le tas domine.
> * Espace*: `O(n)` – tas de magasins tous les numéros.

---

Mise en œuvre

Voici des solutions propres, prêtes à coller pour **Java, Python et C++**. Chacun suit exactement le même algorithme.

---

Java (PriorityQueue – tas max via comparateur)

"Java
Importation de java.util.*;

solution de classe {
Déviation(int[] nombres) {
// max-heap: élément le plus élevé en haut
Priorité Queue<Integer> maxHeap = nouveau PriorityQueue<>(Collections.reverseOrder());
int minVal = entier.MAX_VALUE;

// 1. Normaliser tous les nombres à pair et pousser dans le tas
pour (int num : nombres) {
si ((num & 1)] 1) { // impair
nombre <<= 1; // multiplier par 2
}
maxHeap.offre(num);
minVal = Math.min(minVal, num);
}

int best = entier.MAX_VALUE;

// 2. Boucle d'avidité: continuer à réduire de moitié le maximum actuel
pendant que (!maxHeap.isEmpty()) {
Int curMax = maxHeap.poll();
best = Math.min(best, curMax - minVal);

si ((curMax & 1)) 1) { // impair -> ne peut pas réduire davantage
pause;
}

Int réduit = curMax >> 1; // diviser par 2
minVal = Math.min (minVal, réduit);
maxHeap.offrer(réduit);
}

le meilleur retour;
}
}
«» "

---

### -Python (heapq – utiliser des valeurs négatives pour le tas max)

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
Déviation(même, nombres: Liste[int]) -> Int:
Normaliser tout pour égaliser
max_heap = []
min_val = flotteur('inf')
pour x en nombres:
Si x % 2 == 1: # étrange
x <<= 1
heapq.heappush(max_heap, -x) # négatif pour max-heap
min_val = min(min_val, x)

meilleure = flotteur('inf')
pendant que max_heap:
cur_max = -heapq.heappop(max_heap)
best = min(meilleur, cur_max - min_val)

si cur_max % 2 == 1: # impair -> Arrêter
pause

réduit = cur_max >> 1
min_val = min(min_val, réduit)
heapq.heappush(max_heap, -réduit)

le meilleur retour
«» "

---

### C++ (std::priority_queue – tas max par défaut)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
minimumDéviation(vecteur<int> et nombres) {
priority_queue<int> pq; // max-heap par défaut
int minVal = INT_MAX;

// 1. Convertir les cotes en pair et pousser
pour (int x : nombres) {
si (x & 1) x <<= 1; // double impair
pq.push(x);
minVal = min(minVal, x);
}

int best = INT_MAX;

// 2. L'avidité a diminué de moitié
pendant que (!pq.vide()) {
l'entrée curMax = pq.top(); pq.pop();
best = min(meilleur, curMax - minVal);

si (curMax & 1) casse; // impair – ne peut pas réduire de moitié

moitié int = curMax >> 1;
minVal = min (minVal, moitié);
pq.push(moitié);
}

le meilleur retour;
}
};
«» "

---

Article de blog – référencement Optimisé

> **Titre**
> * Minimiser la déviation dans l'image – LeetCode 1675.

> **Description détaillée**
> Master LeetCode 1675 (Minimize Deviation in Array) avec des solutions Java, Python et C++ propres. Apprenez l'approche gourmande + tas, pièges à éviter, et interviewez des idées qui peuvent vous atterrir votre prochain travail de codage.

> **Mots clés**
> LeetCode 1675, Minimiser la déviation dans Array, entretien de codage, solution Java, solution Python, solution C++, file d'attente prioritaire, algorithme avide, prép d'entretien d'emploi, question d'entretien d'algorithme

---

Aperçu du problème

* Ce que vous avez demandé:*
Transformer le tableau en doublant les cotes et en réduisant de moitié les paires, de sorte que la dernière **déviation** (max – min) soit aussi petite que possible.
Pourquoi c'est important :
Il teste votre capacité à utiliser des stratégies gourmandes, des tas, et de raisonner sur les propriétés de nombre.

---

C'est vrai. La stratégie qui fonctionne

1. **Normalize à pair** – double nombres impairs.
2. **Conservez la plus grande valeur dans un max-heap** – cela donne une extraction O(log n).
3. **Tracker le minimum** – mettre à jour chaque fois qu'un nombre plus petit entre dans le tas.
4. **Il faut réduire de moitié le maximum actuel** – c'est le seul mouvement qui peut réduire l'écart.

> Pourquoi c'est avide ? **
> Chaque moitié diminue strictement le maximum, et nous n'augmentons jamais le minimum sauf quand nous réduisons de moitié un nombre qui devient plus petit. Le processus s'arrête lorsque le maximum devient étrange, ce qui signifie qu'il ne peut être réduit davantage.

---

C'est vrai. Les erreurs communes

Erreurs de fixation
C'est quoi ?
Autres Pas doubler toutes les cotes d'abord. 1) num *= 2; ''Atteinte manquante → Étape égale. Autres
Autres Utiliser un min-heap pour l'élément *max*. Autres
Autres Briser sur le mauvais état. 0'= La boucle doit s'exécuter jusqu'à ce que l'élément le plus grand soit étrange. Autres
Oublier la mise à jour de `minVal`. Autres

---

C'est pas vrai. Les cas de bord et l'optimisation

Bordure Ce qu'il faut regarder pour
- C'est quoi ?
Lire la suite Lire la suite Aucun doublement nécessaire. Autres
Le plus grand nombre est une puissance de deux. Autres
Contient `1`" `1 → 2 → 1` bouclerait infiniment. Autres
Autres Très grands nombres (`109`)" 30 moitiés au maximum" Facteur log négligeable, algorithme toujours `O(n log n)`.

---

####=4== Solutions complètes – prêtes pour copier-pas

(Afficher les extraits de code Java/Python/C++ ci-dessus – un pour chaque langue.)

---

C'est vrai. Conseils d'entrevue

Motif
- Oui.
Autres Expliquez le **odd → même → réduire de moitié** la transformation avant le codage. Autres
Autres Parler de **opérations de pointe** et pourquoi un maximum-pap est nécessaire. Autres
Discutez **début de l'arrêt** (lorsque le max est impair) Autres
Mentionnez la complexité **temps/espace** en amont. Autres
Autres Montrez un petit cas de test à la main. Autres

---

#### 6.

- Oui. L'algorithme est un problème de manuel **greedy + heap** – parfait pour les questions de codage.
- La maîtrise montre que vous pouvez *transformer* les propriétés des nombres en actions de structure de données, une compétence clé pour les rôles moteur, systèmes et algorithmes.
- Le code ci-dessus (Java, Python, C++) est concis, bien commenté et passe tous les tests LeetCode.

> **Vous voulez impressionner les gestionnaires d'embauche? * *
> Inclure ce problème (et ses variations) dans votre repo GitHub, écrire un billet de blog rapide (comme celui ci-dessus) et le référencer dans votre CV. Les recruteurs aiment des solutions propres et autonomes qui démontrent une compréhension profonde des fondamentaux.

---

** Pensée finale** – Les vrais intervieweurs ne sont pas seulement à la recherche de la réponse *correcte*, ils sont à la recherche **comment vous raison**. Montrez-leur que vous pouvez :

- Identifiez un invariant gourmand.
- Choisissez la bonne structure de données (max-heap).
- Gérez tous les cas de bord sans surcomplication.

Bonne chance, et que votre prochaine entrevue soit un *écart minimum* loin du succès! C'est ce qu'il a dit.

---