---
titre: LeetCode 1500. Conception d'un système de partage de fichiers -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1500. Concevoir un système de partage de fichiers – Solution à pile complète
C++*
> **Pourquoi devriez-vous lire ceci* *
> * Obtenez une implémentation propre et prête à la production que vous pouvez déposer dans un test LeetCode.
> * Comprendre les compromis qui comptent dans une entrevue.
> * Apprenez à parler du problème.
> * Boost your SEO-Classed blog post or portfolio with ciblated keywords , tels que le système de partage de fichiers Leetcode 1500.** et **.

---

C'est pas vrai. Le problème en une seule phrase

Construisez une classe qui garde une trace des utilisateurs qui possèdent des morceaux d'un fichier, attribue le plus petit ID utilisateur inutilisé, supprime les utilisateurs, et retourne une liste triée de tous les utilisateurs qui possèdent actuellement un morceau demandé.

> ** Opérations principales**
> * `join(ownedChunks)` – ajouter un utilisateur, retourner le minimum d'ID libre.
> * `leave(userID)` – supprimer un utilisateur et libérer tous ses morceaux.
> * `request(userID, chunkID)` – donnez le chunk au demandeur et retournez la liste triée des utilisateurs qui le possèdent avant la requête.

---

Aperçu de la structure des données

Pourquoi ?
C'est quoi ?
**Identification de l'utilisateur le plus petit******Min-Heap** (`PriorityQueue` / `heapq`) Autres
**Chunk → Utilisateurs**= `Map<int, Set<int>>=`= O(1) ajouter/supprimer par chunk. Autres
**User → Chunks**= `Map<int, Set<int>>=`= O(1) nettoyage sur `leave`. Autres
**Sortie de sortie**="Liste<int>=" + `Collections.sort` / `sorted()=" Appelé uniquement sur demande; taille de sortie ≤ #utilisateurs. Autres

> **Complexité totale* *
> *`join`* – `O(k log n)` où *k* est le nombre de morceaux appartenant.
> *`leave`* – `O(k log n)`.
> *`request`* – `O(k log n)` pour ajouter le nouveau morceau + `O(u log u)` pour trier la sortie (`u` = nombre d'utilisateurs qui possèdent le morceau).

Toutes les opérations satisfont aux contraintes (= 104 appels, m ≤ 105, k ≤ 100).

---

Mise en œuvre du code

Voici les implémentations **ready‐to‐paste** dans **Java, Python et C++**.
Chacun suit la même logique : une file d'attente prioritaire pour les ID libres, deux cartes de hachage pour les relations bipartites, et un traitement minutieux des listes de morceaux vides.

---

### 2.1 Java

"Java
Importation de java.util.*;

classe publique Partage de fichiers {
final privé PriorityQueue<integer> freeIds = new PriorityQueue<>();
carte finale privée<enteger, Set<enteger>> chunkToUsers = nouveau HashMap<>();
carte finale privée<entier, définir<entier>> userToChunks = nouveau HashMap<>();
Int privé suivant Id = 0;

partage de fichiers public(int m) {
// Pré-alterner les touches du morceau (facultatif – paresseux init fonctionne aussi)
pour (int i = 1; i <= m; i++) {
chunkToUsers.put(i, nouveau HashSet<>());
}
}

*** Attribuer le plus petit ID utilisateur non utilisé */
public int join(Liste<Intéger> appartenant àChunks) {
int userId = freeIds.isEmpty() ? ++nextId : freeIds.poll();
Ensemble <entier> chunks = nouveau HashSet<>(titledChunks);
userToChunks.put(userId, morceaux);
pour (int chunk : ownedChunks) {
chunkToUsers.get(chunk).add(userId);
}
retour de l' utilisateur Id;
}

*** Supprimer un utilisateur et libérer tous ses morceaux */
congé non payé(int userID) {
freeIds.offre(userID);
Définir <integer> propriété = userToChunks.remove(userID);
si (propriété) null retour;
pour (int chunk : propriété) {
chunkToUsers.get(chunk).remove(userID);
}
}

*** Retourner la liste triée des utilisateurs qui possèdent le morceau; l'accorder au demandeur */
liste publique<integer> request(int userID, int chunkID) {
Définir <Integer> propriétaires = chunkToUsers.get(chunkID);
Liste <entier> res = nouvelle liste d'array<>(propriétaires);
Collections.sort(s);
si (!propriétaires.isEmpty()) {
propriétaire.add(userID);
userToChunks.get(userID).add(chunkID);
}
retour rés;
}
}
«» "

---

2.2 Python

'`python
importation heapq
de collections importer par défautdict
de taper l'importation Liste

