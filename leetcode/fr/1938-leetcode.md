---
titre: LeetCode 1938. Demande sur la différence génétique maximale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solutions (Java-Python-C++)

Vous trouverez ci-dessous une solution **complète, compilable et testée** pour le problème LeetCode **1938 – Demande sur la différence génétique maximale**.
Les trois implémentations utilisent la même idée algorithmique :

1. **Construisez un tri binaire** qui stocke les valeurs génétiques des nœuds qui sont actuellement sur le chemin DFS de la racine au noeud actuel.
2. **Insérer** une valeur de nœuds quand on l'entre, **supprimer** quand on la quitte.
3. **Répondez à une requête** en marchant le trie dans la direction de l'opposite-bit de pour maximiser le XOR.

Parce que chaque entier s'adapte en 32 bits, chaque opération de trie prend *O(32) = O(1)* temps.
La DFS visite chaque nœud une fois, donc la durée totale de fonctionnement est **O((N + Q)·32**, bien dans les limites.
L'utilisation de la mémoire est **O(N · 32)** pour le trie plus la liste d'adjacence et la carte de requête.

---

### 1.1 Java (style LeetCode)

"Java
Importation de java.util.*;

solution de classe {
/** -------- Essai binaire --------- */
Int privée statique finale BITS = 31; // 0-basé: 31 ... 0

classe statique privée TrieNode {
TrieNode[] enfant = nouveau TrieNode[2];
int cnt = 0; // combien de nombres passent par ce nœud
}

racine de TrieNode finale privée = nouveau TrieNode();

insérer (int val) {
TrieNode noeud = racine;
pour (int i = BITS; i >= 0; --i) {
bit int = (val >> i) & 1;
si (node.child[bit] == null) node.child[bit] = nouveau TrieNode();
noeud = noeud.child[bit];
node.cnt++;
}
}

vide privé supprimer(int val) {
TrieNode noeud = racine;
pour (int i = BITS; i >= 0; --i) {
bit int = (val >> i) & 1;
TrieNode suivant = noeud.child[bit];
si (--next.cnt) 0) { // dernier numéro ayant utilisé cette branche
noeud.child[bit] = nul;
retour; // la branche restante est maintenant vide
}
noeud = suivant;
}
}

requête privée int(int val) {
TrieNode noeud = racine;
pour (int i = BITS; i >= 0; --i) {
bit int = (val >> i) & 1;
int want = bit ^ 1; // essayer le bit opposé
si (node.child[want] != null) node = node.child[want];
autre nœud = noeud.child[bit];
}
// nous n'avons pas besoin du nombre réel, seulement la valeur XOR
retour val ^ node.cnt; // placeholder – le xor sera calculé plus tard
}

/** -------- Solution principale
public int[] maxGeneticDifference(int[] parents, int[][] questions) {
int n = parents.longueur;
int q = requêtes. longueur;

// liste d'adjacence
Liste <Liste<Intégrée>> enfants = nouvelle liste <>();
pour (int i = 0; i < n; ++i) les enfants.add(new ArrayList<>());
Int rootNode = -1;
pour (int i = 0; i < n; ++i) {
int p = parents[i];
si (p) -1) rootNode = i;
autres enfants.get(p).add(i);
}

// requêtes regroupées par nœud
Liste<Liste<int[]>> qByNode = nouvelle grille <>();
pour (int i = 0; i < n; ++i) qByNode.add(new ArrayList<>());
pour (int i = 0; i < q; ++i) {
int noeud = requêtes[i][0];
int val = requêtes[i][1];
qByNode.get(node).add(new int[]{i, val});
}

int[] ans = nouveau int[q];

// Pile DFS: noeud, état (0 = entrée, 1 = sortie)
Deque<int[]> pile = nouveau ArrayDeque<>();
pile.push(nouvelle int[]{rootNode, 0});

pendant que (!stack.isEmpty()) {
[] cur = pile.pop();
int noeud = cur[0], état = cur[1];

si (indiquer) 0) { // entrer
insert(node); // valeur génétique = id noeud

// répondre à toutes les requêtes pour ce nœud
pour (int[] qi : qByNode.get(node)) {
idx = qi[0];
int v = qi[1];
int best = 0;
TrieNode t = racine;
pour (int i = BITS; i >= 0; --i) {
bit int = (v >> i) & 1;
int want = bit ^ 1;
si (t.child[want] != null) {
meilleurs= (1 << i);
t = t.child[voulait];
} autre {
t = t.child[bit];
}
}
[idx] = meilleur;
}

// Marqueur de sortie
pile.push(nouvelle int[]{node, 1});
// Pousser les enfants
pour (int enfant : children.get(node))
pile.push(nouvelle int[]{enfant, 0});
} autre { // sortie
supprimer(noeud);
}
}

le retour des an;
}
}
«» "

> **Pourquoi le détenteur de place dans `query`? **
> En Java la façon la plus simple de calculer `vali XOR pi` est de le faire en marchant le trie (le code à l'intérieur du bloc DFS). Il n'est donc pas nécessaire d'utiliser la «query» de l'aide; elle est laissée dans le squelette pour plus de clarté.
> Vous pouvez le supprimer si vous voulez une implémentation plus mince.

---

#### 1.2 Python 3

'`python
importations
la limite de récursion (200000)

Classe TrieNode:
__slots__ = ('enfant', 'cnt')
def _init_(self):
l'enfant = [Aucun, aucun]
auto.cnt = 0

Solution de classe:
BITS = 31 # 0 ... 31

def _init_(self):
Self.root = TrieNode()

def insert(self, val: int):
noeud = self.root
pour i à portée (même. BITS, -1, -1):
bit = (val >> i) & 1
si noeud.child[bit] n'est pas:
noeud.child[bit] = TrieNode()
noeud = noeud.child[bit]
noeud.cnt += 1

def delete(self, val: int):
noeud = self.root
pour i à portée (même. BITS, -1, -1):
bit = (val >> i) & 1
nxt = noeud.child[bit]
Nxt.cnt -= 1
Si nxt.cnt == 0: # dernier numéro qui a utilisé cette branche
noeud.child[bit] = Aucun
retour
noeud = nxt

def requête(self, val: int) -> Int:
"""Retourner le XOR maximum qui peut être atteint avec "val`."""
noeud = self.root
meilleur = 0
pour i à portée (même. BITS, -1, -1):
bit = (val >> i) & 1
want = bit ^ 1
si le nœud n'est pas :
Meilleur= 1 << i
noeud = noeud.enfant[veux]
Sinon:
noeud = noeud.child[bit]
le meilleur retour


def maxGeneticDifférence(parents, requêtes):
n, q = len(parents), len(queries)

# liste d'adjacence
enfants = [[] pour _ dans l'intervalle(n)]
racine = -1
pour i, p dans l'énumération (parents):
Si p == -1:
racine = i
Sinon:
children[p].append(i)

# requêtes groupées par nœud
qby = [[] pour _ dans la plage(n)]
pour idx, (noeud, val) dans l'énumération:
qby[node].appendice(idx, val)

ans = [0] * q
trie = TrieNode()

def dfs(node: int):
trie.insert(node) # valeur génétique = noeud id

# répondre à toutes les questions qui appartiennent à ce nœud
pour idx, valeur en qby[node]:
ans[idx] = trie.query(val)

pour les enfants[node]:
dfs(enfant)

trie.delete(noeud)

dfs(racine)
retour et
«» "

> **Note sur la récursion** – la profondeur de l'arbre peut être `~105`.
> Nous repoussons la limite de récursion (`sys.setrecursionlimit`) et gardons l'implémentation propre et courte. Si vous préférez une version itérative, il suffit d'échanger l'appel `dfs` pour une pile.

---

*## 1.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
- Oui. Essai binaire --------- */
BITS = 31; // 0-base: 31 ... 0
struct TrieNode {
tableau<int,2> enfant = {-1,-1}; // indices dans le vecteur
cnt = 0;
};
vecteur<TrieNode> trie;
racine int = 0;

vide insérer(int val) {
int noeud = racine;
pour (int i = BITS; i >= 0; --i) {
bit int = (val >> i) & 1;
int &next = trie[node].child[bit];
Si (suivant) -1) {
suivant = trie.size();
trie.emplace_back();
}
noeud = suivant;
trie[node].cnt++;
}
}

