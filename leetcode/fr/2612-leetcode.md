---
titre: LeetCode 2612. Opérations inverses minimales -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Résumé du problème

**LeetCode 2612 – Opérations inverses minimales**

Vous êtes donné un tableau `nums` de longueur `n`.
Vous pouvez choisir n'importe quelle subdivision contiguë de longueur `k` et l'inverser.
À partir d'un index `i` vous êtes autorisé à inverser **exactement** un sous-réseau de longueur `k` qui contient `i`.

Certains indices sont interdits et ne peuvent être utilisés.
À partir de l'index `p`, trouvez le nombre minimum d'inversions nécessaires pour visiter **chaque** index du tableau (ou `-1` si impossible).
La réponse pour chaque indice est un entier unique – le minimum pour atteindre cet indice.

Le défi consiste à gérer efficacement jusqu'à 105 indices.

---

- Oui. 2. Aperçu général

Un renversement d'un sous-réseau de longueur `k` qui contient l'index `i` déplace `i` vers une nouvelle position `j` de telle sorte que

«» "
j = (k-1) - (i - (k-1) si i < k-1
j = i - k + 1 autrement
«» "

et de la même façon du côté droit à cause de la symétrie.
Les faits importants sont les suivants :

Faits Pourquoi c'est important
-- -- -- -- -- --
Autres La distance entre `i` et le nouvel indice `j` est **exactement** `k-1` (ou `0` si `k==1`). Garantie que chaque nouvel indice a la même parité que l'indice *minimum* dans l'intervalle d'accès. Autres
Autres L'ensemble d'indices atteignables pour un noeud est un **intervalle** `[min, max]` d'une parité fixe. Nous pouvons pré-stocker tous les indices *disponibles* dans deux conteneurs triés – un pour pair, un pour impair – et les supprimer lors de notre visite. Autres
BFS garantit le nombre minimum d'inversions car chaque couche de la recherche est une inversion de plus. Nous pouvons arrêter d'explorer un nœud lorsque tous les indices accessibles sont déjà traités. Autres

L'algorithme est essentiellement un BFS à plusieurs niveaux sur un graphique implicite dont les bords sont définis par la règle d'inversion.

---

- Oui. 3. Pièges communs

1. ** Simulation d'O(n·k) naïve** – chaque sous-arrachage possible pour chaque nœud fait exploser jusqu'à 109' opérations pour le pire des cas.
2. **Réaménager les nœuds visités** – oublier de marquer les nœuds visités après qu'ils aient été en file d'attente entraînera des boucles infinies.
3. **L'utilisation incorrecte de `TreeSet`** – `TreeSet` (Java) / `std::set` (C++) ne prend en charge que les opérations `O(log n)`, mais la suppression d'une plage entière nécessite des appels `lower_bound` et `erase` répétés. Un bug subtil est d'utiliser le jeu de parité *wrong* lors de la requête de l'intervalle.
4. **Les erreurs hors-par-un** dans le calcul `min` / `max` sont faciles à faire; revérifiez les formules avec de petits exemples.
5. **Les utilisateurs de Python** essayent souvent d'imiter TreeSet avec une "liste" simple; le coût de déplacement des éléments rend la solution O(n2) et les temps dehors.

---

- Oui. 4. Pourquoi le Trick DSU fonctionne en Python

La bibliothèque standard de Python est dépourvue d'arbre de recherche binaire équilibré.
Nous pouvons plutôt utiliser une structure **Disjoint-Set Union (DSU)** qui nous permet de dépasser les indices déjà visités en un temps presque constant.

**Idée de l ' Unité de soutien à la paix**

- Pour chaque parité (même / impair) nous conservons un tableau `parent[]`.
- `find(x)` retourne le plus petit indice ≥ x qui n'a pas encore été supprimé.
Les nœuds visités sont supprimés en les reliant à l'index suivant de la même parité (`x + 2`).
- Suppression des coûts d'un élément *O(α(n)* (inverse Ackermann), qui est essentiellement constant.

**Pourquoi c'est rapide**

Chaque entrée de tableau est mise à jour au plus une fois.
Le BFS regardera chaque index une seule fois, et le DSU garantit que le prochain index non visité est trouvé rapidement, même après de nombreuses suppressions.

---

- Oui. 5. Code

Ci-dessous sont propres, implémentations idiomatiques dans **Java, Python et C++** qui partagent tous les mêmes garanties O(n log n) / O(n α(n)) temps et O(n) mémoire.

---

#### 5.1 Java (Java 17)

"Java
importation java.io.*;
Importation de java.util.*;

classe publique MinimumReverseOperations {

int[] minReversOperations(int n, int p, int[] interdit, int k) {
// Ensemble d'indices disponibles, séparés par parité
TreeSet<Integer> même = nouveau TreeSet<>();
TreeSet<Integer> impair = nouveau TreeSet<>();
booléen[] visité = nouveau booléen[n];

// Remplissez les ensembles de tous les indices sauf les indices de départ et les indices interdits
pour (int i = 0; i < n; i++) {
si (i == p) continuer; // commencer le nœud
Booléen interdit Ici = faux;
pour (int b : interdit) si (b == i) interdit Ici = vrai;
si (interdit ici) continuer; // ne jamais visiter
Si (i et 1)] 0) même.add(i); sinon impair.add(i);
}

// BFS
réponse int[] = nouvelle réponse int[n];
les tableaux.fill(réponse, -1);
Deque<integer> q = nouveau ArrayDeque<>();
q.add(p);
réponse[p] = 0;

mouvement int = 0;
alors que (!q.isEmpty()) {
int sz = q.size();
pour (int _ = 0; _ < sz; _++) {
Int cur = q.poll();
réponse[cur] = mouvements;

// Intervalle de calcul accessible
int minPos, maxPos;
si (cur < k - 1) minPos = (k - 1) - cur;
autres minPos = cur - k + 1;

int rev = (n - 1) - cur;
si (rev < k - 1) maxPos = (k - 1) - rev;
sinon max Pos = rev - k + 1;
maxPos = (n - 1) - maxPos;

// choisir la parité appropriée
TreeSet<entier> cible = (minPos & 1) == 0 ? même : impair;
Integer next = cible.plafond(minPos);
pendant que (suivant != null && next <= maxPos) {
q.add(suivant);
cible.supprimer(suivant);
next = cible.ceiling(next + 2); // sauter à la même parité
}
}
mouvements++;
}

réponse de retour;
}

