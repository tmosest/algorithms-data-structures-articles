---
titre: LeetCode 3544. Subtree Inversion Somme -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes

> **Subtree Inversion Sum** – LeetCode 3544
>
> On vous donne un arbre non dirigé enraciné au nœud 0.
>
> * `edges` – les bords de l'arbre.
>
> * `nums` – valeur stockée dans chaque noeud.
>
> * `k` – la distance minimale qui doit séparer deux nœuds inversés lorsque l'un est un ancêtre de l'autre.
>
> Lorsqu'un noeud est *inverté*, les valeurs de **chaque noeud dans son sous-arbre** sont multipliées par −1.
>
> Trouvez la somme maximale de toutes les valeurs de nœuds après avoir effectué un ensemble d'inversions qui obéissent à la règle de distance.

Les contraintes ( `n ≤ 5·104`, `k ≤ 50`) rendent impossible une force brute naïve.
L'observation clé est que la décision Invertir ce sous-arbre ou non n'interagit qu'avec *agents* qui sont au plus `k–1` bords au-dessus – rien de plus loin dans la ligne.
Ça donne un DP propre sur les arbres.



-----------------------------------------------------------------------------------

- Oui. 2. Intuition – PDD 3-D

Nous marchons l'arbre dans un ordre DFS.
Pour chaque noeud `u` nous nous souvenons de deux choses:

paramètre de signification
C'est pas vrai.
"dist" (`0 ... k‐1`) Combien de bords restent jusqu'à ce que nous soyons autorisés à inverser à nouveau **dans le sous-arbre de `u`.
Si "dist" Nous ne pouvons pas l'inverser. Si `dist = 0` nous pouvons choisir d'inverser `u` ou non. Autres
Le signe que les valeurs du sous-arbre enracinées à `u` portent actuellement à cause des inversions effectuées **ci-dessus** `u`.
Si un ancêtre supérieur était inversé, tous ses descendants ont le signe opposé. Autres

`dp[u][dist][sign]` – la somme maximale réalisable de tout le sous-arbre de `u`
sous ces deux contraintes.

Transitions:

«» "
si dist > 0 // inversion de u est interdite
résultat = signe * nombres[u] + dp[enfant][dist-1][sign]
Sinon // dist == 0, nous pouvons décider
// 1) ne pas inverser u
pas Invert = signe * nums[u] + dp[enfant][0][signe]
2) invert u
Invert = -sign * nums[u] + dp[enfant][k-1][-sign]
résultat = max (non inversé, inversé)
«» "

Le boîtier de base est une feuille: les mêmes formules fonctionnent encore parce que la boucle sur les enfants est vide.



-----------------------------------------------------------------------------------

- Oui. 3. Preuve d'exactitude

Nous prouvons que l'algorithme renvoie la somme maximale possible.

Lemma 1
Pour tout noeud `u`, tout dist (0,0dist<k)` et tout signe`, `dp[u][dist][sign]` est égal à la somme maximale qui peut être atteinte à l'intérieur du sous-arbre de « u » tout en respectant

* la règle de distance pour les inversions à l'intérieur du sous-arbre, ** et**
* le fait que toutes les valeurs en dehors du sous-arbre ont déjà le signe global.

**Prof.**

Induction sur la hauteur du sous-arbre.

*Base (feuille). *
Le sous-arbre d'une feuille ne contient que le noeud `u`.
Si `dist>0` la feuille ne peut pas être inversée, la seule somme possible est `sign·nums[u]`.
Si `dist=0`, la feuille peut être inversée ou non – l'algorithme choisit la plus grande de `sign·nums[u]` et `-sign·nums[u]`.
Ainsi, l'entrée du tableau est égale à l'optimum.

*Étape d'initiation. *
Supposons que le lemma tient pour tous les enfants appropriés de "u".
Lorsque `dist>0`, aucun noeud à l'intérieur du sous-arbre `u` ne peut être inversé (par définition de `dist`), de sorte que la somme optimale est simplement la somme des sommes optimales des enfants avec le même `dist-1` et le `sign` inchangé.
Par hypothèse d'induction chaque enfant contribue à sa somme optimale, donc l'algorithme calcule le total optimal.

Lorsque `dist=0`, nous pouvons soit laisser `u` inchangé ou l'inverser.
Dans les deux cas, la valeur optimale pour chaque sous-arbre enfant reste la valeur optimale avec la paire correspondante `(dist, signe)`:
* sans inversion: les enfants obtiennent `dist=0` et le même `sign`;
* avec inversion: les enfants obtiennent `dist=k-1` et retournent `sign`.
Par hypothèse d'induction chaque enfant contribue sa valeur optimale pour la paire choisie, de sorte que l'algorithme `max` choisit l'optimum global.

