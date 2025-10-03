---
titre: LeetCode 1494. Cours parallèles II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Cours parallèles II (Leetcode 1494) – De l'interview au travail

> **TL;DR**
> *Parallel Courses II* est un problème difficile DP‐bitmask qui teste votre capacité à penser dans des états, générer des sous-ensembles efficacement et tailler l'espace de recherche.
> La clé pour clouer l'entrevue est de comprendre ** représentation d'état**, ** logique de transition**, et ** astuces de taille**.
> L'article suivant explique le problème, montre des solutions de travail dans **Java**, **Python** et **C++**, et parle du *bon, du mauvais et de la laid* de l'approche DP‐bitmask.
> Bonus : SEO-optimized copie qui fera votre blog ou portfolio rang sur Google pour les mots-clés d'entrevue exacts!

---

- Oui. 1. Déclaration de problème (code de bord 1494)

«» "
Il y a n cours marqués de 1 à n.
relations[i] = [a, b] signifie que le cours a doit être suivi avant le cours b.

Chaque semestre, vous pouvez suivre au plus des cours k,
mais seulement si toutes leurs conditions préalables ont déjà été prises.

Retournez le nombre minimum de semestres requis pour terminer tous les cours.
Les cas d'essai sont garantis comme solvables (le graphique est un DAG).
«» "

1 ≤ n ≤ 15,1 1 ≤ k ≤ n,0 0 ≤ relations,longueur ≤ n(n‐1)

---

- Oui. 2. Intuition – Pourquoi Bitmask DP?

- **État** = ensemble de cours déjà complétés.
Avec *n* ≤ 15, un entier 16 bits peut coder tous les sous-ensembles → **2n états**.
- Oui. Chaque semestre, nous choisissons un sous-ensemble de cours *disponibles* (degré = 0) avec une taille ≤ k.
- Calculez récursivement la réponse pour le nouvel état.
- Mémoriser pour éviter de recomptabiliser le même sous-ensemble.

Il s'agit du modèle classique *DP sur les sous-ensembles* qui apparaît dans les problèmes comme l'annexe III du cours, le nombre minimal de robinets, etc.

---

- Oui. 3. Aperçu de l'algorithme

1. **Liste d'adjacence de construction** et tableau des degrés.
2. **DFS + mémoisation** sur l'état bitmask :
* Si tous les cours suivis → retour 0.
* Identifier les cours *disponibles* : degré = 0 et non en masque.
* Énumérer tous les sous-ensembles de cours disponibles dont la taille ≤ k.
Pour chaque sous-ensemble:
* Mark cours comme pris → newMask.
* Mettre à jour les degrés pour les enfants → newIndegree.
* Répétition: `1 + dfs(newMask, newIndegree)`.
* Prendre le minimum sur tous les sous-ensembles.
3. Retourne le résultat de l'appel initial.

Optimisations

Solution
C'est pas vrai.
Enumerer **k**‐sous-sets naïvement (O(2^m))= Prégénérer toutes les combinaisons de taille 1...k pour chaque `m` (= n) ou utiliser des tricks bit (`_builtin_popcount` en C++). Autres
Redistribuer le tableau des degrés chaque récursion. (Pour plus de clarté, nous recopions – toujours rapide pour n ≤ 15.) Autres
Dupliquer le travail lorsque de nombreux cours sont disponibles. Autres

---

- Oui. 4. Esquisse de preuve d'exactitude

Nous prouvons par induction sur le nombre de cours restants que l'algorithme retourne le nombre optimal de semestres.

*Base*: Lorsque le masque est égal à `(1<n)-1`, tous les cours sont suivis. L'algorithme renvoie 0, ce qui est optimal.

