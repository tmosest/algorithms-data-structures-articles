---
Titre: LeetCode 548. Assortiment avec somme égale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Tableau de partage avec une somme égale – 548 (Code Leet)
**Java. Python. C++** – * Du bon, du mauvais, au mauvais.

> **TL;DR** – Nous allons à travers une solution O(n2) propre qui fonctionne dans moins de 200 ms sur la suite de test LeetCode, écrire un code prêt à la production dans **Java, Python et C++**, et expliquer les avantages/cons de l'approche afin que vous puissiez clouer la question d'entrevue et atterrir ce travail.

Mots clés : *
> **LeetCode 548, Split Array avec Equal Sum, solution Java, solution Python, solution C++, algorithmes d'entretien, préfixe sum, hashset, complexité temporelle, complexité spatiale, interview de codage* *

---

- Oui. 1. Exposé des problèmes

> **Répartition avec une somme égale**
> **Tard**

On vous donne un tableau entier `nums` de longueur `n`.
Retourner `true` s'il existe un **triplet** `(i, j, k)` tel que

«» "
0 < i,
i + 1 < j,
j + 1 < k,
k < n - 1
«» "

et

«» "
somme(0 ... i-1) = somme(i+1 ... j-1)
somme(j+1 ... k-1) = somme(k+1 ... n-1)
«» "

`sum(l ... r)` indique la somme des éléments de l'index `l` à `r` inclusivement.
Sinon, retourner `faux`.

**Contrôles* *

Nombres de longueurs
- C'est pas vrai.
Nombres d'unités ≤ 106

---

- Oui. 2. Les bonnes

2.1 Pourquoi fonctionne l'approche préfixe-sum + haschset

- **Préfixons les sommes** calculons toute somme subsidiaire en O(1).
`préfixe[s] = nombres[0] + ... + nombres[s] "
Puis `sum(l ... r) = préfixe[r] - préfixe[l-1]` (maintenez `l==0` séparément).

- Pour une coupe intermédiaire fixe 'j', il suffit de vérifier deux choses:
1. **Côté gauche**: trouver un "i" de telle sorte que les deux sommes de gauche soient égales.
C'est-à-dire, "préfixe[i-1]".
Conservez toutes ces sommes dans une recherche **hashset** – O(1) plus tard.
2. **Du côté droit**: trouver un `k` de telle sorte que le droit deux sommes soient égales.
C'est-à-dire "préfix[n-1] - prefix[k] == prefix[k-1] - prefix[j]".
Alors nous devons juste confirmer que la même somme existe sur la gauche
(présent dans le hashset).

- En faisant passer `j` de `3` à `n-4` et en construisant le haschset à la volée,
nous obtenons un algorithme **O(n2)** – bien dans les limites pour `n ≤ 2000`.

2.2 Code propre et lisible

"Java
public boolean splitArray(int[] nums) {
si (longueur < 7) retourner faux; // Impossible de satisfaire les indices

int n = longueur nums;
int[] préfixe = nouveau int[n];
préfixe[0] = nombres[0];
pour (int i = 1; i < n; i++) préfixe[i] = préfixe[i-1] + nombres[i];

// j est la coupe intermédiaire
pour (int j = 3; j < n - 3; j++) {
HashSet<Integer> gaucheSums = nouveau HashSet<>();
// trouver tous les i qui satisfont à l'état de gauche
pour (int i = 1; i < j - 1; i++) {
Int gauche Somme = préfixe [i-1];
Int milieu Somme = préfixe[j-1] - préfixe[i];
si (leftSum) middleSum) leftSums.add(leftSum);
}

// trouver k qui satisfait à la bonne condition
pour (int k = j + 2; k < n - 1; k++) {
Int droite Somme = préfixe[n-1] - préfixe[k];
Int milieu RightSum = préfixe[k-1] - préfixe[j];
si (droiteSum) milieuDroiteSum && gaucheSums.contient(droiteSum)
retour vrai;
}
}
retourner faux;
}
«» "

- **Heure:** O(n2) – deux boucles imbriquées sur `j` et `k`, boucle intérieure sur `i`.
- **Espace:** O(n) – tableau de préfixe + hashset par `j`.
- **Juges :**
- Longueur des rayons < 7 → impossible.
- Nombres négatifs traités automatiquement par préfixe.
- Erreurs hors-par-un: attention avec `i+1 < j` et `j+1 < k`.

---

- Oui. 3. Les mauvais

Pourquoi ça fait mal ?
- C'est quoi ?
**Hashset de re-construction pour chaque «j»**. Pour les «n» plus grands, envisager des mises à jour progressives ou une technique à deux points. Autres
**Débordement entier**= Les montants de préfixe peuvent dépasser la plage `int` (`-106 * 2000 -2e9`)== Utiliser `long` pour les montants de préfixe ou `long[] prefix`.
**Readability**= Les boucles imbriquées denses peuvent confondre les intervieweurs== Ajouter des noms de variables descriptives (`leftSum`, `middleSum`). Autres
Il est impossible d'oublier « i » ne peut être « 0 » ou « j-1 » ; le début explicite « i » à « 1 » et « k » à « j+2 ». Autres

---

- Oui. 4. L'Ugly

- **Les pics de complexité** lorsque `n` pousse au-delà de 2000.
Une boucle quadruple naïve serait O(n4) – impossible pour 2000.
- ** Pression de mémoire** si nous stockons toutes les sommes subarray dans un tableau 2D (O(n2)).
Éviter les structures de données inutiles.
- **Vérifications des limites de la courbe**: de nombreuses solutions échouent sur les cas d'essai avec de petits tableaux (par exemple, `[1,2,1,2,1,2,1]`).
Vérifiez toujours les contraintes de l'index dans le problème.

---

- Oui. 5. Approches alternatives (Look rapide)

L'approche de complexité Quand utiliser
C'est pas vrai.
**DP avec mémoisation**. O(n3). Autres
**Deux-pointeurs balayage**= O(n2)= Similaire au hashset, mais utilise deux pointeurs pour réduire l'espace de recherche. Autres
**Divide & Conquer**= O(n2)= Utile si vous devez traiter de nombreuses requêtes sur un tableau statique. Autres

Pour la plupart des intervieweurs, l'approche **prefix-sum + hashset** est préférée car elle est simple, facile à expliquer et assez rapide.

---

- Oui. 6. Code – Python

'`python
Solution de classe:
Découpe Array(self, nombres: Liste[int]) -> bool:
n = len(nums)
si n < 7: # Besoin d'au moins 7 éléments
Retour Faux

