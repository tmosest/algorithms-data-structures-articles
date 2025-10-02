---
titre: LeetCode 2050. Cours parallèles III -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Cours parallèles III – LeetCode 2050
### Du concept au code – Java, Python & C++

Ci-dessous vous trouverez une solution **ready‐to‐copy** dans trois des langues d'interview les plus populaires, un article de blog profond qui explique l'algorithme, met en évidence le bon, le mauvais, le mauvais, et est pleinement optimisé SEO pour quiconque cherche à as ce problème LeetCode ou une interview graph-theory.

---

Table des matières

Lien
- Oui.
Aperçu du problème
Solution Idée Autres
Code
#complexité
Dossiers et pièges #dossiers
#blog-article
À emporter

---

Aperçu du problème
**Cours parallèles III (Code Leet 2050)**
*Hard – Graphique acyclique dirigé (DAG) + Programmation dynamique*

> *Vous recevez des cours `n`, une liste des paires de "relations" préalables et un tableau `time` où `time[i]` est la durée (en mois) bien sûr `i+1`.
> Trouvez les mois minimum requis pour terminer tous les cours si vous pouvez suivre un certain nombre de cours en parallèle aussi longtemps que leurs conditions préalables sont satisfaites. *

Obstacles
- `1 ≤ n ≤ 5·104`
- <0 ≤ relations longueur ≤ 5·104 "
- "1 ≤ temps[i] ≤ 104'
- Oui. Le graphique est un DAG – chaque cours peut éventuellement être terminé.

---

Une idée de solution
Le problème est essentiellement un temps de finition le plus avancé** sur un DAG.

1. ** Ordre topologique** – Les cours de processus seulement après toutes leurs prérequis sont terminés.
2. ** Programmation dynamique sur le DAG** –
* `démarrage[i]` – premier mois vous pouvez commencer le cours *i*.
* `finish[i]` - premier mois vous pouvez terminer le cours *i* (`start[i] + time[i]`).

Pendant un style Kahn - Oui.
- Pour chaque cours `u` sorti de la file d'attente, propager son temps de finition à chaque voisin `v`.
- Mettre à jour `start[v] = max(start[v], fin[u])`.
- Diminuer le degré de `v`; quand il atteint zéro, calculer `finish[v] = start[v] + time[v]` et demande "v".

La réponse est le maximum `finish[i]` sur tous les cours.

---

- Oui. Code

#### Java 17

"Java
Importation de java.util.*;

solution de classe publique {
public int minNumberOfMeths(int n, int[][] relations, int[] temps) {
// Créer une liste d'adjacence et un tableau de degrés
Liste<Liste<Intégrée>> adj = nouvelle liste de distribution<>(n);
pour (int i = 0; i < n; i++) adj.add(new ArrayList<>());
int[] indieg = nouvelle int[n];
pour (int[] r : relations) {
la valeur de l'unité de mesure est égale à la valeur de l'unité de mesure.
adj.get(u).add(v);
endeg[v]++;
}

// Tableaux DP
int[] start = nouveau int[n];
finition int[] = nouvelle int[n];
Deque<Integer> dq = nouveau ArrayDeque<>();

// Initialiser les cours sans prérequis
pour (int i = 0; i < n; i++) {
si (indeg[i]] 0) {
début[i] = 0;
fini[i] = temps[i];
dq.offre(i);
}
}

réponse int = 0;
alors que (!dq.isEmpty()) {
int u = dq.poll();
réponse = Math.max(réponse, finition[u]);

pour (int v : adj.get(u)) {
start[v] = Math.max(start[v], fin[u]); // début pour v
l'indig[v]--;
si (indeg[v]] 0) {/ toutes les conditions préalables sont remplies
fin[v] = début[v] + temps[v];
dq.offre(v);
}
}
}
réponse de retour;
}
}
«» "

### Python 3.10

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def minNumberOfMeths(self, n: int, relations: List[List[int]],
temps: Liste[int]) -> Int:
adj = [[] pour _ dans l'intervalle(n)]
endeg = [0] * n
pour a, b dans les relations:
Annexe b-1
endeg[b-1] += 1

début = [0] * n
fini = [0] * n
q = deque([i pour i, d dans le dénombrement (indég) si d == 0])

pour i en q:
fini[i] = temps[i]

réponse = 0
alors que q:
u = q.popleft()
réponse = max(réponse, finition[u])
pour v in adj[u]:
start[v] = max(start[v], fin[u])
indég[v] -= 1
si indég[v]] 0:
fin[v] = début[v] + temps[v]
q.appendice v)

réponse de retour
«» "

C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minNumberOfMeths(int n, vector<vector<int>>& relations, vector<int>& time) {
vecteur<vecteur<int>> adj(n);
vecteur<int> indég(n, 0);
pour (auto &p : relations) {
int u = p[0] - 1, v = p[1] - 1;
adj[u].push_back(v);
++indég[v];
}

vecteur<int> début(n, 0), fin(n, 0);
file d'attente <int> q;
pour (int i = 0; i < n; ++i)
si (indeg[i]] 0) {
fini[i] = temps[i];
q.push(i);
}

réponse int = 0;
pendant que (!q.vide()) {
i) u = q.front();
réponse = max(réponse, finition[u]);

pour (int v : adj[u]) {
start[v] = max(start[v], fin[u]); // début
si (--indeg[v]] 0) {/ tous les préreqs terminés
fin[v] = début[v] + temps[v];
q.push(v);
}
}
}
réponse de retour;
}
};
«» "

Tous les trois snipets fonctionnent dans **O(n + m)** temps et **O(n + m)** mémoire, facilement adapté aux contraintes du problème.

---

La complexité

Opération Complexité
C'est quoi ?
Graphique de construction
BFS topologique et DP.
Total
Mémoire **O(n + m)** (liste de proximité + tableaux DP)

`m = relations.longueur`, `n ≤ 5·104`, donc la solution est confortablement rapide.

---

## 5-

