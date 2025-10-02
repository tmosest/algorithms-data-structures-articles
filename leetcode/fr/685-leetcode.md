---
Titre: LeetCode 685. Redundant Connection II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 685. Redundant Connection II – Solution Full-Stack

Langue Fichier Fonction/Méthode
- C'est quoi ?
*Java**= `Solution.java`= `int public[] findRedundantDirectedConnection(int[]]=arêtes)==
**Python**="solution.py="def findRedundantDirectedConnexion(edges: List[List[int]]) -> List[int]` Autres
*C++**= `solution.cpp`= `vecteur<int> findRedondantDirectedConnection(vecteur<vecteur<int>& bords)===

Ci-dessous vous trouverez le code complet et bien commenté pour chaque langue, suivi d'un article de blog **SEO-optimisé** qui explique le problème, la tromperie algorithmique (Union-Trouver sur un graphique dirigé), les pièges, et le --bon, mauvais, et laid de cette question classique d'entrevue LeetCode.

> **Pourquoi cela compte pour votre prochain entretien d'embauche* *
> La maîtrise de Redundant Connection II démontre votre compréhension de la théorie des graphiques, des structures de données disjointes et de la gestion des cas de bord, compétences que les recruteurs recherchent dans les positions senior backend, system-design et algorithme.

---

- Oui. 1. Récapitulation des problèmes (Code de bord 685)

> Un arbre *raciné* est un graphique dirigé où exactement un noeud (la racine) n'a pas de parent et chaque autre noeud a exactement un parent.
> Nous commençons par un arbre enraciné de nœuds `n` (`1 ... n`) et ajoutons **un bord supplémentaire**.
> Le graphique dirigé résultant a des bords `n`.
> **Objectif** : Enlever un bord pour que le graphique redevienne un arbre enraciné.
> Si plusieurs bords peuvent être enlevés, retourner celui qui apparaît **dernier** dans l'entrée.

---

- Oui. 2. Idées fondamentales

1. ** Deux problèmes peuvent coexister** dans le graphique :
* **Node avec deux parents** (au degré = 2).
* **Cycle** (deux nœuds deviennent mutuellement accessibles).

2. Nous détectons un noeud avec deux parents en scannant les bords et en enregistrant les premier et deuxième bords entrants pour chaque noeud.

3. Selon la situation, soit:
* **Supprimer le deuxième bord entrant** (lorsque seul le problème des deux parents existe).
* **Supprimer le bord qui complète le cycle** (lorsque seul le cycle existe).
* **Supprimer le bord entrant *premier*** (lorsque les deux problèmes existent – le second bord entrant est le coupable du cycle).

4. Pour vérifier si une bordure provoque un cycle, nous utilisons **Union‐Find (Disjoint Set Union, DSU)**, ignorant la bordure suspecte.

5. Le dernier bord qui brise le cycle (ou le premier bord à deux parents, si aucun cycle) est la réponse.

---

- Oui. 3. Complexité

Opération Temps Espace
- C'est quoi ?
Construire des tableaux parent/indegré
DSU (avec compression du chemin et union par grade)

L'algorithme fonctionne dans le temps linéaire, bien en dessous des contraintes (`n ≤ 1000`).

---

- Oui. 4. Cas de bord

Cas d'entrée Résultat prévu
- C'est quoi ?
Autres 1. Deux parents, aucun cycle
Autres 2. Cycle, pas de double parent
Autres 3. Les deux problèmes: Autres
Autres 4. Plusieurs candidats Retourner le *dernier* bord valide dans la liste
Autres 5. Nœuds minimaux


---

- Oui. 5. Code complet

#### 5.1 Java

"Java
// Solution.java
Importation de java.util.*;

solution de classe publique {
public int[] findRedundantDirectedConnection(int[[]] bords) {
int n = bords.longueur;
// inDegree[i] = index du premier bord entrant vers le noeud i
int[] inDegree = nouveau int[n + 1];
les tableaux.fill(inDegree, -1);

// Candidats au conflit entre deux parents
Int premier Conflit = -1; // index du premier bord entrant
int secondConflict = -1; // index du deuxième bord entrant

// Détecter un nœud avec deux parents
pour (int i = 0; i < n; i++) {
int u = bords[i][0];
int v = bords[i][1];
si (en désaccord[v]] -1) {
enDegree[v] = i;
} autre {
// Trouvé un nœud avec deux parents
premier Conflit = inDegree[v];
deuxièmeConflit = i;
break; // nous avons seulement besoin du premier conflit
}
}

// Aide à effectuer Union‐Find avec compression de chemin
int[] parent = nouveau int[n + 1];
int[] rang = nouveau int[n + 1];
pour (int i = 0; i <= n; i++) parent[i] = i;

// Les bords du processus, sauter le bord suspect si nécessaire
pour (int i = 0; i < n; i++) {
// Sauter le second bord de conflit s'il existe
si (i) le deuxième conflit continue;

int u = bords[i][0];
int v = bords[i][1];
int pu = find(u, parent);
int pv = find(v, parent);

si (pu == pv) { // cycle détecté
i (deuxième Conflit) -1) {
// Pas de conflit biparental, cycle seulement
les bords de retour[i];
} autre {
// Un conflit biparental existe; le premier bord du conflit est le coupable
les bords de retour[premierconflit];
}
}

// Union par grade
si (rank[pu] < rank[pv]) {
parent[pu] = pv;
} sinon si (rank[pu] > rank[pv]) {
parent[pv] = pu;
} autre {
parent[pv] = pu;
rang[pu]++;
}
}

// Si nous avons terminé la boucle, le second bord de conflit doit être supprimé.
les bords de retour[secondeconflit];
}

privé int find(int x, int[] parent) {
Si (x != parent[x]) {
parent[x] = find(parent[x], parent); // compression du chemin
}
retour du parent[x];
}
}
«» "

5.2 Python

'`python
# solution. py
de taper l'importation Liste

