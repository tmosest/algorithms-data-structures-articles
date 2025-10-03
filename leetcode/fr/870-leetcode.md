---
titre: LeetCode 870. Avantage Shuffle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solutions de code pour **LeetCode 870 – Avantage Shuffle* *

Vous trouverez ci-dessous des implémentations propres et prêtes à la production dans **Java, Python et C++**.
Tous les trois utilisent la même idée gourmande (deux-pointeurs / tri + deux indices de stratégie) et fonctionnent dans **O(n log n)** temps avec **O(n)** espace supplémentaire.

---

### Java (Java 17+)

"Java
Importation de java.util.*;

solution de classe publique {
***
* Solution à deux pointes.
*
* @param nums1 tableau que nous allons mélanger
* @param nums2 tableau que nous comparons à
* @return une permutation de nums1 qui maximise l'avantage
*/
avantage public int[]Count(int[] nums1, int[] nums2) {
int n = nombres1.longueur;

Indices de tri des nombres2 dans l'ordre décroissant des nombres2[i]
Ordre entier[] = nouvel ordre entier[n];
pour (int i = 0; i < n; ++i) ordre[i] = i;
les tableaux.sort(ordre, a, b) -> Integer.compare(nums2[b], nums2[a]);

Trier les nombres1 de plus en plus
Tableaux.sort(nums1);

// 3.
réponse int[] = nouvelle réponse int[n];
int low = 0; // plus petit élément non utilisé dans les nombres1
Int high = n - 1; // plus grand élément non utilisé dans les nombres1

pour (int idx : ordre) {
si (nombres1[élevé] > nombres2[idx]) {
réponse[idx] = nombres1[élevé];
haute--; // utiliser le plus grand nombre qui bat nums2[idx]
} autre {
réponse[idx] = nombres1[faible];
bas++; // sacrifier le plus petit nombre
}
}
réponse de retour;
}

/* ------------------------------------------------- *
* Démo rapide (facultatif, supprimer en production) *
* */
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
int[] nums1 = {2, 7, 11, 15};
int[] nums2 = {1, 10, 4, 11};
Système.out.println(Arrays.toString(s.avantageCount(nums1, nums2));
}
}
«» "

---

### Python 3.11+

'`python
de taper l'importation Liste
bisect d'importation
à partir de collections import deque

Solution de classe:
déf avantage Compte(s), nombres1: Liste[int], nombres2: Liste[int] -> Liste[int]:
"""
Solution à deux pointeurs. Complexité: O(n log n).
"""
n = len(nums1)

N° 1 Indices de tri des nombres2 par ordre décroissant des nombres2[i]
ordre = trié(range(n), clé=lambda i: nombres2[i], inverse=True)

N° 2 Copie triée des nombres1
a = deque(sorted(nums1)) # deque permet O(1) pop des deux extrémités

N° 3 Construire la réponse
ans = [0] * n
pour idx dans l'ordre:
si a[-1] > nums2[idx]:
ans[idx] = a.pop() # utiliser le plus grand qui peut gagner
Sinon:
ans[idx] = a.popleft() # sacrifice le plus petit

retour et

♪ Démo optionnelle
si __nom__ == "__main__" :
s = Solution()
print(s.avantageCount([2,7,11,15], [1,10,4,11])
«» "

---

C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<int> avantageCount(vecteur<int>& nums1, vecteur<int>& nums2) {
int n = nombres1.size();

Classer les indices de nombres2 par valeur descendante
vecteur<int> ordre(n);
iota(order.begin(), order.end(), 0); // remplir de 0,1,2,...
tri(order.begin(), order.end(),
[&](int a, int b){ retour nums2[a] > nums2[b]; });

Trier les nombres1 de plus en plus
tri(nums1.begin(), nums1.end());

L'attribution des deux points
vecteur <int> ans(n);
Int low = 0, high = n - 1;
pour (int idx : ordre) {
si (nombres1[élevé] > nombres2[idx]) {
ans[idx] = nombres1[élevé];
--haut;
} autre {
ans[idx] = nombres1[faible];
++faible;
}
}
le retour des an;
}
};

/* Démo optionnelle ---------------------------------
Int main() {
Solution s;
vecteur<int> a = {2,7,11,15};
vecteur<int> b = {1,10,4,11};
auto res = s.avantageCount(a,b);
pour (int x: res) cout << x << ' ';
Cout << '\n';
}
*/
«» "

