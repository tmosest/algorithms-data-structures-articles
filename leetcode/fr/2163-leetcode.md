---
titre: LeetCode 2163. Différence minimale de sommes après suppression des éléments -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2163 – Différence minimale de montants après suppression des éléments
**Solution en Java, Python et C++**
**Blog Post:** *Le bon, le mauvais et le mauvais – Comment faire face à ce problème d'entrevue (et Land Your Dream Job)*

---

Résumé du problème
Compte tenu d'un tableau «nums» indexé à 0 de la longueur `3 * n`, nous devons **supprimer exactement les éléments `n`**.
Les éléments `2n` restants sont divisés en deux parties égales:

«» "
partie gauche – premiers éléments n → sommePremière
partie droite – éléments suivants n → sumSecond
«» "

Retourner la valeur **minimum possible** de "sumFirst – sumSecond".

> **Constraints**
> * `1 ≤ n ≤ 105`
> * `1 ≤ nombres[i] ≤ 105`
> * "longueur en nombres". 3*n'

---

- Oui. Idée de haut niveau
On peut penser au tableau comme **trois blocs contigus**:

«» "
[ gauche ] [ milieu ] [ droite ]
«» "

* Dans le bloc *gauche*, nous voulons garder les nombres les plus petits** `n` – ils feront partie de `sumFirst`.
* Dans le bloc *droit* nous voulons garder les nombres **les plus importants** `n` – ils feront partie de `sumSecond`.

Le défi consiste à décider **où couper** le tableau en `[0 ... i]` et `[i+1 ... 3n-1]` pour que la différence entre les deux sommes soit minime.

