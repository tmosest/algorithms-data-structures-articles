---
titre: LeetCode 3394. Vérifiez si Grid peut être coupé en sections -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3394. Vérifiez si Grid peut être coupé en sections
**Moyenne** – Code Leet
"contrôle public du booléen ValidCuts(int n, int[][] rectangles) "

---

### TL;DR
* Trier les rectangles par leurs frontières *y* (ou *x*).
* Construisez deux préfixes/suffixes qui vous indiquent, pour chaque ligne de coupe possible, combien de rectangles se trouvent complètement en dessous/au-dessus de cette ligne.
* Une paire de coupes horizontales est valable sif:
* au moins un rectangle se trouve sous la première coupe,
* au moins un rectangle se trouve au-dessus de la deuxième coupe, et
* les rectangles restants sont sandwichés entre les deux coupes.
* Faites de même pour les coupes verticales.
* complexité du temps : **O(m log m)**, mémoire: **O(m)**, où *m* = 2 × nombre de rectangles.
* Fonctionne pour les limites les plus défavorables: *n* ≤ 109, jusqu'à 105 rectangles.

---

## Le cauchemar de la Forte-Force (Le gros**)

Une façon naïve est d'énumérer ** chaque** paire de coordonnées de coupe:

Texte
pour chaque y1 en [0..n]
pour chaque y2 en (y1..n)
si tous les rectangles se trouvent entièrement dans l'une des 3 bandes horizontales
retour vrai
«» "

Mais `n` peut être 109! Même si l'on ne regarde que les valeurs *y* qui apparaissent réellement dans l'entrée (il y en a au plus 2·105), la vérification d'une seule paire nécessite toujours la numérisation des 105 rectangles.
Ce serait ~1010 opérations – bien au-delà de ce que tout entretien ou système de production peut gérer.

---

## L'élégant balbutiement (Le ** Bon**)

Le problème a une structure cachée:

*Les anneaux ne se chevauchent pas. *
Par conséquent, la projection **** de chaque rectangle sur l'axe *y* est un intervalle disjoint `[minY, maxY]`.
Il en va de même pour l'axe *x*.

Si nous traitons chaque valeur de bordure distincte (à la fois commence et se termine) comme une ligne de coupe potentielle, nous pouvons répondre à la question "Combien de rectangles se trouvent en dessous de *cette ligne*?
L'astuce est de construire un **préfixe-sum** sur les frontières *end* et un **suffixe-sum** sur les frontières *start*.

Une fois que nous avons ces deux aides, une paire horizontale de coupes se trouve en un seul passage sur les positions de coupe possibles – pas de boucles imbriquées, pas de vérifications par rectangle.

---

L'algorithme, étape par étape

1. **Collecter toutes les frontières**
* Pour chaque rectangle pousser son `startY` et `endY` dans un tableau.
* Trier le tableau et supprimer les duplicatas → `yVals` (taille *m*).

2. **Map une valeur limite → index* *
* Utilisez un `Map<int, int>` (ou un dictionnaire dans Python) pour transformer une coordonnée en un index de tableau dans *O(log m)*.

3. **Count rectangles qui se terminent/commencent à chaque indice**
Texte
endCount[i] = combien de rectangles ont endY == Oui.
startCount[i] = combien de rectangles ont commencé Oui. Oui.
«» "

4. **Préfixe / suffixe**
Texte
ci-dessous[i] = fin du compte[0..i] // rectangles complètement inférieurs à la coupe y = yVals[i]
ci-dessus[i] = γ startCount[i.m‐1] // rectangles complètement au-dessus de la coupe y = yVals[i]
«» "

5. **Essayez toutes les premières coupes**
Texte
pour k = 0 .. m‐2
inférieure = inférieure à [k]
Si bas == 0: continuer

// trouver la première seconde coupe qui a au moins un rectangle au-dessus
l = k + 1
pendant que l < m et au-dessus[l]] 0: l++

si l >= m: pause

haut = supérieur[l]
milieu = totalRectangles - bas - haut
si milieu > 0: retour vrai
«» "

*Pourquoi une seule recherche suffit-elle? *
Alors que nous déplaçons la deuxième coupe vers la droite, « au-dessus » n'augmente jamais – il reste seulement le même ou diminue.
Par conséquent, le nombre de rectangles dans la bande supérieure ne peut que diminuer, tandis que la bande moyenne ne peut que rétrécir.
Si la bande médiane est vide au premier `l` viable, elle restera vide pour tous les `l` plus grands. Donc un seul contrôle par `k` suffit.

6. **Faites la même chose pour l'axe *x*** – exactement le même code, il suffit d'échanger `x` et `y`.

7. **Retour** « vrai » si l'une ou l'autre orientation fonctionne, sinon « faux ».

---

## Mise en oeuvre complète des références