---

> **Pourquoi la même logique fonctionne partout* *
> * *Les deux * `nums1` et les indices triés de `nums2`= sont traités du côté le plus dur au côté le plus facile à battre.
> Chaque fois que le plus grand `nums1` actuel peut battre la valeur `nums2` actuelle, nous le plaçons là; sinon nous rejetons le plus petit nombre restant.
> Il s'agit exactement de la stratégie classique **-Greedy + deux pointeurs** pour maximiser les gains.

---

- Oui. 2. Article de blog: *Le bon, le mauvais, et le mauvais problème de l'avantage Shuffle*

> *Optimisé pour le référencement – LeetCode Avantage Shuffle

---

Introduction

**LeetCode 870 – Avantage Shuffle** est un problème d'aménagement de réseau qui est étonnamment courant dans les entrevues d'ingénierie logicielle.
Il teste votre capacité de penser en termes d'optimisation **greedy**, **tricks de tri**, et **techniques à deux points**.

Cet article passe en revue les parties du problème *good*, *bad* et *ugly*, compare trois solutions prêtes à la production, et vous donne des informations prêtes à l'entrevue qui peuvent stimuler votre CV et CV-search classements.

---

#### 2-

> Compte tenu de deux tableaux entiers `nums1` et `nums2` de la même longueur `n`, retourner une *permutation* de `nums1` qui **maximise** le nombre d'indices `i` pour lesquels `nums1[i] > nums2[i]`.
> En d'autres termes, nous voulons que le plus grand nombre possible de "wins" lorsque nous "battons" les deux tableaux élément-par-élément.

---

C'est vrai. Points de vue clés – Pourquoi Greedy fonctionne

1. **Trier donne l'ordre**
Si nous trions les deux tableaux, la dureté relative de chaque élément `nums2` devient claire : les plus grandes valeurs `nums2` sont plus difficiles à battre.

2. **Mettre le plus fort contre le plus fort gagnant* *
Le plus grand nombre de "nums1` gagnera contre les "nums2" qu'il peut battre.
C'est la seule fois qu'il peut gagner – sinon nous perdrons à tous les "nums2" restants.

3. **Sacrifice le plus faible quand inévitable**
Si un élément `nums2` est trop grand pour tout autre `nums1`, le mieux que nous pouvons faire est de gaspiller le nombre *le plus petit* disponible sur ce point.
Cela permet de conserver un plus grand nombre de possibilités.

Parce que chaque élément `nums1` est utilisé exactement une fois et que nous prenons toujours une décision localement optimale, la stratégie globale est globalement optimale – une preuve classique **greedy par échange argument**.

---

####=4="Grédy Algorithme (Deux-Pointeurs)

Étape Action Pourquoi
C'est quoi ?
Classer les indices de "nums2" **de manière décroissante**
Classer `nums1` **De plus en plus**
Utiliser deux pointeurs (« faible », « élevé »)

**Code Pseudo* *

«» "
ordre = indices de nombres2 triés par nombres décroissants2[i]
Tri(nombres1)
faible = 0
élevé = n- 1
pour idx dans l'ordre:
si nombres1[élevé] > nombres2[idx]:
réponse[idx] = nombres1[élevé]
haute...
Sinon:
réponse[idx] = nombres1[faible]
faible++
réponse de retour
«» "

---

C'est vrai. Implémentations linguistiques spécifiques

Histoire Autres
C'est pas vrai.
**Java**Utilisez `Integer[]` pour le tri de l'indice (comparateur Lambda). `int[]` trié avec `Arrays.sort()`. `Deque` alternative pourrait être utilisé mais `int[]` + pointeurs le garde léger. Autres
**Python**"deque(sorted(nums1)" fournit O(1) pop des deux extrémités. Le tri des indices utilise une fonction clé; « trié » est stable et rapide. Autres
Pour les données, `std::deque` ou `std::vector<int>` pour la copie triée. `std:sort` est utilisé deux fois, et deux indices `bas`/`haut` implémentent l'avidité. Autres

