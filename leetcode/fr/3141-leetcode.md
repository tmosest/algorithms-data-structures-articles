---
titre: LeetCode 3141. Distances maximales de hamburgage -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3141 – Distances maximales de Hamming
* Python C++ – solution DP O(m · 2m)

> **SEO tags** – LeetCode 3141, Hamming maximal Distance, solution d'entretien Java, solution d'entretien Python, solution d'entretien C++, bitmask de programmation dynamique, entretien d'ingénierie logicielle, problème d'entretien de codage

---

- Oui. 1. Exposé des problèmes

> **Donné** d'un nombre entier (longueur *n*, 2 ≤ *n* ≤ 2 m) et d'un nombre entier `m` 1 ≤ *m* ≤ 17)
> **Retour** un tableau `réponse` de la même longueur où
> `answer[i] = max_{j=i} HammingDistance(nums[i], nums[j])`.

La distance de hamming entre deux entiers est le nombre de positions de bit à laquelle leurs représentations binaires diffèrent (les zéros de leader sont autorisés à tamponner les chaînes en bits *m*).

---

- Oui. 2. Les idées naïves et leurs pièges

L'approche Temps L'espace Commentaires
C'est pas vrai.
Brute force appairwise Distance de hamburging (en anglais seulement) O(n2 · m) (en anglais seulement) O(1)(en anglais seulement) n peut être de 2m (en anglais seulement) 131 072 → ~1010 comparaisons → impossible. Autres
Pré-calculer toutes les distances dans une matrice de 2m × 2m. Autres
BFS de chaque élément sur l'hyper-cube O(n · 2m) O(2m)= Fonctionne pour très petit *m*, mais encore trop lent pour *m*=17. Autres

Nous avons besoin d'un algorithme *linéaire* en termes de taille hyper-cube, c'est-à-dire O(m · 2m).

---

- Oui. 3. L'Insight – Propagate

Chaque entier *x* (0 ≤ *x* < 2m) peut être considéré comme un nœud dans un hyper-cube *m*-dimensionnel.
Deux nœuds sont voisins s'ils diffèrent en un seul morceau.

Laissez `dp[x]` soit la distance *maximum* de hamming de *x* à tout élément apparaissant dans "nums".
Si nous connaissons `dp[y]` pour un voisin `y = x ^ (1 << k)` (bit *k* flipped), nous pouvons mettre à jour `dp[x]`:

«» "
dp[x] = max( dp[x] , dp[y] + 1 )
«» "

Le `+1` vient de la différence supplémentaire entre `x` et `y`.
Faire cela une fois pour chaque bit est suffisant: après le premier pass `dp` connaît la distance à l'élément le plus proche dans le même moitié du cube; après le second passe il connaît la distance à l'élément le plus proche dans l'autre moitié, et ainsi de suite.
Après le traitement de tous les bits `m`, `dp[x]` contient la distance maximale à **any** élément dans `nums`.

L'algorithme est essentiellement une programmation dynamique multi-étapes (ou style « Fast Walsh–Hadamard transform ») sur l'hyper-cube.

---

- Oui. 4. Algorithme (code pseudo)

«» "
taille = 1 << m
dp = tableau de taille rempli de -INF
pour chaque v en chiffres:
dp[v] = 0 // la distance à elle-même est 0

pour bit de 0 à m-1:
prev = copie de l'instantané dp // avant ce niveau
pour x de 0 à la taille 1:
voisin = x ^ (1 < < bit)
dp[x] = max( dp[x], prev[voisin] + 1 )

réponse = [ dp[v] pour v en chiffres ]
réponse de retour
«» "

**Complexités* *

* Temps: "O(m · 2m)" – au maximum "17 · 131072 " 2,2 millions " opérations.
* Espace : `O(2m)` – le tableau DP plus un instantané.

Les deux sont assez rapides pour les contraintes.

---

- Oui. 5. Code

#### 5.1 Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
Int[] maxHammingDistances(int[] nums, int m) {
Taille de l'int = 1 << m; // 2^m
int[] dp = nouvelle int[size];
Arrays.fill(dp, Integer.MIN_VALUE / 2); // éviter le débordement

// cas de base: la distance à elle-même est 0
pour (int v : nombres) dp[v] = 0;

// DP sur bits
pour (int bit = 0; bit < m; bit++) {
int[] prev = dp.clone(); // instantané avant ce niveau
masque int = 1 << bit;
pour (int x = 0; x < taille; x++) {
voisin int = x ^ masque;
dp[x] = Math.max(dp[x], prev[voix] + 1);
}
}

// construire la réponse
int[] res = nouvelle int[nums.longueur];
pour (int i = 0; i < nombres.longueur; i++) res[i] = dp[nums[i]];
retour rés;
}

/* ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
Harnais d'essai rapide – ne fait pas partie de la soumission de LeetCode
*/
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(Arrays.toString(
s.maxHammingDistances(nouvelle int[]{9, 12, 9, 11}, 4)); // [2,3,2,3]
}
}
«» "

#### 5.2 Python (Python 3,11)

'`python
de taper l'importation Liste
importer des maths

Solution de classe:
def maxHamming Distances (self, nombres: List[int], m: int) -> Liste[int]:
taille = 1 << m
dp = [-math.inf] * taille

# case de base
pour v en chiffres:
dp[v] = 0

# PDD sur les bits
pour bit dans la plage(m):
prev = dp[:] # instantané
masque = 1 << bits
pour x dans la plage (dimension):
voisin = x ^ masque
val = prev[voix] + 1
si val > dp[x]:
dp[x] = valeur

retour [dp[v] pour v in nums]


# Démo rapide
si __nom__ == "__main__" :
s = Solution()
print(s.maxHammingDistances([9, 12, 9, 11], 4) # [2, 3, 2, 3]
«» "

### 5.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> maxHammingDistances(vecteur<int>& nums, int m) {
taille de l'int = 1 << m;
vector<int> dp(size, INT_MIN / 2); // éviter le débordement

// Cas de base
pour (int v : nombres) dp[v] = 0;

// DP sur bits
pour (int bit = 0; bit < m; ++ bit) {
vector<int> prev = dp; // instantané
masque int = 1 << bit;
pour (int x = 0; x < taille; ++x) {
voisin int = x ^ masque;
dp[x] = max(dp[x], prev[voix] + 1);
}
}

vecteur<int> rés;
res.reserve(nums.size());
pour (int v : nombres) res.push_back(dp[v]);
retour rés;
}
};
«» "

---

- Oui. 6. Bonne, mauvaise, mauvaise de la solution

Aspect du bien
- C'est quoi ?
**Complexité du temps** Aucun – l'algorithme est optimal pour les contraintes. Aucun.
Autres **Complexité de l'espace**. O(2m) – parfaitement acceptable pour *m* ≤ 17.
**Readability**= Effacer la boucle DP, utilise bitwise XOR pour retourner un peu. Il faut comprendre la propagation hyper-cube. La copie d'un snapshot (`prev = dp.clone()`) peut paraître lourde mais est triviale. Autres
**Cas d'esquive**=Poigne des duplicatas, des tableaux monobits, taille maximale. Aucun.
**Pièges potentiels**= Utiliser `Integer.MIN_VALUE/2` pour éviter les débordements lors de l'ajout 1.- Oublier de réinitialiser `dp[v] = 0` pour chaque occurrence d'un nombre. Aucun.

---

- Oui. 7. Pourquoi cela montre que vous êtes prêt pour une entrevue de codage

* **Pensée par les bits** – Les problèmes de LeetCode dépendent souvent de la manipulation de bits individuels; cette solution met en valeur cette compétence.
* ** Programmation dynamique sur les structures combinatoires** – La propagation de l'information à travers un hypercube est un modèle DP non trivial.
* ** compromis spatiaux** – La solution équilibre l'utilisation minimale de la mémoire avec le temps clair O(m · 2m).
* ** Polyvalence linguistique** – Nous avons fourni des implémentations idiomatiques Java, Python et C++, démontrant ainsi la capacité d'adaptation à toute pile utilisée par votre employeur.

Si vous pouvez expliquer l'algorithme, justifier son optimisation et écrire du code propre dans n'importe lequel de ces langages, vous êtes un candidat fort pour un rôle d'ingénierie logicielle senior.

---

- Oui. 8. Liste de contrôle finale avant la soumission

1. **Supprimer les blocs de démonstration `main` ou `__main__`** – LeetCode n'appellera que la méthode de classe.
2. **Éviter `-inf` en Java** – nous avons utilisé `Integer. MIN_VALUE / 2` pour la sécurité.
3. **Test avec tous les exemples fournis** – confirmer `[2,3,2,3]` et `[1,2,1,2]` travail.
4. **Soumettre** – copier la classe pertinente dans l'éditeur de LeetCodes et exécuter la suite de test.

Bonne chance ! C'est ce qu'il a dit