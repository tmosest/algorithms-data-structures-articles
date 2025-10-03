---
titre: LeetCode 3454. Places séparées II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
3454 – Places séparées II
### Le problème le plus dur de division horizontale sur LeetCode
*Vous cherchez un moyen d'impressionner les gestionnaires d'embauche? *
Ce post montre une solution propre et prête à la production en **Java, Python et C++** et explique l'algorithme en anglais simple.
Lire la suite pour découvrir les parties *bon*, *mauvais* et *meilleur* de ce défi – tout ce dont vous avez besoin pour réussir l'entrevue et obtenir ce travail!

---

Table des matières
1. [Résumé du problème] (#résumé du problème)
2. [Intuition et observations clés](#intuition)
3. [Aperçu de l'algorithme] (#algorithme)
4. [Traduit de l'anglais]
5. [Analyse de la complexité] (#complexité)
6. [Pièges communs] (#pièges)
7. [Code – Java](#java-code)
8. [Code – Python](#python-code)
9. [Code – C++](#cpp-code)
10. [Référencement et conseils de recherche d'emploi](#seo)
11. [Réflexions finales] (#finale)

---

<un nom="résumé des problèmes"></a>
- Oui. 1. Résumé du problème

> **Don** un tableau « carrés » où chaque élément est « [xi, yi, li] » – le coin inférieur gauche et la longueur latérale d'un carré –
> **Retour** le *minimum* `y` de telle sorte que la surface syndicale de tous les carrés **ci-dessus** cette ligne égale la surface syndicale **ci-dessous**.
>
> Les carrés peuvent se chevaucher. Les parties superposées ne sont ** comptées qu'une seule fois** (c'est-à-dire que nous travaillons avec la *union* de carrés).

*exemple*

«» "
carrés = [[0,0,1], [2,2,1]]
Réponse: 1.00000
«» "

> Toute ligne horizontale entre `y=1` et `y=2` divise la superficie totale (2) en deux.
> Le plus petit de ces `y` est `1`.

Les contraintes sont importantes (`n ≤ 5·104`, coordonnées jusqu'à `109`, surface totale ≤ `1015`). Des solutions qui fonctionnent dans **O(n log n)** temps et utiliser *O(n)* mémoire sont nécessaires.

---

<un nom></a>
- Oui. 2. Intuition et observations clés

1. **L'aire au-dessous d'une ligne horizontale est une fonction linéaire et monotonique de y**
– Chaque carré apporte une bande rectangulaire `[x, x+l] × [y, y+l]`.
– Lorsque nous balayons `y` vers le haut, la portée horizontale des carrés actifs (la *union des x-intervalles*) ne change qu'en bas ou en haut d'un carré.

2. **L'union des intervalles x est facile à entretenir avec un arbre segmentaire* *
– Nous comprimons les coordonnées `x` (il y a au plus des bords `2n` distincts).
– Chaque événement (début ou fin d'un carré) met à jour une plage dans l'arbre: `+1` en entrant, `-1` en sortant.
– L'arbre conserve la longueur totale couverte dans le temps `O(log n)`.

3. **La zone cumulative entre deux événements consécutifs est**
"couvert Longueur × (y2 – y1)».
– Pendant le balayage, nous pouvons accumuler cette valeur et détecter quand la zone cumulative atteint **la moitié** de la zone syndicale totale.

4. **Le balayage à deux passages est le plus simple* *
– Premier passage: calculer la superficie totale.
– Deuxième passe : balayez à nouveau, s'arrêtant lorsque la surface accumulée ≥ la moitié ; interpolez à l'intérieur de la dalle actuelle pour trouver exactement « y ».

---

<un nom="algorithme"></a>
- Oui. 3. Aperçu de l'algorithme

«» "
1. Construire deux listes d'événements : (y, x1, x2, delta)
delta = +1 au fond du carré, -1 au sommet du carré.

2. Compresser toutes les coordonnées x → xs[0 ... m-1) triés & uniques.

3. Segment Arbre sur xs:
- Compte [noeud] : combien d'intervalles couvrent ce nœud
- longueur[noeud] : longueur totale x couverte par l'intervalle des nœuds

4. Premier passage (pour calculer la superficie totale):
- Trier les événements par y.
- prevY = événements[0]. y
- surface = 0
- Pour chaque événement e:
couvert = segTree.totalCouvert()
zone += couverte * (e.y - prevY)
segTree.update(range x1→x2, delta)
prevY = e.y
- superficie totale = superficie
- moitié = superficie totale / 2

4. Deuxième passage (pour localiser la ligne divisée):
- Réinitialisez l'arbre segmentaire, balayez encore.
- cum = 0
- Pour chaque événement e:
couvert = segTree.totalCouvert()
dalleHauteur = e.y - prevY
si couvert > 0 et cum + couvert * dalleHauteur >= moitié:
// y se trouve à l'intérieur de cette dalle
nécessaire = moitié - cum
ySplit = prevY + nécessaire / couvert
retour ySplit
cum += couvert * dalleHauteur
segTree.update(range x1→x2, delta)
prevY = e.y

// Si nous ne traversons jamais la moitié (par exemple toute la zone concentrée à un seul y),
// il vous suffit de retourner le y du dernier événement (cas de bord).
«» "

**Pourquoi l'interpolation fonctionne**
Dans une dalle, la longueur couverte est constante.
La superficie augmente linéairement avec `y`.
Si nous avons besoin de plus de surface, la hauteur supplémentaire est "nécessaire / couvertLength".

---

<a name="walkthrough"></a>
- Oui. 4. Démarche détaillée

Étape Ce qui se passe Pourquoi ça compte
-- -- -- -- -- -- --
**Création d'événements**= Pour chaque carré `(x, y, l)` ajouter: `(y, x, x+l, +1)` et `(y+l, x, x+l, -1)`= Les événements indiquent quand un carré devient actif ou inactif. Autres
**La compression coordonnée par X**=Tous les différents `x` et `x+l` triés → `xs`.= L'arborescence du segment fonctionne sur des indices, et non sur des coordonnées brutes. Autres
**Segment arbre intérieur**
`tree[v]` – longueur totale couverte dans l'intervalle des nœuds
`cnt[v]` – combien d'intervalles actifs couvrent ce nœud=" Lorsque `cnt[v] > 0`, le noeud est entièrement couvert; sinon nous somme les enfants. Autres
**Première passe – superficie totale**=Passer de la plus petite `y` à la plus grande, mettre à jour l'arbre et ajouter `couvert × Δy` à `zone`. Donne "totalArea". Autres
Autres **Deuxième passage – trouver scission**
Lorsque la superficie cumulée «cum» satisfait «cum + couvert × Δy ≥ la moitié ', calculer exactement `y '. Autres
**Interpolation**=y = prevY + (demi-cum) / couvert`.=Exact `y` dalle intérieure; garantit la précision jusqu'à 1e‐5. Autres

---

<un nom="complexité"></a>
- Oui. 4. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
Autres Génération d'événements Autres
X-compression Autres
Mises à jour de l'arborescence du segment (pourcentage de la taille "4·m") Autres
Autres Premier balayage supplémentaire
Deuxième balayage supplémentaire

**Total**
`Heure : O(n log n) "
"Espace : O(n)"

Avec `n = 5·104` cela correspond confortablement aux limites de LeetCode.

---

<a name="pitfalls"></a>
- Oui. 5. Pièges communs

Comment éviter
C'est quoi ?
**L'utilisation de `int` pour les coordonnées/longueur**. Utilisez `long` (Java) ou `int64_t` (C++). Autres
**Ne pas manipuler la longueur de couverture zéro** Dans une dalle sans carrés actifs, `longueur couverte = 0`. Sauter l'interpolation et continuer à l'événement suivant. Autres
**Overflow pendant le calcul de la surface**=Utilisez `long` pour les longueurs, coulées sur `double` seulement en multipliant par la hauteur. `double` peut représenter jusqu'à `1e308`. Autres
**La mise à jour de l'arborescence du segment doit être *demi-ouverte* `[l, r)`; l'intervalle entre les feuilles est compris entre `xs[i]` et `xs[i+1]`. Autres
** Précision des points de déplacement** La réponse doit être exacte à la rubrique «1e‐5». La formule d'interpolation utilise la division "double" – sûre pour la précision requise. Autres

---

<a name="java-code"></a>
- Oui. 6. Code – Java

"Java
Importation de java.util.*;
importation java.io.*;

solution de classe {
// Événement : changement de couverture à un an donné
classe statique privée Événement {
long y, x1, x2;
int delta; // +1 à l'entrée, -1 à la sortie

Événement(long y, long x1, long x2, int delta) {
y = y;
ce.x1 = x1;
ce.x2 = x2;
Ça. delta = delta;
}
}

// Arbre de segment qui garde la longueur totale couverte x
classe statique privée SegmentTree {
xs; // coordonnées x comprimées
Int final n; // nombre de xs
Compteur de couverture
longueur finale longue[] len; //

SegmentTree(long[] xs) {
ce.xs = xs;
ce.n = longueur xs;
taille de l'int = 4 * n;
cnt = nouvelle int[dimension];
len = nouvelle longueur;
}

// Mise à jour [l, r) par delta
vide update(int node, int l, int r, int ql, int qr, int delta) {
si (qr <= l) ql >= r) retourne;
si (ql <= l && r <= qr) {
cnt[node] += delta;
} autre {
Int milieu = (l + r) >>> 1;
mise à jour (noeud << 1, l, milieu, ql, qr, delta);
mise à jour(noeud << 1), mi, r, ql, qr, delta);
}
si (cnt[node] > 0) {
len[node] = xs[r] - xs[l];
} sinon si (r - l) 1) {
len[node] = 0;
} autre {
len[node] = len[node << 1] + len[node << 1];
}
}

long total Couvert() {
retour len[1];
}
}

carré public double séparé {
int n = carrés. longueur;
// Construire des événements
Liste <Événement> ev = nouvelle liste de distribution<>(2 * n);
long[] xsRaw = nouveau long[2 * n];
Int idx = 0;
pour (int[] sq : carrés) {
longueur x = carré[0];
long y = sq[1];
long l = carré[2];
longueur x1 = x;
longueur x2 = x + l;
ev.add(nouveau événement(y, x1, x2, +1));
ev.add(nouveau événement(y + l, x1, x2, -1));
xsRaw[idx++] = x1;
xsRaw[idx++] = x2;
}

// Compresser x
long[] xs = compresse(xsRaw);

// Premier balayage – calcul de la superficie totale
double zone totale = zone de calcul (ev, xs, n);

moitié double = superficie totale / 2,0;

// Deuxième balayage – trouver la ligne fractionnée
double réponse = findSplit(ev, xs, moitié, n);
réponse de retour;
}

Compresse statique privée longue[] brute {
Tableaux.sort(brut);
int m = 0;
pour (int i = 0; i < longueur brute; ++i) {
si (i) Valeur brute cru[i - 1] {
brut[m++] = brut[i];
}
}
retour Arrays.copyOf(raw, m);
}

ev, long[] xs, int n) {
ev.sort(Comparator.comparingLong(a -> a.y));
Segment m = nouveau segmentTree(xs);
longue prevY = ev.get(0).y;
double surface = 0,0;

pour (événement e : ev) {
long curY = e.y;
long couvertLen = st.totalCouvert();
surface += couvertLen * (double) (curY - prevY);

st.update(1, 0, xs.longueur - 1,
Recherche(xs, e.x1),
Recherche(xs, e.x2),
e.delta);
prevY = curY;
}
zone de retour;
}

privé statique double findSplit(Liste <Event> ev, long[] xs,
double moitié, int n) {
ev.sort(Comparator.comparingLong(a -> a.y));
Segment m = nouveau segmentTree(xs);
longue prevY = ev.get(0).y;
double cum = 0,0;

pour (événement e : ev) {
long curY = e.y;
long couvertLen = st.totalCouvert();
long delta Y = curY - prevY;
si (couvert) 0) {
double besoin = demi-cumul;
si (besoin <= couvertLen * deltaY) {
retour prevY + besoin / couvert Len;
}
cum += couvertLen * (double) delta Y;
}

st.update(1, 0, xs.longueur - 1,
Recherche(xs, e.x1),
Recherche(xs, e.x2),
e.delta);
prevY = curY;
}
// Toute la zone sur une seule ligne horizontale – retour dernier y
retour ev.get(ev.size() - 1).y;
}

// Helper: trouver l'index d'une valeur dans xs compressé
int idx(long[] xs, long val) {
retourner Arrays.binarySearch(xs, val);
}
}
«» "

**Explication des éléments clés**

- `computeArea` utilise la même liste d'événements pour éviter la reconstruction; il suffit de la re-trier.
- `Arrays.binarySearch(xs, value)` retourne l'index compressé d'une coordonnée brute.
- Oui. L'arbre de segment utilise des plages semi-ouvertes; la racine couvre `[0, xs.longueur-1]` (c'est-à-dire entre la première et la dernière coordonnée compressée).

---

<un nom="cxx-code"></a>
- Oui. 7. Code – C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

struct Event {
long y, x1, x2;
int delta; // +1 à l'entrée, -1 à la sortie
Événement (long long y, long long x1, long long x2, int delta)
: y(y), x1(x1), x2(x2), delta(delta) {}
};

struct SegTree {
Const vector<long long> &xs; // coordonnées compressées
int n; // nombre de xs
vector<int> cnt; // compteur de couverture
vectoriel <long long> len; // longueur couverte

SegTree(vecteur const<long> &xs) : xs(xs) {
n = xs.size();
à l'intérieur sz = 4 * n;
cnt. attribuer(sz, 0);
len.assign(sz, 0);
}

vide update(int node, int l, int r,
ql, int qr, int delta) {
si (qr <= l) ql >= r) retourne;
si (ql <= l && r <= qr) {
cnt[node] += delta;
} autre {
Int milieu = (l + r) >> 1;
mise à jour (noeud << 1, l, milieu, ql, qr, delta);
mise à jour(noeud << 1), mi, r, ql, qr, delta);
}
si (cnt[node] > 0) {
len[node] = xs[r] - xs[l];
} sinon si (r - l) 1) {
len[node] = 0;
} autre {
len[node] = len[node << 1] + len[node << 1];
}
}

long total long Couvert() const { retour len[1]; }
};

vecteur<long long> compresse(vecteur<long long> brut) {
tri(raw.begin(), cru.end());
rough.erase(unique(raw.begin(), rough.end()), rough.end());
retour brut;
}

double calcul Zone(vecteur <Event> ev, vecteur const <long> &xs) {
Tri(ev.begin(), ev.end(), [](const Event &a, const Event &b){
retour a.y < b.y;
});

m(xs) SegTree;
longue prévY longue = ev[0].y;
double surface = 0,0;

pour (const auto &e : ev) {
long curY = e.y;
long couvert = st.totalCouvert();
surface += couverte * double(curY - prevY);

int l = lower_bound(xs.begin(), xs.end(), e.x1) - xs.begin();
int r = lower_bound(xs.begin(), xs.end(), e.x2) - xs.begin();
st.update(1, 0, xs.size() - 1, l, r, e.delta);
prevY = curY;
}
zone de retour;
}

double findSplit(vector<Event> ev,
vecteur const <long> &xs,
moitié double) {
Tri(ev.begin(), ev.end(), [](const Event &a, const Event &b){
retour a.y < b.y;
});

m(xs) SegTree;
longue prévY longue = ev[0].y;
double cum = 0,0;

pour (const auto &e : ev) {
long curY = e.y;
long couvert = st.totalCouvert();
long delta Y = curY - prevY;
Si (couvert > 0 & & cum + couvert * double(deltaY) >= moitié) {
double besoin = demi-cumul;
retour prevY + besoin / couvert;
}
cum += couvert * double (deltaY);

int l = lower_bound(xs.begin(), xs.end(), e.x1) - xs.begin();
int r = lower_bound(xs.begin(), xs.end(), e.x2) - xs.begin();
st.update(1, 0, xs.size() - 1, l, r, e.delta);
prevY = curY;
}
// Cas de bord: toute la zone concentrée en un seul y
retour ev.back().y;
}
«» "

**Points clés* *

- `lower_bound` obtient l'index compressé.
- `SegTree` utilise `xs.size() - 1` comme indice le plus droit car chaque feuille représente `[xs[i], xs[i+1]]`.

---

<un nom="cxx-code"></a>
- Oui. 8. Code – C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

// - Oui. Événement...
struct Event {
long y, x1, x2;
int delta; // +1 entrant, -1 départ
Événement (long long y, long long x1, long long x2, int delta)
: y(y), x1(x1), x2(x2), delta(delta) {}
};

// - Oui. Arbre segmenté ---------
struct SegTree {
Const vector<long long> &xs; // comprimé x
vectorielle <int> cnt; // nombre de couverture
vectoriel <long long> len; // longueur couverte

SegTree(vecteur const<long> &xs) : xs(xs) {
int sz = 4 * xs.size();
cnt. attribuer(sz, 0);
len.assign(sz, 0);
}

vide à la hausse(int node, int l, int r, int ql, int qr, int delta) {
si (qr <= l) ql >= r) retourne;
si (ql <= l && r <= qr) {
cnt[node] += delta;
} autre {
Int milieu = (l + r) >> 1;
(noeud << 1, l, milieu, ql, qr, delta);
upd(noeud << 1=1, milieu, r, ql, qr, delta);
}
si (cnt[node] > 0) {
len[node] = xs[r] - xs[l];
} sinon si (r - l) 1) {
len[node] = 0;
} autre {
len[node] = len[node << 1] + len[node << 1];
}
}

long couvert() const { retour len[1]; }
};

// Les assistants...
vecteur<long long> compresse(vecteur<long long> brut) {
tri(raw.begin(), cru.end());
rough.erase(unique(raw.begin(), rough.end()), rough.end());
retour brut;
}

double calcul_area(vecteur <Event> ev, vecteur const <long> &xs) {
Tri(ev.begin(), ev.end(), [](const Event &a, const Event &b){
retour a.y < b.y;
});

m(xs) SegTree;
longue prévY longue = ev.front().y;
double surface = 0,0;

pour (const auto &e : ev) {
long curY = e.y;
long cov = m. recouvert();
surface += cov * double(curY - prevY);

int l = lower_bound(xs.begin(), xs.end(), e.x1) - xs.begin();
int r = lower_bound(xs.begin(), xs.end(), e.x2) - xs.begin();
st.upd(1, 0, xs.size() - 1, l, r, e.delta);
prevY = curY;
}
zone de retour;
}

double find_split(vector<Event> ev, vecteur const<long> &xs,
moitié double) {
Tri(ev.begin(), ev.end(), [](const Event &a, const Event &b){
retour a.y < b.y;
});

m(xs) SegTree;
longue prévY longue = ev.front().y;
double cum = 0,0;

pour (const auto &e : ev) {
long curY = e.y;
long cov = m. recouvert();
long delta Y = curY - prevY;

si (cov > 0 & & cum + cov * double(deltaY) >= moitié) {
double besoin = demi-cumul;
retour prevY + besoin / cov;
}
cum += cov * double (deltaY);

int l = lower_bound(xs.begin(), xs.end(), e.x1) - xs.begin();
int r = lower_bound(xs.begin(), xs.end(), e.x2) - xs.begin();
st.upd(1, 0, xs.size() - 1, l, r, e.delta);
prevY = curY;
}
retour ev.back().y; // cas bord
}

// - Oui. Principale --------
Int main() {
ios::sync_with_stdio(faux);
cin.tie (nullptr);

int N; // nombre de rectangles
if(!(cin >> N)) retourner 0;
vecteur <Event> ev;
vecteur <long> bruts;
pour (int i = 0; i < N; ++i) {
longue longue x1,y1,x2,y2;
cin >> x1 >> y1 >> x2 >> y2;
ev.emplace_back(y1, x1, x2, +1);
ev.emplace_back(y2, x1, x2, -1);
rough.push_back(x1);
rough.push_back(x2);
}

vecteur <long> xs = compresse(raw);
double total = zone de calcul (ev, xs);
moitié double = total / 2,0;
double réponse = find_split(ev, xs, half);

cout.setf(ios:fixed); cout << setprécision(6) << réponse << '\n';
retour 0;
}
«» "

**Compilé**

«» "
g++ -std=c++17 -O2 -Wall main.cpp -o main
«» "

---

- Oui. 9. Analyse de la complexité

- **Événements de tri**: \(O(N \log N)\)
- ** Arbre de segment de construction**: \(O(N)\) (une fois par balayage)
- **Passer** : chaque événement déclenche une mise à jour arborescente – \(O(\log N)\)
- **Total**: \(O(N \log N)\) heure, \(O(N)\) mémoire

Avec \(N \le 10^5\), cela satisfait facilement les limites.

---

10 ans. Remarques finales

- Oui. La technique de balayage de ligne tourne un géométrique apparemment bidimensionnel
problème dans une séquence de mises à jour 1-dimensionnelles, permettant une
Solution \(O(N\log N)\).
- L'utilisation d'un tableau **différence** pour la couverture x simplifie la
mise en œuvre et garantit la mémoire linéaire.
- Oui. La solution fonctionne pour toutes les coordonnées entières dans les limites
\([0,10^9]\) et est robuste contre les cas dégénérés où toute la zone est
concentré sur une seule ligne horizontale.