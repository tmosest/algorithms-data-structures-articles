---
titre: LeetCode 1799. Maximiser le score après les opérations N -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 1799 – ** Maximiser la note après les opérations N**
**Tranquille DP + Bitmask

---

TL;DR

> **Objectif** – coupler tous les nombres `2n` de sorte que la somme pondérée
> \[
> \sum_{i=1}^{n} i \times \gcd(x_i, y_i)
> \]
> est optimisé.
> **Solution** – *exponentielle* bit-mask DP :
> * précalculer toutes les paires \(\gcd\),
> * traverser tous les masques (2n possibilités),
> * ajouter avec cupidité une nouvelle paire si elle ne chevauche pas le masque actuel.

L'algorithme fonctionne dans le temps **O(2n · n2)** (7 · 13 000 opérations) et la mémoire **O(2n)** – bien dans les limites du LeetCode.

---

Défaillance du problème

Point clé Détail
C'est quoi ?
**Longueur de l ' image**
**Exploitation**=Choisir deux numéros non utilisés `x` et `y`, marquer `i * gcd(x, y)` (l'indice d'exploitation commence à 1)=
**Objectif**= Maximiser le score total après exactement les opérations `n` (tous les nombres utilisés)=
**Constraints**= 1 ≤ nums[i] ≤ 106 – s'insère dans l'int de 32 bits

Parce que le tableau est petit, explorer tous les couplages possibles est possible en utilisant un bitmask.

---

Algorithme – Programmation dynamique Bitmask

1. **Précalculer toutes les paires possibles**
Pour chaque paire «(i, j)» (indices basés sur 0)
*bitmask* `1<<i=1<<j` → `gcd(nums[i], nums[j]'.
Nous en aurons besoin pour chaque transition PDD.

2. **Pad array** – `dp[mask]` est le meilleur score possible après avoir utilisé exactement les nombres indiqués par `mask`.
* `masque` a `2n` bits.
* Base: `dp[0] = 0`.
* Transition :
* `k` = bitmask d'une paire.
* Si `k & masque == 0' (aucun des numéros de la paire n'est encore utilisé)
Texte
nouveaux Masque = masque
operationIndex = bitCount(masque) / 2 + 1 // parce que chaque opération consomme 2 nombres
dp[newMask] = max(dp[newMask], dp[mask] + opérationIndex * gcdPair[k])
«» "

3. **Résultat** – 'dp[(1 << (2n)) - 1] ' (tous les numéros utilisés).

Complexité

Valeur métrique
C'est pas vrai.
**Temps**="O(2n · n2)" – au plus `214 · 142 =" 3,3 × 106 ="
** Mémoire** – environ 16 k entiers pour `n = 7`

Les deux sont minuscules pour les processeurs modernes.

---

Mise en œuvre du code

> Toutes les implémentations partagent la même logique ; seule la syntaxe diffère.

### Java (LeetCode Style)

"Java
Importation de java.util.*;

solution de classe {
Int public maxScore(int[] nums) {
int m = longueur nominale; // 2n
dans maxMask = 1 << m;
int[] dp = nouveau int[maxMask]; // dp[mask] = meilleur score

// précalcul gcd pour chaque paire
int[][] paire = nouvelle int[m][m];
pour (int i = 0; i < m; ++i)
pour (int j = i + 1; j < m; ++j)
couple[i][j] = gcd(nums[i], nombres[j];

pour le masque (int = 0; masque < maxMasque; ++Masque) {
// nombre d ' éléments déjà utilisés
int utilisé = Integer.bitCount(masque);
si (utilisé % 2 != 0) continuer; // ne peut pas être un état valide

// Essayez d'ajouter une nouvelle paire
pour (int i = 0; i < m; ++i) {
si ((masque & (1 << i)) != 0) continuer; // i déjà utilisé
pour (int j = i + 1; j < m; ++j) {
si ((masque & (1 << j))) != 0) continuer; // j déjà utilisé
Int nextMasque = masque (= 1 << i)= 1 << j);
int opIdx = utilisé / 2 + 1; // numéro d'exploitation basé sur 1
int cand = dp[mask] + opIdx * pair[i][j];
si (cand > dp[nextMask]) dp[nextMask] = cand;
}
}
}
retour dp[maxMask - 1];
}

Int privé gcd(int a, int b) {
pendant que (b != 0) {
t = a % b;
a = b;
b = t;
}
retour a;
}
}
«» "

### Python (LeetCode Style)

'`python
importer des maths
à partir de functools importer lru_cache

Solution de classe:
def maxScore(self, nums):
m = len(nums) # 2n
max_mask = 1 << m
dp = [0] * max_masque

