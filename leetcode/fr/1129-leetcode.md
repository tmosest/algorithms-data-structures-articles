---
Titre: LeetCode 1129. Voie la plus courte avec des couleurs alternantes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solution 3-langue à **LeetCode 1129 – Voie la plus courte avec des couleurs alternantes* *

L'objectif : du nœud 0 trouver la distance la plus courte à chaque nœud `x` quand ** aucun deux bords consécutifs ont la même couleur** (rouge bleu).
Si un nœud ne peut être atteint en vertu de cette règle, la réponse est `-1`.

La manière classique est **Breadth‐First Search (BFS)** qui garde la trace de la *dernière couleur de bord utilisée*.

Voici des implémentations propres, prêtes à la copie dans **Java, Python et C++**.

---

#### 1.1 Java (Java 17)

"Java
Importation de java.util.*;

***
* Code Leet 1129 – Voie la plus courte avec des couleurs alternantes
*/
solution de classe publique {

/** enum pour les couleurs de deux bords et un état spécial initial */
Enum privé Couleur { INIT, RED, BLUE }

publiques int[] le plus courtAlternatingPaths(int n, int[] redEdges, int[][] blueEdges) {
// liste d'adjacence: noeud -> liste de (voix, bordColor)
Liste<Liste<int[]>> graphique = nouvelle liste de répartition<>();
pour (int i = 0; i < n; i++) graphe.add(new ArrayList<>());

pour (int[] e : redEdges) graph.get(e[0]).add(new int[]{e[1], Color.RED.ordinal()});
pour (int[] e : blueEdges) graph.get(e[0]).add(new int[]{e[1], Color.BLUE.ordinal()});

int[] dist = nouvelle int[n];
Arrays.fill(dist, -1); // -1 = pas encore visité
dist[0] = 0;

// attente en attente (noeud, dernière couleur)
Deque<int[]> q = nouveau ArrayDeque<>();
q.offre(nouvelle int[]{0, Couleur.INIT.ordinal()});

// visité[node][color] = vrai si nous avons déjà traité cet état
booléen[][] visité = nouveau booléen[n][3];
visité[0][Color.INIT.ordinal()] = vrai;

alors que (!q.isEmpty()) {
[] cur = q.poll();
u = cur[0];
int col = cur[1];
étape int = dist[u] + 1;

pour (int[] edge : graph.get(u)) {
int v = bord[0];
int ec = bord[1];
// nous ne pouvons traverser que si la couleur du bord diffère de celle du dernier
si (ec == col) continue;
si (visité[v][ec]) se poursuit;

visité[v][ec] = vrai;
si (dist[v]) -1) dist[v] = pas;
q.offre(nouvelle int[]{v, ec});
}
}

de retour;
}

/* ----- harnais d'essai rapide ----- */
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
la valeur n = 3;
int[] rouge = les points {0,1}, {1,2}};
[] [] bleu = {};
System.out.println(Arrays.toString(s.shortestAlternativePaths(n, rouge, bleu));
// Attendu : [0, 1, -1]
}
}
«» "

**Complexités* *

Complexité
C'est pas vrai.
**O(n + E)**= Chaque noeud + bord est traité une fois par couleur. Autres
**O(n + E)**= Des tableaux supplémentaires pour l'adjacence, la distance, visité. Autres

---

#### 1,2 Python 3 (≥ 3,8)

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def le plus court Paths alternants(
soi-même,
n: int,
rougeEdges: Liste[Liste[int]],
BlueEdges: Liste[Liste[int]]
-> Liste[int]:
# liste d'adjacence: noeud -> liste de (voix, couleur)
graphique = [[] pour _ dans l'intervalle(n)]
pour a, b dans redEdges: graphique[a].appendice(b, 0) # 0 = rouge
pour a, b en bleuEdges: graphique[a].appendice(b, 1)) # 1 = bleu

dist = [-1] * n
dist[0] = 0

# file d'attente tient (noeud, last_color) last_color = -1 signifie "none"
q = deque([(0, -1)])
visité = [[Faux] * 3 pour _ dans la plage(n)] # 0: rouge, 1: bleu, 2: init
visité[0][2] = Vrai

alors que q:
u, dernier = q.popleft()
étape = dist[u] + 1

pour v, c dans le graphique[u]:
if c == last: # même couleur – skip
poursuivre
si visité[v][c]:
poursuivre
visité[v][c] = Vrai
si dist[v] == - 1 :
dist[v] = étape
q.annexe(v, c))

retour


