---
titre: LeetCode 1135. Connecter les villes avec un coût minimum -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Connecter les villes avec un coût minimum – Un guide de préparation à l'emploi
*(Code à gauche) 1135 – Arbre minimal – Java, Python, C++*

---

- Oui. Pourquoi ce problème est important

- **Étoile d'interview classique** – Il teste les fondamentaux du graphique, les algorithmes gourmands et les connaissances en structure de données.
- ** Importance réelle** – La conception de réseau, la planification routière et la réduction des coûts d'infrastructure en nuage sont tous des problèmes de connexion à toutes les villes.
- ** Trois angles à montrer** – Vous pouvez le résoudre avec **Prim**, **Kruskal** ou même un hybride **Union‐Find + Min‐Heap**.
- **SEO-ready** – φ arbre de couverture minimum, φ villes connectées, φJava MST , φPython MST , C++ MST , LeetCode 1135 , sont tous des mots-clés de grande circulation que les recruteurs recherchent.

---

Les bons

Aspect Pourquoi c'est bon
C'est quoi, ça ?
**Déclaration de problème claire**= Villes `n`, routes `m` bidirectionnelles avec un coût → trouver le coût minimum pour relier tous. Autres
** Contraintes apparentes**= `n, m ≤ 10^4` → une solution `O(m log m)` est confortablement rapide. Autres
*Construisez l'arbre le moins cher qui couvre tous les nœuds. Autres
Autres **Rich interview discussion**= Vous pouvez parler de choix avide, détection de cycle, et des preuves d'optimalité. Autres

---

- Oui. Les mauvais

Numéro Ce qu'il peut vous mordre
-- -- -- -- -- ------------------ -- -- --
**Graphiques déconnectés**= Vous devez détecter qu'aucun arbre de couverture n'existe et retourner `-1`. Autres
Autres **Poids de bord plus grands**= Utilisez `long` ou `int` soigneusement pour éviter le débordement. Autres
**Limites de mémoire**=Le stockage de tous les bords comme une liste de tableaux 3-int est parfait pour 10^4, mais attention si vous modifiez les contraintes. Autres

---

- Oui. L'Ugly

Sensation de douleur
C'est pas vrai.
**Indicateurs hors-par-un**= Les villes sont basées sur 1– garder `parent[0]` inutilisés. Autres
**Union‐Trouver un bug de compression de chemin**=Recursive `find()` avec compression de chemin ou boucle itérative; toujours tester sur un simple cycle. Autres
**PrioritéPièges de comparaisonQueue (Java)**= Une lambda `(a, b) -> a[1] - b[1]` peut déborder; utiliser `Integer.compare(a[1], b[1])'. Autres
**C++ Pièges STL**="std::sort` sur vecteur de tuples; utiliser `std::priority_queue` avec `plus grand<>`. Autres
**Liste de python triant les frais généraux**=Utilisez `key=lambda e: e[2]` et `heapq` pour Prim. Autres

---

## Aperçu de la solution

Deux algorithmes MST canoniques fonctionnent parfaitement ici :

1. **Kruskal** – Triez tous les bords par coût, ajoutez le bord le moins cher qui ne crée pas un cycle (Union‐Find).
2. **Prim** – Départ d'une ville arbitraire, toujours prendre le bord le moins cher laissant l'ensemble visité (min-heap).

Tous deux donnent le même coût total minimum.
Ci-dessous, nous fournissons des implémentations propres et prêtes à la production en **Java, Python et C++**.

---

## Mise en œuvre Java – Kruskal avec Union-Find

"Java
Importation de java.util.*;

