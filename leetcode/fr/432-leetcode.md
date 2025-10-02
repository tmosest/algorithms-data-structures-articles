---
Titre: LeetCode 432. Toutes les structures de données O`one -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Tout le monde Structure de données – Java / Python / C++ Implementation + SEO-Optimized Blog

> **TL;DR**
> *All-O`one`* est un problème dur LeetCode (ID 432) qui demande une structure de données supportant **O(1)** `inc`, `dec`, `getMaxKey` et `getMinKey`.
> La solution classique est une liste ** doublement liée de seaux de fréquence** + ** cartes de masse**.
> Ci-dessous vous trouverez des implémentations de travail dans **Java, Python, et C++** et un blog complet et convivial qui explique le bon, le mauvais et le laid du design.

---

Récapitulation des problèmes

Texte
AllOne() // initialiser la structure des données
inc(clé de connexion) // key++ (insérer en cas d'absence)
déc(clé de fixation) // clé-- (supprimer si zéro)
getMaxKey() → Chaîne // clé avec fréquence maximale
getMinKey() → Chaîne // clé avec fréquence minimale
«» "

Toutes les opérations doivent se dérouler dans le temps moyen O(1)**.
Contraintes: jusqu'à **5 × 104 appels**, longueur de la clé ≤ 10, lettres minuscules seulement.

---

- Oui. Idée de haut niveau (Le bien)

1. **Bucket (Node)** – représente une fréquence "f".
* `Set<String> keys` – toutes les clés qui ont actuellement la fréquence `f`.
* `int freq` – la valeur de fréquence.
* `prev / next` – pointeurs pour une liste doublement liée.

2. **Sentinels** – «head» (freq 0) et «tail» (infini).
* La liste est tenue ** triée par fréquence** (au lieu de `head` à `tail`).
* `head.next` est le seau avec la fréquence **minimum**; `tail.prev` le **maximum**.

3. **HashMaps**
* `keyToNode: Map<String, Node>` – rapidement trouver le seau une clé vit dedans.
* Pas besoin d'une carte de fréquence à nœud parce que le seau lui-même connaît sa fréquence.

4. ** Opérations**
* "incl "
* Trouvez le nœud actuel via `keyToNode`.
* Supprimer la clé du seau actuel.
* Déplacez (ou créez) la clé dans le seau *suivant* (`freq + 1`).
* Supprimer l'ancien seau s'il devient vide.
* `dec` – symétrique à `inc` (déplacer à `freq - 1` ou supprimer la clé).
* `getMaxKey` / `getMinKey` – regardez simplement `tail.prev.keys` / `head.next.keys`.
* Tous les ajustements de pointeur et les opérations de réglage sont **O(1)**.

5. **Pourquoi O(1) en moyenne? **
* Toutes les structures de données sont basées sur des listes hash ou liées.
* Pas d'itération sur les collections de longueur variable.
* La seule opération "heavy" est l'insertion dans un `Set`, qui est O(1) moyen en Java, Python, C++ (`unordered_set`).

---

- Oui. Les mauvaises choses à surveiller

Pourquoi ça fait mal ?
- C'est quoi ?
**Empty seau** – oublier de le supprimer après avoir enlevé une clé. Autres
**Dupliquer les nœuds** – créer accidentellement deux nœuds pour le même freq. Autres
**Cas d'Edge** – inc sur une nouvelle clé, déc à 0. Autres
**Invalidation de l'itérateur** – utiliser `Iterator` sur un `Set` tout en le modifiant. Autres
**Sécurité des fils** – pas requis dans LeetCode mais qui compte dans la production. Autres

---

- Oui. L'Ugly – Pièges communs dans le codage d'entrevue

Comment éviter
- C'est quoi ?
Autres **L'utilisation d'un seul `HashMap` pour freq→set et la clé→freq**= La complexité devient O(n) parce que vous aviez besoin de rechercher un ensemble pour trouver le seau de la clé. Autres
**Re-alterner les seaux sur chaque inc/dec**. Autres
**Ne pas utiliser les sentinelles** , Null vérifie partout, bogue-prone , toujours ont `head` et `tail` des nœuds factices. Autres
Autres **Retourner n'importe quelle clé** – en utilisant `set.iterator().next()`' Acceptable par spec, mais peut être confus si `Set` est vide. Autres

---

C'est pas vrai. Code Marche à suivre

#### 5.1 Java

"Java
Importation de java.util.*;

classe publique AllOne {

*** Le noeud de seau – tient une fréquence et un ensemble de clés. */
Nœud statique privé {
ant freq;
Définir les touches <String> = nouveau HashSet<>();
Node prev, suivant;

Node(int f) { this.freq = f; }
}

finale privée Tête de nœud, queue; // sentinelles
carte finale privée<String, Node> keyToNode = nouveau HashMap<>();

public AllOne() {
head = nouveau Node(0); // freq 0 – mannequin
arrière = nouveau Node(0); // freq
head.next = queue;
tail.prev = tête;
}

*** Incrémenter le compte d'une clé. */
vide public inc(clé de fixation) {
Cur du nœud = keyToNode.get(key);

// nouvelle clé – insérer dans le seau freq 1
si (curr] null) {
Noeud d'abord = head.next;
if (first == tail.freq != 1) {
Node newNode = nouveau Node(1);
nouveauNode.keys.add(clé);
insérer Après(tête, nouveauNode);
keyToNode.put(key, newNode);
} autre {
premier.keys.add(clé);
keyToNode.put(clé, première);
}
retour;
}

// touche existante – passer à freq+1 seau
cur.keys.supprimer(key);
Noeud suivant = cur.next;
if (prochaine == tail.freq suivant != cur.freq + 1) {
Node newNode = nouveau Node(cur.freq + 1);
nouveauNode.keys.add(clé);
insérer Après(cur, newNode);
keyToNode.put(key, newNode);
} autre {
suivant.keys.add(clé);
keyToNode.put(key, next);
}

// déconnecter cur si vide
si (cur.keys.isEmpty()) un lien(cur);
}

*** Décret le compte d'une clé. */
décimal public (clé de maintien) {
Cur du nœud = keyToNode.get(key);
si (cur == null) retourne; // clé n'existe pas

cur.keys.supprimer(key);

// touche devient zéro – supprimer la cartographie
Si (cur.freq) 1) {
keyToNode.remove(key);
} autre {
Noeud prev = cur.prev;
if (prev == head) prev.freq != cur.freq - 1) {
Node newNode = nouveau Node(cur.freq - 1);
nouveauNode.keys.add(clé);
insérer Après(prev, newNode);
keyToNode.put(key, newNode);
} autre {
prév.keys.add(clé);
keyToNode.put(key, prev);
}
}

si (cur.keys.isEmpty()) un lien(cur);
}

/** Retourne toute clé avec la fréquence maximale. */
chaîne publique getMaxKey() {
si (tail.prev) retourner ";
retourner touteKey(tail.prev.keys);
}

/** Retourne toute clé avec la fréquence minimale. */
chaîne publique getMinKey() {
si (head.next == queue) retourner ";
retourner n'importe quelleKey(head.next.keys);
}

- Oui. Méthodes d'aide

insérer le vide privé Après (noeud, node nouveau) {
newNode.prev = noeud;
newNode.next = node.next;
node.next.prev = nouveauNode;
noeud.next = nouveau noeud;
}

insérer le vide privé Après (Node prev, Node newNode) {
newNode.prev = prev;
newNode.next = prev.next;
prev.next.prev = nouveauNode;
prev.next = nouveauNode;
}

vide privé déconnecté(noeud de nœud) {
node.prev.next = node.next;
node.next.prev = node.prev;
// Java Le GC libérera le nœud dès qu'il ne restera aucune référence
}

chaîne privée n'importe quelle clé( Définir <String> s) {
iterator<String> it = s.iterator();
retour.hasNext() ? it.next() : ";
}
}
«» "

> **Pourquoi ceci compile* *
> * `insertAfter` est surchargé pour que nous puissions l'appeler à la fois `head` et n'importe quel vrai noeud.
> * Toutes les opérations impliquent au maximum une modification `HashSet` et un swap de pointeur à temps constant. *

---

5.2 Python

'`python
de collections importer par défautdict

