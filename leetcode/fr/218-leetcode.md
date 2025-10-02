---
titre: LeetCode 218. Le problème Skyline -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Le problème Skyline – Java, Python & C++ Solutions + Blog In-Depth

Ci-dessous vous trouverez trois implémentations complètes (Java, Python, C++) pour LeetCode 218 – *Le problème Skyline*.
Après le code, vous trouverez un billet de blog qui explique l'algorithme, les compromis et pourquoi maîtriser ce problème peut vous poser un défi technologique.

---

C'est pas vrai. Java 17 Solution

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<Liste<entier>> getSkyline(int[[]]bâtiments) {
// 1. Construisez une liste de tous les événements (bords gauche et droite)
Liste des événements<int[]> = nouvelle liste d'événements<>();
pour (int i = 0; i < constructions, longueur; i++) {
int[] b = bâtiments[i];
events.add(new int[]{b[0], -b[2]}); // bord gauche: hauteur négative
événements.add(nouveau int[]{b[1], b[2]}); // bord droit: hauteur positive
}
// 2. Tri par x, puis hauteur (négative avant les liens positifs)
events.sort(a, b) -> {
si (a[0] != b[0]) retourne Integer.compare(a[0], b[0]);
retour entier.comparer(a[1], b[1]);
});

Liste <Liste<entier>> résultat = nouvelle liste <>();
// Max-heap pour maintenir les hauteurs actives
Priorité Queue<Integer> maxHeap = nouveau PriorityQueue<>(Collections.reverseOrder());
maxHeap.offre(0); // niveau du sol
la valeur de l'unité de mesure est égale à la valeur de l'unité de mesure.

pour (int[] e : événements) {
int x = e[0], h = e[1];
si (h < 0) { // bord gauche
l'offre maxHeap.(-h);
} autre { // bord droit
// Enlèvement paresseux – le tas peut contenir des hauteurs qui ont déjà fini
pendant que (!maxHeap.isEmpty() && maxHeap.peek() == h) {
le nombre maximal d'unités de mesure est égal à celui des unités de mesure.
pause;
}
}

Int curMax = maxHeap.peek();
si (curMax != prevMax) {
résultat.add(Arrays.asList(x, curMax));
prevMax = curMax;
}
}
le résultat du retour;
}
}
«» "

---

Solution Python 3

'`python
de taper l'importation Liste
importation heapq

Solution de classe:
def getSkyline(self, buildings: List[List[int]]) -> Liste[Liste[int]]:
# événements: (x, hauteur) où la hauteur < 0 pour le bord gauche
événements = []
pour l, r, h dans les bâtiments:
events.append((l, -h)) # début
events.append(r, h)) # fin

# trier par x; pour la même x, commence avant la fin (négatif avant positif)
events.sort(key=lambda x: (x[0], x[1]))

résultat = []
# Levure max de hauteurs actives (stocker comme négatif pour le museau)
max_heap = [0]
prev = 0

pour x, h dans les événements:
si h < 0: # début d'un bâtiment
heapq.heappush(pape maximale, h)
Autre: # fin d'un bâtiment
# Enlevez la hauteur du bâtiment du tas
# Le tas de Python ne supporte pas l'enlèvement, si paresseux pop
pendant que max_heap et max_heap[0] == - Oui.
heapq.heappop(max_heap)
pause

cur = -max_heap[0] # hauteur maximale du courant
Si cur != Prév:
résultat.append([x, cur])
prev = cur
résultat du retour
«» "

---

Solution

'`cpp
#incluez <vecteur>
#incluez <algorithme>
#incluez <queue>
#incluez <utilité>
utilisant l'espace de noms std;

