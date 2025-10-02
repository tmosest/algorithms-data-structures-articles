---
titre: LeetCode 871. Nombre minimum de arrêts de ravitaillement -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 871 – Nombre minimal d'arrêts de ravitaillement
**Hard** – `public int minRefuelStops(int cible, int startFuel, int[] stations) "

> Une voiture voyage d'une position de départ à une destination qui est *cible* miles à l'est de la position de départ.
> Les stations-service sont indiquées en tant que « stations[i] = [positioni, carburanti] ».
> La voiture commence avec "startFuel" litres de gaz et consomme **1 litre par mille**.
> Quand il atteint une station, il peut prendre ** tout** le carburant de cette station.
> Retourner le nombre minimal d'arrêts de ravitaillement nécessaires pour atteindre la destination, ou `‐1` si cela est impossible.

---

## Pourquoi ce problème est une bonne question

C'est bien, c'est mal.
C'est pas vrai.
**Profondeur conceptuelle** – Il teste la pensée cupide et prioritaire, un modèle d'entrevue classique. Certaines solutions DP naïfs débordent ou s'arrêtent dans le temps. Autres
**Scalable** – "stations.longueur ≤ 500", mais l'algorithme est O(n log n) et fonctionne en millisecondes. **Mémoire Mauvaise gestion** – L'utilisation d'un tableau pour une file de priorité en C++ peut s'écraser sur de grandes entrées. Autres
**Analogie du monde réel** – Optimiser les arrêts de ravitaillement est comme la logistique/planification. **Non déterministe** – Si vous oubliez de trier les stations ou d'utiliser un minimum, la réponse peut varier par course. Autres

---

C'est pas vrai. Force vs Optimal

1. **Brute-Force DP**
*État*: `dp[i] = distance maximale atteinte après le ravitaillement en carburant exactement i fois. *
*Complexité*: "O(n2)" – trop lent pour 500 stations.

2. **Greedy + Max-Heap** (optionnel)
*Idée*:
* Gardez un maximum de carburant des stations que nous avons passées* mais qui n'ont pas encore utilisé.
* En conduisant, nous poussons le carburant de chaque station accessible dans le tas.
* Quand nous manquons de carburant avant d'atteindre la prochaine station ou la cible, nous sortons le plus gros carburant du tas – qui est le meilleur carburant à ce moment.
* Répétez jusqu'à ce que nous puissions atteindre la cible ou le tas est vide.

*Complexité*: `O(n log n)` – pousse/pops pour chaque station au plus une fois.

---

## Mise en œuvre de la référence – Java

"Java
Importation de java.util.*;

solution de classe publique {
***
* Nombre minimum d'arrêts de ravitaillement.
*
* @param destination cible
* @param début Carburant initial
* @param stations tableau de [position, carburant]
* @retour stops minimum ou -1 si impossible
*/
public int minRefuelStops(int cible, int startFuel, int[] stations) {
// Max-heap pour stocker les quantités de carburant des stations que nous avons passées.
Priorité Queue<Integer> maxHeap = nouveau PriorityQueue<>(Collections.reverseOrder());
stops int = 0; // nombre de ravitaillements effectués
Int courant Carburant = startFuel; // carburant dont nous disposons actuellement
int idx = 0; // index dans le tableau des stations

pendant que (courantFuel < cible) {
// Poussez toutes les stations que nous pouvons atteindre avec du carburant courant dans le tas
pendant que (idx < stations.longueur && stations[idx][0] <= courantFuel) {
maxHeap.offre(stations[idx][1]); // carburant à cette station
idx++;
}

// Si nous ne pouvons pas aller plus loin et le tas est vide → impossible
si (maxHeap.isEmpty()) {
retour -1;
}

// Carburant avec la meilleure station vue jusqu'à présent
courantFuel += maxHeap.poll();
stops++;
}
les arrêts de retour;
}
}
«» "

