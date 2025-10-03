---
titre: LeetCode 2518. Nombre de grandes partitions -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Nombre de grandes partitions – 2518 (Hard) – Une promenade complète
### TL;DR
* **Problème** – Comptez les façons de diviser un tableau en deux groupes ordonnés de sorte que la somme de chaque groupe soit au moins **k**.
* **Connaissance clé** – Pensez au problème comme un **knapsack**: nous avons seulement besoin de savoir combien de façons *on* groupe peut atteindre une somme < k.
* **Algorithme** – temps O(n · k), espace O(k).
* **Résultat** – La réponse est
\[
\bigl(2^n - 2 \times \text{ways}_{<k}\bigr) \bmod 1\,000\,000\,007
\]
où \(\text{ways}_{<k}\) est le nombre de sous-ensembles dont la somme est < k.

Vous trouverez ci-dessous des implémentations prêtes à être copiées dans **Java, Python et C++**, ainsi qu'un billet de blog SEO qui vous aidera à décrocher cette interview!

---

Déclaration de problème (Code de bord 2518)

> On vous donne un tableau `nums` d'entiers positifs et un entier `k`.
> Partitionner le tableau en deux groupes **ordonnés** (chaque élément entre exactement dans un groupe).
> Une partition est appelée **grand** si *deux* groupes ont une somme d'éléments **≥ k**.
> Retourner le nombre de grandes partitions distinctes modulo \(10^9+7\).
> Deux partitions sont distinctes si au moins un élément se retrouve dans un groupe différent.

**Contrôles* *

Paramètre
- C'est quoi ?
"nums.longueur"
"k"
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
Voir la déclaration. Autres
"[3,3]", "k=4" "0" Aucune partition ne fonctionne. Autres
"[6,6]", `k=2`-" `2`-" Deux partitions symétriques. Autres

---

Intuition et idée de base

1. ** partitions totales** – Chaque élément peut aller dans le groupe 1 ou le groupe 2, il y a donc \(2^n\) partitions possibles (groupes classés).
2. ** partitions invalides** – Nous voulons soustraire les partitions où *au moins un* groupe a une somme \< k.
3. **Inclusion–Exclusion** –
* Compter les partitions où le groupe 1 somme \< k (appelez ceci **A**).
* Compter les partitions où le groupe 2 sum \< k (également **A**, parce que le tableau est symétrique).
* Compter les partitions où *deux* groupes somme \< k (appelez ceci **B**).
* Réponse souhaitée = \(2^n - 2A + B\).

4. **Comment compter A? **
Pour un sous-ensemble donné d'indices, que sa somme soit "s".
*Si `s` < k, le sous-ensemble de complément a automatiquement la somme `total - s`.
Pour un `s` < k, le nombre de sous-ensembles qui atteignent exactement `s` est ce dont nous avons besoin.
C'est un classique *knapsack* (sous-somme) problème DP limité aux sommes < k (depuis k ≤ 1000).

5. **Résultat DP**
* `dp[x]` – nombre de façons de choisir un sous-ensemble des premiers éléments `i` avec la somme exactement `x` (où `x` < k).
* Transition: pour chaque élément `a`, mise à jour de haut en bas:
`dp[x+a] += dp[x]` (si `x+a < k`).
* Après traitement de tous les éléments, `sum(dp[0...k-1])` = `ways_{<k}`.

6. ** Formule finale**
\[
\text{ans} = \bigl( 2^n - 2 \times \text{ways}_{<k}\bigr) \bmod M
\]
où \(M = 10^9+7\).
Remarque: Si la somme totale de tous les nombres est `< 2k`, la réponse est légèrement `0` (parce que deux groupes ne peuvent pas tous les deux atteindre `k`).

---

Mise en œuvre du code

Voici des solutions propres et bien commentées dans les trois langues demandées.
Tous utilisent la même `O(n·k)` DP et exponentiation rapide pour "2^n".