*Étape d'induction*: Assumer pour tout masque avec *t* cours restants l'algorithme retourne l'optimum. Considérez un état avec *t+1* cours restants.
Laissez `S` être l'ensemble des cours disponibles à cet état. Tout planning optimal doit choisir un sous-ensemble `X' S` avec=X=1 ≤ k à prendre au prochain semestre, car nous ne pouvons pas suivre un cours dont les conditions préalables sont incomplètes.

L'algorithme énumère **chaque** tel "X".
Pour chaque `X`, il calcule `1 + optimum(S', X)` où `S'` est le nouveau masque.
Par l'hypothèse d'induction, `optimal(S', X)` est le nombre optimal de semestres pour les cours restants après avoir pris `X`.
Par conséquent, l'algorithme considère toutes les premières étapes optimales possibles et renvoie le minimum, ce qui équivaut à la valeur optimale pour l'état actuel. *

---

- Oui. 5. Analyse de la complexité

- **Etats** : "2n"
- **Par État**: énumérer les sous-ensembles de cours disponibles ('C(m,1)+...+C(m,k)'), dans le pire des cas 'C(15,7) 6435'.
- **Heure**: `O(2n * C(n, k))` → 106 opérations, facilement sous 1 s.
- **Espace**: `O(2n)` pour mémoisation + `O(n)` pour adjacence + tableaux de degrés.
≤ ~ 100 kB.

---

- Oui. 6. Code

> **Les trois implémentations utilisent la même logique mais ne diffèrent que par syntaxe. **
> Chaque fichier est autonome et peut être copié dans l'éditeur de Leetcode correspondant.

#### 6.1 Java (style Leetcode)

"Java
Importation de java.util.*;

solution de classe {
Liste privée<entier>[] graphique;
degré int privé;
Int privé[] mémo;
Int privé n, k;
Int privé FULL_MASK;

public int minNumberOfSemesters(int n, int[][] relations, int k) {
n = n; k = k;
Ça. FULL_MASK = (1 << n) - 1;
graphique = nouvelle liste[n];
pour (int i = 0; i < n; ++i) graphe[i] = nouvelle liste de distribution<>();
indegree = nouvelle int[n];
pour (int[] rel : relations) {
i u = rel[0] - 1, v = rel[1] - 1;
graphic[u].add(v);
degré[v]++;
}
mémo = nouvelle int[1 << n];
Tableau.fill(memo, -1);
retour dfs(0, degré);
}

Int privé dfs(int masque, int[] curIndegree) {
si (masque == FULL_MASK) retourne 0;
si (memo[masque] != -1) retourner le mémo[masque];

// Trouvez les cours disponibles
Liste <Intégrer> product = nouvelle liste d'array<>();
pour (int i = 0; i < n; ++i)
si ((masque >> i) & 1) == 0 && curIndegree[i] == 0)
l'alinéa i) est remplacé par le texte suivant:

int m = disponibilité.size();
i (m <= k) { // prendre tous en même temps
int newMask = masque;
int[] nextInd = curIndegree.clone();
pour (int v : disponibilité) {
nouveauMasque= 1 << v;
pour (int child : graph[v]) suivant Ind [enfant]...
}
retourner mémo[mask] = 1 + dfs(newmask, nextInd);
}

// Énumérer tous les sous-ensembles de taille 1..k
int best = entier.MAX_VALUE;
pour (int sub = 1; sub < (1 < < m); ++sub) {
Si (Integer.bitCount(sub) > k) poursuivre;
int newMask = masque;
int[] nextInd = curIndegree.clone();
pour (int idx = 0; idx < m; ++ idx)
si ((sub >> idx) & 1) {
int v = adv.get(idx);
nouveauMasque= 1 << v;
pour (int child : graph[v]) suivant Ind [enfant]...
}
best = Math.min(best, 1 + dfs(newMask, nextInd));
}
retourner mémo[masque] = meilleur;
}
}
«» "

> *Pourquoi il s'agit d'une solution Java
> - Mise en mémoire claire de l'état à l'état («int[] memory»).
> - Utilise `clone()` pour la brièveté (n ≤ 15 → coût négligeable).
> - Gère le raccourci `m <= k` qui supprime un grand nombre de branches.

---

##### 6.2 Python (style fonctionnel, `functools.lru_cache`)

'`python
à partir de functools importer lru_cache
de collections import defaultdict, deque
de taper l'importation Liste

Solution de classe:
def minNumberOfSemesters(self, n: int, relations: List[List[int]], k: int) -> Int:
graphique = [[] pour _ dans l'intervalle(n)]
endeg = [0]*n
pour a, b dans les relations:
graphe[a-1].annexe(b-1)
endeg[b-1] += 1

FULL = (1 << n) - 1

@lru_cache(Aucun)
def dfs(mask, indeg_tuple):
si masque == C'est bon.
retour 0
indég = list(indeg_tuple)

Nombre de cours disponibles
[i pour i dans l'intervalle(n)
si ce n'est pas le cas (masque >> i) & 1 et indég[i] == 0]
m = len(vail)

i m <= k: # prendre tout
nouveau_masque = masque
pour v en usage:
nouvelle_masque= 1 << v
pour l'enfant dans le graphique[v]:
indig[enfant] -= 1
retour 1 + dfs(new_mask, tuple(indeg))

meilleure = flotteur('inf')
# énumérer les sous-ensembles de taille 1..k
pour les sous-groupes de la gamme(1, 1 << m):
si sub.bit_count() > k:
poursuivre
nouveau_masque = masque
new_indeg = indeg[:]
pour i dans la plage (m):
si sous >> i & 1:
v = disponibilité[i]
nouvelle_masque= 1 << v
pour l'enfant dans le graphique[v]:
nouvelle_indeg[enfant] -= 1
best = min(meilleur, 1 + dfs(new_mask, tuple(new_indeg))
le meilleur retour

retour dfs(0, tuple(indeg))
«» "

> *Pourquoi c'est une solution de Python ? *
> "clone()" de Python et la copie de la liste sont *slower* mais toujours amende pour *n* = 15.
> Pour le code de production, vous retourneriez dans les degrés au lieu de copier.

---

*### 6.3 C++ (style Leetcode)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minNumberOfSemesters(int n, vector<vector<int>>& relations, int k) {
vecteur<vector<int>> g(n);
vecteur<int> indég(n, 0);
pour (auto &r : relations) {
int u = r[0]-1, v = r[1]-1;
g[u].push_back(v);
endeg[v]++;
}

const int FULL = (1<<n)-1;
vecteur<int> dp(1<n, -1);

fonction<int(int, vector<int>&)> dfs = [&](int masque, vector<int>& curIndeg) {
si (masque == FULL) retourner 0;
si (dp[masque] != -1) retour dp[masque];

vecteur<int> disponibilité;
pour (int i=0;i<n;++i)
if (!(mask>>i&1) && curIndeg[i]==0) product.push_back(i);

int m = disponibilité.size();
si (m <= k) { // prendre tout
int newMask = masque;
au lieu de (int v: disponibilité) {
nouveauMasque= 1<<v;
pour (int enfant: g[v]) curIndeg[enfant]--;
}
retour dp[mask] = 1 + dfs(newmask, curIndeg);
}

int best = INT_MAX;
// Énumérer tous les sous-ensembles de disponibilité dont la taille <= k
pour (int sub = 1; sub < (1<<m); ++sub) {
si (_buildingin_popcount(sub) > k) continue;
int newMask = masque;
// modifier temporairement le degré
vector<int> nextIndeg = curIndeg;
pour (int i=0;i<m;++i)
si (sub>>i & 1) {
int v = disponibilité[i];
nouveauMasque= 1<<v;
pour (int enfant: g[v]) suivantIndeg [enfant]--;
}
best = min(meilleur, 1 + dfs(newMask, nextIndeg);
}
retour dp[mask] = meilleur;
};

retour dfs(0, endeg);
}
};
«» "

> *Pourquoi c'est une implémentation C++ ? *
> - Utilise `_builtin_popcount` pour des vérifications rapides de la taille des sous-ensembles.
> - Copies de degré seulement pour l'appel récursif; la copie est bon marché pour `n ≤ 15`.
> - Séparation claire de *état*, *transition* et *mémorisation*.

---

- Oui. 7. Bonnes, mauvaises et mauvaises – DP‐Bitmask dans les entrevues

Aspect du bien
- C'est quoi ?
** Taille de l'État** (2n) **Petit** (`n ≤ 15'). **Exponentiel** – attention à ne pas dépasser «n = 30». **Non prévisible** pour les plus grands
**Cadre de branching** (dénombrement de sous-ensembles) **Le recul sans élagage** conduit à TLE. Autres
**Mémoisation**= Clean `int[] memo` → O(2n). Oublier de stocker les résultats → travail répété. L'utilisation d'un *map* au lieu d'un tableau conduit à *memory tope*. Autres
**Mise à jour des degrés**=Clone ou retourne les modifications → O(n) par récursion. Mise à jour mondialement en place peut produire * états incompatibles*. Trop de copies peuvent devenir un facteur constant caché* ralentissement. Autres
**Compréhension de la complexité** Un excès d'optimisation (p. ex. des tricks bitset) peut distraire l'idée centrale. Autres

> **À emporter :**
> * Expliquez votre taille et la génération de combinaisons avant de plonger dans le code. *
> Les intervieweurs aiment les candidats qui montrent le *pourquoi* avant le *quoi*.

---

- Oui. 8. Solutions de rechange et pourquoi nous avons choisi celle-ci

Description de l'alternative
C'est pas vrai.
**Topological DP + BFS**) Traitez chaque semestre comme un niveau, utilisez BFS pour explorer les états niveau par niveau. Plus simple à comprendre. Autres
**Heuristique / Greedy** (par exemple, toujours prendre le plus grand ensemble disponible) Leetcode nécessite une solution optimale. Autres
**Bitset + DP** (ordonnée)= Utiliser le bitset pour itérer sur tous les états dans l'ordre croissant du masque. Éviter la récursion des frais généraux. Autres
**Moixed DP + BFS**. Potentiellement moins de mémoire. Autres

> *Pourquoi la solution DP‐bitmask est la réponse à l'entrevue de type «standard» : *
> Il cartographie clairement la question de l'interview, les états, les transitions, la mémoisation, que de nombreux intervieweurs demandent.
> Il montre que vous pouvez raisonner sur les sous-ensembles, gérer l'explosion combinatoire, et garder le code dans les limites de temps.

---

- Oui. 9. Liste de contrôle de préparation à l'entrevue

1. **Lisez attentivement les contraintes** → *n* est petit, donc les états exponentiels sont bons.
2. ** Expliquez l'état** (masque) et pourquoi il correspond à 15 cours.
3. **Afficher la transition**: identifier les cours disponibles, énumérer ≤ k sous-ensembles.
4. **Élagage des discussions**: prendre tout lorsque `m <= k`, utiliser la combinaison prégénération.
5. **Énoncer la complexité** en mots (O(2n C(n,k))) et en nombres (1 M ops).
6. **Écrire le code** (de préférence itératif pour C++/Java, récursif avec mémo en Python).
7. **Demander des questions**: Que faire si k étaient 1? Peut-on paralléliser?
8. **Cas de bord de lumière**: "relations" vides, tous les cours indépendants, etc.
8. **Essais de concentration**: test sur les exemples fournis, peut-être un harnais de test aléatoire.

---

- Oui. 10. Réflexions finales

- L'approche **DP‐bitmask** est *propre, optimale et s'inscrit parfaitement dans les limites données*.
- **Les détails de mise en œuvre** (combinaison de dénombrement, `m <= k` raccourci) sont essentiels pour passer la limite de 1 seconde.
- **Communiquer l'idée** est plus important que de fournir un extrait de code parfait ; les intervieweurs cherchent *processus réfléchis*.

---

#### 10-Deuxième explication (pour une récapitulation rapide)

> * Nous utilisons un bitmask pour représenter quels cours sont terminés. Pour chaque masque, nous trouvons tous les cours qui peuvent être suivis (pas de prérequis non satisfait). Si le nombre de ces cours est ≤ k, nous les prenons tous (pas de branchement). Sinon, nous essayons chaque sous-ensemble de ces cours de taille jusqu'à k, mettons à jour le masque et les prérequis, et récursons. Nous mémorisons les semestres minimums pour chaque masque. Complexité: O(2n C(n,k)), avec n = 15 → environ un million d'opérations.

---

10 ans. Mot final

- **Conservez le code lisible** – les intervieweurs préfèrent les solutions propres aux astuces trop intelligentes.
- ** Expliquez votre raisonnement** – il renforce la confiance.
- **Pratique**: passer à travers quelques cas de test aléatoire sur votre machine pour vérifier l'exécution.
- **Deploy**: une fois confiant, poussez le code à Leetcode et soumettez.

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---

11 ans. SEO & Mots-clés (pour votre blog)

- Nombre minimum de semestres codant la solution d'entretien
- Problème de programmation des cours de bitmask
- Leetcode 1850 nombre minimum de semestres solution
- Tri topologique avec sous-ensembles DP
- Masque Python lru_cache DP
- Énumération du sous-ensemble __construitin_popcount
- L'explication d'entrevue DP indique les transitions mémorisation

> *Ces mots clés aident votre classement d'article pour les utilisateurs de Leetcode et les candidats d'entrevue. *

---

*Codage heureux, et bonne chance sur votre prochaine interview!*