Voici trois solutions idiomatiques – **Java**, **Python** et **C++** – chacune annotée pour pouvoir les copier dans une salle d'entrevue ou un harnais de test LeetCode.

---

- Oui. 1. Java

"Java
Importation de java.util.*;

solution de classe publique {
contrôle public du booléenValidCuts(int n, int[][] rectangles) {
// ----- coupes horizontales -----
si (validCuts(n, rectangles, true)) retourne vrai;
// ----- coupes verticales -----
si (validCuts(n, rectangles, faux)) retourne vrai;
retourner faux;
}

// direction = vrai → travailler sur y, faux → travailler sur x
Booléen privé valideCuts(int n, int[][] rects, booléen horizontal) {
int m = longueur rects;
int[] coords = nouveau int[2 * m];
int ptr = 0;
pour (int[] r : rects) {
int a = horizontale ? r[1] : r[0]; // début
int b = horizontale ? r[3] : r[2]; // fin
coords[ptr++] = a;
les coords[ptr++] = b;
}

// unique, trié
les tableaux.sort(coords);
int[] uniq = nouveau int[ptr];
Int sz = 0;
pour (int i = 0; i < ptr; i++) {
si (i) Cods[i] != Codages - 1]) {
uniq[sz++] = coords[i];
}
}
uniq = Arrays.copyOf(uniq, sz); // longueur réelle

// coordonnées de la carte → index
Carte <entier, entier> idx = nouveau HashMap<>(sz * 2);
pour (int i = 0; i < sz; i++) idx.put(uniq[i], i);

début int[] Cnt = nouveau int[sz];
int[] endCnt = nouveau int[sz];
pour (int[] r : rects) {
début int = horizontal ? r[1] : r[0];
l'extrémité int = horizontale ? r[3] : r[2];
gtCnt[idx.get(start)]++;
EndCnt[idx.get(end)]++;
}

Préfixe de la fin Cnt = nombre de rectangles avec fin <= coupe
int[] ci-dessous = nouvelle int[sz];
cum int = 0;
pour (int i = 0; i < sz; i++) {
cum += finCnt[i];
ci-dessous [i] = cum;
}

// suffixe de départ Cnt = nombre de rectangles avec début >= coupé
int[] ci-dessus = nouveau int[sz];
cum = 0;
pour (int i = sz - 1; i >= 0; i--) {
cum += startCnt[i];
ci-dessus [i] = cum;
}

// Essayez toutes les premières positions de coupe
pour (int k = 0; k < sz - 1; k++) {
int fond = en dessous de [k];
si (fond) 0) continuer; // avoir besoin d'au moins un

int l = k + 1;
alors que (l < sz && au-dessus [l]] 0) l++; // sauter les sections supérieures vides
en cas de rupture (l >= sz);

int top = au-dessus de [l];
int milieu = m - bas - haut; // total = m rectangles

Si (moyen > 0 & & top > 0) retour vrai;
}
retourner faux;
}
}
«» "

> **Pourquoi ça marche* *
> * `ci-dessous[k]` compte tous les rectangles dont le **end** est ≤ la première coupe.
> * `ci-dessus[l]` compte tous les rectangles dont **start** est ≥ la seconde coupe.
> * `m - bas - haut` est exactement le nombre de rectangles qui s'assoient strictement entre les deux coupes.
> Si chaque pièce n'est pas vide, nous avons une paire valide de coupes.

---

- Oui. 2. Python

'`python
def checkValidCuts(n: int, rectangles: List[List[int]]) -> Bool:
def try_cuts(coord_start, coord_end):
"""La même logique que Java, mais écrite pour Python."""
m = len(rectangles)

# Recueillir toutes les valeurs limites
Coords = []
pour a, b, c, d en rectangles:
coords.append(coord_start)
Cods.append(coord_end)

# unique trié
uniq = trié(set(coords))
idx = {v: i pour i, v dans énumérate(uniq)}

start_cnt = [0] * len(uniq)
end_cnt = [0] * len(uniq)

pour a, b, c, d en rectangles:
start_cnt[idx[a]] += 1
end_cnt[idx[d]] += 1

# préfixe de fin_cnt
ci-dessous = [0] * len(uniq)
s = 0
pour i, val dans l'énumération(uniq):
s += fin_cnt[i]
en dessous de [i] = s

# suffixe de start_cnt
ci-dessus = [0] * len(uniq)
s = 0
pour i dans la plage (len(uniq) - 1, -1, -1):
s += start_cnt[i]
ci-dessus [i] = s

Total = m
pour k dans la plage (len(uniq) - 1):
inférieure = inférieure à [k]
Si bas == 0:
poursuivre
l = k + 1
pendant que l < len(uniq) et au-dessus[l]== 0:
l += 1
si l >= len(uniq):
pause
haut = supérieur[l]
milieu = total - bas - haut
si milieu > 0:
retour Vrai
Retour Faux