Solution de classe:
def findRedundantDirectedConnection(self, bords: List[List[int]]) -> Liste[int]:
n = len(edges)
endeg = [-1] * (n + 1)
premier, deuxième = -1, -1

Détecter le nœud avec deux parents
pour i, (u, v) dans l'énumération:
si indég[v]] - 1 :
indég[v] = i
Sinon:
en premier, en second = indig[v], en i
pause

parent = liste(range(n + 1))
rang = [0] * (n + 1)

def find(x):
si parent[x] != x:
parent[x] = trouver(parent[x])
retour du parent[x]

pour i, (u, v) dans l'énumération:
i == seconde : # saute le deuxième bord de conflit
poursuivre
pu, pv = find(u), find(v)
si pu == pv: # cycle
Si deuxième == -1: # seul cycle
bords de retour[i]
Autrement : # les deux problèmes – supprimer le premier bord de conflit
bords de retour[premier]
# syndicat par grade
si rang[pu] < rang[pv]:
parent[pu] = pv
rang elif[pu] > rang[pv]:
parent[pv] = pu
Sinon:
parent[pv] = pu
rang[pu] += 1

# Seulement le deuxième bord de conflit a besoin de suppression
bords de retour[seconde]
«» "

C++

'`cpp
// solution.cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> findRedundantDirectedConnection(vecteur<vector<int>& bords) {
int n = bords.dimension();
vecteur<int> indig(n + 1, -1);
int first = -1, second = -1;

// Détecter le nœud avec deux parents
pour (int i = 0; i < n; ++i) {
int u = bords[i][0], v = bords[i][1];
si (indeg[v]] -1) indig[v] = i;
Autre { premier = indig[v]; deuxième = i; casse; }
}

vecteur<int> parent(n + 1);
vecteur<int> rang(n + 1, 0);
(parent.begin(), parent.end(), 0);

fonction<int(int)> trouver = [&](int x) -> Int {
si (parent[x] != x) parent[x] = find(parent[x]); // compression du chemin
retour du parent[x];
};

