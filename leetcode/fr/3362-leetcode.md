---
titre: LeetCode 3362. Zero Array Transformation III -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

- Oui. 1. Code – Java / Python / C++ (Création de Zero Array III)

Texte
LeetCode 2719 – Zero Array Transformation III
«» "

Langue Nom du fichier Faits saillants Autres
- C'est quoi ?
**Java**= `Solution.java`= Utilise `Arrays.sort` + deux `PriorityQueue`s (pape maximale pour les extrémités, lepape min pour les requêtes déjà utilisées)=
**Python**="solution.py`=" Utilise `heapq` + deux compteurs – un pour les requêtes actives, un pour les intervalles ="
*C++**= `Solution.cpp`== Utilise `sort`, `priority_queue<int>` (max-heap) et un vecteur de crédits de décrément

> **NOTE** – Les trois implémentations suivent la même stratégie *greedy + line-sweep* qui garantit le nombre minimum d'opérations requis.
> La réponse est simplement « TotalQueries – UsedQueries» (ou la taille du tas laissé après le balayage).

---

1.1 Mise en œuvre de Java

"Java
// -------- Code de Leet 2719 – Transformation de la représentation zéro III -------
Importation de java.util.*;

solution de classe publique {
***
* @param Un tableau de nombres entiers
* Liste des requêtes @param des opérations [l,r]
* @retour maximum de requêtes amovibles ou -1 si impossible
*/
public int maxRemoval(int[] A, int[][] requêtes) {
int n = longueur A, q = longueur des requêtes;

Trier les requêtes par index de départ (l)
les tableaux.sort(queries, (x, y) -> Integer.compare(x[0], y[0]);

// / / / / / / / / / / / / / / / / / / / / / / / / /
PriorityQueue<Integer> h = nouveau PriorityQueue<>(Collections.reverseOrder());

// EndCount[i] – combien de requêtes sélectionnées terminent *après* position i
int[] endCount = nouveau int[n + 1];
int utilisé = 0; // nombre de requêtes actuellement actives
int pos = 0; // index dans les requêtes[]

pour (int i = 0; i < n; i++) {
// supprimer les requêtes qui viennent de se terminer
utilisé -= finCount[i];

// ajouter de nouvelles requêtes qui commencent à ou avant i
pendant que (pos < q && requêtes[pos][0] <= i) {
h.offre(requêtes[pos][1]); //
pos++;
}

// nous avons besoin de diminutions A[i] sur la position i
pendant la période (utilisée < A[i]) {
si (h.isEmpty()="h.peek() < i) { // aucune requête utilisable
retour -1;
}
int e = h.poll(); // choisir la requête se terminant le plus loin
endCount[e + 1]++; // cessera d'affecter après e
used++; // nous avons maintenant une requête active de plus
}
}

/* Requêtes supplémentaires = toutes les requêtes qui n'ont jamais été choisies */
retourner les requêtes. longueur - utilisée;
}
}
«» "

---

1.2 Mise en œuvre de Python

'`python
# -------- Code de Leet 2719 – Transformation de la représentation zéro III -------
importation heapq
de taper l'importation Liste

Solution de classe:
def maxRemoval(self, A: List[int], requêtes: List[List[int]]) -> Int:
"""
Greedy + line‐sweep avec un lourd max.
"""
Trier par index de départ
requêtes.sort()
n, q = len(A), len(queries)

# 2-pap max pour les extrémités de toutes les requêtes "disponibles"
h = [] # le heapq de python est un min-heap -> utiliser des négatifs
end_cnt = [0] * (n + 1) # combien de requêtes choisies finissent après i
utilisé = 0
pos = 0

pour i dans la plage(n):
# Les requêtes de publication qui ont pris fin
utilisé -= fin_cnt[i]

# 4-- ajouter de nouvelles requêtes qui commencent maintenant
alors que pos < q et requêtes[pos][0] <= i:
heapq.heappush(h, -queries[pos][1]) # stock négatif pour simuler le poids max
pos += 1

Nous avons besoin de diminutions à l'indice i
pendant l'utilisation < A[i]:
si non h ou -h[0] < i: # aucune requête utilisable
retour -1
e = -heapq.heappop(h) # choisir la requête la plus éloignée
fin_cnt[e + 1] += 1
utilisé += 1

Les requêtes restantes sont celles amovibles
retour len(h)
«» "

---

*## 1.3 C++ Mise en œuvre

'`cpp
// -------- Code de Leet 2719 – Transformation de la représentation zéro III -------
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxExemption(vecteur<int>& Un vecteur<vecteur<int>>&questions) {
int n = (int)A.size(), q = (int)queries.size();
trier(queries.begin(), requêtes.end()); // trier par début l

priority_queue<int> h; // max-heap des extrémités
vector<int> endCnt(n + 1, 0); // combien de requêtes sélectionnées finissent après i
int utilisé = 0; // nombre de requêtes actives
int pos = 0; // index dans les requêtes[]

pour (int i = 0; i < n; ++i) {
// publier les requêtes terminées
utilisé -= endCnt[i];

// ajouter de nouvelles requêtes disponibles
pendant que (pos < q && requêtes[pos][0] <= i) {
h.push(queries[pos][1]); // indice de fin de poussée
+pos;
}

// besoin de diminutions A[i] à la position i
pendant la période (utilisée < A[i]) {
si (h.vide()="h.top() < i) // aucune requête utilisable
retour -1;
e = h.top(); h.pop();
endCnt[e + 1]++; // cessera d'affecter après e
++utilisé;
}
}
// Toutes les requêtes qui n'ont jamais été choisies sont amovibles
retour (int)h.size();
}
};
«» "

Les trois codes fonctionnent dans **O(n + q) log q)** time et **O(n + q)** espace, confortablement dans les limites de 1 s / 256 Mo pour le problème.