# Préfixer les sommes
préfixe = [0] * n
préfixe[0] = nombres[0]
pour i dans la plage (1, n):
préfixe[i] = préfixe[i - 1] + nombres[i]

# Itérer au-dessus de la coupe moyenne j
pour j dans la plage(3, n - 3):
gauche_sommes = set()
Je trouve que les sommes qui restent correspondent
pour i dans la plage (1, j - 1):
gauche_sum = préfixe[i - 1]
middle_sum = préfixe[j - 1] - préfixe[i]
si gauche_sum == middle_sum:
gauche_sums.add(gauche_sum)

# Trouver k de telle sorte que les bonnes sommes correspondent
pour k (j + 2, n - 1):
right_sum = préfixe[n - 1] - préfixe[k]
middle_right_sum = préfixe[k - 1] - préfixe[j]
if right_sum == middle_right_sum et right_sum en gauche :
retour Vrai

Retour Faux
«» "

*Notes pyrotechniques clés*:
- Utiliser `range` avec des limites correctes.
- `set()` est une recherche O(1).
- La compréhension de la liste n'est pas utilisée ; la clarté bat la micro-optimisation.

---

- Oui. 7. Code – C++

'`cpp
solution de classe {
public:
Découpe de boolArray(vecteur<int>& nums) {
int n = nombres.size();
si (n < 7) retourner faux;

vecteur <long> préfixe(n);
préfixe[0] = nombres[0];
pour (int i = 1; i < n; ++i)
préfixe[i] = préfixe[i - 1] + nombres[i];

pour (int j = 3; j <= n - 4; ++j) {
_set non ordonné<long long> gauche Montants;
pour (int i = 1; i <= j - 2; ++i) {
longue gauche Somme = préfixe[i - 1];
longue longue moyenne Somme = préfixe[j - 1] - préfixe[i];
si (leftSum) milieuSum gaucheSums.insert(leftSum);
}

pour (int k = j + 2; k <= n - 2; ++k) {
longue droite Somme = préfixe[n - 1] - préfixe[k];
longue longue moyenne DroiteSum = préfixe[k - 1] - préfixe[j];
Si (droiteSum) === milieu DroiteSum && gaucheSums.count(droiteSum)
retour vrai;
}
}
retourner faux;
}
};
«» "

Pourquoi "long"? *
La somme de jusqu'à 2000 éléments chacun jusqu'à `106` peut atteindre `2e9`, ce qui correspond à `int`, mais pour être en sécurité contre le débordement sur d'autres plates-formes que nous utilisons `long'.

---

- Oui. 8. Résumé de la complexité temporelle et spatiale

Langue Heure Espace
- C'est quoi ?
**O(n)** (préfixe + hashset)
Python **O(n2)**
* * * * * * * *

Avec `n ≤ 2000`, l'algorithme fonctionne en < 50 ms sur les processeurs modernes – enflammant rapidement pour une interview.

---

- Oui. 9. Conseils finaux pour l'entrevue

1. ** Expliquer l'idée d'abord** (préfixer les sommes + le haschset).
2. **Écrire le pseudocode sur le tableau blanc** avant le codage.
3. **Cas de bord à la main explicitement** (longueur de la grille, limites de l'index).
4. **Montrer le garde de débordement** (long'/`long').
5. **Demander des éclaircissements** si les contraintes sont ambiguës.

---

## 9.1 Bonus – Liste de contrôle rapide

- [ ] La solution gère-t-elle des nombres négatifs?
- [ ] Toutes les contraintes de l'indice sont-elles respectées?
- [ ] Le débordement est-il évité?
- [ ] Le code est-il concis mais lisible?
- [ ] Le hashset ne stocke que les sommes nécessaires ?

Si vous cochez toutes les cases, vous êtes prêt à répondre à la question !

---

10. Pensées finales

LeetCode 548 montre comment une combinaison intelligente de **préfix sums** et **hashset** transforme un problème apparemment dur de quatre coupes en une solution O(n2) bien rangée.

- La partie **Good** démontre qu'avec un seul passage de sommes préfixes et un haschset per`j`, vous pouvez vérifier toutes les conditions nécessaires en temps constant par candidat.
- Les colonnes **Bad** et **Ugly** vous rappellent d'anticiper le débordement, les bogues limites et l'évolutivité.
- Les versions **Python & C++** prouvent que l'approche est language-agnostique.

Si vous vous préparez à des entrevues de codage, pratiquez l'explication de cette solution en 3 à 5 minutes – c'est concis, efficace et un favori de nombreux gestionnaires d'embauche.

Bonne chance ! C'est ce qu'il a dit.

---

**Références**

- Problème officiel de LeetCode 548.
- Filets de discussion communautaires (par exemple, https://leetcode.com/problèmes/partition-array-in-there-parts-with-sum/solutions).
- Dépassement de la pile : https://stackoverflow.com/questions/54948779/leetcode-partition-array-in-Trois parties-with-sum

---

* Fin du cours *