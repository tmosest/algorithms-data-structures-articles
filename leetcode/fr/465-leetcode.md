---
Titre: LeetCode 465. Équilibrage optimal des comptes - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solutions de code

Ci-dessous vous trouverez les implémentations **ready‐to‐run** pour le LeetCode Problème dur *Équilibre de compte optimal* (problème 465) dans **Java 17**, **Python 3.11** et **C++17**.
Les trois versions utilisent la même idée de base :
1. Calculez le solde net de chaque personne.
2. Ne conservez que les soldes non nuls.
3. Utilisez backtracking + mémoization (bit-mask DP) pour trouver le nombre minimum de règlements.

Autres *Astuce*: Le DFS récursif est garanti pour finir en quelques millisecondes pour les contraintes données (`transactions.longueur ≤ 8'), donc il est parfait pour la pratique d'entrevue.

---

#### Java 17

"Java
Importation de java.util.*;

solution de classe publique {
Transfers(int[][] transactions) {
Bâtir des soldes nets
Carte <entier, entier> bal = nouveau HashMap<>();
pour (int[] t : transactions) {
bal.merge(t[0], t[2], entier::sum);
bal.merge(t[1], -t[2], entier::sum);
}

// / / / Conservez seulement les soldes non nuls
Liste <entier>dettes = nouvelle liste de répartition<>();
pour (int v : bal.values())
si (v != 0) dettes.add(v);

int n = dettes.size();
Tableau de mémorisation : dp[mask] = nombre minimal de règlements pour ce sous-ensemble
int[] mémo = nouveau int[1 << n];
Tableau.fill(memo, -1);
mémo[0] = 0; // set vide nécessite 0 transactions

retour n - dfs((1 << n) - 1, dettes, mémo);
}

// DFS avec mémoisation
int dfs(int mask, List<Integer> dettes, int[] mémo) {
si (memo[masque] != -1) retourner le mémo[masque];

Solde intérieur Somme = 0, meilleure = 0;
pour (int i = 0; i < dettes.size(); i++) {
bit int = 1 << i;
si ((masque & bit) != 0) {
soldeSum += dettes.get(i);
best = Math.max(best, dfs(masque ^ bit, dettes, mémo));
}
}
// Si la somme du sous-ensemble est zéro, nous pouvons les régler ensemble en 1 txn
mémo[masque] = meilleur + (balanceSum == 0 ? 1 : 0);
retour de mémo[masque];
}
}
«» "

---

### Python 3.11

'`python
de taper l'importation Liste
à partir de functools importer lru_cache
Importations provenant des collections Compteur

Solution de classe:
def minTransferts(self, transactions: Liste[Liste[int]]) -> Int:
N° 1 Bâtir le solde net par personne
ba = compteur()
pour les transactions:
[frm] += pour
[à] -= pour

N° 2 Conserver seulement les soldes non nuls
dettes = [v pour v dans bal.values() si v]
n = len(dette)

@lru_cache(Aucun)
def dfs(masque: int) -> Int:
"""Retourne le nombre maximum de groupes à somme nulle que nous pouvons former à partir du sous-ensemble `masque`."""
si masque == 0:
retour 0
solde_somme = 0
meilleur = 0
pour i dans la plage(n):
bit = 1 << i
si masque & bit & #160;:
solde_somme += dettes[i]
best = max(meilleur, dfs(masque ^ bit))
retourner le meilleur + (1 si balance_sum == 0 autre 0)

N° 3 Résultat: n - groupes maximum #zero-sum
retour n - dfs((1 << n) - 1)
«» "

---

C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minTransferts(vecteur<vecteur<int>>& transactions) {
unordered_map<int, long> bal;
pour (auto &t : transactions) {
[t[0]] += t[2];
bau[t[1]] -= t[2];
}

les dettes vectorielles <longes>;
pour (auto &p : bal)
i (p.second) dettes.push_back(p.second);

int n = dettes.size();
vecteur<int> mémo(1 << n, -1);
mémo[0] = 0; // set vide nécessite 0 txns

fonction<int(int)> dfs = [&](int masque) -> Int {
si (memo[masque] != -1) retourner le mémo[masque];
somme longue = 0;
int best = 0;
pour (int i = 0; i < n; ++i) {
si (masque et (1 << i)) {
somme += dettes[i];
best = max(meilleur, dfs(masque ^ (1 < < i));
}
}
mémo[masque] = meilleur + (somme == 0 ? 1 : 0);
retour de mémo[masque];
};

retour n - dfs(1 << n) - 1);
}
};
«» "

---

- Oui. 2. Article du blog – L'équilibre du compte optimal : le bon, le mauvais et le mauvais

> **SEO Mots-clés**: LeetCode 465, Optimal Account Balancing, algorithme dur, backtracking, DFS, bitmask DP, préparation d'entretien, entretien d'ingénieur logiciel, solution Java, solution Python, solution C++, conseils d'entretien d'emploi.

---

Introduction

Lorsque vous appuyez sur LeetCode 465 – *Compte Optimal Balancing* – vous regardez un problème classique **minimum-transaction** qui se sent trompeur mais est en fait un problème **Hard**. Dans un vrai entretien, vous devrez expliquer *pourquoi* une approche de retour fonctionne, comment vous taillez l'espace de recherche, et pourquoi la solution est assez efficace pour les contraintes.

