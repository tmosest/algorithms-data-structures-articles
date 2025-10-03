---
titre: LeetCode 2201. Comptez les artéfacts qui peuvent être extraits -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solution 3 langues au code 2201
> **Problème**: *Combien d'objets qui peuvent être extraits*
> **Difficulté**: Moyenne

Ci-dessous vous trouverez une implémentation propre et prête à la production dans **Java, Python et C++**.
Tous les trois utilisent la même approche O(n2) dans le pire des cas, mais fonctionnent dans le temps O(n2) et dans l'espace O(n2), ce qui est parfaitement bien compte tenu des contraintes (`n ≤ 1000`).

---

### 1.1 Java – `HashSet` + `Map`

"Java
Importation de java.util.*;

solution de classe {
artefacts(int n, int[][] artefacts, int[][] artefacts) {
// Cartez chaque cellule qui a été creusée à l'identifiant de l'artefact qui l'occupe.
Carte<entier,entier>celluleToArtifact = nouvelle HashMap<>();
pour (int id = 0; id < artefacts.longueur; id++) {
int[]a = artefacts[id];
pour (int r = a[0]; r <= a[2]; r++) {
pour (int c = a[1]; c <= a[3]; c++) {
cellToArtifact.put(r * n + c, id);
}
}
}

// Comptez combien de cellules de chaque artefact ont été creusées.
int[] découvert = nouvelle int[artefacts.longueur];
Int extrait = 0;
pour (int[]d : creuser) {
clé int = d[0] * n + d[1];
id entier = cellToArtifact.get(key);
si (id != null) {
si (++ non couvert[id] == countCells(artifacts[id], n)) {
extrait ++;
}
}
}
retour extrait;
}

Cells(int[] a, int n) {
// (r2 - r1 + 1) * (c2 - c1 + 1) est au plus 4 par énoncé de problème
retour (a[2] - a[0] + 1) * (a[3] - a[1] + 1);
}
}
«» "

---

### 1.2 Python – `set` + dictionnaire

'`python
de taper l'importation Liste

Solution de classe:
def digArtifacts(
self, n: int, artefacts: List[List[int]], creuser: List[List[int]]
-> Int:
# Cellulaire de carte -> index des artefacts
Cell_to_id = {}
pour idx, (r1, c1, r2, c2) dans l'énumération (articles):
pour r dans la plage (r1, r2 + 1):
pour c dans la plage(c1, c2 + 1):
cellule_to_id[(r, c)] = idx

découvert = [0] * len(objets)
extrait = 0
pour r, c en creuse:
idx = cell_to_id.get((r, c))
si idx n'est pas None:
découvert[idx] += 1
s'il est découvert[idx]] (artefacts[idx][2] - artefacts[idx][0] +1) * (
artefacts[idx][3] - artefacts[idx][1] + 1
) :
extrait += 1
retour extrait
«» "

---

### 1.3 C++ – `unordered_map` + vecteur

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int digArtifacts(int n, vector<vector<int>>& artefacts, vector<vector<int>>& dig) {
non ordonné_map<long long, int> cellToId;
clé automatique = [n](int r, int c) { retour (long)r * n + c; };

pour (int id = 0; id < artefacts.size(); ++id) {
auto& a = artefacts[id];
pour (int r = a[0]; r <= a[2]; ++r)
pour (int c = a[1]; c <= a[3]; ++c)
cellToId[key(r, c)] = id;
}

vecteur<int> découvert(artefacts.size(), 0);
Int extrait = 0;

pour (auto& d : creuser) {
long k = clé(d[0], d[1]);
auto it = cellToId.find(k);
si (it != cellTod.end()) {
int id = it->seconde;
si (++ non couvert[id] == countCells(artifacts[id], n))
+ extrait;
}
}
retour extrait;
}

particulier:
int countCells(vecteur const<int>& a, int n) {
retour (a[2] - a[0] + 1) * (a[3] - a[1] + 1); // ≤ 4 par déclaration
}
};
«» "

