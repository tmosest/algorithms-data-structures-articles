---
titre: LeetCode 1943. Décrivez la peinture -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Récapitulation des problèmes – LeetCode 1943

> **Objectif** – Convertir un ensemble de segments colorés, recoupant des segments semi-fermés sur une ligne numérique en un ensemble minimum de segments semi-fermés qui décrivent correctement chaque *couleur mixte* sur la ligne.
> **Output** – Pour chaque nouveau segment `[l, r)` nous sortons le *sum* de toutes les couleurs qui sont présentes dans cet intervalle (la couleur mixte est un ensemble de couleurs distinctes, mais nous ne retournons que la somme).

---

- Oui. Pourquoi c'est un problème d'interview classique

* **Line Sweep** – la technique canonique pour traiter les intervalles qui changent aux paramètres.
* **Structures de données** – arbres de recherche binaire équilibrés (`TreeMap`/`std::map`) ou tableaux de différences*.
* **Cas d'Edge** – manipulation des trous (pièces non peintes) et des plages de chevauchement qui ont la même somme mais des couleurs différentes.
* **Complexité** – `O(n log n)` (map) ou `O(n + maxCoord)` (array) – toutes deux acceptables pour les contraintes.

---

Solution Idée – Balayer la ligne avec une carte de différence

1. **Collectez toutes les coordonnées de l'intérêt** – chaque point de départ ou de fin d'un segment.
2. **Store le delta de la somme des couleurs à chaque point* *
* Ajouter `color` au début d'un segment.
* Soustraire `color` à la fin d'un segment.
3. **Trier les coordonnées** (ou utiliser une carte triée) et itérer dans l'ordre.
4. Maintenir un courant Somme.
5. Chaque fois que `currentSum > 0` et la prochaine coordonnée diffèrent de la précédente, émettre un segment `[prevCoord, currCoord)` avec la somme courante.
6. Passer les intervalles où `currentSum == 0' – ils sont non peints.

Parce que chaque couleur de l'entrée est *unique*, l'ensemble des couleurs actives change chaque fois que la somme change. Par conséquent, une somme numérique pure suffit pour la sortie.

---

Code

Voici des solutions propres et idiomatiques dans **Java, Python et C++**.
Chaque solution utilise le même algorithme; seuls les détails de la structure des données diffèrent.

---

- Oui. Java (Mise en œuvre rapide basée sur un tableau)

"Java
Importation de java.util.*;

solution de classe publique {
Liste publique<Liste<Long>> fractionnéPeinture(int[][] segments) {
// Résultat maximal ≤ 1e5 + 1 (fin de demi-fermeture)
MAX = 100001;
long[] diff = nouveau long[MAX + 2]; // diff[i] = changement de somme à i
Booléen[] isEndpoint = nouveau booléen[MAX + 2];

// Créer un tableau de différences
pour (int[] seg : segments) {
début int = seg[0], fin = seg[1];
couleur longue = seg[2];
diff[démarrer] += couleur;
diff[end] -= couleur;
isEndpoint[start] = true;
isEndpoint[end] = true;
}

Liste <Liste<Long>> résultat = nouvelle liste <>();
courant long = 0; // somme courante
int prev = 0; // coordonnées antérieures

pour (int i = 1; i <= MAX + 1; i++) {
si (isEndpoint[i] && à jour > 0) {
// Intervalle de peinture [prev, i) avec la somme actuelle
result.add(Arrays.asList((long)prev, (long)i, courant));
}
prev = isEndpoint[i] ? i : prev; // saut uniquement sur les paramètres
courant += diff[i];
}
le résultat du retour;
}
}
«» "

**Complexité* *

Étape Temps Espace
C'est pas vrai.
Bâtiment diff. Autres
Tableau de numérisation
Total "O(n + maxCoord)" " Autres

---

### Python (utilisation de "conteneurs triés" ou de "dicte" intégré)

'`python
de taper l'importation Liste
de collections importer par défautdict

Solution de classe:
def splitpeinting(self, segments: List[List[int]]) -> Liste[Liste[int]]:
diff = defaultdict(int)
fin = set() # coordonnées qui sont des paramètres réels

# Construire la carte des différences
pour s, e, c en segments:
Diff[s] += c
Diff[e] -= c
fin.add(s)
fin.add(e)

# Liste triée de toutes les coordonnées intéressantes
Coords = triés(fins)

res = []
courant = 0
prev = coords[0] # premier paramètre

pour i dans la plage (1, len(coords)):
curr = coords[i]
courant += diff[prev]
si courant > 0:
res.append([prev, curr, current])
prev = curr

retour res
«» "

> **Astuce** – Si vous préférez les inserts/lookups O(log n), utilisez des conteneurs triés. TriéDict` (pip install).
> Le code ci-dessus fonctionne dans `O(n log n)` en raison du tri de l'ensemble de paramètres (`n ≤ 2·104`).

---

C++ (Tableau rapide + `vecteur`)

'`cpp
#incluez <vecteur>
#incluez <algorithme>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle<vector<long>> splitPaintage(vecteur<vector<int>& segments) {
const int MAX = 100001; // coordonnées maximales + 1
vecteur <long> diff(MAX + 2, 0);
vecteur<char> isEnd(MAX + 2, 0);