# précalculer toutes les valeurs de la paire gcd
paire = [[0] * m pour _ dans l'intervalle(m)]
pour i dans la plage (m):
pour j à portée(i + 1, m):
couple[i][j] = math.gcd(nums[i], nombres[j])

pour masque dans la plage(max_mask):
utilisé = bin(masque).count('1')
si utilisé & 1: # nombre impair -> État impossible
poursuivre

pour i dans la plage (m):
si masque & (1 << i): # déjà utilisé
poursuivre
pour j à portée(i + 1, m):
si masque & (1 << j):
poursuivre
next_mask = masque
op_idx = utilisé // 2 + 1
Cand = dp[mask] + op_idx * pair[i][j]
si cand > dp[next_mask] :
dp[next_mask] = cand

retour dp[max_mask - 1]
«» "

C++ (LeetCode Style)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int maxScore(vecteur<int>& nums) {
int m = nombres.size(); // 2n
dans maxMask = 1 << m;
vecteur<int> dp(maxMasque, 0);

// pré-calculer gcd pour toutes les paires
le vecteur<vector<int>> pair(m, vector<int>(m, 0));
pour (int i = 0; i < m; ++i)
pour (int j = i + 1; j < m; ++j)
couple[i][j] = md::gcd(nums[i], nombres[j];

pour le masque (int = 0; masque < maxMasque; ++Masque) {
int utilisé = __constructin_popcount(mask);
si (utilisé & 1) continuer; // doit être égal

pour (int i = 0; i < m; ++i) {
si (masque & (1 << i)) continuer; // i déjà utilisé
pour (int j = i + 1; j < m; ++j) {
Si (masque & (1 << j)) continuer; // j déjà utilisé
Int nextMasque = masque (= 1 << i)= 1 << j);
= utilisé / 2 + 1;
int cand = dp[mask] + opIdx * pair[i][j];
dp[nextMask] = max(dp[nextMask], cand);
}
}
}
retour dp[maxMask - 1];
}
};
«» "

> **Astuce:** Les trois extraits utilisent la même table `pair` pour éviter de recompiler les GCD pendant DP.

---

Bonne, mauvaise et affreuse

Aspect du bien
- C'est quoi ?
**Approach**. *Bitmask DP* est une solution de manuel pour le petit `n`. 7' cela devient impraticable. Aucun—`n ≤ 7` est garanti, donc l'algorithme est sûr. Autres
**Complexité** L'utilisation de la mémoire est `2n` ints (16 k pour n=7). Si quelqu'un mal lit `n` comme longueur de tableau, il peut définir `maxMask = 1 << n` → mauvais espace d'état. Autres
**Le code Clarity**Le pré-computage des paires GCD permet une transition simple. Les boucles nentées (`i`/`j`) peuvent sembler désordonnées. Autres
Autres **Cas d'Edge** Aucun.
**Extensibilité**= Facile à adapter pour des « n » plus grands avec des « tours » dans le milieu » ou des « tours » dans la branche et dans le milieu. Nécessite une modification algorithmique majeure pour `n > 7`.

---

Conseils d'entrevue

1. **Clarifier les contraintes** – demander à l'intervieweur si `n` peut grandir au-delà de 7.
2. **Énoncer l'état du PDD** – Masque des indices utilisés.
3. **Justifier le pré-computing GCD** – permet d'économiser du temps en boucle DP.
4. **Afficher la complexité** – O(2n · n2) est acceptable.
5. **Parcourez un petit exemple** – par exemple, `nums = [2,3,4,9]` pour illustrer les transitions de masque.

---

Lire plus

Sujet Lien
- Oui.
[LeetCode Discuter: 1072. Colonnes Flip pour le nombre maximal de lignes égales](https://leetcode.com/problems/flip-columns-pour-nombre maximum de lignes égales/discuss/) Autres
[Codeforces 1036C – Flipping Game](https://codeforces.com/problemset/problem/1036/C) Autres
[C++17 std::gcd](https://en.cppreference.com/w/cpp/numeric/gcd) Autres

---

Résumé

* Le problème est petite taille d'entrée transforme un problème combinatoire apparemment dur en un DP bitmask soigné.
* Le pré-comptage de tous les GCD à paires transforme la transition DP en une seule multiplication.
* Les solutions fournies Java, Python et C++ suivent toutes les conventions LeetCode et fonctionnent confortablement sous les limites de temps de la plateforme.

Utilisez ce guide pour répondre à la question, impressionner les recruteurs ou simplement aiguiser votre boîte à outils algorithmique!

---

Codage heureux !
---
**Mots clés:** `maximisation`, `bitmask`, `programmation dynamique`, `gcd`, `LeetCode`, `Java`, `Python`, `C++`, `algorithme design`, `stratégie d'entrevue "
---
**Disclaimer:** Toutes les solutions sont testées sur le juge en ligne officiel LeetCode.