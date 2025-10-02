---
titre: LeetCode 436. Trouver l'intervalle droit -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Leetcode 436 – **Trouver l'intervalle droit**
*Des solutions faciles à comprendre au code d'entrevue prêt à travailler (Java / Python / C++). *

---

## TL;DR – La solution d'une ligne

Texte
Intervalle droit = premier début ≥ interval.end (trié par début)
«» "

* Trier les intervalles par leurs valeurs de «démarrage» (conservation des indices originaux).
* Pour chaque intervalle exécuter une recherche binaire sur le trié commence à localiser le
le plus petit démarrage qui est ≥ l'intervalle courant "end".
* Si elle est trouvée, retournez cet intervalle avec l'index original; sinon retournez `-1`.

Complexité : **O(n log n)** temps, **O(n)** espace supplémentaire.

---

- Oui. Pourquoi ce problème est-il une mine d'or d'emploi

* ** Concepts de base testés** : tri, recherche binaire, cartes de hachage, pointeurs.
* **Langues**: Java, Python, C++ – les langues d'entretien les plus courantes.
* **Variants**: La même logique s'applique à l'élément suivant:
Recherche dans le tri rotatif Array, etc.
* **Points de discussion** :
* Expliquez pourquoi le tri est nécessaire.
* Discutez de l'utilisation de `Map` / `unordered_map` pour préserver les indices originaux.
* Parler de cas de bord (pas d'intervalle correct, valeurs négatives).
* Optimiser pour le temps par rapport à l'espace.

Si vous pouvez expliquer cette solution proprement dans **moins de 5 minutes** vous gagnerez beaucoup d'intervieweurs.

---

- Oui. 1. Récapitulation des problèmes (code de bord 436)

Avec un tableau `intervalles` où chaque élément est `[départ, fin]` et chaque `départ`
est unique, pour chaque intervalle trouver l'index de l'intervalle *droit*:

* Un intervalle correct `j` satisfait `start[j] ≥ end[i]`.
* Parmi tous ces intervalles, choisissez celui avec la valeur de départ **minimum**.
* Si aucune n'existe, retourner `-1`.

Retourner un tableau d'indices d'intervalle de droite pour chaque intervalle dans l'ordre
D'abord donné.

**Contrôles* *

Paramètre Taille Valeur
C'est quoi ?
"Intervalles.longueur"
"Intervalles[i].longueur"
- 106 ≤ début ≤ fin ≤ 106
Les valeurs `start` sont uniques

---

- Oui. 2. L'idée de recherche de l'avidité + binaire

1. **Garder les indices originaux** – créer une liste de paires `(start, originalIndex)`.
2. **Trier par Start** – maintenant nous pouvons binaire-recherche sur `start`.
3. **Binary Search** – pour chaque intervalle, trouvez la limite inférieure* dans le
trié comme début: le premier début qui est ≥ `end`.
4. **Réponse** – si un tel démarrage existe, son index original stocké est la réponse;
sinon "-1".

Pourquoi ça marche :
Tous les démarrages sont uniques → l'ordre trié est strict, donc la limite inférieure est
Bien défini. Parce que nous avons trié une fois, chaque recherche est `O(log n)`.

---

- Oui. 3. Faits saillants de la mise en œuvre

Langue
C'est pas vrai.
*Java** *Arrays.binarySearch *, carte <entier,entier> *, *Arrays.sort *
*Python */ "bisect_left", "sorted" et "dict"
**C++**="bound_lower", `vector<pair<int,int>>, `unordered_map`="

Toutes les solutions sont **itatives** (pas de récursion) et évitent les opérations coûteuses
dans la boucle.

---

- Oui. 4. Code (Java, Python, C++)

### 4.1 Java – Nettoyer, interviewer Prêt

"Java
Importation de java.util.*;

solution de classe publique {
public int[] findRightInterval(int[][] intervalles) {
int n = intervalles de longueur;
réponse int[] = nouvelle réponse int[n];

// (démarrage, indice original)
int[]] startIdx = nouveau int[n][2];
pour (int i = 0; i < n; i++) {
startIdx[i][0] = intervalles[i][0];
= i;
}
// trier par valeur de départ
les tableaux.sort(startIdx, Comparator.comparingInt(a -> a[0]);

// extrait trié commence pour la recherche binaire
int[] starts = nouveau int[n];
pour (int i = 0; i < n; i++) starts[i] = startIdx[i][0];

pour (int i = 0; i < n; i++) {
int end = intervalles[i][1];
int pos = lowerBound (démarrages, fin); // personnalisé lié inférieur
réponse[i] = (pos < n) ? startIdx[pos][1] : -1;
}
réponse de retour;
}

// Recherche binaire standard pour la liaison inférieure
Int privé lowerBound(int[] arr, int cible) {
int lo = 0, hi = arr.longueur;
pendant qu ' il y a (l < bonjour) {
Int milieu = (lo + hi) >>> 1;
si (arr[mid] < cible) lo = milieu + 1;
Autre salut = milieu;
}
retour lo;
}
}
«» "

> **Pourquoi pas `Arrays.binarySearch`?**
> `Arrays.binarySearch` retourne un index seulement lorsque la clé est présente; sinon
> il retourne un point d'insertion négatif. "lowerBound" est plus clair et évite
> double négation.

---

4.2 Python – Élégant et lisible

'`python
de bisect importer bisect_left
de taper l'importation Liste

Solution de classe:
def findRightInterval(self, intervalles: List[List[int]]) -> Liste[int]:
# (démarrage, index_original) trié par début
début = trié((interval[0], idx) pour idx, intervalle dans le dénombrement(intervals))
trié_démarrages = [s pour s, _ en démarrage]

res = []
pour la fin (intervalle[1] pour les intervalles):
pos = bisect_left(sorted_starts, fin)
res.append(starts[pos][1] si pos < len(starts) autre -1)
retour res
«» "

---

### 4.3 C++ – Haute performance et classique

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
std::vector<int> findRightInterval(std::vector<std::vector<int>&intervals) {
int n = intervalles.size();
std::vector<std::pair<int, int>> startIdx(n); // (démarrage, idx original)

pour (int i = 0; i < n; ++i) {
startIdx[i] = {intervalles[i][0], i};
}

à:sort(startIdx.begin(), startIdx.end(),
[](const auto& a, const auto& b) { retourner a.first < b.first; });

std::vector<int> starts(n);
pour (int i = 0; i < n; ++i) commence[i] = startIdx[i].première;

à:vecteur<int> ans(n);
pour (int i = 0; i < n; ++i) {
int end = intervalles[i][1];
auto it = std::lower_bound(starts.begin(), starts.end(), fin);
ans[i] = (it != starts.end()) ? startIdx[it - starts.begin()].seconde : -1;
}
le retour des an;
}
};
«» "

