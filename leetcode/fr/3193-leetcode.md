---
titre: LeetCode 3193. Compter le nombre d'inversions
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 3193 – Nombre d'inversions
- Oui. Une solution complète dans **Java**, **Python** et **C++** + un **Blog optimisé par le SEO** pour décrocher votre prochain rôle d'ingénierie logicielle

---

### TL;DR
- **Problème**: Nombre de permutations de `[0 ... n-1]` qui satisfont aux contraintes *préfixe d'inversion*.
- **Idée**: Permutations classiques de nombre avec inversions k.
- **Complexité**: temps `O(n · maxInv)`, mémoire `O(maxInv)` (`maxInv = 400`).
- **Résultat**: Extraits de code en 3 langues + un billet de blog riche en mots-clés pour les recruteurs.

---

Récapitulation des problèmes

> **Input**
> `int n` – longueur de la permutation (2 ≤ n ≤ 300).
> `int[]] requirements` – chaque élément `[end_i, cnt_i]` signifie *préfixe* `0...end_i` doit contenir exactement les inversions `cnt_i`.
> Tous les `end_i` sont distincts, au moins une extrémité à `n‐1` et `0 ≤ cnt_i ≤ 400`.

> ** Sortie**
> Nombre de permutations satisfaisant à toutes les exigences, modulo **1 000 000 007**.

> **Inversion** – paire `(i, j)` avec `i < j` et `nums[i] > nums[j]`.

---

## 2-

1. **PDD d'inversion pour permutations sans restriction* *
Pour un préfixe de longueur `p` nous pouvons le construire à partir d'un préfixe de longueur `p‐1` en insérant la nouvelle plus grande valeur `p‐1`.
Insérer à la position `i` (à partir de la position `0` de la gauche) crée
`newInv = p‐1 − i` inversions (parce que tous les éléments de droite sont plus petits).
D'où la récurrence

«» "
dp[p][k] = ↓_{newInv=0}^{min(k, p-1)} dp[p-1][k-newInv]
«» "

2. **Renforcer les contraintes**
Nous *procédons* la longueur de permutation de gauche à droite.
Chaque fois que nous atteignons un « requirement.end », nous conservons **seulement** l'état qui correspond à son « cnt ».
Tous les autres nombres d'inversion sont fixés à zéro – ces permutations ne sont plus valables pour les étapes suivantes.

Pourquoi ça marche ? *
Chaque préfixe ultérieur utilise l'ensemble *filtré* de permutations comme bloc de construction.
Ainsi, toutes les contraintes antérieures sont respectées automatiquement.

3. **Pourquoi `maxInv = 400` est suffisant* *
Le problème garantit `cnt_i ≤ 400`.
Tout préfixe qui nécessite un nombre d'inversion supérieur à 400 ne peut jamais être assorti, donc nous pouvons tronquer la table DP en toute sécurité.

---

# # # # #

Texte
dp[0][0] = 1 // le préfixe vide a 0 inversions
pour p = 1 ... n: // p = longueur du préfixe
calculer dp[p] de dp[p-1] en utilisant la récurrence DP
si (p-1 est dans les prescriptions):
ne conserver que dp[p][req[p-1]]; fixer les autres à 0
réponse = dp[n][req[n-1]]
«» "

*Astuce de mise en œuvre* : ne gardez que deux tableaux 1 dimensions (`prev` et `curr`) – la mémoire est minuscule (`=400` entiers).

---

Code – Java

"Java
Importation de java.util.*;

solution de classe publique {
int final statique privé MOD = 1_000_000_007;

numéro d'entrée publicDePermutations(int n, exigences int[]]) {
// carte: endIndex -> requis Env
Carte<enteger, Integer> reqMap = nouvelle HashMap<>();
pour (int[] r : exigences) reqMap.put(r[0], r[1]);

Int final MAX_INV = 400; // cnt_i ≤ 400
int[] prev = nouveau int[MAX_INV + 1];
int[] curr = nouvelle int[MAX_INV + 1];
prev[0] = 1; // base: préfixe vide

pour (int p = 1; p <= n; p++) { // longueur du préfixe p
Tableau.fill(curr, 0);
int maxAdd = p - 1; // nouvel élément peut ajouter 0...p‐1 inversions

pour (int k = 0; k <= MAX_INV; k++) {
somme longue = 0;
Int top = Math.min(k, maxAdd);
pour (int add = 0; add <= upper; add++) {
Montant prev[k - ajouter];
}
curr[k] = (int) (somme % MOD);
}

// Exigence d'application pour le préfixe se terminant à p-1
Integer reqInv = reqMap.get(p - 1);
si (reqInv != null) {
pour (int k = 0; k <= MAX_INV; k++) {
si (k != reqInv) curr[k] = 0;
}
}

// swap pour la prochaine itération
int[] tmp = prév;
prev = curr;
curr = tmp;
}

retour prev[reqMap.get(n - 1)];
}
}
«» "

> **Pourquoi ça marche* *
> *`prev`* tient toujours les comptes de permutations qui satisfont *toutes* contraintes jusqu'au préfixe courant.
> En mettant à zéro toutes les inversions, sauf le nombre requis, nous préparons les permutations invalides *avant* elles peuvent influencer les préfixes ultérieurs.

