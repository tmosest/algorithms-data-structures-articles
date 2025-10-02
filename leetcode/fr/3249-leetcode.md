---
titre: LeetCode 3249. Comptez le nombre de bons nœuds -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – 3 langues

> **Problème (LeetCode 3249 – Compter le nombre de bons nœuds)* *
> On vous donne un arbre enraciné (racine = 0).
> Un noeud est **bon** si chaque sous-arbre enraciné chez ses enfants a la même taille (nombre de nœuds).
> Retourne le nombre de bons nœuds.

Les solutions suivantes suivent la même idée :
1. Construisez une liste d'adjacence.
2. Exécutez un DFS à partir de la racine pour calculer la taille du sous-arbre de chaque noeud.
3. Pour chaque nœud vérifier que tous ses enfants ont des tailles identiques.

'`cpp
// - Oui. C++ - Oui.

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle<vector<int>> g; //
vecteur<int> sz; // taille du sous-arbre

int dfs(int v, int p) {
int cur = 1; // compter le nœud lui-même
pour (int nb : g[v]) {
si (nb == p) continuer;
cur += dfs(nb, v);
}
sz[v] = cur;
retour cur;
}

nombre intGoodNodes(vecteur<vecteur<int>>& bords) {
int n = bords.taille() + 1;
g. attribuer(n, {});
sz.assign(n, 0);

// construire un graphique bidirectionnel
pour (auto &e : bords) {
g[e[0]].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

dfs(0, -1); // calcul des dimensions des sous-arbres

Int ans = 0;
pour (int v = 0; v < n; ++v) {
bool good = true;
Int childSize = -1;
pour (int nb : g[v]) {
si (sz[nb] < sz[v]) { // nb est un enfant
Si (taille de l'enfant) -1) enfantTaille = sz[nb];
sinon si (childSize != sz[nb]) { bon = faux; casse; }
}
}
si (bon) + ans;
}
le retour des an;
}
};
«» "

"Java
// - Oui. Java - Oui.

Importation de java.util.*;

solution de classe publique {
Liste privée<Liste<entier>> graphique;
Taille int[] privée; //

Int dfs(int v, int parent) {
int cur = 1; // compte lui-même
pour (int nb : graph.get(v)) {
si (nb) le parent continue;
cur += dfs(nb, v);
}
taille[v] = cur;
retour cur;
}

nombre d'entrées publiquesGoodNodes(int[[]] bords) {
int n = bords longueur + 1;
graphique = nouvelle liste de répartition<>();
pour (int i = 0; i < n; i++) graphe.add(new ArrayList<>());
taille = nouvelle int[n];

// construire une liste d'adjacence non dirigée
pour (int[] e : bords) {
graphic.get(e[0]).add(e[1]);
graphic.get(e[1]).add(e[0]);
}

dfs(0, -1); // calcul des dimensions des sous-arbres

Int ans = 0;
pour (int v = 0; v < n; v++) {
booléen bon = vrai;
Int childSize = -1;
pour (int nb : graph.get(v)) {
si (size[nb] < size[v]) { // nb est un enfant
Si (taille de l'enfant) -1) enfantTaille = taille[nb];
sinon si (childSize != size[nb]) { good = false; break; }
}
}
si (bonne) ans++;
}
le retour des an;
}
}
«» "

'`python
♪ - Oui. Python - Oui.

de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
Dénombrement GoodNodes(self, bords: List[List[int]]) -> Int:
n = len(edges) + 1
g = defaultdict(list)
taille = [0] * n

# Créer une liste d'adjacence
pour a, b dans les bords:
Annexe b)
g[b].appendice(a)

# DFS pour calculer les tailles de sous-arbres
def dfs(v: int, p: int) -> Int:
cur = 1
pour nb en g[v]:
si nb == p:
poursuivre
cur += dfs(nb, v)
taille[v] = cur
retour cur

dfs(0, -1)

# Compter les bons nœuds
ans = 0
pour v dans la plage(n):
Bien = Vrai
taille_enfant = -1
pour nb en g[v]:
si taille[nb] < taille[v]: # enfant
si enfant_size == - 1 :
taille_enfant = taille[nb]
taille d'enfant elif != taille[nb]:
bonne = Faux
pause
si bon:
+= 1
retour et
«» "

