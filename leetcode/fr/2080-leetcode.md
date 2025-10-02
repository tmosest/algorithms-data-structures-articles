---
titre: LeetCode 2080. Demandes de renseignements sur la fréquence des intervalles -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Questions sur la fréquence de la gamme (LeetCode 2080) – Java, Python & C++ Solutions + un article de blog SEO-Ready

> **TL;DR**
> • **Problème**: Trouver combien de fois une valeur apparaît dans un sous-réseau.
> • **Idée de base**: Stockez les positions de chaque nombre dans une liste *triée* → recherche binaire pour la gamme.
> • **Complexités**: prétraitement `O(n)`, `O(log n)` par requête, `O(n)` mémoire.
> • **Pourquoi c'est génial pour les entrevues**: Structure de données simple, raisonnement clair, et vous pouvez parler de compromis (hash-map + recherche binaire vs segment tree vs. Algorithme Mo).

---

- Oui. 1. Déclaration de problème (Code de bord 2080)

> **Design** une classe `RangeFreqQuery` qui supporte:
> - `RangeFreqQuery(int[] arr)` – constructeur.
> - `int requête(int gauche, int droite, int valeur)` – retourner la fréquence de `valeur` dans le sous-array `arr[gauche ... droite]`.

Contraintes
«» "
1 ≤ longueur d'arrondi ≤ 1e5
1 ≤ arr[i], valeur ≤ 1e4
0 ≤ gauche ≤ droite < arr.longueur
≤ 1e5 requêtes
«» "

---

- Oui. 2. Aperçu de base – *Tableaux des indices*

Depuis `arr[i]` ≤ `10^4`, nous pouvons pré-allouer un tableau de taille `10001`.
Pour chaque valeur possible `v` nous stockons la liste **triée des indices** où `v` se produit.

«» "
indices[v] = [i0, i1, i2, ...] (augmentation stricte)
«» "

Pourquoi ? *
Parce que nous allons effectuer une recherche binaire sur ces listes pendant les requêtes.
Le tri est inhérent parce que nous ajoutons des indices en ordre ascendant pendant la construction.

**Algorithme de requête**

1. `l = lower_bound(indices[valeur], gauche)` – premier indice ≥ `gauche`.
2. `r = upper_bound(indices[valeur], droite) ' – premier indice > "droite".
3. Résultat = `r - l`.

Les deux étapes sont `O(log k)` où `k` est le nombre d'occurrences de `valeur`.
Dans le pire des cas, `k = n`, mais toujours `O(log n)`.

---

- Oui. 3. Mise en œuvre dans trois langues

Ci-dessous sont prêts à compiler des extraits.
N'hésitez pas à copier-coller dans votre aire de jeux IDE ou LeetCode.

---

#### 3.1 Java

"Java
Importation de java.util.*;

classe publique RangeFreqQuery {
// indices[v] détient toutes les positions où arr[i] == v
Liste finale privée<entier>[] les indices;

@SuppressAvertissements("non vérifié")
public RangeFreqQuery(int[] arr) {
indices = nouvelle grille[10001]; // 0 ... 10000
pour (int v = 0; v < indices.longueur; v++) {
indices[v] = nouvelle liste de répartition<>();
}
pour (int i = 0; i < arr.longueur; i++) {
les indices [arr[i]].add(i);
}
}

public int requête(int gauche, int droite, int valeur) {
Liste <entier> liste = indices[valeur];
si (list.isEmpty()) retourne 0;

int l = lowerBound (liste, gauche); // premier >= gauche
int r = upperBound (liste, droite); // premier > droit
retour r - l;
}

// aide à la recherche binaire
int statique privé lowerBound(Liste<Intégrer> liste, int cible) {
int lo = 0, hi = list.size();
pendant qu ' il y a (l < bonjour) {
Int milieu = (lo + hi) >>> 1;
si (list.get(mid) < cible) lo = milieu + 1;
Autre salut = milieu;
}
retour lo;
}

Int statique privé upperBound(Liste <Integer> liste, int cible) {
int lo = 0, hi = list.size();
pendant qu ' il y a (l < bonjour) {
Int milieu = (lo + hi) >>> 1;
si (list.get(mid) <= cible) lo = milieu + 1;
Autre salut = milieu;
}
retour lo;
}
}
«» "

**Points clés* *

* Utilise `ArrayList` – pas de copie supplémentaire pendant la construction.
* `@SuppressAvertissements("non vérifié")` est sûr parce que nous connaissons la taille.
* `lowerBound` / `upperBound` sont les helpers classiques de style C++.

---

3.2 Python

'`python
bisect d'importation
de taper l'importation Liste

