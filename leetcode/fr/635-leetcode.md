---
titre: LeetCode 635. Design Log Système de stockage -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1. Solutions de code

Ci-dessous sont trois implémentations complètes, prêtes à compiler pour le problème LeetCode **635. Design Log Storage System** – un dans **Java**, un dans **Python** et un dans **C++**.
Toutes les solutions suivent la même idée de haut niveau:

Langue Structure des données Pourquoi ça marche Autres
- C'est-à-dire
Java, `TreeMap<String, liste<entier>>` Keeps timestamps triés; `subMap` donne des requêtes O(log n) range.
Python (en anglais seulement) `list` + `bisect` (en anglais seulement) `bisect` donne une recherche binaire sur les horodatages triés; analyse linéaire sur la plage.
La carte ordonnée donne un accès logarithmique ; simple itération sur la plage.

Chaque solution montre comment *trim* un horodatage en fonction de la granularité demandée, qui est le cœur du problème.

---

## 1.1 Java – TreeMap (est 100 % en pratique)

"Java
Importation de java.util.*;

classe publique LogSystem {
// TreeMap conserve les clés triées par ordre naturel des horodatages de chaîne
fini privé TreeMap<String, liste<integer>> grumes;

// Cartographie granularité à la longueur que nous devons garder de l'horodatage
Carte statique privée<String, entier> GRANULARITY_INDEX = Carte de(
"Année", 4,
"Mois", 7,
"Jour", 10,
"Heure", 13,
"Minute", 16 ans,
"Deuxième", 19
);

public LogSystem() {
logs = nouveau TreeMap<>();
}

public vide put(int id, chaîne horodatage) {
logs.computeIfAbsent(timestamp, k -> new ArrayList<>()).add(id);
}

liste publique<integer> récupérer(démarrage de la chaîne, fin de chaîne, granularité de chaîne) {
int idx = GRANULARITY_INDEX.get(granularité);

// Trim deux extrémités à la granularité
Chaîne startKey = start.substring(0, idx);
Chaîne endKey = fin.substring(0, idx);

// subMap nous donne toutes les entrées dans [startKey, endKey] inclusive
Navigable Carte<String, Liste<entier>> sous = logs.sub Carte(démarrer) La clé, vrai, endKey, vrai);

Liste du résultat <entier> = nouvelle liste de distribution<>();
pour (Liste <entier> ids : sub.values()) {
result.addAll(ids);
}
le résultat du retour;
}
}
«» "

---

## 1.2 Python – Liste + Bisec

'`python
bisect d'importation
de collections importer par défautdict
de taper l'importation Liste

classe LogSystem & #160;:
GRANULARITY_INDEX = {
"Année": 4,
"Mois": 7,
"Jour": 10,
"Heure": 13,
"Minute": 16,
"Deuxième": 19,
}

def _init_(self):
# Gardez les horodatage triés
temps libre = [] # liste des chaînes d'horodatage
auto.ids = [] # liste parallèle des identifiants de log
self.idx = defaultdict(list) # map timestamp -> liste des ID

def put(self, id: int, horodatage: str) -> Aucun:
# Insérez les temps de conservation triés
pos = bisect.bisect_left(self.times, timestamp)
auto.times.insert(pos, timestamp)
auto.ids.insert(pos, id)
Self.idx[timestamp].append(id)

def recovery(self, début: str, fin: str, granularité: str) -> Liste[int]:
i = moi. GRANULARITY_INDEX[granularité]
start_key = start[:i]
fin_key = fin[:i]

# trouver la tranche d'indices qui tombent dans la gamme
lo = bisect.bisect_left(self.times, start_key)
hi = bisect.bisect_right(self.times, end_key)

résultat = []
pour pos à portée(lo, hi):
result.append(self.ids[pos])
résultat du retour
«» "

---