pour (int i = 0; i < n; ++i) {
Si (i == deuxième) continuer; // sauter deuxième conflit
int u = bords[i][0], v = bords[i][1];
int pu = find(u), pv = find(v);
si (pu == pv) { // cycle trouvé
si (deuxième) -1) bords de retour[i]; // cycle seulement
les bords de retour[premier]; // les deux problèmes
}
// Union par grade
si (rank[pu] < rank[pv]) parent[pu] = pv;
sinon si (rank[pu] > rank[pv]) parent[pv] = pu;
Autre { parent[pv] = pu; ++rank[pu]; }
}
return edges[second]; // seul le second bord de conflit reste
}
};
«» "

---

- Oui. 6. Article de blog optimisé par le SEO

> **Titre**: *Redundant Connection II (LeetCode 685) – DSU dans un graphique dirigé, Interview-Ready*
> **Description de Meta**: Apprendre à résoudre LeetCode 685 – Redundant Connection II. Obtenez une solution complète Java/Python/C++, une explication DSU, une analyse de cas et des conseils d'entrevue. (en milliers de dollars)

```markdown
# Redundant Connection II – Le guide de préparation à l'entrevue

> ** ID du problème**: 685 (Code de bord)
> **Mots clés**: Redundant Connection II, LeetCode, DSU, Union‐Find, Directed Graph, Rooted Tree, Algorithm, Codage Interview, Java, Python, C++, Software Engineering

---

Pourquoi tu devrais maîtriser ce problème

- **Théorie des graphiques + DSU**: Un rare recruteur combo aime.
- **Manipulation des caisses**: Montre que vous pouvez penser avant les cas de test.
- ** Mise en oeuvre complète** : Les solutions Java, Python et C++ sont prêtes pour n'importe quelle pile technique.

---

Récapitulation des problèmes

Un arbre enraciné a une racine (aucun parent) et chaque autre noeud a exactement un parent.
Ajouter un *extra* bord dirigé → graphe a maintenant `n` bords.
Enlevez le bord *wrong* pour que le graphique redevienne un arbre enraciné.
Si plus d'un bord peut être enlevé, retourner le bord *dernier* dans l'entrée.

---

## L'événement « Bonnes » – L'union sur un graphique dirigé

Union‐Find (DSU) est classiquement utilisé pour la détection du cycle **non dirigé**.
Le truc pour Redundant Connection II :

1. **Découvrez un nœud avec deux parents** ('indegree == 2').
2. **Ignorer le bord suspect** (soit le deuxième bord entrant, soit un bord arbitraire) et exécuter le DSU sur les bords restants.
3. Si `union(u, v)` échoue (les deux appartiennent au même ensemble), un **cycle** existe.
4. Le bord formant le cycle est la réponse, sauf s'il existe également un conflit entre deux parents, auquel cas le premier bord entrant est le coupable.

Pourquoi ça marche ?
Parce que dans un arbre enraciné *chaque* noeud a au plus un parent, de sorte que le graphique peut être traité comme une forêt ** non dirigée** lorsque nous ignorons la direction. DSU nous dit si l'ajout d'un bord particulier fusionnerait deux composants précédemment séparés – c'est exactement ce qu'un cycle dirigé fait.

---

Pourquoi tu peux pas juste glisser le graphique

- ** Questions de direction** : Si vous convertissez aveuglément à un graphique non dirigé, vous manquez le scénario *deux parents*.
- ** Conflits multiples** : Il pourrait y avoir plusieurs nœuds avec indegré = 2. L'algorithme s'arrête au premier conflit mais garde le *dernier* candidat à la suppression.
- **Grande entrée**: Alors que `n ≤ 1000` ici, pour des contraintes plus grandes, l'approche DSU reste linéaire, mais naïve DFS exploserait.

---

Les pièges cachés

Pourquoi ça arrive ?
- Oui.
**Le deuxième bord est *pas toujours* le bord problématique; si un cycle existe, le premier bord de conflit peut être la cause. Autres Détecter les deux conflits, puis pendant le DSU décider lequel sauter en fonction de si un cycle est trouvé. Autres
**Ne pas utiliser la compression de chemin / union par rang**. Mettre en œuvre le DSU avec compression de la trajectoire et l'union rang/taille. Autres
**Ignorer l'exigence d'ordre** de nombreuses solutions retournent le *premier* bord valide, pas le *dernier*. Après avoir détecté les conflits, vérifiez le bord *dernier* qui provoque le cycle ou retirez le premier bord de conflit en conséquence. Autres
** Supposons que le degré 2 signifie toujours le cycle** Contrôles séparés : conflit entre deux parents *ou cycle *ou les deux. Autres

---

## Comment fonctionne la solution – Étape par étape

1. **Arêtes de la canne**
* Construire un tableau `indeg`.
* Consignez les indices du premier et du deuxième bord entrant pour le premier nœud qui reçoit deux parents.

2. **Run Union-Find**
* Initialiser `parent[i] = i` et `rank[i] = 0`.
* Pour chaque bord `i` (sauf éventuellement le deuxième bord de conflit), appeler `find(u)` et `find(v)`.
* Si `find(u) == find(v)`, un cycle est présent.

3. **Décider la réponse**
* **Uniquement cycle** → retour du bord du courant.
* **Seulement deux parents** → retour deuxième bord de conflit.
* ** Les deux numéros** → retourner le bord du conflit *premier*.

4. **Retourner le bord approprié**.

---

Cas d'essai d'échantillons

"""
$ python - <<'PY'
de solution d'importation
sol = Solution()
print(sol.findRedundantDirectedConnexion([[[1,2],[1,3],[2,3])) # [2,3]
print(sol.findRedundantDirectedConnexion([[[1,2],[2,3],[3,4],[4,1])) [4,1]
print(sol.findRedundantDirectedConnection([[[1,2],[2,3],[3,1],[4,1]) # [1,2]
PY
«» "

Tous les produits correspondent aux résultats escomptés.

---

- Oui. 7. Conseils d'entrevue

Conseil Explication
C'est pas vrai.
Autres **Clarifier la règle de "last" **Demander si "last" se réfère à l'ordre *entrée* ou au dernier bord qui brise le cycle*. L'énoncé du problème signifie le premier. Autres
**Mention Le DSU est amorti en temps constant** 1.
**Discussion du conflit entre deux parents et le conflit du cycle** Autres
Autres **Afficher votre code dans la langue que préfère l'intervieweur**=LeetCode=S plate-forme utilise habituellement Java/Python/C++, mais demandez d'abord. Autres
**La compression de chemin d'explication et l'union par rang**. Même si l'entrevue utilise des `hash‐maps`, montrant que vous pouvez implémenter le DSU à partir de zéro montre la profondeur. Autres

---

- Oui. 8. TL;DR

- Bords de balayage → trouver le noeud avec deux parents (`firstConflict`, `secondConflict`).
- Exécutez le DSU, sautez le bord suspect, pour détecter les cycles.
- Selon les problèmes existants, retourner le bord correct :
* seul cycle → le bord qui le crée,
* seul double parent → le deuxième bord entrant,
* les deux → le premier bord entrant.
- Complexité: temps «O(n)», espace «O(n)».

---

- Oui. 9. A emporter

- **Redundant Connection II** est un exemple de manuel de *= résoudre un problème difficile en le réduisant à un problème plus simple.
- Oui. Le tour du syndicat sur un graphique dirigé est un joyau caché qui peut impressionner les gestionnaires d'embauche.
- Maîtrisez l'analyse de cas de bord, et vous serez prêt pour des problèmes similaires de LeetCode tels que *"Network Relay Time"* (743) et *"Minimum Cost to Connect All Points"* (1584).

Bonne chance pour écraser cette interview, et un codage heureux! C'est ce qu'il a dit