Ainsi, le lemma tient pour "u".



Lemma 2
`dp[0][0][+1]` équivaut à la somme maximale réalisable de l'arbre entier.

**Prof.**

Le nœud 0 est la racine, donc aucune inversion de l'ancêtre ne l'influence → global `sign = +1`.
La première inversion possible à la racine est autorisée, donc `dist = 0`.
Par Lemma 1, `dp[0][0][+1]` est exactement la meilleure somme possible pour l'arbre entier. *



- Oui. Théorème
L'algorithme renvoie la somme maximale possible après tout ensemble admissible d'inversions.

**Prof.**

L'algorithme renvoie `dp[0][0][+1]`.
Par Lemma 2 cette valeur égale l'optimum pour l'arbre entier. *



-----------------------------------------------------------------------------------

- Oui. 4. Analyse de la complexité

Poste Coût
- Oui.
Listes d ' adjacissement des bâtiments Autres
Taille de la table DP : `n · k · 2` (5 × 106 pour le pire des cas)
Chaque cellule DP calculée une seule fois
Temps total
"O(n · k)" pour la table DP + listes d'adjacence

Le temps et la mémoire s'adaptent confortablement aux limites de LeetCode.



-----------------------------------------------------------------------------------

- Oui. 5. Mise en oeuvre des références

Vous trouverez ci-dessous des implémentations **Java**, **Python** et **C++** qui suivent la même logique DP.
Les trois codes exposent la même méthode publique :

"Java
sous-arbre public longInversionSum(int[]] bords, int[] nombres, int k);
«» "

'`python
Solution de classe:
def subtreeInversionSum(self, bords: List[List[int]], nombres: List[int], k: int) -> Int:
«» "

'`cpp
solution de classe {
public:
long sous-arbreInversionSum(vecteur<vecteur<int>>& bords, vecteur<int>& nombres, int k);
};
«» "

---


#### 5.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
// dp[node][dist][signIndex] signeIndice: 0 -> +1, 1 -> -1
privé long[][][] dp;
Int. privée k;
Int privé[] les numéros;
Liste privée<entier>[] arbre;

sous-arbre public longInversionSum(int[]] bords, int[] nombres, int k) {
int n = longueur nums;
k = k;
ce.nums = nombres;

// créer une liste d'adjacence
arbre = nouvelle liste de répartition[n];
pour (int i = 0; i < n; i++) arborescence[i] = nouvelle liste d'array<>();
pour (int[] e : bords) {
arbre[e[0]].add(e[1]);
arbre[e[1]].add(e[0]);
}

// initialiser dp avec une valeur sentinelle
dp = nouveau long[n][k][2];
pour (int i = 0; i < n; i++)
pour (int d = 0; d < k; d++)
les tableaux.fill(dp[i][d], Long.MIN_VALUE);

// partir de la racine, pas d'inversion de l'ancêtre, dist = 0, signe = +1
retour dfs(0, -1, 0, 0);
}

// dfs retourne dp[node][dist][signIndex]
privé long dfs(int u, int parent, int dist, int signIdx) {
si [dp[u][dist][signIdx] != Long.MIN_VALUE) {
retour dp[u][dist][signIdx];
}

long signe = (signIdx == 0) ? 1L : -1L;
long noeud Val = signe * nums[u];

long sans = nodeVal; // somme si nous n'invertons pas u (ou ne pouvons pas)
longue avec = Long.MIN_VALUE; // utilisé uniquement en cas de dist==0

// itérer sur les enfants
pour (int v : arbre[u]) {
si (v) le parent continue;
si (distance > 0) {
Sans += dfs(v, u, dist - 1, signeIdx);
} autre {
// enfant lorsque nous n'invertons PAS u
sans += dfs(v, u, 0, signeIdx);
}
}

// Si l'inversion est autorisée (dist.
si (dist) 0) {
longtemps inversés Val = -sign * nombres[u]; // valeur après inversion
longtemps inversés Somme = inversée Val;
int inverse SignIdx = 1 - signeIdx; // signe flip

pour (int v : arbre[u]) {
si (v) le parent continue;
sum inversé += dfs(v, u, k - 1, opposéSignIdx);
}

Sans = Math.max(sans, inverséSum);
}

dp[u]dist[signIdx] = sans;
retour sans;
}
}
«» "

**Notes**

* `signIdx` garde le DP petit – deux signes possibles.
* La valeur sentinelle `Long.MIN_VALUE` garantit qu'une cellule non initialisée est toujours recalculée.
* La fonction retourne un `long` – LeetCode utilise 64-bit pour la réponse.



