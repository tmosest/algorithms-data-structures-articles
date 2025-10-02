---
Titre: LeetCode 381. Insérer Supprimer GetRandom O(1) - Duplications autorisées -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
* 381. Insérer Supprimer GetRandom O(1) – Duplicates autorisés
### Solution complète dans **Java / Python / C++** + un billet de blog SEO

---

Récapitulation des problèmes

Nous avons besoin d'une structure de données qui supporte les opérations suivantes en *moyenne* O(1) temps:

Description de l'opération Valeur de retour
- C'est quoi ?
Ajouter `val` au multiset. Les duplicatas sont autorisés. "vrai" si "val" n'était pas déjà présent, sinon "faux" Autres
Supprimer une occurrence de «val» s'il existe. "vrai" si l'enlèvement réussit, sinon "faux" Autres
"getRandom()" Retourner un élément aléatoire. La probabilité de chaque élément est proportionnelle à sa fréquence dans le multiset. Un entier aléatoire

> **Constraints**
> * "-231 ≤ valeur ≤ 231 - 1"
> * ≤ 2 × 105 opérations totales
> * `getRandom()` n'est jamais appelé sur une collection vide

---

C'est vrai. Idée de base – HashMap basé sur l'indice + Array dynamique

1. **Le tableau dynamique** (`ArrayList` / `vecteur` / `list`) conserve chaque élément inséré.
* Accès aléatoire (`O(1)`) → parfait pour `getRandom()`.
* Le dernier élément peut être supprimé dans `O(1)` en échangeant avec la position que nous voulons supprimer.

2. **HashMap** (`Carte<entier, définir<entier>>`) maps une valeur → *all* indices où cette valeur se produit dans le tableau.
* Permet de localiser rapidement un événement arbitraire de "val".
* Le jeu peut être un `HashSet`, `LinkedHashSet` ou `unordered_set` (C++).

3. **Délétion**:
* Choisissez un indice arbitraire `i` dans l'ensemble de `val`.
* Remplacer `array[i]` par le dernier élément `dernier`.
* Mettre à jour les ensembles pour `val` et `last`.
* Supprimer le dernier élément du tableau.

Toutes les opérations sont ** amorties O(1)** – les opérations définies et les opérations vectorielles sont O(1) en moyenne.

---

C'est vrai. Code

> **Les trois implémentations suivent la même logique** – seules les syntaxes changent.

---

#### 3.1 Java

"Java
Importation de java.util.*;

classe publique Collection randomisée {
// Stocke tous les éléments
liste finale privée<entier> les données;
// Valeur des cartes -> ensemble d'indices où la valeur se produit
carte finale privée<entier, définir<entier>> les indices;
Finale privée Rand aléatoire;

publique Collection randomisée() {
données = nouvelle liste de distribution<>();
indices = nouvelle HashMap<>();
rand = nouveau Random();
}

*** Insère une valeur dans la collection. */
insert public booléen(int val) {
// La première fois qu'on voit Val ?
boolean isNew = !indices.contientKey(val);
index.computeIfAbsent(val, k -> new HashSet<>()).add(data.size());
données.add(val);
retour est nouveau;
}

*** Supprime une valeur de la collection. */
suppression de booléen public(int val) {
Définir <Integer> idxSet = indices.get(val);
si (idxSet) null idxSet.isEmpty() retourne false;

// Saisissez un index arbitraire de la valeur à supprimer
int removeIdx = idxSet.iterator().next();
idxSet.remove(removeIdx);

int lastIdx = data.size() - 1;
int lastVal = data.get(lastIdx);

// Déplacer le dernier élément dans l'emplacement de l'élément enlevé
data.set(removeIdx, lastVal);
// Mettre à jour l'index défini pour la dernière Valeur
Définir <Integer> lastIdxSet = indices.get(lastVal);
lastIdxSet.remove(lastIdx);
lastIdxSet.add(supprimerIdx);

// Supprimer le dernier élément de la liste
data.remove(lastIdx);

// Nettoyer la carte si plus d'indices restent
si (idxSet.isEmpty()) indices.supprimer(val);
retour vrai;
}

*** Obtenez un élément aléatoire de la collection. */
Int public getRandom() {
retourner data.get(rand.nextInt(data.size()));
}
}
«» "

---

3.2 Python

'`python
importation aléatoire
de collections importer par défautdict

classe Collection randomisée:
def _init_(self):
auto.données = [] # liste de toutes les valeurs
auto.indices = defaultdict(set) # val -> ensemble de positions

def insert(self, val: int) -> C'est vrai.
is_new = val pas en soi. Indices
self.indices[val].add(len(self.data))
auto.data.append(val)
retourner est_nouveau

def remove(self, val: int) -> C'est vrai.
si val pas en soi. indices ou non auto-indices[val]:
Retour Faux