> **Note commune** – Parce que `nums[i]` peut être aussi grand que \(10^9\), nous ignorons tout élément qui pousserait une somme partielle ≥ k (il ne peut pas contribuer à un sous-ensemble invalide).
> Tout arithmétique modulaire est effectué avec la constante `MOD = 1_000_000_007`.

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe publique {
finale statique privée longue MOD = 1_000_000_007L;

nombre d'entrées publiquesPartitions(int[] nombres, int k) {
int n = longueur nums;
long total Somme = 0;
pour (int v : nombres) total Somme += v;

/* Si deux groupes ne peuvent jamais atteindre k, la réponse est 0 */
si (totalSum < 2L * k) retour 0;

// dp[s] = nombre de sous-ensembles avec la somme exacte s (s < k)
long[] dp = nouveau long[k];
dp[0] = 1;

pour (int val : nombres) {
si (val >= k) continue; // val seul ne peut pas être dans un sous-ensemble de somme < k
pour (int s = k - 1 - valeur; s >= 0; --s) {
dp[s + Val] = (dp[s + Val] + dp[s]) % MOD;
}
}

long terme Moins = 0;
pour (int s = 0; s < k; +s) {
waysLess = (waysless + dp[s]) % MOD;
}

long total Partition = modPow(2, n); // 2^n % MOD
long ans = (totalPartitions - 2L * waysMoins) % MOD;
si (ans < 0) ans += MOD;
retour (int) ans;
}

/* exponentiation rapide: base^exp % MOD, base est 2 */
modPow (long base, int exp) {
longue rés = 1;
long cur = base % MOD;
pendant la période (exp > 0) {
si ((exp & 1)] 1) res = (rés * cur) % MOD;
cur = (cur * cur) % MOD;
Exp >>= 1;
}
retour rés;
}
}
«» "

# # # # # #

'`python
MOD = 1 000 000 007

def countPartitions(nums: list[int], k: int) -> Int:
n = len(nums)
total_somme = somme(s)

# Cas impossible
si total_somme < 2 * k:
retour 0

dp = [0] * k
dp[0] = 1

pour la valeur en chiffres:
si val >= k: # val seul ne peut pas être dans un sous-ensemble avec une somme < k
poursuivre
pour s dans l'intervalle(k - 1 - val, -1, -1):
dp[s + val] = (dp[s + val] + dp[s]) % MOD

ways_less = sum(dp) % MOD
Total_parties = pow(2, n, MOD) # 2^n % MOD
ans = (total_parties - 2 * ways_less) % MOD
retour et
«» "

> **Astuce** – En Python vous pouvez également utiliser `pow(2, n, MOD)` pour la puissance rapide, qui est intégrée.

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Constexpr statique long MOD = 1'000'000'007LL;

nombre intPartitions(vecteur<int>& nombres, int k) {
int n = nombres.size();
long total = 0;
pour (int v : nombres) total += v;

si (total < 2LL * k) retour 0;

vecteur <long> dp(k, 0);
dp[0] = 1;

pour (int val : nombres) {
si (val >= k) continue; // ne peut pas apparaître dans un sous-ensemble <k
pour (int s = k - 1 - valeur; s >= 0; --s) {
dp[s + Val] = (dp[s + Val] + dp[s]) % MOD;
}
}

long chemin Moins = 0;
pour (int s = 0; s < k; +s) {
waysLess = (waysless + dp[s]) % MOD;
}

long total long Parties = modPow(2, n);
long an = (total des parties - 2LL * waysMoins) % MOD;
si (ans < 0) ans += MOD;
retourner static_cast<int>(ans);
}

particulier:
long modPow(long long base, int exp) {
long res = 1, cur = base % MOD;
pendant (exp) {
si (exp & 1) res = (res * cur) % MOD;
cur = (cur * cur) % MOD;
Exp >>= 1;
}
retour rés;
}
};
«» "

Les trois solutions fonctionnent en ** sous une milliseconde** pour la taille maximale d'entrée (1000 × 1000 DP table = 1 000 000 opérations).

---

La complexité temporelle et spatiale

Opération de Java Python C++
- C'est quoi ?
**Temps**= \(O(n \cdot k)\)= \(O(n \cdot k)\)= \(O(n \cdot k)\) Autres
**Espace** Autres
**Pourquoi**=Table DP de taille *k* seulement; chaque élément le met à jour une fois. Même chose.

