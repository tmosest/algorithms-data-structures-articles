---
titre: LeetCode 2467. Les plus rentables Chemin dans un arbre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 2805 – le chemin le plus rentable dans un arbre
**Une solution complète en Java, Python et C++ + un billet de blog favorable au référencement**

---

- Oui. 1. Le problème (Code Leet 2805)

> ** Signature fonctionnelle**
> ```texte
> plusProfitablePath(edges: List[List[int]], bob: int, montant: List[int]) -> Int
> `` "

Alice commence par le nœud racine `0` d'un arbre enraciné.
Bob commence à un nœud donné `bob` et marche **vers la racine** (node `0`) – chaque étape prend une seconde.
Pendant qu'ils marchent, ils ouvrent tous les nœuds qu'ils atteignent et y ouvrent la porte.
Le *bénéfice* d'un noeud dépend de qui arrive en premier :

Ordre d'arrivée
Il n'y a pas de problème.
Autres Alice d'abord
Bob d'abord Autres
Même heure

Les deux agents s'arrêtent dès qu'ils atteignent un nœud foliaire.
Retourne le bénéfice maximal ** Alice peut collecter** en choisissant le meilleur chemin de feuille à feuille.

*Contrôles*
- `1 ≤ n ≤ 2·104` (n = nombre de nœuds)
- `amount[i]` correspond à un entier signé 32 bits
- `edges` est un arbre valide

---

- Oui. 2. Idées fondamentales

1. **Construisez une liste d'adjacence** pour l'arbre.
2. **Trouver Bobs chemin unique** depuis son nœud de départ jusqu'à la racine.
- Conservez pour chaque noeud le *step* (timestamp) auquel Bob arrive (`bobDepth[node]`).
3. **FDS de la racine** pour Alice.
- À chaque noeud, déterminez combien Alice peut gagner en utilisant le "bobDepth" stocké et sa propre profondeur actuelle.
- Pour les nœuds foliaires, retournez le score accumulé.
- Pour les nœuds internes, explorez récursivement chaque enfant et gardez le score maximum.

L'algorithme fonctionne dans **O(n)** temps et **O(n)** espace auxiliaire.

---

- Oui. 3. Mise en œuvre des références

#### 3.1 Java

"Java
Importation de java.util.*;

classe publique PlusProfitable Voie {
public statique int le plus appropriéPath(Liste<Liste<entier>> bords, int bob, liste<entier> quantité) {
int n = quantity.size();
Liste <liste<entier>> graphique = nouvelle liste <>(n);
pour (int i = 0; i < n; i++) graphe.add(new ArrayList<>());

pour (Liste <entier> e : bords) {
graph.get(e.get(0)).add(e.get(1));
graph.get(e.get(1)).add(e.get(0));
}

// Trouvez le chemin de Bob vers la racine (noeud 0)
int[] bobDepth = nouveau int[n];
les tableaux.fill(bobDepth, -1);
Liste<entier> chemin = nouvelle liste d'array<>();
findPathToRoot(bob, -1, chemin, graphique);
pour (int d = 0; d < path.size(); d++) bobDepth[path.get(d)] = d;

// DFS pour Alice
retour dfsAlice(0, -1, 0, 0, graphique, bobDepth, montant);
}

// backtracking DFS pour collecter le chemin de Bob
Trouvé booléen statique privéPathToRoot(noeud int, parent int,
Liste <entier> chemin, liste<liste<entier>> graphique) {
Si (noeud) 0) retourner true; // atteint racine
pour (int nb : graph.get(node)) {
si (nb) le parent continue;
chemin.add(node);
si (findPathToRoot(nb, noeud, chemin, graphique)) retourne true;
path.size() - 1);
}
retourner faux;
}

// DFS d'Alice – renvoie le bénéfice maximum de ce nœud vers le bas
int privé statique dfsAlice(int node, int parent, int profondeur,
Int curScore, Liste<Liste<entier>> graphique,
Int[] bobDepth, liste<entier> quantité) {
// Mettre à jour le score en fonction des heures d'arrivée
si (bobDepth[node] == -1="bobDepth[node] > profondeur) {
curScore += quantity.get(node);
} sinon si (bobDepth[node] == profondeur) {
curScore += quantity.get(node) / 2;
}

// Si feuille, retournez le score actuel
si (node != 0 && graph.get(node).size() == 1) retour curScore;

int best = Integer.MIN_VALUE;
pour (int nb : graph.get(node)) {
si (nb) le parent continue;
best = Math.max (best,
dfsAlice(nb, noeud, profondeur + 1, curScore, graphique, bobDepth, quantité)
}
le meilleur retour;
}

// Emballage simple pour le test
public statique vide principal(String[] args) {
Liste<Liste<entier>> bords = Liste des
Liste de(0,1), Liste de(1,2), Liste de(1,3)
);
Liste<entier> montant = Liste.de(1,2,3,4);
Système.out.println(principauxPaths (frides, 2, montant)); // Attendu : 4
}
}
«» "

> **Pourquoi ça marche* *
> - `bobDepth[node]` magasins où *l'heure* Bob arrive au "node".
> - En traversant avec profondeur `profondeur`, nous pouvons décider si Alice arrive premier, deuxième ou en même temps.
> - La récursion explore tous les chemins root-to-leaf, en conservant le meilleur score.

---

3.2 Python 3

'`python
de taper l'importation Liste
importations
sys.setrecursionlimite(1 << 25)

