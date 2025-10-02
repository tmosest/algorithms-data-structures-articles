---
titre: LeetCode 2015. Hauteur moyenne des bâtiments dans chaque segment -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La hauteur moyenne des bâtiments dans chaque segment – le guide complet
*(Java / Python / C++ implémentations + un blog convivial pour le référencement)*

---

### TL;DR

Description de la langue Autres
- C'est quoi ?
**Java**= O(n log n) temps, O(n) espace== Ligne de balayage + `TreeMap`=
**Python**= O(n log n) temps, O(n) espace== Ligne de balayage + liste triée==
**C++**= O(n log n) temps, O(n) espace== Ligne de balayage + vecteur + tri=

Nous balayons la rue de gauche à droite, maintenons la hauteur totale *sum* et le nombre de bâtiments actifs *cnt*.
À chaque point d'événement (un début ou une fin de construction) nous recalculons la hauteur moyenne.
Si la moyenne change, nous fermons le segment précédent et en commençons un nouveau.
Les segments sans bâtiments (moyenne = 0) ne sont jamais ajoutés.

---

Récapitulation des problèmes

Une rue est une ligne numérique.
`buildings[i] = [start_i, end_i, height_i]` – un bâtiment occupe `[start_i, end_i)` et a la hauteur `height_i`.

**Objectif**
Retourner la liste des segments semi-fermés «[à gauche, à droite)» sans chevauchement, ainsi que la hauteur moyenne entière de tous les bâtiments couvrant ce segment.
La moyenne est "somme(hauteur)/compte" (division entière).
Les segments avec une moyenne = 0 (aucun bâtiment) doivent être omis.
Les segments avec la même moyenne et se touchant l'un l'autre doivent être fusionnés.

La taille d'entrée est jusqu'à 105 bâtiments, coordonnées jusqu'à 108, hauteurs jusqu'à 105.

---

L'idée fondamentale – Ligne de balayage

1. **Événements** – Pour chaque bâtiment créer deux événements:
* `(départ, +hauteur, +1)` – un bâtiment commence.
* `(fin, -hauteur, -1)` – un bâtiment se termine.

2. **Trier** les événements par leur coordination.
Si plusieurs événements partagent la même coordination, traitez-les ensemble, sinon nous diviserions un segment qui devrait rester continu.

3. ** Maintenez l'état** pendant la numérisation des événements triés :

* "sum" – hauteur totale de tous les bâtiments actifs (besoin de 64 bits).
* `cnt` – nombre de bâtiments actifs.
* `prevCoord` – début du segment actuel.
* `prevAvg` – hauteur moyenne du segment actuel.

4. **Sur chaque coordonnée**
* Mettre à jour `sum` et `cnt` avec *all* événements à cette coordination.
* Calculer `newAvg = cnt > 0 ? somme/cnt : 0'.
* Si `newAvg != prevAvg` **et** "prevAvg" 0` → ajouter `[prevCoord, coord, prevAvg]` à la réponse.
* Définir `prevCoord = coord` et `prevAvg = newAvg`.

5. **Finish** – La boucle ferme automatiquement chaque segment; nous n'avons jamais besoin d'une étape spéciale de post-traitement.

Pourquoi fusionne-t-elle des segments égaux à la moyenne?
Parce que nous ne créons un nouveau segment que lorsque la moyenne change réellement.
Si la moyenne reste la même à travers un point d'événement (par exemple, un bâtiment se termine mais un autre avec la même hauteur commence), `prevAvg == newAvg` → pas de segment split.

---

# # # # # # # Cas et pièges