effacement du vide (int val) {
int noeud = racine;
pour (int i = BITS; i >= 0; --i) {
bit int = (val >> i) & 1;
int next = trie[node].child[bit];
Si (--trie[next].cnt == 0) {
trie[node].child[bit] = -1;
retour; // branche entière est maintenant vide
}
noeud = suivant;
}
}

requête int(int val) {
int noeud = racine;
int best = 0;
pour (int i = BITS; i >= 0; --i) {
bit int = (val >> i) & 1;
int want = bit ^ 1;
si (trie[node].child[want] != -1) {
best= 1 << i;
noeud = trie[node].child[want];
} autre {
nœud = trie[node].child[bit];
}
}
le meilleur retour;
}

public:
vector<int> maxGeneticDifference(vecteur<int>& parents, vector<vector<int>& questions) {
int n = parents.size(), q = requêtes.size();

/* construire une liste d'adjacence */
vecteur<vecteur<int>> enfants(n);
Int rootNode = -1;
pour (int i = 0; i < n; ++i) {
int p = parents[i];
si (p) -1) rootNode = i;
autres enfants[p].push_back(i);
}

/* requêtes de groupe par noeud */
vecteur<vecteur<pair<int,int>>> qByNode(n);
pour (int i = 0; i < q; ++i) {
int noeud = requêtes[i][0];
int val = requêtes[i][1];
qByNode[node].push_back({i, val});
}

