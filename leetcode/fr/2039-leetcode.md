---
titre: LeetCode 2039. Le temps où le réseau devient idle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2039. Le moment où le réseau devient Idle
> **Moyenne – Code de Leet**

Le problème est un problème classique de graphique de style interview qui teste votre capacité à:

* Construire un graphique non dirigé à partir des listes de bord
* Calculer les distances les plus courtes avec un seul BFS
* Raison de la simulation d'événements basée sur le temps sans simuler réellement chaque seconde

Vous trouverez ci-dessous des implémentations propres et prêtes à la production dans **Java, Python et C++**.
Après le code, nous plongeons dans un blog **SEO-friendly** qui explique l'algorithme, les cas de bords que vous devriez surveiller, et pourquoi cette solution est assez rapide pour les limites de problèmes (jusqu'à 105 nœuds/arêtes).

---

1. Aperçu de la solution

Étape Ce que nous faisons Pourquoi ça marche
C'est pas vrai.
**Construisez une liste d'adjacence** pour le graphique non dirigé. Il permet la traversée du voisin O(1). Autres
Autres **BFS du nœud 0** pour trouver le plus court nombre de houblons (distance) à tous les autres serveurs. Le graphique n'est pas pondéré; le BFS donne des longueurs de parcours exactes les plus courtes en O(N+E). Autres
Autres Pour chaque serveur de données *i* (i > 0) calcul: <br>• *roundTrip* = 2 × dist[i] <br>• *lastSend* = -(roundTrip – 1) / patience[i] × patience[i] <br>• *idleTime* = dernier Send + roundTrip=1 *lastSend* est l'horodatage du dernier message que le serveur renvoye *avant que la réponse master=1 arrive. Autres
Autres Réponse = **max(idleTime) + 1**. Autres

L'algorithme fonctionne dans **O(N + E)** temps et utilise **O(N + E)** mémoire.

---

- Oui. 2. Code

### Java

"Java
Importation de java.util.*;

solution de classe {
réseau public intBecomesIdle(int[][]] bords, int[] patience) {
int n = patience. longueur;

// 1. Créer une liste d'adjacence
Liste <entier>[] g = nouvelle liste de distribution[n];
pour (int i = 0; i < n; i++) g[i] = nouveau tableau <>();
pour (int[] e : bords) {
g[e[0]].add(e[1]);
g[e[1]].add(e[0]);
}

// 2. BFS du maître (node 0)
int[] dist = nouvelle int[n];
les tableaux.fill(dist, -1);
Queue<integer> q = nouveau ArrayDeque<>();
q.add(0);
dist[0] = 0;
alors que (!q.isEmpty()) {
int u = q.poll();
pour (int v : g[u]) si (dist[v] == -1) {
dist[v] = dist[u] + 1;
q.add(v);
}
}

// 3. Calculer le dernier temps de ralenti
réponse int = 0;
pour (int i = 1; i < n; i++) {
Int roundTrip = 2 * dist[i];
int dernier Envoyer = ((roundTrip - 1) / patience[i]) * patience [i];
int ralenti = dernier Envoyer + rond Voyage;
réponse = Math.max(réponse, inactif);
}
réponse de retour + 1; // +1 parce que l'inactif commence après la dernière réponse
}
}
«» "

Python

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def réseau Deviens Idle(self, bords: List[List[int]], patience: List[int]) -> Int:
n = len(patience)

# 1. liste d'adjacence
g = [[] pour _ dans l ' intervalle n)]
pour u, v dans les bords:
g[u].appendice(v)
g[v].append(u)

2. Distances de l ' EFS
dist = [-1] * n
dist[0] = 0
q = deque([0)]
alors que q:
u = q.popleft()
pour v en g[u]:
si dist[v] == - 1 :
dist[v] = dist[u] + 1
q.appendice v)

3. calculez les temps de repos
ans = 0
pour i dans la plage (1, n):
round_trip = 2 * dist[i]
Last_send = ((round_trip - 1) // patience[i]) * patience [i]
_temps_inactif = dernière_send + aller-retour
ans = max(ans, _temps inactif)

retour ans + 1
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
réseau int Deviens Idle(vecteur<vecteur<int>>& bords, vecteur<int>& patience) {
int n = patience.size();
vecteur<vector<int>> g(n);
pour (auto &e : bords) {
g[e[0]].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

vecteur<int> dist(n, -1);
file d'attente <int> q;
dist[0] = 0; q.push(0);
pendant que (!q.vide()) {
i) u = q.front();
pour (int v : g[u]) si (dist[v] == -1) {
dist[v] = dist[u] + 1;
q.push(v);
}
}

Int ans = 0;
pour (int i = 1; i < n; ++i) {
Int roundTrip = 2 * dist[i];
int dernier Envoyer = ((roundTrip - 1) / patience[i]) * patience [i];
int ralenti = dernier Envoyer + rond Voyage;
ans = max(ans, au ralenti);
}
retourner les an + 1;
}
};
«» "

---

3. SEO-Optimized Blog Post

Titre
**LeetCode 2039 – Le moment où le réseau devient Idle**
*Fast BFS Solution (Java, Python, C++) – Master Interview Algorithms*

---

Description de la méta
Solve LeetCode 2039 Le temps où le réseau devient Idle avec un algorithme BFS + maths optimal. Lisez notre explication étape par étape, le code Java/Python/C++ et les conseils d'entrevue. Parfait pour les développeurs de backend et les ingénieurs réseau!

---

Introduction