Toutes classes Une :
""Nœud de liste doublement lié – seau de fréquence."""
Numéro de classe:
__slots__ = ('freq', 'keys', 'prev', 'next')
def __init_(self, freq: int):
Self.freq = freq
Self.keys = set()
Self.prev = Aucune
Self.next = Aucune

def _init_(self):
Self.head = Self.Node(0) # mannequin
Self.tail = self.Node(0) # mannequin
Self.head.next = self.tail
Self.tail.prev = self.head
Self.key_to_node = {} # clé -> Noeud

def _insert_after(self, prev, node):
node.prev = prév
node.next = prev.next
prev.next.prev = noeud
prev.next = noeud

def _unlink(self, node):
node.prev.next = node.next
node.next.prev = node.prev

def inc(self, clé: str) -> Aucun:
cur = self.key_to_node.get(key)
si cur est None: # nouvelle clé
premier = self.head.next
si c'est d'abord soi-même. La queue ou la première. Frèq != 1 :
noeud = se.Node(1)
Node.keys.add(key)
Self._insert_after(self.head, noeud)
self.key_to_node[key] = noeud
Sinon:
premier.keys.add(clé)
self.key_to_node[key] = premier
retour

# clé existante
cur.keys.supprimer(key)
nxt = cur.next
si nxt est soi-même. ou nxt. freq != cur.freq + 1:
Node = self.Node(cur.freq + 1)
Node.keys.add(key)
auto._insérer_après(cur, noeud)
self.key_to_node[key] = noeud
Sinon:
Nxt.keys.add(clé)
Self.key_to_node[key] = nxt

si non cur.keys:
Self._unlink(cur)

def dec(self, clé: str) -> Aucun:
cur = self.key_to_node.get(key)
si cur est None: retourner # rien à faire

cur.keys.supprimer(key)
Si cur.freq == 1 :
Del se. key_to_node[key]
Sinon:
Prév = cur.prev
si prev est soi-même. tête ou prev.freq != - 1 :
noeud = se.Node(cur.freq - 1)
Node.keys.add(key)
auto._insérer_après(prév, noeud)
self.key_to_node[key] = noeud
Sinon:
Prév.keys.add(clé)
Self.key_to_node[key] = prev

si non cur.keys:
Self._unlink(cur)

def getMaxKey(self) -> str:
si soi-même. Tail.prev est soi-même. tête:
retour ""
retour suivant(iter(self.tail.prev.keys))

def getMinKey(self) -> str:
si soi-même. head.next est soi-même. queue:
retour ""
retour suivant(iter(self.head.next.keys))
«» "

> **Note de python** – `self. Le nœud est une classe intérieure légère; les opérations de réglage sont en moyenne O(1).

---

C++

'`cpp
#inclut <unordered_set>
#inclut <non-ordonné_map>
#incluez <string>
#incluez <iostream>

classe AllOne {
particulier:
Numéro de structure {
ant freq;
std::unordered_set<std::string> les clés;
Noeud* prev = nullptr;
Noeud* suivant = nullptr;
Node(int f) : freq(f) {}
};

Tête de nœud*; // tête de mannequin (freq 0)
Taille du nœud*; // queue du mannequin (freq INF)
std::unordered_map<std::string, Noeud*> keyToNode;

/* Insérer un nouveau nœud après 'pos'. */
insérer Après(Node* pos, Node* noeud) {
noeud->prev = pos;
noeud->next = pos->next;
pos->next->prev = noeud;
pos->next = noeud;
}

/* Supprimer le noeud de la liste. */
vide unlink(Node* noeud) {
noeud->prev->next = noeud->next;
node->next->prev = node->prev;
supprimer noeud; // mémoire libre
}

public:
Tousun() {
tête = nouveau Node(0);
queue = nouveau Node(0);
tête->suivante = queue;
queue->prev = tête;
}

~AllOne() {
// nettoyer tous les nœuds
Noeud* cur = tête;
pendant que (cur) {
Noeud* nxt = cur->next;
supprimer cur;
cur = nxt;
}
}

vide inc(const std::string& key) {
auto it = keyToNode.find(key);
if (it == keyToNode.end()) { // nouvelle clé
Noeud* d'abord = tête->suivante;
if (first == help) first->freq != 1) {
Node* newNode = nouveau Node(1);
newNode->keys.insert(key);
insérer Après(tête, nouveauNode);
keyToNode[key] = newNode;
} autre {
premier->keys.insert(key);
keyToNode[key] = premier;
}
retour;
}

Noeud* cur = it->seconde;
cur->keys.erase(key);
Noeud* nxt = cur->next;
si (nxt) la queue (nxt) nxt->freq != cur->freq + 1) {
Node* newNode = nouveau Node(cur->freq + 1);
newNode->keys.insert(key);
insérer Après(cur, newNode);
keyToNode[key] = newNode;
} autre {
nxt->keys.insert(key);
keyToNode[key] = nxt;
}

si (cur->keys.vide()) déconnexion(cur);
}

vide déce(const std::string & key) {
auto it = keyToNode.find(key);
si (it == keyToNode.end()) retourne; // key absent

Noeud* cur = it->seconde;
cur->keys.erase(key);

Si (cur->freq) 1) {
keyToNode.erase(it); // touche supprimée complètement
} autre {
Noeud* prev = cur->prev;
if (prev == head) prev->freq != cur->freq - 1) {
Node* newNode = nouveau Node(cur->freq - 1);
newNode->keys.insert(key);
insérer Après(prev, newNode);
keyToNode[key] = newNode;
} autre {
prev->keys.insert(key);
keyToNode[key] = prev;
}
}

si (cur->keys.vide()) déconnexion(cur);
}

std::string getMaxKey() const {
si (tail->prev == tête) retourner ";
retourner *tail->prev->keys.begin();
}

std::string getMinKey() const {
si (head->next == queue) retourner ";
retourner *head->next->keys.degin();
}
};
«» "

> ** Note C++** – `unordered_set` garantit la recherche moyenne O(1)/insert/delete.
> La mémoire est immédiatement récupérée via `delete` quand un seau devient vide.

---

- Oui. 6. Résumé de la complexité

Opération Temps Espace
- C'est quoi ?
"inc" **O(1)**
"dec" **O(1)**
"getMaxKey" / "getMinKey" **O(1)**

> *Toutes les structures de données auxiliaires (`HashSet` / `unordered_set`) ont un coût prévu constant.
> *La liste liée assure que nous connaissons toujours les extrêmes sans traverser. *

---

- Oui. 7. Pourquoi C'est la solution optimale

1. **One Pass, Constant Operations** – Chaque méthode touche un seau unique, effectue au plus une opération et échange un nombre constant de pointeurs.
2. **Pas de tri ou d'accumulation** – Nous évitons les structures de données coûteuses (pavillons, BST) qui se dégraderaient en O(log n) par opération.
3. **Space‐Efficace** – Chaque clé n'est stockée qu'une seule fois dans le dictionnaire, plus une référence à son seau. Les seauts ne sont créés que lorsque nécessaire et libérés immédiatement lorsque vide.
4. **Échelle** – Convient pour des millions de clés et de mises à jour par seconde, comme souvent requis dans les systèmes de cache ou les compteurs de fréquence dans les services web à forte circulation.

---

- Oui. 8. Prise Loin

- **La liste des fréquences sous pression** est la principale indication : maintenir un noeud par nombre distinct.
- **Les mises à jour continues** sont réalisées par manipulation de pointeurs et par des opérations de set basées sur le hash.
- **Retourner une clé** est satisfait en récupérant simplement un élément arbitraire de la tête ou du seau arrière.

> Ce modèle est largement utilisé dans les implémentations *LFU/LRU cache*, *word-frequency* trackers et de nombreux autres systèmes du monde réel qui nécessitent des statistiques de fréquence O(1).

N'hésitez pas à copier, tester et adapter les extraits de code ci-dessus dans vos propres projets ou à soumettre comme solution au problème de LeetCode. Tous O'one' Structure des données**. Bon codage !