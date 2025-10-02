---
titre: LeetCode 2378. Choisissez les bords pour maximiser le score dans un arbre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2378 – Choisissez les bords pour maximiser le score dans un arbre
**Java-optimized blog post** qui explique le bon, le mauvais, et le laid de ce problème afin que vous puissiez aser votre prochaine interview de codage.

---

Récapitulation des problèmes

On vous donne un arbre **raciné** avec des nœuds `n` (0 ... n‐1).
`edges[i] = [parent_i , poids_i]` (la racine a `[-1,-1]`).

Choisissez un sous-ensemble de bords tel que **aucun bord choisi ne partage un noeud** (c.-à-d. qu'il ne soit pas adjacent).
Maximiser la somme des poids des bords choisis.
Si vous ne choisissez rien, le score est `0`.

> **Exemples**
> 1. `edges = [[-1,-1],[0,5],[0,10],[2,6],[2,4] → 11`
> 2. `edges = [[-1,-1],[0,5],[0,0-6],[0,7]] → 7'

---

- Oui. Pourquoi c'est un problème moyen

* **Structure de l'arbre** – vous ne pouvez pas utiliser l'avidité sur des graphiques arbitraires; vous avez besoin d'un PDD qui respecte la hiérarchie parent‐enfant.
* ** Contrainte d'adhérence** – le choix d'un bord interdit tous ses bords d'incident, donc vous devez vous souvenir si * vous êtes autorisé à choisir un bord pour un enfant.
* **Les grandes solutions n (105)** – O(n2) s'explosent; vous avez besoin de temps linéaire.

---

- Oui. Le point de vue de base – PDD de l'arbre

Considérez chaque nœud comme un point de décision qui peut être dans **deux états**:

Qu'est-ce qui est permis ? Autres
- C'est pas vrai.
Le bord du nœud parent à ce noeud ** n'a PAS été choisi. Vous pouvez choisir un bord de ce nœud à un enfant. Autres
Le bord du nœud parent à ce noeud **a été choisi. Vous *ne pouvez pas* choisir n'importe quel bord de ce noeud à un enfant (le parent a déjà utilisé le noeud). Autres

Pour un nœud «u»:

«» "
skip = somme( enfant[1] ) // nous sautons tous les bords de u à ses enfants
prise = max sur les enfants ( enfant[0] - enfant[1] + poids(u, enfant) )
retour [skip, prendre + skip]
«» "

* `skip`* est le meilleur score quand nous faisons **pas** prendre un quelconque avantage de `u`.
*'take`* est le meilleur *additionnel* score si nous décidons de prendre *exactement un* bord à un enfant (d'où nous comparons tous les enfants).
Enfin nous retournons `[skip, take+skip]` parce que lorsque le parent voit ce noeud, il sera dans l'état de prendre ("skip") et l'état de ne pas prendre est "take+skip".

La réponse pour l'arbre entier est `max(root[0], root[1]).

L'algorithme est **O(n)** temps, **O(n)** mémoire (liste d'adjacence + pile de récursion).

---

## 4--Le code passe – trois langues

> **Astuce**: La même idée fonctionne dans chaque langue. Les seules différences sont la syntaxe et la façon dont nous stockons le graphique.

---

#### 4.1 Java (Java 17+)

"Java
Importation de java.util.*;

solution de classe {
public long maxScore(int[]] bords) {
int n = bords.longueur;
Liste<int[]>[] g = nouvelle liste de distribution[n];
pour (int i = 0; i < n; i++) g[i] = nouveau tableau <>();

racine int = 0;
pour (int i = 0; i < n; i++) {
int p = bords[i][0];
si (p >= 0) {
g[p].add(nouvelle int[]{i, bords[i][1]}); // enfant, poids
} autre {
racine = i;
}
}

long[] res = dfs(root, g); // [peut prendre, ne peut prendre]
retour Math.max(res[0], res[1]); // meilleur score possible
}

privé long[] dfs(int u, Liste<int[]>[] g) {
long skip = 0; // meilleur si nous ne prenons pas un bord de u
longue prise = 0; // meilleur *score supplémentaire* quand nous choisissons un bord

pour (int[] e : g[u]) {
longue[] enfant = dfs(e[0], g);
skip += enfant[1]; // l' enfant doit être en "ne peut pas prendre"
prendre = Math.max(prendre, enfant[0] - enfant[1] + e[1]); // choisir ce bord
}
retour de nouveau long[]{skip, prendre + skip}; // retour des deux états
}
}
«» "

---

#### 4.2 Python (Python 3.10+)

'`python
importations
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def maxScore(self, bords: List[List[int]]) -> Int:
sys.setrecursionlimite(1 << 25)

g = defaultdict(list)
racine = 0
pour i, (p, w) en énumération(s) :
si p >= 0:
g[p].appendice(i, w))
Sinon:
racine = i

def dfs(u: int):
sauter, prendre = 0, 0
pour v, w in g[u]:
enfant_can, enfant_cannot = dfs(v)
skip += enfant_ne peut pas
prendre = max(prendre, enfant_can - enfant_ne peut pas + w)
retour skip, prendre + skip

ne peut pas = dfs(root)
retour max(can, impossible)
«» "

> **Note**: `sys.setrecursionlimit` est nécessaire car `n` peut atteindre 105.

---

### 4.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long long maxScore(vecteur<vecteur<int>>& bords) {
int n = bords.dimension();
vecteur<vector<pair<int,int>>> g(n); // enfant, poids
racine int = 0;
pour (int i = 0; i < n; ++i) {
int p = bords[i][0];
si (p >= 0) g[p].push_back({i, bords[i][1]});
autre racine = i;
}

auto dfs = [&](auto&& self, int u) -> paire <long long,long long> {
long saut = 0, prendre = 0;
pour (auto [v,w] : g[u]) {
auto [child_can, child_cannot] = soi-même, v;
sauter += enfant_ne peut pas;
prise = max(prise, enfant_can - enfant_cannot + w);
}
retour {skip, prendre + skip};
};

auto [peut, ne peut] = dfs(dfs, root);
retour max(can, impossible);
}
};
«» "

---

Analyse de complexité

**Métrique**
- C'est quoi ?
Conjoncture Autres
DFS (une seule passe)

Les deux sont optimales pour les contraintes (`n ≤ 105`).

---

C'est pas vrai. Maîtrise de cas

*Cas** **Pitfall**
C'est pas vrai.
**Tous les poids négatifs**=Le retour de nombres négatifs peut être erroné si vous ne vous souvenez pas de =0 est toujours autorisé==Le DP prend automatiquement `max(0, ...)` par `skip = 0`. Autres
**Profondeur > Augmentez la limite de récursion (Python) ou utilisez une pile explicite. Autres
Autres ** Arbre très dense (beaucoup d'enfants) ** La boucle sur les enfants reste linéaire parce que chaque enfant est visité exactement une fois. Pas de frais supplémentaires. Autres
**Poids plus importants (jusqu'à 109)**= Utiliser `long long`/ `long`= Même que ci-dessus. Autres

---

## 6-

1. **Miss-interpreter "Adjacent"** – Les gens pensent souvent que seulement *deux* bords ne peuvent être choisis, mais dans un arbre *tous* bords qui touche un choix est interdit.
2. **Oublier la racine** – Si vous construisez le graphique avec de mauvaises directions, vous finirez par ramasser un bord qui est déjà pris par son parent.
3. **O(n2) gourmand** – Essayer de trier les bords par le poids et cueillir avec cupidité échoue sur un graphique stellaire.
4. **Débordement de la pile** – De nombreux intervieweurs lancent le code avec 105 nœuds; une récursion naïve en Java/Python peut atteindre la limite de la pile.

---

# # # 6 Les bons, les mauvais et les méchants

**Aspect**
C'est pas vrai.
**Efficacité algorithmique**
La paire `[skip, take]` peut se sentir opaque au début.
**Scalabilité**= Fonctionne pour n=105= Nécessite une limite de récursion accrue== Utiliser des listes d'adjacence à tort (par exemple `HashMap<entier, Integer>=) peut gâcher la mémoire
**Robustness**=Poignées de poids négatifs automatiquement=Il faut manipuler avec soin le cas 0‐score== Oublier que le skip== est déjà le meilleur pour =ne peut pas prendre== peut conduire à une mauvaise réponse==

---

## 6=" Conseils pour réussir l'entrevue

1. ** Commencez par un diagramme** – Dessinez l'arbre, marquez la racine et annotez quelques nœuds avec les deux états DP.
2. **Exposer les deux états en tête** – Les intervieweurs aiment vous voir briser le problème en sous-problèmes clairs.
3. **Afficher la formule de transition** – Écrire le pseudo-code du DFS, puis le traduire.
4. **Run à travers un petit exemple** – Passez par le DP sur un arbre de 5 nœuds pour prouver que vous comprenez la mécanique.
5. **Mentionnez la limite de récursion** (Python) ou les options de «tail-recursion / iterative» pour les arbres très profonds.
6. **Discuss cas de bord** – Tout négatif, seul noeud, forme d'étoile, équilibré par rapport à l'arbre biaisé.

---

## 7- Chaleur de référence Feuille

Texte
DP[u] = [skip, prise+skip]
skip = somme(enfant[1]) // skip tous les enfants
prise = max(enfant[0] - enfant[1] + w) // choisir un bord d'enfant
réponse = max(DP[root][0], DP[root][1])
«» "

- **skip** = Node non utilisé par parent
- **Take** = = Node déjà utilisé par parent
- Seulement *un* enfant peut être choisi parce que choisir un bord bloque tous les autres.

---

- Oui. Pensée finale

Ce problème est un exemple de manuel de **tree DP avec des contraintes d'adjacence**.
Si vous pouvez articuler le DP à deux états et le traduire en code, vous allez non seulement résoudre le problème en temps O(n), vous allez également impressionner les intervieweurs avec votre solution *clean*, *correcte* et *well-commented*.

Bonne chance ! C'est ce qu'il a dit.

---