solution de classe {
public:
vector<vector<int>> getSkyline(vector<vector<int>>&bâtiments) {
// 1. Créer des événements: (x, hauteur) – hauteur négative pour le bord gauche
les événements vecteurs<pair<int,int>>;
pour (auto &b : bâtiments) {
events.emplace_back(b[0], -b[2]); // gauche
events.emplace_back(b[1], b[2]); // droite
}
Tri(events.begin(), events.end(), [](auto &a, auto &b){
si (a.first != b.first) retourner a.first < b.first;
retour a.seconde < b.seconde; // gauche avant droite
});

vecteur<vecteur<int>> résultat;
priority_queue<int> maxHeap; // max-heap des hauteurs actives
maxHeap.push(0); // niveau du sol
int prev = 0;

pour (auto & e : événements) {
int x = e.first, h = e.second;
si (h < 0) { // début du bâtiment
le nombre maximal d'heures de travail (-h);
} autre { // fin du bâtiment
// Suppression paresseuse : pop seulement lorsque le haut correspond à la hauteur de fin
pendant que (!maxHeap.vide() && maxHeap.top() == h) {
le point d'entrée est remplacé par le texte suivant:
pause;
}
}
Int cur = maxHeap.top();
si (cur != prev) {
result.push_back({x, cur});
prév = cur;
}
}
le résultat du retour;
}
};
«» "

---

Article du blog : Le problème Skyline – Bon, Mauvais et Ugly

> **Titre:**
> **Le problème de Skyline: bon, mauvais et laide – un guide complet pour les entrevues d'emploi**
>
> **Meta Description:**
> Master LeetCode 218 – Le problème Skyline. Apprenez l'algorithme du balayage, comparez les solutions naïves, prioritaires et segmentées, et comprenez pourquoi ce problème est incontournable pour toute entrevue d'ingénierie logicielle.
>
> **Mots clés:** problème skyline, LeetCode 218, algorithme de ligne de balayage, file d'attente prioritaire, algorithme d'entrevue, entretien d'emploi, structures de données, C++, Java, Python, entretien de codage, conception d'algorithmes

---

C'est pas vrai. Quel est le problème de Skyline ?

Dans l'urbanisme, le *skyline* est le contour que vous voyez en regardant une ville de loin.
Officiellement :

- **Input:** `buildings[i] = [left_i, right_i, height_i]` – chaque bâtiment est un rectangle sur une base plate.
- **Output:** Une liste de *key points* `[[x1, y1], [x2, y2], ...]` qui tracent le contour extérieur.
Le dernier point a toujours `y = 0`.

Le défi est de produire ce contour efficacement pour jusqu'à 104 bâtiments, chacun avec des coordonnées allant jusqu'à 231‐1.

---

C'est vrai. Les trois approches de l'arôme

Complexité du code Complexité d'utilisation typique
-- -- -- -- -- -- -- -- -- -- -- -- -- --
Autres **Bon – Ligne de balayage + réponse à l'entrevue de niveau de production*. Autres
**Bad – Brute Force**. **O(n2)**. Autres
**O(n log N)** (N = taille de compression de la coordonnée) Autres

---

#### 2.1 La solution *Bonne*: Ligne de balayage + Hauteur maximale

1. **Événements**
Pour chaque bâtiment, nous créons deux événements :
- `(gauche, -hauteur)` – début du bâtiment (hauteur négative à différencier).
- `(à droite, +hauteur)` – fin du bâtiment.

2. **Événements graves**
Trier par `x`. Quand `x` liens, commence (négatif) vient avant la fin (positif).

3. **Passer**
Maintenir un maximum de hauteurs de construction *actives*.
*Push* quand un bâtiment commence, *lazy-pop* quand un bâtiment se termine.

4. **Skyline Update**
Après chaque événement, le haut du plateau est la hauteur maximale actuelle.
Si elle diffère de la hauteur précédente, émet un nouveau point clé.

*Pourquoi cela fonctionne: *
Le tas contient toujours les hauteurs des bâtiments qui couvrent la position de balayage actuelle. La plus grande est exactement la hauteur visible de l'horizon.