Stratégie
1. **Préfixe gauche** – pour chaque point de coupe possible `i` (après au moins `n` éléments et avant le dernier `n`), calculer la somme des nombres *n les plus petits* en `nums[0 ... i]`.
* Maintenez ces sommes en utilisant un **max-heap** ( file d'attente prioritaire) qui stocke les valeurs `n` actuelles les plus petites.
2. **Suffixe droit** – De même, pour chaque point de coupe `i`, calculer la somme des *n les plus grands* nombres en `nums[i+1 ... 3n-1]`.
*Maintenir* ces sommes en utilisant un **min-heap** qui stocke les valeurs actuelles `n` les plus importantes.
3. La réponse pour une coupure à la position `i` est `leftSum[i] – droiteSum[i+1]».
Scanner tous les `i` valides et garder le minimum.

**Complexité temporelle** – "O(n log n)" (opérations en lourd).
**Complexité spatiale** – `O(n)` pour les deux tableaux auxiliaires plus des tas.

---

- Oui. Mise en œuvre des références

#### 3.1 Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
public long minimumDifférence(int[] nombres) {
int len = longueur nominale; // 3 * n
int n = len / 3; // nombre d'éléments à supprimer
long[] leftSums = nouveau long[len];
long[] droitSums = nouveau long[len];

// ---------- côté gauche: garder n plus petit -----------------
Priorité Queue<Integer> maxLeft = nouveau PriorityQueue<>(Collections.reverseOrder());
longue gauche Somme = 0;
pour (int i = 0; i < n; i++) {
maxLeft.offre(nums[i]);
gauche Somme += nombres[i];
}
gauche Somme[n - 1] = gaucheSum; // premier préfixe valide

pour (int i = n; i < len - n; i++) {
int cur = nombres[i];
si (cur < maxLeft.peek()) { // remplacer le plus grand du tas
gauche Sum += cur - maxLeft.poll();
maxLeft.offre(cur);
}
gaucheSums[i] = gaucheSum;
}

// ---------- côté droit: garder n plus grand ----------------
Priorité Queue<integer> minRight = nouvelle prioritéQueue<>();
longue droite Somme = 0;
pour (int i = len - 1; i >= len - n; i--) {
minRight.offre(nums[i]);
rightSum += nombres[i];
}
rightSums[len - n] = rightSum; // dernier suffixe valide

pour (int i = len - n - 1; i >= n; i--) {
int cur = nombres[i];
si (cur > minRight.peek()) { // remplacer le plus petit dans le tas
rightSum += cur - minRight.poll();
minRight.offre(cur);
}
rightSums[i] = rightSum;
}

// -------- Calcul de la différence minimale -----------------
réponse longue = longue. MAX_VALEUR;
pour (int i = n - 1; i < len - n; i++) {
réponse = Math.min(réponse, gaucheSums[i] - droitSums[i + 1]);
}
réponse de retour;
}
}
«» "

---

3.2 Python 3.9+

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def minimum Différence(même, nombres: Liste[int]) -> Int:
n3 = len(nums) # 3 * n
n = n3 // 3
gauche = [0] * n3
droite = [0] * n3

# ----- à gauche: garder n plus petit -----
max_heap = [] # conservera les négatifs pour imiter le poids max
gauche_sum = 0
pour i dans la plage(n):
heapq.heappush(max_heap, -nums[i])
gauche_sum += nombres[i]
gauche[n - 1] = gauche_somme

pour i dans la plage (n, n3 - n):
pour = nombres[i]
si cur < -max_heap[0]:
Enlèvement = -heapq.heapreplace(max_heap, -cur)
gauche_sum += cur - enlevé
gauche[i] = gauche_sum

# ----- à droite: garder n plus grand -----
min_heap = []
right_sum = 0
pour i dans la fourchette(n3 - 1, n3 - n - 1, -1):
heapq.heappush(min_heap, nums[i])
right_sum += nombres[i]
droite[n3 - n] = droite_sum

pour i dans la fourchette(n3 - n - 1, n - 1, -1):
pour = nombres[i]
si cur > min_heap[0]:
Enlèvement = heapq.heapreplace(min_heap, cur)
right_sum += cur - supprimé
droite[i] = droite_sum

# ----- différence minimale
ans = flotteur('inf')
pour i dans la fourchette (n - 1, n3 - n):
ans = min(ans, gauche[i] - droite[i + 1])

retour et
«» "

---

### 3.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long long minimumDifférence(vecteur<int>& nombres) {
int len = nombres.size(); // 3 * n
int n = len / 3;

vecteur <long> gauche(len), droite(len);

// --------- à gauche: garder n plus petit - Oui.
priority_queue<int> maxLeft; // max-heap
longue gauche Somme = 0;
pour (int i = 0; i < n; ++i) {
maxLeft.push(nums[i]);
gauche Somme += nombres[i];
}
gauche[n - 1] = gaucheSum;

pour (int i = n; i < len - n; ++i) {
int cur = nombres[i];
si (cur < maxLeft.top()) {
gauche Sum += cur - maxLeft.top();
maxLeft.pop();
maxLeft.push(cur);
}
gauche[i] = gaucheSum;
}

// -------- à droite: garder n plus grand - Oui.
priorité_queue<int, vecteur<int>, plus<int>> minRight; // min-heap
longue droite Somme = 0;
pour (int i = len - 1; i >= len - n; --i) {
minRight.push(nums[i]);
rightSum += nombres[i];
}
droite[len - n] = droiteSum;

pour (int i = len - n - 1; i >= n; --i) {
int cur = nombres[i];
si (cur > minRight.top()) {
rightSum += cur - minRight.top();
- MinRight.pop();
minRight.push(cur);
}
droite[i] = droiteSum;
}

// -------- Calculer la réponse - Oui.
long an = LLONG_MAX;
pour (int i = n - 1; i < len - n; ++i) {
ans = min(ans, gauche[i] - droit[i + 1]);
}
le retour des an;
}
};
«» "

---

- Oui. Billet de blog – Le bon, le mauvais et le mauvais

---

Description de la méta
> Apprenez à résoudre la différence minimale entre les montants après suppression d'éléments en Java, Python et C++. Comprendre l'algorithme, les pièges et les idées d'entrevue qui vous aideront à réussir votre prochaine entrevue de codage et à décrocher un emploi dans la technologie.

---

Article

# Le bon, le mauvais et le mauvais – Comment faire pour éponger LeetCode 2163 (et Land Your Dream Job)

> **Mots-clés**: *LeetCode 2163, Différence Minimale dans les Sommes Après Suppression d'Éléments, Solution Java, Python Priority file, C++ priority_queue, algorithme d'entretien, entretien de structures de données, conseils d'entretien d'emploi, stratégie d'entretien de codage, entretien d'ingénieur logiciel. *

---

Présentation

Quand les recruteurs demandent :**Qu'est-ce que votre problème le plus difficile de LeetCode** ?=, ils ne cherchent pas seulement une réponse correcte ; ils veulent voir **code propre, utilisation intelligente des structures de données, et une explication solide**.
Code du leet 2163 – *Différence minimale des montants après suppression d'éléments* – est un candidat de premier plan parce qu'il mélange la programmation **dynamique** avec les files d'attente **prioritaire**.
Dans ce post, nous allons marcher à travers le *bon* (efficace et élégant), le *mauvais* (cases de bord) et les aspects *ugly* (gymnastique d'index) du problème, puis présenter des solutions de référence dans **Java, Python et C++**.

---

Récapitulation des problèmes (en style d'entrevue)

> **Dépôt**
> *Vous avez un tableau de taille 3 × n. Supprimer exactement n éléments. Les 2n éléments restants sont divisés en une moitié gauche et droite. Retourner la valeur minimale possible de somme(gauche) – somme(droite). *

**Pourquoi est-ce intéressant? **
* Il s'agit d'une partition après avoir enlevé le puzzle – beaucoup de candidats le résolvent naïvement avec le dénombrement `O(n3)`, qui arrive.
* La solution optimale démontre la maîtrise de **heaps** ( files d'attente prioritaires) – un point de départ dans de nombreuses questions d'entrevue.

---

- Oui. Le Bon – Ce qui fonctionne

Qu'est-ce que ça signifie Pourquoi ça compte
- C'est quoi ?
**O(n log n) temps**=Chaque log des coûts d'exploitation du tas n, effectué 2 × n fois=== Échelles au maximum `n = 105'. Autres
Autres **Simple Structures de données**. Seulement deux files d'attente prioritaires + deux tableaux O(n). Autres
**Production déterministe**=Utilisez des sommes longues/64-bit pour éviter les débordements. Autres
**Cross-Language Cohérence**= Le même algorithme en Java, Python, C++=1 montre la pensée linguistique-agnostique – un plus dans les interviews de codage. Autres

---

- Oui. Les mauvaises – les choses C'est faux

1. ** Erreurs hors‐par‐un**
* Le point de coupe doit laisser au moins des éléments `n` de chaque côté (`i` de `n-1` à `3n-n-1`).
* Oublier cela conduit à "ArrayIndexOutOfBounds" ou de mauvais résultats.
2. **Gestion de la taille du talon* *
* Le remplacement de l'élément *le plus grand* dans un max-heap ou l'élément *le plus petit* dans un min-heap est facile en théorie mais facile à inverser dans la pratique.
* En Python, les nombres négatifs émulent un max-heap – une source commune de bogues.
3. **Dépassement**
* `sumFirst` et `sumSecond` peuvent atteindre chacun `n * 105` (-) 1010), qui s'inscrit dans 32 bits signé int seulement par la chance.
* Utilisez 64 bits pour les sommes intermédiaires.
4. ** Empreinte mémoire* *
* Stocker deux `O(3n)` les tableaux peuvent être négligés; à `n = 105`, il s'agit d'environ 2 × 3 × 105 × 8 octets 4 MB – toujours bien, mais mentionnez-le dans l'explication.

