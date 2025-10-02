---
titre: LeetCode 3040. Nombre maximal d'opérations avec le même score II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3040 – **Nombre maximal d'opérations avec le même score II**
### Solutions complètes dans **Java**, **Python** et **C++**
### (Top-down DP, DFS + mémoisation, temps O(n2 · S))

---

- Oui. 1. Récapitulation du problème

Compte tenu d'un tableau "nums" (`1 ≤ nombres[i] ≤ 1 000`, `2 ≤ n ≤ 2 000`), un *opération* enlève une paire d'éléments qui **doivent** se résumer à la même valeur `S` à chaque étape:

* supprimer les deux premiers éléments `nums[l] + nums[l+1] "
* supprimer les deux derniers éléments `nums[r-1] + nums[r] "
* supprimer un élément de chaque fin `nums[l] + nums[r] "

La tâche consiste à trouver le nombre maximum d'opérations qui peuvent être effectuées tout en conservant la somme de paires `S` **constante**.

---

- Oui. 2. Pourquoi ce problème est une bonne question d'entrevue

* ** Contraintes claires** – un tableau de 2 k → facile à raisonner sur le temps/mémoire.
* **Shows maîtrise de la récursion et de la mémorisation** – de nombreux intervieweurs aiment encore cette approche.
* **Scales à `n = 2000`** – avec un cache intelligent il fonctionne confortablement en 2 s sur un juge typique.

---

- Oui. 3. L'algorithme de base

Le principal est que la somme cible `S` est choisie **une fois** (par la première opération) et ne change jamais.
Par conséquent, nous pouvons traiter chaque appel comme combien d'opérations pouvons-nous faire sur le subarray `[l,r]` avec la cible `S`?

«» "
dfs(l, r, S) =
Nombre maximal
// supprimer les deux premiers
(nums[l] + nombres[l+1] == S) ? 1 + dfs(l+2, r, S) : 0,

// supprimer les deux derniers
(nums[r-1] + nombres[r] == S) ? 1 + dfs(l, r-2, S) : 0,

// supprimer le premier + dernier
(nums[l] + nombres[r] == S) ? 1 + dfs(l+1, r-1, S) : 0
)
«» "

*Cas de base* – `l ≥ r` → `0`.

L'algorithme n'explore que les états accessibles à partir de chaque paire de départ possible, la mise en cache des résultats dans un dictionnaire clé par `(l, r, S)`.
Parce que `S ≤ 2000`, la clé peut être emballée dans un entier 64 bits, en maintenant la carte légère.

Complexité

Description de l'étape
- C'est quoi ?
**Sommes uniques**= `S` va de `2` à `2000` → au plus 2000 valeurs distinctes.
Chaque paire `(l,r)` est visitée une fois par `S`. Autres
Nous essayons toutes les sommes uniques ( "O(k · n2)" (8 · 109 cas le plus défavorable, mais dans la pratique beaucoup plus petit)
**Mémoire**=Cached states: 'O(k · n2)` entiers.=' ~ 32 Mo pour l'ensemble d'essai typique. Autres

---

- Oui. 4. Mise en œuvre des références

Ci-dessous vous trouverez trois solutions entièrement adaptées – Java, Python et C++ – qui compilent sur l'environnement officiel LeetCode.

> **Astuce** – Ajouter `import java.util.*;` en haut de votre fichier Java, et la même chose pour C++ (`#include <bits/stdc++.h>`).

---

### 4.1 Python 3 – `@lru_cache` DFS

'`python
#!/usr/bin/env python3
# 3040. Nombre maximal d'opérations ayant le même score II
# PDD du haut vers le bas avec mémoisation – O(n^2 · unique_sums)

importations
à partir de functools importer lru_cache
de taper l'importation Liste

Solution de classe:
def maxOperations(self, nombres: List[int]) -> Int:
n = len(nums)
uniq_sums = set()
pour i dans la plage (n - 1):
Uniq_sums.add(nums[i] + nombres[i + 1])
uniq_sums.add(nums[i] + nombres[n - 1])
uniq_sums.add(nums[0] + nombres[n - 1])

@lru_cache(maxsize=Aucune)
def dfs(l: int, r: int, S: int) -> Int:
si l >= r:
retour 0
meilleur = 0
# Les deux premiers
si l + 1 <= r et nombres[l] + nombres[l + 1]] S:
best = max(meilleur, 1 + dfs(l + 2, r, S))
Deux derniers
si l <= r - 1 et nombres[r - 1] + nombres[r] == S:
best = max(meilleur, 1 + dfs(l, r - 2, S))
# premier + dernier
si l < r et nombres[l] + nombres[r] == S:
best = max(meilleur, 1 + dfs(l + 1, r - 1, S))
le meilleur retour

réponse = 0
# Essayez chaque paire de départ possible
pour i dans la plage (n - 1):
# Les deux premiers
s = nombres[i] + nombres[i + 1]
réponse = max(réponse, 1 + dfs(i + 2, n - 1, s))
# premier + dernier
s = nombres[i] + nombres[n - 1]
réponse = max(réponse, 1 + dfs(i + 1, n - 2, s))
Deux derniers
s = nombres[n - 2] + nombres[n - 1]
réponse = max(réponse, 1 + dfs(i, n - 3, s))

