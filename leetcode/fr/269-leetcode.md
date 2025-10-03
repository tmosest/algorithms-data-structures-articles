---
titre: LeetCode 269. Dictionnaire étranger - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Dictionnaire Alien – Une solution complète et multilingue
*Python C++ – en plus d'un billet de blog favorable au SEO qui peut vous faire passer cet entretien ! *

---

- Oui. 1. Récapitulation des problèmes (Code de bord 269)

> **Don** une liste de mots qui sont déjà triés selon un alphabet extraterrestre **inconnu**.
> **Tâche**: Déduire un ordre possible des lettres.
> *Retourner une chaîne vide si la commande d'entrée est impossible. *

**Exemples**

Entrée Sortie
C'est quoi ?
"["wrf", "er", "ett", "rftt"] ""wrf" Autres
"["z", "x"] ""zx"" Autres
* (invalide)

**Contrôles* *

* `1 <= words.longueur <= 100`
* `1 <= mots[i].longueur <= 100`
* Tous les mots se composent de lettres anglaises minuscules seulement.

---

- Oui. 2. L'algorithme – Tri topologique avec Kahn (BFS)

1. **Construire un graphique**
Pour chaque paire de mots adjacents, trouvez le premier caractère différent.
*Si word1 est plus long mais un préfixe de word2 → impossible. *

2. **Ajouter les bords**
Si `word1[i] != word2[i]`, alors `word1[i]` vient **avant** `word2[i]`.
Edge: `word1[i] → word2[i]`.

3. L'algorithme de Kahns**
* Tableau en degrés pour les 26 lettres.
* Requête des nœuds avec 0 au degré.
* Popedly pop, append to result, décrément voisins, in-degree.

4. **Validité**
*Si résultat longueur < nombre de lettres distinctes → cycle → retour `""`. *

5. **Retour** la chaîne concaténée de l'ordre.

Cette solution fonctionne dans **O(V + E)** où
`V = 26` (lettres), `E ≤ mots.longueur * moyenne_word_longueur`.

---

- Oui. 3. Mise en œuvre du code

Voici des implémentations propres, prêtes à la production dans **Java, Python et C++**.

3.1 Java (Algorithme de Kahn)

"Java
Importation de java.util.*;

solution de classe publique {
chaîne publique alienCommander(mots de chaîne) {
// 1. Graphique de construction
Liste de la nouvelle liste des tableaux <>(26);
pour (int i = 0; i < 26; i++) graphique.add(nouveau HashSet<>());
int[] indegree = nouveau int[26];
booléen[] présent = nouveau booléen[26];

pour (Pièce w : mots) {
pour (charc : w.toCharArray()) présent[c - 'a'] = vrai;
}

pour (int i = 0; i < words.longueur - 1; i++) {
Chaîne w1 = mots[i];
Chaîne w2 = mots[i + 1];
int minLen = Math.min(w1.length(), w2.length());
Int diff Idx = -1;
pour (int j = 0; j < minLen; j++) {
si (w1.charAt(j) != w2.charAt(j)) {
diffIdx = j;
pause;
}
}

Si (diffIdx) -1) {
si (w1.length() > w2.length()) retourne "; // préfixe la violation de la règle
} autre {
int u = w1.charAt(diffIdx) - 'a';
int v = w2.charAt(diffIdx) - 'a';
si (!graph.get(u) contient(v) {
graphic.get(u).add(v);
degré[v]++;
}
}
}

// 2. Algorithme de Kahn
Queue<integer> q = nouveau ArrayDeque<>();
pour (int i = 0; i < 26; i++) {
si (présentent [i] && indegree[i]] 0) q.offre(i);
}

StringBuilder sb = nouveau StringBuilder();
Int traité = 0;
alors que (!q.isEmpty()) {
int u = q.poll();
sb.appendice((char) (u + 'a));
traitement++;
pour (int v : graph.get(u)) {
si (--degré[v]]] 0) q.offre(v);
}
}

// 3. Détecter le cycle
si (traité != countPrésent(présent)) retourne ";
retour sb.toString();
}

