---
Titre: LeetCode 3508. Mettre en œuvre le routeur -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3508 – Mettre en œuvre le routeur
**Solution en Java
**Blog post** – Le Bon, Le Mauvais, Le Méchant – un guide complet et convivial

---

- Oui. 1. Récapitulation des problèmes

Vous construisez un petit routeur in-memory qui doit garder au plus **`memoryLimit`** paquets.
Les paquets ont *source*, *destination* et *timestamp*.

Description de l'opération Valeur de retour
- C'est quoi ?
Ajouter un paquet si c'est **pas** un duplicata. Si le routeur est plein, le paquet **le plus ancien** est expulsé en premier. "vrai" / "faux"
"forwardPacket()" Enlever et retourner le paquet **plus ancien** (FIFO).
Combien de paquets sont encore dans le routeur qui a destination `d` et timestamps dans `[start,end]`? Ensemble

**Contrôles* *

* "2 ≤ mémoireLimité ≤ 105 "
* `1 ≤ source, destination ≤ 2·105 "
* `1 ≤ horodatage ≤ 109 "
* Les appels `addPacket` sont **chronologiquement commandés** (timestamp ne diminue jamais)

---

- Oui. 2. Conception de la structure des données

Nécessaire Ce que nous utilisons
- C'est quoi ?
**FIFO file d'attente**= `LinkedList` / `deque` / `queue<array>==Enregistrez les paquets dans l'ordre d'arrivée afin que nous puissions pop le plus ancien en O(1). Autres
**Détection du duplicata**= `HashSet` d'une clé 64 bits== O(1) insérer / rechercher des duplicatas. Autres
**Pour chaque destination une liste triée des horodatages. Autres
**Requête d'une plage de fréquences suffisante**= Recherche binaire (`lower_bound` / `upper_bound`) sur la liste de destination== O(log N) par requête. Autres
Autres **Gardez la trace des horodatages enlevés** , pointeur de Per-destination "suppriméIdx" Après qu'un paquet soit envoyé ou expulsé, nous ne voulons plus compter son horodatage. Le pointeur nous indique à partir de quel index les timestamps *active* commencent. Autres

Avec ces choix, chaque opération fonctionne en **O(1)** ou **O(log N)** et l'utilisation de la mémoire reste dans la limite.

---

- Oui. 3. Exécution

Voici des solutions propres et prêtes à la production dans **Java, Python et C++**.
Tous les trois partagent la même logique – seulement la syntaxe change.

---

#### 3.1 Java

"Java
Importation de java.util.*;

***
* 3508. Mettre en œuvre le routeur
*/
Routeur public {
mémoire privée finale intLimit;
finale privée Deque<int[]> file d'attente; //
set final privé <Long> duplicata; // pour détection duplicata
carte finale privée<Integer, Liste<Integer>> destTs; // dest -> liste d'horodatage
carte finale privée<entier, entier> enlevéIdx; // det -> #Enlève

public Routeur(int memoryLimit) {
ce.memoryLimit = memoryLimit;
ce.queue = nouveau ArrayDeque<>();
ce.duplicate = nouveau HashSet<>();
ce.destTs = nouveau HashMap<>();
ce.retiréIdx = nouveau HashMap<>();
}

/** Construisez une clé unique 64 bits pour un paquet */
privé longue makeKey(int source, int destination, int timestamp) {
// source et destination < 2^18, horodatage < 2^30
retour (((long) source) << 40)= ((long) destination) << 20)= timestamp;
}

public booléen addPacket(int source, int destination, int timestamp) {
longue clé = make Clé(source, destination, horodatage);
si (duplicates.contient(key)) retourner false; // duplicata

// si le routeur est plein, expulser le paquet le plus ancien d'abord
si (queue.size() == mémoireLimiter) {
int[] expulsé = file d'attente.pollFirst();
doublons.supprimer(makeKey(expulsed[0], expulsé[1], expulsé[2]);
supprimerIdxFor(expulsed[1])++; // marquer ts comme enlevé
}

// demande le nouveau paquet
int[] pkt = nouveau int[]{source, destination, timestamp};
file d'attente.addLast(pkt);
duplicata.add(clé);

// conserver l'horodatage pour la destination
detTs.computeIfAbsent(destination, k -> new ArrayList<>()).add(timestamp);
retour vrai;
}

public int[] forwardPacket() {
si (queue.isEmpty()) retourne une nouvelle int[0];
int[] pkt = file d'attente.pollFirst();
doublons.supprimer(makeKey(pkt[0], pkt[1], pkt[2]);
suppriméIdxFor(pkt[1])++; // paquet n'est plus actif
retour pkt;
}

public int getCount(int destination, int startTime, int endTime) {
Liste <Integer> liste = destTs.get(destination);
si (liste == null) retourner 0;

int startIdx = removedIdxFor(destination);
// recherche binaire sur le suffixe actif de la liste
int l = lowerBound(list, startIdx, startTime);
int r = upperBound(list, startIdx, endTime);
retour r - l;
}

*/

/** recherche binaire pour le premier indice >= valeur */
int private int lowerBound(Liste<integer> liste, int offset, valeur int) {
int lo = offset, hi = list.size();
pendant qu ' il y a (l < bonjour) {
Int milieu = (lo + hi) >>> 1;
si (list.get(mid) < valeur) lo = milieu + 1;
Autre salut = milieu;
}
retour lo;
}

/** recherche binaire pour le premier index > valeur */
int private int upperBound(Liste <Intégrer> liste, int offset, int valeur) {
int lo = offset, hi = list.size();
pendant qu ' il y a (l < bonjour) {
Int milieu = (lo + hi) >>> 1;
si (list.get(mid) <= valeur) lo = milieu + 1;
Autre salut = milieu;
}
retour lo;
}

