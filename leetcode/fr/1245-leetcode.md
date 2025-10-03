---
titre: LeetCode 1245. Diamètre de l'arbre - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1245 – Diamètre de l'arbre
**Blogue d'entrevue optimisé pour les bonnes, les mauvaises et les mauvaises adresses + 3 langues

---

- Oui. 1. Aperçu du problème

> **Diamètre de l'arbre* *
> On vous donne un arbre *non dirigé* avec des nœuds `n` marqués `0 ... n‐1`.
> `edges[i] = [ai, bi]` décrit un bord entre `ai` et `bi`.
> **Retourner le diamètre** – le nombre de bords sur le chemin le plus long de l'arbre.

> **Constraints**
> * `1 ≤ n ≤ 104`
> * "longueur des bords".
> * `0 ≤ ai, bi < n`
> * 'ai != Bi "

Format LeetCode typique, parfait pour une interview **logiciel-ingénierie**.

---

- Oui. 2. Bien, mal et mal

Qu'est-ce qu'il y a ?
- C'est quoi ?
*Deux-pass DFS* (ou BFS) est linéaire, facile à expliquer. Une approche naïve de toutes les paires serait O(n2). L'utilisation de la récursion pour les arbres profonds peut atteindre les limites de la pile dans certaines langues. Autres
**Cas d'Edge**= Arbre avec un seul noeud → diamètre 0.- Oubliant de manipuler des feuilles isolées lors de la pelure topologique.- Mutation de la liste d'adjacence en place pendant le DFS (dangereux si réutilisé). Autres
**Performance**= O(n) temps, O(n) espace.= DFS qui suit la profondeur et met à jour le max. BFS avec une file d'attente de taille n mais en utilisant un `unordered_set` pour chaque niveau visité (plus de frais généraux). Autres
**Readability**= Effacer les noms de variables (`maxDepth`, `diamètre`). La construction du graphique de la chaudière peut encombrer la solution. Des structures de données surcompliquées (p. ex. en utilisant `Map<Set<Integer>>` en Java sans aucun avantage). Autres
**Tests**= Tests unitaires pour les petits arbres, équilibrés, biaisés, étoiles, chemin. Ne pas tester le cas où il y a exactement deux centroïdes. Essai seulement le chemin heureux (pas de manipulation d'entrée invalide). Autres

---

- Oui. 3. Trois faits saillants de la mise en œuvre

Ci-dessous vous trouverez trois solutions idiomatiques:
*Java* – classique DFS, récursion sans pile.
*Python* – DFS avec `defaultdict(list)`.
*C++* – DFS itératif utilisant une pile (pas de problèmes de profondeur de récursion).

Tous les extraits de code sont autonomes, commentés et prêts à être copiés dans votre IDE ou LeetCode.

---

#### 3.1 Java – Deux- Passer le DFS

"Java
Importation de java.util.*;

solution de classe publique {
// Créer une liste d'adjacence
liste privée<Liste<entier>> buildGraph(int n, int[][] bords) {
Liste<Liste<entier>> g = nouvelle liste de répartition<>(n);
pour (int i = 0; i < n; i++) g.add(new ArrayList<>());
pour (int[] e : bords) {
g.get(e[0)].add(e[1]);
g.get(e[1]).add(e[0]);
}
retour g;
}

// Aide DFS qui retourne la profondeur maximale du noeud
Int privé dfs(int node, int parent, Liste<Liste<entier>> g) {
int max1 = 0, max2 = 0; // deux enfants les plus profonds
pour (int nei : g.get(node)) {
si (nei) le parent continue;
profondeur int = dfs(nei, noeud, g);
si (profondeur > max1) { max2 = max1; max1 = profondeur; }
sinon si (profondeur > max2) { max2 = profondeur; }
}
// Mettre à jour le diamètre global (chemin passant par le nœud)
diamètre = Math.max(diamètre, max1 + max2);
retour max1 + 1; // profondeur du sous-arbre
}

diamètre intérieur privé = 0;

arbre public intérieurDiamètre(int[]] bords) {
i (arêtes) : null. 0) retour 0;
int n = bords longueur + 1;
Liste<Liste<entier>> graphique = buildGraph(n, bords);
dfs(0, -1, graphique); // racine à 0 (tout noeud fonctionne)
diamètre de retour;
}
}
«» "