# --- démo simple -------------------------------------------------
si __nom__ == "__main__" :
sol = Solution()
print(sol.shortestAlternativePaths(3, [[0, 1], [1, 2]], [])
# -> [0, 1, -1]
«» "

**Complexités* *

- Heure: 'O(n + E) '
- Espace: 'O(n + E) '

---

*## 1.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<int> plus court Alternatifs Voies(int n,
vecteur<vecteur<int>>& les rougeurs,
vecteur<vector<int>>& blueEdges) {
// liste d'adjacence: noeud -> liste de (voix, couleur)
vecteur<vector<pair<int,int>>> g(n); // couleur: 0 = rouge, 1 = bleu
pour (auto &e : redEdges) g[e[0]].push_back({e[1], 0});
pour (auto &e : blueEdges) g[e[0]].push_back({e[1], 1});

vecteur<int> dist(n, -1);
dist[0] = 0;

// file d'attente: (noeud, dernière couleur) dernière couleur = -1 -> aucune
file d'attente <pair<int,int>> q;
Le paragraphe 2 est remplacé par le texte suivant:

// visité[node][couleur] – nous utilisons 3 emplacements: 0,12 (2 = init)
vecteur <array<bool,3>> vis(n);
vis[0][2] = vrai;

pendant que (!q.vide()) {
auto [u, dernier] = q.front(); q.pop();
étape int = dist[u] + 1;

pour (auto [v, col] : g[u]) {
si (col == dernier) continuer; // même couleur – interdit
si (vis[v][col]) se poursuit;
vis[v][col] = vrai;
si (dist[v]) -1) dist[v] = pas;
q.push({v, col});
}
}
de retour;
}
};

/* - Oui. Démonstration...
Int main() {
Solution s;
vecteur<vector<int>> rouge = {0,1},{1,2}};
vecteur<vecteur<int>> bleu;
auto ans = s.shortestAlternativePaths(3, rouge, bleu);
pour (int x : ans) cerr << x << '; // 0 1 -1
retour 0;
}
*/
«» "

**Complexités* *

- Heure: 'O(n + E) '
- Espace: 'O(n + E) '

---

- Oui. 2. Article de blog – LeetCode de Master 1129: Chemin le plus court avec des couleurs alternantes

> **Mots-clés**: LeetCode 1129, Chemin le plus court avec les couleurs alternantes, BFS, graphique, Java, Python, C++, entretien d'emploi, défi de codage, algorithme, recherche d'emploi, entretien technique, boost carrière

---

2.1 Introduction

Le problème de chemin le plus court avec les couleurs alternantes est un favori sur la section d'entretien de LeetCode. Il met à l'épreuve deux compétences de base dont les recruteurs se soucient :

1. **Graph traversée** – en particulier BFS avec état.
2. **Gestion de l'état** – en se souvenant de la couleur du dernier bord, vous n'avez pas traversé deux bords rouges ou deux bords bleus consécutivement.

Si vous réussissez ce problème, vous aurez un fort point de discussion dans votre prochaine interview. Ci-dessous, nous traversons les aspects *good*, *bad* et *ugly* de la solution, et fournissons un code prêt à la copie en **Java, Python et C++**.

---

2.2 Récapitulation du problème

> **Input**
> `n`: nombre de nœuds (0-basés).
> `redEdges`: liste des bords rouges dirigés `[u, v]`.
> `blueEdges`: liste des bords bleus dirigés `[u, v]`.

> ** Sortie**
> Un tableau `réponse` de longueur `n` où `réponse[x]` est la longueur du chemin le plus court du noeud 0 au noeud x, **couleurs alternantes**, ou `-1` si impossible.

> **Constraints**
> `1 ≤ n ≤ 100`, bords ≤ 400 chacun.

---

2.3 Le bon – Pourquoi BFS est le bon outil

1. **Exploration prolongée**
BFS découvre naturellement le chemin le plus court dans un graphique non pondéré car il explore tous les nœuds à distance `k` avant de passer à `k+1`.

2. **Encodage d'État**
En attachant la couleur du dernier bord à chaque état en file d'attente, nous gardons la recherche *color‐aware* sans faire sauter la taille du graphique.

3. **Simplicité et lisibilité* *
L'algorithme est long de quelques lignes, et la complexité est linéaire dans le nombre de bords. Les recruteurs aiment code propre qui montre que vous pouvez résoudre un problème efficacement.

4. **Langue Agnostique**
La même stratégie BFS-with-color-state fonctionne sans changement en Java, Python ou C++ – une grande illustration de la pensée linguistique-agnostique.

---

2.4 Les mauvaises – Pièges communs

Ce qui arrive
- C'est quoi ?
**Tréating 0 ou 1**Le noeud initial peut prendre n'importe quelle couleur; si vous traitez init comme 0, vous allez bloquer par erreur le premier bord rouge. Utilisez un troisième état de "INIT" ou utilisez `-1` pour "no color". Autres
**Dupliquer le traitement d'Edge**. Sans une matrice visitée par couleur, le même noeud peut être enquêté infiniment. Continuer `visited[node][colore]`. Autres
**Mise à jour incorrecte de la distance** Uniquement définir `dist[v]` quand la première fois vous visitez ce nœud (indépendamment de la couleur). Autres

---

2.5 Les cas de bord qui masquent la logique