classe RangeFreqQuery:
def __init_(self, arr: List[int]):
# indices[v] = liste triée des postes
auto.indices = [[] pour _ dans l'intervalle(10001)]
pour i, v in énumérate(arr):
auto.indices[v].append(i)

def request(self, gauche: int, droite: int, valeur: int) -> Int:
lst = indice de soi[valeur]
si non:
retour 0
l = bisect.bisect_left(lst, left) # first >= gauche
r = bisect.bisect_right(lst, right) # first > right
retour r - l
«» "

*Python="s `bisect`* est déjà une implémentation rapide C, donc vous n'avez pas besoin d'écrire votre propre recherche binaire.

---

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe RangeFreqQuery {
particulier:
Vector<vector<int>> indices; // indices[v] = liste des positions

public:
RangeFreqQuery(vecteur<int> &arr) {
les indices.assigner(10001, {});
pour (int i = 0; i < arr.size(); ++i) {
indices[arr[i]].push_back(i); // les indices sont annexés dans l'ordre
}
}

int requête(int gauche, int droite, int valeur) {
Const vector<int> &vec = indices[valeur];
si (vec.vide()) retourne 0;

auto l = lower_bound(vec.begin(), vec.end(), gauche);
auto r = upper_bound(vec.begin(), vec.end(), droite);
retour r - l;
}
};
«» "

Le code C++ utilise la même logique que Java.

---

- Oui. 4. Analyse de la complexité

Étape Temps Mémoire
C'est pas vrai.
**Préprocessure**="O(n)" – chaque élément est poussé une fois dans son seau. "O(n)" – longueur totale de tous les seaux égale `n`. Autres
**Requête unique**"O(log k)" ≤ "O(log n)"" "O(1)" par requête (à l'exception de la recherche du seau). Autres
**Le cas le plus grave** Total général

*Pourquoi `k ≤ n`? *
Si tous les éléments sont les mêmes (`valeur` = 1), le seau correspondant a la taille `n`.
La recherche binaire sur les éléments `n` est toujours logarithmique.

---

- Oui. 5. Solutions de rechange – Quand choisir

Une approche pour les avantages pour les consommateurs
C'est ce qu'on dit.
**Array des indices + recherche binaire** (notre solution) <br>• Très facile à expliquer. <br>• Pas de plaque de chaudière lourde pour la structure des données. <br>• Si `arr[i]` peut être grand ( > 1e5), nous ne pouvons pas pré-allouer un seau par valeur. Questions d'entrevue où les contraintes permettent un petit domaine. Autres
**L'algorithme de Mo's** (requêtes hors ligne) • O(n + q) √n) – bon lorsque les requêtes sont connues au préalable. <br>• Pas "online". Problèmes d'entrevues ou rondes d'entrevues hors ligne. Autres
Autres **Segment Tree / BIT de HashMaps**. • Log-time requête pour *any* valeur, pas seulement petit domaine. <br>• La complexité de la mise en œuvre est élevée. Autres
**Arbre de baguettes**** • Poignées de grandes valeurs `arr[i]`. Un entretien avancé ou une piste de structures de données. Autres

> **Good**: La méthode index-bucket est parfaite pour les requêtes *online* et les petits domaines.
> **Bad**: Il est gaspillé si la plage de valeur était énorme ('1e9').
> **Ugly**: Si vous ne manipulez pas les seaux vides correctement, vous obtiendrez de mauvaises réponses ou `IndexOutOfBoundsException`.

