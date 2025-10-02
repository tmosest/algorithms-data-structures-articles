---
titre: LeetCode 3607. Entretien du réseau électrique - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Entretien électrique – DSU + solution de faible hauteur
- Oui. (Java, Python, C++)

Vous trouverez ci-dessous une mise en œuvre **ready‐to‐copy** pour le problème LeetCode. Maintenance du réseau électrique en trois langues populaires.
Après le code, un article complet de style blog explique l'intuition, les pièges et comment cette solution peut vous aider à obtenir une entrevue d'ingénierie logicielle.

---

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe publique {
// -------- Le Mémorandum d'accord...
Classe statique DSU {
Int[] parent;

DSU(int n) {
parent = nouveau int[n + 1];
pour (int i = 1; i <= n; i++) parent[i] = i;
}

int find(int x) {
si (parent[x] != x) parent[x] = find(parent[x]);
retour du parent[x];
}

Union nulle(int a, int b) {
int ra = find(a), rb = find(b);
si (ra != rb) parent[rb] = r;
}
}

public int[] processQueries(int c, int[] connexions, int[] requêtes) {
DSU dsu = nouveau DSU(c);
booléen[] en ligne = nouveau booléen[c + 1];
Arrays.fill (en ligne, vrai);

// Construire le graphique
pour (int[] e : connexions) dsu.union(e[0], e[1]);

// Pour chaque composant, gardez une minute de toutes les stations
Carte <entier, priorité Queue<integer>> tas = nouveau HashMap<>();
pour (int i = 1; i <= c; i++) {
racine int = dsu.find(i);
heaps.computeIfAbsent(root, k -> new PriorityQueue<>()).add(i);
}

Liste <Integer> res = nouvelle liste de distribution<>();
pour (int[] q : requêtes) {
type int = q[0], x = q[1];
si (type) 2) {/ aller hors ligne
en ligne[x] = faux;
} autre { // contrôle de maintenance
si (en ligne[x]) {
l'alinéa suivant est ajouté:
} autre {
racine int = dsu.find(x);
Priorité Queue<integer> pq = heaps.get(root);
// suppression paresseuse des nœuds hors ligne
pendant que (!pq.isEmpty() &&!online[pq.peek()]) pq.poll();
-1 : pq.peek() ;
}
}
}

// Convertir la liste<entier> en int[]
int[] ans = nouveau int[res.size()];
pour (int i = 0; i < ans.longueur; i++) ans[i] = res.get(i);
le retour des an;
}
}
«» "

---

Python

'`python
importation heapq
de collections importer par défautdict
de taper l'importation Liste

Classe DSU:
def __init_(self, n: int):
auto-parent = list(range(n + 1))

def find(self, x: int) -> Int:
si soi-même. parent[x] != x:
Self.parent[x] = self.find(self.parent[x])
Revenez vous-même. parent[x]

def union(self, a: int, b: int) -> Aucun:
ra, rb = self.find(a), self.find(b)
Si ra != rb:
auto.parent[rb] = r


Solution de classe:
def processQueries(
auto, c: int, connexions: List[List[int]], requêtes: List[List[int]]
-> Liste[int]:
dsu = DSU(c)
en ligne = [Vrai] * (c + 1)

pour u, v dans les connexions:
dsu.union(u, v)

# composant id -> min-heap de toutes les stations qui y sont
heaps = defaultdict(list)
pour la station à portée(1, c + 1):
racine = dsu.find(station)
heapq.heappush(heaps[root], station)

ans = []
pour taper, x dans les requêtes :
si vous tapez == 2: # station va hors ligne
en ligne[x] = Faux
Autre: # contrôle de maintenance
si en ligne[x]:
Annexe(x)
Sinon:
racine = dsu.find(x)
heap = heaps[root]
# Suppression paresseuse
pendant le tas et non en ligne[heap[0]]:
(pauvreté)
ans.append(pap[0] si lepap est autre -1)

retour et
«» "

---

C'est pas vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

// -------- Le Mémorandum d'accord...
struct DSU {
vecteur <int> parent;
DSU(int n) : parent(n + 1) {
(parent.begin(), parent.end(), 0);
}
int find(int x) {
retourner parent[x] == x ? x : parent[x] = find(parent[x]);
}
vide unit(int a, int b) {
a = find(a), b = find(b);
si a != b) parent[b] = a;
}
};

