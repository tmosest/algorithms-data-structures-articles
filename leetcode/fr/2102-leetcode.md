---
titre: LeetCode 2102. Séquentiellement Ordinal Rank Tracker - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le Code – Trois langues, une idée élégante
Vous trouverez ci-dessous une implémentation complète et prête à la production du **Séquentiellement Ordinal Ranking Tracker (SORTracker)** pour **LeetCode 2102 – Hard**.
La même logique est exprimée en **Java, Python et C++** afin que vous puissiez copier-coller dans n'importe quelle langue du juge en ligne ou votre propre IDE.

> **Pourquoi ces langues? * *
> • Java – le plus commun pour LeetCode, avec un `TreeSet` intégré pour O(log N) insert & search.
> • Python – affiche l'implémentation la plus simple à l'aide de la bibliothèque de conteneurs triés («SortedList»).
> • C++ – démontre le trick classique dual-heap (min-heap & max-heap) pour suivre l'élément k.

---

#### 1.1 Java – TreeSet + Pointeur (Simple et rapide)

"Java
Importer java.util. TreeSet;

***
* LeetCode 2102 – Séquentiel Traqueur de rang ordinal
* Complexité temporelle: O(log N) par add/get
* Complexité spatiale: O(N)
*/
classe publique SORTracker {
la version finale privée TreeSet<Location> set = nouveau TreeSet<>();
// Pointeur vers le dernier élément retourné
private Location last = new Location(", Integer. MAX_VALUE;

public SORTracker() {}

public vide ajouter(nom de la chaîne, cote int) {
Emplacement newLoc = nouveau Emplacement(nom, score);
set.add(nouveauLoc);

// Si l'emplacement nouvellement inséré est meilleur (comprend avant) le dernier
// retourné, déplacez le pointeur un pas en arrière pour le garder valide.
si (nouveauLoc.comparerTo(dernier) < 0) {
dernier = set.lower(dernier); // le prédécesseur du pointeur actuel
}
}

chaîne publique get() {
// Déplacez pointeur une étape vers le prochain meilleur emplacement
dernier = set.higher(dernier);
retour dernier. nom;
}

*** Classe d'aide qui implémente la commande requise:
* - meilleur score → meilleur
* - score égal → lexicographiquement plus petit nom est mieux
*/
classe statique privée Lieux comparables {
finale Nom de la chaîne;
la note finale d'entrée;

Emplacement(Nom de la chaîne, cote int) {
Ça. nom = nom;
Ça. score = score;
}

@Override
public int compare to(Emplacement o) {
if (score != o.score) retourner Integer.compare(o.score, score); // desc score
retour name.compareTo(o.name); // asc name
}

@Override
booléen public est égal(Object o) {
si (celui-ci) est vrai;
si (!(o exemple de lieu)) retourner faux;
Emplacement qui = (emplacement) o;
retour du score == that.score && name.equals(that.name);
}

@Override
code hash() public
Retournez java.util. Objets.hash(nom, score);
}
}
}
«» "

**Points clés* *

C'est bien, c'est mal.
C'est pas vrai.
`TreeSet` donne des inserts et des recherches O(log N). Nécessite Java 8+; pas disponible sur certaines plateformes d'entretien qui utilisent des JDK plus anciens. Le fait de garder un pointeur "last" qui doit être déplacé lorsqu'un nouvel élément est mieux peut être déroutant à première vue. Autres
Autres Pas de gestion manuelle du tas – la structure des données gère la commande. La logique `set.lower(last)` peut lancer `NullPointerException` si vous n'êtes pas prudent (ne se produit jamais dans ce problème mais bon à noter). Autres

---

#### 1.2 Python – TriéListe (bibliothèque des contenants ornés)

Si vous êtes sur LeetCode Python, vous ne pouvez pas importer des bibliothèques externes.
Cependant, le *concept* reste le même : garder un arbre de recherche binaire équilibré et un pointeur.

'`python
# Nécessite des 'conteneurs triés' – disponibles sur LeetCode (Python 3.8+)
♪ Si vous êtes sur une machine locale, pip installer triés conteneurs

de conteneurs triés importer TriéListe

