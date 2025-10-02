---
Titre: LeetCode 364. Liste des nids Poids Somme II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le Code

Ci-dessous sont trois solutions prêtes à coller qui passeront les cas de test officiels LeetCode.
Chaque extrait met en œuvre la même stratégie *one-pass BFS* :
* tout en traversant la liste, nous gardons la profondeur actuelle,
* accumulent la somme de tous les entiers (`sumElements`) et la somme de *profondeur × entier* (`sumDepthProduct`),
* suivre la profondeur maximale ('maxDepth').
Après la boucle, nous pouvons déduire la réponse en O(1):

«» "
réponse = (maxDepth + 1) * sommeÉléments - sumDepthProduit
«» "

Cette formule découle directement de la définition du poids inverse.

---

### Java (Signature de code leet)

"Java
Importation de java.util.*;

solution de classe {
profondeur de l'inte publique SumInverse(Liste<NestedInteger>Liste imbriquée) {
Queue<NestedInteger> q = nouvelle List Linked<>(List nested);

profondeur int = 1;
d'une puissance n'excédant pas 50 kW
les éléments = 0;
int sumDepthProduct = 0;

alors que (!q.isEmpty()) {
taille int = q.size();
maxDepth = Math.max(maxDepth, profondeur);

pour (int i = 0; i < taille; i++) {
NestedInteger cur = q.poll();

si (cur.isInteger()) {
int val = cur.getInteger();
les montants += valeur;
sumDepthProduct += val * profondeur;
} autre {
q.addAll(cur.getList());
}
}
profondeur++;
}

retour (maxDepth + 1) * sumElements - sumDepthProduct;
}
}
«» "

> **Note**: Dans l'environnement LeetCode, l'interface `NestedInteger` est déjà fournie.
> Si vous testez localement, vous pouvez créer un talon simple:

"Java
classe NestedInteger {
privé Valeur entière;
liste privée <NestedInteger>;

// Constructeurs, getters et setters omis pour la brièveté
}
«» "

---

Python 3

'`python
à partir de collections import deque
de la liste d'importation dactylographiée, Union

# LeetCode stub – vous n'avez pas besoin de l'appliquer
classe NestedInteger:
def __init__(self, valeur: Union[int, List] = None):
i isstance(valeur, int):
self._int = valeur
auto_liste = Aucune
Sinon:
auto_int = Aucune
self._list = valeur si la valeur n'est pas Aucune autre []

def isInteger(self) -> bool:
return self._int n'est pas None

def getInteger(self) -> Int:
retourner soi-même._int

def getList(self) -> Liste["NestedInteger"]:
return self._list

Solution de classe:
profondeur SumInverse(self, imbriquéListe: Liste[NestedInteger]) -> Int:
q = deque(NestedList)

profondeur = 1
max_profondeur = 0
somme_éléments = 0
sum_profondeur_product = 0

alors que q:
Taille = lenq
max_profondeur = max(max_profondeur, profondeur)

pour _ dans la gamme(size) :
cur = q.popleft()
si cur.isInteger():
val = cur.getInteger()
somme_éléments += valeur
sum_profondeur_produit += val * profondeur
Sinon:
q.extend(cur.getList())
profondeur += 1

retour (max_profondeur + 1) * somme des éléments - sum_profondeur_produit
«» "

---

C++ (Signature du code à gauche)

'`cpp
#incluez <vecteur>
#incluez <queue>
utilisant l'espace de noms std;

solution de classe {
public:
profondeur intSumInverse(vecteur<NestedInteger> &NestedList) {
file d'attente <NestedInteger> q;
pour (auto &ni : imbriquéListe) q.push(ni);

profondeur int = 1;
d'une puissance n'excédant pas 50 kW
les éléments = 0;
int sumDepthProduct = 0;

pendant que (!q.vide()) {
int sz = q.size();
maxDepth = max(maxDepth, profondeur);

pour (int i = 0; i < sz; ++i) {
NestedInteger cur = q.front(); q.pop();

si (cur.isInteger()) {
int val = cur.getInteger();
les montants += valeur;
sumDepthProduct += val * profondeur;
} autre {
vecteur const<NestedInteger> &lst = cur.getList();
pour (const auto &x : lst) q.push(x);
}
}
+ profondeur;
}

retour (maxDepth + 1) * sumElements - sumDepthProduct;
}
};
«» "

