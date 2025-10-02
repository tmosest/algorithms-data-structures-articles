---
titre: LeetCode 480.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. La récapitulation du problème

> **Fenêtre coulissante médiane**
> On vous donne un tableau entier `nums` et un entier `k`.
> Une fenêtre coulissante de la taille `k` se déplace de la gauche du tableau à la droite, une étape à la fois.
> Pour chaque fenêtre, affichez la médiane des numéros `k` dans la fenêtre.
> Si `k` est impair, la médiane est le nombre moyen dans la fenêtre triée.
> Si `k` est même la médiane est la moyenne* des deux nombres moyens.

Contraintes typiques:
* `1 ≤ k ≤ longueur nums ≤ 10^5`
* "-2^31 ≤ nums[i] ≤ 2^31 – 1"

La précision requise est 1e‐5.

> **Pourquoi est-ce une question de LeetCode ? **
> Il teste votre connaissance des structures de données équilibrées, des techniques de fenêtre coulissante et du traitement minutieux des valeurs dupliquées.

---

- Oui. 2. La solution «Good» – Deux montures + Lazy Deletion

La façon la plus propre de maintenir une médiane dynamique est de garder deux tas:

L'invariant
C'est quoi ?
"maxHeap" (un max-Heap)
"minHeap" (une moitié supérieure (>= médiane)

**Idée clé**
* La médiane est soit «maxHeap.top()» (odd `k`) ou la moyenne de `maxHeap.top()` et `minHeap.top()` (même `k`).
* Lors de l'insertion d'un nouvel élément, nous l'avons mis dans le bon tas, puis rééquilibrer.
* Supprimer un élément qui a *slide out* de la fenêtre est la partie dure parce que les tas Java / Python n'ont pas de `remove(element)` dans O(log n).
Nous le résolvons avec une carte *lazy-deletion* ('relayed') qui enregistre combien d'instances d'une valeur doivent être ignorées lorsqu'elle apparaît sur un plateau.

2.1 Mise en œuvre de Java

"Java
Importation de java.util.*;

cours public coulissantWindowMedien {
public double[] médianeSlidingWindow(int[] nums, int k) {
// Levure maximale pour la moitié inférieure
Priorité Queue<Integer> low = new PriorityQueue<>(Collections.reverseOrder());
// Mince de la moitié supérieure
PrioritéQuue<entier> élevée = nouvelle prioritéQuue<>();

// Carte pour se souvenir des nombres de suppressions retardées
Carte <entier, entier> retardée = nouvelle HashMap<>();

Int lowSize = 0, highSize = 0; // tailles logiques (ignorer retardé)
double[] ans = nouveau double[nums.longueur - k + 1];
Int ansIdx = 0;

// Helper: prune haut d'un tas s'il est prévu pour la suppression
BiConsommateur <PriorityQueue<Intégre>, Intéger> prune = (pap, signe) -> {
pendant que (!heap.isEmpty()) {
int num = heap.peek();
Entier d = retard.get(num);
si (d != null &&d > 0) {
// supprimer cet événement
retard.put(num, d - 1);
si (delayed.get(num)) == 0) retrait différé(num);
poids lourds();
si (signat) 1) faible Taille... Taille...
} autre pause;
}
};

pour (int i = 0; i < nombres de longueur; i++) {
int num = nums[i];

// 1. Insérer un nouvel élément
i (faible.isEmpty()== num <= low.peek()) {
low.offre(num);
faible Taille++;
} autre {
offre élevée(num);
élevé Taille++;
}

// 2. L'équilibre s'accumule de telle sorte que :
si (faible taille > haute taille + 1) {
offre élevée(faible.poll());
faible Taille élevée Taille++;
} sinon si (taille élevée > taille basse) {
faible.offre(haut.poll());
élevé Taille... Taille++;
}

// 3. Slide window si nous avons déjà des éléments k
si (i >= k) {
int out = nombres[i - k];
// Marque pour suppression différée
retarde.merge(out, 1, entier::sum);
si (hors <= low.peek()) taille basse... Taille...

// Planchers si nécessaire
prune.accept(faible, 1);
prune.accept(élevé, -1);

// Rééquilibre après suppression
si (faible taille > haute taille + 1) {
offre élevée(faible.poll());
faible Taille élevée Taille++;
} sinon si (taille élevée > taille basse) {
faible.offre(haut.poll());
élevé Taille... Taille++;
}
}

// 4. Enregistrer la médiane une fois que nous avons une fenêtre complète
si (i >= k - 1) {
si (k & 1) == 1) { // impair
ans[ansIdx++] = low.peek();
} autre { // même
[ansIdx++] = (low.peek() + high.peek()) / 2.0;
}
}
}