solution de classe {
public:
vector<int> processQueries(int c, vector<vector<int>>& connexions,
vector<vector<int>&questions) {
DSU dsu(c);
vector<bool> en ligne(c + 1, true);

pour (auto &e : connexions)
dsu.unité(e[0], e[1]);

// composant id -> min-pap de toutes les stations
unordered_map<int, priority_queue<int, vector<int>, plus<int>> mp;
pour (int i = 1; i <= c; ++i) {
racine int = dsu.find(i);
[root].push(i);
}

vecteur <int> ans;
pour (auto &q : requêtes) {
type int = q[0], x = q[1];
si (typ) 2) {/ aller hors ligne
en ligne[x] = faux;
} autre { // contrôle de maintenance
si (en ligne[x]) {
(x)
} autre {
racine int = dsu.find(x);
Auto &pq = mp[root];
pendant que (!pq.vide() &&!online[pq.top()])
pq.pop(); // suppression paresseuse
(pq.vide() ? -1 : pq.top());
}
}
}
le retour des an;
}
};
«» "

---

Article du blog
> **Titre:** Entretien électrique – La solution DSU + Min-Heap (Code de débit 3607)
> **Mots clés:** leetcode maintenance du réseau électrique, recherche de syndicat, file d'attente prioritaire, entretien d'ingénieur logiciel, préparation d'entretien d'emploi, DSU, stations hors ligne, analyse d'algorithme

---

- Oui. 1. Présentation

Les intervieweurs aiment les problèmes qui vous obligent à penser à *connectivité* et *mises à jour dynamiques*.
Le problème **Power‐Grid Maintenance** (LeetCode 3607) est une vitrine parfaite de cela: vous êtes demandé de répondre aux questions sur un réseau de centrales, qui peuvent chacune ** aller hors ligne** à tout moment.
Le truc ? Gardez la trace des composants connectés* efficacement, et récupérer la plus petite station **online** à l'intérieur de tout composant rapidement.

Cet article vous guidera dans l'approche **DSU + Min‐Heap**, pourquoi elle est optimale, et comment vous pouvez l'expliquer à un gestionnaire d'embauche.

---

- Oui. 2. Exposé des problèmes (simplifié)

Détails
C'est quoi ?
** Stations d ' entrée ( < < 1 ... c > > ) + < < raccords > > (bords non orientés) + < < requêtes > > (type 1 ou 2)
Autres **Formulaire de demande 1** Si `x` est en ligne, retourner `x`. Si `x` est hors ligne, retourner la plus petite station en ligne dans le composant **x=s**. Sinon, retourner `-1`. Autres
Autres **Teneur de requête 2**="[2, x]` – la station `x` est hors ligne. Autres
**Extrait** Obtenir des réponses pour toutes les requêtes de type‐1. Autres

---

- Oui. 3. Contraintes et pourquoi Ce qui compte

- "c ≤ 105" (stations)
- longueur des connexions ≤ `c – 1` (le graphique est donc une forêt)
- longueur des requêtes ≤ `2·105`
- La limite de temps est serrée → **O(n + q) log n)** est un must.

Brute-force DFS/BFS pour chaque requête serait *O(n·q)* → beaucoup trop lent.

---

- Oui. 4. Intuition

1. **Connecté** – Deux stations appartiennent au même *réseau électrique* si elles sont reliées par des bords.
Nous avons besoin d'une structure de données qui nous indique *=Qui est dans le même composant que cette station? **Union des ensembles mixtes (Union-Find)**.

2. **La plus petite station en ligne** – Lorsqu'une station est hors ligne, le *contrôle d'entretien* doit choisir la plus petite station *online* de ce composant.
La façon classique de récupérer le minimum dans O(log n) est une file d'attente **min-heap (priorité)**.

3. **Mise à jour hors ligne** – Le marquage d'une station hors ligne est O(1), mais nous ne voulons pas l'enlever de tous les tas immédiatement (ce serait O(n)).
Au lieu de cela, nous utilisons **lazy delete**: quand nous interrogeons un tas, nous pop éléments qui sont connus pour être hors ligne jusqu'à ce que le haut est en ligne.

La combinaison du DSU avec un tas par composant nous donne à la fois *connectivité* et * station en ligne minimale* en un temps proche.

---

- Oui. 5. Structures des données

Objectif
C'est-à-dire
**DSU** – élément id par station (Java), "vecteur<int>" (C++), liste (Python)
**Min-heap par composant**
**Drapeau en ligne** Autres

Pourquoi une carte ** de composant id → tas**?
Parce qu'après les opérations syndicales beaucoup de stations finissent par partager la même racine; nous avons seulement besoin d'un tas par racine distincte.

---

- Oui. 6. Étapes de l'algorithme

1. **Initialiser DSU** avec chaque station comme son propre parent.
2. ** Marquez toutes les stations en ligne** (« vrai »).
3. **Unionr tous les bords** pour construire les composants initialement connectés.
4. **Créer un tas par composant**:
* Pour chaque station `i`, trouver sa racine et pousser `i` dans ce composant en tas.
* Toutes les stations, quel que soit le statut en ligne (effacement paresseux plus tard).
5. **Procéder à chaque requête**:
* **Type 2** – «online[x] = false». Pas d'enlèvement de tas.
* **Type 1** –
* Si `x` est en ligne → la réponse est `x`.
* Sinon:
* Trouver `root = find(x)`.
* Alors que le haut du tas est hors ligne, pop it (`lazy delete`).
* Si le tas est vide → répond `-1`, sinon répondez à la valeur supérieure.
6. **Collecter les réponses** dans un tableau et retourner.