5.2 Python

'`python
à partir de functools importer lru_cache
de taper l'importation Liste

Solution de classe:
def subtreeInversionSum(self, bords: List[List[int]], nombres: List[int], k: int) -> Int:
n = len(nums)

# liste d'adjacence
g = [[] pour _ dans l ' intervalle n)]
pour a, b dans les bords:
Annexe b)
g[b].appendice(a)

@lru_cache(maxsize=Aucune)
def dfs(u: int, parent: int, dist: int, signe: int) -> Int:
"""
signe : +1 ou -1
dist : 0 .. k-1 (arêtes laissées jusqu'à ce que nous puissions inverser à l'intérieur de ce sous-arbre)
"""
val = signe * nombres[u]
si dist > 0: # inversion interdite
retour val + somme(dfs(v, u, dist - 1, signe) pour v in g[u] if v != parent)

- Oui. 0 – nous pouvons choisir d'inverser ou non
non_invert = valeur
pour v en g[u]:
si v == parent: continuer
not_invert += dfs(v, u, 0, signe)

invert = -val
pour v en g[u]:
si v == parent: continuer
inverser += dfs(v, u, k - 1, -sign)

retour max(not_invert, invert)

retour dfs(0, -1, 0, 1)
«» "

**Pourquoi `lru_cache` fonctionne* *

`dfs` est appelé avec un tuple fixe `(u, parent, dist, signe)` – exactement
les états du tableau DP.
Le cache garantit que chaque état est calculé une fois, de sorte que la complexité reste "O(n·k)".



C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long sous-arbreInversionSum(vecteur<vecteur<int>>& bords,
vecteur <int>& nums, int k) {
int n = nombres.size();
ce->k = k;
ce->nums = nombres;

// liste d'adjacence
arbre.assign(n, {});
pour (auto& e : bords) {
arbre[e[0]].push_back(e[1]);
arbre[e[1]].push_back(e[0]);
}

dp.assign(n, vecteur<vecteur<long>>(k, vecteur<long>(2, LLONG_MIN)));

retour dfs(0, -1, 0, +1);
}

particulier:
vecteur<vecteur<int>> arbre;
vecteur<vecteur<vecteur<vecteur<long>>> dp;
Int k;
vecteur<int> les numéros;

long dfs(int u, int parent, int dist, int signe) {
long &res = dp[u][dist][signe] -1);
si (res != LLONG_MIN) retourne res;

long cur = (long long)sign * nums[u];

// rassembler les enfants d'abord
vector<long long> childSum(k, 0); // aide n'est pas nécessaire – nous ne faisons qu'itérer

// si dist > 0 l'inversion est interdite
si (distance > 0) {
pour (int v : arbre[u]) {
si (v) le parent continue;
cur += dfs(v, u, dist - 1, signe);
}
res = cur;
} autre { // dist == 0 → nous pouvons inverser ou non
longue pas longtemps Inverser = cur;
pour (int v : arbre[u]) {
si (v) le parent continue;
non inversé += dfs(v, u, 0, signe);
}

long invert = -(long long)sign * nums[u];
pour (int v : arbre[u]) {
si (v) le parent continue;
inverser += dfs(v, u, k - 1, -sign);
}

res = max (non inversé, inversé);
}

retour rés;
}
};
«» "

-----------------------------------------------------------------------------------

- Oui. 6. Billet de blog – Subtree Inversion Sum: Le Bon, le Mauvais, le Ugly