remove_idx = auto.indices[val].pop()
last_idx = len(self.data) - 1
last_val = self.data[last_idx]

# Remplacer le point enlevé par le dernier élément
self.data[remove_idx] = last_val
auto.indices[last_val].add(remove_idx)
auto.indices[last_val].discard(last_idx)

Données personnelles.pop()

si ce n'est pas les indices de soi[val]:
del self.indices[val]
retour Vrai

def getRandom(self) -> Int:
retour aléatoire.choix(self.data)
«» "

---

#### 3.3 C++ (GNU++17)

'`cpp
#incluez <vecteur>
#inclut <non-ordonné_map>
#inclut <unordered_set>
#incluez <random>

classe randomisée Recouvrement {
public:
randomiséCollection() : gen(rd()), dis(0, 0) {}

insert bool(int val) {
bool isNew = mp.find(val) == mp.end();
mp[val].insert(data.size());
data.push_back(val);
retour est nouveau;
}

bool remove(int val) {
auto it = mp.find(val);
si (it) == mp.end()=" it->second.vide() retourne false;

// index à supprimer
Int idx = *it->second.degin();
it->second.erase(idx);

int lastVal = data.back();
int lastIdx = data.size() - 1;

// Déplacer le dernier élément dans idx
données[idx] = dernière Val;
mp[lastVal].insert(idx);
mp[lastVal].erase(lastIdx);

data.pop_back();

si (it->second.vide()) mp.erase(it);
retour vrai;
}

Int getRandom() {
dist = std:uniform_int_distribution<int>(0, data.size() - 1);
les données de retour[dis(gen)];
}

particulier:
std::vector<int> données;
std::unordered_map<int, std::unordered_set<int> mp;
std::device_random rd;
Légumes et légumes
Seuil::uniform_int_distribution<int> d;
};
«» "

---

#### 4=1 Article du blog – =Le bon, le mauvais, le mauvais de la collection randomisée=