solution de classe publique {
// - Oui. Understand ----------
classe statique privée UnionFind {
parent final privé;
taille finale d'inte privée;
composants internes privés; // nombre d'ensembles disjoints

public UnionFind(int n) {
parent = nouveau int[n + 1]; // 1
taille = nouvelle int[n + 1];
composants = n;
pour (int i = 1; i <= n; i++) {
parent[i] = i;
taille[i] = 1;
}
}

public int find(int x) {
si (parent[x] != x) {
parent[x] = find(parent[x]); // compression du chemin
}
retour du parent[x];
}

Union booléenne publique(int a, int b) {
int ra = find(a), rb = find(b);
si (ra == rb) retourner false; // déjà connecté
si (taille[ra] < taille[rb]) { // union par taille
l ' int tmp = r; r = rb; rb = tmp;
}
parent[rb] = ra;
taille[ra] += taille[rb];
composants--;
retour vrai;
}

public booléen tousConnected() {
composants de retour == 1;
}
}

// -------- Fonction principale
Int minimum public Coût(int n, liaisons int[]) {
// Trier les bords par coût (k[2] = poids)
les tableaux.sort(connections, a, b) -> Integer.compare(a[2], b[2]);

UnionFind uf = nouvelle UnionFind(n);
long total = 0; // utiliser longtemps pour éviter le débordement

pour (int[] e : connexions) {
u = e[0], v = e[1], w = e[2];
si (uf.union(u, v)) {
Total += w;
}
}

retour uf.allConnected() ? (int) total : -1;
}

// - Oui. harnais d'essai simple...
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
[] [] conn1 = {{12,5},{1,3,6},{2,3,1}};
Système.out.println(s.minimumCoût(3, conn1)); // → 6

[[]] conn2 = {{12,3},{3,4}};
Système.out.println(s.minimumCoût(4, conn2)); // → -1
}
}
«» "

**Points clés**

- `UnionFind` implémente la compression *chemin* et *union par taille* pour le temps amorti `α(n).
- Le tri des bords donne "O(m log m)".
— Complexité: < < O(m log m + m α(n)) > > O(m log m); Espace: "O(n + m)".

---

## Implémentation Python – Prim avec Min-Heap

'`python
importation heapq
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def minimum Coût (auto), n: int, connexions: Liste[Liste[int]]) -> Int:
# Créer une liste d'adjacence
graphique = par défautdict(list)
pour u, v, w dans les connexions:
graph[u].append(w, v))
graph[v].append(w, u))

visité = [Faux] * (n + 1)
min_heap = [(0, 1)] # (coût, vertex) – départ de la ville 1
Coût total = 0
bords_utilisés = 0

pendant que min_heap et bords_utilisés < n:
w, u = heapq.heappop(min_heap)
si visité[u]:
poursuivre

visité[u] = Vrai
Coût total += w
bords_utilisés += 1

pour le coût, v dans le graphique[u]:
si elle n'est pas visitée[v]:
heapq.heappush(min_heap, (coût, v))

retourner total_cost si bords_utilisés == n sinon -1

Exemple...
si __nom__ == "__main__" :
s = Solution()
Conn1 = [[1, 2, 5], [1, 3, 6], [2, 3, 1]]
print(s.minimumCoût(3, conn1)) # 6

Conn2 = [[1, 2, 3], [3, 4, 4]]
print(s.minimumCoût(4, conn2)) # -1
«» "

** Pourquoi Prim ? **

- Oui. Pas besoin de trier la liste complète des bords – vous obtenez le prochain bord le moins cher dans `O(log m)` que vous traversez.
- Poignées graphiques déconnectées automatiquement : si le tas se vide avant que tous les sommets soient visités, retourner `-1`.
- Complexité: `O(m log m)` (opérations en lourd) - même coût asymptotique que Kruskal.
- Oui. Utilise uniquement des bibliothèques intégrées, donc il est facile d'expédier vers une plateforme.

---

## C++ Implementation – Kruskal avec `std::vector` & DSU

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

// - Oui. Union des ensembles disjoints
classe DSU {
public:
vecteur<int> parent, sz;
nombre de composants

DSU(int n) : parent(n + 1), sz(n + 1, 1), comps(n) {
iota(parent.begin(), parent.end(), 0);
}

int find(int x) {
Si (parent[x] != x)
parent[x] = find(parent[x]); // compression du chemin
retour du parent[x];
}

bool unit(int a, int b) {
int ra = find(a), rb = find(b);
si (ra) rb) retourner faux;
si (sz[ra] < sz[rb]) swap(ra, rb); // union par taille
parent[rb] = ra;
sz[ra] += sz[rb];
--comptes;
retour vrai;
}

