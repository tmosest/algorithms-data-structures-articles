---
titre: LeetCode 391. Rectangle parfait -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
* 391. Rectangle parfait – LeetCode dur
**Objectif:**
Compte tenu d'une liste de rectangles alignés sur l'axe, déterminez s'ils forment ensemble **exactement un** grand rectangle (pas de trous, pas de chevauchements).

Langue Heure Espace
- C'est quoi ?
Java **O(n)**
Python **O(n)**
* * * * * * * *

---

Article sur le blog – Le bon, le mauvais, et le mauvais du rectangle parfait

> **Mots clés:** Perfect Rectangle LeetCode, algorithme, Solution Java, solution Python, solution C++, question d'entretien, jeu de hachage, contrôle de zone, entretien d'emploi.

C'est pas vrai. Quel est le problème du rectangle parfait?

Imaginez que vous ayez un ensemble de petits rectangles placés sur un plan 2-D.
Vous avez demandé : **Couvrent-ils un rectangle unique sans trous ni chevauchements? * *

Question typique d'entrevue qui teste:
- **Perspective géométrique**
- **Hashing / Set d'utilisation**
- **Comptabilité de la masse et de la zone**

La solution classique O(n)

L'astuce est de combiner deux observations simples:

Observation Pourquoi ça compte
C'est-à-dire
La somme de tous les petits rectangles doit correspondre à la superficie du rectangle externe. Autres
**Vérification de l'entreprise** Dans une couverture parfaite chaque coin intérieur apparaît *un nombre pair de fois*; seuls les 4 coins extérieurs apparaissent *exactement une fois*. Autres

Étapes

1. **Fixer les limites extérieures**
`minX`, `minY`, `maxX`, `maxY` – le plus petit rectangle qui pourrait contenir tous les autres.

2. **Sommaires**
< TotalArea = < < (ai − xi) > > * (bi − yi) "

3. **Maintenir un ensemble de coins**
Pour chaque rectangle pousser ses 4 coins dans un `HashSet`.
S'il existe déjà un coin, retirez-le – cela ne permet de conserver que les coins *odd-fréquence*.

4. **Après traitement de tous les rectangles**
* L'ensemble doit contenir **exactement quatre coins**.
* Ces quatre coins doivent être `(minX, minY)`, `(minX, maxY)`, `(maxX, minY)`, `(maxX, maxY)`.
* La «zone totale» doit être égale à «(maxX - minX) * (maxY - minY)».

Si les trois conditions sont remplies → **true**; sinon **faux**.

> **Pourquoi ça marche ? **
> Tout coin interne (partagé par 2 ou 4 rectangles) est ajouté et supprimé un nombre pair de fois → disparaît de l'ensemble. Seuls les coins extérieurs du rectangle survivent.

C'est vrai. Les bonnes

Description
C'est pas vrai.
**Temps linéaire**= Chaque rectangle est traité une fois. Autres
**Réservé à la mémoire faible**. Autres
**Déterministe**= Pas de hasard ou de récursion – idéal pour la clarté de l'entrevue. Autres
**Extensible**= Fonctionne pour tout rectangle aligné sur l'axe. Autres

C'est pas vrai. Les mauvais

Pourquoi c'est une douleur
- Oui.
**Les grandes coordonnées**= Besoin de `long`/`int64` pour éviter les débordements dans la zone informatique. Autres
**HashSet au-dessus de l'écran** Autres
**Suppose que l'entrée est correcte. Autres

C'est vrai. L'Ugly

Boîtes de bord Comment manipuler
- C'est quoi ?
**Couvertures déconnectées multiples**Le jeu d'angles aurait >4 coins – pris par le jeu de contrôle. Autres
**Tiny rectangle se chevauche** Autres
**Coordonnées négatives**=Tenue toujours; il suffit de garder la logique min/max. Autres

---

Pourquoi tu devrais maîtriser ce problème

- **Interview Gold‐mine** – C'est une question classique sur le LeetCode et de nombreuses piles d'entretien d'entreprise.
- **Showcase of Thinking** – Démontre que vous pouvez réduire un problème de couverture 2-D aux opérations d'algèbre et de set.
- **Codage** – Propre, autonome et facilement expliqué en 5-10 minutes.

---

Les solutions de code

Ci-dessous sont des implémentations épurées et entièrement commentées dans **Java, Python et C++**. Chacun suit l'algorithme exact décrit.

---

C'est pas vrai. Java

"Java
Importer java.util. HashSet;
Importer java.util. Jeu;

***
* LeetCode 391 - Rectangle parfait
* Heure: O(n)
* Espace: O(n) – ensemble de coins
*/
solution de classe publique {
// Classe d'aide pour représenter un point (x, y)
classe statique privée Point {
à x, y;
Point(int x, int y) { this.x = x; this.y = y; }

@Override
booléen public est égal(Object o) {
si (celui-ci) est vrai;
si (!o exemple de point)) retourner faux;
Point p = (point) o;
retour x == p.x && y == p.y;
}

@Override
code hash() public
retour 31 * x + y;
}
}