> **Complexité temporelle**: «O(n2)» dans le pire des cas (lorsque toutes les cellules font partie d'artefacts).
> **Complexité spatiale**: `O(n2)` pour la carte de hachage qui contient des entrées `n2`.

---

- Oui. 2. Article du blog – LeetCode de maîtrise 2201: Le bon, le mauvais, et le mauvais

> *Référencement Titre:*
> **Count des objets qui peuvent être extraits – Java, Python, C++ Solutions + Conseils d'entrevue**
> *Meta Description: *
> Découvrez comment résoudre LeetCode 2201 avec un code clair et prêt à la production en Java, Python et C++. Comprendre le problème, les pièges et les stratégies prêtes à l'entrevue. Augmentez votre score d'entrevue de codage!

---

2.1 Introduction

Quand vous débarquez un entretien d'ingénierie logicielle, LeetCode , *Moyen , les problèmes sont l'endroit idéal : ils sont assez difficiles pour montrer la profondeur mais toujours solvables avec des fondamentaux solides. L'un de ces problèmes est **2201 – Compter les artefacts qui peuvent être extraits**. C'est comme un puzzle, étant donné un ensemble d'objets rectangulaires et une série de fouilles, compter combien d'objets sont complètement découverts.

Dans cet article, nous allons passer par le **bon** (pourquoi le problème est une grande question d'interview), le **bad** (pièges communs et pourquoi les solutions naïves échouent), et le **ugly** (approches moins optimistes mais toujours correctes). Nous présentons également trois solutions d'agnostic en langage propre en Java, Python et C++, prêtes à être collées dans votre prép d'entrevue ou votre dépôt d'applications.

---

2.2 Récapitulation du problème

- **Grid**: `n × n` (0-indexé).
- **Artefacts**: Jusqu ' à 105 rectangles, chacun couvrant au plus 4 cellules. Pas deux artefacts se chevauchent.
- **Digs**: Jusqu ' à 105 points de coordonnées uniques.
- **Objectif**: Retourner combien d'objets ont *toutes* leurs cellules excavées.

> **Pourquoi c'est important:**
> - Poignées *hachage spatial* (cellule → artefact).
> - Fonctionne avec l'entrée *sparse* (les artefacts et les fouilles sont beaucoup moins nombreux que `n2`).
> - Capacité de tester les coordonnées 2D aux clés 1-D.

---

2.3 Le bon – Ce qui rend ce problème grand

Caractéristiques Pourquoi il est utile
C'est-à-dire
**Petite taille d'artefact**= Limite les boucles intérieures; vous pouvez en toute sécurité itérer sur chaque artefact==cellule. Autres
**Pas de chevauchement**= Simplifie la cartographie : chaque cellule appartient à au plus un artefact. Autres
**Sparse digs** Autres
**Difficulté moyenne**= Indique que vous êtes à l'aise avec les cartes de hachage, la conversion 2D en 1D et le comptage. Autres

2.4 Les mauvaises – erreurs courantes

Conséquence
C'est pas vrai.
**O(n2) simulation de grille complète**= Avec `n = 1000`, cela signifie 1 000 000 cellules; acceptable, mais inutile si les artefacts sont peu nombreux. Autres
**Linear scan pour chaque fouille**= `dig.longueur * artefacts.longueur` peut atteindre les opérations `1010`. Autres
**L'utilisation de tableaux 2D pour toutes les cellules**=La mémoire s'envole: 1 000 000 booléens est bien, mais si vous devez stocker des identificateurs d'artefacts par cellule, cela devient coûteux. Autres
**Ignorer la garantie de 4 cellules au plus** Autres

2.5 L'Ugly – Naïve Brute Approche de la force

'`python
# O(artefacts * creuser) ~ 10^10
def laid_solution(n, artefacts, creuser):
extrait = 0
pour les artefacts:
all_exposé = Vrai
pour r dans la plage (a[0], a[2] + 1):
pour c dans la plage a[1], a[3] + 1:
si [r, c] ne sont pas creusés:
all_exposé = Faux
pause
si ce n'est pas all_exposé:
pause
si all_exposé:
extrait += 1
retour extrait
«» "

Pourquoi c'est moche ? *
- Balayage linéaire sur "dig" pour chaque cellule de chaque artefact.
- La complexité du temps explose même pour des apports modérés.
- Difficile à lire et à déboguer.

2.6 Le code propre – Solution efficace

L'idée clé : **hash chaque cellule creusée** une fois, et **map chaque cellule à son artefact propriétaire**. Puis, pour chaque fouille, il suffit d'augmenter un compteur pour cet artefact. Quand le compteur est égal à la taille de l'artefact, nous l'avons entièrement découvert.

##### 2.6.1 2‐D → 1‐D Key Trick

Une coordonnée 2-D `(r, c)` peut être transformée en un seul numéro:

«» "
clé = r * n + c // fonctionne parce que 0 ≤ r, c < n
«» "

Cela fonctionne pour les cartes de hachage dans les trois langues.

Code Pseudo

«» "
créer map cellToArtifact
pour chaque id artefact, rect:
pour r de rect.r1 à rect.r2:
pour c de rect.c1 à rect.c2:
celluleToArtifact[key(r,c)] = id

Count découvert = tableau[artifactCount] = 0
extrait = 0

pour chaque fouille (r,c):
si clé(r,c) dans cellToArtifact:
id = celluleToArtifact[key(r,c)]
Nombre découvert[id] += 1
si découvertCount[id] == size_of(article[id]):
extrait += 1

retour extrait
«» "

2.6.3 Analyse de complexité

Étape
C'est quoi ?
Bâtiment `cellToArtifact`=1 `O(total_cells)` ≤ `4 * artefacts.longueur` ≤ 4 × 105=1
Traitement des fouilles ≤ 105 %
Total **O(total_cells + dig.longueur)** → linéaire en taille d'entrée. Autres
Espace supplémentaire **O(total_cellules)** pour la carte de hachage + compteurs. Autres

---

2.7 Extraits de code de préparation à la production

*(voir les solutions en 3 langues ci-dessus)*

Tous les trois partagent le même squelette algorithmique, juste adapté aux idiomes du langage. N'hésitez pas à copier-coller dans votre dépôt, à annoter les commentaires ou à les utiliser comme référence d'étude.

---

### 2.8 Conseils d'entrevue et à emporter

1. ** Expliquez votre design d'abord** – parlez de la carte ..cell → artefact.
2. **Mention la clé 2-D à 1-D** – c'est un tour classique dans l'esprit des intervieweurs.
3. **Parler de la taille de l'artefact lié** – montre que vous comprenez les contraintes du problème.
4. **Cas d'Edge**: zéro artefacts, zéro fouille, ou fouilles qui manquent tous les artefacts—couvrez-les dans les tests unitaires.

> En cas de doute, demandez à l'intervieweur ce qu'il considère comme la meilleure approche de la structure des données.
> Cela signale la collaboration et maintient la dynamique de la conversation.

---

2.8 Enveloppe

LeetCode 2201 est un petit problème de comptage spatial bien contraint qui teste une poignée de compétences de base dans la structure des données. La solution efficace est conceptuellement simple mais élégante : hacher toutes les cellules creusées, cartographier les cellules aux artefacts et compter les expositions. Les implémentations Java, Python et C++ ci-dessus sont prêtes à l'emploi, testées au combat, et peuvent être ajoutées à n'importe quelle base de code -interview.

> **Prochaine étape**: Ajouter des tests unitaires, exécuter sur des cas aléatoires et pratique expliquant l'algorithme verbalement.
> **Bonus tip**: Poussez votre dépôt vers GitHub, et ajoutez un `README` qui énumère le problème, les contraintes et les solutions – votre propre compagnon d'entrevue.

Bon codage, et bonne chance pour la prochaine interview !

---

*© 2024 Votre nom – Tous droits réservés. *

---

> **Disclaimer:**
> Les échantillons de code sont fournis à des fins éducatives et ne sont liés à aucune demande d'emploi spécifique. Suivez toujours les normes de codage de votre organisation et les lignes directrices de style lors d'une entrevue.