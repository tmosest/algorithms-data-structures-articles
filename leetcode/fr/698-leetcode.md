---
Titre: LeetCode 698. Partition à K Sous-ensembles de somme égale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 698. Partition à K Sous-ensembles de somme égale – Un guide complet et prêt à l'emploi
> ** Mots clés:** LeetCode 698, Partition à K Equal Sum Subsets, solution Java, solution Python, solution C++, backtracking, bitmask DP, algorithme d'entretien, entretien d'emploi, défi de codage

---

Table des matières

Ce que vous apprendrez
- Oui.
Le défi, les contraintes, et pourquoi il importe
L'Algorithme La stratégie de retour
Code Walk‐through-de-Java, Python, implémentations C++ Autres
Les parties de l'Edge-cases & Pièges communs
Temps, espace et optimisation
Comment discuter de ce problème dans une interview réelle
Lire la suite Ressources et problèmes connexes

---

- Oui. 1. Aperçu du problème

> **LeetCode 698 – Partition à K Sous-ensembles de somme égaux**
> **Difficulté:** Moyenne
> **Input:** `int[] nums`, `int k`
> **Objectif:** Retour `true` si `nums` peut être divisé en sous-ensembles **k** non vides, chaque somme à la valeur **same**.

**Pourquoi est-ce important? **
- Oui. Il teste *backtracking* + *trongue* – un sujet d'interview classique.
- Oui. Cela vous oblige à penser à *la terminaison précoce*, *la compression de l'état* et *le tri* des tours.
- Résoudre la présentation vous pouvez gérer la recherche combinatoire avec des contraintes.

---

- Oui. 2. Insight algorithmique – L'approche « Good »

2.1 Principales observations

1. **Divisibilité du Sommet** – Si la somme totale `S` n'est pas divisible par `k`, impossible → sortie anticipée.
2. **Element Upper Bound** – Tout numéro unique ne peut pas dépasser la somme du sous-ensemble cible `S/k`.
3. **Sorting** – Tri descendant nous permet de placer de grands nombres en premier, coupant les branches tôt.
4. **Backtracking with Buckets** – Essayez récursivement de remplir chaque seau, backtrack quand un chemin échoue.

2.2 Retraçage du Pseudocode

«» "
cible = S/k
Tri(nombres, décroissants)

Dfs(i, seaux):
i == nombres.longueur: // tous les nombres placés
retour vrai
pour chaque seau j:
si seaux[j] + nums[i] <= cible:
les seaux[j] += nums[i]
si dfs(i + 1, seaux): retourner true
les seaux[j] -= nums[i]
si seaux[j] == 0: // taille: seaux vides, pas besoin d'essayer d'autres seaux vides
pause
retourner faux
«» "

**Pourquoi est-ce rapide? **
- Sorties précoces de branches insatisfaites.
- Une fois qu'un seau est vide, nous n'essayons pas d'autres seaux vides – élimination de la symétrie.
- Tri assure que nous échouons tôt quand un grand nombre ne peut pas s'adapter.

2.3 Bitmask DP – La solution de rechange

Lorsque `nums.longueur <= 16` (selon les contraintes), nous pouvons utiliser bitmask DP pour représenter les éléments utilisés:

«» "
dp[mask] = somme du seau actuel (mod cible)
«» "

Transition en ajoutant un élément inutilisé au seau actuel.
Complexité: "O(k * 2^n)" – toujours acceptable pour `n <= 16`.

On s'en tient à la solution de retour dans le code car elle est plus facile à lire et assez rapide pour LeetCode.

---

- Oui. 3. Passage du code

### 3.1 Java – 1 ms, 97 % plus rapide (comme la solution de référence)

"Java
Importer java.util. Les tableaux;

solution de classe publique {
boîte de booléen publiquePartitionKSubsets(int[] nums, int k) {
// Contrôles de base de la santé mentale
= 0;
pour (int x : nombres) la somme += x;
si (somme % k != 0=== nombres.longueur < k) retourner faux;
int cible = somme / k;

// Tri descendant pour la taille
Tableaux.sort(nums);
int n = longueur nums;
// Déplacer le plus grand vers l'avant (ordre inverse)
pour (int i = 0; i < n / 2; i++) {
int tmp = nombres[i];
nombres[i] = nombres[n - 1 - i];
nombres[n - 1 - i] = tmp;
}

int[] seau = nouveau int[k];
retour dfs(nums, 0, cible, seau);
}

booléen privé dfs(int[] nums, int idx, int cible, int seau) {
si (idx) nums.longueur) retourne true; // tous les nombres placés

Int val = nombres[idx];
pour (int i = 0; i < longueur du seau; i++) {
si (bucket[i] + val <= cible) {
seau[i] += valeur;
si (dfs(nums, idx + 1, cible, seau)) retourne vrai;
seau[i] -= val; // retour
}
si (bucket[i]] 0) pause; // éviter le travail en double
}
retourner faux;
}
}
«» "

