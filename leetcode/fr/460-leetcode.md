---
titre: LeetCode 460. LFU Cache -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LFU Cache – Mise en œuvre O(1) en trois langues

Le classique LeetCode problème difficile 460: *Least Fréquemment utilisé (LFU) Cache*.
L'objectif est de soutenir `get` et `put` dans ** moyenne O(1)** temps et d'expulser le
clé avec la fréquence d'accès la plus basse (et, en cas de liens, la moins récente
utilisé un).

Vous trouverez ci-dessous une mise en œuvre complète et prête à la production pour :

Langue Fichier Idée clé Autres
- C'est quoi ?
Java (en anglais seulement) Autres
Python "lfu_cache.py" Deux dictionnaires + "OrdonnanceDict"
C++=1 `lfu_cache.cpp`=2 `unordered_map` + `list` + `unordered_map` des itérateurs

Les trois solutions fonctionnent en **O(1)** en moyenne et gèrent des capacités allant jusqu'à `10^4`
et `2·10^5' appelle – exactement ce que la déclaration de problème exige.

> **Pourquoi deux hash-maps? * *
> *One* garde `key → (valeur, fréquence)`.
> *Deux* conserve `fréquence → list/LinkedHashSet de clés` (préservation de la commande LRU pour chaque fréquence).
> La variable `minFreq` nous indique quelle fréquence contient le candidat à l'expulsion.

---

### Java (`LFUCache.java`)

"Java
Importation de java.util.*;

***
* Concevoir et mettre en oeuvre une structure de données pour un cache le moins fréquemment utilisé.
*
* Toutes les opérations se déroulent en moyenne O(1).
*/
classe publique LFUCache {

// touche -> (fréquence, valeur)
carte finale privée<entier, noeud> cache;

// fréquence -> clés qui ont cette fréquence (conserve la commande LRU)
finale privée Carte<entier, ensemble de HashLinkedin<entier>> freqMap;

capacité interne finale privée;
interne privé minFreq; // fréquence minimale de courant

- Oui. noeud interne --------- */
Nœud statique privé {
clé int, valeur, freq;
Node(int k, int v, int f) { clé = k; valeur = v; freq = f; }
}

public LFUCache(capacité d'insertion) {
Ça. capacité = capacité;
ce.cache = nouveau HashMap<>();
ce.freqMap = nouveau HashMap<>();
ce.minFreq = 0;
}

*** Renvoie la valeur de la clé si présente, sinon -1. */
int public get(int key) {
Noeud = cache.get(key);
si (noeud == null) retourner -1;
// augmentation de la fréquence
mise à jourFreq(node);
noeud de retour. valeur;
}

/** Insère/mise à jour la paire clé/valeur. */
public vide mis(int clé, valeur int) {
si (capacité <= 0) retour;

Noeud = cache.get(key);
si (node != null) { // mettre à jour la clé existante
valeur du noeud = valeur;
mise à jourFreq(node);
retour;
}

si (cache.size() == capacité) { // expulsion requise
l'expulsion();
}

// insérer une nouvelle clé
Node newNode = nouveau Node(key, valeur, 1);
cache.put(key, newNode);
freqMap.computeIfAbsent(1, ignoré -> nouveau LinkedHashSet<>()).add(key);
minFreq = 1; // un nouveau noeud a freq 1
}

*/

*** Déplacez le nœud vers le prochain seau de fréquence. */
mise à jour du vide privé Freq (noeud) {
int oldFreq = node.freq;
LinkedinHashSet<integer> set = freqMap.get(oldFreq);
set.remove(node.key);
si (set.isEmpty()) {
freqMap.remove(oldFreq);
si (minFreq == oldFreq) minFreq++; // si nous avons enlevé le seau min
}

noeud. freq++;
freqMap.computeIfAbsent(node.freq, ignoré -> nouveau LinkedHashSet<>()).add(node.key);
}

*** Évite la clé la moins fréquemment (et la moins récemment). */
vide privé expulsion() {
LinkedinHashSet<Integer> set = freqMap.get(minFreq);
// Lié HashSet préserve l'ordre d'insertion → premier élément est LRU
int keyToRemove = set.iterator().next();
set.supprimer(keyToSupprimer);
si (set.isEmpty()) freqMap.remove(minFreq);

cache.supprimer(keyToSupprimer);
}
}
«» "

---

### Python (`lfu_cache.py`)

'`python
de collections import defaultdict, OrderedDict

classe LFUCache:
"""
Concevoir et mettre en œuvre une structure de données pour un cache le moins utilisé.
Toutes les opérations se déroulent en moyenne O(1).
"""

def __init__(auto, capacité: int):
autocapacité = capacité
taille de soi = 0
auto.min_freq = 0
Self.key_to_val_freq = {} # key -> (valeur, freq)
self.freq_to_keys = defaultdict(OrderedDict) # freq -> Ordonnance Dict{key: Aucun}

def get(self, clé: int) -> Int:
si la clé n'est pas dans self.key_to_val_freq :
retour -1
val, freq = self.key_to_val_freq[key]
auto._augmentation_freq(clé, val, freq)
retour val