le retour des an;
}
}
«» "

**Pourquoi est-ce bien ? * *

* **O(n log k)** time – chaque insertion, suppression ou équilibre est O(log k).
* **O(k)** espace supplémentaire – deux tas + carte retardée.
* Gérez correctement les duplicata grâce à la suppression retardée.
* Pas besoin d'un arbre de recherche binaire équilibré (par exemple "TreeSet") – plus facile à comprendre pour la plupart des intervieweurs.

2.2 Mise en œuvre de Python

'`python
importation heapq
de collections importer par défautdict

Solution de classe:
def médianeSlidingWindow(self, nums, k):
faible, élevé = [], [] # max-pap (comme négatifs), min-pap
reporté = par défautdict(int) # carte de suppression paresseuse
ans = []
taille basse = taille élevée = 0

def prune(pap, signe):
# signe = 1 pour faible, -1 pour élevée
pendant que le tas:
num = -pap[0] si le tas est faible, autrement [0]
si elle est différée[num]:
(pauvreté)
retard[num] -= 1
si signe == 1: taille basse -= 1
Autre : taille élevée -= 1
Sinon:
pause

pour i, num in énumérate(nums):
# insérer
s'il n'est pas faible ou num <= -faible[0]:
heapq.heappush (faible, -num)
faible Taille += 1
Sinon:
heapq.heappush (haut, num)
Taille élevée += 1

# solde
si lowSize > highSize + 1:
heapq.heappush(haut, -heapq.heappop(bas))
Taille basse -= 1
Taille élevée += 1
elif highTaille > faible Taille:
heapq.heappush(bas, -heapq.heappop(haut))
Taille élevée -= 1
faible Taille += 1

# Diapositive
i >= k:
out = nombres[i - k]
retard[out] += 1
si hors <= -faible[0]:
Taille basse -= 1
Sinon:
Taille élevée -= 1
prune(faible, 1)
Prune(élevée, -1)
si lowSize > highSize + 1:
heapq.heappush(haut, -heapq.heappop(bas))
Taille basse -= 1
Taille élevée += 1
elif highTaille > faible Taille:
heapq.heappush(bas, -heapq.heappop(haut))
Taille élevée -= 1
faible Taille += 1

# médiane
Si i >= k - 1:
si k % 2:
(-faible[0])
Sinon:
Annexe((-faible[0] + élevée[0]) / 2.0)

retour et
«» "

C++ Mise en œuvre

Le multiset C++=s nous donne déjà une BST équilibrée avec itération ordonnée, de sorte que nous pouvons maintenir un multiset *simple* et garder un itérateur à la médiane. Cette approche est concise et parfaitement O(n log k).

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur <double> médianeCoulissement Fenêtre(vecteur<int>& nums, int k) {
vecteur<double> rés;
multiset<int> window(nums.begin(), nums.begin() + k);
auto mid = next(window.begin(), k/2); // itérateur à médiane

pour (int i = k; i <= nums.size(); ++i) {
// ajouter le nouvel élément (lorsque i == k nous en avons déjà un)
si (i) k) {
// rien à faire – nous sommes au début plein fenêtre
} autre {
window.erase(window.find(nums[i - k])); // feuilles d'élément
window.insert(nums[i]); // nouvel élément

// se déplacer au milieu pour garder le pointage à la médiane
si (nums[i] < *mid) {
si (k % 2 == 0) ++mid; // nouvel élément est sur la gauche
} autre {
si (k % 2 == 1) --mid; // nouvel élément à droite
}

si (nums[i - k] <= *mid) {
si (k % 2 == 0) --mid; // élément enlevé était sur la gauche
} autre {
si (k % 2 == 1) ++mid; // élément enlevé était à droite
}
}

// calculer la médiane
si (k % 2) { // impair
res.push_back(*mid);
} autre { // même
auto nextMid = next(mid);
res.push_back((static_cast<double>(*mid) + *nextMid) / 2.0);
}
}
retour rés;
}
};
«» "