Les trois solutions partagent le même coût asymptotique :
**Time** – `O(n log n)` (dominé par les deux sortes).
**Espace** – `O(n)` (réseau de réponses + vecteur d'index auxiliaire).

---

- Oui. Bien, mal et mal

Aspect du bien
- C'est quoi ?
Autres **Bon – Idée intuitive**
Autres **Bon – Performance**Le tri domine, mais `O(n log n)` est optimal.
Autres **Certains langages (par exemple Java) ont besoin de deux appels `Arrays.sort()`, légèrement plus lourds sur CPU mais inévitables. Éviter le tri rendrait le problème difficile NP.
Autres **Bad – Edge Cases**.Tous les nombres sont égaux, ou `nums1` est tous plus petit que `nums2` – nous avons encore besoin de les gérer avec grâce (le chemin de Sacrifice).
Autres **Ugly – Détails de la mise en œuvre**= En Java, vous devez convertir `int[]` en `Integer[]` pour le tri de l'index – une subtilité qui peut briser les débutants.
Autres La version Java utilise un `Intéger[]` (boîte de frais généraux) – un prix *tiny* pour la clarté.
Autres **Ugly – Pièges d'entrevue**=Certains candidats sur-optimisent avec une recherche multiset ou binaire et finissent avec le code O(n2).

> **Ligne de bottom:** L'avidité à deux points est l'endroit doux : *rapide*, *simple* et *fortement buggy*.

---

D'autres approches et pourquoi Ils sont plus lents

L'approche de la complexité Pourquoi il est moins attrayant
- C'est quoi ?
**Multi-set / `std::multi-set`**" `O(n log n)` pour les insertions + `O(n log n)` pour les suppressions (ensemble `O(n log n)`)" Facteurs log supplémentaires, plus de code, moins de cache-friendly. Autres
Autres **Recherche binaire + `vector`**="O(n log n)` (chaque pop coûte `O(n)` en raison d'un déplacement) Autres
**DP / BFS (Séquence Reconstruction)**= Irresponsable pour ce problème== L'extrait d'utilisateur était pour un problème différent. Autres

---

Conseils d'entrevue

1. **Énoncer clairement la stratégie** – .Sort `nums1`, trier les indices de `nums2`, puis utiliser deux pointeurs pour attribuer des victoires ou des sacrifices. (en milliers de dollars)
2. **Mention la preuve de l'échange** – Si un grand nombre peut battre un `nums2` courant, il est optimal de l'utiliser maintenant; sinon nous sacrifions le plus petit. (en milliers de dollars)
3. **Complexité** – Afficher le temps `O(n log n)`, l'espace `O(n)`.
4. **Cas d'Edge** – Tous égaux, tous plus petits, tous plus grands.
5. **Tester la solution** – Fournir l'exemple de l'énoncé du problème; en option, afficher un test unitaire.

---

#### #= 9== SEO Boost

- ** Mots-clés principaux**: *LeetCode Advantage Shuffle*, *Advantage Shuffle Java*, *Advantage Shuffle Python*, *Advantage Shuffle C++*, *greedy algorithm interview*, *software ingénierie interview problems*
- ** Mots-clés secondaires** : * technique à deux points*, *sort + deux indices*, *algorithmes d'entretien d'emploi*, *conseils d'entretien de codage*, *meilleures solutions de LeetCode*

En tissant ces phrases naturellement dans l'article, votre billet de blog sera classé plus haut pour les recruteurs et les entraîneurs d'entrevues à la recherche de solutions haut de gamme à ce problème populaire.

---

Clôture

**Avantage Shuffle** peut ressembler à une simple question de tableau d'arrangement, mais la maîtriser démontre que vous pouvez:

- Transformer un défi combinatoire en une stratégie gourmande
- Ecrivez des solutions *cross-language* qui partagent le même squelette logique
- Évitez les pièges communs qui ralentissent le code dans les paramètres de production ou d'entrevue

Utilisez les extraits de code ci-dessus comme référence *prête à copier*.
Ajoutez quelques tests d'unité personnalisés, peut-être en visualisant le processus d'assignation, et vous avez un **killer CV add‐on**.

Bon codage – et peut-être que tous vos «wins» dépassent vos concurrents dans la prochaine interview!

---

> *Auteur: [Votre nom]* – *Algorithme Enthousiast.

---

**Bon entretien!**

---

> **P.S.** Si vous avez aimé ce guide, abonnez-vous pour en savoir plus *LeetCode de plongée profonde*, * solutions linguistiques spécifiques* et *stratégies d'entrevue de démarrage*.