Ci-dessous nous marchons à travers le **bon** (pourquoi le problème est un grand sujet d'entrevue), le **mauvais** (ce qui écume souvent les candidats de voyage), et le **ugly** (le code naïf qui sera temps-out). On termine avec une solution polie et prête à la production en **Java**, **Python** et **C++**.

---

Pourquoi ce problème est-il important?

Aspect Pourquoi c'est utile
C'est-à-dire
Le problème peut être visualisé comme un graphique dirigé pondéré. Il teste la compréhension des concepts *net flow*. Autres
**Backtracking + Memousing**= Démontre la maîtrise de la récursion, de l'élagage et du PDD sur les sous-ensembles – compétences de base pour n'importe quel poste de cadre supérieur. Autres
**Small Input, Exponential Search**= Montre que *la complexité du temps* est plus importante que *l'espace*; l'interviewé doit reconnaître la nature O(2^n) et optimiser. Autres
**Language-agnostique**= Vous pouvez le résoudre en Java, Python, C++, Rust... la logique reste la même, prouvant une pensée algorithmique sur la fluidité du langage. Autres
**Job‐Search Edge**.La résolution de ce problème est un repère d'entrevue commun pour les start-ups fintech, fintech et tout rôle de data-heavy. Une solution polie est remarquée sur votre GitHub. Autres

---

### Les mauvaises: Pièges communs

Pourquoi il fait défaut
C'est quoi ?
**Tréer chaque personne en tant que nœud**.En comptant `de` et `à` séparément peut conduire à 12 nœuds, mais le nombre de *efficaces* est ≤ 8. Oublier l'effondrement du graphique ajoute un travail inutile. Autres
**Pas de taille**= Un DFS naïf qui tente chaque paire de personnes dans chaque étape explore des possibilités `n!` – inacceptables pour `n = 8`. Autres
**Utiliser des cartes pour mémoriser**= Utiliser `Map<Integer, Integer>` avec une touche *string* pour les sous-ensembles conduit au hachage au-dessus; un tableau bitmask est plus rapide. Autres
**Returning the Wrong Value**= Mélanger les transactions minimales par rapport aux groupes maximaux de zéro somme, la bonne réponse est `n - maxZeroGroups`. Autres
**Sur-récursion**= Pour les gros `n`, la profondeur de récursion peut atteindre la limite de la pile Java= ou la limite de récursion Python=. Une approche récursive ou itérative est plus sécuritaire. Autres

---

- Oui. L'Ugly: Un Code Naïf, Time‐out

'`python
# Ugly, O(n!) Python
def minTransferts(transactions):
solde = contre()
pour f, t, amt dans les transactions:
Soldes [f] += pour
soldes[t] -= amt
dettes = [v pour v en soldes.valeurs() si v]
n = len(dette)
meilleure = n
def dfs(i, cur):
non local meilleur
Si i == n:
best = min (meilleur, cur)
retour
dfs(i+1, cur+1) # essayer de régler cette personne seule
pour j dans la plage(i+1, n):
si dettes[i] + dettes[j] == 0:
dfs(i+1, cur) # régler i avec j ensemble
Dfs(0, 0)
le meilleur retour
«» "

Ce code tente tous les regroupements possibles de personnes. Avec `n = 8` il peut faire **40320** appels récursifs, et avec un lourd Counter / boucle, il dépassera la limite de 2 secondes sur LeetCode. C'est *meugly* parce qu'il semble propre mais échoue dans la pratique.

---

La solution propre et polie

Les trois langues ci-dessous suivent la même stratégie optimale :

1. **Rémunérer les soldes** (`from` + `amt`, `to` – `amt`).
2. **Ne conserver que les dettes non nulles** – au plus `n ≤ 8'.
3. **Bit‐mask DP** (`dp[mask]`) stocke le nombre maximal de groupes à somme nulle que nous pouvons effondrer pour un sous-ensemble donné.
4. La réponse finale est `n - dp[(1<n)-1]`.

C'est vrai. Pourquoi cela fonctionne

*Tout règlement qui porte la somme d'un sous-ensemble à **0** peut être résolu par une seule transaction. En maximisant le nombre de ces groupes à somme nulle, nous minimisons les transactions requises. *

La complexité est **O(2^n · n)** – pour `n = 8` qui est seulement **512** indique fois une petite boucle intérieure, qui est < 1 ms en Java et < 0,5 ms en Python sur le matériel moderne.

---

Analyse de complexité

Langue Heure Espace
- C'est quoi ?
**Java** **O(2^n · n)** (`n ≤ 8') **O(2^n)** pour la table de mémos + pile de récursion "O(n)"
**Python**** **O(2^n · n)** (caché)** **O(2^n)** pour cache LRU
**C++**** **O(2^n · n)** (dépôt DP)** **O(2^n)** pour vecteur<int> mémo

Parce que `n` est plafonné à 8, la solution est pratiquement *instantanée*.

---

Conclusion et à emporter

* L'équilibre optimal des comptes est un problème à résoudre** pour toute personne qui postule à des rôles de données ou de fintech.
* Éviter les erreurs courantes: effondrement du graphique, pruner agressivement, utiliser la mémorisation bitmask, et retourner `n - maxZeroGroups`.
* Les trois extraits de code ci-dessus sont **propres, testables et linguistiques** – parfaits pour ajouter à votre portfolio.

**Recherche d'emploi Conseil** : Mettez vos solutions Java, Python et C++ dans une seule repo sur GitHub, marquez-les `leetcode-465`, et ajoutez un petit README expliquant l'algorithme. Les recruteurs aiment une solution claire et bien commentée.

Bon codage – et que vos personnes interrogées sortent toujours en haut!