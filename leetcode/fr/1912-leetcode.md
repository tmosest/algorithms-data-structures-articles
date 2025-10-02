---
titre: LeetCode 1912. Design Movie Rental System - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

# Le bon, le mauvais et le mauvais – Résoudre le LeetCode 1912 (Design Movie Rental System)

**Mots clés**: LeetCode 1912, Design Movie Rental System, Java, Python, C++, interview, structures de données, TreeSet, HashMap, SortedSet, entretien d'emploi, algorithme, ingénieur logiciel

---

- Oui. 1. Récapitulation des problèmes

> *Vous dirigez une chaîne de magasins de cinéma `n`. Chaque boutique peut posséder ** au plus un exemplaire** d'un film.
> Pour un film donné, vous devez pouvoir :*
> * **recherche** – retourner les *boutiques 5* les moins chers qui possèdent actuellement une copie *non louée*
> * **rent** – marquer une copie spécifique telle que louée
> * **drop** – retourner une copie louée
> * **report** – retourner les *moins cher 5* exemplaires loués dans tout le système

Toutes les opérations doivent fonctionner assez rapidement pour pouvoir passer jusqu'à **100 000** appels.
Contraintes typiques: «1 ≤ n ≤ 3·105», «1 ≤ rubriques longueur ≤ 105», «1 ≤ prix ≤ 104».

---

- Oui. 2. Idée de haut niveau

**But** **Structure des données**
- Oui.
Trouver rapidement *pas cher 5 copies non louées* pour un film Trier par prix → magasin → film → nous pouvons prendre juste cinq
Trouver rapidement *pas cher 5 copies louées* dans tout le système.
Une recherche constante de l'élément *exact* dans une boutique.

Ainsi, nous maintenons **trois** structures de données:

1. **`shopMap`** – `Map<shop, Map<movie, Item>>` – pointeur rapide vers une copie particulière.
2. **`unrented`** – `Map<movie, TreeSet<Item>' – toutes les copies actuellement non locatives de ce film.
3. **`loué`** – `TreeSet<Item>` – toutes les copies louées triées par ordre de déclaration.

Toutes les opérations (`search`, `rent`, `drop`, `report`) deviennent `O(log k)` où `k` est la taille de l'ensemble pertinent (= 105).

Avec ces structures nous obtenons:

* **recherche** – il suffit d'itérer les 5 premiers éléments → `O(5 log k)` → essentiellement `O(1)`
* **rent / drop** – supprimer d'un ensemble, insérer dans l'autre → `O(log k)`
* **rapport** – itérer les 5 premiers éléments de l'ensemble mondial loué → `O(1)`

---

- Oui. 3. Conception détaillée

Article 3.1

Représentation linguistique Autres
- C'est pas vrai.
*Java*** Classe intérieure `Item` avec `shopId`, `movieId`, `prix`. Autres
**Python**= Simple dataclass / tuple `(prix, boutique, film)` – nous gardons le `shop` à l'intérieur pour la commande de rapport. Autres
**C++**="struct Item` avec `int shop, film, prix` et un comparateur personnalisé. Autres

Tous les trois utilisent le même ordre **** :
"prix" - "boutique" - "movie".
Cela garantit que le premier élément d'un `TreeSet`/`set` est toujours la *meilleure* copie pour `recherche` ou `rapport`.

3.2 Constructeurs

Pendant la construction nous insérons simplement chaque entrée dans:

* la carte locale de la boutique ('shopMap')
* le set de location global (`loué`) – *vide* au début
* l'ensemble non loué spécifique au film (`unrented.get(movie)`)

Aucune opération n'est `O(n log n)`; nous faisons `O(entries)` inserts, chaque coût au plus `O(log k)` parce que nous créons un nouveau `TreeSet` pour chaque nouveau film une seule fois.

---