Solution de classe:
def mostProfitablePath(
auto, bords: Liste[List[int]], bob: int, quantité: Liste[int]
-> Int:
n = len(montant)
graphique = [[] pour _ dans l'intervalle(n)]
pour u, v dans les bords:
graphic[u].append(v)
graphic[v].append(u)

# La profondeur d'arrivée de Bob sur chaque noeud
bob_profondeur = [-1] * n
chemin = []

def dfs_bob(node: int, parent: int) -> C'est vrai.
en cas de nœud 0:
retour Vrai
pour nb dans le graphique[node]:
si nb == parent:
poursuivre
chemin.append(node)
si dfs_bob(nb, noeud):
retour Vrai
chemin.pop()
Retour Faux

dfs_bob(bob, -1)
pour d, noeud dans l'énumération(chemin):
bob_profondeur[node] = d

def dfs_alice(node: int, parent: int, profondeur: int, ac: int) -> Int:
# ajuster le bénéfice en fonction des heures d'arrivée
si bob_profondeur[node] == -1 ou bob_profondeur[node] > profondeur:
acc += montant[noeud]
elif bob_profondeur[node] == profondeur:
acc += montant[noeud] // 2

# feuille
si noeud != 0 et len(graph[node]) == 1 :
retour

meilleur = -10**18
pour nb dans le graphique[node]:
si nb == parent:
poursuivre
best = max(meilleur, dfs_alice(nb, noeud, profondeur + 1, acc))
le meilleur retour

retour dfs_alice(0, -1, 0, 0)

# Test rapide
si __nom__ == "__main__" :
bords = [[0,1],[1,2],[1,3]]
Montant = [1,2,3,4]
print(Solution().mostProfitablePath(edges, 2, montant)) # 4
«» "

---

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int mostProfitablePath(vector<vector<int>>& bords, int bob, vector<int>& quantity) {
int n = quantity.size();
vecteur<vector<int>> g(n);
pour (auto &e : bords) {
g[e[0]].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

// La profondeur de Bob sur chaque noeud (heure d'arrivée)
vecteur<int> bobDepth(n, -1);
vecteur <int> chemin;
fonction<bool(int,int)> dfsBob = [&](int node, int parent) -> Bool {
Si (noeud) 0) retourner true; // atteint racine
pour (int nb : g[node]) {
si (nb) le parent continue;
path.push_back(node);
si (dfsBob(nb, noeud)) retourne vrai;
chemin.pop_back();
}
retourner faux;
};

dfsBob(bob, -1);
pour (int d = 0; d < (int)path.size(); ++d) bobDepth[path[d]] = d;

fonction<int(int,int,int,long)> dfsAlice = [&](nœud int, parent int, profondeur int,
long et long acc) -> Int {
si (bobDepth[node] == -1="bobDepth[node] > profondeur) {
acc += montant[noeud];
} sinon si (bobDepth[node] == profondeur) {
acc += montant[node] / 2;
}

// feuille
si (node != 0 && g[node].size() == 1) retour (int)acc;

int best = INT_MIN;
pour (int nb : g[node]) {
si (nb) le parent continue;
best = max(meilleur, dfsAlice(nb, noeud, profondeur + 1, acc));
}
le meilleur retour;
};

retour dfsAlice(0, -1, 0, 0);
}
};

// Démo
Int main() {
vector<vector<int>> bords = {{0,1},{1,2},{1,3}};
vecteur<int> montant = {1,2,3,4};
cout << Solution().profitable Path(edges, 2, montant) << endl; // 4
}
«» "

---

- Oui. 4. SEO-Friendly Blog Post

> **Description détaillée**
> Solve LeetCode 2805 Voie la plus rentable dans un arbre avec une solution O(n) DFS.
> Obtenez le code de référence Java, Python et C++, ainsi que des conseils d'entrevue et une analyse de complexité.

---

♪ Chemin le plus rentable dans un arbre – Le LeetCode définitif 2805 Passage à pied

> **Balises clés:** *LeetCode, Chemin le plus rentable, arbre traversant, DFS, question d'entrevue, interview de codage, Python, Java, C++ *

---

Pourquoi ce problème se pose

- **Real interview agrafy:** apparaît sur les interviews technologiques de haut niveau (Google, Amazon, Microsoft).
- **Tree + DP + gourmand** – teste votre compréhension de la première recherche en profondeur et de l'état temporel.
- **Multi-langue** – montre que vous pouvez implémenter la même logique en Java, Python et C++.

---

Récapitulation des problèmes

Alice commence au nœud `0`.
Bob commence au nœud `bob` et marche ** vers la racine**.
Chaque agent profite d'un nœud selon qui arrive le premier.
Les deux s'arrêtent à une feuille.
Rends le maximum de profit qu'Alice peut réaliser.

---

## Stratégie de solution

1. **Liste des dépendances** – construire une fois, O(n).
2. **Le chemin de Bob à la racine** – l'arbre garantit un chemin unique.
- Marchez récursivement de `bob` à `0`, enregistrant la profondeur à laquelle Bob atteint chaque noeud (`bobDepth[node]`).
3. **Alices DFS** – de la racine, suivre sa profondeur actuelle.
- Comparez `profondeur` avec `bobDepth[node]` pour décider du profit à ce nœud.
- Sur les nœuds foliaires, retourner le score accumulé; sur les nœuds internes, explorer tous les enfants et garder le maximum.

L'astuce : *les deux* agents se déplacent à la même vitesse, de sorte que la *profondeur* du noeud dans un DFS correspond exactement au temps écoulé.

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Construire une liste d'adjacence
Bob (n)** (pile de chemin)
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

Dans l'ensemble : **O(n)** temps, **O(n)** espace.
Avec `n ≤ 20 000`, profondeur de récursion ≤ 20 000 – sûr sur la plupart des plateformes modernes (Python: `sys.setrecursionlimit`, C++: `-Wl,--stack` si nécessaire).

---

Pièges communs

Comment éviter
C'est quoi ?
**L'utilisation d'une gamme de booléens pour la visite**. Comme l'arbre a une relation parent-enfant unique, vous pouvez simplement passer le nœud parent au lieu d'un ensemble visité. Autres
**L'arrondissement de la division entière**Le terme `amount[i]` est garanti même lorsqu'il est divisé par 2 dans le même cas, mais l'utilisation de la division entière (`// 2` dans Python, `/ 2` dans Java/C++) est sûre. Autres
**Dépth > Bob's profondeur vs. Bob=S profondeur > profondeur**= Rappelez-vous que `profondeur` est Alice=S distance actuelle de la racine, tandis que `bobDepth` stocke Bob=S arrivée *heure*. Autres
**Détection du noeud Le noeud `0` peut n'avoir qu'un seul voisin mais n'est pas **** une feuille; la condition `noeud != 0 && graph[node].size() == 1' corrige ça. Autres

---

Code complet (toutes langues)

Langue Nom du fichier Faits saillants Autres
- C'est quoi ?
**Java**"MostProfitablePath.java"" utilise `Liste<Liste<Intégre>>` pour l'adjacence, `Arrays.fill`, et `Math.max`. Autres
**Python**="solution.py`=" DFS récursif avec `sys.setrecursionlimit`. Autres
**C++**= `Solution.cpp`= Utilise `vector<vector<int>>` et lambda recursion. Autres

---

- Oui. 5. Conseils d'entrevue

1. ** Clarifier la règle de l'arrêt à la feuille** – Alice et Bob se terminent à la feuille *première* qu'ils frappent.
2. **Énoncer l'hypothèse** que l'arbre est enraciné à « 0 » (par convention).
3. **Exposer le tableau de profondeur de Bob** dans votre réponse – c'est la clé de la solution O(n).
4. **Complexité du comportement** à l'avance; les intervieweurs aiment la concision Big-O.
5. **Cas de bord de discussion**: noeud unique, Bob déjà à la racine, valeurs négatives `amount` (autorisé si votre code les gère).

---

- Oui. 6. Résumé à emporter

Langue Heure Mémoire Remarques
- C'est quoi ?
Java (n) (n) (n) (n) = profondeur de récursion ≤ 20 000 – sécurité si `setRecursionLimit` n'est pas un problème. Autres
Utiliser `sys.setrecursionlimite` pour les grands arbres. Autres
C++= O(n)= O(n)= Pile itérative optionnelle, mais la récursion est plus claire. Autres

> **Ligne de bottom:** L'astuce est de **pré-calculer les temps d'arrivée de Bob** et ensuite de réaliser un DFS *simple* pour Alice qui propage le meilleur score.
> Cela transforme un problème apparemment complexe de deux agents se déplaçant simultanément en un problème classique de chemin maximum *root-to-leaf*.

Bon codage, et bonne chance de briser ce problème LeetCode! C'est ce qu'il a dit