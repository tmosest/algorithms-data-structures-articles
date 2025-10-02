---
titre: LeetCode 952. Taille de la plus grande composante par facteur commun - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 952. Taille de la plus grande composante par facteur commun

**Récapitulation des problèmes* *

Avec un tableau "nums" de nombres *uniques* positifs, construisez un graphique non dirigé où chaque nombre entier est un nœud.
Un bord existe entre deux nœuds `a` et `b` **iff** "gcd(a, b) > 1".
Retourne la taille du plus grand composant connecté.

**Pourquoi Union-Find + Prime-Factorisation?**

- Chaque entier peut être représenté par l'ensemble de ses principaux facteurs.
- Deux numéros sont connectés exactement quand ils partagent au moins un facteur principal.
- Oui. Si nous traitons chaque prime comme un nœud virtuel et unions chaque entier avec chacun de ses principaux facteurs, alors tous les entiers qui partagent n'importe quel facteur finiront dans le même ensemble DSU.
- Oui. La plus grande taille d'ensemble est la réponse.

Vous trouverez ci-dessous des solutions complètes, prêtes à composer en **Java, Python et C++**.

---

## Solution Java (DSU + HashMap)

"Java
Importation de java.util.*;

solution de classe publique {

- Oui. Union–Find (Union de l'ensemble disjoint) ---------- */
classe statique privée DSU {
Int[] parent;
taille int[];

DSU(int n) {
parent = nouveau int[n + 1];
taille = nouvelle int[n + 1];
pour (int i = 0; i <= n; i++) {
parent[i] = i;
taille[i] = 1;
}
}

int find(int x) {
si (parent[x] != x) parent[x] = find(parent[x]);
retour du parent[x];
}

Union nulle(int a, int b) {
int pa = find(a), pb = find(b);
si (pa == pb) retourne;
si (taille[pa] < taille[pb]) { // union par taille
int tmp = pa; pa = pb; pb = tmp;
}
parent[pb] = pa;
taille[pa] += taille[pb];
}
}

- Oui. Solution principale
public int plus grandComponentSize(int[] nums) {
int max = Arrays.stream(nums).max().ouElse(1);
DSU dsu = nouveau DSU(max);

// Union chaque nombre avec tous ses principaux facteurs
pour (int num : nombres) {
int n = nombre;
pour (int p = 2; p * p <= n; p++) {
si (n % p == 0) {
dsu.union(num, p);
pendant que (n % p == 0) n /= p; // supprimer complètement ce facteur primaire
}
}
si (n > 1) { // n est une prime > sqrt(original)
dsu.union(num, n);
}
}

// Nombre de composants
Carte <entier, entier> cnt = nouveau HashMap<>();
réponse int = 0;
pour (int num : nombres) {
racine int = dsu.find(num);
int sz = cnt.get OuDéfaut(racine, 0) + 1;
cnt.put(racine, sz);
réponse = Math.max(réponse, sz);
}
réponse de retour;
}
}
«» "

**Complexités* *

Opération Temps Espace
- C'est quoi ?
Factorisation de tous les nombres ( pire cas)
DSU ops.
Dénombrement Autres

Les tableaux DSU ("parent", "size") sont dimensionnés `max(nums)+1`, s'adaptant confortablement à la mémoire pour les limites données (`max(nums) ≤ 10^5`).

---

## Solution Python (Union-Trouver + Section de première instance)

'`python
de collections importer par défautdict
importer des maths
importations
sys.setrecursionlimite(10**6)

Classe DSU:
def __init_(self, n: int):
auto-parent = list(range(n + 1))
taille de soi = [1] * (n + 1)

def find(self, x: int) -> Int:
si soi-même. parent[x] != x:
Self.parent[x] = self.find(self.parent[x]) # compression du chemin
Revenez vous-même. parent[x]

def union(self, a: int, b: int):
ra, rb = self.find(a), self.find(b)
si rb: retour
si self.size[ra] < self.size[rb]: # union par taille
Le nombre d'heures de travail est égal à celui des heures de travail.
auto.parent[rb] = r
self.size[ra] += self.size[rb]


Solution de classe:
def le plus grandComponentSize(self, nombres: list[int]) -> Int:
max_val = max(nums)
dsu = DSU(max_val)

# Union chaque nombre avec ses principaux facteurs
pour num in nums:
n = nombre
pour p dans la plage(2, int(math.isqrt(n)) + 1):
si n % p == 0:
dsu.union(num, p)
alors que n % p == 0 & #160;:
n //= p
si n > 1: # facteur principal restant
dsu.union(num, n)

freq = defaultdict(int)
ans = 0
pour num in nums:
racine = dsu.find(num)
freq[root] += 1
ans = max(ans, freq[root])
retour et
«» "

**Heure de lancement**

La même factorisation "O(n·sqrt(max(nums))" domine; les opérations du DSU sont presque constantes.

**Pourquoi Python? **
L'arithmétique grand entier de Python est sûr pour les nombres 32 bits et l'algorithme est entièrement déterministe.

---

## Solution C++ (DSU optimisé)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

struct DSU {
vecteur<int> parent, sz;
DSU(int n = 0) { init(n); }

vide init(int n) {
parent.resize(n + 1);
sz.assign(n + 1, 1);
(parent.begin(), parent.end(), 0);
}

int find(int x) { retour parent[x] == x ? x : parent[x] = find(parent[x]); }

vide unit(int a, int b) {
a = find(a); b = find(b);
si a) b) retour;
si (sz[a] < sz[b]) swap(a, b);
parent[b] = a;
sz[a] += sz[b];
}
};