Classe SORTracker:
def _init_(self):
# Trié par (-score, nom) → meilleur élément d'abord
self.s = TriéListe(key=lambda loc: (-loc[1], loc[0])
self.idx = -1 # indice du dernier élément retourné

def add(self, nom: str, score: int) -> Aucun:
(nom, score)
# Si le nouvel élément est avant le pointeur actuel, retournez-le
new_index = self.s.bisect_left((nom, score))
si new_index <= self.idx:
Self.idx -= 1

def get(self) -> str:
Auto.idx += 1
retour de soi.s[self.idx][0]
«» "

> **Pourquoi `bisect_left`?**
> Il retourne la position où le nouvel élément serait inséré tout en conservant la liste triée. Si cette position est <= `idx`, le nouvel élément surpasse l'élément précédemment retourné, nous devons donc déplacer le pointeur en arrière.

**Complexités* *

Opération Temps Espace
- C'est quoi ?
Total des O(log N)
O(1) (indexation)

---

#### 1.3 C++ – Doubles Heaps

C++ n'a pas d'arbre équilibré intégré avec commande personnalisée qui donne également un accès rapide aux éléments k.
Un tour classique : gardez un **max-heap** des éléments top `k` et un **min-heap** du reste.
`k` est le nombre de `get()` appels faits jusqu'ici.

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe SORTracker {
// Max-heap pour les éléments k supérieurs (les meilleurs éléments d'abord)
priority_queue<pair<int, string>> top; // (-score, nom) => poids maximal
// Min‐heap pour les éléments restants
priority_queue<pair<int, string>, vector<pair<int, string>,
plus grande <pair<int, string>>> reste; // (score, nom) => min–heap

requêtes int = 0; // nombre d'appels get()

// Aide à maintenir l'invariant: top.size() == requêtes
solde vide() {
// Si nous avons plus d'éléments k dans 'top', déplacez le pire vers 'repos'
si ((int)top.size() > requêtes) {
auto p = top.top(); top.pop();
Repos.push(p);
}
// Si nous avons moins d'éléments k dans 'top', déplacez le meilleur de 'repos'
si ((int)top.size() < requêtes && !rest.vide() {
auto p = repos.top(); repos.pop();
haut.push(p);
}
}

public:
SORTracker() {}

vide add(nom de la chaîne, score int) {
// Insérer dans le «rest» initialement
repos.emplace(score, nom);
équilibre(); // rééquilibre pour maintenir les tailles
}

chaîne get() {
++queries; // nous avons maintenant besoin de l'élément k‐th
balance(); // apporter des éléments k supérieurs au sommet '
auto best = top.top(); // best (score, nom)
Revenez mieux. deuxième; // nom de kth meilleur élément
}
};
«» "

** Pourquoi deux tas ? **

* Le tas `top` contient toujours les meilleurs éléments `k`, où `k` est l'index de requête actuel.
* Lorsqu'un nouvel élément est ajouté, il peut appartenir au "top". La routine `balance()` garantit que `top.size() == requêtes`.
* Nous n'avons jamais à trier l'ensemble de la liste — seulement maintenir deux tas de tailles `k` et `N‐k`.

**Complexités* *

Opération Temps Espace
- C'est quoi ?
O(log N)
O(log k)

---

- Oui. 2. L'article du blog – -

> **Référence géographique* *
> **Séquentiellement Ordinal Rank Tracker – LeetCode 2102 – Hard**
>
> **Description détaillée**
> Découvrez comment résoudre LeetCode 2102 (Séquentiellement Ordinal Rank Tracker) en Java, Python et C++. Découvrez les meilleurs modèles algorithmiques, les compromis et comment cela peut impressionner les recruteurs lors de votre prochaine entrevue.

---

2.1 Introduction

Dans un défi **hard** LeetCode, vous êtes souvent demandé de maintenir un système de classement dynamique tout en répondant aux requêtes *k*-th ordre.
**SORTracker** est le problème qui vous oblige à penser à ** statistiques d'ordre en ligne** – un sujet d'entrevue commun pour les ingénieurs de logiciels seniors et les rôles data-science.

- **Numéro de dossier:** 2102
- **Difficulté:** Dur
- ** Contraintes principales :**
* `1 ≤ N ≤ 10^5` (ensemble des éléments ajoutés)
* `1 ≤ q ≤ N` (nombre d'appels get())
* Chaque nom est unique (pas de duplicata).

Le but : après chaque appel `add()` ou `get()`, retourner le nom *current*, où `k` correspond au nombre `get()` appels effectués jusqu'ici.

---

2.2 Énoncé du problème (sommaire)

> **Don** une séquence d'opérations
> - `add(nom, score)` – insérer une nouvelle personne.
> - `get()` – retourner le nom de la *k*-th meilleure personne, où *k* est le nombre d'opérations `get()` exécutées jusqu'ici.
> **Ordonnance** : score plus élevé = meilleur; liens résolus par un nom lexicographiquement plus petit.

---

2.3 Stratégie de haut niveau

Il y a trois **canonical** solutions qui correspondent parfaitement aux contraintes:

L'approche Ce qu'il utilise Complexité Quand le choisir
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Balanced BST + Pointer**. Autres
**Dual Heaps**= `priority_queue` (C++)== `O(log N)` par opération== Fonctionne dans chaque langue; bon pour les environnements qui n'exposent pas les arbres équilibrés. Autres
Autres **Segment Tree / Fenwick Tree** Trop de compétences pour ce problème, mais bon à savoir pour les variations futures. Autres

L'approche **TreeSet + pointer** est sans doute la plus **accompagnée de production** : la structure de données gère la commande pour vous, et le pointeur permet de suivre l'élément k avec une comptabilité minimale.

---

### 2.4 Le pointeur de la ligne – Ce qui fait que ça marche

1. **Maintenir une collection triée** de tous les emplacements par `(–score, nom)`.
2. **Gardez un curseur (`dernier`)** pointant vers l'élément le plus récemment retourné.
3. ** Lors de l'insertion** :
* Si le nouvel élément dépasse `last`, le curseur doit pas *back* un endroit.
* Sinon, aucun changement.
4. **À l'obtention**:
* Avancez le curseur d'un pas en avant (`higher()` en Java, `idx += 1` en Python).
* L'élément de ce curseur est le meilleur *k-th* pour le `k` actuel.

L'invariant que le curseur est toujours *inside* le set garantit que `get()` est O(1) pour récupérer le nom, alors que `add()` reste O(log N).

---

#### 2.5 Réconciliations – ##Beau, mauvais, mauvais

Aspect du bien
- C'est quoi ?
**Temps**= `O(log N)` par `add` & `get` → correspond à la limite de 105. Aucun – l'algorithme est optimal pour les contraintes données. La logique de mouvement de pointeur peut se sentir "gugly" si vous êtes nouveau à BST itérateurs. Autres
**Espace**=Linéaire ("O(N)") – inévitable pour un système de classement dynamique. En tête du stockage d'une paire `(nom, score)` deux fois dans certaines langues. Autres
**Le code Java `TreeSet` est concis. Le code Python `SortedList` est un bloc unique. La logique du double-pap est plus longue mais élimine le besoin d'un arbre équilibré. Autres
**Appui à l'environnement** 8+ ou une plate-forme qui expose `TreeSet`. Requiert `priority_queue` – toujours disponible. Autres

---

2.6 Effectuer un essai rapide

"Java
public statique vide principal(String[] args) {
Tracker SORTracker = nouveau SORTracker();
tracker.add("alice", 3);
tracker.add("bob", 4);
System.out.println(tracker.get()); // bob (1er meilleur)
Tracker.add("charlie", 4);
System.out.println(tracker.get()); // alice (2e meilleur)
System.out.println(tracker.get()); // charlie (3e meilleur)
}
«» "

Même test fonctionne avec les extraits de Python et C++ après des changements de syntaxe de langage mineurs.

---

2.7 Conclusion et perspectives pour la prochaine entrevue

1. **Balanced BST + pointeur** – La solution la plus simple, O(log N) que la plupart des recruteurs reconnaîtront.
2. **Deux tas** – Un modèle puissant pour les statistiques de l'ordre *k sans tri.
3. **Conteneurs-ordonnés** – Idéal pour Python, mais rappelez-vous les restrictions environnementales de LeetCode.

**Pourquoi cela compte pour votre CV* *

* Démontre la maîtrise de **statistique de l'ordre** – un thème d'entrevue commun pour les rôles supérieurs (arrière-plan, ingénierie des données, conception d'algorithmes).
* Affiche que vous pouvez ** choisir la bonne structure de données** (BST, tas ou même Fenwick) en fonction des contraintes.
* Vous pouvez encadrer le problème comme un système de classement **dynamique** – un excellent point de discussion lorsqu'on décrit une fonctionnalité du monde réel que vous avez construite (p. ex., classement de classement, classement de recommandation).

> ** Mots-clés du référencement**: `Séquentiellement Ordinal Rank Tracker`, `LeetCode 2102 solution`, `dur algorithme interview`, `Java TreeSet`, `Python TriedList`, `C++ dual heaps`, `online Classing system`, `kth order statistic`, `job interview algorithme`.

Bon codage, et bonne chance à ce LeetCode Hard défi!