- Oui. 4. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
**Constructeur** Autres
**Recherche** (seulement 5 tractions) Autres
**rent/drop** extra pour la recherche de cartes
**rapport** (cinq premiers de l'ensemble mondial) Autres

Toutes les limites sont confortablement inférieures aux 100 000 exigences d'exploitation.

---

- Oui. 5. Mise en œuvre

Vous trouverez ci-dessous une implémentation **prête à la copie** dans **Java**, **Python** et **C++**.
Tous les trois suivent la même logique, juste adaptée aux conteneurs idiomatiques de chaque langue.

> **Conseil pour les intervieweurs**:
> *Expliquez le *pourquoi* derrière chaque choix de structure de données – ils veulent vous voir comprendre les collections triées et les compromis. *

---

#### 5.1 Java (TreeSet + HashMap)

"Java
Importation de java.util.*;

classe publique MovieRentingSystem {
*** Une copie d'un film dans une boutique */
classe statique privée Article {
dernier atelier Id;
dernier film Int Id;
prix final int;

Item(int shopId, int filmId, int price) {
Ça. shopId = shopId;
Ça. film Id = film Id;
Ça. prix = prix;
}
}

// Comparateur utilisé pour les ensembles non loués et loués
Comparaison finale statique privée<Item> COMPARATEUR =
(a, b) -> Prix b. prix ? (a.prix, b.prix)
: a.shopId != b. boutique Id ? Integer.compare(a.shop) Id, b.shopId)
: entier.comparer(a.movie Id, b.movieId);

finale privée Carte<entier, Carte<entier, Item>> shopMap = nouveau HashMap<>();
carte finale privée<entier, TreeSet<Item>> non louée = nouvelle HashMap<>();
final privé TreeSet<Item> loué = nouveau TreeSet<>(COMPARATEUR);

public MovieRentingSystem(int n, int[][] entrées) {
pour (int[] e : rubriques) {
shop int = e[0], film = e[1], prix = e[2];
item = nouveau item (boutique, film, prix);

// 1. Cartographie→movie→ Point
shopMap.computeIfAbsent(shop, k -> new HashMap<>()).put(movie, item);

// 2. Set non loué pour ce film
unrented.computeIfAbsent(movie, k -> new TreeSet<>(COMPARATOR)).add(item);
}
}

*** Retournez les IDs de la boutique des 5 copies les moins chères du film donné. */
liste publique<integer> recherche(int film) {
TreeSet<Item> set = unrented.getOrDefault(film, nouveau TreeSet<>(COMPARATEUR));
Liste <entier> ans = nouvelle liste d'array<>(5);
i = 0;
pour (Item it : set) {
Si (i++) 5) pause;
le nom et l'adresse de l'utilisateur;
}
le retour des an;
}

*** Louez une copie d'une boutique spécifique. */
loyer public à vide (dans un magasin, dans un film) {
Item it = shopMap.get(shop).get(movie);
non located.get(movie).supprimer(it);
location.add(it);
}

/** Retourner une copie louée. */
public vide drop(boutique d'int, film int) {
Item it = shopMap.get(shop).get(movie);
location.supprimer(it);
non located.get(movie).add(it);
}

*** Retourner les moins chers 5 exemplaires loués (boutique, film). */
liste publique<Liste<entier>> rapport() {
Liste <Liste<Intégrée>> res = nouvelle liste <>(5);
i = 0;
pour (Item : loué) {
Si (i++) 5) pause;
res.add(Arrays.asList(it.shop) Id, it.movieId));
}
retour rés;
}
}
«» "

> **Pourquoi c'est rapide** – Toutes les opérations de mutation ne touchent que deux conteneurs triés, chaque insertion/suppression est `O(log k)`.

---

#### 5.2 Python (Liste d`envoi + `bisect`)

Python n'a pas de `TreeSet` intégré, mais la bibliothèque standard `bisect` nous permet de garder une *liste triée* qui se comporte comme un arbre équilibré pour nos contraintes.

'`python
bisect d'importation
de taper l'importation Liste

Catégorie:
__slots__ = ("shop", "movie", "prix")

def __init__(self, boutique: int, film: int, prix: int):
auto.shop = boutique
Self.movie = film
Autoprix = prix

# clé pour le tri : (prix, boutique, film)
def key(self):
retour (auto.prix, auto.shop, auto.movie)

def __lt__(self, autre: 'Item'):
retourner self.key() < other.key()


classe MovieRentingSystem:
def __init_(self, n: int, entrées: List[List[int]]):
# boutique → film → Point
auto.shop_map = {}

# film → trié la liste des éléments non loués
Self.unrented = {}

# liste globale triée des articles loués
auto-loué = []

pour boutique, film, prix dans les entrées:
il = Item(boutique, film, prix)

self.shop_map.setdefault(shop, {})[movie] = it

Si film pas en soi. non loué:
auto.non-loué[film] = []
# insérer tout en conservant la liste triée
bisect.insort_left(self.unrented[movie], it)

def search(self, film: int) -> Liste[int]:
lst = self.unrented.get(film, [])
retour [it.shop pour elle en lst[:5]]

def _remove_from_set(self, lst: List[Item], it: Item):
idx = bisect.bisect_left(lst, it)
# Nous faisons confiance au problème garantit que l'article existe
er.pop(idx)

def _add_to_set(self, lst: List[Item], it: Item):
bisect.insort_left(Ist, it)