LeetCode 2039 vous demande de trouver la première seconde quand un réseau de serveurs devient inactif après une série d'échanges de messages. Bien que la description du problème ressemble à un puzzle de simulation, une approche mathématique propre avec BFS donne une solution O(N+E). Ce post passe par cette approche, l'intuition derrière la formule clé, et pourquoi le code fonctionne assez rapidement pour les limites supérieures (105 nœuds et bords).

---

Récapitulation des problèmes

* **Graphique** – Non dirigé, non pondéré.
* **Serveur maître** – noeud 0.
* ** Serveurs de données** – nœuds 1...n‐1.
* **Message** – chaque serveur de données envoie son premier message à la fois 0.
* **Renvoyez la règle** – toutes les *patiences[i]* secondes après le dernier envoi, si aucune réponse n'est arrivée.
* **Objectif** – première seconde quand aucun message n'est en transit.

---

# # # # Une perspective fondamentale

1. **La distance la plus courte est importante** – car chaque message suit le chemin le plus court*.
2. **Temps de parcours** = "2 * dist[i]".
3. **Dernière réponse** – le plus grand multiple de "patient[i]" qui est *strictement* avant l'arrivée de la réponse.
«» "
lastSend = -(roundTrip – 1) / patience[i] * patience [i]
«» "
4. **Horaire du serveur i** = `lastSend + roundTrip`.
5. **Travail au ralenti** = "max(idleTimes) + 1".

Pourquoi la formule du plancher ?
Si une réponse arrive à l'heure `roundTrip`, toute réenvoi à `roundTrip` ou plus tard est inutile.
Ainsi nous trouvons le plus grand temps d'envoi qui est `< RoundTrip`.
Le "(roundTrip – 1)" Astuce garantit que si `roundTrip` est exactement un multiple de `patient[i]` On ne compte pas le dernier envoi.

---

L'algorithme

- Oui. 1. Construire le graphique
Les listes d'adjacence sont la façon la plus simple de représenter des graphiques clairs et non dirigés.
'`cpp
pour (auto &e : bords) {
g[e[0]].push_back(e[1]);
g[e[1]].push_back(e[0]);
}
«» "

- Oui. 2. BFS pour les distances
Comme les bords ne sont pas pondérés, un seul BFS du nœud 0 donne `dist[v]` pour chaque serveur `v`.
'`python
alors que q:
u = q.popleft()
pour v en g[u]:
si dist[v] == - 1 :
dist[v] = dist[u] + 1
q.appendice v)
«» "

- Oui. 3. Calculer les temps de poche
Pour chaque serveur `i` > 0:
Texte
roundTrip = 2 * dist[i]
LastSend = plancher(round Voyage - 1) / patience[i]) * patience [i]
inactif Temps = dernierEnvoyer + rondTrip
«» "
Prenez le maximum sur tous les serveurs et ajoutez 1.

---

Analyse de complexité

Complexité
- C'est quoi ?
Heure O(N+E)
L'espace O(N+E)

Les trois implémentations utilisent une seule file d'attente, une liste d'adjacence et un tableau de distance. Même dans le cas le plus défavorable (`N = E = 105`), le BFS visite chaque bord deux fois – bien en dessous de la limite de 1 seconde de LeetCode.

---

Bon, mauvais, affreux.

La situation Que surveiller? Autres
-- -- -- -- -- -- -- -- --
**Patience[i] = 0** 1"). Ajouter un garde ou compter sur la garantie de problème. Autres
**roundTrip = 1**. La division de plancher gère le zéro correctement. Autres
Autres **Très grande patience** La formule donne "lastSend = 0". Autres
**Graphiques déconnectés** Cochez toujours `dist[i] != - Pour être en sécurité. Autres
**Huge S.O.**=La récursion de la cheminée (DFS) déborderait. Utilisez BFS itérative – pas de récursion. Autres

---

Pourquoi ce code de Leet limite

* **BFS** est linéaire dans les bords, pas en secondes.
* Tout arithmétique est temps constant par noeud.
* Aucune simulation de chaque seconde ne signifie que l'algorithme fonctionne en microsecondes, même pour 105 nœuds.

---

Liste de contrôle à emporter

- [ ] Créer une liste des dépendances (O(N+E))
- [ ] BFS de maître pour obtenir le plus court houblon
- [ ] Calculer `roundTrip`, `lastSend`, `idleTime "
- [ ] Retour `max(idleTime) + 1`
- [ ] Pas de DFS récursif → éviter le débordement de la pile
- [ ] Essai avec:
* Tous les serveurs ont `patience = 1` (faible-case resends)
* Certains serveurs avec une patience énorme (pas de résend)
* Grand arbre vs graphe dense

---

Mot final

LeetCode 2039 est une question d'entrevue *network-theory* déguisée en simulation. En se concentrant sur **shortestpaths** et un arithmétique soigné, vous pouvez le résoudre en un seul passage. Les implémentations Java, Python et C++ ci-dessus sont prêtes pour une soumission d'entretien de code et passeront les limites strictes de temps/mémoire du problème.

Bon codage ! C'est ce qu'il a dit.

---

Mots clés pour référencement

- LeetCode 2039
- Temps où le réseau devient Idle
- Solution BFS
- Java LeetCode 2039
- Python LeetCode 2039
- C++ LeetCode 2039
- Algorithme de ralenti réseau
- Algorithme du graphique d'entrevue
- Voie la plus courte
- Questions de l'entrevue de référence

N'hésitez pas à copier les extraits de code, à les modifier pour votre style de codage personnel ou à les utiliser comme référence d'étude. Bonne chance pour votre prochain entretien !