"Piège" "Ce qui s'est mal passé"
- Oui.
**Plusieurs événements à la même coordonnée**
** Division par zéro** 0` lorsqu'il n'y a pas de bâtiment.
**Les grandes sommes**=105 bâtiments × 105 hauteur = 1010 → débordement 32-bit==Utiliser 64-bit (`long` / `int64_t`) pour `sum` Autres
**Empty street** Pas de problème.
**Exigences de fusion**

---

Code complet – Java

"Java
Importation de java.util.*;

solution de classe publique {
moyenneHauteur des bâtiments {
// Événement: [coordonné, deltaHeight, deltaCount]
Liste des événements<int[]> = nouvelle liste d'événements<>(bâtiments.longueur * 2);
pour (int[] b : bâtiments) {
events.add(new int[]{b[0], b[2], 1}); // démarrage
events.add(nouvelle int[]{b[1], -b[2], -1}); // fin
}

// trier par coordonnées
events.sort(Comparator.comparingInt(a -> a[0]);

longueur = 0; // hauteur totale (64 bits)
int cnt = 0; // nombre de bâtiments actifs
int prev = events.get(0)[0]; // coordination du premier événement
int prevAvg = 0; // moyenne précédente
Liste<int[]> ans = nouvelle liste de distribution<>();

i = 0;
alors que (i < events.size()) {
int coord = events.get(i)[0];

// ---- traiter tous les événements de cette coordination ----
pendant que (i < events.size() && events.get(i)[0] == coord) {
somme += events.get(i)[1];
cnt += events.get(i)[2];
i++;
}

int newAvg = cnt > 0 ? (int)(sum / cnt) : 0;

// ---- fermer le segment précédent si la moyenne change ----
si (newAvg != prevAvg && prevAvg > 0) {
ans.add(new int[]{prev, coord, prevAvg});
}

// ---- commencer un nouveau segment ----
prev = coord;
prevAvg = nouveauAvg;
}

// ---- convertir la liste en tableau ----
int[][] res = nouveau int[ans.size()][];
pour (int j = 0; j < ans.size(); J++) {
res[j] = ans.get(j);
}
retour rés;
}
}
«» "

**Pourquoi c'est rapide**
*Trier* prend `O(n log n)`; le scan lui-même est linéaire.
Mémoire: un événement par bâtiment → `O(n)`.

---

Code complet – Python

'`python
de taper l'importation Liste

Solution de classe:
moyenne HauteurDeBâtiments(même, bâtiments: Liste[Liste[int]]) -> Liste[Liste[int]]:
événements = []
pour s, e, h dans les bâtiments:
events.append(s, h, 1)) # début
events.append(e, -h, -1) # fin

events.sort() # trier par coordonnées

sum_h = 0 # 64‐bit automatiquement en Python
cnt = 0
prev = événements[0][0]
Prév_avg = 0
ans = []