---

- Oui. 2. Article du blog – La transformation III de Zero Array : le bon, le mauvais, le mauvais

> **Mots clés** – LeetCode, Zero Array Transformation III, problème de codage d'entrevue, algorithme gourmand, file d'attente prioritaire, balayage de ligne, Java, Python, C++, entretien d'emploi, structures de données, algorithme, recherche d'emploi, entretien de programmation, entretien de structures de données.

---

2.1 Introduction

Si vous chassez un rôle d'ingénierie logicielle, l'une des façons les plus rapides de mettre en valeur vos côtelettes algorithmiques est de s'attaquer à un problème *LeetCode* qui combine les connaissances des structures de données avec le raisonnement avide. **Zero Array Transformation III** est une vitrine parfaite : c'est un problème moderne et convivial pour les interviews qui nécessite une solution propre et optimale et offre un bon début de conversation avec votre futur employeur.

---

### 2.2 Énoncé du problème (reformulé)

> **Don**:
> - Un tableau `nums` de longueur `n` (0-indexé), chaque élément `nums[i]` est un entier non négatif.
> - Une liste de requêtes `q`. Chaque requête est une paire `[l, r]` qui signifie "décret" tous les éléments `nums[l] ... nums[r]` par 1.
>
> **Tâche**: Trouvez le nombre maximum de requêtes qui peuvent être supprimées tout en pouvant réduire chaque "nums[i]` à zéro ou moins en appliquant *certaines* des requêtes restantes (chaque requête peut être utilisée au plus une fois).
> Si il est impossible de faire chaque élément zéro, retourner `-1`.

**Contrôles* *
- `1 ≤ n, q ≤ 5 · 104`
- < 0 ≤ nombres[i] ≤ 5 · 104»
- `0 ≤ l ≤ r < n`

---

2.3 Pourquoi ce problème est-il amical?

1. **Overlaps & Greedy** – Vous devez décider *quel* requêtes utiliser, et cette décision dépend du *couverture* de chaque requête.
2. **Priority Queue Mastery** – De nombreux candidats se retrouvent coincés sur la façon de choisir la bonne requête – un test classique de la connaissance de la file prioritaire.
3. **Line Sweep Intuition** – Une combinaison soignée de ligne de balayage et d'avidité qui semble propre dans un cadre de tableau blanc.
4. **Space & Time Trade‐off** – Résoudre le problème dans le journal « O(n+q) log q) » démontre une conscience de la performance asymptotique.

---

2.4 Aperçu de la solution

1. **Transformer le problème** – Au lieu de rechercher directement des requêtes *extra*, nous calculons le nombre de requêtes *minimum* requis pour zéro du tableau.
*Réponse = « Total des requêtes – minimum des requêtes utilisées».*

2. **Passer de gauche à droite* *
- En marchant dans le réseau, nous maintenons:
- `utilisé` – le nombre de requêtes actives qui couvrent actuellement la position `i`.
- Un max-heap (`h`) tenant les indices de fin de *toutes les requêtes disponibles* qui commencent avant ou à `i`.
- À chaque indice `i` nous avons besoin exactement `nums[i]` des diminutions.
- Si `utilisée < nums[i]`, nous choisissons avec cupidité la requête qui se termine le plus à droite (`h.top()`), parce qu'elle nous garde 'couverts' pour le plus long stretch possible.
- Lorsqu'une requête choisie se termine, nous enregistrons qu'elle cessera de couvrir le tableau *after* de son index final, de sorte que nous pourrons plus tard décrémenter `utilisé`.

2. **Traitement des cas** –
- Si, à un moment donné, le tas est vide ou si l'index final de la requête la plus éloignée est `< i`, le tableau ne peut pas être mis à zéro → retourner `-1`.

3. ** Extraction des résultats** – Après le balayage, le tas contient toutes les questions qui ont été ** jamais** choisies. Ce sont exactement ceux qui sont amovibles.

---

### 2.5 Marche pas à pas (Pseudo de Java)