** Faits saillants* *
- Tri effectué en place – O(n log n).
- Le "si (bucket[i]]] 0) rupture; ' ligne est la taille *symétrie*.

### 3.2 Python – Simple et lisible

'`python
de taper l'importation Liste

Solution de classe:
def canPartition KSubsets(self, nombres: List[int], k: int) -> C'est vrai.
total = somme(s)
si total % k != 0 ou len(nums) < k:
Retour Faux
cible = total // k
nums.sort(reverse=True)

seau = [0] * k

def dfs(i: int) -> C'est vrai.
Si i == len(nums):
retour Vrai
val = nombres[i]
pour j dans la plage(k):
si seau[j] + valeur <= cible:
Seau[j] += valeur
si dfs(i + 1):
retour Vrai
Seau[j] -= Val
si seau[j]] 0:
pause
Retour Faux

retour dfs(0)
«» "

### 3.3 C++ – Rapide et moderne

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
bool canPartitionKSubsets(vecteur<int>& nums, int k) {
somme int = accumuler(nums.begin(), nums.end(), 0);
si (somme % k.size() < k) retourne false;
int cible = somme / k;
tri(nums.rbegin(), nums.rend()); // descendant
vecteur<int> seau(k, 0);

fonction<bool(int)> dfs = [&](int idx) {
si (idx) nums.size() retourne true;
Int val = nombres[idx];
pour (int i = 0; i < k; ++i) {
si (bucket[i] + val <= cible) {
seau[i] += valeur;
si (dfs(idx + 1)) retourne vrai;
seau[i] -= valeur;
}
si (bucket[i]] 0) rupture; // élagage symétrique
}
retourner faux;
};

retour dfs(0);
}
};
«» "

---

- Oui. 4. Cas de bordures et pièges communs – Les «Bad» et les «Ugly»

Pourquoi il échoue
- C'est quoi ?
**Vérification de la divisibilité de l'escroquerie** Ajouter un retour anticipé
**Élément d ' ignorance > un élément plus grand que `cible` → impossible.
**Utilisation de BFS/DP sans taille**
**Recommander les seaux**
Autres **Caisse de base erronée** Autres
**Utilisation de la profondeur de récursion > Débordement de la pile pour 16 numéros
**Ne pas manipuler `nums.longueur= k`**=1 Doit retourner `true` si tous les nombres sont égaux à la cible=1 Vérification de la divisibilité + gestion logique du seau=1

---

- Oui. 5. Performance et complexité

Complexité
C'est pas vrai.
Dans le pire des cas (retraçage). Avec la taille, il est beaucoup plus bas. Pour `n <= 16`, acceptable. Autres
**L'espace**=O(k + n)=– pile de récursion + tableau de godets. Autres
**Optimisations** - Tri descendant. <br>- Prune au premier seau vide. <br>- Arrêtez lorsque tous les seaux sont remplis tôt. Autres

---

- Oui. 6. Conseils d'entrevue

1. **Expliquer les vérifications anticipées** – «somme % k» et «max(nums) > cible».
2. **Parler du tri** – Pourquoi la descente aide à pruner.
3. **Afficher l'état de taille** ('bucket[j] == 0').
4. **Complexité des peines** – retour sur le pire des cas par rapport aux performances typiques.
5. **Si vous avez des questions sur bitmask DP**, soyez prêt à expliquer la compression d'état.
6. ** Démontrer la compréhension des contraintes** – `n <= 16` → PDD faisable.

---

- Oui. 7. Lecture supplémentaire

- [LeetCode 698 – Discussion](https://leetcode.com/problèmes/partition-to-k-equal-sum-subsets/)
- [Retour à la taille – GeeksforGeeks] (https://www.geeksforgeeks.org/backtracking/)
(https://medium.com/@shikshanshihari/bitmask-dp-6b7b8e9d2c1a)
- Problème connexe : **"Sous-ensembles de la taille K"** – explorer la génération combinatoire.

---

- Oui. 8. Enveloppage

- **Bon**: La solution de retour est propre, rapide, et passe tous les tests LeetCode.
- **Bad**: Oublier les conditions de sortie anticipée peut vous faire TLE ou WA.
- **Ugly**: Symmetry duplicate gaspille du temps – pruner agressivement.

La maîtrise de ce problème montre que vous pouvez concevoir des solutions récursives efficaces, gérer l'état et penser aux optimisations algorithmiques – toutes les compétences clés pour les intervieweurs de haute technologie.

> **À emporter :** Codez-le, testez les exemples de cas et soyez prêt à expliquer votre processus de pensée. Bonne chance pour la prochaine interview ! C'est ce qu'il a dit.

---