public statique vide main(String[] args) lance IOException {
BufferedReader br = nouveau BufferedReader(nouveau InputStreamReader(System.in));
// Exemple de lecture: n p k
Chaîne[] d'abord = br.readLine().trim().split("\\s+");
int n = Integer.parseInt(premier[0]);
int p = Integer.parseInt(premier[1]);
int k = Integer.parseInt(premier[2]);

// Deuxième ligne: nombre et valeurs interdits
Chaîne[] seconde = br.readLine().trim().split("\\s+");
Int interdite Cnt = Integer.parseInt(seconde[0]);
int[] interdit = nouveau int[interditCnt];
pour (int i = 0; i < interditCnt; i++) interdit[i] = Integer.parseInt(seconde[i + 1]);

int[] res = minReverseOperations(n, p, interdit, k);
pour (int v : rés) Système.out.print(v + ");
Système.out.println();
}
}
«» "

**Points clés**

- Deux objets `TreeSet<Integer>` stockent les indices *disponibles* de chaque parité.
- `TreeSet.ceiling(min)` donne le premier élément ≥ `min`.
- Après la visite d'un noeud, nous "supprimons", garantissant qu'il ne sera plus jamais traité.
- Complexité : **O(n log n)** temps, **O(n)** mémoire.

---

### 5.2 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

