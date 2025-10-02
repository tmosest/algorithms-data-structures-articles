---
titre: LeetCode 1947. Compatibilité maximale Somme de la note -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Note maximale de compatibilité – une somme complète Guide (Java / Python / C++)

**Méta—Description** –
Découvrez comment résoudre LeetCode 1947 *Compatibilité maximale Sum* en Java, Python et C++.
Obtenez le retour complet, le DP bit-mask et les solutions d'algorithme hongrois + un blog SEO-friendly qui vous aidera à décrocher votre prochain entretien technique.

---

Récapitulation des problèmes

> **Deux matrices binaires `students` et `mentors`.
> **Objectif:** Jumeler chaque élève avec un mentor unique afin de maximiser la somme des scores *compatibilité* (nombre de réponses égales).

> **Constraints**
> * `1 ≤ m, n ≤ 8`
> * Les éléments ne sont que `0` ou `1`.

Parce que `m ≤ 8`, nous pouvons énumérer toutes les possibilités d'appariement (`m!`).
Le défi est de le faire proprement, avec un bon équilibre entre la lisibilité, la vitesse et l'espace.

---

3 approches populaires

Démarche Comment ça marche Complexité Pourquoi ça compte
- C'est quoi ?
**Backtracking**
**Bit-masque DP**=_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
**Algorithme hongrois** Temps linéaire pour plus grand `m`, mais le code est lourd

> **Le --Good** – Backtracking est facile à lire et à implémenter.
> **Le "Bad"** – Il souffle de façon exponentielle et sera temps-out pour le pire cas.
> **Le "Ugly"** – Hongrois est rapide, mais se sent comme une boîte noire et est surqualifié pour "m ≤ 8".

---

# # # # # # Code Snippets

Ci-dessous vous trouverez **trois** solutions de travail complet – une par langue – pour chacune des trois approches.

> **Astuce:** L'aide `compatibilité` ci-dessous est identique dans les trois codes.
> Copiez-le une fois dans votre classe/module et appelez-le où vous en avez besoin.

---

#### 3.1 Java

"Java
// -------- 3.1.1 Aide...
score int privé(int[] a, int[] b) {
c = 0;
pour (int i = 0; i < a.longueur; i++) si (a[i]] b[i]) c++;
retour c;
}
«» "

##### 3.1.2 Retraçage (facile à comprendre)

"Java
solution de classe publique {
Int privé le mieux;

public int maxCompatibilitéSum(int[][] étudiants, int[][] mentors) {
booléen[] utilisé = nouveau booléen[élèves.longueur];
retour(étudiants, mentors, 0, 0, utilisé);
le meilleur retour;
}

privé vide backtrack(int[]] étudiants, int[][] mentors,
Int pos, int curScore, booléen[] utilisé {
si (poss) étudiants.longueur) {
best = Math.max (best, curScore);
retour;
}
pour (int j = 0; j < mentors.longueur; j++) {
Si (!utilisé[j]) {
utilisé[j] = vrai;
backtrack(étudiants, mentors, pos + 1,
curScore + score(étudiants[pos], mentors[j]), utilisé);
[j] = faux;
}
}
}
}
«» "

##### 3.1.3 Bit-mask DP (optimal pour m ≤ 8)

"Java
solution de classe publique {
Compatibilité privée []; // scores précalculés

public int maxCompatibilitéSum(int[][] étudiants, int[][] mentors) {
m = élèves. longueur;
compatibilité = nouvelle int[m][m];
pour (int i = 0; i < m; i++)
pour (int j = 0; j < m; j++)
compatibilité[i][j] = score(élèves[i], mentors[j]);

int[] mémo = nouveau int[1 << m];
Tableau.fill(memo, -1);
retourner dp(0, mémo);
}

privé int dp(int mask, int[] memory) {
int i = Integer.bitCount(mask); // quel élève attribuer à la prochaine
si (i == mémo.longueur) retourne 0; // tous les objets assignés
si (memo[masque] != -1) retourner le mémo[masque];

int best = 0;
pour (int j = 0; j < mémo.longueur; j++) {
si ((masque et (1 << j))) 0) {
best = Math.max (best,
compatibilité[i][j] + dp(mask=1 << j), mémo);
}
}
retourner mémo[masque] = meilleur;
}
}
«» "

---

3.2 Python

'`python
3.2.1 Aide...
def score(a, b):
somme de retour(x) pour x, y en zip(a, b))
«» "

##### 3.2.2 Reprise (facile à comprendre)

'`python
Solution de classe:
def maxCompatibilitéSum(eux-mêmes, étudiants: Liste[Liste[int]], mentors: Liste[Liste[int]]) -> Int:
auto.meilleur = 0
utilisé = [Faux] * len(étudiants)
auto.dfs(étudiants, mentors, 0, 0, utilisé)
Revenez vous-même. le meilleur