> **C++ Stub**
> Dans un environnement local, vous pourriez avoir besoin d'une mise en œuvre minimale `NestedInteger`:

'`cpp
classe NestedInteger {
public:
NestedInteger() : is_int(false) {}
NestedInteger(int val) : is_int(true), integer(val) {}
bool isInteger() const { retour is_int; }
int getInteger() const { retourner entier; }
const vector<NestedInteger> &getList() const { return list; }
vide add(const NestedInteger &ni) { list.push_back(ni); }
particulier:
bool is_int;
entier;
vectorielle<NestedInteger> liste;
};
«» "

---

- Oui. 2. L'article du blog

Titre
**LeetCode 364 – Liste de nids Poids Sum II: Une solution BFS à un pass en Java, Python et C++**

Description de la méta
Apprenez comment résoudre efficacement LeetCode 364 (Nested List Weight Sum II). Lisez notre guide étape par étape avec des extraits de code Java, Python et C++, ainsi qu'une plongée profonde dans les compromis algorithmiques.

---

Présentation

Si vous préparez une entrevue d'ingénierie logicielle, problème LeetCode **364 – Liste de nids Poids Sum II** est un classique.
Il vous demande de calculer la somme pondérée d'une liste imbriquée où le poids d'un entier est **profondeur inverse**:

> **Poids = longueur maximale – profondeur + 1**

L'objectif est de revenir
`- (poids entier *)` pour tous les entiers de la liste.

Il est trompeurment simple mais teste votre capacité à raisonner sur la récursion, la recherche profondeur première (DFS), la recherche largeur première (BFS), et la perspicacité mathématique.

Dans ce post, nous allons couvrir:

* Rétablissement des problèmes et contraintes
* Une solution BFS à un seul passage (le code est déjà fourni ci-dessus)
* L'approche de la "bad" qui peut causer le débordement de la pile
* L'astuce basée sur la formule de la formule qui peut faire monter les débutants
* SEO-friendly points saillants pour aider votre classement d'article pour les questions d'entrevue

Laisse plonger.

---

- Oui. Le problème (Résumé)

- Entrée : `Liste<Nestedinteger> Liste imbriquée "
- Chaque élément est :
* un entier
* une liste des autres `NestedInteger`s (négatif arbitrairement)
- Profondeur d'un entier = nombre de listes il est à l'intérieur de
- `maxDepth` = profondeur entière la plus profonde
- Poids d'un entier = `maxDepth - profondeur + 1`
- Retourner la somme pondérée de tous les entiers

**Contrôles* *

Valeur des contraintes
C'est pas vrai.
1 ≤ " longueur de la liste " ≤ 50
Valeur entière
Dépôt maximal ≤ 50
Autres Aucune liste vide

---

- Oui. Le «Good» – Un-Pass BFS

- Oui. Pourquoi BFS ?

* **Niveau par niveau**: piste naturellement la profondeur sans récursion.
* **Itératif** : aucun risque de débordement de cheminée sur des listes profondément imbriquées.
* **Visite unique**: nous pouvons calculer `maxDepth`, `sumElements` et `sumDepthProduct` en un seul passage.

- Oui. Les mathématiques

Laissez :

- `S = entier '
- `P = ↓ (entier × profondeur)`
- `D = Depth max`

La somme pondérée «W» est:

«» "
W = entier = (D - profondeur + 1)
= nombre entier × (D + 1) - nombre entier × profondeur
= (D + 1) × S - P
«» "

Donc, après le BFS, nous calculons juste `W = (D + 1) * S - P`.

Temps et espace