**Pourquoi ça marche* *
*La boucle se termine lorsque `currentFuel >= cible`. Chaque fois que nous n'atteignons pas la cible, nous faisons sauter le plus grand carburant non utilisé, garantissant le nombre minimal d'arrêts. *

---

## Mise en œuvre de la référence – Python

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def minRefuelStops(self, cible: int, startFuel: int, stations: List[List[int]]) -> Int:
"""
Solution Greedy + Max-Heap (O(n log n)).
"""
# Le heapq de Python est un heap min, donc nous stockons des carburants négatifs.
max_heap = []
stops = 0
carburant = démarrage Carburant
idx = 0

pendant que le carburant est < cible:
Poussez toutes les stations que nous pouvons atteindre.
pendant que idx < len(stations) et stations[idx][0] <= carburant:
heapq.heappush(max_heap, -stations[idx][1]) # négatif pour max-heap
idx += 1

# Aucune station de ravitaillement à partir de → impossible.
si ce n'est pas max_heap:
retour -1

Le plein à la station avec le plus de carburant.
fuel -= ligne du mannequin de carburant #; garder la lisibilité
carburant += -heapq.heappop(max_heap)
arrêts += 1

Arrêts de retour
«» "

> **Note**: La ligne `carburant -= carburant` est seulement là pour souligner que nous ajoutons du carburant à la quantité actuelle. Dans la pratique, vous feriez simplement `carburant += -heapq.heappop(max_heap)`.

---

## Mise en œuvre de la référence – C++

'`cpp
#incluez <vecteur>
#incluez <queue>
#incluez <algorithme>

solution de classe {
public:
int minRefuelStops(int cible, int startFuel, std::vector<std::vector<int>& stations) {
// Max-heap pour garder les quantités de carburant des stations que nous avons passées.
std::priority_queue<int> maxHeap;
stops int = 0;
long carburant long = startFuel; // utiliser longtemps pour éviter le débordement
taille_t idx = 0;

pendant la période (carburant < cible) {
// Ajouter toutes les stations accessibles au tas.
pendant que (idx < stations.size() && stations[idx][0] <= carburant) {
maxHeap.push(stations[idx][1]);
++idx;
}

// Si on ne peut atteindre aucune nouvelle station ou la cible.
si (maxHeap.vide()) retourne -1;

// Faites le plein avec la station qui nous donne le plus de carburant.
carburant += maxHeap.top();
le point d'entrée est remplacé par le texte suivant:
+ arrêts;
}
les arrêts de retour;
}
};
«» "

---

- Oui. Comment fonctionne l'algorithme – Étape par étape

Étape Mesure Raison
C'est pas vrai.
Alors que nous n'avons pas atteint la destination. Autres
Autres 2= Poussez toutes les stations avec `position ≤ courantFuel` dans max-heap Ces stations sont accessibles *maintenant*. Autres
Si le tas est vide → retourner `‐1`. Autres
Autres 4. Pop le plus gros carburant du tas et ajouter à `currentFuel`. Greedy: le plus grand carburant donne le plus grand saut avec un arrêt. Autres
Autres 5. Incrément `stops`. Autres
Autres Continuer jusqu'à ce que nous puissions atteindre la cible. Autres

---

## Pièges communs et comment les éviter

Erreur
- Oui.
Utiliser un **min‐heap** au lieu d'un max‐heap. Utiliser un max‐heap (ou stocker des valeurs négatives dans un min‐heap). Autres
Autres Oublier de trier les stations Le problème garantit des positions triées, mais si vous triez, vous devez préserver l'ordre. Autres
Utiliser **int** pour le carburant/cible qui peut être jusqu'à `109` et ajouter de nombreux carburants. Autres
Ne pas gérer le cas `stations = []`.La boucle s'éteint immédiatement si `startFuel ≥ cible`. Autres
Retourner `0` pour les cas impossibles. Autres

---

## Tester votre solution

'`python
Exemple 1
print(Solution().minRefuelStops(1, 1, [])) # -> 0