**Heure**: `O(n log n)` pour le tri + heap ops.
**Espace**: "O(n)" pour les événements + tas.

---

2.2 L'approche *Bad* : la force brute

Texte
Pour chaque x de min (gauche) à max (droite):
pour = 0
pour chaque bâtiment:
si gauche <= x < droite: cur = max(cur, hauteur)
si cur change -> date
«» "

- **Complexité**: `O(n * width)` → impossible pour les grandes coordonnées (jusqu'à 231).
- **En cas d'échec**: la "largeur" peut être des milliards → mémoire/temps.
- **Pourquoi les recruteurs le détestent**: montre le manque de sensibilisation à la structure des données.

---

2.3 L'approche *Ugly* : Arbre segmentaire (compression coordonnée)

1. Compresser toutes les coordonnées uniques `left` et `right`.
2. Construire un arbre de segment sur les indices compressés.
3. Constructions de process triées par hauteur, gammes de mise à jour.
4. Traversez l'arbre pour extraire les points clés.

- **Pros**: Démontre des connaissances avancées en DS.
- **Cons**: Mise en œuvre trop poussée, longue, plus difficile à déboguer.
- **Lorsque les recruteurs l'apprécient**: Dans les rôles fortement axé sur la géométrie ou la programmation compétitive.

---

C'est vrai. Pourquoi maîtriser ce problème vous aide à trouver un emploi

Comment le problème Skyline le démontre
Il n'y a pas de différence entre les deux.
**La pensée algorithmique**Le choix de la ligne de balayage + le tas sur la force brute montre que vous pouvez raisonner sur la complexité optimale. Autres
**Structures de données** Autres
Autres **Edge‐Case Handling**. Autres
**L'écriture de solutions propres et bien commentées qui peuvent être expliquées dans une entrevue. Autres
**Sensibilisation au rendement**= Comprendre les compromis temps/espace et pourquoi certaines solutions ne sont acceptables que pour les petits intrants. Autres

Les intervieweurs aiment les problèmes qui nécessitent une solution claire** et une mise en œuvre propre**. Le problème Skyline coche les deux cases.

---

C'est pas vrai. Extraits de code d'échantillon (pour référence rapide)

Mots clés Autres
C'est pas vrai.
**Java** `PriorityQueue<entier> maxHeap = new PriorityQueue<>(Collections.reverseOrder());` Autres
**Python**"events.sort(key=lambda x: (x[0], x[1])"; "heapq.heappush(max_heap, h)"
**C++**="sort(events.begin(), events.end(), ...)"; `priority_queue<int> maxHeap;`="

---

C'est vrai. Liste de contrôle finale Avant l'entrevue

- [ ] Comprendre pleinement le format d'entrée/sortie.
- [ ] Expliquez le concept de *sweep line* avant de coder.
- [ ] Utilisez un **max-heap** (ou multiset) pour suivre les hauteurs actives.
- [ ] Émettre un point clé ** seulement lorsque la hauteur change**.
- [ ] Discuter du traitement des événements simultanés (par exemple, plusieurs bâtiments commençant par le même `x`).
- [ ] Mention de compression de coordonnées si demandé pour des solutions alternatives.

---

Appel à l'action

> **Vous voulez ace LeetCode 218? **
> Copiez les solutions fournies dans votre éditeur, passez à travers les cas de test, et pratiquez expliquer chaque étape à haute voix.
> Puis, déposez le lien de blog dans votre liste de prép d'entrevue et montrez aux recruteurs que *vous connaissez vos algorithmes*.

---

> **Note de l'auteur:**
> Les trois solutions de code ci-dessus implémentent la stratégie de balayage *Good*, qui ne diffère que par syntaxe. Testez-les localement, de petits commentaires, et vous serez prêt pour toute entrevue où le problème Skyline apparaît.

---

Bon codage, et que votre *skyline* soit aussi claire et efficace que les solutions ci-dessus! C'est ce qu'il a dit.

---

* Fin de l'article. *