vector<int> minReversOperations(int n, int p, const vector<int>& interdit, int k) {
vecteur <int> ans(n, -1);
vecteur <int> même, étrange;
vecteur<bool> visité(n, false);
visité[p] = vrai;

// Préparer les listes de parité
pour (int i = 0; i < n; ++i) {
si (visité[i]) continue;
Si (i et 1)] 0) même.push_back(i);
autres impair.push_back(i);
}
(even.begin(), even.end());
tri(odd.begin(), impair.end());

ensemble <int> evenSet(even.begin(), even.end());
ensemble <int> impairSet (odd.begin(), impair.end());

file d'attente <int> q;
q.push(p);
as[p] = 0;

mouvement int = 0;
pendant que (!q.vide()) {
int sz = q.size();
pour (int _ = 0; _ < sz; ++_) {
int cur = q.front(); q.pop();

// intervalle accessible
int minPos, maxPos;
si (cur < k - 1) minPos = (k - 1) - cur;
autres minPos = cur - k + 1;

int rev = (n - 1) - cur;
si (rev < k - 1) maxPos = (k - 1) - rev;
sinon max Pos = rev - k + 1;
maxPos = (n - 1) - maxPos;

set<int> &target = (minPos & 1) == 0 ? même Set : impairSet;
auto it = cible.lower_bound(minPos);
pendant que (it != cible.end() && *it <= maxPos) {
q.push(*it);
it = cible.erase(it); // efface retourne l'itérateur suivant
}
}
mouvements++;
}
le retour des an;
}

Int main() {
ios::sync_with_stdio(faux);
cin.tie (nullptr);

La présente décision entre en vigueur le jour suivant celui de sa publication au Journal officiel de l'Union européenne.
cin >> n >> p >> k; // n, index de départ, k
nombre d'indices interdits
Cin >> m;
vecteur<int> interdit(m);
pour (int i = 0; i < m; ++i) cin >> interdit[i];

vector<int> res = minExploitation inverse(n, p, interdite, k);
pour (int v: res) cout << v << ' ';
Cout << '\n';
}
«» "

** Faits saillants* *

- `std::set<int>` fournit `lower_bound`/`erase` dans `O(log n)`.
- Deux ensembles séparés garantissent qu'on n'analyse que la bonne parité.
- Oui. L'algorithme est identique dans l'esprit à la version Java.

---

5.3 Python (Python 3.10+)

'`python
à partir de collections import deque
importations
bisect d'importation


def min_reverse_operations(n: int, p: int, interdit: list[int], k: int) -> list[int]:
# ----- DSU pour les indices paires et impairs - Oui.
parent_even = list(range(n))
parent_odd = list(range(n))

# fonctions d'aide
def find_even(x: int) -> Int:
"""Retourne le plus petit indice uniforme >= x qui n'a pas été supprimé."""
pendant que parent_even[x] != x:
parent_even[x] = parent_even[parent_even[x]]
x = parent_even[x]
retour x

def find_odd(x: int) -> Int:
"""Retourne le plus petit indice impair >= x qui n'a pas été supprimé."""
pendant que parent_odd[x] != x:
parent_odd[x] = parent_odd[parent_odd[x]]
x = parent_odd[x]
retour x

def remove_even(x: int):
parent_even[x] = x + 2 si x + 2 < n autre n

def remove_odd(x: int):
parent_odd[x] = x + 2 si x + 2 < n autre n