solution de classe {
public:
Le plus grand ComponentSize(vecteur<int>& nums) {
int mx = *max_element(nums.begin(), nums.end());
DSU dsu(mx);

pour (int x : nombres) {
int n = x;
pour (int p = 2; p * p <= n; ++p) {
si (n % p == 0) {
dsu.unite(x, p);
pendant que (n % p == 0) n /= p;
}
}
si (n > 1) dsu.unite(x, n); //
}

unordered_map<int,int> cnt;
Int ans = 0;
pour (int x : nombres) {
racine int = dsu.find(x);
ans = max(ans, ++cnt[root]);
}
le retour des an;
}
};
«» "

** Faits saillants* *

- Utilise `unordered_map` pour compter la taille des composants – moyenne O(1).
- `dsu.unite` utilise *union par taille* et *compression par voie*.
- La factorisation est efficace car chaque diviseur n'est vérifié que jusqu'à sa racine carrée.

---

## Article du blog : La plus grande taille de composants par facteur commun – Le bon, le mauvais, le mauvais

- Oui. 1. Introduction (SEO: -LeetCode 952 solution, -la plus grande taille des composants, - le graphe de facteur commun)

Problème de LeetCode **952 – Taille de composant la plus grande par facteur commun** vous défie de penser au-delà de la traversée classique du graphique. Vous avez une liste de **unique** entiers positifs, et vous devez construire un graphique non dirigé où deux nombres sont connectés s'ils partagent un facteur principal supérieur à un. L'objectif ? Retourne la taille du plus grand composant connecté.

Ce poste plonge dans le **bon** (ce qui fonctionne magnifiquement), le **mauvais** (pièges communs) et le **ugly** (cases de référence qui voyagent même les ingénieurs chevronnés). Nous terminerons par une mise en œuvre complète et multilingue qui impressionnera les intervieweurs et les chasseurs d'emplois.

---

- Oui. 2. Intuition du problème (Référencement : Intution du graphe du facteur de risque, Code 952 de l'Union)

1. ** La factorisation primaire est la clé** – Deux nombres partagent un bord s'ils partagent au moins un facteur principal.
2. **Traitez les premiers comme des nœuds virtuels Si nous associons chaque entier à tous ses facteurs principaux, tous les nombres qui partagent n'importe quel facteur appartiendront automatiquement au même ensemble DSU.
3. **Plus grande série = réponse** – Après tous les syndicats, la taille du plus grand composant DSU donne la taille requise.

---

- Oui. 3. Pourquoi Union-Find (DSU) est l'endroit doux? (SEO: DSU pour LeetCode, algorithme de recherche de l'union)

Pourquoi ça compte pour 952
- C'est quoi ?
**Syndicat et recherche proches** La factorisation (le pire cas "O(sqrt(max(nums)))") est le goulot d'étranglement; les opérations DSU sont pratiquement libres. Autres
Autres **Aucun besoin de listes explicites d'adjacence**. Le graphique peut avoir jusqu'à ~10^10 bords (le pire cas `gcd` entre chaque paire). DSU nous permet d'effondrer le graphique implicitement. Autres
**Supporte l'union en fonction de la taille/du rang de l'unité + la compression du chemin de l'unité** Autres

---

- Oui. 4. Le Bon – Quoi est élégant?

- **Dénombrement linéaire des composants** – Une fois les syndicats terminés, un seul passage sur `nums` plus une carte de hachage vous donne la taille des composants dans O(n).
**Efficacité de la mémoire** – Même si nous attribuons des tableaux de taille `max(nums)+1`, les limites (`max(nums) ≤ 10^5`) rendent cela trivial.
- **Pas de soucis de profondeur de récursion** – le DSU est itératif `find` (ou arrière-récursif en Python) nous assure de rester en dessous des limites de la pile.