**Pourquoi est-ce bien ? * *

* Utilise l'arbre équilibré STL, pas d'équilibrage de tas laminé à la main.
* Conserve l'itérateur à la médiane afin que nous puissions demander en O(1).
* Toujours **O(n log k)** – chaque effacer/insérer dans le multiset est O(log k).

---

- Oui. 3. L'approche "Bad" (Simpler) – Trier chaque fenêtre

'`python
def bad(nums, k):
res = []
pour i dans la plage (len(nums) - k + 1):
win = trié(nums[i:i+k])
milieu = len(win)//2
si k % 2: res.append(win[mid])
autres: res.append((win[mid-1]+win[mid])/2)
retour res
«» "

* **O(n k log k)** – beaucoup trop lent pour `k = 10^5'.
* Fonctionne uniquement sur les entrées de jouets; les intervieweurs signaleront immédiatement l'inefficacité.

C'est la base de *mauvais* qui démontre pourquoi vous ne pouvez pas simplement re-sort.

---

- Oui. 4. Les affaires du coin de l'Ugly

Scénario Qu'est-ce qui peut mal tourner ? Comment l'éviter
-- -- -- -- -- -- -- -- -- -- -- --
Un "TreeSet" naïf s'effondrera en un seul élément, perdant des comptes. Utiliser `multiset` (C++), ou `TreeMap<Intéger, Integer>` + itérateur (Java), ou cartes de suppression différée (approche du talon). Autres
**Sliding window delete** Lazy‐deletion, ou utilisez une BST qui supporte la suppression dans O(log n). Autres
**Même la précision `k`** Explicitement jeté sur `double` ou `float` avant la division. Autres
En C++ `multiset::erase(it)` invalide seulement `it`.
**Les plus grands nombres négatifs**= En Java max‐heap avec `PriorityQueue<Intéger>` fonctionne bien; en Python vous avez besoin de nombres négatifs pour un max‐heap. Stick à des idiomes spécifiques au langage. Autres
**Excédent de débit en moyenne**= `maxHeap.top() + minHeap.top()` peut déborder de 32 bits int.== Conversion en `long long` ou `double` avant le summing. Autres

---

- Oui. 5. Résumé de la complexité

Démarche Temps Espace supplémentaire
- C'est quoi ?
Autres Deux-pap + suppression paresseuse
"multiset" + itérateur médian (C++)
Tri de chaque fenêtre (mauvais)

Toutes les solutions sont acceptables pour la solution officielle LeetCode, mais l'approche à deux fois est *la* la plus conviviale pour les interviews.

---

- Oui. 6. Écrire l'article du blog – SEO‐Ready, Job‐Ready

> **Titre:**
> *=Sliding-Window Median – L'intervieweur est un problème difficile favori (Java, Python, C++)*

### 6.1 Description de la méta (= 155 caractères)

> Maîtrisez le problème difficile *Fenêtre coulissante Médiane* LeetCode. Lisez notre guide détaillé avec le code Java, Python et C++, des astuces de performance et des conseils d'entrevue.

6.2 Aperçu

1. **Énoncé du problème et importance**
* Récapitulation rapide + pourquoi elle compte dans l'analyse du monde réel.
2. **Naïf contre optimal**
* Afficher l'astuce O(n k log k) tri-in-window, puis expliquer pourquoi elle échoue.
3. **Stratégie des deux puits**
* Expliquez les structures de données, les invariants et comment conserver la médiane.
* Afficher le pseudo-code et mettre en évidence la suppression paresseuse.
4. ** Multiset + itérateur** (C++ & Java alternative)
* Lorsqu'une TVB équilibrée est plus simple.
5. **Liste de contrôle des cas* *
* Dupliquer les valeurs, les nombres négatifs, la taille de la fenêtre.
6. **Performance et mémoire**
* Big-O, la convivialité du cache, pourquoi la suppression paresseuse est encore rapide.
7. **Conseils d'entrevue**
* Comment parler de l'algorithme en 5 minutes d'entrevues.
* Ce que les intervieweurs recherchent habituellement: * arbres équilibrés, tricks de tas, O(n log k) temps, clarté*.
8. **À emporter et lecture supplémentaire**
* Lien vers des sujets avancés : *Arbres statistiques de commande, Fenwick/BIT avec deux pointeurs, RMQ*.

6.3 L'article complet du blog

---

### Sliding-Window Median: Masterclass pour les entrevues

> **TL;DR** – Garder deux tas (pap maximum pour la moitié inférieure, un peu pour la moitié supérieure). Utilisez la suppression paresseuse pour supprimer les éléments hors fenêtre dans *O(log k*). Complexité : **O(n log k)** temps, **O(k)** espace.

---

Problème profond Plongée

Dans le monde réel, vous aurez souvent besoin de calculer une statistique sur une fenêtre coulissante – pensez * moyenne tournante*, * médiane mobile* ou * détection aberrante en ligne*. La médiane est le *centre* des données et est robuste aux valeurs extrêmes – c'est pourquoi elle est utilisée dans la finance, la fusion des capteurs et la détection des anomalies.

Compte tenu des contraintes (`n = 10^5`), toute solution qui re-trie chaque fenêtre (`O(n k log k)`) sera time‐out. Vous avez besoin d'une structure de données qui supporte **insertion, suppression et récupération de l'élément k/2-th** dans le temps logarithmique.

---

C'est pas vrai. Pourquoi gagner

* Un **max-heap** vous permet de connaître toujours l'élément le plus important de la moitié *inférieure*.
* Un **min-heap** vous donne le plus petit élément de la moitié *upper*.
* La médiane est soit la partie supérieure de la heap max (fenêtre od) soit la moyenne des deux parties supérieures (même la fenêtre).

Lorsque la fenêtre glisse, vous supprimez un élément qui peut être n'importe où dans les tas. Supprimer un élément arbitraire directement d'un tas est coûteux, mais nous pouvons **retard** la suppression:

«» "
paresseux[num]++ // marque qu'une instance de 'num' doit être ignorée
«» "

Lorsqu'un élément se trouve en haut d'un tas, nous vérifions s'il est marqué pour être supprimé; si oui, nous le popons et nous décrétons le compteur paresseux. Cela permet de garder chaque tas propre et maintient les opérations O(log k).

---

- Oui. Code Marche à suivre

> **Java**

"Java
public double[] médianeSlidingWindow(int[] nums, int k) {
// deux tas + carte de suppression différée
Priorité Queue<integer> low = new PriorityQueue<>(Collections.reverseOrder()); // max‐heap
PrioritéQuue<entier> élevée = nouvelle prioritéQuue<>();
Carte <entier, entier> retardée = nouvelle HashMap<>();
Int lowSize = 0, highSize = 0;

double[] ans = nouveau double[nums.longueur - k + 1];
Int idx = 0;

// ... fonctions d'aide prune(), balance(), slide() ...
}
«» "

> **Python**

'`python
Solution de classe:
def médianeSlidingWindow(self, nombres: List[int], k: int) -> Liste [float]:
# deux tas + Compteur pour suppression paresseuse
faible, élevé = [], [] # max-heap (négatifs)
différé = defaultdict(int)
# ... reste du code ...
«» "