def dfs(self, étudiants, mentors, pos, cur, used):
i pos == len(s) :
Self.best = max (self.best, cur)
retour
pour j dans la plage (lent(menteurs):
si elle n'est pas utilisée[j]:
utilisé[j] = Vrai
auto.dfs(étudiants, mentors, pos+1,
cur + score(étudiants[pos], mentors[j]), utilisé)
utilisé[j] = Faux
«» "

##### 3.2.3 Bit-mask DP (Optimal)

'`python
Solution de classe:
def maxCompatibilitéSum(eux-mêmes, étudiants: Liste[Liste[int]], mentors: Liste[Liste[int]]) -> Int:
n = len(étudiants)
compat = [[score(s, m) pour m en mentors] pour s en étudiant]

@lru_cache(Aucun)
def dfs(masque):
i = bin(mask).count('1') # prochain élève
i == n: retourner 0
meilleur = 0
pour j dans la plage(n):
si non (masque >> j) & 1:
best = max(meilleur, compat[i][j] + dfs(masque=1 << j))
le meilleur retour

retour dfs(0)
«» "

---

### 3.3 C++

'`cpp
// -------- 3.3.1 Aide -------
score int(const vector<int>& a, const vector<int>& b) {
c = 0;
pour (int i = 0; i < a.size(); ++i) si (a[i]]. b[i]) ++c;
retour c;
}
«» "

3.3.2 Retour en arrière

'`cpp
solution de classe {
public:
int maxCompatibilitéSum(vecteur<vecteur<int>>& étudiants,
vecteur<vecteur<int>& mentors) {
m = élèves.taille();
meilleure = 0;
used.assign(m, false);
retour (étudiants, mentors, 0, 0);
le meilleur retour;
}

particulier:
int m, meilleur;
vecteur <bool> utilisé;

vide retour (vecteur Const<vector<int>>& s,
vecteur const <vector<int>>& mnt,
C'est la première fois qu'il s'agit d'un problème.
si (pos == m) { best = max(best, cur); retour; }
pour (int j = 0; j < m; ++j) {
Si (!utilisé[j]) {
utilisé[j] = vrai;
retour(s, mnt, pos+1, cur + score(s[pos], mnt[j]);
[j] = faux;
}
}
}
};
«» "

#### 3.3.3 Bit-mask DP

'`cpp
solution de classe {
public:
int maxCompatibilitéSum(vecteur<vecteur<int>>& étudiants,
vecteur<vecteur<int>& mentors) {
n = élèves.taille();
(n, vecteur <int>(n));
pour (int i = 0; i < n; ++i)
pour (int j = 0; j < n; ++j)
compat[i][j] = score(étudiants[i], mentors[j]);

dp.assign(1 << n, -1);
retour resolve(0);
}

particulier:
l'élément n;
vecteur<vecteur<int>> Compat;
vecteur<int> dp;

int solid(int masque) {
i = __constructin_popcount((non signé)mask); // étudiant suivant
si (i) n) retourner 0;
si (dp[masque] != -1) retour dp[masque];

int best = 0;
pour (int j = 0; j < n; ++j)
si (!(masque & (1 << j)))
best = max(meilleur, compat[i][j] + resoudre(masque=1 << j));
retour dp[mask] = meilleur;
}
};
«» "

---

Analyse de complexité

L'approche Temps Espace Remarques
C'est pas vrai.
"O(m)" (pile de récursion)" Fast pour minuscule `m`, impraticable pour 8! = 40320
"O(2^m · m · n)" Avec `m = 8` → `256 · 8 · 8 = 16k` ops
Hongrois Les échelles à `m = 500` facilement mais surtuber ici

Parce que `m ≤ 8`, **Bit‐mask DP** est l'endroit doux: il est rapide, utilise peu de mémoire, et est encore lisible.

---

C'est pas vrai. Les bons, les mauvais, les méchants

Les bons
* **Le retour** est *instantanément compréhensible* – vous essayez littéralement chaque mission.
* Il est parfait pour *interviews éducatives* où l'intervieweur veut d'abord voir votre logique.

- Oui. Les mauvais
* Blow-up exponentiel: même à `m = 8`, la récursion explore 40320 branches.
* Pour un test de résistance plus * ou des cas de test cachés, le DFS peut *timeout*.

- Oui. L'Ugly
* **Le hongrois** se sent comme un bouton -magique : l'algorithme fonctionne, mais l'implémentation est un labyrinthe **10 lignes**.
* Pour les intervieweurs qui voient l'étoile-notation algorithmique, il peut * soulever des sourcils* et * tuer votre score de lisibilité*.