---

- Oui. 6. Bon, mauvais et ugly – Une lentille d'entretien

Stade Bonne Mauvais Ugly
- C'est quoi ?
**Concept**=Intuition d'une recherche dans une liste de positions=– très explicable.= None=Si vous choisissez un arbre *segment* ou un algorithme *Mo=s* sans tout d'abord expliquer la gamme plus simple d'indices, les intervieweurs penseront que vous êtes sur-enginé. Autres
**Prétraitement**= O(n) temps; juste un seul passage. Aucun. Autres
**Query**= O(log n) par requête; utilise la recherche binaire standard. Aucun. Autres
**Mémoire**= O(n) total, bien dans les limites. En stockant l'ensemble du tableau dans un `HashMap<entier, entier>` pour chaque valeur (taille 1e4) va souffler la mémoire – **éviter** cela. Autres
**Tests**= Tests d'unité faciles à écrire – il suffit de forcer un tableau aléatoire. Aucun. Autres

---

- Oui. 7. FAQ – Pièges et Gotchas communs

Question Réponse
C'est pas vrai.
Autres **Et si la valeur est 0?** Les contraintes de problème disent `arr[i]` ≥ 1, mais vous pouvez toujours soutenir 0 en allouant `size 10001`. Attention à ce que votre seau soit assez grand. Autres
**Est-ce que `upperBound` retournera jamais `-1`?** Si tous les éléments sont ≤ `right`, il retourne `list.size()`. Autres
Autres **Pourquoi ne pas utiliser `Collections.binarySearch`? Il retourne l'index * de l'élément exact* ou `-(insertionPoint) - 1`. Convertir cela en `lowerBound` / `upperBound` est plus susceptible d'erreur que d'écrire les deux petits assistants. Autres
Autres **Comment m'adapter si `arr[i]` peut être de 10^9?**.Utilisez un `HashMap<entier, liste<entier>>` au lieu d'un éventail de listes; l'approche reste la même. Autres

---

- Oui. 8. Conseils d'entrevue prêts

1. **Commencez avec la solution la plus simple** – expliquez les jeux d'indices ; demandez ensuite si l'intervieweur aimerait une approche plus sophistiquée (arbre de segment, algorithme de Mo...).
2. **Parler des compromis** – mentionner que l'approche du seau est linéaire mais rapide, alors qu'un arbre de segment utilise plus de mémoire mais fonctionne pour toute valeur `arr[i]`.
3. **Afficher votre style de codage** – utilisez le nom approprié (`indices`, `lowerBound`, `upperBound`) et commentez votre code.
4. **Cas de bord de Mention** – godet vide, valeur non présente, gauche > droite (ne devrait pas se produire par contraintes mais encore vérifier).
5. **Fournir des tests unitaires** – écrire une petite fonction principale ou une méthode `@Test` qui affirme des sorties connues.
6. **Show familiarité with C++ STL and Python bisect** – de nombreux intervieweurs aiment vous voir connaître des idiomes spécifiques à la langue.

---

- Oui. 9. Mise en forme et fin Pensées

* La solution de la liste des indices est ** la réponse canonique** pour LeetCode 2080.
* Il fonctionne dans `O(n)` temps de prétraitement, `O(log n)` par requête, et `O(n)` mémoire - parfait pour les contraintes données.
* Si vous vous préparez à une interview de codage **** ou à un emploi de structure de données ****, vous pouvez parler avec confiance de cette solution, de ses forces et de la raison pour laquelle vous l'avez choisi sur un arbre de segment à moins que l'entrevue ne l'exige explicitement.

Bon codage, et que votre prochaine interview soit aussi lisse qu'une recherche binaire sur une liste triée! Les

---

*Mots clés pour le référencement*: **Range Frequency Queries LeetCode 2080, RangeFreqQuery implementation, solution Java Python C++, structure de données d'entrevue, codage d'entrevue d'emploi, recherche binaire, tableaux d'indices, segment arborescence alternative**.