## 1.3 C++ – std::map

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe LogSystem {
public:
// map ordonnée – clé = chaîne timestamp, valeur = liste des ID
la carte <string, vectorielle<int>> les journaux;
ranIndex = {
{"Année", 4},
"Mois", 7 ans,
{"Jour", 10}
"Heure", 13 heures,
{"minute", 16},
{"Deuxième", 19}
};

SystèmeLog() {}

vide put(int id, const string & timestamp) {
logs[timestamp].push_back(id);
}

vector<int> récupérer (const string& start, const string& end, const string& granularity) {
int idx = granIndex.at(granularité);
chaîne s = start.substr(0, idx);
chaîne e = fin.substr(0, idx);

vecteur<int> rés;
pour (auto it = logs.lower_bound(s); it != logs.end() && it->first <= e; ++it) {
res.insert(res.end(), it->second.begin(), it->second.end());
}
retour rés;
}
};
«» "

---

♪ 2. Article de blog – Design Log Storage System: The Good, The Bad et The Ugly

> **SEO Mots-clés**: Leetcode 635, Design Log Storage System, entretien d'emploi, entretien de codage, Java TreeMap, bisect Python, carte C++, conception du système de log, granularité, complexité temporelle, complexité spatiale.

---

2.1 Le problème en anglais clair

Vous construisez un petit service **log-stockage**. Chaque entrée de journal est livrée avec un unique **ID** et un **timestamp** dans le format

«» "
AAAA:MM:JJH:MM:SS
«» "

Par exemple: `"2017:01:01:23:59:59"`.
Vous recevrez au plus des appels **500** `put` (insérer) et `retrieve` (query).

A **query** demande: *donnez-moi tous les ID dont l'horodatage se situe entre `start` et `end` (inclusive), mais ne considérez le temps jusqu'à une certaine **granularité*** (par exemple, ignorez les secondes si la granularité est `"Minute"`).

Le défi est de soutenir les requêtes rapides tout en maintenant la mise en œuvre propre.

---

2.2 Les Naïfs (mais assez) Approche

**Idée**
* Gardez tout dans une liste simple*.

Texte
logs = [] // [(timestamp, id), ...]
«» "

*Lorsque vous demandez, il suffit de scanner toute la liste, de tailler chaque timestamp à la granularité, et de vérifier si elle tombe dans la gamme. *

Texte
pour (timestamp, id) dans les journaux:
si trim(timestamp) dans [départ, fin]:
ajouter id à la réponse
«» "

**Pour**

- Facile à écrire, pas de bibliothèques externes.
- Fonctionne parce que la taille de l'entrée est minuscule.

**Cons**

- **O(n)** temps par requête – bien pour 500, mais terrible pour les entrées plus grandes.
- Oui. Aucune garantie intégrée que les horodatages sont triés, ce qui peut causer des bugs subtils si vous oubliez de garder la commande.

> **Interview Tip** – Lorsque l'intervieweur dit que vous pouvez utiliser un vecteur/liste, il sera très bien, il est généralement un drapeau rouge: l'intervieweur veut que vous pensiez à une structure *ordered*.

---

## 2.3 Le problème d'Ugly: Trimming Timestamps

L'opération *trimming* est au cœur de ce problème.