booléen public estRectangleCover(int[][] rectangles) {
// Coordonnées du rectangle
int minX = entier.MAX_VALUE, minY = entier.MAX_VALUE;
int maxX = entier.MIN_VALUE, maxY = entier.MIN_VALUE;

longue zone totale = 0; // Utilisez longtemps pour éviter le débordement
Définir <Point> cornerSet = nouveau HashSet<>();

pour (int[] rect : rectangles) {
int x1 = rect[0], y1 = rect[1];
int x2 = rect[2], y2 = rect[3];

// Mettre à jour les limites
minX = Math.min(minX, x1);
minY = Math.min(minY, y1);
maxX = Math.max(maxX, x2);
maxY = Math.max(maxY, y2);

// Zone d'accumulation
Zone totale += (long)(x2 - x1) * (y2 - y1);

// Traiter quatre coins
Coins point[] = {
nouveau point(x1, y1),
nouveau point(x1, y2),
nouveau point(x2, y1),
nouveau point(x2, y2)
};

pour (Point p : coins) {
si (!cornerSet.add(p)) { // déjà présent -> supprimer
coinSet.supprimer(p);
}
}
}

// Après traitement de tous les rectangles
si (cornerSet.size() != 4) retourner faux;

// Ces quatre coins doivent correspondre aux coins rectangles
si (!cornerSet.contient(nouveau point(minX, minY))) retourner faux;
si (!cornerSet.contient(nouveau point(minX, maxY))) retourner faux;
si (!cornerSet.contient(nouveau point(maxX, minY))) retourner faux;
si (!cornerSet.contient(nouveau point(maxX, maxY))) retourner faux;

// Contrôle de zone
longue zone attendue = (long)(maxX - minX) * (maxY - minY);
retour total Zone == zone prévue;
}
}
«» "

---

# # # # # #

'`python
de taper la liste d'importation, Tuple, Set

Solution de classe:
def isRectangle Couverture(self, rectangles: List[List[int]]) -> bool:
# Boîte forte
min_x, min_y = flotteur('inf'), flotteur('inf')
max_x, max_y = flotteur('-inf'), flotteur('-inf')

surface = 0
coins: Set[Tuple[int, int]] = set()

pour x1, y1, x2, y2 en rectangles:
min_x, min_y = min(min_x, x1), min(min_y, y1)
max_x, max_y = max(max_x, x2), max(max_y, y2)
surface += (x2 - x1) * (y2 - y1)

Quatre coins du rectangle
pour coin dans ((x1, y1), (x1, y2), (x2, y1), (x2, y2)):
Si coin dans les coins:
coins.supprimer
Sinon:
coins.add(corner)

Après tous les rectangles traités
si len(corners) != 4 :
Retour Faux

wond_corners = {(min_x, min_y), (min_x, max_y),
(max_x, min_y), (max_x, max_y)}

Si les coins != _corners attendus :
Retour Faux

Zone de retour == (max_x - min_x) * (max_y - min_y)
«» "

---

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
bool isRectangleCover(vecteur<vecteur<int>>& rectangles) {
longue surface = 0;
long minX = LLONG_MAX, minY = LLONG_MAX;
long maxX = LLONG_MIN, maxY = LLONG_MIN;

// Ensemble de points d'angle représentés par la paire<int,int>
unordered_set<long long> corners; // utiliser le hachage

encode automatique = [](int x, int y) -> long {
// Emballage 32 bits (usines pour coordonnées à +/-1e5)
retour (long) (x + 100000) << 32) (int non signé) (y + 100000);
};

pour (auto &r : rectangles) {
int x1 = r[0], y1 = r[1];
int x2 = r[2], y2 = r[3];

minX = min(minX, (long)x1);
minY = min(minY, (long)y1);
maxX = max(maxX, long)x2;
maxY = max(maxY, long)y2;

surface += (long) (x2 - x1) * (y2 - y1);

vector<pair<int,int>> pts = {{x1,y1},{x1,y2},{x2,y1},{x2,y2}};
pour (auto &p : pts) {
longue clé longue = encode(p.first, p.second);
si (!corners.insert(key).seconde) { // déjà présent -> supprimer
coins.erase(clé);
}
}
}

si (corners.size() != 4) retourner faux;

vecteur<pair<long long,long long>> attendu = {
{minX, minY}, {minX, maxY},
{maxX, minY}, {maxX, maxY}
};
pour (auto &e : attendu) {
si (!corners.count(encode(int)e.first, (int)e.second)) retourner faux;
}

longue durée attendueZone = (max.X - min.X) * (max.Y - min.Y);
zone de retour Zone;
}
};
«» "

> **Note sur l'encodage C++ –
> L'utilisation d'un entier 64 bits pour emballer deux coordonnées 32 bits évite la nécessité d'une structure de hachage personnalisée.
> Pour le problème des contraintes ( `=coordonné== ≤ 1e5`) le déplacement de 32 bits est sûr.

---

Les pensées finales

- **Time & Space** – Linéaire et faible; parfait pour une entrevue de codage.
- **Key Insight** – Réduisez le problème de couverture 2-D en *parité de corner* + *égalité de zone*.
- **Quoi mettre en lumière dans une entrevue** –
- Pourquoi le coin se termine avec exactement quatre coins.
- Pourquoi les captures de contrôle de zone Ohio et les scénarios d'overlap.
- Manipulation de cas de bord (coordonnées négatives, grande entrée).

Autres Maîtriser cette question vous donne une base solide dans les problèmes de hachage géométrique, un thème d'interview commun dans les entreprises de haute technologie.

Bon codage, et que votre couverture soit parfaite! C'est ce qu'il a dit