### L'Ugly-but-Fast
* Lorsque `m` saute au-delà de 10, **Bit‐mask DP** commence à devenir la mémoire-faim (`2^10 = 1024` encore très bien, mais `2^20 = 1 048 576` commence à s'étirer).
* Dans ces cas, vous devez passer à *Hungarian* ou *Min‐Cost Max‐Flow*, mais ces bibliothèques sont accompagnées de *coûts de configuration plus élevés* (y compris un bon conteneur STL C++ ou une bibliothèque 3e partie).

---

C'est pas vrai. Conseils d'utilisation du monde réel

1. **Pre-compute scores** – `compatibilité[i][j]` une fois, utiliser partout.
2. **Mémoisation avec bitmask** – `dp[mask]` en Java/C++ ou `lru_cache` en Python.
3. **Itérer sur les bits** – `pour (int j = 0; j < n; ++j) si (!(mask & (1 << j)))' dans C++; utiliser `itertools.combinations` ou des tours de bits dans Python.
4. **Cas d'urgence** – Le code les gère déjà: `m = 1`, `n = 1`, etc.

---

Liste de contrôle de l'entrevue et de la préparation

1. **Comprendre le problème** – articuler que vous êtes assorti de graphiques bipartites avec une matrice de coûts.
2. **Choisir le bon algorithme** – expliquer pourquoi Bit-mask DP est préférable pour `m ≤ 8`.
3. **Ecrire le code propre** – utilisez les fonctions d'aide, commentez vos boucles et gardez les noms variables expressifs.
4. **Test sur l'échantillon** – p.ex.
'`python
s = [[0,1],[1,0]]
m = [[1,0],[0,1]]
print(Solution().maxCompatibilitéSum(s, m)) # → 4
«» "
5. **Exposer la complexité** – montrer le calcul de l'enveloppe pour convaincre l'intervieweur.

---

- Oui. Bonus: Une mise en œuvre hongroise légère (facultative)

Si vous êtes intéressé à voir une implémentation hongroise rapide (travaille pour tous `m`), l'extrait de Python suivant est concis et entièrement dactylographié:

'`python
classe Hongrois:
def __init_(self, cost): # cost[i][j] est la pénalité (plus élevée est pire)
auto.n = len(coût)
Self.u = [0] * (self.n+1)
Self.v = [0] * (self.n+1)
auto.p = [0] * (auto.n+1)
Autoroute = [0] * (self.n+1)
coût autonome = coût

def min_cost(self):
pour i dans la plage(1, self.n+1):
auto.p[0] = i
minv = [float('inf')] * (self.n+1)
utilisé = [Faux] * (self.n+1)
J0 = 0
alors que Vrai:
utilisé[j0] = Vrai
i0 = auto.p[j0]
delta, j1 = flotteur('inf'), 0
pour j dans la gamme(1, self.n+1):
si elle n'est pas utilisée[j]:
cur = auto.cost[i0-1][j-1] - auto.u[i0] - Self.v[j]
si cur < minv[j]:
minv[j], auto.way[j] = cur, j0
Si minv[j] < delta:
delta, j1 = minv[j], j
pour j dans la plage (self.n+1):
si utilisé[j]:
self.u[self.p[j]] += delta
Soi.v[j] -= delta
Sinon:
[j] -= delta
j0 = j1
si self.p[j0]] 0:
pause
alors que Vrai:
j1 = autoroute[j0]
Self.p[j0] = self.p[j1]
j0 = j1
si j0 == 0:
pause
# Résultat
match = [-1]*self.n
pour j dans la gamme(1, self.n+1):
si self.p[j] != 0:
= j-1
total = somme(self.cost[i][match[i]] pour i dans la fourchette(self.n))
retour total
«» "

> **Mais** pour `m ≤ 8` ce n'est pas nécessaire*.

---

## 6.--Enveloppe & Prochaines étapes

1. Choisir **Bit‐mask DP** pour la solution d'entrevue finale.
2. Gardez la "compatibilité" précomputation ; elle est la même pour toutes les langues.
3. Soyez prêt à *expliquer* pourquoi vous avez choisi DP plutôt que DFS.
4. Cas de bord pratique (par exemple, tous les zéros, tous les zéros, `m = n = 8`).

---

### Ressources de bonus

La langue Ce que vous allez apprendre
- C'est quoi ?
[LeetCode 1772 Discussion – Bit‐mask DP](https://leetcode.com/problèmes/maximize-compatibilité-score/discuss/2514872/JavaC%2B%2BPython-Backtracking-Bitmask-DP)
Autres [GeeksForGeeks – Algorithme hongrois](https://www.geeksforgeeks.org/hungarian-algorithm-for-assignments-problème/)

---

C'est pas vrai. Dernier départ

- Pour LeetCode **1772** (ou tout bipartite correspondant à `m ≤ 8`), **Bit-mask DP** est la solution gagnante.
- Gardez le code **clean** – pré-calculer les scores une fois, mémorisez avec `int[]`/`lru_cache`.
- Oui. Dans une entrevue, *expliquez* votre choix : Nous utilisons DP avec un masque 8 bits car 28 = 256 états; il est à la fois rapide et facile à comprendre.

Bonne chance ! C'est ce qu'il a dit.
N'hésitez pas à déposer des questions dans les commentaires ou sur le forum choisi. Bon codage ! (en milliers de dollars)

---


---

* Fin de l'article*
---
Ceci complète le guide complet.