# coupes horizontales (axe y)
si try_cuts(lambda r: r[1], lambda r: r[3]):
retour Vrai
# coupes verticales (axe x)
si try_cuts(lambda r: r[0], lambda r: r[2]):
retour Vrai
Retour Faux
«» "

> *Python* maintient le même comportement O(m log m) tout en étant très ters.

---

- Oui. 3. C++

'`cpp
solution de classe {
public:
Vérification du boolValidCuts(int n, vecteur<vector<int>>& rects) {
si (solve(rects, true)) retourne true; // horizontale
si (solve(rects, false)) retourne true; // verticale
retourner faux;
}

particulier:
solution bool(vecteur<vecteur<int>>& rects, bool horizontal) {
int m = rects.size();

// 1. collecte des frontières
vecteur<int> les coûts;
les réserves de coords(2 * m);
pour (auto &r : rects) {
début int = horizontal ? r[1] : r[0];
l'extrémité int = horizontale ? r[3] : r[2];
coords.push_back(start);
coords.push_back(end);
}

// 2. unique trié
tri(coords.begin(), coords.end());
coords.erase(unique(coords.begin(), coords.end()), coords.end());

// 3. coordonner → index map
non ordonné_map<int, int> idx;
idx.reserve(coords.size() * 2);
pour (int i = 0; i < (int)coords.size(); ++i) idx[coords[i]] = i;

vector<int> startCnt(coords.size(), 0), endCnt(coords.size(), 0);
pour (auto &r : rects) {
début int = horizontal ? r[1] : r[0];
l'extrémité int = horizontale ? r[3] : r[2];
++startCnt[idx[start]];
++endCnt[idx[end]];
}

// 4. préfixe de fin Cnt → ci-dessous
vecteur<int> ci-dessous(coords.size(), 0);
Int cur = 0;
pour (int i = 0; i < (int)coords.size(); ++i) {
pour += finCnt[i];
ci-dessous [i] = cur;
}

// 5. suffixe de départ Cnt → ci-dessus
vecteur<int> ci-dessus(coords.size(), 0);
cur = 0;
pour (int i = (int)coords.size() - 1; i >= 0; --i) {
cur += startCnt[i];
ci-dessus [i] = cur;
}

// 6. essayez toutes les premières coupes
pour (int k = 0; k < (int)coords.size() - 1; ++k) {
int fond = en dessous de [k];
si (!bottom) continue; // besoin de quelque chose ci-dessous

int l = k + 1;
pendant que [l < (int)coords.size() & && aprés] ++l;
si (l >= (int)coords.size()) se brise;

int top = au-dessus de [l];
int milieu = m - bas - haut;
si (moyen > 0) retour vrai;
}
retourner faux;
}
};
«» "

> La version C++ suit le même pipeline, mais utilise `unordered_map` et `vector<int>` pour la vitesse.

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Collecte aux frontières
Tri + dedup.
Nombre de bâtiments
Vérification de toutes les premières coupes **O(m)**
**O(m log m)**

L'utilisation de la mémoire est linéaire dans le nombre de bordures distinctes (2 m).

---

## Et si vous voulez gérer la gamme complète [0, n]?

L'algorithme ci-dessus utilise uniquement les frontières qui apparaissent réellement dans l'entrée.
Si vous voulez également autoriser une coupe à `0` ou `n` (même si aucun rectangle ne les touche), ajoutez simplement ces valeurs à la liste des bordures avant la déduplication.
Tout le reste reste reste identique.

---

## Cas de bord et pièges communs

Autres Décision Pourquoi il importe de savoir comment le code le gère
C'est-à-dire
Autres **Un seul rectangle. sera 0 pour toute première coupe; boucle ne reviendra jamais vrai. Autres
Autres **Tous les rectangles empilés** (touchant l'un l'autre) : Les coupes ne peuvent passer que par l'espace vide. Autres
**Rectangles partageant une frontière** Puisque l'intervalle `[minY, maxY]` serait vide, ces rectangles sont ignorés automatiquement. Autres
Autres **Coordonnées importantes** 2 B Utilisez «long long» ou des ints 64 bits, le cas échéant. Autres

---

Les pensées finales

- L'idée **core** – préfixe des extrémités + suffixe des départs – est universelle pour les problèmes basés sur l'intervalle.
- Oui. Une fois que vous avez ces aides, *any* question qui demande combien d'intervalles se trouvent entièrement d'un côté d'un seuil de la réponse peut être répondu en *O(1)*.
- Oui. L'algorithme fonctionne en *O(m log m)* temps et *O(m)* espace, confortablement rapide pour des rectangles `10^5`, ce qui est typique pour les contraintes LeetCode.

N'hésitez pas à adapter le code à votre langue de choix, à modifier les commentaires, et à apporter l'intuition des bordures distantes → deux tableaux de préfixes à votre prochaine interview. Bonne chance ! C'est ce qu'il a dit.

---