> **C++**

'`cpp
solution de classe {
public:
vecteur <double> médianeCoulissement Fenêtre(vecteur<int>& nums, int k) {
multiset<int> window(nums.begin(), nums.begin()+k);
auto middle = next(window.begin(), k/2);
// ... glissière, pruneau, balance ...
}
};
«» "

Les trois extraits partagent les mêmes **variantes** et **complexités temps/espace**.

---

Analyse de complexité

Opération (Java/Python)
Il y a un problème.
Insérer "O(log k)" Autres
Suppression de la mention "O(log k)" Autres
Médiane Autres
**O(n log k)
Mémoire **O(k)**

La suppression **lazy** garantit que vous ne payez jamais plus que `O(log k)` pour supprimer un élément, même si l'élément réel peut être profond dans un tas.

---

##### 5.

Une erreur fréquente
Il n'y a pas de lien entre les deux.
Les valeurs dupliquées `TreeSet` les effondrent `multiset` (C++), `TreeMap` + nombres (Java)
Autres Même la taille de la fenêtre.
Nombres négatifs , Max-heap a besoin de négatifs dans Python , Utilisez `-value` pour le tas
Autres Le dépassement sur la somme `max + min` peut déborder de 32-bits.

---

C'est pas vrai. Présentation de l'entrevue