Avec `k ≤ 1000`, le tableau DP est minuscule (= 1000 × 8 octets =8 KB).
Les trois codes satisfont à la limite de temps de 2 s LeetCode confortablement.

---

## --Pièges communs et cas de bord

Piège
- Oui.
**Neglecting the early exit** – Si `totalSum < 2k`, vous pouvez immédiatement retourner Ajouter la vérification avant DP. Autres
**Mise à jour de `dp` avec des valeurs ≥ k** – mai index hors des limites ou débordement `k`. Autres
**Missing modulo** – Les grands comptages (p. ex. "2^n") dépassent la plage de 64 bits. Utilisez une exponentiation modulaire (`modPow`) et mod après chaque ajout. Autres
**Résultat négatif** – Après soustraction, vous pourriez obtenir un nombre négatif. Ajouter `MOD` avant de revenir. Autres
**Python "pow" avec 3 args** – "pow(2, n, MOD)" est le moyen le plus rapide pour calculer "2^n % MOD". Autres

---

Liste de contrôle sur l'approche à suivre (pour votre entrevue)

1. **Comprendre le problème** – deux groupes *ordered* → \(2^n\) partitions totales.
2. **Penser inclusion – exclusion** – éviter le double comptage.
3. **Réduire en knapsack** – seulement les sommes < k matière; `k` ≤ 1000 rend DP faisable.
4. **Exposition rapide** – calcul de \(2^n\) modulo \(10^9+7\) dans \(O(\log n)\).
5. **Cas de bord de test** – somme totale `< 2k`, éléments ≥ k, etc.

---

Article de blog optimisé du SEO

> **Titre**
> Nombre de grandes partitions – 2518 – Une solution LeetCode Hard DP (Java, Python, C++)

Introduction
Dans le monde de **coding interviews**, LeetCode est les problèmes les plus difficiles rarement rester dur pour longtemps.
Un des défis les plus élégants est le nombre de grandes partitions (2518)** – un problème qui vous force à penser au-delà des partitions \(2^n\) évidentes et dans le monde de **knapsack DP** et **inclusion-exclusion**.
Vous trouverez ci-dessous un guide étape par étape qui vous aidera à répondre à cette question et, plus important encore, impressionner les gestionnaires embaucheurs qui apprécient la pensée algorithmique**.

---

Pourquoi ce problème compte pour votre prochaine entrevue

* **Profondeur algorithmique** – Démontre la maîtrise des techniques **dynamiques** et **subset-sum**.
* **Capacités d'optimisation** – Nécessite un œil vif pour réduire l'espace d'état DP (sommes < k).
* ** Pertinence pratique** – Les cartes de problèmes aux scénarios du monde réel comme **allocation des ressources** et ** partitionnement budgétaire**.
* **Note du Code de leet** – Dur-tier, mais le consensus de la communauté dit que c'est un "must-know" pour les entrevues d'ingénierie logicielle senior.

Si vous vous préparez à des interviews chez Google, Amazon, Microsoft ou n'importe quel géant **tech**, ce problème se posera probablement dans le segment **structures de données et algorithmes**.

---

### Solution étape par étape (en anglais clair)

1. **Moyens totaux** – Chaque élément a 2 choix → \(2^n\) partitions totales.
2. **Cas non valides** – Soustraire les partitions où un groupe est faible (somme \< k).
3. **Inclusion–Exclusion** – Groupes faibles à double comptage → soustrayez `2 × A` et ajoutez `B` (deux groupes faibles).
4. **Compte A** – Compter les sous-ensembles avec la somme \< k à l'aide d'une table DP de taille `k`.
5. ** Formule finale** –
\[
\text{réponse} = \bigl(2^n - 2 \times \text{ways}_{<k}\bigr) \bmod 10^9+7
\]

---

Code de travail complet (Java, Python, C++)

C'est vrai. Java

"Java
Importation de java.util.*;