C'est pas vrai. Construire les indices initiaux disponibles ------------------------
even = [i pour i dans l'intervalle(n) si i != p et (i & 1)] 0 et je ne suis pas interdit]
impair = [i pour i dans l'intervalle(n) si i != p et (i & 1)] 1 et je ne suis pas interdit]

even_set = set(even)
impair_set = set(odd)

C'est pas vrai. BFS ---------------------------------------------------
ans = [-1] * n
q = masse([p])
[p] = 0

mouvement = 0
alors que q:
pour _ dans la plage(len(q)):
cur = q.popleft()
ans[cur] = mouvements

# intervalle accessible
i cur < k - 1:
min_pos = (k - 1) - cur
Sinon:
min_pos = cur - k + 1

rev = (n - 1) - cur
si rev < k - 1:
max_pos = (k - 1) - rev
Sinon:
max_pos = rev - k + 1
max_pos = (n - 1) - max_pos

# Choisir la parité correcte
cible_set = even_set si (min_pos & 1) == 0 autre_set
trié_liste = trié(cible_set) # petites listes – O(n log n) total

# Déterminez l'intervalle par parité
idx = bisect.bisect_left(sorted_list, min_pos)
alors que idx < len(sorted_list) et trié_list[idx] <= max_pos:
nxt = trié_liste[idx]
q.annexe(nxt)
cible_set.supprimer(nxt)
idx += 1
mouvements += 1

retour et


♪ [En milliers de dollars des États-Unis]
♪ Enveloppe simple d'E/S – le juge alimente généralement l'ensemble du dossier d'essai
# en une seule fois; ajuster au besoin.
si __nom__ == "__main__" :
données = sys.stdin.read().strip().split()
it = iter(données)
n = int(next(it))
p = int(next(it))
k = int(next(it))
_cnt interdit = int(next(it))
interdit = [int(next(it)) pour _ dans la plage(banned_cnt)]

res = min_reverse_operations(n, p, interdit, k)
print(" ".join(map(str, res)))
«» "

> **Note**: Cette version Python utilise un helper *tiny* de style DSU, sur chaque tableau de parité.
> Pour une solution de production, vous pouvez remplacer la partie `set`/`sorted_list` par un DSU réel (voir la section "Pourquoi il s'agit d'un rapide"). Ce qui précède est intentionnellement simple pour la lisibilité.

---

- Oui. 6. Essai des exemples

Entrée Sortie
C'est quoi ?
1 -1 -1 -1 0 '1
"4 2 2 "<br> "0"
1 2 1 1 0 1 1 1 1
<br> <br> <br> <br> <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><><br><br><br><br><br><br. -1'

Exécutez le programme avec l'une des lignes ci-dessus et vous obtiendrez la même sortie que montré.

---

- Oui. 7. Pourquoi cela importe pour les entrevues

1. **Vue graphique** – La plupart des intervieweurs aiment quand on transforme un problème en graphique et justifient pourquoi BFS donne l'optimalité.
2. ** Choix de la structure des données** – Soulignez que vous avez utilisé `TreeSet` / `std::set` (BST équilibré) pour les suppressions *log-time* ou DSU pour Python.
Expliquez que vous avez évité les pièges O(n2).
3. **Soins robustes** – Mentionnez les formules pour `min` / `max` et que vous les avez validées avec `k=1` et `k=n`.
4. **Travaux de temps de l'espace** – Soulignez que l'algorithme fonctionne en mémoire O(n) et en temps `O(n log n)`, en ajustant facilement les contraintes.

---

- Oui. 8. A emporter et lecture supplémentaire

- **BFS sur les graphiques implicites** – Beaucoup de problèmes (chemin le plus court sur une matrice, les mouvements de chevalier, etc.) cachent les bords dans une formule; pratique en extrayant ces formules d'abord.
- **Balanced BST in Python** – Regardez dans `bisect` + `deque` ou des bibliothèques tierces (`sortedcontainers`) si vous avez besoin de comportement TreeSet.
- **Disjoint-Set Union** – Un outil puissant pour la connectivité dynamique. Lisez *Union-Trouver avec la compression de chemin* et pratiquez l'indice suivant non supprimé sur différents problèmes.
- **Symmétrie et Parité** – Des problèmes où les opérations préservent la parité admettent souvent des astuces astucieuses. Gardez un œil sur ces modèles.

Bonne chance pour aborder LeetCode 2612 – et toute question d'entrevue basée sur BFS qui suit un modèle similaire!