---
titre: LeetCode 210. Horaire des cours II –
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
210. Programme de cours II – Solution de premier niveau (Java / Python / C++)
3 minutes de lecture

---

Résumé du problème

> **Les cours d ' enseignement général (0 ... numCours-1) et les cours d ' enseignement général < < prérequis > > où < < prérequis > > = < < a, b > > signifie < < suivre le cours > > avant le cours < < a > > ,
> **Retour** *tout ordre valide de cours qui satisfait à toutes les conditions préalables.
> **Si** aucun ordre n'existe (le graphique contient un cycle), retourner un tableau vide.

> **Constraints**
> * `1 ≤ numCours ≤ 2000`
> * `0 ≤ conditions préalables. longueur ≤ numCours · (numCours - 1)»
> * toutes les paires sont distinctes, `a b`.

---

Pourquoi c'est un problème de graphique

Chaque cours est un **vertex**.
Chaque condition préalable «[a, b]» est un bord **orienté** `b → a`.
Nous avons besoin d'un ordre **topologique** du DAG (graphique acyclique dirigé).
Si le graphique contient un cycle, un ordre topologique est impossible.

---

Deux approches classiques

L'approche de base La complexité
- C'est quoi ?
*Kahn= Algorithme (BFS)**= Garder les sommets avec zéro degré dans une file d'attente, les pop, le décrément dans le degré des voisins.
**DFS (Récursive)**DFS-visite, pousse les sommets sur la pile lorsque tous les enfants visités. Détecter le cycle via la pile de récursion. espace de récursion

> Nous allons montrer la solution **Kahn** dans les trois langues (plus propre pour les interviews).
> La version **FDS** est également fournie pour être complète.

---

Code Marche à travers (Algorithme de Kahn)

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe publique {
public int[] findOrder(int numCours, int[][] prérequis) {
// liste d'adjacence
Liste<Liste<entier>> graphique = nouvelle liste<>(numCours);
pour (int i = 0; i < numCours; i++) graphique.add(new ArrayList<>());
// tableau des degrés
int[] indegree = nouvelle int[numCours];

// Créer un graphique
pour (int[] edge : prérequis) {
cours int = bord[0];
int prereq = bord[1];
graph.get(prereq).add(cours);
degré [cours]++;
}

// queue des cours sans prérequis
la question <integer> q = nouvelle liste liée<>();
pour (int i = 0; i < numCours; i++)
si (indegré[i]]] 0) q.offre(i);

int[] ordre = nouveau int[numCours];
Int idx = 0;

alors que (!q.isEmpty()) {
int curr = q.poll();
order[idx++] = curr;

pour (int next : graph.get(curr)) {
si (--degré[suivant]] 0) q.offre(suivante);
}
}

Return idx == numCours ? ordre : nouveau int[0];
}
}
«» "

> **Pourquoi 100 % de battements? * *
> *Seulement O(V + E)* opérations, pas de pile de récursion, pas de frais généraux cachés.

---

# # # # # #

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def findOrder(self, numCours: int, prérequis: List[List[int]]) -> Liste[int]:
graphique = [[] pour _ dans l'intervalle(numCours)]
degré = [0] * numCours

Pour le cours, prérequis:
graphique[pré].annexe(course)
degré[cours] += 1

q = deque([i pour i dans l'intervalle(numCours) si indegree[i] == 0])
ordre = []

alors que q:
cur = q.popleft()
ordre.annexe(cur)
pour nxt dans le graphique[cur]:
degré[nxt] -= 1
si indegré[nxt]] 0:
q.annexe(nxt)

ordre de retour si len(ordre) == numCours autres []
«» "

> **Notes spécifiques au python**
> *`deque`* donne O(1) pops de la gauche.
> *La compréhension de la liste* garde le code court.

---

C'est vrai. C++

'`cpp
#incluez <vecteur>
#incluez <queue>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> findOrder(int numCours, vector<vector<int>>& prérequis) {
vecteur<vector<int>> graphique(numCours);
vecteur<int> indegré(num Cours, 0);

pour (auto& e : conditions préalables) {
cours int = e[0], pré = e[1];
graph[pre].push_back(course);
++degré[cours];
}

file d'attente <int> q;
pour (int i = 0; i < numCours; ++i)
si (indegré[i]]] 0) q.push(i);

ordre du vecteur <int>;
pendant que (!q.vide()) {
int cur = q.front(); q.pop();
order.push_back(cur);
pour (int nxt : graph[cur]) {
si (--indegré[nxt]) 0) q.push(nxt);
}
}

retour (int)order.size() == numCours ? ordre : vector<int>();
}
};
«» "