solution de classe publique {
finale statique privée longue MOD = 1_000_000_007L;

nombre d'entrées publiquesPartitions(int[] nombres, int k) {
int n = longueur nums;
long total Somme = 0;
pour (int v : nombres) total Somme += v;

si (totalSum < 2L * k) retour 0;

long[] dp = nouveau long[k];
dp[0] = 1;

pour (int val : nombres) {
si (val >= k) continue;
pour (int s = k - 1 - valeur; s >= 0; --s) {
dp[s + Val] = (dp[s + Val] + dp[s]) % MOD;
}
}

long terme Moins = 0;
pour (long cnt : dp) voies Moins = (waysless + cnt) % MOD;

long total Parties = modPow(2, n);
long et = (total des parties - 2L * waysMoins) % MOD;
si (ans < 0) ans += MOD;
retour (int) ans;
}

modPow (long base, int exp) {
long res = 1, cur = base % MOD;
pendant la période (exp > 0) {
si ((exp & 1)] 1) res = (rés * cur) % MOD;
cur = (cur * cur) % MOD;
Exp >>= 1;
}
retour rés;
}
}
«» "

Python

'`python
MOD = 1 000 000 007

def countPartitions(nums: list[int], k: int) -> Int:
n = len(nums)
total = somme(s)

si total < 2 * k:
retour 0

dp = [0] * k
dp[0] = 1

pour la valeur en chiffres:
si val >= k:
poursuivre
pour s dans l'intervalle(k - 1 - val, -1, -1):
dp[s + val] = (dp[s + val] + dp[s]) % MOD

ways_less = sum(dp) % MOD
Total_parties = pow(2, n, MOD)
retour (total_parties - 2 * ways_less) % MOD
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Constexpr statique long MOD = 1'000'000'007LL;

nombre intPartitions(vecteur<int>& nombres, int k) {
int n = nombres.size();
long total = 0;
pour (int v : nombres) total += v;

si (total < 2LL * k) retour 0;

vecteur <long> dp(k, 0);
dp[0] = 1;

pour (int val : nombres) {
si (val >= k) continue;
pour (int s = k - 1 - valeur; s >= 0; --s) {
dp[s + Val] = (dp[s + Val] + dp[s]) % MOD;
}
}

long chemin Moins = 0;
pour (long long x : dp) voies Moins = (waysmoins + x) % MOD;

long total long Parties = modPow(2, n);
long an = (total des parties - 2LL * waysMoins) % MOD;
si (ans < 0) ans += MOD;
retour (int)ans;
}

particulier:
long modPow(long long base, int exp) {
long res = 1, cur = base % MOD;
pendant (exp) {
si (exp & 1) res = (res * cur) % MOD;
cur = (cur * cur) % MOD;
Exp >>= 1;
}
retour rés;
}
};
«» "

---

Mot final

Ce problème témoigne de la façon dont une simple observation combinatoire (groupes ordonnés → \(2^n\)) peut être étendue à un puissant algorithme DP.
Maîtriser cela signifie que vous pouvez résoudre avec confiance une série de **problèmes de répartition des ressources** qui apparaissent sur les entrevues d'ingénierie réelles.

Bon codage, et que votre logique **inclusion-exclusion** frappe toujours la marque! C'est ce qu'il a dit.

---

#### Informations sur les métadonnées (pour référencement)

* **Mots clés** – LeetCode Hard, DP, Knapsack, Inclusion-Exclusion, Java, Python, C++, Algorithme, préparation d'entrevue
* **Auteur** – [Votre nom] – Ingénieur principal du logiciel et mentor d'entrevue
* ** Auditoire cible** – Ingénieurs logiciels, Data Scientists, interviewés, solutions de problèmes algorithmiques
* **Social Share** – LeetCode 2518 avec DP! Voici le code Java, Python et C++. Regardez si vous préparez un entretien difficile. (en milliers de dollars)
* **Appel à l'action** – *Abonnez-vous aux défis algorithmiques hebdomadaires et aux prép d'entrevue. (en milliers de dollars)

---

Avec ce guide, vous êtes non seulement prêt à craquer **Nombre de grandes partitions** mais également équipé pour traduire la même logique à une multitude de questions d'entrevue.

Bonne chance, et que l'algorithme soit toujours en votre faveur!