classe Partage de fichiers & #160;:
def __init_(self, m: int):
# paresseux init de morceaux → utilisateurs
self.chunk_to_users = defaultdict(set) # key: chunk, value: set of user IDs
self.user_to_chunks = defaultdict(set) # key: user ID, valeur: set of chunks
self.free_ids = [] # min-heap des IDs libérés
self.next_id = 0 # prochain nouvel ID à attribuer

def join(self, owned_chunks: List[int]) -> Int:
user_id = heapq.heappop(self.free_ids) si soi-même. free_ids autre self.next_id + 1
si ce n'est pas soi. _ids libres :
Self.next_id = user_id
Sinon:
heapq.heapify(self.free_ids) # conserver la propriété de heap

self.user_to_chunks[user_id] = set(owned_chunks)
pour ch in own_chunks:
Self.chunk_to_users[ch].add(user_id)
retourner user_id

def leave(self, user_id: int) -> Aucun:
heapq.heappush(self.free_ids, user_id)
propriété = self.user_to_chunks.pop(user_id, set())
pour ch en propriété:
Self.chunk_to_users[ch].discard(user_id)

def request(self, user_id: int, chunk_id: int) -> Liste[int]:
propriétaires = self.chunk_to_users[chunk_id]
res = trié(s)
si les propriétaires:
propriétaire.add(user_id)
Self.user_to_chunks[user_id].add(chunk_id)
retour res
«» "

> *Note:* Python="s `defaultdict(set)` crée un jeu sur le premier accès, donc vous n'avez pas besoin de pré-alterner les touches `m`.

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe Partage de fichiers {
priorité_queue<int, vecteur<int>, plus<int>> gratuit Ids;
sans ordre_map<int, sans ordre_set<int>> chunkToUsers; // chunk -> utilisateurs
utilisateur non classé_map<int, non classé_set<int>> ToChunks; // utilisateur -> morceaux
int suivant Id = 0;

public:
Partage de fichiers(int m) {
// Préaffectation facultative: pas nécessaire pour la justesse
pour (int i = 1; i <= m; ++i) chunkToUsers[i] = {};
}

int joint(vecteur const<int>&propriétéChunks) {
int uid = freeIds.vide() ? ++suivantId : freeIds.top();
si (!freeIds.vide()) freeIds.pop();
si (uid > nextId) nextId = uid; // garder une trace de l'ID maximal utilisé

userToChunks[uid] = unordered_set<int>(ownedChunks.begin(), propriétaireChunks.end());
pour (int ch : ownedChunks) chunkToUsers[ch].insert(uid);
retour uid;
}

congé vide(int utilisateur Id) {
ids.push(userId);
auto it = userToChunks.find(userId);
si (it) l'utilisateurToChunks.end() retourne;
pour (int ch : it->seconde) chunkToUsers[ch].erase(userId);
userToChunks.erase(it);
}

vector<int> request(int user Id, partie int Id) {
auto & propriétaire = chunkToUsers[chunk Id];
vector<int> res(owners.begin(), owners.end());
tri(res.begin(), res.end());
si (!propriétaires.vide()) {
propriétaires.insert(userId);
userToChunks[userId].insert(chunkId);
}
retour rés;
}
};
«» "

> *Astuce:* Dans C++17+, `unordered_set` donne la moyenne O(1) insert/supprime. La `priority_queue` avec `plus grand<int>` se comporte comme un min‐heap.

---

Article du blog – Le bon, le mauvais, et le mauvais système de partage de fichiers (Leetcode 1500)

Introduction
> _ Concevoir un système de partage de fichiers est un problème d'entrevue classique qui teste votre capacité à modéliser une relation *bipartite*, choisir la bonne structure de données et garder votre code propre. Dans ce post, nous disséquerons le problème, marcherons dans les implémentations **Java/Python/C++** ci-dessus, et expliquerons les aspects *good*, *bad* et *ugly* que vous voulez évoquer dans un entretien d'embauche.

---

3.1 Pourquoi ce problème se complique
* **La pertinence du monde réel** – La même idée permet le partage de fichiers P2P, les CDN et la livraison de contenu dans le cloud.
* **L'intervieweur est convivial** – Les contraintes sont modérées (soit 104 opérations, taille du morceau ≤ 100), ce qui en fait un endroit agréable pour une entrevue de codage de 30 minutes.
* **Showcases data-structure fluency** – Parfait pour les gestionnaires d'embauche qui aiment voir **min-heap**, **hash maps** et **sets** en action.

> **Mots clés pour le référencement:** `File Sharing System Leetcode 1500`, `Concevoir une solution de système de partage de fichiers`, `Interview algorithme data structures`, `Java Python C++ implementation`.

---

### 3.2 Le *Bon* – Qu'est-ce que le problème vous apprend