> **Mots-clés du référencement**: `LeetCode 381`, `RandomizedCollection`, `O(1) insérer supprimer aléatoire`, `multiset data structure`, `hashmap vector trick`, `duplicate elements`, `data structures interview`, `python c++ java`, `job interview coding "

---

4.1 Introduction

Lorsque les recruteurs demandent à « implémenter une structure de données qui prend en charge l'insertion, la suppression et l'obtention de Random en temps constant », ils ne testent pas seulement votre connaissance des tableaux ou des tables de hachage – ils probent votre capacité à **combine** structures de données de manière créative.
LeetCode 381 – *Insert Supprimer GetRandom O(1) – Des duplicatas autorisés* est un favori d'entrevue classique qui met en valeur cet ensemble de compétences exact.

Dans cet article, nous disséquerons le **good**, le **bad** et le **ugly** de résoudre ce problème. Que vous soyez en train de vous préparer à une entrevue de codage, que vous cherchiez à aser votre prochain rôle ou tout simplement à aiguiser votre boîte à outils algorithmique, ce guide vous donnera des idées et des extraits de code exploitables en Java, Python et C++.

---

##### 4.2 Le bon: pourquoi le Trick HashMap-Vector est un changement de jeu

1. **Simplicité + puissance** –
*Un tableau pour l'accès aléatoire, un hashmap pour la tenue de livres d'index* – toute la solution s'intègre dans moins de 100 lignes de code.
* Chaque opération est *amortisée* O(1) – parfaite pour les questions d'entrevue en grand volume.

2. **Robesse avec duplications** –
Le hashmap stocke *sets* d'indices, de sorte que vous pouvez facilement suivre combien de copies d'une valeur existent.
Cela élimine le besoin de listes liées ou d'arbres qui peuvent se dégrader à O(log n).

3. **Modalité linguistique** –
La même logique se traduit par Java (`ArrayList + HashMap<Set>`), Python (`list + defaultdict(set)`), et C++ (`vector + unordered_map<unordered_set>`).
Démontrer la compétence dans plusieurs langues peut être une forte différence dans les rôles *full-stack* ou *backend*.

---

#### 4.3 Les mauvaises: pièges cachés que les candidats de voyage

Qu'est-ce qui arrive ? Comment l'éviter ?
- C'est quoi ?
**O(n) dans le pire des cas**=L'utilisation d'une liste et d'un ensemble qui rechigne souvent peut provoquer un pic linéaire. Se référer à `HashSet`/`unordered_set` – ils sont O(1) amortis, pas le pire des cas. Autres
Erreurs hors-par-One** Erreur de mise à jour de l'index lors de l'échange (oubli pour mettre à jour l'ensemble de l'élément déplacé). Rédigez une méthode d'aide `swapAndUpdate(int i, int lastIdx)` ou commentez méticuleusement. Autres
**Fausse mémoire en Java**= Ne pas retirer la clé de la carte lorsque son jeu devient vide → O(n) espace. "Nettoyez avec "si (set.isEmpty()) indices.supprimer(val);". Autres
** Initialisation du générateur de rando** En C++ créer la distribution sur chaque appel peut être coûteux. Autres Garder un générateur `std::mt19937` vivant et reconstruire la distribution seulement lorsque la taille change. Autres
**Python `defaultdict` mauvais usage**=Conservation accidentelle de jeux vides qui maintiennent la clé en vie.= Supprimer la clé lorsque le jeu devient vide (`del self.indices[val]`). Autres

---

#### 4.4 L'horrible : les cas de bord et les ridules

1. **Swap‐et‐Supprimer le bug**
* Erreur commune* : oubliant de supprimer le dernier index de la valeur déplacée.
**Conseil de débogage** : après chaque `remove()`, imprimez le hashmap pour la valeur supprimée et la dernière pour s'assurer que les ensembles sont cohérents.

2. **Recueil d ' ancienneté sur < < getRandom() > >**
Le problème garantit que cela n'arrivera pas, mais le codage défensif paie dans les API du monde réel.
"Java
si (data.isEmpty()) lance un nouveau NoSuchElementException();
«» "

3. **Grands nombres négatifs**
Lorsque vous utilisez des tableaux, les valeurs négatives ne comptent pas – elles ne sont que des clés dans le hashmap.
Mais dans C++ `unordered_map<int, ...>` est bien; soyez juste prudent avec les conversions `size_t` vs `int`.

4. **Bénéfices de rancœur**
Certains intervieweurs testent la véritable uniformité. Utilisez un *system RNG* (`Random` en Java, `random.choice` en Python, `mt19937` en C++) et **re-seed** si vous écrivez un service de longue durée.

---

4.5 Comment cela gagne les intervieweurs

* **Showcases Data‐Structure Fusion** – Combiner le tableau et le hashmap est une caractéristique de l'ingénierie intelligente.
* **Illustrer la gestion des cas** – Des duplicata, des suppressions de valeurs manquantes et une logique de nettoyage témoignent de l'attention portée aux détails.
* ** Démontre la compétence linguistique** – Fournir des solutions Java, Python et C++ vous montre que vous êtes prêt pour n'importe quelle pile.
* **L'utilisation réelle du monde** – `RandomizedCollection` est essentiellement un *multiset* avec un échantillonnage aléatoire rapide – un modèle utilisé dans les caches, les balanceurs de charge et les moteurs de jeu.

---

4.6 Liste de contrôle rapide Avant l'entrevue

Objet
- Oui.
**Comprendre le problème** – les duplicatas sont autorisés. Autres
Autres **Connais les structures de données** – tableau dynamique + hashmap des ensembles d'index. Autres
**Planifier le delete** – échanger avec le dernier élément, mettre à jour les indices. Autres
**Write helper functions** – pour garder le code lisible. Autres
Autres **Testez attentivement** – insérez, supprimez, getRandom, cas de bord. Autres
** Expliquez votre design** – grand– O, pourquoi nous utilisons un ensemble, pourquoi il est temps constant. Autres
**Mention compromis** – mémoire au-dessus, pire cas potentiel, détails linguistiques. Autres

---

4.7 Mot final

LeetCode 381 peut sembler trompeurment simple, mais c'est un test *code-génération* de compréhension profonde.
Le **good** est l'élégance du motif tableau-hashmap.
Le **bad** est les bugs subtils qui se cachent dans la logique d'échange et de retrait.
Le **ugly** est le premier cas qui voyage même les programmeurs chevronnés.

Montrer une implémentation propre et bien commentée – comme nous l'avons fait ci-dessus – vous permettra d'entrer dans une salle de recruteur et de dire :
> Je peux construire un **multiset** qui se comporte comme un sac et toujours choisir un élément aléatoire en O(1) – le tout en Java, Python et C++. (en milliers de dollars)

Bonne chance ! C'est ce qu'il a dit.

---

> *Si vous avez trouvé cet article utile, donnez-lui un ", partagez-le sur LinkedIn, ou laissez un commentaire ci-dessous – laissez-nous aider la prochaine génération d'ingénieurs crack LeetCode 381 et atterrir leurs rôles de rêve. *

---

> *Copyright © 2023 - Tous droits réservés. *

---

Références et lectures supplémentaires

1. [LeetCode 381 – Insérer Supprimer GetRandom O(1) – Des duplicata autorisés](https://leetcode.com/problèmes/insert-delete-getrandom-o1-duplicata autorisés/)
2. [GeeksforGeeks – randomized Set & Multiset](https://www.geeksforgeeks.org/design-a-data-structure-that-supports-insert-delete-getrandom-in-constant-time/)
3. [InterviewBit – Constante Time Operations](https://www.interviewbit.com/question/insert-delete-get-random-o1/)

---

Bon codage ! C'est pas vrai