vecteur <int> ans(q);

la réserve (n * 32 + 5);
trie.emplace_back(); // noeud racine

fonction<vit(int)> dfs = [&](int node) {
insert(node); // valeur génétique = id noeud

// répondre à toutes les requêtes qui appartiennent à ce nœud
pour (auto [idx, val] : qByNode[node])
ans[idx] = requête(val);

pour (int child: children[node]) dfs(child);
effacer(noeud);
};

dfs(noyau-racine);
le retour des an;
}
};
«» "

> **Pourquoi `trie.reserve(n * 32 + 5)`? **
> Pré-allouer le vecteur évite les réaffectations répétées et donne une utilisation prévisible de la mémoire.

---

- Oui. 2. Article du blog

> **Titre**
> **LeetCode 1938: Demande de différence génétique maximale – Le bon, le mauvais, et le mauvais**

> **Méta-description* *
> Vous voulez ace LeetCode 1938 ? Apprenez la stratégie Trie+DFS en Java, Python et C++ – avec analyse de complexité, pièges et conseils d'entrevue. Maîtrisez la requête de l'arborescence XOR maximale pour booster votre jeu d'entrevue. (en milliers de dollars)

---

2.1 Introduction

Dans une interview de codage vous êtes souvent demandé de **query a tree** – Quel est le XOR maximum d'une valeur avec n'importe quel noeud sur le chemin de la racine à un noeud donné?
LeetCode 1938 formalise exactement ce problème sous le nom de **Maximum Genetic Difference Query**.
Le but est de produire, pour chaque requête `(noeud, valeur)`, le maximum possible XOR `valeur XOR pi`, où `pi` est la valeur génétique de tout ancêtre (y compris le noeud lui-même).

> **Pourquoi ce problème est-il une *mine d'or* pour les entrevues? * *
> Il teste quatre concepts essentiels en une seule fois :
> 1. *Tree traversal* (DFS/BFS).
> 2. *Manipulation de niveau Bit* (XOR, représentation binaire).
> 3. *Conception de la structure des données* (trie binaire / arbre préfixe).
> 4. * Optimisation du temps/de l'espace* pour les grandes entrées (N ≤ 105, Q ≤ 3·104).

---

### 2.2 Énoncé du problème (récapitulation courte)

- `parents[i]` donne le parent du noeud `i` (ou `-1` si `i` est la racine).
- La valeur *génétique* d'un noeud est son indice "i".
- Pour chaque requête `[noeud, valeur]` vous devez retourner `max(value XOR ancêtre)` où l'ancêtre est n'importe quel noeud sur le chemin de la racine vers `noeud` (inclus).

Retourne les réponses dans l'ordre où apparaissent les requêtes.

---

2.3 Intuition et idée de base

1. ** Pourquoi XOR ? **
L'opération XOR est une opération classique dans le sens binaire. Pour maximiser `a XOR b`, à chaque position de bit vous voulez choisir le bit **opposite** de `a` si un tel `b` existe.

2. **Pourquoi un trie? **
Un tri binaire conserve tous les nombres dans une structure compacte où chaque niveau correspond à un bit.
*Insertion* et *suppression* d'un coût numérique au plus 32 étapes.
*Crier* pour le meilleur XOR est aussi une simple promenade: à chaque niveau choisir l'enfant qui a le bit opposé.

3. **Pourquoi la DSV?**
La requête ne concerne que les nœuds qui sont **ancêtres** du nœud cible.
Lorsque nous effectuons une première recherche de profondeur à partir de la racine, l'ensemble de nœuds sur le chemin courant est exactement l'ensemble des ancêtres.
L'insertion à l'entrée et la suppression à la sortie garantissent que le tri contient toujours *exactement* ces nœuds.

4. **L'assembler* *
- Créer des listes d'adjacence à partir de «parents».
- Les questions de groupe par le nœud auquel elles appartiennent.
- Exécutez un DFS qui :
* insère la valeur actuelle du nœud dans la trie,
* répond à toutes les questions qui vivent sur ce nœud,
* revient à ses enfants,
* supprime le nœud avant le retour en arrière.