Int privé countPresent(boolean[] present) {
cnt = 0;
pour (booléen b : présent) si (b) cnt++;
retour cnt;
}
}
«» "

> **Pourquoi ce code? * *
> * Utilise `Set` pour éviter les bords dupliqués.
> * Règle de préfixe des poignées (`w1` plus long que `w2`).
> * Conserve la complexité O(26 + bords).
> * Séparation propre des étapes de lecture.

3.2 Python (DFS + Kahn hybride)

'`python
de collections import defaultdict, deque
de taper l'importation Liste

Solution de classe:
def alienOrder(self, words: List[str]) -> str:
1. Construire le graphique et les degrés
graphique = par défautdict(set)
endeg = [0] * 26
Présent = [Faux] * 26

pour w en mots:
pour ch in w:
présent[ord(ch) 97] = Vrai

pour w1, w2 dans zip(mots, mots[1:]):
min_len = min(len(w1), len(w2))
diff = -1
pour i dans range(min_len):
Si w1[i] != L'annexe I est modifiée comme suit:
diff = i
pause
Si diff == -1:
Si len(w1) > len(w2):
retour ""
Sinon:
u, v = ord(w1[diff]) - 97, ord(w2[diff]) - 97
si v n'est pas dans le graphique[u]:
graphic[u].add(v)
endeg[v] += 1

# 2. Kahn
q = deque([i pour i dans l'intervalle(26) si présent[i] et indég[i]== 0])
res = []
traité = 0

alors que q:
u = q.popleft()
Annexe(chr(u + 97))
traitées += 1
pour v dans le graphique[u]:
indég[v] -= 1
si indég[v]] 0:
q.appendice v)

si traité != somme(présent):
retour ""
retourner "".join(res)
«» "

> ** Touche pyronique**
> * `defaultdict(set)` garde l'unicité des bords.
> * Utilise `deque` pour une FIFO efficace.
> * Vérification du compte actuel d'un liner.

*## 3.3 C++ (Modern STL, Kahn)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne alienOrder(vecteur<string>& mots) {
vectoriel <unordered_set<int>> graphique(26);
vecteur<int> indég(26, 0);
vecteur<bool> présent(26, faux);

// marquer les lettres présentes
pour (cost string & w : mots)
pour (charc : w) présent[c - 'a'] = vrai;

// Créer un graphique
pour (size_t i = 0; i + 1 < words.size(); ++i) {
const string& w1 = mots[i];
Const string& w2 = mots[i + 1];
int minLen = min(w1.size(), w2.size());
Int diff = -1;
pour (int j = 0; j < minLen; ++j) {
si (w1[j] != w2[j]) { diff = j; break; }
}
Si (diff) -1) {
si (w1.size() > w2.size()) retourne ";
} autre {
u = w1[diff] - 'a';
int v = w2[diff] - 'a';
si (!graph[u].count(v)) {
graphic[u].insert(v);
++indég[v];
}
}
}

// Kahn
file d'attente <int> q;
pour (int i = 0; i < 26; ++i)
si (présenter [i] && indég[i]] 0) q.push(i);

ordre des chaînes;
Int traité = 0;
pendant que (!q.vide()) {
i) u = q.front();
order.push_back(char('a' + u));
++ traitées;
pour (int v : graph[u]) {
si (--indeg[v]] 0) q.push(v);
}
}

int présent Cnt = count(present.begin(), present.end(), true);
si (transformé != presentCnt) retourne ";
l'ordre de retour;
}
};
«» "

> **C++ Faits saillants* *
> * Utilise `unordered_set` pour les contrôles d'existence de bord O(1).
> * `queue<int>` pour BFS.
> * Style direct qui est facile à vérifier lors d'une entrevue.

---

- Oui. 4. Article de blog: -Le bon, le mauvais, et l'atroce problème du dictionnaire étranger

