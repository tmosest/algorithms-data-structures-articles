---
titre: LeetCode 363. Somme maximale du rectangle Pas plus grand que K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Somme maximale du rectangle pas plus grand que K – LeetCode 363
*(Hard – 2-D Kadane + Préfixe-Sum + Recherche binaire)*

> **TL;DR** – La solution optimale compresse la matrice 2-D en un tableau 1-D pour chaque paire de lignes (ou colonnes).
> Pour chaque tableau compressé, nous trouvons la plus grande somme de sous-réseau ≤ k dans *O(n log n)* avec un `TreeSet` (Java) / `multiset` (C++) / `bisect` (Python).
> Durée: **O(min(m, n)2 · max(m, n) · log max(m, n))**, Mémoire: **O(max(m, n))**.

---

- Oui. 1. Récapitulation des problèmes

> **Input**
> `matrix`: `m × n` 2-D array (`1 ≤ m, n ≤ 100`, `-100 ≤ matrix[i][j] ≤ 100`)
> `k`: un entier (`-105 ≤ k ≤ 105`)

> **Objectif**
> Retourner la somme maximale de tout rectangle aligné sur l'axe à l'intérieur de la `matrice' dont la somme ne dépasse pas** "k".
> Un rectangle est défini par deux lignes et deux colonnes; sa somme est la somme de tous les éléments à l'intérieur.

> ** Garantie** – Il existe au moins un rectangle dont la somme ≤ k.

---

- Oui. 2. L'approche « Good » – 2-D Kadane + Préfixe Sum + Recherche binaire

1. **Compresser des lignes ou des colonnes* *
*Si la matrice a plus de colonnes que de lignes, itérer sur des paires de lignes; sinon itérer sur des paires de colonnes. *
La compression réduit le problème 2-D à un problème 1-D sur un tableau de longueur `max(m, n)`.

2. **1-D Problème de sous-audience* *
Pour le tableau compressé `nums` nous avons besoin de la plus grande somme de sous-tarifs ≤ k.
C'est un problème classique qui peut être résolu dans *O(n log n)*:
* Gardez un ensemble trié de montants de préfixe vus jusqu'à présent (`préfixe = 0` initialement).
* Marchez dans les "nums", en maintenant une somme courante "curr".
* Pour chaque `curr` nous avons besoin du plus petit préfixe `p` tel que `curr - p ≤ k` → `p ≥ curr - k`.
La recherche à la limite inférieure ( 'plafond') donne cette 'p'.
* Mettre à jour la meilleure réponse avec `curr - p`.
* Insérez `curr` dans le multiset.

3. **Arrêter tôt** – Si la meilleure réponse jamais atteint `k`, il est optimal; casser immédiatement.

La complexité totale de l'algorithme est dominée par la double boucle sur les paires de lignes/colonnes (-) min(m,n)2) et le *O(n log n)* routine 1-D, donnant

«» "
Durée : O(min(m, n)2 · max(m, n) · log max(m, n))
Mémoire : O(max(m, n))
«» "

Avec `m, n ≤ 100` cela va dans bien au-dessous de 1 ms en pratique.

---

- Oui. 3. Les mauvaises boucles naïves

Une force brute de manuel énumère tous les rectangles `(en haut, à gauche, en bas, à droite)` et les résume avec une table 2-D préfixe.
*Time*: `O(m2 · n2)` → jusqu'à 108 opérations pour 100 × 100, encore trop lent pour la limite de 2 s de LeetCode.
* Mémoire*: `O(m · n)` pour la table de préfixe 2-D.

---

- Oui. 4. L'Ugly – O(m2 · n2) sans montants préfixes

Récapitulez le rectangle à chaque fois, en recomptant la somme de zéro pour chaque rectangle.
C'est *O(m3 · n3)* et tout à fait impraticable.

---

- Oui. 5. Suivi – Lignes beaucoup plus grandes Plus que les colonnes

Si `m >> n` (tout, matrice maigre), l'algorithme fonctionne toujours – nous ne faisons que l'itérer sur les paires de colonnes au lieu des paires de lignes, en échangeant les rôles de `m` et `n`.
Dans la pratique, cela maintient le tableau 1-D interne aussi court que possible, donnant les meilleures performances.

---

- Oui. 6. Mise en œuvre du code

Voici des solutions propres et autonomes dans **Java, Python et C++**.
Tous les trois utilisent la même idée de cœur – des lignes compressées, une recherche binaire sur les sommes de préfixe, et une sortie anticipée lorsque nous touchons `k`.

> **Conseil pour les entrevues** – Mentionnez que l'observation clé est une dimension et résolvez le problème 1-D avec une BST. (en milliers de dollars)
> Parlez à travers le sous-programme *O(n log n)* et pourquoi le `TreeSet` / `multiset` est essentiel.

---

#### 6.1 Java

"Java
Importation de java.util.*;

solution de classe {
int public maxSumSubmatrix(int[][] matrice, int k) {
les lignes int = matrice.longueur, cols = matrice[0].longueur;
ligne booléenneMajor = lignes <= cols; // itérer sur la dimension plus petite
résultat int = Integer.MIN_VALUE;

si (rowMajor) { // compresser les lignes
int[] temp = nouveau int[cols];
pour (int top = 0; top < lignes; top++) {
Tableau.fill(temp, 0);
pour (int bas = haut; bas < lignes; bas++) {
pour (int c = 0; c < cols; c++) {
temp[c] += matrice[bottom][c];
}
résultat = Math.max(résultat, maxSubarrayNoMoreThanK(temp, k));
si (résultat == k) retourner k; // le mieux possible
}
}
} autres { // colonnes de compression
int[] temp = nouveau int[rows];
pour (int gauche = 0; gauche < cols; gauche++) {
Tableau.fill(temp, 0);
pour (int droite = gauche; droite < cols; droite++) {
pour (int r = 0; r < lignes; r++) {
temp[r] += matrice[r][droite];
}
résultat = Math.max(résultat, maxSubarrayNoMoreThanK(temp, k));
si (résultat == k) retourner k;
}
}
}
le résultat du retour;
}

/** routine 1‐D – plus grande somme de sous‐aires <= k dans O(n log n) */
Int privé maxSubarrayNoMoreThanK(int[] nums, int k) {
int best = Integer.MIN_VALUE;
pour les véhicules à moteur à allumage par compression
TreeSet<Integer> préfixe = nouveau TreeSet<>();
Préfixe.add(0);

pour (int x : nombres) {
Carrière += x;
// nous avons besoin du plus petit préfixe >= curr - k
Cible entière = préfix.plafond(curr - k);
si (cible != null) {
best = Math.max(best, curr - cible);
si (meilleur == k) retourner le mieux; // arrêt précoce
}
Préfix.add(curr);
}
le meilleur retour;
}
}
«» "

**Complexité** – *O(min(m,n)2 · max(m,n) · log max(m,n)* temps, *O(max(m,n)* mémoire.
Le `TreeSet` nous donne la recherche binaire dans *log n*.

---

6.2 Python

'`python
bisect d'importation
de taper l'importation Liste