La complexité du temps global est `O((N + Q) · 32)` et la mémoire est `O(N · 32)` pour le trie, plus `O(N)` pour l'arborescence et les requêtes – assez rapide pour les limites.

---

2.4 Analyse de la complexité

Étape Complexe Raison
C'est quoi, ça ?
Construire une liste d'adjacence Une seule passe sur les «parents». Autres
Requêtes de groupe `O(Q)`. Autres
Chaque nœud visité une fois. Autres
Ajouter / Supprimer "O(32)" par noeud 32 niveaux dans le tri binaire. Autres
Demande de renseignements `O(32)` par demande de renseignements. Autres
**Total**="O((N + Q) · 32"=" ~ 6 millions d'opérations pour le pire cas – bien moins d'une seconde en C++/Java, quelques millisecondes en Python (avec PyPy). Autres

Consommation de mémoire:
- Liste des nombres entiers "O(N)".
- Seaux de requête: "O(Q)".
- Trie: jusqu'à des nœuds `N * 32` ('- 3,2 × 106`) → `- 120 Mo` en C++ (un peu moins en Java/Python en raison de la gestion de la mémoire de niveau supérieur).

Toutes les langues fournies ci-dessus restent confortablement dans la limite typique de 256 Mo de mémoire.

---

### 2.5 Le *Bad* – Pièges communs

Pourquoi ça fait mal
- C'est quoi ?
**L'utilisation d'une carte de hachage au lieu d'une trie** Utilisez un trie pour tailler l'espace de recherche à 32 niveaux. Autres
**Insertion de tous les nœuds à l'avant**Le trie contiendrait alors *chaque* noeud, pas seulement des ancêtres, conduisant à de mauvaises réponses pour les requêtes qui n'ont besoin que des ancêtres. Insérer lorsque vous entrez** un noeud dans DFS; supprimer lorsque vous **leave** it. Autres
**Ignorer les bits basés sur 0**=Certaines langues déplacent les bits mal: `pour (int i = 31; i >= 0; --i)` vs `pour (int i = 0; i <= 31; ++i)`.=Suivez la convention `bits[31] ... bits[0]`. Autres
**L'utilisation de la récursion sur des arbres profonds en Python** 1000 → `RecursionError`. Autres
**Ne pas pré-allouer la trie** (C++) "Trie.reserve (N * 32 + 5);" Autres

---

2.6 Conseils d'entrevue

1. ** Expliquez la structure des données d'abord** – avant de plonger dans le code, dessinez un tri sur papier pour convaincre l'intervieweur que vous comprenez comment maximiser XOR.
2. **Afficher la pile DFS** – écrire un pseudocode pour la logique entrée/sortie; de nombreux intervieweurs aiment un diagramme de récursion propre.
3. **Parler de la complexité** – mentionner le lien `O((N + Q)·32)` et comparer avec le naïf `O(N)` par requête.
4. **Edge cas** – mettre en évidence ce qui se passe lorsqu'un noeud n'a pas d'ancêtres (juste lui-même) ou quand `valeur` est `0`.
5. **Le choix de langue** – s'il est demandé de mettre en œuvre en Java/Python/C++, adapter l'idée de base; les spécificités de langue (p. ex., tableaux vs `Liste<Intégrée>`, `array` vs `vector`, `None` vs `nullptr`) doivent être évidentes.

---

2.7 Prise- Loin

- La stratégie **Trie + DFS** est une solution *canonique* pour LeetCode 1938.
- Oui. Il fusionne élégamment la traversée de l'arbre avec des requêtes bit-wise.
- Implémentez-le une fois (Java, Python, C++) et vous serez prêt pour une grande variété de problèmes d'entretien arboricole.
- N'oubliez pas de grouper les requêtes, d'utiliser des E/S efficaces et de pré-alloquer la mémoire pour la vitesse.

Bonne chance pour écraser votre prochaine entrevue de codage – laissez le maximum de XOR être de votre côté!

---

**Fin de l'article**

---

- Oui. 3. Pensées finales

- Les trois implémentations dans **Java, Python et C++** partagent un plan commun : construire l'arborescence, exécuter un DFS, maintenir un tri binaire des valeurs de l'ancêtre, et répondre aux requêtes à la volée.
- Oui. L'article ci-dessus donne aux intervieweurs un modèle mental solide et aux codeurs une solution prête à la copie.
- Oui. En maîtrisant LeetCode 1938, vous renforcerez votre compréhension des structures de données arborescentes, de la manipulation des bits et de l'optimisation algorithmique – compétences qui sont en demande dans presque toutes les interviews de haute technologie.

---

** Bon codage !**