pour (auto &seg : segments) {
int s = seg[0], e = seg[1];
long c = seg[2];
Diff[s] += c);
diff[e] -= c;
isEnd[s] = isEnd[e] = 1;
}

vecteur<vecteur<long>> rés;
longue courbure = 0;
int prev = 0;

pour (int i = 1; i <= MAX + 1; ++i) {
si (isEnd[i] && cur > 0) {
res.push_back({prev, i, cur});
}
prev = isEnd[i] ? i : prev;
cur += diff[i];
}
retour rés;
}
};
«» "

**Pourquoi `vecteur<char>` pour `isEnd`?* *
`bool` peut avoir des frais généraux définis. Un «char» est un octet et suffit pour indiquer si une coordonnée est un véritable paramètre.

---

Blog détaillé – Décrivez la peinture dans le style d'une interview technique Blog

---

# Comment Master LeetCode 1943 – Description de la peinture

> **Mots clés:** LeetCode 1943, Décrivez la peinture, balayage de ligne, solution Java, solution Python, solution C++, interview algorithmique, interview de codage, entretien d'emploi, structures de données, BST équilibrée, tableau de différence.

---

Table des matières

1. Déclaration de problème
2. Principales observations
3. Algorithme – Balayage de ligne et différence Carte
4. Trois mises en œuvre propres
5. Pièges communs
6. Qu'insister dans une entrevue
7. Comment présenter votre solution dans un portefeuille
8. Pourquoi ce problème t'amène au boulot
9. Autres lectures et ressources

---

- Oui. 1. Exposé des problèmes (Récapitulation)