> **[SEO TAGS]** `Subtree Inversion Sum`, `LeetCode 3544`, `DP on Trees`, `Coding Interview`, `Tree Algorithms`, `Algorithm Design`, `Java`, `Python`, `C++`, `Interview Question`, `Interview Preparation "

---

#### 6.1 Crochet – Pourquoi cette question Rocks

Dans une interview de codage typique, l'intervieweur aime *trees* parce qu'il s'agit d'une structure de données du monde réel – vous les voyez dans les systèmes de fichiers, dans les arbres DOM et même dans les organigrammes.
Le subtree Inversion Sum ajoute une torsion: vous pouvez retourner le signe d'une branche entière, mais seulement si vous gardez une distance minimale d'un ancêtre flip.
C'est un grand mélange de la théorie **graph**, **récursion** et **programmation dynamique** – exactement le genre de problème qui transforme un candidat de la moyenne à l'étoile dans un appel d'embauche.

---

#### 6.2 Le bon – Un pur 3-D DP

* **La machine d'état intuitif** – le compteur "dist" se souvient de combien au-dessus nous sommes encore interdits d'inverser, tandis que l'état "sign" garde une trace de la parité globale des inversions au-dessus du nœud actuel.
* **Temps linéaire** – "O(n·k)" n'est qu'environ 2,5 millions d'opérations pour les entrées les plus mauvaises, ce qui est une brise pour tout processeur moderne.
* **Pas de tricks ad-hoc** – l'algorithme ne repose pas sur l'heuristique ou la randomisation; il découle d'une formulation rigoureuse du PDD.

Parce que chaque choix de nœud dépend uniquement de l'état de son parent, le DP est *exactement* un arbre– PDD. C'est pour cela que la solution est simple une fois que vous reconnaissez le fait "look‐ahead" jusqu'aux bords `k–1`.

---

#### 6.3 La mauvaise – Une force de brute flaquée

Une approche naïve pourrait essayer :

1. Énumérer chaque sous-ensemble de nœuds (2n possibilités) et appliquer des inversions.
2. Pour chaque sous-ensemble, vérifiez la règle de distance en marchant chaque paire d'ancêtres.

Les deux étapes explosent exponentiellement. Même avec la taille, l'explosion combinatoire de l'inversion de tout sous-arbre est intractable pour `n = 5·104`.
Les gens pensent parfois que parce que l'inversion retourne les signes, on peut tout simplement *gredily* retourner les nœuds de valeur négative – mais cette règle gourmande échoue parce que le fait de retourner un parent nie un sous-arbre *entier** et peut détruire de nombreuses petites valeurs positives.

---

### 6.4 Le mauvais – Manipulation des panneaux et des distances

La mise en œuvre correcte du PDD n'est pas -trivial, mais il est *gérable*:

* **Sign bookkeeping** – vous devez vous rappeler si un ancêtre a été inversé. Un moyen propre est d'encoder le signe comme `0 → +1` et `1 → –1`.
* ** Compteur de distance** – gardez un compteur qui déprime à mesure que vous allez plus loin. Réinitialisez-le à `k–1` après une inversion.
* **Cache / Mémotisation** – car chaque nœud peut être visité pour de nombreuses paires `(dist, signe)`, une table de mémorisation ou une `@lru_cache` en Python est essentielle ; sinon vous recalculeriez des millions de sous-sous-problèmes.

Les formules du noyau de l'algorithme cachent beaucoup de détails algébriques:
`sign * nums[u]` vs `-sign * nums[u]` et les deux enfants différents appellent.
Obtenir les indices et l'ordre de récursion mal est une source courante de bugs.

---

6.5 A emporter – Maître l'État

Lorsque vous vous asseyez dans une entrevue et que vous voyez Subtree Inversion Sum, votre premier instinct devrait être de poser des questions claires:

* Est-ce que `k` est garanti être petit? Cela peut aller jusqu'à `n`, mais nous ne nous soucions que de `k–1`.
Qu'est-ce qu'une inversion fait aux descendants d'un noeud? Il retourne le signe de chaque descendant exactement une fois.

De là vous pouvez définir les états DP, prouver que chaque valeur optimale de nœud dépend seulement de son état parent, puis écrire la fonction récursive.
L'intervieweur va adorer le fait que vous avez transformé une règle apparemment confuse en un DP **mathématiquement sonore**.

---

6.6 Pensée finale – Écrire, tester, répéter

* Écrivez d'abord l'aide récursive (pas encore de mémo).
* Ajouter la table de mémoisation ou `@lru_cache`.
* Tester sur les petits boîtiers artisanaux (`n=4, k=2`) pour s'assurer que le panneau fonctionne.
* Agrandissez et vérifiez par rapport à la solution officielle LeetCode.

Une fois que vous avez fait cela, vous allez non seulement résoudre le problème, mais aussi démontrer une bonne compréhension de la programmation dynamique sur les arbres** – une compétence qui est précieuse dans de nombreux domaines : des services backend aux arbres de décision AI.

---

> **Vous voulez impressionner les recruteurs? * *
> Ajoutez Subtree Inversion Sum à votre portfolio et pratiquez l'approche DP propre en Java, Python ou C++.
> Rappelez-vous : bons algorithmes *regarder propre* – et des algorithmes propres *regarder grand* sur votre CV.

---

**Fin du blog**

---

- Oui. 7. Clôture

Le problème « Subtree Inversion Sum » est un exemple d'une question d'entrevue bien conçue.
Une solution DP propre est à la fois **efficace** et **conceptuellement élégante**.
Que vous le codez en Java, Python ou C++, la même machine d'état sous-tend la logique – la différence est dans les détails d'implémentation et les astuces de mémorisation spécifiques au langage.

Bon codage !