La complexité Raison
C'est pas vrai.
Chaque entier/liste traité une fois
**O(d)**=d` = profondeur maximale; la taille de la file ne dépasse jamais la largeur du niveau actuel

Le code des trois langues figure déjà dans la section précédente.

---

- Oui. Le "Bad" – Récursion profonde

Une solution étudiante commune utilise DFS avec récursion, passant la profondeur actuelle comme paramètre. Bien qu'élégant, il a des pièges:

* **Débordement de la pile** si la profondeur de nidification approche de la limite de récursion (~1000 en Java, ~1000 en Python, ~10 000 en C++). LeetCodeS contrainte de profondeur ≤ 50 est sûr, mais les intervieweurs aiment vous pousser plus fort.
* **Deux passes**: soit calculer `maxDepth` d'abord (DFS) puis recalculer la somme pondérée, soit stocker chaque entier et sa profondeur dans une liste, puis post-processus.

Si vous devez utiliser DFS, assurez-vous:

1. Entreposer les paires (entier, profondeur) dans un vecteur/array.
2. Trouvez "maxDepth".
3. Calculer `(maxDepth + 1) * S - P '.

Même alors, le code devient plus verbeux et plus difficile à lire.

---

- Oui. L'Ugly – Essayer d'éviter la formule

Certains participants tentent d'appliquer directement des poids pendant la traversée :

```pseudo
pour chaque entier:
poids = (dente + 1)
résultat += entier * poids
«» "

Mais `maxDepth` est *inconnu* jusqu'à la fin de la traversée!
Vous finissez ainsi :

* **Storing** tous les entiers ayant un poids provisoire, ou
* **Mise à jour** poids à la volée après avoir découvert des nœuds plus profonds (qui nécessitent une recomputation ou une structure de données dynamique).

C'est exactement ce que supprime la formule : vous n'avez besoin de *profondeur × entier* qu'une fois, puis d'un liner pour la somme finale.

---

## Une liste de vérification pour les intervieweurs

Conseil rapide Ce que le candidat devrait mettre en évidence
- Oui.
*Utiliser le BFS, pas le DFS*
*Track trois agrégats *= `S`, `P`, `D` dans une boucle
*Afficher la formule (D + 1) × S – P – démontre la pensée mathématique.
*Les limites de la pile de Mention*
*Espace d'explication * , largeur de la file < largeur du niveau le plus profond

---

## SEO Boosters

Le pilier du référencement Comment nous l'utilisons
C'est quoi ?
**Mots-clés**=LeetCode 364=,=Nested List Poids Sum II=,=Interview BFS=,=Java Python C++ solution=
**Balises d'en-tête**=H2/H3 utilisé pour problème, algorithme, langues, pièges
**Points du bulletin** , c'est clair, concis, aide les lecteurs
**C clôtures de code**= `java`, `python`, balises `cpp` pour les moteurs de recherche à index=
**Description détaillée**
**Liens internes**

N'hésitez pas à ajouter le lien d'ancrage suivant au bas de l'article:

html
Code de la java
Code du python
<a href="#c++-solution">C++ Code </a>
«» "

---

Conclusion

LeetCode 364 est une illustration soignée de la façon dont un problème simple peut avoir des solutions élégantes, efficaces et risquées. Le **one-pass BFS** est le plus convivial pour les entrevues :

1. **Itératif** – aucune limite de récursion.
2. **Heure linéaire** – un scan de toute la liste.
3. **Mathématiquement concis** – une seule ligne d'arithmétique après la boucle.

Utilisez les extraits de code ci-dessus pour ajouter à votre repo GitHub, portfolio ou pratique personnelle.
N'hésitez pas à copier l'article dans Medium, Dev.to, ou votre blog personnel et regardez-le classer pour *=LeetCode 364 solution==*.

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit.

---

### TL;DR

* **Problème** – Somme pondérée avec profondeur inverse.
* ** Bonne solution** – One-pass BFS + `(maxDepth+1)*S – P`.
* **Bad solution** – DFS récursif qui peut déborder.
* **Ugly** – Tentative d'appliquer des poids directement sans la formule.

Le code Java, Python et C++ ci-dessus est prêt pour copier et coller et passera tous les tests officiels de LeetCode.