Cas odieux Pourquoi il est confus Comment garder
- C'est pas vrai.
Autres **RedEdges = [0,1],[1,2]", `blueEdges = [0,2]" – vous devez commencer par le rouge, puis le bleu, puis le rouge à nouveau. Cochez explicitement `ec != last` avant de traverser. Autres
**Le plus grand nombre de bords parallèles**=Les bords rouges peuvent être dupliqués, ou le rouge et le bleu peuvent pointer vers la même paire. Utilisez une matrice visitée pour éviter de reproduire la même paire `(noeud, couleur)`. Autres
Un bord `[u,u]` de n'importe quelle couleur peut être traversé, mais si c'est le premier bord, vous ne pouvez pas prendre une seconde boucle de même couleur. La même règle de différence de couleur s'applique; les auto-boucles n'ont pas brisé BFS. Autres

---

#### 2.6 Algorithme pas à pas

1. **Construire la liste d'attente**
`adj[u] = liste de (v, couleur)'. Couleur: 0 = rouge, 1 = bleu.

2. **Initialiser**
`dist[0] = 0`, tous les autres `-1`.
La file commence par `(0, INIT)`.

3. **BFS Loop**
«» "
alors que la file d'attente n'est pas vide :
u, lastColor = file d'attente.pop()
nextDist = dist[u] + 1
pour (v, bord Couleur) en adj[u]:
if ledgeColor == dernière couleur: continuer
si visité[v][edgeColor]: continuer
visité[v][edgeColor] = vrai
si dist[v] == -1: dist[v] = suivant Dist.
file d'attente.push((v, edgeColor))
«» "

4. **Retour** `dist`.

La clé est que chaque nœud peut être atteint deux fois (une fois par rouge, une fois par bleu). C'est pourquoi nous conservons une matrice "visitée" de 3 colonnes ("INIT" aussi).

---

2.7 Prêt à... Copier le code – trois langues

> **Java**
> [Voir plus haut mise en œuvre] (#1.1)

> **Python**
> [Voir plus haut la mise en œuvre] (#1.2)

> **C++**
> [Voir plus haut la mise en œuvre] (#1.3)

Copiez la classe, déposez-la dans votre IDE, et lancez les démos `main`. Vous serez prêt à en discuter dans un entretien.

---

2.8 Conseils pour votre entrevue

1. **Parler de la complexité* *
Le BFS fonctionne dans l'espace "O(n+E)" et "O(n+E)". Avec `n ≤ 100`, c'est trivial pour les intervieweurs. (en milliers de dollars)

2. ** Justification de l'état* *
Nous attachons la dernière couleur à l'état afin d'imposer l'alternance. Ceci est similaire à la résolution du problème de voyage routier avec les types de carburant. (en milliers de dollars)

3. **Délibérations**
Mention: *Si `redEdges` ou `blueEdges` est vide, nous trouvons toujours un chemin en utilisant l'autre couleur ou retour `-1`. *

4. ** Expliquer pourquoi `-1`**
Si nous ne définissons jamais `dist[v]`, le noeud est inaccessible sous la contrainte d'alternance. (en milliers de dollars)

---

2.9 Pourquoi cela stimule votre recherche d'emploi

- **Résoudre les problèmes**: Montrez aux recruteurs que vous pouvez concevoir une solution efficace pour un problème de graphique non trivial.
- **Codage Style**: Le code BFS propre démontre la lisibilité, qui est un grand plus dans les entrevues de programmation par paires.
- ** Flexibilité de la langue**: Avoir des solutions en Java, Python et C++ prouve que vous n'êtes pas seulement un codeur de langue.
- **Confidentialité** : Savoir comment discuter d'un BFS majestueux vous aidera à aborder des questions d'entrevue semblables (p. ex., *=Shortest Path with K‐color changes)*, Nombre minimal d'étapes pour atteindre la cible.

---

2.10 Conclusion

Le problème **Shortest Path with Alternating Colors** est plus qu'un exercice de codage ; c'est une vitrine de maturité algorithmique.
En maîtrisant le modèle BFS avec l'état et en étant en mesure d'expliquer les choix de conception *bon*, vous vous démarquerez dans les interviews techniques et gagnerez un véritable avantage dans votre chasse à l'emploi.

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit.

---

*Si vous avez trouvé cet article utile, partagez-le sur LinkedIn ou Twitter en utilisant les balises ci-dessus. Bonne chance pour votre voyage d'entrevue ! *

---

* Fin de l'article. *

---

> ** Bon codage !**
> * Se sentir libre d'adapter les harnais de démonstration à votre propre cadre de test. *

---

- Oui. 3. Remarques finales

Vous avez maintenant :

- **Trois solutions prêtes à la production** qui passeront tous les tests LeetCode en quelques minutes.
- Une plongée profonde dans la logique algorithmique** que les recruteurs aiment.
- Un article **blog** pour alimenter votre marque personnelle sur Linked Dans ou sur un site Web personnel, compléter avec des mots-clés pertinents à l'entrevue.

Bonne interview préparer!

---

*Tout le code et l'article sont open-source ; n'hésitez pas à le modifier et à le partager. *