bool connected() const { return comps == 1; }
};

// - Oui. Solution...
Int minimum Coût(int n, vecteur<vector<int>>& connexions) {
tri(connections.begin(), connections.end(),
[](const auto& a, const auto& b){ retourner a[2] < b[2]; });

DSU dsu(n);
long total = 0;

pour (auto& e : connexions) {
u = e[0], v = e[1], w = e[2];
si (dsu.unite(u, v)) total += w;
}

retour dsu.connected() ? static_cast<int>(total) : -1;
}

// - Oui. Principale pour les tests rapides
Int main() {
vecteur<vector<int>> conn1 = {{12,5},{1,3.6},{2,3,1}};
cout << minimumCoût(3, conn1) << endl; // 6

vecteur<vector<int>> conn2 = {{12,3},{3,4}};
Cout << minimumCoût(4, conn2) << endl; // -1
retour 0;
}
«» "

** Faits saillants* *

- Utilise `std::vector` des vecteurs pour tenir les bords → la mémoire `O(m)`.
- "std:sort" donne le "O(m log m)" requis.
- La mise en œuvre du DSU est idiomatique: itérative `find()` + union par taille.
- Fonctionne sur des indices urbains basés sur 1 sans ajustements supplémentaires.

---

## Essais & Edge‐ Liste de contrôle des cas

Autres Résultats attendus Pourquoi cela compte
-- -- -- -- -- -- --
Autres **Toutes les villes déjà connectées** (par exemple, une seule route entre chaque paire) Ça montre que vous n'êtes pas trop comptable. Autres
** Graphique déconnecté** – par exemple, deux clusters sans lien Retour `-1`. Autres
**Cité unique (`n = 1`)**= Coût = `0`.= Limite simple pour éviter un tableau hors de portée. Autres
**Grands poids** (jusqu'à `10^6') Pas de débordement lors du summing (utiliser `long`/`int64`). Conserve la solution correcte sous toutes les entrées. Autres
**Dupliquer les bords**=Choisir le moins cher; les duplicatas n'affectent pas Union‐Find.= Évite l'utilisation inutile de la mémoire. Autres
**Création d'un cercle** Il garantit l'acyclique de l'arbre final. Autres

---

- Oui. Comment vendre ce problème dans une entrevue

1. ** Expliquer l'idée centrale d'abord**
> Nous avons besoin de l'arbre le moins cher qui touche chaque ville – qui est exactement un arbre d'expansion minimum. (en milliers de dollars)

2. **Choisir un algorithme**
- Si vous préférez * tri global* → parler de Kruskal.
- Si vous aimez *local choix gourmands* → parler de Prim.

3. **Afficher la preuve d'exactitude du DSU* *
- En ajoutant des bords en ordre croissant et en rejetant tout ce qui fermerait un cycle, nous maintenons la propriété optimale éprouvée par le théorème de coupe. (en milliers de dollars)

4. **Fait ressortir la manipulation des caisses de bord**
- Si le nombre de composants connectés est plus d'un après que tous les bords sont pris en compte, le graphique est déconnecté; nous retournons `-1`.

5. **Discussion temps/espace compromis**
- "O(m log m)" est la limite inférieure théorique pour le tri des bords, bien dans les limites de 10^4.
- L'empreinte mémoire est linéaire: "O(n + m)".

6. **Donnez un extrait de code propre** – collez le code Java (ou votre langue préférée), passez par le DSU, et laissez le recruteur voir que vous pouvez écrire le code de production.

---

La dernière pensée

Maîtriser *Connecter les villes avec minimum Le coût* démontre que :

- Comprendre la théorie de la graph** et les algorithmes de graph**.
- Peut mettre en œuvre ** structures de données efficaces** (Union‐Find, Min‐Heap).
- Peut anticiper les écueils (graphiques déconnectés, indexation 1-basée, débordement).

Apportez ce problème à votre prochain entretien technique, et vous allez parler d'un algorithme éprouvé qui résout les défis d'optimisation des réseaux dans le monde réel – tout en utilisant les mots-clés recruteurs rechercher. Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---