> **Pourquoi utiliser `std::lower_bound`?**
> Il implémente directement la recherche binaire pour le premier élément ≥ `cible`
> – exactement ce dont nous avons besoin.

---

- Oui. 5. Le Bon, le Mauvais, le Méchant

Aspect du bien
- C'est quoi ?
**Complexité du temps**=Le `O(n log n)` est optimal pour les données non triées. Aucun – l'algorithme est déjà optimal. Aucun.
Autres **Complexité de l'espace** Frais généraux supplémentaires de stockage des indices, mais inévitables.
**Code Simplicité** Nécessite une compréhension de la limite inférieure. Si vous essayez d'utiliser des tas ou un truc à deux points, ça devient désordonné. Autres
**Cas d'escroquerie** Il faut se rappeler d'utiliser 64 bits si la plage > `int`. Autres
**Pièges spécifiques à la langue**=Java: valeurs négatives `Arrays.binarySearch`. Python: `bisect_left` vs `bisect_right`. Autres

**Bottom Ligne :** S'en tenir au modèle **trié + recherche binaire**. Il est propre, rapide et couvre tous les cas de bord.

---

- Oui. 6. Article de blog optimisé par le SEO

Titre
**Leetcode 436 – Trouver le bon Intervalle: Java / Python / C++ Solutions et guide d'entrevue**

Description de la méta
Maître Leetcode 436 Trouver l'intervalle droit avec des solutions étape par étape en Java, Python et C++. Apprenez l'algorithme optimal, les compromis et les explications prêtes à l'entrevue pour stimuler votre préparation d'entrevue de codage.

---

C'est pas vrai. Qu'est-ce que Trouver l'intervalle droit?

Leetcodes **436** vous demande de trouver, pour chaque intervalle, le plus petit intervalle dont le début est au moins l'intervalle courant. Il s'agit d'un problème classique de recherche de la prochaine plus grande valeur, mais avec des intervalles.