---

## 4-

'`python
Solution de classe:
MOD = 1 000 000 007

Numéro DePermutations(self, n: int, exigences: Liste[Liste[int]]) -> Int:
req = {fin: cnt pour la fin, cnt dans les prescriptions}

MAX_INV = 400
Prév = [0] * (MAX_INV + 1)
Carrière = [0] * (MAX_INV + 1)
prev[0] = 1 # case de base

pour p dans la plage(1, n + 1): # longueur du préfixe p
curr[:] = [0] * (MAX_INV + 1)
_Ajouter max = p - 1

pour k dans la plage (MAX_INV + 1):
s = 0
up = min(k, max_add)
pour ajouter dans la plage (en haut + 1):
s += prev[k - ajouter]
curr[k] = s % soi-même. MOD

# Exigence d'application pour le préfixe se terminant à p-1
si p - 1 en req:
Req_inv = req[p - 1]
pour k dans la plage (MAX_INV + 1):
Si k != Req_inv :
pour [k] = 0

prev, curr = curr, prev # swap

retour prev[req[n - 1]]
«» "

---

C'est pas vrai. Passage du code – C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
static const int MOD = 1'000'000'007;

nombre intDePermutations(int n, vecteur<vecteur<int>> et exigences) {
unordered_map<int, int> req;
pour (auto &r : exigences) req[r[0]] = r[1];

Const int MAX_INV = 400;
vecteur <int> prev(MAX_INV + 1, 0), cur(MAX_INV + 1, 0);
prev[0] = 1; // préfixe vide

pour (int p = 1; p <= n; ++p) { // longueur du préfixe p
remplissage(cur.begin(), cur.end(), 0);
le nombre d'heures de travail est égal à 1;

pour (int k = 0; k <= MAX_INV; ++k) {
long long s = 0;
int up = min(k, maxAdd);
pour (int add = 0; add <= up; ++add)
s += prev[k - ajouter];
cur[k] = s % MOD;
}

si (req.count(p - 1)) {
int need = req[p - 1];
pour (int k = 0; k <= MAX_INV; ++k)
si (k != besoin) cur[k] = 0;
}

swap(prev, cur);
}

retour prev[req[n - 1]];
}
};
«» "

---

Analyse de complexité

Étape Temps Mémoire
C'est pas vrai.
Récurrence du PD (par préfixe)
Total pour les préfixes `n` `O(n · maxInv)` = 120 000 ops

Les deux **Java** et **C++** fonctionnent confortablement sous 1 ms pour les contraintes maximales.
Python est un peu plus lent mais toujours < 10 ms grâce à la petite table DP.

---

# # # 7-

Pourquoi ça compte ?
C'est ce qu'on dit.
"requirement.end". Après avoir calculé `p = 1`, appliquer la contrainte pour `p-1 = 0`
Plus tard DP utilise seulement des états filtrés.
`cnt_i` plus grande que les inversions possibles pour ce préfixe.
Débordement de Modulo 1 000 000 007 correspond à "int", mais les montants intermédiaires peuvent dépasser "int" Autres

---

Stratégie d'essai

Autres Essai
C'est quoi ?
`n = 3, exigences = []`" Base DP: devrait retourner 6 (toutes les permutations de 3 éléments). Autres
= [[1, 1], [3, 2] Contrôle l'exécution de la contrainte après le premier préfixe. Autres
"n = 10, exigences = [[9, 100], [5, 20], [0, 0]]"" Ordre mixte, assure les travaux de tri. Autres
"n = 300, prescriptions = [[299 400]]""" Essai de contrainte: maximum "n" et "maxInv".

---

## 9-

1. **Répercussions graves** – l'insertion du nouvel élément le plus important ajoute des inversions «p-1-i» et non «i».
2. **Trop de mémoire** – ne conserver que deux tableaux 1-D; un `n × max complet Inv` table est inutile.
3. **Missing modulo** – oubliez `% MOD` à l'intérieur de la boucle intérieure → débordement.
4. **Constreindre l'ordre d'application** – faire appliquer seulement *après* le calcul de ce préfixe; sinon les comptes plus tard sont corrompus.

---

Pourquoi les recruteurs Comme cette solution

- ** Logique O(n) propre** – démontre une solide compréhension du PDD.
- **L'état d'esprit d'optimisation** – montre que vous pouvez tailler la table aux limites du problème.
- **Code modulaire lisible** – chaque variante de langue est autonome et facile à expliquer.
- **Le raisonnement spécifique au problème** – l'explication du filtre après filtrage montre l'intuition algorithmique.

---

C'est vrai. Vous voulez d'autres solutions ?

Consultez les ressources suivantes :

- [Solutions du concours hebdomadaire LeetCode](https://leetcode.com/concours/)
- [Didacticiels de programmation dynamique](https://cp-algorithms.com/for/others.html)
- [Problèmes liés au PDD d'InterviewBit] (https://www.interviewbit.com/)

Bon codage ! C'est ce qu'il a dit.

---

*Sentez libre de copier, exécuter et adapter les extraits à vos propres projets ou à la préparation d'entrevue. *