/** obtenir ou initialiser l'index supprimé pour une destination */
Int privé suppriméIdxFor(int destination) {
retour suppriméIdx.computeIfAbsent(destination, k -> 0);
}

carte finale privée<entier, entier> enlevéIdx = nouveau HashMap<>();
}
«» "

> **Pourquoi c'est génial* *
> * Toutes les recherches/insertions sont **O(1)**.
> * `getCount` est **O(log N)** grâce à la recherche binaire.
> * Utilise uniquement des classes JDK standard – aucune bibliothèque externe n'est nécessaire.

---

3.2 Python 3

'`python
#!/usr/bin/env python3
"""
3508. Mettre en œuvre le routeur
"""

à partir de collections import deque
de bisect importer bisect_left, bisect_right
de taper l'importation Liste, Deque, Prêt, Dict

Routeur de classe:
def __init__(self, memoryLimit: int):
self.memory_limit = mémoireLimit
Self.queue: Deque[List[int]] = deque() # FIFO
self.duplicates: Set[int] = set() # 64-bit clé
self.dest_ts: Dict[int, List[int] = {} # dest -> horodatage
Self.removed: Dict[int, int] = {} # dest -> #Enlève

def _key(self, s: int, d: int, t: int) -> Int:
# source < 2^18, dest < 2^18, t < 2^30 → correspond à 64 bits
retour (s << 40)

def addPacket(self, source: int, destination: int, horodatage: int) -> C'est vrai.
key = self._key(source, destination, timestamp)
Si la clé en soi. duplicata:
Retour Faux

si len(self.queue) == self.memory_limit:
expulsed = self.queue.popleft()
ev_key = auto._key(* expulsé)
auto.duplicates.supprimer(ev_key)
Self.remoted[expulsed[1]] = self.remoted.get(expulsed[1], 0) + 1

auto.queue.append([source, destination, horodatage])
auto.duplicates.add(key)
self.dest_ts.setdefault(destination, []).append(timestamp)
retour Vrai

def forwardPacket(self) -> Liste[int]:
si ce n'est pas soi. file d'attente :
retour []
pkt = self.queue.popleft()
Self.duplicates.supprimer(self._key(*pkt))
self.removed[pkt[1]] = self.emoved.get(pkt[1], 0) + 1
retour pkt

def getCount(self, destination: int, startTime: int, endTime: int) -> Int:
si la destination n'est pas en soi. _destinations :
retour 0
ts = autodest_ts[destination]
start_idx = self.exempted.get(destination, 0)
gauche = bisect_left(ts, startTime, lo=start_idx)
droite = bisect_right(ts, finTime, lo=start_idx)
retour à droite - gauche
«» "

> **Notes de python**
> * Utilise `deque` pour O(1) pop de la gauche.
> * `bisect` donne une recherche binaire sur la tranche *active* de la liste d'horodatage.

---

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

***
* 3508. Mettre en œuvre le routeur
*/
Routeur de classe {
public:
Routeur(int memoryLimit) : memoryLimit(memoryLimit) {}

bool addPacket(int source, int destination, int timestamp) {
longue longue clé = make Clé(source, destination, horodatage);
si (dup.count(key)) retourne false; // duplicata

si ((int)q.size() == mémoireLimiter) { // expulser le plus ancien
auto ev = q.front(); q.pop();
dup.erase(makeKey(ev[0], ev[1], ev[2]);
supprimé[ev[1]]++;
}

int pkt[3] = {source, destination, timestamp};
q.emplace(pkt[0], pkt[1], pkt[2]);
dup.insert(clé);
destTs[destination].push_back(timestamp);
retour vrai;
}

vector<int> forwardPacket() {
si (q.vide()) retourne {};
auto pkt = q.front(); q.pop();
dup.erase(makeKey(pkt[0], pkt[1], pkt[2]);
enlevé[pkt[1]]++;
retour {pkt[0], pkt[1], pkt[2]};
}

int getCount(int destination, int startTime, int endTime) {
auto it = destTs.find(destination);
si (it) destTs.end() retourne 0;

Const vector<int> &vec = it->seconde;
début int Idx = enlevé[destination]; // premier t actif
auto left = lower_bound(vec.begin() + startIdx, vec.end(), startTime);
auto right = upper_bound(vec.begin() + startIdx, vec.end(), endTime);
retourner static_cast<int>(à droite - à gauche);
}

particulier:
mémoire int Limite;
file d'attente <array<int, 3>> q; // FIFO
unordered_set<long long> dup; // clés dupliquées
unordered_map<int, vector<int>> destTs; // dest -> horodatage
non ordonné_map<int, int> supprimé; // det -> #Enlève

longue marque en ligne Clef(int s, int d, int t) const {
retour (static_cast<long long>(s) << 40)
(static_cast <long long>(d) << 20)
static_cast<long long>(t);
}
};
«» "

> **Notes C++**
> * `array<int,3>` garde un paquet de taille fixe dans la file d'attente.
> * `lower_bound`/`upper_bound` sur un `vector<int>` donnent la même performance O(log N) que la version Python.

---

- Oui. 4. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
"AddPacket" **O(1)** (spectacle hash-set + pop possible)
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**O(log M)** où *M* est le nombre de paquets *actifs* pour cette destination.

La consommation totale de mémoire est linéaire dans le nombre de paquets dans le routeur (lié par `memoryLimit`).

---

- Oui. 5. Les pièces de "Good" et "Bad" – un regard rapide

- **Bien**
* Utilisation déterministe de la mémoire linéaire – aucune fuite accidentelle.
* Toutes les structures de données sont construites à partir de la bibliothèque standard.
* La recherche binaire sur les horodatages ignore élégamment les paquets expulsés via « removedIdx ».
* La clé unique 64 bits ne garantit aucune collision de hachage (avec probabilité 1).

- **Pièges potentiels**
* Si vous utilisez un hachage 32 bits sur Python/Java et que vous oubliez de emballer la clé, les collisions peuvent causer de faux négatifs.
* Les listes d'horodatage conservent *tous* les horodatages, même supprimés – dans les cas pathologiques, vous pouvez avoir une très grande liste mais "supprimé" conserver la bonne tranche; c'est bien, mais vous devez vous rappeler de les couper si vous voulez libérer la mémoire (pas nécessaire pour les contraintes de problème).
* L'approche suppose que les contraintes (source, destin, temps) s'inscrivent dans 64 bits – ce qui tient pour l'énoncé du problème.

---

- Oui. 5. Le bien et le mal – un résumé rapide

**Ce qui est bon**
- Oui.
O(1) `addPacket`/`forwardPacket`" rend la solution rapide même pour 105 opérations. Autres
O(log N) `getCount`= Échelles vers de nombreuses destinations distinctes. Autres
Autres Pas de bibliothèque externe. Autres
Encodage de la clé 64 bits. Autres

**Ce qu'il faut faire attention**
Il n'y a pas de différence entre les deux.
Autres Éviter le mauvais paquet par accident. Autres
Autres Oublier de mettre à jour `retiré` après l'expulsion. Autres
Utilisez l'argument `lo=` pour limiter la recherche au suffixe actif. Autres

---

- Oui. 6. A emporter pour votre prochaine entrevue

- **L'encodage par changement de cap** est une astuce puissante pour générer un identifiant unique à partir de plusieurs petits entiers.
- **Les ensembles deash** vous donnent des vérifications en double à temps constant.
- **Desques** (ou `ArrayDeque` / `ArrayDeque` en Java) vous donnent des opérations de queue efficaces.
- **La recherche binaire sur les tranches** (via `bisect` ou `lower_bound`) vous permet d'interroger une liste triée tout en ignorant les éléments "inactifs".
- **Cartographier les données par destination** garde `getCount` efficace même lorsque le routeur contient de nombreux paquets.

Cette solution démontre un code propre, des structures de données efficaces et un traitement minutieux des cas de bord – exactement ce que les recruteurs recherchent dans une interview par algorithme.

---

5.1 Liste de contrôle finale

Toutes les fonctions sont publiques (signature LeetCode).
- Utiliser uniquement des conteneurs de bibliothèque standard.
- Il gère correctement la logique de l'expulsion.
- Marque correctement les horodatages comme enlevés lorsque les paquets quittent le routeur.
- "getCount" fonctionne sur le suffixe *actif* de la liste des horodatages.
- La génération de clés 64 bits évite les collisions compte tenu des limites d'entrée.

Bon codage, et bonne chance sur LeetCode et futures interviews!