---

- Oui. Pourquoi devriez - vous vous en soucier?

* **Interview or:** Tri + recherche binaire montre que vous connaissez les fondamentaux de la structure des données.
* **Job-ready:** Les entreprises comme Google, Amazon et Stripe demandent des variations de ceci.
* **Langage brut:** La logique est identique en Java, Python et C++ – parfait pour les portfolios multilingues.

---

C'est vrai. La solution optimale en coque

1. **Conserver les indices** – stocker les paires `(start, originalIndex)`.
2. **Trier au début** – une passe O(n log n).
3. **Recherche binaire** – pour chaque « fin », trouvez la limite inférieure dans les départs triés.
4. **Indice de retour** – si trouvé, utiliser l'index original stocké; sinon `-1`.

---

#####=4=1 Étape par étape (Python)

'`python
de bisect importer bisect_left

def findRightInterval(intervalles):
début = trié(s, i) pour i, (s, _) dans le dénombrement(intervalles)
trié_démarrages = [s pour s, _ en démarrage]
résultat = []

pour _, e à intervalles :
pos = bisect_left(sorted_starts, e)
result.append(starts[pos][1] if pos < len(starts) other -1)
résultat du retour
«» "

*Heure*: `O(n log n) "
*Espace*: "O(n)"

---

Code C++ et Java (même idée)

* **C++** – utilise `std::lower_bound`.
* **Java** – utilise la coutume `lowerBound` pour éviter toute confusion avec `Arrays.binarySearch`.

Les deux sont de moins de 40 lignes, entièrement compilables et prêtes pour Leetcode.

---

#### 6=2 Points d'entrevue

1. **Pourquoi trier?**
*Nous devons rapidement trouver le prochain départ ≥ fin. Le tri transforme le problème en une recherche binaire. *

2. **Pourquoi la recherche binaire? **
*Nous sommes à la recherche du début de qualification *le plus petit*; la limite inférieure le donne dans `O(log n)`. *

3. **Échanges spatiaux* *
*Nous stockons un tableau auxiliaire de starts + indices. Espace encore linéaire, mais beaucoup moins cher qu'une solution de tas. *

4. **Juge**
*Pas de bon intervalle → retour `-1`.
*Les valeurs de démarrage negatives et les grandes plages → utilisent `int` (la plage ±106 convient confortablement). *

5. ** Solutions alternatives**
*TreeMap (Java) / std::map (C++) – O(n log n) mais facteur constant plus élevé.
*PriorityQuue approche – O(n2) pire cas. *

---

Référence rapide

Langue Fonctions clés Complexité
- C'est quoi ?
**Java**="Arrays.sort`, personnalisé `lowerBound`="O(n log n)` Autres
**Python**= `bisect_left`, `sorted`== `O(n log n)` Autres
**C++**="std::sort`, `std::lower_bound`=" `O(n log n)` Autres

---

- Oui. A emporter

Le problème "Find Right Interval" est une vitrine parfaite de *sorting + recherche binaire*.
Maîtriser cette solution démontre aux recruteurs que vous pouvez :

* Réduire une recherche apparemment complexe à un modèle algorithmique standard.
* Écrire un code propre et translinguistique.
* Parlez avec confiance des compromis temps/espace.

Bon codage, et bonne chance avec votre prochaine interview! C'est ce qu'il a dit.

---

Ressources en bonus

Sujet Ressources
C'est pas vrai.
(https://www.geeksforgeeks.org/binary-search/) Autres
LeetCode Explore, Cracking the Coding Interview
Portefeuille vitrine de GitHub repos avec tags de langue, Leetcode soumission stats

---

Réflexions finales

Maintenant que vous avez:

* ** Trois solutions complètes** (Java, Python, C++).
* A ** justification algorithmique claire**.
* Un article de blog prêt à paraître** pour présenter votre CV.

Vous êtes prêt à transformer Leetcode 436 en une victoire de portefeuille et sécuriser cet appel d'entrevue de codage convoité. Continuez à pratiquer et à explorer les variations – le prochain défi est juste au coin de la rue! C'est ce qu'il a dit.

---

*© 2024 Votre voyage de codage. *

---

Nombre de mots
900 mots (prêts pour le référencement, concis et facile à écumer).