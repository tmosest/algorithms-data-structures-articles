---
titre: LeetCode 3613. Minimiser le coût maximal de la composante -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes

> ** Minimiser le coût maximal de la composante**
> On vous donne un graphique non dirigé relié avec des sommets `n` (`0 ... n‐1`) et des bords pondérés `m`.
> Chaque bord `edges[i] = [u, v, w]` relie `u` et `v` avec le poids `w`.
> Vous pouvez supprimer **any** ensemble de bords, mais après les suppressions le graphique doit contenir **au plus `k` composants connectés**.
>
> *Coût d'un composant* = poids maximal du bord qui reste à l'intérieur de ce composant
> (une composante sans bords a un coût `0`).
>
> **Objectif** – choisissez les suppressions de sorte que le coût de la composante *maximum* sur toutes les composantes soit le plus petit possible.

> Retournez le coût maximal possible.

Contraintes
«» "
1 ≤ n ≤ 5·10^4
0 ≤ m ≤ 10^5
1 ≤ w ≤ 10^6
1 ≤ k ≤ n
Le graphique d'entrée est connecté.
«» "

Le problème est le même que LeetCode 3613 – * Minimiser le coût maximum de la composante*.



-----------------------------------------------------------------------------------

- Oui. 2. Idée de base – Recherche binaire + DSU (Union mixte)

Lorsque nous fixons une valeur candidate `mid`, nous demandons:

> * Pouvons-nous supprimer les bords de sorte que chaque composant restant ait un poids maximal de bord ≤ `mid` et le nombre de composants ≤ `k`? *

Si nous supprimons tous les bords dont le poids est ** strictement supérieur** à `mi`, le graphique restant est celui qui satisfait à la condition de coût.
Compter les composants connectés dans ce graphique est trivial avec un DSU:

1. Commencez par chaque vertex dans son propre ensemble – `components = n`.
2. Procéder à des bords avec un poids <= milieu > dans un ordre ** croissant**.
Chaque fois que nous unissons deux composants précédemment séparés, nous réduisons les "composants" de 1.
3. Dès que `composants ≤ k` nous avons réussi pour ce `mid`.

Parce que `mid` est monotone – si un certain `mid` fonctionne, chaque plus grande valeur fonctionne aussi – nous pouvons binaire-rechercher la réponse:

«» "
faible = 0
haute = poids maximal
alors que faible ≤ élevée:
milieu = (faible + élevé) // 2
si can(mid): # routine DSU décrite ci-dessus
réponse = milieu
haute = milieu - 1 # essayer de le réduire
Sinon:
faible = milieu + 1
réponse de retour
«» "

**Complexités* *

Opération Heure Mémoire
C'est quoi ?
Tri des bords une fois Autres
Chaque "can(mid)" est pratiquement constant. Autres
"O(log maxW)" ("" 20" parce que "maxW ≤ 10^6")

Dans l'ensemble: "O(m log m + m α(n) log maxW" temps, "O(n + m)" mémoire.
Cela satisfait facilement les contraintes.



-----------------------------------------------------------------------------------

- Oui. 3. Mise en œuvre des références

Voici des solutions propres et idiomatiques dans **Java**, **Python** et **C++**.
Tous les trois utilisent la même stratégie binaire de recherche + DSU.

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe {

// -------- Le Mémorandum d'accord...
classe statique privée DSU {
Int[] parent, grade;

DSU(int n) {
parent = nouveau int[n];
rang = nouvelle int[n];
pour (int i = 0; i < n; ++i) parent[i] = i;
}

int find(int x) {
si (parent[x] != x) parent[x] = find(parent[x]);
retour du parent[x];
}

Union booléenne(int a, int b) {
int ra = find(a), rb = find(b);
si (ra) rb) retourner faux;
si (rank[ra] < rank[rb]) parent[ra] = rb;
sinon si (rank[ra] > rank[rb]) parent[rb] = ra;
Autre { parent[rb] = ra; rang[ra]++; }
retour vrai;
}
}
// --------------------------------

Int public int minCost(int n, int[]] bords, int k) {
int m = bords, longueur;
= 0;
pour (int[] e : bords) maxW = Math.max(maxW, e[2]);

// Trier les bords une fois par poids
les tableaux.sort(edges, Comparator.comparingInt(a -> a[2]);

Int low = 0, high = maxW, ans = maxW;
alors que (faible <= haut) {
int milieu = faible + (élevé - faible) / 2;
si (peut (au milieu, n, bords, k, m)) {
ans = milieu;
haute = milieu - 1; // essayer plus petit
} autre {
faible = milieu + 1; // besoin d'une plus grande indemnité de coûts
}
}
le retour des an;
}

canette booléenne privée(int limite, int n, int[]] bords, int k, int m) {
DSU dsu = nouveau DSU(n);
composants int = n;

// seulement les bords dont le poids <= limite est maintenu
pour (int[] e : bords) {
Si la rupture (e[2] > limite); // le repos est trop lourd
si (dsu.union(e[0], e[1]) composants--;
si (composantes <= k) retourne true; // succès
}
composants de retour <= k;
}
}
«» "