> **Audience cible** – développeurs front‐end/back‐end, passionnés d'algorithmes, candidats à l'entrevue.
> ** Mots-clés du référencement** – dictionnaire extraterrestre, tri topologique, algorithme Kahn, LeetCode 269, algorithme d'entretien, graphe traversal, détection de cycle.

---

4.1 Introduction

> Quand un recruteur vous montre une liste de mots "alien" et demande l'ordre des lettres, ils sont vraiment tester votre capacité à traduire un ordre *partiel* dans un ordre *total*.
> Le problème LeetCode **269. Alien Dictionary** est l'exercice canonique qui emballe *graph construction*, *cycle détection* et *topological tri* en un seul défi de taille.

> Dans cet article, nous allons décomposer **le bon**, **le mauvais**, et **la laid** du problème, passer à travers la solution la plus efficace, et partager des prises d'entrevue clés qui impressionneront les gestionnaires d'embauche.

---

4.2 Les bonnes – Pourquoi Ce problème est

Aspect Pourquoi ça aide
C'est pas vrai.
Le tri avec des informations incomplètes est courant dans **la résolution de dépendance**, **les systèmes de construction** et **la planification des tâches**. Autres
Autres **Compact pourtant riche** . Il couvre *la manipulation de chaînes*, *la théorie du graphique*, *BFS/DFS* et *la détection du cycle* en une seule fois. Autres
**Plusieurs sorties valides** Autres
**Échelle facile à étendre : ajouter Unicode, gérer des alphabets plus grands ou incorporer des poids. Autres

> **Takeaway**: Maîtriser ce problème indique que vous êtes à l'aise avec **abstraction des contraintes de commande** – exactement ce que beaucoup d'entreprises technologiques recherchent.

---

### 4.3 Les mauvaises – Pièges communs

Pourquoi ça fait mal ?
C'est quoi ?
**Ignorer la règle du préfixe**. Un mot plus long qui préfixe un mot plus court (par exemple, `["abc","ab"]`) doit retourner `""". Ne pas vérifier cela brise la logique. Autres
**L'ajout du même bord plusieurs fois gonfle le nombre de degrés et peut causer une mauvaise détection du cycle. Autres
**En supposant que les 26 lettres existent**= Certains mots pourraient omettre des lettres; construire le graphique pour les nœuds inutilisés peut conduire à des nœuds supplémentaires avec zéro au degré qui ne devraient pas apparaître dans la réponse. Autres
**L'utilisation de DFS sans détection de cycle**DFS peut renvoyer une commande, mais vous devez encore détecter des back-edges pour gérer les entrées invalides. Autres
**Over-optimizing hâtive**=Essai de micro-optimiser avec des bits ou des files d'attente personnalisées avant d'obtenir la bonne logique est contre-productif. Autres

> **Check-list pour les intervieweurs**
> 1. Validation du préfixe.
> 2. Unicité des bords.
> 3. Corriger l'initialisation en degrés.
> 4. Détection du cycle.
> 5. Retournez la chaîne uniquement pour les lettres présentes.

---

#### 4.4 La folie – Les causes et la complexité cachée

Pourquoi c'est difficile
- Oui.
**L'exemple `["a","a"]` est valide mais devrait encore produire `"a"`. Autres
**Sous-graphes déconnectés** , des lettres qui n'apparaissent jamais dans un bord peuvent être placées n'importe où ; tout ordre qui respecte les contraintes connues est bon. Autres
**Longe chaîne de contraintes**= Entrée comme "["a", "b", "c", ...]` tests si vous manipulez des récursions profondes (DFS) ou des opérations de queue longues (Kahn) gracieusement. Autres
**Dépendance circulaire**Le terme `["z","x","z"]` indique un cycle qui doit être pris. Autres
**Sparse vs graphic dense**. Les données réelles peuvent avoir 26 nœuds mais seulement une poignée de bords. Assurez-vous que votre algorithme fonctionne dans `O(V+E)` indépendamment. Autres