Solution de classe:
def maxSumSubmatrix(self, matrix: List[List[int]], k: int) -> Int:
lignes, cols = len(matrix), len(matrix[0])
row_major = lignes <= cols
ans = -10**9

si ligne_major :
temps = [0] * cols
pour le haut de gamme(s) :
temps = [0] * cols
pour le bas dans la plage (haut, lignes):
pour c dans la plage(cols):
temp[c] += matrice[fond][c]
ans = max(ans, self._best_no_more_than_k(temp, k))
Si ans == k:
retour k
Autre: # colonnes de compression
temp = [0] * lignes
pour gauche (cols):
temp = [0] * lignes
pour droite (à gauche, cols):
pour r dans la plage (lignes):
temp[r] += matrice[r][droite]
ans = max(ans, self._best_no_more_than_k(temp, k))
Si ans == k:
retour k
retour et

def _best_no_more_than_k(self, nombres: List[int], k: int) -> Int:
préfixe = [0]
meilleurs = -10**9
Carrière = 0
pour x en nombres:
Carrière += x
# besoin plus petit p >= curr - k
idx = bisect.bisect_left (préfixe, curr - k)
si idx < len(préfixe):
best = max(meilleur, curr - préfixe[idx])
bisect.insort(préfixe, curr)
le meilleur retour
«» "

La version Python utilise `bisect.insort` pour garder la liste des préfixes triée – équivalente à un arbre de recherche binaire.

---

*### 6.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxSumSubmatrix(vecteur<vecteur<int>>& matrice, int k) {
int m = matrice.size(), n = matrice[0].size();
bool rowMajor = m <= n; // itérer sur plus petite dimension
int best = INT_MIN;

si (rowMajor) { // compresser les lignes
vecteur<int> température(n);
pour (int top = 0; top < m; ++top) {
remplir(temp.begin(), temp.end(), 0);
pour (int bas = haut; bas < m; + fond) {
pour (int c = 0; c < n; ++c) temp[c] += matrice[fond][c];
best = max(best, subarrayNoMoreThanK(temp, k));
si (meilleur) k) retourner k;
}
}
} autres { // colonnes de compression
vecteur<int> température(m);
pour (int gauche = 0; gauche < n; ++ gauche) {
remplir(temp.begin(), temp.end(), 0);
pour (int droite = gauche; droite < n; ++ droite) {
pour (int r = 0; r < m; ++r) temp[r] += matrice[r][droit];
best = max(best, subarrayNoMoreThanK(temp, k));
si (meilleur) k) retourner k;
}
}
}
le meilleur retour;
}