i = 0
n = len(événements)
alors que i < n:
Coord = événements[i][0]
# totaliser tous les événements à cette coordination
alors que i < n et événements[i][0]] C'est ce qui s'est passé.
sum_h += événements[i][1]
cnt += événements[i [2]
i += 1

new_avg = (sum_h // cnt) si cnt > 0 autre 0

si new_avg != prev_avg et prev_avg > 0:
([prev, coord, prev_avg])

prev = coord
prev_avg = new_avg

retour et
«» "

---

Code complet – C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle<vector<int>> moyenneHauteur des bâtiments(vecteur<vector<int>>&bâtiments) {
// événement: {coordonné, deltaHeight, deltaCount}
vecteur<tuple<int,int,int>> ev;
ev.reserve(buildings.size() * 2);
pour (auto &b : bâtiments) {
ev.emplace_back(b[0], b[2], 1); // démarrage
ev.emplace_back(b[1], -b[2], -1); // fin
}

(v.begin(), ev.end(),
[](auto const &a, auto const &b){ retour get<0>(a) < get<0>(b); });

longue somme longue = 0; // hauteur totale
int cnt = 0; // nombre de bâtiments actifs
int prev = get<0>(ev[0]); // début du segment actuel
Int prevAvg = 0;
vecteur <array<int,3>> ans;

taille_t i = 0;
pendant que (i < ev.size()) {
int coord = obtenir <0>(ev[i]);

// mise à jour avec tous les événements de cette coordination
(i < ev.size() && get<0>(ev[i]) == coord) {
la somme += obtenir <1>(ev[i]);
cnt += obtenir <2>(ev[i]);
++i;
}

int newAvg = cnt > 0 ? static_cast<int>(sum / cnt) : 0;

si (newAvg != prevAvg && prevAvg > 0) {
le nom et l'adresse de l'utilisateur;
}

prev = coord;
prevAvg = nouveauAvg;
}

// convertir en vecteur<vecteur<int>> (comme int[[]] en Java)
vecteur<vector<int>> res(ans.size());
pour (size_t k = 0; k < ans.size(); ++k)
res[k] = { ans[k][0], ans[k][1], ans[k][2] };
retour rés;
}
};
«» "

---

C'est pas vrai. Prime – Pourquoi c'est la variante de Skyline

Problème Similarités Différences
- C'est quoi ?
**Skyline**. Nous balayons et maintenons également des hauteurs actives.
**Hauteur moyenne**= Utilise la même mise à jour événementielle= Nous avons besoin d'une somme de 64 bits et d'une division entière=
**Merging**. Skyline ne fusionne jamais des hauteurs égales à travers un événement. Notre algorithme saute la création de segment quand la moyenne reste la même.

---

# # # 6 Comment utiliser ceci dans votre entrevue / Résumé

1. **Tag de votre solution** – `@lc` ─ Hauteur moyenne des bâtiments dans chaque segment – `Moyenne`.
2. **Exposer la ligne de balayage** – afficher la liste des événements et la mise à jour de l'état.
3. **Complexité de la concentration** – temps O(n log n), espace O(n).
4. **Discuses pièges** – débordement, division par zéro, regroupement des événements.
5. **Afficher les trois implémentations** – prouver que vous pouvez coder en Java, Python, C++.

---

Article de blog amical

> **Titre**
> Master the LeetCode Problème moyen: Hauteur moyenne des bâtiments – Java, Python & C++

> **Description détaillée* *
> Apprendre à résoudre le LeetCode ‘ Hauteur moyenne des bâtiments dans chaque segment avec un algorithme de balayage. Solutions détaillées Java, Python et C++, analyse de complexité et conseils d'entrevue. (en milliers de dollars)

> **Mots clés**
> LeetCode, Hauteur moyenne des bâtiments, Algorithme de ligne de balayage, Problème Skyline, Codage Interview, Java, Python, C++, Algorithme Thinking, complexité du temps, Complexité spatiale, Ingénieur logiciel, Structures de données, Préparation d'entrevue, Recherche d'emploi, Entretien technique, Problème moyen.

---

Article de blog

> **Auteur:** *Votre nom* – * Ingénieur logiciel
> ** Publié :** * Aujourd'hui*

---

La hauteur moyenne des bâtiments dans chaque segment – Ce que chaque ingénieur logiciel devrait savoir

La hauteur moyenne des bâtiments dans chaque segment est une vitrine parfaite de:

- **Élégance algorithmique**: Une ligne de balayage à un passage bat la force brute par un facteur de 105.
- **Maîtrise de la structure des données**: La gestion des mises à jour d'événements avec une `TreeMap` (Java) ou une liste triée (Python/C++) démontre la connaissance d'arbres / tas équilibrés.
- **L'état d'esprit de résolution des problèmes** : Reconnaître la connexion au problème classique de Skyline et réutiliser le modèle de ligne de balayage est exactement le genre d'intervieweurs perspicaces recherchés.

Ci-dessous, nous allons parcourir le raisonnement, les pièges et les solutions en trois langues. Prenez un café, plongez et n'hésitez pas à copier-coller dans votre dépôt local IDE ou GitHub.

---

Déclaration de problème (paraphrasée)

> Une rue est une ligne numérique.
> `buildings[i] = [start_i, end_i, height_i]` – le bâtiment occupe `[start_i, end_i)` avec la hauteur `hight_i`.
> Retourner une liste des segments semi-fermés «[à gauche, à droite)» avec la hauteur moyenne **entier** de tous les bâtiments couvrant ce segment.
> Les segments où la moyenne est nulle (aucun bâtiment) doivent être omis et les segments touchant la même moyenne doivent être fusionnés.

*Pourquoi ça compte : *
- **Plage coordonnée**: jusqu'à 108, donc on peut pas discrétiser toute la rue.
- ** Taille des entrées**: 105 bâtiments → O(n2) la force brute est impossible.
- ** Pertinence de l'entrevue**: Il s'agit d'un problème classique qui apparaît dans de nombreuses interviews de codage et est une question courante de LeetCode Medium.

---

C'est pas vrai. Le balayage Stratégie sectorielle

1. **Événements de construction**
Pour chaque bâtiment créer deux événements:
Texte
(début, +hauteur, +1) # le bâtiment entre
(fin, -hauteur, -1) # sorties du bâtiment
«» "

2. **Trier par coordonnées* *
Tous les événements triés de gauche à droite.
Si plusieurs événements partagent la même coordination, nous les traitons **ensemble** pour éviter les fractionnements artificiels.

3. **Entretien de l'État**
Texte
somme – hauteur totale de tous les bâtiments actifs (64 bits)
cnt – nombre de bâtiments actifs
prevCoord – début du segment actuel
prevAvg – hauteur moyenne actuelle
«» "

4. **Cité**
* Pour chaque coordonnées «x»:
- Mettre à jour `sum` et `cnt` avec **all** événements à `x`.
- Calculer `newAvg = somme // cnt` si `cnt > 0`, sinon `0`.
- Si `newAvg != prevAvg` **et** `prevAvg > 0`, appuyez sur `[prevCoord, x, prevAvg]` pour répondre à la liste.
- Définir `prevCoord = x` et `prevAvg = newAvg`.

5. **Finale**
Convertir la liste de réponses en tableau/vecteur.

*Complexité:*
- **Time**: `O(n log n)` en raison du tri; le scan est linéaire.
- **Espace**: `O(n)` – un événement par bâtiment.
- **Sécurité d'écoulement**: utiliser 64 bits pour la somme; Les entiers de Python sont non liés, C++/Java ont besoin de "long long`/`long`".

---

##### 3--Pièges communs et comment nous les avons évités

Ce qui arrive
- C'est quoi ?
**Débordement entier**. `sum` dépasse 32 bits. Autres
**La division par zéro** La garde "cnt" 0' avant de diviser. Autres
**Les segments inutiles**La moyenne reste la même sur un événement mais nous créons encore un segment. ** et** "prevAvg > 0". Autres
**Logique de fusion Wrong**. Les segments avec la moyenne zéro ne doivent pas être produits du tout. 0' avant de pousser. Autres

---

C'est pas vrai. Trois implémentations linguistiques spécifiques

##### Java (en utilisant `ArrayList` + analyse d'événement)

"Java
solution de classe {
moyenneHauteur des bâtiments {
Liste des événements<int[]> = nouvelle liste d'événements<>();
pour (int[] b : bâtiments) {
événements.add(nouvelle int[]{b[0], b[2], 1});
événements.add(nouvelle int[]{b[1], -b[2], -1});
}
events.sort(Comparator.comparingInt(a -> a[0]);

somme longue = 0;
cnt = 0;
int prev = events.get(0)[0];
Int prevAvg = 0;
Liste<int[]> ans = nouvelle liste de distribution<>();

pour (int i = 0; i < events.size(); ) {
int x = events.get(i)[0];
pendant que (i < events.size() && events.get(i)[0] == x) {
somme += events.get(i)[1];
cnt += events.get(i)[2];
i++;
}
int newAvg = cnt > 0 ? (int)(sum / cnt) : 0;
si (newAvg != prevAvg && prevAvg > 0)
as.add(new int[]{prev, x, prevAvg});
prev = x;
prevAvg = nouveauAvg;
}

retourner les ans.àArray(nouveau int[0][0]);
}
}
«» "

##### Python (liste/tuple vers l'avant)

'`python
Solution de classe:
moyenne HauteurDeBâtiments(même, bâtiments: Liste[Liste[int]]) -> Liste[Liste[int]]:
événements = []
pour s, e, h dans les bâtiments:
événements.annexe(s, h, 1))
events.append(e, -h, -1))
events.sort()
_h, cnt = 0, 0
prev, prev_avg = événements[0][0], 0
ans = []
i = 0
alors que i < len(events):
x = événements[i][0]
alors que i < len(events) et events[i][0] == x:
sum_h += événements[i][1]
cnt += événements[i [2]
i += 1
new_avg = sum_h // cnt si cnt autre 0
si new_avg != prev_avg et prev_avg > 0:
([prev, x, prev_avg])
prev, prev_avg = x, new_avg
retour et
«» "

##### C++17 (en utilisant `tuple` pour la clarté)

'`cpp
solution de classe {
public:
vectorielle<vector<int>> moyenneHauteur des bâtiments(vecteur<vector<int>>&bâtiments) {
vecteur<tuple<int,int,int>> ev;
pour (auto &b : bâtiments) {
ev.emplace_back(b[0], b[2], 1);
ev.emplace_back(b[1], -b[2], -1);
}
(v.begin(), ev.end(),
[](auto const &a, auto const &b){ retour get<0>(a) < get<0>(b); });

longue somme = 0; int cnt = 0;
int prev = get <0>(ev[0]), prevAvg = 0;
vecteur <array<int,3>> ans;
pour (size_t i = 0; i < ev.size();) {
int x = obtenir <0>(ev[i]);
pendant que (i < ev.size() && get<0>(ev[i]) == x) {
la somme += obtenir <1>(ev[i]);
cnt += obtenir <2>(ev[i]);
++i;
}
int newAvg = cnt ? static_cast<int>(sum / cnt) : 0;
si (newAvg != prevAvg && prevAvg > 0) ans.push_back({prev, x, prevAvg});
prev = x; prevAvg = newAvg;
}

vecteur<vector<int>> res(ans.size());
pour (size_t k = 0; k < ans.size(); ++k)
res[k] = { ans[k][0], ans[k][1], ans[k][2] };
retour rés;
}
};
«» "

---

- Oui. Pourquoi C'est une grande question d'entrevue

1. ** Réutilisabilité** – La technique de balayage de ligne est utilisée pour le nombre minimal d'arcs pour couvrir un point, et le problème classique de Skyline.
2. **Edge‐Case Handling** – montrer que vous savez gérer les grosses sommes et la division par zéro est un moyen rapide d'impressionner les recruteurs.
3. **Travaux de temps/d'espace** – Discuter des raisons pour lesquelles vous pouvez discréter toute la rue, mais peut encore traiter les événements efficacement démontre une forte compréhension des contraintes algorithmiques.

---

- Oui. Conseils de préparation à l'entrevue

- ** Diagramme d'état** : Dessiner la chronologie de l'événement et les changements d'état; aider à clarifier la logique.
- **Test**: Courir les cas d'angle – un seul bâtiment, recoupement des intervalles, aucun chevauchement, bâtiments couvrant le même segment avec différentes hauteurs.
- **Explain Complexity**: `O(n log n)` est optimal pour ce problème; vous ne pouvez pas battre tri.
- ** Flexibilité linguistique** : Montrer les trois implémentations pour prouver la polyvalence.

---

À emporter

Maîtriser ce problème signifie que vous pouvez :

- Appliquer **sweep‐line** aux problèmes impliquant des moyennes, des minima, des maxima ou des sommes sur intervalles.
- Évitez les erreurs courantes comme le débordement ou les événements non groupés.
- Communiquer une solution algorithmique propre dans plusieurs langues.

Ajoutez-le à votre portfolio, pratiquez avec des variations (p. ex., Hauteur moyenne maximale) et vous aurez un solide problème LeetCode Medium dans votre boîte à outils. Bon codage !

---

Références et lectures supplémentaires

- *Algorithmes sur les arbres et les graphiques* – Cormen et al. (Section sur les arbres de recherche binaire équilibrés).
- *LeetCode 1504 : Subarray II* moyen maximum – un autre problème d'intervalle moyen.
- *Cracking the Coding Interview* – chapitre sur les algorithmes Sweep Line.

---

**Fin du blog**

---

Les pensées finales

- **Tag votre solution** dans votre plateforme de codage ou dépôt.
- **Mentionner le motif algorithmique** – ligne de balayage, liste des événements, mise à jour de l'état.
- **Afficher les trois extraits de langue** – c'est un signal fort de fluence de codage.
- **Tenir la discussion sur les pièges** – débordement, division par zéro, regroupement d'événements.

Bonne chance dans votre prochaine interview, et profitez du codage! C'est ce qu'il a dit.

---

* Sentez-vous libre de commenter ci-dessous si vous avez des questions ou voulez discuter de variations plus profondes de ce problème. *