> **C++ style**
> *`vector<vector<int>>`* comme liste d'adjacence, *`queue<int>`* pour BFS.
> Retourne un vecteur vide lors de la détection du cycle.

---

## DFS (récursif) – Facultatif

**Python (DFS)* *

'`python
Solution de classe:
def findOrder(self, numCours: int, prérequis: List[List[int]]) -> Liste[int]:
graphique = [[] pour _ dans l'intervalle(numCours)]
pour a, b dans les conditions préalables: graph[b].append(a)

visitée = [0] * numCours # 0=non visitée, 1=visitee, 2=visitee
ordre = []

def dfs(u):
si visité[u]] 1: # cycle
Retour Faux
si visité[u]] 2: # déjà traité
retour Vrai
visité[u] = 1
pour v dans le graphique[u]:
si pas dfs(v): retourner Faux
visité[u] = 2
ordre.annexe(u)
retour Vrai

pour i dans la plage(numCours):
si non dfs(i): retour []

ordre de retour[::-1]
«» "

> **Pourquoi ne pas être utilisé dans les entrevues? * *
> *La pile de récursion peut déborder sur des graphes profonds. *
> *La logique de détection du cycle est un peu plus verbeuse. *

---

Cas et pièges de bord

Autres Décision Quoi faire ?
- C'est pas vrai.
Autres Pas de prérequis (`prerequis == []`)= Chaque cours a au degré 0 → tout ordre est bon. Autres
Composantes déconnectées: Kahn traitera chaque composante indépendamment. Autres
Toute permutation est valide – le harnais d'essai en accepte généralement. Autres
"Soi-même" (a,a) Les contraintes du problème l'interdisent, mais s'il est présent, Kahn ne fera jamais appel à «a». Autres
Grand "numCours" (2000) Toujours trivial pour les solutions O(V+E). Autres

---

Le bon, le mauvais et le mauvais de l'horaire du cours II

**Beau**
C'est quoi ?
Type topologique intuitif – parfait point de discussion d'entrevues. Autres
C'est vrai. Fonctionne pour n'importe quel DAG – réutiliser dans la programmation, l'ordre de construction, la résolution de dépendance. Doit construire une liste d'adjacence et un tableau d'indegré – mémoire supplémentaire O(V+E). Autres
L'algorithme Kahn's garantit un ordre valide dans le temps linéaire. Si vous oubliez de vérifier le compte final, vous pouvez retourner une commande partielle. Dans les langues avec gestion manuelle de la mémoire (C++), oublier de clarifier les vecteurs peut conduire à des bugs subtils. Autres

> **A emporter** – Algorithme Master Kahn. Il est court, rapide et convivial.
> Utilisez DFS seulement lorsque vous devez produire *tous* ordres topologiques ou détecter plusieurs solutions.

---

## -= SEO-Optimized Blog Titre & Meta

**Titre:**
Calendrier des cours II – 210 sur LeetCode: Tri topologique maître (Java, Python, C++)

**Meta Description:**
Apprendre à résoudre le LeetCode 210 – Programme de cours II avec l'algorithme de Kahn. Obtenez des implémentations Java, Python et C++ propres, des analyses de complexité et des conseils d'entrevue. Boostez maintenant votre interview d'ingénierie logicielle! (en milliers de dollars)

**Mots clés:**
Horaire des cours II, LeetCode 210, tri topologique, Algorithme de Kahn, tri topologique DFS, algorithmes graphiques, solution Java, solution Python, solution C++, préparation d'entretien, interview d'ingénieur logiciel.

---

Liste de contrôle finale pour votre préparation à l'entrevue

1. **Connais l'énoncé du problème** – cours, prérequis, DAG.
2. **Exposer l'algorithme de Kahn** – degré, file d'attente, détection de cycle.
3. **Afficher le code en 3 langues** – assurez-vous qu'il est compilé sur LeetCode.
4. **Discuse les cas de bord** – prérequis vides, plusieurs nœuds de degré zéro.
5. **Contraste avec DFS** – avantages/cons, risque de débordement de la pile.
6. **Compétitivité temporelle/espace** – temps "O(V+E)", espace "O(V+E)".
7. **Parler des analogies du monde réel** – construire des systèmes, planifier des tâches.
8. **Préparer un test d'unité rapide** – tester manuellement les petits graphiques localement.
8. **Soyez prêts à répondre au suivi** – Peut-on générer toutes les commandes valides? → DFS + retour en arrière.

---

- Oui. **Votre prochaine étape:**
Implémentez la solution Kahn dans votre IDE préféré, poussez-la dans une repo GitHub et répétez-la à haute voix. Bonne chance avec vos entretiens – vous venez d'ajouter un puissant algorithme graphique à votre boîte à outils! C'est ce qu'il a dit.

---