Exemple 2
print(Solution(.minRefuelStops(100, 1, [[10, 100]])) - 1

Exemple 3
print(Solution().minRefuelStops(100, 10, [[10,60],[20,30],[30,30],[60,40]]) - Oui. 2
«» "

---

## SEO – Blog optimisé Article: Le bon, le mauvais, et le mauvais problème de LeetCode 871

Titre
> * * * * * * * * * * * * * * * * * * * * * * * *

Description de la méta
> Master LeetCode 871 avec notre guide détaillé. Comprendre les stratégies gourmandes, résoudre le problème en Java, Python, C++, et apprendre comment ace interview questions sur la logistique et la programmation dynamique.

En-tête

1. **Introduction** – Pourquoi ce problème est important pour les interviews technologiques.
2. **Récapitulatif du problème** – Énoncé clair + contraintes.
3. **Bien** – La beauté de l'avidité + max-heap; analogie du monde réel.
4. **Bad** – Cas de bord, grand nombre, et erreurs courantes.
5. **Ugly** – Pièges dans les paramètres d'entrevue et comment les éviter.
6. ** Solution optimale Passage à pied** – Explication étape par étape.
7. **Samples de code** – Java, Python, C++ (comme ci-dessus).
8. **Testing & Edge Cases** – Vérifications rapides de la santé mentale.
9. **Engagements pour des entrevues d'emploi** – Ce que les intervieweurs veulent voir.
10. **Conclusion et ressources** – Lectures complémentaires, liens pratiques.

- Oui. Extrait de blog

> **Les bonnes**
> Dans LeetCode 871, vous n'êtes pas seulement codant ; vous construisez une stratégie *smart*. L'approche gourmande avec un talon max montre qu'avec une structure de données simple, vous pouvez prendre des décisions *optimales* en temps linéarithmique. Il démontre une compréhension approfondie des files d'attente prioritaires*, un élément essentiel des entrevues techniques.

> **Les mauvais**
> Les contraintes trompent le codeur moyen. `cible` et `fueli` peuvent atteindre un milliard, donc un débordement naïf `int` ou un DP O(n2) va s'écraser. De plus, le problème de phrasé – un réservoir infini – mais un litre par mille – amène souvent à la confusion quant à l'importance de la capacité.

> **Les impies**
> Les essais cachés peuvent comprendre des stations avec zéro carburant restant ou une cible pouvant être atteinte avec *exactement* zéro carburant restant. Beaucoup de solutions échouent parce qu'elles oublient qu'une arrivée de 0-carburant compte toujours comme succès. La partie "gugly" est que le bug est minuscule mais fatal.

> **Solution**
> Voici une implémentation cupide succincte en Java... (insérer le code). Il fonctionne dans `O(n log n)` et s'occupe de tous les cas bord, y compris l'arrivée de carburant zéro difficile.

> **Conseil d'entrevue**
> Lors de l'explication de votre solution, commencez par « I »ll garder un maximum de carburant des stations que nous avons passées. Cela indique à l'intervieweur que vous pensez *optimalement* utiliser les ressources. Puis marchez à travers comment vous rechargez quand vous êtes sur le point de s'épuiser.

Clôture

> Mastering LeetCode 871 vous rapporte non seulement un score parfait, mais démontre également votre capacité d'appliquer des algorithmes gourmands, de gérer de grands nombres et de gérer des cas de bord – exactement les recruteurs set de compétences recherchent chez les ingénieurs logiciels.

---

Mot final

- **Complexité temporelle**: "O(n log n) "
- **Complexité spatiale**: "O(n)" (taille du lourd limitée par le nombre de stations)
- **Pourquoi ça paie**: Ce problème teste le raisonnement cupide + prioritaire, un modèle d'entrevue classique. Résoudre cela montre élégamment que l'on peut penser à la grande image et gérer efficacement les ressources, qualités très appréciées par les employeurs.

Bon codage – et bonne chance d'atterrir ce travail de rêve!