Texte
1. trier les requêtes par l
2. h = poids maximal des extrémités
3. EndCount = [0 ... n] // combien de requêtes choisies finissent après i
4. utilisé = 0, pos = 0
5. pour i en 0 ... n-1:
used -= endCount[i] // release des requêtes terminées
alors que pos < q && requêtes[pos].l <= i:
h.push(queries[pos].r) // nouvelle requête disponible
pos += 1
pendant l'utilisation < nums[i]:
si h.isEmpty ou h.peek() < i: retour -1
e = h.pop() // requête la plus éloignée
finCount[e+1] += 1 // il s'arrêtera après e
utilisé += 1
6. retour totalQueries - utilisé
«» "

Les extraits de code Java, Python et C++ dans la première section implémentent cet algorithme en un seul passage.

---

2.6 Les bonnes

Qu'est-ce qui est génial ? Autres
- Oui.
**Optimal** – Le choix avide de la requête qui se termine le plus est certainement optimal. Autres
**Clarity** – Une seule boucle, deux structures de données simples ; vous pouvez dessiner la logique en moins de 30 secondes. Autres
**Language-agnostic** – Fonctionne également bien en Java, Python et C++ – parfait pour un *écran de téléphone technique* où vous pouvez changer de langue. Autres
**Test-ready** – Écrivez `unittest`/`pytest`/`gtest` en minutes pour montrer que votre solution passe tous les cas d'angle. Autres

---

2.7 Les mauvais

Pièges communs
- Oui.
**Penser à supprimer toutes les requêtes sauf une** – Ne pas réaliser que nous avons besoin de l'ensemble *minimum* de requêtes. Autres
**Scan linéaire + sélection de force brute** – O(`n·q`) solutions time-out sur les plus grands cas de test. Autres
**L'orientation d'un tas de déchets** – L'utilisation d'un petit tas où un lourd max est nécessaire conduit à la sélection d'une requête et à des boucles infinies. Autres
**Ignorer les crédits de fin** – oublier de marquer quand une requête choisie cesse de couvrir conduit à un double comptage et à des résultats incorrects. Autres

---

#### 2.8 La moche

> Et si le tableau est gigantesque ? Et si les requêtes étaient trop nombreuses ? Comment puis-je gérer les caisses de bord?

Dans les interviews du monde réel, vous pourriez rencontrer:

- **Très hautes valeurs «nums[i]»** – La cupidité fonctionne encore; vous avez juste besoin de suffisamment de demandes de couverture.
- **Couverture par voie de communication** – Si de nombreuses requêtes sont courtes et que le tableau a une valeur énorme à un certain index, vous allez rapidement frapper la branche `-1` – un bon moment pour discuter de pourquoi il est impossible.
- ** Pression de mémoire** – Un vecteur naïf de la taille `nq` va exploser. L'astuce `endCount` maintient la mémoire linéaire.

---

2.9 Comment parler Sur un appel

1. **Sketch la ligne de balayage** – Dessinez une ligne d'index, placez tous les intervalles de requête, et pointez les intervalles disponibles par rapport aux intervalles choisis.
2. **Expliquez la règle gourmande** – Nous utilisons toujours l'intervalle qui s'étend le plus loin car il maintient nos options ouvertes le plus longtemps possible. (en milliers de dollars)
3. **Mention le tas** – La "PriorityQueue" (max-heap) est idéale ; la "heapq" de Python avec des valeurs negées fonctionne tout aussi bien. (en milliers de dollars)
4. **Afficher les maths** – Le temps de running est `O(n+q) log q)` parce que chaque push/pop est `log q`. La mémoire est `O(n+q)` Parce que nous gardons un tableau de comptoir simple. (en milliers de dollars)
5. **Couverture du test de mise en évidence** – Cas d'Edge : tous les zéros → réponse = `q`. Cas impossible → `-1`.

---

#### 2.10 TL;DR pour votre mémoire

> **Création d'un rayon d'antenne III**
> • Greedy + ligne de balayage + max-heap
> • temps `O(n+q) log q)`, `O(n+q)` espace
> • Implémenté en Java, Python et C++ (prêt pour l'interview)

Ajoutez ceci à votre portfolio, lancez-le contre les *Sample Test Cases* de LeetCode, et vous aurez une histoire prête à partager qui montre que vous pouvez *lire* un tableau, *penser* au chevauchement des intervalles, et *appliquer* une solution optimale – tous dans un seul passage.

---

- Oui. 3. Liste de contrôle de démarrage rapide pour votre entrevue

1. **Lisez l'énoncé du problème** – soulignez le nombre minimum de requêtes requis.
2. **Trier les requêtes par index de démarrage** – O(q log q).
3. **Passer de gauche à droite** – Gardez un compteur de requêtes actives.
4. **Utilisez un max-heap** – Choisissez l'intervalle le plus lointain lorsque vous avez besoin de plus de couverture.
5. **Supprimer les requêtes terminées** – Soustraire du compteur actif en utilisant `endCount[i]`.
6. **Retourner `totalQueries – usedQueries`** – C'est la réponse que vous avez demandée.

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit