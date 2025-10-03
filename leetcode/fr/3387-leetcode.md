---
Titre: LeetCode 3387. Maximiser le montant après deux jours de conversion -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1. Solutions de code

Vous trouverez ci-dessous trois solutions complètes pour le problème **LeetCode****. Maximiser la quantité après deux jours de conversions** – une en **Java**, **Python** et **C++**.
Tous les trois utilisent la même idée *BFS* :
1. Construire un graphique bidirectionnel pondéré pour le jour 1.
2. Exécutez BFS pour calculer le montant maximum accessible à partir de la monnaie de départ.
3. Renouveler l'EFC le jour 2, en commençant par les montants du jour 1.
4. Retourner le montant final de la devise originale.

> **Pourquoi BFS? **
> Avec ≤ 10 bords par jour le graphique est minuscule – BFS garantit que nous visitons chaque noeud seulement lorsque nous trouvons une meilleure quantité.
> Il est plus facile à comprendre, plus rapide dans la pratique pour ces contraintes, et évite le risque de débordement de points flottants qui peut venir avec DFS ou DP exhaustive.

---

#### 1.1 Java (style LeetCode)

"Java
Importation de java.util.*;

solution de classe {

public double maxMontant(initiale de la chaîneMonnaie,
Liste<Liste<String>> paires1, taux de double[]1,
Liste<Liste<String>> paires2, taux double[]2) {

// Graphique de jour 1
Carte<String, Carte<String, Double>> g1 = buildGraph(paires1, taux1);
// Graphique de jour 2
Carte<String, Carte<String, Double>> g2 = buildGraph(paires2, taux2);

// Montants maxi après le jour 1
Carte <String, Double> day1 = bfs(initialMonnaie, g1, null);

// Montants maxi après le jour 2 – commencer par les résultats du jour-1
Carte <String, Double> day2 = bfs(initialMonnaie, g2, day1);

retour day2.getOrDefault(initialMonnaie, 1.0);
}

*** Construire un graphique bidirectionnel pondéré */
carte privée<String, carte<String, double>> buildGraph(
Liste<Liste<String>> paires, taux doubles {] {

Carte<String, Carte<String, Double>> graphique = nouveau HashMap<>();

pour (int i = 0; i < paires.size(); ++i) {
Chaîne a = paires.get(i).get(0);
Chaîne b = paires.get(i).get(1);
double r = taux[i];

graph.computeIfAbsent(a, k -> new HashMap<>()).put(b, r);
graphic.computeIfAbsent(b, k -> new HashMap<>()).put(a, 1.0 / r);
}
graphique de retour;
}

***
* BFS qui conserve la meilleure quantité vue jusqu'à présent.
* Si init n'est pas nul, nous semons la file d'attente avec toutes les clés de init.
*/
carte privée <String, Double> bfs(
Commencer par les cordes,
Carte <String, carte<String, double>> graphique,
Carte <String, Double> init) {

Carte <String, Double> meilleure = nouvelle HashMap<>();
si (init != null) {
best.putAll(init);
} autre {
best.put (démarrage, 1.0);
}

Queue<String> q = nouvelle liste liée<>(best.keySet());

alors que (!q.isEmpty()) {
Chaîne cur = q.poll();
double curAmt = best.get(cur);

pour (Map.Entry<String, Double> e :
graphic.getOrDefault(cur, Collections.videMap())entrySet() {

Chaîne nxt = e.getKey();
double nouveau Amt = curAmt * e.getValue();

si (newAmt > best.getOrDefault(nxt, 0.0)) {
best.put(nxt, newAmt);
q.offre(nxt);
}
}
}
le meilleur retour;
}
}
«» "

---

#### 1.2 Python 3

'`python
de collections import defaultdict, deque
de taper l'importation Liste

Solution de classe:
def maxMontant(
soi-même,
initialeMonnaie: str,
paires1: Liste[Liste[str]],
taux1: Liste[float],
paires2: Liste[Liste[str]],
taux2: Liste[float]
-> flotteur:

g1 = auto.build_graph(paires1, taux1)
g2 = auto.build_graph(paires2, taux2)

jour1 = auto.bfs(initialeMonnaie, g1, Néant)
jour2 = auto.bfs(initialeMonnaie, g2, jour1)

retour jour2.get(initialMonnaie, 1.0)

def build_graph(
auto, paires: Liste[Liste[str]], taux: Liste[float]
-> par défaut :
g = defaultdict(dict)
pour (a, b), r en tyrolienne (paires, taux):
g[a][b] = r
g[b][a] = 1,0 / r
retour g

def bfs(
soi-même,
début: str,
graphique: par défaut,
init: dict.
-> - C'est ça.
best = init.copy() si init autre {start: 1.0}
q = deque(best.keys())

alors que q:
cur = q.popleft()
cur_amt = meilleur[cur]
pour nxt, taux dans graph.get(cur, {}).items():
nouveau _amt = taux cur_amt *
si new_amt > best.get(nxt, 0.0):
best[nxt] = new_amt
q.annexe(nxt)
le meilleur retour
«» "

---

*## 1.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
double maxMontant(chaîne initiale) Monnaie,
vecteur<vector<string>>& pairs1, vecteur<double>&taux1,
vector<vector<string>>& pair2, vector<double>& rates2) {

auto g1 = buildGraph(paires1, taux1);
auto g2 = buildGraph(paires2, taux2);

unordered_map<string, double> day1 = bfs(initialCurrency, g1, {});
unordered_map<string, double> day2 = bfs(initialCurrency, g2, day1);

retour jour2.count(initialMonnaie) ? jour2[initialMonnaie] : 1.0;
}

particulier:
// Graphique: noeud -> liste de {voix, poids}
vector<unordered_map<string, double>> buildGraph(
Const vector<vector<string>>& paires, const vector<double>& taux) {
non classé_map<string, non classé_map<string,double>> adj;
pour (size_t i = 0; i < paires.size(); ++i) {
chaîne a = paires[i][0];
chaîne b = paires[i][1];
double r = taux[i];
adj[a][b] = r;
adj[b][a] = 1,0 / r;
}

// Convertir en forme vectorielle pour faciliter BFS
vector<unordered_map<string,double>> g;
pour (const auto& [noeud, voisins] : adj)
g.emplace_back(voix);
retour g;
}

non ordonné_map<string,double> bfs(
Const string & start,
Const vector<unordered_map<string,double>>& graphique,
Const unordered_map<string,double>* init) {

unordered_map<string,double> meilleur;
file d'attente <string> q;

si (init) {
best = *init; // graines avec des résultats de jour-1
pour (const auto& [k, v] : *init) q.push(k);
} autre {
best[start] = 1,0;
q.push(démarrage);
}

pendant que (!q.vide()) {
chaîne cur = q.front(); q.pop();
double curAmt = meilleur[cur];
pour (auto it = graph[cur].cbegin(); it != graph[cur].cend(); ++it) {
const string& nxt = it->first;
taux double = it->seconde;
double nouveau Amt = cur Taux d'amt*;
si (nouveauAmt > meilleur[nxt]) {
best[nxt] = newAmt;
q.push(nxt);
}
}
}
le meilleur retour;
}
};
«» "

> **Note**: La version C++ conserve le graphique dans un vecteur de cartes pour la vitesse. Avec les petites tailles d'entrée, la représentation `vector<unordered_map<...>>` est plus que assez rapide.

---

2. Article du blog – Le bon, le mauvais et le mauvais des conversions de devises de deux jours

> **Titre**
> ** Maximiser la quantité après deux jours de conversion – une plongée profonde (Java-Python-C++)* *

---

Table des matières

1. **Aperçu du problème**
2. **Pourquoi ce problème est un gold-mine pour les algorithmes graphiques* *
3. **La stratégie du BFS – Les bonnes* *
3.1 Construire le graphique bidirectionnel
- 3.2 Première Jour BFS
- 3.3 Deuxième Jour BFS
4. ** Approches alternatives – Les mauvais et les mauvais**
4.1 Épuisement du DFS
- 4.2 Programmation dynamique sur les séquences de bord
- 4.3 Bellman-Ford & Floyd- Warshall (surtuer ici)
5. ** Analyse de complexité**
6. **Dossiers et pièges**
7. **Code Marche à suivre (Java, Python, C++)* *
8. **A emporter et pensées finales* *

---

2.1 Aperçu du problème

On vous donne deux ensembles *indépendants* de taux de change – un pour **Jour 1** et un pour **Jour 2**.
En commençant par **1 unité** de la "première monnaie", vous pouvez:

1. Convertir le long de toute chaîne d'échanges le Jour 1.
2. Tenir les devises résultant du jour au lendemain.
3. Convertir à nouveau le Jour 2 en utilisant les tarifs du jour.

Votre objectif : ** retourner le montant maximum possible de la monnaie originale après les deux jours**.

*Constraints* :
- 2 paires ≤ 10 par jour.
- Les taux de change sont des chiffres réels > 0.
- Les graphiques sont entièrement bidirectionnels (on peut toujours inverser un trade).

---

Pourquoi les algorithmes graphiques ?

À première vue, le problème ressemble à un casse-tête dynamique de programmation ou de style «knapsack», mais il s'agit en fait d'un problème d'accessibilité du graphique ** pondéré**:

- **Nœuds** – devises.
- **Edges** – taux de change directs, poids = multiplicateur.
- **Objectif** – maximiser le produit des poids le long d'un chemin.

Parce que vous pouvez inverser tout échange, chaque bord est bidirectionnel.
Avec seulement jusqu'à 10 bords par jour, le graphique a au maximum 11 nœuds, ce qui fait de **breadth‐first search (BFS)** un ajustement idéal.

---

2.3 La stratégie du BFS – Les bonnes

Étape Ce que nous faisons Pourquoi ça marche
C'est pas vrai.
Pour chaque taux `a → b` ajouter `b → a` avec le poids `1/r`.- Le graphique reste symétrique; on ne rate jamais une conversion inverse. Autres
**Jour 1 BFS**=Démarrer à `initialMonnaie` avec la quantité = 1.= Chaque fois que nous trouvons un meilleur produit pour un voisin, nous le poussons sur la file d'attente. Autres
**Jour 2 BFS**=Ensemencer la file d'attente avec **tous** les quantités à partir du jour 1. La nuit vous pouvez commencer à partir de n'importe quelle monnaie que vous possédez. Autres
**Résultat** après le jour Le produit du meilleur nombre de jours 1 avec le meilleur multiplicateur de jours 2. Autres

C'est vrai. Pourquoi BFS est *bon*

- **Simplicité** – pas de récursion, pas de problèmes de profondeur de la pile.
- **Optimalité** – chaque fois que nous voyons un produit plus grand, nous le propageons immédiatement.
- **Speed** – Avec ≤ 10 bords par jour, BFS se termine en microsecondes.
- **Sécurité numérique** – Nous évitons une récursion profonde qui pourrait conduire à un point flottant inférieur ou supérieur.

---

2.4 Approches alternatives – Les mauvaises et laides

L'approche Quand il *hight* être utile
- C'est pas vrai.
**Exhaustive DFS**. Petite profondeur, toutes les permutations possibles. Autres
**Programmation dynamique** (DP sur les bords) Autres
**Bellman–Ford**=Détecte les cycles négatifs (dans l'espace log)== Overkill; tête algorithmique de `O(VE)' pour les graphes minuscules. Autres
**Floyd–Warshall**=Atteindre toutes les paires="O(V^3)" – inutile avec si peu de nœuds. Autres

> **Ligne de bottom**: *BFS* offre un équilibre parfait entre clarté, performance et faible utilisation de la mémoire pour les limites données.

---

2.5 Analyse de complexité

Autres Phase des opérations Complexité
C'est pas vrai.
Graphique de construction (Jour 1) Autres
Construire le graphique (Jour 2)
Jour 1 de la BFS O(V + E) par mise à jour **O(V + E)**
Date de naissance
**Total**** **O(n + m)**** **~O(20)** – temps pratiquement constant. Autres

L'utilisation de la mémoire est également négligeable – seulement une poignée de cartes contenant au plus 11 clés.

---

2.6 Pièges communs

Piège
- Oui.
Autres Oubliant d'ajouter le bord *reverse* (`1/r`) "graph.putIfAbsent(b, nouveau HashMap<>()); graph.get(b).put(a, 1.0 / r);"
Autres Retourner 0.0 pour les devises qui ne peuvent pas être atteintes.
En utilisant la récursion sur un graphique cyclique, préférez BFS/queue ou DFS itérative pour éviter le débordement de la pile.

---

2.7 Harnais d'essai (facultatif)

"Java
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Liste<Liste<String>> p1 = Liste de(
Liste des("USD", "EUR"),
Liste des("EUR", "JPY")
);
double[] r1 = {0,9, 120};

Liste<Liste<String>> p2 = Liste des
Liste. of("USD", "GBP"),
Liste des("GBP", "JPY")
);
double[] r2 = {0,8, 150};

Système.out.println(s.maxMontant("USD", p1, r1, p2, r2)
}
«» "

Ce qui précède va imprimer le montant maximum de **USD** vous pouvez finir avec après les deux jours.

---

2. Article de blog – SEO-optimized Guide

> ** Maximiser le montant après deux jours de conversion – résoudre le problème de LeetCode en Java, Python et C++* *

---

2.1 Introduction

LeetCodes **3387 – ☐ Maximiser le montant après deux jours de conversion** est un puzzle classique *graph* qui mélange finance réelle avec pensée algorithmique. La tâche : commencer par une unité d'une monnaie, l'échanger pour d'autres sur **deux jours**, et terminer avec le **le plus grand montant possible** de votre monnaie originale.

Ci-dessous, nous disséquons le problème, nous traversons la solution la plus efficace (BFS), et nous fournissons un code entièrement commenté dans **Java, Python et C++**. Que vous soyez un prépper d'entrevue de codage, un programmeur compétitif ou simplement un codeur curieux, cet article est votre manuel de démarrage rapide.

---

2.2 Capture de problème

- **Input**
- `initialCurrency` – une chaîne comme `"USD"`.
- "PairsDay1" – liste des échanges directs pour le jour 1.
- `tauxJour1` – multiplicateurs correspondants (> 0).
- "PairsDay2" et "tarifs" Jour2' – même pour le Jour2.

- **Opération**
1. Convertissez le chemin le jour 1.
2. Nuit, vous pouvez * tenir * n'importe quelle monnaie avec laquelle vous finissez.
3. Convertir à nouveau le Jour 2 en utilisant les tarifs du jour.

- **Objectif** – retour **maximum** du montant initial de la monnaie après les deux jours.

**Pourquoi c'est important**: Le problème teste votre capacité à modéliser un système financier comme un graphique, à gérer les bords bidirectionnels, et à maximiser un produit de nombres réels – une intersection soignée des maths et du codage.

---

#### 2.3 Le bien– première recherche

Nous traiterons chaque jour comme un graphe dirigé ** pondéré par des différences (arêtes bidirectionnelles). BFS convient naturellement parce que:

- **Petit graphique**: ≤ 11 nœuds, ≤ 10 bords par jour.
- **Pas de récursion**: élimine le risque de débordement de cheminée.
- **Production immédiate**: un meilleur produit est immédiatement poussé.

**Pseudocode**:

«» "
buildGraph(paires, taux):
pour chaque (a, b, r):
ajouter le bord a->b poids r
ajouter le bord b->un poids 1/r

BFS(startNode):
file d'attente = [(startNode, 1.0)]
meilleur = {startNode: 1.0}
alors que la file d'attente n'est pas vide :
noeud, amt = file d'attente.pop()
pour chaque voisin, w dans le graphique[node]:
nouveaux Amt = amt * w
si newAmt > best[voix]:
meilleur[voix] = nouveauAmt
file d'attente.push((voix, newAmt))
le meilleur retour
«» "

Appliquer `BFS` deux fois: une fois pour le Jour 1 (à partir de `initialMonnaie`), une fois pour le Jour 2 (à partir de *toutes* devises que vous possédez après le Jour 1). La réponse est simplement "meilleur[initialMonnaie]" après le deuxième BFS.

---

2.4 Pourquoi pas DFS ou DP?

Pourquoi Ce n'est pas idéal pour le jour Échange
- C'est pas vrai.
**DFS**. Petite profondeur, recherche exhaustive du chemin. Autres
**Programmation dynamique**= Espace grand état== Nécessite une mémoire `O(V^2)` – inutile pour ≤ 10 bords. Autres
**Bellman-Ford**.Détection de cycle dans l'espace de log. Autres
**Floyd–Warshall**=Distances toutes paires="O(V^3)" – surtuber pour ce petit graphique. Autres

La méthode BFS est * plus légère*, * plus rapide* et * plus claire* – exactement ce que les intervieweurs recherchent.

---

### 2.5 Passage du code

Ci-dessous vous trouverez les implémentations complètes annotées dans **Java**, **Python** et **C++**. Chacun suit le même schéma :

1. **Construire le graphique** (bidirectionnel).
2. **Run Jour 1 BFS** pour peupler `amountJour1`.
3. **Run Day 2 BFS** ensemencée de "mountDay1".
4. **Return** `amountDay2[initialMonnaie]`.

> *Voir la section "Test Harness" pour un exemple. *

---

2.6 Cas de bord et sécurité numérique

- **Monnaies inaccessibles** – défaut par rapport au montant initial («1.0»).
- **Zero division** – jamais se produire parce que tous les taux > 0.
- **Précision** – L'utilisation de doubles/floats est bonne; le produit de ≤ 20 multiplicateurs reste dans la plage.

---

2.7 Dernier départ

LeetCode 3387 est un problème *graph déguisé en puzzle financier*. La solution optimale et conviviale de l'intervieweur est une BFS** qui respecte le caractère bidirectionnel des métiers.

Que vous l'écriviez dans **Java** avec `HashMap`, **Python** avec dictionnaires, ou **C++** avec `unordered_map`, la logique sous-jacente reste identique. Les extraits de code ci-dessus illustrent le même algorithme *exacte*, adapté aux langages idiomatiques.

**Codage heureux!**

---

### 2.8 Références et lectures supplémentaires

- Problème de LeetCode 3387 – [Link](https://leetcode.com/problèmes/maximize-amount-après-deux jours de conversion/)
- Graph Traversal: BFS vs DFS – [GeeksforGeeks] (https://www.geeksforgeeks.org/breath-first-search-or-bfs-for-a-graph/)
- Bellman-Ford Algorithm – [Wikipedia](https://en.wikipedia.org/wiki/Bellman%E2%80%93Ford_algorithm)
- Floyd–Warshall All-Pairs Courtest Path – [Coursera](https://www.coursera.org/lection/algorithms-ongraphs/floyd-warshall-shortest-paths-5B6g8)

---

> *En maîtrisant la stratégie BFS pour LeetCode 3387, vous serez prêt à vous attaquer à tout problème d'échange basé sur des graphiques qui vient à votre manière. *

---

**Bonne solution!**