Les trois codes fonctionnent en temps **O(n)** et en mémoire **O(n)** (n = #nodes).

---

- Oui. 2. Article de blog – Le nombre de bons nœuds dans un arbre: le bon, le mauvais, et le mauvais

> **Meta-Titre**: Master LeetCode 3249 – Compter le nombre de bons nœuds
> **Meta‐Description**: Solution étape par étape en C++, Java et Python. Apprenez l'astuce DFS, l'analyse de complexité, et des conseils d'entrevue pour les bons nœuds dans un arbre.

Introduction

Si vous êtes à la recherche d'un poste d'interview de structure de données, les problèmes de LeetCode qui combinent la théorie **graph** avec la programmation **dynamique** sont de l'or.
LeetCode 3249 – *Le nombre de bons nœuds* est l'un de ces problèmes.
Il teste votre capacité à traverser un arbre, calculer les tailles de sous-arbre, et la raison sur la consistance enfant.

Dans cet article, nous disséquerons l'approche **good** (facile à comprendre), le **bad** (écueils communs) et le **ugly** (pièges à corner). On termine avec une solution propre et prête à la production en **C++**, **Java** et **Python**.

---

Récapitulation du problème

Étant donné qu'un arbre enraciné (root = 0) est représenté par un tableau «edges», comptez les nœuds qui satisfont:

> **Bon nœud** – Tous les sous-arbres enracinés chez ses enfants ont la même taille (nombre de nœuds).

> **Constraints**
2 ≤ n ≤ 105
> * `edges` est un arbre valide (arêtes n-1, pas de cycles)

---

- Oui. 1. L'Open – Pourquoi un DFS simple fonctionne

Une idée naïve est de forcer chaque noeud, de compter ses descendants et de comparer la taille des enfants.
Mais faire cela pour chaque noeud conduirait à O(n2) temps.

La perspicacité: **Si nous connaissons la taille de chaque sous-arbre une fois, nous pouvons vérifier la --bonneté de chaque noeud dans O(1)**.

**Étapes:**

1. **Liste d'Adjacence** – Construire un graphique bidirectionnel à partir de «edges».
2. **DFS (Depth‐First Search)** – Calculer de façon récursive la taille de chaque sous-arbre de nœuds.
3. **Taille des enfants Check** – Pour le nœud `v`, tous les voisins `u` tels que `size[u] < size[v]` sont des enfants.
Si tous ces enfants partagent la même taille, alors "v" est bon.

Le DFS fonctionne une fois, donnant **O(n)** temps et **O(n)** mémoire.

---

- Oui. 2. Les erreurs communes

Pourquoi il échoue
- C'est quoi ?
**En utilisant la liste d'adjacence, mais en oubliant le parent** Passer `parent` dans le DFS et sauter. Autres
Autres **Comparer la taille de l'enfant avec la taille propre du nœud** Comparer les enfants entre eux, pas avec le parent. Autres
**En supposant que la racine n'a pas d'enfants**.Une racine peut encore être bonne si tous ses sous-sous-arbres sont égaux. Traiter la racine comme n'importe quel autre noeud. Autres
Pour n = 105 arbres profonds, la profondeur de récursion peut souffler la pile dans certaines langues. Python: utilisez `sys.setrecursionlimit` ou pile itérative. Autres

---

- Oui. 3. Les cas de bord et les pièges

Ce qui peut mal tourner Comment garder
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Etoile arbre** (la racine est reliée à toutes les feuilles) Pas de manipulation spéciale; l'algorithme s'en occupe naturellement. Autres
Autres **Arbre de ligne** (chemin)= Chaque noeud a un enfant → trivially bon. Fonctionne, mais soyez prudent lorsque vous calculez "childSize = -1". Autres
Autres **Arbre très profond** (profondeur de l'arbre) Augmenter la profondeur de récursion ou utiliser la pile itérative. Autres
**Grande entrée** (n = 105) ) L'utilisation de listes de Python pour l'adjacence peut causer des problèmes de mémoire si elle n'est pas pré-attribuée. Pré-allouer les listes ou utiliser `defaultdict(list)` et faire confiance au gestionnaire de mémoire de CPython. Autres

---

- Oui. 4. Solution complète – Passage en code

Ci-dessous est l'implémentation la plus propre que vous verrez jamais. C'est la même logique, mais écrite une fois pour **C++**, **Java** et **Python**.

> **Pourquoi est-ce une solution prête à la production? **
> * Un DFS, un passe pour compter de bons nœuds.
> * Utilise uniquement des listes d'adjacence – pas de structures de données supplémentaires.
> * Poignée tous les cas de bord.
> * Effacer les noms de variables : `graph`, `size`, `good`.

Voir la section code en haut de cette page. N'hésitez pas à copier-coller dans votre bac à sable LeetCode.

---

- Oui. 5. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
Construire une liste d'adjacence
Tailles des sous-arbres DFS
Autres Compter les bons nœuds **O(n)**

Total : **Heure O(n)**, **Espace O(n)**.
La complexité temporelle linéaire satisfait la contrainte étroite «n ≤ 105».

---

- Oui. 6. Conseils d'entrevue – Comment faire face à cette question

1. ** Expliquer le DFS dans une phrase** : Nous calculons les tailles des sous-arbres en un seul DFS, puis nous comparons les tailles des enfants. (en milliers de dollars)
2. **Mention la vérification des parents** – les intervieweurs aiment voir le paramètre `parent`.
3. **Afficher votre processus de pensée**: Pourquoi pas O(n2)? Comment le réduire ? (en milliers de dollars)
4. **Précipitations** – demandez à l'intervieweur s'il veut que vous preniez en charge une récursion profonde.
5. ** Astuce optionnelle** – si l'intervieweur le veut, vous pouvez modifier le DFS pour également retourner le "childSize" et éviter une seconde boucle.

---

6.1 Bonus – Testez votre compréhension

Ajoutez un test de santé rapide à votre environnement :

'`python
♪ Essai de l'arbre stellaire
bords = [[0, i] pour i dans la plage (1, 100000)]
print(Solution().countGoodNodes(edges)) # devrait retourner 100000
«» "

Si vous êtes à l'aise avec cet extrait, vous êtes prêt pour les bons nœuds dans un arbre.

---

- Oui. 6. Pensées finales

LeetCode 3249 est plus qu'une question astucieuse – il s'agit d'un micro-examen de graph traversal, de DP et de raisonnement prudent.
En maîtrisant le modèle **DFS + consistance enfant-size**, vous gagnerez en confiance pour s'attaquer à une foule de problèmes de style de nombre de nœuds.

Bonne chance pour votre prochaine entrevue, et n'oubliez pas de pratiquer plus d'arbre‐ Problèmes DP !

---

### Appel à l'action

* **Essayez maintenant**: Copiez le code C++, Java ou Python dans LeetCode et résolvez 3249 en quelques minutes.
* **Partager** cet article avec des amis se préparant pour les entrevues.
* **S'abonner** pour des plongées plus profondes dans la théorie des graphiques et DP sur LeetCode.

---

**Auteur**: [Votre nom] – Passionné de structure de données, contributeur de source ouverte et coach d'entrevue de codage.
**Contact**: `youremail@exemple.com "
**Suivez**: @YourHandle sur Twitter, GitHub, Linked Dans

---

Codage heureux !

---

Fin de l'article

---

Cet article devrait vous donner un parcours d'apprentissage ** clair**: saisir le concept, éviter les pièges, gérer les cas de bord, et mettre en œuvre une solution rapide.
Combinez-le avec les extraits de code prêts à l'emploi ci-dessus, et vous êtes tous mis pour la question d'interview de bons nœuds – pas de surprises !

---

* Bonne chance pour vos interviews de codage! *

---

**Note**: Toutes les URL, les balises et les métadonnées sont des supports; remplacez-les par les vôtres si vous publiez sur un blog personnel ou un site de recherche d'emploi.