Vous êtes donné un tableau `segments`, chaque élément `[départ, fin, couleur]`.
Toutes les valeurs `color` sont uniques.
La tâche : produire l'ensemble *minimum* de segments semi-fermés qui décrivent correctement les couleurs mélangées sur la ligne.
Extraire une liste de `[gauche, droite, sum_of_colors]` pour chaque intervalle peint.
Intervalles sans couleur (`sum == 0') doit être omis.

Contraintes: `1 ≤ n ≤ 20000`, `1 ≤ début < fin ≤ 100000`, toutes les couleurs ≤ `109`.

---

- Oui. 2. Principales observations

Observation Pourquoi ça compte
C'est pas vrai.
**Modification du point d'arrivée**=Un segment commence ou se termine uniquement aux coordonnées entières. Autres
**Couleurs uniques**Le jeu de couleurs actives change si la somme numérique change. Autres
**Half-fermé**="end" est *not* une partie du segment, donc nous pouvons utiliser un tableau de différence sans erreurs off-by-one. Autres
Autres **Pas de trous peints**. Autres
**Désorption requise**=Nous avons besoin des coordonnées en ordre ascendant pour effectuer un balayage. Autres

---

- Oui. 3. Algorithme – Balayage de ligne avec une carte de différence

1. **Créer une carte delta**
* Pour chaque segment `[s, e, c]`: `delta[s] += c`, `delta[e] -= c`.
* Conservez à la fois `s` et `e` dans un ensemble 'endpoints'.
2. **Trier `endpoints`** – cela nous donne l'ordre de balai.
3. **Traverse**
* Gardez `curSum = 0`, `prev = first_endpoint`.
* Pour chaque coordonnée `x` dans l'ordre trié:
* `curSum += delta[prev]`.
* Si `curSum > 0`, sortie `[prev, x, curSum]`.
* "prev = x".
4. Retourne la liste.

Parce que la somme est strictement positive pour tout intervalle peint, nous pouvons sauter des gammes non peintes et nous n'avons pas besoin de reconstruire le *set* de couleurs.

---

- Oui. 4. Trois mises en œuvre propres

> **Conseil** – La logique de base est identique; seul le choix de la structure des données diffère.

Langue de préférence Structure des données Autres
Il y a un problème.
Autres Tableau Java (`diff`) + tableau booléen (`isEndpoint`) Autres
Python : `defaultdict` + `set` (trié plus tard) Autres
* C++ *vecteur <long> + *vecteur <char> * * O(n + maxCoord) * * O(maxCoord) * Autres

---

### Java – Array basé (le plus performant)

"Java
Importation de java.util.*;

solution de classe publique {
Liste publique<Liste<Long>> fractionnéPeinture(int[][] segments) {
Int final MAX = 100001; // 1e5 + 1 est sûr
long[] diff = nouveau long[MAX + 2];
Booléen[] isEnd = nouveau booléen[MAX + 2];

pour (int[] seg : segments) {
int s = seg[0], e = seg[1];
long c = seg[2];
Diff[s] += c);
diff[e] -= c;
isEnd[s] = true;
isEnd[e] = true;
}

Liste <Liste<Long>> ans = nouvelle liste <>();
longueur du cur = 0;
int prev = 0;

pour (int i = 1; i <= MAX + 1; i++) {
si (isEnd[i] && cur > 0) {
as.add(Arrays.asList((long)prev, (long)i, cur));
}
prev = isEnd[i] ? i : prev;
cur += diff[i];
}
le retour des an;
}
}
«» "

---

### Python – Utilisation d'une carte triée

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def splitpeinting(self, segments: List[List[int]]) -> Liste[Liste[int]]:
diff = defaultdict(int)
fin = set()

pour s, e, c en segments:
Diff[s] += c
Diff[e] -= c
fin.add(s)
fin.add(e)

Coords = triés(fins)
res = []
pour = 0
prev = coords[0]

pour i dans la plage (1, len(coords)):
cur += diff[prev]
si cur > 0:
Annexe([prev, coords[i], cur])
prev = coords[i]

retour res
«» "

> **Si vous avez besoin strictement `O(n log n)`** (le tri domine), cela satisfait déjà les limites.
> Le code est plus court de 80 % que la solution de la carte et maintient la même logique.

---

### C++ – Base d'array (très efficace)

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle<vector<long>> splitPaintage(vecteur<vector<int>& segments) {
const int MAX = 100001;
vecteur <long> diff(MAX + 2, 0);
vecteur<char> isEnd(MAX + 2, 0);

pour (auto &seg : segments) {
int s = seg[0], e = seg[1];
long c = seg[2];
Diff[s] += c);
diff[e] -= c;
isEnd[s] = isEnd[e] = 1;
}

vecteur<vecteur<long>> ans;
longue courbure = 0;
int prev = 0;

pour (int i = 1; i <= MAX + 1; ++i) {
si (isEnd[i] && cur > 0) {
le nom de l'autorité compétente,
}
prev = isEnd[i] ? i : prev;
cur += diff[i];
}
le retour des an;
}
};
«» "

---

## -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Catégorie
C'est pas vrai.
**Algorithme**= Balayage linéaire; stable même avec grand `maxCoord`.== itération non triée des coordonnées brutes → points d'arrêt manquants. En utilisant une carte *plain* non ordonnée et en itérant arbitrairement – produit un ordre incorrect. Autres
**Structure des données**= `TreeMap` / `std::map` pour les clés triées. "vector<bool>" pour les paramètres (travaille mais légèrement désordonné). Utiliser `ArrayList<entier>` + `HashMap<entier, Long>` puis trier *seulement les touches delta* – vous manquez les coordonnées qui ont "delta". 0'. Autres
**Complexité**"O(n log n)" – fin pour les limites de LeetCode. Autres
**Manipulation de la cornière** Oubliez de mettre à jour `prev` uniquement aux paramètres. Émettre les intervalles de longueur zéro (`[x, x)`), ce qui provoque une mauvaise réponse. Autres
**Readability**= Effacer les noms de variables (`currentSum`, `prevCoord`). Dense logique d'un liner – difficile à déboguer. La sécurité de type manquant (`List.of` vs. `Arrays.asList`). Autres

> **Ligne de bottom** – l'approche de la différence de tableau est la plus propre pour les intervieweurs; la version basée sur la carte est plus facile à lire si vous n'êtes pas à l'aise avec l'indexation de tableau.

---

Comment ce problème vous aide à décrocher votre job de rêve

1. ** Démontre les connaissances de base en matière de structure des données** – Carte, arbre, tableau.
2. **Shows Clean Code & Edge‐case Handling** – les intervieweurs aiment les solutions qui ne s'écrasent pas sur `end=0`.
3. **Expositions La pensée algorithmique** – transformer un problème de peinture en une ligne de balayage* – un modèle de problème d'entrevue classique.
4. **Portfolio Ready** – Téléchargez votre solution avec des commentaires et des tests unitaires sur GitHub ou LinkedIn.
5. **Blog Post / Medium Article** – Partager cet article, comme ci-dessus, prouve que vous pouvez communiquer des idées complexes.
6. **Leverage sur les plateformes de codage** – Ajoutez le problème à votre liste de 50 solutions sur LeetCode, Codeforces, HackerRank.

---

Autre lecture

Pourquoi
- C'est quoi ?
Cracking the Coding Interview (en anglais seulement) – Chapitre sur le schéma d'intervalle* Autres
Algorithmes sur données géométriques – Coursera Autres
De nombreux exemples et explications visuelles. Autres
Université d'entrevue de codage (GitHub) (en anglais seulement) Autres

---

Pensée de clôture

Mastering LeetCode 1943 est un test *soft-skill* – vous ne vous contentez pas de résoudre un puzzle; vous prouvez que vous pouvez:

- **Un problème pour les structures de données* *
- **Boîtes de bord à la main élégantes**
- **Ecrire un code lisible et à jour* *
- ** Expliquez clairement votre raisonnement* *

Mettez cette solution dans votre portfolio, joignez-la à un blog propre, et vous brillerez dans n'importe quel entretien de codage ou sur LinkedIn. Bonne chance ! C'est ce qu'il a dit.

---

*Bon code ! *