---
titre: LeetCode 3382. Superficie maximale Rectangle avec contraintes ponctuelles II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

Code du leet 3382 – maximum Domaine Rectangle avec contraintes ponctuelles II
- Oui. Java / Python / C++ – Solutions de travail complètes
### SEO-Optimized Blog Post – Comment j'ai craqué le plus dur problème de rectangle de Leetcode

> **Mots clés:**
> *Réceptangle maximal de la zone avec contraintes ponctuelles*= *LeetCode 3382*== *solution de java*= *solution de python*== *solution de C++*== *Arbre du printemps*== *Arbre du printemps*== *Ligne de balayage*== *Interview Algorithme*== *Entretien d'emploi*

---

Table des matières

Lien
- Oui.
Aperçu du problème
Pourquoi c'est dur
Données Structures requises
#algorithme #algorithme
Code (Java)
Code (Python)
Code (C++)
Temps et complexité de l'espace
Pièges communs
#interview-tips
Conclusion du blog

---

## # problème-visualisation

> **Objectif:**
> Compte tenu de «n» points distincts sur un plan infini, trouver la zone *maximum* d'un rectangle aligné sur l'axe qui utilise **exactement quatre** des points comme coins et ** ne contient aucun autre point** (intérieur ou à sa frontière).
> Retourner la zone ou `-1` si aucun rectangle de ce type n'existe.

** Contraintes d'entrée* *

Variable
C'est quoi ?
"n = xCoord.longueur = yCoord.longueur" Autres
"0 ≤ xCoord[i], yCoord[i] ≤ 8·107` Autres
Autres Tous les points sont uniques.

---

Pourquoi ?

- **Plus grande taille d'entrée (200k)** → Les solutions O(n2) ou O(n·log2n) sont trop lentes.
- **Aucun point ne peut se trouver sur ou à l'intérieur du rectangle** → nous devons savoir si un point se trouve entre deux coordonnées x‐ et y choisies.
- **Axe-aligné** simplifie la géométrie mais exige toujours une manipulation attentive de l'adjacence verticale/horizontale.
- **Typical LeetCode Défi** : nécessite un mélange de ligne de balayage, de compression des coordonnées et de structures avancées de données (arbre Fenwick / Segment).

---

Structures de données

Pourquoi ?
- Oui.
**Compression coordonnée** sur les valeurs y. Autres
**Fenwick Tree (Binary Indexed Tree) **= O(log n) game‐sum requêtes pour le nombre de points entre les coordonnées y. Autres
**HashMap** (`long` → `int`)= Entreposer le dernier segment vertical vu entre deux indices de y. Autres
**Carte** pour les valeurs de x (`long` → `int`) Autres

---

## #algorithme

1. **Comprimer les coordonnées y**
*Créer un tableau `ys` trié & dédoublé; map chaque original y à son index. *

2. **Traitement des points de construction**
Pour chaque point «i»:
`points[i] = {xCoord[i], compriméYIndex(i)} "

3. **Trier les points par x, puis par y**
Balayer à gauche → à droite de l'avion.

4. **Initialiser l'arbre du Fenwick** (taille = `ys.longueur`).

5. **Passer sur les points triés* *

Pour chaque point `(x, yIdx)`:

- Mettre à jour Fenwick: `add(yIdx, 1)` – nous voyons maintenant ce y en cours x.
- **Si ce point partage le même x avec le point précédent** (c'est-à-dire deux points sur la même ligne verticale):
- Que `y1` et `y2` soient les indices y des deux points consécutifs (en premier lieu).
- Calculer `entre = somme(y2) - somme(y1-1)` → nombre de points dont y se trouve dans `(y1, y2)` *à jour x*.
- Encoder la paire `(y1, y2)` dans une clé de 64 bits: `key = (long)y2 << 32= y1`.
- Si cette clé était déjà vue :
- 'prevBetween = map[key] "
- Si "entre == prevBetween + 2`
(ce qui signifie que le rectangle entre ces deux segments verticaux a *exactement* 4 coins et rien d'autre à l'intérieur),
puis calculer la zone:
`area = (long)(x - prevX[key]) * (y[y2] - ys[y1]) "
Mettre à jour la réponse.
- Stocker `map[key] = entre` et `prevX[key] = x`.

6. **Retourner la réponse** (`-1` si toujours `-1`).

**Pourquoi est-ce que "entre == prevBetween + 2`?**