Nombre de caractères à conserver
- C'est quoi ?
Année Autres
Mois 7 ('AAAA:MM') Autres
Jour 10 ('AAAA:MM:JJ') Autres
Heure : 13 (aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa Autres
Minute 16 ('AAAA:MM:JJ:HH:MM') Autres
Deuxième ('AAAA:MM:JJ:HH:MM:SS')

Donc `trim("2017:01:01:23:59:59", "Minute")` → `"2017:01:01:23:59"`.

Si vous ne le faites pas correctement, vous retournerez les résultats *wrong* ou manquerez les journaux qui devraient être inclus.

---

2.4 La solution efficace – Utiliser une carte **Ordonnée* *

L'astuce est que les horodatages sont **lexicographiquement triables**.
Si nous les conservons dans une structure de données qui maintient l'ordre, nous pouvons couper le temps de requête de façon spectaculaire.

* # # # 2.4.1 Pourquoi un arbre / BST fonctionne

1. **Ordre ordonné**
Chaque horodatage peut être comparé à une chaîne. L'ordre naturel de la chaîne est le même que l'ordre chronologique car tous les composants sont rembourrés à zéro.

2. ** Demandes de renseignements**
Dans un *balanced BST* (Java="TreeMap`, C++="s `std::map`, Python="s `sortedcontainers`" ou même une `list` simple avec `bisect`), nous pouvons localiser le *premier* élément ≥ `start` dans *O(log n*).

3. **Délimitations implicites**
Les fonctions de bibliothèque (`subMap` en Java, `lower_bound`/`upper_bound` en C++/Python) nous permettent de récupérer *exactement* les clés qui nous intéressent.

2.4.2 Mise en œuvre complète de Java (TreeMap)

"Java
TreeMap<String, liste<entier>> journaux;
«» "

*Insertion* – "put"
`computerIfAbsent` + `add` – **O(log n)**

*Query* – "retirer" "

1. Calculer l'indice de tranche pour la granularité demandée.
2. Truncate `start` et `end`.
3. Utilisez `subMap(startKey, true, endKey, true)` pour obtenir la tranche exacte dans **O(log n)**.
4. Aplatissez les listes d'identités.

Résultat : **O(log n + k)** par requête (`k` = nombre de journaux correspondants).

---

## 2.5 Python Spécial: `bisect` sur une liste triée

Le module `bisect`s de Python nous permet de faire une recherche binaire sur une liste **plain**.
L'astuce est de garder **deux listes parallèles**:

Texte
temps = horodatage trié
ids = liste parallèle des ID
«» "

*Inserting* – `bisect.insort` – *O(n)* (éléments de changement), mais toujours bon pour 500 opérations.

*Querying* – `bisect_left/right` pour trouver la tranche d'indices qui appartiennent à la gamme tronquée, puis juste recueillir les IDs.

Le temps global par requête est `O(log n + k)` – assez rapide pour LeetCode et agréable à montrer dans une interview.

---

## 2.6 Edge- Liste de contrôle des cas

Pourquoi ça compte ?
- Oui.
Autres **Même horodatage inséré à deux reprises. `computerIfAbsent` (Java), `log[timestamp].push_back(id)` (C++). Autres
**Granularité = "Second**" Pas de parage – chronomètre complet utilisé. "index = 19". Autres
**Granularité = Année** Autres
**Démarrer > Fin**La requête doit retourner vide. `subMap`/`lower_bound` produira une plage vide. Autres
Autres **Pas de logs dans la plage**. Utilité sur tranche vide – retourne vectoriel/liste vide. Autres

---

2.7 Suivis communs des entrevues

Question: Ce que vous êtes vraiment demandé
-- -- -- -- -- -- -- -- --------------------------------------------------
Autres Et si nous avions 1 000 000 grumes ? Testez votre capacité à raisonner sur *log‐n* vs *n* performance. Autres
Autres Pouvez-vous faire la requête dans O(1)? Trick question – vous ne pouvez pas sauter la recherche binaire si vous avez besoin de garder l'ordre. Autres
Autres Comment supporteriez-vous la suppression ? Dans la solution BST, vous avez pop l'ID du vecteur ou effacer la clé si le vecteur devient vide. Autres
Autres Et si les horodatages n'étaient pas rembourrés ? Vous avez besoin d'un comparateur personnalisé ou d'une analyse dans un objet `datetime`. Autres
Autres Pourriez-vous pré-bucket logs par granularité?=== Oui, vous pouvez garder six tableaux (`an`, `mois`, ...) et la recherche binaire sur le bon. Il permet d'économiser la coupe mais utilise plus d'espace. Autres

---

## 2.8 Prise finale

1. **Trimming** – Une simple tranche de chaîne suffit parce que le format est fixe.
2. ** Carte ordonnée** – Le noyau de la solution efficace.
3. **Complexités** – Avec `TreeMap`/`std::map`, les requêtes s'exécutent dans *O(log n + k*), les insertions dans *O(log n*).
4. **Entretien de codage** – Montrez à l'intervieweur que vous comprenez pourquoi l'ordre compte; posez des questions claires sur les contraintes et les extensions possibles.

Si vous pouvez écrire une solution Java `TreeMap` propre (comme celle ci-dessus) et expliquer la logique de triming, vous allez clouer cette question d'entrevue LeetCode et impressionner tout gestionnaire d'embauche qui aime bonne conception de structure de données.

Bon codage – et bonne chance pour la prochaine interview!