réponse de retour
«» "

---

### 4.2 Java 17 – `HashMap<Long, entier>` mémoisation

"Java
Importation de java.util.*;

solution de classe publique {
les noms de la finale privée;
final privé n;
// Carte de mémorisation saisie par (l,r,S) emballée dans une longue
carte finale privée<Long, entier> mémo = nouveau HashMap<>();

int maxOpérations(int[] nombres) {
ce.n = longueur nums;
ce.nums = nombres;
réponse int = 0;

// Essayez toutes les paires de démarrage possibles pour fixer la somme cible S
pour (int i = 0; i < n - 1; i++) {
// les deux premiers
réponse = Math.max(réponse, 1 + dfs(i + 2, n - 1, nombres[i] + nombres[i + 1]);
// première + dernière
réponse = Math.max(réponse, 1 + dfs(i + 1, n - 2, nombres[i] + nombres[n - 1]);
// les deux derniers
réponse = Math.max(réponse, 1 + dfs(i, n - 3, nombres[n - 2] + nombres[n - 1]);
}
réponse de retour;
}

Int privé dfs(int l, int r, int S) {
si (l >= r) retourne 0;
clé longue = paquet(l, r, S);
Integer cached = mémo.get(key);
si (cached != null) retour en cache;

int best = 0;
// les deux premiers
si (l + 1 <= r && nums[l] + nums[l + 1] == S) {
best = Math.max(meilleur, 1 + dfs(l + 2, r, S));
}
// les deux derniers
si (l <= r - 1 && nombres[r - 1] + nombres[r] == S) {
best = Math.max(meilleur, 1 + dfs(l, r - 2, S));
}
// première + dernière
si (l < r && nums[l] + nums[r] == S) {
best = Math.max(meilleur, 1 + dfs(l + 1, r - 1, S);
}

mémo.put(clé, meilleur);
le meilleur retour;
}

pack privé long(int l, int r, int s) {
// l et r ont besoin de 11 bits chacun (0-2047), s a besoin de 11 bits.
retour ((long) l << 22)
}
}
«» "

---

### 4.3 C++17 – `unordered_map<long long, int>` mémoisation

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxOpérations(vecteur<int>& nums) {
n = nombres.size();
ce->nums = nombres;
réponse int = 0;
pour (int i = 0; i < n - 1; ++i) {
réponse = max(réponse, 1 + dfs(i + 2, n - 1, nombres[i] + nombres[i + 1]);
réponse = max(réponse, 1 + dfs(i + 1, n - 2, nombres[i] + nombres[n - 1]);
réponse = max(réponse, 1 + dfs(i, n - 3, nombres[n - 2] + nombres[n - 1]);
}
réponse de retour;
}

particulier:
vecteur<int> les numéros;
l'élément n;
unordered_map<long long, int> memory; // key = pack(l,r,S)

int dfs(int l, int r, int S) {
si (l >= r) retourne 0;
longue clé longue = pack(l, r, S);
auto it = mémo.find(key);
si (it != memo.end()) retourne->seconde;

int best = 0;
Si (l + 1 <= r && nums[l] + nums[l + 1] == S)
best = max(meilleur, 1 + dfs(l + 2, r, S);
Si (l <= r - 1 && nums[r - 1] + nums[r] == S)
best = max(meilleur, 1 + dfs(l, r - 2, S);
Si (l < r && nums[l] + nums[r] == S)
best = max(meilleur, 1 + dfs(l + 1, r - 1, S);

mémo[key] = meilleur;
le meilleur retour;
}

Boîte longue (int l, int r, int s) {
// l & r: 11 bits chacun, s: 11 bits
retour ((long long)l << 22)
}
};
«» "

---

- Oui. 5. L'Éclat – pourquoi vous devriez éviter certains pièges

Pièges Qu'est-ce qui s'est passé ?Comment réparer ?
- C'est quoi ?
**Recréer la carte de mémo pour chaque cible** Conservez **une** carte; la clé contient `S`. Autres
Une table ascendante fonctionnerait encore, mais les limites de récursion de Python le rendent fragile. Se tenir à la mémoire DFS + haut de page. Autres
**L'utilisation d'un « set » de toutes les valeurs possibles de « S »**Le set devient énorme (« O(n2) ») et est inutile. N'utilisez que les 2 k de sommes possibles ('''2000'). Autres
**Ne pas manipuler correctement le sous-barrage vide** -1... Explicite `si (l >= r) retourner 0;`

---

- Oui. 6. Réflexion finale

> **Si vous vous préparez à une entrevue de style LeetCode, ce problème est un *must-know*:* *
> * il teste la récursion, la mémorisation et l'art d'emballer un état en une seule clé;
> * la solution est compacte, efficace et facilement portable entre les langues.

Bonne chance pour le prochain défi de codage – vous aurez une réponse propre et prête à la production prête à tomber dans votre entrevue!