def losing(self, boutique: int, film: int) -> Aucun:
il = auto.shop_map[shop][movie]
Self._retirez_de_set(self.unrented[movie], it)
Self._add_to_set(self.rented, it)

def drop(self, boutique: int, film: int) -> Aucun:
il = auto.shop_map[shop][movie]
Self._retirer_de_set(self.rented, it)
Self._add_to_set(self.unrented[movie], it)

def rapport(self) -> Liste[Liste[int]]:
retour [[it.shop, it.movie] pour elle en soi.loué[:5]]
«» "

*Pourquoi `bisect` fonctionne*:
La liste est toujours triée par `(prix, boutique, film)`. Insérer ou supprimer un seul élément coûte `O(log k)` plus un quart de liste (`O(k)`) – mais avec 105 éléments il est encore bien en dessous de la limite de 100 000-opérations.

---

### 5.3 C++ (std::set + unordered_map)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

élément de structure {
magasin, film, prix;
Item(int s, int m, int p) : magasin(s), film(m), prix(p) {}
// clé pour le tri: prix → boutique → film
opérateur de bool<(const item& other) const {
si (prix != autre.prix) prix de retour < autre.prix;
si (shop != other.shop) retour boutique < other.shop;
retour du film < other.movie;
}
};

classe MovieRentingSystem {
// shop -> (movie -> pointeur vers l'article)
non classé_map<int, non classé_map<int, Item*>> shopMap;
// film -> ensemble d'éléments non loués
non ordonné_map<int, set<Item*>> non loué;
// Ensemble global d'articles loués
set<Item*> loué;

public:
MovieRentingSystem(int n, vector<vector<int>& entrys) {
vecteur<Item*> tous lesItems;
tousItems.reserve(entries.size());

pour (auto& e : rubriques) {
shop int = e[0], film = e[1], prix = e[2];
allItems.push_back(nouveau) Item(boutique, film, prix)
item* it = allItems.back();

shopMap[shop][movie] = elle;
non loué[movie].insérer(it);
}
}

vector<int> search(int movie) {
vecteur<int> rés;
auto it = unrented.find(movie);
si (it == unrented.end() renvoie res;
cnt = 0;
pour (Item* ip : it->seconde) {
si (cnt++) 5) pause;
res.push_back(ip->shop);
}
retour rés;
}

location vide (dans un magasin, dans un film) {
Item* ip = shopMap[shop][movie];
non locative[movie].erase(ip);
location.insert(ip);
}

vide drop(boutique d'int, film int) {
Item* ip = shopMap[shop][movie];
location.erase(ip);
non loué[movie].insérer(ip);
}

Rapport du vecteur<vector<int>> {
vecteur<vecteur<int>> rés;
cnt = 0;
pour (poste* ip : loué) {
si (cnt++) 5) pause;
res.push_back({ip->shop, ip->movie});
}
retour rés;
}
};
«» "

> ** Nettoyage de mémoire** – Pour la brièveté, le destructeur ne libère pas `Item*`. Dans un vrai entretien, vous l'avez mentionné ou utilisez `unique_ptr`.

---

- Oui. 6. Ce qui ne va pas? – Pièges communs

1. **Choisir le mauvais conteneur trié**
*Solution*: Utilisez `TreeSet`/`set` pour continuer à commander; évitez les solutions hash-only parce que vous perdez la récupération d'élément de meilleur.

2. **Ne pas partager le comparateur**
*Résultat*: `recherche` et `rapport` donneraient des éléments différents.
*Fix*: Conservez un seul comparateur pour tous les ensembles triés.

3. **Storing seulement le prix dans l'ensemble loué mondial**
*Problème*: Le rapport nécessite aussi l'identification du magasin.
*Fix*: Inclure `shop` dans l'élément ou dans la touche.

4. **Copier des objets au lieu de stocker des pointeurs**
*Effet* : Chaque opération mutante créerait de nouveaux objets → mémoire inutile et recherche plus lente.
*Solution*: Entreposez des pointeurs ou des références à la même instance `Item` dans tous les ensembles.

---

- Oui. 7. A emporter

- **Des collections ordonnées** (TreeSet/TreeSet/TreeSet) vous permettent d'extraire *constante-time* des meilleurs éléments.
- **Hash maps** vous donne *O(1)* boutique → film → copie recherche.
- Oui. La combinaison résout à la fois *recherche* et *rapport* en O(1) tout en conservant les mises à jour bon marché.

> **Rappelez-vous**: L'entrevue n'est pas seulement sur l'écriture de code; il s'agit de démontrer *pourquoi* vos choix de structure de données rendent la solution efficace.

Bon codage et bonne chance pour votre prochaine interview!

---