*Complexités: *
- **Heure:** O(n)
- **Espace:** O(n) (liste d'adjacence + pile de récursion)

---

3.2 Python – DFS récursif

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def treeDiameter(self, bords: List[List[int]]) -> Int:
si ce n'est pas les bords:
retour 0

# Créer une liste d'adjacence
graphique = par défautdict(list)
pour a, b dans les bords:
graphique[a].appendice(b)
graphique[b].appendice(a)

diamètre de soi = 0

def dfs(node: int, parent: int) -> Int:
profondeurs = [0, 0] # deux plus longues profondeurs enfant
pour nb dans le graphique[node]:
si nb == parent:
poursuivre
d = dfs(nb, noeud) + 1
Si d > profondeur[0]:
profondeur[1] = profondeur[0]
profondeurs[0] = d
d ' autres profondeur[1]:
profondeur[1] = d
Self.diameter = max (self.diameter, profondeur[0] + profondeur[1])
profondeurs de retour[0]

dfs(0, -1) # commencer par un nœud arbitraire
Revenez vous-même. diamètre
«» "

*Complexités: *
- **Heure:** O(n)
- **Espace:** O(n) (graphique + profondeur de récursion)

---

### 3.3 C++ – DFS itératif (pas de récursion)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
arbreDiamètre(vecteur<vecteur<int>>& bords) {
si (edges.vide()) retourne 0;
int n = bords.taille() + 1;

// liste d'adjacence
vecteur<vector<int>> g(n);
pour (auto &e : bords) {
g[e[0]].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

diamètre int = 0;
vecteur<int> parent(n, -1);
vectorielle<int> profondeur(n, 0);
Pile <int> m;
st.push(0); // racine arbitraire

// Passage après commande
ordre du vecteur <int>;
pendant que (!st.vide()) {
Int v = st.top(); st.pop();
order.push_back(v);
pour (int nb : g[v]) si (nb != parent[v]) {
parent[nb] = v;
b) Poussées st.
}
}

// Nœuds de processus en sens inverse (après l'ordre)
pour (int i = order.size() - 1; i >= 0; --i) {
int v = ordre[i];
Int best1 = 0, best2 = 0;
pour (int nb : g[v]) si (nb != parent[v]) {
int d = profondeur[nb] + 1;
si (d > best1) { best2 = best1; best1 = d; }
sinon si (d > best2) { best2 = d; }
}
diamètre = max (diamètre, meilleur1 + meilleur2);
profondeur[v] = meilleur1;
}
diamètre de retour;
}
};
«» "

*Complexités: *
- **Heure:** O(n)
- **Espace:** O(n) (liste des dépendances + pile + tableaux)

---

- Oui. 4. Pourquoi le DSV à deux passes (ou à un passe) fonctionne

1. **La voie la plus longue implique deux congés**
Le diamètre est toujours un chemin entre deux nœuds foliaires.
Pendant la DFS, nous suivons les profondeurs les plus longues et les plus longues de chaque nœud – la somme de ces deux profondeurs est le chemin le plus long qui traverse ce nœud.

2. **Meilleure mise à jour mondiale**
Lors du désenroulement de la récursion, nous conservons une variable globale `diamètre` mise à jour avec `max(diamètre, profondeur1 + profondeur2)`.

3. ** Pass unique**
L'algorithme visite chaque bord deux fois (une fois de chaque côté), donc le travail global est linéaire.

---

- Oui. 5. Pièges courants et comment les éviter