def put(self, clé: int, valeur: int) -> Aucun:
si soi-même. capacité <= 0:
retour

if key in self.key_to_val_freq :
# Mettre à jour la valeur, conserver la fréquence
_, freq = self.key_to_val_freq[key]
Self.key_to_val_freq[key] = (valeur, freq)
auto_augmentation_freq(clé, valeur, freq)
retour

si soi-même. taille == autocapacité:
Self._evit()

# Insérer une nouvelle clé
Self.key_to_val_freq[key] = (valeur, 1)
Self.freq_to_keys[1][key] = Aucun
auto.min_freq = 1
taille de soi += 1

C'est... aide interne - Oui.
def _augmentation_freq(self, clé: int, valeur: int, freq: int) -> Aucun:
"""Déplacer la clé de freq à freq+1."""
# enlever du vieux seau freq
Del se. freq_to_keys[freq][key]
si ce n'est pas soi. freq_to_keys[freq] :
Del se. freq_to_keys[freq]
si soi-même. min_freq == freq:
Self.min_freq += 1

# ajouter au nouveau seau freq
Self.freq_to_keys[freq + 1][key] = Aucun
# Mettre à jour la cartographie
Self.key_to_val_freq[key] = (valeur, freq + 1)

def _evit(self) -> Aucun:
""Vivre la clé LRU dans le seau avec la plus basse fréquence."""
# CommandedDict préserve l'ordre d'insertion -> la première clé est LRU
evit_key, _ = self.freq_to_keys[self.min_freq].popitem(last=False)
si pas self.freq_to_keys[self.min_freq]:
del self.freq_to_keys[self.min_freq]
Del self.key_to_val_freq[evit_key]
taille de soi -= 1
«» "

> **Pourquoi `OrdonnéDict`?**
> Dans Python 3.7+, le `dict` conserve l'ordre d'insertion, mais `OrdonnéDict`
> nous donne encore une interface explicite `popitem(last=False)` qui fonctionne dans l'ancienne
> Les versions de CPython et garantit O(1) pour supprimer.

---

### C++ (`lfu_cache.cpp`)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

***
* Concevoir et mettre en oeuvre une structure de données pour un cache le moins fréquemment utilisé.
* Toutes les opérations se déroulent en moyenne O(1).
*/
classe LFUCache {
public:
Numéro de structure {
clé int, val, freq;
Node(int k, int v, int f) : key(k), val(v), freq(f) {}
};

LFUCache(capacité d'int) : capacité(capacité), taille(0), minFreq(0) {}

int get (clé d'int) {
auto it = keyMap.find(key);
si (it == keyMap.end() retourne -1;
Noeud &node = *(it->seconde);
mise à jour(noeud);
retour node.val;
}

vide put(int key, valeur int) {
si (capacité <= 0) retour;

auto it = keyMap.find(key);
si (it != keyMap.end()) { // key existe
it->seconde->val = valeur;
mise à jour(*(it->seconde));
retour;
}

si (taille == capacité) exvit();

// insérer une nouvelle clé
Noeud *noeud = nouveau Noeud (clé, valeur, 1);
keyMap[key] = noeud;
freqMap[1].push_back(key);
freqPos[key] = --freqMap[1].end(); // itérateur à sa position
minFreq = 1;
++ Taille;
}

particulier:
capacité, taille, minFreq;
unordered_map<int, Node*> keyMap; // key -> noeud*
unordered_map<int, list<int>> freqMap; // freq -> liste des clés (LRU)
unordered_map<int, list<int>:iterator> freqPos; // key -> itérateur dans sa liste

vide update(Node &node) {
Int oldF = node.freq;
// supprimer la clé de l'ancien seau
freqMap[oldF].erase(freqPos[node.key]);
si (freqMap[oldF].vide()) {
freqMap.erase(oldF);
si (minFreq) ++minFreq;
}

// ajouter la clé au nouveau seau
noeud. freq++;
freqMap[node.freq].push_back(node.key);
freqPos[node.key] = --freqMap[node.freq].end();
}

vide expulsion() {
clé int = freqMap[minFreq].front();
freqMap[minFreq].pop_front();
si (freqMap[minFreq].vide()) freqMap.erase(minFreq);
supprimer keyMap[key];
keyMap.erase(key);
--taille;
}
};
«» "

> **Pourquoi `list` + carte de l'itérateur? * *
> `list` nous donne une suppression à temps constant avec un itérateur.
> La carte `freqPos` se souvient de chaque clé dans son seau de fréquence,
> nous permettant de le supprimer en O(1).

---

- Oui. 2. Le bon, le mauvais et le mauvais – un article de blog de SEO-Ready

> ** Auditoire cible** : ingénieurs en logiciels se préparant à des entrevues de conception de systèmes, gestionnaires embaucheurs à la recherche de compétences en structure de données, et toute personne curieuse de savoir comment l'UGL fonctionne sous le capot.

---

Pourquoi l'UGL compte

* **Caching du monde réel** – Bases de données, serveurs de bord CDN et remplacement des pages OS
les politiques utilisent toutes l'UGL (ou les variantes).
Démontrer la maîtrise de l'UGL montre que vous comprenez * l'expulsion basée sur la fréquence*,
pas seulement *temps* (LRU) ou *taille* (FIFO).

* **Interview buzz-word** – LeetCode problem 460 est un agrafe de niveau supérieur
Entretiens. Le résoudre correctement et efficacement est un drapeau vert pour l'embauche
les gestionnaires.

* **O(1) complexité** – prouver que vous pouvez concevoir des structures de données qui répondent
des garanties strictes en matière d'espace temporel présentent une connaissance approfondie des tables de hachage, liées
liste et analyse amortie.

---

### Les mauvaises: Pièges communs

Symptômes Correction
C'est pas vrai.
**Ne pas garder l'ordre de LRU par fréquence**= Évite la clé la plus récemment utilisée → mauvaise réponse== Utiliser `LinkedHashSet` (Java), `OrderedDict` (Python), ou `list` avec itérateurs (C++) pour préserver l'ordre dans chaque seau. Autres
**Mettre à jour la fréquence sur mis mais pas sur get**=Mettre à jour le mauvais candidat à l'expulsion=Mettre toujours à niveau la fréquence pour `get` et pour une mise à jour seulement `put'. Autres
**Missing `minFreq` update after seau delete**= `evit()` tire d'un seau vide → `KeyError` / `IndexError`=Après avoir enlevé la dernière clé d'un seau de fréquence, augmenter `minFreq` **seulement si** ce seau était le minimum. Autres
Autres **Les fuites de mémoire dans le C++**. Autres

---

- Oui. L'horrible : des cas de bord qui rompent votre code

1. ** Capacité zéro** – Votre cache ne devrait pas faire avec grâce.
2. **Dupliquer `put`** – Mettre à jour une clé existante ne doit pas réinitialiser sa fréquence.
3. ** Grandes fréquences** – Les fréquences peuvent croître sans limite; la carte du seau doit
affecter dynamiquement de nouveaux seaux et laisser tomber les anciens.
4. **Éliminations simultanées** – Lorsque la capacité est atteinte, vous devez toujours
Expulsez * exactement une* clé. Une implémentation buggy pourrait essayer d'expulser deux
les clés d'un appel.

---

- Oui. 3. Mettre tout ensemble – Ce que les recruteurs recherchent

* **Capacité de conception du système** – Vous pouvez expliquer *pourquoi* le modèle à deux cartes
résout le problème dans O(1).
* **Code propre** – Pas d'état mondial mutable, toutes les méthodes sont "publiques"/"privées"
le cas échéant, et la mémoire est nettoyée (l'exemple C++ supprime les nœuds).
* **Testabilité** – Chaque mise en œuvre peut être testée avec
`TestCase` de LeetCode, et vous pouvez ajouter votre propre `si __name__ == "_main__"` harnais de test.
* **Documentation** – Des commentaires clairs et une brève section « Pourquoi » aident à embaucher
les gestionnaires et votre futur moi.

> ** Conseil professionnel :** Quand vous êtes dans une interview, marchez l'intervieweur
> diagramme de la structure des données, nommez chaque composant (`cache`, `freqMap`,
> `minFreq`), et expliquer les invariants *O(1)*.

---

- Oui. 4. Comment utiliser le billet de blog dans votre CV / Linked Dans

1. **Blog Title** – *=LFU Cache – Le bon, le mauvais et le mauvais*
Termes de recherche: cache LFU, LeetCode 460.
2. **Ajouter un lien** – Lire l'article complet avec le code : https://your‐blog.com/lfu‐cache‐blog.
3. **Voir cas** – Dans la section *Projets*, mentionner:
*Mise en œuvre d'un cache LFU prêt à la production en Java, Python et C++ avec des opérations O(1); résolu LeetCode 460*.
4. **Mots-clés** – Description de la complexité temporelle, description de la carte, description de la structure, description de la structure.
5. **Cover Letter** – Soulignez que vous avez abordé un problème *hard* LeetCode et que la solution est réutilisable dans les scénarios de cache du monde réel (CDN, in-memory DB, etc.).

---

### TL;DR

Comment le montrer dans une interview
-- -- -- -- -- -- -- -- --
Java'''O(1)''' Parlez des deux hash-maps, `minFreq`, et expulsion via `LinkedHashSet`. Autres
Python "O(1)" Mention `defaultdict(OrderedDict)` et comment il maintient l'ordre LRU. Autres
Utiliser `unordered_map` + `list` + carte itérateur pour les suppressions O(1). Autres

Implémentez-le, ajoutez le code à votre repo GitHub, et référez-le dans votre
LeetCode -Discuss ou -Interview Notes.
Lorsque les recruteurs remarquent que vous avez maîtrisé un cache O(1) LFU en plusieurs langues, ils penseront : Cet ingénieur connaît les tables de hachage, les listes liées et peut optimiser la production 