- Les deux lignes verticales à x = prevX et x = x doivent chacune avoir *exactement* deux points à y1 et y2 (les angles rectangles).
- Entre eux (à l'intérieur du rectangle) il doit y avoir *non* autre point.
- Oui. Dans l'arbre Fenwick, nous avons compté combien de points se trouvent *strictement* entre y1 et y2 au courant x.
- Oui. Au x précédent, ce nombre était "prevBetween".
- Ajouter les deux nouveaux points d'angle donne "prevBetween + 2".
- Oui. Si la différence est plus grande, un autre point se trouve à l'intérieur → rectangle invalide.

---

Java

"Java
Importation de java.util.*;
importation java.io.*;

solution de classe publique {
// -------- Fenwick Tree...
classe statique privée Fenwick {
bit[];
Fenwick(int n) { bit = nouvelle int[n + 1]; }
vide add(int idx, int delta) {
pour (int i = idx + 1; i < bit.longueur; i += i & -i) bit[i] += delta;
}
(int idx) { // inclusivement
int s = 0;
pour (int i = idx + 1; i > 0; i -= i & -i) s += bit[i];
retour s;
}
}

public long maxRectangleArea(int[] xCoord, int[] yCoord) {
int n = longueur xCoord;
int[] ys = compresse(yCoord); // compression de coordonnées
int[] pts = nouvelle int[n][2];
pour (int i = 0; i < n; i++) {
pts[i][0] = xCoord[i];
pts[i][1] = Arrays.binarySearch(ys, yCoord[i]); // comprimé y
}

// trier par x, puis par y
(a, b) -> a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]);

Fenwick ft = nouveau Fenwick (longueur ys.);
Carte < Longue, entière> entreCnt = nouvelle HashMap<>(); // clé: (y2 << 32)
Carte<Long, Integer> prevX = nouveau HashMap<>(); // touche: dernier x pour cette paire de y

long ans = -1;
pour (int i = 0; i < n; i++) {
int x = pts[i][0];
int y = pts[i][1];
ft.add(y, 1); // nous voyons maintenant ce y au courant x

// deux points sur la même ligne verticale ?
si (i > 0 & & pts[i][0] == pts[i - 1][0] {
int yLow = Math.min(pts[i - 1][1], y);
int yHigh = Math.max(pts[i - 1][1], y);
int cntInside = ft.sum(yHigh - 1) - ft.sum(yLow);

clé longue = ((long) yHaute << 32)
si (entreCnt.contientKey(key)) {
int prevCnt = entreCnt.get(key);
int prevXVal = prevX.get(key);
si (cntInside == prevCnt + 2) {
longue surface = (long) (x - prevXVal) *
(y[yHigh] - ys[yLow]);
si (zone > ans) ans = zone;
}
}

entreCnt.put(clé, cntInside);
prevX.put(clé, x);
}
}
le retour des an;
}

// --------- aide: y compression ---------
compresse statique privée int[] a) {
int[] b = a.clone();
les tableaux.sort(b);
int p = 0;
pour (int val : b) {
si (p=0=0== b[p - 1]) b[p++] = val;
}
retour Arrays.copyOf(b, p);
}

// --------------------------
carte privée<Long, Integer> prevX = nouveau HashMap<>();
}
«» "

**Explication**

- Tous les indices sont basés sur 0 à l'intérieur de «Fenwick».
- Oui. La clé est une valeur 64 bits de sorte que les paires `(yLow, yHigh)` ne se heurtent jamais.
- `prevX` est une carte *parallèle* qui détient la coordination x précédente pour chaque paire de y.

---

## #python

'`python
de bisect importer bisect_left
de collections importer par défautdict
importations

Catégorie Fenwick:
def __init_(self, n):
Self.bit = [0] * (n + 1)

def add(self, idx, delta):
i = idx + 1
pendant que i < len(self.bit):
Soi.bit[i] += delta
i += et -i

def sum(self, idx): # inclusivement
s = 0
i = idx + 1
alors que i:
s += self.bit[i]
I -= et -i
retour s

def compresse(arr):
uniq = trié(set(arr))
retour uniq