---

- Oui. 4. Les mauvaises – Pièges communs (Référencement :

Piège Explication
- C'est quoi ?
**Utiliser la ligne « gcd » pour chaque paire** temps est impossible pour `n = 10^4`. Remplacer « gcd » par « union entre facteurs principaux ». Autres
**N'enlevez pas les facteurs principaux dupliqués**= `alors que (n % p == 0) n /= p;` manquant → syndicats redondants, plus grand tableau DSU, mémoire supérieure. Toujours démêler un facteur principal complètement. Autres
**Taille du DSU Wrong**= Initialiser le DSU avec `max(nums)+1` mais oublier d'inclure `+1` → erreurs off-by-one.== `DSU dsu(max_value);` où les tableaux sont `n+1`. Autres
**Utiliser `sqrt(n)` par nombre** sans maths entiers** peut déborder sur de très grands ints; utiliser `math.isqrt(n)` ou `int(math.isqrt(n)'. Autres

---

- Oui. 4. L'Ugly – Quirks de bord de cas (SEO: LeetCode 952 cas de bord de cas de facteur de risque)

- **Grandes primaires** – Si un nombre est lui-même un premier («> sqrt(original)») nous devons l'unir à ce premier.
- **Les nombres qui sont des pouvoirs d'un premier** – Exemple: `8 (2^3)` – assurez-vous que vous unissez une seule fois avec `2` (union par taille gère les duplicatas).
- **Très petits tableaux** – Si `n == 1`, la réponse est évidemment `1`.
- **Limites d'entrée** – `max(nums)` jusqu'à `10^5` est sûr pour les tableaux, mais peut souffler la mémoire si vous sur-allotez (par exemple, utiliser `10^7` juste parce que vous pensez qu'il est assez grand).

Le traitement de ces cas transforme correctement un algorithme propre en une solution *proof-bullet*.

---

- Oui. 5. Mise en œuvre multi-langue (Référencement : solution de Java pour le LeetCode 952, Python 3 LeetCode 952, C++ 952 LeetCode)

Voir les blocs de code ci-dessus pour les solutions Java, Python et C++ qui suivent le modèle exact décrit :

1. Trouver "max(nums)" → Taille du DSU.
2. Pour chaque numéro, trier jusqu'à `sqrt(n)' pour extraire les premiers.
3. "dsu.union(num, prime)".
4. Compter la taille de chaque racine DSU et retourner le maximum.

N'hésitez pas à copier ces extraits dans vos propres projets ou notes d'entrevue. Ils compilent les résultats en dehors de la boîte, réussissent les tests officiels et sont entièrement documentés.

---

- Oui. 6. Liste de contrôle des essais (Référencement :

Autres Essai Que vérifier
-- -- -- -- -- --
De petits tableaux aléatoires "n = 5`–`10` → graphe de force brute + DFS vs. DSU. Autres
Autres Tous les nombres sont des nombres premiers distincts. Autres
Autres Tous les nombres partagent un premier commun (par exemple, tous les mêmes)
Un mélange de nombres monoprimes et de nombres composites. Autres
De grandes entrées (`n = 10^4`, `max(nums)=10^5`)" Temps d'exécution < 1 s sur des machines d'entretien typiques. Autres

---

- Oui. 7. Que souligner dans une entrevue?

- ** Expliquez le truc des nœuds virtuels Ça montre que vous comprenez les maths sous-jacents.
- **Discuse l'optimisation du DSU** – Compression du chemin + union‐par‐dimension.
- **Analyse de la complexité des concentrations** – Les intervieweurs aiment un modèle de coût clair.
- **Afficher que vous pouvez le coder en plusieurs langues** – Démontre l'adaptabilité et la compréhension profonde.

---

- Oui. 8. Pensées finales

LeetCode 952 peut sembler un puzzle graphique à première vue, mais une fois que vous voyez **facteurs primaires** comme connecteurs et **DSU** comme un opérateur d'union magique, la solution devient presque inévitable.
Évitez les pièges typiques: ne pas utiliser pairwise gcd, ne pas oublier de dédoubler les premiers, et toujours tailler votre DSU correctement.

Avec les extraits Java, Python et C++ ci-dessus, vous êtes entièrement équipé pour relever ce défi dans n'importe quel entretien de codage ou bootcamp. Bonne chance – et le codage heureux!

---

**Mots clés (pour les recruteurs et les demandeurs d'emploi)* *
`LeetCode 952 solution`, `plus grande taille de composants`, `common factor graph`, `Union-Find`, `DSU`, `prime factorisation`, `algorithme analyse`, `Java Python C++ LeetCode`, `interview de codage`.