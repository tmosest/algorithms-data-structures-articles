---
titre: LeetCode 1851. Intervalle minimum pour inclure chaque requête -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1851 – Intervalle minimal pour inclure chaque requête
### Solutions complètes (Java, Python, C++)

Ci-dessous vous trouverez trois implémentations complètes et prêtes à la production de la solution balay-line + file prioritaire la plus efficace.
Tous les trois partagent la même idée fondamentale :

1. **Trier les intervalles par heure de début.
2. **Demandes par valeur (conservation de leurs indices originaux).
3. Pour chaque requête `q`
* Poussez chaque intervalle dont le début est ≤ `q` dans un **min-heap** ordonné par la longueur de l'intervalle.
* pop chaque intervalle dont la fin < `q` (il ne peut pas couvrir la requête).
* le haut du tas est le plus petit intervalle valide – sa longueur est la réponse à cette requête.
4. Restaurer les réponses dans l'ordre de requête original.

La solution fonctionne
**O((n + m) log(n + m)** time et **O(n + m)** espace – assez rapide pour les limites (= 105 intervalles et requêtes).

---

C'est pas vrai. Java

"Java
Importation de java.util.*;

***
* Leetcode 1851 – Intervalle minimal pour inclure chaque requête
*
* L'algorithme utilise une ligne de balayage + min-heap.
* • Les intervalles sont traités par ordre de début.
* • Les requêtes sont traitées en ordre croissant.
* • Une file d'attente prioritaire ne conserve que des intervalles qui pourraient encore contenir la requête actuelle.
* • La file d'attente donne toujours le plus petit intervalle couvrant la requête.
*/
solution de classe publique {
public int[] minInterval(int[][] intervalles, int[] requêtes) {
// Trier les intervalles par heure de début
les tableaux.sort(intervalles, comparator.comparingInt(a -> a[0]);

// Jumeler chaque requête avec son index original
[] qWithIdx = nouvelle int[queries.longueur][2];
pour (int i = 0; i < requêtes.longueur; i++) {
qWithIdx[i][0] = requêtes[i]; // valeur
qWithIdx[i][1] = i; // position originale
}
// Trier les requêtes par valeur
(qWithIdx, Comparator.comparingInt(a -> a[0]);

// Min-heap ordonné par la longueur de l'intervalle (fin - début + 1)
PrioritéQueue<int[]> heap =
nouveau PriorityQueue<>(Comparator.comparingInt(a -> a[0] - a[1] + 1));

int[] result = nouvelle int[queries.longueur];
intervalIdx = 0; // pointeur par intervalles

pour (int[] q : qWithIdx) {
valeur int = q[0];
Int original Idx = q[1];

// Ajouter tous les intervalles qui démarrent la requête actuelle <=
pendant que (intervalleIdx < intervalles.longueur && intervalles[intervalleIdx][0] <= valeur) {
heap.offrer(intervalles[intervalleIdx++]); // stocker tout l'intervalle
}

// Supprimer les intervalles qui se sont terminés avant la requête
alors que (!heap.isEmpty() &&heap.peek()[1] < valeur) {
poids lourds();
}

// Le sommet du tas est le plus court intervalle couvrant la requête
résultat[originalIdx] = heap.isEmpty()
? -1
: heap.peek()[1] - heap.peek()[0] + 1;
}

le résultat du retour;
}
}
«» "

---

# # # # # #

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def minInterval(self, intervalles: List[List[int]], requêtes: List[int]) -> Liste[int]:
"""
Ligne de balayage + file d'attente prioritaire.

Durée : O(n + m) log(n + m)
Espace : O(n + m)
"""
# 1. Trier les intervalles par heure de début
intervalles.sort(key=lambda x: x[0])

2. Joindre les indices originaux aux requêtes
qs = trié([(q, i) pour i, q dans le dénombrement(creuses)])

3. Suspensions d'un lourd (longueur, fin)
heap = []

ans = [0] * len(creuses)
i = 0 # pointeur par intervalles

pour q, idx dans qs:
# ajouter tous les intervalles qui commencent <= q
alors que i < len(intervalles) et intervalles[i][0] <= q:
début, fin = intervalles[i]
heapq.heappush(pap, (fin - début + 1, fin))
i += 1

# supprimer les intervalles qui se sont terminés avant q
pendant le tas et le tas[0][1] < q:
(pauvreté)

# réponse à cette requête
ans[idx] = tas[0][0] si le tas est différent -1

retour et
«» "

---

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

/*
* Leetcode 1851 – Intervalle minimal pour inclure chaque requête
* Ligne de balayage avec priorité_queue (min-heap).
*/
solution de classe {
public:
vecteur<int> minIntervalle(vecteur<vecteur<int>> et intervalles,
vectorielle<int>&questions) {
// 1. Trier les intervalles par début
tri(intervalles.debut(), intervals.end(),
[](const auto& a, const auto& b) { retourner a[0] < b[0]; });

// 2. Conserver les indices originaux des requêtes
vecteur<pair<int,int>> q(queries.size());
pour (size_t i = 0; i < requêtes.size(); ++i) {
q[i] = {queries[i], static_cast<int>(i)};
}
Tri(q.begin(), q.end(),
[](const auto& a, const auto& b) { retourner a.first < b.first; });

// 3. Min-heap ordonné par la longueur de l'intervalle
utilisant pii = paire<int,int>; // {longueur, fin}
priorité_queue<pii, vecteur<pii>, plus<pii>> pq;

vectorielle <int> ans(queries.size());
taille_t i = 0; // pointeur à intervalles

pour (auto [val, idx] : q) {
// Les intervalles de poussée qui démarrent la requête actuelle <=
pendant que (i < intervals.size() && intervals[i][0] <= val) {
int len = intervalles[i][1] - intervalles[i][0] + 1;
pq.emplace(len, intervalles[i][1]);
++i;
}
// Les intervalles pop qui se terminent avant la requête
pendant que (!pq.vide() && pq.top().seconde < val)
La présente décision entre en vigueur le vingtième jour suivant celui de sa publication au Journal officiel de l'Union européenne.

ans[idx] = pq.vide() ? -1 : pq.top().first;
}
le retour des an;
}
};
«» "

Les trois implémentations utilisent la même stratégie de ligne de balayage + file prioritaire et fonctionnent confortablement sous les contraintes du problème.

---

Article de blog optimisé du SEO
**Titre:** 1851 – Intervalle minimum pour inclure chaque requête: Sweep‐Line + Heap en Java, Python, C++

**Meta Description:**
Résolvez le code 1851 en millisecondes. Découvrez la stratégie de file d'attente prioritaire, Java, Python, C++ et pourquoi elle surpasse la force brute. Parfait pour le codage des entrevues, la pratique des algorithmes et la préparation des entrevues.

---

C'est pas vrai. Pourquoi ce problème est important
Lorsque vous préparez une entrevue de codage, *interval requests* surgissent tout le temps : (en milliers de dollars)
Leetcode 1851 (Intervalle minimal pour inclure chaque requête) est un exemple canonique qui teste:

- **Capacités gâcheuses** – vous devez commander les intervalles et les requêtes efficacement.
- **Greedy + Data-structure synergie** – l'intervalle de couverture le plus court n'est pas évident sans un tas.
- **Travaux dans l'espace temporel** – force brute TLE; la solution optimale doit être sub-quadratique.

Si vous clouez ceci, vous aurez des problèmes similaires sur les entretiens réels et renforcer votre confiance algorithmique.

---

## 2=2 Bonne – L'élégante approche de la ligne de balayage + du talon
**Pourquoi c'est bon:**

Qu'est-ce que ça vous donne ? Pourquoi ça compte ?
-- -- -- -- -- -- -- -- --
**O((n+m) log(n+m)**= Fast for 105 intervals/quries= Performance prête à l'entrevue=
Autres **Un seul passage**= Pas de boucles imbriquées== Mémoire & CPU friendly==
**Clarifier la logique**= Ajouter au début ≤ q, pop quand fin < q=== Facile à expliquer & debug=
**Cadre réutilisable**

- Oui. Aperçu clé

À un point de requête `q` vous avez seulement besoin d'intervalles qui:

- début (autrement ils ne peuvent pas le couvrir)
- fin **≥ q** (autrement ils ont expiré)

L'intervalle *le plus petit* est ce que vous donne instantanément le talon min.

---

- Oui. Mauvais – Brute-Force, Hash Maps, ou deux-pointeurs erreurs
**Pièges communs** qui conduisent à des solutions ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- **Hash map of starts → lengths** – O(n+m) pour construire mais nécessite toujours de scanner *all* intervalles pour chaque requête → **O(n ·m)**.
- **Two-pointer avec un vecteur** – sans un tas, vous ne pouvez pas garantir l'intervalle le plus court.
- **La recherche binaire sur une liste triée de longueurs** – vous devez savoir si chaque longueur peut encore couvrir `q` ; c'est la même chose que le tas, mais la réimplantation manuelle est sujette à erreur.

> **Ligne de bottom:**
> Brute-force (`pour q dans les requêtes: pour l'intervalle dans les intervalles`) prend ~109 opérations → TLE.
> Toute solution qui fait ** plus que le travail linéaire** est généralement suspecte pour ce problème.

---

Pourquoi Brute ? Coups de force
Si vous êtes nouveau au problème, vous pouvez essayer une boucle imbriquée ou une carte simple des longueurs d'intervalle.
** Qu'est-ce qui ne va pas ? **

1. **Temps trimestriel** – 105 × 105 = 1010 opérations.
2. **Cache miss** – Accès à la mémoire aléatoire dans un grand vecteur.
3. **Pouvoir de tracer** – Même un petit bug (off‐by‐one en longueur) peut faire fausser toute la solution.

Les intervieweurs vous aiment pour expliquer *pourquoi* une solution naïve est inacceptable. Montrez-leur que vous connaissez les pièges et pourquoi le tas gagne.

---

C'est pas vrai. La mise en œuvre (Code Pseudo)

«» "
trier les intervalles au début
requêtes paires avec indices originaux
trier les requêtes par valeur

heap = heap min ordonné par la longueur de l'intervalle

intervallePtr = 0
pour la valeur, origIdx dans les requêtes triées :
pendant l'intervalle Ptr < intervals.size et intervals[intervalPtr].start <= valeur:
intervalles de poussée[intervalle Ptr] dans le tas
intervalle Ptr++

alors que le tas n'est pas vide et le tas. top.end < valeur:
Couche

réponse[origIdx] = tas vide ? -1 : lourd.top. longueur
«» "

> Ce pseudocode est language-agnostique; les trois extraits de code ci-dessus ne sont qu'un remplacement drop-in pour la langue avec laquelle vous êtes à l'aise.

---

## 6-
Opération Complexe Explication
- C'est quoi ?
Tri des intervalles **O(n log n)**
Tri des requêtes **O(m log m)**
Opérations de masse (poussées/pop)

Total: **O((n+m) log(n+m)** time, **O(n + m)** memory.

---

Questions d'entrevue courantes autour de ce problème

1. Pouvez-vous expliquer le choix avide? *
*Réponse:* À toute requête `q` nous ne considérons que les intervalles qui pourraient encore couvrir. Le min-heap garantit que nous choisissons celui avec la plus petite longueur immédiatement. (en milliers de dollars)

2. Et si deux intervalles ont la même longueur ? *
*Réponse:* Le tas est stable pour des longueurs égales parce que nous stockons aussi le point final – il n'affecte pas la justesse, juste l'ordre de rupture de cravate. (en milliers de dollars)

3. Comment adapteriez-vous cela si les requêtes venaient dans l'ordre arbitraire (non triées)? *
*Réponse:* Vous les triez toujours en interne, mais n'oubliez pas de stocker l'index original afin de pouvoir réassembler la sortie à la fin. (en milliers de dollars)

---

## 8:0 Réflexions finales et conseils d'entrevue

- **Afficher le motif** – la ligne de balayage + le tas est un puissant combo.
- **Edge cas** – test avec des requêtes en dehors de tous les intervalles et intervalles de longueur 1.
- **Exposer le tas** – beaucoup d'intervieweurs demandent pourquoi un tas? – Disons : Parce que nous avons besoin de la longueur *minimum* en tout temps. (en milliers de dollars)
- **Pratique** – résoudre des problèmes similaires: * Salles de réunion II*, * Flotte de voiture*, * Couverture d'intervalle*, * Overlap maximal*, etc.

Mastering Leetcode 1851 vous donne un bloc de construction algorithmique réutilisable que vous pouvez apporter avec confiance dans toute entrevue de structure de données. Bonne chance ! C'est ce qu'il a dit