particulier:
int subarrayNoMoreThanK(vecteur const<int>& nums, int k) {
int curr = 0, mieux = INT_MIN;
multiset<int> pref{0};

pour (int x : nombres) {
Carrière += x;
auto it = pref.lower_bound(curr - k); // plus petit préfixe >= curr - k
si (it != pref.end())
best = max (meilleur, curr - *it);
pref.insert(curr);
}
le meilleur retour;
}
};
«» "

`multiset` donne le même comportement de recherche binaire que `TreeSet`.
Le retour précoce ('meilleur == k') maintient la solution à l'éclair.

---

- Oui. 7. Conseils d'entrevue et de recherche d'emploi

Question: Quoi mettre en avant
-- -- -- -- -- -- -- -- --
*Pourquoi comprimer une dimension?*= Réduit un problème 2-D à un problème 1-D – un aperçu clé qui réduit la complexité de 4-nested à 3-nested boucles. Autres
*Comment fonctionne la routine 1-D? *= Utiliser les montants préfixés + la TVB. Expliquez `curr - p ≤ k` → `p ≥ curr - k`. Afficher la recherche en moins. Autres
*Complexité du temps* ─ O(min(m,n)2 · max(m,n) · log max(m,n)» Pour 100 × 100 il s'agit d'environ 106 opérations, facilement dans les limites. Autres
*Space*="O(max(m,n)" pour le tableau compressé + BST. Autres
*Causes d'Edge*="Négatif `k`, toutes les valeurs matricielles négatives, matrices monolignes / monocolonnes, `k` égales au max global. Autres
*Suivez-nous*= Si les lignes >> colonnes, échangez des boucles. Autres
*Pourquoi cela est important pour les emplois* Idéal pour les entrevues techniques de niveau supérieur. Autres

---

- Oui. 8. Résumé du blog ami(e) SEO

- **Mots-clés**: LeetCode 363, Max Sum of Rectangle No Larger Than K, Hard LeetCode Problem, 2-D Kadane, Prefix Sums, TreeSet, multiset, recherche binaire, question d'entrevue, interview de codage, algorithme, entretien d'emploi, interview dev senior, C++, Java, solutions Python.
- **Description détaillée**: Code de Leet 363 – Somme maximale du rectangle Pas plus grand que K (Hard). Apprenez le préfixe 2-D Kadane + Solution Sum + BST en Java, Python et C++. Guide prêt à l'entrevue. (en milliers de dollars)

---

- Oui. 9. FAQ

C'est ce qu'il a dit.
-- -- -- -- -- --
Autres **Puis-je utiliser une carte de hachage au lieu d'ArbreSet?**= Une carte de hachage donne *O(n*) le temps moyen, mais elle ne peut pas effectuer la recherche de la limite inférieure requise pour `curr - p ≤ k`. Vous avez besoin d'une structure triée. Autres
Autres **Que faire si tous les nombres sont positifs?**.La routine 1-D fonctionne toujours; elle retourne simplement la plus grande sous-couche ≤ k (ou le tableau entier si sa somme ≤ k). Autres
**La solution est-elle optimale?**= Oui – la meilleure somme possible ≤ k ne peut pas dépasser `k`, et nous nous arrêtons dès que nous touchons `k`. Autres
Autres **Pouvons-nous utiliser une fenêtre coulissante à la place?**=La fenêtre coulissante ne fonctionne que lorsque tous les chiffres sont non-négatifs. Ici, nous avons des négatifs, donc nous devons utiliser l'approche de la BST. Autres

---

## 10. Dernier départ

Le problème 2-D Hard LeetCode 363 vous enseigne l'un des modèles les plus précieux pour le codage des interviews : **compresser une dimension, réduire à 1-D, puis résoudre avec un arbre équilibré**.
Il démontre :

- Compréhension profonde de l'algorithme de Kadanes et de son extension 2-D.
- Maîtrise des montants préfixés et de la recherche binaire dans un conteneur trié.
- Capacité de raisonner sur les compromis temps-espace et la résiliation anticipée.

La mise en œuvre de ce programme en Java, Python et C++ montre la compétence linguistique-agnostique – une vitrine parfaite pour un entretien technique de niveau supérieur.

> **Pro‐Tip** – Lors d'une entrevue, décrivez d'abord l'idée de haut niveau, puis plongez dans la routine 1‐D; l'intervieweur vous verra immédiatement comprendre l'astuce qui donne le temps optimal fixé.

Bon codage – et que votre recherche d'emploi soit aussi réussie que cette solution!