def maxRectangle Zone(xCoord, yCoord):
n = len(xCoord)
ys = compresse(yCoord)
pts = [(xCoord[i], bisect_left(ys, yCoord[i])) pour i dans l'intervalle(n)]
pts.sort() # lexicographie

ft = Fenwick(len(ys))
entre_cnt = {}
prev_x = {}
as = -1

pour i, (x, y) dans l'énumération(pts):
ft.add(y, 1 )
si i > 0 et pts[i][0]== pts[i-1][0]: # même ligne verticale
y1, y2 = trié((pts[i-1][1], y))
entre = ft.sum(y2 - 1) - ft.sum(y1)

clé = (y2 < < 32)
si la clé entre_cnt & #160;:
prev_entre = entre_cnt[key]
si entre == prev_entre + 2:
zone = (x - prev_x[key]) * (y[y2] - ys[y1])
si zone > ans: ans = zone
entre_cnt[key] = entre
prev_x[key] = x

retour et

♪ -------------------------------------------------------------------
si __nom__ == "__main__" :
# test local rapide
print(maxRectangleArea([1,1,2,3,4,4,5,5],[1,3,1,3,1,3,1,3])
«» "

> **Astuce:** Dans Python, le dictionnaire intégré est une carte de hachage, de sorte que le truc `key` fonctionne exactement comme dans Java.

---

C'est pas vrai.

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

// --------- Fenwick Tree --------
struct Fenwick {
vecteur <int> bit;
Fenwick(int n) : bit(n + 1, 0) {}
vide add(int idx, int delta) {
pour (int i = idx + 1; i < (int)bit.size(); i += et -i)
bit[i] += delta;
}
Int sum(int idx) const { // inclusivement
int s = 0;
pour (int i = idx + 1; i > 0; i -= i & -i)
s += bit[i];
retour s;
}
};

solution de classe {
public:
long maxRectangleZone(vecteur<int>& xCoord, vecteur <int>& yCoord) {
int n = xCoord.size();
vector<int> ys = compresse(yCoord); // compression de coordonnées
vecteur<pair<int,int>> pts(n); // {x, compressé y}
pour (int i = 0; i < n; ++i) {
int cy = lower_bound(ys.begin(), ys.end(), yCoord[i]) - ys.begin();
pts[i] = {xCoord[i], cy};
}

Tri(pts.begin(), pts.end(), [](auto &a, auto &b){
si (a.first != b.first) retourner a.first < b.first;
retour a.seconde < b.seconde;
});

Fenwick ft(ys.size());
sans ordre_map<long long,int> entreCnt; // clé = (yHigh<32)
non ordonné_map<long long,int> prevX; // précédent x pour la clé

long an = -1;
pour (size_t i = 0; i < pts.size(); ++i) {
int x = pts[i].
int y = pts[i].seconde;
ft.add(y, 1);

si (i > 0 && pts[i].first == pts[i-1].first) { // même ligne verticale
int y1 = pts[i-1].seconde, y2 = pts[i].seconde;
si (y1 > y2) swap(y1, y2); // moins en premier
Int entre = ft.sum(y2 - 1) - ft.sum(y1);

longue clé longue = ((long long)y2 << 32)
auto it = entreCnt.find(key);
si (it != entreCnt.end()) {
int prevBetween = it->seconde;
si (entre == prevBetween + 2) {
longue zone = 1LL * (x - prevX[key]) *
(y[y2] - ys[y1]);
ans = max(ans, surface);
}
}
entreCnt[key] = entre;
prevX[key] = x;
}
}
le retour des an;
}

particulier:
vecteur<int> compresse(vecteur<int>& a) {
vecteur<int> b = a;
tri(b.begin(), b.end());
b.erase(unique(b.begin(), b.end()), b.end());
retour b;
}
};
«» "

> **Note :**
> *`unordered_map<long long, int>`* fonctionne bien pour les entrées de 200k dans C++.
> *Tout arithmétique qui pourrait déborder 32-bit est fait avec "long long". *

---

La complexité

Opération Coût
- C'est quoi ?
(Traitement)
Points de tri **O(n log n)** Autres
**O(log n)** chaque → **O(nlog n)** total
HashMap amortisé
**Temps total****O(n log n)** (2 × 105 × log 2 × 105 3 × 106 opérations) Autres
**Espace**** **O(n)** pour les points, y-array, arbre de Fenwick, cartes de hachage

---

## #Les chutes

Erreur
- Oui.
**Utiliser `int` pour la zone**=La zone peut être jusqu'à (8·107)2 . Utilisez `long/long`. Autres
Autres **Les indices de Fenwick ne compresseraient pas jusqu'à 8·107 → mémoire. Autres
La requête "sum" de Fenwick doit être *exclusive* des deux coins rectangles. Utiliser `(yHigh-1)` correctement. Autres
**Dupliquer les valeurs de y**= Après compression, chaque indice de y est unique. La clé `(y2 << 32)= y1` ne garantit aucune collision. Autres
**Off‐by‐one dans Fenwick**= Fenwick est basé sur 1 interne; passez `idx+1`. Autres
**Trier la paire de y correctement** Sinon, la clé pourrait être incohérente. Autres

---

## Dernier départ

- Oui. La solution repose sur **traverser l'horizon**: chaque fois que vous terminez un segment vertical (deux points avec le même `x`), vous vérifiez si la même paire de valeurs y est apparue avant.
- Oui. Si c'est le cas, vous calculez la largeur du rectangle (courant `x` moins le `x` précédent) et vous vérifiez que le nombre de points strictement à l'intérieur est égal à `prevCnt + 2`.
Cela garantit qu'aucun point intermédiaire ne bloque le rectangle.
- L'arbre Fenwick nous permet de maintenir l'ensemble *current* de valeurs 'y` à chaque ligne verticale, nous donnant le nombre de points entre les deux coins efficacement.

---

Joyeux codage !

Ces implémentations sont prêtes à être collées dans LeetCode (ou n'importe quelle plateforme de concours de codage). Bonne chance !