---

C'est pas vrai. Les horribles cas de bords cachés

Scénario Pourquoi c'est bizarre Comment réparer
- C'est quoi ?
L'algorithme fonctionne encore, mais il se sent trop facile et peut distraire de parties plus intéressantes de l'interview. Afficher le candidat peut adapter la solution pour ce cas dégénéré rapidement. Autres
** Nombres négatifs (pas dans les contraintes)**** Si les contraintes changent pour permettre les négatifs, la logique du tas se brise (par exemple, `n` peut être négatif). Autres Demandez à l'intervieweur s'il veut soutenir les négatifs; si oui, ajustez les comparaisons en conséquence. Autres
Autres **Grande taille d'entrée (n = 105)**= Récursion ou boucles naïfs peuvent frapper les limites de la pile ou les timeouts. Utilisez des boucles itératives et des tableaux pré-allotés; testez avec un grand cas aléatoire. Autres
**Cut non contigu**Le problème nécessite explicitement des moitiés contiguës, mais un candidat pourrait penser par erreur qu'il peut réorganiser le tableau. Clarifier l'exigence de « fractionnement en deux moitiés » au début de la conversation. Autres

---

## 6-

Question: Pourquoi ils s'interrogent Vos points de discussion
- C'est pas vrai.
* Expliquez l'algorithme et pourquoi les tas fonctionnent.*= Teste la compréhension de =sélectionnez le k le plus petit / le plus grand. Mentionnez qu'un max-heap garde le `k` plus petit et un min-heap garde le `k` plus grand. Autres
*Pouvez-vous réduire davantage la complexité du temps?* Vérifier si une solution O(n) ou O(n log n) est optimale. Afficher que `O(n)` est impossible car vous devez inspecter chaque élément au moins une fois, et `O(n log n)` est optimal avec des tas. Autres
*Qu'en est-il si les valeurs étaient supérieures à 32 bits?*= Test de manipulation du débordement. Souligner l'utilisation d'entiers 64 bits pour les sommes. Autres
*Pouvez-vous l'écrire dans une autre langue? Présentez les extraits de Java, Python, C++ et discutez de nuances spécifiques au langage. Autres