> **Conseil pro**: Utilisez une matrice *boolean* ou *unordered_set* pour protéger les bords contre les duplicatas, et exécutez un "indegré" rapide. 0 ' file d'attente pour attraper les cycles tôt.

---

4.5 La solution efficace (Algorithme de Kahn)

1. **Graphique Construction* *
*Scan toutes les paires adjacentes, trouver le premier caractère différent, et ajouter un bord. *

2. ** Calcul d'ensemble* *
*Track combien de prérequis chaque lettre a. *

3. **Traitement topologique (BFS)* *
*Démarrer avec tous les nœuds zéro-en-degré, pop, annexe au résultat, voisins de décrément. *

4. **Détection du cycle**
*Si le nombre de nœuds traités est inférieur au nombre de lettres distinctes, un cycle existe. *

> **Complexité**:
> *Time*: `O(V + E)` → `O(26 + bords)` → pratiquement linéaire.
> *Space*: `O(V + E)` → petits frais généraux constants.

---

4.6 Faits saillants du code (Java, Python, C++)

Pourquoi ça compte ?
- C'est quoi ?
**Java**= `Set<integer>` pour les bords, `Queue<integer>` pour BFS== Évite les bords en double, garantit FIFO=
**Python**="defaultdict(set)", `deque`=" Syntaxe concise, intégré rapidement="
**C++**= `unordered_set`, `queue<int>== Commande de bas niveau, garanties de compilation==

> *Toutes les implémentations sont commentées et prêtes à être collées dans une console d'entretien. *

---

4.7 Entretien Points de discussion prêts

1. **Exposer le graphique** – Afficher comment les différences de chaînes se traduisent par des bords dirigés.
2. **Énoncer la règle du préfixe** – Mentionnez le cas de bord et pourquoi elle compte.
3. **Choisir Kahn vs DFS** – Décrivez les avantages et les inconvénients de chaque méthode topologique.
4. **Détection de cycle** – Démontrer la compréhension des données rétrospectives ou de la vérification des comptes traités.
5. **Edge Uniqueness** – Parlez de l'utilisation d'un jeu de hachage pour éviter la surestimation en degrés.

> **Résultat**: Vous démontrerez *code propre et durable* et *raison algorithmique solide* — une recette pour une réponse d'entrevue 5 étoiles.

---

### 4.7 Conclusion

> Le problème **Alien Dictionary** est plus qu'un simple puzzle graphique.
> Il s'agit d'un microcosme de **gestion de la dépendance**, d'un terrain de jeu de la théorie de la graph**, et d'un **test d'hygiène de bord**.
> En maîtrisant les *bonnes* (analogies du monde réel), en évitant les *mauvaises* (bogues communes) et en manipulant les *grosses* (cases de référence), vous transformerez une prompte apparemment fantasque en une vitrine de vos prouesses algorithmiques.

> Qu'il s'agisse d'un ingénieur chevronné qui se prépare à un entretien *software-engineering* ou d'un codeur junior visant ce prochain rôle, ce problème est incontournable dans votre boîte à outils en algorithme.

---

4.8 Pensée finale

> Si vous pouvez résoudre le dictionnaire Alien, vous pouvez résoudre *toute* problème de programmation où l'ordre compte, même si vous manquez certaines pièces du puzzle. (en milliers de dollars)

> ** Bon codage, et que votre tri topologique soit toujours valide !**

---

- Oui. 5. Clôture

> 1. **Run** les solutions fournies localement.
> 2. **Pratique** le problème des variations (par exemple, alphabets personnalisés).
> 3. **Lire** l'article, mettre en évidence les principaux choix d'entrevues, et les utiliser pour répondre.
> 4. **Partager** votre code sur GitHub ou une plate-forme de codage pour la communauté à voir.

> Bonne chance et rappelez-vous : *un alphabet bien trié peut ouvrir la porte à votre prochain travail ! *

---

N'hésitez pas à adapter l'article à votre propre voix ou à ajouter des anecdotes personnelles. Joyeux entretien !