**Pourquoi il passe* *

* Tri des bords ("O(m log m)") est fait une fois – réutilisé pour chaque `mid`.
* Dans `can(limit)` nous ne partons que jusqu'à `composants ≤ k`; pour le meilleur candidat cela peut s'arrêter tôt, mais même une analyse complète est toujours `O(m α(n)'.
* La recherche binaire liée `haute` commence au plus grand poids, garantissant que la réponse sera toujours trouvée.



3.2 Python 3

'`python
de taper l'importation Liste

Classe DSU:
def __init_(self, n: int):
auto-parent = liste(range(n))
Self.rank = [0] * n

def find(self, x: int) -> Int:
si soi-même. parent[x] != x:
Self.parent[x] = self.find(self.parent[x])
Revenez vous-même. parent[x]

def union(self, a: int, b: int) -> C'est vrai.
ra, rb = self.find(a), self.find(b)
si rb:
Retour Faux
si self.rank[ra] < self.rank[rb]:
auto-parent[ra] = rb
elif self.rank[ra] > self.rank[rb]:
auto.parent[rb] = r
Sinon:
auto.parent[rb] = r
Self.rank[ra] += 1
retour Vrai


Solution de classe:
def minCost(self, n: int, bords: List[List[int]], k: int) -> Int:
m = len(edges)
max_w = max(w pour _, _, w dans les bords), par défaut=0)

# Trier une fois
arêtes.sort(key=lambda e: e[2])

0, max_w, max_w
alors que lo <= bonjour:
milieu = (lo + hi) // 2
si self._can(mid, n, bords, k):
ans = milieu
Bonjour = milieu - 1
Sinon:
lo = milieu + 1
retour et

def _can(self, limite: int, n: int, bords: List[List[int]], k: int) -> C'est vrai.
dsu = DSU(n)
Comps = n
pour u, v, w dans les bords:
si w > limite:
pause
si dsu.union(u, v):
Comps -= 1
si comps <= k:
retour Vrai
retour comps <= k
«» "

### 3.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

// -------- Le Mémorandum d'accord...
struct DSU {
vecteur <int> parent, grade;
DSU(int n = 0) { init(n); }
vide init(int n) {
parent.resize(n);
rang. assigné(n, 0);
(parent.begin(), parent.end(), 0);
}
int find(int x) {
si (parent[x] != x) parent[x] = find(parent[x]);
retour du parent[x];
}
bool unit(int a, int b) {
int ra = find(a), rb = find(b);
si (ra) rb) retourner faux;
si (rank[ra] < rank[rb]) parent[ra] = rb;
sinon si (rank[ra] > rank[rb]) parent[rb] = ra;
Autre { parent[rb] = ra; ++rank[ra]; }
retour vrai;
}
};
// --------------------------------

solution de classe {
public:
Int minCost(int n, vecteur<vector<int>>& bords, int k) {
int m = bords.dimension();
= 0;
pour (auto& e : bords) maxW = max(maxW, e[2]);

tri(edges.begin(), bords.end(),
[](vecteur Const<int>& a, vecteur Const<int>& b){ retour a[2] < b[2]; });

int lo = 0, hi = maxW, ans = maxW;
pendant que (lo <= bonjour) {
Int milieu = lo + (h - lo) / 2;
si (pouvant (milieu, n, bords, k)) {
ans = milieu;
hé = milieu - 1;
} autre {
lo = milieu + 1;
}
}
le retour des an;
}

particulier:
bool can(int limite, int n,
Const vector<vector<int>& bords, int k) {
DSU dsu(n);
d ' int comps = n;
pour (auto& e : bords) {
si (e[2] > limite) rupture;
si (dsu.unite(e[0], e[1])) {
--comptes;
si (comps <= k) retourne true;
}
}
retour des comps <= k;
}
};
«» "

> **Note** – Les trois solutions utilisent les bords *une fois triés* et une simple recherche binaire.
> Ils compilent dans les environnements les plus courants: `javac 17`, `python3 3.9`, `g++ 11`.



-----------------------------------------------------------------------------------

- Oui. 4. Billet de blog – Comment résoudre LeetCode 3613: Minimiser le coût maximal de la composante

> **Titre** – Comment résoudre le LeetCode 3613 (coût maximal des composants) en Java, Python & C++ – Recherche binaire + DSU expliqué

### 4.1 Introduction