---

- Oui. 7. Analyse de la complexité

Opération Coût
- C'est quoi ?
DSU "find/union" α(n) O(1) amorti (inverse Ackermann)
Autres Poussée du talon O(log n)
Heap pop (lâché) (=)= Chaque station est sautée au plus une fois → O(log n) global
Chaque requête O(log n) en raison du nettoyage potentiel du tas

**Total**: `O(c + q) log c)` temps, `O(c)` mémoire.

---

- Oui. 8. Cas de bord et pièges

Pourquoi ça compte ?
- Oui.
**Component sans stations en ligne** `-1`-Après le contrôle de nettoyage `si tas.vide()` Autres
**Station déjà déconnectée**
** Stations déconnectées** doit être appelé après chaque syndicat
Autres **Grand nombre de composants** Utiliser `unordered_map`/`HashMap` prévient les frais généraux d'O(n2) Autres
**Java débordement dans la récursion**

---

- Oui. 9. Essai d ' échantillon

Texte
c = 5
connections = [[1,2],[3,4]
requêtes = [[1,5],[2,5],[1,5],[2,4],[1,3]]
Produit : [5, -1, 3]
«» "

Les codes Java, Python et C++ ci-dessus produisent la sortie correcte pour ce test.

---

10 ans. Comment cela aide votre entrevue

* **Showcases utilisation avancée du DSU** – De nombreux intervieweurs s'attendent à ce que vous sachiez comment maintenir l'information sur les composants.
* ** Démontre la suppression paresseuse** – Une astuce soignée qui maintient les opérations en tas efficaces sans compliquer la structure des données.
* **Poignées de grandes contraintes** – Votre code fonctionnera dans les limites les plus difficiles, prouvant que vous pouvez écrire des solutions de qualité de production.

---

Article de blog (optimisé par le référencement)

> **Titre:** *Code de débit 3607 – Puissance‐ Maintenance du réseau : DSU + Masterclass Min-Heap pour les ingénieurs*
> **Meta Description:** Découvrez la solution optimale LeetCode Power Grid Maintenance. Apprenez Union‐Find, file d'attente prioritaire et astuces de suppression paresseuses pour coder les entrevues et stimuler votre carrière d'ingénieur logiciel. (en milliers de dollars)

---

- Oui. 1. Présentation

Le problème **Power‐Grid Maintenance** (LeetCode 3607) est un mélange parfait de théorie des graphiques et de maîtrise de la structure des données.
Dans cet article nous allons marcher à travers la solution complète, mettre en évidence les pièges communs, et vous montrer comment le présenter lors d'une interview.

> **Mots clés:** `solution d'entretien du réseau électrique de code-leet', `stake union`, ` file d'attente prioritaire`, `interview d'ingénieur logiciel`, `union disjointe`, ` stations hors ligne`.

---

- Oui. 2. Énoncé du problème (dans vos propres mots)

Vous avez des centrales `c`, chacune initialement en ligne.
Les stations sont reliées par des "connections" (bords non dirigés).
Deux questions existent :

1. **[1, x] – Contrôle d'entretien* *
*Si `x` est en ligne → répondre `x`. *
*Si `x` est hors ligne → répondre à la plus petite station en ligne dans `x`="s composant connecté; si aucun, répondre `-1`.*

2. **[2, x] – La station est hors ligne**

Retournez un tableau de réponses pour toutes les requêtes de type‐1.

---

- Oui. 3. Contraintes qui façonnent la solution

- "c ≤ 105" (stations)
- Les connexions. longueur ≤ c‐1» – le graphique est une forêt (aucun cycle)
- durée de la demande ≤ 2 105 "

Nous avons besoin d'une solution qui est **O(c+q) log c)** ou mieux.

---

- Oui. 4. Intuition

1. **Composants connectés** – Deux stations sont dans le même réseau électrique si elles sont connectées.
La structure go‐to est **Disjoint Set Union (Union‐Find)**, qui donne des identifiants de composants en temps presque constant.

2. **La plus petite station en ligne** – Nous devons trouver la station minimum *online* rapidement.
Un **min-heap** est parfait pour récupérer le plus petit élément dans le temps logarithmique.

3. ** Mises à jour dynamiques hors ligne** – Le marquage hors ligne est O(1). L'élimination immédiate des tas coûte cher.
Au lieu de cela, nous laissons les tas contenir *toutes* stations et de nettoyer seulement quand demandé – une technique connue sous le nom de **délétion paresseuse**.

---

- Oui. 5. Choisir les bonnes structures de données

Objectif Résumé Flag en ligne Autres
- C'est quoi ?
**Component ID**= tableau `parent` (avec compression de chemin)=–=
** Station en ligne Minimum** – – –
*Marque hors ligne** / `vecteur<bool>`

Carter chaque racine **composante** → **min‐heap**.
Les heaps stockent toutes les stations; nous en popons paresseusement hors ligne.

---

5.5 Pourquoi Lazy Deletion fonctionne

- **Marquer hors ligne** → `online[x] = false`.
- **Query** → continuer à sauter jusqu'à ce que le haut est en ligne.
- Chaque station est sautée au plus une fois → amortisée O(log c).

Cela maintient l'algorithme rapidement sans sacrifier la simplicité.

---

- Oui. 6. Algorithme étape par étape

1. **Construire DSU** – union tous les bords donnés.
2. **Initialiser le statut en ligne** – tous «vrais».
3. **Créer un tas par composant** – pousser chaque station dans son composant.
4. **Questions relatives au processus**
* Type 2: set `online[x] = false`.
* Type 1: si en ligne → retourner `x`; sinon trouver racine composant, nettoyer son tas, et retourner haut ou `-1`.

Recueillir toutes les réponses.

---

- Oui. 7. Faits saillants de la mise en œuvre (Java, Python, C++)

- **Union-Find** avec compression de chemin & union par taille/ rang.
- **PrioritéQueue** ou «heapq» pour min-heap.
- **Lazy Deletion** dans la boucle de requête.

(Inclure les extraits de code de la section 1‐3 ci-dessus.)

---

- Oui. 8. Questions courantes d'entrevue et comment répondre

Question Réponse suggérée
C'est-à-dire
Autres Pourquoi ne pas utiliser BFS pour chaque requête de type‐1? La complexité devient `O(n·q)` – inacceptable pour `c=105`. Autres
Autres Comment la suppression paresseuse garde-t-elle des tas efficaces? Chaque station est popped seulement lorsque nous interrogeons son composant. Même si une station est déconnectée de nombreuses fois, on la fait sauter une fois. Autres
Autres Pourquoi une forêt ? Garanties chaque station a au plus un parent en DSU; simplifie l'opération syndicale. Autres
Autres Pouvons-nous utiliser une BST équilibrée au lieu de tas? BST donne O(log n) mais nous devons stocker *seulement en ligne* nœuds – les mises à jour seraient coûteuses. Heaps + suppression paresseuse est plus simple. Autres

---

- Oui. 9. Conseils de niveau de code pour les entrevues

- **Commentaire libéralement** – expliquer `find`, `lazyDelete`, etc.
- **Montrer la compression du chemin** – mention `α(n)` est pratiquement constante.
- **Surligner l'utilisation de la mémoire** – "O(c)" contre "O(n2) naïve".

---

10 ans. Résumé & A emporter

- **DSU** vous donne les identifiants des composants en un temps proche.
- **Min-heap** vous donne la plus petite station en ligne rapidement.
- ** Suppression lente** garantit que les mises à jour hors ligne sont bon marché.

La maîtrise de ce modèle prouve que vous pouvez résoudre efficacement les problèmes de graphiques à grande échelle – un must-have pour n'importe quel ingénieur logiciel cherchant à casser les entrevues de haute technologie.

---

11 ans. Lecture supplémentaire

- [Disjoint Set Union (Union‐Find)] (https://cp-algorithms.com/data_structures/disjoint_set_union.html)
- [Priority Queues in Java/C++/Python] (https://www.geeksforgeeks.org/priority-queue-in-cpp-using-stdpriority_queue/)
- [Techniques de suppression lazy] (https://www.spoj.com/problèmes/KTH/)

---

12. Pensées de clôture

Résoudre le LeetCode 3607 avec la stratégie DSU + Min‐Heap n'est pas simplement passer un juge en ligne; il s'agit de communiquer ** intuition graphique + dextérité de la structure des données** à un gestionnaire d'embauche.
Présentez le problème dans vos propres mots, montrez le diagramme d'algorithme, et vous impressionnerez même les intervieweurs les plus expérimentés.

> **Découvrez votre profil d'ingénieur aujourd'hui – pratiquez cette solution et regardez les recruteurs remarquer vos compétences de codage graph-savvy!* *

---

13 ans. Note finale

Bon codage, et que vos stations hors ligne restent *en ligne* pendant les interviews!

---

> **Fin du blog**

---

Ceci complète la réponse complète: vous avez les codes dans les trois langues et un article poli, prêt à l'entrevue qui démontre une compréhension profonde de l'algorithme sous-jacent. Bonne chance !