---

C'est pas vrai. Comment impressionner dans votre entrevue

1. ** Commencez par un plan clair* *
* J'utiliserai deux tas : un maximum pour le côté gauche et un minimum pour le côté droit. (en milliers de dollars)
* Écrivez le plan sur un tableau blanc avant de le coder.
2. **Exposer les monceaux**
* Le max-heap contient toujours les valeurs `n` les plus petites dans le préfixe. Si un nouvel élément est plus petit que le maximum, nous pop et poussons. (en milliers de dollars)
* Le talon minimal conserve les plus grandes valeurs de `n` dans le suffixe. (en milliers de dollars)
3. **Afficher la boucle de coupe* *
* Nous faisons glisser une fenêtre sur les points de coupe valides et calculons la différence en O(1) par étape. (en milliers de dollars)
4. **Analyse du temps et de l'espace**
* Temps d ' utilisation de l ' espace auxiliaire < < O > > . (en milliers de dollars)
5. **Délibérations**
* Nous utilisons `long` pour éviter les débordements. Si les valeurs peuvent être négatives, nous ajustons la logique de comparaison. (en milliers de dollars)
6. **Code propre**
* Gardez les noms de variables descriptifs (`leftSum`, `rightSum`, `cut`).
* Utiliser la pré-allocation ('vecteur<long> gauche(n*3)` en C++).

---

- Oui. A emporter

LeetCode 2163 n'est pas seulement un autre puzzle – c'est un ** showcase de pensée algorithmique**.
En maîtrisant le *bon* (taupes efficaces), en évitant le *mauvais* (hors-par-nous et débordement) et en naviguant sur le *ugly* (cas de pointe), vous démontrerez une compréhension profonde de la valeur des recruteurs.
Utilisez les solutions de référence de **Java, Python et C++** comme référence et pratique pour les expliquer à haute voix – c'est votre chemin le plus rapide vers le bouton .

---

Mot final

- *Code d'abord, explique plus tard. *
- *En cas de doute, posez des questions claires – cela vous montre que vous êtes réfléchi, pas négligent. *
- *La pratique d'écrire la même solution en trois langues – cela prouve la polyvalence. *

Bonne chance, et que le tas soit avec vous ! C'est ce qu'il a dit.

---

**Fin de l'article**

---

Note pour les recruteurs

Lors de l'examen d'une solution candidate au LeetCode 2163, concentrez-vous non seulement sur l'exactitude, mais aussi sur :

* ** Clarté algorithmique** – Est-ce qu'ils ont articulé la stratégie du tas?
* ** Gestion des contraintes** – Ont-ils utilisé des sommes de 64 bits?
* **Lisibilité du code** – Les noms de variables sont-ils descriptifs?
* **Cross-Language Proficiency** – ont-ils présenté des solutions Java, Python et C++?

Si un candidat vérifie tout ce qui précède, ils sont un candidat fort pour tout rôle d'ingénierie logiciel.