Symptômes Correction
C'est pas vrai.
**Dépassement de l'emplacement** (arbres à écailles profondes) Autres
**Choix de racine incorrect**=Diamètre incorrect== Tout noeud fonctionne; il suffit de choisir 0 ou le premier noeud à partir de `edges`. Autres
**Non à la mise à jour Parent** Autres
**Miss-counting Edges vs Nodes**=Diamètre désactivé par 1=Rappelez-vous le nombre de diamètres *edges*, alors ajoutez 1 en se déplaçant vers l'enfant ('profondeur = enfantDepth + 1'). Autres

---

- Oui. 6. Valeur de l'entrevue et du rappel

* **Structures de données:** Graphique, liste d'adjacence, récursion/arrêt.
* **Algorithmes:** Première recherche de profondeur, programmation dynamique sur les arbres.
* ** Analyse de complexité :** Temps linéaire et espace – crucial pour les entrevues de performance.
* **Test et traitement des cas :** Fait preuve d'attention aux détails.

Lors de l'écriture de votre CV:

«» "
- LeetCode résolu #1245 Diamètre de l'arbre – mise en œuvre d'une solution efficace O(n) DFS en Java, Python et C++.
- Capacité démontrée d'analyser les compromis temps/espace et de gérer la récursion profonde par des approches itératives.
- Il a montré une bonne compréhension de la programmation graphe et dynamique sur les arbres.
«» "

---

- Oui. 7. Article de blog optimisé par le SEO (Pour les demandeurs d'emploi)

Titre
*Cracking LeetCode 1245 – Diamètre de l'arbre: Java, Python, & C++ Solutions & Conseils d'entretien *

Description de la méta
> Master LeetCode -Tree Diameter (1245) avec le code Java, Python et C++ propre. Apprenez l'algorithme, la manipulation des cas de bord et les explications prêtes à l'entrevue pour décrocher votre prochain travail d'ingénierie logicielle.

### Rubriques & Contenu

Mot-clé
C'est pas vrai.
Autres **Qu'est-ce que le diamètre de l'arbre? Diamètre de l'arbre, LeetCode 1245
Autres **Pourquoi est-ce un problème d'entrevue classique?** Discutez de la pertinence algorithmique. Entretien logiciel, structures de données
**Deux-Pass DFS expliqué**
Autres **Mise en œuvre de Java** Java DFS, LeetCode Java Autres
**Python Implementation** Python DFS, LeetCode Python Autres
**C++ Mise en œuvre** C++ DFS, LeetCode C++
**Les erreurs communes et le débogage**Les pièges.
**Performance et complexité**
**Interview Take-aways**= Comment discuter de la solution. Conseils d'entretien, algorithme
**Ajouter à votre curriculum vitae** Récapitulez les conseils, codez l'entrevue

- Oui. Exemple de paragraphe intro
> *Le problème du diamètre de l'arbre (LeetCode #1245) est un élément essentiel des entrevues d'ingénierie logicielle. Il teste votre compréhension de la transition graphique, de la récursion et de la programmation dynamique sur les arbres. Dans ce post, nous allons passer à travers la solution O(n) optimale, vous montrer nettoyer Java, Python, et les implémentations C++, et vous donner des points de discussion prêts à l'entrevue qui impressionneront les gestionnaires d'embauche.

Clôture du CTA
> Essayez le code sur LeetCode, ajoutez-le à votre GitHub, et mentionnez-le dans votre prochaine interview. Tu veux plus d'entretiens ? Abonnez-vous à notre newsletter pour connaître les problèmes hebdomadaires. (en milliers de dollars)

---

- Oui. 8. Liste de contrôle finale pour les intervieweurs

- ** Expliquez l'algorithme** en termes simples.
- **Afficher le code** et souligner où le diamètre est mis à jour.
- **Discuss ledge cases** (graphique vide, nœud unique).
- **Parler de la complexité** et des limites potentielles de la pile.
- **Contre-mesures** (récursive ou itérative).

Bonne chance pour décrocher ce rôle – vous venez de résoudre un problème classique en trois langues principales! C'est ce qu'il a dit.

---

**Codage heureux!**