* ** Commencez par un diagramme** – dessinez deux tas et montrez comment la médiane se trouve au milieu.
* ** Indiquer les invariants** :
* `low.size() == high.size()` ou `low.size()== high.size() + 1` (selon la parité `k`).
* Tous les éléments dans `faible` ≤ tous les éléments dans `haut`.
* ** Expliquez la suppression paresseuse** dans une phrase : "Nous allons garder un compteur d'éléments qui doivent être enlevés, et les nettoyer quand ils atteignent le sommet. (en milliers de dollars)
* **Voir le pseudo-code**: O(n log k) est le titre.
* **Adresse Pourquoi il est robuste**: la médiane est moins affectée par des valeurs aberrantes que la moyenne, un bon point de discussion pour les rôles financiers/analytiques.

Les intervieweurs apprécient le code qui est *clair* et *testable*, donc inclure des tests unitaires pour les fenêtres impair/même, les duplicata et les nombres négatifs.

---

À emporter

1. **Two-heap + délétion paresseuse** est la norme or pour la médiane de la fenêtre coulissante.
2. Pour les utilisateurs C++, un « multiset » avec un itérateur médian peut être encore plus simple.
3. Toujours vérifier les cas de bord: duplicata, nombres négatifs, et même `k`.
4. Dans une entrevue, énoncez le *pourquoi* derrière chaque opération, pas seulement le *comment*.
5. Pratiquez le codage dans les trois langues – chaque entreprise peut vous tester sur votre pile préférée.

---

Autres ressources

* **Arbre de statistiques de commande** – maintenir l'élément k/2-th dans O(log n).
* **Binary Indexed Tree (Fenwick)** avec deux pointeurs – une solution hors ligne soignée pour les tableaux statiques.
* **Segment Trees avec propagation paresseuse** – pour les mises à jour et les requêtes de portée.

---

##### # 8

La médiane de la fenêtre coulissante est plus qu'un exercice de codage; c'est un outil d'analyse des données du monde réel. La maîtrise démontre votre capacité à :

* Choisissez la bonne structure de données (pavillons, BST).
* Optimisez pour le temps/l'espace sous de grandes entrées.
* Pensez à des suppressions et des données statiques.

Avec les implémentations Java, Python et C++ fournies, vous êtes prêt à saisir le problème difficile de LeetCode *et* as l'interview.

---

** Fait!**

Cet article présente non seulement le code, mais il donne un *talk track* interviewers aimera. En mettant l'accent sur la performance, la clarté et la robustesse du boîtier, vous êtes prêt à briller dans toute entrevue de codage.

---

- Oui. 7. Mot final

Vous avez maintenant :

* Trois solutions prêtes à la production dans les trois langues principales.
* Une explication claire de la raison pour laquelle l'approche à deux montants est optimale.
* Une feuille d'écueils concise.
* Un billet de blog prêt à publier, SEO, optimisé pour améliorer votre visibilité en tant qu'ingénieur logiciel.

Bon codage – et bonne chance pour votre prochaine interview! C'est ce qu'il a dit.

---