Scénario Que regarder
C'est pas vrai.
Autres **Pas de prérequis** («relations» vide) Notre file d'attente initiale gère cela. Autres
La réponse est la durée maximale de finition de toutes les chaînes. Autres
**Les plus grandes valeurs de temps** ( ' ' 104 ') si vous préférez la sécurité; Java, Python, C++ poignées d'inte jusqu'à ~2·109. Autres
**Dimension de la couche près des limites** Notre solution BFS est itérative. Autres
**Indicateurs basés sur des Zéros et des indices basés sur des Uno**= Conversion de toutes les étiquettes de cours (`1...n`) en `0...n‐1` lors de la construction de listes d'adjacence. Autres

---

Article du blog
> **Titre**: Cours Parallèle III – Mastering DAG DP pour votre prochain entretien logiciel-ingénieur

---

Introduction
Dans les entrevues d'ingénierie logicielle, les problèmes qui impliquent **graphes**, **ordre topologique** et **programmation dynamique** sont fréquents. L'un des défis les plus appréciés sur LeetCode est **Parallel Courses III (Problème 2050)** – un problème *hard* qui vous force à combiner l'algorithme de Kahns avec DP sur un DAG.

Dans cet article, nous traversons l'énoncé du problème, illustrons l'idée algorithmique, comparons les implémentations "good" vs "bad" et livrons des solutions prêtes à la production dans **Java, Python et C++**. Nous fournirons également des mots-clés SEO-friendly de sorte que les recruteurs qui cherchent la solution de Parallel Courses III ou d'interview de tri topologique DAG de trouver ce post instantanément.

---

- Oui. Aperçu du problème (mots clés du référencement: Cours parallèles III, LeetCode 2050, DAG)

> **Objectif**: Déterminer les mois minimum requis pour terminer les cours `n` où chaque cours prend un certain nombre de mois et peut avoir des cours préalables.
> **Contraintes**:
> * `1 ≤ n ≤ 5·104`
> * `relations` est une liste des bords orientés, taille `=5·104`.
> * Graph est un DAG – chaque cours peut être fini.

---

Idée de solution (mots clés du référencement : tri topologique, programmation dynamique, algorithme de Kahn)

Le cœur de la solution est le plus rapide temps de finition sur un DAG

1. ** Ordre topologique** – s'assure que les prérequis sont traités avant les cours à charge.
2. **DP sur DAG** – propager les temps de finition des prérequis aux personnes à charge, suivre le mois de départ le plus tôt pour chaque cours.
3. **Réponse** – la durée maximale d'arrivée de tous les cours.

*Pourquoi c'est bon*:
- **Temps linéaire** – pas de recul ou de rebond exponentiel.
- **Itératif** – sûr pour les entrées énormes, aucun risque de débordement de la pile de récursion.
- **Mémoire-efficace** – liste d'adjacence + deux tableaux entiers.

*Pourquoi le DFS naïf avec récursion est mauvais*:
- La profondeur de récursion peut atteindre 50 000 → débordement de pile en Java ou C++.
- Plus difficile à raisonner au sujet des sous-problèmes qui se chevauchent – vous devriez mémoriser manuellement.

---

Bonnes et mauvaises implémentations

Mise en œuvre Force Faiblesses
C'est pas vrai.
**Kahn + DP (notre BFS)**.O(n + m), la séparation itérative, claire des temps de départ et de finish. Autres
**DFS + Memoussation** Risque de débordement de cheminée; plus difficile à justifier la complexité pour les intervieweurs. Autres
**Brute-Force DP** (boucles à nerfs sur toutes les paires) " Non acceptable pour "n = 5·104". Autres

---

Code en trois langues

*Les trois extraits de code ci-dessus sont entièrement commentés et prêts pour une entrevue en tableau blanc ou un test de codage. Vous pouvez les coller dans votre IDE préféré ou dans l'éditeur LeetCode. *

---

La complexité (mots clés : complexité temporelle, complexité spatiale, O(n+m))

- **Time**: `O(n + m)` – linéaire dans le nombre de cours et les paires préalables.
- **Espace**: `O(n + m)` – liste de proximité + tableaux DP.

Parce que le problème limite `n` et `m` à 50 000, la solution s'inscrit confortablement dans les limites de 1 s/512 MB de LeetCode.

---

### ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Réparer
- C'est quoi ?
Autres Pas de prérequis. Autres
Les étiquettes 1-based se convertissent en indices 0-based immédiatement. Autres
Autres Très grande `temps`. Autres
En profondeur de la récursion Éviter le DFS; utiliser le BFS (Kahn) pour rester dans les limites de la pile. Autres

---

Conclusion (mots clés du référencement : questions d'entretien graphique, DAG DP, solutions LeetCode, entretien Java-Python-C++)

Cours parallèles III est un graphique *iconique* Problème de PDD qui met en évidence deux compétences essentielles d'entrevue :

1. **Topological tri (Kahn)** – vous assurer de respecter les conditions préalables.
2. ** Programmation dynamique sur DAGs** – calcul des heures de début et de fin.

La maîtrise de ce problème prouve que vous pouvez gérer **les DAG de niveau dur** dans un cadre de production, une compétence très prisée par les recruteurs de Google, Amazon, Microsoft et fintechs.

Ajoutez l'extrait à votre repo GitHub, pratiquez sur les DAG aléatoires, et vous vous sentirez confiant dans n'importe quelle question d'entrevue de cours parallèles.

---

À emporter

- **Itérative BFS + DP** → **O(n + m)**, sans danger pour les nœuds de 50 k.
- Évitez la récursion → aucun débordement de pile.
- Convertir les indices en 0 pour plus de clarté.
- Mettre cette solution en avant sur votre CV ou portfolio en tant qu'expert en Griff DP.

Bon codage ! Les

---

## 7=" Takeaway (mots clés du SEO: préparation de l'entrevue, problèmes de graphique, entretien de codage)

*Cours de parallèle III est un exemple de manuel de **DAG + DP** en action. En présentant des solutions itératives en Java, Python et C++, vous démontrez à la fois la maîtrise du langage et une profonde perspicacité algorithmique – exactement ce que les recruteurs recherchent. *

N'hésitez pas à copier, modifier et exécuter ces solutions sur LeetCode ou lors d'entretiens simulés. Et rappelez-vous : **Les algorithmes graphiques sont le pain-and-butter des rôles d'ingénierie logicielle senior**. Bonne chance !