> Dans cet article, vous allez apprendre à fissurer LeetCode 3613 – * Minimiser le coût maximum des composants*.
> Nous allons parcourir le problème, la solution optimale de recherche binaire + DSU, et vous donner un code prêt à copier en Java, Python et C++.
> Que vous soyez en train de vous préparer à une entrevue de codage ou simplement d'affiner vos compétences en théorie graphique, ce post couvre tout ce dont vous avez besoin.

4.2 Pourquoi ce problème est-il important?

- **La taille de la grille avec des contraintes** – un modèle d'entrevue classique.
- **Recherche de motone** – parfait pour la recherche binaire + DSU ou union‐find.
- **Exemple du monde réel** – • Garder les câbles les plus légers, divisés en groupes k au maximum (penser à la conception du réseau, à une infrastructure rentable, etc.).

### 4.3 Marche pas à pas Par

> 1. **Trier tous les bords par le poids (croissant). * *
> 2. **Rechercher la réponse** ('faible = 0', 'haute = maxPoids').
> 3. Pour une valeur intermédiaire "mid":
> - **Supprimer** tous les bords > `mid`.
> - **Couvercle des composants** utilisant un DSU pendant le traitement des bords restants.
> - Si `composants ≤ k` → `mid` est réalisable, essayez une valeur plus petite; sinon, augmentez `mid`.

> 4. Retourner le plus petit "mid".

4.4 Extraits de code

- **Java** – voir [section 3.1] (#31-Java)
- **Python** – voir [section 3.2] (#32-python)
- **C++** – voir [section 3.3](#33-c)

4.5 Analyse de la complexité

Étape Temps Mémoire
C'est pas vrai.
Autres Trier les bords `O(m log m)`= `O(m)` Autres
Autres Une itération de recherche binaire [`can(mid)`)] Autres
Une boucle de recherche binaire
* Total * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

> Les constantes sont minuscules – Ackermann inverse est pratiquement 1 – donc la solution fonctionne confortablement sous 1 s pour les limites.

4.6 Pièges communs et conseils de débogue

Symptôme Cause probable Correction
- C'est quoi ?
Autres Mauvaise réponse pour `k = n` (devrait être 0)=J'ai oublié de permettre que les composants 0-edge soient comptés comme un composant. Dans `can(mid)`, démarrez `components = n` et ne fusionnez jamais les bords vides – vous obtiendrez immédiatement `components= n` → OK. Autres
TLE sur les grandes entrées. Autres
"Réponse incorrecte pour `k = 1`. devrait considérer **tous** bords ≤ `mid`; nous ne nous arrêtons que lorsque `composants <= k`.

### 4.7 FAQ

C'est ce qu'il a dit.
-- -- -- -- -- --
Autres **Pouvons-nous utiliser le DFS au lieu du DSU?**=Le DFS compte les composants dans `O(n+m)` par `mid`. Parce que la recherche binaire ajoute un facteur de `log maxW`, le total devient `O(n+m) log maxW)`, tout de même OK, mais le DSU est plus rapide et plus compatible avec la mémoire pour les grands graphiques. Autres
Autres **Qu'en est-il si les poids sont négatifs?**Le problème indique les entiers non négatifs. Si vous rencontrez des poids négatifs, ajustez le `faible` initial à `minPoids`. Autres
Autres **Y a-t-il une alternative gourmande?**=Un avide =prendre les plus petits bords jusqu'à ce que vous ne puissiez pas fusionner plus de choses, mais il échoue pour tous `k` parce qu'il ne respecte pas la contrainte de groupes `k` maximum=. Autres

À emporter

> La clé pour le LeetCode 3613 est de reconnaître la nature monotone du paramètre de poids de bord autorisé.
> Une recherche binaire sur ce paramètre combinée à une recherche syndicale qui suit efficacement le nombre de composants vous donne la solution la plus rapide et la plus propre.

> Gardez ce modèle dans votre boîte à outils – il apparaît dans des problèmes comme l'arborescence minimale avec des contraintes, la connectivité après les retraits des bords, et même la distance maximale minimale du groupe de K.

---

**Fin de l'article**



-----------------------------------------------------------------------------------

- Oui. 5. Résumé

Nous avons:

1. **Énoncé du problème** – fractionner un graphique pondéré en tout au plus des groupes liés « k » tout en minimisant le bord le plus large conservé.
2. ** Solution optimale** – recherche binaire monotone combinée avec union‐find (DSU).
3. **Proof** – test de faisabilité est monotonique ; la recherche binaire trouve le minimum.
4. **Mise en œuvre** – code complet pour Java, Python, C++ avec analyse temps/mémoire.
5. **Aperçu du blog** – article prêt à publier expliquant l'approche, le code, les pièges et la FAQ.

Ces livrables couvrent tout ce que l'utilisateur a demandé.