Autres Comment ça aide
C'est pas vrai.
**Modélisation des graphiques** – La relation du morceau d'utilisateur est un graphique bipartite. Autres Montrez que vous pouvez résumer les contraintes du monde réel dans un problème de graphique. Autres
**Min-Heap pour l'attribution d'ID** – Garanties plus petites ID inutilisées. Démontrer la connaissance des files d'attente prioritaires et de leur complexité. Autres
**Deux cartes de hachage** – nettoyage O(1) sur `leave`. Souligne l'importance de l'indexation *bidirectionnelle* pour des suppressions efficaces. Autres
** initialisation lente** – Répartir uniquement les ensembles au besoin. Sensation de mémoire pour les grandes valeurs *m*. Autres

> **Conseil d'entrevue :** Lorsqu'on vous demande pourquoi avez-vous choisi un mini-pap? Si l'entrevue était un vrai système, nous pourrions aussi utiliser une liste libre ou un bitset si les ID étaient limités.

---

### 3.3 Le *Bad* – Où la mise en œuvre pourrait tomber à court

Question Conséquences Correction
- Oui.
** – Pré-allouer toutes les touches du morceau `m` utilise la mémoire ~O(m). Pas un problème pour LeetCode (m = 105), mais peut être dans un environnement restreint. Utilisez paresseux `defaultdict(set)` dans Python ou créez un ensemble sur le premier accès dans Java/C++. Autres
**Trier sur chaque demande** – "O(u log u)" peut être cher si de nombreux utilisateurs possèdent le même morceau. Autres La sortie triée domine le coût lorsque *u* est grand. Autres Conservez le jeu déjà trié (par exemple, `std::set<int>` dans C++) – compromis: insert/supprimer plus lentement. Autres
**Reconstruction de la file d'attente** – Dans Python, appeler `heapq.heapify` après `push`/`pop` est inutile parce que `heapq` maintient la propriété de tas automatiquement. Frais généraux mineurs, mais inoffensifs pour la taille du problème. Autres Supprimer la ligne manuelle `heapify`. Autres

> **Key Takeaway:** Lors d'une interview, vous devriez mentionner explicitement ces points—*=J'ai opté pour une minute parce que l'intervieweur a demandé la plus petite carte d'identité gratuite; si nous avions un budget de mémoire très serré, nous créerions paresseusement les clés du morceau.

---

3.4 Les cas les plus graves – les cas de bord et les cas de gotchas

1. **Liste de morceaux appartenant à Empty** (`join([])`) – obtient toujours un ID unique; vous ne devez pas l'insérer dans une carte de morceaux.
2. **Demander un morceau que personne ne possède** – La liste de retour est vide, mais vous accordez toujours le morceau au demandeur.
3. **Laisser un utilisateur inexistant** – Le code défensif ('pop' par défaut) empêche les accidents.
4. **Réutiliser des IDs libres** – La file d'attente prioritaire garantit la réutilisation de l'ID *le plus petit*; jamais réutiliser un ID toujours actif.

---

- Oui. Comment utiliser ceci dans votre prochaine entrevue

1. **Démarrer par le croquis de la structure des données** – Les intervieweurs adorent voir votre plan de haut niveau avant le code.
2. **Exposer la complexité** – Montrez que vous comprenez pourquoi chaque opération répond aux contraintes.
3. **Travaux de Mention** – J'ai utilisé un `HashSet` pour les utilisateurs par morceau pour obtenir O(1) supprimer; si nous voulions une sortie triée garantie sur chaque demande, nous pourrions le remplacer par un `TreeSet`, au prix d'O(log u) par insertion. (en milliers de dollars)
4. **Parler de l'évolutivité** – Si nous avions des millions d'utilisateurs, nous devrions passer à un bitset ou à un filtre à fleurs pour sauver la mémoire. (en milliers de dollars)

> **Interview :**
> *'I'd garder les deux cartes pour le nettoyage rapide, utiliser un min-heap pour attribuer le prochain ID libre, et trier seulement la liste des propriétaires sur demande. Cela garantit que chaque opération reste bien en dessous de la limite de 104 appels.

---

C'est pas vrai. Liste de contrôle de l'approche à suivre (SEO et portefeuille)

Point Que mettre en évidence
-- -- -- -- -- -- --
**Mots clés**="File Sharing System Leetcode 1500`, `Java implementation`, `Python solution`, `C++ interview algorithme`. Autres
**Cliquer pour copier le code Java, Python, C++. Autres
**Complexité**= Mention *O(k log n)* pour `join`/`leave` et *O(u log u)* pour `request`. Autres
**Trade-offs**= Montrez que vous considérez la mémoire par rapport à la vitesse (préallocation, init paresseux, types de jeu). Autres
**Exemple du monde réel**= Carte de **Peer-to-Peer** ou **Réseaux de livraison de contenu**. Autres

Utilisez les points ci-dessus pour créer un billet de blog poli, une entrée de portfolio ou une feuille de triche d'entrevue rapide. Bonne chance—**vous venez de transformer un problème de LeetCode en un point de discussion de carrière!* *